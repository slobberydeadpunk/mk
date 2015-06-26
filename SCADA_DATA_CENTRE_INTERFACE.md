Preface
======
This document defines the interface and interaction between SCADA Data Centre and MFT Client application, such as IMS Super Panel, Trend Viewer and IEMS.

Use Case
=======
 1. Alarm Information
-------------------------
- Client: subscribe alarm message from DC, then receive real-time alarm message from DC by ZMQ.
- DC: listen and receive the subscribe message sending from MFT, then publish real-time structured alarm information.

 2. Trending Indicator Information
----------------------------------------
- Client: request data of indicators to DC by TCP socket, need information as following:
-- a. Indicator names, separated by ','
-- b. Update sequence of the indicator.
- DC: listen and receive the indicator monitoring request, and response follow the update frequency as requirement.

3. Super Panel Information
--------------------------------
- Client: send request command to DC. 
- DC: listen and receive the client request command, and response as following:
-- a. response all indicators to the client at the first time.
-- b. response the updated indicators to the client by event driven.

Interaction Protocol
================
1. Direction
--------------
- Alarm Information(DC -> Client)
- Indicator Information(DC -> Client)
- Request Command(Client -> DC)
2. Protocol
-------------
- Use protobuf do the message serialization and deserialization.
- Use ZMQ do the alarm transportation.
- Use TCP socket do the indicator information transportation. 
3. Data Format
------------------
- Alarm Message
Field Name	| Field Attribute	| Type	| Content			| Remarks	|
-------------	| -----------------	| ------	| ---------			| ----------	|
name			| required				| string	| Alarm Name	| 				|
time stamp	| required				| string	| 时间戳			| yyyymmddhhmmss (24hrs) 	|

- Indicator Message


