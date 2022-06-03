# Keptn + Jenkins when Jenkins Has No Inbound Access

![keptn_private](https://user-images.githubusercontent.com/26523841/171775279-b2254809-1503-4f7a-a4ba-01245f725deb.png)

In this scenario, a user again triggers a Keptn sequence. However Jenkins is deployed on a private network and as such, no inbound connections are allowed.

This setup requires that a kubernetes cluster is available inside the network.

1. Install the [job executor service (JES)](https://github.com/keptn-contrib/job-executor-service)
2. Configure the JES to connect to the Keptn control plane. Can be done via Helm during install.
3. Configure the JES to listen for your `task.triggered` event. JES will periodically poll (outbound) to the Keptn control plane and wait for an event.
4. Create a `job/config.yaml` for the `task.triggered` event ([sample here](job/config.yaml)). Use `curlimages/curl` image and craft a `POST` request which triggers a Jenkins job.


Result: No inbound network calls and Jenkins is still triggered.