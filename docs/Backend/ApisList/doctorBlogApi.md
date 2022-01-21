# DoctorBlog Api

Note:

## Doctor creating a blog
>- **Mapping:**  POST (role DOCTOR)
>- **URL:**  /api/i/blog/createblog
>- **Request:** DoctorBlogDTO
>>- Long doctorId
>>- String title
>>- String text
>>- String image
>>- String linkToVideo
>- **Response:** Srting (Shows a message if blog was created!)
>- if used: 

## Get all blogs
>- **Mapping:**  GET (role DOCTOR, PATIENT or SYSTEMADMIN)
>- **URL:**  /api/i/blog/getallblogs
>- **Request:** 
>- **Response:** List&LT;DoctorBlog>
>>- Long doctorId
>>- String title
>>- String text
>>- String image
>>- String linkToVideo
>- if used: 

## Get all blogs for a specific doctor
>- **Mapping:**  GET (role DOCTOR, PATIENT or SYSTEMADMIN)
>- **URL:**  /api/i/blog/getallblogs/{doctorid}
>- **Request:** 
>- **Response:** List&LT;DoctorBlog>
>>- Long doctorId
>>- String title
>>- String text
>>- String image
>>- String linkToVideo
>- if used: 

## Get a specific blog
>- **Mapping:**  GET (role DOCTOR, PATIENT or SYSTEMADMIN)
>- **URL:**  /api/i/blog/getblog/
>- **Request:** 
>- **Response:** DoctorBlogDTO
>>- Long doctorId
>>- String title
>>- String text
>>- String image
>>- String linkToVideo
>- if used: 
