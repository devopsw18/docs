---
sidebar_position: 3
sidebar_label: Laboratory API
---

# Laboratory UI API

---
## Adds a scientist to database
>- **Mapping:** POST (role LABADMIN)
>- **URL:** /api/i/laboratory/addscientist
>- **Request:** ScientistDTO
>>- String title
>>- String firstName
>>- String lastName
>>- String email
>>- String mobile
>>- Long labId
>>- ~~Long id~~
>- **Response:** String message created or not
>- if used: 


## Add a laboratory to the database
>- **Mapping:** POST (role LABADMIN)
>- **URL:** /api/i/laboratory/addlab
>- **Request:** LaboratoryDTO
>>- String labName
>>- String contactPerson
>>- String email
>>- String mobileNumber
>>- String address
>>- String postcode
>>- String state
>>- ~~Long id~~
>>- ~~Long signerId~~
>- **Response:** String message created or not
>- if used: 


## Update a laboratory in the database
>- **Mapping:** PUT (role LABADMIN)
>- **URL:** /api/i/laboratory/{labid}/updatelabprofile
>> Long labid
>- **Request:** LaboratoryDTO
>>- String labName
>>- String contactPerson
>>- String email
>>- String mobileNumber
>>- String address
>>- String postcode
>>- String state
>>- ~~Long id~~
>>- ~~Long signerId~~
>- **Response:** String message updated or not
>- if used: 


## Gets all scientists from database
>- **Mapping:** GET (role LABADMIN or SYSTEMADMIN)
>- **URL:** /api/i/laboratory/getallscientists
>- **Request:** 
>- **Response:** List&LT;ScientistDTO>
>>- Long id
>>- String title
>>- String firstName
>>- String lastName
>>- String email
>>- String mobile
>>- Long labId
>- if used: 

## Get a specific scientist
>- **Mapping:** GET (role LABADMIN or SYSTEMADMIN)
>- **URL:** /api/i/laboratory/{scientistid}
>> Long scientistid
>- **Request:** 
>- **Response:** ScientistDTO or String error message
>>- Long id
>>- String title
>>- String firstName
>>- String lastName
>>- String email
>>- String mobile
>>- Long labId
>- if used: 

## Update a scientist profile
>- **Mapping:** PUT (role LABADMIN)
>- **URL:** /api/i/laboratory/{scientistid}/updatescientist
>- **Request:** ScientistDTO
>>- String title
>>- String firstName
>>- String lastName
>>- String email
>>- String mobile
>>- Long labId
>>- ~~Long id~~
>- **Response:** String message updated or not
>- if used: 

## Delete a scientist from database
>- **Mapping:** DELETE (role LABADMIN)
>- **URL:** /api/i/laboratory/{scientistid}/deletescientist
>> Long scientistid
>- **Request:** 
>- **Response:** String message deleted or not
>- if used: 

## Add a labrequest with a QR code to the database
>- **Mapping:** POST (role LABADMIN)
>- **URL:** /api/i/laboratory/labrequestentry
>- **Request:** LabRequestDTO
>>- String patientName
>>- Long patientId
>>- ELabRequest testRequested
>>- String doctorName
>>- String testReason
>>- ~~Long id~~
>>- ~~String date~~
>>- ~~byte[] qrCode~~
>- **Response:** String message created or not
>- if used: ELabRequest is enum

## Get all labrequest from database
>- **Mapping:** GET (role LABADMIN or SYSTEMADMIN)
>- **URL:** /api/i/laboratory/getalllabrequest
>- **Request:** 
>- **Response:** List&LT;LabRequest>
>>- Long id
>>- String patientName
>>- Long patientId
>>- ELabRequest testRequested
>>- String date
>>- String doctorName
>>- String testReason
>>- byte[] qrCode
>- if used: ELabRequest is enum

## 	Get all labrequest from database by patientId
>- **Mapping:** GET (role PATIENT or SYSTEMADMIN)
>- **URL:** /api/i/laboratory/getalllabrequests/{patientid}
>> Long patientid
>- **Request:** 
>- **Response:** List&LT;LabRequestDTO>
>>- Long id
>>- String patientName
>>- Long patientId
>>- ELabRequest testRequested
>>- String date
>>- String doctorName
>>- String testReason
>>- byte[] qrCode
>- if used: 

## 	Creates a labResult 
>- **Mapping:** POST (role LABSCIENTIST)
>- **URL:** /api/i/laboratory/labresult
>- **Request:** LabResultDTO
>>- String resultName
>>- long labRequestId
>>- String laboratory
>>- String result
>>- ~~Long id~~
>>- ~~long patientId~~
>>- ~~Boolean finished~~
>>- ~~String date~~
>>- ~~String testName~~
>- **Response:** LabResultDTO or String error message
>>- Long id
>>- String resultName
>>- long labRequestId
>>- long patientId
>>- Boolean finished
>>- String date
>>- String testName
>>- String laboratory
>>- String result
>- if used: 

## Sets a labResult as finished
>- **Mapping:** PUT (role LABSCIENTIST)
>- **URL:** /api/i/laboratory/labresult/{labResultId}/finish
>> Long labResultId
>- **Request:** 
>- **Response:** String message finished or not
>- if used: 

## Get a specific labResult
>- **Mapping:** GET (role LABSCIENTIST)
>- **URL:** /api/i/laboratory/labresult/{labResultId}
>> Long labResultId
>- **Request:** 
>- **Response:** LabResultDTO or String error message
>>- Long id
>>- String resultName
>>- long labRequestId
>>- long patientId
>>- Boolean finished
>>- String date
>>- String testName
>>- String laboratory
>>- String result
>- if used: 

## Get all LabResults by a specific labRequest
>- **Mapping:** GET (role LABSCIENTIST)
>- **URL:** /api/i/laboratory/labresult/getAllByLabRequestId/{labRequestId}
>> Long labRequestId
>- **Request:** 
>- **Response:** List&LT;LabResultDTO>
>>- Long id
>>- String resultName
>>- long labRequestId
>>- long patientId
>>- Boolean finished
>>- String date
>>- String testName
>>- String laboratory
>>- String result
>- if used: 

## Get all labResult by a specific patient
>- **Mapping:** GET (role PATIENT or DOCTOR)
>- **URL:** /api/i/laboratory/labresult/getAllByPatientId/{patientId}
>> Long patientId
>- **Request:** 
>- **Response:** List&LT;LabResultDTO>
>>- Long id
>>- String resultName
>>- long labRequestId
>>- long patientId
>>- Boolean finished
>>- String date
>>- String testName
>>- String laboratory
>>- String result
>- if used: 

## Update a labResult
>- **Mapping:** PUT (role LABSCIENTIST)
>- **URL:** /api/i/laboratory/labresult/update
>- **Request:** LabResultDTO
>>- Long id
>>- String resultName
>>- long labRequestId
>>- long patientId
>>- Boolean finished
>>- String date
>>- String testName
>>- String laboratory
>>- String result
>- **Response:** LabResultDTO or String error message
>>- Long id
>>- String resultName
>>- long labRequestId
>>- long patientId
>>- Boolean finished
>>- String date
>>- String testName
>>- String laboratory
>>- String result
>- if used: 
