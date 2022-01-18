# DoctorBlog Api

| **Mapping** | URL | **Purpose** | **Request** | **Response**| if used |
| --- | --- | --- | --- | --- | --- |
| POST (role DOCTOR)                         | /api/i/blog/createblog              | Doctor creating a blog               | DoctorBlogDTO(Long doctorId, String title, String text, String image, String linkToVideo)  |                   |          |
| GET (role DOCTOR, PATIENT or SYSTEMADMIN)  | /api/i/blog/getallblogs             | Get all blogs                        |                                                                                            |                   |          |
| GET (role DOCTOR, PATIENT or SYSTEMADMIN)  | /api/i/blog/getallblogs/{doctorid}  | Get all blogs for a specific doctor  |                                                                                            | Long doctorId     |          |
| GET (role DOCTOR, PATIENT or SYSTEMADMIN)  | /api/i/blog/getblog/{blogid}        | Get a specific blog                  |                                                                                            | Long blogId       |          |