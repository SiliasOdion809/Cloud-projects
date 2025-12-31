---
title: "Automating System Monitoring with Bash Scripts and Cron Jobs"
seoTitle: "How to Automate Linux System Monitoring Using Bash Scripts and CronJob"
seoDescription: "Learn how to automate system monitoring on Linux using Bash scripting and cron jobs. This beginner-friendly project covers disk usage checks, memory monitor"
datePublished: Wed Dec 31 2025 10:32:12 GMT+0000 (Coordinated Universal Time)
cuid: cmjtvmyf9000202ky17ygg0ze
slug: automating-system-monitoring-with-bash-scripts-and-cron-jobs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1767173483231/356a47c7-9eb1-4b7d-a21c-2fb767f2e410.png
tags: linux, bash, devops, hashnode, cronjob, crontab, linux-for-beginners, bash-script, altschool-africa

---

# Linux Automation Made Easy with Bash Scripts and Cron Jobs

---

## A Beginner-Friendly Linux Automation Project (AltSchool Cloud Engineering)

---

## Introduction

As a beginner in **Linux system administration, Cloud computing, or DevOps**, learning how to automate routine tasks is a very important skill. Instead of manually checking system status every time, Linux allows us to write **Bash scripts** and schedule them to run automatically using **cron jobs**.

In this blog, I’ll walk you through a **simple but practical project** where we:

* Check disk usage on the `/home` directory
    
* Identify the **top 5 processes consuming memory**
    
* Save the results to a log file
    
* Automate the script to run **every 5 minutes** using cron
    

This project was completed as part of my **AltSchool Cloud Engineering Program (Second Semester – Month Two Assignment)**.

---

## Prerequisites

Before starting, you should have:

* A Linux-based system (Ubuntu, Debian, CentOS, etc.)
    
* Basic familiarity with the Linux terminal
    
* Permission to create and execute scripts
    
* Access to `cron` on your system
    

---

## Project Objective

The goal of this project is to **automate system monitoring** tasks that system administrators and cloud engineers frequently perform, such as:

* Monitoring disk usage
    
* Identifying memory-heavy processes
    
* Logging system information for future review
    

Automation helps reduce human error and ensures consistent system visibility.

---

## Step 1: Writing the Bash Script

### What the Script Does

The Bash script performs the following actions:

1. Checks the disk usage of the `/home` directory
    
2. Displays the top 5 processes consuming memory
    
3. Saves all output into a single log file
    
4. Prints a meaningful completion message
    

---

### Bash Script Code

```bash
#!/bin/bash

LOGFILE="/var/log/system_monitor.log"

echo "===== System Monitoring Log =====" >> $LOGFILE
echo "Date: $(date)" >> $LOGFILE

echo "" >> $LOGFILE
echo "Disk usage of /home:" >> $LOGFILE
du -sh /home >> $LOGFILE

echo "" >> $LOGFILE
echo "Top 5 memory-consuming processes:" >> $LOGFILE
ps aux --sort=-%mem | head -n 6 >> $LOGFILE

echo "" >> $LOGFILE
echo "Logging done successfully." >> $LOGFILE
echo "=================================" >> $LOGFILE
```

---

### 📸 Bash Script Screenshot

> ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1767173742908/1934a6bd-6dee-4ffa-8c17-aa9d53957ae7.png align="center")

---

## Step 2: Making the Script Executable

After saving the script, make it executable using:

```bash
chmod +x system_monitor.sh
```

This allows the script to be executed like a program.

---

## Step 3: Running the Script Manually

Before automation, it is good practice to test the script manually:

```bash
./system_monitor.sh
```

If successful, the log file will be created and updated with system information.

---

### 📸 Manual Script Execution

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1767174741209/25dd18f5-cc1b-4a79-aac1-df99c35664c0.png align="center")

---

## Step 4: Automating the Script Using Cron

### What Is a Cron Job?

A **cron job** is a Linux scheduler that allows tasks to run automatically at specified time intervals. It is widely used for backups, monitoring, and maintenance tasks.

---

### Editing the Crontab File

Open your crontab file with:

```bash
crontab -e
```

---

### Cron Job Configuration (Every 5 Minutes)

Add the following line:

```bash
*/5 * * * * /path/to/system_monitor.sh
```

This configuration ensures the script runs **every 5 minutes**, meeting the assignment requirement of running at least three times in 15 minutes.

---

### 📸 Cron Job Configuration

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1767175386998/656517cd-03ca-4706-8eb7-16bbe3c24b45.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1767175447973/061bfef9-f3e6-4fd0-aae5-041f8897863e.png align="center")

---

## Step 5: Verifying Cron Job Output

After waiting at least 15 minutes, check the log file to confirm multiple executions:

```bash
cat /var/log/system_monitor.log
```

You should see multiple timestamps indicating that the cron job executed successfully.

---

### 📸 Cron Job Log File Output

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1767175640285/22e79f21-1497-4d6b-beb9-615680788a00.png align="center")

---

## Common Issues and Troubleshooting

* Ensure absolute paths are used in cron jobs
    
* Confirm the script has execute permission
    
* Check cron service status if the job does not run
    

---

## Key Learnings from This Project

Through this project, I gained hands-on experience with:

* Bash scripting fundamentals
    
* Linux process and disk monitoring
    
* Task automation using cron jobs
    
* Log file management
    

These skills are essential for anyone pursuing a career in **Cloud Engineering or DevOps**.

---

## Conclusion

This beginner-friendly project demonstrates how powerful Linux automation can be when Bash scripting and cron jobs are combined. By automating system monitoring, we save time, improve reliability, and gain deeper insight into system behavior.

This assignment significantly strengthened my confidence in Linux administration and automation as part of my **AltSchool Cloud Engineering journey**.

---

### ✍️ Author

**Silias Odion Adodo**  
Cloud Engineering Student | Linux & DevOps Enthusiast  
AltSchool Africa