# Keptn Integration Boilerplate

Handy code snippets to integrate Keptn with your favourite tools. Can't find what you need here? Look at the [Keptn integrations page](https://keptn.sh/docs/integrations/)

## Jenkins

### Usecase: Keptn and Jenkins Deployed in the same network

For example, both Keptn and Jenkins are deployed privately on premise OR keptn and Jenkins are both available publicly.

In other words, inbound comms from Keptn to Jenkins is possible. Keptn is able to send POST requests to trigger a Jenkins Job.

![keptn_jenkins_1](https://user-images.githubusercontent.com/26523841/171759371-9aab309b-7526-4ace-8030-dda23a4ec875.png)

Keptn triggers a Jenkins Pipeline. The webhook service either sends the `task.started` event or let your pipeline build and send it.

[Sample code here](Jenkinsfile.sample).
