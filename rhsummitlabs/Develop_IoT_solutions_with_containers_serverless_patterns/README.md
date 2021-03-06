== App Dev in the Cloud - Agile Cloud Integration with Destinasia

:numbered:

== Overview

Short description: Agile cloud integration with 6 container solution on OCP

Long description: Ready to get hands-on with AppDev in the Cloud with container based services? This
workshop will let you experience the wonders of Red Hat's open technologies for cloud-based container
application development, letting you integrate multiple services in to a polyglot cloud solution. In
this workshop you're a developer working for Destinaisa, a travel agency that needs to setup its online
bookings applications backend services. You'll be given the OpenShift Container Platform, then installing
JBoss BRMS to work in the Destinasia discount rules. Once they are completed, you leverage Ansible playbooks
to see infrastructure automation in action. Each playbook will deploy a new container based service to
support flight, hotel, car and discount rule queries from your application. In total you will be running
6 container based applications or services in a private PaaS before testing this solution with a REST
client, sending a booking and verifying the discounts provided by the rules you implemented.


. This demonstration showcases the following:

* Deploying a multi-layered, agile integration services application on OpenShift Container Platform.
* Deploying JBoss BRMS product with business rules project, exploring and testing business logic.
* Using Ansible playbooks to deploy xPaaS container-based services.
* Using Ansible playbooks to deploy web services in containers (PHP, .Net and Java).
* Using Ansible playbook to deploy xPaaS integration service in a container.
* Testing complete application by submitting RestAPI call to application.

. Goal

* Deploy a complex agile integration application in the Cloud.
* Test integration application with a REST client.

. Prerequisites

* A basic understanding of OpenShift, JBoss BRMS and Ansible playbooks.

Current versions of products used:

[cols="1,1",options="header"]
|=======
|Product |Version 
|`OpenShift Container Platform` |`3.6`
|`JBoss EAP` |`7.0`
|`JBoss BRMS` |`6.4`
|`xPaaS Decision Server` |`6.4`
|`PHP` |`7.0`
|`.NET Core` |`2.0`
|`xPaaS Fuse Integration Service (FIS)` |`2.0`
|=======

=== Environment

The demo environment consists of the following systems:

[cols="3",options="header"]
|=======
|Hostname              |Internal IP    |Description
|`bastion.example.com` |`192.168.0.5`  | Bastion host
|`master.example.com`  |`192.168.0.10` | Master
|`node01.example.com`  |`192.168.0.11` | Node 01
|`node02.example.com`  |`192.168.0.12` | Node 02
|`node03.example.com`  |`192.168.0.13` | Node 03
|`cmfe.example.com`    |`192.168.0.50` | Cloudforms
|=======


NOTE: HAProxy is running on the *workstation* machine.  This provides a level of port forwarding to allow access to the OpenShift console and the JBoss application and other services running on OpenShift to overcome some DNS and routing limitations in the underlying Ravello environment.  This includes port 80, 8443 and 8080-8085.

=== Provision Your Demo Environment

. If you have Red Hat Product Demo System access, log in to the link:https://rhpds.redhat.com/[Red Hat Product Demo System] with your SSO credentials.

. Go to *Services -> Catalogs -> Service Catalogs*.

. Under *All Services -> AppDev in the Cloud*, select *Agile Cloud Integration with Destinasia*.

. On the right, click *Order*.

. Read all of the information on the resulting page, check the necessary box, and click *Submit*.
+
[IMPORTANT]
====
* It takes about 15-20 minutes for the demo to load completely and become accessible.
** Wait for the full demo to load, even if some of its systems are marked "Up."
* Watch for an email with information about how to access your demo environment.
** Make note of the email's contents: a list of hostnames, IP addresses, and your GUID.
** Whenever you see GUID in the demo instructions, replace it with the GUID provided in the email.
* You can get real-time updates of your demo environment at https://www.opentlc.com/rhpds-status.
====
+
[TIP]
Be mindful of the runtime of your demo environment! It may take you longer than the 3 hours allotted to complete the demo, so you may need to extend the runtime. This is especially important in later steps when you are building virtual machines. For information on how to extend runtime and lifetime, see https://www.opentlc.com/lifecycle.

== Getting Started

. From a web browser, open URL below in its own window or tab, using `admin` for the username and `r3dh4t1!` for the password:

* *OpenShift console:* `https://workstation-<YOUR-GUID>.rhpds.opentlc.com:8443`


[TIP]
You can also find these URLs in the email you received when you provisioned the demo environment.


== Review the Environment

. Once the OpenShift environment is up and running, log in to the *OpenShift Enterprise Console* at `https://<IP_ADDRESS_OF_WORKSTATION>:8443/console`, using these credentials:
+
* *Username*: `admin`
* *Password*: `r3dh4t1!`

. Nothing has been installed yet, so no projects have been created yet. You'll do this soon.

=== Access the Destinasia project on workstation (Bastion host)

The project you're using to install the various services that make up the Destinasia application are located on this host.
To access it will require you ssh into as the root user:

 $ ssh root@workstation-<YOUR-GUID>.rhpds.opentlc.com

 $ cd rhcs-destinasia-rules-demo

Here you will find the following structure:

* Dockerfile
* docs/
* init.sh
* installs/
* Readme.md
* support/

You can browse the Readme.md file for details of the contents, but for now you only need to take the first step.
You will be installing the first container, with JBoss BRMS.

=== Build and deploy JBoss BRMS with travel discount rules project

