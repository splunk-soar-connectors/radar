[comment]: # "Auto-generated SOAR connector documentation"
# Radar

Publisher: RADAR, LLC  
Connector Version: 1\.0\.3  
Product Vendor: RADAR, LLC  
Product Name: Radar  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 4\.9\.39220  

This app integrates with the Radar incident response platform

[comment]: # ""
[comment]: # "File: readme.md"
[comment]: # "Copyright (c) 2020-2021 RADAR, LLC"
[comment]: # ""
[comment]: # "Licensed under Apache 2.0 (https://www.apache.org/licenses/LICENSE-2.0.txt)"
[comment]: # ""
## About Radar Software for Privacy Incident Response Management:

Radar performs a comprehensive privacy risk assessment and determines when the incident is
notifiable under current data breach regulations. Radar guides privacy analysts through the
profiling and risk scoring of an incident, providing all necessary documentation to support an
organization’s burden of proof obligation under federal, state, and international breach laws.

For more information visit: <https://www.radarfirst.com/radar>

## Setup and Configuration

To use the Radar Phantom App, a Radar admin should request documentation from the Radar integrations
team.

To request this documentation:

-   Log into Radar at <https://app.radarfirst.com/login>
-   Select "Admin" from the top navigation.
-   From the admin UI, select "Integrations" from the top navigation.
-   From the list of integrations, select "Learn more" where Splunk Phantom is listed.
-   Follow the directions for contacting the Radar integration team.

When running the Radar app on the Splunk Phantom platform, the 'base_url' must be configured on the
company settings page. To configure the 'base_url' go to admin/company_settings/info and specify a
valid URL for the base URL field. If the 'base_url' is not configured, the 'create_privacy_incident'
action will throw an error message as 'Base URL for phantom appliance must be configured'.

## Asset Configuration

The configuration that must be set is under the "Asset Settings" tab. Below lists some details for
each configuration setting:

-   Radar API Bearer Token - A valid Radar bearer token with privileges for reading and writing
    radar incidents and notes.
-   Radar API URL - Defaults to the production URL, but can be set to a test or staging URL.
-   Time Zone - Should reflect the time that the Splunk Phantom instance is running in. This
    configuration is used in a couple of different ways:
    -   To specify a privacy incident’s ‘discovered’ timezone, when it is created by the “create
        privacy incident” action. This data is used during incident assessment and is critically
        important in determining regulatory timelines for incident notification to governmental
        agencies.
    -   Used when displaying certain action outputs, such as the “created at” and “updated at”
        outputs from the “get privacy incident” action. These timestamps are converted to the time
        zone specified in the asset configuration.

#### Environment Variables

Under the 'Advanced' section of the asset settings, set environment variables to configure the app
settings:

**ALLOW_SELF_SIGNED_CERTS** - Should be set to '1' to turn off verification of SSL Certificates
during action requests.


### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a Radar asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**radar\_api\_token** |  required  | password | Radar API Bearer Token
**radar\_api\_url** |  required  | string | Radar API URL
**time\_zone** |  optional  | string | Time Zone

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate Radar asset configuration for connectivity using supplied configuration  
[create privacy incident](#action-create-privacy-incident) - Create a Radar privacy incident  
[get privacy incident](#action-get-privacy-incident) - Get a Radar privacy incident  
[add note](#action-add-note) - Add a note to a Radar privacy incident  
[get notes](#action-get-notes) - Get all notes for a Radar privacy incident  

## action: 'test connectivity'
Validate Radar asset configuration for connectivity using supplied configuration

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'create privacy incident'
Create a Radar privacy incident

Type: **generic**  
Read only: **False**

This action creates a privacy incident in Radar using Splunk Phantom settings and asset configurations\. The base URL for the Splunk Phantom appliance configured on the company settings page is used to link the incident's "intake method" to this instance of the Splunk Phantom\. The time zone specified in the asset settings is used in combination with the current moment the action is triggered to set the incident's "discovered" date and time\. The container ID for the associated Splunk Phantom event or case is used to specify the Radar incident channel ID\. This is used to associate the Radar incident with the Splunk Phantom container\. Action parameters are used to set the Radar incident name and description\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**name** |  required  | A name summarizing the privacy incident | string | 
**description** |  optional  | A description of the privacy incident | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.name | string | 
action\_result\.parameter\.description | string | 
action\_result\.data\.\*\.incident\_id | numeric |  `radar incident id` 
action\_result\.data\.\*\.name | string | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.discovered | string | 
action\_result\.data\.\*\.url | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get privacy incident'
Get a Radar privacy incident

Type: **investigate**  
Read only: **True**

This action gets a Radar privacy incident using the incident ID supplied in the action parameters\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**incident\_id** |  required  | Radar incident ID | numeric |  `radar incident id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.incident\_id | numeric |  `radar incident id` 
action\_result\.data\.\*\.incident\_id | numeric |  `radar incident id` 
action\_result\.data\.\*\.name | string | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.url | string | 
action\_result\.data\.\*\.created\_at | string | 
action\_result\.data\.\*\.discovered\_at | string | 
action\_result\.data\.\*\.updated\_at | string | 
action\_result\.data\.\*\.updated\_by | string | 
action\_result\.data\.\*\.incident\_status | string | 
action\_result\.data\.\*\.assignee | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'add note'
Add a note to a Radar privacy incident

Type: **generic**  
Read only: **False**

This action adds a note to a given Radar incident using asset configurations and action parameters\. The incident ID action parameter is used to add a note to a given incident\. The content action parameter is used for the content of the note\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**incident\_id** |  required  | Radar incident ID | numeric |  `radar incident id` 
**content** |  required  | Note content | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.incident\_id | numeric |  `radar incident id` 
action\_result\.parameter\.content | string | 
action\_result\.data\.\*\.id | numeric | 
action\_result\.data\.\*\.incident\_id | numeric |  `radar incident id` 
action\_result\.data\.\*\.content | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get notes'
Get all notes for a Radar privacy incident

Type: **investigate**  
Read only: **True**

This action gets all notes for a given Radar incident using the incident ID supplied in the action parameters\. Only notes that were created with the 'create note' action will be fetched from Radar\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**incident\_id** |  required  | Radar incident ID | numeric |  `radar incident id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.incident\_id | numeric |  `radar incident id` 
action\_result\.data\.\*\.id | numeric | 
action\_result\.data\.\*\.content | string | 
action\_result\.data\.\*\.created\_at | string | 
action\_result\.data\.\*\.created\_by | string | 
action\_result\.data\.\*\.updated\_at | string | 
action\_result\.data\.\*\.updated\_by | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric | 