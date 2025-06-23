## 2025 02 04 Setup Storage Account
```PowerShell
$PSVersionTable.PSVersion # Needs to be version 5.1
Get-ExecutionPolicy # Need remote signed to run scripts 
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned # Yes to all 
Install-Module -name Powershellget -Force # Can run twice to make sure it is installed 
Install-Module -name az -AllowClobber # Powershell modules

# Authenticate to Azure
Connect-AzAccount -DeviceCode
# Copy the link it gives you into the browser, paste the code it gives you. Then login with your saskpolytech.ca account

$RGName = 'RGdenalit1' # replace this with 'RGfnamelastinitial1'
$LOC = 'canadaeast'
$STOR = 'coos294denalit239' # 'coos294fnamelastintial239'

# Create the resource group
New-AzResourceGroup -Name $RGName -Location $LOC
# Create the storage account in the resource group
# If you get an error saying it can't find the subscription login to your azure portal, go to Subscriptions -> Azure for students -> Resource Providers -> Search "Storage" -> Click on the ... for "Microsoft.Storage" -> Click Register -> Wait for it to finish
New-AzStorageAccount -ResourceGroupName $RGName -Name $STOR -Location $LOC -SkuName Standard_LRS -Kind StorageV2 -AccessTier Hot
```
