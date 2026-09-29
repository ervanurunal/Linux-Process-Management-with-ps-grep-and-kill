## Linux Process Management with `ps`, `grep`, and `kill`

---

### Overview

In this lab, I practiced **monitoring and managing Linux processes** using the command line.

I learned how to:

* List running processes
* Filter processes using `grep`
* Identify Process IDs (PIDs)
* Terminate a specific process
* Find multiple processes using a keyword
* Terminate multiple processes
* Verify that processes have been stopped

Process management is an important IT Support and Linux administration skill because poorly behaving or unwanted processes can consume system resources and affect system performance.

---

### Tools & Resources

* Linux Virtual Machine (Qwiklabs)
* Linux Terminal / Shell
* `ps`
* `grep`
* `kill`
* `sudo`
* Process ID (PID)

### Lab Type: 
* Linux / IT Support Hands-On Lab

---

## 1. List Running Processes With `grep` 

* The `ps` command can be used to display information about running processes.

* The `grep` command can filter text from command output.

I can combine `ps` and `grep` using a pipe:

```bash
ps -aux | grep totally_not_malicious
```

The output may look similar to:

```text
root       315  0.0  0.0  7232  520 ?   S  15:29  0:00 sudo nohup bash /home/totally_not_malicious
root       320  0.0  0.1  3652  892 ?   S  15:29  0:00 bash /home/totally_not_malicious
student   5431  0.0  0.1  3084  880 pts/0 S+ 15:29  0:00 grep totally_not_malicious
```

The important number is the **PID**.

For example:

```text
315
320
```

These are the Process IDs of the two target processes.

![1](https://i.imgur.com/oJHyqQh.png)

---

## 2. Terminate a Specific Process

Linux uses the `kill` command to send a signal to a process.

The basic syntax is:

```bash
sudo kill [PROCESS_ID]
```

The processes in this lab are running as the `root` user.

A regular user may not have permission to terminate processes owned by another user.

Therefore, the lab uses:

```bash
sudo kill [PROCESS_ID]
```

![2](https://i.imgur.com/6y2aBWH.png)

---

## 3. Verify the Process Was Terminated

Run the original search again:

```bash
ps -aux | grep totally_not_malicious
```

![3](https://i.imgur.com/CvqNwBA.png)

After successfully terminating the target processes, the output should only show the `grep` process.

---

## 4. Find Multiple Processes

The lab also contains multiple processes with the word:

```text
razzle
```

Use:

```bash
ps -aux | grep razzle
```

Because `grep` searches for the specified text anywhere in the line, it can find multiple processes containing `razzle`.

![4](https://i.imgur.com/v2FLOnK.png)

---

## 5. Terminate Multiple Processes

Use the `kill` command for each process ID.

Example:

```bash
sudo kill 101
sudo kill 102
sudo kill 103
sudo kill 104
sudo kill 105
sudo kill 106
```

![5](https://i.imgur.com/QZjoUgt.png)

---

## 6. Verify Multiple Processes Were Terminated

Run:

```bash
ps -aux | grep razzle
```

If the target processes were successfully terminated, you should only see the `grep` process.

![5](https://i.imgur.com/QZjoUgt.png)

---

### Commands Learned

| Command                | Purpose                                              |
| ---------------------- | ---------------------------------------------------- |
| `ps`                   | Display information about running processes          |
| `ps -aux`              | Display detailed information about running processes |
| `grep`                 | Search/filter text                                   |
| `ps -aux | grep name`  | Find processes containing specific text              |
| `kill PID`             | Send a termination signal to a process               |
| `sudo kill PID`        | Terminate a process with elevated privileges         |
| `sudo`                 | Run a command with elevated permissions              |
| `\|`                   | Pipe output from one command into another            |

---

## Key Concepts

### Process

A **process** is a running instance of a program.

---

### Process ID (PID)

A **PID** is a unique number assigned to a running process.

---

### ps

The `ps` command provides information about running processes.

Basic example:

```bash
ps
```

More detailed example:

```bash
ps -aux
```

---

### grep

`grep` searches for text within command output or files.

Example:

```bash
ps -aux | grep ssh
```

---

### Pipe `|`

The pipe sends the output of one command to another command.

---

### kill

The `kill` command sends a signal to a process.

Example:

```bash
sudo kill 1234
```

The PID `1234` identifies the process that receives the signal.

---

## Cybersecurity Relevance

Linux process management is highly relevant to cybersecurity and SOC Analyst work.

Security analysts may investigate running processes to identify:

* Suspicious applications
* Malware
* Unauthorized processes
* Unexpected scripts
* Resource-intensive processes
* Processes running with elevated privileges
* Potentially compromised systems

For example, during an investigation, an analyst may use:

```bash
ps -aux
```

to inspect running processes and then use:

```bash
ps -aux | grep suspicious_name
```

to filter the results.

Understanding processes and PIDs provides a foundation for **Linux endpoint monitoring and incident response**.

---

## Troubleshooting Notes

### Too much output from ps

Instead of:

```bash
ps -aux
```

use:

```bash
ps -aux | grep process_name
```

This filters the output.

---

### Process not found

Check the process list:

```bash
ps -aux
```

Then search using a keyword:

```bash
ps -aux | grep keyword
```

---

### Permission denied

Try using `sudo`:

```bash
sudo kill [PROCESS_ID]
```

---

### grep appears in the results

This is normal.

For example:

```text
student  870 ... grep razzle
```

This is the `grep` command itself, not the target process.

---

### Need to find multiple processes

Use a partial keyword:

```bash
ps -aux | grep razzle
```

`grep` can find multiple lines containing the specified text.

---

###  Process Management Workflow

A basic Linux process-management workflow is:

```text
1. List processes
       ↓
2. Filter the process list
       ↓
3. Identify the PID
       ↓
4. Terminate the process
       ↓
5. Verify the process is gone
```

---

## Skills Demonstrated

**Technical Skills**

* Linux command line
* Linux process management
* `ps`
* `grep`
* `kill`
* `sudo`
* Process ID identification
* Command piping

**IT Support Skills**

* Process monitoring
* Troubleshooting running applications
* Identifying unwanted processes
* Terminating processes
* Linux system administration

**Cybersecurity Foundation**

* Linux endpoint monitoring
* Process analysis
* Suspicious process identification
* Privilege awareness
* Incident-response fundamentals

---

## Final Takeaway

This lab gave me hands-on experience managing **Linux processes from the command line**.

I learned how to use `ps` to view running processes, `grep` to filter process information, identify PIDs, use `kill` to terminate processes, and verify that processes were successfully stopped.

These skills provide a strong foundation for both **IT Support** and **Cybersecurity/SOC Analyst** roles.
