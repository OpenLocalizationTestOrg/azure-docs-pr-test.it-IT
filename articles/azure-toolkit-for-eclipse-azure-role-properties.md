---
title: "Proprietà ruolo aaaAzure"
description: Informazioni su come toouse hello Azure Toolkit per le impostazioni del ruolo Azure tooconfigure Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5c0ec412-5702-465a-8f47-87a8ce99a267
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: d111b4b9e4f12e49f38755bf6c9acc1a1de17a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-properties"></a>Proprietà del ruolo di Azure
All'interno di hello Azure Toolkit per Eclipse, è possono impostare varie impostazioni di configurazione per il ruolo di Azure.

## <a name="configuring-azure-role-properties"></a>Configurazione delle proprietà del ruolo di Azure
Configurazione delle proprietà del ruolo di Azure viene eseguita tramite le finestre di dialogo di hello proprietà per il ruolo di lavoro. Menu di scelta rapida aprire hello ruolo hello nel riquadro Esplora progetti di Eclipse e seleziona hello **Azure** sottomenu. (Se non viene visualizzato il ruolo di hello in hello Project Explorer di Eclipse, espandere il progetto in Project Explorer di Azure).

![][ic789599]

Hello varie proprietà che può essere impostata da hello **proprietà** le finestre di dialogo sono descritti in questo argomento. Si noti che molte proprietà vengono compilate automaticamente quando si crea un nuovo progetto di distribuzione di Azure.

Hello pagine delle proprietà seguenti sono disponibile per i ruoli Azure.

