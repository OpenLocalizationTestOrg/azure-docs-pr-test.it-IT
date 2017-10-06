---
title: aaaRun qualsiasi app di Windows in tutti i dispositivi con Azure RemoteApp | Documenti Microsoft
description: Informazioni su come tooshare qualsiasi app di Windows con gli utenti con Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 961d40ca-9673-4977-aa54-d6b22fc61ce1
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 750f3b881e0cb671ff6e8f3e851bccdf2262d156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-any-windows-app-on-any-device-with-azure-remoteapp"></a>Eseguire qualsiasi app su qualsiasi dispositivo con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

È possibile eseguire un'applicazione Windows ovunque e veramente su qualsiasi dispositivo - semplicemente utilizzando Azure RemoteApp. Se si tratta di un'applicazione personalizzata programmata 10 anni, o un'app di Office, gli utenti non più necessario toobe legata tooa specifico del sistema operativo (ad esempio Windows XP) alcuni di tali applicazioni.

Con Azure RemoteApp, gli utenti possono anche usare i propri Android o get e i dispositivi di Apple hello stessa esperienza che ottenuti in Windows (o in Windows Phone). A questo scopo, occorre ospitare l'applicazione Windows in una raccolta di macchine virtuali Windows in Azure, dove gli utenti possono ottenere l'accesso ovunque sia disponibile una connessione Internet. 

Continuare a leggere per un esempio di esattamente come toodo questo.

In questo articolo verrà tooshare accesso con tutti gli utenti di. Tuttavia, è possibile usare QUALSIASI app. Come è possibile installare l'app in un computer Windows Server 2012 R2, è possibile condividerla con passaggi hello riportati di seguito. È possibile esaminare hello [requisiti delle app](remoteapp-appreqs.md) toomake che l'applicazione funzionerà.

Si noti che poiché l'accesso è un database e si desidera utile toobe tale database, è necessario effettuare alcuni passaggi aggiuntivi toolet utenti accedere condivisione dati di accesso hello. Se l'app non è un database o non è necessario il tooaccess in grado di una condivisione file toobe di utenti, è possibile ignorare questi passaggi in questa esercitazione

