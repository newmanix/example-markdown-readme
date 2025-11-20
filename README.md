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
