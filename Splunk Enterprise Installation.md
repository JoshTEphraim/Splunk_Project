# Splunk Enterprise Installation

## Objective

The objective of this task is to configure Splunk on an Ubuntu machine. By completing this task, you will have Splunk up and running to collect and analyze security logs.

### Lab Setup
***

**Requirements**

**System:** _Ubuntu 22.04 / 20.04 (Server or Desktop)_
**Tools Required**: _Splunk Enterprise (Free version for local setup)_
**Terminal** _(Command Line Access)_

## Steps to Install and Configure Splunk on Ubuntu


### Task 1: Download Splunk

- Open Terminal and download Splunk using wget:

```bash
wget -O splunk-9.3.0-51ccf43db5bd-linux-2.6-amd64.deb "https://download.splunk.com/products/splunk/releases/9.3.0/linux/splunk-9.3.0-51ccf43db5bd-linux-2.6-amd64.deb"
```

- Once downloaded, install Splunk:

```bash
sudo dpkg -i splunk-9.3.0-51ccf43db5bd-linux-2.6-amd64.deb
```

### Task 2: Enable Splunk as a Service

- Move to the Splunk installation directory:

```bash
cd /opt/splunk/bin
```

- Accept the license agreement and enable Splunk at boot:

```bash
sudo ./splunk enable boot-start --accept-license
```

- Start Splunk:

```bash
sudo ./splunk start
```

- When prompted, set up an admin username and password.

### Task 3: Access Splunk Web Interface

- Open a web browser and go to:

```bash
http://<your-ubuntu-ip>:8000
```

- Log in with the admin credentials created earlier.

**Conclusion**

Successfully installed Splunk on an Ubuntu machine.
Configured Splunk as a service and enabled auto-start.
