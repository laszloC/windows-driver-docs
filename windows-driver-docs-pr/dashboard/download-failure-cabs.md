---
title: Download failure Cabs
description: Use the report delivered as part of the Get Report Data API to retrieve the CabURL and then download the failure cab.
author: balapv
ms.author: balapv
ms.date: 08/20/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
---

# Download Failure Cabs

You can use the report delivered as part of the Get Report Data API to retrieve the CabURL and then download the failure cab before the URL expires. Please continue to use one of the following Cab Download APIs to get the download link to the cab file by passing the CabIdHash.

- [Download the CAB file for an OEM hardware error](https://docs.microsoft.com/windows/uwp/monetize/download-the-cab-file-for-an-oem-hardware-error)

- [Download the CAB file for a Windows 10 driver error](https://docs.microsoft.com/windows/uwp/monetize/download-the-cab-file-for-a-windows-10-driver-error)

## REQUEST

### Request Syntax

|Method|Request URI|
|----|----|
|Get|`https://manage.devcenter.microsoft.com/v1.0/my/analytics/driver/cabdownloadbatch`|

### Request Header

|Header|Type|Description|
|----|----|----|
|Authorization|string|Required. The Azure AD access token in the form **Bearer** *\<token\>*.|

### Request parameters

|Parameter|Type|Description|Required|
|----|----|----|----|
|applicationId|string|The product ID value of the driver for which you want to retrieve error data.|Yes|
|failureHash|string|The unique ID of the error for which you want to get detailed info.|Yes|
|startDate|date|The start date in the date range of error reporting data to retrieve. The default is 30 days before the current date.|No|
|endDate|date|The end date in the date range of error reporting data to retrieve. The default is the current date.|No|
|top|int|The number of rows of data to return in the request. The maximum value and the default value if not specified is 100. If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.|No|
|skip|int|The number of rows to skip in the query. Use this parameter to page through large data sets. For example, top=100 and skip=0 retrieves the first 100 rows of data, top=100 and skip=100 retrieves the next 100 rows of data, and so on.|No|

### Request example

The following example demonstrates how to getting cabURIs using this method.

```json
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/driver/cabdownloadbatch?
applicationId=13984104677400476&failureHash=1fd83f6d-9fe0-96ec-2c47-ef08b65ccbed
HTTP/1.1
Authorization: Bearer <your access token>
```

## RESPONSE

The following example demonstrates an example JSON response body for this request.

```json
{
  "Value": [
      {
      "applicationId": "13984104677400476",
      "submissionId": "29989690_13984104677400476_1152921504626153337",
      "failureHash": "1fd83f6d-9fe0-96ec-2c47-ef08b65ccbed",
      "cabIdHash": "fb57b37b-d364-4caf-995b-d99ae651ee18",
      "cabUrl": "https://uswewatcab09.blob.core.windows.net/kernel-20170407/fb57b37b-d364-4caf-995b-d99ae651ee18.ext.zip?sv=2015-07-08&sr=b&sig=lRVFxW%2F7GlumJHas0QxX5%2Bnvkrdi5lqijKQaGeB%2BUQA%3D&se=2017-04-28T02%3A37%3A28Z&sp=r",
      "date": "2017-04-07 13:53:43",
      "cabExpirationTime": "2017-05-07 13:53:43"
    },
    {
      "applicationId": "13984104677400476",
      "submissionId": "29989690_13984104677400476_1152921504626153337",
      "failureHash": "1fd83f6d-9fe0-96ec-2c47-ef08b65ccbed",
      "cabIdHash": "e261603b-1e86-4094-bca5-7ac4f8bf1aab",
      "cabUrl": "https://uswewatcab12.blob.core.windows.net/kernel-20170406/e261603b-1e86-4094-bca5-7ac4f8bf1aab.ext.zip?sv=2015-07-08&sr=b&sig=WCM3yNXJsIb1ME4hQICNGHBxSCWU%2FPq7ykCGNrd3lNo%3D&se=2017-04-28T02%3A37%3A28Z&sp=r",
      "date": "2017-04-07 06:17:01",
      "cabExpirationTime": "2017-05-07 06:17:01"
    }]
}
```

## See also

- [Analytics Reporting APIs (Swagger )](https://apidocs.microsoft.com/services/analyticsreportingapis)