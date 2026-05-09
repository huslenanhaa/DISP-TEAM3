# DISP Team 3 2026 - ProBuild Process Modelling and Automation

## Project Summary

This repository contains the DISP Team 3 portfolio submission for the ProBuild Supplies Ltd case study.

The project models ProBuild as a socio-technical system and then develops the business process through strategic BPMN, operational BPMN, Camunda Forms, and Camunda 8 automation. The implemented solution demonstrates how ProBuild’s retail sales, tool hire, finance, warehouse, supplier, and repair workflows can be coordinated through a process automation engine.

The automation uses Camunda 8 SaaS for process execution and monitoring, with a Java Spring Boot worker application connecting to Camunda through the Camunda API. Camunda Forms are used to capture user input, and Java workers automate service tasks such as stock checks, payment handling, finance decisions, warehouse updates, and FixPro repair interactions.

---

## Technologies Used

- Camunda 8 SaaS
- Camunda Web Modeler
- Camunda Forms
- Camunda Operate
- Java 17
- Spring Boot
- Camunda Spring Boot Starter
- Maven
- BPMN 2.0
- i* socio-technical modelling
- GitHub for configuration management

---

## Repository Structure

```text
DISP TEAM3/
│
├── README.md
│
├── Socio-Technical-Model/
│   ├── ProBuild_iStar_SocioTechnical_Model.docx
│   └── goalModel.txt
│
├── Strategic-BPMN/
│   ├── ProBuild_Strategic_BPMN.bpmn
│   └── ProBuild_Strategic_BPMN.png
│
├── Operational-BPMN/
│   ├── ProBuild_Operational_BPMN.bpmn
│   └── ProBuild_Operational_BPMN.png
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
│           │   ├── demo/
│           │   │   └── ImportantAutomationSnippets.java
│           │   └── workers/
│           │       ├── FinanceWorkers.java
│           │       ├── FixProWorkers.java
│           │       ├── FinTrustWorkers.java
│           │       ├── RetailSalesWorkers.java
│           │       ├── ToolHireWorkers.java
│           │       └── WarehouseImsWorkers.java
│           │
│           └── resources/
│               ├── application.yml
│               ├── probuild-operational-model.bpmn
│               └── forms/
│
└── Evidence/
    ├── ProBuild_Camunda8_Testing_Evidence_22025274.docx
    └── ProBuild_Camunda8_Test_Case_Table_22025274.docx
Portfolio Coverage
Marking Area	Evidence in Repository
Socio-technical model	Socio-Technical-Model/
Strategic BPMN	Strategic-BPMN/
Operational BPMN	Operational-BPMN/ and Camunda-Upload-Resources/
Forms	Camunda-Upload-Resources/forms/
Automation	Java-Worker-Project/
Testing	Evidence/
Configuration management	GitHub repository, commits, README and organised folder structure
Camunda 8 Automation Overview
The operational BPMN model is designed for Camunda 8. User tasks are supported by Camunda Forms, while service tasks are automated using Java external workers.

The key automation pattern is:

Camunda BPMN Service Task
        ↓
Zeebe Job Type
        ↓
Java Spring Boot @JobWorker
        ↓
Business Logic / Service Simulation
        ↓
Variables returned to Camunda
        ↓
Process continues through gateways and events
Example:

@JobWorker(type = "run-real-time-credit-check-on-customer")
public Map<String, Object> runCreditCheck(final ActivatedJob job) {
    Map<String, Object> variables = job.getVariablesAsMap();

    boolean approved = true;

    return Map.of(
        "financeDecision", approved ? "approved" : "declined",
        "approved", approved,
        "declined", !approved,
        "correlationId", variables.get("correlationId")
    );
}
This shows how a BPMN service task is connected to Java code using a matching Zeebe job type.

How to Run the Java Worker Project
Open a terminal.

Navigate to the worker project:

cd Java-Worker-Project
Check that application.yml contains valid Camunda 8 SaaS client credentials:
camunda:
  client:
    mode: saas
    auth:
      client-id: YOUR_CLIENT_ID
      client-secret: YOUR_CLIENT_SECRET
    cloud:
      cluster-id: YOUR_CLUSTER_ID
      region: YOUR_REGION
Run the Spring Boot worker application:
mvn spring-boot:run
Keep the terminal running while testing the process in Camunda.
How to Deploy the BPMN and Forms
Open Camunda Web Modeler.
Upload the BPMN file from:
Camunda-Upload-Resources/probuild-operational-model.bpmn
Upload all forms from:
Camunda-Upload-Resources/forms/
Deploy the BPMN and forms to the Camunda 8 cluster.
Start a new process instance.
Monitor the process in Camunda Operate.
Example Test Variables
These variables can be used when starting a test process instance:

{
  "correlationId": "test-001",
  "toolAvailable": true,
  "stockAvailable": true,
  "paymentSuccessful": true,
  "financeDecision": "approved",
  "repairApproved": true,
  "tradeCard": false,
  "standard": true,
  "orderTotal": 150,
  "quantity": 1,
  "customerName": "Test Customer",
  "toolId": "DRILL-001",
  "approved": true,
  "declined": false,
  "confirmed": true,
  "routine": true,
  "repair": false,
  "passed": true,
  "failed": false
}
Testing Evidence
Testing evidence is stored in the Evidence/ folder.

The testing documentation includes:

Test strategy
Test cases
Expected results
Actual results
Defects identified
Defects fixed
Limitations and future improvements
Testing focused on deployment, form validation, variable passing, gateway decisions, Java worker execution, and monitoring through Camunda Operate.
