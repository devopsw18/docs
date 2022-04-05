---
sidebar_position: 3
sidebar_label: Reference Survey API
---

# Reference Survey API

---

## Submits a reference survey
>- **Mapping:** POST
>- **URL:** /api/referencesurvey/submit
>- **Request:** ReferenceSurveyDTO
>>- Long id
>>- String responderEmail
>>- String responderName
>>- Long doctorId
>>- String doctorFullName
>>- List&LT;String> questions
>>- List&LT;String> answers
>>- String notes
>- **Response:** String message submitted or not
>- if used: 

## Generate Survey
>- **Mapping:** POST
>- **URL:** /api/referencesurvey/getsurvey
>- **Request:** ReferenceSurveyVerificationDTO
>>- String email
>>- String responderName
>>- Long doctorId
>- **Response:** ReferenceSurveyDTO or String error message
>>- Long id
>>- String responderEmail
>>- String responderName
>>- Long doctorId
>>- String doctorFullName
>>- List&LT;String> questions
>>- List&LT;String> answers
>>- String notes
>- if used: 

## Send reference request to reference email
>- **Mapping:** POST (role DOCTOR)
>- **URL:** /api/i/referencesurvey/sendReferenceRequest
>- **Request:** SendReferenceRequestDTO
>>- String referenceEmail
>>- String referenceName
>>- String doctorFullName
>>- Long doctorId
>- **Response:** String message sent or not
>- if used: 

## Get all reference survey by doctor Id
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/i/referencesurvey/getSurveysByDoctorId/{doctorId}
>> Long doctorId
>- **Request:** 
>- **Response:** List&LT;ReferenceSurvey>
>>- Long id
>>- String responderEmail
>>- String responderName
>>- Long doctorId
>>- String doctorFullName
>>- List&LT;String> questions
>>- List&LT;String> answers
>>- String notes
>- if used: 

## 
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/i/referencesurvey/getSurveyById/{surveyId}
>> Long surveyId
>- **Request:** 
>- **Response:** ReferenceSurvey
>>- Long id
>>- String responderEmail
>>- String responderName
>>- Long doctorId
>>- String doctorFullName
>>- List&LT;String> questions
>>- List&LT;String> answers
>>- String notes
>- if used: 

## Get all survey question
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/i/referencesurvey/getAllQuestions
>- **Request:** 
>- **Response:** List&LT;SurveyQuestion>
>>- Long id
>>- String question
>- if used: 

## Create a survey question
>- **Mapping:** POST (role SYSTEMADMIN)
>- **URL:** /api/i/referencesurvey/addQuestion
>- **Request:** SurveyQuestionDTO
>>- String question
>>- ~~Long id~~
>- **Response:** String message added
>- if used: 

## 
>- **Mapping:** POST (role SYSTEMADMIN)
>- **URL:** /api/i/referencesurvey/updateQuestion
>- **Request:** SurveyQuestionDTO
>>- Long id
>>- String question
>- **Response:** String message updated or not
>- if used: 

## 
>- **Mapping:** DELETE (role SYSTEMADMIN)
>- **URL:** /api/i/referencesurvey/deleteQuestionById/{questionId}
>> Long questionId
>- **Request:** 
>- **Response:** String message deleted or not
>- if used: 
