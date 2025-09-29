Perfect! Let’s do a **full AWS SAM (Serverless Application Model) walkthrough** from scratch to advanced, with **line-by-line explanations** and a working example. I’ll guide you step by step, covering **installation, project setup, local testing, deployment, and advanced topics** like environment variables, layers, and CI/CD integration.

We’ll do this using **Node.js** as an example runtime.

---

## **1️⃣ Prerequisites**

Before starting, make sure you have:

1. **AWS CLI installed & configured**

   ```bash
   aws configure
   ```

   This sets your AWS credentials (`Access Key ID` + `Secret Access Key` + region).

2. **SAM CLI installed**

   ```bash
   sam --version
   ```

   Latest versions support `sam init`, local testing, and advanced features.

3. **Docker installed** (for local Lambda simulation)

   ```bash
   docker --version
   ```

   Docker is required for testing Lambdas locally.

---

## **2️⃣ Initialize a SAM Project**

```bash
sam init
```

**Step-by-step interactive setup:**

1. **Template source:** `1` → AWS Quick Start Templates
2. **Runtime:** `nodejs18.x` (latest LTS Node.js for Lambda)
3. **Package type:** `Zip` (standard, small projects)
4. **Project name:** `sam-node-api`

This creates a folder `sam-node-api` with structure:

```
sam-node-api/
├── README.md
├── template.yaml        # SAM template (CloudFormation syntax)
├── hello-world/         # Lambda function code
│   ├── app.js
│   └── package.json
```

---

## **3️⃣ Understand `template.yaml`**

This is **the core of SAM** – it defines your serverless infrastructure.

Example snippet:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
Description: >
  sam-node-api

Globals:
  Function:
    Timeout: 3  # Default Lambda timeout in seconds

Resources:
  HelloWorldFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: hello-world/
      Handler: app.lambdaHandler
      Runtime: nodejs18.x
      Events:
        HelloWorld:
          Type: Api
          Properties:
            Path: /hello
            Method: get
```

**Explanation line by line:**

* `AWSTemplateFormatVersion` → Required CloudFormation version.
* `Transform: AWS::Serverless-2016-10-31` → Enables SAM-specific syntax.
* `Globals` → Default properties for all Lambda functions.
* `Resources` → Defines AWS resources.
* `HelloWorldFunction` → Logical name for the Lambda.

  * `Type: AWS::Serverless::Function` → SAM Lambda resource.
  * `CodeUri` → Folder containing Lambda code.
  * `Handler` → Entry point (`file.functionName`).
  * `Runtime` → Node.js runtime.
  * `Events` → Triggers for Lambda. Here, an API Gateway GET `/hello`.

---

## **4️⃣ Write Lambda Code**

`hello-world/app.js`:

```javascript
exports.lambdaHandler = async (event) => {
    console.log("Event:", event);

    return {
        statusCode: 200,
        body: JSON.stringify({
            message: "Hello from SAM Lambda!",
            input: event
        }),
    };
};
```

**Line by line:**

* `exports.lambdaHandler` → Lambda entry function.
* `async (event)` → Receives API Gateway request or other events.
* `console.log` → Logs visible in CloudWatch.
* `return {statusCode, body}` → API Gateway response.
* `JSON.stringify` → Converts JS object to string.

---

## **5️⃣ Install Dependencies**

If your Lambda uses npm packages:

```bash
cd hello-world
npm init -y
npm install axios
```

**Note:** SAM will package dependencies automatically when deploying.

---

## **6️⃣ Local Testing**

### Using SAM CLI:

```bash
sam build
sam local invoke HelloWorldFunction --event events/event.json
```

`events/event.json` example:

```json
{
  "key1": "value1"
}
```

✅ This simulates Lambda locally.

### Local API Gateway:

```bash
sam local start-api
```

* Opens a local server at `http://127.0.0.1:3000/hello`
* You can test using Postman or curl:

```bash
curl http://127.0.0.1:3000/hello
```

---

## **7️⃣ Deploy to AWS**

```bash
sam deploy --guided
```

Interactive prompts:

1. Stack Name → `sam-node-api-stack`
2. AWS Region → `us-east-1`
3. Confirm changes → `Y`
4. Allow SAM CLI to create roles → `Y`
5. Save arguments for future → `Y`

After deployment, SAM outputs the **API Gateway URL**.

---

## **8️⃣ Advanced Topics**

### 8.1 Environment Variables

```yaml
Properties:
  Environment:
    Variables:
      STAGE: dev
      API_KEY: !Ref ApiKeyParameter
```

* Access in Lambda: `process.env.STAGE`

---

### 8.2 Layers (Shared Code/Dependencies)

Create a layer:

```bash
sam init
# Choose "AWS Quick Start Templates" -> "Node.js" -> "Zip"
# Then add layer in template.yaml
```

```yaml
Layers:
  MyUtilsLayer:
    Type: AWS::Serverless::LayerVersion
    Properties:
      LayerName: my-utils
      Description: Utilities layer
      ContentUri: layer-code/
      CompatibleRuntimes:
        - nodejs18.x
```

Use in Lambda:

```yaml
Properties:
  Layers:
    - !Ref MyUtilsLayer
```

---

### 8.3 CI/CD with SAM

* Use **GitHub Actions** or **CodePipeline**
* Typical steps: `sam build → sam package → sam deploy`
* SAM generates CloudFormation artifacts (`.aws-sam` folder).

---

### 8.4 Monitoring & Logging

* SAM Lambda automatically logs to **CloudWatch**
* Use `sam logs -n HelloWorldFunction --stack-name sam-node-api-stack --tail` to stream logs.

---

## **9️⃣ Summary of Best Practices**

1. Always use **SAM Quick Start Templates** for new projects.
2. Structure code clearly: `functions/`, `layers/`.
3. Use **environment variables** instead of hardcoding.
4. Test locally with `sam local start-api` before deploying.
5. Use **SAM CLI guided deploy** for first-time deployment.
6. Use **Layers** for shared dependencies.
7. Integrate **CI/CD** early for automated deployments.

---

