# 👻 Ghost Security Module
**PowerShell-Based Windows & Azure Security Hardening Tool**

> **Proactive security hardening for Windows endpoints and Azure environments.** Ghost provides PowerShell-based hardening functions that can help reduce common attack vectors by disabling unnecessary services and protocols.

## ⚠️ Important Disclaimers

**TESTING REQUIRED**: Always test Ghost in non-production environments first. Disabling services may impact legitimate business functions.

**NO GUARANTEES**: While Ghost targets common attack vectors, no security tool can prevent all attacks. This is one component of a comprehensive security strategy.

**OPERATIONAL IMPACT**: Some functions may affect system functionality. Review each setting carefully before deployment.

**PROFESSIONAL ASSESSMENT**: For production environments, consult with security professionals to ensure settings align with your organization's needs.

## 📊 The Security Landscape

Ransomware damages reached **$57 billion in 2025**, with research indicating that many successful attacks exploit basic Windows services and misconfigurations. Common attack vectors include:

- **90% of ransomware incidents** involve RDP exploitation
- **SMBv1 vulnerabilities** enabled attacks like WannaCry and NotPetya  
- **Document macros** remain a primary malware delivery method
- **USB-based attacks** continue to target air-gapped networks
- **PowerShell abuse** has increased significantly in recent years

## 🛡️ Ghost Security Functions

Ghost provides **16 Windows hardening functions** plus **Azure security integration**:

### Windows Endpoint Hardening

| Function | Purpose | Considerations |
|----------|---------|----------------|
| `Set-RDP` | Manages Remote Desktop access | May impact remote administration |
| `Set-SMBv1` | Controls legacy SMB protocol | Required for very old systems |
| `Set-AutoRun` | Controls AutoPlay/AutoRun | May impact user convenience |
| `Set-USBStorage` | Restricts USB storage devices | May impact legitimate USB use |
| `Set-Macros` | Controls Office macro execution | May impact macro-enabled documents |
| `Set-PSRemoting` | Manages PowerShell remoting | May impact remote management |
| `Set-WinRM` | Controls Windows Remote Management | May affect remote administration |
| `Set-LLMNR` | Manages name resolution protocol | Usually safe to disable |
| `Set-NetBIOS` | Controls NetBIOS over TCP/IP | May affect legacy applications |
| `Set-AdminShares` | Manages administrative shares | May impact remote file access |
| `Set-Telemetry` | Controls data collection | May affect diagnostic capabilities |
| `Set-GuestAccount` | Manages Guest account | Usually safe to disable |
| `Set-ICMP` | Controls ping responses | May affect network diagnostics |
| `Set-RemoteAssistance` | Manages Remote Assistance | May impact help desk operations |
| `Set-NetworkDiscovery` | Controls network discovery | May affect network browsing |
| `Set-Firewall` | Manages Windows Firewall | Critical for network security |

### Azure Cloud Security

| Function | Purpose | Requirements |
|----------|---------|--------------|
| `Set-AzureSecurityDefaults` | Enables basic Azure AD security | Microsoft Graph permissions |
| `Set-AzureConditionalAccess` | Configures access policies | Azure AD P1/P2 licensing |
| `Set-AzurePrivilegedUsers` | Audits privileged accounts | Global Admin permissions |

### Enterprise Deployment Options

| Method | Use Case | Requirements |
|--------|----------|--------------|
| **Direct Execution** | Testing, small environments | Local admin rights |
| **Group Policy** | Domain environments | Domain admin, GP management |
| **Microsoft Intune** | Cloud-managed devices | Intune licensing, Graph API |

## 🚀 Quick Start

### Security Assessment
```powershell
# Load Ghost module
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')

# Check current security posture
Get-Ghost
```

### Basic Hardening (Test First)
```powershell
# Essential hardening - test in lab environment first
Set-Ghost -SMBv1 -AutoRun -Macros

# Review changes
Get-Ghost
```

