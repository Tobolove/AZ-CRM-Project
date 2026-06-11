# Write-up Comparing VM against App Service

For this project I have to choose between deploying the CMS on a Virtual
Machine or on an App Service. I compare both on costs, scalability,
availability and workflow, and then explain my choice.

### Virtual Machine

With a VM I get a full server, but I also have to set up and manage everything by
myself: THe Python environment, the ODBC, nginx, certificates and the process that keeps the
app running, which can be quite a lot.

- Costs: I pay for the VM every hour it runs, even when nobody visits the site.
  There is no real free option for a web server.
- Scalability: Scaling has to be done here manual. To handle more traffic I have to adjust the size of the VM
  or add more VMs with a load balancer and keep them in sync myself.
- Availability: A single VM is one point of failure. If it goes down, the site is
  down. To make it reliable I would need an extra or backup VMs and a load balancer.
- Workflow: I have to handle it for the whole server: OS updates, installing
  packages, certificates, and restarting the app after every change. This gives a lot
  of control but takes a lot of time.

### App Service

App Service is a more or less managed platform. I just give Azure my code and it provides the
operating system, the Python environment, the web server and HTTPS.

- Costs: There is a free tier option (F1) that is enough for this app, so for a small
  project the cost is basically nearly zero.
- Scalability: Scaling is easy. I can change the plan to scale it up, or
  add instances / use autoscale rules to scale, without managing a load balancer.
- Availability: Azure manages the infrastructure and offers a SLA on the paid
  tiers, with automatic restarts if an instance fails.
- Workflow: Azure takes care of the OS, python environment, web server and certificates.
  Deployment is one command, and I can store all my secrets safely as Application
  Settings (which is how this app gets its SQL, Blob and Microsoft login values).

### My choice: App Service

I chosoe App Service. This CMS is a simple Flask app that does not need any
special control over the OS, so the extra work of a VM is not worth it I think.
App Service is free for this size of app, deploys in only one step, scales easily if i need to and lets
me keep all credentials secure as Application Settings, so it is faster, cheaper and
more reliable for my use case.

### What would change my decision

I would switch to a VM if the app needed more control than App Service allows, more customization for example. For
example, if it required a special library, a custom ODBC or nginx setup,
more processes, or full control over the network and security. In that case the extra effort
of managing a VM would be worth it for the extra control the app would need.