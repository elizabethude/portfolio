---
layout: post
title: Introduction to Detection Engineering - TryHackME
---

In this room, well go through the concept of detection engineering and frameworks used toowards crafting effective threat detecction strategies.

Before starting, I’d recommend checking out the reading material provided with each task—it’ll give you a solid foundation. 
This guide will cover just the essentials needed to answer the questions.


##  Task 2 What is Detection Engineering?

####  Detection Engineering
Cybersecurity is rapidly evolving, and so are the tactics of adversaries, making it challenging for security teams to keep pace. 

Detection engineering addresses this by continuously building and refining threat intelligence analytics to spot potentially harmful activities or misconfigurations. 

This process necessitates a cultural shift, aligning all security teams and management to create effective, threat-aware defense systems.


####  Detection Types
Threat detection can be approached from two main perspectives:

**Environment-based Detection**: This focuses on identifying changes in an environment based on established configurations and baseline activities, comprising:

**Configuration Detection**: Utilizes current knowledge of the environment to spot misalignments, with benefits like ease of creation and maintenance but challenges in dynamic settings.

**Modelling**: Involves defining baseline operations and monitoring for deviations, helping identify unknown adversary activities but lacking contextual information during investigations.

**Threat-based Detection**: This centers on elements linked to adversary activities, including:

**Indicator Detection**: Involves using indicators to identify legitimate and malicious activities. It's quick to deploy but dependent on the adversary's rate of change and can be retroactive.

**Threat Behaviour Detection**: Focuses on an adversary's tactics, techniques, and procedures, allowing for a scalable approach to detection. While it minimizes false positives, it requires extensive data for effective coverage.

Combining these detection types enhances overall defense systems, as model-based detection can be bolstered by expert-led configuration detection to minimize false alerts.

#### Detection as Code
Detection as Code (DaC) is a method that treats detection processes like software development, promoting scalability and adaptability to changing environments. 

By incorporating principles from Continuous Integration/Continuous Development (CI/CD), DaC offers:

**Version Control**: Enhances the ability to track and review changes in detection rules.

**Automation Workflows**: Facilitates quick testing and deployment of detection processes.

**Customizable Detections**: Allows for vendor-agnostic solutions across various security products.

**Test-Driven Development**: Ensures high-quality detections through rigorous testing.

**Team Collaboration**: Breaks down silos between security teams, fostering teamwork in coding processes.

**Code Reusability**: Enables engineers to leverage existing code for similar detection functions, accelerating the overall detection process.



**Which detection type focuses on misalignments within the current infrastructure?**

>  Configuration


**Which detection approach involves building an asset or activity baseline profile for detection?**

>  Modelling


**Which type of detection integrates with defensive playbooks?**

>  Threat Behaviour



## Task 4 Detection Engineering Frameworks 1

####**MITRE and CVEs**

MITRE is recognized for cataloging CVEs that adversaries might exploit in their malicious activities. 

They also offer a knowledge base that security analysts can leverage to track the tactics and techniques frequently used by malicious actors across various platforms like Windows, macOS, Linux, and mobile devices.


####**ATT&CK Framework**

The ATT&CK framework is essential for mapping adversarial actions relevant to detection engineering. 

It serves as a guide for identifying what to monitor, especially during the detection gap analysis phase.


####**Cyber Analytics Repository (CAR)**

The CAR knowledge base is utilized for detecting adversary behaviors, prioritizing them based on insights from the ATT&CK framework, ensuring that security efforts are focused on the most critical threats.


####**Pyramid of Pain**

The Pyramid of Pain is a widely recognized framework that illustrates the challenges adversaries face when defenders detect their tactics, techniques, and procedures (TTPs). 

It emphasizes the difficulty and cost for adversaries to adapt their TTPs once they are identified.


####**Cyber Kill Chain**

Inspired by military strategy, Lockheed Martin developed the Cyber Kill Chain framework to outline the key steps typically taken by adversaries during cyber-attacks. 

It consists of seven critical phases:

```
Reconnaissance
Weaponisation
Delivery
Exploitation
Installation
Command & Control
Actions on Objectives
```

For security analysts and detection engineers, understanding the Cyber Kill Chain is vital for recognizing intrusion attempts and integrating them into detection plans. 

The Unified Kill Chain enhances this concept by merging it with other frameworks, including the MITRE ATT&CK framework, expanding the original model into 18 phases that encompass all known elements of a cyber attack.


**Which framework looks at how to make it difficult for an adversary to change their approach when detected?**

>  Pyramid of Pain

**What is the improved Cyber Kill Chain framework called?**

