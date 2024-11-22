# Execution Process

## 1. Transfer Assignment 4 file to Putty Server using UNT credentials

## 2. Install Cyberduck on Mac

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

<img width="579" alt="image" src="https://github.com/user-attachments/assets/591c1f35-6892-480a-bdc1-961f23f13561">



## 3. Run Script

After loading the Assignment 4 file, follow these steps:

<img width="468" alt="image" src="https://github.com/user-attachments/assets/092ba799-2ca2-4aec-bc7c-c07b0893f389">

<img width="1005" alt="image" src="https://github.com/user-attachments/assets/1a9c776d-a412-4f54-8202-4ab643a9bb0b">

<img width="992" alt="image" src="https://github.com/user-attachments/assets/b79f82a2-1b90-4e3e-ba3c-100b2f5104ee">

## 4. Use the following to run the script!

```bash
uv0032@cell03-cse:~$ cd Assignment4/
uv0032@cell03-cse:~/Assignment4$ cd d4-7
uv0032@cell03-cse:~/Assignment4/d4-7$ vi run_cache_simulator.sh
uv0032@cell03-cse:~/Assignment4/d4-7$ chmod 777 run_cache_simulator.sh
uv0032@cell03-cse:~/Assignment4/d4-7$ ./run_cache_simulator.sh
```

<img width="1324" alt="image" src="https://github.com/user-attachments/assets/58598cb7-1206-46d7-b8e5-9941c47c81e6">

