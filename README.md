<p align="center">
  <img src="https://github.com/user-attachments/assets/c48e28da-9e3d-43b2-a283-e9725bb26c08" width="150" height="auto">
  <h1 align="center">Create and Configure Secure Storage Accounts</h1>
</p>

#### *In this tutorial, we will:*
*•	Create a storage account, disable public access, and set lifecycle rules.*

*•	Create a blob container, upload a file, and configure access.*

*•	Create a file share, upload a file, and restrict network access.*

#### Tasks:
 1. Set up and configure a storage account.
 2. Implement and secure Blob storage.
 3. Configure and secure Azure File Storage.

## Task 1: Set up and configure a storage account.

Set up a storage account with geo-redundant storage and restricted public access to ensure data durability and security.

1.	In the Azure portal, search for and select "Storage accounts".
2.	Click "+ Create".
3.	On the "Basics" tab of the "Create a storage account" blade, configure:
    -  Subscription: Select your subscription.
    -  Resource group: Choose or create a resource group.
    -  Storage account name: Enter a unique name (e.g., "storagemgmt").
    -  Region: Select your preferred region (e.g., "(US) East US").
    -  Performance: Choose "Standard" (suitable for most applications).
    -  Redundancy: Select "Geo-redundant storage (GRS)" for data replication across regions.
    -  Make read access to data in the event of regional unavailability: Check this box (enables read access from a secondary region if the primary fails).

<p align="center">
<img src="https://github.com/user-attachments/assets/9abfa090-532c-418e-9578-2d8095b1a657">
</p>

4.	Click "Next: Networking >".
5.	On the "Networking" tab, select "Disable public access and use private access" (blocks all public internet access for enhanced security).

<p align="center">
<img src="https://github.com/user-attachments/assets/84cca693-8376-4e2d-9e95-8f6d9b39e4ef">
</p>

6.	Click "Review + Create". After validation completes, click "Create".
7.	Once the storage account is deployed, click "Go to resource".
8.	In the "Security + Networking" section, select "Networking".
9.	Change "Public network access" to "Enabled from selected virtual networks and IP addresses".
10.	In the "Firewall" section, check "Add your client IP address", then click "Save".

<p align="center">
<img src="https://github.com/user-attachments/assets/6b1e6cb4-f303-4055-997e-fd37239503a4">
</p>

11.	In the "Data management" section, select "Lifecycle management".
12.	Click "Add a rule" and name it "changetocool", then click "Next".

<p align="center">
<img src="https://github.com/user-attachments/assets/1d971ee8-8ee2-4fd2-8e97-1201b6a00558">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/66550d54-12a8-4ba2-9619-d22e8c88c4ed">
</p>

13.	On the "Base blobs" tab, configure:
    -  Condition: "If base blobs were last modified more than 30 days ago".
    -  Action: "Move to cool storage" (a cost-effective tier for infrequently accessed data).
14.	Click "Add".

<p align="center">
<img src="https://github.com/user-attachments/assets/48ed250b-8925-47e5-b5e4-1323356d605f">
</p>

## Task 2: Implement and secure Blob storage.

Create a blob container (a directory-like structure for storing unstructured data) in the storage account, upload a file, and configure limited access.

1.	In the "Data storage" section of your storage account, click "Containers".
2.	Click "+ Container", name it "info", then click "Create".

<p align="center">
<img src="https://github.com/user-attachments/assets/e08e4329-1ee1-4493-a66b-08b48e7e1fc3">
</p>

3.	Select the "info" container, scroll to the ellipsis (...) on the right, and click "Access policy".

<p align="center">
<img src="https://github.com/user-attachments/assets/a5404ab1-f201-4cd2-a967-11b85cf0f039">
</p>

4.	In the "Immutable blob storage" area, click "Add policy" and configure:
    -  Policy type: "Time-based retention".
    -  Set retention period for: "1 day".
5.	Click "Save".

<p align="center">
<img src="https://github.com/user-attachments/assets/3922049f-694d-45f9-b9c5-6f8caea1d852">
</p>


<p align="center">
<img src="https://github.com/user-attachments/assets/dc0e5834-180f-48d0-b051-cca7879a3258">
</p>

6.	Return to the "Containers" page, select the "info" container, and click "Upload".
7.	On the "Upload blob" blade, expand the "Advanced" section and configure:
    -  Blob type: "Block blob" (suitable for most file uploads).
    -  Block size: "4 MiB".
    -  Access tier: "Hot" (optimized for frequent access).
    -  Upload to folder: "sectesting".
    -  Encryption scope: "Use existing default container scope".

