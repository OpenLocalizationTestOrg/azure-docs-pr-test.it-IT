---
title: contatori delle prestazioni in diagnostica Azure aaaUse | Documenti Microsoft
description: Utilizzare i contatori delle prestazioni in servizi cloud di Azure o i colli di bottiglia toofind macchina virtuale e ottimizzare le prestazioni.
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a>Creare e usare contatori di prestazioni in un'applicazione Azure
Questo articolo descrive i vantaggi hello e come i contatori delle prestazioni tooput nell'applicazione Azure. È possibile utilizzarli come dati toocollect, individuare i colli di bottiglia e ottimizzare le prestazioni del sistema e dell'applicazione.

Contatori delle prestazioni disponibili per Windows Server, IIS e ASP.NET possono anche essere raccolti e utilizzato integrità hello toodetermine di ruoli web di Azure e i ruoli di lavoro, le macchine virtuali. È anche possibile creare e usare contatori delle prestazioni personalizzati.  

È possibile esaminare i dati dei contatori delle prestazioni

1. Direttamente nell'host di applicazioni hello con lo strumento Performance Monitor hello accesso tramite Desktop remoto
2. Con System Center Operations Manager hello Azure Management Pack
3. Con altri strumenti di monitoraggio che accedono a hello tooAzure archiviazione trasferire i dati di diagnostica. Per altre informazioni, vedere [Archiviare e visualizzare i dati di diagnostica nell'account di archiviazione Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) .  

Per ulteriori informazioni sul monitoraggio delle prestazioni di hello dell'applicazione in hello [portale di Azure](http://portal.azure.com/), vedere [come servizi Cloud tooMonitor](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).

Per altre informazioni dettagliate sulla creazione di una registrazione e traccia strategia e sull'uso della diagnostica e altri problemi tootroubleshoot tecniche e ottimizzare le applicazioni Azure, vedere [risoluzione dei problemi di procedure consigliate per lo sviluppo di Azure Applicazioni](https://msdn.microsoft.com/library/azure/hh771389.aspx).

## <a name="enable-performance-counter-monitoring"></a>Abilitare il monitoraggio del contatore delle prestazioni
Per impostazione predefinita, i contatori delle prestazioni non sono abilitati. L'applicazione o un'attività di avvio deve modificare diagnostica predefinito hello prestazioni specifici di agente configurazione tooinclude hello contatori che si desidera toomonitor per ogni istanza del ruolo.

### <a name="performance-counters-available-for-microsoft-azure"></a>Contatori delle prestazioni disponibili per Microsoft Azure
Azure fornisce un subset di contatori delle prestazioni di hello disponibili per Windows Server, IIS e ASP.NET stack hello. Hello nella tabella seguente sono elencati alcuni dei contatori delle prestazioni di hello di particolare interesse per le applicazioni Azure.

| Categoria contatore: oggetto (istanza) | Nome contatore | Riferimento |
| --- | --- | --- |
| Eccezioni CLR .NET (*globale*) |N. eccezioni/sec |Contatori delle prestazioni delle eccezioni |
| Memoria CLR .NET (*globale*) |Percentuale tempo in GC |Contatori delle prestazioni di memoria |
| ASP.NET |Riavvii applicazione |Contatori delle prestazioni per ASP.NET |
| ASP.NET |Tempo di esecuzione della richiesta |Contatori delle prestazioni per ASP.NET |
| ASP.NET |Richieste disconnesse |Contatori delle prestazioni per ASP.NET |
| ASP.NET |Riavvii processo di lavoro |Contatori delle prestazioni per ASP.NET |
| Applicazioni ASP.NET (**totale**) |Totale richieste |Contatori delle prestazioni per ASP.NET |
| Applicazioni ASP.NET (**totale**) |Richieste/sec |Contatori delle prestazioni per ASP.NET |
| ASP.NET v4.0.30319 |Tempo di esecuzione della richiesta |Contatori delle prestazioni per ASP.NET |
| ASP.NET v4.0.30319 |Tempo di attesa richiesta |Contatori delle prestazioni per ASP.NET |
| ASP.NET v4.0.30319 |Richieste correnti |Contatori delle prestazioni per ASP.NET |
| ASP.NET v4.0.30319 |Richieste in coda |Contatori delle prestazioni per ASP.NET |
| ASP.NET v4.0.30319 |Richieste respinte |Contatori delle prestazioni per ASP.NET |
| Memoria |MByte disponibili |Contatori delle prestazioni di memoria |
| Memoria |Byte vincolati |Contatori delle prestazioni di memoria |
| Processor(_Total) |% di tempo processore |Contatori delle prestazioni per ASP.NET |
| TCPv4 |Errori di connessione |Oggetto TCP |
| TCPv4 |Connessioni stabilite |Oggetto TCP |
| TCPv4 |Connessioni ripristinate |Oggetto TCP |
| TCPv4 |Segmenti inviati/sec |Oggetto TCP |
| Interfaccia di rete (*) |Byte ricevuti/sec |Oggetto interfaccia di rete |
| Interfaccia di rete (*) |Byte inviati/sec |Oggetto interfaccia di rete |
| Interfaccia di rete (Scheda di rete per il bus delle macchine virtuali Microsoft _2) |Byte ricevuti/sec |Oggetto interfaccia di rete |
| Interfaccia di rete (Scheda di rete per il bus delle macchine virtuali Microsoft _2) |Byte inviati/sec |Oggetto interfaccia di rete |
| Interfaccia di rete (Scheda di rete per il bus delle macchine virtuali Microsoft _2) |Totale byte/sec |Oggetto interfaccia di rete |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a>Creare e aggiungere l'applicazione di tooyour i contatori delle prestazioni personalizzati
Azure dispone di supporto toocreate e modificare i contatori delle prestazioni personalizzati per i ruoli web e ruoli di lavoro. contatori di Hello possono essere utilizzato il comportamento di specifiche dell'applicazione tootrack e monitoraggio. È possibile creare ed eliminare categorie e identificatori dei contatori delle prestazioni personalizzati da un'attività di avvio, un ruolo Web o un ruolo di lavoro con autorizzazioni elevate.

> [!NOTE]
> Codice che modifica i contatori delle prestazioni toocustom deve elevate toorun autorizzazioni. Se il codice hello è in un ruolo web o un ruolo di lavoro, il ruolo di hello deve includere tag hello <Runtime executionContext="elevated" /> in hello servicedefinition. Csdef del file per hello ruolo tooinitialize correttamente.
>
>

È possibile inviare archiviazione tooAzure dati contatore di prestazioni personalizzati utilizzando hello diagnostica agente.

i dati dei contatori delle prestazioni standard Hello viene generati da hello che Azure elabora. I dati dei contatori delle prestazioni personalizzati devono essere creati dall'applicazione ruolo Web o ruolo di lavoro. Vedere [tipi di contatori delle prestazioni](https://msdn.microsoft.com/library/z573042h.aspx) per informazioni sui tipi di hello di dati che possono essere archiviati in contatori delle prestazioni personalizzati. Per un esempio di creazione e impostazione dei dati dei contatori delle prestazioni personalizzati in un ruolo Web, vedere [Esempio PerformanceCounters](http://code.msdn.microsoft.com/azure/) .

## <a name="store-and-view-performance-counter-data"></a>Archiviare e visualizzare i dati dei contatori delle prestazioni
Azure memorizza nella cache i dati dei contatori delle prestazioni con altre informazioni di diagnostica. Questi dati sono disponibili per il monitoraggio remoto durante l'esecuzione di istanza del ruolo hello utilizzando gli strumenti tooview accesso desktop remoto, ad esempio Performance Monitor. toopersist hello trasferimento dei dati all'esterno di istanza del ruolo hello, agente di diagnostica hello deve archiviazione tooAzure dei dati hello. limite delle dimensioni dei dati dei contatori delle prestazioni memorizzati nella cache di hello Hello può essere configurato nell'agente di diagnostica hello o può essere configurato toobe parte di un limite condiviso per tutti i dati di diagnostica di hello. Per ulteriori informazioni sull'impostazione delle dimensioni del buffer hello, vedere [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) e [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx). Vedere [archivio e visualizza i dati di diagnostica in archiviazione di Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) per una panoramica dell'impostazione di account di archiviazione di hello diagnostica agente tootransfer dati tooa.

Ogni istanza del contatore delle prestazioni configurati viene registrata con una frequenza di campionamento specificata e trasferimento dei dati campionato hello toohello account di archiviazione tramite una richiesta di trasferimento pianificato o di una richiesta di trasferimento su richiesta. I trasferimenti automatici possono essere pianificati con una frequenza di una volta ogni minuto. Dati del contatore di prestazioni trasferiti dall'agente di diagnostica hello sono archiviati in una tabella, WADPerformanceCountersTable, nell'account di archiviazione hello. Questa tabella è accessibile e può essere sottoposta a query con i metodi API di archiviazione standard di Azure. Vedere [esempio PerformanceCounters di Microsoft Azure](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) per un esempio di query e visualizzazione di dati del contatore delle prestazioni dalla tabella WADPerformanceCountersTable hello.

> [!NOTE]
> A seconda della frequenza di trasferimento dell'agente di diagnostica hello e latenza della coda, hello dati più recente del contatore delle prestazioni nell'account di archiviazione hello sia aggiornata alcuni minuti.
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a>Abilitare i contatori delle prestazioni con il file di configurazione della diagnostica
Utilizzare i seguenti contatori delle prestazioni di stored procedure tooenable nell'applicazione Azure hello.

## <a name="prerequisites"></a>Prerequisiti
In questa sezione si presuppone di aver importato monitor di diagnostica hello nell'applicazione e aggiunto hello diagnostica configurazione file tooyour soluzione di Visual Studio (Diagnostics. wadcfg in SDK 2.4 e di sotto o wadcfgx in SDK 2.5 e versioni successive). Per altre informazioni, vedere i passaggi 1 e 2 in [Abilitazione della diagnostica nei servizi cloud e nelle macchine virtuali di Azure](cloud-services-dotnet-diagnostics.md).

## <a name="step-1-collect-and-store-data-from-performance-counters"></a>Passaggio 1: Raccogliere e archiviare i dati dei contatori delle prestazioni
Dopo aver aggiunto la diagnostica hello file tooyour soluzione di Visual Studio, è possibile configurare hello raccolta e l'archiviazione dei dati dei contatori delle prestazioni in un'applicazione Azure. Questa operazione viene eseguita mediante l'aggiunta di file di diagnostica toohello dei contatori delle prestazioni. Dati di diagnostica, inclusi i contatori delle prestazioni, vengono prima raccolti nell'istanza di hello. dati Hello sono persistente toohello WADPerformanceCountersTable tabella hello servizio tabelle di Azure, pertanto sarà anche necessario toospecify hello account di archiviazione nell'applicazione. Se si sta testando l'applicazione localmente nell'emulatore di calcolo di hello, è anche possibile archiviare i dati di diagnostica a livello locale in hello emulatore di archiviazione. Prima di archiviare dati di diagnostica, è necessario passare toohello [portale di Azure](http://portal.azure.com/) e creare un account di archiviazione classico. È consigliabile toolocate account di archiviazione nella stessa posizione geografica dell'applicazione Azure hello. Da mantenere hello Azure account di archiviazione e di applicazione sono in hello stessa località geografica, evitare di sostenere costi di larghezza di banda esterna e ridurre la latenza.

### <a name="add-performance-counters-toohello-diagnostics-file"></a>Aggiungere file di diagnostica toohello dei contatori delle prestazioni
È possibile usare diversi contatori. Hello riportato di seguito diversi contatori delle prestazioni consigliati per il web e ruolo di lavoro monitoraggio.

Aprire il file di hello diagnostica (Diagnostics. wadcfg in SDK 2.4 e versioni precedenti o wadcfgx in SDK 2.5 e versioni successive) e aggiungere hello successivo elemento DiagnosticMonitorConfiguration toohello:

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

attributo di bufferQuotaInMB Hello, che specifica hello quantità massima di archiviazione nel file system disponibile per il tipo di raccolta dati hello (log di Azure, i log di IIS e così via). valore predefinito di Hello è 0. Quando viene raggiunta la quota hello, dati meno recenti di hello vengono eliminati man mano che vengono aggiunti nuovi dati. somma di Hello di tutte le proprietà di bufferQuotaInMB hello deve essere maggiore del valore di hello dell'attributo OverallQuotaInMB hello. Per una discussione più dettagliata di determinare la quantità di archiviazione richiesta per la raccolta di hello dei dati di diagnostica, vedere hello sezione WAD il programma di installazione di [risoluzione dei problemi di procedure consigliate per lo sviluppo di applicazioni Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).

l'attributo scheduledTransferPeriod Hello, che specifica l'intervallo di hello tra i trasferimenti di dati pianificati, arrotondato per eccesso toohello più vicino al minuto. In hello seguono esempi, è impostato tooPT30M (30 minuti). Impostazione hello trasferimento tooa periodo valore basso, ad esempio 1 minuto, influisce negativamente sulle prestazioni dell'applicazione nell'ambiente di produzione, ma può essere utile per visualizzare l'esecuzione rapida, quando si esegue il test della diagnostica. periodo di trasferimento pianificato Hello deve essere sufficientemente piccole tooensure che i dati di diagnostica non viene sovrascritti nell'istanza di hello, ma sufficientemente elevato che non influirà hello delle prestazioni dell'applicazione.

attributo counterSpecifier Hello specifica toocollect contatore delle prestazioni di hello. attributo sampleRate Hello specifica velocità hello in corrispondenza del quale hello delle prestazioni del contatore, in questo caso 30 secondi.

Una volta aggiunti i contatori delle prestazioni di hello che si desidera toocollect, salvare il file di diagnostica toohello di modifiche. Successivamente, è necessario l'account di archiviazione hello toospecify che verranno mantenuti per i dati di diagnostica hello.

### <a name="specify-hello-storage-account"></a>Specificare l'account di archiviazione hello
toopersist il tooyour informazioni di diagnostica Azure Storage account, è necessario specificare una stringa di connessione nel file di configurazione (ServiceConfiguration. cscfg) del servizio.

Per Azure SDK 2.5, hello Account di archiviazione può essere specificato nel file Diagnostics. wadcfgx hello.

> [!NOTE]
> Queste istruzioni si applicano solo tooAzure SDK 2.4 e versioni precedenti. Per Azure SDK 2.5, hello Account di archiviazione può essere specificato nel file Diagnostics. wadcfgx hello.
>
>

stringhe di connessione tooset hello:

1. Aprire il file ServiceConfiguration hello utilizzando l'editor di testo preferito e stringa di connessione hello set per l'archiviazione. Hello *AccountName* e *AccountKey* i valori sono disponibili in hello portale Azure nel dashboard dell'account di archiviazione hello, in corrispondenza delle chiavi di accesso.

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. Salvare file ServiceConfiguration hello.
3. Aprire il file local. cscfg hello e verificare che UseDevelopmentStorage sia impostato tootrue.

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   Ora che sono impostate le stringhe di connessione hello, quando l'applicazione viene distribuita l'applicazione viene mantenuto account di archiviazione tooyour dati di diagnostica.
4. Salvare e compilare il progetto, quindi distribuire l'applicazione.

## <a name="step-2-optional-create-custom-performance-counters"></a>Passaggio 2: (Facoltativo) Creare contatori delle prestazioni personalizzati
Inoltre toohello predefiniti i contatori delle prestazioni, è possibile aggiungere che i ruoli web o di lavoro toomonitor contatori delle proprie prestazioni personalizzati. Contatori delle prestazioni personalizzati possono modo utilizzati tootrack e monitoraggio specifici dell'applicazione e può essere creati o eliminati in un'attività di avvio, un ruolo web o un ruolo di lavoro con autorizzazioni elevate.

agente di diagnostica di Azure Hello Aggiorna hello configurazione contatori di prestazioni dal file con estensione wadcfg hello un minuto dopo l'avvio.  Se si creano i contatori delle prestazioni personalizzati nel metodo OnStart hello e le attività di avvio richiedono più di un minuto tooexecute, i contatori delle prestazioni personalizzati non è state create quando l'agente diagnostica Azure hello tenta tooload li.  In questo scenario Diagnostica di Azure acquisirà correttamente tutti i dati di diagnostica tranne i contatori delle prestazioni personalizzati.  tooresolve questo problema, creare hello contatori delle prestazioni in un'attività di avvio o spostare alcune delle attività di avvio funziona metodo OnStart toohello dopo la creazione di contatori delle prestazioni di hello.

Eseguire i seguenti passaggi toocreate una semplice personalizzata contatore delle prestazioni "\MyCustomCounterCategory\MyButton1Counter" hello:

1. Aprire hello file di definizione del servizio (CSDEF) per l'applicazione.
2. Aggiungere hello elemento toohello WebRole o WorkerRole elemento tooallow esecuzione con privilegi elevati:

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. Salvare il file hello.
4. Aprire il file di hello diagnostica (Diagnostics. wadcfg in SDK 2.4 e versioni precedenti o wadcfgx in SDK 2.5 e versioni successive) e aggiungere hello seguente toohello DiagnosticMonitorConfiguration

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. Salvare il file hello.
6. Creare categoria del contatore delle prestazioni personalizzati hello nel metodo OnStart hello del ruolo, prima di chiamare base. OnStart. Hello esempio c# seguente viene creata una categoria personalizzata, se non esiste già:

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. Aggiornare i contatori di hello all'interno dell'applicazione. Hello di esempio seguente aggiorna un contatore delle prestazioni personalizzato in eventi Button1_Click:

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. Salvare il file hello.  

I dati dei contatori delle prestazioni personalizzati verranno ora raccolti dal monitor di diagnostica di Azure hello.

## <a name="step-3-query-performance-counter-data"></a>Passaggio 3: Eseguire query sui dati dei contatori delle prestazioni
Dopo l'applicazione viene distribuita e in esecuzione, il monitor di diagnostica hello inizierà a raccogliere i contatori delle prestazioni e che tooAzure l'archiviazione dei dati di persistenza. Utilizzare gli strumenti, ad esempio Esplora Server in Visual Studio, [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), o [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) di Cerebrata in hello dati dei contatori delle prestazioni di hello tooview Tabella WADPerformanceCountersTable. È possibile eseguire una query anche a livello di codice hello tabella servizio tramite [c#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), o [PHP](../cosmos-db/table-storage-how-to-use-php.md).

Hello esempio c# seguente viene illustrata una query di base sulla tabella WADPerformanceCountersTable hello e Salva il file CSV tooa di hello diagnostica dei dati. Dopo che i contatori delle prestazioni di hello vengono salvati i file CSV tooa, è possibile utilizzare le funzionalità di Microsoft Excel o alcuni altri dati hello toovisualize dello strumento di creazione di grafi hello. Impossibile verificare tooadd tooMicrosoft.WindowsAzure.Storage.dll un riferimento, incluso in hello Azure SDK per .NET ottobre 2012 e versioni successive. assembly Hello è installato toohello % programma Files%\Microsoft SDKs\Microsoft Azure.NET sdk\version-num\ref\. directory.

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

Eseguire il mapping di entità tooC # oggetti usando una classe personalizzata derivata da **TableEntity**. il codice seguente Hello definisce una classe di entità che rappresenta un contatore delle prestazioni in hello **WADPerformanceCountersTable** tabella.

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a>Passaggi successivi
[Visualizzare altri articoli sulla diagnostica di Azure](../azure-diagnostics.md)
