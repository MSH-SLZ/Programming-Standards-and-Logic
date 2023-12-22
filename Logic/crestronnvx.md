# Director Routing & Offline Endpoint
So if a receiver comes online it will not update to the same source as what the director is sent. In SIMPL program the director may report back that it is on a particular source but actually the receiver is not on the source because it was offline when the source was sent. Source will have to be cleared and resent on the director. It takes about 90 seconds after the receiver comes online for the source to actually take effect.

So in sequence..
1) director out source set to 7
2) receiver goes to source 7
3) director reports receiver is on 7
4) receiver goes offline
5) director out source set to 9
6) director reports source is 9. It takes the director quite a while to detect that the receiver is actually offline (greater than 1 minute).
7) receiver goes online
8) receiver is booting up (takes about 180 seconds). During this time the receiver may show the video from source 7.
9) wait 180 seconds after receiver goes online (step 7).
10) set receiver source to 0
11) wait 2 seconds resend correct source to receiver (source 9).

# Endpoint Feedback
When an endpoint goes offline, its feedback can stay high if it is high prior to going offline.

# Audio Breakaway
To decode/extract a different audio stream than the video
1) Set the Audio Source to 5d (Secondary Audio Stream)
2) NVX Slot-3 (Secondary Audio) - SecondaryAudioMode set to 1d (Manual Mode)
3) NVX Slot-3 (Secondary Audio) - MulticastAddress set to the MulticastAddress of a Transmitter's Secondary Audio Stream.