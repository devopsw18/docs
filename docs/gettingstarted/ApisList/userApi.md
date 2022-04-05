---
sidebar_position: 3
sidebar_label: User API
---

# User Api

---
## Update a users password
>- **Mapping:** PUT
>- **URL:** /api/i/user/updatePassword/{userId}
>> Long userId
>- **Request:** UpdatePasswordDTO
>>- String currentPassword
>>- String newPassword
>- **Response:** String message update or not
>- if used: 

## Update a users email
>- **Mapping:** PUT
>- **URL:** /api/i/user/updateEmail/{userId}
>> Long userId
>- **Request:** UpdateEmailDTO
>>- String code
>>- String password
>>- String newEmail
>- **Response:** String message updated or not
>- if used: 

## Update a users email
>- **Mapping:** PUT
>- **URL:** /api/i/user/updatePhoneNumber/{userId}
>> Long userId
>- **Request:** UpdateEmailDTO
>>- String password
>>- String newPhoneNumber
>- **Response:** String message updated or not
>- if used: 

## Sends a code to a email address
>- **Mapping:** PUT
>- **URL:** /api/i/user/code/{userId}
>> Long userId
>- **Request:** EmailDTO
>>- String email
>- **Response:** String message sent or not
>- if used: 
