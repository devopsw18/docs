# getLabResults

> const getLabResults = async (patientId) => {
  const loggedInUser = Auth.getAuthicatedUser()
  return await apiCall(Routes.getLabResults(patientId), 'GET', {}, loggedInUser.options)
}  

The getLabResults query will get the patient's lab results by the patient id.
