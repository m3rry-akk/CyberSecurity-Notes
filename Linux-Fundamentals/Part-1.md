# Linux Fundamentals Part 1 🐧

Welcome to my Linux Fundamentals Part 1 study notes. This module establishes the foundational mechanics required for system navigation, data retrieval, and command-line automation.

---

## 🐧 Introduction to the Linux Terminal

In enterprise and cybersecurity environments, operating systems like Ubuntu are often used without a **GUI (Graphical User Interface)** to keep the system lightweight and efficient. Instead, interaction with the OS is done entirely through the text-based **Terminal (CLI)**.

### 🔑 Essential Core Commands

Here are the first two fundamental commands used to interact with the Linux operating system:

| Command | Description | Example Usage |
| :--- | :--- | :--- |
| `echo` | Outputs/prints any text provided to the screen. | `echo "Hello Friend!"` |
| `whoami` | Displays the username of the currently logged-in session. | `whoami` |

### 💻 Command Examples & Syntax Rules

#### 1. The `echo` Command
The `echo` command is used to print text strings. 

* **Single Words:** Double quotes are **optional** for single-word arguments.
  ```bash
  tryhackme@linux1:~$ echo Hello
  Hello
