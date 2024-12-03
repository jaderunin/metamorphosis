# Description 
> McSkidy's fingers flew across the keyboard, her eyes narrowing at the suspicious website on her screen. She had seen dozens of malware campaigns like this. This time, the trail led straight to someone who went by the name "Glitch."
 "Too easy," she muttered with a smirk.
 "I still have time," she said, leaning closer to the screen. "Maybe there's more."
 Little did she know, beneath the surface lay something far more complex than a simple hacker's handle. This was just the beginning of a tangled web unravelling everything she thought she knew.

# Learning Objectives
- Learn how to investigate malicious link files.
- Learn about OPSEC and OPSEC mistakes.
- Understand how to track and attribute digital identities in cyber investigations.

# Notes
Risks provided by websites that convert youtube to mp3 include:
- Malvertising: Many sites contain malicious ads that can exploit vulnerabilities in a user's system, which could lead to infection.
- Phishing scams: Users can be tricked into providing personal or sensitive information via fake surveys or offers.
- Bundled malware: Some converters may come with malware, tricking users into unknowingly running it.
The file command in the terminal is used to determine and display the type of a file. It analyzes the file's content rather than relying solely on its extension, providing accurate information about its format and type.
By running it, we infer that the somg.mp3 file is actually an "MS Windows shortcut", also known as a .lnk file. This file type is used in Windows to link to another file, folder, or application. These shortcuts can also be used to run commands.
I then run exiftool for reading, editing, and managing metadata like the mp3 audio file we just downloaded.
After that, I scrolled down to the powershell command and here's what this PowerShell command does:

The -ep Bypass -nop flags disable PowerShell's usual restrictions, allowing scripts to run without interference from security settings or user profiles.
The DownloadFile method pulls a file (in this case, IS.ps1) from a remote server (https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1) and saves it in the C:\\ProgramData\\ directory on the target machine.
Once downloaded, the script is executed with PowerShell using the iex command, which triggers the downloaded s.ps1 file.
We then open the contents of the file where we see a script. The script is designed to collect highly sensitive information from the victim's system, such as cryptocurrency wallets and saved browser credentials, and send it to an attacker's remote server.
Once we see some content of the files, including the authors name, we look it up on github. If you look through the search results, you can be able infer the malicious actor's identity based on information on the project's page and the GitHub Issues section. Which then leads us to understand that this is a classic case of OPSEC. More about OPSEC below. 

# OPSEC 
OPSEC (Operations Security) is a risk management process designed to identify and protect sensitive information that adversaries could exploit. Originally developed for military use, it is now widely applied in business, cybersecurity, and personal privacy contexts.

## Key Components of OPSEC:
- Identification of Critical Information
- Threat Analysis
- Vulnerability Assessment
- Risk Assessment
- Implementation of Countermeasures

In the context of cyber security, when malicious actors fail to follow proper OPSEC practices, they might leave digital traces that can be pieced together to reveal their identity. Some common OPSEC mistakes include:
- Reusing usernames, email addresses, or account handles across multiple platforms. One might assume that anyone trying to cover their tracks would remove such obvious and incriminating information, but sometimes, it's due to vanity or simply forgetfulness.
- Using identifiable metadata in code, documents, or images, which may reveal personal information like device names, GPS coordinates, or timestamps.
- Posting publicly on forums or GitHub (Like in this current scenario) with details that tie back to their real identity or reveal their location or habits.
- Failing to use a VPN or proxy while conducting malicious activities allows law enforcement to track their real IP address.


