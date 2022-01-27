# Patient UI Api

Note: Unless specified otherwise, all APIs require a patient token (the system admin APIs will be moved into their own document later)

---
## Add referral a user to the currently logged in user
>- **Mapping:** PUT (role PATIENT, DOCTOR, PHARMACYUSER, HOSPITALUSER or LABSCIENTIST)
>- **URL:** /api/i/referral/addreferral/{mobile}
>> String mobile
>- **Request:** 
>- **Response:** String message added or not
>- if used: 

## Get referral user ID as a String
>- **Mapping:** GET (role PATIENT, DOCTOR, PHARMACYUSER, HOSPITALUSER or LABSCIENTIST)
>- **URL:** /api/i/referral/getreferraluser
>- **Request:** 
>- **Response:** String referral user ID or error message
>- if used: 

## Adds the currently logged in user to the referred users list of their referral user
>- **Mapping:** PUT (role PATIENT, DOCTOR, PHARMACYUSER, HOSPITALUSER or LABSCIENTIST)
>- **URL:** /api/i/referral/addreferreduser
>- **Request:** 
>- **Response:** String message added or not
>- if used: 

## Get referred users list of a specific user
>- **Mapping:** GET (role PATIENT, DOCTOR, PHARMACYUSER, HOSPITALUSER or LABSCIENTIST)
>- **URL:** /api/i/referral/getreferredusers/{id}
>> Long id
>- **Request:** 
>- **Response:** List&LT;Long> referredUserList
>- if used: 

## Get all patients
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/i/patients
>- **Request:** 
>- **Response:** List&LT;PatientDTO>
>>- Long userId
>>- String email
>>- String mobile
>>- Long patientId
>- if used: 

## Get all patients profile
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/i/patients/viewallpatients
>- **Request:** 
>- **Response:** List&LT;PatientProfileResponseDTO>
>>- Long userId
>>- String email
>>- String mobileNumber
>>- Boolean profileComplete
>>- Long patientId
>>- String title
>>- String nationalIdNumber
>>- String firstName
>>- String surName
>>- String dateOfBirth
>>- String gender
>>- String maritalStatus
>>- String heightFeet_cm
>>- String heightInches_cm
>>- String weight
>>- String bloodType
>>- String allergies
>>- String medicalProblems
>>- String disabilities
>>- String language
>>- String country
>>- String state
>>- String community
>>- String address
>>- String postCode
>>- String purposeOfVisit
>>- String closestHospital
>>- Boolean hasChildren
>>- Boolean hasDependent
>- if used: 

## get a specific patient
>- **Mapping:** GET (role PATIENT or SYSTEMADMIN)
>- **URL:** /api/i/patients/{patientId}
>> Long patientId
>- **Request:** 
>- **Response:** PatientDTO or String error message
>>- Long userId
>>- String email
>>- String mobile
>>- Long patientId
>- if used: 

## get a specific patient profile
>- **Mapping:** GET (role PATIENT or SYSTEMADMIN)
>- **URL:** /api/i/patients/patientinfo/{patientId}
>> Long patientId
>- **Request:** 
>- **Response:** PatientProfileResponseDTO or String error message
>>- Long userId
>>- String email
>>- String mobileNumber
>>- Boolean profileComplete
>>- Long patientId
>>- String title
>>- String nationalIdNumber
>>- String firstName
>>- String surName
>>- String dateOfBirth
>>- String gender
>>- String maritalStatus
>>- String heightFeet_cm
>>- String heightInches_cm
>>- String weight
>>- String bloodType
>>- String allergies
>>- String medicalProblems
>>- String disabilities
>>- String language
>>- String country
>>- String state
>>- String community
>>- String address
>>- String postCode
>>- String purposeOfVisit
>>- String closestHospital
>>- Boolean hasChildren
>>- Boolean hasDependent
>- if used: 

