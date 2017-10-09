---
title: aaaHow toocreate immagini di macchina virtuale Windows Azure con chi | Documenti Microsoft
description: Informazioni su come le immagini di toocreate chi toouse delle macchine virtuali di Windows in Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: d310fae3becb453b52d21281cb8ac53fa14a3fc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-windows-virtual-machine-images-in-azure"></a>Come le immagini di macchina virtuale Windows di toouse chi toocreate in Azure
Ogni macchina virtuale (VM) in Azure viene creato da un'immagine che definisce la distribuzione di Windows hello e versione del sistema operativo. Le immagini possono includere applicazioni e configurazioni preinstallate. Hello Azure Marketplace fornisce molte immagini prima e di terze parti per più comuni del sistema operativo e gli ambienti di applicazione, oppure è possibile creare le proprie esigenze tooyour immagini personalizzate personalizzate. In questo articolo illustra in dettaglio come hello toouse aprire lo strumento di origine [chi](https://www.packer.io/) toodefine e compilazione immagini personalizzate in Azure.


## <a name="create-azure-resource-group"></a>Creare un gruppo di risorse di Azure
Durante il processo di compilazione hello, chi crea risorse di Azure temporanee durante la compilazione di macchina virtuale di origine hello. toocapture che VM di origine per l'utilizzo come un'immagine, è necessario definire un gruppo di risorse. l'output dal processo di compilazione chi hello Hello viene archiviato in questo gruppo di risorse.

Creare un gruppo di risorse con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a>Creare credenziali di Azure
Per eseguire l'autenticazione con Azure, Packer usa un'entità servizio. Un'entità servizio di Azure è un'identità di sicurezza che è possibile usare con le app, con i servizi e con strumenti di automazione come Packer. È controllare e definire le autorizzazioni di hello come entità di servizio toowhat operazioni hello è possibile eseguire in Azure.

Creare un servizio principale con [New AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) e assegnare le autorizzazioni per toocreate principale di servizio hello e gestire le risorse con [New AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

tooAzure tooauthenticate, è necessario anche tooobtain degli ID tenant e una sottoscrizione Azure con [Get AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

Utilizzare queste due ID nel passaggio successivo hello.


## <a name="define-packer-template"></a>Definire un modello di Packer
immagini toobuild, si crea un modello come un file JSON. Nel modello hello definisce generatori e provisioners per l'esecuzione di hello effettivo processo di compilazione. Chi ha un [strumento di provisioning per Azure](https://www.packer.io/docs/builders/azure.html) che consentono di toodefine Azure risorse, ad esempio credenziali dell'entità servizio hello create nel passaggio precedente hello.

Creare un file denominato *windows.json* e Incolla hello seguendo il contenuto. Immettere i valori per i seguenti hello:

| .                           | Dove tooobtain |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | ID entità servizio di visualizzazione con `$sp.applicationId` |
| *client_secret*                     | Password specificata in`$securePassword` |
| *tenant_id*                         | Output del comando `$sub.TenantId` |
| *subscription_id*                   | Output del comando `$sub.SubscriptionId` |
| *object_id*                         | ID oggetto entità servizio di visualizzazione con `$sp.Id` |
| *managed_image_resource_group_name* | Nome del gruppo di risorse creato nel primo passaggio hello |
| *managed_image_name*                | Nome dell'immagine di disco gestito hello creato |

```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "0831b578-8ab6-40b9-a581-9a880a94aab1",
    "client_secret": "P@ssw0rd!",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",
    "object_id": "a7dfb070-0d5b-47ac-b9a5-cf214fff0ae2",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Windows",
    "image_publisher": "MicrosoftWindowsServer",
    "image_offer": "WindowsServer",
    "image_sku": "2016-Datacenter",

    "communicator": "winrm",
    "winrm_use_ssl": "true",
    "winrm_insecure": "true",
    "winrm_timeout": "3m",
    "winrm_username": "packer",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "type": "powershell",
    "inline": [
      "Add-WindowsFeature Web-Server",
      "if( Test-Path $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml ){ rm $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml -Force}",
      "& $Env:SystemRoot\\System32\\Sysprep\\Sysprep.exe /oobe /generalize /shutdown /quiet"
    ]
  }]
}
```

Questo modello crea una macchina virtuale di Windows Server 2016, viene installato IIS, quindi consente di generalizzare hello macchina virtuale con Sysprep.


## <a name="build-packer-image"></a>Compilare l'immagine in Packer
Se non si dispone già installati nel computer locale, chi [seguire le istruzioni di installazione di hello chi](https://www.packer.io/docs/install/index.html).

Creare immagini hello specificando il chi file modello nel modo seguente:

```bash
./packer build windows.json
```

Un esempio di output di hello da hello precedenti comandi è la seguente:

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> task : Image deployment
==> azure-arm:  ->> dept : Engineering
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting hello certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM toobecome available...
==> azure-arm: Connected tooWinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-pq0mthtbtt/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Compute Name              : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

Sono necessari alcuni minuti per toobuild hello chi macchina virtuale, eseguire provisioners hello e pulizia hello distribuzione.


## <a name="create-vm-from-azure-image"></a>Creare una macchina virtuale da un'immagine di Azure
Impostare un amministratore di nome utente e password per le macchine virtuali hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).

```powershell
$cred = Get-Credential
```

È ora possibile creare una macchina virtuale dall'immagine con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). esempio Hello crea una macchina virtuale denominata *myVM* da *myPackerImage*.

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod "Static" `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Define hello image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

Sono necessari alcuni minuti toocreate hello macchina virtuale.


## <a name="test-vm-and-iis"></a>Testare la macchina virtuale e IIS
Ottenere l'indirizzo IP pubblico hello della macchina virtuale con [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). esempio Hello Ottiene hello di indirizzo IP per *myPublicIP* creato in precedenza:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

È quindi possibile immettere l'indirizzo IP pubblico hello nel browser web tooa.

![Sito IIS predefinito](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a>Passaggi successivi
In questo esempio, chi toocreate un'immagine di macchina virtuale è usato con installato IIS. È possibile utilizzare questa immagine di macchina virtuale insieme a distribuzione flussi di lavoro esistenti, ad esempio toodeploy tooVMs l'app creata da hello immagine con Team Services, Ansible, Chef o Puppet.

Per altri modelli di Packer di esempio per distribuzioni di Windows di altro tipo, vedere [questo repository di GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).