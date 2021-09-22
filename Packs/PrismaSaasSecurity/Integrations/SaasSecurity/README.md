Use the SaaS Security integration to protect against cloud‑based threats by scanning and analyzing all your assets; applying Security policy to identify exposures, external collaborators, risky user behavior, and sensitive documents; and identifying the potential risks associated with each asset.

## Configure SaaSSecurity on Cortex XSOAR

1. Navigate to **Settings** > **Integrations** > **Servers & Services**.
2. Search for **SaaS Security**.
3. Click **Add instance** to create and configure a new integration instance.

    | **Parameter** | **Description** | **Required** |
    | --- | --- | --- |
    | Server URL | https://api.aperture.paloaltonetworks.com (US)<br/>https://api.aperture-eu.paloaltonetworks.com (EU)<br/>https://api.aperture-apac.paloaltonetworks.com (APAC) | True |
    | Client ID | Saas Security Client ID | True |
    | Client Secret | Saas Security Client Secret | True |
    | Fetch incidents | Whether to fetch incidents from the SaaS Security platform | False |
    | Incidents Fetch Interval |  | False |
    | Incident type |  | False |
    | Number of incidents per fetch | Minimum is 10 | True |
    | First fetch timestamp | (&lt;number&gt; &lt;time unit&gt;, e.g., 12 hours, 7 days) | False |
    | Fetch only incidents with matching state |  | False |
    | Fetch only incidents with matching severity | If nothing is selected, all severities will be used. | False |
    | Fetch only incidents with matching status | If nothing is selected, all statuses will be used. | False |
    | Fetch only incidents with matching App IDs | Comma-separated list of Application IDs. Run the 'saas-security-get-apps'
    command to return the Application ID, Name, and Type for all applications. | False |
    | Trust any certificate (not secure) |  | False |
    | Use system proxy settings |  | False |

4. Click **Test** to validate the URLs, token, and connection.
## Commands
You can execute these commands from the Cortex XSOAR CLI, as part of an automation, or in a playbook.
After you successfully execute a command, a DBot message appears in the War Room with the command details.
### saas-security-incidents-get
***
Retrieve incidents from the SaaS Security platform.


#### Base Command

