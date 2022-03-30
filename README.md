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

Adding sample web log data to Kibana.

![alt text](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-rochoabanuelos/blob/main/EXPLORING%20KIBANA/EXPLORING%20KIBANA%20-%201.PNG?raw=true)

- In the last 7 days, there was 249 unique visitors located in India.

![alt text](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-rochoabanuelos/blob/main/EXPLORING%20KIBANA/EXPLORING%20KIBANA%20-%202.PNG?raw=true)

- In the last 24 hours, of the visitors from China, 8 were using Mac OSX.

![alt text](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-rochoabanuelos/blob/main/EXPLORING%20KIBANA/EXPLORING%20KIBANA%20-%203.PNG?raw=true)

- In the last 2 days, what percentage of visitors received 404 errors were 7.5% and 2.5% for 503 errors.

![alt text](Diagram/ELK-DIAGRAM.png)

- In the last 7 days, China produced the majority of the traffic on the website at 264 unique visitors.

![alt text](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-rochoabanuelos/blob/main/EXPLORING%20KIBANA/EXPLORING%20KIBANA%20-%204.PNG?raw=true)

- Of the traffic that's coming from that country, 11:00AM to 13:00 had the highest amount of activity.

![alt text](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-rochoabanuelos/blob/main/EXPLORING%20KIBANA/EXPLORING%20KIBANA%20-%205.PNG?raw=true)

- Below are all the types of downloaded files the past 7 days and a short description.

- gz: Are compressed files created using the gzip compression utility.

- css: Are files that can define font, size, color, spacing, border and location of HTML information on a webpage.

- zip: A lossless compression format. Can contain one or more files or directories that have been compressed.

- deb: A Debian (Linux) Software Package file. These files are installed when using the apt package manager.

- rpm: A Red Hat Software Package file. RPM stands for Red Hat Package Manager.

![alt text](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-rochoabanuelos/blob/main/EXPLORING%20KIBANA/EXPLORING%20KIBANA%20-%206.PNG?raw=true)

### Unique Visitors Vs. Average Bytes.
- 15:00 to 21:00 time frame in the last 7 days seems to have the most amount of bytes (activity).

![alt text](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-rochoabanuelos/blob/main/EXPLORING%20KIBANA/EXPLORING%20KIBANA%20-%207.PNG?raw=true)

- We can see one visitor with usually high activity.

![alt text]

- Filter the data by this event.

![alt text]

- What is the timestamp for this event is 14:58

![alt text]

- The type of file downloaded is .gz file.

![alt text]

- The country this activity originated from is China.

![alt text]

- What HTTP response codes were 200 OK.

![alt text]

- On the Kibana Discover page we can see more details about this activity.

![alt text]

- The source IP address of this activity is 

![alt text]

- The geo coordinates of this activity is

![alt text]

- The OS that the source machine was running is

![alt text]

- The full URL that was accessed

![alt text]

- The website that the visitor's traffic originated from

![alt text]

### Finish your investigation with a short overview of your insights.
- What do you think the user was doing?
  
  I believe that the visitor may be trying to access and download archive files as indicated by the tar.gz file type from the Elastic downloads section.

- Was the file they downloaded malicious? If not, what is the file used for?

  Does not seem is malicious. It is an compressed file from the ‘downloads’ section for the software.

- Is there anything that seems suspicious about this activity?

  Can’t confirm if activity is suspicious. Visitor can just be downloading the software to work with on their workstation.

- Is any of the traffic you inspected potentially outside of compliance guidelines?

  Based on the data given, the traffic seems evenly distributed with high spikes during normal peak hours of the day. The spike samples that were investigated seem normal behavior often referred from Facebook.
