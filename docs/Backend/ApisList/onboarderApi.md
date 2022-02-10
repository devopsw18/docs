# OnBoarder API
## Get users by roleId
>- **Mapping:** GET
>- **URL:** /api/i/onboarder/getusersbyrole/{roleId}
>>- Long roleId
>- **Request:** 
>- **Respnse:** List&LT;UserDTO.Response>
>>- Long id
>>- String email
>>- String mobile
>>- List&LT;String> roles 
>- if used: Using a roleId that does not correspond to a role in the database will return all users with no roles.
---
## Update user roles
>- **Mapping:** PUT
>- **URL** /api/i/onboarder/{userId}/updateRoles
>>- Long userId
>- **Request:** List&LT;Long> roles
>- **Response:** String
>- if used: On boarder can only access roles SYSTEMADMIN and SUPPORT
---
## Get roles
>- **Mapping:** GET
>- **URL:** /api/i/onboarder/getroles
>- **Request:** 
>- **Respnse:** List&LT;Role>
>>- Long id
>>- String name
>- if used:
---