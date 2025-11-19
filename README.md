# Task 4: Basic Firewall Configuration and Testing (UFW)

## Task Objective
The objective was to configure and test basic firewall rules on a Linux system using **Uncomplicated Firewall (UFW)** to demonstrate the ability to control network traffic, enforce secure policies, and understand the filtering process.

##  Tool Used
* **UFW (Uncomplicated Firewall):** The command-line utility used to manage Netfilter rules on Linux.

## ⚙️ Configuration Summary

The task was executed on a Linux machine (e.g., Ubuntu) using the principle of **Default Deny**—blocking all incoming traffic unless explicitly allowed.

### 1. Default Policy Setup
| Command | Purpose |
| :--- | :--- |
| `sudo ufw default deny incoming` | **Blocked** all incoming connections by default (secure posture). |
| `sudo ufw default allow outgoing` | **Allowed** the system to make outgoing connections (e.g., browse the web). |
| `sudo ufw enable` | Activated the firewall. |

### 2. Rule Configuration and Testing

| Action Performed | Command | Observation / Test |
| **Block Rule (Telnet)** | `sudo ufw deny 23/tcp` | Tested with `nc -z -v 10.**.**.**`. The connection **failed**, confirming the rule's effectiveness. |
| **Allow Rule (SSH)** | `sudo ufw allow ssh` | Explicitly **allowed** inbound traffic on port 22 for secure remote management. |
| **Cleanup** | `sudo ufw delete [RULE NUMBER]` | Removed the temporary block rule after testing to maintain the final secure configuration (only SSH allowed). |

---

##  Firewall Filtering Summary

A firewall like UFW filters traffic based on a **Rule Chain** .

1.  **Ordered Processing:** Incoming packets are checked against the firewall's rules **sequentially** (top to bottom).
2.  **Match and Action:** The firewall applies the first rule that matches the packet's attributes (Source/Destination IP, Port, Protocol). The action is then taken (**ALLOW**, **DENY**, or **DROP**).
3.  **Default Policy:** If a packet does not match any specific rule, the system applies the **Default Policy** (`deny incoming`), ensuring no unauthorized traffic is permitted.
4.  **Stateful Inspection:** UFW tracks established connections (Stateful), allowing return traffic for legitimate outbound sessions without needing specific inbound rules.
