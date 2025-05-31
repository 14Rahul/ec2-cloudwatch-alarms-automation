# AWS EC2 CloudWatch Alarms Automation with SSM

Automate the installation of the CloudWatch Agent and management of CPU, Memory, and Disk usage alarms on your EC2 instances using AWS Systems Manager (SSM).

---

## 🚀 Overview

Managing CloudWatch alarms manually for EC2 instances can be tedious and error-prone, especially when dealing with dynamic infrastructure. This automation:

- Installs the CloudWatch Agent on tagged EC2 instances
- Creates and updates alarms for CPU, Memory, and Disk utilization
- Deletes alarms for terminated instances to save cost
- Supports scheduling via SSM State Manager or triggering via EventBridge
- Works based on instance tags (`AutoAlarm=True`)

---

## ⚙️ Features

- Automatic CloudWatch Agent installation
- Creation of metric alarms with customizable thresholds
- Alarm updates on instance type changes
- Cleanup of alarms for deleted instances
- Supports SNS topic notifications (optional)

---

## 📋 Prerequisites

- AWS CLI or AWS Console access
- IAM Role with permissions:
  - `AmazonEC2FullAccess`
  - `AmazonSSMFullAccess`
  - `CloudWatchFullAccessV2`
- EC2 instances tagged with: `AutoAlarm=True`
- SSM Agent installed and running on EC2 instances (default on most Amazon Linux / Windows AMIs)

---

## 🔧 Setup Instructions

1. **Create SSM Parameter for CloudWatch Agent Config**

   Create an SSM Parameter named `AmazonCloudWatch-cw-agent-config` with your preferred memory and disk paths for monitoring.

2. **Create IAM Role**

   Create an IAM Role for automation with the above-mentioned policies and configure it as the `AutomationAssumeRole` in the runbook.

3. **Create SSM Automation Document**

   Use the provided YAML automation document to create a new automation runbook in AWS Systems Manager.

4. **Schedule the Automation**

   Use AWS Systems Manager State Manager to schedule the automation on a daily or hourly basis, targeting EC2 instances tagged with `AutoAlarm=True`.

---

## 📂 Repository Contents

- `automation-runbook.yaml`: Full SSM automation document YAML for CloudWatch Agent installation and alarm management.
- `cloudwatch-agent-config.json`: Sample CloudWatch Agent configuration for monitoring memory and disk.
- `README.md`: This documentation file.

---

## 📈 Usage

- Tag your EC2 instances with `AutoAlarm=True`.
- Ensure the IAM role is properly attached.
- Schedule or trigger the automation to install the agent and configure alarms automatically.
- Monitor alarms via CloudWatch and receive notifications if configured.

---

## 💡 Notes

- Alarm names are generated in the format:  
  `{Instance Name} {Metric Name} {Threshold}% Utilization`
- Existing alarms not matching this format will not be updated, and new alarms will be created instead.
- Always test automation in a development environment before applying to production.

---

## 🙌 Contributing

Contributions, improvements, and bug reports are welcome! Feel free to open issues or submit pull requests.

---

## 📞 Contact

For questions or support, please open an issue in this repository.

---

## License

MIT License © 2025 Prodigees

