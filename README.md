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

In this task, we will set up and configure a storage account with geo-redundant storage and restricted public access.

1.  Search for and select Storage accounts, and then click "+ Create".
2.  On the Basics tab of the Create a storage account blade, specify Subscription, Resource group, Storage account name	(in this case storagemgmt), Region, Performance	(for most applications the standard tier is ok), Redundancy	and Make read access to data in the event of regional availability.

<p align="center">
<img src="https://github.com/user-attachments/assets/9abfa090-532c-418e-9578-2d8095b1a657">
</p>

3.  On the Networking tab select Disable public access and use private access (blocks all public internet access to the storage account ensuring enhanced security and preventing unauthorized exposure).

<p align="center">
<img src="https://github.com/user-attachments/assets/84cca693-8376-4e2d-9e95-8f6d9b39e4ef">
</p>

4.  Select "Review + Create", wait for the validation process to complete, and then click "Create". Once the storage account is deployed, select "Go to resource".
5.  In the "Security + Networking" section, select "Networking". Notice public network access is disabled.
6.  Change the public network access to "Enabled from selected virtual networks and IP addresses" and in the Firewall section, check the box for "Add your client IP address". Be sure to Save your changes.

<p align="center">
<img src="https://github.com/user-attachments/assets/6b1e6cb4-f303-4055-997e-fd37239503a4">
</p>

7.  In the "Data management" section, select "Lifecycle management", and then select "Add a rule".We will name the rule changetocool. Select "Next".

<p align="center">
<img src="https://github.com/user-attachments/assets/1d971ee8-8ee2-4fd2-8e97-1201b6a00558">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/66550d54-12a8-4ba2-9619-d22e8c88c4ed">
</p>

8.  On the Base blobs tab, you will configure the condition if based blobs were "last modified more than 30 days ago" then "Move to cool storage". Select "Add" and our Storage Account is ready.

<p align="center">
<img src="https://github.com/user-attachments/assets/48ed250b-8925-47e5-b5e4-1323356d605f">
</p>

## Task 2: Implement and secure Blob storage.

In this task, we will create a blob container and upload a file. Blob containers function as directory-like structures for storing unstructured data.

1.  In the "Data storage" section of the Storage Account, click "Containers". Click "+ Container" and Create a container called info.

<p align="center">
<img src="https://github.com/user-attachments/assets/e08e4329-1ee1-4493-a66b-08b48e7e1fc3">
</p>

2.  On your container, scroll to the ellipsis (...) on the far right, select Access Policy.

<p align="center">
<img src="https://github.com/user-attachments/assets/a5404ab1-f201-4cd2-a967-11b85cf0f039">
</p>

3.  In the Immutable blob storage area, select Add policy. Set the following values, Policy type:	Time-based retention, Set retention period for:	1 day(s). Select "Save".

<p align="center">
<img src="https://github.com/user-attachments/assets/3922049f-694d-45f9-b9c5-6f8caea1d852">
</p>


<p align="center">
<img src="https://github.com/user-attachments/assets/dc0e5834-180f-48d0-b051-cca7879a3258">
</p>

4.  Return to the containers page, select your data container and then click "Upload" (here we'll uploaded a sample txt file). On the Upload blob blade, expand the Advanced section and select, Blob type: Block blob, Block size: 4 MiB, Access tier: Hot, Upload to folder: sectesting, Encryption scope:	Use existing default container scope. Click Upload. Confirm you have a new folder, and your file was uploaded.

<p align="center">
<img src="https://github.com/user-attachments/assets/24a379dd-e211-48da-b06c-5e7666311186">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/0beaad56-a915-4c38-9ec3-853a4bb38447">
</p>

5.  Select your upload file and copy the file URL. Open an Inprivate browsing window and paste the URL (You should be presented with an XML-formatted message stating ResourceNotFound or PublicAccessNotPermitted. This is expected, since the container you created has the public access level set to Private).

<p align="center">
<img src="https://github.com/user-attachments/assets/c93c6105-7d82-4cf7-9049-ad27df089462">
</p>

6.  Let's configure limited access to the blob storage. Select your uploaded file and then on the "Generate SAS" tab, specify the following settings, Signing key: Key 1, Permissions: Read, Start date: yesterday's date, Start time:	current time, Expiry date: tomorrow's date, Expiry time: current time. Click Generate SAS token and URL. Copy the Blob SAS URL and try access again. You should be able to view the content of the file.

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

In this task, you will create and configure Azure File Shares, using Storage Browser to manage them.

1.  In the Azure portal, navigate back to your storage account, in the Data storage section, click File shares. Click "+ File share" and on the Basics tab give the file share the name, filesharetest.

<p align="center">
<img src="https://github.com/user-attachments/assets/899ed12f-3c79-4e4e-acb9-2264b129289f">
</p>

2.  Click "Review + create", and then "Create". Wait for the file share to deploy.
3.  Return to your storage account and select Storage Browser. Select File shares and verify your share1 directory is present.

<p align="center">
<img src="https://github.com/user-attachments/assets/70cfba1d-4a9a-47a1-bdb7-8483d0d9145c">
</p>

4.  Select your filesharetest directory and select "Upload". Browse to a file of your choice, and then click Upload.

<p align="center">
<img src="https://github.com/user-attachments/assets/2f46d2b8-62f3-4e11-b5ac-784eb8819549">
</p>

5.  Now we'll restrict network access to the storage account. In the portal, search for and select "Virtual networks". Select "+ Create". Select your resource group. and give the virtual network a name, StorageVnet. Take the defaults for other parameters, select "Review + create", and then "Create". Wait for the virtual network to deploy, and then select "Go to resource".

<p align="center">
<img src="https://github.com/user-attachments/assets/9340f0c9-7241-4bc8-92c6-6f83a7c85d21">
</p>

6.  In the Settings section, select the "Service endpoints" blade and select "Add". In the Services drop-down select Microsoft.Storage. In the Subnets drop-down check the Default subnet. Click "Add" to save your changes and return to your storage account.

<p align="center">
<img src="https://github.com/user-attachments/assets/479a0cf1-cc55-4490-8b86-f84c830f0442">
</p>

7.  In the "Security + networking" section, select the "Networking" blade. Select add existing virtual network and select StorageVnet and default subnet, select "Add". In the Firewall section, Delete your machine IP address. Allowed traffic should only come from the virtual network we've just created. Be sure to Save your changes.

<p align="center">
<img src="https://github.com/user-attachments/assets/827956b1-96a8-47df-9bf2-3bc64aa0ceb1">
</p>

8.  Select the Storage browser and Refresh the page. Navigate to your file share or blob content. You should receive a message not authorized to perform this operation. You are not connecting from the virtual network. It may take a couple of minutes for this to take effect.

<p align="center">
<img src="https://github.com/user-attachments/assets/3b4e9d3d-cf03-48bc-a897-3083812e3c16">
</p>
