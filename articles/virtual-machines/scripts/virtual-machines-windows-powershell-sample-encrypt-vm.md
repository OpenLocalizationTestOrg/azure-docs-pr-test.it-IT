---
title: Esempio di script di Azure PowerShell - Crittografare una VM Windows | Microsoft Docs
description: Esempio di script di Azure PowerShell - Crittografare una VM Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 9279fea482fcd8716bcd996985e10f500a4775ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="61142-103">Crittografare una macchina virtuale Windows con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="61142-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="61142-104">Questo script crea un Azure Key Vault sicuro, le chiavi di crittografia, un'entità servizio di Azure Active Directory e una macchina virtuale (VM) Windows.</span><span class="sxs-lookup"><span data-stu-id="61142-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="61142-105">La VM viene quindi crittografata usando la chiave di crittografia del Key Vault e le credenziali dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="61142-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="61142-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="61142-106">Sample script</span></span>

<span data-ttu-id="61142-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Crittografare i dischi delle VM")]</span><span class="sxs-lookup"><span data-stu-id="61142-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="61142-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="61142-108">Clean up deployment</span></span> 

<span data-ttu-id="61142-109">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="61142-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="61142-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="61142-110">Script explanation</span></span>

<span data-ttu-id="61142-111">Questo script usa i comandi seguenti per creare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="61142-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="61142-112">Ogni elemento della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="61142-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="61142-113">Comando</span><span class="sxs-lookup"><span data-stu-id="61142-113">Command</span></span> | <span data-ttu-id="61142-114">Note</span><span class="sxs-lookup"><span data-stu-id="61142-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="61142-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="61142-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="61142-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="61142-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="61142-117">New-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="61142-117">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="61142-118">Crea un Azure Key Vault per archiviare i dati protetti, ad esempio le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="61142-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="61142-119">Add-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="61142-119">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="61142-120">Crea una chiave di crittografia in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="61142-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="61142-121">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="61142-121">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="61142-122">Crea un'entità servizio di Azure Active Directory per autenticare in modo sicuro e controllare l'accesso alle chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="61142-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="61142-123">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="61142-123">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="61142-124">Imposta le autorizzazioni in Key Vault per concedere l'accesso dell'entità servizio alle chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="61142-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="61142-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="61142-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="61142-126">Crea una configurazione di subnet.</span><span class="sxs-lookup"><span data-stu-id="61142-126">Creates a subnet configuration.</span></span> <span data-ttu-id="61142-127">Questa configurazione viene usata con il processo di creazione della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="61142-127">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="61142-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="61142-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="61142-129">Crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="61142-129">Creates a virtual network.</span></span> |
| [<span data-ttu-id="61142-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="61142-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="61142-131">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="61142-131">Creates a public IP address.</span></span> |
| [<span data-ttu-id="61142-132">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="61142-132">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="61142-133">Crea una configurazione di regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="61142-133">Creates a network security group rule configuration.</span></span> <span data-ttu-id="61142-134">Questa configurazione viene usata per creare una regola NSG quando viene creato il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="61142-134">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="61142-135">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="61142-135">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="61142-136">Crea un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="61142-136">Creates a network security group.</span></span> |
| [<span data-ttu-id="61142-137">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="61142-137">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="61142-138">Ottiene informazioni sulla subnet.</span><span class="sxs-lookup"><span data-stu-id="61142-138">Gets subnet information.</span></span> <span data-ttu-id="61142-139">Queste informazioni vengono usate durante la creazione di un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="61142-139">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="61142-140">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="61142-140">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="61142-141">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="61142-141">Creates a network interface.</span></span> |
| [<span data-ttu-id="61142-142">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="61142-142">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="61142-143">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="61142-143">Creates a VM configuration.</span></span> <span data-ttu-id="61142-144">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="61142-144">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="61142-145">La configurazione viene usata durante la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="61142-145">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="61142-146">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="61142-146">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="61142-147">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="61142-147">Create a virtual machine.</span></span> |
| [<span data-ttu-id="61142-148">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="61142-148">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="61142-149">Ottiene le informazioni necessarie in Key Vault</span><span class="sxs-lookup"><span data-stu-id="61142-149">Gets required information on the Key Vault</span></span> |
| [<span data-ttu-id="61142-150">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="61142-150">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="61142-151">Abilita la crittografia in una VM usando le credenziali dell'entità servizio e la chiave di crittografia.</span><span class="sxs-lookup"><span data-stu-id="61142-151">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="61142-152">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="61142-152">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="61142-153">Mostra lo stato del processo di crittografia della VM.</span><span class="sxs-lookup"><span data-stu-id="61142-153">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="61142-154">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="61142-154">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="61142-155">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="61142-155">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="61142-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61142-156">Next steps</span></span>

<span data-ttu-id="61142-157">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="61142-157">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="61142-158">Altri esempi di script PowerShell della macchina virtuale sono reperibili nella [documentazione della VM Windows di Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="61142-158">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
