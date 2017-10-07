---
title: aaaEnabling metriche di archiviazione nel portale di Azure hello | Documenti Microsoft
description: Come tooenable metriche di archiviazione per hello servizi Blob, coda, tabella e File
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 2fb5b229-f099-4334-92be-4e0e7dd257d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 4c990371e08a6586d935b0535149eabd4960cfaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a>Abilitazione di Metriche di archiviazione e visualizzazione dei dati di metrica
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>Panoramica
Le metriche di archiviazione vengono abilitate per impostazione predefinita quando si crea un nuovo account di archiviazione. È possibile configurare il monitoraggio tramite entrambi hello [portale di Azure classico](https://manage.windowsazure.com), Windows PowerShell, o a livello di codice tramite un'API di archiviazione.

Quando si abilita metriche di archiviazione, è necessario scegliere un periodo di memorizzazione per i dati di hello: questo periodo determina per quanto tempo archiviazione hello servizio mantiene le metriche hello e spese di hello spazio richiesto toostore li. In genere, è consigliabile utilizzare un periodo di memorizzazione più breve per le metriche al minuto più metrica oraria a causa di hello significativo spazio richiesto per le metriche al minuto. È consigliabile scegliere un periodo di memorizzazione in modo che si dispone di sufficiente tempo tooanalyze hello dati e download delle metriche che si desidera tookeep per l'analisi offline o creazione di report. Tenere presente che verrà addebitato anche il download dei dati di metrica dall'account di archiviazione.

## <a name="how-tooenable-storage-metrics-using-hello-azure-classic-portal"></a>Come tooenable metriche di archiviazione usando hello portale classico di Azure
In hello [portale di Azure classico](https://manage.windowsazure.com), usare hello Configura pagina relativa a un toocontrol di account di archiviazione metriche di archiviazione. Per il monitoraggio, è possibile impostare un livello e un periodo di memorizzazione in giorni per ciascun BLOB, tabella e coda. In ogni caso, il livello di hello è uno dei seguenti hello:

* Disattivato: non vengono raccolte metriche.
* Minimo tra Metriche di archiviazione raccoglie un set di metriche come ingresso/uscita, disponibilità, latenza e percentuali di successo aggregate per i servizi Blob, tabelle e code di hello base.
* -Verbose Raccoglie le metriche di archiviazione set completo di metriche che include hello stesse metriche per ogni operazione API di archiviazione, inoltre toohello a livello di servizio metriche. Le metriche dettagliate consentono un'analisi più accurata dei problemi che si verificano durante l'elaborazione dell'applicazione.

Si noti che hello portale classico di Azure non attualmente consentono tooconfigure metrica al minuto nell'account di archiviazione; è necessario abilitare le metriche al minuto mediante PowerShell o a livello di codice.

## <a name="how-tooenable-storage-metrics-using-powershell"></a>Come tooenable metriche di archiviazione con PowerShell
È possibile usare PowerShell sulle metriche di archiviazione di tooconfigure computer locale nell'account di archiviazione usando le impostazioni correnti di hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello e hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello le impostazioni correnti.

cmdlet di Hello che controllano metriche di archiviazione usano hello seguenti parametri:

* I valori possibili di MetricsType sono Hour e Minute.
* I valori possibili di ServiceType sono Blob, Queue e Table.
* MetricsLevel i valori possibili sono None (tooOff equivalente nel portale di Azure classico hello), il servizio (tooMinimal equivalente nel portale di Azure classico hello) e ServiceAndApi (tooVerbose equivalente nel portale di Azure classico hello).

Ad esempio, hello seguente comando attiva le metriche per il servizio blob hello nell'account di archiviazione predefinito con il periodo di memorizzazione hello impostare i giorni toofive minuto:

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
Hello seguente comando Recupera hello corrente oraria metriche livello e alla conservazione dei giorni per il servizio blob hello nell'account di archiviazione predefinito:

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
Per informazioni su come tooconfigure hello Azure PowerShell cmdlet toowork con la sottoscrizione di Azure e come tooselect hello spazio di archiviazione predefinito degli account toouse, vedere: [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

## <a name="how-tooenable-storage-metrics-programmatically"></a>Come tooenable metriche di archiviazione a livello di codice
Hello frammento di codice c# seguente viene illustrato come tooenable metrica e registrazione per il servizio Blob hello utilizzando hello libreria client di archiviazione per .NET:

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days. 
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a>Visualizzazione di Metriche di archiviazione
Quando è stato configurato toomonitor metriche di archiviazione di account di archiviazione, registra le metriche hello in un set di tabelle note nell'account di archiviazione. È possibile utilizzare pagina monitoraggio hello dell'account di archiviazione in hello metrica oraria di portale di Azure classico tooview hello man mano che diventano disponibili in un grafico. In questa pagina in hello portale classico di Azure, è possibile:

* Selezionare quali tooplot metriche sul grafico hello (hello scelta delle metriche disponibili dipende se si è scelto di monitoraggio dettagliato o minimo per il servizio di hello nella pagina Configurazione hello).
* Selezionare l'intervallo di tempo hello per le metriche di hello visualizzate nel grafico hello.
* Scegliere toouse metriche di hello tooplot una scala assoluta o relativa.
* Configurare toonotify gli avvisi di posta elettronica quando una metrica specifica raggiunge un determinato valore.

Se si desidera metriche hello toodownload per l'archiviazione a lungo termine o tooanalyze usarle in locale, si necessario toouse uno strumento o scrivere codice tabelle hello tooread. È necessario scaricare le metriche al minuto hello per l'analisi. tabelle di Hello non vengono visualizzati se si elencano tutte le tabelle di hello presenti account di archiviazione, ma è possibile accedervi direttamente per nome. Molti strumenti di esplorazione di archiviazione di terze parti sono a conoscenza di queste tabelle e consentono di tooview direttamente (vedere post di blog hello [Esplora archivi di Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) per un elenco degli strumenti disponibili).

### <a name="hourly-metrics"></a>Metriche orarie
* $MetricsHourPrimaryTransactionsBlob
* $MetricsHourPrimaryTransactionsTable
* $MetricsHourPrimaryTransactionsQueue

### <a name="minute-metrics"></a>Metriche al minuto
* $MetricsMinutePrimaryTransactionsBlob
* $MetricsMinutePrimaryTransactionsTable
* $MetricsMinutePrimaryTransactionsQueue

### <a name="capacity"></a>Capacità
* $MetricsCapacityBlob

È possibile trovare i dettagli completi degli schemi di hello delle tabelle in [Schema di tabella delle metriche di archiviazione Analitica](https://msdn.microsoft.com/library/azure/hh343264.aspx). le righe di esempio Hello riportato di seguito mostrano solo un subset di colonne hello disponibili, ma illustrano alcune importanti funzionalità della modalità di hello che metriche di archiviazione Salva le metriche:

| PartitionKey | RowKey | Timestamp | TotalRequests | TotalBillableRequests | TotalIngress | TotalEgress | Disponibilità | AverageE2ELatency | AverageServerLatency | PercentSuccess |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| 20140522T1100 |user;All |2014-05-22T11:01:16.7650250Z |7 |7 |4003 |46801 |100 |104.4286 |6.857143 |100 |
| 20140522T1100 |user;QueryEntities |2014-05-22T11:01:16.7640250Z |5 |5 |2694 |45951 |100 |143.8 |7.8 |100 |
| 20140522T1100 |user;QueryEntity |2014-05-22T11:01:16.7650250Z |1 |1 |538 |633 |100 |3 |3 |100 |
| 20140522T1100 |user;UpdateEntity |2014-05-22T11:01:16.7650250Z |1 |1 |771 |217 |100 |9 |6 |100 |

Nei dati di metrica al minuto in questo esempio, la chiave di partizione hello utilizza ora hello risoluzione minuti. chiave di riga Hello identifica il tipo di hello di informazioni archiviate nella riga hello ed è composta da due tipi di informazioni, il tipo di accesso hello e il tipo di richiesta di hello:

* il tipo di accesso di Hello è l'utente o sistema, in cui utente fa riferimento a servizio di archiviazione toohello richieste utente tooall e ci si riferisce toorequests effettuate da archiviazione Analitica.
* tipo di richiesta Hello è tutte nel qual caso è una riga di riepilogo, oppure identifica hello API specifica, ad esempio QueryEntity o UpdateEntity.

dati di esempio Hello precedente che tutti hello Registra per un singolo minuto (a partire da 11:00 AM), in tal caso hello numerose richieste QueryEntities più hello numero di richieste QueryEntity più hello un numero di richieste UpdateEntity somma tooseven, che è hello totale mostrato in riga user: All Hello. Analogamente, è possibile derivare hello end-to-end latenza media 104.4286 riga user: All hello calcolando ((143.8 * 5) + 3 + 9) / 7.

È consigliabile impostare degli avvisi nella hello portale classico di Azure nella pagina monitoraggio hello in modo che le metriche di archiviazione può notificare automaticamente eventuali importanti modifiche di comportamento hello dei servizi di archiviazione. Se si utilizzano un toodownload strumento soluzioni di archiviazione dati di metrica in un formato delimitato, è possibile utilizzare dati di Microsoft Excel tooanalyze hello. Vedere post di blog hello [Esplora archivi di Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) per un elenco di strumenti di esplorazione di archiviazione disponibile.

## <a name="accessing-metrics-data-programmatically"></a>Accesso ai dati di metrica a livello di codice
Hello seguito è riportato codice c# che accede metrica al minuto per un intervallo di minuti hello e Visualizza risultati hello in una finestra della console. Usa hello libreria di archiviazione di Azure versione 4 che include hello classe CloudAnalyticsClient che semplifica l'accesso alle tabelle di metrica hello nel servizio di archiviazione.

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0 
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
    string.Format("Time: {0}, ", entity.Time) +
    string.Format("AccessType: {0}, ", entity.AccessType) +
    string.Format("TransactionType: {0}, ", entity.TransactionType) +
    string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a>Quali addebiti è necessario sostenere quando si abilitano le metriche di archiviazione?
Scrivere l'entità della tabella toocreate richieste per le metriche vengono addebitate con operazioni di archiviazione di Azure di hello tariffe standard applicabili tooall.

Sono fatturabili in base alle tariffe standard anche le richieste di lettura ed eliminazione da una data toometrics client. Se è stato configurato un criterio di memorizzazione dati, non è necessario sostenere alcun addebito quando Archiviazione di Azure elimina i vecchi dati di metrica. Tuttavia, se si eliminano dati analitica, l'account viene addebitato hello nelle operazioni di eliminazione.

capacità di Hello utilizzata dalle tabelle di metrica hello è fatturabile: è possibile utilizzare hello seguente quantità di hello tooestimate di capacità usata per l'archiviazione dei dati di metrica:

* Se ogni ora un servizio utilizza ogni API in ogni servizio, quindi circa 148KB di dati è ogni ora archiviati nelle tabelle di metrica di transazione hello se è stata abilitata servizio sia a livello dell'API di riepilogo.
* Se ogni ora un servizio utilizza ogni API in ogni servizio, quindi circa 12KB di dati è ogni ora archiviati nelle tabelle di metrica di transazione hello se sono stati abilitati solo i livello di servizio riepilogo.
* Hello tabella della capacità per i BLOB dispone di due righe aggiunte ogni giorno (purché l'utente ha scelto i log): questo implica che ogni giorno hello dimensioni della tabella aumentano da backup tooapproximately 300 byte.

## <a name="next-steps"></a>Passaggi successivi:
[Abilitazione della registrazione di Analisi archiviazione e accesso ai dati di log](https://msdn.microsoft.com/library/dn782840.aspx)
