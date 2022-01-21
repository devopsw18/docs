# Hospital UI Api

Note:

| **Mapping** | URL | **Purpose** | **RequestDTO** | **ResponseDTO** | if used  |
| --- | --- | --- | --- | --- | --- |
| Put(role HOSPITALADMIN)                  | /api/i/hospital/id                                | update hospital profile                   | Long id,HospitalProfileDTO                       | hospital profile dto or hospital couldn't be found                |  |
| Post(role HOSPITALADMIN)                 | /api/i/hospital/id/addhospitalstaff               | add hospitalstaff                         | Long id,HospitalStaffSignUpDTO                   | hospital staff dto                                                |  |
| Put(role HOSPITALADMIN)                  | /api/i/hospitalstaff/updatehospitalstaff          | To update hospitalstaff                   | HospitalStaffProfileDTO hospitalStaffProfileDTO  | hospital staff dto or hospital staff couldn't be found            |  |
| Delete(role HOSPITALADMIN)               | /api/i/hospitalstaff/hospitalStaffId              | To delete hospitalstaff                   | Long hospitalStaffId                             | successfully deleted or hospital staff doesn't exist              |  |
| Put(role HOSPITALADMIN or HOSPITALUSER)  | /api/i/hospitalstaff/updatepassword               | To update new password for hospitalstaff  | ResetPasswordDTO resetPasswordDTO                | password has been reset or email is not associated with any user  |  |
| Get(role HOSPITALADMIN)                  | /api/i/hospitalstaff/searchhospitalstaff/id       | get hospitalstaff DTO                     | Long hospitalstaffId                             | hospital staff dto or hospital staff doesn't exist                |  |
| Get(role HOSPITALADMIN)                  | /api/i/hospitalstaff/allhospitalstaff/hospitalId  | get list of hospitalstaff                 | Long hospitalId                                  | list of hospital staff dtos or hospital doesn't exist             |  |