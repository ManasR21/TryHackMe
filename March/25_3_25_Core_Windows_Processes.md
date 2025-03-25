**Core Windows Processes**

---



## Task 2: Task Manager
Task Manager is a built-in Windows tool that provides insights into running processes, system performance, and application usage. It is crucial for monitoring system activity and detecting suspicious behavior.

### Key Features:
- **Processes Tab**: Displays active processes and resource consumption.
- **Performance Tab**: Shows CPU, memory, disk, and network usage.
- **Details Tab**: Provides advanced details such as PID, status, and user account.
- **Startup Tab**: Manages programs that launch at startup.

---

## Task 3: System
The System process is a core component of Windows responsible for managing system-level operations. It interacts with hardware and software to ensure seamless functioning.

### Normal Behavior:
- Runs as SYSTEM user.
- Located at **C:\Windows\System32**.
- High CPU usage might indicate driver issues or malware activity.

---

## Task 4: smss.exe (Session Manager Subsystem)
The **Session Manager Subsystem (smss.exe)** initializes the system environment during boot.

### Normal Behavior:
- Runs once during startup.
- Located at **C:\Windows\System32**.
- Terminates after launching **wininit.exe** and **csrss.exe**.

### Unusual Behavior:
- Running after boot completion.
- Located outside **System32**.
- Multiple instances running simultaneously.

---

## Task 5: csrss.exe (Client Server Runtime Process)
**csrss.exe** is critical for Windows and manages graphical console windows and process creation/deletion.

### Normal Behavior:
- Two instances run: **Session 0 (PID 392)** and **Session 1 (PID 512)**.
- Parent process is **smss.exe**.
- Located at **C:\Windows\System32**.

### Unusual Behavior:
- Parent process other than **smss.exe**.
- Incorrect file path.
- Running under an unknown user account.

---

## Task 6: wininit.exe (Windows Initialization Process)
The **wininit.exe** process launches key system services like **services.exe**, **lsass.exe**, and **lsaiso.exe**.

### Normal Behavior:
- Runs as **SYSTEM**.
- Parent process is **smss.exe**.
- Located at **C:\Windows\System32**.

### Unusual Behavior:
- Incorrect file path.
- More than one instance.

---

## Task 7: services.exe (Service Control Manager)
The **Service Control Manager (SCM)** manages system services, loading them at boot.

### Normal Behavior:
- Located at **C:\Windows\System32**.
- Runs as **SYSTEM**.
- Parent process is **wininit.exe**.

### Unusual Behavior:
- Different parent process.
- Multiple running instances.

---

## Task 8: svchost.exe (Service Host)
**svchost.exe** is responsible for hosting and managing Windows services.

### Normal Behavior:
- Multiple instances run concurrently.
- Parent process is **services.exe**.
- Located at **C:\Windows\System32**.

### Unusual Behavior:
- Parent process other than **services.exe**.
- No **-k** parameter in the command line.
- Incorrect file path.

---

## Task 9: lsass.exe (Local Security Authority Subsystem Service)
**lsass.exe** enforces security policies, verifies login credentials, and manages authentication.

### Normal Behavior:
- Parent process is **wininit.exe**.
- Located at **C:\Windows\System32**.
- Runs as **SYSTEM**.

### Unusual Behavior:
- Incorrect parent process.
- Multiple instances.
- Located outside **System32**.

---

## Task 10: winlogon.exe (Windows Logon Process)
**winlogon.exe** manages user authentication and handles secure attention sequence (Ctrl+Alt+Del).

### Normal Behavior:
- Parent process is **smss.exe** (though smss.exe terminates).
- Located at **C:\Windows\System32**.
- Runs as **SYSTEM**.

### Unusual Behavior:
- Incorrect parent process.
- Located outside **System32**.
- Incorrect registry shell value (should be **explorer.exe**).

---

## Task 11: explorer.exe (Windows Explorer)
**explorer.exe** provides the graphical interface, including the desktop, taskbar, and file manager.

### Normal Behavior:
- Launched by **userinit.exe**, which exits after execution.
- Located at **C:\Windows**.
- Runs under the logged-in user.

### Unusual Behavior:
- Incorrect parent process.
- Located outside **C:\Windows**.
- Unexpected outbound TCP/IP connections.

---
