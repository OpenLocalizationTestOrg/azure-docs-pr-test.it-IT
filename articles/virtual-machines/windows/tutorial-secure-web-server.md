---
title: i certificati aaaSecure IIS con SSL in Azure | Documenti Microsoft
description: Informazioni su come toosecure hello IIS web server con certificati SSL in una macchina virtuale Windows in Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/14/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 7a9e0ce07be2f55095fdb5347b64faf5caa4f7e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="05417-103">Proteggere il server Web IIS con i certificati SSL in una macchina virtuale Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="05417-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="05417-104">server web toosecure, un certificato in un secondo momento SSL (Secure Sockets) può essere utilizzato il traffico web tooencrypt.</span><span class="sxs-lookup"><span data-stu-id="05417-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="05417-105">Questi certificati SSL possono essere archiviati nell'insieme di credenziali chiave di Azure e consentono le distribuzioni sicure di certificati tooWindows le macchine virtuali (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="05417-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooWindows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="05417-106">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="05417-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="05417-107">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="05417-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="05417-108">Generare o caricare un insieme di credenziali chiave di toohello certificato</span><span class="sxs-lookup"><span data-stu-id="05417-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="05417-109">Creare una macchina virtuale e installare il server web IIS di hello</span><span class="sxs-lookup"><span data-stu-id="05417-109">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="05417-110">Inserire il certificato di hello in hello VM e configurare IIS con un binding SSL</span><span class="sxs-lookup"><span data-stu-id="05417-110">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="05417-111">Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo.</span><span class="sxs-lookup"><span data-stu-id="05417-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="05417-112">Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="05417-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="05417-113">Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="05417-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="05417-114">Panoramica</span><span class="sxs-lookup"><span data-stu-id="05417-114">Overview</span></span>
<span data-ttu-id="05417-115">Azure Key Vault consente di proteggere chiavi di crittografia, chiavi private, certificati e password.</span><span class="sxs-lookup"><span data-stu-id="05417-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="05417-116">Insieme di credenziali chiave consente di ottimizzare processo di gestione dei certificati hello e consente il controllo toomaintain delle chiavi che accedono a tali certificati.</span><span class="sxs-lookup"><span data-stu-id="05417-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="05417-117">È possibile creare un certificato autofirmato in Key Vault o caricarne uno esistente, un certificato attendibile di cui si è già proprietari.</span><span class="sxs-lookup"><span data-stu-id="05417-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="05417-118">Invece di usare un'immagine di macchina virtuale personalizzata che include certificati incorporati, si inseriscono i certificati in una macchina virtuale in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="05417-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="05417-119">Questo processo assicura che i certificati più aggiornati di hello siano installati in un server web durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="05417-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="05417-120">Se si rinnovare o sostituire un certificato, non è inoltre necessario toocreate una nuova immagine di macchina virtuale personalizzata.</span><span class="sxs-lookup"><span data-stu-id="05417-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="05417-121">i certificati più recenti di Hello vengono inseriti automaticamente durante la creazione di macchine virtuali aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="05417-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="05417-122">Durante l'intero processo hello, i certificati di hello mai lasciare hello piattaforma Azure o vengono esposti in uno script, una cronologia della riga di comando o un modello.</span><span class="sxs-lookup"><span data-stu-id="05417-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="05417-123">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="05417-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="05417-124">Per poter creare un insieme di credenziali delle chiavi e i certificati, è prima necessario creare un gruppo di risorse con il comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="05417-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="05417-125">esempio Hello crea un gruppo di risorse denominato *myResourceGroupSecureWeb* in hello *Stati Uniti orientali* percorso:</span><span class="sxs-lookup"><span data-stu-id="05417-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="05417-126">Creare quindi un insieme di credenziali delle chiavi con [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="05417-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="05417-127">Ogni Key Vault deve avere un nome univoco in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="05417-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="05417-128">Sostituire `<mykeyvault>` in hello esempio con il proprio nome univoco di insieme di credenziali chiave seguente:</span><span class="sxs-lookup"><span data-stu-id="05417-128">Replace `<mykeyvault>` in hello following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="05417-129">Generare un certificato e archiviarlo in Key Vault</span><span class="sxs-lookup"><span data-stu-id="05417-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="05417-130">Per la produzione è necessario importare un certificato valido firmato da un provider attendibile con il comando [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="05417-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="05417-131">Per questa esercitazione, hello esempio seguente viene illustrato come è possibile generare un certificato autofirmato con [Aggiungi AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) che utilizza hello criteri di certificato predefiniti da [ Nuovo AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="05417-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses hello default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

```powershell
$policy = New-AzureKeyVaultCertificatePolicy `
    -SubjectName "CN=www.contoso.com" `
    -SecretContentType "application/x-pkcs12" `
    -IssuerName Self `
    -ValidityInMonths 12

Add-AzureKeyVaultCertificate `
    -VaultName $keyvaultName `
    -Name "mycert" `
    -CertificatePolicy $policy 
```


## <a name="create-a-virtual-machine"></a><span data-ttu-id="05417-132">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="05417-132">Create a virtual machine</span></span>
<span data-ttu-id="05417-133">Un nome utente amministratore e una password per hello macchina virtuale con set [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="05417-133">Set an administrator username and password for hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="05417-134">Ora è possibile creare hello macchina virtuale con [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="05417-134">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="05417-135">Crea componenti di rete virtuale hello necessario, la configurazione del sistema operativo hello, Hello seguente e quindi crea una macchina virtuale denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="05417-135">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myVnet" `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleRDP"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 443
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleWWW"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name "myNic" `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS2" | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName "myVM" -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" -Skus "2016-Datacenter" -Version "latest" | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create virtual machine
New-AzureRmVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig

# Use hello Custom Script Extension tooinstall IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="05417-136">Sono necessari alcuni minuti per hello VM toobe creato.</span><span class="sxs-lookup"><span data-stu-id="05417-136">It takes a few minutes for hello VM toobe created.</span></span> <span data-ttu-id="05417-137">ultimo passaggio Hello utilizza hello estensione dello Script di Azure personalizzata tooinstall hello server web di IIS con [Set AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="05417-137">hello last step uses hello Azure Custom Script Extension tooinstall hello IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-toovm-from-key-vault"></a><span data-ttu-id="05417-138">Aggiungere un certificato tooVM dall'insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="05417-138">Add a certificate tooVM from Key Vault</span></span>
<span data-ttu-id="05417-139">certificato di hello tooadd dall'insieme di credenziali chiave tooa macchina virtuale, ottenere l'ID di hello del certificato con [Get AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="05417-139">tooadd hello certificate from Key Vault tooa VM, obtain hello ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="05417-140">Aggiungere hello certificato toohello VM con [Aggiungi AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="05417-140">Add hello certificate toohello VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a><span data-ttu-id="05417-141">Configurare IIS toouse hello certificato</span><span class="sxs-lookup"><span data-stu-id="05417-141">Configure IIS toouse hello certificate</span></span>
<span data-ttu-id="05417-142">Utilizzare hello estensione Script personalizzata con [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate la configurazione di IIS hello.</span><span class="sxs-lookup"><span data-stu-id="05417-142">Use hello Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS configuration.</span></span> <span data-ttu-id="05417-143">Questo aggiornamento si applica il certificato di hello inserito dall'insieme di credenziali chiave tooIIS e configura hello web associazione:</span><span class="sxs-lookup"><span data-stu-id="05417-143">This update applies hello certificate injected from Key Vault tooIIS and configures hello web binding:</span></span>

```powershell
$PublicSettings = '{
    "fileUris":["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/secure-iis.ps1"],
    "commandToExecute":"powershell -ExecutionPolicy Unrestricted -File secure-iis.ps1"
}'

Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString $publicSettings
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="05417-144">App web in modo sicuro hello di test</span><span class="sxs-lookup"><span data-stu-id="05417-144">Test hello secure web app</span></span>
<span data-ttu-id="05417-145">Ottenere l'indirizzo IP pubblico hello della macchina virtuale con [Get AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="05417-145">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="05417-146">esempio Hello Ottiene hello di indirizzo IP per `myPublicIP` creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="05417-146">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="05417-147">È ora possibile aprire un web browser e immettere `https://<myPublicIP>` nella barra degli indirizzi hello.</span><span class="sxs-lookup"><span data-stu-id="05417-147">Now you can open a web browser and enter `https://<myPublicIP>` in hello address bar.</span></span> <span data-ttu-id="05417-148">avviso di sicurezza hello tooaccept se è stato utilizzato un certificato autofirmato, selezionare **dettagli** e quindi **andare nella pagina Web toohello**:</span><span class="sxs-lookup"><span data-stu-id="05417-148">tooaccept hello security warning if you used a self-signed certificate, select **Details** and then **Go on toohello webpage**:</span></span>

![Accettare l'avviso di sicurezza del Web browser](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="05417-150">Il sito Web IIS protetto viene quindi visualizzato come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="05417-150">Your secured IIS website is then displayed as in hello following example:</span></span>

![Visualizzare il sito protetto IIS in esecuzione](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="05417-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="05417-152">Next steps</span></span>

<span data-ttu-id="05417-153">In questa esercitazione si è protetto un server Web IIS con un certificato SSL archiviato in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="05417-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="05417-154">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="05417-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="05417-155">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="05417-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="05417-156">Generare o caricare un insieme di credenziali chiave di toohello certificato</span><span class="sxs-lookup"><span data-stu-id="05417-156">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="05417-157">Creare una macchina virtuale e installare il server web IIS di hello</span><span class="sxs-lookup"><span data-stu-id="05417-157">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="05417-158">Inserire il certificato di hello in hello VM e configurare IIS con un binding SSL</span><span class="sxs-lookup"><span data-stu-id="05417-158">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="05417-159">Seguire questo toosee di collegamento incorporati gli esempi di script di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="05417-159">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="05417-160">Esempi di script delle macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="05417-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)