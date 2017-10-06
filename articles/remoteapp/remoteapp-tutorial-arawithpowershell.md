---
title: i cmdlet di PowerShell con Azure RemoteApp aaaUse | Documenti Microsoft
description: Informazioni su come toouse cmdlet di Windows PowerShell in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a>Usare i cmdlet Windows PowerShell con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

 È possibile utilizzare tooadminister i cmdlet di PowerShell di Azure RemoteApp hello e mantenere le raccolte. Utilizzare hello seguente tooget informazioni avviato.

## <a name="get-hello-cmdlets"></a>Ottenere i cmdlet di hello
- - -
Prima di scaricare i cmdlet di Azure Powershell hello [qui](http://go.microsoft.com/?linkid=9811175), sono inclusi i cmdlet di RemoteApp hello in essa contenuti. 

Estrarre hello [Guida sui cmdlet di Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a>Configura la sottoscrizione di toouse i cmdlet di Azure
- - -
Seguire [questa Guida](/powershell/azure/overview) in modo è possibile utilizzare i cmdlet di hello rispetto alla sottoscrizione di Azure.

È possibile utilizzare tooget questi passaggi in tempi brevi:

1. Scaricare e installare hello [cmdlet di Azure PowerShell](http://go.microsoft.com/?linkid=9811175).
2. Avviare Microsoft Azure PowerShell.
3. Eseguire **Add-AzureAccount** tooauthenticate tooyour sottoscrizione di Azure. Quando richiesto, immettere hello stesso nome utente e password che si usa toosign nel portale di tooAzure.  
4. Eseguire **Get-AzureSubscription** sottoscrizioni hello toolist associate all'account utente. 
5. Eseguire **Select-AzureSubscription - SubscriptionName &lt;nome sottoscrizione&gt;**  o **Select-AzureSubscription - SubscriptionId &lt;ID sottoscrizione&gt;**  toospecify hello sottoscrizione toouse.

Complimenti, la console di PowerShell di Azure è configurato e pronto toouse. Tenere presente che è necessario toorepeate i passaggi da 2 a 5 ogni volta che si avvia console di Azure PowerShell hello hello.  


## <a name="list-all-collections"></a>Elencare tutte le raccolte
- - -
     Get-AzureRemoteAppCollection

## <a name="delete-a-collection"></a>Eliminare una raccolta
- - -
    Remove-AzureRemoteAppCollection <enter collection name>

Esempio: `Remove-AzureRemoteAppCollection ContosoProduction`.

## <a name="create-a-cloud-collection"></a>Creare una raccolta nel cloud
- - -
È semplice, eseguire hello comando seguente:

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

Hello sopra comando Pubblica automaticamente le applicazioni di Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio e Word).

Creazione della raccolta può richiedere 30 minuti o più toocomplete. Questo comando restituisce quindi un ID di traccia che è possibile usare come indicato di seguito:

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

Al termine dell'insieme di hello, è possibile aggiungere una raccolta degli utenti toohello con hello comando seguente:

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

L'operazione è così completata. Tale utente deve essere in grado di tooconnect toohello applicazione utilizzando il client di Azure RemoteApp hello trovato [qui](https://www.remoteapp.windowsazure.com/).

## <a name="available-cmdlets"></a>Cmdlet disponibili
Esistono molti altri comandi che è disponibile, a breve sarà presto documentazione hello:

Cmdlet della raccolta RemoteApp di base: 

* New-AzureRemoteAppCollection
* Get-AzureRemoteAppCollection
* Set-AzureRemoteAppCollection
* Update-AzureRemoteAppCollection
* Remove-AzureRemoteAppCollection
* Add-AzureRemoteAppUser
* Get-AzureRemoteAppUser
* Remove-AzureRemoteAppUser
* Get-AzureRemoteAppSession
* Disconnect-AzureRemoteAppSession
* Invoke-AzureRemoteAppSessionLogoff
* Send-AzureRemoteAppSessionMessage
* Get-AzureRemoteAppProgram
* Get-AzureRemoteAppStartMenuProgram
* Publish-AzureRemoteAppProgram
* Unpublish-AzureRemoteAppProgram
* Get-AzureRemoteAppCollectionUsageDetails
* Get-AzureRemoteAppCollectionUsageSummary
* Get-AzureRemoteAppPlan

Cmdlet della rete virtuale RemoteApp:

* New-AzureRemoteAppVNet
* Get-AzureRemoteAppVNet
* Set-AzureRemoteAppVNet
* Remove-AzureRemoteAppVNet
* Get-AzureRemoteAppVpnDevice
* Get-- AzureRemoteAppVpnDeviceConfigScript
* Reset-AzureRemoteAppVpnSharedKey

Cmdlet dell'immagine modello RemoteApp:

* New-AzureRemoteAppTemplateImage
* Get-AzureRemoteAppTemplateImage
* Rename-AzureRemoteAppTemplateImage
* Remove-AzureRemoteAppTemplateImage

Altri cmdlet di RemoteApp:

* Get-AzureRemoteAppLocation
* Get-AzureRemoteAppWorkspace
* Set-AzureRemoteAppWorkspace
* Get-AzureRemoteAppOperationResult

