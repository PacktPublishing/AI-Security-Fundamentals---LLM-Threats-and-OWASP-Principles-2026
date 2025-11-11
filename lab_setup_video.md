# Video Transcript: Setting Up the LLM Security Labs on Your Local Machine

## Introduction

Hello everyone, and welcome to this comprehensive tutorial on setting up the LLM Security Labs environment on your local machine. I'm [Your Name], and today I'll be walking you through the entire process of creating your own secure testing environment for exploring LLM vulnerabilities.

The LLM Security Labs platform, which you may have seen at llm-sec.dev, provides an interactive way to understand and test various security vulnerabilities in Large Language Model applications. While the website offers a great visual overview, having your own local environment allows for deeper experimentation, customization, and a better understanding of the underlying security concepts.

## Overview of What We'll Cover

In this video, we'll cover:
1. Understanding what the LLM Security Labs environment is
2. Required prerequisites for your system
3. Setting up a Docker-based environment
4. Alternative setup methods if you encounter issues
5. Verifying your installation
6. Troubleshooting common problems

Let's get started!

## Understanding the LLM Security Labs Environment

Before we dive into the technical setup, let's understand what we're building. The LLM Security Labs is an educational platform designed to demonstrate the OWASP Top 10 vulnerabilities for Large Language Model applications. 

This environment consists of several interconnected components:
- A frontend interface for interacting with the labs
- Multiple backend services that simulate various LLM components
- A series of vulnerable endpoints that demonstrate specific security issues
- Documentation and guidance for each vulnerability

The architecture mirrors real-world LLM applications with components like:
- Client interfaces
- Ingress points
- LLM services
- Vector databases
- Training pipelines
- Security layers

Each component plays a role in demonstrating how vulnerabilities can manifest and be exploited in different parts of an LLM application stack.

## Prerequisites

Before we begin the installation, make sure your system meets these requirements:

1. **Operating System**: 
   - Linux (Ubuntu 20.04 or newer recommended)
   - macOS (10.15 or newer)
   - Windows 10/11 with WSL2 enabled

2. **Software Requirements**:
   - Docker and Docker Compose (latest stable version)
   - Git
   - Python 3.8 or newer
   - Node.js 16 or newer (for frontend components)
   - At least 8GB of RAM
   - 20GB of free disk space

3. **Technical Knowledge**:
   - Basic command line familiarity
   - Understanding of Docker concepts
   - Familiarity with web applications

Let's verify these prerequisites are installed on your system.

## Checking Your Prerequisites

Open your terminal or command prompt and run the following commands to verify your installations:

```bash
# Check Docker installation
docker --version
docker-compose --version

# Check Git installation
git --version

# Check Python installation
python --version  # or python3 --version on some systems

# Check Node.js installation
node --version
npm --version
```

If any of these commands fail, you'll need to install the missing software before proceeding.

## Setting Up the Environment

Now, let's proceed with setting up the LLM Security Labs environment. Typically, we would clone the official repository, but as of the time of this recording, the repository may not be directly accessible at the expected GitHub location. Let's explore alternative approaches.

### Approach 1: Creating Your Own Lab Environment

We'll create a Docker-based environment that simulates the key components needed for the LLM security labs:

1. First, create a new directory for our project:

```bash
mkdir llm-security-labs
cd llm-security-labs
```

2. Create a basic docker-compose.yml file:

```bash
touch docker-compose.yml
```

3. Open this file in your favorite text editor and add the following configuration:

```yaml
version: '3'

services:
  frontend:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - ./frontend:/usr/share/nginx/html
    depends_on:
      - api

  api:
    build: ./api
    ports:
      - "5000:5000"
    environment:
      - FLASK_APP=app.py
      - FLASK_ENV=development
    volumes:
      - ./api:/app

  vector-db:
    image: qdrant/qdrant
    ports:
      - "6333:6333"
    volumes:
      - ./data/qdrant:/qdrant/storage

  llm-service:
    build: ./llm-service
    ports:
      - "8000:8000"
    volumes:
      - ./llm-service:/app
    environment:
      - MODEL_PATH=/app/models
```

4. Now, let's create the necessary directories and basic files:

```bash
mkdir -p frontend api llm-service data/qdrant
```

5. Create a basic API service in the api directory:

```bash
cd api
touch Dockerfile app.py requirements.txt
```

6. Edit the Dockerfile:

```Dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["flask", "run", "--host=0.0.0.0"]
```

7. Edit requirements.txt:

```
flask==2.0.1
requests==2.26.0
```

8. Edit app.py:

```python
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/')
def index():
    return jsonify({"message": "Welcome to LLM Security Labs API"})

@app.route('/vulnerable/llm01', methods=['POST'])
def llm01_vulnerability():
    # Prompt injection vulnerability
    user_input = request.json.get('prompt', '')
    # Deliberately vulnerable endpoint
    return jsonify({"response": f"Processing your input: {user_input}"})

# Add more vulnerable endpoints for other LLM vulnerabilities

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')
```

9. Similarly, set up the LLM service:

```bash
cd ../llm-service
touch Dockerfile app.py requirements.txt
```

10. Edit the LLM service Dockerfile:

```Dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
```

11. Edit the LLM service requirements.txt:

```
fastapi==0.68.0
uvicorn==0.15.0
pydantic==1.8.2
```

12. Edit the LLM service app.py:

```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel

app = FastAPI()

class Prompt(BaseModel):
    text: str

@app.get("/")
def read_root():
    return {"message": "LLM Service for Security Labs"}

@app.post("/generate")
def generate_text(prompt: Prompt):
    # Simulate LLM response
    return {"generated_text": f"This is a simulated response to: {prompt.text}"}
```

13. Create a simple frontend:

```bash
cd ../frontend
touch index.html
```

14. Edit index.html:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LLM Security Labs</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #1e2130;
            color: white;
        }
        h1 {
            color: #61dafb;
            text-align: center;
        }
        .lab-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }
        .lab-item {
            border: 2px solid #61dafb;
            border-radius: 8px;
            padding: 15px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
        }
        .lab-item:hover {
            background-color: #2c3e50;
            transform: translateY(-5px);
        }
    </style>
</head>
<body>
    <h1>LLM Security Labs Playground</h1>
    <p>A hands-on learning platform for understanding and testing LLM security vulnerabilities. Explore interactive labs, experiment with real-world scenarios, and learn how to protect your LLM applications through practical experience.</p>
    
    <div class="lab-container">
        <div class="lab-item" onclick="alert('LLM01 Lab: Prompt Injection')">LLM01</div>
        <div class="lab-item" onclick="alert('LLM02 Lab: Insecure Output Handling')">LLM02</div>
        <div class="lab-item" onclick="alert('LLM03 Lab: Training Data Poisoning')">LLM03</div>
        <div class="lab-item" onclick="alert('LLM04 Lab: Vector DB Vulnerabilities')">LLM04</div>
        <div class="lab-item" onclick="alert('LLM05 Lab: Supply Chain Vulnerabilities')">LLM05</div>
        <div class="lab-item" onclick="alert('LLM06 Lab: Sensitive Information Disclosure')">LLM06</div>
        <div class="lab-item" onclick="alert('LLM07 Lab: Insecure Plugin Design')">LLM07</div>
        <div class="lab-item" onclick="alert('LLM08 Lab: Excessive Agency')">LLM08</div>
        <div class="lab-item" onclick="alert('LLM09 Lab: Overreliance')">LLM09</div>
        <div class="lab-item" onclick="alert('LLM10 Lab: Model Denial of Service')">LLM10</div>
    </div>
</body>
</html>
```

15. Now, let's start our environment:

```bash
cd ..
docker-compose up -d
```

This will build and start all the services defined in our docker-compose.yml file.

16. Verify the installation by opening your browser and navigating to:
    - Frontend: http://localhost:8080
    - API: http://localhost:5000
    - LLM Service: http://localhost:8000

### Approach 2: Using Alternative Repositories

If you're looking for more comprehensive examples that demonstrate LLM vulnerabilities, there are several open-source projects that can be adapted:

1. **LLM Security Sandbox Projects**: Search GitHub for "LLM security sandbox" or "LLM vulnerability examples"

2. **OWASP LLM Resources**: The OWASP foundation provides resources and code examples for their Top 10 LLM vulnerabilities

3. **Academic Research Repositories**: Many universities have published code demonstrating LLM vulnerabilities

For any of these alternatives, the general process would be:

```bash
git clone [repository-url]
cd [repository-directory]
# Follow the specific setup instructions in the repository's README
```

## Enhancing Your Lab Environment

Once you have the basic environment running, you can enhance it by:

1. **Adding More Vulnerabilities**: Expand the API service to include endpoints demonstrating all ten OWASP LLM vulnerabilities

2. **Integrating Real LLMs**: If you have the resources, integrate with open-source LLMs like Llama 2 or similar models that can run locally

3. **Improving the Frontend**: Develop a more interactive frontend that better visualizes the components and their relationships

4. **Adding Documentation**: Create detailed documentation for each vulnerability, explaining how it works and how to mitigate it

## Troubleshooting Common Issues

Here are some common issues you might encounter and how to resolve them:

1. **Docker Compose Errors**:
   - Ensure all services are properly defined in your docker-compose.yml
   - Check for port conflicts with existing services on your machine
   - Verify Docker has sufficient resources allocated

2. **API Connection Issues**:
   - Check that all services are running with `docker-compose ps`
   - Verify network connectivity between containers
   - Check logs with `docker-compose logs [service-name]`

3. **Performance Problems**:
   - If using real LLMs, ensure your machine has sufficient RAM and CPU
   - Consider using smaller models for testing purposes
   - Optimize Docker resource allocation

## Conclusion

In this video, we've walked through setting up your own LLM Security Labs environment for testing and learning about LLM vulnerabilities. While we've had to create our own implementation due to the unavailability of the official repository, this approach gives you more flexibility and a deeper understanding of how these systems work.

In the next video, we'll explore the dashboard of the LLM Security Labs platform and explain how the different components interact with each other.

Remember that security testing should always be performed in controlled environments and never against production systems without proper authorization.

Thank you for watching, and I'll see you in the next video where we'll dive into the dashboard overview!