> [!NOTE]
> <a name="note"></a>È necessario un account di Azure di toocomplete questa esercitazione:
> 
> * È possibile [aprire un account Azure, gratuitamente](https://azure.microsoft.com/free/?WT.mc_id=A261C142F): si ottiene crediti è possibile utilizzare tootry out a pagamento di servizi di Azure e anche dopo che vengono utilizzati fino è possibile tenere conto di hello e liberare di utilizzare servizi di Azure, ad esempio siti Web. Carta di credito non verranno mai addebitata, a meno che non modificare le impostazioni in modo esplicito e chiedere toobe addebitati.
> * È possibile [attivare i benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): con la sottoscrizione MSDN ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.
> 
> 

## <a name="create-a-collection-in-remoteapp"></a>Creare una raccolta in RemoteApp
Iniziare con la creazione di una raccolta, che servirà come contenitore per le app e gli utenti. raccolta di Hello funge da contenitore per le App e gli utenti. È possibile creare un'immagine personalizzata o usarne una fornita con la sottoscrizione. Per questa esercitazione viene usata l'immagine di valutazione di Office 2013 hello - app hello tooshare che contiene.

1. Nel portale di Azure hello, scorrere verso il basso nella struttura di spostamento a sinistra di hello fino a visualizzare RemoteApp. Aprire la pagina.
2. Fare clic su **Crea una raccolta RemoteApp**.
3. Fare clic su **Creazione rapida** e immettere un nome per la raccolta.
4. Selezionare l'area di hello desiderato toouse toocreate la raccolta. Per un'esperienza ottimale hello, selezionare l'area di hello che più si avvicina geograficamente toohello posizione in cui gli utenti accederanno app hello. Ad esempio, in questa esercitazione, gli utenti di hello troverà a Redmond, Washington. area di Azure più vicino Hello è **Stati Uniti occidentali**.
5. Selezionare il piano di fatturazione hello desiderato toouse. piano di fatturazione di base di Hello inserisce 16 utenti in una VM di Azure di grandi dimensioni, mentre il piano di fatturazione standard di hello ha 10 utenti in una macchina virtuale Azure di grandi dimensioni. Un esempio generale piano base hello funziona perfettamente per flusso di lavoro tipo di voce dati. Per un'app di produttività, ad esempio Office, è opportuno piano standard hello.
6. Infine, selezionare l'immagine di Office 2013 Professional hello. Questa immagine contiene le app di Office 2013. Promemoria - questa immagine è valida solo per le raccolte della versione di valutazione e le POCs. Non è possibile utilizzare questa immagine in una raccolta di produzione.
7. Fare clic su **Crea raccolta RemoteApp**.

![Creare una raccolta nel cloud in RemoteApp](./media/remoteapp-anyapp/ra-anyappcreatecollection.png)

Verrà avviata la creazione di raccolta, ma può richiedere fino a ora tooan.

È ora è pronto tooadd gli utenti.

## <a name="share-hello-app-with-users"></a>App hello condivisione con utenti
Dopo la raccolta è stata creata correttamente, è ora toopublish accesso toousers e aggiungere utenti hello devono avere accesso tooit.

Se si passa dal nodo di Azure RemoteApp hello durante la creazione di raccolta hello, iniziare creando il modo di eseguire il backup tooit da hello home page di Azure.

1. Fare clic sulla raccolta hello creato tooaccess precedenti opzioni aggiuntive e configurare la raccolta di hello.
   ![Nuova raccolta nel cloud di RemoteApp](./media/remoteapp-anyapp/ra-anyappcollection.png)
2. In hello **pubblicazione** scheda, fare clic su **pubblica** nella parte inferiore di hello della schermata Ciao e quindi fare clic su **pubblicare avviare i programmi di menu**.
   ![Pubblicare un programma di RemoteApp](./media/remoteapp-anyapp/ra-anyapppublish.png)
3. Selezionare le app di hello da toopublish dall'elenco di hello. Per questa esercitazione si è scelto Access. Fare clic su **Complete**. Attesa per la pubblicazione di toofinish App hello.
   ![Pubblicazione di Access in RemoteApp](./media/remoteapp-anyapp/ra-anyapppublishaccess.png)
4. Dopo l'applicazione hello ha terminato la pubblicazione, visitare toohello **accesso utente** scheda tooadd tutti gli utenti di hello che devono accedere alle App tooyour. Immettere i nomi utente (indirizzo di posta elettronica) degli utenti e quindi fare clic su **Salva**.

![Aggiungere gli utenti tooRemoteApp](./media/remoteapp-anyapp/ra-anyappaddusers.png)

1. A questo punto, è ora tootell agli utenti le nuove applicazioni e come tooaccess li. toodo, inviare loro un messaggio di posta elettronica puntarli toohello URL di download del client Desktop remoto.
   ![URL di download client di Hello per RemoteApp](./media/remoteapp-anyapp/ra-anyappurl.png)

## <a name="configure-access-tooaccess"></a>Configurare l'accesso tooAccess
Alcune app richiedono una configurazione aggiuntiva dopo la distribuzione tramite RemoteApp. In particolare, per l'accesso, siamo toocreate corso una condivisione di file in Azure che qualsiasi utente può accedere. (Se non si desidera toodo, è possibile creare un [raccolta ibrida](remoteapp-create-hybrid-deployment.md) [anziché la raccolta cloud] che consente agli utenti di accedere ai file e le informazioni sulla rete locale.) Quindi, è necessario tootell nostri toomap agli utenti un'unità locale nel loro toohello computer del sistema di file di Azure.

Hello prima parte che è come salve. quindi alcuni passaggi dovranno essere eseguiti dagli utenti.

1. Avviare interfaccia della riga di pubblicazione hello comando (cmd.exe). In hello **pubblicazione** , selezionare **cmd**, quindi fare clic su **pubblica > pubblica programma utilizzando percorso**.
2. Immettere il nome di hello dell'applicazione hello e il percorso di hello. A questo scopo, utilizzare "Esplora File" come nome hello e "% SYSTEMDRIVE%\windows\explorer.exe" come percorso di hello.
   ![Il file cmd.exe hello pubblicazione.](./media/remoteapp-anyapp/ra-publishcmd.png)
3. Ora è necessario toocreate di Azure [account di archiviazione](../storage/common/storage-create-storage-account.md). È denominato interna "accessstorage", quindi scegliere un nome significativo tooyou. (toomisquote Highlander, può essere presente un solo "accessstorage.") ![L'account di archiviazione](./media/remoteapp-anyapp/ra-anyappazurestorage.png)
4. Tornare tooyour dashboard è possibile ottenere l'archiviazione di tooyour hello percorso (posizione endpoint). che verrà usato tra poco, quindi assicurarsi di copiarlo.
   ![percorso di account di archiviazione Hello](./media/remoteapp-anyapp/ra-anyappstoragelocation.png)
5. Successivamente, dopo aver creato l'account di archiviazione hello, sarà necessario chiave di accesso primaria hello. Fare clic su **Gestisci chiavi di accesso**e quindi chiave di accesso primaria hello copia.
6. A questo punto, impostare il contesto di hello hello dell'account di archiviazione e creare una nuova condivisione file per l'accesso. Eseguire hello seguente cmdlet in una finestra di Windows PowerShell con privilegi elevato:
   
        $ctx=New-AzureStorageContext <account name> <account key>
        $s = New-AzureStorageShare <share name> -Context $ctx
   
    Per la quota di mercato, pertanto sono cmdlet hello eseguiamo:
   
        $ctx=New-AzureStorageContext accessstorage <key>
        $s = New-AzureStorageShare <share name> -Context $ctx

A questo punto, il turno di hello utente del. Innanzitutto chiedere agli utenti di installare un [client RemoteApp](remoteapp-clients.md). Successivamente, gli utenti di hello necessario toomap un'unità dal loro toothat account Azure file condividere creato e aggiungono i file di accesso. Ecco come eseguire questa operazione:

1. Nel client di RemoteApp hello, l'App pubblicate hello di accesso. Avviare cmd.exe hello.
2. Eseguire hello successivo comando toomap un'unità dalla condivisione di file toohello di computer:
   
        net use z: \\<accountname>.file.core.windows.net\<share name> /u:<user name> <account key>
   
    Se si imposta hello **/ permanente** parametro tooyes, hello unità mappata verrà mantenuto tra le sessioni.
3. A questo punto, avvia app Esplora File hello da RemoteApp. Copiare i file di accesso desiderato toouse nella condivisione di file toohello app condiviso hello.
   ![Inserimento dei file di Access in una condivisione di Azure](./media/remoteapp-anyapp/ra-anyappuseraccess.png)
4. Infine, aprire l'accesso e quindi aprire il database di hello appena condivisa. Si devono visualizzare i dati in esecuzione dal cloud hello di accesso.
   ![Un database di Access reale in esecuzione dal cloud hello](./media/remoteapp-anyapp/ra-anyapprunningaccess.png)

A questo punto è possibile usare Access su qualsiasi dispositivo, basta avere installato un client RemoteApp.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
Dopo avere appreso come si crea una raccolta, provare a creare una [raccolta che usa Office 365](remoteapp-tutorial-o365anywhere.md). In alternativa è possibile creare una [raccolta ibrida ](remoteapp-create-hybrid-deployment.md)in grado di accedere alla rete locale.

<!--Image references-->

