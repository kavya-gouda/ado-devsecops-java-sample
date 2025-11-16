# ado-devsecops-java-sample

# 🚀 java-devsecops-azure: End-to-End DevSecOps for a Java Project

This repository contains the source code and Azure DevOps pipeline configuration files (YAML) for implementing a comprehensive **DevSecOps** pipeline for a Java web application. The pipeline integrates industry-standard security tools across the Continuous Integration (CI) and Continuous Delivery (CD) process to "Shift Left" security.

The project is built on Maven/Java and uses the `pom.xml` for dependency management.

---

## 🎯 Case Study Objectives

This project demonstrates a real-world DevSecOps workflow to ensure application security and code quality from commit to deployment.

| Security Principle | Tool Integrated | Azure DevOps Stage | Focus |
| :--- | :--- | :--- | :--- |
| **Code Quality & SAST** | **SonarCloud** | Build/CI | Static Application Security Testing (SAST) to detect security issues and code smells directly in the source code. |
| **SCA** | **Snyk** | Build/CI | Software Composition Analysis (SCA) to scan third-party libraries (defined in `pom.xml`) for known vulnerabilities (CVEs). |
| **DAST** | **OWASP ZAP** | Release/CD | Dynamic Application Security Testing (DAST) to scan the deployed web application for runtime vulnerabilities (e.g., XSS, weak ciphers). |

---


## ⚙️ Pipeline Flow Overview

The Azure DevOps pipeline is structured sequentially, with automated security gates ensuring that the application meets quality and security standards before moving to the next stage.

1.  **Commit:** Java developer commits code to the source repository.
2.  **Build Stage (CI):**
    * **Compile:** Java code is compiled using Maven.
    * **SAST Scan (SonarCloud):** Analysis runs against the source code.
    * **SCA Scan (Snyk):** Dependencies in `pom.xml` are scanned.
    * **Quality Gate:** The build will fail if SonarCloud's Quality Gate or Snyk's vulnerability check finds critical issues.
    * **Publish Artifacts:** The built application is packaged and published as an artifact.
3.  **Deployment Stage:**
    * **Deploy:** The application artifact is automatically deployed to a **Test/QA environment**.
4.  **Security Stage (CD):**
    * **DAST Scan (OWASP ZAP):** The running web application in the Test/QA environment is scanned.
    * **Report Archival:** The DAST report is collected and archived within the Azure DevOps pipeline for future review and auditing.
5.  **Review & Promotion:** Security scan results are reviewed directly within the Azure DevOps dashboard before manual or automated promotion to production.

---

## 💻 Prerequisites & Setup

To replicate this pipeline, you will need the following accounts and configurations:

1.  **Azure DevOps Account:** For setting up the project, Azure Repos, and Azure Pipelines.
2.  **Java Environment:** The Azure DevOps agent must have the correct **Java JDK** installed (e.g., **Java 17** as per the latest course updates).
3.  **SonarCloud Account:** A security token/login must be configured as an **Azure DevOps Service Connection** for SAST integration.
4.  **Snyk Account:** An API token must be configured as a **Secure File/Variable Group** in Azure DevOps for SCA integration.
5.  **OWASP ZAP:** The pipeline will typically use a containerized or pre-installed version of ZAP on the agent to run the DAST scan against the deployed endpoint.

---

## 📁 Key Files in this Repository

| File Name | Purpose |
| :--- | :--- |
| **`pom.xml`** | Maven project configuration and definition of third-party Java libraries. |
| **`azure-pipeline.yaml`** | The complete multi-stage YAML definition for the DevSecOps CI/CD pipeline, including SAST, SCA, and DAST stages. |
| **`/src/`** | Contains the core Java source code for the web application. |
| **`Jenkinsfile` (Optional)** | (In a hybrid scenario) Demonstrates an alternative CI/CD orchestration. |

**Note:** The `azure-pipeline.yaml` file demonstrates the use of **modular pipeline (Parent & Child YAML/YML files)** for improved organization, utilizing the `depends-on` keyword for sequential stage execution.

---

## 📈 Learning Outcomes

By implementing this case study, you will gain hands-on experience in:

* Implementing **DevSecOps** principles within the Azure DevOps platform.
* Integrating **SonarCloud/SonarQube** for Quality Gates and SAST.
* Integrating **Snyk** for SCA and dependency vulnerability management.
* Implementing **OWASP ZAP** for automated DAST scanning.
* Archiving security reports and reviewing scan results within the Azure DevOps dashboard.
* Using **JIRA integration** (as covered in the full course) to report security issues automatically.