## Complete profile of patient
>- **Mapping:** PUT (role PATIENT, SUPPORT or SYSTEMADMIN)
>- **URL:** /api/i/patients
>- **Request:** PatientProfileRequestDTO
>>- Long userId
>>- Long patientId
>>- String title
>>- String nationalIdNumber
>>- String firstName
>>- String surName
>>- String dateOfBirth
>>- String gender
>>- String maritalStatus
>>- String heightFeet_cm
>>- String heightInches_cm
>>- String weight
>>- String bloodType
>>- String allergies
>>- String medicalProblems
>>- String disabilities
>>- String language
>>- String country
>>- String state
>>- String community
>>- String address
>>- String postCode
>>- String purposeOfVisit
>>- Integer noOfChild
>>- List&LT;Child> children
>>>- Long childId
>>>- String firstName
>>>- String surName
>>>- String dateOfBirth
>>>- String gender
>>>- Long patientId
>>>- String weight
>>>- String bloodType
>>>- String allergies
>>>- String disabilities
>>- String closestHospital
>>- Integer noOfDependent
>>- List&LT;NeedyPerson> dependents
>>>- Long NeedyPersonId
>>>- Long patientId
>>>- String title
>>>- String nationalIdNr
>>>- String firstName
>>>- String surName
>>>- String dateOfBirth
>>>- String gender
>>>- String caregiver
>>>- String email
>>>- String mobile
>>>- String language
>>>- String address
>>>- String postcode
>>>- String state
>>>- String country
>- **Response:** PatientProfileResponseDTO
>>- Long userId
>>- String email
>>- String mobileNumber
>>- Boolean profileComplete
>>- Long patientId
>>- String title
>>- String nationalIdNumber
>>- String firstName
>>- String surName
>>- String dateOfBirth
>>- String gender
>>- String maritalStatus
>>- String heightFeet_cm
>>- String heightInches_cm
>>- String weight
>>- String bloodType
>>- String allergies
>>- String medicalProblems
>>- String disabilities
>>- String language
>>- String country
>>- String state
>>- String community
>>- String address
>>- String postCode
>>- String purposeOfVisit
>>- String closestHospital
>>- Boolean hasChildren
>>- Boolean hasDependent
>- if used: 

## Create a consultation for a patient
>- **Mapping:** POST (role PATIENT)
>- **URL:** /api/i/consultations/book
>- **Request:** BookConsultationDTO
>>- String patient
>>- Long patientId
>>- String illness
>>- List&LT;String> symptoms
>>- String detailedDescription
>>- String transactionReference
>>- String language
>>- Integer amountPaid
>>- ~~String date~~
>- **Response:** BookConsultationDTO
>>- String patient
>>- Long patientId
>>- String illness
>>- List&LT;String> symptoms
>>- String detailedDescription
>>- String transactionReference
>>- String language
>>- Integer amountPaid
>>- String date
>- if used: 

## Add Child to a specific patient
>- **Mapping:** POST (role PATIENT)
>- **URL:** /api/i/children/{patientId}/createchild
>> Long patientId
>- **Request:** ChildRequestDTO
>>- Long childId
>>- String firstName
>>- String surName
>>- String dateOfBirth
>>- String gender
>>- String weight
>>- String bloodType
>>- String allergies
>>- String disabilities
>>- ~~Long patientId~~
>- **Response:** String message Added or not
>- if used: 

## Get all Children
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/i/children/getallchildren
>- **Request:** 
>- **Response:** List&LT;ChildResponseDTO>
>>- Long patientId
>>- Long childId
>>- String firstName
>>- String surName
>>- String dateOfBirth
>>- String gender
>>- String weight
>>- String bloodType
>>- String allergies
>>- String disabilities
>- if used: 

## Get all Children of a specific patient
>- **Mapping:** GET (role PATIENT or SYSTEMADMIN)
>- **URL:** /api/i/children/{Patientid}
>> Long Patientid
>- **Request:** 
>- **Response:** List&LT;ChildResponseDTO>
>>- Long patientId
>>- Long childId
>>- String firstName
>>- String surName
>>- String dateOfBirth
>>- String gender
>>- String weight
>>- String bloodType
>>- String allergies
>>- String disabilities
>- if used: 

## Update child profile
>- **Mapping:** PUT (role PATIENT or SYSTEMADMIN)
>- **URL:** /api/i/children/{childid}
>> Long childid
>- **Request:** ChildRequestDTO
>>- String firstName
>>- String surName
>>- String dateOfBirth
>>- String gender
>>- String weight
>>- String bloodType
>>- String allergies
>>- String disabilities
>>- ~~Long childId~~
>>- ~~Long patientId~~
>- **Response:** 
>- if used: 


## Create dependent(needy person) for a specific patient
>- **Mapping:** POST (role PATIENT)
>- **URL:** /api/i/needyperson/{patientId}/createneedyperson
>> Long patientId
>- **Request:** NeedyPersonDTO
>>- String title
>>- String nationalIdNr
>>- String firstName
>>- String surName
>>- String dateOfBirth
>>- String gender
>>- String caregiver
>>- String email
>>- String mobile
>>- String language
>>- String address
>>- String postcode
>>- String state
>>- String country
>>- ~~Long NeedyPersonId~~
>>- ~~Long patientId~~
>- **Response:** String message created or not
>- if used: 

