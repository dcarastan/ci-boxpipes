README
------
`ci-boxpipes` is a collection of basic concourse CI pipelines pipelines purposely written with no external task dependencies. Main purpose of it is to showcase simple container based workflows for Erlang and Python applications. Resulting CPU load is not too big, which makes perfect for running them locally using a [Concourse in a box](https://github.com/dcarastan/concourse-docker) deployment

Pipelines
---------
### chatbus

Chatbus is a containerized Erlang application build and deploy exercise. It starts with building the official Erlang container, augments the image with a couple of tools then builds the application container. Resulting container is then used  for deployment, allowed to run for a bit then teared down. Pipeline also has a plain old blob deployment path that can be triggered manually. To make it more realistic, deployment runs in a separate VM instance.

### flaskapp

This builds and deploys the docker-compose flask app example on a remote VM instance. Deployment is validated with a simple curl command to verify that it is up an running. Teardown occurs when the test passes.

### dr_check

Performs periodic docker registry container list queries. Pipeline shows what it takes to trigger a run at a certain time interval and serves as a docker registry monitoring watchdog.

Usage
-----
Pipelines can be deployed using the `ci/sp` script and destroyed using the `ci/dp` script as well as manually using Concourse's `fly` tool. The scripts assume that you have the `.` target defined and pointing to the intended Concourse server. Note that the `ci/dp` script exposes the pipelines for public view. The `dr_check` pipeline is also set as public, means it can be triggered by anyone.
