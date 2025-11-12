# 🏥 Healthcare IoT Monitoring System using Zabbix

This project demonstrates a hospital monitoring dashboard where patient vitals (heart rate) are monitored in real time using **Zabbix**.  
When abnormal readings occur, alerts are displayed on the dashboard.

---

## 🚀 Features
- Monitors 5 patient devices (`Patient-1` to `Patient-5`)
- Displays live heart rate using `custom.heart.rate`
- Shows top 5 patients by heart rate
- Alerts on **heart rate > 120 bpm**
- Custom hospital room map visualization
- Dashboard-only alerts (no external messaging)

---

## ⚙️ Tools & Technologies
- **Zabbix Server & Frontend**
- **Zabbix Sender**
- **Linux (Ubuntu/WSL)**
- Optional: **SNMP Simulator (for device emulation)**

---

## 🩺 Setup Steps Summary
1. Create hosts in Zabbix for 5 patients.
2. Add an item:
   - Key: `custom.heart.rate`
   - Type: Zabbix trapper
3. Send data using:
   ```bash
   zabbix_sender -z <zabbix-server-ip> -s "Patient-1" -k custom.heart.rate -o 85
