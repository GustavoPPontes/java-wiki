# Terminal

## What's a Terminal?
Early known as "dumb terminals" in the 70s and 80s, the device consisted of a display monitor and keyboard that lacked computational power. It was merely connected to a server and displayed on its screen everything the developer sent through commands typed on the keyboard. Just that.

Nowadays, terminal refers to a software (called **Command-Line Interface**, or **CLI**) that emulates a terminal on our own computer, typing text comands instead of visual interfaces.

Technically, the **terminal** is the program that provides a text window, showing what you type and the responses to your commands. What really does the work is its 'brain', called the **Shell**. The shell reads your input, analyzes the command, interacts with the operating system, and sends the response back to the terminal.

So we can "interact" with our own PC (Personal Computer) instead of a real server. Although it is still used today by large companies to manage large servers.

## Advantages of using Terminal
The reason why it is still used today is as follows:
- **Servers:** Many mainframes (servers) that host websites and systems do not have a visual interface, being controlled exclusively by text.
- **Speed:** Executing actions through the terminal uses fewer computer resources than loading images, menus, and visual buttons (Graphical User Interface - GUI).
- **Automation:** It is possible to create small programs, called scripts, so that the computer does repetitive tasks automatically.
- **Software Development:** Many of the commands that the programmers use nowadays to install, manage and test their programs/tools are used in terminals.

## PowerShell vs CMD (Windows)

On Windows, the two most common shells are **Command Prompt (CMD)** and **PowerShell**.

**CMD** is the older one. It has been around since the early versions of Windows and is based on simple text commands (like `dir`, `copy`, `cd`). It works well for basic tasks, such as navigating folders, running simple scripts (`.bat` files), and troubleshooting small issues. However, it is limited when compared to modern needs.

**PowerShell**, on the other hand, is more modern and much more powerful. It was created by Microsoft to improve automation and system administration. Unlike CMD, PowerShell works with **objects instead of plain text**, which makes it more structured and powerful for scripting. It uses commands called **cmdlets** (like `Get-Process`, `Set-Location`, etc.) and allows deeper interaction with the Windows system, services, registry, cloud platforms (like Azure), and more.

In the IT and Back-End job market in 2026, **PowerShell is much more relevant**. It is widely used for:
- Automation of system administration tasks  
- DevOps processes and CI/CD pipelines  
- Managing Windows Servers and cloud environments  
- Writing advanced deployment and maintenance scripts  

CMD is still available and sometimes used for legacy systems or very simple commands, but in professional environments, **PowerShell is the standard choice** on Windows.