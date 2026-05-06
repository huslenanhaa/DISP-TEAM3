# ProBuild Camunda 8 Automation

This is a Camunda 8 Spring Boot worker project for the ProBuild operational model.

## What is included

- `src/main/resources/probuild-operational-model.bpmn` - the ProBuild v6 BPMN model.
- `src/main/resources/forms/*.form` - Camunda Forms used by Tasklist user tasks.
- `src/main/java/com/probuild/automation/workers/*Workers.java` - Camunda external workers using `@JobWorker`.
- `src/main/resources/application.yml` - Camunda SaaS API connection settings.

## Configure Camunda Cloud

The project uses the official Camunda 8.8 `camunda.client.*` configuration:

```yaml
camunda:
  client:
    mode: saas
    auth:
      client-id: ...
      client-secret: ...
    cloud:
      cluster-id: ...
      region: lhr-1
```

Your credentials are already present in `application.yml`. To override them without editing the file, set:

```bash
export ZEEBE_CLUSTER_ID="your-cluster-id"
export ZEEBE_CLIENT_ID="your-client-id"
export ZEEBE_CLIENT_SECRET="your-client-secret"
export ZEEBE_REGION="lhr-1"
```

## Run

```bash
mvn spring-boot:run
```

The app connects to Camunda 8 SaaS and subscribes to all job types used in the BPMN.

By default, automatic deployment is disabled because Camunda SaaS clients need explicit
`CREATE` permission on the `Resource` resource before they can deploy BPMN/forms by API.
Deploy the BPMN and forms manually from Web Modeler, or grant that permission and run:

```bash
mvn spring-boot:run -Dspring-boot.run.arguments=--probuild.deployment.enabled=true
```

If you see `403 Forbidden` with `Insufficient permissions to perform operation 'CREATE' on resource 'RESOURCE'`,
add an Orchestration Cluster authorization for this API client:

- Owner type: `Client`
- Owner ID: your client ID
- Resource: `Resource`
- Resource ID: `*`
- Permission: `CREATE`

## Demo Variables

For a smooth coursework demo, these variables control the main gateways:

- `toolAvailable` - defaults to `true`
- `stockAvailable` - defaults to `true`
- `paymentSuccessful` - defaults to `true`
- `financeDecision` - defaults to `approved`
- `repairApproved` - defaults to `true`

You can enter these through forms or include them when starting a process instance.
