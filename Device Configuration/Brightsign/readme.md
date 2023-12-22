# Configuring BrightSign Signage for Control From Crestron or AMX

The BrightSign signage player is controlled using Serial Port using Ascii strings or Ethernet using UDP protocol. Use BrightAuthor to create event strings that trigger specific actions.

In this example, the request is for BrightSign to switch between its HDMI input and it’s signage content. We will use UDP port 5000 to tell command the BrightSign to switch between the two.

1. Change the Presentation Properties – Interactive -UDP Settings to
    - All devices connected via Ethernet
    - UDP Destination Port 5000
    - UDP Receiver Port 5000

2. Add a user event for “ShowSignage” and “ShowHDMI”. This is adding an UDP event when the UDP port receives a specified string
    - Select the User Events tab
    - Select Manage
    - Click “Add User Event”
    - Name the event “ShowSignage”
    - Click “Add Event”
    - On the drop down that usually says “Timeout” select it to be UDP Input
    - On the text box on the left type in ShowSignage
    - Repeat steps c to g for ShowHDMI

3. Change your playlist to be interactive

4. Add the signage content
    - For this we will use a Image List but the signage content can be something completely different.
    - Add it to the play list
    - Double-click on the image list and change its properties:
        - Set as initial state: yes
        - Advance to next item on Image timeout: yes
        - Image timeout: 6 seconds
        - Play from beginning: yes
        - Media Files: add files

5. Add the Live Video to the Play list

6. Add Events to states.
    - Image List is a State
    - Live Video is a State
    - We’re going to add an event to go from one state to the other.
    - On the User Events tab, click and drag the ShowHDMI user event to the Image list State.
        - Select Transition to new state
        - Specify the state to be “Live Video”
    - Add the user event “ShowSignage” to the Live Video state
        - On the user events tab, click and drag ShowSignage to the Live Video State


7.  Save the project
8. Publish the project to the Signage Player
9. Test the UDP by sending “ShowHDMI” and “ShowSignage” to the Signage player on UDP port 5000.
