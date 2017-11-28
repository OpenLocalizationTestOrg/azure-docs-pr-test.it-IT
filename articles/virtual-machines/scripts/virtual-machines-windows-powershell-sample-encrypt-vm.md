---
title: Esempio di Script di PowerShell - aaaAzure crittografare una macchina virtuale Windows | Documenti Microsoft
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
ms.openlocfilehash: 80c52a0b734a52a051ed30026b294840fd521143
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="b4dcf-103">Crittografare una macchina virtuale Windows con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4dcf-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="b4dcf-104">Questo script crea un Azure Key Vault sicuro, le chiavi di crittografia, un'entità servizio di Azure Active Directory e una macchina virtuale (VM) Windows.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="b4dcf-105">Hello macchina virtuale viene quindi crittografata con la chiave di crittografia hello dall'insieme di credenziali chiave e le credenziali dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b4dcf-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="b4dcf-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b4dcf-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="b4dcf-107">Clean up deployment</span></span> 

<span data-ttu-id="b4dcf-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b4dcf-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="b4dcf-109">Script explanation</span></span>

<span data-ttu-id="b4dcf-110">Questo script utilizza hello dopo la distribuzione di comandi toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="b4dcf-111">Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b4dcf-112">Comando</span><span class="sxs-lookup"><span data-stu-id="b4dcf-112">Command</span></span> | <span data-ttu-id="b4dcf-113">Note</span><span class="sxs-lookup"><span data-stu-id="b4dcf-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b4dcf-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b4dcf-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b4dcf-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b4dcf-116">New-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="b4dcf-116">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="b4dcf-117">Crea un insieme credenziali chiavi Azure toostore sicura di dati, ad esempio le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="b4dcf-118">Add-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="b4dcf-118">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="b4dcf-119">Crea una chiave di crittografia in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="b4dcf-120">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="b4dcf-120">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="b4dcf-121">Crea un servizio di Azure Active Directory principale toosecurely autenticare e controllare le chiavi di accesso tooencryption.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="b4dcf-122">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="b4dcf-122">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="b4dcf-123">Imposta le autorizzazioni per hello insieme di credenziali chiave toogrant hello servizio principale tooencryption tasti di scelta.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="b4dcf-124">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="b4dcf-124">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="b4dcf-125">Crea una configurazione di subnet.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-125">Creates a subnet configuration.</span></span> <span data-ttu-id="b4dcf-126">Questa configurazione viene utilizzata con processo di creazione di hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-126">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="b4dcf-127">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="b4dcf-127">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="b4dcf-128">Crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-128">Creates a virtual network.</span></span> |
| [<span data-ttu-id="b4dcf-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="b4dcf-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="b4dcf-130">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-130">Creates a public IP address.</span></span> |
| [<span data-ttu-id="b4dcf-131">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="b4dcf-131">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="b4dcf-132">Crea una configurazione di regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-132">Creates a network security group rule configuration.</span></span> <span data-ttu-id="b4dcf-133">Questa configurazione è toocreate utilizzata una regola di gruppo quando hello gruppo viene creato.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-133">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="b4dcf-134">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="b4dcf-134">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="b4dcf-135">Crea un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-135">Creates a network security group.</span></span> |
| [<span data-ttu-id="b4dcf-136">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="b4dcf-136">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="b4dcf-137">Ottiene informazioni sulla subnet.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-137">Gets subnet information.</span></span> <span data-ttu-id="b4dcf-138">Queste informazioni vengono usate durante la creazione di un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-138">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="b4dcf-139">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="b4dcf-139">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="b4dcf-140">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-140">Creates a network interface.</span></span> |
| [<span data-ttu-id="b4dcf-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="b4dcf-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="b4dcf-142">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-142">Creates a VM configuration.</span></span> <span data-ttu-id="b4dcf-143">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="b4dcf-144">configurazione di Hello viene utilizzato durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="b4dcf-145">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="b4dcf-145">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="b4dcf-146">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-146">Create a virtual machine.</span></span> |
| [<span data-ttu-id="b4dcf-147">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="b4dcf-147">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="b4dcf-148">Ottiene le informazioni necessarie su hello insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="b4dcf-148">Gets required information on hello Key Vault</span></span> |
| [<span data-ttu-id="b4dcf-149">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="b4dcf-149">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="b4dcf-150">Abilita la crittografia in una macchina virtuale con le credenziali dell'entità servizio di hello e la chiave di crittografia.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-150">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="b4dcf-151">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="b4dcf-151">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="b4dcf-152">Mostra stato hello di hello il processo di crittografia di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-152">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="b4dcf-153">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b4dcf-153">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b4dcf-154">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="b4dcf-154">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b4dcf-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b4dcf-155">Next steps</span></span>

<span data-ttu-id="b4dcf-156">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b4dcf-156">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b4dcf-157">Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4dcf-157">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
