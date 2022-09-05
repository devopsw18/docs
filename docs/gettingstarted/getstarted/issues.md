---
sidebar_position: 2
sidebar_label: Issues
---
# Working with issues

When working with issues you have:

1. Main Task
2. Sub Task

## Main Task
This is a task that will have sub-tasks. For example [Fix doctor complete profile functionality](https://gitlab.com/carelyo/frontend-team/doctorui2.0/-/issues/83)

### How to create a Main Task
1. Click issues
2. List
3. New issues
4. Give it a name
5. Give a short description with bullet points max 3 points
6. Assignee i.e., Yourself
7. Due Date 
8. Milestion (MVP)
9. Label (Backlog)
10. Create issue

### Create a branch for the Main Task
In the project that you are working on i.e., [doctorui](https://gitlab.com/carelyo/frontend-team/doctorui2.0/-/branches) click New branch
Naming convention: branchname = issuenumber + taskname (#134 Make sure no content is outsid the completeProfile_card)


## Sub Task
This a task or tasks that are linked to a Main Task

### How to create a Sub Task
1. Find the Main Task and click it. You can find it by going to the Project => Issues => List => search the issue
2. Under Tasks click Add
3. Then give it a name and click create. See example (https://gitlab.com/carelyo/frontend-team/doctorui2.0/-/issues/83)
4. Create a new branch for a Sub Task: branchname = Main Task issuenumber + subtaskname 

## Merging Sub Task
Once you completed your sub task. Do the following:

1. Push it to the origin remote branch of the Sub Task branch
2. On GitLab create a merge request for your Sub Task to Main Task
3. Assigne it to the reviewer for your Team 
4. Merge it  
5. Remember to remind your reviwer close the Sub Task 

## Merging Main Task
When all subtasks are done them:

1. Push it the origin remote of the Main Tast branch 
2. On GitLab create a merge request from Main Task to the Develop
3. Assigne it to the reviewer for your Team
4. Merge it
5. Move your Main Task to Tesing


