# DISP Team 3 2026 - ProBuild Camunda 8 Portfolio Submission

## Project Overview

This repository contains the DISP Team 3 portfolio submission for the ProBuild case study.

The project models and automates the ProBuild operational process using:

- i* socio-technical modelling
- Strategic BPMN
- Operational BPMN
- Camunda 8 SaaS
- Camunda Forms
- Java Spring Boot external workers
- Maven
- GitHub version control

The automation is designed to run in Camunda 8. The BPMN process is deployed to Camunda Web Modeler, while the Java worker project runs locally and connects to Camunda through the Camunda API.

---

## Repository Structure

```text
DISP TEAM3/
│
├── README.md
├── repository-link.txt
│
├── Camunda-Upload-Resources/
│   ├── probuild-operational-model.bpmn
│   └── forms/
│       ├── approve-repair-request.form
│       ├── check-tool-availability.form
│       ├── finance-application.form
│       ├── fixpro-service-report.form
│       ├── payment.form
│       ├── place-retail-order.form
│       └── submit-hire-request.form
│
├── Java-Worker-Project/
│   ├── pom.xml
│   ├── README.md
│   └── src/
│       └── main/
│           ├── java/com/probuild/automation/
│           │   ├── ProBuildApplication.java
│           │   ├── CamundaDeploymentRunner.java
│           │   └── workers/
│           │       ├── FinanceWorkers.java
│           │       ├── FixProWorkers.java
│           │       ├── InventoryWorkers.java
│           │       ├── ReportingWorkers.java
│           │       ├── RetailSalesWorkers.java
│           │       ├── ToolHireWorkers.java
│           │       └── WorkerSupport.java
│           │
│           └── resources/
│               ├── application.yml
│               ├── probuild-operational-model.bpmn
│               └── forms/
│                   ├── approve-repair-request.form
│                   ├── check-tool-availability.form
│                   ├── finance-application.form
│                   ├── fixpro-service-report.form
│                   ├── payment.form
│                   ├── place-retail-order.form
│                   └── submit-hire-request.form
│
├── Operational-BPMN/
│   ├── ProBuild_Operational_BPMN.bpmn
│   └── ProBuild_Operational_BPMN.png
│
├── Strategic-BPMN/
│   ├── ProBuild_Strategic_BPMN.bpmn
│   └── ProBuild_Strategic_BPMN.png
│
├── pistar/
│   ├── goalModel.txt
│   └── istar.png
│
└── Evidence/
    └── Team 3 test case.docx
