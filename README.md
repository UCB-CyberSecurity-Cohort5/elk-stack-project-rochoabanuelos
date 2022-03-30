# ELK-Stack-Project

The files in this repository were used to configure the network depicted below.

![alt text](Diagram/ELK-DIAGRAM.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Playbook file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-rochoabanuelos/blob/b4f5600461c4c13980b7a37bd67b7b4d972b02fa/Ansible/elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting traffic to the network.

Load balancers protect against Denial of Service (DoS) Attacks. 

Jump box can act as a gateway router to control access to other machines on a network by allowing approved IP addresses.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network traffic and system logs.

- Filebeat monitors log files, collects log events for updates and sends to Elasticsearch or Logstash.

- Metricbeat periodically collects metrics and statistics to send to Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.7   | Linux            |
| WEB1     | SERVER   | 10.0.0.5   | Linux            |
| WEB2     | SERVER   | 10.0.0.6   | Linux            |
| WEB3     | SERVER   | 10.0.0.10  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 98.224.12.22

Machines within the network can only be accessed by the Ansible Container.
- The only machine allowed to access the ELK machine is the Jump-Box VM.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |     No              | 98.224.12.22         |
| ELK VM   |     No              | 10.0.0.7             |
| WEB1     |     No              | 10.0.0.7             |
| WEB2     |     No              | 10.0.0.7             |
| WEB3     |     No              | 10.0.0.7             |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it will do the exact same thing every time it is ran.

The playbook implements the following tasks:
- Installs docker.io
- Installs pip3
- Installs Docker Python module
- Downloads and launches docker elk container
	- downloads image sebp/elk:761
	- sets restart_policy: always
	- sets published_ports: 5601:5601, 9200:9200, 5044:5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![alt text](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-rochoabanuelos/blob/main/IMAGES/10%20-%201%20SHH%20INTO%20ELK%20AND%20VERIFY%20DOCKER%20INSTALL.PNG?raw=true)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- WEB1: 10.0.0.5
- WEB2: 10.0.0.6
- WEB3: 10.0.0.10

We have installed the following Beats on these machines:
- WEB1, WEB2, WEB3 all have Filebeat and Metricbeat installed an configured to output to elasticsearch using ELK server’s IP address.

These Beats allow us to collect the following information from each machine:
-	Filebeat collects log events such as web logs indicating GET requests over HTTP. 
-	Metricbeat collects system and services running on the server’s metrics, such as CPU usage, Memory usage, Disk usage, Network I/O (in bytes).

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/filebeat/.

- Update the filebeat-config.yml file to include ELK server’s IP address.

- Run the playbook, and navigate to Kibana using ELK server to check that the installation worked as expected.
- The URL you use to navigate in order to check that the ELK server is running is http://20.231.2.88:5601/app/kibana 

**Bonus**
In order to download the playbook, update the files, etc. run this in ansible container:
curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat >> /etc/ansible/filebeat-config.yml 

## Exploring Kibana

1.	Adding sample web log data to Kibana.

[PHOTO]

2.	Answer the following questions:
o	In the last 7 days, there was 249 unique visitors located in India.

[PHOTO]

o	In the last 24 hours, of the visitors from China, 8 were using Mac OSX.


[PHOTO]

o	In the last 2 days, what percentage of visitors received 404 errors were 7.5% and 2.5% for 503 errors.

[PHOTO]

o	In the last 7 days, China produced the majority of the traffic on the website at 264 unique visitors.

[PHOTO]

o	Of the traffic that's coming from that country, 11:00AM to 13:00 had the highest amount of activity.

[PHOTO]

o	Below are all the types of downloaded files the past 7 days and a short description.

o	gz: Are compressed files created using the gzip compression utility.

o	css: Are files that can define font, size, color, spacing, border and location of HTML information on a webpage.

o	zip: A lossless compression format. Can contain one or more files or directories that have been compressed.

o	deb: A Debian (Linux) Software Package file. These files are installed when using the apt package manager.

o	rpm: A Red Hat Software Package file. RPM stands for Red Hat Package Manager.

[PHOTO]

3.	Unique Visitors Vs. Average Bytes.
o	15:00 to 21:00 time frame in the last 7 days seems to have the most amount of bytes (activity).

[PHOTO]

o	We can see one visitor with usually high activity.

[PHOTO]

4.	Filter the data by this event.

[PHOTO]

o	What is the timestamp for this event is 14:58

[PHOTO]

o	The type of file downloaded is .gz file.

[PHOTO]

o	The country this activity originated from is China.

[PHOTO]

o	What HTTP response codes were 200 OK.

[PHOTO]

5.	On the Kibana Discover page we can see more details about this activity.

[PHOTO]

o	The source IP address of this activity is 

[PHOTO]

o	The geo coordinates of this activity is

[PHOTO]

o	The OS that the source machine was running is

[PHOTO]

o	The full URL that was accessed

[PHOTO]

o	The website that the visitor's traffic originated from

[PHOTO]

6.	Finish your investigation with a short overview of your insights.
o	What do you think the user was doing?
I believe that the visitor may be trying to access and download archive files as indicated by the tar.gz file type from the Elastic downloads section from the Columbian site.

o	Was the file they downloaded malicious? If not, what is the file used for?

Does not seem is malicious. It is an compressed file from the ‘downloads’ section for the software.

o	Is there anything that seems suspicious about this activity?

Can’t confirm if activity is suspicious. Visitor can just be downloading the software to work with on their workstation.

o	Is any of the traffic you inspected potentially outside of compliance guidelines?

Based on the data given, the traffic seems evenly distributed with high spikes during normal peak hours of the day. The spike samples that were investigated seem normal behavior often referred from Facebook.
