Patients Hosts Setup — Zabbix Healthcare Monitoring System
Overview

In this phase, we’ll create patient hosts inside Zabbix to represent medical monitoring devices.
Each host (like Patient-1, Patient-2, etc.) will store and display vital signs such as heart rate, device status, and location on your healthcare dashboard.

Step 1: Navigate to Hosts
Log in to your Zabbix Web Interface.
From the top menu, go to:
Configuration → Hosts
Click Create host.

Step 2: Create a Patient Host

For each patient, enter the following details:

Field	                              Example Value	                    Description
Host name	                            Patient-1	       Unique identifier for each patient
Visible name	                        Patient 1	          Display name (optional)
Groups	                                Patients	         Create a new group if not present
Interfaces	                     Agent (127.0.0.1 or dummy IP)	Used for data connection

 Repeat this process for all patients you want to monitor (Patient-1 to Patient-5).
Step 3: Add Custom Items for Heart Rate
After creating each host:
Go to Configuration → Hosts → Patient-1 → Items
Click Create item

Fill in the details below:

Field	                               Example Value
Name	                                Heart Rate
Key	                                 custom.heart.rate
Type	                              Zabbix trapper
Value type	                        Numeric (unsigned)
Units	                                  bpm
Update interval	           (leave empty, trapper items don’t poll)
History storage period	                   7d
Trend storage period	                   90d
Applications	                      Heart Monitoring

Click Add to save the item.
This allows Zabbix to receive external data (like heart rate values) via zabbix_sender.

Step 4: Test Host Data Input

Use the following command in your terminal to send simulated patient data to Zabbix:
zabbix_sender -z 172.24.113.11 -s "Patient-1" -k custom.heart.rate -o 85
If configured correctly, you’ll see output like:
Response from "172.24.113.11:10051": "processed: 1; failed: 0; total: 1"
sent: 1; skipped: 0; total: 
Then check the Latest data section in the Zabbix web interface to confirm that the value has been received.

Step 5: Duplicate Hosts (Optional but Recommended)
Once one host works:
Go back to Configuration → Hosts.

Select your working host (e.g., Patient-1).
Click Clone → Rename it to Patient-2, Patient-3, etc.
Modify host names but keep the same custom.heart.rate item key.
This saves setup time and keeps all hosts identical for testing.

Step 6: Simulate Multiple Patients’ Data
You can send different heart rate values for multiple patients:

zabbix_sender -z 172.24.113.11 -s "Patient-1" -k custom.heart.rate -o 78
zabbix_sender -z 172.24.113.11 -s "Patient-2" -k custom.heart.rate -o 102
zabbix_sender -z 172.24.113.11 -s "Patient-3" -k custom.heart.rate -o 95
zabbix_sender -z 172.24.113.11 -s "Patient-4" -k custom.heart.rate -o 130
zabbix_sender -z 172.24.113.11 -s "Patient-5" -k custom.heart.rate -o 70

After sending these values, you can visualize them on your custom healthcare dashboard.

Step 7: Verify Data in Dashboard

Go to:
Monitoring → Dashboards

Add widgets:
Data Overview — shows live heart rates.
Top N Values — list top 5 patients by heart rate.
Graph — visualize trends for each patient.

Expected Outcome
Patient	Heart Rate (bpm)	Status
Patient-1	78	            Normal
Patient-2	102	           Elevated
Patient-3	95	            Normal
Patient-4	130	          Critical 🚨
Patient-5	70	            Normal

Tips
Use Zabbix trapper items for manual or simulated data input.
Ensure your Zabbix server and agent are communicating properly (port 10051 open).
You can adjust thresholds later in triggers for alert levels.