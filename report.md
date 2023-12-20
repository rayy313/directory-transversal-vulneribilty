# OVERVIEW  
A path traversal attack, also referred to as directory traversal, is a type of security exploit that seeks to reach files and directories located outside the designated web root folder. By manipulating variables that reference files with sequences like "dot-dot-slash (../)" and its variations, or by utilizing absolute file paths, attackers may potentially gain unauthorized access to various files and directories. These could include sensitive data such as application source code, configuration files, or critical system files. It's important to note that the extent of file access is constrained by system operational access controls, such as locked or in-use files, particularly in the case of the Microsoft Windows operating system.

Commonly recognized by terms like "dot-dot-slash," "directory traversal," "directory climbing," and "backtracking," this type of attack exploits vulnerabilities in file path handling to navigate beyond the intended directory structure, posing a significant risk to the security of web applications.  

# HOW TO AVOID PATH TRANSVERSAL VULNERIBILTIES  
In the development of web applications, incorporating local resources like images, themes, and scripts is a common necessity. However, with each inclusion of a resource or file in the application, there exists a potential risk. Attackers may exploit vulnerabilities to include unauthorized files or remote resources, posing a threat to the application's security.  
## Identifying if you are vulnerable  
- Ensure a clear understanding of how the operating system will handle filenames that are provided to it.
- Avoid placing sensitive configuration files within the web root directory.
- On Windows IIS servers, it's advisable not to have the web root located on the system disk to prevent potential recursive traversal into system directories.  
