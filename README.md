


# Nessus Essential Vulnerability Scanner: Multi-OS Security Assessment

## Key Learnings and Skills Demonstrated

- **Vulnerability Scanning**: Demonstrated proficiency in setting up and using Nessus Essentials for network vulnerability assessment.
- **Network Configuration**: Showcased skills in configuring virtual machines for network scanning, including firewall management and IP addressing.
- **Windows System Administration**: Exhibited expertise in configuring Windows 10 and Windows XP systems for authenticated scanning, including registry modifications and service configurations.
- **Security Analysis**: Demonstrated ability to interpret and analyze vulnerability scan results, prioritizing findings based on severity.
- **Credential Management**: Implemented and managed authenticated scans, showcasing understanding of the importance of internal system access for thorough vulnerability assessment.
- **Remediation Techniques**: Applied vulnerability remediation strategies, including software updates, uninstallation of deprecated software, and system patching.
- **Cross-Version OS Security**: Compared security postures across different Windows versions (10 and XP), demonstrating understanding of how OS age affects vulnerability.
- **Documentation Skills**: Created comprehensive, step-by-step documentation of the setup process and findings, showcasing technical writing abilities.
- **Problem-Solving**: Displayed troubleshooting skills in addressing scan errors and system configuration issues.
- **Risk Assessment**: Demonstrated ability to assess and prioritize security risks based on scan results and system configurations.
- **Virtualization**: Utilized virtual machine technology to create isolated environments for security testing.
- **Continuous Improvement**: Showcased the iterative nature of security assessments through multiple scans and remediation efforts.

This project simulates a real-world vulnerability assessment scenario across multiple operating system versions. It demonstrates practical skills in network security, system administration, and vulnerability management. The hands-on experience gained is directly applicable to roles in information security, particularly in vulnerability management and security operations.

<h1 align="center">Summary Diagram</h1>


<p align="center">
<br/>
<img width="750" alt="Portfolio" src="https://i.imgur.com/6KMFeSz.png">
<br />
</p>


<br />
<br />

<h1 align="center">Project walk-through</h1>

<br />
<br />

---
<a name="toc"></a>
**Table of Contents:**