>  The Unified Kill Chain

**How many phases are in the improved kill chain?**

>  18



## Task 5 Detection Engineering Frameworks 2


### Alerting and Detection Strategy Framework

Palantir's ADS Framework aims to guide the documentation of detection content, addressing the common issue of alert fatigue and apathy in security teams. 

This problem often stems from ineffective detection alerts that hinder incident response and mitigation. 

The framework provides a structured approach to creating effective detections and alerts.

#### Framework Stages

The ADS Framework outlines a strict process for detection engineers before publishing rules into production, which includes several key stages:

1. **Goal:** This stage defines the purpose of the alert and specifies the behaviors that need detection.
   
2. **Categorization:** Detection is mapped to the MITRE ATT&CK framework to inform analysts about the TTPs for investigation and relevant phases of the kill chain.

3. **Strategy Abstract:** This section offers a high-level overview of the detection strategy, detailing what the alert will monitor, the data sources involved, enrichment resources, and methods for minimizing false positives.

4. **Technical Context:** Here, the technical environment for the detection is described, ensuring analysts and responders have the necessary information to comprehend the alert. This should align with the tools used for collecting and processing threat data.

5. **Blind Spots and Assumptions:** This part identifies potential issues where suspicious activities might not activate the detection strategy. Recognizing these blind spots helps clarify where the ADS might fail or be evaded by an attacker.

6. **False Positives:** This section outlines situations that could trigger alerts due to misconfigurations or benign activities, helping configure SIEMs to focus on genuine threats when the detection goes live.

7. **Validation:** Every detection must be verified, outlining steps to ensure a true-positive event triggers the alert. This process includes developing a test plan, documenting it, and executing it in a testing environment to validate the detection strategy.

8. **Priority:** This stage establishes alerting levels for the detection strategy, detailing the criteria for setting preferences, distinct from the alert levels shown in the SIEM.

9. **Response:** Finally, this section details how to triage and investigate detection alerts, providing essential guidance for analysts and responders to mitigate potential risks effectively.



### Detection Maturity Level Model

Ryan Stillions introduced the Detection Maturity Level (DML) model in 2014 to help organizations evaluate how well they can use cyber threat intelligence for detecting adversary actions. 

He emphasizes two key principles: first, that maturity is determined not just by the ability to gather intelligence, but by the capability to apply it in detection and response; second, that without established detection functions, effective response functions cannot occur.

### Maturity Levels Overview

The DML model features nine maturity levels, ranging from 0 to 8. The lower levels focus on technical aspects of attacks, while the higher levels emphasize abstract and intelligence-based considerations. Here’s a breakdown of each level:

- **DML-8 Goals:** This top level indicates organizations capable of detecting an adversary's motives and goals, although it's often difficult since it largely relies on behavioral interpretations from lower levels.
  
- **DML-7 Strategy:** This level shifts to non-technical aspects, highlighting the adversary's intentions and strategies. Organizations here utilize mature intelligence sources for context on adversaries' plans, aiding responders.

- **DML-6 Tactics:** Organizations must detect the tactics employed by adversaries without necessarily identifying the specific tools used. This detection is based on recognizing patterns over time.

- **DML-5 Techniques:** At this level, organizations can identify specific techniques tied to particular adversaries or Advanced Persistent Threats (APTs), gaining an advantage by recognizing attackers' behavioral evidence.

- **DML-4 Procedures:** This level requires detecting sequences of actions taken by adversaries, as they typically follow organized patterns, such as pre-exfiltration reconnaissance.

- **DML-3 Tools:** Detection at this level involves recognizing tools during two phases: the transfer phase, where tools are downloaded, and operational detection, which may require reverse engineering, adding complexity to the process.

- **DML-2 Host & Network Artefacts:** Organizations focus on gathering Indicators of Compromise (IOCs) and artefacts, often only identifying threats after damage has occurred, akin to "chasing the vapor trail of an aircraft."

- **DML-1 Atomic Indicators:** At this level, organizations utilize threat intelligence feeds, such as lists of IP addresses and domains, to detect threats.

- **DML-0 None:** The lowest level indicates organizations that lack any established detection processes, highlighting a critical vulnerability.

**Read the above.**

>  No answer needed



##  Task 6 

In this task, I work to establish a detection engineering process aimed at identifying changes made to privileged and administrative groups and accounts in their Active Directory. 

As a detection analyst, I’ve been assigned the task of developing the strategy based on a series of questions. 

Each question has one correct answer, and it's up to me to identify and select it. 



**What is the flag?**

>  THM{Sup3r-D3t3ct1v3}
