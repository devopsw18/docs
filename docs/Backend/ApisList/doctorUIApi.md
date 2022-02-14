# Doctor UI Api

Note:

---
## Get all doctors
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/i/doctors
>- **Request:** 
>- **Response:**  List &LT;DoctorDTO>
>>- Long userId
>>- String mobile
>>- String email
>>- Long doctorId
>>- String systemStatus
>- if used: 

## Get all doctors that has this kind of illness as speciality
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/i/doctors/{illnessId}
>> Long illnessId
>- **Request:** 
>- **Response:** List &LT;DoctorDTO>
>>- Long userId
>>- String mobile
>>- String email
>>- Long doctorId
>>- String systemStatus
>- if used: 

## Get a specific doctor
>- **Mapping:** GET (role DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/doctors/doctor/{userId}
>> Long userId
>- **Request:** 
>- **Response:** DoctorProfileDTO.Response or String error message
>>- Long userId
>>- String mobile
>>- String email
>>- Long doctorId
>>- String systemStatus
>>- Boolean approved
>>-  String fullName
>>- String dateOfBirth
>>- String gender
>>- String maritalStatus
>>- String officeAddress
>>- String city
>>- String state
>>- String mdcnCertificateNumber
>>- Long dependantStandBy
>>- Set&LT;Long/> attachedDoc
>>- List&LT;Long/> specialities
>>- String systemStatus
>- if used: 

## Add profile to a doctor
>- **Mapping:** POST (role DOCTOR)
>- **URL:** /api/i/doctors/{userId}
>> Long userId
>- **Request:** DoctorProfileDTO.Update
>>- String fullName
>>- String dateOfBirth
>>- String gender
>>- String maritalStatus
>>- String officeAddress
>>- String city
>>- String state
>>- String mdcnCertificateNumber
>>- List&LT;Long> specialities
>- **Response:** DoctorProfileDTO.Response or String error message
>>- Long userId
>>- String mobile
>>- String email
>>- Long doctorId
>>- String systemStatus
>>- Boolean approved
>>-  String fullName
>>- String dateOfBirth
>>- String gender
>>- String maritalStatus
>>- String officeAddress
>>- String city
>>- String state
>>- String mdcnCertificateNumber
>>- Long dependantStandBy
>>- Set&LT;Long/> attachedDoc
>>- List&LT;Long/> specialities
>>- String systemStatus
>- if used: 

## Update the email for a doctor
>- **Mapping:** POST (role DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/doctors/{userId}/update/email
>> Long userId
>- **Request:** EmailDTO
>>- String email
>- **Response:** String message updated or not
>- if used: 

## Update mobilenumber for a doctor
>- **Mapping:** POST (role DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/doctors/{userId}/update/mobile
>> Long userId
>- **Request:** MobileDTO
>>- String mobile
>- **Response:** String message updated or not
>- if used: 

## Get all booked consultations
>- **Mapping:** GET (role DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/consultations/booked
>- **Request:** 
>- **Response:** List&LT;ConsultationDTO>
>>- Long id
>>- String patient
>>- Long patientId
>>- String doctor
>>- String illness
>>- String date
>>- String timeBooked
>>- String timeAccepted
>>- String timeStarted
>>- String status
>>- List&LT;String> symptoms
>>- String detailedDescription
>>- String transactionReference
>>- Integer timeSlot
>>- String language
>>- String timeFinished
>- if used: 

## Doctor accepts a consultation
>- **Mapping:** GET (role DOCTOR)
>- **URL:** /api/i/consultations/{consultationId}/accept/{doctor}
>> String doctor
>- **Request:** 
>- **Response:** String message accepted or not
>- if used: 

## Doctor unaccept a consultation
>- **Mapping:** POST (role DOCTOR)
>- **URL:** /api/i/consultations/{consultationId}/unaccept
>> Long consultationId
>- **Request:** 
>- **Response:** String message unaccepted or not
>- if used: 

## Start a consultation
>- **Mapping:** GET (role DOCTOR)
>- **URL:** /api/i/consultations/{consultationId}/start
>> Long consultationId
>- **Request:** 
>- **Response:** String message started or not
>- if used: 

## Finish a consultation, Create a doneConsultation
>- **Mapping:** POST (role DOCTOR)
>- **URL:** /api/i/consultations/{consultationId}/finish
>> Long consultationId
>- **Request:** DoneConsultationWithJournalDTO
>>- String patient
>>- Long patientId
>>- String doctor
>>- String doctorId
>>- String illness
>>- String language
>>- String patientDescription
>>- String headIn
>>- String summary
>>- Long consultationDurationInMinute
>>- PatientJournal patientJournal
>>>- String patientName
>>>- String illnessSummary
>>>- String doctorName
>>>- String doctorsRemark
>>>- ~~Long id~~
>>>- ~~Long patientId~~
>>>- ~~String date~~
>>>- ~~Boolean hasBeenRead~~
>>- ~~Long id~~
>>- ~~String date~~
>>- ~~Boolean hasBeenRead~~
>- **Response:** String message finished or not
>- if used: 

## View done consultation by doneconsultationId
>- **Mapping:** GET (role DOCTOR)
>- **URL:** /api/i/consultations/viewdoneconsultation/{doneconsultationId}
>> Long doneconsultationId
>- **Request:** 
>- **Response:** DoneConsultationWithJournalDTO or String error message
>>- Long id
>>- String patient
>>- Long patientId
>>- String doctor
>>- String doctorId
>>- String illness
>>- String language
>>- String patientDescription
>>- String headIn
>>- String date
>>- String summary
>>- Long consultationDurationInMinute
>>- PatientJournal patientJournal
>>>- Long id
>>>- String patientName
>>>- Long patientId
>>>- String illnessSummary
>>>- String date
>>>- String doctorName
>>>- String doctorsRemark
>>>- Boolean hasBeenRead
>>- Boolean hasBeenRead
>- if used: 

## Doctor gets all accepted consultations by the doctor
>- **Mapping:** GET (role DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/consultations/{doctor}/accepted
>> Sring doctor
>- **Request:** 
>- **Response:** List&LT;ConsultationDTO>
>>- Long id
>>- String patient
>>- Long patientId
>>- String doctor
>>- String illness
>>- String date
>>- String timeBooked
>>- String timeAccepted
>>- String timeStarted
>>- String status
>>- List&LT;String> symptoms
>>- String detailedDescription
>>- String transactionReference
>>- Integer timeSlot
>>- String language
>>- String timeFinished
>- if used: 

## Doctor request a lab test
>- **Mapping:** POST (role DOCTOR)
>- **URL:** /api/i/consultations/{consultationId}/labrequest
>> Long consultationId
>- **Request:** LabRequestDTO
>>- String patientName
>>- Long patientId
>>- ELabRequest testRequested
>>- String date
>>- String doctorName
>>- String testReason
>>- ~~Long id~~
>>- ~~byte[] qrCode~~
>- **Response:** String message created or not
>- if used: 

## Create a follow up consultation
>- **Mapping:**  GET (role DOCTOR)
>- **URL:** /api/i/followupconsultation/{consultationId}/createfollowup
>> Long consultationId
>- **Request:** 
>- **Response:** String message
>- if used: 

## Get all follow up consultations
>- **Mapping:** GET (role DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/followupconsultation/getallfollowups
>- **Request:** 
>- **Response:** List&LT;FollowUpConsultation>
>>- Long id
>>- Long patientId
>>- LocalDate dateCreated
>- if used: 

## Get all follow-ups for a specific patient
>- **Mapping:** GET (role DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/followupconsultation/{patientId}/getfollowup
>> Long patientId
>- **Request:** 
>- **Response:** List&LT;FollowUpConsultation>
>>- Long id
>>- Long patientId
>>- LocalDate dateCreated
>- if used: 

## Get all illnesses that are registered
>- **Mapping:** GET (role PATIENT, DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/illnesses
>- **Request:** 
>- **Response:** List&LT;IllnessDTO>
>>- Long id
>>- String illness
>>- List&LT;String> symptoms
>- if used: 

## Get a specific illness
>- **Mapping:** GET (role PATIENT, DOCTOR or SYSTEMADMIN)
>- **URL:** /api/i/illnesses/{illness}
>> String illness
>- **Request:** 
>- **Response:** IllnessDTO or String error message
>>- Long id
>>- String illness
>>- List&LT;String> symptoms
>- if used: 

## Doctor post a prescription form
>- **Mapping:** POST (role DOCTOR)
>- **URL:** /api/i/prescriptions
>- **Request:** PrescriptionFormDTO
>>- String date
>>- String patientMobileNumber
>>- String illness
>>- Long patientId
>>- String patientName
>>- String patientDateOfBirth
>>- String patientAddress
>>- String medicationName
>>- String medicationForm
>>- String medicationStrength
>>- String medicationDose
>>- String medicationRoute
>>- String medicationFrequency
>>- String medicationRefills
>>- String medicationQuantity
>>- String doctorName
>>- String doctorMobileNumber
>- **Response:** PrescriptionDTO or String error message
>>- Long id
>>- String date
>>- String patientMobileNumber
>>- String illness
>>- Long patientId
>>- String patientName
>>- String patientDateOfBirth
>>- String patientAddress
>>- String medicationName
>>- String medicationForm
>>- String medicationStrength
>>- String medicationDose
>>- String medicationRoute
>>- String medicationFrequency
>>- String medicationRefills
>>- String medicationQuantity
>>- String doctorName
>>- String doctorMobileNumber
>>- String pharmacistRemark
>- if used: 

## Add a referral user to the currently logged-in user
>- **Mapping:** PUT (role PATIENT, DOCTOR or PHARMACIST)
>- **URL:** /api/i/referral/addreferral/{mobile}
>> String mobile
>- **Request:** 
>- **Response:** String message added or not
>- if used: 

## Gets the current referral user of the currently logged-in user
>- **Mapping:** GET (role PATIENT, DOCTOR or PHARMACIST)
>- **URL:** /api/i/referral/getreferraluser
>- **Request:** 
>- **Response:** String message referral users id
>- if used: 

## Adds the currently logged-in user to their referral users list of referred users
>- **Mapping:** PUT (role PATIENT, DOCTOR or PHARMACIST)
>- **URL:** /api/i/referral/addreferreduser
>- **Request:** 
>- **Response:** String message added or not
>- if used: 

## Gets all the users a certain user has referred
>- **Mapping:** GET (role PATIENT, DOCTOR or PHARMACIST)
>- **URL:** /api/i/referral/getreferredusers/{id}
>> Long id
>- **Request:** 
>- **Response:** List&LT;Long> referredUserList
>- if used: 
