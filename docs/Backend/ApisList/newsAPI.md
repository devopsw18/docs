# News Api

Note:

---
##	Create new news
>- **Mapping:** POST (Role SYSTEMADMIN)
>- **URL:** 	/api/i/news/create
>- **Request:** form-data(String newsDTO + MultipartFile image)
>> newsDTO
>>- String title
>>- String content
>>- String timeStamp
>>- String writtenBy
>>- String category
>- **Response:** String message created or not
>- if used: 

## Update a specific news
>- **Mapping:** PUT(Role SYSTEMADMIN)
>- **URL:** /api/i/news/update/{newsId}
>> Long newsId
>- **Request:** form-data(String newsDTO + MultipartFile image)
>> newsDTO
>>- String title
>>- String content
>>- String timeStamp
>>- String writtenBy
>>- String category
>- **Response:** String message updated or not
>- if used: 

## Delete a specific news
>- **Mapping:** DELETE (Role SYSTEMADMIN)
>- **URL:** /api/i/news/delete/{newsId}
>> Long newsId
>- **Request:** 
>- **Response:** String message deleted or not
>- if used: 

## Get all news
>- **Mapping:** GET
>- **URL:** /api/i/news/getAll
>- **Request:** 
>- **Response:** List&LT;NewsArticleDTO>
>>- Long id
>>- String title
>>- String content
>>- String timeStamp
>>- String writtenBy
>>- String category
>>- byte[] image
>>- int nrOfViews
>- if used: 

## Get a specific news
>- **Mapping:** GET
>- **URL:** /api/i/news/getById/{newsId}
>> Long newsId
>- **Request:** 
>- **Response:** NewsArticleDTO or String error message
>>- Long id
>>- String title
>>- String content
>>- String timeStamp
>>- String writtenBy
>>- String category
>>- byte[] image
>>- int nrOfViews
>- if used: 

## Increase number of views by 1
>- **Mapping:** PUT
>- **URL:** /api/i/news/
incrementNumberOfViews/{newsId}
>> Long newsId
>- **Request:** 
>- **Response:** String message increased or not
>- if used: 