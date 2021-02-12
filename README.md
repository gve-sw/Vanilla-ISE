# Vanilla ISE
#### Your endpoint specialists' go-to UI <img src="img/ISE logo.png">
## The Challenge

Cisco ISE (Identity Services Engine) is THE policy engine for your network. It provides many (many) different services that are all required to meet today's user expectations while protecting the organization from threats:
* TACACS/Radius for central management of networking equipment.
* Network Admission Control (NAC) identifying endpoints as they connect to the network (both wired and wireless).
* Group-based Policy using Cisco TrustSec.
* VPN policy with Cisco ASA/FTD.
* Guest lifecycle management.
* Device profiling.
* And more...

While Cisco ISE's richness of features and capabilities is highly appreciated by networking and security experts, endpoint technicians and helpdesk representatives prefer a simpler, limited GUI for their day-to-day tasks.

A specific capability asked by endpoint teams is the concept of a "voucher": a time-limited access token, given to a specific endpoint in order to grant immediate network access (while bypassing security checks) for a distressed user, allowing the technicians to remediate gaps in the endpoint's posture later.

## The Solution

Using Cisco ISE's open APIs, primarily ERS (External RESTful Services), we have created "Vanilla ISE": a simple UI for endpoint technicians and helpdesk representatives.

### Vanilla ISE's Capabilities:
* Query a network device for current authentication sessions.
* Query a specific endpoint for details (status, NAD's IP and interface, authentication mechanism, username, and failure reason - if failed)
* Grant and revoke network access "vouchers".


## Running vanilla ISE:

There are several options for running vanilla ISE:
1. Running the code on a computer/server with Python. Probably the easiest, but a waste of resources.
2. Running the code on a Docker container. Requires to <a href="https://docs.docker.com/get-docker/"> install Docker</a>.
3. Running the code on a Cisco device using Guestshell (Cisco Guestshell is a virtualized Linux-based environment, designed to run custom Linux applications, including Python for automated control and management of Cisco devices). See details below.

### Enable ISE ERS API

The ISE REST APIs (AKA External RESTful Services or ERS) are disabled by default for security. You must enable it:
1. Login to your ISE PAN using the admin or other SuperAdmin user.
2. Navigate to **Administration** > **System** > **Settings** and select **ERS Settings** from the left panel.
4. Enable the ERS APIs by selecting **Enable ERS for Read/Write**
5. Do not enable CSRF unless you know how to use the tokens.
6. Select **Save** to save your changes.

Note: its good practice to disable CSRF to make sure you are able to authenticate successfully.

<a href="https://community.cisco.com/t5/security-documents/ise-ers-api-examples/ta-p/3622623#toc-hId--623796905"> Reference to official documentation </a>

### Set a environment variables file
```
ISE_IP= <ISE hostname/IP>
ISE_USER= <ISE username>
ISE_PASS= <ISE password>
SWITCH_USER= <username for network devices>
SWITCH_USER= <password for network devices>
SWITCH_ENABLE= <enable password for network devices>
```

### Create a Docker image
`docker build -t vanilla_ise .`

### Run the Docker
`docker run -d --env-file <path to env file> -v <path to data dir>:/Cisco-ISE-Email-Notifications/data vanilla_ise`

running the Docker in interactive mode:
`docker run -ti --env-file <path to env file> -v <path to data dir>:/Cisco-ISE-Email-Notifications/data vanilla_ise`


## Screenshots:


----
### Licensing info
Copyright (c) 2020 Cisco and/or its affiliates.

This software is licensed to you under the terms of the Cisco Sample
Code License, Version 1.1 (the "License"). You may obtain a copy of the
License at

               https://developer.cisco.com/docs/licenses

All use of the material herein must be in accordance with the terms of
the License. All rights not expressly granted by the License are
reserved. Unless required by applicable law or agreed to separately in
writing, software distributed under the License is distributed on an "AS
IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express
or implied.
