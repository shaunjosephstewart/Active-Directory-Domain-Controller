## Active Directory - Domain-Controller
Working with Active Directory in Windows Server 2022

Description
In this lab I download and configure a Windows server 2022 instance in Oracle VirtualBox. I deploy the server as a domain controller and configure services such as Ras, Nat, and DHCP. I create a user, set it as an admin account and connect to the domain controller.

Step 1: Download Windows Server 2022 ISO File from Microsoft.

Windows Server File



Step 2: Setting up two network adapters on this Windows Server instance. The first will be for NAT and internet access. The second will be set to internal network so that our client machine can connect to it. Client machine adapter is set only to internal network.

First Interface Server Second Interface Server



These are the two network adapters in the server. The first one is connected to the internet and recieved a DHCP lease from my gateway. We gave the second one a private IPv4 address of 172.16.0.1 with a subnet mask of 255.255.255.0. Later we will set up DHCP scope so it can serve as gateway and lease out IP addresses within a certain range.

Internet Interface APIPA Interface



Step 3: Adding features for DHCP, Remote Access, AD Domain Services, and Routing Services.

DHCP, Remote Access, AD Domain Services Routing Services and RAS



Step 4: Deploying this server as a domain controller "jakesdomain.com"

First Interface Server



Step 5: Setting up RAS / NAT tools. Routing/remote access —> right click DC local —> configure RAS. Setting up NAT to allow internal clients to connect to the internet using one public IP address. The NIC Selected for NAT is the "Internet" one so we can access the internet.

NAT NAT2 Internet Selected



Step 6: Setting up DHCP. Tools --> DHCP

First Interface Server



Step 7: Setting up DHCP. Select your domain --> IPv4 --> New Scope

First Interface Server



Step 8: Setting up DHCP. Naming our scope the range that it will be.

First Interface Server



Step 9: Setting up DHCP scope and making it a /24 subnet with a mask of 255.255.255.0. This allows for 253 usable IP addresses but we will only have a range of 101 in our scope. We are not going to exclude any addresses so we skip this part.

First Interface Server First Interface Server



Step 10: Setting up the default gateway, the router that will be used by our clients. We set this to our "Internal" IP address of 172.16.0.1 that we created earlier. After this step we did not set up a WINS server.

First Interface Server



Step 11: Right click our domain and click "authorize", right click IPv4 and click "refresh". Now it should be working. One can see the scope and leased out IP addressses.

First Interface Server



Step 12: Now we'll create a user account that I can log into this domain with. Click tools --> Active Directory Users and computers --> Right click jakesdomain --> New --> User.

First Interface Server First Interface Server



Step 13: Changing this account to an admin account! Right click on name --> Properties --> Member of.

First Interface Server
