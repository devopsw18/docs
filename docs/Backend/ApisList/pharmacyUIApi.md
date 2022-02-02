# Pharmacy UI Api

Note:

---
## Get a specific pharmacy
>- **Mapping:** GET (role PHARMACYADMIN)
>- **URL:** /api/i/pharmacy/{pharmacyId}
>> Long pharmacyId
>- **Request:** 
>- **Response:** PharmacyDTO or String error message
>>- Long id
>>- String email
>>- String mobile
>>- Long userId
>- if used: 

## Update pharmacy profile
>- **Mapping:** PUT (role PHARMACYADMIN)
>- **URL:** /api/i/pharmacy/{pharmacyId}
>> Long pharmacyId
>- **Request:** PharmacyProfileDTO
>>- String name
>>- String contactPersonFirstName
>>- String contactPersonLastName
>>- String companyRegistrationNumber
>>- String contactEmail
>>- String contactNumber
>>- String streetAddress
>>- String cityTown
>>- String state
>- **Response:** PharmacyDTO or String error message
>>- Long id
>>- String email
>>- String mobile
>>- Long userId
>- if used: 

## Create pharmacist for a specific pharmacy
>- **Mapping:** POST (role PHARMACYADMIN)
>- **URL:** /api/i/pharmacy/{pharmacyId}/addpharmacist
>> Long pharmacyId
>- **Request:** PharmacistSignUpDTO
>>- String title
>>- String fullName
>>- String email
>>- String mobile
>>- String password
>- **Response:** PharmacistDTO or String error message
>>- Long id
>>- String title
>>- String fullName
>>- String email
>>- String mobile
>>- Long userId
>>- Long pharmacyId
>- if used: 

## Update new password for a specific pharmacist
>- **Mapping:** PUT (role PHARMACYADMIN or PHARMACYUSER)
>- **URL:** /api/i/pharmacy/resetpassword
>- **Request:** ResetPasswordDTO
>>- String email
>>- String code
>>- String password
>- **Response:** String message updeted or not
>- if used: 

## Get a specific pharmacist
>- **Mapping:** GET (role PHARMACYADMIN)
>- **URL:** /api/i/pharmacist/{pharmacistId}
>> Long pharmacistId
>- **Request:** 
>- **Response:** PharmacistDTO or String error message
>>- Long id
>>- String title
>>- String fullName
>>- String email
>>- String mobile
>>- Long userId
>>- Long pharmacyId
>- if used: 

## Update a pharmacist
>- **Mapping:** PUT (role PHARMACYADMIN)
>- **URL:** /api/i/pharmacist/updatepharmacist
>- **Request:** PharmacistUpdateDTO
>>- Long id
>>- String title
>>- String fullName
>>- String email
>>- String mobile
>>- ~~Long userId~~
>- **Response:** PharmacistDTO or String error message
>>- Long id
>>- String title
>>- String fullName
>>- String email
>>- String mobile
>>- Long userId
>>- Long pharmacyId
>- if used: 

## Get all phramacists from a specific pharmacy
>- **Mapping:** GET (role PHARMACYADMIN)
>- **URL:** /api/i/pharmacist/{pharmacyId}/allpharmacists
>> Long pharmacyId
>- **Request:** 
>- **Response:** List&LT;PharmacistDTO> or String error message
>>- Long id
>>- String title
>>- String fullName
>>- String email
>>- String mobile
>>- Long userId
>>- Long pharmacyId
>- if used: 

## Delete a specific pharmacist
>- **Mapping:** DELETE (role PHARMACYADMIN)
>- **URL:** /api/i/pharmacist/{pharmacistId}
>> Long pharmacistId
>- **Request:** 
>- **Response:** String message deleted or not
>- if used: 