## 5. Run Cache Simulator
```bash
#!/bin/bash

# Create output directory if it doesn't exist
mkdir -p output

# Function to run Dinero IV tests for a specific trace
run_trace_tests() {
    local trace_file=$1

    # L1 Cache Configurations without L2
    echo "# L1 Cache Tests without L2 for $trace_file #"
    
    # 16KB, 32B, 1-way
    echo "## 16KB, 32B, 1-way L1 Cache ##"
    ./dineroIV -l1-isize 16K -l1-ibsize 32 -l1-isbsize 32 -l1-iassoc 1 \
               -l1-dsize 16K -l1-dbsize 32 -l1-dsbsize 32 -l1-dassoc 1 \
               -informat d < "$trace_file" > "output/results_$(basename "$trace_file" .din)_16k_32b_1way.txt"

    # 16KB, 32B, 2-way
    echo "## 16KB, 32B, 2-way L1 Cache ##"
    ./dineroIV -l1-isize 16K -l1-ibsize 32 -l1-isbsize 32 -l1-iassoc 2 \
               -l1-dsize 16K -l1-dbsize 32 -l1-dsbsize 32 -l1-dassoc 2 \
               -informat d < "$trace_file" > "output/results_$(basename "$trace_file" .din)_16k_32b_2way.txt"

    # 16KB, 32B, 4-way
    echo "## 16KB, 32B, 4-way L1 Cache ##"
    ./dineroIV -l1-isize 16K -l1-ibsize 32 -l1-isbsize 32 -l1-iassoc 4 \
               -l1-dsize 16K -l1-dbsize 32 -l1-dsbsize 32 -l1-dassoc 4 \
               -informat d < "$trace_file" > "output/results_$(basename "$trace_file" .din)_16k_32b_4way.txt"

    # 16KB, 64B, 1-way
    echo "## 16KB, 64B, 1-way L1 Cache ##"
    ./dineroIV -l1-isize 16K -l1-ibsize 64 -l1-isbsize 64 -l1-iassoc 1 \
               -l1-dsize 16K -l1-dbsize 64 -l1-dsbsize 64 -l1-dassoc 1 \
               -informat d < "$trace_file" > "output/results_$(basename "$trace_file" .din)_16k_64b_1way.txt"

    # 16KB, 64B, 2-way
    echo "## 16KB, 64B, 2-way L1 Cache ##"
    ./dineroIV -l1-isize 16K -l1-ibsize 64 -l1-isbsize 64 -l1-iassoc 2 \
               -l1-dsize 16K -l1-dbsize 64 -l1-dsbsize 64 -l1-dassoc 2 \
               -informat d < "$trace_file" > "output/results_$(basename "$trace_file" .din)_16k_64b_2way.txt"

    # 16KB, 64B, 4-way
    echo "## 16KB, 64B, 4-way L1 Cache ##"
    ./dineroIV -l1-isize 16K -l1-ibsize 64 -l1-isbsize 64 -l1-iassoc 4 \
               -l1-dsize 16K -l1-dbsize 64 -l1-dsbsize 64 -l1-dassoc 4 \
               -informat d < "$trace_file" > "output/results_$(basename "$trace_file" .din)_16k_64b_4way.txt"

    # L1 and L2 Cache Configurations
    echo "# L1 and L2 Cache Tests for $trace_file #"
    
    # 16KB L1, 128KB L2, 32B, 1-way
    echo "## 16KB L1, 128KB L2, 32B, 1-way ##"
    ./dineroIV -l1-isize 16K -l1-ibsize 32 -l1-isbsize 32 -l1-iassoc 1 \
               -l1-dsize 16K -l1-dbsize 32 -l1-dsbsize 32 -l1-dassoc 1 \
               -l2-usize 128K -l2-ubsize 32 -l2-usbsize 32 -l2-uassoc 1 \
               -informat d < "$trace_file" > "output/results_$(basename "$trace_file" .din)_16k_128k_32b_1way.txt"

    # 16KB L1, 128KB L2, 32B, 2-way
    echo "## 16KB L1, 128KB L2, 32B, 2-way ##"
    ./dineroIV -l1-isize 16K -l1-ibsize 32 -l1-isbsize 32 -l1-iassoc 2 \
               -l1-dsize 16K -l1-dbsize 32 -l1-dsbsize 32 -l1-dassoc 2 \
               -l2-usize 128K -l2-ubsize 32 -l2-usbsize 32 -l2-uassoc 2 \
               -informat d < "$trace_file" > "output/results_$(basename "$trace_file" .din)_16k_128k_32b_2way.txt"

    # 16KB L1, 128KB L2, 32B, 4-way
    echo "## 16KB L1, 128KB L2, 32B, 4-way ##"
    ./dineroIV -l1-isize 16K -l1-ibsize 32 -l1-isbsize 32 -l1-iassoc 4 \
               -l1-dsize 16K -l1-dbsize 32 -l1-dsbsize 32 -l1-dassoc 4 \
               -l2-usize 128K -l2-ubsize 32 -l2-usbsize 32 -l2-uassoc 4 \
               -informat d < "$trace_file" > "output/results_$(basename "$trace_file" .din)_16k_128k_32b_4way.txt"

    # 16KB L1, 128KB L2, 64B, 1-way
    echo "## 16KB L1, 128KB L2, 64B, 1-way ##"
    ./dineroIV -l1-isize 16K -l1-ibsize 64 -l1-isbsize 64 -l1-iassoc 1 \
               -l1-dsize 16K -l1-dbsize 64 -l1-dsbsize 64 -l1-dassoc 1 \
               -l2-usize 128K -l2-ubsize 64 -l2-usbsize 64 -l2-uassoc 1 \
               -informat d < "$trace_file" > "output/results_$(basename "$trace_file" .din)_16k_128k_64b_1way.txt"

    # 16KB L1, 128KB L2, 64B, 2-way
    echo "## 16KB L1, 128KB L2, 64B, 2-way ##"
    ./dineroIV -l1-isize 16K -l1-ibsize 64 -l1-isbsize 64 -l1-iassoc 2 \
               -l1-dsize 16K -l1-dbsize 64 -l1-dsbsize 64 -l1-dassoc 2 \
               -l2-usize 128K -l2-ubsize 64 -l2-usbsize 64 -l2-uassoc 2 \
               -informat d < "$trace_file" > "output/results_$(basename "$trace_file" .din)_16k_128k_64b_2way.txt"

    # 16KB L1, 128KB L2, 64B, 4-way
    echo "## 16KB L1, 128KB L2, 64B, 4-way ##"
    ./dineroIV -l1-isize 16K -l1-ibsize 64 -l1-isbsize 64 -l1-iassoc 4 \
               -l1-dsize 16K -l1-dbsize 64 -l1-dsbsize 64 -l1-dassoc 4 \
               -l2-usize 128K -l2-ubsize 64 -l2-usbsize 64 -l2-uassoc 4 \
               -informat d < "$trace_file" > "output/results_$(basename "$trace_file" .din)_16k_128k_64b_4way.txt"
}

# Main execution for all traces
run_trace_tests "Trace1.din"
run_trace_tests "Trace2.din"
run_trace_tests "Trace3.din"
```

## 6. Output Files

<img width="1305" alt="image" src="https://github.com/user-attachments/assets/3a43fc2d-cb6d-4577-8a39-70e212a51735">


