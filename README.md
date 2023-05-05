# EMS_config
EMS configurations of the EMS Server and of an EMS Client that guarantees the optimal performance

In order to make an optimal configuration from the message delivery to the receiving of the message, one should make many considerations on how the message is delivery(including which type of scenario, how heavier is the message, requirements to be fulfilled, and so on)

<img src="https://user-images.githubusercontent.com/45208254/236501374-2fa65c7b-7897-4cf1-87f9-a500ede44254.png" width="900" />

Here we adapted the following congifurations:
- TIBCO EMS RELIABLE DELIVERY
- AUTO_ACKNOWLEDGE
- serverflowcontrol=1000kb(basing on the average size of the message)
- maxbytes=0 (unlimited)
- maxmsgs=0 (unlimited)


As a result, the time needed to completely deliver and receive the message increased linearly.

<img src="https://user-images.githubusercontent.com/45208254/236502671-56413e19-5105-4234-85d4-35aa6bbf6fa9.png" width="850" />

As an observation, the time needed to completely deliver and receive the message increased linearly.
