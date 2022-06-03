# Keptn and Jenkins Deployed on Same Network (inbound connections allowed from Keptn to Jenkins)

![keptn_jenkins_1](https://user-images.githubusercontent.com/26523841/171759371-9aab309b-7526-4ace-8030-dda23a4ec875.png)

> TLDR: [Sample pipeline code here](Jenkinsfile.sample)

This scenario applies when Keptn control plane and Jenkins are on the same network (ie. Keptn can trigger Jenkins).

1. Use the keptn webhook service to listen for the `task.triggered` event
1. Craft a `POST` message to trigger the Jenkins job
1. Delegate sending the `task.started` event to the webhook receiver (Jenkins) (optional - see below)
1. Delegate sending the `task.finished` event to the webhook receiver (Jenkins)

## Started and Finished Events: Webhook service or Jenkins Sends?

Choosing the webhook service to automatically send the `task.started` and `task.finished` events is the easiest solution. In this case, zero modifications are required to the Jenkins job.

However, in this case, the timing of the task is wrong because the time "seen" by keptn is really the time it took to fire the HTTP POST (ie. instant).

You can also let the webhook service send the `task.started` event and delegate the `task.finished` event to the webhook receiver (ie. Jenkins). In which case, a modification is required so the job sends the `task.finished` event back to Keptn.

The benefit of this is that the timing is correct. Time is between firing of the HTTP POST and whenever you send the `task.finished` event.

> Webhook service sending the started event. Jenkins sends finished event. 99% of the time this is the correct setup.

The edge case for this setup is if you have included a start delay on Jenkins. Again, the timing starts when the webhook service fires the POST request. In these cases, you may wish to delegate BOTH `task.started` and `task.finished` events to Jenkins. More modifications required to the pipeline, but you are in complete control of the timings.