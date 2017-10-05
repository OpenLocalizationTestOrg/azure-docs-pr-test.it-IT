---
title: Passaggio di credenziali ad Azure con DSC | Microsoft Docs
description: Panoramica del passaggio sicuro di credenziali alle macchine virtuali di Azure tramite PowerShell Desired State Configuration
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: ea76b7e8-b576-445a-8107-88ea2f3876b9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: acd768c0219ec23c0453a65c575faf5213d9c616
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="passing-credentials-to-the-azure-dsc-extension-handler"></a><span data-ttu-id="11217-103">Passaggio di credenziali al gestore estensione DSC di Azure</span><span class="sxs-lookup"><span data-stu-id="11217-103">Passing credentials to the Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="11217-104">Questo articolo illustra l'estensione DSC (Desired State Configuration) per Azure.</span><span class="sxs-lookup"><span data-stu-id="11217-104">This article covers the Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="11217-105">Una panoramica del gestore estensione DSC è disponibile in [Introduzione al gestore dell'estensione DSC (Desired State Configuration) di Azure](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="11217-105">An overview of the DSC extension handler can be found at [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="11217-106">Passaggio di credenziali</span><span class="sxs-lookup"><span data-stu-id="11217-106">Passing in credentials</span></span>
<span data-ttu-id="11217-107">Nell'ambito del processo di configurazione, potrebbe essere necessario configurare account utente, servizi di accesso o installare un programma in un contesto utente.</span><span class="sxs-lookup"><span data-stu-id="11217-107">As a part of the configuration process, you may need to set up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="11217-108">Per eseguire queste operazioni, è necessario fornire le credenziali.</span><span class="sxs-lookup"><span data-stu-id="11217-108">To do these things, you need to provide credentials.</span></span> 

<span data-ttu-id="11217-109">DSC consente di eseguire configurazioni con parametri in cui le credenziali vengono passate nella configurazione e archiviate in modo sicuro in file MOF.</span><span class="sxs-lookup"><span data-stu-id="11217-109">DSC allows for parameterized configurations in which credentials are passed into the configuration and securely stored in MOF files.</span></span> <span data-ttu-id="11217-110">Per semplificare la gestione delle credenziali, il gestore estensione di Azure offre la gestione automatica dei certificati.</span><span class="sxs-lookup"><span data-stu-id="11217-110">The Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="11217-111">Considerare lo script di configurazione DSC seguente che crea un account utente locale con la password specificata:</span><span class="sxs-lookup"><span data-stu-id="11217-111">Consider the following DSC configuration script that creates a local user account with the specified password:</span></span>

<span data-ttu-id="11217-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="11217-112">*user_configuration.ps1*</span></span>

```
configuration Main
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PSCredential]
        $Credential
    )    
    Node localhost {       
        User LocalUserAccount
        {
            Username = $Credential.UserName
            Password = $Credential
            Disabled = $false
            Ensure = "Present"
            FullName = "Local User Account"
            Description = "Local User Account"
            PasswordNeverExpires = $true
        } 
    }  
} 
```

<span data-ttu-id="11217-113">È importante includere *node localhost* come parte della configurazione.</span><span class="sxs-lookup"><span data-stu-id="11217-113">It is important to include *node localhost* as part of the configuration.</span></span> <span data-ttu-id="11217-114">Se l'istruzione manca, la successiva procedura non funzionerà dal momento che il gestore dell'estensione cerca specificamente l'istruzione node localhost.</span><span class="sxs-lookup"><span data-stu-id="11217-114">If this statement is missing, the following steps do not work as the extension handler specifically looks for the node localhost statement.</span></span> <span data-ttu-id="11217-115">È importante anche includere il cast di tipo *[PsCredential]*, perché questo tipo specifico attiva l'estensione per crittografare la credenziale.</span><span class="sxs-lookup"><span data-stu-id="11217-115">It is also important to include the typecast *[PsCredential]*, as this specific type triggers the extension to encrypt the credential.</span></span> 

<span data-ttu-id="11217-116">Pubblicare questo script nell'archivio BLOB:</span><span class="sxs-lookup"><span data-stu-id="11217-116">Publish this script to blob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="11217-117">Impostare l'estensione DSC di Azure e specificare la credenziale:</span><span class="sxs-lookup"><span data-stu-id="11217-117">Set the Azure DSC extension and provide the credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="11217-118">Protezione delle credenziali</span><span class="sxs-lookup"><span data-stu-id="11217-118">How credentials are secured</span></span>
<span data-ttu-id="11217-119">Durante l'esecuzione del codice viene chiesta una credenziale.</span><span class="sxs-lookup"><span data-stu-id="11217-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="11217-120">Una volta fornita, viene archiviata nella memoria per breve tempo.</span><span class="sxs-lookup"><span data-stu-id="11217-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="11217-121">Quando viene pubblicata con il cmdlet `Set-AzureVmDscExtension` , viene trasmessa tramite HTTPS alla VM, dove Azure la archivia crittografata su disco, usando il certificato della VM locale.</span><span class="sxs-lookup"><span data-stu-id="11217-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS to the VM, where Azure stores it encrypted on disk, using the local VM certificate.</span></span> <span data-ttu-id="11217-122">Viene quindi brevemente decrittografata nella memoria e nuovamente crittografata per passarla a DSC.</span><span class="sxs-lookup"><span data-stu-id="11217-122">Then it is briefly decrypted in memory and re-encrypted to pass it to DSC.</span></span>

<span data-ttu-id="11217-123">Questo comportamento è diverso dall' [uso di configurazioni sicure senza il gestore dell'estensione](https://msdn.microsoft.com/powershell/dsc/securemof).</span><span class="sxs-lookup"><span data-stu-id="11217-123">This behavior is different than [using secure configurations without the extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="11217-124">L'ambiente di Azure offre un modo per trasmettere i dati di configurazione in maniera sicura tramite certificati.</span><span class="sxs-lookup"><span data-stu-id="11217-124">The Azure environment gives a way to transmit configuration data securely via certificates.</span></span> <span data-ttu-id="11217-125">Quando si usa il gestore dell'estensione DSC, non è necessario fornire $CertificatePath o una voce $CertificateID/$Thumbprint in ConfigurationData.</span><span class="sxs-lookup"><span data-stu-id="11217-125">When using the DSC extension handler, there is no need to provide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11217-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="11217-126">Next steps</span></span>
<span data-ttu-id="11217-127">Per altre informazioni sul gestore dell'estensione DSC, vedere [Introduzione al gestore dell'estensione DSC (Desired State Configuration) di Azure](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="11217-127">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="11217-128">Esaminare il [modello di Azure Resource Manager per l'estensione DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="11217-128">Examine the [Azure Resource Manager template for the DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="11217-129">Per altre informazioni su PowerShell DSC, [vedere il centro di documentazione di PowerShell](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="11217-129">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="11217-130">Per trovare altre funzionalità che è possibile gestire con PowerShell DSC, [cercare in PowerShell Gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) altre risorse DSC.</span><span class="sxs-lookup"><span data-stu-id="11217-130">To find additional functionality you can manage with PowerShell DSC, [browse the PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