`saas-security-incidents-get`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| limit | The number of incidents to pull. Default is 50, maximum is 200, minimum is 10. Default is 50. | Optional | 
| from | The start time of the query, filtered by the date the incident was updated, e.g., 2021-08-23T09:26:25.872Z. | Optional | 
| to | The end time of the query, filtered by the date the incident was updated, e.g., 2021-08-23T09:26:25.872Z. | Optional | 
| app_ids | Comma-separated list of application IDs. Run the 'saas-security-get-apps' command to return the Application ID, Name, and Type for all applications. | Optional | 
| state | 'The state of the incidents. If empty, retrieves all states. Possible values: "All", "Open", and "Closed".' | Optional | 
| severity | 'The severity of the incidents. In none is selected, all severities will be pulled. Possible values: "1", "2", "3", "4", and "5".' | Optional | 
| status | 'The status of the incidents. Possible values:"New", "Assigned", " In Progress", "Pending", "No Reason", "Business Justified", "Misidentified", "In The Cloud", and "Dismiss".' | Optional | 
| next_page | Get the next batch of incidents. No other argument is needed when providing this. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| SaasSecurity.Incident.incident_id | Number | Incident ID. | 
| SaasSecurity.Incident.tenant | String | Tenant associated with the incident. | 
| SaasSecurity.Incident.app_id | String | Application ID. | 
| SaasSecurity.Incident.app_name | String | Application name. | 
| SaasSecurity.Incident.app_type | String | Application type. | 
| SaasSecurity.Incident.cloud_id | String | Cloud ID. | 
| SaasSecurity.Incident.asset_name | String | Asset name. | 
| SaasSecurity.Incident.asset_sha256 | String | SHA256 hash value of the asset. | 
| SaasSecurity.Incident.asset_id | String | Asset ID. | 
| SaasSecurity.Incident.asset_page_uri | String | Asset page URI. | 
| SaasSecurity.Incident.asset_cloud_uri | String | Asset cloud URI. | 
| SaasSecurity.Incident.exposure_type | Number | Exposure type \(Internal/External\). | 
| SaasSecurity.Incident.exposure_level | String | Exposure level. | 
| SaasSecurity.Incident.policy_id | String | Policy ID. | 
| SaasSecurity.Incident.policy_name | String | Policy name. | 
| SaasSecurity.Incident.policy_version | Number | Policy version. | 
| SaasSecurity.Incident.policy_page_uri | String | Policy page URI. | 
| SaasSecurity.Incident.severity | String | Severity of the incident. | 
| SaasSecurity.Incident.status | String | Incident status. | 
| SaasSecurity.Incident.state | String | Incident state. | 
| SaasSecurity.Incident.category | String | Incident category. | 
| SaasSecurity.Incident.resolved_by | String | Name of the user who resolved the incident. | 
| SaasSecurity.Incident.resolution_date | Date | Date the incident was resolved. | 
| SaasSecurity.Incident.created_at | Date | Date the incident was created, e.g., \`2021-08-23T09:26:25.872Z\`. | 
| SaasSecurity.Incident.updated_at | Date | Date the incident was last updated, e.g., \`2021-08-24T09:26:25.872Z\`. | 
| SaasSecurity.Incident.asset_owner_id | String | ID of the asset owner. | 
| SaasSecurity.Incident.asset_owner_name | String | Name of the asset owner. | 
| SaasSecurity.Incident.asset_owner_email | String | Email of the asset owner. | 
| SaasSecurity.NextResultsPage | String | URI for the next batch of incidents. | 


#### Command Example
```!saas-security-incidents-get limit=11 app_ids=acf49b2389c09f26ad0ccd2b1a603328 from=2021-08-23T20:25:17.495Z state=open```

#### Context Example
```json
{
    "SaasSecurity": {
        "Incident": [
            {
                "app_id": "acf49b2389c09f26ad0ccd2b1a603328",
                "app_name": "Box 1",
                "app_type": "box",
                "asset_cloud_uri": "https://www.box.com/files/0/f/114948778953/1/f_675197457403",
                "asset_id": "61099dc26b544e38fa3ce06d",
                "asset_name": "SP0605 copy 6.java",
                "asset_owner_email": "xsoartest@cirrotester.com",
                "asset_owner_id": "22FD054D362DC548A9C22F25782E1DAEED03C12F3898CD0F2E2A1B4CF728D04BD644B3CC010FDAC3D10EC0D408F4F79AC147E3D56415D1052BCFCD899A8E249F",
                "asset_owner_name": "Xsoar test",
                "asset_page_uri": "https://xsoartest.staging.cirrotester.com/cloud_assets/61099dc26b544e38fa3ce06d",
                "asset_sha256": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
                "category": "business_justified",
                "cloud_id": "675197457403",
                "collaborators": [],
                "created_at": "2021-08-03T20:25:15.417Z",
                "data_patterns": [],
                "exposure_level": "internal",
                "exposure_type": 8,
                "group_ids": [],
                "incident_id": 4,
                "policy_id": "6109a5d0e64152534b240f48",
                "policy_page_uri": "https://xsoartest.staging.cirrotester.com/data_policies/6109a5d0e64152534b240f48",
                "policy_version": 1,
                "policy_name": "policy name",
                "resolution_date": "2021-08-24T07:44:21.608Z",
                "resolved_by": "api",
                "severity": "Low",
                "state": "closed",
                "status": "Closed-Business Justified",
                "tenant": "xsoartest",
                "updated_at": "2021-08-24T07:44:21.608Z"
            },
            {
                "app_id": "acf49b2389c09f26ad0ccd2b1a603328",
                "app_name": "Box 1",
                "app_type": "box",
                "asset_cloud_uri": "https://www.box.com/files/0/f/114948778953/1/f_675197556380",
                "asset_id": "61099dbe6b544e38fa3cc9b8",
                "asset_name": "SP0605 copy 2.java",
                "asset_owner_email": "xsoartest@cirrotester.com",
                "asset_owner_id": "22FD054D362DC548A9C22F25782E1DAEED03C12F3898CD0F2E2A1B4CF728D04BD644B3CC010FDAC3D10EC0D408F4F79AC147E3D56415D1052BCFCD899A8E249F",
                "asset_owner_name": "Xsoar test",
                "asset_page_uri": "https://xsoartest.staging.cirrotester.com/cloud_assets/61099dbe6b544e38fa3cc9b8",
                "asset_sha256": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
                "category": "business_justified",
                "cloud_id": "675197556380",
                "collaborators": [],
                "created_at": "2021-08-03T20:25:12.000Z",
                "data_patterns": [],
                "exposure_level": "internal",
                "exposure_type": 8,
                "group_ids": [],
                "incident_id": 1,
                "policy_id": "6109a5d0e64152534b240f48",
                "policy_page_uri": "https://xsoartest.staging.cirrotester.com/data_policies/6109a5d0e64152534b240f48",
                "policy_version": 1,
                "resolution_date": "2021-08-24T08:19:57.429Z",
                "resolved_by": "api",
                "severity": "Low",
                "status": "Closed-Business Justified",
                "tenant": "xsoartest",
                "updated_at": "2021-08-24T08:19:57.429Z"
            }
        ]
    }
}
```

#### Human Readable Output

>### Incidents
>|Incident Id|App Id|App Name|Asset Name|Exposure Level|Severity|Category|Created At|Updated At|
>|---|---|---|---|---|---|---|---|---|
>| 4 | acf49b2389c09f26ad0ccd2b1a603328 | Box 1 | SP0605 copy 6.java | internal | Low | business_justified | 2021-08-03T20:25:15.417Z | 2021-08-24T07:44:21.608Z |
>| 1 | acf49b2389c09f26ad0ccd2b1a603328 | Box 1 | SP0605 copy 2.java | internal | Low | business_justified | 2021-08-03T20:25:12.000Z | 2021-08-24T08:19:57.429Z |
>| 5 | acf49b2389c09f26ad0ccd2b1a603328 | Box 1 | SP0605 copy 7.java | internal | Low | aperture | 2021-08-03T20:25:16.842Z | 2021-08-24T17:08:51.022Z |
>| 8 | acf49b2389c09f26ad0ccd2b1a603328 | Box 1 | ml_file.java | internal | Low | aperture | 2021-08-03T20:25:17.043Z | 2021-08-24T17:10:37.433Z |
>| 3 | acf49b2389c09f26ad0ccd2b1a603328 | Box 1 | SP0605 copy 5.java | internal | Low | misidentified | 2021-08-03T20:25:13.770Z | 2021-08-25T14:29:42.288Z |


### saas-security-incident-get-by-id
***
Gets an incident by its ID.


#### Base Command

`saas-security-incident-get-by-id`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| id | The incident ID. | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| SaasSecurity.Incident.incident_id | Number | Incident ID. | 
| SaasSecurity.Incident.tenant | String | Tenant associated with the incident. | 
| SaasSecurity.Incident.app_id | String | Application ID. | 
| SaasSecurity.Incident.app_name | String | Application name. | 
| SaasSecurity.Incident.app_type | String | Application type. | 
| SaasSecurity.Incident.cloud_id | String | Cloud ID. | 
| SaasSecurity.Incident.asset_name | String | Asset name. | 
| SaasSecurity.Incident.asset_sha256 | String | SHA256 hash value of the asset. | 
| SaasSecurity.Incident.asset_id | String | Asset ID. | 
| SaasSecurity.Incident.asset_page_uri | String | Asset page URI. | 
| SaasSecurity.Incident.asset_cloud_uri | String | Asset cloud URI. | 
| SaasSecurity.Incident.exposure_type | Number | Exposure type \(Internal/External\). | 
| SaasSecurity.Incident.exposure_level | String | Exposure level. | 
| SaasSecurity.Incident.policy_id | String | Policy ID. | 
| SaasSecurity.Incident.policy_name | String | Policy name. | 
| SaasSecurity.Incident.policy_version | Number | Policy version. | 
| SaasSecurity.Incident.policy_page_uri | String | Policy page URI. | 
| SaasSecurity.Incident.severity | String | Severity of the incident. | 
| SaasSecurity.Incident.status | String | Incident status. | 
| SaasSecurity.Incident.state | String | Incident state. | 
| SaasSecurity.Incident.category | String | Incident category. | 
| SaasSecurity.Incident.resolved_by | String | Name of the user who resolved the incident. | 
| SaasSecurity.Incident.resolution_date | Date | Date the incident was resolved. | 
| SaasSecurity.Incident.created_at | Date | Date the incident was created, e.g., \`2021-08-23T09:26:25.872Z\`. | 
| SaasSecurity.Incident.updated_at | Date | Date the incident was last updated, e.g., \`2021-08-24T09:26:25.872Z\`. | 
| SaasSecurity.Incident.asset_owner_id | String | The ID of the asset owner. | 
| SaasSecurity.Incident.asset_owner_name | String | The name of the asset owner. | 
| SaasSecurity.Incident.asset_owner_email | String | The email address of the asset owner. | 


#### Command Example
```!saas-security-incident-get-by-id id=4```

#### Context Example
```json
{
    "SaasSecurity": {
        "Incident": {
            "app_id": "acf49b2389c09f26ad0ccd2b1a603328",
            "app_name": "Box 1",
            "app_type": "box",
            "asset_cloud_uri": "https://www.box.com/files/0/f/114948778953/1/f_675197457403",
            "asset_id": "61099dc26b544e38fa3ce06d",
            "asset_name": "SP0605 copy 6.java",
            "asset_owner_email": "xsoartest@cirrotester.com",
            "asset_owner_id": "22FD054D362DC548A9C22F25782E1DAEED03C12F3898CD0F2E2A1B4CF728D04BD644B3CC010FDAC3D10EC0D408F4F79AC147E3D56415D1052BCFCD899A8E249F",
            "asset_owner_name": "Xsoar test",
            "asset_page_uri": "https://xsoartest.staging.cirrotester.com/cloud_assets/61099dc26b544e38fa3ce06d",
            "asset_sha256": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
            "category": "business_justified",
            "cloud_id": "675197457403",
            "collaborators": [],
            "created_at": "2021-08-03T20:25:15.417Z",
            "data_patterns": [],
            "exposure_level": "internal",
            "exposure_type": 8,
            "group_ids": [],
            "incident_id": 4,
            "policy_id": "6109a5d0e64152534b240f48",
            "policy_page_uri": "https://xsoartest.staging.cirrotester.com/data_policies/6109a5d0e64152534b240f48",
            "policy_version": 1,
            "resolution_date": "2021-08-26T07:04:14.598Z",
            "resolved_by": "api",
            "severity": "Low",
            "state": "closed",
            "tenant": "xsoartest",
            "updated_at": "2021-08-26T07:04:14.598Z"
        }
    }
}
```

#### Human Readable Output

>### Incident 4 details
>|Incident Id|App Id|App Name|Asset Name|Exposure Level|Severity|State|Category|Created At|Updated At|
>|---|---|---|---|---|---|---|---|---|---|
>| 4 | acf49b2389c09f26ad0ccd2b1a603328 | Box 1 | SP0605 copy 6.java | internal | 1.0 | closed | business_justified | 2021-08-03T20:25:15.417Z | 2021-08-26T07:04:14.598Z |



### saas-security-incident-state-update
***
Close an incident and update its category.


#### Base Command

`saas-security-incident-state-update`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| id | The incident ID. | Required | 
| category | 'Reason for closing the incident. Possible values: "Misidentified", "No Reason", and "Business Justified".' | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| SaasSecurity.IncidentState.incident_id | String | The incident ID. | 
| SaasSecurity.IncidentState.state | String | Incident state \(open/closed\). | 
| SaasSecurity.IncidentState.category | String | Incident category. | 
| SaasSecurity.IncidentState.resolved_by | String | Name of the user who resolved the incident. | 
| SaasSecurity.IncidentState.resolution_date | Date | Date when the incident was resolved. | 


#### Command Example
```!saas-security-incident-state-update category="Business Justified" id=4```

#### Context Example
```json
{
    "SaasSecurity": {
        "IncidentState": {
            "category": "business_justified",
            "incident_id": "4",
            "resolution_date": "2021-08-26T07:04:14.598Z",
            "resolved_by": "api",
            "state": "closed"
        }
    }
}
```

#### Human Readable Output

>### Incident 4 status details
>|Category|Incident Id|Resolution Date|Resolved By|State|
>|---|---|---|---|---|
>| business_justified | 4 | 2021-08-26T07:04:14.598Z | api | closed |


### saas-security-get-apps
***
Returns the Application ID, Name, and Type for all applications.


#### Base Command

`saas-security-get-apps`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| SaasSecurity.App.app_name | String | Application name. | 
| SaasSecurity.App.app_id | String | Application ID. | 
| SaasSecurity.App.app_type | String | Application type. | 


#### Command Example
```!saas-security-get-apps```

#### Context Example
```json
{
    "SaasSecurity": {
        "App": [
            {
                "app_id": "acf49b2389c09f26ad0ccd2b1a603328",
                "app_name": "Box 1",
                "app_type": "box"
            },
            {
                "app_id": "2642aaa03dc6fc44496bdfffe5e1bc74",
                "app_name": "Office 365 1",
                "app_type": "office365"
            }
        ]
    }
}
```

#### Human Readable Output

>### Apps Info
>|App Id|App Name|App Type|
>|---|---|---|
>| acf49b2389c09f26ad0ccd2b1a603328 | Box 1 | box |
>| 2642aaa03dc6fc44496bdfffe5e1bc74 | Office 365 1 | office365 |


### saas-security-asset-remediate
***
Remediate an asset.


#### Base Command

`saas-security-asset-remediate`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| asset_id | The ID of the asset to remediate. | Required | 
| remediation_type | 'The remediation action to take. Possible values: "Remove public sharing", "Quarantine", and "Restore".' | Required | 
| remove_inherited_sharing | 'Used when the remediation type is “Remove public sharing”. When set
        to true, all the parent folders with a shared URL will be removed. Possible values: "True" and "False"' | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| SaasSecurity.Remediation.asset_id | String | Asset ID. | 
| SaasSecurity.Remediation.remediation_type | String | Remediation type. | 
| SaasSecurity.Remediation.status | String | Remediation action status. | 


#### Command Example
```!saas-security-asset-remediate asset_id=61099dc46b544e38fa3ce89a remediation_type=Quarantine```

#### Context Example
```json
{
    "SaasSecurity": {
        "Remediation": {
            "asset_id": "61099dc46b544e38fa3ce89a",
            "remediation_type": "system_quarantine",
            "status": "pending"
        }
    }
}
```

#### Human Readable Output

>### Remediation details for asset: 61099dc46b544e38fa3ce89a
>|Asset Id|Remediation Type|Status|
>|---|---|---|
>| 61099dc46b544e38fa3ce89a | system_quarantine | pending |


### saas-security-remediation-status-get
***
Get the remediation status for a given asset ID.


#### Base Command

`saas-security-remediation-status-get`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| asset_id | The asset ID. | Required | 
| remediation_type | 'The remediation action that was taken. Possible values: "Remove public sharing", "Quarantine", and "Restore".' | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| SaasSecurity.Remediation.asset_id | String | Asset ID. | 
| SaasSecurity.Remediation.asset_name | String | Asset name. | 
| SaasSecurity.Remediation.remediation_type | String | Remediation type. | 
| SaasSecurity.Remediation.action_taker | String | Source of the remediation action, e.g., 'api'. | 
| SaasSecurity.Remediation.action_date | Date | Date when the remediation action was taken. | 
| SaasSecurity.Remediation.status | String | Remediation action status. | 


#### Command Example
```!saas-security-remediation-status-get asset_id=61099dc46b544e38fa3ce89a remediation_type=Quarantine```

#### Context Example
```json
{
    "SaasSecurity": {
        "Remediation": {
            "action_date": "2021-08-25T21:18:37.148+0000",
            "action_taker": "api",
            "asset_id": "61099dc46b544e38fa3ce89a",
            "asset_name": "SP0605 copy.java",
            "remediation_type": "system_quarantine",
            "status": "success"
        }
    }
}
```

#### Human Readable Output

>### Asset 61099dc46b544e38fa3ce89a remediation details
>|Action Date|Action Taker|Asset Id|Asset Name|Remediation Type|Status|
>|---|---|---|---|---|---|
>| 2021-08-25T21:18:37.148+0000 | api | 61099dc46b544e38fa3ce89a | SP0605 copy.java | system_quarantine | success |
