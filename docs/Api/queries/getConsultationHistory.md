# getConsultationHistory

> const getConsultationHistory = async (userTypeId) => {
  const loggedInUser = Auth.getAuthicatedUser()
  return await apiCall(Routes.getConsultationHistory(userTypeId), 'GET', {}, loggedInUser.options)
}

The getConsultationHistory query will get the patient's done consultations by the patient id.
