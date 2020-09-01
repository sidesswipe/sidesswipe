## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/GetImage.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - Ansible-to-elk.yml
  - Filebeat-config.yml
  - Metricbeat-config.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

The job of the Load balancers is to distribute the incoming traffic among the servers in the pool based on the load balancing algorithm and allows for redundancy and high availability. load balancer can monitor the service status by configuring health check to ensure the traffic is send to the up node. it depends on the load balancer features it can protect against session attack or DDos.

The jump box is used to access and manage devices in a separate security zone. A jump server is a hardened and monitored device that spans two dissimilar security zones and provides a controlled means of access between them. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system configuration.
- Filbeat watches for events in log files or other specified locations. It forwards these events to either Elasticsearch of Logstash.
- Metricbeat records metrics and statistics from the system services running on the server. It forwards these to Elasticsearch or Logstash

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web1     |WebServer | 10.0.0.5   | Linux            |
| Web2     |WebServer | 10.0.0.6   | Linux            |
| ELK      |LogServer | 10.1.0.4   | Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 174.91.102.119

Machines within the network can only be accessed by Jump Box.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |174.91.102.119			|
| NLB      | Yes                 | Internet             |
| Web1     | Yes                 | NLB IP Addr          |
| Web2     | Yes                 | NLB IP Addr          |
| Elk      | Yes                 | 10.0.0.4     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

The playbook implements the following tasks:
Ansible allows you to quickly and easily deploy multi-tier apps. By writing simple playbooks rather than custome code, Ansible allows youto get your system to the state you want it to be in, all with little effort.

The playbook implements the following tasks:

- Create the virtual machine, configure the new ELK VM to connect through your Jump-Box using Docker attatched to the Ansible container, and add peering to your other virtual network connected to the webservers.
- Add ELK to the Ansible hosts file and create a new Ansible playbook to use for your new ELK VM.
- The playbook will download and install Docker on your ELK VM, you then need to download and run the ELK container.
-You then need to configure the ELK security group to allow traffic over port 5601 from the workstation.  
-Verify that you can load the ELK stack server from your browser at `http://[your.VM.IP]:5601/app/kibana`.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output]did not take a screenshot at that time

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- | Machine | Private IP | 
  | Web1    | 10.0.0.5   | 
  | Web2    | 10.0.0.6   | 

We have installed the following Beats on these machines:

These Beats allow us to collect the following information from each machine:
- Filbeat watches for events in log files or other specified locations. It forwards these events to either Elasticsearch of Logstash.
- Metricbeat records metrics and statistics from the system services running on the server. It forwards these to Elasticsearch or Logstash

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the my-playbook.yml file to /etc/ansible/my-playbook.yml.
- Update the hosts file to include [host IP] ansible_python_interpreter=/usr/bin/python3 
- Run the playbook, and navigate to http://40.122.215.184:5601/app/kibana to check that the installation worked as expected.


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

To Download playbook from the internet use:

`curl -O https://URL/playbook-name.yml`

To Update hosts file 
- Open the file with `nano /etc/ansible/hosts`.
    - Uncomment the `[webservers]` header line.
    - Add the internal IP address under the `[webservers]` header.
	- Add the python line: `ansible_python_interpreter=/usr/bin/python3` besides each IP.

To update administrator account for ssh connections

    - Open the file with `nano /etc/ansible/ansible.cfg` and scroll down to the `remote_user` option.
    
    - Uncomment the `remote_user` line and replace `root` with your admin username using this format:
				- `remote_user = <user-name-for-web-VMs>`


To run playbook

`ansible-playbook PATH TO YML FILE/FILENAME.YML 
 



ansible-playbook /etc/ansible/pentest.yml