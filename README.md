DISP Team 3 2026 - ProBuild Camunda 8 Submission

Project purpose
This project implements the ProBuild Supplies Ltd operational process using Camunda 8. It demonstrates how the business process can be automated using BPMN, Camunda Forms, Tasklist user tasks, service tasks, Java workers, and process monitoring in Operate.

The model covers retail sales, tool hire, stock checking, payment handling, Trade Card benefits, FixPro maintenance, and FinTrust finance approval.

Submission contents

1. Camunda-Upload-Resources/
   Contains the BPMN model and Camunda Forms that must be uploaded into Camunda Web Modeler.

   Main files:
   - probuild-operational-model.bpmn
   - forms/*.form

2. Java-Worker-Project/
   Contains the Spring Boot Camunda 8 worker application.

   The Java workers complete automated BPMN service tasks such as:
   - checking tool availability in IMS
   - checking stock availability
   - processing payment/deposit
   - reserving hired tools
   - updating tool status
   - applying Trade Card points
   - syncing FixPro service records
   - running FinTrust credit checks

3. Operational-BPMN/
   Contains the operational BPMN model evidence.

4. Strategic-BPMN/
   Contains the higher-level strategic BPMN model evidence.

5. pistar/
   Contains the piStar/iStar socio-technical goal model evidence.

6. Evidence/
   Contains screenshots, test evidence, and supporting demo material.

How to run the demo

1. Open Camunda Web Modeler.
2. Upload the BPMN and forms from Camunda-Upload-Resources.
3. Deploy the BPMN to the Camunda 8 cluster.
4. Start the Java worker application:

   cd Java-Worker-Project
   mvn spring-boot:run

5. Start a process instance in Camunda.
6. Use Tasklist to complete user tasks and forms.
7. Use Operate to show the running process, completed tasks, variables, and service task execution.

Recommended demo scenario

The clearest demo path is the successful tool hire process:

1. Customer submits a tool hire request.
2. ProBuild validates the hire request.
3. IMS checks whether the tool is available.
4. The system creates a provisional booking.
5. Payment or deposit is processed.
6. Tool stock is reserved.
7. Booking confirmation is generated.
8. The tool is issued to the customer.
9. When returned, the tool can either go back to ready-to-hire or be sent to FixPro for maintenance.

External partner processes

FixPro Ltd:
FixPro handles tool maintenance, repair, PAT testing, compliance checks, service reports, and out-of-service decisions. This shows how ProBuild depends on an external maintenance partner to keep hire tools safe and compliant.

FinTrust UK:
FinTrust handles customer finance. It receives the finance application, runs a credit check, sends approval or rejection to ProBuild, pays ProBuild upfront if approved, and collects customer repayments.

Important implementation note

The external APIs are simulated by Java workers. This is suitable for the coursework because the aim is to demonstrate process automation, service tasks, user tasks, forms, variables, and workflow execution. The workers represent real integrations that ProBuild could later replace with live APIs.

Recommended test variables

{
  "correlationId": "test-001",
  "customerName": "Test Customer",
  "toolId": "DRILL-001",
  "toolAvailable": true,
  "stockAvailable": true,
  "paymentSuccessful": true,
  "financeDecision": "approved",
  "repairApproved": true,
  "tradeCard": false,
  "orderTotal": 150,
  "quantity": 1,
  "routine": true,
  "repair": false,
  "oos": false,
  "passed": true,
  "over50": false,
  "approved": true,
  "confirmed": true
}

What to show in the presentation

- Web Modeler: BPMN and forms
- Tasklist: user tasks completed through forms
- Operate: process instance, variables, and completed jobs
- Java console: workers receiving and completing service tasks
- Evidence folder: screenshots and test results
