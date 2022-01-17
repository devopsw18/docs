# Pharmacy UI Api

| **Mapping** | URL | **Purpose** | **RequestDTO** | **ResponseDTO** |  if used  |
| --- | --- | --- | --- | --- | --- |
| Put(role PHARMACYADMIN) |  /api/i/pharmacy/id | update pharmacy profile | Long id, PharmacyProfileDTO | pharmacy id, user email, user mobile, user id |  |
| Post(role PHARMACYADMIN) | /api/i/pharmacy/id/addpharmacist | add pharmacist | Long id,PharmacistSignUpDTO | pharmacist title, pharmacist fullname,user email, user mobile, pharmacist user id, pharmacy id  |  |
| Put(role PHARMACYADMIN or PHARMACYUSER)  | /api/i/pharmacy/resetpassword | To update new password for pharmacist | ResetPasswordDTO resetPasswordDTO | password has been reset or email is not associated with any user. |  |
| Get(role PHARMACYADMIN) | /api/i/pharmacist/pharmacistId  get pharmacist DTO | Long pharmacistId | returns pharmacist dto (id, title, full name, user email,user mobile, user Id, pharmacy Id |  |
| Put(role PHARMACYADMIN) | /api/i/pharmacist/updatepharmacist | To update pharmacist | Pharmacist update DTO pharmacistUpdateDTO  | returns pharmacist dto or user or pharmacist doesn't exist |  |
| Get(role PHARMACYADMIN) | /api/i/pharmacist/pharmacyId/allpharmacists | get list of phramacists | Long pharmacyId                            | returns pharmacists dto or pharmacy couldn't be found |  |
| Delete(role PHARMACYADMIN) | /api/i/pharmacist/pharmacistId | To delete pharmacist | Long pharmacistId | successfully deleted or user  or phramacy or pharmacist doesn't exist |  |