# getJournal

> const getJournal = async (userTypeId) => {
  const loggedInUser = Auth.getAuthicatedUser()
  return await apiCall(Routes.getJournal(userTypeId), 'GET', {}, loggedInUser.options)
}

The getJournal query will get the patient's journal list by the patient id.
