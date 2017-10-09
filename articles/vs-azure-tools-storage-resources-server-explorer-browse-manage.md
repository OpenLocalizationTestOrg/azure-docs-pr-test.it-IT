---
title: aaaBrowsing e la gestione delle risorse di archiviazione con Esplora Server | Documenti Microsoft
description: Esplorazione e gestione delle risorse di archiviazione con Esplora server
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 658dc064-4a4e-414b-ae5a-a977a34c930d
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/24/2017
ms.author: kraigb
ms.openlocfilehash: f5b456b812f2ad8103c50538d532a57397bcccbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a>Esplorazione e gestione delle risorse di archiviazione con Esplora server
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Panoramica
Se è stato installato hello Azure Tools per Microsoft Visual Studio, è possibile visualizzare blob, coda e i dati della tabella dagli account di archiviazione di Azure. nodo di archiviazione di Azure Hello in Esplora Server Mostra i dati dell'account dell'emulatore di archiviazione locale e di altri account di archiviazione di Azure.

Scegliere tooview Esplora Server in Visual Studio, sulla barra dei menu hello, **vista**, **Esplora Server**. nodo di archiviazione Hello Mostra tutti gli account di archiviazione hello che esistono in ogni sottoscrizione/certificato Azure che si è connessi. Se non viene visualizzato l'account di archiviazione, è possibile aggiungere seguendo le istruzioni di hello [più avanti in questo argomento](#add-storage-accounts-by-using-server-explorer).

A partire da Azure SDK 2.7, è anche possibile usare hello nuovo Cloud Explorer tooview e gestire le risorse di Azure. Per altre informazioni, vedere [Gestione delle risorse di Azure con Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md) .

## <a name="view-and-manage-storage-resources-in-visual-studio"></a>Visualizzare e gestire le risorse di archiviazione in Visual Studio
Esplora server mostra automaticamente un elenco di BLOB, code e tabelle nell'account dell'emulatore di archiviazione. account dell'emulatore di archiviazione Hello è elencato in Esplora Server nel nodo archiviazione hello come hello **sviluppo** nodo.

risorse toosee hello emulatore account di archiviazione, espandere hello **sviluppo** nodo. Se l'emulatore di archiviazione hello non è stata avviata quando si espande hello **sviluppo** nodo, verrà avviato automaticamente. Ciò può richiedere alcuni secondi. È possibile continuare toowork in altre aree di Visual Studio durante l'avvio di emulatore di archiviazione hello.

tooview risorse in un account di archiviazione, espandere il nodo dell'account di archiviazione hello in Esplora Server. vengono visualizzati Hello i sottonodi seguenti:

* Blobs
* Code
* Tables

## <a name="work-with-blob-resources"></a>Usare le risorse BLOB
nodo BLOB Hello Visualizza un elenco di contenitori per l'account di archiviazione hello selezionato. I contenitori BLOB contengono file BLOB che possono essere organizzati in cartelle e sottocartelle. Vedere [come archiviazione di Blob da .NET toouse](storage/blobs/storage-dotnet-how-to-use-blobs.md) per ulteriori informazioni.

### <a name="toocreate-a-blob-container"></a>toocreate un contenitore blob
1. Menu di scelta rapida aprire hello hello **BLOB** nodo, quindi scegliere **crea contenitore Blob**.
2. In hello **crea contenitore Blob** finestra di dialogo immettere il nome di hello del nuovo contenitore hello.  
3. Premere **invio** sulla tastiera o è possibile fare clic o toccare di fuori del contenitore di blob hello hello Nome campo toosave.
   
   > [!NOTE]
   > nome del contenitore blob Hello deve iniziare con una lettera minuscola (a-z) o un numero (0-9).
   > 
   > 

### <a name="toodelete-a-blob-container"></a>toodelete un contenitore blob
* Menu di scelta rapida aprire hello contenitore di blob hello tooremove desiderato e quindi scegliere **eliminare**.