* [Proprietà della macchina virtuale](#virtual_machine_properties)
* [Proprietà di memorizzazione nella cache](#caching_properties)
* [Proprietà dei certificati](#certificates_properties)
* [Proprietà dei componenti](#components_properties)
<!-- * [Debugging properties](#debugging_properties) -->
* [Proprietà di endpoint](#endpoints_properties)
* [Proprietà di variabili di ambiente](#environment_variables_properties)
* [Proprietà di bilanciamento del carico/affinità di sessione (dette anche "sessioni permanenti")](#session_affinity_properties)
* [Proprietà di archiviazione locale](#local_storage_properties)
* [Proprietà di configurazione del server](#server_configuration_properties)
* [Proprietà di offload SSL](#ssl_offloading_properties)

<a name="virtual_machine_properties"></a>

### <a name="virtual-machine-properties"></a>Proprietà della macchina virtuale
Aprire hello menu di scelta rapida ruolo hello nel riquadro Project Explorer di Eclipse, fare clic su **Azure**, quindi fare clic su **proprietà**, e hanno dimensioni della macchina virtuale hello toochange possibilità hello e inoltre modificare numero di Hello di istanze, come illustrato nella seguente immagine hello.

![][ic719499]

> [!NOTE]
> Solo Windows: quando si imposta hello numero di istanze tooa valore maggiore di 1 e si configura anche un server applicazioni, hello toolkit consentirà solo 1 toorun di istanza di ruolo nell'emulatore di hello, indipendentemente da questa impostazione. Si tratta di conflitti di binding porta tooavoid tra istanze del server diverse hello (ad esempio, tutti durante il tentativo toobind tooport 8080) quando vengono eseguite su hello stesso computer. Il numero di istanze desiderato impostazione viene mantenuto, ma diventa effettiva solo quando si distribuisce toohello cloud.
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a>Proprietà di memorizzazione nella cache
Aprire hello menu di scelta rapida ruolo hello nel riquadro Project Explorer di Eclipse, fare clic su **Azure**, quindi fare clic su **la memorizzazione nella cache**. In questa finestra di dialogo è possibile abilitare cache con risorse condivise compatibile con memcache denominate, consentendo di velocità toohelp le applicazioni web.

![][ic719483]

All'interno di hello **la memorizzazione nella cache** pagina delle proprietà, è possibile specificare impostazioni globali per hello seguenti:

* Se è abilitata la memorizzazione nella cache con risorse condivise.
* dimensione della cache di Hello come percentuale della memoria.
* nome account di archiviazione Hello per salvare lo stato della cache di hello quando l'applicazione viene eseguita come un servizio cloud o none se non si desidera che lo stato della cache di hello toosave. (nome di account di archiviazione hello non è utilizzato quando si esegue l'applicazione nell'emulatore di calcolo hello.) Se si imposta nome di account di archiviazione hello troppo**(auto)** (ovvero predefinito hello), la configurazione di memorizzazione nella cache userà automaticamente hello stesso account di archiviazione, come quello selezionato in hello hello **pubblicare tooAzure**finestra di dialogo.

> [!NOTE]
> Hello **(auto)** impostazione avrà effetto hello desiderato solo se si pubblica la distribuzione utilizzando hello Eclipse toolkit pubblicazione guidata. Se invece si pubblica file con estensione cspkg hello manualmente tramite un meccanismo esterno, ad esempio hello [il portale di gestione di Azure][Azure Management Portal], distribuzione hello non funzionerà correttamente.
> 
> 

Hello seguente finestra di dialogo Visualizza le proprietà di hello per una cache.

![][ic719501]

* **Nome:** nome hello di hello cache con percorso condiviso.
* **Numero di porta:** hello toouse numero di porta per la cache di hello.
* **Criteri di scadenza:** uno di hello seguente i valori che specifica dopo la scadenza di una chiave nella cache di hello.
  * **Assoluto:** hello chiave scade quando hello ora specificata da **minuti toolive** viene raggiunto.
  * **NeverExpires:** hello key non dispone di un'ora di scadenza.
  * **SlidingWindow:** chiave hello scade se non ha ricevuto accessi per hello di tempo specificato da **minuti toolive**; ogni volta che è possibile accedervi, hello scadenza viene reimpostata.
* **Minuti toolive:** numero massimo di minuti per una chiave con memcache toolive, oggetto Criteri di scadenza toohello.
* **La disponibilità elevata con backup replicati in istanze del ruolo diverse:** se abilitata, questa opzione fornisce disponibilità elevata usando backup replicati in diverse istanze del ruolo. Si noti che almeno due istanze del ruolo devono essere attiva per la distribuzione toowork questa funzionalità.

tooadd una nuova cache, fare clic su hello **Aggiungi** pulsante hello **la memorizzazione nella cache** pagina delle proprietà e un **Configura Cache denominata** verrà aperta una finestra di dialogo. Fornire valori per le proprietà di hello descritte sopra.

toomodify una cache denominata, selezionare una cache di hello e fare clic su hello **modifica** pulsante hello **la memorizzazione nella cache** pagina delle proprietà. Verrà aperta una finestra di dialogo che consente di toomodify hello le proprietà della cache. Premere **OK** toosave i valori della cache di hello.

toodelete una cache, selezionare una cache di hello e fare clic su hello **rimuovere** pulsante hello **la memorizzazione nella cache** pagina delle proprietà e quindi fare clic su **Sì** eliminazione hello tooconfirm.

Per ulteriori informazioni su come toouse la memorizzazione nella cache, vedere [come tooUse con percorso condiviso Caching][How tooUse Co-located Caching].

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a>Proprietà dei certificati
Aprire hello menu di scelta rapida ruolo hello nel riquadro Project Explorer di Eclipse, fare clic su **Azure**, quindi fare clic su **certificati**.

![][ic710964]

In questa finestra di dialogo è possibile aggiungere o rimuovere i certificati a cui fa riferimento il progetto Eclipse. Si noti che i certificati di hello elencati di seguito non vengono automaticamente archiviati in qualsiasi keystore Java e pertanto non sono automaticamente disponibili per l'uso in un'applicazione Java. Vengono registrati solo con Azure in modo da poter essere precaricati in hello Windows certificato archiviare nelle macchine virtuali hello esegue la distribuzione e successivamente utilizzato da altri software Windows. Attualmente, hello solo funzionalità di hello toolkit che usa certificati hello a cui fa riferimento in questo modo nella hello **certificati** finestra di dialogo [offload SSL][SSL Offloading], perché tooits Internet Information Services (IIS) e Application Request Routing (ARR), che richiedono l'affidabilità hello toobe certificato appropriato resi disponibili in questo modo.

Quando si distribuisce il tooAzure progetto utilizzare hello pubblicazione guidata, sarà richiesta toopoint in hello Exchange PFX (Personal Information) file corrispondenti certificati toothese, e le relative password, in ordine tooautomatically caricarli toohello Servizio di Azure, ma solo se si sono non stati caricati in precedenza.

<a name="components_properties"></a> 

### <a name="components-properties"></a>Proprietà dei componenti
Aprire hello menu di scelta rapida ruolo hello nel riquadro Project Explorer di Eclipse, fare clic su **Azure**, quindi fare clic su **componenti**. In questa finestra di dialogo è hanno hello possibilità tooadd, modificare, o rimuovere componenti hello del ruolo, nonché modificare l'ordine di hello in cui vengono elaborati.

![][ic719502]

funzionalità di componenti Hello consente tooadd dipendenze tooyour progetto di distribuzione Azure, ad esempio progetti di applicazioni Java, file speciali e istruzioni a riga di comando eseguibile che sono necessari per la distribuzione.

Per ogni componente, è possibile specificare:

* Hello toobe di passaggio eseguito durante l'importazione componente hello nel progetto di distribuzione di Azure durante la compilazione.
* toobe di passaggio Hello attenzione quando si distribuisce il componente nel cloud di Azure hello.

> [!NOTE]
> Quando si specificano i file di componenti o le righe di comando, tenere presente che la distribuzione sarà pubblicato tooa macchina virtuale di Windows, pertanto le procedure personalizzate devono essere valide per un sistema operativo basato su Windows. 
> 
> 

I componenti sono hello le proprietà seguenti:

* **Importazione:** metodo che indica la modalità di importazione componente hello nel progetto hello quando hello progetto viene compilato. Può trattarsi di uno dei seguenti valori hello:
  * **copia:** hello componente viene copiato dal percorso locale di hello specificato hello **da** proprietà del ruolo hello **approot** directory.
  * **Sporgenza:** componente hello è un file Java enterprise archive (EAR) importato da un progetto di applicazione Enterprise nel percorso locale di hello specificato da hello **da** proprietà. (Ciò viene rilevata automaticamente dal toolkit hello in base hello natura del progetto hello in tale posizione).
  * **File JAR:** componente hello è un file Java archive (JAR) e viene importato da un progetto Java nel percorso locale di hello specificato da hello **da** proprietà. (Ciò viene rilevata automaticamente dal toolkit hello in base hello natura del progetto hello in tale posizione).
  * **None:** componente hello tooimport non viene eseguita alcuna azione. Questa opzione è disponibile quando si presuppone che il componente hello tooalready essere presente nel ruolo di hello **approot** directory, oppure quando il componente hello è semplicemente un'istruzione eseguibile riga di comando, come specificato in hello **come**proprietà quando hello **Distribuisci** metodo **exec**.
  * **WAR:** componente hello è un file Java web application archive (WAR) e viene importato da un progetto Web dinamico nel percorso locale di hello specificato da hello **da** proprietà. (Ciò viene rilevata automaticamente dal toolkit hello in base hello natura del progetto hello in tale posizione).
  * **zip:** componente hello è un file zip e viene importato da compressione directory hello o il file specificato da hello **da** proprietà.
* **Da:** percorso di origine nei file che rappresenta la distribuzione di hello elementi tooimport tooyour cartella toohello computer locale. In questa proprietà è possibile usare variabili di ambiente di Windows. Tutti i componenti importabili verranno importati nel ruolo di hello **approot** directory quando viene compilato il progetto hello.
  
    Si noti che è necessario hello possibilità toodeploy un componente da un download durante la distribuzione cloud toohello (non emulatore di calcolo di hello). Vedere le informazioni correlate seguenti sull'aggiunta di un componente.    
* **Esempio:** nome di File in cui hello componente verrà importato del ruolo hello **approot** directory e infine distribuito nel cloud di Azure hello. Lasciare questo tookeep vuoto proprietà hello hello nome corrisponde a quello è nel computer locale hello. (Per i componenti eseguibili, vale a dire quelli il cui **Distribuisci** il metodo è stato impostato troppo**exec**, può trattarsi di un'istruzione di riga di comando di Windows arbitraria.)
  
  > [!IMPORTANT]
  > Se si utilizzano i caratteri di spazio per questo valore, verranno gestiti in modo diverso a seconda di hello metodo di distribuzione. Se il metodo di distribuzione hello è **exec**, gli spazi verranno interpretati come separatori di argomento della riga di comando e non come parte del nome file hello. Per tutti gli altri metodi di distribuzione, gli spazi verranno interpretati come parte del nome file hello.
  > 
  > 
* **Distribuire:** metodo che indica l'azione di hello applicato toohello componente quando viene avviata la distribuzione di hello. Può trattarsi di uno dei seguenti valori hello:
  
  * **copia:** componente hello è il percorso di destinazione copiato toohello specificato da hello **a** proprietà.
  * **EXEC:** componente hello è un'istruzione di riga di comando di Windows eseguibile eseguita nel contesto di hello del percorso hello specificato da hello **a** proprietà in fase di hello hello distribuzione viene avviata.
  * **None:** alcuna azione non viene applicata toohello componente all'avvio di distribuzione hello.
  * **zip:** componente hello è decompresso toohello percorso di destinazione specificato da hello **a** proprietà. Questo metodo è disponibile solo quando hello **importazione** proprietà **zip**.
* **A:** percorso di destinazione nella macchina virtuale hello in cui verrà distribuito il componente di hello. In questa proprietà è possano usare variabili di ambiente Windows e i percorsi dei file sono correlati troppo**approot**.

tooadd un nuovo componente, fare clic su hello **Aggiungi** pulsante hello **componenti** pagina delle proprietà e un **componente ruolo Azure** verrà aperta una finestra di dialogo. Fornire valori per le proprietà di hello descritte sopra. 

Hello seguito è riportato un esempio per l'aggiunta di un nuovo componente WAR.

![][ic719503]

Quando si distribuiscono toohello cloud (non hello emulatore di calcolo), se si desidera che il componente hello toodeploy da un download, assicurarsi che **nel cloud anziché includere nel pacchetto di hello, eseguire la distribuzione da** è selezionata. Se si desidera toodownload dall'account di archiviazione di Azure, selezionare l'account di archiviazione hello da hello **account di archiviazione** riepilogo (è possibile fare clic su hello **account** collegamento toomodify novità nell'elenco di hello), che compilerà parzialmente hello **URL** campo, quindi compilare la restante parte dell'URL hello hello. Se non si desidera toouse archiviazione di Azure, selezionare **(nessuno)** da hello **account di archiviazione** elenco a discesa elenco e immettere componente tooyour di URL hello in hello **URL** campo. Specificare uno dei seguenti metodi hello:

* **copia:** il componente di download di hello è il percorso di destinazione copiato toohello specificato da hello **tooDirectory** percorso.
* **stesso:** hello stesso metodo utilizzato per **distribuzione da download** per **distribuzione da pacchetto**.
* **zip:** il componente di download di hello viene decompresso toohello percorso di destinazione specificato da hello **tooDirectory** percorso.

toomodify hello di componente e fare clic su un componente, selezionare hello **modifica** pulsante hello **componenti** pagina delle proprietà. Verrà aperta una finestra di dialogo che consente di toomodify hello proprietà del componente. Premere **OK** toosave i valori dei componenti hello.

toodelete hello di componente e fare clic su un componente, selezionare hello **rimuovere** pulsante hello **componenti** pagina delle proprietà e quindi fare clic su **Sì** eliminazione hello tooconfirm.

I componenti vengono elaborati in ordine di hello elencati. Hello utilizzare **Sposta su** e **Sposta giù** pulsanti ordine hello tooarrange.

> [!NOTE]
> funzionalità di configurazione del server Hello si basa sui componenti anche. Impossibile rimuovere o modificare senza rimozione della configurazione di server corrispondente hello tali componenti. Verrà richiesto informazioni durante il tentativo di toomake modifiche toosuch componenti.
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have hello ability tooenable or disable remote debugging, as well as create debug configurations, as shown in hello following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a>Proprietà di endpoint
Aprire hello menu di scelta rapida ruolo hello nel riquadro Project Explorer di Eclipse, fare clic su **Azure**, quindi fare clic su **endpoint**. In questa finestra di dialogo dispone di un endpoint, hello possibilità toocreate, nonché modificare o rimuovere un endpoint, come illustrato nella seguente immagine hello.

![][ic719505]

tooadd un endpoint, fare clic su hello **Aggiungi** pulsante hello **endpoint** pagina delle proprietà e un **Aggiungi Endpoint** verrà aperta una finestra di dialogo.

![][ic710897]

Immettere un nome per l'endpoint di hello, selezionare il tipo di hello (entrambi **Input**, **interno**, o **InstanceInput**) e specificare una porta pubblica e privata hello. Premere **OK** toosave hello nuovi valori dell'endpoint.

In base al tipo di hello di endpoint, è possibile utilizzare gli intervalli di porte come indicato di seguito:

* Per un endpoint dell'istanza di input, la porta pubblica di hello può essere un intervallo di porte (ad esempio **2000-2010**) e porta privata hello è un valore fisso.
* Per un endpoint interno, la porta pubblica hello non viene usata e la porta privata hello può essere un intervallo vuoto o set tooan asterisco tooindicate che viene impostato automaticamente da Azure.
* Per gli endpoint di input, la porta pubblica hello può essere solo un valore fisso e porta privata hello può essere un valore fisso, vuoto o set tooan asterisco tooindicate che viene impostato automaticamente da Azure.

Se si desidera toouse un solo numero di porta anziché un intervallo, lasciare vuota la casella di testo hello per entità finale dell'intervallo di hello hello.

Per le porte tooautomatic set, se è necessario toodetermine la porta effettivamente utilizzata in fase di esecuzione, l'applicazione può utilizzare l'API di Runtime del servizio Azure, è documentato in hello hello [com.microsoft.windowsazure.serviceruntime pacchetto riepilogo][com.microsoft.windowsazure.serviceruntime package summary].

<!-- toosee how instance input endpoints can be used toohelp with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

toomodify un endpoint, selezionare l'endpoint hello e fare clic su hello **modifica** pulsante hello **endpoint** pagina delle proprietà. Verrà aperta una finestra di dialogo in cui è il nome dell'endpoint toomodify hello e tipo porte pubbliche e private. Premere **OK** toosave hello modificato i valori di endpoint.

toodelete un endpoint, selezionare l'endpoint hello e fare clic su hello **rimuovere** pulsante hello **endpoint** pagina delle proprietà e quindi fare clic su **Sì** eliminazione hello tooconfirm.

In ordine tooproperly configurare alcune funzionalità di hello (ad esempio, la memorizzazione nella cache, l'affinità di sessione o SSL offloading) abilitata dall'utente hello in un ruolo, hello toolkit può configurare automaticamente gli endpoint speciali che verranno elencati con gli endpoint definiti dall'utente. Hello toolkit impedisce utente hello di modificare o eliminare tali endpoint generati automaticamente, purché hello associata funzionalità è abilitata.

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a>Proprietà di variabili di ambiente
Aprire hello menu di scelta rapida ruolo hello nel riquadro Project Explorer di Eclipse, fare clic su **Azure**, quindi fare clic su **le variabili di ambiente**. In questa finestra di dialogo sono hello possibilità toocreate una variabile di ambiente, nonché modificare o rimuovere una variabile di ambiente, come illustrato nella seguente immagine hello.

![][ic719506]

Variabili di ambiente sono script di avvio tooyour disponibile all'avvio ruolo hello.

> [!NOTE]
> Quando si specificano le variabili di ambiente, tenere presente che la distribuzione sarà pubblicato tooa macchina virtuale di Windows, pertanto le variabili di ambiente devono essere valide per un sistema operativo basato su Windows.
> 
> 

Un esempio di una variabile di ambiente sono disponibili all'avvio hello ruolo, creare una nuova variabile di ambiente facendo hello **Aggiungi** pulsante. Hello seguente illustra la variabile di ambiente denominata **MyRoleVersion** viene creato e assegnato il valore di hello **1.0**.

![][ic659268]

All'interno del codice jsp è possibile visualizzare il valore di hello utilizzando hello `System.getenv` metodo:

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

Questo è l'output risultante quando viene eseguita l'applicazione:

![][ic552233]

toomodify una variabile di ambiente, selezionare la variabile di ambiente hello e fare clic su hello **modifica** pulsante hello **le variabili di ambiente** pagina delle proprietà. Verrà aperta una finestra di dialogo consentendo si toomodify hello ambiente proprietà delle variabili. Premere **OK** valori delle variabili toosave hello ambiente.

toodelete una variabile di ambiente, selezionare la variabile di ambiente hello e fare clic su hello **rimuovere** pulsante hello **le variabili di ambiente** pagina delle proprietà e quindi fare clic su **Sì**eliminazione hello tooconfirm.

In ordine tooproperly configurare alcune funzionalità di hello (ad esempio di configurazione del Server, il debug remoto o l'archiviazione locale) abilitata dall'utente hello in un ruolo, hello toolkit può configurare automaticamente le variabili di ambiente speciali che verranno elencate insieme a variabili di ambiente definita dall'utente. Hello toolkit impedisce utente hello di modificare o eliminare tali variabili di ambiente generate automaticamente purché hello associata funzionalità è abilitata.

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a>Proprietà di bilanciamento del carico/affinità di sessione (dette anche "sessioni permanenti")
Aprire hello menu di scelta rapida ruolo hello nel riquadro Project Explorer di Eclipse, fare clic su **Azure**, quindi fare clic su **il bilanciamento del carico**. In questa finestra di dialogo sono hello possibilità tooenable o disabilitare l'affinità di sessione, come illustrato nella seguente immagine hello.

![][ic719492]

Per informazioni correlate, vedere [Affinità di sessione][Session Affinity]. Si noti inoltre il comportamento della funzionalità nel contesto di hello di offload SSL, come descritto in [offload SSL][SSL Offloading].

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a>Proprietà di archiviazione locale
Aprire hello menu di scelta rapida ruolo hello nel riquadro Project Explorer di Eclipse, fare clic su **Azure**, quindi fare clic su **archiviazione locale**. In questa finestra di dialogo sono hello possibilità toocreate, modificare o rimuovere spazio di archiviazione locale temporanea per la macchina virtuale hello che esegue l'applicazione. Valori specifici possono essere impostati per le dimensioni di hello di archiviazione locale di hello, anche se il contenuto di hello viene mantenuto quando il ruolo di hello viene riciclato, come illustrato nella seguente immagine hello.

![][ic719508]

È anche possibile specificare una variabile di ambiente corrispondente toohello di archiviazione locale.

Per impostazione predefinita, tutto ciò che si distribuiscono in Azure viene inserito (e decompressi) in hello **approot** cartella dell'istanza del ruolo hello. Mentre la maggior parte delle distribuzioni semplici dimensioni della cartella sono anche dopo la decompressione, spazio hello allocato per hello **approot** directory è limitato e non ben definito (minore di 1 GB è una regola empirica ragionevole). Pertanto, tooensure Azure alloca spazio su disco sufficiente per le distribuzioni di dimensioni maggiori che potrebbero non rientrare nella hello **approot** cartella, è necessario configurare una risorsa di archiviazione locale tramite hello **archiviazione locale** finestra di dialogo. Per un toodo facilmente questa operazione, vedere [distribuzione grandi distribuzioni][Deploying Large Deployments].

È possibile fare riferimento la risorsa di archiviazione hello dagli script di avvio (ad esempio, il **startup.cmd**) utilizzando variabile di ambiente hello associata automaticamente dal toolkit di Eclipse hello risorsa hello, come illustrato nel hello  **Archiviazione locale** finestra di dialogo. Tale variabile di ambiente conterrà percorso completo di hello di aver configurato in fase di hello che script di avvio viene eseguito la risorsa locale hello. 

toomodify una risorsa di archiviazione locale, selezionare la risorsa di archiviazione locale hello e fare clic su hello **modifica** pulsante hello **archiviazione locale** pagina delle proprietà. Verrà aperta una finestra di dialogo che consente di toomodify hello archiviazione locale le proprietà delle risorse. Premere **OK** valori della risorsa di archiviazione locale hello toosave.

toodelete una risorsa di archiviazione locale, selezionare la risorsa di archiviazione locale hello e fare clic su hello **rimuovere** pulsante hello **archiviazione locale** pagina delle proprietà e quindi fare clic su **Sì** eliminazione di hello tooconfirm.

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a>Proprietà di configurazione del server
Aprire hello menu di scelta rapida ruolo hello nel riquadro Project Explorer di Eclipse, fare clic su **Azure**, quindi fare clic su **configurazione Server**. In questa finestra di dialogo è hello possibilità tooadd, rimuovere, modificare hello JDK e server applicazioni Java usati dalla distribuzione, nonché aggiungere o rimuovere applicazioni hello (ad esempio file WAR, JAR o EAR) usate dalla distribuzione.

### <a name="jdk-configuration"></a>Configurazione di JDK
Questa finestra di dialogo consente toospecify hello JDK package toouse per la distribuzione. Se si usa Eclipse in Windows, è possibile specificare hello JDK package toouse localmente quando in esecuzione in hello dell'emulatore di Azure e si dispone di hello opzione toodeploy tooAzure tale installazione locale. Nei sistemi operativi non Windows, impostazione di JDK come emulatore hello non è applicabile e non è possibile distribuire hello localmente installato JDK perché non è compatibile con Windows. Tuttavia, indipendentemente dal sistema operativo di hello in uso, è sempre possibile tra hello 3rd party JDK package toodeploy tooAzure o puntare al proprio pacchetto JDK compatibile con Windows da un percorso di download alternativo.

Hello Ecco un esempio di come è possibile specificare un pacchetto JDK in Windows:

![][ic780647]

Se si usa Eclipse in Windows, è possibile specificare un toouse JDK con hello; emulatore di calcolo In tal caso, assicurarsi di toodo **hello Usa JDK da questo percorso di file per test locale** hello viene archiviato **distribuzione emulatore** sezione. Quindi, specificare il percorso locale di hello tooyour JDK; è possibile esplorare toodifferent JDK se hello quello che si desidera toouse non è selezionato automaticamente. È inoltre hello opzione toodeploy il tooyour JDK servizio cloud di Azure. toodo in tal caso, selezionare hello **distribuire JDK locale (caricamento automatico toocloud archiviazione)** opzione hello **distribuzione Cloud** sezione.

Nota: Nei sistemi operativi non Windows, hello **distribuzione emulatore** hello e impostazioni **distribuire JDK locale** opzione non sono disponibili. Hello esempio seguente viene illustrato come specificare un pacchetto JDK in un Mac o altro supporto del sistema operativo non Windows:

![][ic789643]

Indipendentemente dal sistema operativo hello trovano in, si dispone di hello seguenti due **distribuzione Cloud** opzioni per l'origine hello e il tipo del pacchetto JDK:

* **Deploy a 3rd party JDK package available on Azure** 
* **Deploy from a custom download** 

Se si utilizza hello **distribuire un pacchetto 3rd party JDK disponibile in Azure** opzione:

1. Casella di controllo hello denominato **distribuire un pacchetto 3rd party JDK disponibile in Azure**.
2. Dall'elenco a discesa hello, selezionare hello 3rd party JDK pacchetto è disponibile in Azure.
3. Il **JDK** scheda avrà un aspetto simile toohello seguente in Windows: ![][ic780648] e avrà un aspetto simile toohello seguenti su Mac OS o altri sistemi operativi Windows non è supportato:![][ic789643]
4. Fare clic su **OK** toosave le modifiche.
5. Quando richiesto tooaccept hello contratto di licenza dal provider di hello 3rd party JDK package, esaminare condizioni di licenza hello. Supponendo che si accettino i termini di hello, fare clic su **Sì** tooclose hello **accettare il contratto di licenza** finestra di dialogo.
    Si noti che hello sottostante la logica per il quale gli elementi vengono visualizzati nell'elenco a discesa hello hello **distribuire un pacchetto 3rd party JDK disponibile in Azure** opzione può essere personalizzato. hello elementi hello toocustomize **JDK** finestra di dialogo, fare clic su hello **Personalizza** collegamento. Verrà chiusa hello **JDK** pagina delle proprietà e aprire hello **componentsets.xml** file in Eclipse, che è quindi possibile modificare in base alle esigenze. Documentazione per **componentsets.xml** è incluso in hello **componentsets.xml** file stesso.

Se si utilizza hello **distribuire un pacchetto JDK da un download personalizzato** opzione:

1. Creare un file ZIP della directory di installazione di JDK, assicurandosi che hello nodo della directory è figlio di hello hello ZIP struttura e non il relativo contenuto. Prendere nota del nome di hello della directory di hello, sarà necessaria in seguito, quindi tenere presente questo JDK installazione sarà distribuito tooa macchina virtuale di Windows.
2. Caricare hello ZIP nell'account di archiviazione di Azure come blob. È possibile farlo tramite uno strumento disponibile esternamente per il caricamento dei blob tooAzure archiviazione. È consigliabile toouse un blob privato. Prendere nota dell'URL blob hello del contenuto di hello ZIP.
3. Casella di controllo hello denominato **distribuire un pacchetto JDK da un download personalizzato**.
    Se si desidera toodownload dall'account di archiviazione di Azure, selezionare l'account di archiviazione hello da hello **account di archiviazione** riepilogo (è possibile fare clic su hello **account** collegamento toomodify novità nell'elenco di hello), che compilerà parzialmente hello **URL** campo, quindi compilare la restante parte dell'URL hello hello. Se non si desidera toouse archiviazione di Azure, selezionare **(nessuno)** da hello **account di archiviazione** elenco a discesa elenco, quindi immettere hello URL tooyour download JDK nel hello **URL** campo. Se si utilizza l'archiviazione di Azure, i nomi di blob nell'URL hello devono essere minuscoli.
4. Verificare che hello **JAVA_HOME** textbox fa riferimento il nome di directory corretta toohello. Per impostazione predefinita, questo farà riferimento hello stesso nome di directory JDK come valore di hello scelto per l'uso locale. Tuttavia, se la directory hello contenuta in hello ZIP dispone di un nome diverso (ad esempio, scadenza toousing una versione diversa), nome di directory aggiornamento hello in hello **JAVA_HOME** casella di testo di conseguenza, poiché questo valore verrà utilizzato in hello cloud ( non nell'emulatore di calcolo hello).
5. Fare clic su **OK** toosave le modifiche.

È tutto. A questo punto, quando si compila per cloud hello, si noterà dimensioni pacchetto di hello saranno molto più piccola, il processo di compilazione hello richiederà in genere meno tempo e la distribuzione di hello quando si pubblica toohello cloud deve anche richiedere meno tempo. Si noti che hello **distribuire JDK locale (caricamento automatico toocloud archiviazione)** o **distribuire un pacchetto JDK da un download personalizzato** opzioni sono attive solo quando l'applicazione viene distribuita nel cloud hello. Non hanno alcun effetto sulle esperienze di emulatore di calcolo; versione locale di Hello dei componenti di hello verrà comunque utilizzato quando si distribuisce l'emulatore di calcolo toohello. 

### <a name="server-configuration"></a>Configurazione del server
Hello Ecco un esempio di come è possibile specificare un server applicazioni.

![][ic796926]

Verificare che hello **distribuire un server di questo tipo** casella di controllo è selezionata e quindi scegliere il tipo di hello del server applicazioni desiderato toouse.

Per specificare un toouse server per la distribuzione cloud, è possibile sfruttare hello le opzioni seguenti:

1. **Distribuire un server di terze parti 3rd disponibile in Azure** -questo vale in particolare in scenari di sviluppo/test in cui l'efficienza di distribuzione e la semplicità è una priorità e non è necessaria una configurazione personalizzata server hello. O quando si desidera toouse uno di questi server come punto di partenza hello ma includono i passaggi di personalizzazione del server appropriato nella logica di avvio della distribuzione.
2. **Distribuire da un download personalizzato** -questo vale in particolare negli scenari di produzione quando si dispone di un server appositamente preparato e configurato che si desidera toouse nel cloud hello.
3. **Deploy my local server installation** : questa opzione è applicabile in particolare se l'installazione del server locale è già configurata in modo personalizzato per l'uso. Se si sceglie questa opzione, è necessario specificare anche il percorso del server locale in hello **percorso server locale** casella di testo sottostante.

Se si utilizza hello **distribuire un server di terze parti 3rd disponibile in Azure** opzione:

1. Casella di controllo hello denominato **distribuire un server di terze parti 3rd disponibile in Azure**.
2. Scegliere dal menu a discesa hello toouse di software server desiderato hello con la distribuzione nel cloud hello. Si noti che se è stato specificato un tipo di server toouse in precedenza, sarà possibile toochoosing limitato solo un server cloud in hello stessa famiglia di quel tipo di server. Tuttavia, se non si è scelto un tipo di server, è possibile scegliere tra uno qualsiasi dei server hello che sono attualmente disponibili in Azure e il tipo di server hello verrà selezionato automaticamente per l'utente.
3. Fare clic su **OK** toosave le modifiche.

Se si utilizza hello **Distribuisci da un download personalizzato** opzione:

1. Assicurarsi di aver già selezionato un tipo di server in base toohello passaggi precedenti. In questo modo hello di plug-in modalità server hello toodeploy dal download personalizzato, che deve essere da hello stessa famiglia del tipo di server selezionato.
2. Casella di controllo hello denominato **Distribuisci da un download personalizzato**.
    Se si desidera toodownload dall'account di archiviazione di Azure, selezionare l'account di archiviazione hello da hello **account di archiviazione** riepilogo (è possibile fare clic su hello **account** collegamento toomodify novità nell'elenco di hello), che compilerà parzialmente hello **URL** campo e compilare la restante parte dell'URL del server di tooyour hello hello download del file ZIP (quando l'utilizzo di archiviazione di Azure, i nomi di blob nell'URL hello deve essere minuscola). Se non si desidera toouse archiviazione di Azure, selezionare **(nessuno)** da hello **account di archiviazione** elenco a discesa elenco e immettere il download hello URL tooyour server ZIP in hello **URL** campo. Hello ZIP conterrebbe una cartella figlio che rappresenta la directory di installazione dell'applicazione server. Ad esempio, se si utilizza un file zip per Apache Tomcat 7.0.35, all'interno di hello zip sarà hello figlio cartella che rappresentano hello directory di installazione, ad esempio **apache tomcat-7.0.35**. 
3. Specificare il valore di hello hello home directory variabile di ambiente. Verrà aperta toohello usata per il server applicazioni locale, se presente, ma è possibile specificare un valore diverso se il server applicazioni cloud è diverso dal server applicazioni locale. Tuttavia, è necessario che sia il server applicazioni cloud di hello toomake stessa famiglia hello tipo di server selezionato in precedenza.
    Se si aggiorna il codice postale del server applicazioni cloud in hello future, è possibile modificare manualmente impostazione della home directory hello o toohave corrisponda nuovamente all'impostazione locale (se è stato modificato anche il server applicazioni locale).
4. Fare clic su **OK** toosave le modifiche.

Hello sottostante la logica per il quale gli elementi vengono visualizzati in hello **Server** scheda di hello **configurazione Server** pagina delle proprietà può essere personalizzata. Si tratta di una funzionalità avanzata che potrebbe essere necessario se le proprie esigenze si estendono oltre i valori predefiniti di hello o se si desidera tooadd altri server. hello logica hello toocustomize **Server** finestra di dialogo, fare clic su hello **Personalizza** collegamento. Verrà chiusa hello **configurazione Server** pagina delle proprietà e aprire hello **componentsets.xml** file in Eclipse, che è quindi possibile modificare come modello di configurazione server hello tooextend necessari. Documentazione per **componentsets.xml** è incluso in hello **componentsets.xml** file stesso.

Se si utilizza hello **distribuire un server locale (caricamento automatico toocloud archiviazione)** opzione:

1. Casella di controllo hello denominato **distribuire un server locale (caricamento automatico toocloud archiviazione)**.
2. Utilizzo di hello **account di archiviazione** elenco a discesa, seleziona **(auto)**. Se si specifica **(auto)** qui, hello Eclipse toolkit utilizzerà hello stesso account di archiviazione per il server come hello quello selezionato per la distribuzione di hello **pubblicare tooAzure** finestra di dialogo.
3. Fare clic su **OK** toosave le modifiche.

Selezionare un percorso di installazione del server nel computer in uso in hello **percorso server locale** casella di testo se si verifica una delle seguenti condizioni hello:

* Si desidera tootest la distribuzione nell'emulatore hello (si applica solo a tooWindows).
* Si desidera toodeploy cloud toohello server installato localmente.
* Si desidera toouse un download server personalizzato nel cloud hello, nel qual caso, assicurarsi inoltre di hello **distribuire un server locale (caricamento automatico toocloud archiviazione)** opzione è selezionata in precedenza.

Se nessuna delle precedenti opzioni hello applica tooyour situazione, impostazioni del server locale hello sono facoltativo.

### <a name="applications-configuration"></a>Configurazione di applicazioni
Hello Ecco un esempio di come è possibile specificare un'applicazione.

![][ic719512]

Fare clic su **Aggiungi** tooadd un'altra applicazione, o **rimuovere** tooremove un'applicazione. Per motivi di efficienza, se si desidera toouse un download per l'origine di hello di un'applicazione durante la distribuzione cloud toohello, utilizzare hello [proprietà dei componenti](#components_properties) toospecify un URL, account di archiviazione e così via. 

A partire dalla versione di aprile 2014 hello, le applicazioni vengono caricate automaticamente nello hello stesso account di archiviazione (in hello **eclipsedeploy** contenitore) come hello selezionato per la distribuzione. logica di avvio Hello della distribuzione contiene un passaggio che prima di scaricare le applicazioni dall'account di archiviazione. Ciò significa che è possibile aggiornare le applicazioni nella distribuzione senza la necessità di toorebuild e ridistribuire l'intero pacchetto hello, caricando manualmente le versioni più recenti di un'applicazione hello direttamente nell'account di archiviazione (tramite, ad esempio hello portale di Azure) , sostituendo i file WAR hello originariamente caricati dal toolkit hello. Iniziare quindi semplicemente hello riciclo di tutte le istanze del ruolo tramite il portale di gestione di Azure nuovo o tramite l'utilità della riga di comando. (Attivare il riciclo del ruolo direttamente in hello Eclipse toolkit non è attualmente supportato.)

### <a name="notes-about-server-configuration"></a>Note sulla configurazione del server
Le modifiche apportate mediante hello **configurazione Server** pagina delle proprietà vengono riflesse in hello `<component>` elementi del file package.xml hello.

Quando si utilizza hello **caricamento automatico...**  o **distribuzione da download...**  opzioni per JDK hello o server applicazioni e si esegue la compilazione per il cloud hello (non hello emulatore di calcolo) e si è connessi toohello rete, è possibile riscontrare i messaggi di compilazione come segue hello nell'output di Console hello, come hello Ant Generatore di verifica della disponibilità del download hello:

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

Se si seleziona hello **distribuzione da download...**  opzione hello seguente avviso potrebbe essere visualizzato, ma hello compilazione continuerà:

`[windowsazurepackage] warning: Failed tooconfirm blob availability! Make sure hello URL and/or hello access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

Questo avviso è hello unica indicazione hello disponibilità del download non è stata verificata. Pertanto se un errore di distribuzione nel cloud hello per qualche motivo, controllare toosee se si è ricevuto questo avviso.

Se si desidera verifica del download hello toodisable (ad esempio, se si ritiene che rallenti inutilmente la compilazione di hello), hello impostare `verifydownloads` attributo troppo`false` in hello `<windowsazurepackage>` elemento del file package.xml: 

`<windowsazurepackage verifydownloads="false" ...>` 

Se si seleziona hello **caricamento automatico...**  opzione, nella finestra di console hello si vedrà reporting hello lo stato di avanzamento del caricamento hello ogni 5 secondi, ogni volta che un'operazione di caricamento di messaggi di compilazione.

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a>Proprietà di offload SSL
Aprire hello menu di scelta rapida ruolo hello nel riquadro Project Explorer di Eclipse, fare clic su **Azure**, quindi fare clic su **offload SSL**. 

![][ic719481]

In questa finestra di dialogo è possibile abilitare SSL offloading, consentono di abilitare tooeasily Hypertext Transfer Protocol Secure (HTTPS) supportano nella distribuzione Java in Azure, senza la necessità di tooconfigure SSL nel server applicazioni Java. Per ulteriori informazioni, vedere [offload SSL] [ SSL Offloading] e [come tooUse offload SSL][How tooUse SSL Offloading].

## <a name="see-also"></a>Vedere anche
[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]

[L'installazione di hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse]

[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Proprietà del progetto Azure][Azure Project Properties]

[Elenco di account di archiviazione di Azure][Azure Storage Account List]

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Project Properties]: http://go.microsoft.com/fwlink/?LinkID=699524
[Azure Storage Account List]: http://go.microsoft.com/fwlink/?LinkID=699528
[com.microsoft.windowsazure.serviceruntime package summary]: http://azure.github.io/azure-sdk-for-java/com/microsoft/windowsazure/serviceruntime/package-summary.html
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debugging a specific role instance in a multi-instance deployment]: http://go.microsoft.com/fwlink/?LinkID=699535#debugging_specific_role_instance
[Debugging Azure Applications in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Deploying Large Deployments]: http://go.microsoft.com/fwlink/?LinkID=699536
[How tooUse Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How tooUse SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699549

<!-- IMG List -->

[ic789599]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789599.png
[ic719499]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719499.png
[ic719483]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719483.png
[ic719501]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719501.png
[ic710964]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710964.png
[ic719502]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719502.png
[ic719503]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719503.png
[ic719504]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719504.png
[ic719505]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719505.png
[ic710897]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710897.png
[ic719506]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719506.png
[ic659268]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic659268.png
[ic552233]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic552233.png
[ic719492]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719492.png
[ic719508]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719508.png
[ic780647]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780647.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic780648]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780648.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic796926]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic796926.png
[ic719512]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719512.png
[ic719481]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719481.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690945.aspx -->
