# User Api

## PUT /api/i/user/updatePassword/{userId}

Changes a users password

**PathVariable** : userId

**RequestBody** : UpdatePasswordDTO(currentPassword,newPassword)

**ResponseBody** : String

**Authorization** : any role

---

## PUT /api/i/user/updateEmail/{userId}

Changes a users email

**PathVariable** : userId

**RequestBody** : UpdateEmailDTO(code,password,newEmail)

**ResponseBody** : String

**Authorization** : any role

---

## PUT /api/i/user/updatePhoneNumber/{userId}

Changes a users email

**PathVariable** : userId

**RequestBody** : UpdateEmailDTO(password,newPhoneNumber)

**ResponseBody** : String

**Authorization** : any role

---

## PUT /api/i/user/code/{userId}

Sends a code to a email address

**RequestBody** : UpdateEmailDTO(email)

**ResponseBody** : String

**Authorization** : any role