### <a name="toodisplay-a-list-of-hello-items-contained-in-a-blob-container"></a>toodisplay un elenco di elementi di hello contenuti in un contenitore blob
* Aprire il menu di scelta rapida hello per un nome di contenitore blob nell'elenco di hello e quindi scegliere **aprire**.
  
    Quando si visualizza il contenuto di hello di un contenitore blob, viene visualizzata in una scheda nota come visualizzazione del contenitore blob hello.
  
    ![VST_SE_BlobDesigner](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    È possibile eseguire dopo le operazioni sui BLOB utilizzando i pulsanti di hello nell'angolo superiore destro di hello di visualizzazione del contenitore blob hello hello:
  
  * Immettere un valore di filtro e applicarlo
  * Aggiornare l'elenco di hello di BLOB nel contenitore hello
  * Caricare un file
  * Eliminare un BLOB
    
    > [!NOTE]
    > Eliminazione di un file da un contenitore blob non comporta l'eliminazione di file sottostante hello. viene solo rimosso dal contenitore blob hello.
    > 
    > 
  * Aprire un BLOB
  * Salvare un computer locale toohello di blob

### <a name="toocreate-a-folder-or-subfolder-in-a-blob-container"></a>toocreate una cartella o una sottocartella in un contenitore blob
1. Scegliere il contenitore di blob hello in Cloud Explorer. Nella finestra contenitore hello scegliere hello **carica Blob** pulsante.
   
    ![Caricamento di un file in una cartella BLOB](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. In hello **Carica nuovo File** finestra di dialogo scegliere hello **Sfoglia** pulsante toospecify hello file desiderato tooupload, quindi immettere un nome di cartella in hello **cartella (facoltativo)** casella .
   
    È possibile aggiungere sottocartelle nelle cartelle del contenitore seguendo hello stessa procedura. Se non si specifica un nome di cartella, file hello è caricato toohello di livello superiore del contenitore blob hello. file di Hello viene visualizzato nella cartella specificata hello contenitore hello.
   
    ![Aggiunta di cartella contenitore blob tooa](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. Fare doppio clic sulla cartella hello o premere INVIO toosee hello contenuto hello cartella. Quando si è nella cartella del contenitore di hello, è possibile spostarsi indietro toohello radice del contenitore hello scegliendo hello **Apri Directory padre** (freccia su) pulsante.

### <a name="toodelete-a-container-folder"></a>toodelete una cartella del contenitore
* Eliminare tutti i file nella cartella hello hello
  
  > [!NOTE]
  > Poiché le cartelle nei contenitori blob sono cartelle virtuali, è possibile creare una cartella vuota, né è possibile eliminare una cartella toodelete il contenuto del file. È l'intero contenuto hello toodelete di una cartella di hello toodelete cartella.
  > 
  > 

### <a name="toofilter-blobs-in-a-container"></a>toofilter BLOB in un contenitore
È possibile filtrare i BLOB visualizzati specificando un prefisso comune hello.

Ad esempio, se si immette il prefisso hello `hello` nella casella di testo filtro hello e quindi scegliere hello **Execute** (**!**) pulsante, viene visualizzato solo i blob che iniziano con "hello".

![VST_SE_FilterBlobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> campo filtro Hello tra maiuscole e minuscole e non supporta l'applicazione di filtri con caratteri jolly. I BLOB possono essere filtrati solo in base al prefisso. prefisso Hello può includere un delimitatore se si utilizza un BLOB tooorganize delimitatore in una gerarchia virtuale. Ad esempio, il filtro sui hello prefisso HelloFabric / restituisce tutti i blob che iniziano con tale stringa.
> 
> 

### <a name="toodownload-blob-data"></a>dati blob toodownload
* In **Cloud Explorer**, aprire il menu di scelta rapida hello per uno o più BLOB e quindi scegliere **aprire**, o scegliere il nome di blob hello quindi hello **aprire** pulsante oppure fare doppio clic nome del blob Hello.
  
    stato Hello di un download di blob viene visualizzato in hello **Log attività Azure** finestra.
  
    blob Hello aperto nell'editor di predefinito hello per tale tipo di file. Sistema operativo hello riconosce il tipo di file hello, hello file verrà aperto in un'applicazione installata in locale. in caso contrario, viene chiesto di un'applicazione che è appropriata per il tipo di file hello del blob hello toochoose. file Hello locale viene creato quando si scarica un blob è contrassegnato come sola lettura.
  
    Dati BLOB nella cache in locale e confrontati hello ora dell'ultima modifica del blob nel servizio Blob hello. Se il blob hello è stato aggiornato dopo l'ultimo è stato scaricato, verrà scaricato. in caso contrario, verrà caricato dal disco locale hello blob hello. Per impostazione predefinita, un blob è la directory temporanea tooa scaricato. toodownload BLOB tooa specifica directory, menu di scelta rapida aprire hello hello selezionato i nomi di blob e scegliere **Salva con nome**. Quando si salva un blob in questo modo, non è aperto il file di blob hello e file locale hello viene creato con gli attributi di lettura / scrittura.

### <a name="tooupload-blobs"></a>BLOB tooupload
* Scegliere hello **carica Blob** pulsante quando il contenitore di hello è aperto nella visualizzazione del contenitore blob hello relativa visualizzazione.
  
    È possibile scegliere uno o più tooupload file ed è possibile caricare i file di qualsiasi tipo. Hello **Log attività Azure** Mostra hello lo stato di avanzamento del caricamento hello. Per ulteriori informazioni su come toowork con i dati blob, vedere [come toouse hello il servizio di archiviazione Blob di Azure in .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).

### <a name="tooview-logs-transferred-tooblobs"></a>i registri di tooview trasferiti tooblobs
* Se si utilizzano dati di diagnostica Azure toolog dall'applicazione Azure e sono stati trasferiti log tooyour account di archiviazione, verranno visualizzati i contenitori creati da Azure per tali log. Visualizzazione di questi log in Esplora Server è un problemi tooidentify facilmente con l'applicazione, soprattutto se è stato distribuito tooAzure. Per altre informazioni su Diagnostica di Azure, vedere [Raccogliere dati di registrazione usando Diagnostica di Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx).

### <a name="tooget-hello-url-for-a-blob"></a>tooget hello URL per un blob
* Aprire il menu di scelta rapida del blob hello e quindi scegliere **Copia URL**.

### <a name="tooedit-a-blob"></a>tooedit un blob
* Selezionare i blob hello e quindi scegliere hello **Apri Blob** pulsante.
  
    file Hello percorso temporaneo tooa scaricato e aperto nel computer locale hello. Dopo aver apportato modifiche, è necessario caricare nuovamente i blob hello.

## <a name="work-with-queue-resources"></a>Usare le risorse di accodamento
Code di servizi di archiviazione sono ospitate in un account di archiviazione di Azure e di utilizzarli tooallow toocommunicate di ruoli del servizio cloud tra loro e con altri servizi mediante un meccanismo di passaggio dei messaggi. È possibile accedere a livello di programmazione coda hello tramite un servizio cloud e in un servizio web per i client esterni. È inoltre possibile accedere coda hello tramite Esplora Server in Visual Studio.

Quando si sviluppa un servizio cloud che utilizza le code, si desidera che le code toocreate di Visual Studio toouse e lavorare con essi in modo interattivo durante lo sviluppo e test del codice.

In Esplora Server, è possibile visualizzare code hello in un account di archiviazione, creare ed eliminare le code, aprire tooview una coda dei messaggi e aggiungere tooa coda dei messaggi. Quando si apre una coda per la visualizzazione, è possibile visualizzare i singoli messaggi hello ed è possibile eseguire hello seguenti azioni in coda hello mediante i pulsanti di hello nell'angolo superiore sinistro hello:

* Aggiornare la visualizzazione hello della coda di hello
* Aggiungere una coda di messaggi toohello
* Messaggio hello del livello più alto di rimozione dalla coda
* Intera coda crittografato hello

Hello immagine seguente viene illustrata una coda contenente due messaggi.

![Visualizzazione di una coda](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

Per ulteriori informazioni sull'archiviazione code dei servizi, vedere [come: hello Usa servizio di archiviazione code](http://go.microsoft.com/fwlink/?LinkID=264702). Per informazioni sul servizio web hello per le code dei servizi di archiviazione, vedere [concetti relativi al servizio di Accodamento](http://go.microsoft.com/fwlink/?LinkId=264788). Per informazioni su come archiviazione tooa di messaggi toosend coda di servizi tramite Visual Studio, vedere [tooa l'invio di messaggi della coda di servizi di archiviazione](https://msdn.microsoft.com/library/azure/jj649344.aspx).

> [!NOTE]
> Le code di servizi di archiviazione sono diverse dalle code del bus di servizio. Per altre informazioni sulle code del bus di servizio, vedere Code, argomenti e sottoscrizioni del bus di servizio.
> 
> 

## <a name="work-with-table-resources"></a>Usare le risorse di una tabella
servizio di archiviazione tabelle Azure Hello archivia grandi quantità di dati strutturati. servizio Hello è autenticato di un archivio dati NoSQL che accetta chiamate dall'interno e all'esterno di hello cloud di Azure. Le tabelle di Azure sono ideali per l'archiviazione di dati strutturati non relazionali.

### <a name="toocreate-a-table"></a>toocreate una tabella
1. In Esplora risorse di Cloud, selezionare hello **tabelle** nodo di archiviazione hello account e quindi scegliere **Create Table**.
2. In hello **Create Table** finestra di dialogo immettere un nome per la tabella hello.

### <a name="tooview-table-data"></a>dati della tabella tooview
1. In Cloud Explorer, aprire hello **Azure** nodo e quindi aprire hello **archiviazione** nodo.
2. Nodo di account di archiviazione di hello aprire interessati e quindi aprire hello **tabelle** toosee nodo un elenco di tabelle per account di archiviazione hello.
3. Aprire il menu di scelta rapida hello per una tabella e quindi scegliere **tabella vista**.
   
    ![Tabella di Azure in Esplora soluzioni](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

tabella di Hello è organizzata in entità (mostrate nelle righe) e proprietà (mostrate nelle colonne). Ad esempio, hello nella figura seguente mostra le entità elencate in hello **Progettazione tabelle**:

### <a name="tooedit-table-data"></a>dati della tabella tooedit
1. In hello **Progettazione tabelle**, aprire il menu di scelta rapida hello per un'entità (una singola riga) o una proprietà (una singola cella) e quindi scegliere **modifica**.
   
    ![Aggiunta o modifica di un'entità di tabella](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    Le entità in una singola tabella non sono necessari toohave hello stesso set di proprietà (colonne). Tenere hello presente seguenti restrizioni sulla visualizzazione e modifica dei dati della tabella.
   
   * I dati binari (tipo byte[]) non possono essere visualizzati o modificati, ma possono essere archiviati in una tabella.
   * Non è possibile modificare hello **PartitionKey** o **RowKey** valori, perché l'archiviazione tabelle di Azure non supporta questa operazione.
   * Una proprietà chiamata Timestamp non può essere creata perché una proprietà con quel nome è usata dai servizi di archiviazione di Azure.
   * Se si immette un valore DateTime, è necessario seguire un formato appropriato toohello paese e lingua delle impostazioni del computer (ad esempio gg/MM/aaaa hh.mm.ss [AM | PM] per gli Stati Uniti Stati Uniti).

### <a name="tooadd-entities"></a>entità tooadd
1. In hello **Progettazione tabelle**, scegliere hello **Aggiungi entità** pulsante.
   
    ![Aggiungi entità](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. In hello **Aggiungi entità** finestra di dialogo immettere i valori hello di hello **PartitionKey** e **RowKey** proprietà.
   
    ![Finestra di dialogo Aggiungi entità](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    Immettere i valori hello con attenzione perché non è possibile modificare dopo aver chiuso la finestra di dialogo hello, a meno che non si elimina entità di hello e aggiungerlo di nuovo.

### <a name="toofilter-entities"></a>entità toofilter
È possibile personalizzare il set di hello di entità che vengono visualizzati in una tabella se si utilizza il generatore di query hello.

1. Generatore di query tooopen hello, aprire una tabella per la visualizzazione.
2. Scegliere il pulsante Generatore di Query hello sulla barra degli strumenti della visualizzazione tabella hello.
   
    Hello **generatore di Query** viene visualizzata la finestra di dialogo. Hello nella figura seguente viene illustrata una query che viene generata in Generatore di query hello.
   
    ![Generatore di query](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. Quando si completa la creazione di query hello, chiudere la finestra di dialogo hello. Hello risultante in formato testo della query hello viene visualizzata una casella di testo come filtro di WCF Data Services.
4. hello toorun di query, scegliere l'icona del triangolo verde hello.
   
    È inoltre possibile filtrare i dati entità visualizzati in hello **Progettazione tabelle** se si immette una stringa di filtro di WCF Data Services direttamente nel campo filtro hello. Questo tipo di stringa è simile tooa clausola SQL WHERE, ma viene inviato al server toohello come una richiesta HTTP. Per informazioni su come tooconstruct stringhe di filtro, vedere [la costruzione di stringhe di filtro per Progettazione tabelle hello](https://msdn.microsoft.com/library/azure/ff683669.aspx).
   
    Hello nella figura seguente viene illustrato un esempio di una stringa di filtro valide:
   
    ![VST_SE_TableFilter](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a>Aggiornare i dati di archiviazione
Quando Esplora Server si connette tooor Ottiene dati da un account di archiviazione, operazione può richiedere minuto tooa per toocomplete operazione hello. Se non è possibile connettersi, operazione hello potrebbe scadere. Mentre i dati vengono recuperati, è possibile continuare toowork in altre parti di Visual Studio. operazione di hello toocancel se sta richiedendo troppo tempo, scegliere hello **Arresta aggiornamento** sulla barra degli strumenti Esplora Server hello.

#### <a name="toorefresh-blob-container-data"></a>dati del contenitore blob toorefresh
* Seleziona hello **BLOB** nodo sotto **archiviazione** scegliere hello **aggiornamento** sulla barra degli strumenti Esplora Server hello.
* toorefresh hello elenco di BLOB visualizzato, scegliere hello **Execute** pulsante.

#### <a name="toorefresh-table-data"></a>dati della tabella toorefresh
* Seleziona hello **tabelle** nodo sotto **archiviazione** scegliere hello **aggiornamento** pulsante.
* elenco hello toorefresh di entità che viene visualizzato in hello **Progettazione tabelle**, scegliere hello **Execute** pulsante hello **Progettazione tabelle**.

#### <a name="toorefresh-queue-data"></a>dati della coda toorefresh
* Seleziona hello **code** nodo, quindi scegliere hello **aggiornamento** pulsante.

#### <a name="toorefresh-all-items-in-a-storage-account"></a>toorefresh tutti gli elementi in un account di archiviazione
* Scegliere il nome di account hello e quindi scegliere hello **aggiornamento** sulla barra degli strumenti hello per Esplora Server.

### <a name="add-storage-accounts-by-using-server-explorer"></a>Aggiungere account di archiviazione usando Esplora server
Esistono due modi tooadd gli account di archiviazione tramite Esplora Server. È possibile creare un nuovo account di archiviazione nella sottoscrizione di Azure o è possibile collegare un account di archiviazione esistente.

#### <a name="toocreate-a-new-storage-account-by-using-server-explorer"></a>toocreate un nuovo account di archiviazione tramite Esplora Server
1. In Esplora Server, aprire il menu di scelta rapida hello per il nodo di archiviazione hello e quindi scegliere Crea Account di archiviazione.
   
    ![Creare un nuovo account di archiviazione di Azure](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. Selezionare o immettere le seguenti informazioni per hello nuovo account di archiviazione in hello hello **crea Account di archiviazione** la finestra di dialogo.
   
   * Hello desiderato di account di archiviazione hello tooadd toowhich di sottoscrizione di Azure.
   * Hello nome toouse per il nuovo account di archiviazione hello.
   * area di Hello o un gruppo di affinità (ad esempio Stati Uniti occidentali o Asia orientale).
   * Hello tipo di replica desiderato toouse hello account di archiviazione, ad esempio con ridondanza geografica.
3. Scegliere **Create**.
   
    viene visualizzato il nuovo account di archiviazione Hello in hello **archiviazione** elenco in Esplora soluzioni.

#### <a name="tooattach-an-existing-storage-account-by-using-server-explorer"></a>tooattach un account di archiviazione esistente mediante Esplora Server
1. In Esplora Server, aprire il menu di scelta rapida hello per il nodo di archiviazione di Azure hello e quindi scegliere **collega archiviazione esterna**.
   
    ![Aggiunta di un account di archiviazione esistente](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. Selezionare o immettere le seguenti informazioni per hello nuovo account di archiviazione in hello hello **crea Account di archiviazione** la finestra di dialogo.
   
   * nome Hello di hello esistente account di archiviazione da tooattach. È possibile immettere un nome o selezionarlo dall'elenco di hello.
   * chiave di Hello per hello selezionati account di archiviazione. Questo valore viene in genere immesso automaticamente quando si seleziona un account di archiviazione. Se si desidera chiave account di archiviazione hello tooremember di Visual Studio, selezionare hello memorizza account chiave.
   * Hello protocollo toouse tooconnect toohello account di archiviazione, ad esempio HTTP, HTTPS o un endpoint personalizzato. Vedere [come stringhe di connessione tooConfigure](https://msdn.microsoft.com/library/azure/ee758697.aspx) per ulteriori informazioni sugli endpoint personalizzati.

### <a name="tooview-hello-secondary-endpoints"></a>endpoint secondario di hello tooview
* Se è stato creato un account di archiviazione utilizzando hello **archiviazione con ridondanza geografica e accesso in lettura** opzione di replica, è possibile visualizzare gli endpoint secondari. Aprire il menu di scelta rapida hello per il nome di account hello e quindi scegliere **proprietà**.
  
    ![Endpoint secondari di archiviazione](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="tooremove-a-storage-account-from-server-explorer"></a>tooremove un account di archiviazione da Esplora Server
* In Esplora Server, aprire il menu di scelta rapida hello per il nome di account hello e quindi scegliere **eliminare**. Se si elimina un account di archiviazione, anche le informazioni sulla chiave salvate per tale account verranno rimosse.
  
  > [!NOTE]
  > Se si elimina un account di archiviazione da Esplora Server, non influisce su account di archiviazione o tutti i dati in esso inclusi. riferimento hello vengono semplicemente rimossi da Esplora Server. toopermanently eliminare un account di archiviazione, utilizzare hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).
  > 
  > 

## <a name="next-steps"></a>Passaggi successivi
toolearn informazioni su come utilizzare i servizi di archiviazione di Azure, vedere [l'accesso a servizi di archiviazione di Azure hello](https://msdn.microsoft.com/library/azure/ee405490.aspx).

