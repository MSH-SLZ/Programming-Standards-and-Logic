## Fire Life Safety Logic
When systems are being programmed it is usually not specified if the Fire System is Normally Open or Normally Closed. Thus it becomes a punch item during commissioning. To avoid that I use the following logic or algorithm.

When the processor boots up, assume that the fire system is not in alarm. Thus the opposite of the sensor input on the processor is the alarm state.

A Crestron implementation:
```mermaid
flowchart LR
    PP[/"Program Ready Pulse"/] -- enable --> SetNormal["BUF"]
    Sensor(("Fire Life Safety Sensor")) --> CL(("is Closed"))
    CL --> NT["Not"] & SetNormal & W1["pulse"]
    NT --> OP(("is Open"))
    OP --> SetNormal
    SetNormal -- closed/b --> IL["ILOCK"]
    SetNormal -- open/b --> IL
    IL -- normally closed --> NCO("n.c. AND opened pulsed")
    IL -- normally open --> NOC("n.o. AND closed pulsed")
    OP -- trailing edge --> W2["pulse"]
    W2 -. open pulsed .-> NCO
    NCO --> SD["Do Shutdown"]
    W1 -. closed pulsed .-> NOC
    NOC --> SD
    style PP stroke:#AA00FF
    style CL stroke:#D50000,stroke-width:4px,stroke-dasharray: 0
    style OP stroke:#00C853,stroke-width:4px,stroke-dasharray: 0
    linkStyle 2 stroke:#D50000,fill:none
    linkStyle 3 stroke:#D50000,fill:none
    linkStyle 4 stroke:#D50000,fill:none
    linkStyle 5 stroke:#00C853,fill:none
    linkStyle 6 stroke:#00C853,fill:none
    linkStyle 7 stroke:#D50000,fill:none
    linkStyle 8 stroke:#00C853,fill:none
    linkStyle 9 stroke:#D50000,fill:none
    linkStyle 10 stroke:#00C853,fill:none
    linkStyle 11 stroke:#00C853
    linkStyle 12 stroke:#00C853,fill:none
    linkStyle 14 stroke:#D50000,fill:none



```