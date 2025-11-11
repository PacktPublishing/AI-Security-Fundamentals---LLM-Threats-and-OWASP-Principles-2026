# LLM Security Labs Demonstration Course Structure

## Course Overview

This course provides a comprehensive guide to understanding, setting up, and exploiting the vulnerabilities in the OWASP Top 10 for Large Language Model Applications. The course is structured as a series of video modules, each with its own detailed transcript.

## Module Sequence and Descriptions

### Module 1: Lab Setup
**File:** [lab_setup_video.md](/home/ubuntu/transcripts/lab_setup_video.md)

This introductory module guides students through setting up the LLM Security Labs environment on their local machines. It covers:
- Required prerequisites and software
- GitHub repository cloning and configuration
- Environment setup and verification
- Troubleshooting common setup issues

### Module 2: Dashboard Overview
**File:** [dashboard_overview_video.md](/home/ubuntu/transcripts/dashboard_overview_video.md)

This module provides a comprehensive overview of the LLM Security Labs dashboard, explaining:
- The dashboard's organization and components
- How vulnerabilities are categorized (security layer, training pipeline, vector DB, ingress, etc.)
- Navigation and interaction with the lab environment
- Understanding the relationship between components

### Module 3: LLM01 - Prompt Injection
**File:** [llm01_vulnerability_demo.md](/home/ubuntu/transcripts/llm01_vulnerability_demo.md)

This module explores the first vulnerability in the OWASP Top 10 for LLMs: Prompt Injection. It covers:
- Understanding prompt injection vulnerabilities
- Direct and indirect prompt injection techniques
- Live demonstration of exploiting prompt injection
- Mitigation strategies and best practices

### Module 4: LLM02 - Insecure Output Handling
**File:** [llm02_vulnerability_demo.md](/home/ubuntu/transcripts/llm02_vulnerability_demo.md)

This module explores the second vulnerability: Insecure Output Handling. It covers:
- Understanding the risks of insecure output handling
- XSS, CSRF, and other injection attacks via LLM outputs
- Live demonstration of exploiting output handling vulnerabilities
- Mitigation strategies and secure output processing techniques

### Module 5: LLM03 - Training Data Poisoning
**File:** [llm03_vulnerability_demo.md](/home/ubuntu/transcripts/llm03_vulnerability_demo.md)

This module explores the third vulnerability: Training Data Poisoning. It covers:
- Understanding training data poisoning attacks
- Different poisoning techniques and their impacts
- Live demonstration of poisoned model behavior
- Mitigation strategies and data validation techniques

### Module 6: LLM04 - Model Denial of Service
**File:** [llm04_vulnerability_demo.md](/home/ubuntu/transcripts/llm04_vulnerability_demo.md)

This module explores the fourth vulnerability: Model Denial of Service. It covers:
- Understanding resource consumption attacks against LLMs
- Techniques for causing excessive token usage or processing time
- Live demonstration of DoS attacks against LLM systems
- Mitigation strategies and resource management techniques

### Module 7: LLM05 - Supply Chain Vulnerabilities
**File:** [llm05_vulnerability_demo.md](/home/ubuntu/transcripts/llm05_vulnerability_demo.md)

This module explores the fifth vulnerability: Supply Chain Vulnerabilities. It covers:
- Understanding the LLM supply chain and its vulnerabilities
- Risks in model sources, dependencies, and integrations
- Live demonstration of supply chain vulnerability exploitation
- Mitigation strategies and supply chain security practices

### Module 8: LLM06 - Sensitive Information Disclosure
**File:** [llm06_vulnerability_demo.md](/home/ubuntu/transcripts/llm06_vulnerability_demo.md)

This module explores the sixth vulnerability: Sensitive Information Disclosure. It covers:
- Understanding how LLMs can leak sensitive information
- Techniques for extracting training data and system details
- Live demonstration of information extraction attacks
- Mitigation strategies and information protection techniques

### Module 9: LLM07 - Insecure Plugin Design
**File:** [llm07_vulnerability_demo.md](/home/ubuntu/transcripts/llm07_vulnerability_demo.md)

This module explores the seventh vulnerability: Insecure Plugin Design. It covers:
- Understanding the security risks of LLM plugins and extensions
- Common plugin vulnerabilities and attack vectors
- Live demonstration of exploiting vulnerable plugins
- Mitigation strategies and secure plugin design principles

### Module 10: LLM08 - Excessive Agency
**File:** [llm08_vulnerability_demo.md](/home/ubuntu/transcripts/llm08_vulnerability_demo.md)

This module explores the eighth vulnerability: Excessive Agency. It covers:
- Understanding the risks of giving LLMs too much autonomy
- Scenarios where excessive agency leads to security issues
- Live demonstration of excessive agency exploitation
- Mitigation strategies and appropriate agency design

### Module 11: LLM09 - Overreliance
**File:** [llm09_vulnerability_demo.md](/home/ubuntu/transcripts/llm09_vulnerability_demo.md)

This module explores the ninth vulnerability: Overreliance. It covers:
- Understanding the risks of excessive trust in LLM outputs
- How overreliance leads to security and operational issues
- Live demonstration of overreliance scenarios
- Mitigation strategies and appropriate trust calibration

### Module 12: LLM10 - Model Denial of Service
**File:** [llm10_vulnerability_demo.md](/home/ubuntu/transcripts/llm10_vulnerability_demo.md)

This module explores the tenth vulnerability: Model Denial of Service. It covers:
- Understanding sophisticated DoS attacks against LLM systems
- Advanced techniques for resource exhaustion
- Live demonstration of model-specific DoS attacks
- Mitigation strategies and advanced resource protection

## Course Flow and Progression

The course follows a logical progression:

1. **Setup and Orientation (Modules 1-2)**: Students first learn how to set up the lab environment and understand the dashboard organization.

2. **Input-Related Vulnerabilities (Modules 3-4)**: The course then explores vulnerabilities related to inputs and outputs.

3. **Training and Model Vulnerabilities (Modules 5-6)**: Next, students learn about vulnerabilities in the training process and model operation.

4. **Integration Vulnerabilities (Modules 7-9)**: The course then covers vulnerabilities related to the broader ecosystem and integrations.

5. **Human-AI Interaction Vulnerabilities (Modules 10-11)**: Students explore vulnerabilities related to human-AI interaction patterns.

6. **Advanced Attack Vectors (Module 12)**: The course concludes with advanced attack techniques.

Each module builds on knowledge from previous modules, creating a comprehensive understanding of LLM security risks and mitigations.
