---
title: Guida di programmazione aaaSCP.NET | Documenti Microsoft
description: Informazioni su come toouse SCP.NET toocreate. Topologie di Storm basata su rete per utilizzano con Storm in HDInsight.
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a>Guida alla programmazione SCP
SCP è una piattaforma toobuild in tempo reale, l'applicazione di elaborazione di dati affidabili, coerenti e a elevate prestazioni. È compilato in cima [Apache Storm](http://storm.incubator.apache.org/) - un flusso di sistema progettato per community hello OSS di elaborazione. Storm è stato progettato da Nathan Marz e reso open source da Twitter. Si avvale [ZooKeeper Apache](http://zookeeper.apache.org/), Apache un altro progetto di coordinamento distribuito in tooenable altamente affidabile e la gestione dello stato. 

Non solo progetto hello SCP trasferita Storm in Windows, ma anche l'aggiunta di progetto hello estensioni e personalizzazione per l'ecosistema di Windows hello. le estensioni di Hello includono esperienza dello sviluppatore .NET e librerie, hello personalizzazione comprende la distribuzione basata su Windows. 

personalizzazione ed estensione hello viene eseguita in modo che i progetti OSS hello toofork non è necessaria, è possibile sfruttare tutte derivati ecosistemi basati su Storm.

## <a name="processing-model"></a>Modello di elaborazione
dati Hello in SCP viene modellati come flussi continui di tuple. In genere hello tuple confluire alcuni coda prima di tutto, quindi prelevato e trasformati dalla logica di business ospitata all'interno di una topologia di Storm, infine output di hello possibile reindirizzare i dati come tuple tooanother SCP sistema oppure essere eseguito il commit toostores come file system distribuito o i database, ad esempio SQL Server.

