# DNS Records & Caching Lab: Active Directory Domain Environment  

## 📌 Project Summary  
This project demonstrates how I configured and tested **DNS records** inside an Active Directory domain hosted on **Microsoft Azure**.  
I worked with two virtual machines:  
- **DC-1** → Windows Server Domain Controller (mydomain.com)  
- **Client-1** → Windows 10 domain-joined client  

**Technologies & Environments Used:**  
- Microsoft Azure (Virtual Machines/Compute)  
- Windows Server (Domain Controller & DNS)  
- Windows 10 Client  
- DNS Management Console  
- Command-line Tools (ping, nslookup, ipconfig)  

The exercises showcase core skills in **DNS management, troubleshooting, and local caching**, which are essential for system administrators and network engineers.  

## 📝 Notes  

### 1. Local DNS Cache  
<img width="1817" height="954" alt="Local DNS Cache Notes" src="https://github.com/user-attachments/assets/97d2120b-59a8-4b17-93b2-3a622a13b9c2" />  

---

### 2. Local Host File  
- Editing the `hosts` file to test name resolution behavior.  

<img width="1111" height="784" alt="Local Host File - Part 1" src="https://github.com/user-attachments/assets/7ae68966-75cd-4922-b0d7-21441a157873" />  
<img width="1173" height="762" alt="Local Host File - Part 2" src="https://github.com/user-attachments/assets/fe50b639-0e0d-4708-9413-b3a6cfdff965" />  
<img width="1167" height="735" alt="Local Host File - Part 3" src="https://github.com/user-attachments/assets/4ad5bde8-06ff-4450-9964-d0e8e0c580f8" />  
<img width="1591" height="887" alt="Local Host File - Part 4" src="https://github.com/user-attachments/assets/50505cdc-b9e8-45df-8849-ace0bc328a10" />  

---

### 3. DNS Server  
- **DC-1 Private IP:** `10.0.0.5`  

---
## 🛠️ Demonstration  

### **1. A-Record Exercise**  
- Started both DC-1 and Client-1 in the Azure Portal.  
- Logged into **DC-1** as `mydomain.com\jane_admin` and **Client-1** as `mydomain\jane_admin`.  
- From **Client-1**, I attempted to ping `mainframe` → it failed.
  <img width="1449" height="611" alt="From Client-1 try to ping “mainframe” notice that it fails" src="https://github.com/user-attachments/assets/30bb5c1d-d5d5-4b98-8b4a-550fdb28e0c5" />

- Verified with `nslookup mainframe` → no DNS record found.
 <img width="1120" height="541" alt="Nslookup “mainframe” notice that it fails (no DNS record)" src="https://github.com/user-attachments/assets/402d7af9-873e-48ae-9058-c09c4e21a169" />
 
- On **DC-1**, I created a new **A-record** for `mainframe` pointing to DC-1’s private IP.
  <img width="828" height="808" alt="Create a DNS A-record on DC-1 for “mainframe” and have it point to DC-1’s Private IP address(1)" src="https://github.com/user-attachments/assets/d28e3253-354f-499b-a06f-0ce7d1162b83" />
<img width="1029" height="905" alt="Create a DNS A-record on DC-1 for “mainframe” and have it point to DC-1’s Private IP address(2)" src="https://github.com/user-attachments/assets/658f5933-1615-4db0-93a6-7bc550bffc42" />
<img width="1106" height="748" alt="Create a DNS A-record on DC-1 for “mainframe” and have it point to DC-1’s Private IP address(3)" src="https://github.com/user-attachments/assets/e5ce1300-86d4-4300-9339-8bca40b57aa1" />
<img width="1068" height="686" alt="Create a DNS A-record on DC-1 for “mainframe” and have it point to DC-1’s Private IP address(4)" src="https://github.com/user-attachments/assets/eb1bef41-1c74-47e4-aa60-2542a1adc2a2" />

- Back on **Client-1**, I pinged `mainframe` again → success.  

<img width="1119" height="518" alt="Go back to Client-1 and try to ping it  Observe that it works" src="https://github.com/user-attachments/assets/68c49ce5-2a53-4c9e-b497-7d7ad5326456" />
 

---

### **2. Local DNS Cache Exercise**  
- Modified the A-record on **DC-1** to point `mainframe` → `8.8.8.8`.
  <img width="1304" height="717" alt="Go back to DC-1 and change mainframe’s record address to 8 8 8 8" src="https://github.com/user-attachments/assets/c51ccc25-c09d-4dce-8e31-5f2e88ce2969" />

- From **Client-1**, pinging `mainframe` still resolved to the old IP.
  <img width="648" height="339" alt="Go back to Client-1 and ping “mainframe” again  Observe that it still pings the old address" src="https://github.com/user-attachments/assets/48394099-b00f-47bc-a22e-9ae426ed9574" />

- Displayed cache with:  
  ```bash
  ipconfig /displaydns
  ```
  <img width="474" height="237" alt="Observe the local dns cache" src="https://github.com/user-attachments/assets/c1712db8-d365-4ad8-951e-d0339eacb236" />

- Flushed cache with:  
  ```bash
  ipconfig /flushdns
  ```  
- Verified the cache was empty.
  <img width="1041" height="505" alt="Flush the DNS cache and Observe that the cache is empty" src="https://github.com/user-attachments/assets/3d4debe9-3083-4538-b4e7-99f5d08e4a7b" />
 
- Re-pinged `mainframe` → now resolved to `8.8.8.8`.  
 <img width="585" height="286" alt="Attempt to ping “mainframe” again" src="https://github.com/user-attachments/assets/3a5b3336-4a3d-460a-8825-9f1849f2fcec" />
 

---

### **3. CNAME Record Exercise**  
- On **DC-1**, created a **CNAME record** that mapped `search` → `www.google.com`.  
- From **Client-1**, ran:  
  ```bash
  ping search
  nslookup search
  ```  
- Verified results → the CNAME successfully redirected to Google.  

📸 *[Screenshot placeholder: CNAME creation → ping/nslookup results]*  

---
## 🚀 What I Learned  
- How to create and test **A-records** and **CNAME records** in Active Directory DNS.  
- How **local DNS cache** can retain outdated records and how to flush it.  
- Hands-on troubleshooting with **ping, nslookup, and ipconfig**.  
- Reinforced real-world system administration tasks that are critical in enterprise IT.  

---


```
