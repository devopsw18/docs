# News Api

| **Mapping** | URL                                          | **Purpose**           | **Request** | **Response** | if used |
|-------------|----------------------------------------------|-----------------------|-------------|--------------|-----|
| POST        | /api/i/news/create                           | Create new news       | form-data(String dto(title, content, timeStamp, writtenBy, category), MultipartFile image)            | String       |     |
| PUT         | /api/i/news/update                           | Update news           |  form-data(String dto(title, content, timeStamp, writtenBy, category), MultipartFile image)           | String       |     |
| DELETE      | /api/i/news/delete/{id}                      | Delete news by {id}   |             | String       |     |
| GET         | /api/i/news/getAll                           | Get all news          |             | List<NewsArticleDTO\>       |     |
| GET         | /api/i/news/getById/{id}                     | Get one news by {id}  |             | NewsArticleDTO(id, title, content, timeStamp, writtenBy, category, (byte[]) image,nrOfViews)       |     |
| PUT         | /api/i/news/<br/>incrementNumberOfViews/{id} | Count number of views |             | String       |     |
