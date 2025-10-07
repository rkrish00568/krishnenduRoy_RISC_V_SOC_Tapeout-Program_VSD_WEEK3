# Timing path 
![Timing Path Diagram](images/timingpath.png)
A timing path is a chain of connected logic elements through which a signal propagates.

## ⏱️ What is Arrival Time?

The **arrival time (AT)** is the **actual time** at which a signal reaches a particular point (usually the **endpoint**) in the circuit.

### Required Time 
Allowed time for signal arrival

## 🧮 Slack Definitions

Type of Check

Slack Formula

Condition for Passing

Meaning

**Setup (Max Path)**

`Slack = Required Time − Arrival Time`

Slack ≥ 0

Data arrives **before** capture clock edge ✅

**Hold (Min Path)**

`Slack = Arrival Time − Required Time`

Slack ≥ 0

Data remains **stable after** capture edge ✅
