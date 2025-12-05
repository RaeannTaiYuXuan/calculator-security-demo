# Security Scanning

## Overview
This repository uses three types of security scanning to ensure that the code, dependencies, and live application are secure:

### SAST (Static Analysis with CodeQL)
- **Purpose**: Scans source code for vulnerabilities such as **code injections**, **buffer overflows**, and **logic errors**.
- **Trigger**: Runs on **push** to the `main` branch or **pull requests**.
- **Checks for**:
  - Code quality issues
  - Data flow vulnerabilities
  - OWASP Top 10 issues
  - Security risks in the source code logic
- **Artifacts**: Results are available in the **GitHub Security tab** under the "Code Scanning" section.

**Workflow File**: [.github/workflows/1-sast-only.yml](https://github.com/your-repo-path/.github/workflows/1-sast-only.yml)

### SCA (Dependency Check)
- **Purpose**: Scans Python packages for known **CVE** (Common Vulnerabilities and Exposures) vulnerabilities in third-party libraries.
- **Trigger**: Runs on **push** to the `main` branch or **pull requests**.
- **Checks for**:
  - Outdated or vulnerable dependencies
  - Known CVEs in libraries used by the project
- **Artifacts**: Download the **sca-reports** from the GitHub Actions Artifacts section.

**Workflow File**: [.github/workflows/2-sca-only.yml](https://github.com/your-repo-path/.github/workflows/2-sca-only.yml)

### DAST (Live Application with ZAP)
- **Purpose**: Tests the running application for runtime vulnerabilities such as **SQL injection**, **XSS**, and missing **security headers**.
- **Trigger**: Runs on **push** to the `main` branch or **pull requests**.
- **Checks for**:
  - Missing security headers (e.g., `X-Frame-Options`, `X-Content-Type-Options`)
  - Misconfigured HTTP methods
  - Vulnerabilities in API endpoints
  - Cross-Site Scripting (XSS) and SQL Injection in the running app
- **Artifacts**: Results available as **zap-baseline-reports** and **zap-fullscan-reports** in GitHub Actions Artifacts.

**Workflow File**: [.github/workflows/3-dast-only.yml](https://github.com/your-repo-path/.github/workflows/3-dast-only.yml)

---

## Understanding Results

### **SAST (CodeQL) Results**
- The CodeQL results are available in the **Security** tab of your GitHub repository. 
- If vulnerabilities are found in the code, they will be listed with their **severity** and **location**.
- Pay close attention to issues marked as **Critical** or **High**, as they represent immediate security risks to the application.

### **SCA (Dependency Check) Results**
- The **sca-reports** artifact will contain the list of **vulnerable dependencies** in the project.
- The report will classify vulnerabilities based on their **CVSS score** (Common Vulnerability Scoring System).
  - **High** severity vulnerabilities need immediate attention.
  - **Medium** severity issues should be addressed based on project timelines.
  - **Low** severity issues should be addressed for long-term code hygiene.

### **DAST (ZAP) Results**
- The **zap-baseline-reports** and **zap-fullscan-reports** artifacts will contain the runtime security issues identified by ZAP.
- The baseline scan will find **passive issues** like **missing headers**.
- The full scan will actively test the application for issues like **SQL Injection** or **Cross-Site Scripting (XSS)**.
- ZAP provides detailed explanations of the issues along with **risk levels** (Low, Medium, High).

## Reporting Vulnerabilities

If you find any **critical vulnerabilities** during the scans, please report them to the security team at **security@example.com**.

For **non-critical issues**, please open a GitHub issue under the **Security** label in this repository.

---

### **Best Practices**
- **Monitor Regularly**: Ensure that the security scans are running as expected by checking the GitHub Actions tab regularly.
- **Fix Critical Issues First**: Prioritize addressing critical vulnerabilities (e.g., injection attacks, outdated dependencies with known CVEs).
- **Improve Code Quality**: Use CodeQL's recommendations to improve the overall security of your codebase.
- **Stay Updated**: Regularly update dependencies to avoid using libraries with known vulnerabilities.

