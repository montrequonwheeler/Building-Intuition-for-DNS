</p>

<h1>Building Intuition for DNS</h1>
This walkthrough focuses on Building Intuition for DNS after the install configuration of Microsoft Active Directory Domain Services.
<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop (Microsoft Remote Access in the App Store for MAC users)
- Active Directory Domain Services

<h2>Operating Systems Used</h2>

- Windows Server 2022</b> (21H2)
- Windows 10</b> (21H2)

<h2>Setup Resources in Azure</h2>

- Create the Domain Controller VM (Windows Server 2022) named “DC-1”
- Take note of the Resource Group and Virtual Network (Vnet) that get created at this time

<h2>A-Record Exercise</h2>

- Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
- Connect/log into Client-1 as an admin (mydomain\jane_admin)
- From Client-1 try to ping “mainframe” notice that it fails
- Nslookup “mainframe” notice that it fails (no DNS record)
- Create a DNS A-record on DC-1 for “mainframe” and have it point to DC-1’s Private IP address
- Go back to Client-1 and try to ping it. Observe that it works
<img width="1439" alt="DNS 1" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/082887f7-f984-4bc5-8217-8de4d5dbe5dd">
<img width="1439" alt="DNS 2" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/dcfc5a57-abbf-44a1-8ae5-a0f7bd75c8d3">
<img width="1439" alt="DNS 4" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/753e8aa7-a7de-42b7-b60f-55d0fe318429">
<img width="1439" alt="DNS 5" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/71d73972-165a-4441-a485-bd08bfdebdf4">
<img width="1439" alt="DNS 6" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/4e9cf3b3-60fa-42c7-bca2-8c228bd88e2f">
<img width="1439" alt="DNS 7" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/a84c62e7-9a4c-46de-b0ca-4d0c89a5e807">
<img width="1439" alt="DNS 8" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/59dcdf6d-8198-43e4-bed7-8d56f7e7619f">
<img width="1439" alt="DNS 9" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/ae0ebce4-d626-4e23-ac4b-798a7b319e01">
<img width="1439" alt="DNS 10" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/ab0e6a19-7c21-4a19-880a-35beec56f768">

<h2>Local DNS Cache Exercise</h2>

- Go back to DC-1 and change mainframe’s record address to 8.8.8.8
- Go back to Client-1 and ping “mainframe” again. Observe that it still pings the old address
- Observe the local dns cache (ipconfig /displaydns)
- Flush the DNS cache (ipconfig /flushdns). Observe that the cache is empty
- Attempt to ping “mainframe” again. Observe the address of the new record is showing up
<img width="1439" alt="DNS 11" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/5db85a8f-b7b3-4515-a10d-94c7c1d381b5">
<img width="1439" alt="DNS 12" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/55f28897-09df-4411-86cc-68e842204688">
<img width="1439" alt="DNS 13" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/7922c544-cacc-485c-b9c6-7b51e50242cc">

- Make sure to run the command as an administrator in order to flush the dns

<img width="1439" alt="DNS 14" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/1dc40c14-0141-48c2-8dac-f6bae1eb6454">

<h2>CNAME Record Exercise</h2>

- Go back to DC-1 and create a CNAME record that points the host “search” to “www.google.com”
- Go back to Client-1 and attempt to ping “search”, observe the results of the CNAME record
- On Client-1, nslookup “search”, observe the results of the CNAME record
<img width="1439" alt="DNS 15" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/8a792901-69f4-4aa2-8956-44673a82aec2">
<img width="1439" alt="DNS 16" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/e5fee6d3-5f1c-4bcc-a8cf-f52c1a4eeb67">
<img width="1439" alt="DNS 17" src="https://github.com/montrequonwheeler/building-intuition-for-dns/assets/127397594/504ee27d-2955-4bb5-a624-a8f02380272d">

- Afterwards remember to delete all resource groups to avoid ongoing costs
