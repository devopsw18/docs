# getHospitalAppointments

> const getHospitalAppointments = async (patientId) => {
  const loggedInUser = Auth.getAuthicatedUser()
  return await apiCall(Routes.getHospitalAppointments(patientId), 'GET', {}, loggedInUser.options)
}  

The getHospitalAppointments query will get the patient's hospital appointments by the patient id.
