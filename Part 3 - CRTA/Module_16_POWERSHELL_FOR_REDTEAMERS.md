# ⚡ Module 16 – POWERSHELL FOR RED TEAMERS
<br>

> [!NOTE]
> **Module Overview:** PowerShell is one of the most powerful "Living off the Land" (LotL) tools available to a Red Teamer. Because it is built directly into Windows, executing attacks via PowerShell often avoids triggering traditional antivirus and EDR solutions. This module covers the foundational aspects of PowerShell necessary for Red Team operations.

---

## 💻 1. What is PowerShell?

PowerShell is a cross-platform task automation solution made up of a command-line shell, a scripting language, and a configuration management framework.

### Why Red Teamers Love PowerShell
*   **Built-in:** Available on almost all modern Windows systems by default.
*   **Deep Integration:** Full access to the .NET framework, WMI (Windows Management Instrumentation), and the Windows API.
*   **Fileless Malware:** Scripts can be executed directly in memory without touching the disk, making detection extremely difficult.

<details>
<summary><b>🛠️ The Power of Objects (Not Text)</b></summary>
<br>

Unlike bash (which outputs text strings), PowerShell outputs **objects**. This means you can directly access properties and methods of the output without needing complex `grep` or `awk` commands.

```powershell
# Example: Getting all running processes and filtering by name
Get-Process | Where-Object {$_.Name -eq "explorer"} | Select-Object Id, CPU
```
</details>

---

## 📝 2. PowerShell Editors

While you can type commands directly into the terminal, Red Teamers often need to write, modify, and obfuscate complex scripts (like `Invoke-Mimikatz.ps1` or PowerSploit modules).

| Editor | Use Case | Pros |
| :--- | :--- | :--- |
| **PowerShell ISE** | Built-in Windows IDE | Available by default, good for quick edits on compromised hosts. (Note: Deprecated by Microsoft). |
| **VS Code** | Primary Development | The standard for writing offensive tooling. Excellent syntax highlighting and debugging. |
| **Notepad/Vim** | Quick/Stealth Edits | Used when operating purely through a reverse shell or low-privileged terminal. |

---

## 🚀 3. Starting PowerShell in Windows

During an engagement, you might need to launch PowerShell under specific conditions, especially if you are trying to bypass Execution Policies or AMSI (Anti-Malware Scan Interface).

### Execution Policies
By default, Windows restricts running PowerShell scripts to prevent accidental execution of malicious code. Red Teamers must bypass this.

```powershell
# Check current policy
Get-ExecutionPolicy

# Bypass the policy for the current process (does not require Admin rights)
powershell.exe -ExecutionPolicy Bypass -File .\malicious_script.ps1
```

<details>
<summary><b>🕵️ Stealth Execution Techniques</b></summary>
<br>

When launching PowerShell payloads (e.g., via a malicious macro or a reverse shell payload), you want to hide the window and bypass profiles.

```powershell
# -NoP: NoProfile (speeds up load, ignores user profiles)
# -NonI: NonInteractive (doesn't prompt for input)
# -W Hidden: WindowStyle Hidden (hides the blue console window)
# -Enc: EncodedCommand (executes base64 encoded commands to evade simple string detection)

powershell.exe -NoP -NonI -W Hidden -Exec Bypass -Enc JABzAD0ATgBlAHcALQBPAGIAagBlAGMAdAAgAEkATwAuAE0AZQBtAG8AcgB5AFMAdAByAGUAYQBtACgAWwBDAG8AbgB2AGUAcgB0AF0AOgA6AEYAcgBvAG0AQgBhAHMAZQA2ADQAUwB0AHIAaQBuAGcAKAAiAEgA...
```
</details>

---

## 🐧 4. PowerShell in Linux (PowerShell Core)

PowerShell is no longer restricted to Windows. Attackers can use **PowerShell Core (pwsh)** on Linux (like Kali) to interact with compromised Windows machines using PowerShell Remoting (WinRM).

### Installing PowerShell on Kali Linux

```bash
# Update repositories and install powershell
sudo apt update
sudo apt install -y powershell

# Launch PowerShell from the bash terminal
pwsh
```

### Why Use `pwsh` on Kali?
*   **WinRM Connections:** Directly connect to a Windows target's PowerShell session from your Kali machine using `Enter-PSSession`.
*   **Offensive Tooling:** Run PowerSploit or Empire stagers locally to test them before deploying them to a target.

<details>
<summary><b>🔗 Example: Remote Connection from Linux to Windows</b></summary>
<br>

```powershell
# Connecting to a compromised Windows machine (10.0.0.5) from Kali
$cred = Get-Credential
Enter-PSSession -ComputerName 10.0.0.5 -Credential $cred -Authentication Negotiate
```
</details>

<br>
<p align="center"><i>End of Module 16</i></p>
