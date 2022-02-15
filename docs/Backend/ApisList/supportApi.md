# Support Api

Note:

---
## Create support messages by patient, doctor, pharmacy, pharmacyAdmin
>- **Mapping:** POST (role PATIENT, DOCTOR, PHARMACY, PHARMACYADMIN)
>- **URL:** /api/i/support/{userId}/createsupport
>> Long userId
>- **Request:** SupportDTO
>>- String subject
>>- String supportMSG
>>- ~~Long supportId~~
>>- ~~Long userId~~
>>- ~~Long handler~~
>>- ~~Boolean isHandled~~
>- **Response:** String message created or not
>- if used: 

## Get all unanswered messages
>- **Mapping:** GET (role PATIENT or SUPPORT) 
>- **URL:** /api/i/support/getallmessages
>- **Request:** 
>- **Response:** List&LT;Support>
>>- Long supportId
>>- Long userId
>>- String subject
>>- String supportMSG
>>- LocalDate dateCreated
>>- boolean isHandled
>>- Long handler
>- if used: change the role to SUPPORT in API

## Get all unanswered messages for a specific patient
>- **Mapping:** GET (role PATIENT or SUPPORT)
>- **URL:** /api/i/support/{userId}
>> Long userId
>- **Request:** 
>- **Response:** List&LT;Support>
>>- Long supportId
>>- Long userId
>>- String subject
>>- String supportMSG
>>- LocalDate dateCreated
>>- boolean isHandled
>>- Long handler
>- if used: change the role to SUPPORT in API

## Update a support message
>- **Mapping:** PUT(role SUPPORT)
>- **URL:** /api/i/support/update
>- **Request:** SupportDTO
>>- Long supportId
>>- Long userId
>>- String subject
>>- String supportMSG
>>- Long handler
>>- Boolean isHandled
>- **Response:** SupportDTO or String error message
>>- Long supportId
>>- Long userId
>>- String subject
>>- String supportMSG
>>- Long handler
>>- Boolean isHandled
>- if used: 