To start a container build and eventual deployment of this project you need only to pass the host name to
the 'init.sh' as follows:

 $ ./init.sh master.example.com

The console will show you the output and just follow along as the project is sent to build on OpenShift.
At the same time, log in to the OpenShift console and watch the build:

 https://workstation-<YOUR-GUID>.rhpds.opentlc.com:8443
 user: admin
 pass: r3dh4t1!

You will find a new project has been created called 'appdev-in-cloud', click on this to view the container builds and
deployments in the rest of this lab. For more details select the 'Monitoring' tab.

The 'init.sh' running in the console will finish with output like this:

 =============================================================================
 =                                                                           =
 =  Login to JBoss BRMS to start developing rules projects, something like:  =
 =                                                                           =
 =  http://workstation-<YOUR-GUID>.rhpds.opentlc.com:8080/business-central   =
 =                                                                           =
 =  [ u:erics / p:jbossbrms1! ]                                              =
 =                                                                           =
 =  Note: it takes a few minutes to expose the service...                    =
 =                                                                           =
 =============================================================================

Note: An online step-by-step lab is available, see this for details and screenshots of
this installation:

`https://appdevcloudworkshop.github.io/lab02.html`

==== Explore the Destinasia discount rules project
View online step-by-step lab for this section of the workshop containing details and screenshots for
exploring the project:

`https://appdevcloudworkshop.github.io/lab03.html`


=== Ansible playbooks for container deployment automation
The backend services for Destinasia are deployed using Ansible automation toolling, specifically Ansible
playbooks. They are found in the following directory:

 $ cd support/playbooks/deploy-ocp-services

You will find the playbooks wrapped into individual scripts:

 - ansible-playbook-dotnetservice.sh
 - ansible-playbook-fuseservice.sh
 - ansible-playbook-javaservice.sh
 - ansible-playbook-phpservice.sh
 - ansible-playbook-ruleservice.sh

==== Deploy xPaaS rule service
Run the wrapper to leverage Ansible playbook for deployment of an xPaaS decision server that extracts the
business rules from the previously installed container:

 $ ./ansible-playbook-ruleservice.sh

If you followed the first steps to setup the Destinasia Travel Rules on OpenShift Container Platform,
the following will install the Travel Discount ruleservice now...

In the OpenShift console you can watch the deployment unfold in the project 'appdev-in-cloud'.

Note: An online step-by-step lab is available, see this for details and screenshots of
this installation:

`https://appdevcloudworkshop.github.io/lab04.html`


==== Deploy Java flight service
Run the wrapper to leverage Ansible playbook for deployment of a Java flight reservation web service:

 $ ./ansible-playbook-javaservice.sh

If you followed the first steps to setup the Destinasia Travel Rules on OpenShift Container Platform,
the following will install the Flights javaservice now...

In the OpenShift console you can watch the deployment unfold in the project 'appdev-in-cloud'.

Note: An online step-by-step lab is available, see this for details and screenshots of
this installation:

`https://appdevcloudworkshop.github.io/lab05.html`

==== Deploy .Net car service
Run the wrapper to leverage Ansible playbook for deployment of a .Net car rental web service:

 $ ./ansible-playbook-dotnetservice.sh

If you followed the first steps to setup the Destinasia Travel Rules on OpenShift Container Platform,
the following will install the Car dotnetservice now...

In the OpenShift console you can watch the deployment unfold in the project 'appdev-in-cloud'.

Note: An online step-by-step lab is available, see this for details and screenshots of
this installation:

`https://appdevcloudworkshop.github.io/lab06.html`

==== Deploy PHP hotel service
Run the wrapper to leverage Ansible playbook for deployment of a PHP hotel reservation web service:

 $ ./ansible-playbook-phpservice.sh

If you followed the first steps to setup the Destinasia Travel Rules on OpenShift Container Platform,
the following will install the Hotel phpservice now...

In the OpenShift console you can watch the deployment unfold in the project 'appdev-in-cloud'.

Note: An online step-by-step lab is available, see this for details and screenshots of
this installation:

`https://appdevcloudworkshop.github.io/lab07.html`

==== Deploy Fuse agile integration service
Run the wrapper to leverage Ansible playbook for deployment of a Fuse xPaaS integration service:

 $ ./ansible-playbook-fuseservice.sh

If you followed the first steps to setup the Destinasia Travel Rules on OpenShift Container Platform,
the following will install the integration  now...

In the OpenShift console you can watch the deployment unfold in the project 'appdev-in-cloud'.

Note: this container takes the longest to fully build and deploy due to extensive Maven dependency downloads that need
to complete before the integration service can build. Watch the container log for realtime progress found in the
OpenShift console:

 Select project 'appdev-in-cloud' -> locate Application 'fusetravelagency' -> open details of container by clicking
 on the left down arrow -> see log of build progress in bottom right of window that is opened

Note: An online step-by-step lab is available, see this for details and screenshots of
this installation:

`https://appdevcloudworkshop.github.io/lab08.html`

=== Test application
Use a browser REST client to ping the xPaaS Fuse endpoint with as explained in the readme file found
here, just view in console for the details:

 $ cat support/playbooks/deploy-ocp-services/Readme.md

When the Fuse container has fully deployed, you should get a valid REST response as described in the readme file above.

Note: An online step-by-step lab is available, see this for details and screenshots of
this installation:

`https://appdevcloudworkshop.github.io/lab09.html`

== Conclusion
This concludes the demo workshop for this AppDev in the Cloud example application.
