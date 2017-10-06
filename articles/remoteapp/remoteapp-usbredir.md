---
title: "aaaHow è reindirizzare i dispositivi USB in Azure RemoteApp? | Microsoft Docs"
description: Informazioni su come il reindirizzamento toouse per i dispositivi USB in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 191d98af-2f5a-4307-9042-aae0e4049f9f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 661b90c0910167d76ac3886b5af7a32d00b3943f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a>Come reindirizzare i dispositivi USB in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Il reindirizzamento dei dispositivi consente agli utenti di usare computer tootheir collegati dispositivi USB di hello o il tablet con App hello in Azure RemoteApp. Ad esempio, se è stata condivisa Skype tramite Azure RemoteApp, gli utenti devono toouse in grado di toobe le telecamere di dispositivo.

Prima di proseguire, assicurarsi di leggere le informazioni di reindirizzamento USB hello in [mediante il reindirizzamento in Azure RemoteApp](remoteapp-redirection.md). Tuttavia hello consigliato nusbdevicestoredirect:s: * non funzionerà per webcam USB e potrebbero non funzionare per alcune stampanti USB o dispositivi multifunzionali USB. Per impostazione predefinita e per motivi di sicurezza, amministratore di Azure RemoteApp hello ha tooenable reindirizzamento per la classe GUID di dispositivi o per ID istanza del dispositivo prima che gli utenti possono usare tali dispositivi.

Sebbene in questo articolo illustra il reindirizzamento della fotocamera web, è possibile utilizzare un simile stampanti USB tooredirect di approccio e multifunzionale che altre periferiche USB non vengono reindirizzate dai hello **nusbdevicestoredirect:s:*** comando.

## <a name="redirection-options-for-usb-devices"></a>Opzioni di reindirizzamento per i dispositivi USB
Azure RemoteApp utilizza meccanismi di molto simile per il reindirizzamento di dispositivi USB, come quelle disponibili hello per Servizi Desktop remoto. Hello tecnologia sottostante consente di scegliere il metodo corretto reindirizzamento hello per un determinato dispositivo, hello tooget migliore di alto livello entrambi e il reindirizzamento dei dispositivi USB di RemoteFX utilizzando hello **usbdevicestoredirect:s:** comando. Esistono quattro elementi toothis comando:

| Ordine di elaborazione | Parametro | Description |
| --- | --- | --- |
| 1 |* |Seleziona tutti i dispositivi che non vengono selezionati dal reindirizzamento ad alto livello. Nota: per impostazione predefinita, * non funziona per le webcam USB. |
| {Device class GUID} |Seleziona tutti i dispositivi che corrispondono a hello specificato classe di installazione. | |
| USB\InstanceID |Seleziona un dispositivo USB specificato per hello specificato l'ID dell'istanza. | |
| 2 |-USB\Instance ID |Rimuove le impostazioni di reindirizzamento hello per il dispositivo specificato hello. |

## <a name="redirecting-a-usb-device-by-using-hello-device-class-guid"></a>Reindirizzamento di un dispositivo USB utilizzando la classe GUID di hello dispositivi
Esistono due modi la classe di dispositivi hello toofind GUID che può essere usato per il reindirizzamento. 

Hello prima opzione consiste hello toouse [tooVendors definite dal sistema dispositivo installazione classi disponibili](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx). Seleziona classe hello che corrisponde maggiormente computer locale di hello dispositivo toohello associata. Per le videocamere digitali può essere una classe dispositivo di acquisizione immagini o una classe dispositivo di acquisizione video. Toodo è necessario eseguire alcune prove con GUID che funziona con hello localmente classe associata dispositivo USB (nel nostro webcam hello case) corretto hello toofind classi dispositivo hello.

Un modo migliore, o la seconda opzione hello, è toofollow questi passaggi toofind hello periferica il GUID di classe:

1. Aprire Gestione dispositivi hello, individuare il dispositivo hello che verrà reindirizzato e pulsante destro del mouse e quindi aprire le proprietà di hello.
   ![Aprire Gestione dispositivi hello](./media/remoteapp-usbredir/ra-devicemanager.png)
2. In hello **dettagli** scheda, scegliere Proprietà hello **Guid classe**. valore Hello visualizzato è hello GUID di classe per il tipo di dispositivo.
   ![Proprietà della videocamera](./media/remoteapp-usbredir/ra-classguid.png)
3. Utilizzare hello Guid classe valore tooredirect dispositivi corrispondenti.

ad esempio:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

È possibile combinare più reindirizzamenti dispositivo hello stesso cmdlet. Ad esempio: tooredirect di archiviazione locale e una porta USB web fotocamera, cmdlet è simile al seguente:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

Quando si imposta il reindirizzamento dei dispositivi mediante la classe GUID vengono reindirizzati tutti i dispositivi che corrispondono a che la classe GUID in hello raccolta specificata. Ad esempio, se sono presenti più computer nella rete locale hello con hello stesso webcam USB, è possibile eseguire tooredirect un singolo cmdlet tutti webcam hello.

## <a name="redirecting-a-usb-device-by-using-hello-device-instance-id"></a>Reindirizzamento di un dispositivo USB con ID di istanza hello dispositivo
Se si desidera un controllo più accurato e reindirizzamento toocontrol per ogni dispositivo, è possibile utilizzare hello **USB\InstanceID** parametro reindirizzamento.

ID dell'istanza. dispositivo USB hello sta trovando più o parte di più difficile Hello di questo metodo Sarà necessario accedere toohello computer e dispositivo USB specifico hello. Seguire quindi questa procedura:

1. Abilitare il reindirizzamento della periferica di hello nella sessione Desktop remoto come descritto in [come è possibile utilizzare i dispositivi e risorse in una sessione Desktop remoto?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)
2. Aprire una connessione Desktop remoto e fare clic su **Mostra opzioni**.
3. Fare clic su **salvare come** toosave hello connessione impostazioni tooan RDP file corrente.  
    ![Salvare le impostazioni di hello come file RDP](./media/remoteapp-usbredir/ra-saveasrdp.png)
4. Scegliere un nome di file e un percorso, ad esempio MyConnection.rdp e questo PC\Documents e salvare file hello.
5. Aprire hello MyConnection.rdp file utilizzando un editor di testo e trovare l'ID istanza hello del dispositivo hello desiderato tooredirect.

A questo punto, è possibile utilizzare l'ID hello nel hello seguente cmdlet:

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a>Come contribuire al miglioramento
Non tutti sanno che in toorating aggiunta in questo articolo e aggiunta di commenti verso il basso, è possibile rendere articolo toohello di modifiche se stesso. Mancano informazioni? Alcune informazioni non sono corrette? Qualcosa non è abbastanza chiaro? Scorrere verso l'alto e fare clic su **modifica su GitHub** modifiche toomake - provengono quelli toous per la revisione e quindi, al termine è disconnettersi su di essi, si noterà delle modifiche e miglioramenti a destra.

