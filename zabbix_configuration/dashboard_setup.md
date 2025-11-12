Zabbix Dashboard Setup Guide
Overview
This guide explains how to create and customize a Zabbix Dashboard to monitor real-time heart rate data from multiple patients in a healthcare IoT system.

Step 1: Login to Zabbix
Open your browser and go to your Zabbix web interface:
http://<ZABBIX_SERVER_IP>/zabbix
Log in using your admin credentials:
Username: Admin
Password: (your configured password)

Step 2: Access the Dashboard Section
In the left-side menu, click Monitoring → Dashboards.
Click the Create dashboard button.
Name your dashboard something meaningful, e.g.:
Patient Monitoring Dashboard

Step 3: Add Widgets to Display Data
You can add different widgets to visualize heart rate data and trigger alerts.
(A) Graph Widget — Patient Heart Rate
Click Add Widget → select Graph (classic).
Title: Patient-1 Heart Rate
Host: Patient-1
Item: custom.heart.rate
Set time period to Last 1 hour or Last 24 hours.
Save it.
Repeat the same for Patient-2, Patient-3, etc.

(B) Trigger Overview Widget — Active Alerts
Click Add Widget → choose Triggers.
Title: Active Alerts
Filter by severity: Warning and above.
Show status: Problem.
Click Apply.
This will show active alerts like high heart rate (e.g., >120 bpm).

(C) Data Overview Widget
Add Widget → choose Data Overview.
Title: Patient Heart Rate Summary
Add hosts: All patients (Patient-1 to Patient-5).
Select item key: custom.heart.rate.
Save.
This gives a quick summary of all patient heart rates on one screen.

(D) Plain Text Widget — Recent Updates
Add Widget → Plain Text.
Title: Recent Heart Rate Updates
Add items:
/Patient-1/custom.heart.rate
/Patient-2/custom.heart.rate
/Patient-3/custom.heart.rate
/Patient-4/custom.heart.rate
/Patient-5/custom.heart.rate
Click Apply.

Step 4: Test and Verify Alerts
Use these commands to simulate data from each patient node:
zabbix_sender -z 172.24.113.11 -s "Patient-4" -k custom.heart.rate -o 150
If your trigger threshold is configured (e.g., >120), you’ll see a red alert appear in:
Dashboard → Triggers widget
Monitoring → Problems

Step 5: Customize Layout
Resize widgets to show graphs side-by-side.
Arrange “Active Alerts” at the top for quick visibility.
Add the hospital or project logo for presentation.

Step 6: Save and Share
Click Save Dashboard.
(Optional) Share it with your teammates:
Click Sharing settings → Add user group → Everyone (read-only).
Done! Your live IoT health monitoring dashboard is ready to demonstrate.

Tips
Use different colors for different patient graphs for better visibility.
You can add Trigger severity color coding for easy identification:
🟢 Normal (OK)
🟡 Warning
🔴 Critical