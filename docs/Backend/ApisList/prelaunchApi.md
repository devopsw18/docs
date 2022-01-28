# Prelaunch Api

Note: APis here always have response with http state 200, even error message 

---
## Preregister doctor to get information on the app
>- **Mapping:** POST
>- **URL:** /api/preregister/doctor
>- **Request:** PreLaunchDoctorRegistrationDTO
>>- String email
>>- String phoneNumber
>>- String referrerMobile
>>- String uploadedCV
>>- ~~Long doctorId~~
>>- ~~String dateTime~~
>- **Response:** String message created or not
>- if used: 

## Get a list of all uploaded CV-files
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/preregister/files
>- **Request:** 
>- **Response:** List&LT;String> CVs
>- if used: 

## Get a CV for a specific doctor
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/i/preregister/files/{doctorId}
>> Long doctorId
>- **Request:** 
>- **Response:** header with attachment:Filename.pdf and body with String CV
>- if used: 

## Get all preregistered doctors
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/preregister/getdoctors
>- **Request:** 
>- **Response:** List&LT;PreLaunchDoctorDTO>
>>- Long doctorId
>>- String email
>>- String phoneNumber
>>- String referrerMobile
>>- String dateTime
>- if used: 

## Preregister patient
>- **Mapping:** POST
>- **URL:** /api/preregister/patient
>- **Request:** PrelaunchPatientDTO
>>- String email
>>- String phoneNumber
>>- String referrerMobile
>>- String closestHospital
>>- ~~Long id~~
>>- ~~String dateTime~~
>- **Response:** String message created or not
>- if used: 

## Get all preregistered patients
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/preregister/getpatients
>- **Request:** 
>- **Response:** List&LT;PrelaunchPatientDTO>
>>- Long id
>>- String email
>>- String phoneNumber
>>- String referrerMobile
>>- String dateTime
>>- String closestHospital
>- if used: 

## Preregister hospital
>- **Mapping:** POST
>- **URL:** /api/preregister/hospital
>- **Request:** PrelaunchHospitalDTO
>>- String email
>>- String phoneNumber
>>- String referrerMobile
>>- ~~Long id~~
>>- ~~String dateTime~~
>- **Response:** String message created or not
>- if used: 

## Get all preregistered hospitals
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/preregister/gethospitals
>- **Request:** 
>- **Response:** List&LT;PrelaunchHospitalDTO>
>>- Long id
>>- String email
>>- String phoneNumber
>>- String referrerMobile
>>- String dateTime
>- if used: 

## Preregister pharmacy
>- **Mapping:** POST
>- **URL:** /api/preregister/pharmacy
>- **Request:** PrelaunchPharmacyDTO
>>- String email
>>- String phoneNumber
>>- String referrerMobile
>>- ~~Long id~~
>>- ~~String dateTime~~
>- **Response:** String message created or not
>- if used: 

## Get all preregistered pharmacies
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/preregister/getpharmacies
>- **Request:** 
>- **Response:** List&LT;PrelaunchPharmacyDTO>
>>- Long id
>>- String email
>>- String phoneNumber
>>- String referrerMobile
>>- String dateTime
>- if used: 

## Preregister laboratory
>- **Mapping:** POST
>- **URL:** /api/preregister/laboratory
>- **Request:** PrelaunchLaboratoryDTO
>>- String email
>>- String phoneNumber
>>- String referrerMobile
>>- ~~Long id~~
>>- ~~String dateTime~~
>- **Response:** String message created or not
>- if used: 

## Get all preregistered laboratories
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/preregister/getlaboratories
>- **Request:** 
>- **Response:** List&LT;PrelaunchLaboratoryDTO>
>>- Long id
>>- String email
>>- String phoneNumber
>>- String referrerMobile
>>- String dateTime
>- if used: 