### Enterprise Deployment
```powershell
# Group Policy deployment (domain environments)
Set-Ghost -SMBv1 -AutoRun -GroupPolicy

# Intune deployment (cloud-managed devices)
Set-Ghost -SMBv1 -RDP -USBStorage -Intune
```

## 📋 Installation Methods

### Option 1: Direct Download (Testing)
```powershell
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')
```

### Option 2: Module Installation
```powershell
# Install from PowerShell Gallery (when available)
Install-Module Ghost -Scope CurrentUser
Import-Module Ghost
```

### Option 3: Enterprise Deployment
```powershell
# Copy to network location for Group Policy deployment
# Configure Intune PowerShell scripts for cloud deployment
```

## 💼 Use Case Examples

### Small Business
```powershell
# Basic protection with minimal impact
Set-Ghost -SMBv1 -AutoRun -Macros -ICMP
```

### Healthcare Environment
```powershell
# HIPAA-focused hardening
Set-Ghost -SMBv1 -RDP -USBStorage -AdminShares -Telemetry
```

### Financial Services
```powershell
# High-security configuration
Set-Ghost -RDP -SMBv1 -AutoRun -USBStorage -Macros -PSRemoting -AdminShares
```

### Cloud-First Organization
```powershell
# Intune-managed deployment
Connect-IntuneGhost -Interactive
Set-Ghost -SMBv1 -RDP -AutoRun -Macros -Intune
```

## 🔍 Function Details

### Core Hardening Functions

#### Network Services
- **RDP**: Blocks remote desktop access or randomizes port
- **SMBv1**: Disables legacy file sharing protocol
- **ICMP**: Prevents ping responses for reconnaissance
- **LLMNR/NetBIOS**: Blocks legacy name resolution protocols

#### Application Security  
- **Macros**: Disables macro execution in Office applications
- **AutoRun**: Prevents automatic execution from removable media

#### Remote Management
- **PSRemoting**: Disables PowerShell remote sessions
- **WinRM**: Stops Windows Remote Management
- **Remote Assistance**: Blocks remote assistance connections

#### Access Control
- **Admin Shares**: Disables C$, ADMIN$ shares
- **Guest Account**: Disables Guest account access
- **USB Storage**: Restricts USB device usage

### Azure Integration
```powershell
# Connect to Azure tenant
Connect-AzureGhost -Interactive

# Enable security defaults
Set-AzureSecurityDefaults -Enable

# Configure conditional access
Set-AzureConditionalAccess -BlockLegacyAuth -RequireMFA

# Audit privileged users
Set-AzurePrivilegedUsers -AuditOnly
```

### Intune Integration (New in v2)
```powershell
# Connect to Intune
Connect-IntuneGhost -Interactive

# Deploy via Intune policies
Set-IntuneGhost -Settings @{
    RDP = $true
    SMBv1 = $true
    USBStorage = $true
    Macros = $true
}
```

## ⚠️ Important Considerations

### Testing Requirements
- **Lab Environment**: Test all settings in isolated environment first
- **Phased Deployment**: Roll out gradually to identify issues
- **Rollback Plan**: Ensure you can reverse changes if needed
- **Documentation**: Record which settings work for your environment

### Potential Impact
- **User Productivity**: Some settings may affect daily workflows
- **Legacy Applications**: Older systems may require certain protocols
- **Remote Access**: Consider impact on legitimate remote administration
- **Business Processes**: Verify settings don't break critical functions

### Security Limitations
- **Defense in Depth**: Ghost is one layer of security, not a complete solution
- **Ongoing Management**: Security requires continuous monitoring and updates
- **User Training**: Technical controls must be paired with security awareness
- **Threat Evolution**: New attack methods may bypass current protections

## 🎯 Example Attack Scenarios

While Ghost targets common attack vectors, specific prevention depends on proper implementation and testing:

### WannaCry-Style Attacks
- **Mitigation**: `Set-Ghost -SMBv1` disables the vulnerable protocol
- **Consideration**: Ensure no legacy systems require SMBv1

