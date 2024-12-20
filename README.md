# Centralized-Data-Storage

## Objective

This is part 1 of a several part project. I am repurposing my old hp desktop to server as a home server. The first task I have planned is to setup
a cetralized data storage that can easily share data between all devices on my LAN. This way all files, pictures, movies, etc. can be stored and
accessed from one place. It will also serve as an additional backup for my data.

### Skills Learned

- Creating a shared network drive
- Backing up data on a server
- File sharing across different devices

### Tools Used

- Samba for file sharing

## Steps
1 Set up Samba

  - 1.1 Samba is an open-source software suite that allows Linux and Unix-based systems to interact with Windows systems using the SMB (Server Message Block) protocol. It enables           file and printer sharing across different operating systems over a network, allowing devices to share files and resources. I insalled using the command ‘sudo apt install            samba’.

    ![image](https://github.com/user-attachments/assets/21ea477e-01b6-42ca-a053-38e6eeb4c993)


2 Set up directory to be used as file share

  - 2.1 I gave the directory the name below and ensured it exists with the ls command.
    
    ![image](https://github.com/user-attachments/assets/15ea3595-757f-436b-8d7f-74702643a786)


3 Configure samba to utilize the directory

  - 3.1 I modified the configuration file by using the command 'sudo nano /etc/samba/smb.conf’. Then I entered the below entry so the samba configuration file
    would know how to utilize the shared directory 'mothership-share'.

    ![image](https://github.com/user-attachments/assets/550b3483-74a1-4f58-a985-d9664629bfc9)


  - 3.2 I then had to restart the samba service to apply the changes to the configuration file using the command 'sudo service smbd restart'.


4 Ensure samba traffic is allowed on the samba server

  - 4.1 There may be firewall issues with samba traffic not passing through if this is not applied.

      ![image](https://github.com/user-attachments/assets/6804b91b-12c1-4fe5-b8c1-69f7311f5e59)


5 Create a password for network share

  - 5.1 These login credentials will be asked for everytime I attempt to connect to the network share from another device on the LAN.

      ![image](https://github.com/user-attachments/assets/db226365-8dfd-4a31-9393-b3ae4edf403e)


6 Map a Network Drive and login
  - 6.1 In order to access, this shared folder from a windows device I need to map a drive on the network. Any drive letter can be given (as long as it isn't in use). I chose M:        for mothership and then selected the path to the file share. Which is the IP of my server followed by the name of the shared folder.
    
    ![image](https://github.com/user-attachments/assets/1be360d1-b00b-4f64-8522-ee03748777f5)

  - 6.2 I then used the SMB credentials created in step 5 to successfully access the drive.
  
    ![image](https://github.com/user-attachments/assets/2f6f06cc-9687-4c8a-b790-3524d6715d73)
    
7 Test the drive by sharing a file
  - 7.1 The shared drive now displays on my windows device as shown in the picture below. I can now add files, photos, and videos to this drive from any device on my LAN.
    
    ![image](https://github.com/user-attachments/assets/82168224-597e-48b4-b7c3-9fc8926a5bec)

  - 7.2 Below I created a new file called 'File Goals' from the windows pc and shared it to the drive.

    ![image](https://github.com/user-attachments/assets/5d86546f-57c9-4886-9b9e-9cfaf63191c8)

  - 7.3 If I now move back to my SSH session I can see that the file exists within the shared folder. It is stored locally on the server -- eventhough it was created on the
    Windows pc.

    ![image](https://github.com/user-attachments/assets/54b187a6-7fd1-4f59-8321-2e7128eceacc)
