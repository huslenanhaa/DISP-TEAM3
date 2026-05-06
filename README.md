DISP Team 3 2026 - ProBuild Camunda 8 Submission
Student ID: 22025274

Contents:
1. Camunda-Upload-Resources/
   - probuild-operational-model.bpmn
   - forms/*.form
   Upload these resources into Camunda Web Modeler.

2. Java-Worker-Project/
   - Spring Boot Camunda 8 worker application
   - Run using:
     cd Java-Worker-Project
     mvn spring-boot:run

3. Evidence/
   - Add screenshots here for final submission/demo evidence if needed.

Demo notes:
- The Java worker connects to Camunda 8 SaaS using the credentials in application.yml.
- The BPMN uses Camunda Forms linked by form ID.
- Operate can be used to show completed/running process instances and variables.
- Tasklist can be used to complete user tasks/forms.

Recommended test variables:
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
  "yes": true,
  "no": false,
  "approved": true,
  "declined": false,
  "eligible": true,
  "notEligible": false,
  "collect": true,
  "delivery": false,
  "routine": true,
  "repair": false,
  "oos": false,
  "passed": true,
  "failed": false,
  "under50": true,
  "over50": false,
  "rejected": false,
  "unavailable": false,
  "confirmed": true
}