<p align="center">
<img src="https://github.com/user-attachments/assets/24a379dd-e211-48da-b06c-5e7666311186">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/0beaad56-a915-4c38-9ec3-853a4bb38447">
</p>

8.	Select a sample text file (e.g., "sample.txt"), then click "Upload".
9.	Confirm the "sectesting" folder and your uploaded file appear.
10.	Select the uploaded file, copy its URL, and paste it into an InPrivate browsing window. (You should see an XML error like "ResourceNotFound" or "PublicAccessNotPermitted" since public access is disabled.)

<p align="center">
<img src="https://github.com/user-attachments/assets/c93c6105-7d82-4cf7-9049-ad27df089462">
</p>

11.	To configure limited access, select the uploaded file and click the "Generate SAS" tab.
12.	Configure the Shared Access Signature (SAS) settings:
    -  Signing key: "Key 1".
    -  Permissions: "Read".
    -  Start date: Set to yesterday’s date.
    -  Start time: Set to the current time.
    -  Expiry date: Set to tomorrow’s date.
    -  Expiry time: Set to the current time.
13.	Click "Generate SAS token and URL", then copy the "Blob SAS URL".
14.	Paste the SAS URL into an InPrivate browsing window. Verify you can view the file’s contents. (The SAS token temporarily grants read access.)

<p align="center">
<img src="https://github.com/user-attachments/assets/cb66ca48-da91-4f1f-b4f1-e3568e6b05eb">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/b9df08bd-9a95-4fa8-936e-a926e9843a5e">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/0a454ec1-b7bc-4c2f-9c0c-edeaee4ff223">
</p>

## Task 3: Configure and secure Azure File Storage.

Create an Azure file share (a managed file storage service) in the storage account, upload a file, and restrict network access using a virtual network.

1.  In the Azure portal, navigate back to your storage account, in the Data storage section, click File shares. Click "+ File share" and on the Basics tab give the file share the name, filesharetest.

1.	In your storage account, under the "Data storage" section, click "File shares".
2.	Click "+ File share".
3.	On the "Basics" tab, name the file share "filesharetest", then click "Review + create".

<p align="center">
<img src="https://github.com/user-attachments/assets/899ed12f-3c79-4e4e-acb9-2264b129289f">
</p>

4.	Click "Create" and wait for the file share to deploy.
5.	Return to your storage account and select "Storage browser".
6.	Click "File shares" and verify the "filesharetest" directory is present.

<p align="center">
<img src="https://github.com/user-attachments/assets/70cfba1d-4a9a-47a1-bdb7-8483d0d9145c">
</p>

7.	Select "filesharetest" and click "Upload".
8.	Browse to a file of your choice, then click "Upload".

<p align="center">
<img src="https://github.com/user-attachments/assets/2f46d2b8-62f3-4e11-b5ac-784eb8819549">
</p>

9.	To restrict network access, search for and select "Virtual networks" in the Azure portal.
10.	Click "+ Create".
11.	Configure the virtual network:
    -  Resource group: Select the same resource group as your storage account.
    -  Name: Enter "StorageVnet".
    -  Take defaults for other parameters.
12.	Click "Review + create", then click "Create".
13.	After deployment, click "Go to resource".

<p align="center">
<img src="https://github.com/user-attachments/assets/9340f0c9-7241-4bc8-92c6-6f83a7c85d21">
</p>

14.	In the "Settings" section, select "Service endpoints" and click "Add".
15.	Configure the service endpoint:
    -  Service: Select "Microsoft.Storage".
    -  Subnets: Check "default".
16.	Click "Add".

<p align="center">
<img src="https://github.com/user-attachments/assets/479a0cf1-cc55-4490-8b86-f84c830f0442">
</p>

17.	Return to your storage account and, in the "Security + networking" section, select "Networking".
18.	Under "Virtual networks", click "Add existing virtual network".
19.	Select "StorageVnet" and the "default" subnet, then click "Add".
20.	In the "Firewall" section, remove your client IP address (previously added in Task 1) so only traffic from "StorageVnet" is allowed, then click "Save".

<p align="center">
<img src="https://github.com/user-attachments/assets/827956b1-96a8-47df-9bf2-3bc64aa0ceb1">
</p>

21.	In "Storage browser", refresh the page and navigate to your file share or blob content. (You should see a "not authorized" message since you’re not connecting from the virtual network. This may take a few minutes to take effect.)

<p align="center">
<img src="https://github.com/user-attachments/assets/3b4e9d3d-cf03-48bc-a897-3083812e3c16">
</p>
