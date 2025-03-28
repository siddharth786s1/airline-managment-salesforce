# airline-managment-salesforce

Okay, this is a comprehensive project specification for an Airlines Management System. It outlines the data model, relationships, business logic, security requirements, and reporting needs. This system would be complex to build, involving multiple objects, workflows, and integrations.

Here's a breakdown of the requirements, organized for clarity:

1.  Application Setup

App Name: AirlinesManagementSystem

Branding: Add a flight company logo.

2.  Data Model

Object: Flight

Fields:

FlightID (AutoGenerated)

FlightName (e.g., Go-102)

FlightCompany (Picklist: Indigo/AirIndia/GoAir/Kingfisher)

Relationships:

One-to-many with FlightSchedule (show all schedules for this flight in its related list)

Object: FlightSchedule

Fields:

SelectFlight (Master-Detail relationship with Flight)

SourceName (Picklist of cities)

DestinationName (Picklist of cities)

DepartureDateTime (Date and Time)

ArrivalDateTime (Date and Time)

Duration (Formula field, format: 02Hours 10Minutes)

Status (Picklist: Open/InProgress/Closed/Canceled)

NameofFirstPilot (Take from child object Pilots)

NameofSecondPilot (Take from child object Pilots)

Validation Rules:

SourceName and DestinationName must not be the same.

DepartureDateTime and ArrivalDateTime must not be the same.

DepartureDateTime must not be after ArrivalDateTime.

Workflow Rules:

When a new FlightSchedule record is created, default Status is "Open."

When the flight is ready to depart, Status should be "InProgress."

When the flight arrives, Status should be "Closed."

Email Notifications:

Send an email to the user/system admin whenever a new flight is scheduled, a flight departs, and a flight arrives.

Send an email to the system admin and pilots if a flight schedule is canceled.

Object: Pilots

Fields:

FirstName (Mandatory)

LastName (Mandatory)

DOB (Date)

Age (Formula field, based on DOB)

ContactNumber (Phone)

EmailAddress (Mandatory Email)

Experience (Picklist: Less than 1 Year/2-5 Years/More than 05 Years)

Level (Formula field: Junior if Less than 1 Year; Senior if 2-5 Years; SuperSenior if More than 05 Years)

Photo (Rich Text Area)

Validation Rules:

FirstName and LastName must not be the same.

Age must be greater than or equal to 18.

Object: PilotSchedule

Fields:

SelectFlightSchedule (Master-Detail relationship with FlightSchedule)

SelectPilot1 (Lookup relationship with Pilot)

SelectPilot2 (Lookup relationship with Pilot)

Email Notifications:

Send an email to Pilot that he has been scheduled for a flight and flight name, departure city, arrival city, departure and arrival datetime.

3.  Users and Security

User Creation:

Create the following users:

Rajesh Deshpande

Anna Hajare

Neha Kakkad

Anu Malik

Katappa

Babubali

Roles:

CEO (System Admin)

Manager (Anna Hajare)

Flight Operators (Rajesh Deshpande, Neha Kakkad, Anu Malik)

User Hierarchy:

All operators report to Anna Hajare.

Anna Hajare reports to the CEO.

Data Security:

Operators can create, read, and edit data.

Only Rajesh Deshpande can delete records.

Operators can view only their owned records, not those of others.

Public Folders:

Create public folders: "Mumbai" and "Pune."

Add Katappa to the "Mumbai" public folder.

Add Babubali to the "Pune" public folder.

Sharing Rules:

When a flight is arriving in Mumbai, share the flight record with Katappa.

When a flight is arriving in Pune, share the flight record with Babubali.

General: Apply data security measures as needed to protect sensitive information and enforce business rules.

4.  Reports and Dashboards

Dashboards:

Dashboard showing scheduled flights for today.

Dashboard showing scheduled flights month-wise.

Pie chart showing total closed and canceled flights.

Reports:

Report showing flights and all their scheduled flights to date.

Report showing flights and all their scheduled flights in the current month.

Report showing flights and all their scheduled flights in the last 03 months.
