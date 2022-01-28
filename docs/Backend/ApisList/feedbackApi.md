# Feedback Api

Note:

---
## Create feedback messages by patient, doctor, pharmacy, pharmacyAdmin
>- **Mapping:** POST (role PATIENT, DOCTOR, PHARMACY, PHARMACYADMIN or SYSTEMADMIN)
>- **URL:** /api/i/feedback/{userId}/createfeedback
>>- Long userId
>- **Request:** FeedBackDTO
>>- String experienceSoFar
>>- String addRemoveFeatures
>>- int easeOfUse
>>- ~~Long userId~~
>>- ~~Long feedbackId~~
>- **Response:** String message created or not
>- if used: 

## Support can view all feedback messages
>- **Mapping:** GET (role PATIENT, SUPPORT or SYSTEMADMIN)
>- **URL:** /api/i/support/getallmessages
>- **Request:** 
>- **Response:** List&LT;FeedBack>
>>- Long feedbackId
>>- Long userId
>>- String experienceSoFar
>>- LocalDate dateCreated
>>- int easeOfUse
>- if used: change the role to SUPPORT in API

## Support can view all feedback messages for a specific patient
>- **Mapping:** GET (role PATIENT, SUPPORT or SYSTEMADMIN)
>- **URL:** /api/i/support/{userId}
>>- Long userId
>- **Request:** 
>- **Response:** List&LT;FeedBack>
>>- Long feedbackId
>>- Long userId
>>- String experienceSoFar
>>- LocalDate dateCreated
>>- int easeOfUse
>- if used: change the role to SUPPORT in API
