# Building an Active Directory in VM Home Lab 
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
