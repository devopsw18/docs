# Reference Survey API

## Not logged in

## POST /api/referencesurvey/submit

Submits a reference survey

**RequestBody** : ReferenceSurveyDTO(id, responderEmail, responderName, doctorId, doctorFirstName, doctorSurname, questions(ist), answers(list), notes)

**ResponseBody** : String

---

## GET /api/referencesurvey/getsurvey

**RequestBody** :ReferenceSurveyVerificationDTO(email, responderName, doctorId)

**ResponseBody** : ReferenceSurveyDTO(id, responderEmail, responderName, doctorId, doctorFirstName, doctorSurname, questions(ist), answers(list), notes)

---

## Logged in

## POST /api/i/referencesurvey/sendReferenceRequest

**RequestBody** : SendReferenceRequestDTO(referenceEmail, referenceName, doctorFirstName, doctorSurname, doctorId)

**ResponseBody** : String

**Authorization** : hasRole:DOCTOR

---

## GET /api/i/referencesurvey/getSurveysByDoctorId/{doctorId}

**PathVariable** : doctorId

**ResponseBody** : List\<ReferenceSurvey\>

**Authorization** : hasRole:SYSTEMADMIN

---

## GET /api/i/referencesurvey/getSurveyById/{id}

**PathVariable** : id

**ResponseBody** : ReferenceSurvey(id, responderEmail, responderName, doctorId, doctorFirstName, doctorSurname, questions(ist), answers(list), notes)

**Authorization** : hasRole:SYSTEMADMIN

---

## GET /api/i/referencesurvey/getAllQuestions

**ResponseBody** : List\<SurveyQuestion\>

**Authorization** : hasRole:SYSTEMADMIN

---

## POST /api/i/referencesurvey/addQuestion

**RequestBody** : SurveyQuestionDTO(id, question)

**ResponseBody** : String

**Authorization** : hasRole:SYSTEMADMIN

---

## POST /api/i/referencesurvey/updateQuestion

**RequestBody** : SurveyQuestionDTO(id, question)

**ResponseBody** : String

**Authorization** : hasRole:SYSTEMADMIN

---

## DELETE /api/i/referencesurvey/deleteQuestionById/{id}

**PathVariable** : id

**ResponseBody** : String

**Authorization** : hasRole:SYSTEMADMIN

---
