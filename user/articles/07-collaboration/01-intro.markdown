---
header-id: team-collaboration-access-control
---

# Team Collaboration & Access Control

With DXP Cloud's team collaboration features, you can better manage access to 
your environments. Each environment can have unique members, and each member can 
have a role that matches their job's access level in the environment. 

## Managing Team Members

You can manage teams from the *Team* tab in the left menu of your environment.

Follow these steps to invite a user to your team: 

1.  Search for the user's email in the *Email* field.

2.  Use the *Role* menu to select the role to assign to the user. These roles 
    set the user's access level in the environment. For more information, see 
    [Understanding Team Roles](#understanding-team-roles). 

3.  Click *Send Invite*. 

Current and invited team members appear in the *Members* table, in separate 
tabs. You can manage team members via the *Actions* button for each, which lets 
you change the team member's role and remove the member from the team. 

![Figure 1: The Team tab shows your team members.](../../images/invite-member.png)

![Figure 2: Use the Actions button to manage each team member.](../../images/manage-members.png)

## Team Activities

To see a list of activities performed by your team members, click your 
environment's *Activities* tab in the menu on the left. Each activity lists the 
team member who performed it and the date it occurred. This way, you always know 
who is doing what in your environment. 

![Figure 3: The Activities tab shows your team's activities.](../../images/team-activities.png)

## Understanding Team Roles

You can assign these roles to team members: 

**Admin:** Has full control over the environment and its members. Only Admins 
can enable/disable auto scaling, restore from a backup, and add/remove team 
members. 

**Contributor:** Can handle application management and most of the development
lifecycle, but can't manage team members or other actions exclusive to the Admin 
role. 

**Guest:** Has view-only access. Guests can see what's happening in the 
environment but can't perform actions or make any changes. 
