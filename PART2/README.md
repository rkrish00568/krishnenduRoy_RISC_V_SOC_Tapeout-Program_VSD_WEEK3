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

1)reg2reg
2)in2reg
3)reg2out
4)in2out