![Un diagramma di una coda di alimentazione tooprocessing di dati, quale un archivio dati feed](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

In Storm, una topologia applicazione definisce un grafo di elaborazione. Ogni nodo in una topologia contiene logica di elaborazione e i collegamenti tra i nodi indicano il flusso dei dati. Hello nodi tooinject dati di input nella topologia hello vengono chiamati Spouts, che può essere utilizzato toosequence hello dati. Hello dati di input può risiedere nel file log, database transazionale, contatore delle prestazioni di sistema vengono chiamati nodi hello e così via con entrambi i flussi di dati di input e output dadi, quale hello filtrare i dati effettivi e le selezioni e aggregazione.

SCP supporta l'elaborazione dati di tipo best effort, at-least-once ed exactly-once. In un'applicazione di elaborazione di streaming distribuita, possono verificarsi diversi errori durante l'elaborazione di dati, ad esempio un'interruzione di rete, un errore del computer o del codice utente e così via. L'elaborazione di at-least-once garantisce verranno elaborati tutti i dati almeno una volta riproducendo automaticamente hello stessi dati in caso di errore. L'elaborazione at-least-once è semplice e affidabile e offre risultati positivi in molte applicazioni. Tuttavia, quando un'applicazione hello richiede il conteggio esatto, ad esempio, l'elaborazione di at-least-once è insufficiente poiché hello stessi dati potrebbero potenzialmente essere riprodotto nella topologia applicazione hello. In tal caso, esattamente-dopo l'elaborazione è progettata risultato hello che toomake sia corretto, anche quando i dati di hello possono essere riprodotti ed elaborati più volte.

SCP consente alle applicazioni di processo di .NET sviluppatori toodevelop in tempo reale dati hello usare Java Virtual Machine (JVM) basata su Storm sotto coperchio hello. .NET Hello e JVM comunicano tramite socket locale TCP. Ogni beccuccio/fulmine è fondamentalmente una coppia di processo .net/Java, in cui viene eseguita la logica di hello utente nel processo .net come un plug-in.

toobuild un'applicazione nella parte superiore di SCP per l'elaborazione di dati, sono necessari diversi passaggi:

* Progettare e implementare toopull Spouts hello nei dati dalla coda.
* Progettare e implementare i dati di input di bulloni tooprocess hello e salvare dati tooexternal archivi, ad esempio Database.
* Progettare la topologia di hello, inviare ed eseguire topologia hello. Hello topologia definisce vertici e dati hello flussi tra vertici hello. SCP verrà richiedere specifica topologia hello e distribuirlo in un cluster Storm in cui ogni vertice viene eseguito in un nodo logico. failover Hello e ridimensionamento verrà essere preso in considerazione di hello Storm utilità di pianificazione.

Questo documento verrà utilizzato toowalk alcuni semplici esempi come applicazione di elaborazione dei dati toobuild con SCP.

## <a name="scp-plugin-interface"></a>Interfaccia del plug-in SCP
SCP i plug-in o le applicazioni sono file exe autonomo che possono entrambi in esecuzione all'interno di Visual Studio durante la fase di sviluppo hello ed essere collegati alla pipeline Storm hello dopo la distribuzione nell'ambiente di produzione. Scrittura di plug-in hello SCP è appena hello stesso come la scrittura di eventuali altre applicazioni Windows standard console. Piattaforma SCP.NET dichiara un tipo di interfaccia per beccuccio/fulmine e codice di plug-in di hello utente deve implementare queste interfacce. scopo principale di Hello di questa progettazione è che l'utente hello può concentrarsi sulla propria logica di business e lasciando toobe altri elementi gestiti dalla piattaforma SCP.NET.

codice di plug-in di Hello utente deve implementare una delle interfacce seguenti hello, a seconda se la topologia hello è transazionale o non transazionale e se il componente hello è beccuccio o fulmine.

* ISCPSpout
* ISCPBolt
* ISCPTxSpout
* ISCPBatchBolt

### <a name="iscpplugin"></a>ISCPPlugin
ISCPPlugin è l'interfaccia di hello comune per tutti i tipi di plug-in. Attualmente è un'interfaccia fittizia.

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a>ISCPSpout
ISCPSpout è interfaccia hello per beccuccio non transazionale.

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

Quando `NextTuple()` viene chiamato, hello C\# codice utente può creare uno o più tuple. Se non c'è niente tooemit, questo metodo deve restituire senza la creazione di qualsiasi elemento. Si noti che `NextTuple()`, `Ack()` e `Fail()` vengono chiamati in un ciclo ridotto in un singolo thread nel processo C\#. Quando sono non presenti alcun tooemit tuple, è toohave cortesia NextTuple sospensione per un breve periodo di tempo (ad esempio 10 millisecondi) in modo da non toowaste una quantità eccessiva della CPU.

`Ack()` e `Fail()` verranno chiamati solo se il meccanismo di acknowledgement è abilitato nel file delle specifiche. Hello `seqId` tooidentify utilizzati hello tupla che non è riconosciuto o non è riuscita. Pertanto se ack è abilitato nella topologia non transazionale, hello seguono questa funzione deve essere utilizzata in beccuccio:

    public abstract void Emit(string streamId, List<object> values, long seqId); 

Se ack non è supportato nella topologia non transazionale, hello `Ack()` e `Fail()` può essere lasciato come funzione vuoto.

Hello `parms` parametri di input in queste funzioni sono dizionario appena vuoto, riservati per utilizzi futuri.

### <a name="iscpbolt"></a>ISCPBolt
ISCPBolt è interfaccia hello per fulmine non transazionale.

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

Quando sono disponibili nuove tuple hello `Execute()` funzione verrà chiamata tooprocess è.

### <a name="iscptxspout"></a>ISCPTxSpout
ISCPTxSpout è interfaccia hello per beccuccio transazionale.

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

Come avviene per la controparte non transazionale, `NextTx()`, `Ack()` e `Fail()` vengono chiamati in un ciclo ridotto in un singolo thread nel processo C\#. Quando sono non presenti tooemit alcun dati, è toohave cortesia `NextTx` sospensione per un breve periodo di tempo (10 millisecondi) in modo da non toowaste una quantità eccessiva della CPU.

`NextTx()`viene chiamato toostart una nuova transazione hello parametro out `seqId` è usato tooidentify hello transazione, viene utilizzato anche in `Ack()` e `Fail()`. In `NextTx()`, generare lato tooJava dati utente. riproduzione toosupport ZooKeeper verranno archiviati dati Hello. Poiché la capacità di hello di ZooKeeper è molto limitata, l'utente deve creare solo metadati, non i dati di massa beccuccio transazionale.

Storm riprodurrà automaticamente una transazione in caso di errore, dunque in un caso normale `Fail()` non dovrebbe essere chiamato. Ma se SCP è possibile archiviare metadati hello emesso beccuccio transazionale, può chiamare `Fail()` quando hello metadati non sono valido.

Hello `parms` parametri di input in queste funzioni sono dizionario appena vuoto, riservati per utilizzi futuri.

### <a name="iscpbatchbolt"></a>ISCPBatchBolt
ISCPBatchBolt è interfaccia hello per fulmine transazionale.

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

`Execute()`viene chiamato quando è presente una nuova tupla che pervengono a fulmine hello. `FinishBatch()` viene chiamato al termine di questa transazione. Hello `parms` parametro di input è riservato per utilizzi futuri.

Per la topologia transazionale esiste un concetto importante, `StormTxAttempt`. Ha due campi, `TxId` e `AttemptId`. `TxId`è tooidentify utilizzati una transazione specifica e per una determinata transazione, se potrebbero essere presenti più tentativo ha esito negativo e transazione hello riprodotti. SCP.NET nuovo sarà un diverso ISCPBatchBolt oggetto tooprocess ogni `StormTxAttempt`, analogamente a cosa Storm sul lato di Java. scopo di Hello di questa struttura è l'elaborazione delle transazioni parallele toosupport. Utente necessario mantenerla tenga presente che se il tentativo di transazione è terminato, hello corrispondente ISCPBatchBolt oggetto verrà eliminato e raccolti nel Garbage Collector.

## <a name="object-model"></a>Modello a oggetti
SCP.NET fornisce inoltre un semplice set di oggetti chiave per gli sviluppatori tooprogram con. Si tratta degli oggetti **Context**, **StateStore** e **SCPRuntime**, Essi verranno descritte in questa sezione parte rest hello.

### <a name="context"></a>Context
Contesto fornisce un'applicazione toohello ambiente in esecuzione. Ogni istanza di ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) dispone di un'istanza Context corrispondente. funzionalità di Hello fornita dal contesto possono essere suddivisi in due parti: parte statica di hello (1) disponibile in hello C intero\# elaborare, parte dinamica di hello (2) che è disponibile solo per l'istanza contesto hello specifico.

### <a name="static-part"></a>Parte statica
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

`Logger` è fornito a scopi di log.

`pluginType`viene utilizzato tooindicate hello plug-in tipo di hello C\# processo. Se hello C\# processo viene eseguito in modalità test locale (senza Java), il tipo di plug-in di hello è `SCP_NET_LOCAL`.

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

`Config`viene fornito tooget i parametri di configurazione da parte di Java. Hello parametri vengono passati dal lato Java quando C\# plug-in è stato inizializzato. Hello `Config` i parametri sono suddivisi in due parti: `stormConf` e `pluginConf`.

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

`stormConf`è definiti dall'elevato numero di parametri e `pluginConf` è parametri hello definiti dal SCP. ad esempio:

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

`TopologyContext`viene fornito il contesto di topologia hello tooget, risulta maggiormente utile per i componenti con più di parallelismo. Di seguito è fornito un esempio:

    //demo how tooget TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a>Parte dinamica
Hello seguenti interfacce sono pertinente tooa determinato contesto dell'istanza. l'istanza contesto Hello creato dal SCP.NET piattaforma e codice utente toohello passato:

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

Per non transazionale beccuccio supporto ack, verrà fornita al metodo hello:

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

Per non transazionale fulmine supporto ack, dovrebbe essere in modo esplicito `Ack()` o `Fail()` hello tupla ricevuto. E per la creazione dei nuovi tupla, è necessario specificare anche Anchor hello di hello nuova tupla. viene fornito Hello dei seguenti metodi.

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a>StateStore
`StateStore` fornisce servizi metadati, generazione di sequenze monotone e coordinamento senza attesa. `StateStore`consente di creare astrazioni di concorrenza distribuite di livello superiore, tra cui blocchi distribuiti, code distribuite e servizi di transazione.

SCP applicazioni utilizzano hello `State` oggetto toopersist alcune informazioni riportate in ZooKeeper, soprattutto per topologia transazionale. In questo modo, se si blocca beccuccio transazionale e si riavvia, può recuperare le informazioni necessarie hello ZooKeeper e riavviare pipeline hello.

Hello `StateStore` principalmente oggetto dispone di questi metodi:

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

Hello `State` principalmente oggetto dispone di questi metodi:

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

Per hello `Commit()` metodo, quando simpleMode è impostato tootrue, semplicemente eliminerà hello ZNode in ZooKeeper corrispondente. In caso contrario, verrà eliminata hello ZNode corrente e l'aggiunta di un nuovo nodo in hello COMMITTED\_percorso.

### <a name="scpruntime"></a>SCPRuntime
SCPRuntime fornisce hello due metodi seguenti.

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

`Initialize()`è l'ambiente di runtime di tooinitialize utilizzati hello SCP. In questo metodo, hello C\# processo si connetterà lato Java toohello e ottiene i parametri di configurazione e il contesto di topologia.

`LaunchPlugin()`è tookick utilizzato dal messaggio hello l'elaborazione del ciclo. In questo ciclo, hello C\# plug-in verrà visualizzato il modulo di messaggi sul lato di Java (compresi i segnali tuple e controllo), e quindi elaborare i messaggi hello, ad esempio chiamando il metodo di interfaccia hello forniscono codice utente hello. parametro di input per il metodo Hello `LaunchPlugin()` è un delegato che può restituire un oggetto che implementa l'interfaccia ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

Per ISCPBatchBolt, è possibile ottenere `StormTxAttempt` da `parms`e utilizzare toojudge se si tratta di un tentativo di riproduzione. Questa operazione viene in genere eseguita in fulmine commit hello e viene fornita in hello `HelloWorldTx` esempio.

In generale, hello SCP i plug-in possono essere eseguite in due modalità di seguito:

1. Modalità di Test locale: In questa modalità, hello SCP i plug-in (hello C\# codice utente) eseguiti in Visual Studio durante la fase di sviluppo hello. `LocalContext`può essere utilizzato in questa modalità, che fornisce i metodo tooserialize hello generato tuple toolocal file e rileggerle toomemory.
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. Modalità normale: In questa modalità, i plug-in di hello SCP vengono avviati dal processo java storm.
   
    Di seguito è riportato un esempio di avvio del plug-in SCP:
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a>Linguaggio di specifica della topologia
SCP Topology Specification è un linguaggio specifico di dominio (DSL) per la descrizione e la configurazione di topologie SCP. È basato sul DSL di Storm in linguaggio Clojure (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) ed esteso da SCP.

Specifiche di topologia possono essere inviate direttamente toostorm cluster per l'esecuzione tramite hello ***runspec*** comando.

SCP.NET add seguire funzioni toodefine hello transazionale topologia:

| **Nuove funzioni** | **Parametri** | **Descrizione** |
| --- | --- | --- |
| **tx-topolopy** |topology-name<br />spout-map<br />bolt-map |Definire una topologia transazionale con il nome di topologia hello, &nbsp;spouts mappa definizione e hello bulloni definizione mappa |
| **scp-tx-spout** |exec-name<br />args<br />fields |Consente di definire uno Spout transazionale. Verrà eseguito con un'applicazione hello ***exec nome*** utilizzando ***args***.<br /><br />Hello ***campi*** campi di Output di hello per beccuccio |
| **scp-tx-batch-bolt** |exec-name<br />args<br />fields |Consente di definire un Bolt batch transazionale. Verrà eseguito con un'applicazione hello ***exec nome*** utilizzando ***args.***<br /><br />Hello campi sono hello campi di Output per fulmine. |
| **scp-tx-commit-bolt** |exec-name<br />args<br />fields |Consente di definire un Bolt di commit transazionale. Verrà eseguito con un'applicazione hello ***exec nome*** utilizzando ***args***.<br /><br />Hello ***campi*** campi di Output di hello per fulmine |
| **nontx-topolopy** |topology-name<br />spout-map<br />bolt-map |Definire una topologia non transazionale con il nome di topologia hello,&nbsp; spouts mappa definizione e hello bulloni definizione mappa |
| **scp-spout** |exec-name<br />args<br />fields<br />Parametri |Consente di definire uno Spout non transazionale. Verrà eseguito con un'applicazione hello ***exec nome*** utilizzando ***args***.<br /><br />Hello ***campi*** campi di Output di hello per beccuccio<br /><br />Hello ***parametri*** è facoltativo, utilizzarlo toospecify alcuni parametri, ad esempio "nontransactional.ack.enabled". |
| **scp-bolt** |exec-name<br />args<br />fields<br />Parametri |Consente di definire un Bolt non transazionale. Verrà eseguito con un'applicazione hello ***exec nome*** utilizzando ***args***.<br /><br />Hello ***campi*** campi di Output di hello per fulmine<br /><br />Hello ***parametri*** è facoltativo, utilizzarlo toospecify alcuni parametri, ad esempio "nontransactional.ack.enabled". |

In SCP.NET sono disponibili le parole chiave seguenti:

| **Parole chiave** | **Descrizione** |
| --- | --- |
| **:name** |Definire nome topologia hello |
| **:topology** |Definire topologia con hello sopra le funzioni hello e in quelli di compilazione. |
| **:p** |Definire l'hint di parallelismo hello per ogni beccuccio o di un fulmine. |
| **:config** |Definire configurare parametri o aggiornamento hello quelli esistenti |
| **:schema** |Definire hello dello Schema del flusso. |

E i parametri di uso frequente seguenti:

| **Parametro** | **Descrizione** |
| --- | --- |
| **"plugin.name"** |nome di file exe di plug-in hello c# |
| **"plugin.args"** |Argomenti del plug-in. |
| **"output.schema"** |Schema di output. |
| **"nontransactional.ack.enabled"** |Abilitazione o meno dell'acknowledgement per la topologia non transazionale. |

comando runspec Hello verrà distribuito insieme a bits hello, utilizzo di hello è ad esempio:

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

Hello ***risorse dir*** parametro è facoltativo, è necessario toospecify quando si desidera tooplug C\# applicazione e la directory conterrà un'applicazione hello, le dipendenze di hello e configurazioni.

Hello ***classpath*** parametro è facoltativo. È utilizzato toospecify hello Java classpath se file specifica hello contiene Spout Java o fulmine.

## <a name="miscellaneous-features"></a>Funzionalità varie
### <a name="input-and-output-schema-declaration"></a>Dichiarazione dello schema di input e di output
utente Hello può generare una tupla in C\# elaborare, hello piattaforma deve essere tooserialize hello tupla in byte [], trasferimento tooJava lato, e Storm trasferirà questo destinazioni toohello tupla. Nel frattempo nel componente a valle, hello C\# processo ricevere tupla dal lato java e convertirlo tipi originali toohello dalla piattaforma, tutte queste operazioni sono nascosti da hello piattaforma.

serializzazione di hello toosupport e la deserializzazione, il codice utente deve schema hello toodeclare di hello input e output.

schema di flusso di input/output di Hello è definito come un dizionario, hello è hello StreamId e il valore di hello è hello tipi di colonne hello. componente Hello può avere più flussi dichiarati.

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


Nell'oggetto di contesto, abbiamo hello aggiunto API seguente:

    public void DeclareComponentSchema(ComponentStreamSchema schema)

Il codice utente deve assicurarsi che le tuple hello generate rispettano schema hello definito per il flusso, o hello verrà generata un'eccezione di runtime.

### <a name="multi-stream-support"></a>Supporto di più flussi
Utente supporta SCP codice tooemit o ricevere da più flussi distinti a hello stesso tempo. supporto di Hello riflette nell'oggetto di contesto hello hello Emit metodo accetta un parametro di ID flusso facoltativo.

Sono stati aggiunti due metodi nell'oggetto di contesto SCP.NET hello. Sono utilizzati tooemit toospecify StreamId tupla o tuple. Hello StreamId è una stringa e deve toobe coerente in entrambi C\# e hello specifica definizione di topologia.

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

Hello concessioni tooa inesistente flusso causerà le eccezioni di runtime.

### <a name="fields-grouping"></a>Raggruppamento dei campi
Hello compilazione aggiuntivo raggruppamento di campi in Strom non funziona correttamente in SCP.NET. Sul lato di Java Proxy hello, tutti i tipi di dati di campi di hello sono effettivamente byte [] e i campi di hello raggruppamento utilizza hello byte [] oggetto hash tooperform hello raggruppamento di codice. codice hash dell'oggetto Hello byte [] è l'indirizzo di hello di questo oggetto in memoria. Il raggruppamento di hello sarà errato per due byte [] oggetti hello tale condivisione di contenuto ma non hello stesso indirizzo.

SCP.NET aggiunge un metodo di raggruppamento personalizzati e verrà utilizzato il contenuto di hello di raggruppamento hello toodo di hello byte []. In **SPEC** file, la sintassi di hello è ad esempio:

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


Qui

1. "scp-field-group" vuol dire "raggruppamento campi personalizzato implementato da SCP".
2. ":tx" o ":non-tx" indica se si tratta o meno di una topologia transazionale. Queste informazioni è necessario poiché hello indice iniziale è diversa in tx e topologie non tx.
3. [0,1] indica un hashset di Id campo, che parte da 0.

### <a name="hybrid-topology"></a>Topologia ibrida
Hello che Storm native viene scritta in Java. E SCP.Net è migliorato è tooenable nostri toowrite doganali C\# toohandle di codice la logica di business. SCP supporta però anche le topologie ibride, che contengono spout/bolt sia in linguaggio Java sia in C\#.

### <a name="specify-java-spoutbolt-in-spec-file"></a>Specificare gli Spout e i Bolt Java nel file delle specifiche
Nel file specifica, "scp beccuccio" e "scp fulmine" può essere anche usato toospecify Java Spouts e le viti, di seguito è riportato un esempio:

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

Qui `microsoft.scp.example.HybridTopology.Generator` hello nome di classe Java Spout hello.

### <a name="specify-java-classpath-in-runspec-command"></a>Specificare il classpath Java nel comando runSpec
Se si desidera topologia toosubmit contenente Spouts Java o bulloni, necessario toofirst compilazione hello Spouts Java o bulloni e ricevere i file Jar hello. Quindi è necessario specificare il classpath java hello che contiene i file Jar hello durante l'invio di topologia. Di seguito è fornito un esempio:

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

Qui **esempi\\HybridTopology\\java\\destinazione\\**  è la cartella hello contenente file Jar di Java beccuccio/fulmine hello.

### <a name="serialization-and-deserialization-between-java-and-c"></a>Serializzazione e deserializzazione tra Java e C\
Il componente SCP include il lato Java e il lato C\#. In ordine toointeract con bulloni/Spouts Java native, serializzazione/deserializzazione devono essere effettuata tra il lato di Java e C\# sul lato, come illustrato nel seguente grafico hello.

![diagramma del componente java invio componente tooSCP invio tooJava componente](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. **Serializzazione sul lato Java e deserializzazione sul lato C#\#**
   
   Prima di tutto è necessario fornire l'implementazione predefinita per la serializzazione sul lato Java e la deserializzazione sul lato C\#. metodo di serializzazione Hello sul lato di Java può essere specificato nel file specifica:
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   metodo di deserializzazione in C Hello\# lato deve essere specificato in C\# codice utente:
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   Questa implementazione predefinita deve gestire la maggior parte dei casi, se il tipo di dati di hello non è troppo complesso. In alcuni casi, sia perché hello tipo di dati utente è troppo complessa o perché hello prestazioni dell'implementazione predefinita non soddisfano hello requisito dell'utente, è possibile plug-nella propria implementazione.
   
   interfaccia di serializzazione Hello in java lato è definito come:
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   Hello deserializzare interfaccia c\# lato è definito come:
   
   interfaccia pubblica ICustomizedInteropCSharpDeserializer
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. **Serializzazione sul lato C\# e deserializzazione sul lato Java**
   
   metodo di serializzazione in C Hello\# lato deve essere specificato in C\# codice utente:
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   metodo di deserializzazione nel lato Java Hello deve essere specificato nel file specifica:
   
     (scp-spout
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   Ecco di nome hello del deserializzatore "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" e "microsoft.scp.example.HybridTopology.Person" è dati hello classe di destinazione hello vengano deserializzati.
   
   L'utente può anche collegare una propria implementazione del serializzatore C\# e del deserializzatore Java. Si tratta dell'interfaccia hello per C\# serializzatore:
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   Questa è l'interfaccia di hello deserializzatore Java:
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a>Modalità host di SCP
In questa modalità, utente possa compilare tooDLL i codici e utilizzare SCPHost.exe fornito dalla topologia toosubmit SCP. file di specifiche Hello è simile al seguente:

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

Qui `plugin.name` viene specificato come file `SCPHost.exe` fornito dall’SDK di SCP. SCPHost.exe accetta esattamente tre parametri:

1. Hello prima uno è il nome DLL hello, ovvero `"HelloWorld.dll"` in questo esempio.
2. Hello secondo è il nome classe hello, ovvero `"Scp.App.HelloWorld.Generator"` in questo esempio.
3. Hello terzo uno è hello nome di un metodo statico pubblico, che può essere richiamato tooget un'istanza di ISCPPlugin.

In modalità host il codice utente viene compilato come DLL e richiamato dalla piattaforma SCP. Pertanto piattaforma SCP possibile ottenere il controllo completo della logica di elaborazione intero hello. Pertanto si consiglia ai clienti toosubmit topologia in modalità di host SCP poiché può semplificare l'esperienza di sviluppo hello e fine di rendere più flessibilità e una migliore compatibilità con le versioni precedenti per e versioni successive.

## <a name="scp-programming-examples"></a>Esempi di programmazione SCP
### <a name="helloworld"></a>HelloWorld
**HelloWorld** è un esempio molto semplice di tooshow un'idea di SCP.Net. Usa una topologia non transazionale con uno spout denominato **generator** e due bolt denominati **splitter** e **counter**. beccuccio Hello **generatore** verrà generare alcune frasi in modo casuale e generare le frasi troppo**divisione**. fulmine Hello **divisione** verrà suddiviso toowords frasi hello e generare queste parole troppo**contatore** fulmine. Hello fulmine "counter" utilizza un numero di occorrenze dizionario toorecord hello di ogni parola.

Per questo esempio sono presenti due file di specifiche, **HelloWorld.spec** e **HelloWorld\_EnableAck.spec**. In C hello\# codice, è possibile scoprire se ack è abilitato tramite il recupero pluginConf hello da parte di Java.

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

In beccuccio hello, se ack è abilitato, un dizionario è usato toocache hello tuple che non sono stato riconosciuto. Se viene chiamato Fail(), hello tupla verrà riprodotta:

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a>HelloWorldTx
Hello **HelloWorldTx** nell'esempio viene illustrato come tooimplement transazionale topologia. Contiene uno spout denominato **generator**, un bolt batch denominato **partial-count** e un bolt di commit denominato **count-sum**. Sono presenti anche tre file txt già creati: **DataSource0.txt**, **DataSource1.txt** e **DataSource2.txt**.

In ogni transazione, hello beccuccio **generatore** verrà selezionare due file hello tre file creato in precedenza in modo casuale e generare hello due file nomi toohello **conteggio parziale** fulmine. fulmine Hello **conteggio parziale** verrà innanzitutto ottenere il nome di file hello dalla tupla hello ricevuto, hello Apri file e conteggio hello il numero di parole in questo file e infine creare hello word numero toohello **conteggio, somma**fulmine. Hello **conteggio somma** fulmine riepiloga il numero totale di hello.

tooachieve **esattamente una volta** semantica, fulmine commit hello **conteggio somma** toojudge è necessario se si tratta di una transazione di riproduzione. In questo esempio, contiene una variabile membro statica:

    public static long lastCommittedTxId = -1; 

Quando viene creata un'istanza di ISCPBatchBolt, otterrà hello `txAttempt` da parametri di input:

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

Quando `FinishBatch()` viene chiamato, hello `lastCommittedTxId` sarà update se non è una transazione di riproduzione.

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a>HybridTopology
Questa topologia contiene uno spout Java e un bolt C\#. Usa hello la serializzazione e deserializzazione l'implementazione predefinita fornita dalla piattaforma SCP. Eseguire hello ref **HybridTopology.spec** in **esempi\\HybridTopology** cartella hello specifica dettagli dei file, e **SubmitTopology.bat** per informazioni su come classpath Java toospecify.

### <a name="scphostdemo"></a>SCPHostDemo
In pratica, questo esempio è hello come HelloWorld. Hello unica differenza è che il codice utente hello viene compilato come DLL e topologia hello viene inviata tramite SCPHost.exe. Fare riferimento hello sezione "SCP Host alla modalità" per informazioni più dettagliate.

## <a name="next-steps"></a>Passaggi successivi
Per esempi di topologie di Storm create utilizzando SCP, vedere l'esempio hello:

* [Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [Creare più flussi di dati in una topologia Storm C#](hdinsight-storm-twitter-trending.md)
* [Utilizzare i dati di Power Bi toovisualize da una topologia di Storm](hdinsight-storm-power-bi-topology.md)
* [Elaborare i dati del sensore veicolo dall'hub di eventi usando Storm in HDInsight](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [Estrazione, trasformazione e caricamento (ETL) da tooHBase hub eventi di Azure](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [Correlare gli eventi  con Storm e HBase in HDInsight](hdinsight-storm-correlation-topology.md)

