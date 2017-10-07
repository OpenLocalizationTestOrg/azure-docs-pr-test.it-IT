---
title: reindirizzamento aaaUsing in Azure RemoteApp | Documenti Microsoft
description: Informazioni su come tooconfigure e utilizzare il reindirizzamento in RemoteApp
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
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a>Uso del reindirizzamento in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Reindirizzamento della periferica consente agli utenti di interagire con le applicazioni remote utilizzando hello dispositivi collegati tootheir locale computer, telefono o tablet. Ad esempio, se sono stati forniti Skype tramite Azure RemoteApp, l'utente deve fotocamera hello installata toowork i PC con Skype. Lo stesso vale per stampanti, altoparlanti, monitor e vari dispositivi con connessione USB.

RemoteApp sfrutta hello Remote Desktop Protocol (RDP) e RemoteFX tooprovide reindirizzamento.

## <a name="what-redirection-is-enabled-by-default"></a>Quale reindirizzamento è abilitato per impostazione predefinita?
Quando si usa RemoteApp, hello dopo i reindirizzamenti è abilitato per impostazione predefinita. informazioni di Hello tra parentesi indicano impostazione RDP hello.

* Riprodurre suoni del computer locale hello (**riprodurre su questo computer**). (audiomode:i:0)
* Acquisizione audio dal computer locale hello e il computer remoto di trasmissione toohello (**registra da questo computer**). (audiocapturemode:i:1)
* Stampa toolocal stampanti (redirectprinters:i:1)
* Porte COM (redirectcomports:i:1)
* Dispositivo smart card (redirectsmartcards:i:1)
* Appunti (toocopy possibilità e Incolla) (redirectclipboard:i:1)
* Disattivazione caratteri smussati (allowfontsmoothing:i:1)
* Reindirizzamento di tutti i dispositivi Plug and Play supportati. (devicestoredirect:s:*)

## <a name="what-other-redirection-is-available"></a>Quali altri reindirizzamenti sono disponibili?
Due opzioni di reindirizzamento sono disabilitate per impostazione predefinita:

* Il reindirizzamento dell'unità (unità): unità del computer locale diventano le unità mappate in sessione remota hello. In questo modo si salvano o i file aperti da unità locali mentre si lavora nella sessione remota hello.
* Il reindirizzamento USB: È possibile utilizzare un computer locale tooyour collegati dispositivi USB hello all'interno della sessione remota hello.

## <a name="change-your-redirection-settings-in-remoteapp"></a>Modificare le impostazioni di reindirizzamento in RemoteApp
È possibile modificare le impostazioni di reindirizzamento dispositivo hello per una raccolta con hello Microsoft Azure PowerShell SDK. Dopo aver installato hello PowerShell nuovo e SDK, configurarlo toomanage la sottoscrizione come descritto in [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

Utilizzare quindi un toohello simile comando hello personalizzato tooset RDP le proprietà seguenti:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

(Si noti che  *`n*  viene utilizzato come delimitatore tra le singole proprietà.)

tooget un elenco di quali proprietà RDP personalizzate sono configurate, eseguire hello cmdlet seguente. Si noti che le proprietà personalizzate solo sono visualizzate come risultati di output e non hello proprietà predefinite:  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

Quando si impostano le proprietà personalizzate è necessario specificare tutte le proprietà personalizzate ogni volta; in caso contrario impostazione hello Ripristina toodisabled.   

### <a name="common-examples"></a>Esempi comuni
Utilizzare hello dopo il reindirizzamento delle unità tooenable cmdlet:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

Utilizzare questo cmdlet tooenable il reindirizzamento USB e unità:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

Utilizzare la condivisione degli Appunti di cmdlet toodisable:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> Essere toocompletely che disconnette tutti gli utenti nella raccolta di hello (e non solo disconnetterle) prima di testare modifica hello. tooensure gli utenti sono completamente disconnessi, andare toohello **sessioni** scheda nella raccolta di hello nel portale di Azure hello e disconnettersi da tutti gli utenti vengono disconnessi o l'accesso. Talvolta può richiedere alcuni secondi per hello unità locali tooshow Explorer all'interno della sessione di hello.
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a>Modificare le impostazioni di reindirizzamento USB nel client Windows
Se si desidera il reindirizzamento USB toouse in un computer che si connette tooRemoteApp, esistono 2 azioni che richiedono toohappen. 1 - l'amministratore deve il reindirizzamento USB tooenable a livello di raccolta hello tramite Azure PowerShell. 2 - in ogni dispositivo in cui si desidera il reindirizzamento USB toouse, è necessario tooenable criteri di gruppo è consentito. Questo passaggio sarà necessario eseguire per ogni utente che richiede il reindirizzamento USB toouse toobe.

> [!NOTE]
> Il reindirizzamento USB con Azure RemoteApp è supportato solo per i computer Windows.
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a>Abilitare il reindirizzamento USB per hello raccolta RemoteApp
Utilizzare hello dopo il reindirizzamento USB tooenable di cmdlet a livello di raccolta hello:

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a>Abilitare il reindirizzamento USB per computer client hello
impostazioni di reindirizzamento tooconfigure USB nel computer in uso:

1. Hello aprire Editor criteri di gruppo locali (GPEDIT. MSC). (eseguire gpedit.msc da un prompt dei comandi).
2. Aprire **Configurazione computer\Criteri\Modelli amministrativi\Componenti di Windows\Servizi Desktop remoto\Client di connessione desktop remoto\Reindirizzamento dispositivo USB RemoteFX**.
3. Fare doppio clic su **Consenti il reindirizzamento RDP di altri dispositivi USB RemoteFX supportati da questo computer**.
4. Selezionare **abilitato**, quindi selezionare **amministratori e utenti in hello diritti di accesso il reindirizzamento USB di RemoteFX**.
5. Aprire un prompt dei comandi con autorizzazioni di amministratore ed eseguire hello comando seguente:
   
        gpupdate /force
6. Riavviare il computer di hello.

È anche possibile utilizzare toocreate strumento di gestione criteri di gruppo hello e applicare i criteri per il reindirizzamento USB hello per tutti i computer nel dominio:

1. Accedere al controller di dominio hello come amministratore di dominio hello.
2. Aprire Console Gestione criteri di gruppo hello. (fare clic su **Start > Strumenti di amministrazione > Gestione Criteri di gruppo**).
3. Passare toohello dominio o unità organizzativa per il quale si desidera che i criteri di hello toocreate.
4. Fare clic con il pulsante destro del mouse su **Criterio dominio predefinito** e quindi fare clic su **Modifica**.
5. Aprire **Configurazione computer\Criteri\Modelli amministrativi\Componenti di Windows\Servizi Desktop remoto\Client di connessione desktop remoto\Reindirizzamento dispositivo USB RemoteFX**.
6. Fare doppio clic su **Consenti il reindirizzamento RDP di altri dispositivi USB RemoteFX supportati da questo computer**.
7. Selezionare **abilitato**, quindi selezionare **amministratori e utenti in hello diritti di accesso il reindirizzamento USB di RemoteFX**.
8. Fare clic su **OK**.  

