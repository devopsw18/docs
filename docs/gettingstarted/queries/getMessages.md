# getMessages

> const getMessages = async (userId) => {
  const loggedInUser = Auth.getAuthicatedUser()
  return await apiCall(Routes.messages.getMessages(userId), 'GET', {}, loggedInUser.options)
}

The getMessages query will get user's messages list by the user id.
