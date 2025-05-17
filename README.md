# Azure Infrastructure Project

# End-to-End Azure Infrastructure Deployment with Monitoring, Logging, and Troubleshooting

This project demonstrates a step-by-step deployment of a Windows-based Azure infrastructure in the India region. It includes networking, virtual machines (VMs), file sharing, NSG configuration, monitoring, and basic troubleshooting.

## 🧱 Project Components

- Virtual Network: `Infra-VNet`
- Subnets:
  - `WebSubnet` for WebVM
  - `AppSubnet` for AppVM
- Windows VMs:
  - `WebVM` (public IP enabled)
  - `AppVM` (private only, RDP via WebVM)
- Azure File Share
- NSG with custom rules
- Monitoring: Log Analytics + Azure Monitor

---

## ✅ Phase 1: Networking Setup

1. **Create Resource Group**: `AzureInfra-RG` (Region: India)
2. **Create Virtual Network**: `Infra-VNet` with IP range `10.0.0.0/16`
3. **Create Subnets**:
   - `WebSubnet` → `10.0.1.0/24`
   - `AppSubnet` → `10.0.2.0/24`

---

## 💻 Phase 2: VM Creation (Windows)

### WebVM

- OS: Windows Server 2019
- Subnet: `WebSubnet`
- Public IP: Enabled
- NSG: Allow RDP (3389) inbound
- Username/password: Set securely

### AppVM

- OS: Windows Server 2019
- Subnet: `AppSubnet`
- Public IP: Disabled
- NSG: No public access (only allow RDP from `WebSubnet`)

---

## 🔐 Phase 3: NSG Configuration

- **WebVM-NSG**:  
  - Inbound: Allow port 3389 from Internet

- **AppVM-NSG**:  
  - Inbound: Allow port 3389 only from `WebSubnet` range (10.0.1.0/24)

---

## 🔗 Phase 4: Azure File Share

1. Create a **Storage Account**
2. Create a **File Share**
3. From both VMs, mount it using PowerShell:
   ```powershell
   net use Z: \<storageaccount>.file.core.windows.net\<fileshare> /u:<storageaccount> <key>
   ```

---

## 🔍 Phase 5: Monitoring & Logging

1. Create **Log Analytics Workspace**
2. Enable Monitoring from VM > Insights
3. View metrics: CPU, disk, memory usage

---

## 🛠️ Troubleshooting Tips

- RDP not working?
  - Check NSG rules
  - Ensure VM status is "Running"
  - Try restarting the VM
- File share not mounting?
  - Check network connectivity
  - Validate access key

---

## 📦 Outcome

You now have a secure, segmented, and monitored Azure infrastructure deployed manually—ideal for real-world L1/L2 Azure support roles and interview practice.

---

## 🔗 Optional Add-ons

- Add Application Gateway or Load Balancer
- Configure backup/recovery
- Deploy IIS and test site-to-site communication
