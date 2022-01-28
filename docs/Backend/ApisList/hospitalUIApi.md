# Hospital UI Api

Note:

---
## Update hospital profile
>- **Mapping:** PUT (role HOSPITALADMIN)
>- **URL:** /api/i/hospital/{hospitalId}
>> Long hospitalId
>- **Request:** HospitalProfileDTO
>>- String name
>>- String contactPersonFirstName
>>- String contactPersonLastName
>>- String contactEmail
>>- String contactMobile
>>- List&LT;String> departments
>>- String address
>>- String postCode
>>- String state
>- **Response:** HospitalDTO or String error message
>>- Long id
>>- String email
>>- String mobile
>>- Long userId
>- if used: 

## Add hospitalstaff to a specific hospital
>- **Mapping:** POST (role HOSPITALADMIN)
>- **URL:** /api/i/hospital/{hospitalId}/addhospitalstaff
>> Long hospitalId
>- **Request:** HospitalStaffSignUpDTO
>>- String title
>>- String firstName
>>- String lastName
>>- String email
>>- String mobile
>>- String password
>- **Response:** HospitalStaffDTO or String error message 
>>- Long id
>>- String title
>>- String firstName
>>- String lastName
>>- String email
>>- String mobile
>>- Long userId
>>- Long hospitalId
>- if used: 

## Update a specific hospitalstaff
>- **Mapping:** PUT (role HOSPITALADMIN)
>- **URL:** /api/i/hospitalstaff/updatehospitalstaff
>- **Request:** HospitalStaffProfileDTO
>>- Long id
>>- String title
>>- String firstName
>>- String lastName
>>- String email
>>- String mobile
>>- String department
>>- String subDepartment
>>- String jobTitle
>>- String speciality
>>- String clinicalFocus
>>- String academicQualification
>>- String hospitalAccreditation
>>- String positionHel
>>- String directManager
>>- String homeAddress
>>- String zipCode
>>- String state
>>- String language
>- **Response:** HospitalStaffDTO or String error message
>>- Long id
>>- String title
>>- String firstName
>>- String lastName
>>- String email
>>- String mobile
>>- Long userId
>>- Long hospitalId
>- if used: 

## Delete a specific hospitalstaff
>- **Mapping:** DELETE (role HOSPITALADMIN)
>- **URL:** /api/i/hospitalstaff/{hospitalStaffId}
>> Long hospitalStaffId
>- **Request:** 
>- **Response:** String message deleted or not
>- if used: 

## Update new password for a specific hospitalstaff
>- **Mapping:** Put (role HOSPITALADMIN or HOSPITALUSER)
>- **URL:** /api/i/hospitalstaff/updatepassword
>- **Request:** ResetPasswordDTO
>>- String email
>>- String code
>>- String password
>- **Response:** String message updated or not
>- if used: 

## Searches a hospital staff
>- **Mapping:** Get (role HOSPITALADMIN)
>- **URL:** /api/i/hospitalstaff/searchhospitalstaff/{hospitalStaffId}
>> Long hospitalStaffId
>- **Request:** 
>- **Response:** HospitalStaffDTO or String error message
>>- Long id
>>- String title
>>- String firstName
>>- String lastName
>>- String email
>>- String mobile
>>- Long userId
>>- Long hospitalId
>- if used: 

## 	Get all hospitalstaffs from a specific hospital
>- **Mapping:** Get (role HOSPITALADMIN)
>- **URL:** /api/i/hospitalstaff/allhospitalstaff/{hospitalId}
>> Long hospitalId
>- **Request:** 
>- **Response:** List&LT;HospitalStaffDTO> or String error message
>>- Long id
>>- String title
>>- String firstName
>>- String lastName
>>- String email
>>- String mobile
>>- Long userId
>>- Long hospitalId
>- if used: 
