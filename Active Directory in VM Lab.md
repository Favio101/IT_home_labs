# Building an Active Directory and Creating GPOs in VM Home Lab 
- Installed VMware and Windows Server 25
- Created the VM and set up it's specs
- Learned how to mount an ISO and assign a boot location for the OS
- Specs:
  
![VM specs](https://github.com/user-attachments/assets/c0698009-9d88-48d0-839a-8320189895dd)

- Verifying Windows OS with winver:

![winver](https://github.com/user-attachments/assets/228fdb1d-1838-4ae1-9197-aa23d6cd7397)

- Installed Active Directory Domain Services and other roles and features through the Server Manager
- Created an AD domain (FavioServer.local) and promoted the server to domain controller

# Creating OUs, Users, Computers, and Servers
1. Creating OUs
   - Created OU for USA
     
  ![Screenshot 2025-07-02 163116](https://github.com/user-attachments/assets/a3ec809f-04ea-425d-9c10-ea7633849efc)

   - Repeat process for Europe
   - Repeat process for Asia
   - Created common sub-OUs (Computers, User, Servers) for every country OU
     
     ![Final OUs](https://github.com/user-attachments/assets/72904270-10f9-46fb-ac36-505ad690f696)

2. Creating Groups ("Deparments")
   - Created groups under each of the sub-OUs (each group represents a department)
   - Department groups given global scope (accessible only within this domain) and set as security groups 
   - Departments included: IT, Sales, and Management
   - Created a distribution group for all employees within each OU (distribution list for email purposes)
     
     ![Final Groups](https://github.com/user-attachments/assets/82a8f508-7585-4c53-9dc8-93fd9583f304)

  3. Creating Users
- Created users under the OUs
  
![Creating User](https://github.com/user-attachments/assets/eda3f861-47a9-453a-9ac2-c9ac90749f91)

- Added users to groups
  
![Add User to Group](https://github.com/user-attachments/assets/a3b8296d-80e2-49ea-9f12-2fff12f6baad)

# Implementing GPOs in the GPMC  (* = right click)
1. Creating a Password GPO (enhances domain security and enforces strong passwords)
   - Created a GPO, named "Password Policy" for Computer under the USA OU
   - Navigation: "*Edit" ---> "Computer Configuration" --> "Policies" --> "Windows Settings" --> "Security Settings" --> "Account Policies" --> "Password Policy"
   - Set the password expiration date to each quarter (90 days), set the minimum password length to 12 characters, and enabled password complexity requirements.
   - Learned the basics of creating GPOs and establishing basic security measures
   
<img width="1026" height="773" alt="Password Policy" src="https://github.com/user-attachments/assets/e353ca07-6134-4652-9075-1ac4daf551b5" />

2. Drive Mapping with a GPO
- Created a GPO, named "Drive Mapping", for Users under the USA OU
- Navigation: "*Edit" ---> "User Configuration" --> "Preferences" --> "Windows Settings" --> "Drive Maps" --> "*New" --> "*Mapped Drive"
- Set the location and drive letter for the new drive

<img width="1026" height="776" alt="Mapped Drive" src="https://github.com/user-attachments/assets/8282829a-fd37-4e37-a660-e908b9c0120b" />


3. Setting a Desktop Wallpaper Policy (default wallpaper for all users)
   - Created a GPO, named "Desktop Wallpaper" for Users under the USA OU
   - Navigation: "*Edit" ---> "User Configuration" --> "Policies" --> "Administrative Templates..." --> "Desktop" --> "Desktop" --> "Desktop Wallpaper"
   - Enabled desktop wallpaper policy and set the local path to the wallpaper 

<img width="1023" height="770" alt="Desktop Wallpaper GPO" src="https://github.com/user-attachments/assets/64621c57-ecb2-40d4-b123-c91d90958459" />


4. Restrict Access to Control Panel (prevent users from accessing Control Panel)
   - Created a GPO, named "Restrict Control Panel" for Users under the USA OU
   - Navigation: "*Edit" ---> "User Configuration" --> "Policies" --> "Administrative Templates..." --> "" --> "Control Panel" --> "Prohibit access to Control..."
   - Enabled "Prohibit access to Control Panel and PC settings" in "Control Panel" configurations

<img width="1025" height="775" alt="Restrict Access to Control Panel" src="https://github.com/user-attachments/assets/fe4da725-de20-44d4-8620-f2b91d060f74" />


5. Disable USB Storage (security measure, prevents the use of USB storage devices)
   - Created a GPO, named "Disable USB Devices", for Computer under the USA OU
   - Navigation: "*Edit" ---> "Computer Configuration" --> "Policies" --> "Administrative Templates..." --> "System" --> "Removable Storage Access" --> "All Removable Storage Classes: Deny all access"
   - Enabled setting to deny access to removable storage

<img width="1024" height="770" alt="USB Denial" src="https://github.com/user-attachments/assets/2ed13d64-4dee-43e0-a386-93731c0038bf" />


6. Account Lockout GPO (helps prevent brute force attacks)
   - Created a GPO, named "Account Lockout Policy", for Computer under the USA OU
   - Navigation: "*Edit" ---> "Computer Configuration" --> "Policies" --> "Windows Settings" --> "Security Settings" --> "Account Policies" --> "Account Lockout Policy"
   - Set the account lockout threshold to 3 attempts and the lockout duration to 30 minutes

<img width="1027" height="767" alt="Account Lockout" src="https://github.com/user-attachments/assets/c7977bc2-ee7c-4618-88c3-f694d8b37c78" />


#Applying and Testing GPOs 
- Downloaded Windows 11 Enterprise
- Setup another VM, but with Windows 11 Enterprise
- VM specs:

<img width="1066" height="573" alt="2nd VM Specs" src="https://github.com/user-attachments/assets/442745ea-7439-4f4e-9274-8420656ff9d1" />


1. Set up DNS server 
  - Set up a static IP address and configured the DNS address (used loopback address) (on domain controller)
  - Verified IP addresses with "ipconfig /all" in command line

<img width="1038" height="773" alt="Host VM ipconfig" src="https://github.com/user-attachments/assets/6ec917dd-fbd0-4df0-8e0b-f429770a47dd" />


  - Changed DNS server address on client VM to the host VM DNS server address
  - Verified DNS server address configuration and resolution on client VM through the command line ("ipconfig /all" and "nslookup")

<img width="1032" height="766" alt="Client VN Ipconfig" src="https://github.com/user-attachments/assets/8d1bfe28-d5d7-40e2-88fd-9619aa8b3d21" />

  - Joined the domain on the client VM through the Settings app and signed in with user "John Snith" which I created earlier as part of the USA OU
  - Moved the client VM computer to the Computers OU under USA in the Active Directory Users and Computers
  - Used "gpupdate /force" and verified that GPOs are functional (control panel was inaccessible for John Smith, had default wallpaper, mapped drive, etc)
     





