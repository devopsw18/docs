# Not Logged In Api

Note: These APIs are for all UIs

---
## Sends code to given email
>- **Mapping:** POST
>- **URL:** /api/register/code
>- **Request:** EmailAndMobileDTO
>>- String email
>>- String mobile
>- **Response:** String message sent or not
>- if used: 

## Validate email with a four-digits code
>- **Mapping:** POST
>- **URL:** /api/register/code/validate
>- **Request:** ValidateCodeDTO
>>- String email
>>- String code
>- **Response:** String message verified or not
>- if used: Should not be used together with forgot_password since validating a code deletes it.

## Register an admin account
>- **Mapping:** POST
>- **URL:** /api/register/admin
>- **Request:** AdminSignupDTO
>>- String email
>>- String password
>>- String mobile
>- **Response:** UserDTO or String error message
>>- Long userId
>>- String email
>>- String mobile
>>- List&LT;String> roles
>- if used: Do not use. This will probably be removed or it will require extra validation/safety checks (like an already existing admin validating your registration)

## Register a patient account
>- **Mapping:** POST
>- **URL:** /api/register/patient
>- **Request:** PatientSignupDTO
>>- String email
>>- String mobile
>>- String password
>>- String closestHospital
>>- String referralCode?
>>- ~~boolean profileComplete~~
>- **Response:** PatientSignUpResponseDTO or String error message
>>- Long userId
>>- String email
>>- String mobile
>>- Long patientId
>>- String jwt
>- if used: 

## Register a doctor account
>- **Mapping:** POST
>- **URL:** /api/register/doctor
>- **Request:** form-data(String doctorSignUpDTO + MultipartFile multipartFile)
>> doctorSignUpDTO
>>- String mobile
>>- String email
>>- String fullName
>>- String password
>>- String referralCode
>>- List&LT;Reference> references
>>>- String name
>>>- String email
>- **Response:** DoctorDTO or String error message
>>- Long userId
>>- String mobile
>>- String email
>>- Long doctorId
>>- String systemStatus
>- if used: Request should be sent as form-data with doctorSignUpDTO and multipartFile

## Register a lab admin account
>- **Mapping:** POST
>- **URL:** /api/register/labadmin
>- **Request:** LabSignupDTO
>>- String mobile
>>- String email
>>- String password
>>- String location
>>- String labName
>>- String referralCode?
>- **Response:** UserDTO or String error message
>>- Long userId
>>- String email
>>- String mobile
>>- List&LT;String> roles
>- if used: 

## Register a lab scientist account
>- **Mapping:** POST
>- **URL:** /api/register/labscientist
>- **Request:** LabScientistSignupDTO
>>- String mobile
>>- String email
>>- String password
>>- String referralCode?
>- **Response:** UserDTO or String error message
>>- Long userId
>>- String email
>>- String mobile
>>- List&LT;String> roles
>- if used: 

## Register a pharmacy admin account
>- **Mapping:** POST
>- **URL:** /api/register/pharmacy
>- **Request:** PharmacySignUpDTO
>>- String email
>>- String mobile
>>- String password
>>- String location
>>- String pharmacyName
>- **Response:** UserDTO or String error message
>>- Long userId
>>- String email
>>- String mobile
>>- List&LT;String> roles
>- if used: 

## Register a pharmacist account
>- **Mapping:** POST
>- **URL:** /api/register/pharmacy
>- **Request:** PharmacistRegistrationDTO
>>- String mobile
>>- String email
>>- String password
>>- String referralCode?
>- **Response:** UserDTO or String error message
>>- Long userId
>>- String email
>>- String mobile
>>- List&LT;String> roles
>- if used: 

## Register a hospital account
>- **Mapping:** POST
>- **URL:** /api/register/hospital
>- **Request:** HospitalSignUpDTO
>>- String email
>>- String mobile
>>- String location
>>- String hospitalName
>>- String password
>- **Response:** UserDTO or String error message
>>- Long userId
>>- String email
>>- String mobile
>>- List&LT;String> roles
>- if used: 

## Register a hospital staff account
>- **Mapping:** POST
>- **URL:** /api/register/hospitalstaff
>- **Request:** HospitalStaffSignUpDTO
>>- String title
>>- String firstName
>>- String lastName
>>- String email
>>- String mobile
>>- String password
>- **Response:** UserDTO or String error message
>>- Long userId
>>- String email
>>- String mobile
>>- List&LT;String> roles
>- if used: 

## Log in to app
>- **Mapping:** POST
>- **URL:** /api/login
>- **Request:** LoginDTO
>>- String emailOrMobile
>>- String password
>- **Response:** JwtDTO or String error message
>>- String token
>>- String type
>>- Long id
>>- String mobile
>>- String email
>>- Long typeId
>>- List&LT;String> role
>- if used: 

## Send verification Code to email for reset the password
>- **Mapping:** POST
>- **URL:** /api/forgotpassword/code
>- **Request:** EmailAndMobileDTO
>>- String email
>>- String mobile
>- **Response:** String message sent or not
>- if used: 


## Validate code and reset the password
>- **Mapping:** POST
>- **URL:** /api/forgotpassword
>- **Request:** ResetPasswordDTO
>>- String email
>>- String code
>>- String password
>- **Response:** String message reset or not
>- if used: 