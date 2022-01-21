# Feedback Api

Note:

| **Mapping** | URL | **Purpose** | **Request** | **Response**| if used |
| --- | --- | --- | --- | --- | --- |
| POST (role PATIENT, DOCTOR, PHARMACY, PHARMACYADMIN)  | /api/i/feedback/{userId}/createfeedback  | Create feedback messages by patient, doctor, pharmacy, pharmacyAdmin                                    |                 |                  |          |
| GET (role PATIENT or SUPPORT)                         | /api/i/support/getallmessages            | Support can view all feedback messages [obs: change the role to SUPPORT in API]                         |                 |                  |          |
| GET (role PATIENT or SUPPORT)                         | /api/i/support/{userId}                  | Support can view all feedback messages for a specific patient [obs: change the role to SUPPORT in API]  |                 |                  |          |