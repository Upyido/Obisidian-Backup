Question 4Incorrect

What type of cloud model would allow the sharing of resources by multiple organizations to create a service that benefits all of its members?

Private Cloud

Your answer is incorrect

Hybrid Cloud

Correct answer

Community Cloud

Public Cloud

Overall explanation

OBJ-4.1: A community cloud in computing is a collaborative effort in which infrastructure is shared between several organizations from a specific community with common concerns, whether managed internally or by a third party and hosted internally or externally. Community Cloud is a hybrid form of private cloud. They are multi-tenant platforms that enable different organizations to work on a shared platform. Community Cloud may be hosted in a data center, owned by one of the tenants, or by a third-party cloud services provider and can be either on-site or off-site. A public cloud contains services offered by third-party providers over the public Internet and is available to anyone who wants to use or purchase them. They may be free or sold on-demand, allowing customers to pay only per usage for the CPU cycles, storage, or bandwidth they consume. A private cloud contains services offered either over the Internet or a private internal network and only to select users instead of the general public. A hybrid cloud is a cloud computing environment that uses a mix of on-premises, private cloud, and third-party public cloud services with orchestration between these platforms. This typically involves a connection from an on-premises data center to a public cloud.

Domain

4 - Virtualization and Cloud Computing

Question 16Incorrect

You work as a computer technician for a production company that travels worldwide while filming and editing music videos. Due to the nature of video editing, you will be building a video production workstation for the company that will have the maximum amount of RAM, an 8-core CPU, a dedicated GPU, and a redundant array of solid-state devices for storage. You are now determining which power supply to install in the system. What is the MOST important characteristic to consider when choosing a power supply?

Correct answer

Input voltage

Amperage of 12V rail

Your answer is incorrect

Number of SATA connectors

Efficiency rating

Overall explanation

OBJ-3.5: This question provides you with many details, but the key phrase in finding the answer is in the first sentence. This computer will be traveling worldwide, and the most important consideration will be the input voltage. If you choose a 120-volt power supply, it would be destroyed if plugged into a 240-volt outlet (commonly used outside the United States). Conversely, if you use a 240-volt power supply and plug it into a 120-volt outlet, it will not function due to the lower voltage. Therefore, you need to pick a power supply with dual voltage selection capability for maximum compatibility worldwide.

Domain

3 - Hardware

Question 18Incorrect

During a disaster recovery, which of the following statements is true?

Correct answer

A virtual machine has less downtime than a physical server

Your answer is incorrect

A virtual machine cannot be used for redundancy or load balancing

Both a virtual machine and a physical server has the same downtime

A virtual machine has more downtime than a physical server

Overall explanation

OBJ-4.1: A virtual machine can usually be restored much faster than a physical server. Physical servers must be modified to fit the right drivers for the disk drives, NIC, and other necessary components whenever they must be rebuilt after a crash. Often, a new physical server will also be required to replace a faulty one, and then the right drivers are needed to ensure a smooth transition. Conversely, a virtual machine can be recreated using another instance, clone, or restoration from a backup in much less time. Therefore, the downtime associated with virtual machines and their restoral is much lower.

Domain

4 - Virtualization and Cloud Computing

Question 30Incorrect

You are configuring a new client workstation on the network. Which type of IP address should you configure it with?

Your answer is incorrect

Static

Correct answer

Dynamic

Link-local

APIPA

Overall explanation

OBJ-2.5: A dynamic IP address should be used for client workstations and devices to ensure they are easy to configure and less prone to human error. When configuring a dynamic IP address, the DHCP server should issue the IP address, subnet mask, gateway, and DNS server's IP address to the workstation or device. A static IP address should be used for servers to ensure they are easy to find, access, and manage on the network. When configuring a static IP address, you need to include the IP address, subnet mask, gateway, and DNS server's IP address. A static IP address is used when the DHCP server is disabled and clients are configured manually to join the network properly. Automatic Private IP Addressing (APIPA) is a feature of Windows-based operating systems that enables a computer to automatically assign itself an IP address when there is no Dynamic Host Configuration Protocol (DHCP) server available to perform that function. When a host uses an APIPA address, it can communicate with other hosts on the same network using APIPA. Still, it cannot reach other networks or communicate with hosts who have managed to obtain a valid DHCP lease. An APIPA address is also known as a link-local address.

