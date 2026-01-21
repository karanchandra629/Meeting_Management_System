# Meeting Management System – Salesforce Admin Task

## About This Task
This repository contains the Salesforce Admin implementation of the
Meeting Management System task provided during the assignment.

The focus of this task is on Salesforce Admin configuration such as
custom objects, fields, validation rules, email automation, and access control.
No Apex or LWC development is used in this implementation.



## Custom Objects Configuration

### Meeting__c Object
The Meeting__c object is created to store meeting-related information.

Fields created:
- Name (Text)
- Meeting_Date__c (Date)
- Location__c (Text)
- Capacity__c (Number)
- Status__c (Picklist: Scheduled, Full, Completed)
- Registered_Participants__c (Number)
- Remaining_Capacity__c (Formula)

Formula used for Remaining Capacity:
Capacity__c - Registered_Participants__c

This formula helps to identify how many seats are still available in a meeting.


### Participant__c Object
The Participant__c object is used to store participant details.

Fields created:
- Name (Text)
- Email__c (Email)
- Meeting__c (Lookup to Meeting__c)
- Status__c (Picklist: Registered, Cancelled)

Each participant record is linked to a meeting using a lookup relationship.



## Validation Rules

### Meeting Date Validation
A validation rule is applied to ensure that a meeting cannot be scheduled in the past.

Formula used:
Meeting_Date__c < TODAY()



### Participant Capacity Validation
A validation rule is added to prevent participants from registering
when the related meeting is already full.

Formula used:
Meeting__r.Remaining_Capacity__c <= 0



## Email Notification Setup

An email template is created to send a confirmation email to participants
after successful registration.

Email Template Name:
Participant Registration Confirmation

Subject:
Meeting Registration Confirmation

Email Body:
Hello {{{Participant__c.Name}}}

You have been successfully registered for the meeting.

Meeting Details:
Name: {{{Participant__c.Meeting__r.Name}}}
Date: {{{Participant__c.Meeting__r.Meeting_Date__c}}}
Location: {{{Participant__c.Meeting__r.Location__c}}}

Thank you.

A record-triggered flow is configured on Participant__c to send this email
when a participant is created with status set to "Registered".



## User Access Control

- Meeting Manager:
  - Can create, view, and edit Meeting__c records

- Attendee:
  - Can create and view Participant__c records
  - Can only see their own participant records

This setup ensures proper role-based access and data security.



## Final Notes
- Task completed using Salesforce Admin features only
- No Apex, LWC, or custom code used
- No Salesforce org credentials or screenshots shared
- Task completed within the given time limit
