# Airlines Management System (Salesforce Application)

This repository contains a complete specification and implementation plan for an Airlines Management System built on Salesforce (App: AirlinesManagementSystem). The project defines the data model (custom objects and fields), relationships, validation and workflow rules, email alerts, security and sharing model, reports and dashboards, and sample users/roles for a production-ready Salesforce org.

## Objective

To design and implement a Salesforce-based Airlines Management System that enables flight creation and scheduling, pilot assignment, notifications, role-based access, and reporting for operational oversight.

## Key components
- Custom Objects: Flight, FlightSchedule, Pilots, PilotSchedule
- Core features: Flight scheduling, pilot assignment, duration calculation, status lifecycle (Open → InProgress → Closed/Canceled), email notifications for events
- Security: Role hierarchy, record ownership restrictions, sharing rules tied to destination, and controlled delete permissions
- Reporting & Dashboards: Daily/monthly schedules, closed vs canceled trends, and flight schedule history reports

## Project summary (based on included specification)
- Flights: Each Flight record (FlightID, FlightName, FlightCompany) has many FlightSchedules.
- FlightSchedule: Stores SourceName, DestinationName, DepartureDateTime, ArrivalDateTime, Duration (formula), Status (Open/InProgress/Closed/Canceled), and auto-fills pilot names from associated PilotSchedule.
- Pilots: Pilot records include personal and professional fields (FirstName, LastName, DOB, ContactNumber, EmailAddress, Experience) and validation rules (age >= 18, first/last name not identical).
- PilotSchedule: Links Pilots to a FlightSchedule; triggers email notifications to assigned pilots with schedule details.
- Validation & Business Rules: Enforce that source != destination, departure != arrival, departure before arrival, and that schedule lifecycle transitions trigger appropriate status updates and notifications.

## Users, Roles & Security
- Sample users included in the spec: Rajesh Deshpande, Anna Hajare, Neha Kakkad, Anu Malik, Katappa, Babubali
- Roles: CEO (System Admin), Manager (Anna Hajare), Flight Operators (Rajesh, Neha, Anu)
- Sharing: Operators can only view owned records; Rajesh can delete; flights arriving in Mumbai/Pune are shared with Katappa/Babubali respectively via sharing rules; public folders for Mumbai and Pune exist for shared content.

## Reports & Dashboards
- Dashboards suggested: Today's scheduled flights, month-wise scheduled flights, pie chart of closed vs canceled flights
- Reports: Flight-to-schedule history, current month schedules, last 3 months schedules

## Included artifacts
- README.md (this file)
- Airlines Management System.pdf — full project specification and diagrams

## How to use this repository
This repository is primarily a specification and implementation guide for building the solution in a Salesforce org. It can be used to:
1. Manually create the custom objects and fields in a Salesforce Developer org following the spec.
2. Implement Validation Rules, Workflow Rules/Process Builder or Flows, Email Alerts, and Sharing Rules as described.
3. Build the reports and dashboards listed under Reports & Dashboards.

If you prefer a metadata-driven approach (recommended for teams):
- Convert the spec into Salesforce metadata (CustomObject, CustomField, ValidationRule, Workflow/Flow, EmailTemplate, SharingRule, Report, Dashboard) and deploy using Salesforce DX (SFDX) or change sets.

## Implementation notes
- Duration formula: Use a formula field to compute hours and minutes between DepartureDateTime and ArrivalDateTime.
- Pilot name fields on FlightSchedule: Use roll-up or formula fields to display PilotSchedule lookup values.
- Email notifications: Use Workflow/Flow or Apex scheduled actions to send emails on create/update/status changes.
- Sharing rules: Use criteria-based sharing rules for destination-based sharing.

## Testing & Validation
- Create test user accounts and assign roles as specified, then verify record access, creation, editing, and delete permissions.
- Test validation rules by attempting invalid schedule entries (same source/destination, departure after arrival).
- Validate notification flows by creating/canceling schedules and ensuring expected emails are delivered.

## Roadmap / Enhancements
- Automate pilot rostering with optimization (avoid back-to-back impossible schedules)
- Add seat inventory and booking objects to extend into passenger management
- Integrate with external systems for real-time status updates (e.g., airport feeds)
- Convert the spec to SFDX metadata for CI/CD deployments

## Author
Specification and implementation prepared by Siddharth (@siddharth786s1). The full PDF spec is included in the repo.
