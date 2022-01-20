---
sidebar_position: 10
sidebar_label: Consultation
---
# Carelyo Consulation Services

## Consulation


## Consultation Request
This request is sent when payment is successful.

> - Patient Details
> - Symptoms Summary
> - Preferred language
> - Booked Duration (Timeslot)

## Consultation Broadcast
This are consultation requests that are sent to all doctors in the network

Condition that govern the operation of the consultation broadcast includes:

> - All doctor can see/view the request.
> - Only one doctor can accept.
> - Request is removed from broadcast once accepted.
> - Accepted request's time-to-live is set to 60s once accepted.
> - Start consultation is set to duration when patient joins the session.
> - Timmer count down is visible to doctor only.
> - Consultation can be extended.
> - Ended consutation.

## Done Consultation
> - Shows complete consultation request by doctor.
> - Details cannot be view.
> - Used to determin credit to doctors.

## Onging Consultation
> - Opens doctors access to patient data for duration of consultation.
> - 5 minutes is added for documentation or closed when doctor picks another request.
> - Has consultation request in view.
> - Has journal taking
> - Can add services:
> - - Hospital visit
> - - Prescription
> - - Digital follow up
> - - Add Lab test request
> - - View lab test result