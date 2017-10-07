---
title: topologie di Storm aaaApache con Visual Studio e Visual c# - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come le topologie di Storm toocreate in c#. Creare una topologia di conteggio parole semplice in Visual Studio utilizzando gli strumenti di hello Hadoop per Visual Studio.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a>Sviluppare le topologie di c# per Apache Storm utilizzando gli strumenti di Data Lake hello per Visual Studio

Informazioni su come toocreate una topologia c# Storm utilizzando hello Azure Data Lake (Hadoop) degli strumenti per Visual Studio. Questo documento descrive fasi hello della creazione di un progetto di Storm in Visual Studio, eseguire il test in locale e distribuirlo tooan Apache Storm nel cluster HDInsight di Azure.

Verrà inoltre descritto come le topologie di toocreate ibride che utilizzano componenti di c# e Java.

> [!NOTE]
> Durante i passaggi di hello in questo documento si basano su un ambiente di sviluppo Windows con Visual Studio, progetto compilato hello può essere inviato tooeither un cluster HDInsight basati su Windows o di Linux. Solo i cluster basati su Linux creati dopo il 28 ottobre 2016 supportano le topologie SCP.NET.

topologia toouse c# con un cluster basato su Linux, è necessario aggiornare hello pacchetto Microsoft.SCP.Net.SDK NuGet usato per il tooversion progetto 0.10.0.6 o versione successivo. versione di Hello del pacchetto di hello deve corrispondere anche versione principale di hello di Storm installato in HDInsight.

| Versione HDInsight | Versione di Storm | Versione di SCP.NET | Versione Mono predefinita |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| 3.3 |0.10.x |0.10.x.x</br>(solo in HDInsight per Windows) | ND |
| 3.4 | 0.10.0.x | 0.10.0.x | 3.2.8 |
| 3,5 | 1.0.2.x | 1.0.0.x | 4.2.1 |
| 3.6 | 1.1.0.x | 1.0.0.x | 4.2.8 |

> [!IMPORTANT]
> C# topologie nei cluster basati su Linux è necessario utilizzare .NET 4.5 e toorun Mono nel cluster HDInsight hello. Controllare la [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/) per potenziali problemi di incompatibilità.

## <a name="install-visual-studio"></a>Installazione di Visual Studio

È possibile sviluppare le topologie di c# con SCP.NET utilizzando una delle seguenti versioni di Visual Studio hello:

* Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)

* Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)

* Visual Studio 2015 o [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)

* Visual Studio 2017, qualsiasi edizione

## <a name="install-data-lake-tools-for-visual-studio"></a>Installare gli strumenti Data Lake per Visual Studio

