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
- From **Client-1**, pinging `mainframe` still resolved to the old IP.  
- Displayed cache with:  
  ```bash
  ipconfig /displaydns
  ```  
- Flushed cache with:  
  ```bash
  ipconfig /flushdns
  ```  
- Verified the cache was empty.  
- Re-pinged `mainframe` → now resolved to `8.8.8.8`.  

📸 *[Screenshot placeholder: DNS cache before/after flush]*  

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

## 📂 Repository Layout  
```
DNS-Lab/
│── screenshots/   # My captured images from the lab
│── README.md      # This file
```
