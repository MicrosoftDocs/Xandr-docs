---
title: App Email Service
description: The App Email service manages automatic email notifications sent to admin users when apps are installed, modified, or deleted.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# App email service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The app email service is an admin-only service that manages automatic email notifications sent to admin users when apps are installed, modified, or deleted. This is also the service used to change the content of email notifications on app install, modification, or deletion.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/app-email`<br> <br>(`new_email` JSON) | Add an app email |
| `PUT` | `https://api.appnexus.com/app-email?id=ID` <br>(`update_email` JSON) | Modify an existing app email |
| `GET` | `https://api.appnexus.com/app-email` | View all app emails |
| `GET` | `https://api.appnexus.com/app-email?id=ID` | View a specific app email |
| `DELETE` | `https://api.appnexus.com/app-email?id=ID` | Delete an app email |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | **Read Only**. The auto-generated ID of the email being sent through the `app_email` service.<br>**Required On**: `PUT`, `DELETE` |
| `recipient` | string | The name of the person, people, team, or teams receiving the email. Name(s) may contain up to 225 characters.<br>**Required On**: `POST (JSON)` |
| `type` | string | The type field is used to assign a category to the email - for example `"data team"` or `"services bugs"`. It may contain up to 225 characters.<br>**Default**: `null` |
| `action` | enum | The event that trigger the notification email. Possible values are <br> - `"put"` <br> - `"post"` <br> - `"delete"`. <br><br>**Default**: `POST`<br>**Required On**: `POST (JSON)` |
| `recipient_emails` | string | The email addresses of the people who should receive the notification. Can contain specific email addresses separated by commas and/or a variable that pulls specific emails from the database to populate the field.<br><br>Examples:<br>- `name1@appnexus.com` <br>- `name1@appnexus.com,name2@appnexus.com`<br>- `%developer_email%,name1@appnexus.com`<br> - `%developer_email%,%installer_email%`<br><br>**Required On**: `POST (JSON)` |
| `subject` | string | The text that will appear in the subject field of the email.<br>**Required On**: `POST (JSON)` |
| `body` | string | The body of the email. Does not have a character limit.<br>**Required On**: `POST (JSON)` |
| `bcc` | string | The email addresses of the people who should receive the notification as bcc recipients. Can contain specific email addresses separated by commas and/or a variable that pulls specific emails from the database to populate the field.<br><br>Examples:<br> - `name1@appnexus.com` <br> - `name1@appnexus.com,name2@appnexus.com`<br> - `%developer_email%,name1@appnexus.com`<br> - `%developer_email%,%installer_email%`<br><br>**Default**: `null` |

## Examples

### Add a new app email

```
$ cat new_email.json
                      {
                      "app-email": {
                      "recipient": "Jane User",
                      "action": "put",
                      "recipient_emails": "juser@email.com",
                      "subject": "App Added",
                      "body": "Hello world!"
                      }
                      }
                      $ curl -b cookies -c cookies -X POST -d @new_email.json 'https://api.appnexus.com/app-email'
                      {
                      "response": {
                      "status": "OK"
                      "count": 1
                      "id": 54
                      "start_element": 0
                      "num_elements": 100
                      "app-email": {
                      "id": 54
                      "recipient": "Jane User"
                      "type": null
                      "action": "put"
                      "recipient_emails": "juser@email.com"
                      "subject": "App Added"
                      "body": "Hello world!"
                      "bcc": null
                      }
                      }
                      }
```

### Update an existing app email

```
$ cat update_email.json
                      {
                      "app-email":
                      {
                      "body": "Goodbye world!"
                      }
                      }
                      $ curl -b cookies -c cookies -X PUT -d @update_email 'https://api.appnexus.com/app-email?id=30'
                      {
                      "response": {
                      "status": "OK"
                      "count": 1
                      "id": "30"
                      "start_element": 0
                      "num_elements": 100
                      "app-email": {
                      "id": 30
                      "recipient": "DataTeam"
                      "type": "LogLevelData"
                      "action": "delete"
                      "recipient_emails": "psung@appnexus.com"
                      "subject": "Log Level Data consuming app %app_name% (%app_id%) has been uninstalled"
                      "body": "Goodbye world!"
                      "bcc": null
                      }
                      }
                      }
```

### View all app emails

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/app-email'
                      
                      {
                      "response": {
                      "status": "OK"
                      "count": 3
                      "start_element": 0
                      "num_elements": 100
                      "app-emails": [
                      {
                      "id": 29
                      "recipient": "SalesOps"
                      "type": "LogLevelData"
                      "action": "post"
                      "recipient_emails": "psung@appnexus.com"
                      "subject": "Log Level Data consuming app %app_name% (%app_id%) has been installed"
                      "body": "<p>Hi SalesOps, </p> <p>%subscriber_entity_name% (%subscriber_entity_id%) has installed %app_name% (%app_id%) on %installed_on%. Since %app_name% consumes LLD, please make the appropriate updates in SFDC. </p> <p>Thanks, <br /> The Apps Team</p>"
                      "bcc": null
                      },
                      {
                      "id": 32
                      "recipient" "AppDeveloper"
                      "type": null
                      "action": "delete"
                      "recipient_emails": "%developer_email%"
                      "subject": "%subscriber_entity_name% has uninstalled %app_name%"
                      "body": "<p>Hi %app_name%, </p> <p>%subscriber_entity_name% (%subscriber_entity_id%) has uninstalled your app on AppNexus. They uninstalled on %uninstalled_on%. This email is for your records.</p> <p>Thanks, <br /> The Apps Team<br /> </p>"
                      "bcc": "auser@appnexus.com"
                      },
                      {
                      "id": 34
                      "recipient": "AppSubscriber"
                      "type": null
                      "action": "delete"
                      "recipient_emails": "%installer_email%"
                      "subject": "You have uninstalled %app_name%"
                      "body": "<p>Hi %subscriber_entity_name%,</p> <p>You have uninstalled %app_name% (%app_id%) at %uninstalled_on%. This                           email is for your records. </p> <p>Thanks, <br /> The Apps Team</p>"
                      "bcc": null
                      }
                      ]
                      }
                      }
```

### View a specific app email

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/app-email?id=54'
                      
                      {
                      "response": {
                      "status": "OK"
                      "count": 1
                      "start_element": 0
                      "num_elements": 100
                      "app-email": {
                      "id": 54
                      "recipient": "Jane User"
                      "type": null
                      "action": "put"
                      "recipient_emails": "juser@email.com"
                      "subject": "App Added"
                      "body": "Hello world!"
                      "bcc": null
                      }
                      }
                      }
```

### Delete an app email

```
$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/app-email?id=54
                      {
                      "response": {
                      "status": "OK"
                      }
                      }
```
