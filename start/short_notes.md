Perfect 👍
Below is a **single, clean, GitHub-ready `README.md`** that combines:

* ✅ **STEP 1 – AWS CLI**
* ✅ **STEP 2 – Docker**
* ✅ **STEP 3 – AWS SAM CLI**

It’s written so **someone starting from zero** can follow it end-to-end.

You can **copy–paste this directly into GitHub**.

---

````md
# AWS SAM Local Development Setup (Windows)

This guide explains how to set up **AWS CLI**, **Docker**, and **AWS SAM CLI** on Windows so you can:
- Develop AWS Lambda locally
- Debug easily
- Deploy confidently to AWS
- Avoid repeated AWS Console debugging

---

## Prerequisites

- Windows 10 or later
- An AWS Account
- Internet connection
- Basic command-line familiarity

---

## STEP 1: Install and Configure AWS CLI

### What is AWS CLI?
AWS CLI is a command-line tool that allows your local machine to communicate with AWS services securely.

> There is **no separate AWS terminal**.  
> You use AWS CLI **inside CMD / PowerShell**.

---

### 1.1 Install AWS CLI

1. Download AWS CLI v2 from:
   https://aws.amazon.com/cli/

2. Run the installer (`AWSCLIV2.msi`)
3. Click **Next → Install → Finish**

---

### 1.2 Verify AWS CLI Installation

Open **Command Prompt (CMD)** and run:

```bat
aws --version
````

Expected output (example):

```text
aws-cli/2.x.x Python/3.x Windows/10 exe/AMD64
```

---

### 1.3 Configure AWS CLI

Run:

```bat
aws configure
```

Enter:

```text
AWS Access Key ID:     <your-access-key>
AWS Secret Access Key: <your-secret-key>
Default region name:   ap-south-1
Default output format: json
```

This creates:

```
C:\Users\<username>\.aws\credentials
C:\Users\<username>\.aws\config
```

---

### 1.4 Verify AWS Authentication

Run:

```bat
aws sts get-caller-identity
```

Expected output:

```json
{
  "UserId": "AIDAXXXXXXXX",
  "Account": "123456789012",
  "Arn": "arn:aws:iam::123456789012:user/your-user-name"
}
```

✅ This confirms AWS CLI is installed and connected to AWS.

---

## STEP 2: Install and Verify Docker

### Why Docker is Required

AWS Lambda always runs on **Linux**.
Docker allows SAM to run your Lambda **inside the same runtime environment locally**.

Without Docker:

* `sam local` will not work
* Local debugging is impossible

---

### 2.1 Install Docker Desktop

1. Download Docker Desktop:
   [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)

2. Install and **restart your system** if prompted

---

### 2.2 Start Docker Desktop

* Open **Docker Desktop**
* Wait until it shows:
  **“Docker Desktop is running”**

Ensure Docker is using **Linux containers**:

* If you see **“Switch to Linux containers”**, click it
* If you see **“Switch to Windows containers”**, you’re already in Linux mode

---

### 2.3 Verify Docker Installation

Open **CMD as Administrator** and run:

```bat
docker --version
```

Then run:

```bat
docker run hello-world
```

Expected output:

```text
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

✅ Docker Engine is running correctly.

---

## STEP 3: Install AWS SAM CLI

### What is AWS SAM?

AWS SAM (Serverless Application Model) is a tool that:

* Builds Lambda functions
* Runs them locally using Docker
* Deploys them using AWS CloudFormation

SAM internally uses **AWS CLI + Docker**.

---

### 3.1 Install SAM CLI

Download from:
[https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html)

Run the installer and finish setup.

---

### 3.2 Verify SAM Installation

Run:

```bat
sam --version
```

Expected output:

```text
SAM CLI, version x.x.x
```

---

## How Everything Fits Together

```
CMD / PowerShell
   ↓
AWS CLI  → talks to AWS
SAM CLI  → builds & deploys Lambda
Docker   → runs Lambda locally (Linux runtime)
```

---

## Common Troubleshooting

### ❌ `docker_engine` not found

* Docker Desktop is not running
* Start Docker Desktop and retry

### ❌ `aws: command not found`

* AWS CLI not installed
* PATH not updated
* Restart terminal or system

### ❌ `sam local` fails

* Docker not running
* Not in Linux container mode

---

## What’s Next?

After completing these steps, you are ready to:

* Create a SAM project:

  ```bat
  sam init
  ```
* Run Lambda locally:

  ```bat
  sam local start-api
  ```
* Debug locally using VS Code
* Deploy using:

  ```bat
  sam deploy
  ```

---

## Final Checklist

| Tool    | Status                   |
| ------- | ------------------------ |
| AWS CLI | ✅ Installed & configured |
| Docker  | ✅ Running                |
| SAM CLI | ✅ Installed              |

🚀 You now have a professional local AWS Lambda development setup.

```

---

If you want, next I can:
- Add **STEP 4: Create your first SAM Lambda**
- Add **local debugging with VS Code**
- Split this into `docs/` for a polished GitHub repo

Just tell me 👍
```
