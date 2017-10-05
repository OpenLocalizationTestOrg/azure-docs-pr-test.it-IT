---
title: Proteggere IIS con i certificati SSL in Azure | Microsoft Docs
description: Informazioni su come proteggere il server Web IIS con i certificati SSL in una VM Windows in Azure
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
ms.openlocfilehash: 6567853e9ef3cad63595dc0afe7a793bdc5d972c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="8144f-103">Proteggere il server Web IIS con i certificati SSL in una macchina virtuale Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="8144f-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="8144f-104">Per proteggere i server Web, si può usare un certificato Secure Sockets Layer (SSL) per crittografare il traffico Web.</span><span class="sxs-lookup"><span data-stu-id="8144f-104">To secure web servers, a Secure Sockets Later (SSL) certificate can be used to encrypt web traffic.</span></span> <span data-ttu-id="8144f-105">Questi certificati SSL possono essere archiviati in Azure Key Vault e consentono distribuzioni sicure dei certificati nelle macchine virtuali (VM) Windows in Azure.</span><span class="sxs-lookup"><span data-stu-id="8144f-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates to Windows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="8144f-106">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="8144f-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8144f-107">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="8144f-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="8144f-108">Generare o caricare un certificato in Key Vault</span><span class="sxs-lookup"><span data-stu-id="8144f-108">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="8144f-109">Creare una macchina virtuale e installare il server Web IIS</span><span class="sxs-lookup"><span data-stu-id="8144f-109">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="8144f-110">Inserire il certificato nella macchina virtuale e configurare IIS con un'associazione SSL</span><span class="sxs-lookup"><span data-stu-id="8144f-110">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="8144f-111">Questa esercitazione richiede il modulo Azure PowerShell 3.6 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="8144f-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="8144f-112">Eseguire ` Get-Module -ListAvailable AzureRM` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="8144f-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="8144f-113">Se è necessario eseguire l'aggiornamento, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="8144f-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="8144f-114">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8144f-114">Overview</span></span>
<span data-ttu-id="8144f-115">Azure Key Vault consente di proteggere chiavi di crittografia, chiavi private, certificati e password.</span><span class="sxs-lookup"><span data-stu-id="8144f-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="8144f-116">Key Vault semplifica il processo di gestione dei certificati e consente di mantenere il controllo delle chiavi che accedono a tali certificati.</span><span class="sxs-lookup"><span data-stu-id="8144f-116">Key Vault helps streamline the certificate management process and enables you to maintain control of keys that access those certificates.</span></span> <span data-ttu-id="8144f-117">È possibile creare un certificato autofirmato in Key Vault o caricarne uno esistente, un certificato attendibile di cui si è già proprietari.</span><span class="sxs-lookup"><span data-stu-id="8144f-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="8144f-118">Invece di usare un'immagine di macchina virtuale personalizzata che include certificati incorporati, si inseriscono i certificati in una macchina virtuale in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8144f-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="8144f-119">Questo processo assicura che, durante la distribuzione, in un server Web vengano installati i certificati più aggiornati.</span><span class="sxs-lookup"><span data-stu-id="8144f-119">This process ensures that the most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="8144f-120">Se si rinnova o sostituisce un certificato, non è necessario creare anche una nuova immagine di macchina virtuale personalizzata.</span><span class="sxs-lookup"><span data-stu-id="8144f-120">If you renew or replace a certificate, you don't also have to create a new custom VM image.</span></span> <span data-ttu-id="8144f-121">I certificati più recenti vengono automaticamente inseriti quando si creano macchine virtuali aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="8144f-121">The latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="8144f-122">Durante l'intero processo, i certificati non lasciano mai la piattaforma Azure e non vengono mai esposti in uno script, in una cronologia della riga di comando o in un modello.</span><span class="sxs-lookup"><span data-stu-id="8144f-122">During the whole process, the certificates never leave the Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="8144f-123">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="8144f-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="8144f-124">Per poter creare un insieme di credenziali delle chiavi e i certificati, è prima necessario creare un gruppo di risorse con il comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="8144f-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="8144f-125">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroupSecureWeb* nella località *East US*:</span><span class="sxs-lookup"><span data-stu-id="8144f-125">The following example creates a resource group named *myResourceGroupSecureWeb* in the *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="8144f-126">Creare quindi un insieme di credenziali delle chiavi con [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="8144f-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="8144f-127">Ogni Key Vault deve avere un nome univoco in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="8144f-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="8144f-128">Nell'esempio seguente, sostituire `<mykeyvault>` con il nome univoco del proprio Key Vault:</span><span class="sxs-lookup"><span data-stu-id="8144f-128">Replace `<mykeyvault>` in the following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="8144f-129">Generare un certificato e archiviarlo in Key Vault</span><span class="sxs-lookup"><span data-stu-id="8144f-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="8144f-130">Per la produzione è necessario importare un certificato valido firmato da un provider attendibile con il comando [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="8144f-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="8144f-131">Per questa esercitazione, l'esempio seguente illustra come sia possibile generare un certificato autofirmato con il comando [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) che usi i criteri dei certificati predefiniti da [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="8144f-131">For this tutorial, the following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses the default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

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


