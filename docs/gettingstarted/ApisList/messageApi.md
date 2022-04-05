---
sidebar_position: 3
sidebar_label: Message API
---

# Message API

---
## Create new message
>- **Mapping:** POST (role PATIENT, DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/message/create
>- **Request:** MessageDTO
>>- String subject
>>- Long receiverId
>>- String sender
>>- String text
>>- ~~Long id~~
>>- ~~String date~~
>>- ~~boolean hasBeenRead~~
>- **Response:** MessageDTO or String error message
>>- Long id
>>- String subject
>>- Long receiverId
>>- String sender
>>- String text
>>- String date
>>- boolean hasBeenRead
>- if used: 

## Get all messages in database
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/i/message/getall
>- **Request:** 
>- **Response:** List&LT;MessageDTO>
>>- Long id
>>- String subject
>>- Long receiverId
>>- String sender
>>- String text
>>- String date
>>- boolean hasBeenRead
>- if used: 

## Get all messages of a specific user
>- **Mapping:** GET (role PATIENT, DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/message/get/{userId}
>> Long userId
>- **Request:** 
>- **Response:** List&LT;MessageDTO> or String error message
>>- Long id
>>- String subject
>>- Long receiverId
>>- String sender
>>- String text
>>- String date
>>- boolean hasBeenRead
>- if used: 

## Set a specific message as readed
>- **Mapping:** PUT (role PATIENT, DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/message/setread/{messageId}
>> Long messageId
>- **Request:** 
>- **Response:** String message set or not
>- if used: 

## Delete a specific message
>- **Mapping:** DELETE (role PATIENT, DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/message/delete/{messageId}
>> Long messageId
>- **Request:** 
>- **Response:** String message deleted or not
>- if used: 

