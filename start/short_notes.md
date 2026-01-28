Perfect — here’s a **single, clean, GitHub-ready Markdown file** that covers **STEP 1 only**, written for **absolute beginners**, with **detailed steps + examples**, exactly as discussed.

You can copy-paste this into a repo as something like:

```
STEP-1-install-aws-cli.md
```

---

````md
# STEP 1: Install Prerequisites (One Time)
## Installing and Configuring AWS CLI (From Absolute Zero)

This guide assumes:
- You have **nothing installed**
- You are on **Windows 10 / 11 (64-bit)**
- You want to use **AWS SAM later for local Lambda development**

This step is **mandatory** and needs to be done only once.

---

## What is AWS CLI?

**AWS CLI (Command Line Interface)** allows your local machine to communicate with AWS services using commands.

Example:
```bash
aws s3 ls
````

AWS SAM **depends on AWS CLI**, so SAM will not work without it.

---

## STEP 1.1 — Install AWS CLI (Windows)

### 1. Download AWS CLI

1. Open your browser
2. Go to the official AWS page:
   [https://aws.amazon.com/cli/](https://aws.amazon.com/cli/)
3. Click **Download for Windows**
4. Download the file:

   ```
   AWSCLIV2.msi
   ```

---

### 2. Install AWS CLI

1. Double-click `AWSCLIV2.msi`
2. Click **Next**
3. Click **Next**
4. Click **Install**
5. Wait for installation to complete
6. Click **Finish**

---

### 3. Verify Installation

1. Press **Win + R**
2. Type `cmd` and press Enter
3. Run the command:

   ```bash
   aws --version
   ```

#### Expected Output (example):

```
aws-cli/2.15.10 Python/3.11 Windows/10 exe/AMD64
```

✅ If you see output → AWS CLI installed successfully
❌ If command not found → reboot once and try again

---

## STEP 1.2 — Create an AWS Account (Skip if you already have one)

1. Go to [https://aws.amazon.com/](https://aws.amazon.com/)
2. Click **Create an AWS Account**
3. Sign up using email and password
4. Add payment details (Free Tier eligible)
5. Choose **Basic Support (Free)**

---

## STEP 1.3 — Create IAM User (Important)

⚠️ **Never use root account access keys**

IAM users are safer and recommended for development.

---

### 1. Open IAM Console

1. Login to AWS Console
2. Search for **IAM**
3. Click **Users**
4. Click **Create user**

---

### 2. Create User

* User name:

  ```
  sam-local-user
  ```
* Click **Next**

---

### 3. Attach Permissions

1. Select **Attach policies directly**
2. Search and select:

   ```
   AdministratorAccess
   ```
3. Click **Next**
4. Click **Create user**

> For learning purposes we use AdministratorAccess.
> In production, permissions should be restricted.

---

### 4. Create Access Keys

1. Open the created user
2. Go to **Security credentials**
3. Click **Create access key**
4. Select:

   ```
   Command Line Interface (CLI)
   ```
5. Click **Next**
6. Click **Create access key**

You will see:

* **Access Key ID**
* **Secret Access Key**

⚠️ **Save them securely** — you will not see the secret again.

---

## STEP 1.4 — Configure AWS CLI

Open **Command Prompt** and run:

```bash
aws configure
```

Enter values as shown:

```
AWS Access Key ID [None]: <PASTE ACCESS KEY>
AWS Secret Access Key [None]: <PASTE SECRET KEY>
Default region name [None]: ap-south-1
Default output format [None]: json
```

---

## STEP 1.5 — Verify AWS CLI Configuration

Run:

```bash
aws sts get-caller-identity
```

### Expected Output (example):

```json
{
  "UserId": "AIDAEXAMPLE",
  "Account": "123456789012",
  "Arn": "arn:aws:iam::123456789012:user/sam-local-user"
}
```

✅ This confirms:

* AWS CLI is installed
* Credentials are working
* You are authenticated with AWS

---

## What We Achieved in STEP 1

✔ Installed AWS CLI
✔ Created AWS account
✔ Created IAM user
✔ Configured local credentials
✔ Verified AWS access

---

## Next Step

➡️ **STEP 2: Install Docker (Required for AWS SAM)**

Docker is mandatory because AWS SAM runs Lambda locally inside containers.

```

---

If you want, next I can:
- Create **STEP 2 (Docker)** in the same GitHub style  
- Combine **STEP 1 + STEP 2 + STEP 3 (SAM)** into a **single README.md**
- Convert this into a **full beginner AWS SAM tutorial repo**

Just tell me 👍
```
