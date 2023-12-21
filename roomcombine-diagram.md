# Room Combine 
This is how to effectively program for a Combinable Room's Combine State. Sometimes partition sensors fail, go offline, or incorrectly report their state. It is then essential to let users be able to change the state of the room combination.
To achieve this, I recommend 3 buttons on the panel that determines the combine state of the room. 

A variable call it MODE which will have 3 values:
* AUTO
  - will use the partition's sensor state to determine the Combine State
* FORCE SEPARATE
  - will set the Combine State as SEPARATED
* FORCE COMBINE
  - will set the Combine State as COMBINED

```mermaid
flowchart TD
    Z("Partition Changed") -- Closed --> C1{"AND"}
    Z -- Opened --> C2{"AND"}
    C["Mode - Auto"] --> C1 & C2
    C1 --> E["Rooms are Separated"]
    C2 --> F["Rooms are Combined"]
    G["Mode - Force Separate"] --> E
    H["Mode - Force Combined"] --> F
    style Z stroke-width:4px,stroke-dasharray: 0
    style C stroke-width:4px,stroke-dasharray: 0,stroke:#FF6D00
    style E stroke:#FFD600
    style F stroke:#AA00FF
    style G stroke-width:4px,stroke-dasharray: 0,stroke:#FF6D00
    style H stroke-width:4px,stroke-dasharray: 0,stroke:#FF6D00
    linkStyle 0 stroke:#BBDEFB
    linkStyle 1 stroke:#BBDEFB,fill:none

```
