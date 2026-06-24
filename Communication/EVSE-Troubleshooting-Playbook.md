# 🚨 EVSE Troubleshooting Playbook

> Complete NOC Engineer & EVSE Support Engineer Troubleshooting Guide for AC Chargers, DC Chargers, OCPP, PLC Communication, CCS Charging, and Field Fault Analysis.

---

## 🛠️ Purpose

This playbook provides a structured approach to troubleshoot:

* AC Chargers
* DC Chargers
* OCPP Issues
* Charging Failures
* Communication Failures
* Hardware Faults
* Customer Complaints
* EV Suspended / EVSE Suspended
* CCS Communication Problems

---

# 🔄 Standard Troubleshooting Workflow

```text
Alarm Received
      │
      ▼
Check Charger Status
      │
      ▼
Review OCPP Logs
      │
      ▼
Identify Fault Category
      │
      ▼
Check Hardware Signals
      │
      ▼
Perform RCA
      │
      ▼
Resolve Issue
      │
      ▼
Monitor Charger
```

---

# 📊 Fault Classification

| Category        | Examples                  |
| --------------- | ------------------------- |
| Communication   | OCPP Offline, PLC Failure |
| Vehicle Related | EV Suspended              |
| Charger Related | EVSE Suspended            |
| Power Related   | Contactor Fault           |
| Hardware        | Gun Overheating           |
| Safety          | Insulation Fault          |
| Network         | SIM Failure               |
| Software        | Firmware Bug              |

---

# 🔌 Charger Not Available

## Symptoms

```text
OCPP Status = Unavailable
```

## Possible Causes

* Charger disabled from CMS
* Firmware issue
* Internal fault
* Maintenance mode

## Checks

* Heartbeat messages
* Charger logs
* CMS commands

## Resolution

* Reboot charger
* Verify backend status
* Check firmware health

---

# 🌐 OCPP Offline

## Symptoms

```text
Heartbeat Missing
```

## Possible Causes

* Network failure
* SIM issue
* DNS issue
* Backend unreachable

## Troubleshooting

### Step 1

Check:

```text
Ping Backend
```

### Step 2

Verify:

```text
WebSocket Connection
```

### Step 3

Check:

```text
SIM Signal
APN Configuration
```

---

# ⚡ Charging Not Starting

## Symptoms

```text
Preparing
```

but charging never begins.

## Possible Causes

* EV issue
* Authentication issue
* CP issue
* PP issue
* PLC issue

## Checks

* CP Voltage
* PP Resistance
* OCPP Authorize
* StartTransaction

---

# 🔌 CP Communication Failure

## Symptoms

```text
Vehicle Not Detected
```

## Expected CP States

| Voltage | State |
| ------- | ----- |
| 12V     | A     |
| 9V      | B     |
| 6V      | C     |

## Possible Causes

* CP Wire Damage
* Control Board Fault
* Connector Fault

---

# 🔥 Gun Overheating

## Symptoms

```text
Connector Temperature High
```

## Possible Causes

* Loose terminals
* High contact resistance
* Damaged connector
* Excessive current

## Checks

* Temperature sensor readings
* Connector condition
* Current logs

## Resolution

* Replace gun
* Tighten connections
* Verify current limits

---

# 🚗 EV Suspended

## Meaning

Vehicle is intentionally pausing charging.

## Common Reasons

* High Battery Temperature
* High SOC
* Cell Balancing
* Scheduled Charging

## OCPP Status

```text
SuspendedEV
```

## Resolution

Usually no charger fault.

Monitor vehicle behavior.

---

# ⚙️ EVSE Suspended

## Meaning

Charger cannot provide power.

## OCPP Status

```text
SuspendedEVSE
```

## Possible Causes

* Load Management
* Grid Limitation
* Power Module Fault
* Contactor Issue

## Checks

* Available power
* Power module alarms
* Contactor status

---

# 🔋 Charging Stops at 80%

## Possible Causes

### Vehicle Side

* Battery protection
* Thermal limitation
* SOC tapering

### Charger Side

* Current limit
* Firmware issue

## Checks

* CurrentDemand messages
* BMS current requests

---

# ⚡ CCS Communication Failure

## Symptoms

```text
Plugged In
Preparing
No Charging
```

## Possible Causes

* SLAC Failure
* PLC Failure
* ISO 15118 Error

## Troubleshooting

### Verify

```text
SLAC Pairing
```

### Verify

```text
SessionSetup
```

### Verify

```text
CurrentDemand
```

---

# 🌐 SLAC Failure

## Meaning

EV and charger cannot pair.

## Symptoms

```text
Preparing
Timeout
```

## Checks

* PLC modem health
* CP signal quality
* Cable integrity

---

# 📡 SessionSetup Failure

## Possible Causes

* Protocol mismatch
* PLC communication loss
* ISO 15118 error

## Verify

```text
SessionSetupReq
SessionSetupRes
```

---

# 🔌 Cable Check Failed

## Meaning

Insulation verification failed.

## Possible Causes

* Moisture
* Cable damage
* Ground fault

## Resolution

* Inspect connector
* Measure insulation resistance

---

# ⚡ Precharge Failure

## Symptoms

```text
Charging Never Starts
```

## Possible Causes

* Voltage mismatch
* Contactor fault
* Battery fault

## Verify

```text
EV Voltage
EVSE Voltage
```

---

# 🔋 CurrentDemand Timeout

## Meaning

EV stopped sending charging requests.

## Possible Causes

* PLC loss
* Vehicle communication fault
* Software issue

## Resolution

* Restart session
* Check PLC logs

---

# ⚠️ Contactor Fault

## Symptoms

```text
Charging Command Sent
No Power Output
```

## Checks

* Coil voltage
* Auxiliary feedback
* Weld detection

---

# 🔥 Insulation Fault

## Symptoms

```text
Isolation Error
```

## Possible Causes

* Moisture
* Damaged cable
* Battery fault

## Resolution

* Insulation resistance test

---

# 📈 OCPP Status Reference

| Status        | Meaning        |
| ------------- | -------------- |
| Available     | Ready          |
| Preparing     | Session Setup  |
| Charging      | Power Transfer |
| SuspendedEV   | Vehicle Pause  |
| SuspendedEVSE | Charger Pause  |
| Finishing     | Session Ending |
| Faulted       | Error State    |

---

# 🧠 RCA Template

## Fault

```text
EVSE Suspended
```

## Root Cause

```text
Power Module Temperature High
```

## Corrective Action

```text
Cooling Fan Replaced
```

## Preventive Action

```text
Periodic Thermal Inspection
```

---

# 💼 NOC Engineer Checklist

Before closing any ticket:

✅ Check OCPP logs

✅ Verify charger status

✅ Verify transaction history

✅ Verify alarms

✅ Check CP state

✅ Check communication health

✅ Confirm customer impact

✅ Record RCA

---

# 🎯 Golden Rule

Always identify:

```text
Vehicle Problem
OR
Charger Problem
OR
Network Problem
OR
Backend Problem
```

before starting deep troubleshooting.

---

# 📚 References

* IEC 61851
* IEC 62196
* DIN 70121
* ISO 15118
* OCPP 1.6J
* OCPP 2.0.1

---

# 👨‍💻 Author

**Avanish Pandey**

EV Charging Infrastructure | OCPP | EVSE Troubleshooting | NOC Engineering
