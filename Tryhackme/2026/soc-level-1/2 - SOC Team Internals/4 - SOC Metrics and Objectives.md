
# SOC Metrics and Objectives

Explore key metrics driving SOC effectiveness and discover ways to improve them.

# Task 1 Introduction

As with any other department, the efficiency of the SOC team can be measured using different indicators and metrics. This room explores the most common evaluation approaches like MTTD and MTTR and describes both methods to improve the metrics and potential consequences of ignoring them.

## Learning Objectives

- Discover the concepts of SLA, MTTD, MTTA, and MTTR
- Understand the importance of the False Positive rate
- Learn why and how to improve the metrics as an L1 analyst
- Practice with managing SOC team performance metrics

## Prerequisites

- Complete the preceding [SOC Workbooks and Lookups](https://tryhackme.com/room/socworkbookslookups) room
- Understand key alert properties like severity or verdict
- Know the difference between in-house and managed SOC

Answer the questions below

Let's begin!


# Task 2 Core Metrics

To begin with, let's recall the main goal of a SOC - to protect the confidentiality, integrity, and availability of the organisation's digital assets. The SOC team performs its purpose by developing, receiving, and triaging alerts. The L1 analysts' role in this process is to reliably report True Positives to the higher level, to L2. This leads us to the first four metrics:

|Metric|Formula|Measures|
|---|---|---|
|Alerts Count|`AC = Total Count of Alerts Received`|Overall load of SOC analysts|
|False Positive Rate|`FPR = False Positives / Total Alerts`|Level of noise in the alerts|
|Alert Escalation Rate|`AER = Escalated Alerts / Total Alerts`|Experience of L1 analysts|
|Threat Detection Rate|`TDR = Detected Threats / Total Threats`|Reliability of the SOC team|

## Alerts Count

Imagine starting your shift and seeing 80 unresolved alerts in the queue. That's definitely overwhelming and prone to missing real threats hiding behind the noise spam. On the other hand, consider a whole week without any alerts. Sounds better at first glance, but also concerning since a too low count of alerts may indicate an issue in the SIEM or lack of visibility, leading to undetected breaches. The ideal metric value depends on company size but in general, **5 to 30 alerts per day per L1 analyst is a good metric**.

## False Positive Rate

If 75 out of 80 alerts (94%) were confirmed to be False Positives like system noise or typical IT activity - that's a bad signal for your team. With more noise, analysts tend to become less vigilant and more likely to miss the threat and treat all alerts just like "yet another spam". A False Positive rate of **0% is an unachievable ideal, but 80% or higher is a serious problem**, usually fixed by a tool and detection rules tuning, often called "False Positive Remediation".

## Alert Escalation Rate

L2 analysts rely on L1 to filter out the noise and escalate only the actionable, threatening alerts. At the same time, as L1, you don't want to be overconfident and triage alerts you do not fully understand without a senior support. The alert escalation rate comes in handy to evaluate how experienced and independent the L1 analysts are and how often they decide to escalate the alert. It is usually **aimed to be below 50%, or even better below 20%**.

## Threat Detection Rate

Imagine that out of six attacks for 2025, your SOC team detected and prevented four attacks, missed the fifth because of the broken detection rule, and the sixth because one of the L1 analysts misclassified the breach as False Positive. The resulting metric is TDR = 4 / 6 = 67%, and this is a very bad result. The threat detection rate **should always be at 100%** since every missed threat can have devastating consequences, such as ransomware infection and data exfiltration.

## Answer the questions below

Is zero alerts for one month a good sign for your SOC team? (Yea/Nay)

 Nay

What is the False Positive Rate if only 10 out of 50 alerts appear to be real threats?

80%

# Task 3 Triage Metrics

Next, remember that an alert by itself will not stop the breach, and it is important to timely receive the alert, triage it, and respond to the attack before the attackers achieve their goals. The requirements to ensure a quick detection and remediation of the threat are commonly grouped into a **Service Level Agreement (SLA)** - a document signed between the internal SOC team and its company management, or by the managed SOC provider (MSSP) and its customers. The agreement usually requires quick threat detection (measured by **MTTD**), timely alert acknowledgement by L1 analysts (measured by **MTTA**), and finally, prompt response to the threat, like isolating the device or securing the breached account (measured by **MTTR**):

## Reference Table

Note that different teams might have different definitions or formulas for the SOC metrics, depending on what they want to measure. For this and the following tasks, please use the illustration above and the reference table below to answer the questions.

|Metric|Common SLA|Description|
|---|---|---|
|SOC Team Availability|24/7|Working schedule of the SOC team, often Monday-Friday (8/5) or 24/7 mode|
|Mean Time to Detect (MTTD)|5 minutes|Average time between the attack and its detection by SOC tools|
|Mean Time to Acknowledge (MTTA)|10 minutes|Average time for L1 analysts to start triage of the new alert|
|Mean Time to Respond (MTTR)|60 minutes|Average time taken by SOC to actually stop the breach from spreading|

Answer the questions below

Imagine a scenario where the SOC team receives a critical alert on Saturday.  
If the team works 8/5, on which day of the week will they acknowledge the alert?

Monday


Imagine a scenario where an employee was lured into running data stealer malware.  
  1. The SOC team received the "Connection to Redline Stealer C2" alert after **12** minutes.  
  2. One of the L1 analysts on shift moved the alert to In Progress **10** minutes later.  
  3. After **6** minutes, the alert was escalated to L2, who spent **35** minutes cleaning the malware.  

Provide the MTTD, MTTA, and MTTR via comma as your answer (e.g. 10,20,30).

12,10,51


# Task 4 Improving Metrics

Now that you know a lot about different metrics, why would it matter to you as an L1 analyst? First, you should understand that metrics were built to make the SOC more efficient and, therefore, to make the attacks far less successful. Second, the metrics are often used to evaluate your performance, and good results lead to career growth and a raise to more senior positions like L2 analyst. So, how can you improve the metrics?

## Reference Table

|Issue|Recommendations|
|---|---|
|False Positive Rate  <br>over 80%|**Your team receives too much noise in the alerts. Try to:**  <br>  <br>1. Exclude trusted activities like system updates from your EDR or SIEM detection rules  <br>2. Consider automating alert triage for most common alerts using SOAR or custom scripts|
|Mean Time to Detect  <br>over 30 min|**Your team detects a threat with a high delay. Try to:**  <br>  <br>1. Contact SOC engineers to make the detection rules run faster or with a higher rate  <br>2. Check if SIEM logs are collected in real-time, without a 10-minute delay|
|Mean Time to Acknowledge  <br>over 30 min|**L1 analysts start alert triage with a high delay. Try to:**  <br>  <br>1. Ensure the analysts are notified in real-time when a new alert appears  <br>2. Try to evenly distribute alerts in the queue between the analysts on shift|
|Mean Time to Respond  <br>over 4 hours|**SOC team can't stop the breach in time. Try to:**  <br>  <br>1. As L1, make everything possible to quickly escalate the threats to L2  <br>2. Ensure your team has documented what to do during different attack scenarios|

Answer the questions below

What is the highest acceptable False Positive Rate for SOC teams?

 80%

Should all SOC roles work together to keep metrics improving? (Yea/Nay)

yea

# Task 5 Practice Scenarios



# Task 6 Conclusion