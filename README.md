# Team-Moevenpick 🍨

## Running workflow instance

<https://digibp.herokuapp.com/camunda/app/cockpit/default/> with Tennant ID *moevenpick* the workflow name is *Process_to_be_final*.

## Project description

Nowadays, it is possible to understand cancer, with the help of DNA sequencing as well as complex diagnostic procedures better than years before. In order to support doctors to understand the patients cancer even better, it is mandatory to have a well-defined process which covers the needed steps from the initial order to the finally send report.  Within Switzerland, the Unispital Zürich acts as one of the providers for the above described procedure.  

Therefore, they implemented the process to create a medical report based on the incoming order and performed DNA sequencing. This "Order to Report" process requires a huge variety of information systems, supporting actions, medical doctors and communication flows. Therefore, the project will focus on reviewing the AS-IS process to gather information for improving actions, communication and information flows. 

## Project Goal

1. Automate process steps which for now include a huge amount of manual labour. 
2. Eliminate existing "dead ends" in the AS-IS processes two improve process quality 

## Team-Member

|Name|Email|
|----------|---------------|
|Sascha Frossard|sascha.frossard@students.fhnw.ch|
|Selina Hodel|selina.hodel@students.fhnw.ch|
|Denis Moser|denis.moser@students.fhnw.ch|
|Marvin Marqua|marvin.marqua@students.fhnw.ch|  
  
**Coach:**  
- Andreas Martin
- Charuta Panda

---

## AS-IS Process

This chapter provides insights into the as-is process and its identified issues.

### Process Model

![as-is process model](00_Assets/AS-IS_Process.png)

### Roles

*Patient Management* The patient management is responsible taking care of administrative task regarding lab work such as processing orders and checking the order contains all necessary information.

*Accessioning* The accessioning responsible is handling incoming samples including tasks such as registrate and check samples.

*Lab technician* The lab technician is doing the actual work in the lab by processing the samples.

*Bio informatics* Runs algorithms on the sequenced data from the lab.

*Clinical Operations* Responsible for correct creation of analytical reports that will be sent to the client.

### Process Description

The process start with an internal or external client sending a request for a disgnosis order by email to the mailbox of the lab.

#### Order processing

**Process Order** The order is viewed in the mail and processed and checked if the important information is available.

**Register Sample-Order** The sample order is registered in the central pathology system. Internal orders will execute a sample extraction process from the patient. With external orders the patient material is directly acquired by the client.

**Sent extraction kit** For external orders a special box is sent to the client where the patient material will be sent back to the lab.

**Receive sample** The process is on halt until the sample phyisically arrives at the lab.

**Register sample** The incoming sample is registered in the laboratory system and the status of the order is updated in the order management system.

**Check sample** The sample is checked against certain criteria. If the sample does not fullfil the criteria the order is aborted. If ok the sample enters the lab.

**Check order form** A formally correct form has to be sent by the client for a sample to be sequenced. E.g. all information has to be correct and includes a signature consent by patient and physician.

#### Lab process

**Start Pre-Analytics** The sample is prepared for the lab process, that highly depends on the type of the processed patient material.

**DNA/RNA Extraction** The DNA/RNA is extracted which will be used for further analysis. The lab process can halt here until the order form is validated.

**Sequencing** The rna/dna is sequenced.

#### Post lab processing

**Sent sequencing data** The sequenced data is sent to external partner for generating a report.

**Finalize report** The report from the external partner is validated and finalized.

**Send report** The report is sent back to the client, that finishes the process.

#### Abort order

The abort order process can be triggered by multiple processes if e.g. the order form is uncomplete or missing for too long. Or if the sample fails in the lab process.

### Identified Issues and Problems

- The order is digitally processed in different systems. The user has to use different systems and even copy certain data from one system to another by hand. A workflow management system could be used to centralize the workflow implementation and provide a single user interface to do the work.
- Updating the order status has to be done by hand and needs to be automatized. This includes cancelling or aborting a order.

---

## TO-BE Process

This chapter provides the optimized process with the related benefits and improvments.

### Process Description

The TO-BE Process improves the steps from *Order processing* as described in the AS-IS Process. Everything else is out-of-scope for this project.

make better

### Process Model

tbd

### Architecture

tbd

#### Process variables

| Variable          | Description                           | Data Type    |
|-------------------|---------------------------------------|--------------|
|orderId            | unique order id                       | string       |
|orderInternal      | true if order is internal             | boolean       |
|sampleId           | unique sample id                      | string        |
|sampleType         | Type of the received sample           | string        | ffpe, dna, bonemarrow
|orderFromComplete  |True if order form is complete         | boolean       |
|sampleAcceptanceOk | true if sample acceptance is fullfilled | boolean     |
|customerEmail      | email of the ordering client          | string        |
|failureReason      | reason why order failed               | string        |

### Services

| Service           | Parameters                            | url    |
|-------------------|---------------------------------------|--------------|
|registerSample     | sampleId, sampleType                  | <https://hook.eu2.make.com/ycuwr6q9br1a17isbfccp6kpsvvcg3fd> |
|updateOrderStatus  | orderId, orderStatus                  | <https://hook.eu2.make.com/swvbhj5qjw62gad48ivy6r5704n55662> |
|abort order        | orderId, sampleId, customerEmail      | https://hook.eu2.make.com/7znnj319uhp4a1xuryaunn87gla72dcf   |
|notify customer    | orderId, sampleId, customerEmail,<br>orderFromComplete, sampleAcceptanceOk| https://hook.eu2.make.com/kvpu9ync60hgj1b46ycwzq00rpc0n4ge   |
|registerOrderToPIS | sampleId, orderId                             | <https://hook.eu2.make.com/ido2q831oxvbl0pwq4njjbyloh8rneuu> | 
|registerOrderToOMS | sampleId, orderId, orderStatus, orderInternal | <https://hook.eu2.make.com/4s0vhghjtmba9gshrsm2nk4mznu40yeq> | 
|checkSample|       sampleType, formfields, sampleAcceptanceOk    | <https://deepnote.com/workspace/digbp-33286cab-ee00-4c9f-a201-adadf03e74e9/project/DigiBIP-Moevenpick-External-Task-13a3d82c-c958-4b10-bb5d-322eec9658e4/notebook/Service%20Integration%20using%20External%20Task-4993c5c6b67645c1b0a57cfbeb0461bc> |

### Benefits and Improvements

## Conclusion