## Get all dependents(needy persons)
>- **Mapping:** GET (role SYSTEMADMIN)
>- **URL:** /api/i/needyperson/getallneedypersons
>- **Request:** 
>- **Response:** List&LT;NeedyPerson>
>>- Long NeedyPersonId
>>- Long patientId
>>- String title
>>- String nationalIdNr
>>- String firstName
>>- String surName
>>- String dateOfBirth
>>- String gender
>>- String caregiver
>>- String email
>>- String mobile
>>- String language
>>- String address
>>- String postcode
>>- String state
>>- String country
>- if used: 

## Get all dependents(needy persons) of a specific patient
>- **Mapping:** GET (role PATIENT or SYSTEMADMIN)
>- **URL:** /api/i/needyperson/{Patientid}
>> Long Patientid
>- **Request:** 
>- **Response:** List&LT;NeedyPerson>
>>- Long NeedyPersonId
>>- Long patientId
>>- String title
>>- String nationalIdNr
>>- String firstName
>>- String surName
>>- String dateOfBirth
>>- String gender
>>- String caregiver
>>- String email
>>- String mobile
>>- String language
>>- String address
>>- String postcode
>>- String state
>>- String country
>- if used: 

## Update a specific dependent(needy persons)
>- **Mapping:** PUT (role PATIENT or SYSTEMADMIN)
>- **URL:** /api/i/needyperson/{needypersonid}
>> Long needypersonid
>- **Request:** NeedyPersonDTO
>>- String title
>>- String nationalIdNr
>>- String firstName
>>- String surName
>>- String dateOfBirth
>>- String gender
>>- String caregiver
>>- String email
>>- String mobile
>>- String language
>>- String address
>>- String postcode
>>- String state
>>- String country
>>- ~~Long NeedyPersonId~~
>>- ~~Long patientId~~
>- **Response:** String message updated or not
>- if used: 

## Gets all prescriptions
>- **Mapping:** GET (role PATIENT)
>- **URL:** /api/i/prescriptions/{patientId}/prescriptionsbydate
>> Long patientId
>- **Request:** 
>- **Response:** List&LT;PrescriptionDTO>
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

## Gets all unfilled prescriptions
>- **Mapping:** GET (role PATIENT)
>- **URL:** /api/i/prescriptions/{patientId}/unfilled_prescriptions
>> Long patientId
>- **Request:** 
>- **Response:** List&LT;PrescriptionDTO>
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

## Gets all done consultations of a specific patient
>- **Mapping:** GET (role PATIENT or SYSTEMADMIN)
>- **URL:** /api/i/consultations/viewalldoneconsultations/{patientId}
>> Long patientId
>- **Request:** 
>- **Response:** List&LT;DoneConsultationWithJournalDTO>
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

## Get all journals of a specific patient
>- **Mapping:** GET (role PATIENT)
>- **URL:** /api/i/consultations/viewalljournals/{patientId}
>> Long patientId
>- **Request:** 
>- **Response:** List&LT;PatientJournal>
>>- Long id
>>- String patientName
>>- Long patientId
>>- String illnessSummary
>>- String date
>>- String doctorName
>>- String doctorsRemark
>>- Boolean hasBeenRead
>- if used: 

## Sets a DoneConsultation as Read
>- **Mapping:** PUT (role PATIENT)
>- **URL:** /api/i/consultations/setconsultationasread/{doneConsultationId}
>> Long doneConsultationId
>- **Request:** 
>- **Response:** String message setted or not
>- if used: 

## Sets a Patientjournal as Read
>- **Mapping:** PUT (role PATIENT)
>- **URL:** /api/i/consultations/setjournalasread/{journalId}
>> Long journalId
>- **Request:** 
>- **Response:** String message setted or not
>- if used: 


## Get all lab requests for a specific patient
>- **Mapping:** GET (role PATIENT or SYSTEMADMIN)
>- **URL:** /api/i/laboratory/getalllabrequest/{patientid}
>- **Request:** 
>- **Response:** List&LT;LabResultDTO>
>>- Long id
>>- String resultName
>>- long labRequestId
>>- long patientId
>>- Boolean finished
>>- String date
>>- String testName
>>- String laboratory
>>- String result
>- if used: 
