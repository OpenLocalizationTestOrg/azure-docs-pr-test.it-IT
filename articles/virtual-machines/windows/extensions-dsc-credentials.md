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
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a>Il passaggio di gestore dell'estensione DSC di Azure toohello credenziali
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

In questo articolo descrive l'estensione DSC hello per Azure. Una panoramica del gestore dell'estensione DSC hello è reperibile in [gestore di estensioni di Azure DSC toohello Introduzione](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="passing-in-credentials"></a>Passaggio di credenziali
Come parte del processo di configurazione di hello, potrebbe essere necessario tooset gli account utente, accedere ai servizi o installare un programma in un contesto utente. toodo queste operazioni, sono necessarie le credenziali tooprovide. 

DSC Consente configurazioni con parametri in cui le credenziali vengono passate configurazione hello e archiviate in modo sicuro nel file MOF. Hello gestore dell'estensione Azure semplifica la gestione delle credenziali fornendo la gestione automatica dei certificati. 

Prendere in considerazione hello lo script di configurazione DSC che crea un account utente locale con la password specificata hello seguente:

*user_configuration.ps1*

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

È importante tooinclude *nodo localhost* come parte della configurazione di hello. Se l'istruzione è manca, hello seguenti passaggi non funzionano come gestore dell'estensione hello Cerca specificatamente per l'istruzione di hello nodo localhost. È inoltre importante il cast di tipo hello tooinclude *[PsCredential]*, come il tipo specifico attiva delle credenziali di hello estensione tooencrypt hello. 

Questo tipo di archiviazione tooblob script di pubblicazione:

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

Impostare l'estensione DSC per Azure hello e fornire le credenziali di hello:

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a>Protezione delle credenziali
Durante l'esecuzione del codice viene chiesta una credenziale. Una volta fornita, viene archiviata nella memoria per breve tempo. Quando viene pubblicato con `Set-AzureVmDscExtension` cmdlet, viene trasmessa tramite HTTPS toohello macchina virtuale, in cui Azure archivia crittografati su disco, utilizzando i certificati di macchina virtuale locale hello. È decrittografato brevemente in memoria e crittografare nuovamente toopass è tooDSC.

Questo comportamento è diverso da quello [utilizzando la configurazione protetta senza il gestore dell'estensione hello](https://msdn.microsoft.com/powershell/dsc/securemof). Hello ambiente Azure offre un modo tootransmit configurazione di dati in modo sicuro tramite certificati. Quando si utilizza il gestore di estensioni di hello DSC, non è tooprovide necessità $CertificatePath o un $CertificateID / $Thumbprint voce ConfigurationData.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sul gestore di estensioni di hello DSC per Azure, vedere [gestore di estensioni di Azure DSC toohello Introduzione](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Esaminare hello [il modello di gestione risorse di Azure per l'estensione DSC hello](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Per ulteriori informazioni su PowerShell DSC, [visitare Centro documentazione di PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

funzionalità aggiuntive di toofind è possibile gestire con PowerShell DSC, [Sfoglia raccolta PowerShell hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) per più risorse DSC.