Domain

2 - Networking

Question 33Incorrect

You are connecting a laptop to a brand new digital high definition TV. Unfortunately, the laptop is a little outdated and only has an analog display output. Which of the following adapters could you use to convert the signal from analog to digital for use with the new television?

S-Video to RCA

Your answer is incorrect

HDMI to VGA

Correct answer

VGA to DVI-D

DVI-D to HDMI

Overall explanation

OBJ-3.1: Since this question asks you to select the converter that can convert a signal from analog to digital, you need to consider which of the connectors are analog and digital. S-Video, RCA, and VGA are all analog. HDMI and DVI-D are both digital. Therefore, the correct answer is VGA (analog) to DVI-D (Digital). HDMI to VGS would be digital to analog. S-Video to RCA would be analog to analog. DVI-D to HDMI would be digital to digital.

Domain

3 - Hardware

Question 37Incorrect

What type of connector provides power to an internal hard drive from the computer's power supply using a 4-pin connector?

Correct answer

Molex

Your answer is incorrect

SATA

Thunderbolt

SCSI

Overall explanation

OBJ-3.1: A Molex connector provides DC power to the various drives inside a computer case. Molex and Mini-Molex are both 4-pins connectors, with Mini-Molex only being used to support floppy disk drives. The large-sized one is used for hard disk drives, CD-ROM drives, and DVD drives. SATA connectors have 15 pin and 7 pin varieties. Thunderbolt has 20 and 24 pin varieties. SCSI has 50 and 36 pin varieties.

Domain

3 - Hardware

Question 41Incorrect

Which of the following is the MOST dangerous type of threat when using virtualization?

Your answer is incorrect

Virtual NIC duplication

Correct answer

VM escape

VM sprawl

Rogue VM

Overall explanation

OBJ-4.2: VM escape refers to malware running on a guest OS jumping to another guest or the host. As with any other software type, it is vital to keep the hypervisor code up-to-date with patches for critical vulnerabilities. VM escape is the biggest threat to virtualized systems. A virtual network interface card (vNIC) represents the configuration of a VM connected to a network. A VM can be configured to have multiple vNICs. A rogue VM is one that has been installed without authorization. VM sprawl is the uncontrolled deployment of more and more VMs.

Domain

4 - Virtualization and Cloud Computing

Question 47Incorrect

Which of the following is a security concern with using a cloud service provider and could result in a data breach caused by data remnants?

Metered services

Correct answer

Rapid elasticity

Your answer is incorrect

Resource Pooling

On-Demand

Overall explanation

OBJ-4.1: Rapid elasticity can be a security threat to your organization's data due to data remanences. Data remanence is the residual representation of digital data that remains even after attempts have been made to remove or erase it. So, when a cloud resource is deprovisioned and returned to the cloud service provider, it can be issued to another organization for use. If the data was not properly erased from the underlying storage, it could be exposed to the other organization. For this reason, all cloud-based storage drives should be encrypted by default to prevent data remanence from being read by others. Metered services are pre-paid, a-la-carte, pay-per-use, or committed offerings. A metered service like a database may charge its users based on the actual usage of the service resources on an hourly or monthly basis. For example, Dion Training used the AWS Lambda serverless product in some of our automation. This service charges us $0.20 for every 1 million requests processed. Resource pooling refers to the concept that allows a virtual environment to allocate memory and processing capacity for a VMs use. On-demand refers to the fact that a consumer can unilaterally provision computing capabilities, such as server time and network storage, as needed automatically without requiring human interaction with each service provider.

