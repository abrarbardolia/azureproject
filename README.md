# azureproject

To deploy the described infrastructure, you will need to follow these steps. The instructions are somewhat high-level, so ensure you have the necessary permissions and understand Azure concepts:

### Pre-requisites:
1. **Azure Account:** Ensure you have an Azure account with the necessary permissions to create resources.
2. **Azure CLI:** Install and configure Azure CLI on your local machine.

### Steps:

#### 1. Create Resources in Central US Region:
   - **Virtual Network (VNet):** Create a VNet in the Central US region.
   - **VM1:** Deploy a VM in the Central US region, attach it to the VNet, and clone the GitHub repo. Run `vm1.sh`.
   - **Azure Blob Storage:** Create a storage account in the Central US region. Configure it as specified.
   - **Error Page Hosting:** Host `error.html` as a static website in a container in the storage account.

#### 2. Create Resources in West US Region:
   - **Virtual Network (VNet):** Create a VNet in the West US region.
   - **VM2:** Deploy a VM in the West US region, attach it to the VNet, and clone the GitHub repo. Run `vm2.sh`.
   - **Application Gateway:** Configure the Application Gateway in the West US region.
   - **VNet Peering:** Establish VNet-VNet peering between Central US and West US VNets.

#### 3. Configure VMs:
   - On VM1, edit `config.py` with details related to the Central US storage account.
   - On VM2, run `sudo python3 app.py` to start the home page.

#### 4. Configure Application Gateway:
   - Point `example.com` to the home page in Central US.
   - Point `example.com/upload` to the upload page in Central US.
   - Configure error pages in Application Gateway to point to the hosted `error.html` in Central US storage account.

#### 5. Configure Traffic Manager:
   - Create a Traffic Manager profile and configure it to point to the Application Gateway in both Central US and West US.

### Notes:
- Ensure you have the necessary security groups, network security groups, and other configurations to allow traffic between VMs, VNets, and Application Gateway.
- Properly configure DNS settings for `example.com` to point to the Traffic Manager profile.
- Use Azure CLI or Azure Portal to create these resources based on the specifications provided.

This is a high-level guide, and you might need to adapt these steps based on your specific requirements and the evolving Azure service offerings. Always refer to the Azure documentation for the most accurate and up-to-date information.
