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

## 🖼️ Media (Screenshots)  
*(Insert your screenshots here at each step – turning on VMs, DNS record creation, ping/nslookup results, cache flush results, etc.)*  

---

## 🛠️ Demonstration  

### **1. A-Record Exercise**  
- Started both DC-1 and Client-1 in the Azure Portal.  
- Logged into **DC-1** as `mydomain.com\jane_admin` and **Client-1** as `mydomain\jane_admin`.  
- From **Client-1**, I attempted to ping `mainframe` → it failed.  
- Verified with `nslookup mainframe` → no DNS record found.  
- On **DC-1**, I created a new **A-record** for `mainframe` pointing to DC-1’s private IP.  
- Back on **Client-1**, I pinged `mainframe` again → success.  

📸 *[Screenshot placeholder: Failed ping/nslookup → Creating A-record → Successful ping]*  

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
