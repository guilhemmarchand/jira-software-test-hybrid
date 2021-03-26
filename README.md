# README

- Use VSCode ideally
- Start the containers:

``
docker-compose up -d
``

## SPLUNK

Wait a a few dozens of seconds, the Splunk instances are available at:

- https://localhost:8000 (remote search head)
- https://localhost:8001 (hybrid search head)

login: admin
pass: ch@ngeM3

Go in settings and re-enter the credentials in distributed search (Settings / Distributed Search)

Both instances are forwarding to a third Splunk instance acting as an indexer.

## JIRA

Access JIRA via the nginx SSL reverse proxy:

https://localhost:8081

- Get a trial for Jira core

--> "Set it up for me"
--> once connected, seletc Jira Software in the dropdown list, then Jira Software (Data Center)
--> A trial is automatically inserted in the JIRA container, since we use a local volume, every JIRA data is preserved
--> Setup an admin account
--> Wait for the end of the process
--> You may end up with an empty white error page, no worries, just refresh at the root URL after 5 minutes to let time enough for the initialisation of JIRA
--> logs can be accessed easily within the volume

Once JIRA is ready, follow the process and create a new project. (Basic software development for instance)

At the end, a fully working JIRA instance is ready, from the Splunk instance, we will join the JIRA via :

https://nginx:8081

(For Splunk Cloud vetting purposes, non SSL connections are not allowed)

## Connect the hybrid search head to JIRA

- Open the JIRA Addon, go to settings
- Add the index:

nginx:8081 (disable SSL verification)

- Run a Get project to verify the connectivity.
