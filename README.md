# OpenSSH Controller for Windows (Dev-C++ Edition)

##  Overview

This repository hosts a lightweight, secure, and Windows-native OpenSSH controller application developed using **Dev-C++**, following **Microsoft's Windows Development Guidelines**. The project aims to bridge the usability of SSH on Windows systems while retaining full control over the source and build process.

This controller supports launching OpenSSH sessions via native Windows APIs, manages basic SSH connection parameters, integrates a minimal resource UI (via `.rc` scripts), and ensures compatibility with Windows 10, 11, and Server editions. While not a full SSH stack reimplementation, it offers a modular controller for OpenSSH invocation and configuration.

---

##  Project Structure

```
OpenSSH_Controller_Project/
├── .vscode/                  # VSCode environment settings (optional)
├── main.cpp                  # Core source code for controller logic
├── OpenSSH.dev               # Dev-C++ project descriptor
├── OpenSSH.exe               # Compiled SSH controller binary
├── OpenSSH_private.h         # Custom header with macro/constant definitions
├── OpenSSH_private.rc        # Resource file for icons, metadata, and versioning
├── OpenSSH_private.res       # Compiled Windows resources
├── resource.h                # Resource ID declarations
├── resource.rc               # Icon and metadata definitions
├── myicon.ico                # Application icon
├── sop.html / sop.pdf        # SSH usage SOP for Win11 terminals
├── sshpicture.txt            # ASCII banner or connection metadata
```

---

##  Build Instructions

### Requirements

* Windows 10, 11, or Server 2019+
* [Dev-C++ 5.11](https://sourceforge.net/projects/orwelldevcpp/) with TDM-GCC compiler
* Optional: [OpenSSL for Windows](https://slproweb.com/products/Win32OpenSSL.html) if encryption libraries are needed
* Windows SDK preinstalled (for headers like `winsock2.h` and `wincrypt.h`)

###  Compilation Steps

1. Launch Dev-C++ and open `OpenSSH.dev`
2. Navigate to **Project > Project Options > Parameters**
3. Add required linker flags:

   ```bash
   -lws2_32 -mwindows
   ```

   *(Append `-lssl -lcrypto` for OpenSSL integration)*
4. Click **F11** to build and execute

###  Notes

* Ensure `myicon.ico` is available during compilation
* Resource scripts must be compiled before linking if modified
* Always run Dev-C++ as Administrator when working in `Program Files`

---

##  Microsoft Windows Compliance

This project was designed with full compliance to Microsoft Windows guidelines for native applications:

| Compliance Category  | Details                                                               |
| -------------------- | --------------------------------------------------------------------- |
|  File Paths         | Unicode-compliant paths, support for `%APPDATA%`, `%LOCALAPPDATA%`    |
|  Registry Access    | Optional configuration keys can be stored in `HKCU\Software\OpenSSH`  |
|  Windows API        | Uses `WinSock2`, `Crypt32`, `ShellExecuteW`, `GetUserNameW`           |
|  Resource Usage     | Implements `.rc` for icons, versioning, manifest (UAC ready)          |
|  Privilege Handling | Supports user-mode execution and optional elevation via UAC prompt    |
|  Console Support    | UTF-8 compliant console output, `SetConsoleOutputCP(CP_UTF8)` applied |

---

##  Features

* Custom launcher for SSH sessions via native `ssh.exe`
* Windows-native implementation in ANSI C++
* Minimal graphical integration using Windows `.rc` and icon files
* Clean separation between logic and UI metadata
* SOP documents available in both PDF and HTML formats for end users
* Designed for network admins and sysadmins on Windows-only environments

---

##  Developer Notes

### Header Highlights (`OpenSSH_private.h`):

* Macro definitions for buffer sizes
* Path constants for SSH binary
* Command templates for automatic host connection

### Icon/Resource Usage

* Project embeds icons and version metadata through `resource.rc`
* Can be extended to support multilingual `StringTable`

### Potential Additions

* PowerShell integration layer
* WinForms-based GUI wrapper
* Background process service registration (via Windows Task Scheduler or SCM)

---

##  Roadmap (Planned Development Phases)

| Stage | Feature / Goal                    | Description                                                                       |
| ----- | --------------------------------- | --------------------------------------------------------------------------------- |
| 1     | Dev-C++ Integration               | Ensure compatibility with legacy IDE for educational and lightweight builds       |
| 2     | Console-based SSH Launcher        | Launch `ssh.exe` with parameters using `CreateProcessW` and `ShellExecute`        |
| 3     | Windows Icon & Manifest Embedding | Include UAC awareness, versioning, and branding in `.rc` files                    |
| 4     | C++ GUI Frontend                  | Build a lightweight Win32 GUI using pure API calls or integrate Qt for modern UI  |
| 5     | Session Logger                    | Log each SSH session's start/end time, username, target IP, return codes          |
| 6     | SSH Key Generator                 | Use `CryptGenKey` or `NCryptCreatePersistedKey` to generate RSA/ED25519 key pairs |
| 7     | Key Storage Management            | Encrypt private keys using DPAPI (`CryptProtectData`) and store in `%APPDATA%`    |
| 8     | Remote Config Fetch               | Load SSH connection profiles from an INI, JSON or remote config server            |
| 9     | Integration Tests                 | Automated CLI tests for connection handling, output capture, and error resilience |
| 10    | Portable Executable               | Build a fully portable version (single EXE + INI + icons), without installer      |
| 11    | Windows Installer                 | Create `.msi` or `.exe` installer with icon registration, registry keys, etc.     |
| 12    | Localized UI Support              | Add UTF-8 multilingual support using `StringTable` and Windows `LocaleNameToLCID` |
| 13    | Documentation Site                | Host user/developer documentation via GitHub Pages or mkdocs                      |

---

##  License

This project is licensed under the **MIT License**.

```
MIT License

Copyright (c) 2025

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software...
```

---

##  Credits

* [OpenSSH](https://www.openssh.com/) for foundational tools
* [Microsoft Developer Docs](https://learn.microsoft.com/) for Win32 API references
* [Dev-C++](https://sourceforge.net/projects/orwelldevcpp/) for IDE
* [OpenSSL](https://www.openssl.org/) (if used) for crypto libraries

---

> For any issues, bugs, or enhancement requests, please open an issue or submit a pull request. Contributions are welcome!
