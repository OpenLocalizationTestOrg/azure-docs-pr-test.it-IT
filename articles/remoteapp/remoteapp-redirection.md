---
title: Uso del reindirizzamento in Azure RemoteApp | Microsoft Docs
description: Informazioni su come configurare e usare il reindirizzamento in RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: b5a65d129225fde46e3b090bc3cd9427989005ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a>Uso del reindirizzamento in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Il reindirizzamento dei dispositivi consente agli utenti di interagire con applicazioni remote tramite i dispositivi collegati al proprio computer, telefono o tablet locale. Ad esempio, se Skype è accessibile tramite Azure RemoteApp, sul computer dell'utente deve essere installata una telecamera per poter usare Skype. Lo stesso vale per stampanti, altoparlanti, monitor e vari dispositivi con connessione USB.

RemoteApp usa il protocollo RDP (Remote Desktop Protocol) e RemoteFX per il reindirizzamento.

## <a name="what-redirection-is-enabled-by-default"></a>Quale reindirizzamento è abilitato per impostazione predefinita?
Quando si usa RemoteApp, i reindirizzamenti seguenti sono abilitati per impostazione predefinita. Le informazioni tra parentesi mostrano l'impostazione RDP.

* Riproduzione di suoni sul computer locale (**Riproduci nel computer locale**). (audiomode:i:0)
* Acquisizione di audio dal computer locale e invio al computer remoto (**Registra da questo computer**). (audiocapturemode:i:1)
* Stampa su stampanti locali (redirectprinters:i:1)
* Porte COM (redirectcomports:i:1)
* Dispositivo smart card (redirectsmartcards:i:1)
* Appunti (funzionalità di copia e incolla) (redirectclipboard:i:1)
* Disattivazione caratteri smussati (allowfontsmoothing:i:1)
* Reindirizzamento di tutti i dispositivi Plug and Play supportati. (devicestoredirect:s:*)

## <a name="what-other-redirection-is-available"></a>Quali altri reindirizzamenti sono disponibili?
Due opzioni di reindirizzamento sono disabilitate per impostazione predefinita:

* Reindirizzamento delle unità (mapping di unità): le unità del computer locale diventano unità mappate nella sessione remota. In questo modo è possibile salvare o aprire file da unità locali mentre si lavora nella sessione remota.
* Reindirizzamento USB: è possibile usare i dispositivi USB collegati al computer locale all'interno della sessione remota.

## <a name="change-your-redirection-settings-in-remoteapp"></a>Modificare le impostazioni di reindirizzamento in RemoteApp
È possibile modificare le impostazioni di reindirizzamento del dispositivo per una raccolta usando Microsoft Azure PowerShell con SDK. Dopo aver installato il nuovo PowerShell e l'SDK, configurarlo per gestire la sottoscrizione, come descritto in [Come installare e configurare Azure PowerShell](/powershell/azure/overview).

Usare quindi un comando simile al seguente per impostare le proprietà RDP personalizzate:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

(Si noti che  *`n*  viene utilizzato come delimitatore tra le singole proprietà.)

Per un elenco delle proprietà RDP configurate, eseguire il cmdlet seguente. Si noti che solo le proprietà personalizzate vengono visualizzate come risultati di output, non le proprietà predefinite:  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

Quando si impostano proprietà personalizzate, è necessario specificare tutte le proprietà personalizzate ogni volta. In caso contrario, l'impostazione viene nuovamente disabilitata.   

### <a name="common-examples"></a>Esempi comuni
Per abilitare il reindirizzamento delle unità, usare il cmdlet seguente:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

Usare questo cmdlet per abilitare sia il reindirizzamento delle unità che il reindirizzamento USB:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

Usare questo cmdlet per disabilitare la condivisione degli Appunti:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> Assicurarsi di disconnettere completamente tutti gli utenti nella raccolta (non solo scollegarli) prima di verificare la modifica. Per assicurarsi che gli utenti siano disconnessi completamente, andare alla scheda **Sessioni** nella raccolta nel portale di Azure e disconnettere tutti gli utenti scollegati o collegati. Talvolta è necessario attendere alcuni secondi perché le unità locali vengano mostrate in Esplora risorse all'interno della sessione.
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a>Modificare le impostazioni di reindirizzamento USB nel client Windows
Se si desidera usare il reindirizzamento USB su un computer che si connette a RemoteApp, è necessario eseguire 2 azioni. 1 - L'amministratore deve abilitare il reindirizzamento USB a livello di raccolta tramite Azure PowerShell. 2 - Su ogni dispositivo su cui si desidera usare il reindirizzamento USB, è necessario abilitare un criterio di gruppo che lo consente. È necessario eseguire questo passaggio per ogni utente che desidera usare il reindirizzamento USB.

> [!NOTE]
> Il reindirizzamento USB con Azure RemoteApp è supportato solo per i computer Windows.
> 
> 

### <a name="enable-usb-redirection-for-the-remoteapp-collection"></a>Abilitare il reindirizzamento USB per la raccolta di RemoteApp
Per abilitare il reindirizzamento USB a livello di raccolta, utilizzare il cmdlet seguente:

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-the-client-computer"></a>Abilitare il reindirizzamento USB per il computer client
Per configurare le impostazioni di reindirizzamento USB sul computer:

1. Aprire l'Editor Criteri di gruppo locali (GPEDIT.MSC) (eseguire gpedit.msc da un prompt dei comandi).
2. Aprire **Configurazione computer\Criteri\Modelli amministrativi\Componenti di Windows\Servizi Desktop remoto\Client di connessione desktop remoto\Reindirizzamento dispositivo USB RemoteFX**.
3. Fare doppio clic su **Consenti il reindirizzamento RDP di altri dispositivi USB RemoteFX supportati da questo computer**.
4. Selezionare **Attivato** e quindi selezionare **Amministratori e utenti nei diritti di accesso del reindirizzamento USB RemoteFX**.
5. Aprire un prompt dei comandi con autorizzazioni amministrative ed eseguire il comando seguente:
   
        gpupdate /force
6. Riavviare il computer.

È anche possibile usare lo strumento Gestione criteri di gruppo per creare e applicare i criteri di reindirizzamento USB per tutti i computer nel dominio:

1. Accedere al controller di dominio come amministratore di dominio.
2. Aprire Console Gestione criteri di gruppo (fare clic su **Start > Strumenti di amministrazione > Gestione Criteri di gruppo**).
3. Passare al dominio o unità organizzativa per cui si desidera creare il criterio.
4. Fare clic con il pulsante destro del mouse su **Criterio dominio predefinito** e quindi fare clic su **Modifica**.
5. Aprire **Configurazione computer\Criteri\Modelli amministrativi\Componenti di Windows\Servizi Desktop remoto\Client di connessione desktop remoto\Reindirizzamento dispositivo USB RemoteFX**.
6. Fare doppio clic su **Consenti il reindirizzamento RDP di altri dispositivi USB RemoteFX supportati da questo computer**.
7. Selezionare **Attivato** e quindi selezionare **Amministratori e utenti nei diritti di accesso del reindirizzamento USB RemoteFX**.
8. Fare clic su **OK**.  

