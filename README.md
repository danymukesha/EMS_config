# EMS_config
EMS configurations of the EMS Server and of an EMS Client that provides the optimal performance

In order to make an optimal configuration from the message delivery to the receiving of the message, one should make many considerations on how the message is delivery(including which type of scenario, how heavier is the message, requirements to be fulfilled, and so on)

The example below show EMS messaging system works. There is a producer that create and send the message to the destination(e.g. a queue). The consumer that is ready to receive the message from the destination. 

**Example description**: We did five consecutive tests using three different ways of configuration on the producers's side. The sent message weighed 1.36kb (relatively light) and was sent 100 times for each launch. 

<img src="https://user-images.githubusercontent.com/45208254/236501374-2fa65c7b-7897-4cf1-87f9-a500ede44254.png" width="900" />

Here we adapted the following congifurations, in order to optimize the transmissione of messages:
- TIBCO EMS RELIABLE DELIVERY (producer)
- AUTO_ACKNOWLEDGE (consumer)
- serverflowcontrol=1000kb(basing on the average size of the message)
- maxbytes=0 (unlimited)
- maxmsgs=0 (unlimited)


As a result, the time needed to completely deliver and receive the message increased linearly.

<img src="https://user-images.githubusercontent.com/45208254/236502671-56413e19-5105-4234-85d4-35aa6bbf6fa9.png" width="850" />

As an observation, the time needed to completely deliver and receive the message increased linearly.

The producer is sending more messages than what the consumer(s) can receive. The above curve shows then that there were some pending messages for a destination that are stored by the server until they can be delivered/consumed and this causes a very significant delay(time consuming). The server tended to potentially exhaust its storage capacity if the message receivers/consumers do not receive messages quickly enough or there are not as many consumers as the messages available(sent by the producer). 

EMS Server configuration, known as ***flowcontrol***, allows you to manage the flow of communications to a destination to manage this issue. Each destination can specify a maximum storage size for waiting messages. When the target is reached, EMS prohibits message producers from sending new messages. This effectively slows down message producers until the pending messages are received by message consumers.
