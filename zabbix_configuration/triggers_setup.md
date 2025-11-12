Triggers Setup Guide — Zabbix Patient Monitoring System
Overview

This guide explains how to create and configure Zabbix Triggers to automatically detect and flag abnormal heart rate readings for patients.
These triggers help identify when a patient’s condition is critical and display alerts on the dashboard.

Step 1: Go to Trigger Configuration
Log in to your Zabbix Web Interface.
Navigate to:
Configuration → Hosts
Select the host (e.g., Patient-4).
Open the Triggers tab.
Click Create trigger.

Step 2: Define the Trigger Details
Basic Information
Name:
Heart Rate Critical Alert
Severity:
High
Description (optional):
Alerts when the heart rate crosses a dangerous threshold (e.g., >120 bpm).

Step 3: Create the Expression

In the Expression field, click on Add (or use the Expression Constructor):

Select:
Host: Patient-4
Item: custom.heart.rate
Function: last()
Operator: >
Value: 120
The resulting expression should look like:

{Patient-4:custom.heart.rate.last()} > 120
This means: “Trigger an alert if the latest heart rate value for Patient-4 exceeds 120 bpm.”

Step 4: Configure OK Event (Recovery)
You can optionally define when the problem is considered resolved.
For example:
{Patient-4:custom.heart.rate.last()} < 100
That means once the patient’s heart rate drops below 100 bpm, the alert automatically clears.

Step 5: Optional Trigger Tags (for better organization)
Add tags to categorize alerts (useful if you expand your system later):
Tag	Value
patient	4
alert_type	heart_rate
severity	critical

Step 6: Save the Trigger
Click Add or Update.
Your trigger is now active.

Step 7: Test the Trigger
Run the following command in your terminal to simulate patient data:
zabbix_sender -z 172.24.113.11 -s "Patient-4" -k custom.heart.rate -o 150
If your trigger expression is correct:
A red Critical Alert appears on the Zabbix Dashboard or Monitoring → Problems page.
The problem status will automatically change when the value goes below the recovery threshold.

Step 8: View Alerts on Zabbix Dashboard

Go to:
Monitoring → Dashboards
You should now see:
Active alert in red (Critical)
Heart rate graphs spiking at alert value
Trigger summary in the “Active Alerts” widget

Example Trigger Summary
Patient	              Expression	                   Threshold	Severity	Status
Patient-1	{Patient-1:custom.heart.rate.last()} > 120	>120 bpm	  High	    Active
Patient-2	{Patient-2:custom.heart.rate.last()} > 120	>120 bpm	  High	      OK
Patient-3	{Patient-3:custom.heart.rate.last()} > 120	>120 bpm	  High	      OK
Patient-4	{Patient-4:custom.heart.rate.last()} > 120	>120 bpm	  High	    Critical
Patient-5	{Patient-5:custom.heart.rate.last()} > 120	>120 bpm	  High	      OK

Tips
You can copy the same trigger for all patients — just change the host name.
Always test your trigger using zabbix_sender before relying on real data.
Make sure the Item Key (custom.heart.rate) matches exactly with the item name configured in Zabbix.

Example of a Working Expression
{Patient-4:custom.heart.rate.last()} > 120
✅ Triggers an alert when heart rate exceeds 120
🟢 Automatically clears when it drops below recovery threshold (if configured)