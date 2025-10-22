---
title: Registration Form Service
description: Explore the Registration Form service to upload the registration forms required by certain states for political advertising purchased by independent expenditure committees.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Registration Form service

The Registration Form Service allows you to upload the registration forms required by certain states for political advertising purchased by independent expenditure committees. Creatives won't serve in New Jersey or New York State until the form is uploaded and associated with the appropriate insertion order.

> [!NOTE]
>
> - `PUT`and `DELETE`are not supported for this service. Instead of modifying an existing form, you must upload a new form and then associate the new form with the insertion order.
> - You must record the `file-location` specified in the response to the uploaded form so that you can associate the form with the appropriate insertion order. There is no way to retrieve this information later. If you did not record the file location and still need to associate the form with an insertion order, you will need to upload a new form.

## REST API

| HTTP Method | Endpoint | Description |
|---|---|---|
| `POST` | [https://api.appnexus.com/registration-form/upload-F uploadFile=@<local_path/local_file_name.pdf](https://api.appnexus.com/registration-form/upload)<br>where `local_path/local_file_name.pdf` is the path and name of the file to be uploaded.<br>If you do not have access to your local file path because you are calling the API from a browser, you will need to create a `FormData` object with the variable name `uploadFile` and upload that.<br>If you're using JavaScript to create a FormData object, for example, the code should look something like [this](#formdata-object). | Upload a new registration form. |
| `GET` | [https://api.appnexus.com/registration-form?member_id=MEMBER_ID](https://api.appnexus.com/registration-form?member_id=MEMBER_ID) | View all registration forms for a member. |
| `GET` | [https://api.appnexus.com/registration-form?file_path=FILE_PATH/FILE_NAME.PDF](https://api.appnexus.com/registration-form?file_path=FILE_PATH/FILE_NAME.PDF) | View a registration form.<br>To view a registration form, you must know the location to which the file was uploaded. Simply enter the URL in a browser or perform a `GET` on the URL. |

### `FormData` object

```
savePoliticalFormFile: async (uploadFile) => {
const formData = new FormData();
formData.append('uploadFile', uploadFile);
const response = await
httpPostMultiPart(`${API_URL}/registration-forms/upload`, formData);
return response['location'];
},
```

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `member_id` | int | The ID of the member.<br>**Required On:** `POST` |
| `file_path` | int | The location to which the file is uploaded. This is returned in the response and cannot be specified when uploading the file. |

## Examples

### Upload a registration form and associate the form with an insertion order

#### Upload a registration form

In this example, `NYS_Registration_Form_My_Favorite_Candidate.pdf` is the New York State disclosure form for the ad purchase by the independent expenditure committee.

```
curl -b cookies -X POST https://api.appnexus.com/registration-form/upload -F uploadFile=@/users/myname/NYS_Registration_Form_My_Favorite_Candidate.pdf>
```

The response includes the following:

```
{
    "file-path": "https://cleversafe03.appnexus.net/s3/political-ads-forms/p/958/20191010/fd241b14-1620-4e16-99d7-d57b19078649/A01055Registration20180907111141.PDF"
}
```

#### Associate the form with an insertion order

In this example, the insertion order used for political advertisements is `5432`.

```
cat io-registration-form.json
{
 
  "insertion-order": {
    "registration-forms": [
      {
        "file-path": "https://cleversafe03.appnexus.net/s3/political-ads-forms/p/958/20191010/fd241b14-1620-4e16-99d7-d57b19078649/A01055Registration20180907111141.PDF"
      }
    ]
  }
}
 
curl -b cookies -X PUT https://api.appnexus.com/insertion-order?id=5432 
```

### View an uploaded form

```
GET https://api.appnexus.com/registration-form?file_path=https://cleversafe03.appnexus.net/s3/political-ads-
forms/p/958/20191010/fd241b14-1620-4e16-99d7-d57b19078649/A01055Registration20180907111141.PDF
```

## Related topic

[Insertion Order Service](insertion-order-service.md)
