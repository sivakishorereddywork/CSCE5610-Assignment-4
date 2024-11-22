# Execution Process

## Transfer Assignment 4 file to Putty Server using UNT credentials

## Install Cyberduck on Mac

<img width="1470" alt="image" src="https://github.com/user-attachments/assets/65ba6289-e565-45ba-8395-2c7144450f76">


### Step 1: Download Cyberduck
1. Open your web browser.
2. Go to the official Cyberduck website: [https://cyberduck.io](https://cyberduck.io).
3. Click on the **Download for Mac** button.
4. The installer file (Cyberduck-x.x.x.zip) will download to your Mac.

### Step 2: Install Cyberduck
1. Locate the downloaded file in your **Downloads** folder.
2. Double-click the **Cyberduck-x.x.x.zip** file to extract it.
3. Drag the **Cyberduck** app into your **Applications** folder.

### Step 3: Open Cyberduck
1. Go to your **Applications** folder.
2. Double-click the **Cyberduck** icon to launch the app.

### Step 4: Set Up Cyberduck for Your UNT Server
1. In Cyberduck, click **Open Connection**.
2. Enter the following details:
   - **Protocol**: Choose **SFTP (SSH File Transfer Protocol)**.
   - **Server**: `cell03-cse.eng.unt.edu`.
   - **Port**: `22` (default for SSH).
   - **Username**: Your UNT username (e.g., `uv0032`).
   - **Password**: Your password for the server.
3. Click **Connect**.

### Step 5: Transfer Files
1. Once connected, the right panel will show your files on the UNT server.
2. Drag and drop files between your Mac and the server.

## Run Script

After loading the Assignment 4 file, follow these steps:

```bash
uv0032@cell03-cse:~$ cd Assignment4/
uv0032@cell03-cse:~/Assignment4$ cd d4-7
uv0032@cell03-cse:~/Assignment4/d4-7$ vi run_cache_simulator.sh
uv0032@cell03-cse:~/Assignment4/d4-7$ chmod 777 run_cache_simulator.sh
uv0032@cell03-cse:~/Assignment4/d4-7$ ./run_cache_simulator.sh
