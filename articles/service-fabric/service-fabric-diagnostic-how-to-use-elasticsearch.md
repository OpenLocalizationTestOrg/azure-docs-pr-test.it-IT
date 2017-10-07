---
title: aaaUsing Elasticsearch come archivio di analisi applicazione di Service Fabric | Documenti Microsoft
description: "Descrive come è possono utilizzare le applicazioni di Service Fabric toostore Elasticsearch e Kibana, indicizzazione e ricerca tramite tracce di applicazione (log)"
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: adegeo
editor: 
ms.assetid: e59b0c39-e468-4d9e-b453-d5f2a8ad20d8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: karolz@microsoft.com
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: b5977c54e69319e3caa376e44a02f971b66a3254
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>Usare ElasticSearch come archivio di traccia delle applicazioni di Service Fabric
## <a name="introduction"></a>Introduzione
Questo articolo descrive le modalità in cui le applicazioni di [Azure Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric/) possono usare **ElasticSearch** e **Kibana** per l'archiviazione delle tracce, l'indicizzazione e la ricerca. [ElasticSearch](https://www.elastic.co/guide/index.html) è un motore di ricerca e analisi open source, distribuito e scalabile in tempo reale, nonché particolarmente adatto per questa attività, che può essere installato in macchine virtuali Windows o Linux con Microsoft Azure. Elasticsearch può elaborare in modo efficiente tracce *strutturate* create con tecnologie come **Event Tracing for Windows (ETW)**.

ETW è usato da informazioni di diagnostica toosource runtime Service Fabric (tracce). È hello metodo consigliato per Service Fabric applicazioni toosource le informazioni di diagnostica, troppo. Utilizzo di hello consente stesso meccanismo per la correlazione tra tracce fornito dal runtime e fornita dall'applicazione e facilita la risoluzione dei problemi semplificata. Modelli di progetto Service Fabric in Visual Studio includono un'API di registrazione (in base a hello .NET **EventSource** classe) che emette le tracce ETW per impostazione predefinita. Per una panoramica generale sulla definizione delle tracce delle applicazioni di Service Fabric con ETW, vedere [Monitorare e diagnosticare servizi in una configurazione di sviluppo con computer locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

Per tooshow tracce hello backup in Elasticsearch, hanno bisogno toobe acquisiti nei nodi del cluster di Service Fabric hello in tempo reale (quando è in esecuzione un'applicazione hello) e inviati tooan Elasticsearch endpoint. Per l'acquisizione di tracce sono disponibili due opzioni principali:

* **Acquisizione di tracce in-process**  
  un'applicazione Hello o più precisamente, processo del servizio, è responsabile per l'invio all'archivio di analisi hello dati di diagnostica toohello (Elasticsearch).
* **Acquisizione di tracce out-of-process**  
  Un agente distinto è acquisire tracce da servizio hello o più processi e inviarli toohello archivio di analisi.

Di seguito, viene descritto come tooset backup Elasticsearch in Azure, discutere i professionisti hello e gli svantaggi di entrambe le opzioni di acquisizione e spiegano come tooconfigure un'infrastruttura di servizio del servizio toosend dati tooElasticsearch.

## <a name="set-up-elasticsearch-on-azure"></a>Configurare ElasticSearch in Azure
Hello tooset modo più semplice il servizio Elasticsearch hello in Azure viene eseguita tramite [ **modelli di gestione risorse di Azure**](../azure-resource-manager/resource-group-overview.md). Un [modello di avvio rapido di Azure Resource Manager per ElasticSearch](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) è disponibile nel repository dei modelli di avvio rapido di Azure. Questo modello usa account di archiviazione separati per le unità di scala (gruppi di nodi) e può effettuare il provisioning di nodi client e server distinti con configurazioni diverse e un numero variabile di dischi dati collegati.

Qui, si utilizza un modello diverso, denominato **ES MultiNode** da hello [archivio degli strumenti di diagnostica Azure](https://github.com/Azure/azure-diagnostics-tools). Questo modello è più facile toouse e viene creato un cluster Elasticsearch protetto dall'autenticazione di base HTTP. Prima di continuare, scaricare repository hello dalla macchina tooyour GitHub (per la clonazione del repository hello o download di un file zip). Hello ES MultiNode modello si trova nella cartella hello con hello stesso nome.

### <a name="prepare-a-machine-toorun-elasticsearch-installation-scripts"></a>Preparare un toorun macchina Elasticsearch gli script di installazione
Hello modello di hello ES MultiNode toouse modo più semplice è tramite uno script di PowerShell di Azure fornito denominato `CreateElasticSearchCluster`. toouse questo script, è necessario uno strumento denominato e moduli tooinstall **openssl**. Hello quest'ultimo è necessaria per la creazione di una chiave SSH che può essere utilizzati tooadminister Elasticsearch cluster in modalità remota.

`CreateElasticSearchCluster`script è progettato per facilitare l'utilizzo con il modello di hello ES MultiNode da un computer Windows. È possibile toouse hello al modello in un computer non Windows, ma tale scenario esula dall'ambito di hello di questo articolo.

1. Se non sono già stati installati, installare i [**moduli di Azure PowerShell**](http://aka.ms/webpi-azps). Quando richiesto, fare clic su **Esegui** e su **Installa**. È richiesto Azure PowerShell 1.3 o versioni successive.
2. Hello **openssl** lo strumento è incluso nella distribuzione hello di [ **Git per Windows**](http://www.git-scm.com/downloads). Se non è già stato fatto, installare [Git per Windows](http://www.git-scm.com/downloads) . le opzioni di installazione predefinite hello sono OK.
3. Supponendo che Git è stato installato ma non inclusi nel percorso di sistema hello, aprire una finestra di Microsoft Azure PowerShell ed eseguire hello seguenti comandi:
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    Sostituire hello `<Git installation folder>` con percorso di hello Git nel computer; valore predefinito di hello è **"C:\Programmi\Microsoft Files\Git"**. Si noti il carattere punto e virgola hello all'inizio di hello del primo percorso hello.
4. Verificare che si è connessi tooAzure (tramite [ `Add-AzureRmAccount` ](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet) e di aver selezionato una sottoscrizione di hello che deve essere utilizzato il cluster di ricerca elastico toocreate. Per verificare che sia selezionata la sottoscrizione corretta, è possibile usare i cmdlet `Get-AzureRmContext` e `Get-AzureRmSubscription`.
5. Se non è già fatto, Modifica cartella toohello ES MultiNode della directory corrente hello.

### <a name="run-hello-createelasticsearchcluster-script"></a>Eseguire script CreateElasticSearchCluster hello
Prima di eseguire script hello, aprire hello `azuredeploy-parameters.json` file e verificare o fornire valori per parametri di script hello. viene fornito Hello seguenti parametri:

| Nome parametro | Description |
| --- | --- |
| dnsNameForLoadBalancerIP |Hello nome toocreate utilizzati hello visibili pubblicamente nome DNS cluster ricerca elastico hello (aggiungendo toohello fornito di dominio di hello regione di Azure). Ad esempio, se il valore del parametro è "myBigCluster" e area di Azure hello scelto è Stati Uniti occidentali, hello risultante nome DNS cluster hello è myBigCluster.westus.cloudapp.azure.com. <br /><br />Questo nome funge anche da un nome radice per tutti gli elementi associati hello ricerca elastico cluster, ad esempio i nomi dei nodi di dati. |
| adminUsername |nome di Hello dell'account di amministratore hello per la gestione dei cluster di ricerca elastico hello (chiavi SSH corrispondenti vengono generate automaticamente). |
| dataNodeCount |numero di Hello di nodi nel cluster ricerca elastico hello. la versione corrente di Hello dello script di hello non distingue tra nodi di dati e query. tutti i nodi riprodurre entrambi ruoli. Nodi too3 valori predefiniti. |
| dataDiskSize |dimensione di Hello dei dischi di dati (in GB) allocata per ogni nodo di dati. Ogni nodo riceve 4 dischi dati, in modo esclusivo dedicato tooElastic servizio di ricerca. |
| region |nome Hello dell'area di Azure in cui deve essere collocato cluster ricerca elastico hello. |
| esUserName |Hello nome utente dell'utente hello che viene configurato toohave accesso tooES cluster (soggetto tooHTTP l'autenticazione di base). Hello password non fa parte del file di parametri e deve essere specificata quando `CreateElasticSearchCluster` script viene richiamato. |
| vmSizeDataNodes |dimensioni di macchina virtuale di Azure per i nodi del cluster ricerca elastico Hello. TooStandard_D2 impostazioni predefinite. |

Si è ora script hello toorun pronto. Eseguire hello comando seguente:

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

dove 

| Nome del parametro di script | Descrizione |
| --- | --- |
| `<es-group-name>` |nome Hello hello Azure del gruppo di risorse che conterrà tutte le risorse cluster ricerca elastico. |
| `<azure-region>` |nome Hello dell'area di Azure in cui deve essere creato il cluster di ricerca elastico hello hello. |
| `<es-password>` |password di Hello per hello elastico ricerca utente. |

> [!NOTE]
> Se si verifica un'eccezione NullReferenceException dal cmdlet hello AzureResourceGroup di Test, è stata dimenticata toolog su tooAzure (`Add-AzureRmAccount`).
> 
> 

Se si verifica un errore dell'esecuzione dello script hello e si stabilisce che l'errore hello è stato causato da un valore di parametro di modello errato, correggere il file di parametro hello ed eseguire script hello nuovamente con il nome di un gruppo di risorse diverso. È inoltre possibile riutilizzare hello stesso nome del gruppo di risorse e dispone di script hello pulizia hello precedente aggiungendo hello `-RemoveExistingResourceGroup` chiamata dello script toohello di parametro.

### <a name="result-of-running-hello-createelasticsearchcluster-script"></a>Risultato dell'esecuzione di script CreateElasticSearchCluster hello
Dopo aver eseguito hello `CreateElasticSearchCluster` script, verrà creato hello segue gli elementi principali. In questo esempio si presuppone che si usa "myBigCluster" come valore di hello di hello `dnsNameForLoadBalancerIP` parametro e tale area hello in cui è stato creato il cluster hello è Stati Uniti occidentali.

| Elemento | Nome, percorso e note |
| --- | --- |
| Chiave SSH per l'amministrazione remota |file myBigCluster.key (nella directory hello da quale hello è stato eseguito CreateElasticSearchCluster). <br /><br />Questo file di chiave può essere utilizzato tooconnect toohello admin nodo e (tramite nodo Amministrazione hello) toodata nodi nel cluster hello. |
| Nodo amministratore |myBigCluster admin.westus.cloudapp.azure.com  <br /><br />Una macchina virtuale dedicata per l'amministrazione remota del cluster di Elasticsearch - hello solo uno che consenta le connessioni SSH esterne. Viene eseguito nella stessa rete virtuale come tutti i nodi del cluster Elasticsearch hello, ma non eseguita servizi Elasticsearch hello. |
| Nodi dati |myBigCluster1 … myBigCluster*N* <br /><br />Nodi di dati che eseguono servizi Elasticsearch e Kibana. È possibile connettersi tramite SSH tooeach nodo, ma solo tramite nodo Amministrazione hello. |
| Cluster Elasticsearch |http://myBigCluster.westus.cloudapp.azure.com/es/ <br /><br />Hello endpoint primario per il cluster di Elasticsearch hello (suffisso /es di hello nota). È protetta da autenticazione HTTP di base (hello credenziali hello specificato esUserName/esPassword parametri di modello hello ES MultiNode). cluster Hello presenta inoltre hello head plug-in installati (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head) per l'amministrazione del cluster di base. |
| Servizio Kibana |http://myBigCluster.westus.cloudapp.azure.com <br /><br />Hello Kibana servizio impostare dati tooshow da hello Elasticsearch cluster creato. È protetta da hello stesse credenziali di autenticazione come hello del cluster stesso. |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>Acquisizione di tracce in-process e out-of-process
Introduzione di hello, accennato in due modi fondamentali per la raccolta dei dati di diagnostica: in-process e out-of-process. Ognuna presenta vantaggi e svantaggi.

Vantaggi di hello **nel processo di acquisizione traccia** includono:

1. *Facilità di configurazione e distribuzione*
   
   * configurazione di Hello di raccolta dati di diagnostica è solo parte della configurazione dell'applicazione hello. È facile tooalways keep "sincronizzato" con hello il resto dell'applicazione hello.
   * È facile ottenere la configurazione per ogni applicazione o servizio.
   * Acquisizione traccia out-of-process richiede in genere una distribuzione separata e la configurazione dell'agente, diagnostica hello è un'attività amministrativa extra e una potenziale fonte di errori. tecnologia di agente specifico Hello consente spesso di solo un'istanza dell'agente di hello per ogni macchina virtuale (nodo). Ciò significa che la configurazione per la raccolta hello della configurazione di diagnostica hello viene condiviso tra tutte le applicazioni e servizi in esecuzione su tale nodo.
2. *Flessibilità*
   
   * un'applicazione Hello può inviare dati di hello ogni volta che è necessario toogo, purché vi è una libreria client che supporta il sistema di archiviazione dati hello di destinazione. Nuovi sink possono essere aggiunti secondo le esigenze.
   * È possibile implementare complesse regole di acquisizione, filtro e aggregazione dati.
   * Un'acquisizione della traccia out-of-process è spesso limitato dal sink dati hello che hello agente supporta. Alcuni agenti sono estendibili.
3. *Contesto e accedere ai dati di applicazione toointernal*
   
   * sottosistema di diagnostica Hello in esecuzione nel processo di applicazioni o servizi hello possibile integrare facilmente le tracce di hello con informazioni contestuali.
   * Nell'approccio a out-of-process hello, hello devono essere inviati dati agente tooan tramite un meccanismo di comunicazione tra processi, ad esempio Event Tracing for Windows. Questo meccanismo può imporre limitazioni aggiuntive.

Vantaggi di hello **acquisizione traccia out-of-process** includono:

1. *un'applicazione hello toomonitor possibilità Hello e raccogliere i dump di arresto anomalo*
   
   * Acquisizione traccia in-process può essere esito negativo se un'applicazione hello toostart o arresti anomali. Un agente indipendente ha maggiori possibilità di acquisire informazioni cruciali sulla risoluzione dei problemi.<br /><br />
2. *Maturità, affidabilità e prestazioni comprovate*
   
   * Un agente sviluppato da un fornitore di piattaforma (ad esempio, un agente di Microsoft Azure Diagnostics) è stata toorigorous oggetto test e la protezione avanzata di battaglia.
   * Con la traccia nel processo di acquisizione, prestare attenzione tooensure attività hello di invio dei dati di diagnostica da un processo dell'applicazione non interferire con l'attività principale dell'applicazione hello o introdurre problemi di temporizzazione o prestazioni. Un agente in modo indipendente in esecuzione è meno soggetto a problemi toothese ed è specificamente progettato toolimit impatto sul sistema hello.

È possibile toocombine e trarre vantaggio da entrambi gli approcci. Infatti, potrebbe essere la soluzione migliore di hello per molte applicazioni.

In questo caso, utilizziamo hello **Microsoft.Diagnostic.Listeners libreria** e di traccia in-process hello acquisizione dei dati toosend da un cluster di Service Fabric application tooan Elasticsearch.

## <a name="use-hello-listeners-library-toosend-diagnostic-data-tooelasticsearch"></a>Utilizzare hello listener libreria toosend dati di diagnostica tooElasticsearch
libreria Microsoft.Diagnostic.Listeners Hello è parte dell'applicazione di Service Fabric esempio PartyCluster. toouse è:

1. Scaricare [: esempio hello PartyCluster](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster) da GitHub.
2. Copiare hello Microsoft.Diagnostics.Listeners e Microsoft.Diagnostics.Listeners.Fabric progetti (intere cartelle) dalla cartella di soluzione toohello per la directory esempio hello PartyCluster dell'applicazione hello che dovrebbe toosend hello dati tooElasticsearch .
3. Aprire una soluzione di destinazione hello, fare doppio clic su nodo della soluzione in Esplora soluzioni hello hello e scegliere **Aggiungi progetto esistente**. Aggiunge una soluzione hello Microsoft.Diagnostics.Listeners progetto toohello. Ripetere il passaggio hello stesso per il progetto Microsoft.Diagnostics.Listeners.Fabric hello.
4. Aggiungere un riferimento al progetto da uno o più progetti toohello due aggiunto progetti di servizi di. (Ogni servizio che si suppone toosend dati tooElasticsearch deve fare riferimento a Microsoft.Diagnostics.EventListeners e Microsoft.Diagnostics.EventListeners.Fabric).
   
    ![Progetto fa riferimento a tooMicrosoft.Diagnostics.EventListeners e librerie Microsoft.Diagnostics.EventListeners.Fabric][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>Versione di disponibilità generale di Service Fabric e pacchetto NuGet Microsoft.Diagnostics.Tracing
Il framework di destinazione delle applicazioni compilate con la versione di disponibilità generale di Service Fabric (2.0.135, rilasciata il 31 marzo 2016) è **.NET Framework 4.5.2**. Questa versione è hello versione più recente di .NET Framework supportata da Azure in fase di hello della versione di hello GA hello. Sfortunatamente, questa versione di hello framework non dispone di alcune APIs EventListener tale libreria deve Microsoft.Diagnostics.Listeners hello. Poiché sono strettamente collegati EventSource (componente hello che costituisce la base hello di registrazione API nelle applicazioni di infrastruttura) ed EventListener, ogni progetto che utilizza hello Microsoft.Diagnostics.Listeners libreria deve utilizzare un'implementazione alternativa del EventSource. Questa implementazione è fornita dalla hello **pacchetto Microsoft.Diagnostics.Tracing Nuget**, creati da Microsoft. pacchetto Hello è completamente compatibile con EventSource incluso nel framework di hello, pertanto alcuna modifica del codice non dovrebbe essere necessario oltre a cui viene fatto riferimento dello spazio dei nomi.

toostart utilizzando hello Microsoft.Diagnostics.Tracing implementazione della classe EventSource hello, seguire questi passaggi per ogni progetto di servizio che deve toosend dati tooElasticsearch:

1. Fare clic sul progetto di servizio hello e scegliere **Gestisci pacchetti Nuget**.
2. Passare l'origine del pacchetto nuget.org toohello (se non è già selezionata) e cercare "**Microsoft.Diagnostics.Tracing**".
3. Installare hello `Microsoft.Diagnostics.Tracing.EventSource` pacchetto (e le relative dipendenze).
4. Aprire hello **ServiceEventSource.cs** o **ActorEventSource.cs** file nel progetto di servizio e sostituire hello `using System.Diagnostics.Tracing` direttiva sopra file hello con hello `using Microsoft.Diagnostics.Tracing` direttiva.

Questi passaggi non sono necessari una volta hello **.NET Framework 4.6** è supportata da Microsoft Azure.

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>Creazione dell'istanza e configurazione del listener ElasticSearch
Hello passaggio finale per l'invio di dati di diagnostica tooElasticsearch è toocreate un'istanza di `ElasticSearchListener` e configurarlo con i dati di connessione Elasticsearch. listener Hello acquisisce automaticamente tutti gli eventi generati tramite classi EventSource definite nel progetto di servizio hello. È necessario che toobe alive nel corso della durata hello del servizio di hello, in modo migliore hello inserire toocreate è presente nel codice di inizializzazione servizio hello. Ecco come codice di inizializzazione hello per un servizio senza stato può apparire dopo le modifiche necessarie hello (aggiunte indicata nei commenti a partire da `****`):

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add hello following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>        
        private static void Main()
        {
            try
            {
                // **** Instantiate ElasticSearchListener
                var configProvider = new FabricConfigurationProvider("ElasticSearchEventListener");
                ElasticSearchListener esListener = null;
                if (configProvider.HasConfiguration)
                {
                    esListener = new ElasticSearchListener(configProvider, new FabricHealthReporter("ElasticSearchEventListener"));
                }

                // hello ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name tooa .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of hello class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that hello ElasticSearchListner instance is not garbage-collected prematurely
                GC.KeepAlive(esListener);
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e);
                throw;
            }
        }
    }
}
```

Dati di connessione Elasticsearch dovrebbero essere inseriti in una sezione distinta nel file di configurazione del servizio hello (**PackageRoot\Config\Settings.xml**). nome Hello della sezione di hello deve corrispondere il valore di toohello passato toohello `FabricConfigurationProvider` costruttore, ad esempio:

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
i valori di Hello `serviceUri`, `userName` e `password` parametri corrispondono toohello Elasticsearch indirizzo dell'endpoint del cluster, Elasticsearch nome di utente e password, rispettivamente. `indexNamePrefix`è un prefisso per gli indici Elasticsearch; hello libreria Microsoft.Diagnostics.Listeners Hello crea un nuovo indice per i propri dati ogni giorno.

### <a name="verification"></a>Verifica
L'operazione è terminata. A questo punto, ogni volta che viene eseguito il servizio di hello, viene avviato l'invio del servizio di Elasticsearch toohello tracce specificato nella configurazione di hello. È possibile verificarlo hello apertura che kibana UI associata hello destinazione Elasticsearch istanza. In questo esempio, l'indirizzo della pagina hello è http://myBigCluster.westus.cloudapp.azure.com/. Verificare che gli indici con prefisso del nome hello scelto per hello `ElasticSearchListener` istanza effettivamente creato e popolato con i dati.

![Eventi di Kibana che mostrano l'applicazione PartyCluster][2]

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni sulla diagnostica e il monitoraggio di un servizio di infrastruttura di servizi](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png
