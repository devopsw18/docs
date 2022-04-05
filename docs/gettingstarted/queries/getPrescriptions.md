# getPrescriptions

> const getPrescriptions = async (userTypeId) => {
  const loggedInUser = Auth.getAuthicatedUser()
  return await apiCall(Routes.getPrescriptions(userTypeId), 'GET', {}, loggedInUser.options)
}  

The getPrescriptions query will get the patient's prescription list by the patient id.
