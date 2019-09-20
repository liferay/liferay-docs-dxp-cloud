---
header-id: team-collaboration-access-control
---

# Team Collaboration & Access Control

You can use DXP Cloud's team collaboration features to manage access to your 
environments. Each environment can have unique members, and each member can have 
a role that matches their job's access level in the environment. 

## Managing Team Members

You can manage teams from your environment's *Team* tab in the menu on the left. 

Follow these steps to invite a user to your team: 

1.  Search for the user's email in the *Email* field. 

2.  Use the *Role* menu to select the role to assign to the user. These roles 
    set the user's access level in the environment. For more information, see 
    [Understanding Team Roles](#understanding-team-roles). 

3.  Click *Send Invite*. 

Current and invited team members appear in the *Members* table, in separate 
tabs. You can manage team members via the *Actions* button for each, which lets 
you change the team member's role and remove the member from the team. 

![Figure 1: The Team tab shows your team members and lets you invite new ones.](../../images/invite-member.png)

![Figure 2: Use the Actions button to manage each team member.](../../images/manage-members.png)

## Team Activities

To see your team members' activities, click your environment's *Activities* tab 
in the menu on the left. Each activity lists the person who performed it and the 
date it occurred. This way, you always know who is doing what in your 
environment. 

![Figure 3: The Activities tab shows your team's activities.](../../images/team-activities.png)

## Understanding Team Roles

You can assign these roles to team members: 

**Admin:** Has full control over the environment and its members. They have 
exclusive permission to: 

-   Enable/disable auto scaling
-   Manually downscale a service
-   Restore from a backup
-   Change user role
-   Invite members to the environment
-   Remove members from the environment
-   Enable/disable support access
-   Delete a service

Admins also have the permissions that Contributors have. 

**Contributor:** Can handle application management and most of the development 
lifecycle, but can't manage team members or perform other Admin-exclusive 
actions. They have permission to: 

-   Start a backup
-   Change VPN settings
-   Restart a service
-   Deploy a build
-   Remove themselves from the environment

**Guest:** Has view-only access. Guests can see what's happening in the 
environment but can't perform actions or make any changes. This includes not 
having access to service features such as using shell access to run commands, 
changing/creating environment variables, or specifying custom domains. They only 
have permission to: 

-   Remove themselves from the environment
