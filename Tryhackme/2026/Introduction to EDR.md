#edr #blueteam
# Introduction to EDR

Learn the fundamentals of EDR and explore its features and working.

# Task 1 Introduction

Endpoint Detection and Response (EDR) is a security solution designed to monitor, detect, and respond to advanced threats at the endpoint level. As a SOC analyst, it is essential for you to understand how the EDR works since it is a widely adopted solution in organizations to protect their endpoints. In this room, we will see how an EDR differs from a traditional antivirus and what data it collects from the endpoints. We will also discuss the detection and response capabilities it provides.
## Learning Objectives

- Understand the basics of EDR and how it works
- Differentiate EDR from traditional Antivirus solutions
- Examine the architecture of an EDR solution
- Analyze the types of telemetry it collects from endpoints
- Understand the detection and response capabilities of an EDR
- Investigate a realistic alert in the EDR

## Room Prerequisites

- Basic knowledge of different endpoints (Windows, Linux, Mac) and the common attacks on them
- Awareness of the role of the SOC team

# Task 2What is an EDR?

The increase in the use of digital devices is undeniable. Most of the business's core functions rely on the use of these digital devices. Cyber threats, on the other hand, are also increasing day by day. To protect these devices, organizations implement several security measures, most of which are to protect the network on which they operate these digital devices. However, the fast adoption of Remote Work has exposed these devices as they are out of the perimeter protection deployed on the organization's network. 

To ensure these endpoint devices are protected even out of the network, we need a security solution that guards all devices in different areas and is capable of fighting advanced threats. Endpoint Detection and Response (EDR) is a security solution that offers deep-level protection for endpoints. No matter where the endpoints are, the EDR will make sure they are monitored constantly and threats are detected.

Below are some of the EDR solutions in the market:

- [**CrowdStrike Falcon**](https://www.crowdstrike.com/wp-content/uploads/2022/03/crowdstrike-falcon-insight-data-sheet.pdf)
- [**SentinelOne ActiveEDR**](https://sentinelone.com/resources/datasheets/assets/usecase/sentinel-one-active-#page=1)
- [**Microsoft Defender for Endpoint**](https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-endpoint)
- [**OpenEDR**](https://www.openedr.com/)
- [**Symantec EDR**](https://docs.broadcom.com/doc/endpoint-detection-and-response-atp-endpoint-en)

Several other EDR solutions are available in the market. Their underlying architecture is mostly similar, but the features may vary.

Let's take a look at the core features of an EDR. We will be using the screenshots from CrowdStrike Falcon EDR to demonstrate the core features of EDR.

## Features of EDR

There are three main features of an EDR, which can also be referred to as the three pillars of an EDR solution.

## Visibility 

A good analysis often depends on the available level of visibility of the activity. This is one of the features of **EDR** that makes it unique from other endpoint security solutions. The level of visibility EDR provides is impressive. It collects detailed data from the endpoints, which includes process modifications, registry modifications, file and folder modifications, user actions, and much more. It then presents this information in a very structured format to the analyst. The analyst can see the whole process tree with a complete activity timeline of the sequence of actions. The analyst can also access the historical data of any endpoint for threat hunting or any other purpose. Any detections in the EDR land with a whole context.

|   |   |   |   |   |
|---|---|---|---|---|
|Process Modifications|Registry Modifications|File And Folder Modifications|User Actions|And Much More|

The following screenshot shows graphical representation of a process tree. We can see which processes were spawned on the endpoint. Each node represents a process. The lines connecting them represents their relationship. If we click on the `+` icon given with each process, we will be able to see all the network connections, registry changes, file changes etc. associated with that process.