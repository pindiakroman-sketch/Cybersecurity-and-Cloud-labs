# My TryHackMe Lab: Windows PowerShell Fundamentals

This repository contains my practical notes and hands-on exercises from the TryHackMe "Windows PowerShell" room. After completing the basic Windows CMD module, I advanced to PowerShell to understand object-oriented administration, remote task execution, and basic filtering techniques.

---

## 📋 Core Concepts Learned

Unlike the traditional Windows Command Line (CMD), which handles data purely as text, PowerShell is developed using an **object-oriented** approach. This means commands pass structured objects containing rich properties down the pipeline, making management and automation much more efficient.

---

## 🛠️ Practical Scenarios & Lab Exercises

### Scenario 1: Discovery & Exploring Commands (Task 2)
I practiced how to find hidden capabilities and look up help manuals within the shell environment.

* **Finding Commands by Verb:** To look up all available commands that start with a specific action like `Remove`, I used wildcards (`*`):
  ```powershell
  Get-Command Remove*
  ```
* **Reading Command Examples:** Instead of reading the whole manual, I requested only practical usage examples for the user creation tool:
  ```powershell
  Get-Help New-LocalUser -Examples
  ```
* **Checking Aliases (Shortcuts):** I discovered that Linux/CMD shortcuts are mapped to PowerShell under the hood. For example, checking what `echo` actually triggers:
  ```powershell
  Get-Alias echo
  :: Výstup mi ukázal, že pod kapotou sa spustí oficiálny príkaz Write-Output
  ```

### Scenario 2: Data Filtering with `Where-Object` (Task 5)
I practiced how to filter outputs based on specific criteria. I learned to stick to the standard built-in parameters rather than overcomplicating the syntax.

* **Task:** Find all files in the directory that are larger than 100 bytes.
* **Command Syntax:**
  ```powershell
  Get-ChildItem | Where-Object -Property Length -gt 100
  ```
  *Note for my future self:* `Length` means size in bytes, and `-gt` stands for "Greater Than" (väčší ako).

### Scenario 3: Real-Time Network & Process Mapping
I learned how security analysts link active network connections to the actual programs running them on the machine.

* **Command Used:** `Get-NetTCPConnection`
* **Key Discovery:** While the terminal screen displays the short label **`PID`** in the column header for human readability, the true underlying system property is called **`OwningProcess`**. Knowing this property name is essential for writing accurate filtering skripts.

### Scenario 4: The Pirate's Motto (Incident Response Challenge)
A practical troubleshooting challenge where a user profile was modified to mess with a system service. I resolved it using a two-step investigative process:

1. **Step 1 (Find the Clue):** Inspect the suspicious user profile description to extract their secret motto.
   ```powershell
   Get-LocalUser -Name p1r4t3 | Select-Object -Property Description
   :: Tento príkaz mi na obrazovke odhalil motto: "A merry life and a short one."
   ```
2. **Step 2 (Find the Target Service):** Search the system services to isolate which one was altered to match that exact motto.
   ```powershell
   Get-Service | Where-Object -Property DisplayName -eq "A merry life and a short one."
   ```
   *Result:* Discovered that the true underlying system name of the affected service was **`p1r4t3-s-compass`**.

### Scenario 5: Windows Remoting (Executing Tasks on Distance)
I learned that a junior technician does not need to walk to every machine physically. We can use remoting tools to check configurations from our desk.

* **Task:** Run a service check on a remote machine named `RoyalFortune` without using quotes or credentials.
* **Command Syntax:**
  ```powershell
  Invoke-Command -ComputerName RoyalFortune -ScriptBlock {Get-Service}
  ```
  *Note for my future self:* `Invoke-Object` sends the request, and the curly brackets `{}` wrap the block of code we want to run on the other side.

---

## 📊 Summary Table of Key Operators & Commands

| Cmdlet / Element | What it means in plain English | My Slovak Notes (Pre mňa) |
| :--- | :--- | :--- |
| `Get-Command` | Lists or searches for available tools. | Hľadá príkazy v systéme. |
| `Get-Help` | Opens the manual for a specific command. | Otvorí nápovedu a návod. |
| `Where-Object` | Filters data streaming through a pipe. | Filter, ktorým vyberám len to, čo ma zaujíma. |
| `-gt` | Greater Than (Mathematical `>`). | Operátor "väčší ako". |
| `-eq` | Equals (Mathematical `=`). | Operátor "rovná sa" (presná zhoda). |
| `OwningProcess` | The official name for a Process ID (PID) in network tables. | Skutočný názov vlastnosti pre stĺpec PID. |
| `Invoke-Command` | Runs a script or command on a remote target. | Spustí príkaz na úplne inom počítači v sieti. |

---
*Learning Milestone Progress: Moved from purely theoretical knowledge to hands-on command application via TryHackMe.*
