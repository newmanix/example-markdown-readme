# 🛠️ System Log Triage & Assignment Tool (`triage-log-processor.sh`)

## Project Overview

This is a robust Bash script designed for system administrators and DevOps teams to rapidly triage and categorize system log errors (`app_output.log`) into actionable assignments. It uses a chain of standard Linux text processing tools (`sed`, `sort`, `tee`) to transform raw log data into a clean, prioritized list of tickets, assigning responsibility based on keyword (e.g., `ERROR`, `DEBUG`, `INFO`).

This project serves as a comprehensive demonstration of advanced pattern matching, data piping, and bulk text substitution using Extended Regular Expressions in a professional Linux environment.

### 🔑 Key Features

  * **Bulk Triage:** Processes thousands of lines of log data in seconds.
  * **Role Assignment:** Automatically substitutes generic keywords with specific owner IDs (`INFO` -> `INFO-spock`).
  * **Case Insensitive:** Searches and substitutes keywords regardless of case (e.g., `info`, `Info`, `INFO`).
  * **Sorted Output:** Prioritizes output by sorting the generated assignments file.
  * **Non-Destructive:** Outputs assignments to a new file (`assignments.txt`) while preserving the original log file.

-----

## 🔍 Case Study: The Problem & The Solution

### Background

During peak traffic events, our application server generates log files that can exceed 1GB per hour. The volume of noise makes it impossible for the Human Triage Team to manually identify and prioritize critical issues (like `ERROR` and `FAILURE`) from standard noise (like `INFO` and `DEBUG`).

### The Problem

The team needed an automated way to:

1.  Isolate all severity levels.
2.  Assign a specific engineer to each severity level (e.g., Spock handles all `INFO` messages).
3.  Generate a clean, sorted ticket list for immediate action.

### The Solution

The `triage-log-processor.sh` script executes a highly efficient pipeline to perform five separate case-insensitive substitution passes (for `INFO`, `DEBUG`, `ERROR`, `FAILURE`, and `WARN`) on the raw log file. This single execution transforms the log into a categorized list, which is then sorted and saved to a dedicated assignment file. This reduced log analysis time from hours to under 30 seconds.

-----

## ⚙️ Usage

### Prerequisites

A Linux environment (Bash shell) with standard utilities (`sed`, `sort`, `tee`).

### 1\. Script Execution

Run the script, passing the target log file as the first argument:

```bash
./triage-log-processor.sh app_output.log

### 2\. The Core Command Pipeline (For reference)

The script uses a multi-line, copy-paste-safe structure for readability:

```bash
sed -E \
  -e 's/info/INFO-spock/gi' \
  -e 's/debug/DEBUG-kirk/gi' \
  -e 's/error/ERROR-mccoy/gi' \
  -e 's/failure/FAILURE-scotty/gi' \
  -e 's/warn/WARN-uhura/gi' \
  "$1" | sort | tee assignments.txt

*The use of `-e` for each substitution ensures clean execution across terminals.*

### 3\. Reviewing Output

The resulting `assignments.txt` file is automatically sorted alphabetically, making immediate prioritization simple:

```text
DEBUG-kirk: Database connection successful (Line 4)
DEBUG-kirk: User login successful (Line 5)
ERROR-mccoy: Resource not found (Line 1)
FAILURE-scotty: System crash detected (Line 3)
INFO-spock: Health check running (Line 2)

-----

## 🤝 Attribution and Professional Disclosure

### Base Repository/Code Reference

This project was based on initial concepts and structures derived from the "Linux Text Processing Tools" module at North Seattle College (IT135). The core concepts for pipeline design are adapted from [link to a specific external tutorial or resource if applicable].

### AI/Chatbot Assistance Policy

In line with academic integrity and modern development practices, I utilized Google's Gemini large language model (LLM) for the following purposes:

1.  **Syntax Debugging:** Correcting the initial `sed` multi-command syntax (e.g., moving from chained `-E` flags to chained `;` or multiple `-e` flags).
2.  **Code Review:** Verifying best practices for shell variable usage and quoting.
3.  **Documentation Drafting:** Structuring and refining the language used in this `README.md` and the initial project overview.

No copyrighted code was used, and the final script logic was engineered and tested independently.

-----

## 👤 Author

  * **[Your Name Here]**
  * **[Your LinkedIn or Portfolio Link]**
  * **[Your Email]**
