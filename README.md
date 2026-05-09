# ProBuild Process Modelling and Automation

**DISP Team 3 2026 |

This repository contains the portfolio submission for the ProBuild Supplies Ltd case study. The project models ProBuild as a socio-technical system and then develops the process into strategic BPMN, operational BPMN, Camunda Forms, and Camunda 8 automation.

The final automation uses **Camunda 8 SaaS** with a **Java Spring Boot external worker application**. Camunda Forms capture user input, BPMN service tasks create Zeebe jobs, and Java workers complete those jobs through matching `@JobWorker` methods.

---

## Project Scope

The project covers the following ProBuild business areas:

| Area | Included Process Work |
|---|---|
| Retail sales | Customer order, stock check, payment and order confirmation |
| Tool hire | Hire request, tool availability, deposit/payment and return flow |
| Warehouse | Stock updates, order fulfilment, IMS synchronisation |
| Finance | Credit checks, finance approval, repayment handling |
| FixPro repairs | Tool maintenance, repair reports and approval handling |
| Suppliers | Delivery and stock replenishment support |

---

## Portfolio Evidence

| Marking Area | Repository Evidence |
|---|---|
| Socio-technical model | `Socio-Technical-Model` |
| Strategic BPMN | `Strategic-BPMN` |
| Operational BPMN | `Operational-BPMN` |
| Camunda deployment resources | `Camunda-Upload-Resources` |
| Camunda Forms | `Camunda-Upload-Resources/forms` |
| Java automation workers | `Java-Worker-Project` |
| Testing evidence | `Evidence` |
| Configuration management | GitHub repository, commits and README |

---

## Main Folders

### `Socio-Technical-Model`

Contains the i* socio-technical model, including the visual model and source text file.

### `Strategic-BPMN`

Contains the high-level strategic BPMN model showing the business process before technical automation detail.

### `Operational-BPMN`

Contains the detailed operational BPMN model used for automation, including service tasks, user tasks, gateways, pools and message flows.

### `Camunda-Upload-Resources`

Contains the BPMN and Camunda Forms that can be uploaded to Camunda Web Modeler.

### `Java-Worker-Project`

Contains the Spring Boot application that connects to Camunda 8 and executes external workers using `@JobWorker`.

### `Evidence`

Contains the testing evidence, including test strategy, test cases, expected results, actual results and defects identified.

---

## Automation Design

The operational process follows this automation flow:

```text
Camunda Form
    ↓
BPMN User Task
    ↓
Process Variables
    ↓
BPMN Service Task
    ↓
Zeebe Job Type
    ↓
Java @JobWorker
    ↓
Variables returned to Camunda
    ↓
Gateway / Next Process Step
```

Service tasks in the BPMN are connected to Java workers by matching the BPMN job type with the Java `@JobWorker` annotation.

Example:

```java
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
```

---

## Running the Java Worker

Open a terminal and navigate to the worker project:

```bash
cd Java-Worker-Project
```

Run the Spring Boot application:

```bash
mvn spring-boot:run
```

The worker application must remain running while process instances are tested in Camunda.

---

## Deploying to Camunda 8

Upload the following BPMN file to Camunda Web Modeler:

`Camunda-Upload-Resources/probuild-operational-model.bpmn`

Upload the forms from:

`Camunda-Upload-Resources/forms`

Deploy the BPMN and forms to the Camunda 8 cluster, then start a new process instance and monitor it in Camunda Operate.

---

## Example Test Variables

```json
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
```

---

## Testing

Testing evidence is stored in the `Evidence` folder.

Testing covers:

- BPMN deployment
- Camunda Form validation
- Variable passing
- Gateway decision paths
- Java worker execution
- Completed process instances in Camunda Operate
- Defects and fixes found during deployment

---

## Authors

**DISP Team 3**  

