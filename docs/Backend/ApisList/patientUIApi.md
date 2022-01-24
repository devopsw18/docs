# Patient UI Api

Note: Unless specified otherwise, all APIs require a patient token (the system admin APIs will be moved into their own document later)

---

## Referral

## PUT /api/i/referral/addreferral/{mobile}

Add referral a user to the currently logged in user.

**PathVariable** : (string) mobile

**ResponseBody**: success or failed (string)

**Authorization** : hasRole: PATIENT,DOCTOR,PHARMACYUSER,HOSPITALUSER,LABSCIENTIST

## GET /api/i/referral/getreferraluser

Get referral users ID as a String.

**ResponseBody**: user id (string)

**Authorization** :  hasRole: PATIENT,DOCTOR,PHARMACYUSER,HOSPITALUSER,LABSCIENTIST

## PUT /api/i/referral/getreferraluser

Adds the currently logged in user to the referred users list of their referral user.

**ResponseBody**:  success or failed (string)

**Authorization** :  hasRole: PATIENT,DOCTOR,PHARMACYUSER,HOSPITALUSER,LABSCIENTIST

## GET /api/i/referral/getreferredusers/{id}

gets the ids of all the referred users in the given users list

**PathVariable** : id

**ResponseBody**:  list of user ids (list of longs)

**Authorization** :  hasRole: PATIENT,DOCTOR,PHARMACYUSER,HOSPITALUSER,LABSCIENTIST

---

## Patients

## GET /api/i/patients

returns a list of all PatientDTOs

**ResponseBody**:  list of PatientDTOs (user id, email, mobile, patient id)

**Authorization** :  hasRole: SYSTEMADMIN

## GET /api/i/patients/viewallpatients

get a list of PatientProfileResponseDTO

**ResponseBody** : list of PatientProfileResponseDTOs (user id, email, mobileNumber, profileComplete patient id, title, national id number, first name, sur name, date of birth, gender, marital status, weight, blood type, allergies, disabilities, language, country, state, community, address, post code, purpose of visit, closestHospital, hasChildren, hasDependent)

**Authorization** : hasRole: SYSTEMADMIN

## GET /api/i/patients/{id}

 get a specific patientDTO

**PathVariable** : id

**ResponseBody** : PatientDTO (user id, email, mobile, patient id)

**Authorization** :  hasRole: SYSTEMADMIN,PATIENT(only entities assosiated with their userId)

## /api/i/patients/patientinfo/{id}

gets the PatientProfileResponseDTO

**PathVariable** : id

**ResponseBody** : PatientProfileResponseDTO(user id, email, mobileNumber, profileComplete, patient id, title, national id number, first name, sur name, date of birth, gender, marital status, weight, blood type, allergies, disabilities, language, country, state, community, address, post code, purpose of visit, closestHospital, hasChildren, hasDependent)

**Authorization** :  hasRole: SYSTEMADMIN,PATIENT(only entities assosiated with their userId)

## PUT /api/i/patients

to complete patient profile, returns a PatientProfileResponseDTO

**RequestBody** : PatientProfileRequestDTO(ser id, patient id, title, national id number, first name, sur name, date of birth, gender, marital status, weight, blood type, allergies, disabilities, language, country, state, community, address, post code, purpose of visit, noOfChild, children(list<Child\>),closestHospital,noOfDependent,dependents(List<Dependent\>))

**ResponseBody** : PatientProfileResponseDTO(user id, email, mobileNumber, profileComplete, patient id, title, national id number, first name, sur name, date of birth, gender, marital status, weight, blood type, allergies, disabilities, language, country, state, community, address, post code, purpose of visit, closestHospital, hasChildren, hasDependent)

**Authorization** : hasRole: SYSTEMADMIN,PATIENT(only entities assosiated with their userId), SUPPORT

---

## Consultations

## POST /api/i/consultations/book

books a consultation for a patient

**RequestBody** : BookConsultationDTO((string) patient name, (long) patient id, (string) illness, (list of strings) symptoms, (string) detailed description, (string) transaction reference, (string) language, (integer) amount paid)

**ResponseBody** : ConsultationDTO(consultation id, patient name, patiend id, doctor name, illness, date, time booked, time accepted, time started, status, symptoms, detailed description, transaction reference, timeSlot, language,timeFinished)

**Authorization** : hasRole: PATIENT

## GET /api/i/consultations/viewalldoneconsultations/{patientId}

Gets all done consultations (aka the consultation history) of a specific patient sorted by the date

