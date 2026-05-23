# Wireshark-And-Network-Analysis-Lab
Azure Wireshark Lab

<p align="center">
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/d9193c52-7295-4c14-ba3c-51c82df42f1b" />
>
</p>

<img width="1344" height="755" alt="image" src="https://github.com/user-attachments/assets/f7f86392-acc2-4307-a591-16f6fe310b8f" />


## Lab 2 - WIRESHARK /NETWORK ANALYSIS 

Windows Server 2025 · Azure · Identity & Access Management

### Link to Loom

<https://loom.com/share/d81f1163e52345e79ddc03a43d30b590>

## SOP: Capture and Analyze Network Traffic with Wireshark

### Objective

This SOP explains how to install Wireshark, capture live network traffic, and analyze DNS and HTTP activity to identify resolved IP addresses, form submissions, and TCP streams. It is intended to help a team member reproduce the lab workflow and understand what to look for in each capture.

### Key Steps

 

**1. Download and install Wireshark** [0:00](https://loom.com/share/d81f1163e52345e79ddc03a43d30b590?t=0)

<img width="1728" height="1080" alt="image" src="https://github.com/user-attachments/assets/d5afa956-27f2-40ec-82a5-b08e673534d9" />


- Go to **Wireshark.org** and open the **Download** section.
- Select the correct installer for your operating system (for example, **Windows 64-bit** on Windows).
- Download the `.exe` file and run the installer.
- Complete the installation wizard and launch **Wireshark**.

 

**2. Start a live packet capture** [0:55](https://loom.com/share/d81f1163e52345e79ddc03a43d30b590?t=55)

<img width="1728" height="1080" alt="image" src="https://github.com/user-attachments/assets/3130d25e-8f0a-41fd-b456-97a9147016ef" />


- In Wireshark, choose the active network interface you want to monitor.
- Select **Ethernet** or **Ethernet 6** depending on your system.
- Confirm that packets are being captured in real time.
- Keep the capture running while you generate network activity.

 

**3. Generate DNS traffic with nslookup** [1:33](https://loom.com/share/d81f1163e52345e79ddc03a43d30b590?t=93)

<img width="1728" height="1080" alt="image" src="https://github.com/user-attachments/assets/6e533bc8-e2ad-43f8-aac0-a6a07d1c4f2f" />


- Open a command prompt or terminal window.
- Run the command: 
  - `nslookup google.com`
- This creates DNS traffic that can be observed in Wireshark.
- Return to Wireshark after the command completes.

 

**4. Stop the capture and filter for DNS** [2:18](https://loom.com/share/d81f1163e52345e79ddc03a43d30b590?t=138)

<img width="1728" height="1080" alt="image" src="https://github.com/user-attachments/assets/6b26bbac-6c65-43a2-bc8e-ae52b87ce38d" />



- Stop the live capture using the red stop button.
- In the Wireshark display filter bar, type **DNS** and press **Enter**.
- Review the filtered results for a **standard query response** related to `google.com`.
- Expand the DNS details and open the **Answers** section to view the resolved IP address.

 

**5. Verify the DNS response matches the command output** [3:15](https://loom.com/share/d81f1163e52345e79ddc03a43d30b590?t=195)

<img width="1728" height="1080" alt="image" src="https://github.com/user-attachments/assets/f23f2ec8-e1e3-4ddf-a657-1bf9c536dbd5" />



- Compare the IP address shown in Wireshark with the result returned by `nslookup`.
- Confirm that the DNS answer corresponds to `google.com`.
- Use this step to validate that Wireshark is correctly capturing and displaying DNS resolution data.

 

**6. Capture traffic from a website visit** [5:05](https://loom.com/share/d81f1163e52345e79ddc03a43d30b590?t=305)

<img width="1728" height="1080" alt="image" src="https://github.com/user-attachments/assets/24255d79-9215-4e37-950e-f3b49dba0fd7" />


- Start a new packet capture in Wireshark.
- Open a web browser and visit a target site such as `0.webappsecurity.com`.
- Let the page load so that HTTP/HTTPS traffic is generated.
- Stop the capture after enough traffic has been collected.

 

**7. Inspect HTTP form data in the capture** [9:31](https://loom.com/share/d81f1163e52345e79ddc03a43d30b590?t=571)

<img width="1728" height="1080" alt="image" src="https://github.com/user-attachments/assets/a71af12b-716a-490e-a08b-e89e5315a3fb" />


- In Wireshark, filter the traffic using: 
  - `http.request.method == POST`
- Locate the relevant packet and expand the **HTML Form URL Encoded** section.
- Review the captured form fields, including any submitted login or password values.
- Use this step to understand how unencrypted form submissions can expose sensitive data.

 

**8. Review TCP stream content** [11:41](https://loom.com/share/d81f1163e52345e79ddc03a43d30b590?t=701)

<img width="1728" height="1080" alt="image" src="https://github.com/user-attachments/assets/5c81ac14-5f41-4557-891b-0cedf37f665b" />


- Filter the capture for **HTTP** traffic.
- Right-click a relevant packet and select **Follow → TCP Stream**.
- Review the full conversation between client and server in the stream window.
- This helps reconstruct the session and inspect the exchanged data in context.

 

**9. Save the capture for later analysis** [13:24](https://loom.com/share/d81f1163e52345e79ddc03a43d30b590?t=804)

<img width="1728" height="1080" alt="image" src="https://github.com/user-attachments/assets/b9272bcb-369a-4b72-bcbf-5d8e0a8bf7e3" />


- In Wireshark, go to **File**.
- Choose **Save As** or **Export Specified Packets** depending on what you need to preserve.
- Name the file clearly, such as **Capture One**.
- Save the capture in a known location for future review or reporting.

### Cautionary Notes

- **Do not capture or inspect traffic without authorization.** Only perform these steps in a lab or on systems you are permitted to analyze.
- **HTTP traffic can expose credentials in plain text.** Use HTTPS whenever possible to protect sensitive information.
- **Be careful when handling captured data.** Packet captures may contain usernames, passwords, session tokens, and other confidential details.
- **Make sure you stop and restart captures intentionally.** Accidentally stopping too early may cause you to miss the traffic you need.
- **Use the correct interface.** Capturing on the wrong adapter may result in no useful packets being recorded.

### Tips for Efficiency

- Keep Wireshark and the command prompt visible side by side to compare results quickly.
- Use display filters like `DNS` and `http.request.method == POST` to narrow results faster.
- Label saved captures with descriptive names and dates for easier retrieval.
- If a capture is too noisy, stop it, clear the filter, and repeat the test with only the required traffic.
- For repeatable analysis, generate one type of traffic at a time so the packet trace is easier to interpret.

