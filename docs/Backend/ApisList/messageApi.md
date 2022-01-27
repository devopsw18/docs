# Message Api

Note: 

## Create new message
>- **Mapping:** POST (Role PATIENT, DOCTOR or SYSTEMADMIN)
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
>- **Mapping:** GET (Role SYSTEMADMIN)
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
>- **Mapping:** GET (Role PATIENT, DOCTOR or SYSTEMADMIN)
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

## set a specific message as readed
>- **Mapping:** PUT (Role PATIENT, DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/message/setread/{messageId}
>> Long messageId
>- **Request:** 
>- **Response:** String message seted or not
>- if used: 

## delete a specific message
>- **Mapping:** DELETE (Role PATIENT, DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/message/delete/{messageId}
>> Long messageId
>- **Request:** 
>- **Response:** String message deleted or not
>- if used: 

