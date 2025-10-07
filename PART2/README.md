# Timing path 
![Timing Path Diagram](images/timingpath.png)
A timing path is a chain of connected logic elements through which a signal propagates.

## ⏱️ What is Arrival Time?

The **arrival time (AT)** is the **actual time** at which a signal reaches a particular point (usually the **endpoint**) in the circuit.

### Required Time 
Allowed time for signal arrival

## Slack 
It is the difference btw arrival and expected time for a signal

-   **Max Slack** → Computed for **maximum delay (setup path)** → Slackmin​=Arrival Time−Required Time
    
-   **Min Slack** → Computed for **minimum delay (hold path)** → Slackmax​\=Required Time−Arrival Time
    
-   **Negative Slack** → Timing violation
    
-   **Positive Slack** → Timing met

## types of setup/hold analyis

 - reg2reg
 - in2reg
 - reg2out
 - in2out
 - clock gating
 - recovery/removal
 - data-to-data
 - latch(time borrow/time given)
![Timing Path Diagram](images/rar.png)
showing the recovery/removal path
![Timing Path Diagram](images/gating.png)
showing the clock gating path
![Timing Path Diagram](images/data2data.png)
showing the data to data path
![Timing Path Diagram](images/latch.png)
showing the latch(time borrow/time given)

## Skew/Transition analysis

 - Data(max/min)
 -  clock(max/min)
## Load Analysis
 - Fanout(max/min)
 - Capacitance(max/min)
## Clock Analysis
 - skew
 - pulse width

# Actual Arrival Time
time at any node where we see latest transition after first rise clock edge