**PathVariable** : patientId

**ResponseBody** : list of DoneConsultationWithJounralDTOs (id, patient, patient id, doctor, doctor id, illness, language, patient description, headIn, date, summary, consultation duration in minutes, patient journal (id, patient name, illness summary, date, doctor name, doctors remark))

**Authorization** : hasRole: SYSTEMADMIN,PATIENT

---

## Children

## POST /api/i/children/{patientId}/createchild

Create Child with patientsID and supply child info as JSON in body

**PathVariable** : patientId

**RequestBody** : ChildRequestDTO((long) childId, (string) first name, (string) sur name, (string) date of birth, (string) gender, (string) weight,  (string) blood type, (string) allergies, (string) disabilities )

**ResponseBody** : patientID x has y child/children or Child cannot be created. Patient is not present (string)

**Authorization** : hasRole: PATIENT

## GET /api/i/children/getallchildren

Get all child info from repository as JSON

**ResponseBody** : list of ChildResponseDTO (child id, first name, sur name, date of birth, gender, patient id, weight, blood type, allergies, disabilities)

**Authorization** : hasRole: SYSTEMADMIN

## GET /api/i/children/{Patientid}

Get all child info for a specific patient from repository as JSON| patientId

**PathVariable** : patientId

**ResponseBody** : ChildResponseDTO (child id, first name, sur name, date of birth, gender, patient id, weight, blood type, allergies, disabilities)

**Authorization** : hasRole: SYSTEMADMIN,PATIENT

## PUT /api/i/children/{childid}

Update child profile

**PathVariable** : childid

**RequestBody** : ChildRequestDTO((long) childId, (string) first name, (string) sur name, (string) date of birth, (string) gender, (string) weight,  (string) blood type, (string) allergies, (string) disabilities )

**Authorization** :  hasRole: SYSTEMADMIN,PATIENT

---

## Dependant/Needyperson

## POST /api/i/needyperson/{patientId}/createneedyperson

create needy person with patientId  and supply needy person info as JSON body

**PathVariable** : patientId

**RequestBody** : NeedyPersonDTO((string) title, (string) national Id number, (string) first name, (string) surname, (string) date of birth, (string) gender, (string) caregiver, (string) email, (string) mobile, (string) language, (string) address, (string) postcode,  (string) state, (string) country))

**ResponseBody** : String

**Authorization** :  hasRole: PATIENT

## GET /api/i/needyperson/getallneedypersons

get all needy persons info from repository as JSON

**ResponseBody** : list NeedyPerson(needy person id, patient id, title, national id number, first name, sur name, date of birth, gender, caregiver, email, mobile, language, address, post code, state, country)

**Authorization** :  hasRole: SYSTEMADMIN

## GET /api/i/needyperson/{Patientid}

 get all needy persons info from a specific patient from repository as JSON

**PathVariable** : PatientId

**ResponseBody** : list NeedyPerson(needy person id, patient id, title, national id number, first name, sur name, date of birth, gender, caregiver, email, mobile, language, address, post code, state, country)

**Authorization** :  hasRole: SYSTEMADMIN,PATIENT

## PUT /api/i/needyperson/{needypersonid}

update needy person profile

**PathVariable** : needypersonid

**ResponseBody** : NeedyPerson((string) title, (string) national Id number, (string) first name, (string) surname, (string) date of birth, (string) gender, (string) caregiver, (string) email, (string) mobile, (string) language, (string) address, (string) postcode,  (string) state, (string) country )

**Authorization** : hasRole: SYSTEMADMIN,PATIENT

---

## Prescriptions

## GET  /api/i/prescriptions/{id}/prescriptionsbydate

get all prescriptions with a specific patient id sorted by the date

**PathVariable** : id

**ResponseBody** : list of prescriptionDTOs (id, date, patient mobile number, illness, patient id, patient name, patient date of birth, patient address, medication name, medication form, medication strength, medication dose, medication route, medication frequency, medication refills, medication quantity, doctor name, doctor mobile number, pharmacist remark)

**Authorization** : hasRole: PATIENT

---

## Laboratory

## GET /api/i/laboratory/getalllabrequest/{patientid}

 Get all lab requests for a specific patient sorted by the date

**PathVariable** : patientid

**ResponseBody** : LabRequestDTOs (id, patient name, patient id, test requested, date, doctors name, test reason, qr code (as a byte array))

**Authorization** : hasRole: SYSTEMADMIN,PATIENT