- [Downloading Nessus Essentials](#downloading-nessus-essentials)
- [Installing the Nessus Essentials Vulnerability Scanner](#installing-the-nessus-essentials-vulnerability-scanner)
- [Installing Windows 10 VM and Configuring Network](#installing-windows-10-vm-and-configuring-network)
- [Network Scan Settings](#network-scan-settings)
- [Performing a Non-Credentialed Scan](#performing-a-non\-credentialed-scan)
- [Scan Result](#scan-result)
- [Configuring Windows 10 VM for Authenticated Scanning](#configuring-windows-10-vm-for-authenticated-scanning)
- [Authenticated Scan Settings](#authenticated-scan-settings)
- [Performing an Authenticated Scan](#performing-an-authenticated-scan)
- [Installing Deprecated Software](#installing-deprecated-software)
- [Windows XP VM Installation and Configuration](#windows-xp-vm-installation-and-configuration)
- [Configuring Windows XP VM for Authenticated Scanning](#configuring-windows-xp-vm-for-authenticated-scanning)
- [Performing an Authenticated Scan on Windows XP Professional](#performing-an-authenticated-scan-on-windows-xp-professional)
- [Windows 10 VM Remediation](#windows-10-vm-remediation)
- [Credentialed Scan after Remediation](#credentialed-scan-after-remediation)



---

<h4>Tip: Any configuration options not mentioned in the walkthrough can be left at their default settings</h4>

---

[back to top](#toc)
## Downloading Nessus Essentials

<br />
<br />


 - Open the web browser and navigate to Tenable's website (https://www.tenable.com/products/nessus/nessus-essentials).
 - Register your name and email to receive the email with the download link and the activation code.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/JWpquyb.png">
<br />
<br />
<br />
<br />



 - Go to your email and click on [Download Nessus]
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/cFcNPhN.png">
<br />
<br />
<br />
<br />


---

[back to top](#toc)
## Installing the Nessus Essentials Vulnerability Scanner

<br />
<br />

 - Open the installation file.
<p align="center">
<br/>
<img width="480" alt="Portfolio" src="https://i.imgur.com/d5qfYWe.png">
<br />
<br />
<br />
<br />


 - Proceed with the default settings.
<p align="center">
<br/>
<img width="480" alt="Portfolio" src="https://i.imgur.com/Cgd9zKB.png">
<br />
<br />
<br />
<br />


 - After the installation completes, launch Nessus' web application by clicking the provided button in the installer. The application will open at:
http://localhost:8834/WelcomeToNessus-Install/welcome
     - *Important: Bookmark this URL or save it somewhere secure. Retrieving it later can be challenging if forgotten.*
 - Click [Connect via SSL] *(This just means your browser initiates a secure, encrypted connection with the Nessus server)*

   
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/0j9f3Zc.png">
<br />
<br />
<br />
<br />


 - You will see a warning sign. Click [Proceed to localhost (unsafe)]
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/mfRlff8.png">
<br />
<br />
<br />
<br />



 - Follow the below steps. You need the activation code you got from the email. Also, register a new user account for the web interface.
 - The installation will take quite a long time. Let's proceed to our VM deployment!
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/Z6kIPBN.png">
<br />
<br />
<br />
<br />


---

[back to top](#toc)
## Installing Windows 10 VM and Configuring Network

<br />
<br />


 - Open VMware. Configure the Windows 10 VM like below. Note that it is important to select the "Bridged" option for the network setting. *(Our scanner will not work if the VM's network configuration is NAT.)*
 - Run the virtual machine. I will skip explaining the OS installation part since I've written about it in other tutorials. 
<p align="center">
<br/>
<img width="380" alt="Portfolio" src="https://i.imgur.com/VFJDR9Q.png">
<br />
<br />
<br />
<br />



 - Log in to the VM with your admin credentials.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/989Wu6H.png">
<br />
<br />
<br />
<br />


 - The left screen is the Windows 10 VM, and the right is the host machine with Nessus Essential installed.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/al0mkFJ.png">
<br />
<br />
<br />
<br />



 - We are going to use our host machine to perform a vulnerability scan against the VM, so we first need to check the network connection between them.
 - Open the command prompt on your host machine and type `ping x.x.x.x -t` *(x.x.x.x should be replaced with your VM's private IP address)*
 - It will return "Request timed out." This means we need to turn off the firewall on the VM.
<p align="center">
<br/>
<img width="700" alt="Portfolio" src="https://i.imgur.com/gH6lzFh.png">
<br />
<br />
<br />
<br />


 - Open the Windows Firewall on the VM.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/s4MjoAH.png">
<br />
<br />
<br />
<br />


 - Select Firewall state "off" for the [domain/private/public] profiles. 
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/375M21x.png">
<br />
<br />
<br />
<br />


 - We can now successfully ping our VM.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/lMIX5G0.png">
<br />
<br />
<br />
<br />

---

[back to top](#toc)
## Network Scan Settings

<br />
<br />

 - Go back to the Nessus Essential web app on your host machine. Select [My Scans] > [New Scan]
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/sQmooTt.png">
<br />
<br />
<br />
<br />


 - Select [Basic Network Scan]
     - *(Sometimes you don't see this option. That means you have to rerun the web application until the option is visible)*
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/YabzLl5.png">
<br />
<br />
<br />
<br />



 - Name the scan "test-scan"
 - Enter your VM's private IP address on [Targets]
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/sWkwGm5.png">
<br />
<br />
<br />
<br />


 - Note that we can also perform a scheduled scan if we are working in a corporate environment (For example, we can make it automatically perform scanning every Tuesday) 
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/LcTnHEz.png">
<br />
<br />
<br />
<br />




 - We can also choose whether to scan common ports or all ports. Scanning all ports will take longer. We can also select the [Custom] option to specify the ports we want to scan.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/UIAhVJ1.png">
<br />
<br />
<br />
<br />


 - When we click on [Credentials], we can enter Windows username and password information. This allows the scanner to perform internal scans, uncovering deeper vulnerabilities related to the registry, file system, outdated software, and insecure services.
 - However, we'll start with a basic network port scan without credentials.
 - Let's go back to the [Settings] tab and click [Save]
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/QBmIHrf.png">
<br />
<br />
<br />
<br />


---

[back to top](#toc)
## Performing a Non-Credentialed Scan

<br />
<br />

 - We now have a scan configured. Let's run it. Click on the small right-arrow button on the right. 
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/ZKffe8A.png">
<br />
<br />
<br />
<br />



 - The check mark indicates that the scan is finished. Let's take a look at the result.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/cjjHSj6.png">
<br />
<br />
<br />
<br />



---

[back to top](#toc)
## Scan Result

<br />
<br />



 - Our scan has revealed 14 vulnerabilities. In the bottom right corner, you'll notice a graphical representation of these findings, categorized by severity from Low to Critical.
 - While approaches vary, many organizations prioritize addressing High and Critical vulnerabilities, investing fewer resources to those classified as Low or Medium. This strategy allows them to focus on the most pressing security issues first, balancing risk management with resource constraints.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/Ch3YfKA.png">
<br />
<br />
<br />
<br />





 - Let's take a look at the medium-level vulnerability found on our VM. For example, "SMB Signing not required" 
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/miNpVBB.png">
<br />
<br />
<br />
<br />



 - We can see the description of this particular vulnerability. In this case, our VM's SMB server doesn't require message signing, which can allow attackers to perform man-in-the-middle attacks against the server.
 - We also see the recommended remediation solution, enabling mandatory message signing in the server's configuration.
 - Additionally we see Nessus plugin codes on the top-right, and the CVSS (Common Vulnerabilities Scoring System) on the bottom-right corner.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/HCbSlOL.png">
<br />
<br />
<br />
<br />



 - If plugins are tagged as "info," it means they are not necessarily vulnerabilities but something we should be aware of.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/rqJTSsh.png">
<br />
<br />
<br />
<br />




 - As we can see from the below detail, we’ve only performed basic scanning without providing any credentials. The next thing we are going to do is set up the VM to accept authenticated scans and also provide credentials to Nessus.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/1mxb5rN.png">
<br />
<br />
<br />
<br />


---

[back to top](#toc)
## Configuring Windows 10 VM for Authenticated Scanning

<br />
<br />

 - Run "services.msc"
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/1SoB6js.png">
<br />
<br />
<br />
<br />



 - Our first step is to enable the Remote Registry service. This allows the scanner to connect to the VM's registry and examine it for insecure configurations.
 - To do this, locate the Remote Registry service in the Services list. Then, change its [Startup type] to [Automatic] and start the service.
 - Click [Start] > [OK]
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/L11u71y.png">
<br />
<br />
<br />
<br />



 - Next, we will go to [Advanced sharing settings] > [Private] > [Guest or Public] and enable all the options.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/TtH5aRF.png">
<br />
<br />
<br />
<br />



 - Go to UAC (User Account Control) Setting. Disable the User Account Control like below:
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/Bf24G3P.png">
<br />
<br />
<br />
<br />






 - Open the Registry Editor by typing "regedit" in the Start menu and running it as an administrator. We're going to add a key that will further reduce User Account Control (UAC) restrictions for remote connections to the VM.

<br />
Navigate to this path in the registry: 
<br />

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
```

<br />

<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/3tpmMaG.png">
<br />
<br />

Once there, right-click in the right pane, select New > DWORD (32-bit).

<br />
<br />
<br />
<br />


 - Name it "LocalAccountTokenFilterPolicy". Double-click the new entry and set its value to 1.
 - This change allows the remote account to connect to the VM with fewer UAC limitations, facilitating our vulnerability scan.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/pGKYRAF.png">
<br />
<br />
<br />
<br />


 - Reboot the VM.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/ZnDUd2h.png">
<br />
<br />
<br />
<br />


---

[back to top](#toc)
## Authenticated Scan Settings

<br />
<br />

 - Now, we are ready to perform a credential scan. Go back to the Nessus Browser App. We will modify the existing scan configuration.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/C5eZmbn.png">
<br />
<br />
<br />
<br />






 - Go to [Credentials] and provide the Windows 10 VM admin credentials. Click [Save]
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/VbmyHtq.png">
<br />
<br />
<br />
<br />


---

[back to top](#toc)
## Performing an Authenticated Scan

<br />
<br />

 - Now that we've made these changes, let's run the scanner again. With credentialed scanning enabled, we should expect to see more comprehensive results this time. The scanner will have deeper access to the system, allowing it to uncover vulnerabilities that weren't visible in our initial, unauthenticated scan.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/rdtQisg.png">
<br />
<br />
<br />
<br />


 - Our credentialed scan has uncovered significantly more vulnerabilities than our initial unauthenticated scan. 
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/7vj1yji.png">
<br />
<br />
<br />
<br />



 - Let's compare the results to the initial scan results:
 - **#1** (Initial, unauthenticated scan): *1 medium, 1 low vulnerability*
 - **#2** (Credentialed scan): *33 critical, 125 high, 19 medium, 1 low vulnerability*


<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/K2zZpn8.png">
<br />
<br />
<br />
<br />



 - Let's examine the discovered vulnerabilities. The top finding shows 110 instances of Microsoft Edge-related issues.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/xNrvNRR.png">
<br />
<br />
<br />
<br />


 - Under [Remediations], Nessus provides recommended actions to address the discovered vulnerabilities. Most suggestions involve applying Windows Updates to patch security flaws.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/YiAQm0w.png">
<br />
<br />
<br />
<br />


---

[back to top](#toc)
## Installing Deprecated Software


<br />
<br />

 - Let's try installing some deprecated software on this VM to make it more vulnerable. We are going to install Firefox 3.6, which was released on January 21, 2010.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/eybNgdX.png">
<br />
<br />
<br />
<br />


 - Install the deprecated firefox.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/pdZNX9m.png">
<br />
<br />
<br />
<br />


 - Let's run the Nessus credentialed scan again.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/lJwNuFX.png">
<br />
<br />
<br />
<br />


 - This high number of vulnerabilities highlights the significant security risk posed by outdated software in your system.
<p align="center">
<br/>
<img width="700" alt="Portfolio" src="https://i.imgur.com/8nhv0vq.png">
<br />







<p align="center">
<br/>
<img width="640" alt="Portfolio" src="https://i.imgur.com/bQcuQo0.png">
<br />
<br />
<br />
<br />

---

[back to top](#toc)
## Windows XP VM Installation and Configuration

Now, let's take our exploration a step further. We're going to examine the results of scanning an even more outdated system: **Windows XP.** This operating system, which Microsoft stopped supporting in 2014, is notoriously vulnerable. By scanning it with the Nessus vulnerability scanner, we'll see just how severe the security risks can become when using extremely outdated software.

<br />
<br />
<br />

 - For the Windows XP OS setup, you can use the default settings throughout the installation process. We won't cover this in detail as it's straightforward.
<p align="center">
<br/>
<img width="420" alt="Portfolio" src="https://i.imgur.com/z4Mxjk6.png[">
<br />


<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/Hln2uD5.png">
<br />


<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/1QyzmLd.png">
<br />


<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/yEff7b6.png">
<br />



<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/pnmXMQf.png">
<br />
<br />
<br />
<br />



 - Check the IP address of the Windows XP VM so we can use it for scanning.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/jpg3uf6.png">
<br />
<br />
<br />
<br />


---

[back to top](#toc)
## Configuring Windows XP VM for Authenticated Scanning


<br />
<br />

 - turn off the firewall
<p align="center">
<br/>
<img width="450" alt="Portfolio" src="https://i.imgur.com/sMimpc4.png">
<br />
<br />
<br />
<br />

 - right-click on [My Computer] and select [Properties]
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/HxsrrBp.png">
<br />
<br />
<br />
<br />

 - Check [Allow users to connect remotely to this computer]
<p align="center">
<br/>
<img width="450" alt="Portfolio" src="https://i.imgur.com/Xt5n4nj.png[">
<br />
<br />
<br />
<br />


 - Go to [Control Panel] > [Administrative Tools]
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/XjbVnux.png">
<br />
<br />
<br />
<br />


 - Open [Local Security Policy]
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/7YDJTi3.png">
<br />
<br />
<br />
<br />


 - Navigate to [Security Settings] > [Local Policies] > [Security Options] > [Network access: Sharking and security model for local accounts]. Ensure it has enabled the [Classic- local users authenticate as themselves...] option.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/Tw87Zyd.png">
<br />
<br />
<br />
<br />

 - Open the [Registry Editor]. Just like what we did in Windows 10 VM, go to the following registry path:

<br />

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
```

<br />


<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/U5pi4sd.png">
<br />

Once there, right-click in the right pane, select New > DWORD (32-bit), and name it "LocalAccountTokenFilterPolicy." Double-click the new entry and set its value to 1.


---

[back to top](#toc)
## Performing an Authenticated Scan on Windows XP Professional



 - Let's initiate the scan! If you encounter any errors, you may need to perform additional configuration steps on the XP VM to enable authenticated scanning. For detailed instructions, consult Nessus' official documentation.
<p align="center">
<br/>
<img width="380" alt="Portfolio" src="https://i.imgur.com/I8KLhYR.png">
<br />
<br />
<br />
<br />


 - The results of the scanning are quite interesting. As expected, we've found significantly more vulnerabilities compared to our Windows 10 VM with the outdated Firefox installation. However, the number of vulnerabilities is lower than one might anticipate for such an old operating system.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/hOFLtm1.png">
<br />


<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/I65wvms.png">
<br />

Interestingly, older systems like Windows XP may be less attractive targets for threat actors, as their user base has dwindled significantly. This reduced attention can result in fewer newly discovered vulnerabilities.

<br />

However, this doesn't make Windows XP safe to use – it still poses substantial security risks due to its lack of updates and modern security features.

<br />

It's worth noting a related real-world example: Southwest Airlines reportedly avoided a major CrowdStrike-Microsoft outage because some of their systems were still running Windows 3.1

<br />

Now, let's return to our Windows 10 VM and remediate its vulnerabilities by following Nessus's recommended solution.

<br />
<br />
<br />
<br />

---

[back to top](#toc)
## Windows 10 VM Remediation


 - Now let's address the vulnerabilities on our Windows 10 VM. We'll focus on three key remediation steps:
     - Completely uninstall the outdated Firefox browser
     - Update Microsoft Edge to its latest version
     - Perform comprehensive Windows Updates

<br />
<br />
<br />

 - Run "appwiz.cpl". Uninstall the Firefox browser.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/49evlfV.png">
<br />
<br />
<br />
<br />



 - Go to Microsoft Edge Settings via Browser. Select [About Microsoft Edge] > [Update]
<p align="center">
<br/>
<img width="450" alt="Portfolio" src="https://i.imgur.com/55hsfg9.png">
<br />
<br />
<br />
<br />




 - Navigate to [Settings] > [Update & Security], then click on [Windows Update]. Start the update process. This may take time to complete.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/tYqTsTj.png">
<br />
<br />
<br />
<br />

---

[back to top](#toc)
## Credentialed Scan after Remediation


<br />
<br />

 - Let's perform a credentialed scan again with Nessus.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/BSzJyo1.png">
<br />
<br />
<br />
<br />


 - You can see the vulnerabilities have shrunk down significantly.
<p align="center">
<br/>
<img width="670" alt="Portfolio" src="https://i.imgur.com/f9CIiw8.png">
<br />
<br />
<br />
<br />



 - To summarize our findings, I've compiled a comparison of all our scan results in the image below:
<p align="center">
<br/>
<img width="650" alt="Portfolio" src="https://i.imgur.com/L29Hzua.png">
<br />
<br />
<br />
<br />




\<end\>

[back to top](#toc)

<br />
<br />
<br />

