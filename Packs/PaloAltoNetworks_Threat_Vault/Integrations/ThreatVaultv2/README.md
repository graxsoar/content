Use the Palo Alto Networks Threat Vault to research the latest threats (vulnerabilities/exploits, viruses, and spyware) that Palo Alto Networks next-generation firewalls can detect and prevent.
This integration was integrated and tested with version 2.0 of Palo Alto Networks Threat Vault v2

Some changes have been made that might affect your existing content. 
If you are upgrading from a previous of this integration, see [Breaking Changes](#breaking-changes-from-the-previous-version-of-this-integration---palo-alto-networks-threat-vault-v2).

## Configure Palo Alto Networks Threat Vault v2 on Cortex XSOAR

1. Navigate to **Settings** > **Integrations** > **Servers & Services**.
2. Search for Palo Alto Networks Threat Vault v2.
3. Click **Add instance** to create and configure a new integration instance.

    | **Parameter** | **Description** | **Required** |
    | --- | --- | --- |
    | URL |  | True |
    | API Key |  | True |
    | Source Reliability | Reliability of the source providing the intelligence data. |  |
    | Trust any certificate (not secure) |  | False |
    | Use system proxy settings |  | False |
    | Fetch incidents |  | False |
    | Incident type |  | False |
    | First fetch timestamp (&lt;number&gt; &lt;time unit&gt;, e.g., 3 days) | The time unit must be days, months, or years. | False |
    | Incidents Fetch Interval |  | False |

4. Click **Test** to validate the URLs, token, and connection.
## Commands
You can execute these commands from the Cortex XSOAR CLI, as part of an automation, or in a playbook.
After you successfully execute a command, a DBot message appears in the War Room with the command details.
### file
***
Checks the reputation of an antivirus in Threat Vault.


#### Base Command

`file`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| file | A comma-separated list of SHA256 or MD5 hashes of the antivirus signature. | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| DBotScore.Vendor | String | The vendor used to calculate the score. | 
| DBotScore.Score | Number | The actual score. | 
| DBotScore.Type | String | The indicator type. | 
| DBotScore.Indicator | String | The indicator that was tested. | 
| File.MD5 | String | The MD5 hash of the file. | 
| File.SHA1 | String | The SHA1 hash of the file. | 
| File.SHA256 | String | The SHA256 hash of the file. | 
| File.Malicious.Vendor | String | For malicious files, the vendor that made the decision. | 
| ThreatVault.FileInfo.filetype | String | The file type of the file. | 
| ThreatVault.FileInfo.sha256 | String | The SHA256 of the file. | 
| ThreatVault.FileInfo.sha1 | String | The SHA1 of the file. | 
| ThreatVault.FileInfo.md5 | String | The MD5 of the file. | 
| ThreatVault.FileInfo.size | String | The size of the file. | 
| ThreatVault.FileInfo.type | String | The type of the file. | 
| ThreatVault.FileInfo.family | String | The family of the file. | 
| ThreatVault.FileInfo.platform | String | The platform of the file. | 
| ThreatVault.FileInfo.wildfire_verdict | String | The Wildfire verdict. | 
| ThreatVault.FileInfo.create_time | String | The threat signature creation time. | 
| ThreatVault.FileInfo.signatures | String | The signatures. |

#### Command example
```!file file= 7a520be9db919a09d8ccd9b78c11885a6e97bc9cc87414558254cef3081dccf8```
#### Context Example
```json
{
    "DBotScore": {
        "Indicator": "7a520be9db919a09d8ccd9b78c11885a6e97bc9cc87414558254cef3081dccf8",
        "Reliability": "D - Not usually reliable",
        "Score": 3,
        "Type": "file",
        "Vendor": "Palo Alto Networks Threat Vault v2"
    },
    "File": {
        "Hashes": [
            {
                "type": "MD5",
                "value": "7e8d3744c0a06d3c7ca7f6dbfce3d576"
            },
            {
                "type": "SHA256",
                "value": "7a520be9db919a09d8ccd9b78c11885a6e97bc9cc87414558254cef3081dccf8"
            }
        ],
        "MD5": "7e8d3744c0a06d3c7ca7f6dbfce3d576",
        "Malicious": {
            "Description": null,
            "Vendor": "Palo Alto Networks Threat Vault v2"
        },
        "SHA256": "7a520be9db919a09d8ccd9b78c11885a6e97bc9cc87414558254cef3081dccf8"
    }
}
```

#### Human Readable Output

>### Hash 7a520be9db919a09d8ccd9b78c11885a6e97bc9cc87414558254cef3081dccf8 antivirus reputation:
>|Active|CreateTime|FileType|MD5|Release|SHA256|SignatureId|
>|---|---|---|---|---|---|---|
>| active | 2012-07-04T03:36:54Z | PE32 | 7e8d3744c0a06d3c7ca7f6dbfce3d576 | antivirus: {"first_release_version": "316", "first_release_time": "2010-10-04T17:03:41Z", "last_release_version": "786", "last_release_time": "2012-07-05T17:03:14Z"} | 7a520be9db919a09d8ccd9b78c11885a6e97bc9cc87414558254cef3081dccf8 | 93534285 |


### cve
***
Checks the reputation of CVE in Threat Vault.


#### Base Command

`cve`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| cve | A comma-separated list of CVE names. | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| DBotScore.Score | Number | The actual score. | 
| DBotScore.Type | String | The indicator type. | 
| CVE.ID | String | The CVE ID. | 
| CVE.Description | String | A description of the CVE. | 
| CVE.CVSS.Score | String | The CVSS of the CVE. | 
| CVE.Modified | String | The timestamp of when the CVE was last modified. | 
| CVE.Published | String | The timestamp of when the CVE was published. | 
| ThreatVault.Vulnerability.id | String | The unique ID of the signature. | 
| ThreatVault.Vulnerability.name | String | The name of the signature. | 
| ThreatVault.Vulnerability.description | String | The description of the signature. | 
| ThreatVault.Vulnerability.category | String | The threat category of the signature. | 
| ThreatVault.Vulnerability.min_version | String | The PAN-OS minimum version. | 
| ThreatVault.Vulnerability.max_version | String | The PAN-OS maximum version. | 
| ThreatVault.Vulnerability.severity | String | The severity of the threat. | 
| ThreatVault.Vulnerability.default_action | String | The default action when the signature is triggered. | 
| ThreatVault.Vulnerability.cve | Array | The CVE \(Common Vulnerabilities and Exposures\) of the threat. | 
| ThreatVault.Vulnerability.vendor. | Array | The vulnerability identifier issued by the vendor on advisories. | 
| ThreatVault.Vulnerability.reference | Array | The public reference of the threat. | 
| ThreatVault.Vulnerability.status | String | The status of the signature. | 
| ThreatVault.Vulnerability.details | Object | Any additional details of the signature. | 
| ThreatVault.Vulnerability.ori_release_version | String | The original release version of the signature. | 
| ThreatVault.Vulnerability.latest_release_version | String | The latest release version of the signature. | 
| ThreatVault.Vulnerability.ori_release_time | String | The original release time of the signature. | 
| ThreatVault.Vulnerability.latest_release_time | String | The latest release time of the signature. |

#### Command example
```!cve cve=CVE-2020-2040```
#### Context Example
```json
{
    "CVE": {
        "CVSS": {
            "Score": "critical"
        },
        "Description": "Palo Alto Networks PAN-OS is prone to a buffer overflow vulnerability while parsing certain crafted HTTP requests. The vulnerability is due to the lack of proper checks on HTTP requests, leading to an exploitable buffer overflow vulnerability. An attacker could exploit the vulnerability by sending crafted HTTP requests. A successful attack could lead to remote code execution.",
        "ID": "CVE-2020-2040",
        "Modified": "2020-09-09T09:45:08Z",
        "Published": "2020-09-09T09:45:08Z"
    },
    "DBotScore": {
        "Indicator": "CVE-2020-2040",
        "Score": 0,
        "Type": "cve",
        "Vendor": "Palo Alto Networks Threat Vault v2"
    }
}
```

#### Human Readable Output

>### CVE CVE-2020-2040 vulnerability reputation:
>|CVE|Category|Default action|ID|Latest release time|Latest release version|Name|Ori release time|Ori release version|Reference|Severity|Status|
>|---|---|---|---|---|---|---|---|---|---|---|---|
>| CVE-2020-2040 | code-execution | reset-server | 59255 | 2020-09-09T09:45:08Z | 8317 | Palo Alto Networks PAN-OS Buffer Overflow Vulnerability | 2020-09-09T09:45:08Z | 8317 | https://security.paloaltonetworks.com/CVE-2020-2040 | critical | released |


### threatvault-threat-signature-get
***
Gets the antivirus or anti-spyware or files signature.


#### Base Command

`threatvault-threat-signature-get`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| sha256 | A comma-separated list of SHA256 hashes of the antivirus signature. | Optional | 
| md5 | A comma-separated list of MD5 hash of the antivirus signature. | Optional | 
| signature_id | A comma-separated list of IDs of the anti-spyware or antivirus signature. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| DBotScore.Vendor | String | The vendor used to calculate the score. | 
| DBotScore.Score | Number | The actual score. | 
| DBotScore.Type | String | The indicator type. | 
| DBotScore.Indicator | String | The indicator that was tested. | 
| File.MD5 | String | The MD5 hash of the file. | 
| File.SHA1 | String | The SHA1 hash of the file. | 
| File.SHA256 | String | The SHA256 hash of the file. | 
| File.Malicious.Vendor | String | For malicious files, the vendor that made the decision. | 
| ThreatVault.Vulnerability.id | String | The unique ID of the signature. | 
| ThreatVault.Vulnerability.name | String | The name of the signature. | 
| ThreatVault.Vulnerability.description | String | The description of the signature. | 
| ThreatVault.Vulnerability.category | String | The threat category of the signature. | 
| ThreatVault.Vulnerability.min_version | String | The PAN-OS minimum version. | 
| ThreatVault.Vulnerability.max_version | String | The PAN-OS maximum version. | 
| ThreatVault.Vulnerability.severity | String | The severity of the threat. | 
| ThreatVault.Vulnerability.default_action | String | The default action when the signature is triggered. | 
| ThreatVault.Vulnerability.cve | Array | The CVE \(Common Vulnerabilities and Exposures\) of the threat. | 
| ThreatVault.Vulnerability.vendor. | Array | The vulnerability identifier issued by the vendor on advisories. | 
| ThreatVault.Vulnerability.reference | Array | The public reference of the threat. | 
| ThreatVault.Vulnerability.status | String | The status of the signature. | 
| ThreatVault.Vulnerability.details | Object | Any additional details of the signature. | 
| ThreatVault.Vulnerability.ori_release_version | String | The original release version of the signature. | 
| ThreatVault.Vulnerability.latest_release_version | String | The latest release version of the signature. | 
| ThreatVault.Vulnerability.ori_release_time | String | The original release time of the signature. | 
| ThreatVault.Vulnerability.latest_release_time | String | The latest release time of the signature. | 
| ThreatVault.Spyware.id | String | The unique ID of the signature. | 
| ThreatVault.Spyware.name | String | The name of the signature. | 
| ThreatVault.Spyware.description | String | The description of the signature. | 
| ThreatVault.Spyware.vendor | Array | The spyware identifier issued by the vendor on advisories. | 
| ThreatVault.Spyware.severity | String | The severity of the threat. | 
| ThreatVault.Spyware.default_action | String | The default action when the signature is triggered. | 
| ThreatVault.Spyware.details | Object | Any additional details of the signature. | 
| ThreatVault.Spyware.reference | Array | The public reference of the threat. | 
| ThreatVault.Spyware.status | String | The status of the signature. | 
| ThreatVault.Spyware.min_version | String | The PAN-OS minimum version. | 
| ThreatVault.Spyware.max_version | String | The PAN-OS maximum version. | 
| ThreatVault.Spyware.cve | Array | The CVE \(Common Vulnerabilities and Exposures\) of the threat. | 
| ThreatVault.Antivirus.id | String | The unique ID of the signature. | 
| ThreatVault.Antivirus.name | String | The name of the signature. | 
| ThreatVault.Antivirus.description | String | The description of the signature. | 
| ThreatVault.Antivirus.subtype | String | The subtype of the signature. | 
| ThreatVault.Antivirus.type | String | The type of the signature. | 
| ThreatVault.Antivirus.create_time | String | The create time of the signature. | 
| ThreatVault.Antivirus.related_sha256_hashes | String | The related SHA256 hashes of the threat. | 
| ThreatVault.Antivirus.release | String | The default action when the signature is triggered. | 
| ThreatVault.Fileformat.id | String | The unique ID of the signature. | 
| ThreatVault.Fileformat.name | String | The name of the signature. | 
| ThreatVault.Fileformat.description | String | The description of the signature. | 
| ThreatVault.Fileformat.category | String | The threat category of the signature. | 
| ThreatVault.Fileformat.min_version | String | The PAN-OS minimum version. | 
| ThreatVault.Fileformat.max_version | String | The PAN-OS maximum version. | 
| ThreatVault.Fileformat.severity | String | The severity of the threat. | 
| ThreatVault.Fileformat.default_action | String | The default action when the signature is triggered. | 
| ThreatVault.Fileformat.cve | Array | The CVE \(Common Vulnerabilities and Exposures\) of the threat. | 
| ThreatVault.Fileformat.vendor | Array | The file format identifier issued by the vendor on advisories. | 
| ThreatVault.Fileformat.reference | Array | The public reference of the threat. | 
| ThreatVault.Fileformat.status | String | The status of the signature. | 
| ThreatVault.Fileformat.details | Array | Any additional details of the signature. | 
| ThreatVault.Fileformat.ori_release_version | String | The original release version of the signature. | 
| ThreatVault.Fileformat.latest_release_version | String | The latest release version of the signature. | 
| ThreatVault.Fileformat.ori_release_time | String | The original release time of the signature. | 
| ThreatVault.Fileformat.latest_release_time | String | The latest release time of the signature. | 
| ThreatVault.FileInfo.filetype | String | The file type of the file. | 
| ThreatVault.FileInfo.sha256 | String | The SHA256 of the file. | 
| ThreatVault.FileInfo.sha1 | String | The SHA1 of the file. | 
| ThreatVault.FileInfo.md5 | String | The MD5 of the file. | 
| ThreatVault.FileInfo.size | String | The size of the file. | 
| ThreatVault.FileInfo.type | String | The type of the file. | 
| ThreatVault.FileInfo.family | String | The family of the file. | 
| ThreatVault.FileInfo.platform | String | The platform of the file. | 
| ThreatVault.FileInfo.wildfire_verdict | String | The Wildfire verdict. | 
| ThreatVault.FileInfo.create_time | String | The threat signature creation time. | 
| ThreatVault.FileInfo.signatures | String | The signatures. | 

#### Command example
```!threatvault-threat-signature-get signature_id=93534285```
#### Context Example
```json
{
    "ThreatVault": {
        "Antivirus": {
            "action": "",
            "create_time": "2010-10-01T03:28:57Z",
            "description": "This signature detected Worm/Win32.autorun.crck",
            "id": "93534285",
            "name": "Worm/Win32.autorun.crck",
            "related_sha256_hashes": [
                "7a520be9db919a09d8ccd9b78c11885a6e97bc9cc87414558254cef3081dccf8",
                "9e12c5cdb069f74487c11758e732d72047b72bedf4373aa9e3a58e8e158380f8"
            ],
            "release": {
                "antivirus": {
                    "first_release_time": "2010-10-04T17:03:41Z",
                    "first_release_version": "316",
                    "last_release_time": "2012-07-05T17:03:14Z",
                    "last_release_version": "786"
                }
            },
            "severity": "medium",
            "status": "active",
            "subtype": "virus",
            "type": "0"
        }
    }
}
```

#### Human Readable Output

>### 93534285 antivirus reputation:
>|Create time|ID|Name|Related sha256 hashes|Release|Severity|Subtype|
>|---|---|---|---|---|---|---|
>| 2010-10-01T03:28:57Z | 93534285 | Worm/Win32.autorun.crck | 7a520be9db919a09d8ccd9b78c11885a6e97bc9cc87414558254cef3081dccf8,<br/>9e12c5cdb069f74487c11758e732d72047b72bedf4373aa9e3a58e8e158380f8 | antivirus: {"first_release_version": "316", "first_release_time": "2010-10-04T17:03:41Z", "last_release_version": "786", "last_release_time": "2012-07-05T17:03:14Z"} | medium | virus |


### threatvault-release-note-get
***
Retrieves the release notes information by version.


#### Base Command

`threatvault-release-note-get`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| version | The release version (ex. 8446) or content version (ex. 8446-6886) of the release notes. | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| ThreatVault.ReleaseNote.release_version | String | The release version of the update. | 
| ThreatVault.ReleaseNote.type | String | The type of the release notes. | 
| ThreatVault.ReleaseNote.content_version | String | The content version of the update. | 
| ThreatVault.ReleaseNote.notes | Array | General notices and reminders. | 
| ThreatVault.ReleaseNote.decoders | Array | The decoder updates in the release notes. | 
| ThreatVault.ReleaseNote.spyware.new | Array | List of new entries. | 
| ThreatVault.ReleaseNote.spyware.modified | Array | List of modified entries. | 
| ThreatVault.ReleaseNote.spyware.disabled | Array | List of disabled entries. | 
| ThreatVault.ReleaseNote.vulnerability.new | Array | List of new entries. | 
| ThreatVault.ReleaseNote.vulnerability.modified | Array | List of modified entries. | 
| ThreatVault.ReleaseNote.vulnerability.disabled | Array | List of disabled entries. | 
| ThreatVault.ReleaseNote.applications.new | Array | List of new entries. | 
| ThreatVault.ReleaseNote.applications.modified | Array | List of modified entries. | 
| ThreatVault.ReleaseNote.applications.obsoleted | Array | List of obsolete entries. | 

#### Command example
```!threatvault-release-note-get version=8615```
#### Context Example
```json
{
    "ThreatVault": {
        "ReleaseNote": {
            "content_version": "8615-7549",
            "release_notes": {
                "applications": {
                    "modified": [],
                    "new": [],
                    "obsoleted": []
                },
                "data_correlation": {
                    "deleted": [],
                    "modified": [],
                    "new": []
                },
                "decoders": {
                    "modified": [],
                    "new": []
                },
                "file_type": {
                    "disabled": [],
                    "modified": [],
                    "new": []
                },
                "notes": [
                    "<p><strong>Reminder:</strong></p><ul><li>(8/23/22) As part of Applications and Threats content update 8609 (released August 17, 2022), we updated the&nbsp;<em data-stringify-type=\"italic\">vmware&nbsp;</em>App-ID to include coverage for VMware traffic that was previously identified using the&nbsp;<em data-stringify-type=\"italic\">ssl</em>&nbsp;App-ID. Please review&nbsp;<a class=\"c-link\" href=\"https://live.paloaltonetworks.com/t5/customer-resources/content-8609-vmware-app-id/ta-p/512741\" target=\"_blank\" rel=\"noopener noreferrer\" data-stringify-link=\"&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/content-8609-vmware-app-id/ta-p/512741' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/content-8609-vmware-app-id/ta-p/512741&lt;/a&gt;\" data-sk=\"tooltip_parent\">this article</a>&nbsp;for details.<br /><br /></li><li>(8/22/22)&nbsp;As part of the&nbsp;<a class=\"c-link\" href=\"https://live.paloaltonetworks.com/t5/customer-resources/app-id-decoders-enhancement-plan/ta-p/469547\" target=\"_blank\" rel=\"noopener noreferrer\" data-stringify-link=\"&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/app-id-decoders-enhancement-plan/ta-p/469547' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/app-id-decoders-enhancement-plan/ta-p/469547&lt;/a&gt;\" data-sk=\"tooltip_parent\" aria-describedby=\"sk-tooltip-5262\">App-ID&trade; decoders improvement process</a>&nbsp;and as announced on 6/30/2022, we released a&nbsp;<strong data-stringify-type=\"bold\"><em data-stringify-type=\"italic\">dns-non-rfc</em></strong>&nbsp;placeholder App-ID (beginning with content update 8586) and we intend to activate the decoder for this App-ID with the content update scheduled for September 20, 2022. Review&nbsp;<a class=\"c-link\" href=\"https://live.paloaltonetworks.com/t5/customer-resources/dns-app-id-enhancement-release-plan/ta-p/487590\" target=\"_blank\" rel=\"noopener noreferrer\" data-stringify-link=\"&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/dns-app-id-enhancement-release-plan/ta-p/487590' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/dns-app-id-enhancement-release-plan/ta-p/487590&lt;/a&gt;\" data-sk=\"tooltip_parent\">this article</a>&nbsp;for details.</li><li><p>(8/17/22) The update for App-IDs associated with Google Drive API traffic is scheduled for the new App-IDs content update on September 20, 2022. Refer to&nbsp;<a class=\"c-link\" tabindex=\"-1\" href=\"https://live.paloaltonetworks.com/t5/customer-resources/app-id-update-for-google-drive-apis/ta-p/504345\" target=\"_blank\" rel=\"noopener noreferrer\" data-stringify-link=\"&lt;a href='&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/app-id-update-for-google-drive-apis/ta-p/504345' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/app-id-update-for-google-drive-apis/ta-p/504345&lt;/a&gt;' target='_blank'&gt;&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/app-id-update-for-google-drive-apis/ta-p/504345&lt;' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/app-id-update-for-google-drive-apis/ta-p/504345&lt;&lt;/a&gt;;/a&gt;\" data-sk=\"tooltip_parent\" data-remove-tab-index=\"true\">this article</a>&nbsp;for the details.</p></li><li data-stringify-indent=\"0\" data-stringify-border=\"0\"><p>(8/17/22) We released new placeholder App-IDs for several new OT/ICS App-IDs (FL-net, OpenADR, SafetyNET, and Siemens-S7) in content update version 8609 and we intend to activate these new App-IDs with the new App-IDs content update scheduled for September 20, 2022. (Review&nbsp;<a class=\"c-link\" href=\"https://live.paloaltonetworks.com/t5/customer-resources/release-plan-for-fl-net-openadr-safetynet-and-siemens-s7-app-ids/ta-p/511342\" target=\"_blank\" rel=\"noopener noreferrer\" data-stringify-link=\"&lt;a href='&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/release-plan-for-fl-net-openadr-safetynet-and-siemens-s7-app-ids/ta-p/511342' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/release-plan-for-fl-net-openadr-safetynet-and-siemens-s7-app-ids/ta-p/511342&lt;/a&gt;' target='_blank'&gt;&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/release-plan-for-fl-net-openadr-safetynet-and-siemens-s7-app-ids/ta-p/511342&lt;' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/release-plan-for-fl-net-openadr-safetynet-and-siemens-s7-app-ids/ta-p/511342&lt;&lt;/a&gt;;/a&gt;\" data-sk=\"tooltip_parent\">the details here</a>.)</p></li><li data-stringify-indent=\"0\" data-stringify-border=\"0\"><p>(8/17/22) We released a new placeholder App-ID for PsExec traffic in content update version 8609 and we intend to activate this new App-ID, as well, with the new App-IDs content update scheduled for September 20,2022. (Review&nbsp;<a class=\"c-link\" href=\"https://live.paloaltonetworks.com/t5/customer-resources/new-app-id-announcement-psexec/ta-p/508023\" target=\"_blank\" rel=\"noopener noreferrer\" data-stringify-link=\"&lt;a href='&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/new-app-id-announcement-psexec/ta-p/508023' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/new-app-id-announcement-psexec/ta-p/508023&lt;/a&gt;' target='_blank'&gt;&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/new-app-id-announcement-psexec/ta-p/508023&lt;' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/new-app-id-announcement-psexec/ta-p/508023&lt;&lt;/a&gt;;/a&gt;\" data-sk=\"tooltip_parent\">the details here</a>.)</p></li><li data-stringify-indent=\"0\" data-stringify-border=\"0\"><p>(8/17/22) We introduced new App-ID tags to help you categorize your application traffic. The first four of these tags (Proxy Avoidance, Uploading, Posting, Editing, Downloading) are included content update version 8609 and we will continue to introduce one or more of these new App-ID tags in these same monthly content updates where we introduce new App-IDs. Watch these release notes for updates and review&nbsp;<a class=\"c-link\" href=\"https://live.paloaltonetworks.com/t5/customer-resources/app-id-new-tags-announcement/ta-p/508005\" target=\"_blank\" rel=\"noopener noreferrer\" data-stringify-link=\"&lt;a href='&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/app-id-new-tags-announcement/ta-p/508005' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/app-id-new-tags-announcement/ta-p/508005&lt;/a&gt;' target='_blank'&gt;&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/app-id-new-tags-announcement/ta-p/508005&lt;' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/app-id-new-tags-announcement/ta-p/508005&lt;&lt;/a&gt;;/a&gt;\" data-sk=\"tooltip_parent\">this article for details</a>&nbsp;about upcoming new App-ID tags.</p></li><li data-stringify-indent=\"0\" data-stringify-border=\"0\">(7/11/22; updated 8/1/22) As part of the&nbsp;<a class=\"c-link\" tabindex=\"-1\" href=\"https://live.paloaltonetworks.com/t5/customer-resources/app-id-decoders-enhancement-plan/ta-p/469547\" target=\"_blank\" rel=\"noopener noreferrer\" data-stringify-link=\"&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/app-id-decoders-enhancement-plan/ta-p/469547' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/app-id-decoders-enhancement-plan/ta-p/469547&lt;/a&gt;\" data-sk=\"tooltip_parent\" data-remove-tab-index=\"true\">App-ID&trade; decoders improvement process</a>, we will modify the&nbsp;<strong data-stringify-type=\"bold\"><em data-stringify-type=\"italic\">smtp&nbsp;</em></strong>App-ID. As announced on 7/11/2022, we intend to release an&nbsp;<strong data-stringify-type=\"bold\"><em data-stringify-type=\"italic\">smtp-non-rfc</em></strong>&nbsp;placeholder App-ID but now intend to do this with the Applications and Threats content update scheduled for September 20, 2022, and will then activate the decoder for this App-ID with the content update scheduled for October 18, 2022. Review&nbsp;<a class=\"c-link\" tabindex=\"-1\" href=\"https://live.paloaltonetworks.com/t5/customer-resources/smtp-app-id-enhancement-release-plan/ta-p/508224\" target=\"_blank\" rel=\"noopener noreferrer\" data-stringify-link=\"&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/smtp-app-id-enhancement-release-plan/ta-p/508224' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/smtp-app-id-enhancement-release-plan/ta-p/508224&lt;/a&gt;\" data-sk=\"tooltip_parent\" data-remove-tab-index=\"true\">this article</a>&nbsp;for the details.</li></ul>"
                ],
                "spyware": {
                    "disabled": [],
                    "modified": [
                        {
                            "action": "reset-both",
                            "attack_name": "Manuscrypt Command and Control Traffic Detection",
                            "category": "command-and-control",
                            "change_data": "improved detection logic to address a possible fp issue",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 86322,
                            "severity": "critical"
                        }
                    ],
                    "new": [
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22059,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22060,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22061,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22062,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22063,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22064,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22065,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22066,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22067,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22068,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22069,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22070,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22071,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22072,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22073,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22074,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22075,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22076,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22077,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Pastebin Command and Control Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 22078,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Manjusaka Default Command and Control Traffic Detection",
                            "category": "hacktool",
                            "change_data": "improved detection logic to cover a new c2 variant",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 86663,
                            "severity": "critical"
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "SocGholish Malware Download Traffic Detection",
                            "category": "spyware",
                            "change_data": "new coverage",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 86664,
                            "severity": "critical"
                        }
                    ]
                },
                "vulnerability": {
                    "disabled": [],
                    "modified": [
                        {
                            "action": "reset-both",
                            "attack_name": "Microsoft PowerPoint Presentation Buffer Overrun RCE Vulnerability",
                            "category": "code-execution",
                            "change_data": "improved detection logic to address a possible fp issue",
                            "cve": "CVE-2011-1270",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 33951,
                            "severity": "high",
                            "vendor": "MS11-036"
                        },
                        {
                            "action": "reset-server",
                            "attack_name": "Nagios XI SQL Injection Vulnerability",
                            "category": "code-execution",
                            "change_data": "improved detection logic to cover a new exploit",
                            "cve": "CVE-2021-37350",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 91633,
                            "severity": "critical",
                            "vendor": ""
                        },
                        {
                            "action": "reset-server",
                            "attack_name": "Jolokia Agent JNDI Injection Vulnerability",
                            "category": "code-execution",
                            "change_data": "improved detection logic to cover a new exploit",
                            "cve": "CVE-2018-1000130",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 92364,
                            "severity": "high",
                            "vendor": ""
                        },
                        {
                            "action": "reset-server",
                            "attack_name": "Microsoft Exchange Server Remote Code Execution Vulnerability",
                            "category": "code-execution",
                            "change_data": "improved detection logic to cover a new exploit",
                            "cve": "CVE-2022-23277",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 92903,
                            "severity": "high",
                            "vendor": ""
                        }
                    ],
                    "new": [
                        {
                            "action": "reset-server",
                            "attack_name": "H3C IMC Intelligent Management Center Remote Code Execution Vulnerability",
                            "category": "code-execution",
                            "change_data": "new coverage",
                            "cve": "",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 92955,
                            "severity": "medium",
                            "vendor": ""
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Apache APISIX Remote Code Execution Vulnerability",
                            "category": "code-execution",
                            "change_data": "improved detection logic to cover a new exploit",
                            "cve": "CVE-2022-24112",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 92980,
                            "severity": "critical",
                            "vendor": ""
                        },
                        {
                            "action": "alert",
                            "attack_name": "Ivanti Avalanche Web Server authenticate Authentication Bypass Vulnerability",
                            "category": "code-execution",
                            "change_data": "new coverage",
                            "cve": "CVE-2022-36980",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 92996,
                            "severity": "medium",
                            "vendor": ""
                        },
                        {
                            "action": "reset-server",
                            "attack_name": "Microsoft HTTP Protocol Stack Remote Code Execution Vulnerability",
                            "category": "code-execution",
                            "change_data": "new coverage",
                            "cve": "CVE-2022-21907",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 92998,
                            "severity": "critical",
                            "vendor": ""
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "PHP-Proxy Local File Inclusion Vulnerability",
                            "category": "info-leak",
                            "change_data": "improved detection logic to cover a new exploit",
                            "cve": "CVE-2018-19246",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 92999,
                            "severity": "high",
                            "vendor": ""
                        },
                        {
                            "action": "reset-both",
                            "attack_name": "Mozilla Firefox Prototype Pollution Vulnerability",
                            "category": "code-execution",
                            "change_data": "new coverage",
                            "cve": "CVE-2022-1802",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 93002,
                            "severity": "high",
                            "vendor": ""
                        },
                        {
                            "action": "reset-server",
                            "attack_name": "Open Web Analytics Remote Code Execution Vulnerability",
                            "category": "code-execution",
                            "change_data": "new coverage",
                            "cve": "CVE-2022-24637",
                            "max_version": "",
                            "min_version": "8.1.0",
                            "pan_id": 93014,
                            "severity": "critical",
                            "vendor": ""
                        }
                    ]
                }
            },
            "release_time": "2022-09-01T17:04:33Z",
            "release_version": 8615,
            "type": "content"
        }
    }
}
```

#### Human Readable Output

>### Release notes:
>|Content version|Disabled Spyware|Modified Spyware|Modified Vulnerability|New Spyware|New Vulnerability|Notes|Release time|Release version|type|
>|---|---|---|---|---|---|---|---|---|---|
>| 8615-7549 | {'severity': 'critical', 'pan_id': 86322, 'attack_name': 'Manuscrypt Command and Control Traffic Detection', 'category': 'command-and-control', 'action': 'reset-both', 'change_data': 'improved detection logic to address a possible fp issue', 'min_version': '8.1.0', 'max_version': ''} | {'severity': 'critical', 'pan_id': 86322, 'attack_name': 'Manuscrypt Command and Control Traffic Detection', 'category': 'command-and-control', 'action': 'reset-both', 'change_data': 'improved detection logic to address a possible fp issue', 'min_version': '8.1.0', 'max_version': ''} | severity: high<br/>pan_id: 33951<br/>attack_name: Microsoft PowerPoint Presentation Buffer Overrun RCE Vulnerability<br/>cve: CVE-2011-1270<br/>vendor: MS11-036<br/>category: code-execution<br/>action: reset-both<br/>change_data: improved detection logic to address a possible fp issue<br/>min_version: 8.1.0<br/>max_version:  | {'severity': 'critical', 'pan_id': 22059, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22060, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22061, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22062, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22063, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22064, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22065, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22066, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22067, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22068, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22069, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22070, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22071, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22072, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22073, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22074, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22075, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22076, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22077, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 22078, 'attack_name': 'Pastebin Command and Control Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 86663, 'attack_name': 'Manjusaka Default Command and Control Traffic Detection', 'category': 'hacktool', 'action': 'reset-both', 'change_data': 'improved detection logic to cover a new c2 variant', 'min_version': '8.1.0', 'max_version': ''},<br/>{'severity': 'critical', 'pan_id': 86664, 'attack_name': 'SocGholish Malware Download Traffic Detection', 'category': 'spyware', 'action': 'reset-both', 'change_data': 'new coverage', 'min_version': '8.1.0', 'max_version': ''} | severity: medium<br/>pan_id: 92955<br/>attack_name: H3C IMC Intelligent Management Center Remote Code Execution Vulnerability<br/>cve: <br/>vendor: <br/>category: code-execution<br/>action: reset-server<br/>change_data: new coverage<br/>min_version: 8.1.0<br/>max_version:  | <p><strong>Reminder:</strong></p><ul><li>(8/23/22) As part of Applications and Threats content update 8609 (released August 17, 2022), we updated the&nbsp;<em data-stringify-type="italic">vmware&nbsp;</em>App-ID to include coverage for VMware traffic that was previously identified using the&nbsp;<em data-stringify-type="italic">ssl</em>&nbsp;App-ID. Please review&nbsp;<a class="c-link" href="https://live.paloaltonetworks.com/t5/customer-resources/content-8609-vmware-app-id/ta-p/512741" target="_blank" rel="noopener noreferrer" data-stringify-link="&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/content-8609-vmware-app-id/ta-p/512741' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/content-8609-vmware-app-id/ta-p/512741&lt;/a&gt;" data-sk="tooltip_parent">this article</a>&nbsp;for details.<br /><br /></li><li>(8/22/22)&nbsp;As part of the&nbsp;<a class="c-link" href="https://live.paloaltonetworks.com/t5/customer-resources/app-id-decoders-enhancement-plan/ta-p/469547" target="_blank" rel="noopener noreferrer" data-stringify-link="&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/app-id-decoders-enhancement-plan/ta-p/469547' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/app-id-decoders-enhancement-plan/ta-p/469547&lt;/a&gt;" data-sk="tooltip_parent" aria-describedby="sk-tooltip-5262">App-ID&trade; decoders improvement process</a>&nbsp;and as announced on 6/30/2022, we released a&nbsp;<strong data-stringify-type="bold"><em data-stringify-type="italic">dns-non-rfc</em></strong>&nbsp;placeholder App-ID (beginning with content update 8586) and we intend to activate the decoder for this App-ID with the content update scheduled for September 20, 2022. Review&nbsp;<a class="c-link" href="https://live.paloaltonetworks.com/t5/customer-resources/dns-app-id-enhancement-release-plan/ta-p/487590" target="_blank" rel="noopener noreferrer" data-stringify-link="&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/dns-app-id-enhancement-release-plan/ta-p/487590' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/dns-app-id-enhancement-release-plan/ta-p/487590&lt;/a&gt;" data-sk="tooltip_parent">this article</a>&nbsp;for details.</li><li><p>(8/17/22) The update for App-IDs associated with Google Drive API traffic is scheduled for the new App-IDs content update on September 20, 2022. Refer to&nbsp;<a class="c-link" tabindex="-1" href="https://live.paloaltonetworks.com/t5/customer-resources/app-id-update-for-google-drive-apis/ta-p/504345" target="_blank" rel="noopener noreferrer" data-stringify-link="&lt;a href='&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/app-id-update-for-google-drive-apis/ta-p/504345' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/app-id-update-for-google-drive-apis/ta-p/504345&lt;/a&gt;' target='_blank'&gt;&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/app-id-update-for-google-drive-apis/ta-p/504345&lt;' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/app-id-update-for-google-drive-apis/ta-p/504345&lt;&lt;/a&gt;;/a&gt;" data-sk="tooltip_parent" data-remove-tab-index="true">this article</a>&nbsp;for the details.</p></li><li data-stringify-indent="0" data-stringify-border="0"><p>(8/17/22) We released new placeholder App-IDs for several new OT/ICS App-IDs (FL-net, OpenADR, SafetyNET, and Siemens-S7) in content update version 8609 and we intend to activate these new App-IDs with the new App-IDs content update scheduled for September 20, 2022. (Review&nbsp;<a class="c-link" href="https://live.paloaltonetworks.com/t5/customer-resources/release-plan-for-fl-net-openadr-safetynet-and-siemens-s7-app-ids/ta-p/511342" target="_blank" rel="noopener noreferrer" data-stringify-link="&lt;a href='&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/release-plan-for-fl-net-openadr-safetynet-and-siemens-s7-app-ids/ta-p/511342' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/release-plan-for-fl-net-openadr-safetynet-and-siemens-s7-app-ids/ta-p/511342&lt;/a&gt;' target='_blank'&gt;&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/release-plan-for-fl-net-openadr-safetynet-and-siemens-s7-app-ids/ta-p/511342&lt;' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/release-plan-for-fl-net-openadr-safetynet-and-siemens-s7-app-ids/ta-p/511342&lt;&lt;/a&gt;;/a&gt;" data-sk="tooltip_parent">the details here</a>.)</p></li><li data-stringify-indent="0" data-stringify-border="0"><p>(8/17/22) We released a new placeholder App-ID for PsExec traffic in content update version 8609 and we intend to activate this new App-ID, as well, with the new App-IDs content update scheduled for September 20,2022. (Review&nbsp;<a class="c-link" href="https://live.paloaltonetworks.com/t5/customer-resources/new-app-id-announcement-psexec/ta-p/508023" target="_blank" rel="noopener noreferrer" data-stringify-link="&lt;a href='&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/new-app-id-announcement-psexec/ta-p/508023' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/new-app-id-announcement-psexec/ta-p/508023&lt;/a&gt;' target='_blank'&gt;&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/new-app-id-announcement-psexec/ta-p/508023&lt;' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/new-app-id-announcement-psexec/ta-p/508023&lt;&lt;/a&gt;;/a&gt;" data-sk="tooltip_parent">the details here</a>.)</p></li><li data-stringify-indent="0" data-stringify-border="0"><p>(8/17/22) We introduced new App-ID tags to help you categorize your application traffic. The first four of these tags (Proxy Avoidance, Uploading, Posting, Editing, Downloading) are included content update version 8609 and we will continue to introduce one or more of these new App-ID tags in these same monthly content updates where we introduce new App-IDs. Watch these release notes for updates and review&nbsp;<a class="c-link" href="https://live.paloaltonetworks.com/t5/customer-resources/app-id-new-tags-announcement/ta-p/508005" target="_blank" rel="noopener noreferrer" data-stringify-link="&lt;a href='&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/app-id-new-tags-announcement/ta-p/508005' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/app-id-new-tags-announcement/ta-p/508005&lt;/a&gt;' target='_blank'&gt;&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/app-id-new-tags-announcement/ta-p/508005&lt;' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/app-id-new-tags-announcement/ta-p/508005&lt;&lt;/a&gt;;/a&gt;" data-sk="tooltip_parent">this article for details</a>&nbsp;about upcoming new App-ID tags.</p></li><li data-stringify-indent="0" data-stringify-border="0">(7/11/22; updated 8/1/22) As part of the&nbsp;<a class="c-link" tabindex="-1" href="https://live.paloaltonetworks.com/t5/customer-resources/app-id-decoders-enhancement-plan/ta-p/469547" target="_blank" rel="noopener noreferrer" data-stringify-link="&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/app-id-decoders-enhancement-plan/ta-p/469547' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/app-id-decoders-enhancement-plan/ta-p/469547&lt;/a&gt;" data-sk="tooltip_parent" data-remove-tab-index="true">App-ID&trade; decoders improvement process</a>, we will modify the&nbsp;<strong data-stringify-type="bold"><em data-stringify-type="italic">smtp&nbsp;</em></strong>App-ID. As announced on 7/11/2022, we intend to release an&nbsp;<strong data-stringify-type="bold"><em data-stringify-type="italic">smtp-non-rfc</em></strong>&nbsp;placeholder App-ID but now intend to do this with the Applications and Threats content update scheduled for September 20, 2022, and will then activate the decoder for this App-ID with the content update scheduled for October 18, 2022. Review&nbsp;<a class="c-link" tabindex="-1" href="https://live.paloaltonetworks.com/t5/customer-resources/smtp-app-id-enhancement-release-plan/ta-p/508224" target="_blank" rel="noopener noreferrer" data-stringify-link="&lt;a href='https://live.paloaltonetworks.com/t5/customer-resources/smtp-app-id-enhancement-release-plan/ta-p/508224' target='_blank'&gt;https://live.paloaltonetworks.com/t5/customer-resources/smtp-app-id-enhancement-release-plan/ta-p/508224&lt;/a&gt;" data-sk="tooltip_parent" data-remove-tab-index="true">this article</a>&nbsp;for the details.</li></ul> | 2022-09-01T17:04:33Z | 8615 | content |


### threatvault-threat-batch-search
***
Retrieves the threats signature metadata by ID, name, or sample hash (sha256 or md5) in batch mode. Batch limit is 100 entries.


#### Base Command

`threatvault-threat-batch-search`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| id | The signature IDs. | Optional | 
| md5 | The hash of the sample. | Optional | 
| name | The signature names. | Optional | 
| sha256 | The hash of the sample. | Optional | 
| type | Use together with the other fields to filter out the results. Possible values are: ips, fileformat, spyware, vulnerability, antivirus, dns, rtdns, spywarec2. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| ThreatVault.Antivirus.id | String | The unique ID of the signature. | 
| ThreatVault.Antivirus.name | String | The name of the signature. | 
| ThreatVault.Antivirus.description | String | The description of the signature. | 
| ThreatVault.Antivirus.subtype | String | The subtype of the signature. | 
| ThreatVault.Antivirus.type | String | The type of the signature. | 
| ThreatVault.Antivirus.create_time | String | The create time of the signature. | 
| ThreatVault.Antivirus.related_sha256_hashes | String | The related SHA256 hashes of the threat. | 
| ThreatVault.Antivirus.release | String | The default action when the signature is triggered. | 
| ThreatVault.FileInfo.filetype | String | The file type of the file. | 
| ThreatVault.FileInfo.sha256 | String | The SHA256 of the file. | 
| ThreatVault.FileInfo.sha1 | String | The SHA1 of the file. | 
| ThreatVault.FileInfo.md5 | String | The MD5 of the file. | 
| ThreatVault.FileInfo.size | String | The size of the file. | 
| ThreatVault.FileInfo.type | String | The type of the file. | 
| ThreatVault.FileInfo.family | String | The family of the file. | 
| ThreatVault.FileInfo.platform | String | The platform of the file. | 
| ThreatVault.FileInfo.wildfire_verdict | String | The Wildfire verdict. | 
| ThreatVault.FileInfo.create_time | String | The threat signature creation time. | 
| ThreatVault.FileInfo.signatures | String | The signatures. | 

#### Command example
```!threatvault-threat-batch-search sha256=380082fbf9e57bcd524648efce14c92a4cb58cb745c30ef29730959d79164549```
#### Context Example
```json
{
    "DBotScore": {
        "Indicator": "380082fbf9e57bcd524648efce14c92a4cb58cb745c30ef29730959d79164549",
        "Reliability": "D - Not usually reliable",
        "Score": 3,
        "Type": "file",
        "Vendor": "Palo Alto Networks Threat Vault v2"
    },
    "File": {
        "Hashes": [
            {
                "type": "MD5",
                "value": "ca066f965dfbc5392871d3fa281236cf"
            },
            {
                "type": "SHA1",
                "value": "d58869fb948c60bef544e1a36f4489fd76fd10ae"
            },
            {
                "type": "SHA256",
                "value": "380082fbf9e57bcd524648efce14c92a4cb58cb745c30ef29730959d79164549"
            }
        ],
        "MD5": "ca066f965dfbc5392871d3fa281236cf",
        "Malicious": {
            "Description": null,
            "Vendor": "Palo Alto Networks Threat Vault v2"
        },
        "SHA1": "d58869fb948c60bef544e1a36f4489fd76fd10ae",
        "SHA256": "380082fbf9e57bcd524648efce14c92a4cb58cb745c30ef29730959d79164549"
    },
    "ThreatVault": {
        "FileInfo": {
            "create_time": "2021-12-02T20:27:12Z",
            "family": "WGeneric",
            "filetype": "DLL",
            "md5": "ca066f965dfbc5392871d3fa281236cf",
            "platform": "Win32",
            "sha1": "d58869fb948c60bef544e1a36f4489fd76fd10ae",
            "sha256": "380082fbf9e57bcd524648efce14c92a4cb58cb745c30ef29730959d79164549",
            "signatures": {
                "antivirus": [
                    {
                        "action": "",
                        "create_time": "2019-06-19T17:06:12Z",
                        "description": "This signature detected trojan/Win32 DLL.razy.slo",
                        "id": "280392504",
                        "name": "trojan/Win32 DLL.razy.slo",
                        "related_sha256_hashes": [
                            "5c825eae80aa0f376626387193c8ededa445cb066ca36813c7af49428e372cfb",
                            "d4a06653ad6d25ab69595c69656ce4c7f8ec60874b77998777fed7e741ad7003",
                            "88a5a664dbd3459b4fd1e55e450786c493989b994606d7b8cbe589fb9358dd74",
                            "4977929b742a47fafd4e4d0e2b765428ce8ec2764a4463d083914b30aa4d3a1b",
                            "0b66779d8910e365c8de5ea030f9827ee32b418bc303c26e3252a4843b86118d",
                            "3b3d767226aa796013b075fd7d6baa432e3f2bf380c55655dedaa8ead038829e",
                            "b8cbc5c1b01ae17dec42eca0f4b448407a2d5b9f85580e0e122c1854f4f80e37",
                            "47e3da7e179b755a1ccc8fe8fc506a2fb15baff2c124b15cf2f5e29038f3d1ac",
                            "5cd3e058f6049a31a42c292ebb091a1b5ea4bd9c7bc6fed5ac8a33c5fc89924a",
                            "4a2b514a753611b464e7583ba512310cd58c8066f19b631134012ebe05cd0e5f"
                        ],
                        "release": {
                            "antivirus": {
                                "first_release_time": "2019-06-21T13:37:09Z",
                                "first_release_version": "3017",
                                "last_release_time": "2022-11-05T11:36:34Z",
                                "last_release_version": "4258"
                            },
                            "wildfire": {
                                "first_release_time": "2019-06-19T17:06:35Z",
                                "first_release_version": "359199",
                                "last_release_time": "2022-11-06T12:47:08Z",
                                "last_release_version": "713954"
                            }
                        },
                        "severity": "medium",
                        "status": "active",
                        "subtype": "virus",
                        "type": "0"
                    }
                ]
            },
            "size": "176128",
            "type": "Virus",
            "wildfire_verdict": "malicious"
        }
    }
}
```

#### Human Readable Output

>### File 380082fbf9e57bcd524648efce14c92a4cb58cb745c30ef29730959d79164549:
>|Active|CreateTime|Description|Family|FileType|MD5|Platform|Release|SHA1|SHA256|Severity|Signature Name|SignatureId|Size|Wildfire verdict|
>|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
>| active | 2021-12-02T20:27:12Z | This signature detected trojan/Win32 DLL.razy.slo | WGeneric | DLL | ca066f965dfbc5392871d3fa281236cf | Win32 | antivirus: {"first_release_version": "3017", "first_release_time": "2019-06-21T13:37:09Z", "last_release_version": "4258", "last_release_time": "2022-11-05T11:36:34Z"}<br/>wildfire: {"first_release_version": "359199", "first_release_time": "2019-06-19T17:06:35Z", "last_release_version": "713954", "last_release_time": "2022-11-06T12:47:08Z"} | d58869fb948c60bef544e1a36f4489fd76fd10ae | 380082fbf9e57bcd524648efce14c92a4cb58cb745c30ef29730959d79164549 | medium | trojan/Win32 DLL.razy.slo | 280392504 | 176128 | malicious |


### threatvault-threat-search
***
Retrieves threat metadata. The nature of the query is determined by the query parameter you provide.


#### Base Command

`threatvault-threat-search`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| cve | The CVE tied to the signature. | Optional | 
| vendor | The vendor ID tied to the signatures. | Optional | 
| signature-name | The signature name. | Optional | 
| from-release-date | The release dates range (use with the to-release-date argument), Format: YYYY-MM-DD or timestamp (&lt;number&gt; &lt;time unit&gt;, e.g., 12 hours, 7 days, 3 months, 1 year). | Optional | 
| to-release-date | The right boundary of date range query (use with the from-release-date argument), Format: YYYY-MM-DD or timestamp (&lt;number&gt; &lt;time unit&gt;, e.g., 12 hours, 7 days, 3 months, 1 year). | Optional | 
| from-release-version | The release versions range (use with the to-release-version argument). | Optional | 
| to-release-version | The right boundary of version range query (use with the from-release-version argument). | Optional | 
| release-date | The release date. Format: YYYY-MM-DD or timestamp (&lt;number&gt; &lt;time unit&gt;, e.g., 12 hours, 7 days, 3 months, 1 year). | Optional | 
| release-version | The release version. | Optional | 
| type | The threat type. Use together with the other fields to filter out the results. Possible values are: ips, fileformat, spyware, vulnerability, antivirus, dns, rtdns, spywarec2. | Optional | 
| page | Page number to get result from. Needs to be use with the page_size argument. | Optional | 
| page_size | The page size of the returned results. Needs to be use with the page argument. | Optional | 
| limit | The maximum number of results to return (default is 50). | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| ThreatVault.Vulnerability.id | String | The unique ID of the signature. | 
| ThreatVault.Vulnerability.name | String | The name of the signature. | 
| ThreatVault.Vulnerability.description | String | The description of the signature. | 
| ThreatVault.Vulnerability.category | String | The threat category of the signature. | 
| ThreatVault.Vulnerability.min_version | String | The PAN-OS minimum version. | 
| ThreatVault.Vulnerability.max_version | String | The PAN-OS maximum version. | 
| ThreatVault.Vulnerability.severity | String | The severity of the threat. | 
| ThreatVault.Vulnerability.default_action | String | The default action when the signature is triggered. | 
| ThreatVault.Vulnerability.cve | Array | The CVE \(Common Vulnerabilities and Exposures\) of the threat. | 
| ThreatVault.Vulnerability.vendor. | Array | The vulnerability identifier issued by the vendor on advisories. | 
| ThreatVault.Vulnerability.reference | Array | The public reference of the threat. | 
| ThreatVault.Vulnerability.status | String | The status of the signature. | 
| ThreatVault.Vulnerability.details | Object | Any additional details of the signature. | 
| ThreatVault.Vulnerability.ori_release_version | String | The original release version of the signature. | 
| ThreatVault.Vulnerability.latest_release_version | String | The latest release version of the signature. | 
| ThreatVault.Vulnerability.ori_release_time | String | The original release time of the signature. | 
| ThreatVault.Vulnerability.latest_release_time | String | The latest release time of the signature. | 
| ThreatVault.Spyware.id | String | The unique ID of the signature. | 
| ThreatVault.Spyware.name | String | The name of the signature. | 
| ThreatVault.Spyware.description | String | The description of the signature. | 
| ThreatVault.Spyware.vendor | Array | The spyware identifier issued by the vendor on advisories. | 
| ThreatVault.Spyware.severity | String | The severity of the threat. | 
| ThreatVault.Spyware.default_action | String | The default action when the signature is triggered. | 
| ThreatVault.Spyware.details | Object | Any additional details of the signature. | 
| ThreatVault.Spyware.reference | Array | The public reference of the threat. | 
| ThreatVault.Spyware.status | String | The status of the signature. | 
| ThreatVault.Spyware.min_version | String | The PAN-OS minimum version. | 
| ThreatVault.Spyware.max_version | String | The PAN-OS maximum version. | 
| ThreatVault.Spyware.cve | Array | The CVE \(Common Vulnerabilities and Exposures\) of the threat. | 
| ThreatVault.Antivirus.id | String | The unique ID of the signature. | 
| ThreatVault.Antivirus.name | String | The name of the signature. | 
| ThreatVault.Antivirus.description | String | The description of the signature. | 
| ThreatVault.Antivirus.subtype | String | The subtype of the signature. | 
| ThreatVault.Antivirus.type | String | The type of the signature. | 
| ThreatVault.Antivirus.create_time | String | The create time of the signature. | 
| ThreatVault.Antivirus.related_sha256_hashes | String | The related SHA256 hashes of the threat. | 
| ThreatVault.Antivirus.release | String | The default action when the signature is triggered. | 
| ThreatVault.Fileformat.id | String | The unique ID of the signature. | 
| ThreatVault.Fileformat.name | String | The name of the signature. | 
| ThreatVault.Fileformat.description | String | The description of the signature. | 
| ThreatVault.Fileformat.category | String | The threat category of the signature. | 
| ThreatVault.Fileformat.min_version | String | The PAN-OS minimum version. | 
| ThreatVault.Fileformat.max_version | String | The PAN-OS maximum version. | 
| ThreatVault.Fileformat.severity | String | The severity of the threat. | 
| ThreatVault.Fileformat.default_action | String | The default action when the signature is triggered. | 
| ThreatVault.Fileformat.cve | Array | The CVE \(Common Vulnerabilities and Exposures\) of the threat. | 
| ThreatVault.Fileformat.vendor | Array | The file format identifier issued by the vendor on advisories. | 
| ThreatVault.Fileformat.reference | Array | The public reference of the threat. | 
| ThreatVault.Fileformat.status | String | The status of the signature. | 
| ThreatVault.Fileformat.details | Array | Any additional details of the signature. | 
| ThreatVault.Fileformat.ori_release_version | String | The original release version of the signature. | 
| ThreatVault.Fileformat.latest_release_version | String | The latest release version of the signature. | 
| ThreatVault.Fileformat.ori_release_time | String | The original release time of the signature. | 
| ThreatVault.Fileformat.latest_release_time | String | The latest release time of the signature. | 

#### Command example
```!threatvault-threat-search signature-name=Code+Injection+JS```
#### Context Example
```json
{
    "ThreatVault": {
        "Vulnerability": {
            "category": "code-execution",
            "cve": [
                "CVE-2020-28502"
            ],
            "default_action": "alert",
            "description": "Node.js is prone to a code injection vulnerability while parsing certain crafted HTTP requests. The vulnerability is due to the lack of proper checks on HTTP requests, leading to an exploitable code injection vulnerability. An attacker could exploit the vulnerability by sending crafted HTTP requests. A successful attack could lead to remote code execution with the privileges of the server.",
            "details": {
                "change_data": "new coverage"
            },
            "id": "91119",
            "latest_release_time": "2021-05-14T05:00:11Z",
            "latest_release_version": "8406",
            "max_version": "",
            "min_version": "8.1.0",
            "name": "Node.js Code Injection Vulnerability",
            "ori_release_time": "2021-05-14T05:00:11Z",
            "ori_release_version": "8406",
            "reference": [
                "https://github.com/s-index/CVE-2020-28502"
            ],
            "severity": "high",
            "status": "released",
            "vendor": []
        }
    }
}
```

#### Human Readable Output

>### 91119 vulnerability reputation:
>|CVE|Category|Default action|ID|Latest release time|Latest release version|Name|Ori release time|Ori release version|Reference|Severity|Status|
>|---|---|---|---|---|---|---|---|---|---|---|---|
>| CVE-2020-28502 | code-execution | alert | 91119 | 2021-05-14T05:00:11Z | 8406 | Node.js Code Injection Vulnerability | 2021-05-14T05:00:11Z | 8406 | https://github.com/s-index/CVE-2020-28502 | high | released |


## Breaking changes from the previous version of this integration - Palo Alto Networks Threat Vault v2

The following sections list the changes in this version.

### Commands
The following commands were removed in this version:
* ***threatvault-antivirus-signature-get*** - replaced by ***threatvault-threat-signature-get***.
* ***threatvault-dns-signature-get-by-id***.
* ***threatvault-antispyware-signature-get-by-id*** - replaced by ***threatvault-threat-signature-get***.
* ***threatvault-ip-geo-get***.
* ***ip***.
* ***threatvault-antivirus-signature-search*** - replaced by ***threatvault-threat-signature-search***.
* ***threatvault-dns-signature-search*** - replaced by ***threatvault-threat-signature-search***.
* ***threatvault-antispyware-signature-search*** - replaced by ***threatvault-threat-signature-search***.
* ***threatvault-signature-search-results***.

## Additional Considerations for this version
Note: The Threat Vault API key is **not** the same as the Autotargeting API key. Make sure you have the required API key, as instructed on the integration configuration page.