Domain

4 - Virtualization and Cloud Computing

Question 51Incorrect

The touch screen on your Windows 10 laptop is not working properly. You have been asked to troubleshoot the laptop. What should you check FIRST?

Performance monitor

Device manager

Your answer is incorrect

System configuration

Correct answer

Digitizer settings

Overall explanation

OBJ-5.5: Most laptops have a digitizer and an LCD screen if they are touchscreen devices. The digitizer is a piece of glass glued to the LCD's surface and is used to capture your touches and translate them into input for your system. If the touch screen is not working, but the display doesn't look cracked or broken, this is often a sign that the digitizer settings are incorrect or the digitizer is defective.

Domain

5 - Hardware and Network Troubleshooting

Question 53Incorrect

Your company has recently migrated much of your data center to the cloud. Now, your boss needs a method to monitor all services used in supporting your customers to be properly billed based on their usage. Which of the following cloud computing concepts is your boss describing?

Rapid elasticity

Correct answer

Measured services

On-demand

Your answer is incorrect

Resource pooling

Overall explanation

OBJ-4.1: Measured service is a term that IT professionals apply to cloud computing that references services where the cloud provider measures or monitors the provision of services for various reasons, including billing, effective use of resources, or overall predictive planning. Rapid elasticity is used to describe scalable provisioning or the capability to provide scalable cloud computing services. Rapid elasticity is very critical to meet the fluctuating demands of cloud users. The downside of rapid elasticity implementations is that they can cause significant loading of the system due to the high resource number of allocation and deallocation requests. On-demand refers to the fact that a consumer can unilaterally provision computing capabilities, such as server time and network storage, as needed automatically without requiring human interaction with each service provider. Resource pooling refers to the concept that allows a virtual environment to allocate memory and processing capacity for a VMs use.

Domain

4 - Virtualization and Cloud Computing

Question 65Incorrect

You have been asked to set up the corporate email on several mobile devices for Dion Training's employees. The employees will use their mobile devices to send their emails when out of the office. Which of the following mail protocols should you configure to allow the employees to send their mail?

Correct answer

SMTP

POP3

HTTPS

Your answer is incorrect

IMAP

Overall explanation

OBJ-1.4: You should configure SMTP since it is the only protocol used to send emails. POP3 and IMAP are used to receive emails. HTTPS is used for web browsing, not for receiving emails. The post office protocol (POP3) is a TCP/IP application protocol providing a means for a client to access email messages stored in a mailbox on a remote server over port 110. The server usually deletes messages once the client has downloaded them. The internet message access protocol (IMAP) is a TCP/IP application protocol that provides a means for a client to access email messages stored in a mailbox on a remote server using TCP port number 143. Unlike POP3, messages persist on the server after the client has downloaded them. IMAP also supports mailbox management functions, such as creating subfolders and access to the same mailbox by more than one client at the same time. The simple mail transfer protocol (SMTP) is the protocol used to send mail between hosts on the Internet using TCP port 25. The hypertext transfer protocol secure (HTTPS) is a secure protocol used to provide web content to browsers using SSL/TLS encryption over port 443.

Domain

1 - Mobile Devices

Question 67Incorrect

You are troubleshooting a workstation for a customer. The workstation will not boot. When it is powered on, an error message of "OS not found" is displayed on the screen. What is the MOST likely solution to fix this error?

Replace the HDD with an SSD

Correct answer

Repair the GPT

Perform a chkdsk

Your answer is incorrect

Repartition the drive

Overall explanation

OBJ-5.3: The "OS not found" error at boot time is an indication that the MBR (Master Boot Record) or GPT (Globally Unique ID Partition Table) is corrupted or faulty. If this occurs, you should reboot into the Windows recovery mode and use the 'bootrec /fixboot' command to fix the GPT.

Domain

5 - Hardware and Network Troubleshooting

