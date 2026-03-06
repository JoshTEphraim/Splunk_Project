# Splunk SSH Brute Force Detection Lab

## 1. Objective

The project demostrates how Splunk can be used to detect suspicious brute-force attempts, repeated authentication failures and unusual SSH connection attempts. Logs were injested into Splunk and the 
Splunk Processing Language (SPL) was used to query the suspected malicious events.

## 2. Lab Environment

- SIEM: Splunk Enterprise
- Virtualization: VirtualBox or VMWare
- Operating System: Ubuntu
- Log source: SSH Log dataset (ssh_log.json)[https://drive.google.com/drive/folders/1BL-kVlc3yCRcAH8NnDmAyRm_3j_2mNLM]

## 3. Data Ingestion

- Log into Splunk using your credentials
- Click on Apps then go to Search and Reporting
- Select Add Data and proceed to select Upload
- Select the provided SSH log dataset
- Proceed choosing `sourcetype=_json` ( Splunk will autopopulate the fields)
- Index it under new index e.g `ssh_logs`
- Review and click start searching

**Verification search**

```spl
index=ssh_logs | stats count by event_type
```
<img width="1185" height="462" alt="image" src="https://github.com/user-attachments/assets/cd7d818d-38b9-4d68-9247-56e4e8bb7ea1" />

## 4. Detecting Failed Login Attempts

Query used: 

```spl
index=ssh_logs event_type="Failed SSH Login"
| stats count by id.orig_h
```

<img width="1851" height="844" alt="image" src="https://github.com/user-attachments/assets/9713af98-4f9c-4d8b-8386-0d22c04da98b" />

Events are narrowed down to only 305 showing the count of each IP that attempted to login but failed.

To find the top 10 source IP genereting failed logins we will use;

```spl
index=ssh_logs event_type="Failed SSH Login"| stats count by id.orig_h | sort - count | head 10
```
 where: 
   - `stats count by id.orig_h` - Failed login attempts by source IP
   - `sort -count` - Orders result from highest to lowest
   -  `head - 10` - shows only the top 10

<img width="1844" height="675" alt="image" src="https://github.com/user-attachments/assets/4bf90b4a-0d91-4da7-b6e8-7ba7967fddd6" />

The shows multiple failed login attempts from the top most source IPs with `10.0.0.30` being with the higest count (11) followed closely with the others with 9 - 10 counts. 
This can indicate an automated brute-force attack or simply a user typing incorrect passwords.












