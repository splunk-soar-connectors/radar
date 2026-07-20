# Radar

Publisher: RADAR, LLC <br>
Connector Version: 1.0.0 <br>
Product Vendor: RADAR, LLC <br>
Product Name: Radar <br>
Minimum Product Version: 4.9.39220

This app integrates with the Radar incident response platform

### Configuration variables

This table lists the configuration variables required to operate Radar. These variables are specified when configuring a Radar asset in Splunk SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**radar_api_token** | required | password | Radar API Bearer Token |
**radar_api_url** | required | string | Radar API URL |
**time_zone** | optional | string | Time Zone |

### Supported Actions

[test connectivity](#action-test-connectivity) - Validate Radar asset configuration for connectivity using supplied configuration <br>
[create privacy incident](#action-create-privacy-incident) - Create a Radar privacy incident <br>
[get privacy incident](#action-get-privacy-incident) - Get a Radar privacy incident <br>
[add note](#action-add-note) - Add a note to a Radar privacy incident <br>
[get notes](#action-get-notes) - Get all notes for a Radar privacy incident

## action: 'test connectivity'

Validate Radar asset configuration for connectivity using supplied configuration

Type: **test** <br>
Read only: **True**

#### Action Parameters

No parameters are required for this action

#### Action Output

No Output

## action: 'create privacy incident'

Create a Radar privacy incident

Type: **generic** <br>
Read only: **False**

This action creates a privacy incident in Radar using Splunk Phantom settings and asset configurations. The base URL for the Splunk Phantom appliance configured on the company settings page is used to link the incident's "intake method" to this instance of the Splunk Phantom. The time zone specified in the asset settings is used in combination with the current moment the action is triggered to set the incident's "discovered" date and time. The container ID for the associated Splunk Phantom event or case is used to specify the Radar incident channel ID. This is used to associate the Radar incident with the Splunk Phantom container. Action parameters are used to set the Radar incident name and description.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**name** | required | A name summarizing the privacy incident | string | |
**description** | optional | A description of the privacy incident | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.name | string | | |
action_result.parameter.description | string | | |
action_result.data.\*.incident_id | numeric | `radar incident id` | |
action_result.data.\*.name | string | | |
action_result.data.\*.description | string | | |
action_result.data.\*.discovered | string | | |
action_result.data.\*.url | string | | |
action_result.status | string | | success failed |
action_result.message | string | | Successfully created a privacy incident |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get privacy incident'

Get a Radar privacy incident

Type: **investigate** <br>
Read only: **True**

This action gets a Radar privacy incident using the incident ID supplied in the action parameters.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**incident_id** | required | Radar incident ID | numeric | `radar incident id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.incident_id | numeric | `radar incident id` | |
action_result.data.\*.incident_id | numeric | `radar incident id` | |
action_result.data.\*.name | string | | |
action_result.data.\*.description | string | | |
action_result.data.\*.url | string | | |
action_result.data.\*.created_at | string | | |
action_result.data.\*.discovered_at | string | | |
action_result.data.\*.updated_at | string | | |
action_result.data.\*.updated_by | string | | |
action_result.data.\*.incident_status | string | | |
action_result.data.\*.assignee | string | | |
action_result.status | string | | success failed |
action_result.message | string | | Successfully fetched privacy incident |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'add note'

Add a note to a Radar privacy incident

Type: **generic** <br>
Read only: **False**

This action adds a note to a given Radar incident using asset configurations and action parameters. The incident ID action parameter is used to add a note to a given incident. The content action parameter is used for the content of the note.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**incident_id** | required | Radar incident ID | numeric | `radar incident id` |
**content** | required | Note content | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.incident_id | numeric | `radar incident id` | |
action_result.parameter.content | string | | |
action_result.data.\*.id | numeric | | |
action_result.data.\*.incident_id | numeric | `radar incident id` | |
action_result.data.\*.content | string | | |
action_result.status | string | | success failed |
action_result.message | string | | Successfully added note |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get notes'

Get all notes for a Radar privacy incident

Type: **investigate** <br>
Read only: **True**

This action gets all notes for a given Radar incident using the incident ID supplied in the action parameters. Only notes that were created with the 'create note' action will be fetched from Radar.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**incident_id** | required | Radar incident ID | numeric | `radar incident id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.incident_id | numeric | `radar incident id` | |
action_result.data.\*.id | numeric | | |
action_result.data.\*.content | string | | |
action_result.data.\*.created_at | string | | |
action_result.data.\*.created_by | string | | |
action_result.data.\*.updated_at | string | | |
action_result.data.\*.updated_by | string | | |
action_result.status | string | | success failed |
action_result.message | string | | Successfully fetched notes |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

______________________________________________________________________

Auto-generated Splunk SOAR Connector documentation.

Copyright 2026 Splunk Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations under the License.
