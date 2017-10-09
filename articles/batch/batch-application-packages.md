---
title: pacchetti di applicazioni aaaInstall sui nodi di calcolo - Azure Batch | Documenti Microsoft
description: "Funzionalità di pacchetti dell'applicazione hello uso di Azure Batch tooeasily gestire più applicazioni e nodi di calcolo di versioni per l'installazione nel Batch."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a>Distribuire i nodi toocompute di applicazioni con pacchetti di applicazione di Batch

funzionalità di pacchetti di applicazione Hello del Batch di Azure consente una gestione semplificata delle applicazioni di attività e i relativi toohello distribuzione nodi di calcolo nel pool di. Con i pacchetti di applicazioni, è possibile caricare e gestire più versioni di applicazioni hello che eseguire le attività, inclusi i relativi file di supporto. È possibile quindi distribuire automaticamente uno o più di queste applicazioni toohello nodi di calcolo nel pool di.

In questo articolo si apprenderà come tooupload e gestire i pacchetti di applicazione nel portale di Azure hello. Si apprenderà quindi come tooinstall in un pool nodi di calcolo con hello [.NET per Batch] [ api_net] libreria.

> [!NOTE]
> 
> I pacchetti dell'applicazione sono supportati in tutti i pool di Batch creati dopo il 5 luglio 2017. Sono supportate nei pool di Batch creato tra 10 marzo 2016 e 5 luglio 2017 solo se il pool di hello è stato creato utilizzando una configurazione del servizio Cloud. Pool di batch creati too10 precedente marzo 2016 non supportano pacchetti di applicazioni.
>
> API per la creazione e gestione dei pacchetti di applicazione Hello fanno parte di hello [gestione .NET per Batch] [[api_net_mgmt]] libreria. API per l'installazione di pacchetti di applicazioni in un nodo di calcolo Hello fanno parte di hello [.NET per Batch] [ api_net] libreria.  
>
> funzionalità di pacchetti di applicazione Hello descritti di seguito sostituisce funzionalità delle App Batch hello disponibili nelle versioni precedenti del servizio hello.
> 
> 

## <a name="application-package-requirements"></a>Requisiti dei pacchetti dell'applicazione
pacchetti di applicazioni toouse, è necessario troppo[collegare un account di archiviazione di Azure](#link-a-storage-account) tooyour account Batch.

Questa funzionalità è stata introdotta in [API REST di Batch] [ api_rest] versione 2015-12-01.2.2 e hello corrispondente [.NET per Batch] [ api_net] versione della libreria 3.1.0. È consigliabile utilizzare sempre versione API più recente di hello quando si utilizzano Batch.

> [!NOTE]
> I pacchetti dell'applicazione sono supportati in tutti i pool di Batch creati dopo il 5 luglio 2017. Sono supportate nei pool di Batch creato tra 10 marzo 2016 e 5 luglio 2017 solo se il pool di hello è stato creato utilizzando una configurazione del servizio Cloud. Pool di batch creati too10 precedente marzo 2016 non supportano pacchetti di applicazioni.
>
>

## <a name="about-applications-and-application-packages"></a>Informazioni sulle applicazioni e sui pacchetti dell’applicazione
All'interno di Batch di Azure, un *applicazione* fa riferimento il set di tooa dei file binari con controllo delle versioni che possono essere nodi di calcolo toohello automaticamente scaricato nel pool di. Un *pacchetto di applicazione* fa riferimento tooa *set specifico* di tali file binari e rappresenta un determinato *versione* dell'applicazione hello.

![Diagramma di alto livello di applicazioni e pacchetti applicazione][1]

### <a name="applications"></a>Applicazioni
Un'applicazione in Batch contiene uno o più applicazioni, pacchetti e specifica le opzioni di configurazione per un'applicazione hello. Ad esempio, un'applicazione può specificare hello predefinito applicazione pacchetto versione tooinstall in nodi di calcolo e se i pacchetti possono essere aggiornati o eliminati.

### <a name="application-packages"></a>Pacchetti dell'applicazione
Un pacchetto di applicazione è un file con estensione zip che contiene i file binari dell'applicazione hello e i file di supporto necessari per l'applicazione hello toorun di attività. Ogni pacchetto di applicazione rappresenta una versione specifica di un'applicazione hello.

È possibile specificare i pacchetti di applicazioni a livello di pool e attività hello. È possibile specificare uno o più di questi pacchetti ed eventualmente una versione quando si crea un pool o un'attività.

* **Pacchetti di applicazioni del pool** vengono distribuiti troppo*ogni* nodo nel pool di hello. Le applicazioni vengono distribuite quando un nodo viene aggiunto a un pool e quando viene riavviato o oppure la sua immagine viene ricreata.
  
    I pacchetti dell'applicazione del pool possono essere usati quando tutti i nodi in un pool eseguono le attività di un processo. È possibile specificare uno o più pacchetti dell'applicazione quando si crea un pool e aggiungere o aggiornare i pacchetti di un pool esistente. Se si aggiornano pacchetti di applicazioni del pool esistenti, è necessario riavviare il nuovo pacchetto hello tooinstall nodi.
* **Attività di pacchetti di applicazioni** vengono distribuiti solo tooa del nodo di calcolo toorun un'attività pianificata, appena prima di eseguire la riga di comando dell'attività hello. Se specificato hello versione e pacchetto dell'applicazione è già presente nel nodo hello, non viene ridistribuito e viene utilizzato un pacchetto esistente hello.
  
    Pacchetti di applicazioni di attività sono utili in ambienti pool condiviso, in cui diversi processi vengono eseguiti in un pool e pool hello non viene eliminato quando un processo viene completato. Se il processo è l'attività più o meno di nodi nel pool di hello, pacchetti di applicazioni di attività possono ridurre al minimo il trasferimento dei dati poiché l'applicazione viene distribuita toohello solo i nodi che eseguono attività.
  
    Altri scenari che possono trarre vantaggio dai pacchetti dell'applicazione per le attività sono i processi che usano un'applicazione di dimensioni elevate, ma solo per poche attività. Ad esempio, una fase di pre-elaborazione o un'attività di tipo merge, in cui un'applicazione hello pre-elaborazione o di tipo merge è pesante, potrebbe trarre vantaggio dall'utilizzo di pacchetti di applicazioni di attività.

> [!IMPORTANT]
> Esistono limitazioni alle dimensioni di pacchetto di applicazione massimo hello e numero hello di applicazioni e pacchetti di applicazioni all'interno di un account Batch. Vedere [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md) per informazioni dettagliate su questi limiti.
> 
> 

### <a name="benefits-of-application-packages"></a>Vantaggi dei pacchetti dell'applicazione
Pacchetti di applicazioni possono semplificare il codice di hello in Batch soluzione e inferiore hello overhead toomanage obbligatorio hello le applicazioni che eseguono le attività.

Con i pacchetti di applicazioni, attività di avvio del pool non ha toospecify un lungo elenco di risorse singoli file tooinstall nei nodi hello. Non è necessario toomanually gestire più versioni dei file dell'applicazione nell'archiviazione di Azure o sui nodi di. E non è necessario tooworry sulla generazione di [URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide accedere ai file di toohello nell'account di archiviazione. Batch funziona in background hello con pacchetti di applicazioni di servizio di archiviazione Azure toostore e distribuirli toocompute nodi.

> [!NOTE] 
> Hello dimensione totale di un'attività di avvio deve essere minore o uguale too32768 caratteri, inclusi i file di risorse e le variabili di ambiente. Se l'attività di avvio supera questo limite, l'uso di pacchetti dell'applicazione è un'altra opzione. Si può anche creare un archivio compresso contenente i file di risorse, caricare il file come tooAzure un blob Storage e decomprimere dalla riga di comando hello dell'attività di avvio. 
>
>

## <a name="upload-and-manage-applications"></a>Caricare e gestire le applicazioni
È possibile utilizzare hello [portale di Azure] [ portal] o hello [gestione .NET per Batch](batch-management-dotnet.md) pacchetti di applicazioni di libreria toomanage hello nell'account di Batch. Hello successivamente in sezioni, è innanzitutto illustrano toolink un account di archiviazione, quindi illustrati aggiungendo applicazioni e pacchetti e gestirli con hello portale.

### <a name="link-a-storage-account"></a>Collegare un account di archiviazione
pacchetti di applicazioni toouse, è innanzitutto necessario collegare un tooyour di account di archiviazione di Azure account Batch. Se non è ancora stato configurato un account di archiviazione, hello portale di Azure consente di visualizzare hello un avviso prima volta che si fa clic su hello **applicazioni** riquadro in hello **account Batch** blade.

> [!IMPORTANT]
> Batch attualmente supporta *solo* hello **generica** tipo di account di archiviazione come descritto nel passaggio 5, [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account)nella [su Azure gli account di archiviazione](../storage/common/storage-create-storage-account.md). Quando si collega un tooyour di account di archiviazione di Azure account Batch, collegare *solo* un **generica** account di archiviazione.
> 
> 

!['Nessun account di archiviazione configurato' nel portale di Azure][9]

Hello Batch servizio utilizza hello associati toostore account di archiviazione i pacchetti di applicazioni. Dopo avere collegato due account hello, Batch possibile distribuire automaticamente i pacchetti hello archiviati in nodi di calcolo tooyour account archiviazione hello collegato. toolink un tooyour di account di archiviazione account Batch, fare clic su **impostazioni dell'account di archiviazione** su hello **avviso** blade e quindi fare clic su **Account di archiviazione** su hello **Account di archiviazione** blade.

![Selezionare il pannello Account di archiviazione nel portale di Azure][10]

È consigliabile creare un account di archiviazione da usare *specificamente* con l'account Batch e selezionarlo qui. Per informazioni dettagliate su come toocreate un account di archiviazione, vedere "Creazione di un account di archiviazione" nella [gli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md). Dopo aver creato un account di archiviazione, è possibile quindi collegarlo account Batch tooyour utilizzando hello **Account di archiviazione** blade.

> [!WARNING]
> Hello servizio Batch utilizza i pacchetti di applicazioni toostore di archiviazione di Azure come BLOB in blocchi. Si è [addebitato come normale] [ storage_pricing] per i dati blob blocco hello. Dimensioni di hello che tooconsider e il numero dei pacchetti di applicazione, quindi periodicamente rimuovere pacchetti deprecati toominimize costi.
> 
> 

### <a name="view-current-applications"></a>Visualizzare le applicazioni correnti
applicazioni di hello tooview nell'account di Batch, fare clic su hello **applicazioni** voce di menu nel menu a sinistra di hello durante la visualizzazione hello **account Batch** blade.

![Riquadro Applicazioni][2]

Selezionare questa opzione di menu per aprire hello **applicazioni** pannello:

![Elenco applicazioni][3]

Hello **applicazioni** pannello Visualizza hello ID di ogni applicazione nel proprio account e hello le proprietà seguenti:

* **Pacchetti**: hello numero di versioni associate a questa applicazione.
* **Versione predefinita**: versione dell'applicazione hello installato se non è necessario indicare una versione quando si specifica un'applicazione hello per un pool. Questa impostazione è facoltativa.
* **Consenti aggiornamenti**: valore hello che specifica se pacchetto aggiornamenti, eliminazioni e aggiunte sono consentiti. Se viene impostato troppo**n**, eliminazioni e aggiornamenti pacchetto sono disabilitate per l'applicazione hello. È possibile aggiungere solo nuove versioni del pacchetto dell'applicazione. valore predefinito di Hello è **Sì**.

### <a name="view-application-details"></a>Visualizzare i dettagli dell'applicazione
Pannello hello tooopen che include i dettagli di hello per un'applicazione hello dell'applicazione, selezionare in hello **applicazioni** blade.

![Dettagli applicazione][4]

Nel Pannello di dettagli applicazione hello, è possibile configurare hello seguenti impostazioni per l'applicazione.

* **Consenti aggiornamenti**: specificare se i pacchetti dell'applicazione possono essere aggiornati o eliminati. Vedere "Aggiornare o eliminare un pacchetto dell'applicazione" più avanti in questo articolo.
* **Versione predefinita**: specificare un pacchetto di predefinito applicazione toodeploy toocompute nodi.
* **Nome visualizzato**: specificare un nome descrittivo del Batch soluzione può impiegare quando vengono visualizzate informazioni sull'applicazione hello, ad esempio, nell'interfaccia utente di un servizio fornito ai clienti tooyour tramite Batch hello.

### <a name="add-a-new-application"></a>Aggiungere un’applicazione nuova
toocreate una nuova applicazione, aggiungere un pacchetto di applicazione e specificare un ID applicazione di nuovi e univoci. Inoltre, Hello primo pacchetto di applicazione si aggiunge con un nuovo ID applicazione di hello Crea nuova applicazione hello.

Fare clic su **Aggiungi** su hello **applicazioni** hello tooopen pannello **nuova applicazione** blade.

![Pannello Nuova applicazione nel portale di Azure][5]

Hello **nuova applicazione** pannello fornisce seguente hello campi impostazioni hello toospecify della nuova applicazione e il pacchetto di applicazione.

**ID applicazione**

Questo campo specifica hello ID della nuova applicazione, che è soggetto toohello standard ID Batch di Azure le regole di convalida. le regole per fornire un ID applicazione Hello sono come segue:

* I nodi Windows hello ID può contenere qualsiasi combinazione di caratteri alfanumerici, trattini e caratteri di sottolineatura. Nei nodi di Linux, sono consentiti solo caratteri alfanumerici e caratteri di sottolineatura.
* Non può contenere più di 64 caratteri.
* Deve essere univoco all'interno di hello account Batch.
* Mantiene le maiuscole/minuscole e non fa distinzione tra maiuscole e minuscole.

**Versione**

Questo campo specifica versione di hello hello del pacchetto di applicazione che si sta caricando. Le stringhe di versione sono toohello soggetto alle regole di convalida:

* Nei nodi di Windows, la stringa di versione hello può contenere qualsiasi combinazione di caratteri alfanumerici, trattini, caratteri di sottolineatura e punti. Nei nodi di Linux, stringa di versione di hello può contenere solo caratteri alfanumerici e caratteri di sottolineatura.
* Non può contenere più di 64 caratteri.
* Deve essere univoco all'interno di un'applicazione hello.
* Mantengono le maiuscole/minuscole e non fanno distinzione tra maiuscole e minuscole.

**Pacchetto dell'applicazione**

Questo campo specifica hello con estensione zip che contiene i file binari dell'applicazione hello e i file di supporto dell'applicazione hello tooexecute obbligatorio. Fare clic su hello **selezionare un file** casella o hello tooand toobrowse icona di cartella selezionare un file con estensione zip che contiene i file dell'applicazione.

Dopo aver selezionato un file, fare clic su **OK** toobegin hello caricamento tooAzure archiviazione. Quando l'operazione di caricamento hello è stata completata, portale hello Visualizza una notifica e chiude il pannello hello. A seconda delle dimensioni di hello del file hello che si sta caricando e hello velocità della connessione di rete, questa operazione potrebbe richiedere alcuni minuti.

> [!WARNING]
> Non chiudere hello **nuova applicazione** pannello prima operazione di caricamento hello è stata completata. In questo modo, il processo di caricamento hello verrà interrotta.
> 
> 

### <a name="add-a-new-application-package"></a>Aggiungere un nuovo pacchetto dell’applicazione
tooadd una nuova versione del pacchetto dell'applicazione per un'applicazione esistente, selezionare un'applicazione hello **applicazioni** pannello, fare clic su **pacchetti**, quindi fare clic su **Aggiungi** tooopen Hello **Aggiungi pacchetto** blade.

![Pannello per aggiungere un pacchetto dell'applicazione nel portale di Azure][8]

Come si può notare, i campi di hello corrispondono a quelle di hello **nuova applicazione** pannello ma hello **id applicazione** casella è disabilitata. Come per la nuova applicazione hello, specificare hello **versione** per il nuovo pacchetto, visitare tooyour **pacchetto di applicazione** ZIP file, quindi fare clic su **OK** hello tooupload pacchetto.

### <a name="update-or-delete-an-application-package"></a>Aggiornare o eliminare un pacchetto dell'applicazione
tooupdate o eliminare un pacchetto di applicazione esistente, il pannello dettagli hello open per un'applicazione hello, fare clic su **pacchetti** tooopen hello **pacchetti** pannello, fare clic su hello **i puntini di sospensione**nella riga hello hello del pacchetto di applicazione che si desidera toomodify e selezionare hello azione che si desidera tooperform.

![Aggiornare o eliminare un pacchetto nel portale di Azure][7]

**Aggiornare**

Quando fa clic su **aggiornamento**, hello *pacchetto di aggiornamento* pannello viene visualizzato. Questo pannello è simile toohello *nuovo pacchetto di applicazione* pannello, tuttavia, solo il campo selezione pacchetto hello è abilitato, consente toospecify un nuovo tooupload file ZIP.

![Pannello per aggiornare un pacchetto nel portale di Azure][11]

**Eliminazione**

Quando fa clic su **eliminare**, viene richiesto l'eliminazione di hello tooconfirm della versione del pacchetto hello e Batch Elimina pacchetto di hello da archiviazione di Azure. Se si elimina una versione di hello predefinita di un'applicazione, hello **versione predefinita** impostazione è stata rimossa per un'applicazione hello.

![Eliminare un'applicazione ][12]

## <a name="install-applications-on-compute-nodes"></a>Installare le applicazioni su nodi di calcolo
Ora che si è appreso come applicazione toomanage dei pacchetti con hello portale di Azure, è possibile illustrare come toodeploy tali nodi toocompute ed eseguirli con le attività Batch.

### <a name="install-pool-application-packages"></a>Installare pacchetti dell'applicazione nel pool
tooinstall un pacchetto dell'applicazione in tutti i nodi di calcolo in un pool, specificare uno o più pacchetti di applicazione *riferimenti* per pool hello. pacchetti di applicazione Hello specificato per un pool vengono installati in ogni nodo di calcolo quando viene aggiunto a tale nodo pool hello e quando il nodo hello viene riavviato o ricreata l'immagine.

In Batch .NET specificare uno o più [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] quando si crea un nuovo pool oppure aggiungerli al pool esistente. Hello [ApplicationPackageReference] [ net_pkgref] classe specifica un ID applicazione e la versione tooinstall in un pool di nodi di calcolo.

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> Se una distribuzione del pacchetto di applicazione non riesce per qualsiasi motivo, i segni di servizio Batch hello hello nodo [inutilizzabile][net_nodestate], e nessuna attività viene pianificata per l'esecuzione in tale nodo. In questo caso, è necessario **riavviare** hello distribuzione dei pacchetti hello tooreinitiate nodo. Nodo hello riavviare consente inoltre di pianificazione delle attività nuovamente nel nodo hello.
> 
> 

### <a name="install-task-application-packages"></a>Installare pacchetti dell'applicazione per le attività
Pool tooa simile, specificare il pacchetto di applicazione *riferimenti* per un'attività. Quando un'attività è pianificata toorun in un nodo, il pacchetto di hello viene scaricato ed estratto prima riga di comando dell'attività hello venga eseguito. Se un pacchetto specificato e la versione è già installato nel nodo hello, non viene scaricato il pacchetto di hello e viene utilizzato un pacchetto esistente hello.

tooinstall un pacchetto di applicazione di attività, configurare dell'attività hello [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] proprietà:

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a>Eseguire le applicazioni hello installato
vengono scaricati Hello pacchetti specificati per un pool o un'attività ed estratti tooa denominato directory all'interno di hello `AZ_BATCH_ROOT_DIR` del nodo hello. Batch Crea inoltre una variabile di ambiente contenente toohello percorso hello denominato directory. Le righe di comando attività usare questa variabile di ambiente quando si fa riferimento a un'applicazione hello nel nodo hello. 

Variabile hello è nodi Windows in hello seguente formato:

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

In nodi di Linux, il formato di hello è leggermente diverso. Punti (.), trattini (-) e simboli di cancelletto (#) sono bidimensionali toounderscores nella variabile di ambiente hello. ad esempio:

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

`APPLICATIONID`e `version` sono valori che corrispondono toohello applicazione e versione del pacchetto è stato specificato per la distribuzione. Ad esempio, se è stata specificata la versione 2.7 di applicazione *blender* deve essere installata nei nodi di Windows, le righe di comando attività utilizzerà questo tooaccess variabile di ambiente relativi file:

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

Nei nodi di Linux, specificare la variabile di ambiente hello nel formato seguente:

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

Quando si carica un pacchetto di applicazione, è possibile specificare un tooyour toodeploy di versione predefinito nodi di calcolo. Se è stata specificata una versione predefinita per un'applicazione, è possibile omettere il suffisso di versione di hello quando si fa riferimento a un'applicazione hello. È possibile specificare una versione di hello predefinito dell'applicazione nel portale di Azure, nel Pannello di applicazioni hello, hello come illustrato nella [caricare e gestire applicazioni](#upload-and-manage-applications).

Ad esempio, se si imposta come versione di hello predefinita per l'applicazione "2.7" *blender*, le attività di riferimento hello seguente variabile di ambiente, quindi i nodi Windows eseguirà versione 2.7:

`AZ_BATCH_APP_PACKAGE_BLENDER`

Hello frammento di codice seguente viene illustrata una riga di comando di attività di esempio che avvia versione di hello predefinita di hello *blender* applicazione:

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> Vedere [impostazioni di ambiente per l'attività](batch-api-basics.md#environment-settings-for-tasks) in hello [Cenni preliminari sulle funzionalità di Batch](batch-api-basics.md) per ulteriori informazioni sulle impostazioni di ambiente nodo di calcolo.
> 
> 

## <a name="update-a-pools-application-packages"></a>Aggiornare i pacchetti dell’applicazione di un pool
Se un pool esistente è già stato configurato con un pacchetto di applicazione, è possibile specificare un nuovo pacchetto per il pool di hello. Se si specifica un nuovo riferimento pacchetto per un pool, si applicano i seguenti hello:

* Hello servizio Batch installa hello appena specificato per il pacchetto in tutti i nuovi nodi che uniscono in join pool hello e su qualsiasi nodo esistente che è stato riavviato oppure ricreata l'immagine.
* Consente di calcolare i nodi già presenti nel pool di hello quando si aggiorna hello pacchetto fa riferimento non installano automaticamente il nuovo pacchetto di applicazione hello. Questi nodi è necessario riavviare o calcolo tooreceive nuove immagini hello nuovo pacchetto.
* Quando viene distribuito un nuovo pacchetto, creata variabili di ambiente hello riflettono hello nuova applicazione pacchetto fa riferimento.

In questo esempio, un pool esistente hello è versione 2.7 di hello *blender* applicazione configurata come uno dei relativi [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref]. i nodi del pool di hello tooupdate con versione 2.76b, specificare un nuovo [ApplicationPackageReference] [ net_pkgref] con una nuova versione di hello e commit hello modifica.

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

Ora che hello nuova versione è stata configurata, hello servizio Batch installa versione 2.76b tooany *nuova* nodi aggiunti al pool di hello. tooinstall 2.76b in hello i nodi *già* nel pool di hello, riavviare o ricreare l'immagine di essi. Si noti che i nodi riavviati mantengono file hello da distribuzioni di pacchetto precedente.

## <a name="list-hello-applications-in-a-batch-account"></a>Elenco di applicazioni hello in un account Batch
È possibile elencare i pacchetti in un account di Batch e applicazioni hello utilizzando hello [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] metodo.

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a>Eseguire il wrapping
Con pacchetti di applicazioni, è possibile aiutare i clienti selezionare applicazioni hello per svolgere il lavoro e specificare hello versione esatta toouse durante l'elaborazione di processi con il servizio Batch abilitata. Potrebbe inoltre offrono possibilità di hello per tooupload i clienti e tenere traccia delle proprie applicazioni del servizio.

## <a name="next-steps"></a>Passaggi successivi
* Hello [API REST di Batch] [ api_rest] fornisce inoltre supporto toowork con pacchetti di applicazioni. Ad esempio, vedere hello [applicationPackageReferences] [ rest_add_pool_with_packages] elemento [aggiungere un account del pool di tooan] [ rest_add_pool] per informazioni su come toospecify tooinstall di pacchetti tramite hello API REST. Vedere [applicazioni] [ rest_applications] per informazioni dettagliate su come le informazioni sull'applicazione tooobtain utilizzando hello API REST di Batch.
* Informazioni su come tooprogrammatically [gestire gli account Azure Batch e le quote con gestione .NET per Batch](batch-management-dotnet.md). Hello [gestione .NET per Batch][api_net_mgmt] libreria è possibile abilitare funzionalità di creazione e l'eliminazione di account per l'applicazione di Batch o di un servizio.

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Diagramma di alto livello di pacchetti applicazione"
[2]: ./media/batch-application-packages/app_pkg_02.png "Riquadro Applicazioni nel portale di Azure"
[3]: ./media/batch-application-packages/app_pkg_03.png "Pannello Applicazioni nel portale di Azure"
[4]: ./media/batch-application-packages/app_pkg_04.png "Pannello Dettagli applicazione nel portale di Azure"
[5]: ./media/batch-application-packages/app_pkg_05.png "Pannello Nuova applicazione nel portale di Azure"
[7]: ./media/batch-application-packages/app_pkg_07.png "Elenco a discesa per aggiornamento o eliminazione pacchetto nel portale di Azure"
[8]: ./media/batch-application-packages/app_pkg_08.png "Pannello per nuovo pacchetto dell'applicazione nel portale di Azure"
[9]: ./media/batch-application-packages/app_pkg_09.png " Nessun account di archiviazione collegato"
[10]: ./media/batch-application-packages/app_pkg_10.png "Selezionare il pannello Account di archiviazione nel portale di Azure"
[11]: ./media/batch-application-packages/app_pkg_11.png "Pannello Aggiorna pacchetto nel portale di Azure"
[12]: ./media/batch-application-packages/app_pkg_12.png "Finestra di conferma eliminazione pacchetto nel portale di Azure"