gli strumenti di Data Lake tooinstall per Visual Studio, seguire i passaggi di hello in [iniziare a usare gli strumenti di Data Lake per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a name="install-java"></a>Installare Java

Quando si invia una topologia di Storm da Visual Studio, SCP.NET genera un file zip che contiene le dipendenze e la topologia di hello. Java è toocreate utilizzati questi file, di zip perché utilizza un formato che è più compatibile con cluster basati su Linux.

1. Installare hello Java Developer Kit (JDK) 7 o versione successiva in ambiente di sviluppo. È possibile ottenere hello Oracle JDK da [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html). È inoltre possibile usare [altre distribuzioni Java](http://openjdk.java.net/).

2. Hello `JAVA_HOME` directory di toohello punto deve variabile di ambiente contenente Java.

3. Hello `PATH` variabile di ambiente deve includere hello `%JAVA_HOME%\bin` directory.

È possibile utilizzare hello seguente c# console application tooverify Java e hello JDK siano installati correttamente:

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a>Modelli Storm

gli strumenti di Data Lake Hello per Visual Studio forniscono hello seguenti modelli:

| Tipo di progetto | Dimostra |
| --- | --- |
| Applicazione Storm |Un progetto di topologia Storm vuoto |
| Esempio di writer SQL di Azure per Storm |Come toowrite tooAzure Database SQL. |
| Esempio di reader Storm per Azure Cosmos DB |Come tooread dal database di Azure Cosmos. |
| Esempio di writer Storm per Azure Cosmos DB |Come toowrite tooAzure DB Cosmos. |
| Esempio di lettore EventHub per Storm |Come tooread dagli hub di eventi di Azure. |
| Esempio di writer EventHub per Storm |Come toowrite tooAzure hub eventi. |
| Esempio di lettore HBase per Storm |Come cluster tooread da HBase in HDInsight. |
| Esempio di writer HBase per Storm |Come cluster tooHBase toowrite in HDInsight. |
| Esempio ibrido di Storm |Come toouse un componente di Java. |
| Esempio di Storm |Topologia di conteggio parole di base |

> [!WARNING]
> Non tutti i modelli funzionano con HDInsight basato su Linux. Pacchetti NuGet usati dai modelli hello potrebbero non essere compatibili con Mono. Controllare hello [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/) dei documenti e utilizzare hello [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potenziali problemi.

Nei passaggi hello in questo documento, utilizzare hello base tempesta applicazione progetto tipo toocreate una topologia.

### <a name="hbase-templates-notes"></a>Note sui modelli HBase

Hello HBase lettore e modelli di writer utilizzano hello l'API REST HBase non hello API Java HBase, toocommunicate con un HBase nel cluster HDInsight.

### <a name="eventhub-templates-notes"></a>Note sui modelli EventHub

> [!IMPORTANT]
> Hello basati su Java EventHub spout componente incluso con hello modello EventHub lettore potrebbe non funzionare con Storm in HDInsight 3.5 o versione successiva. Una versione aggiornata di questo componente è disponibile in [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).

Per una topologia di esempio che usa questo componente e funziona con Storm in HDInsight 3.5, vedere [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

## <a name="create-a-c-topology"></a>Creare una topologia C#

1. Aprire Visual Studio, selezionare **File** > **Nuovo** e quindi **Progetto**.

2. Da hello **nuovo progetto** finestra, espandere **installato** > **modelli**e selezionare **Azure Data Lake**. Selezionare nell'elenco dei modelli di hello **Storm applicazione**. In basso hello hello, immettere **WordCount** come nome di hello dell'applicazione hello.

    ![Screenshot della finestra Nuovo progetto](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. Dopo aver creato il progetto di hello, è necessario avere i seguenti file hello:

   * **Program.cs**: questo file definisce topologia hello per il progetto. Per impostazione predefinita viene creata una topologia predefinita costituita da uno spout e da un bolt.

   * **Spout.cs**: spout di esempio che genera numeri casuali.

   * **BOLT.cs**: un fulmine di esempio che mantiene un conteggio dei numeri generati da beccuccio hello.

     Quando si crea il progetto di hello, download NuGet hello più recente [SCP.NET pacchetto](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a>Beccuccio hello implementare

1. Aprire **Spout.cs**. Spouts sono dati tooread utilizzato in una topologia da un'origine esterna. componenti principali di Hello per beccuccio sono:

   * **NextTuple**: chiamato da Storm beccuccio hello è consentito tooemit nuove Tuple.

   * **ACK** (solo per topologia transazionale): gestisce i riconoscimenti da altri componenti nella topologia hello per le tuple inviate da beccuccio hello. Una conferma di una tupla consente beccuccio hello di sapere che è stata elaborata correttamente dai componenti a valle.

   * **Esito negativo** (solo per topologia transazionale): gestisce le tuple che sono non è riuscita l'elaborazione di altri componenti della topologia hello. Implementazione di un metodo Fail consente toore-emit hello tupla in modo che possa essere elaborato nuovamente.

2. Sostituire il contenuto di hello di hello **Spout** classe con hello dopo il testo. Questo beccuccio genera in modo casuale una frase nella topologia hello.

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a>Implementare bulloni hello

1. Eliminare hello esistente **Bolt.cs** file dal progetto hello.

2. In **Esplora**, fare clic sul progetto hello e selezionare **Aggiungi** > **nuovo elemento**. Selezionare nell'elenco hello **Storm fulmine**e immettere **Splitter.cs** come nome hello. Ripetere questo processo toocreate denominato di un fulmine secondo **Counter.cs**.

   * **Splitter.cs**: implementa un bolt che divide le frasi in singole parole e crea un nuovo flusso di parole.

   * **Counter.cs**: implementa un fulmine che il conteggio di ogni parola e genera un nuovo flusso di parole e conteggio hello per ogni parola.

     > [!NOTE]
     > Questi dadi leggere e scrivere toostreams, ma è inoltre possibile utilizzare un toocommunicate fulmine con origini, ad esempio un database o un servizio.

3. Aprire **Splitter.cs**. Per impostazione predefinita, dispone soltanto del metodo **Execute**. metodo Execute Hello viene chiamato quando fulmine hello riceve una tupla per l'elaborazione. È possibile leggere ed elaborare tuple in ingresso e generare tuple in uscita.

4. Sostituire il contenuto di hello di hello **divisione** classe con hello seguente codice:

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. Aprire **Counter.cs**e sostituire il contenuto di classe hello con hello seguente:

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a>Definire la topologia hello

Spouts e le viti vengono disposte in un grafico, che definisce il flusso dei dati hello tra componenti. Per questa topologia, hello è come segue:

![Diagramma della disposizione degli elementi](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

Frasi vengono emessi da beccuccio hello e sono distribuite tooinstances di fulmine divisione hello. fulmine divisione Hello interrompe frasi hello in parole, che sono distribuite toohello fulmine di contatore.

Poiché il conteggio di word viene mantenuto localmente nell'istanza di contatore hello, si desidera assicurarsi che le parole specifiche flusso toohello toomake stessa istanza di contatore fulmine. Ogni istanza tiene traccia di una parola specifica. Poiché fulmine divisione hello non mantiene lo stato, effettivamente non è importante che l'istanza della barra di divisione hello riceve quali frase.

Aprire **Program.cs**. metodo importante Hello è **GetTopologyBuilder**, ovvero topologia hello toodefine utilizzati che viene inviato tooStorm. Sostituire il contenuto di hello di **GetTopologyBuilder** con hello seguente topologia di hello tooimplement codice descritta in precedenza:

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a>Inviare hello topologia

1. In **Esplora**, fare clic sul progetto hello e selezionare **inviare tooStorm in HDInsight**.

   > [!NOTE]
   > Se richiesto, immettere le credenziali di hello per la sottoscrizione di Azure. Se si dispone di più di una sottoscrizione, accedere toohello uno che contiene l'elevato numero di cluster HDInsight.

2. Selezionare l'elevato numero di cluster HDInsight da hello **Cluster Storm** elenco a discesa e quindi selezionare **Invia**. È possibile monitorare se invio hello ha esito positivo tramite hello **Output** finestra.

3. Quando la topologia hello è stata inviata correttamente, hello **Storm topologie** per cluster hello devono essere visualizzati. Seleziona hello **WordCount** topologia da hello elenco tooview informazioni hello in esecuzione sulla topologia.

   > [!NOTE]
   > È inoltre possibile visualizzare le **topologie Storm**  da **Esplora Server**. Espandere **Azure** > **HDInsight**, fare clic con il pulsante destro del mouse sul cluster Storm in HDInsight e quindi selezionare **Visualizza topologie Storm**.

    tooview informazioni sui componenti di hello nella topologia hello, fare doppio clic sul componente hello nel diagramma hello.

4. Da hello **topologia riepilogo** consente di visualizzare, fare clic su **Kill** topologia hello toostop.

   > [!NOTE]
   > Topologie di Storm continuare toorun fino a quando non sono disattivate o hello cluster verrà eliminato.

## <a name="transactional-topology"></a>Topologia transazionale

topologia di Hello precedente è non transazionale. i componenti di Hello nella topologia hello non implementano messaggi tooreplaying funzionalità. Per un esempio di una topologia transazionale, creare un progetto e selezionare **esempio Storm** come tipo di progetto hello.

Topologie transazionale implementano hello toosupport riproduzione di dati seguenti:

* **La memorizzazione nella cache di metadati**: beccuccio hello deve archiviare i metadati relativi a dati hello generati, in modo che i dati di hello possono essere recuperati e generati nuovamente se si verifica un errore. Poiché i dati di hello generati dall'esempio hello sono ridotta, dati non elaborati hello ogni tupla viene archiviati in un dizionario per la riproduzione.

* **ACK**: ogni fulmine nella topologia hello può chiamare `this.ctx.Ack(tuple)` tooacknowledge che è stato elaborato correttamente una tupla. Quando tutti i bulloni tupla hello riconosciuto, hello `Ack` di beccuccio hello viene richiamato. Hello `Ack` metodo consente hello beccuccio tooremove i dati è stato memorizzato nella cache per la riproduzione.

* **Esito negativo**: ogni fulmine può chiamare `this.ctx.Fail(tuple)` tooindicate che l'elaborazione non è riuscita per una tupla. Errore Hello propaga toohello `Fail` metodo beccuccio hello, in cui la tupla hello possa essere riprodotta utilizzando metadati memorizzati nella cache.

* **ID sequenza**: quando si genera una tupla, è possibile specificare un ID sequenza univoco. Questo valore identifica hello tupla per l'elaborazione di riproduzione (Ack e hanno esito negativo). Ad esempio, hello beccuccio in hello **esempio Storm** seguente hello utilizzato in project per la creazione dei dati:

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    Questo codice genera una tupla che contiene un flusso predefinito toohello frase, con valore di ID sequenza hello contenuti in **lastSeqId**. Ai fini di questo esempio, **lastSeqId** viene incrementato per ogni tupla generata.

Come dimostrato nel hello **esempio Storm** del progetto, la transazione o meno un componente può essere impostata in fase di esecuzione, in base alla configurazione.

## <a name="hybrid-topology-with-c-and-java"></a>Topologia ibrida con C# e Java

È inoltre possibile utilizzare strumenti di Data Lake per Visual Studio toocreate ibrida le topologie, in cui alcuni componenti sono in c# e gli altri sono Java.

Per un esempio di topologia ibrida, creare un progetto e selezionare **Storm Hybrid Sample**. Il tipo di questo esempio viene illustrato hello seguenti concetti:

* **Java spout** e **C# bolt**: definiti in **HybridTopology_javaSpout_csharpBolt**.

    * Una versione transazionale è definita in **HybridTopologyTx_javaSpout_csharpBolt**.

* **C# spout** e **Java bolt**: definiti in **HybridTopology_csharpSpout_javaBolt**.

    * Una versione transazionale è definita in **HybridTopologyTx_csharpSpout_javaBolt**.

  > [!NOTE]
  > Questa versione viene inoltre illustrato come il codice da un file di testo come componente Java toouse Clojure.


topologia di hello tooswitch utilizzata quando il progetto hello viene inviato, è sufficiente spostare hello `[Active(true)]` istruzione toohello topologia toouse, prima di inviarla toohello cluster.

> [!NOTE]
> Tutti i file Java hello necessari vengono forniti come parte di questo progetto in hello **JavaDependency** cartella.

Quando si desidera creare e inviare una topologia ibrida considerare hello segue:

* È necessario utilizzare **JavaComponentConstructor** toocreate un'istanza della classe Java per un beccuccio o fulmine hello.

* È consigliabile utilizzare **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooJSON di oggetti dati tooserialize interno o all'esterno di componenti Java da Java.

* Quando si inviano server toohello di hello topologia, è necessario utilizzare hello **configurazioni aggiuntive** hello toospecify opzione **i percorsi di File Java**. percorso Hello specificato deve essere una directory hello che contiene i file JAR hello che contengono le classi di Java.

### <a name="azure-event-hubs"></a>Hub eventi di Azure

Versione SCP.NET 0.9.4.203 introduce una nuova classe e metodo in modo specifico per l'utilizzo con beccuccio Hub eventi hello (Java beccuccio che legge da hub eventi). Quando si crea una topologia che utilizza un beccuccio Hub eventi, utilizzare hello dei seguenti metodi:

* **EventHubSpoutConfig** classe: crea un oggetto che contiene la configurazione hello componente beccuccio hello.

* **TopologyBuilder.SetEventHubSpout** metodo: aggiunge la topologia toohello hello Hub eventi beccuccio componente.

> [!NOTE]
> È necessario usare hello **CustomizedInteropJSONSerializer** tooserialize dati prodotti da beccuccio hello.

## <a id="configurationmanager"></a>Usare ConfigurationManager

Non utilizzare **ConfigurationManager** tooretrieve configurazione valori bullone e spout componenti. Questa operazione può generare un'eccezione del puntatore null. Configurazione di hello per il progetto viene invece passata nella topologia Storm hello come una coppia chiave / valore nel contesto di topologia hello. Ogni componente che si basa su valori di configurazione necessario recuperarli dal contesto hello durante l'inizializzazione.

Hello codice seguente viene illustrato come tooretrieve questi valori:

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

Se si utilizza un `Get` tooreturn metodo un'istanza del componente, è necessario assicurarsi che entrambi hello passa `Context` e `Dictionary<string, Object>` costruttore toohello parametri. esempio Hello è un basic `Get` metodo correttamente passa questi valori:

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a>Come tooupdate SCP.NET

Le versioni recenti di SCP.NET supportano l'aggiornamento del pacchetto tramite NuGet. Quando è disponibile un nuovo aggiornamento, si riceve una notifica. controllo toomanually per un aggiornamento, eseguire la procedura seguente:

1. In **Esplora**, fare clic sul progetto hello e selezionare **Gestisci pacchetti NuGet**.

2. Gestione di pacchetti hello, selezionare **aggiornamenti**. Se un aggiornamento è disponibile, è presente nell'elenco. Fare clic su **aggiornamento** per tooinstall pacchetto hello è.

> [!IMPORTANT]
> Se il progetto è stato creato con una versione precedente di SCP.NET che non utilizza NuGet, è necessario eseguire hello versione più recente tooa tooupdate di passaggi seguente:
>
> 1. In **Esplora**, fare clic sul progetto hello e selezionare **Gestisci pacchetti NuGet**.
> 2. Utilizzo di hello **ricerca** campo, cercare e quindi aggiungere, **Microsoft.SCP.Net.SDK** toohello progetto.

## <a name="troubleshoot-common-issues-with-topologies"></a>Risoluzione di problemi comuni con le topologie

### <a name="null-pointer-exceptions"></a>Eccezioni del puntatore null

Quando si utilizza una topologia c# con un cluster HDInsight basati su Linux, bullone e componenti che utilizzano spout **ConfigurationManager** tooread le impostazioni di configurazione in fase di esecuzione possono restituire le eccezioni di puntatore null.

configurazione di Hello per il progetto viene passato come una coppia chiave / valore nel contesto di topologia hello topologia Storm hello. Può essere recuperato dall'oggetto dizionario hello passato tooyour componenti quando vengono inizializzati.

Per ulteriori informazioni, vedere hello [ConfigurationManager](#configurationmanager) sezione di questo documento.

### <a name="systemtypeloadexception"></a>System.TypeLoadException

Quando si utilizza una topologia c# con un cluster HDInsight basati su Linux, è possibile riscontrare hello errore seguente:

    System.TypeLoadException: Failure has occurred while loading a type.

Questo errore si verifica quando si utilizza un file binario che non è compatibile con la versione di hello di .NET che supporta Mono.

Per i cluster HDInsight basati su Linux, è necessario verificare che il progetto usi file binari compilati per .NET 4.5.

### <a name="test-a-topology-locally"></a>Testare la topologia in locale

Sebbene sia facile toodeploy un cluster di tooa topologia, in alcuni casi, potrebbe essere necessario tootest una topologia in locale. Utilizzare i seguenti passaggi toorun hello e testare la topologia di esempio hello in questa esercitazione in locale nell'ambiente di sviluppo.

> [!WARNING]
> I test locali funzionano solo per topologie di base di tipo C#. Non è possibile usare il test locale per topologie ibride o topologie che impiegano più flussi.

1. In **Esplora**, fare clic sul progetto hello e selezionare **proprietà**. Nelle proprietà del progetto hello, modificare hello **tipo di Output** troppo**applicazione Console**.

    ![Screenshot delle proprietà di progetto, con il tipo di Output evidenziato](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > Ricordare hello toochange **tipo di Output** troppo indietro**libreria di classi** prima di distribuire cluster tooa di hello topologia.

2. In **Esplora**, fare clic sul progetto hello e quindi selezionare **Aggiungi** > **nuovo elemento**. Selezionare **classe**, quindi immettere **LocalTest.cs** come nome della classe hello. Infine fare clic su **Aggiungi**.

3. Aprire **LocalTest.cs**e aggiungere il seguente hello **utilizzando** istruzione nella parte superiore di hello:

    ```csharp
    using Microsoft.SCP;
    ```

4. Esempio di codice seguente di hello utilizzare come contenuto di hello di hello **LocalTest** classe:

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    Richiedere un tooread momento tramite i commenti di codice hello. Questo codice Usa **LocalContext** componenti hello toorun nell'ambiente di sviluppo hello e mantiene il flusso di dati hello tra file tootext componenti sul disco locale hello.

1. Aprire **Program.cs**e aggiungere hello seguente toohello **Main** metodo:

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. Salvare le modifiche di hello e quindi fare clic su **F5** o seleziona **Debug** > **Avvia debug** progetto hello toostart. Una finestra della console dovrà essere visualizzato e stato del log come stato di avanzamento test hello. Quando **test completato** viene visualizzato, premere qualsiasi finestra hello tooclose chiave.

3. Utilizzare **Esplora** directory hello toolocate contenente il progetto. Ad esempio **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**. In questa directory, aprire **Bin** e quindi fare clic su **Debug**. Dovrebbe essere file di testo hello generati durante l'esecuzione di test hello: sentences.txt counter.txt e splitter.txt. Aprire ogni file di testo e verificare dati hello.

   > [!NOTE]
   > In questi file i dati stringa vengono resi permanenti come matrice di valori decimali. Ad esempio, \[[97,103,111]] in hello **splitter.txt** file è una parola hello *e*.

> [!NOTE]
> Essere certi hello tooset **tipo di progetto** troppo indietro**libreria di classi** prima di distribuire tooa Storm nel cluster HDInsight.

### <a name="log-information"></a>Informazioni di log

È possibile registrare facilmente le informazioni provenienti dai componenti della topologia usando `Context.Logger`. Ad esempio, l'esempio hello crea una voce di log informativo:

```csharp
Context.Logger.Info("Component started");
```

Le informazioni registrate possono essere visualizzate dal hello **registro del servizio Hadoop**, che si trovano in **Esplora Server**. Espandere la voce hello per le Storm nel cluster HDInsight e quindi **registro del servizio Hadoop**. Infine, selezionare tooview file di log hello.

> [!NOTE]
> Hello log vengono archiviati in account di archiviazione di Azure che viene utilizzato il cluster hello. log di hello tooview in Visual Studio, è necessario accedere toohello sottoscrizione Azure a cui appartiene l'account di archiviazione hello.

### <a name="view-error-information"></a>Visualizzare le informazioni sugli errori

tooview errori che si sono verificati in una topologia in esecuzione, utilizzare hello alla procedura seguente:

1. Da **Esplora Server**, hello Storm nel cluster HDInsight e scegliere **topologie Storm vista**.

2. Per hello **Spout** e **bulloni**, hello **ultimo errore** colonna contiene informazioni sull'ultimo errore hello.

3. Seleziona hello **Spout Id** o **Id fulmine** per il componente hello che contiene un errore elencato. Nella pagina dettagli hello di errore visualizzato e altre informazioni sono elencate nella hello **errori** sezione hello parte inferiore della pagina hello.

4. tooobtain ulteriori informazioni, selezionare un **porta** da hello **executor** sezione della pagina hello, toosee hello Storm lavoro registro hello ultimi minuti.

### <a name="errors-submitting-topologies"></a>Errori durante l'invio delle topologie

Se si verificano errori di invio di una topologia tooHDInsight, è possibile trovare log dei componenti lato server hello che gestiscono l'invio di topologia il cluster HDInsight. tooretrieve questi log, utilizzare hello comando seguente dalla riga di comando:

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

Sostituire __sshuser__ con account utente SSH per il cluster hello hello. Sostituire __clustername__ con nome hello del cluster HDInsight hello. Per altre informazioni sull'uso di `scp` e `ssh` con HDInsight, vedere l'articolo [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Gli invii possono non riuscire per diversi motivi:

* JDK non è installato o non è presente nel percorso di hello.
* Dipendenze di Java richieste non sono inclusi in inoltro hello.
* Dipendenze incompatibili.
* Nomi di topologia duplicati.

Se hello `hdinsight-scpwebapi.out` registro contiene un `FileNotFoundException`, ciò potrebbe dipendere da hello seguenti condizioni:

* Hello JDK non è presente nel percorso di hello nell'ambiente di sviluppo hello. Verificare che hello JDK è installato nell'ambiente di sviluppo hello e che `%JAVA_HOME%/bin` si trova nel percorso di hello.
* Manca una dipendenza Java. Verificare che si sono inclusi tutti i file JAR richiesto come parte dell'invio hello.

## <a name="next-steps"></a>Passaggi successivi

Per un esempio di elaborazione dei dati dall'hub eventi, vedere [Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).

Per un esempio di una topologia di C# che divide il flusso di dati in più flussi, vedere [csharp-storm-example](https://github.com/Blackmist/csharp-storm-example).

vedere altre informazioni sulla creazione di c# con le topologie, toodiscover [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).

Per altre modalità toowork con HDInsight e altre Storm su campioni di HDInsight, vedere hello seguenti documenti:

**Microsoft SCP.NET**

* [Guida alla programmazione SCP](hdinsight-storm-scp-programming-guide.md)

**Apache Storm in HDInsight**

* [Distribuzione e monitoraggio di topologie con Apache Storm in HDInsight](hdinsight-storm-deploy-monitor-topology.md)
* [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md)

**Apache Hadoop in HDInsight**

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)
* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)
* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)

**Apache HBase in HDInsight**

* [Introduzione a HBase in HDInsight](hdinsight-hbase-tutorial-get-started.md)
