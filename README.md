# ProBuild Camunda 8 Process Automation

## DISP Team 3 - 2026 Submission

This project is a Camunda 8 process automation solution for the ProBuild case study. It demonstrates how a business process can be modelled using BPMN and automated using Camunda 8, Camunda Forms, and Java-based external workers.

The solution covers ProBuild’s operational process, including customer tool hire, retail ordering, stock checking, payment handling, finance application processing, FixPro repair handling, and reporting.

---

## Project Overview

The project contains:

- An executable Camunda 8 BPMN model
- Camunda Forms for human user tasks
- A Spring Boot Java application
- External workers implemented using Camunda `@JobWorker`
- SaaS connection configuration for Camunda 8
- Supporting resources for deployment and testing

Camunda 8 is used as the process automation engine. The Java application connects to Camunda and handles service tasks when they are created by the running process instance.

---

## Technologies Used

- Java
- Spring Boot
- Maven
- Camunda 8
- Zeebe
- Camunda Web Modeler
- Camunda Tasklist
- Camunda Operate
- Camunda Forms
- BPMN 2.0

---

## Project Structure

```text
ProBuild-Camunda8-Run/
│
├── pom.xml
├── README.md
│
├── src/
│   └── main/
│       ├── java/
│       │   └── com/probuild/automation/
│       │       ├── ProBuildApplication.java
│       │       ├── CamundaDeploymentRunner.java
│       │       └── workers/
│       │           ├── FinanceWorkers.java
│       │           ├── FixProWorkers.java
│       │           ├── InventoryWorkers.java
│       │           ├── ReportingWorkers.java
│       │           ├── RetailSalesWorkers.java
│       │           ├── ToolHireWorkers.java
│       │           └── WorkerSupport.java
│       │
│       └── resources/
│           ├── application.yml
│           ├── probuild-operational-model.bpmn
│           └── forms/
│               ├── approve-repair-request.form
│               ├── check-tool-availability.form
│               ├── finance-application.form
│               ├── fixpro-service-report.form
│               ├── payment.form
│               ├── place-retail-order.form
│               └── submit-hire-request.form
│
└── Camunda-Upload-ProBuild/
    ├── probuild-operational-model.bpmn
    ├── approve-repair-request.form
    ├── check-tool-availability.form
    ├── finance-application.form
    ├── fixpro-service-report.form
    ├── payment.form
    ├── place-retail-order.form
    └── submit-hire-request.form