Question 69Incorrect

(This is a simulated PBQ. If you had this question on the real exam, you would be asked to drag-and-drop a label with the component’s name on top of the appropriate cable's connector.)  

![](https://img-c.udemycdn.com/redactor/raw/quiz_question/2022-01-18_17-35-33-5c30d1b952a963abca46534c71850475.png)

Using the image above, which of the following correctly identifies the fiber optic connector shown as Connector C?

F

Your answer is incorrect

ST

Correct answer

LC

SC

Overall explanation

OBJ-3.1: This is an LC connector. A ST, SC, LC, or MTRJ connector is used to terminate a fiber optic cable. An LC, or Lucent connector, is a small form factor connector that combines the transmit and receive cables into a single square, snap-in connector. The F-type connector is used with coaxial cables, not fiber optic cables. An SC, or subscriber connector, is a general-purpose push/pull style connector that has a square, snap-in connector that latches with a simple push-pull motion. SC connectors are widely used in single-mode fiber optic systems. An ST, or straight tip, connector is a quick-release bayonet-style connector that has a long cylindrical connector.

Domain

3 - Hardware

Question 76Incorrect

Tom is running some new Cat 5e cabling in an office building to connect a few offices. The ceiling is constructed as a drop ceiling with fluorescent lights and does not have any cable trays. Due to the proximity of the fluorescent lights to the cable being run, what type of CAT 5e cable should be run?

Correct answer

STP

Coaxial

Fiber

Your answer is incorrect

UTP

Overall explanation

OBJ-5.7: STP (Shielded Twisted Pair) is a type of cabling that can help prevent electrical interferences or cross-talk. A cross-talk is when electrical interference data passing through can cause CRC (Cyclic Redundancy Check) errors. A CRC is used to calculate the before and after checksum is made when transferring data. If electrical interference gets in the way, such as proximity to fluorescent light bulbs, it can cause data to be corrupted and produce an error. UTP (Unshielded Twisted Pair) is cheaper and easier to work with but is subject to interference. Coaxial and fiber are not types of CAT 5e cabling. Coaxial and fiber are not Cat 5E cable types and cannot be used for this network.

Domain

5 - Hardware and Network Troubleshooting

Question 81Incorrect

A customer contacts the service desk because their laptop will not power on when plugged in, and the battery is dead. The service desk replaces its battery, connects it to a different power adapter, and the laptop works all day until the battery runs out. Now, the laptop won't turn on, and the battery won't charge. Which of the following do you recommend to solve this issue?

Replace the power adapter

Connect the laptop to a 220v outlet

Your answer is incorrect

Replace the battery

Correct answer

Replace the DC jack

Overall explanation

OBJ-5.5: This scenario indicates that the DC jack is faulty. Since the battery was replaced and the laptop continues to work, this indicates it isn't a battery issue but is, instead, most likely a DC jack issue. The DC jack often gets broken on a laptop, and if the jack is broken, the device cannot charge or receive power from the power adapter or wall outlet.

Domain

5 - Hardware and Network Troubleshooting

Question 83Incorrect

**You are troubleshooting a computer that won't display any output on the screen. First, you powered the computer off and on again, noting that the fans were spinning, but there was still no display output. You confirmed that the monitor and video cable were working by testing them with another computer. Next, you re-seated the PCIe x16 video card and tried a different video card, but the issue persisted. You checked all power connections inside the case to ensure they were secure. Finally, you tested the computer with minimal components (motherboard, processor, one stick of RAM, and power supply), but there was still no display and no POST beep codes. Given the steps taken, what is the MOST likely cause of the issue?**

**The power supply's voltage switch is set to 240V but the power outlet is providing 110V**

Correct answer

**The power supply wattage is too low for the components in the computer**

**The CMOS battery needs to be replaced**

Your answer is incorrect

**The motherboard has failed and needs to be replaced**

Overall explanation

OBJ-5.2: If the power supply does not provide enough power, the system may turn on partially (fans spinning) but not fully power the components needed to display output or perform a POST (Power-On Self-Test), therefore no beep codes would be present. A motherboard failure is still possible; however, it would most likely cause a POST beep code if the other components are functioning properly. This is less likely because the fans spinning indicate that the motherboard is receiving at least some power as they use low wattage, with the additional findings suggesting a power supply issue. If the power supply's voltage switch is set incorrectly (e.g., to 240V while the power outlet provides 110V), the computer components would likely not turn on at all (no fans spinning), or the power supply would immediately fail. A dead CMOS battery can cause BIOS settings to reset, but it typically does not prevent the computer from displaying output or performing a POST. The computer should still boot with default BIOS settings.

Domain

5 - Hardware and Network Troubleshooting

Question 87Incorrect

(This is a simulated PBQ. If you had this question on the real exam, you would be asked to drag-and-drop a label with the component’s name on top of the appropriate cable's connector.)  

![](https://img-c.udemycdn.com/redactor/raw/quiz_question/2022-01-18_17-33-01-f2d629388e74d2cb4bdf3c40293d2760.png)

Using the image above, which of the following correctly identifies the fiber optic connector shown as Connector B?

Your answer is incorrect

LC

Correct answer

ST

F

SC

Overall explanation

OBJ-3.1: This is an ST connector. A ST, SC, LC, or MTRJ connector is used to terminate a fiber optic cable. An ST, or straight tip, connector is a quick-release bayonet-style connector that has a long cylindrical connector. An SC, or subscriber connector, is a general-purpose push/pull style connector that has a square, snap-in connector that latches with a simple push-pull motion. SC connectors are widely used in single-mode fiber optic systems. An LC, or Lucent connector, is a small form factor connector that combines the transmit and receive cables into a single square, snap-in connector. The F-type connector is used with coaxial cables, not fiber optic cables.

Domain

3 - Hardware

Question 88Incorrect

A computer technician is building a server that will run multiple virtual machines simultaneously. Which CPU technology should be selected so that the processor can utilize two logical cores?

32-bit CPU

Dedicated GPU

Correct answer

Hyperthreading

Your answer is incorrect

Multi-core processor

Overall explanation

OBJ-3.4: HyperThreading (HT) is an Intel CPU architecture implemented to expose two or more logical processors to the OS to deliver performance benefits. This allows the system to run multiple cores for each operating system in a virtualized environment. Since the question asked about logical cores and not physical cores, the answer is hyperthreading and not a multi-core processor. A 32-bit CPU is a hardware item and used by low-end notebooks or thin clients. A dedicated GPU is a graphics card and would not help with running multiple virtual machines.

Domain

3 - Hardware

Question 90Incorrect

(This is a simulated PBQ. If you had this question on the real exam, you would be asked to drag-and-drop a label with the component's name onto the proper location on the motherboard.)  

![](https://img-c.udemycdn.com/redactor/raw/quiz_question/2022-01-18_17-37-55-c0057c7bb147c1b44d6b97376d6c138e.png)

Using the image of the motherboard above, which of the following correctly indicates the circled area?

PCI

Correct answer

PCIe x1

Your answer is incorrect

PCIe x4

AGP

Overall explanation

OBJ-3.4: The area circled indicates the PCIe x1 slots. PCIe (peripheral component interconnect express) is an interface standard for connecting high-speed components. Every desktop PC motherboard has some PCIe slots you can use to add GPUs (video cards or graphics cards), RAID cards, network adapters, Wi-Fi cards, or SSD (solid-state drive) add-on cards. The types of PCIe slots available in your PC will depend on your motherboard and are designated as PCIe x1, x4, x8, and x16. PCIe x1 slots are usually used for external input/output devices such as network interface cards. For the exam, it is important that you can identify the different parts of the motherboard by sight.

Domain

3 - Hardware