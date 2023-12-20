# OVERVIEW  
A path traversal attack, also referred to as directory traversal, is a type of security exploit that seeks to reach files and directories located outside the designated web root folder. By manipulating variables that reference files with sequences like "dot-dot-slash (../)" and its variations, or by utilizing absolute file paths, attackers may potentially gain unauthorized access to various files and directories. These could include sensitive data such as application source code, configuration files, or critical system files. It's important to note that the extent of file access is constrained by system operational access controls, such as locked or in-use files, particularly in the case of the Microsoft Windows operating system.

Commonly recognized by terms like "dot-dot-slash," "directory traversal," "directory climbing," and "backtracking," this type of attack exploits vulnerabilities in file path handling to navigate beyond the intended directory structure, posing a significant risk to the security of web applications.  

# HOW TO AVOID PATH TRANSVERSAL VULNERIBILTIES  
In the development of web applications, incorporating local resources like images, themes, and scripts is a common necessity. However, with each inclusion of a resource or file in the application, there exists a potential risk. Attackers may exploit vulnerabilities to include unauthorized files or remote resources, posing a threat to the application's security.  
## identifying if you are vulnerable  
- Ensure a clear understanding of how the operating system will handle filenames that are provided to it.
- Avoid placing sensitive configuration files within the web root directory.
- On Windows IIS servers, it's advisable not to have the web root located on the system disk to prevent potential recursive traversal into system directories.
## how to avoid  
- When making file system calls, it is recommended to minimize reliance on user input.
- Ensure that users cannot specify every part of the file path; instead, incorporate it within your own code for added security.
- Check if the user's input is valid by only accepting trusted information. Avoid trying to clean or modify the data.
- If you have to use information from users for working with files, make sure to organize or standardize it before using it in file operations.

## Example 1  
The examples below illustrate how the application handles the resources currently in use.  
- http://some_site.com.br/get-files.jsp?file=report.pdf  
- http://some_site.com.br/get-page.php?home=aaa.html  
- http://some_site.com.br/some-page.asp?page=index.html

In these instances, it's feasible to insert a harmful string as the variable parameter to potentially access files situated beyond the web publish directory.  
- http://some_site.com.br/get-files?file=../../../../some dir/some file  
- http://some_site.com.br/../../../../some dir/some file

On a Windows system, an attacker can only navigate within a partition where the web root is located, whereas on Linux, they have the ability to navigate throughout the entire disk.  

# ABSOLUTE PATH TRANSVERSAL  
The following URLs may be vulnerable to this attack:  
http://testsite.com/get.php?f=list  
http://testsite.com/get.cgi?f=2  
http://testsite.com/get.asp?f=test  

An attacker can execute this attack like this:  
http://testsite.com/get.php?f=/var/www/html/get.php  
http://testsite.com/get.cgi?f=/var/www/html/admin/get.inc  
http://testsite.com/get.asp?f=/etc/passwd  

When the web server provides error information in a web application, it becomes simpler for attackers to make educated guesses about the correct locations, such as the path to a file containing source code, which might then be revealed.  

# TOOLS USED FOR DIRECTORY TRANSVERSAL ATTACK  
- BURPSUITE
- OWASP ZAP
- DOTDOTPWN
- METASPLOIT
- DIRBUSTER

# how to fix this vulneribility  
Fixing a directory traversal vulnerability involves implementing secure coding practices and applying proper input validation. Here are some general steps to help address and mitigate directory traversal vulnerabilities:  


## Input Validation:

Implement strict input validation on all user-supplied input, especially parameters involving file paths. Ensure that input adheres to expected patterns and rejects any attempts at directory traversal.  

## Use Whitelists:

Create whitelists of allowed characters or patterns for file and directory names. Validate user input against these whitelists to prevent malicious characters or sequences.  

## Absolute File Paths:

Instead of relying on relative paths, use absolute file paths when including or accessing files. This helps to ensure that the file is retrieved from the intended location.  

## Limit File Access:  


Set up proper file access controls to restrict which files and directories the web server and application have permission to access. Avoid giving unnecessary permissions to files and directories.  

## Web Server Configuration:  


Configure the web server to run with the least privilege necessary. Ensure that the web server process has restricted access to sensitive files and directories.  

## Error Handling:  


Customize error messages to provide minimal information to attackers. Avoid disclosing specific details about file paths or the server's directory structure in error messages.  

## Use Security Libraries:  
Leverage security libraries or frameworks that offer built-in protection against directory traversal attacks. Many web development frameworks have security features that can help prevent such vulnerabilities.  

## CONCLUSION:  
Attackers can gain access to configuration files, user databases, and proprietary information, leading to breaches of privacy and data theft. Furthermore, this vulnerability can serve as a stepping stone for launching more sophisticated attacks, such as remote code execution.