## <a name="create-a-virtual-machine"></a><span data-ttu-id="8144f-132">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="8144f-132">Create a virtual machine</span></span>
<span data-ttu-id="8144f-133">Impostare nome utente e password dell'amministratore della macchina virtuale con il comando [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="8144f-133">Set an administrator username and password for the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="8144f-134">A questo punto è possibile creare la macchina virtuale con il comando [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="8144f-134">Now you can create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="8144f-135">Nell'esempio seguente vengono creati i componenti della rete virtuale necessari e viene eseguita la configurazione del sistema operativo. Viene quindi creata una macchina virtuale denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="8144f-135">The following example creates the required virtual network components, the OS configuration, and then creates a VM named *myVM*:</span></span>

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

# Use the Custom Script Extension to install IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="8144f-136">Per creare la macchina virtuale sono necessari alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="8144f-136">It takes a few minutes for the VM to be created.</span></span> <span data-ttu-id="8144f-137">L'ultimo passaggio usa l'estensione Script personalizzato di Azure per installare il server Web IIS con [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="8144f-137">The last step uses the Azure Custom Script Extension to install the IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-to-vm-from-key-vault"></a><span data-ttu-id="8144f-138">Aggiungere un certificato alla macchina virtuale da Key Vault</span><span class="sxs-lookup"><span data-stu-id="8144f-138">Add a certificate to VM from Key Vault</span></span>
<span data-ttu-id="8144f-139">Per aggiungere un certificato da Key Vault a una macchina virtuale, ottenere l'ID del certificato con [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="8144f-139">To add the certificate from Key Vault to a VM, obtain the ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="8144f-140">Aggiungere il certificato alla macchina virtuale con [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="8144f-140">Add the certificate to the VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-to-use-the-certificate"></a><span data-ttu-id="8144f-141">Configurare IIS per usare il certificato</span><span class="sxs-lookup"><span data-stu-id="8144f-141">Configure IIS to use the certificate</span></span>
<span data-ttu-id="8144f-142">Usare di nuovo l'estensione Script personalizzato con [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) per aggiornare la configurazione di IIS.</span><span class="sxs-lookup"><span data-stu-id="8144f-142">Use the Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to update the IIS configuration.</span></span> <span data-ttu-id="8144f-143">Questo aggiornamento applica il certificato inserito da Key Vault a IIS e configura l'associazione Web:</span><span class="sxs-lookup"><span data-stu-id="8144f-143">This update applies the certificate injected from Key Vault to IIS and configures the web binding:</span></span>

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


### <a name="test-the-secure-web-app"></a><span data-ttu-id="8144f-144">Testare l'applicazione Web protetta</span><span class="sxs-lookup"><span data-stu-id="8144f-144">Test the secure web app</span></span>
<span data-ttu-id="8144f-145">Ottenere l'indirizzo IP pubblico della macchina virtuale con il comando [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="8144f-145">Obtain the public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="8144f-146">L'esempio seguente ottiene l'indirizzo IP `myPublicIP` creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="8144f-146">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="8144f-147">È ora possibile aprire un Web browser e immettere `https://<myPublicIP>` bella barra degli indirizzi.</span><span class="sxs-lookup"><span data-stu-id="8144f-147">Now you can open a web browser and enter `https://<myPublicIP>` in the address bar.</span></span> <span data-ttu-id="8144f-148">Per accettare l'avviso di sicurezza se si è usato un certificato autofirmato, selezionare **Dettagli** e quindi **Continua per la pagina Web**:</span><span class="sxs-lookup"><span data-stu-id="8144f-148">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**:</span></span>

![Accettare l'avviso di sicurezza del Web browser](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="8144f-150">Il sito Web IIS protetto viene quindi visualizzato come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="8144f-150">Your secured IIS website is then displayed as in the following example:</span></span>

![Visualizzare il sito protetto IIS in esecuzione](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="8144f-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8144f-152">Next steps</span></span>

<span data-ttu-id="8144f-153">In questa esercitazione si è protetto un server Web IIS con un certificato SSL archiviato in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8144f-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="8144f-154">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="8144f-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8144f-155">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="8144f-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="8144f-156">Generare o caricare un certificato in Key Vault</span><span class="sxs-lookup"><span data-stu-id="8144f-156">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="8144f-157">Creare una macchina virtuale e installare il server Web IIS</span><span class="sxs-lookup"><span data-stu-id="8144f-157">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="8144f-158">Inserire il certificato nella macchina virtuale e configurare IIS con un'associazione SSL</span><span class="sxs-lookup"><span data-stu-id="8144f-158">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="8144f-159">Seguire questo collegamento per vedere esempi di script predefiniti delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8144f-159">Follow this link to see pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8144f-160">Esempi di script delle macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="8144f-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)