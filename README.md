# Keptn Integration Boilerplate

Handy code snippets to integrate Keptn with your favourite tools. Can't find what you need here? Look at the [Keptn integrations page](https://keptn.sh/docs/integrations/)

## Jenkins

### Usecase: Keptn and Jenkins Deployed in the same network

For example, both Keptn and Jenkins are deployed privately on premise OR keptn and Jenkins are both available publicly.

In other words, inbound comms from Keptn to Jenkins is possible. Keptn is able to send POST requests to trigger a Jenkins Job.

![keptn_jenkins_1](https://user-images.githubusercontent.com/26523841/171759371-9aab309b-7526-4ace-8030-dda23a4ec875.png)

Keptn triggers a Jenkins Pipeline. The webhook service either sends the `task.started` event or let your pipeline build and send it.

[Sample code here](jenkins_same_network).

### Usecase: No Inbound Connections Allowed to Jenkins

![keptn_private](https://user-images.githubusercontent.com/26523841/171775279-b2254809-1503-4f7a-a4ba-01245f725deb.png)

In this scenario, Jenkins does not allow inbound connections. For example where Jenkins is deployed on premise and Keptn is deployed in the cloud.

Here, a component called the job executor service is installed on premise (requires an on-prem Kubernetes cluster). This service polls the Keptn API for `task.triggered` events and when one is "heard", the job executor service starts and execute a `curlimages/curl` container.

The curl command is formatted to trigger the Jenkins pipeline. No inbound communication is required.

Just like the previous scenario, when Jenkins starts, the job sends the `task.started` event. When the job is finished, the job sends the `task.finished` event.

[Sample code here](jenkins_no_inbound_access)

------------------------------------------------------------------------------------
