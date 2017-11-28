---
title: aaaPassing credenziali tooAzure con DSC | Documenti Microsoft
description: Panoramica sul passaggio in modo sicuro le credenziali tooAzure le macchine virtuali mediante PowerShell Desired State Configuration
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
ms.openlocfilehash: 306ecd3fd481f49a0beca5052fc7531a52999330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a><span data-ttu-id="f50b2-103">Il passaggio di gestore dell'estensione DSC di Azure toohello credenziali</span><span class="sxs-lookup"><span data-stu-id="f50b2-103">Passing credentials toohello Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f50b2-104">In questo articolo descrive l'estensione DSC hello per Azure.</span><span class="sxs-lookup"><span data-stu-id="f50b2-104">This article covers hello Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="f50b2-105">Una panoramica del gestore dell'estensione DSC hello è reperibile in [gestore di estensioni di Azure DSC toohello Introduzione](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f50b2-105">An overview of hello DSC extension handler can be found at [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="f50b2-106">Passaggio di credenziali</span><span class="sxs-lookup"><span data-stu-id="f50b2-106">Passing in credentials</span></span>
<span data-ttu-id="f50b2-107">Come parte del processo di configurazione di hello, potrebbe essere necessario tooset gli account utente, accedere ai servizi o installare un programma in un contesto utente.</span><span class="sxs-lookup"><span data-stu-id="f50b2-107">As a part of hello configuration process, you may need tooset up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="f50b2-108">toodo queste operazioni, sono necessarie le credenziali tooprovide.</span><span class="sxs-lookup"><span data-stu-id="f50b2-108">toodo these things, you need tooprovide credentials.</span></span> 

<span data-ttu-id="f50b2-109">DSC Consente configurazioni con parametri in cui le credenziali vengono passate configurazione hello e archiviate in modo sicuro nel file MOF.</span><span class="sxs-lookup"><span data-stu-id="f50b2-109">DSC allows for parameterized configurations in which credentials are passed into hello configuration and securely stored in MOF files.</span></span> <span data-ttu-id="f50b2-110">Hello gestore dell'estensione Azure semplifica la gestione delle credenziali fornendo la gestione automatica dei certificati.</span><span class="sxs-lookup"><span data-stu-id="f50b2-110">hello Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="f50b2-111">Prendere in considerazione hello lo script di configurazione DSC che crea un account utente locale con la password specificata hello seguente:</span><span class="sxs-lookup"><span data-stu-id="f50b2-111">Consider hello following DSC configuration script that creates a local user account with hello specified password:</span></span>

<span data-ttu-id="f50b2-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="f50b2-112">*user_configuration.ps1*</span></span>

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

<span data-ttu-id="f50b2-113">È importante tooinclude *nodo localhost* come parte della configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="f50b2-113">It is important tooinclude *node localhost* as part of hello configuration.</span></span> <span data-ttu-id="f50b2-114">Se l'istruzione è manca, hello seguenti passaggi non funzionano come gestore dell'estensione hello Cerca specificatamente per l'istruzione di hello nodo localhost.</span><span class="sxs-lookup"><span data-stu-id="f50b2-114">If this statement is missing, hello following steps do not work as hello extension handler specifically looks for hello node localhost statement.</span></span> <span data-ttu-id="f50b2-115">È inoltre importante il cast di tipo hello tooinclude *[PsCredential]*, come il tipo specifico attiva delle credenziali di hello estensione tooencrypt hello.</span><span class="sxs-lookup"><span data-stu-id="f50b2-115">It is also important tooinclude hello typecast *[PsCredential]*, as this specific type triggers hello extension tooencrypt hello credential.</span></span> 

<span data-ttu-id="f50b2-116">Questo tipo di archiviazione tooblob script di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="f50b2-116">Publish this script tooblob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="f50b2-117">Impostare l'estensione DSC per Azure hello e fornire le credenziali di hello:</span><span class="sxs-lookup"><span data-stu-id="f50b2-117">Set hello Azure DSC extension and provide hello credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="f50b2-118">Protezione delle credenziali</span><span class="sxs-lookup"><span data-stu-id="f50b2-118">How credentials are secured</span></span>
<span data-ttu-id="f50b2-119">Durante l'esecuzione del codice viene chiesta una credenziale.</span><span class="sxs-lookup"><span data-stu-id="f50b2-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="f50b2-120">Una volta fornita, viene archiviata nella memoria per breve tempo.</span><span class="sxs-lookup"><span data-stu-id="f50b2-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="f50b2-121">Quando viene pubblicato con `Set-AzureVmDscExtension` cmdlet, viene trasmessa tramite HTTPS toohello macchina virtuale, in cui Azure archivia crittografati su disco, utilizzando i certificati di macchina virtuale locale hello.</span><span class="sxs-lookup"><span data-stu-id="f50b2-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS toohello VM, where Azure stores it encrypted on disk, using hello local VM certificate.</span></span> <span data-ttu-id="f50b2-122">È decrittografato brevemente in memoria e crittografare nuovamente toopass è tooDSC.</span><span class="sxs-lookup"><span data-stu-id="f50b2-122">Then it is briefly decrypted in memory and re-encrypted toopass it tooDSC.</span></span>

<span data-ttu-id="f50b2-123">Questo comportamento è diverso da quello [utilizzando la configurazione protetta senza il gestore dell'estensione hello](https://msdn.microsoft.com/powershell/dsc/securemof).</span><span class="sxs-lookup"><span data-stu-id="f50b2-123">This behavior is different than [using secure configurations without hello extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="f50b2-124">Hello ambiente Azure offre un modo tootransmit configurazione di dati in modo sicuro tramite certificati.</span><span class="sxs-lookup"><span data-stu-id="f50b2-124">hello Azure environment gives a way tootransmit configuration data securely via certificates.</span></span> <span data-ttu-id="f50b2-125">Quando si utilizza il gestore di estensioni di hello DSC, non è tooprovide necessità $CertificatePath o un $CertificateID / $Thumbprint voce ConfigurationData.</span><span class="sxs-lookup"><span data-stu-id="f50b2-125">When using hello DSC extension handler, there is no need tooprovide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f50b2-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f50b2-126">Next steps</span></span>
<span data-ttu-id="f50b2-127">Per ulteriori informazioni sul gestore di estensioni di hello DSC per Azure, vedere [gestore di estensioni di Azure DSC toohello Introduzione](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f50b2-127">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="f50b2-128">Esaminare hello [il modello di gestione risorse di Azure per l'estensione DSC hello](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f50b2-128">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f50b2-129">Per ulteriori informazioni su PowerShell DSC, [visitare Centro documentazione di PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="f50b2-129">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="f50b2-130">funzionalità aggiuntive di toofind è possibile gestire con PowerShell DSC, [Sfoglia raccolta PowerShell hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) per più risorse DSC.</span><span class="sxs-lookup"><span data-stu-id="f50b2-130">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

