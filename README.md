# Keptn Integration Boilerplate

Handy code snippets to integrate Keptn with your favourite tools. Can't find what you need here? Look at the [Keptn integrations page](https://keptn.sh/docs/integrations/)

## Jenkins

### Usecase: Jenkins has a public IP and Keptn can trigger Jenkins Jobs

![keptn_jenkins_1](https://user-images.githubusercontent.com/26523841/171759371-9aab309b-7526-4ace-8030-dda23a4ec875.png)

Keptn triggers a Jenkins Pipeline. The webhook service either sends the `task.started` event or let your pipeline build and send it.

[Sample code here](Jenkinsfile.sample).