### RDP-Based Ransomware
- **Mitigation**: `Set-Ghost -RDP` blocks remote desktop access
- **Consideration**: May require alternative remote access methods

### Document-Based Malware
- **Mitigation**: `Set-Ghost -Macros` disables macro execution
- **Consideration**: May impact legitimate macro-enabled documents

### USB-Delivered Threats
- **Mitigation**: `Set-Ghost -USBStorage -AutoRun` restricts USB functionality
- **Consideration**: May impact legitimate USB device usage

## 🏢 Enterprise Features

### Group Policy Support
```powershell
# Apply settings via Group Policy registry
Set-Ghost -SMBv1 -RDP -AutoRun -GroupPolicy

# Settings apply domain-wide after GP refresh
gpupdate /force
```

### Microsoft Intune Integration
```powershell
# Create Intune policies for Ghost settings
Set-IntuneGhost -Settings $GhostSettings -Interactive

# Policies deploy to managed devices automatically
```

### Compliance Reporting
```powershell
# Generate security assessment report
Get-Ghost | Export-Csv -Path "SecurityAudit-$(Get-Date -Format 'yyyy-MM-dd').csv"

# Azure security posture report
Get-AzureGhost | Out-File "AzureSecurityReport.txt"
```

## 📚 Best Practices

### Pre-Deployment
1. **Document Current State**: Run `Get-Ghost` before changes
2. **Test Thoroughly**: Validate in non-production environment
3. **Plan Rollback**: Know how to reverse each setting
4. **Stakeholder Review**: Ensure business units approve changes

### During Deployment
1. **Phased Approach**: Deploy to pilot groups first
2. **Monitor Impact**: Watch for user complaints or system issues
3. **Document Issues**: Record any problems for future reference
4. **Communicate Changes**: Inform users of security improvements

### Post-Deployment
1. **Regular Assessment**: Periodically run `Get-Ghost` to verify settings
2. **Update Documentation**: Keep security configurations current
3. **Review Effectiveness**: Monitor for security incidents
4. **Continuous Improvement**: Adjust settings based on threat landscape

## 🔧 Troubleshooting

### Common Issues
- **Permission Errors**: Ensure elevated PowerShell session
- **Service Dependencies**: Some services may have dependencies
- **Application Compatibility**: Test with business applications
- **Network Connectivity**: Verify remote access still works

### Recovery Options
```powershell
# Re-enable specific services if needed
Set-RDP -Enable
Set-SMBv1 -Enable
Set-AutoRun -Enable
Set-Macros -Enable
```

## 👨‍💻 About the Author

**Jim Tyler** - Microsoft MVP for PowerShell
- **YouTube**: [@PowerShellEngineer](https://youtube.com/@PowerShellEngineer) (10,000+ subscribers)
- **Newsletter**: [PowerShell.News](https://powershell.news) - Weekly security intelligence
- **Author**: "PowerShell for Systems Engineers"
- **Experience**: Decades of PowerShell automation and Windows security

## 📄 License & Disclaimer

### MIT License
Ghost is provided under the MIT License for free use, modification, and distribution.

### Security Disclaimer
- **No Warranty**: Ghost is provided "as-is" without warranty of any kind
- **Testing Required**: Always test in non-production environments first
- **Professional Guidance**: Consult security professionals for production deployments
- **Operational Impact**: The authors are not responsible for any operational disruption
- **Comprehensive Security**: Ghost is one component of a complete security strategy

### Support
- **GitHub Issues**: [Report bugs or request features](https://github.com/jimrtyler/Ghost/issues)
- **Documentation**: Use `Get-Help <function> -Full` for detailed help
- **Community**: PowerShell and security community forums

---

**🔐 Strengthen your security posture with Ghost - but always test first.**

```powershell
# Start with assessment, not assumptions
Get-Ghost
```

**⭐ Star this repository if Ghost helps improve your security posture!**