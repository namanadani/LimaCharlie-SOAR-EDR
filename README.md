<div align="center">
  <h2>Lima-Charlie edr integration and automation</h2>
</div>
<div align="center">
  <img src="https://github.com/user-attachments/assets/99015181-7014-4409-8cc4-2ff765068727" alt="Description" width="500">
</div>

# Project overview
This project highlights the seamless integration of Security Orchestration, Automation, and Response (SOAR) with Endpoint Detection and Response (EDR) to streamline security workflows and strengthen an organization’s cybersecurity posture. By leveraging **LimaCharlie** for EDR and **Tines** for SOAR, it delivers real-time security insights and automated responses to swiftly tackle threats.
The project focuses on detecting and mitigating credential access attacks using the **LaZagne** tool. When LimaCharlie identifies LaZagne activity on endpoint devices, it instantly triggers alerts and remediation actions. Users can also decide whether to isolate compromised machines, adding a layer of control to automated processes. 
To ensure a fast and effective response, the system integrates with **Slack** and **email** for instant communication, keeping security teams informed and responsive. This combination of automation, real-time detection, and adaptable workflows demonstrates a modern, proactive approach to security operations.
# Tools Used
- <b>Windows Machine</b>: Target machine LimaCharlie will detect for isolation decision, where users can choose to isolate it based on the threat severity.
- <b> LimaCharlie (EDR)</b>: Used to detect and respond to security threats.
- <b>Tines (SOAR)</b>: Automates the security workflows and orchestrates the response actions.
- <b>Slack</b>: Serves as the communication platform to receive alert detections.
- <b>Temp Mail(Email)</b>: Used for temporary email, used for receiving emails from tines.
# Skills Gained 
- **Integrating SOAR with EDR**: Learned how to integrate SOAR tools with EDR platforms to enhance automated incident response and streamline security operations.  
- **Automating Security Workflows**: Gained hands-on experience in designing and implementing automated workflows for real-time threat detection, response, and notifications, simplifying incident handling.  
- **Threat Detection and Response**: Worked with LimaCharlie to detect threats on compromised endpoints and made critical decisions like isolating affected machines based on threat analysis.  
- **Communication and Alerts**: Set up Slack and email integrations to ensure timely alerts and effective communication during incident response, keeping all stakeholders informed.  
- **Interactive User Prompts**: Configured user prompts within the SOAR workflow to enable interactive decision-making during critical stages of incident management.  
- **Incident Response Coordination**: Enhanced skills in managing incident responses across multiple tools and platforms, ensuring efficient and cohesive resolution of security events.  
# Windows Server Virtual Machine
<div align="center">
<img src="https://github.com/user-attachments/assets/cd87f03d-5a1e-44bb-bce4-558de05107d0">
</div>
Windows Server hosted on VMware was used to simulate a real-world environment for testing and validating security workflows. The server acted as an endpoint to deploy LimaCharlie for EDR and run simulated credential access attacks using the LaZagne tool.

# Installing Lima-charlie sensor 
In order to connect the Limacharlie edr and our windows server hosted on vm, we have to install the limacharlie sensor hcp.exe along with it's sensor key.

<div align="center">
  <img src="https://github.com/user-attachments/assets/88052883-76fa-4bbf-9791-174b02fe4ea3">
</div>

We have to install the sensor using administrator privileges in windows powershell. Once, the sensor is installed successfully, we can see it in our limacharlie edr sensor list.

<div align="center">
  <img src="https://github.com/user-attachments/assets/eeae051f-b2ae-429e-b5af-d2dfaf41fac0" >
</div>

We are going to use lazagne for credential access. So, we are going to create a special rule for a custom rule for lazagne in lima-charlie. Also, testing it with previously occured event by lazagne collected by lima-charlie.

<div align="center">
  <img src="https://github.com/user-attachments/assets/981b7958-a0d7-4673-ae54-f24d5a46eea3">
