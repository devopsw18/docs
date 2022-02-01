# getLabRequests

> const getLabRequests = async (patientId) => {
  const loggedInUser = Auth.getAuthicatedUser()
  return await apiCall(Routes.getLabRequests(patientId), 'GET', {}, loggedInUser.options)
}

The getLabRequests query will get the patient's lab requests by the patient id.