</div>
<b>
Once, running lazagne on command line with "all" option, the event is created by limacharlie.
<div align="center">
  <img src="https://github.com/user-attachments/assets/74160da9-5394-49ee-baf3-489b599e53f2">
</div>
<div align="center">
  <img src="https://github.com/user-attachments/assets/2c75a229-b4e7-4d60-ac7d-834403ab591b">
</div>

# Integrating slack and tines
Create a free [slack](https://slack.com/intl/en-gb) account.
Create a free [tines](https://www.tines.com/).
In tines, create a new story and drag slack application for sending messages fromes tines to slack. In order to send messages and data from tines to slack, the selected channel's id is used. 
<div align="center">
  <img src="https://github.com/user-attachments/assets/9f3402df-8089-4c62-9481-9b0fcc8b53c5">
  <img src="https://github.com/user-attachments/assets/5ecadef3-7e0f-490e-855a-e54ef918c713">
</div>
Once, access is given to tines, we can check whether it will work or not by running the slack in tines. We can see it in the botttom whether tines can send message to slack or not.
<div align="center">
  <img src="https://github.com/user-attachments/assets/0d30f0ce-96bc-493a-8c32-6a9f8ef7b272">
</div>

# Integrating tines and limacharlie
Unlike slack, we have to manually add credential for limacharlie in tines by uploading a jwt key. 
<div align="center">
  <img src="https://github.com/user-attachments/assets/9f943125-6120-4b84-9fe0-4ae33eae5f38">
</div>

# 
Now, when lazagne is run on our windows server, lima-charlie will detect it with the custom rule created. Lima-charlie will further send all the events along with data to tines. Here, in tines only important information are transferred to security team via email and slack. Note: for email i've used a temporary email platform for receiving emails.
<div align="center">
  <img src="https://github.com/user-attachments/assets/3b5af05e-a65a-42b6-80cf-ff4ca0474610">
</div>
Here, in tines only important information are transferred to security team via email and slack. Note: for email i've used a temporary email platform for receiving emails.
<div align="center">
  <img src="https://github.com/user-attachments/assets/b7e8ee96-fe9a-49fe-86a2-a7462ea744e2">
</div>
We can see the information in detailed on slack and on email.
<div align="center">
  <img src="https://github.com/user-attachments/assets/402d63de-e3bc-448a-aa8d-266898b7aea4" meta="slack">
  <img src="https://github.com/user-attachments/assets/446a0451-593a-4bd6-a2a1-c3ac768c87d1" meta="email">
</div>
Overview of event on email.
<div align="center">
  <img src="https://github.com/user-attachments/assets/f6b8e605-8259-4009-9d0b-d6b2005ed791">
</div>
If the security team chooses to see the event in-depth, they can do so, by clicking the link in the bottom of the message for every specific event. If security team wishes to isolate the sensor(machine), they can simply choose yes and isolate sensor application from tines which will be reflected in lima-charlie.
<div align="center">
  <img src ="https://github.com/user-attachments/assets/eca0e0dc-2532-4f70-bd32-571940b25687">
</div>
Further, in windows server, if we try to connect to internet or any other network won't be possible. We can see that by a small demonstration in the below picture in which we tried to ping to google.com which isn't possible because the machine has been isolated.
<div align="center">
  <img src="https://github.com/user-attachments/assets/c400007a-3730-46c5-838c-e8c5f99ee2ad">
</div>
Also, in lima charlie machine status has been changed to isolated.
<div align="center">
  <img src="https://github.com/user-attachments/assets/18de4fb7-8316-4232-b05c-3b20b16ae1b3">
</div>
We also have received a final message on slack regarding machine isolation.
<div align="center">
  <img src="https://github.com/user-attachments/assets/bbbffbad-bcf7-45b4-9a64-78db61bcc4e8">
</div>
If user had selected no in when asked for the action on the machine none of these would happen and will receieve a message on slack instead.
<div align="center">
  <img src="https://github.com/user-attachments/assets/a1b7d484-d6a8-465c-877f-e2d673a0edaa">
</div>

