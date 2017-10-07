---
title: servizi di Service Fabric aaaPartitioning | Documenti Microsoft
description: Viene descritto come servizi con stati di toopartition Service Fabric. Partizioni consente l'archiviazione dei dati sul computer locale hello in modo da dati e calcolo possono essere ridimensionate, insieme.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a>Partizionare Reliable Services di Service Fabric
Questo articolo fornisce un'introduzione toohello concetti di base di servizi di Azure Service Fabric affidabili di partizionamento. Hello codice sorgente utilizzato nell'articolo hello disponibile anche su [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="partitioning"></a>Partizionamento
Il partizionamento non è univoco tooService dell'infrastruttura. bensì si tratta di un modello di base per la creazione di servizi scalabili. In senso più ampio, è possibile considerare di partizionamento come concetto della divisione di stato (dati) e di calcolo di prestazioni e scalabilità di tooimprove accessibile unità più piccole. Una forma molto conosciuta di partizionamento è il [partizionamento dei dati][wikipartition], noto anche come partizionamento orizzontale.

### <a name="partition-service-fabric-stateless-services"></a>Partizionamento dei servizi senza stato di Service Fabric
Per i servizi senza stato un partizionamento può essere considerato un'unità logica contenente una o più istanze di un servizio. La figura 1 illustra un servizio senza stato con cinque istanze distribuite in un cluster usando una partizione.

![Servizio senza stato](./media/service-fabric-concepts-partitioning/statelessinstances.png)

Sono disponibili due tipi di soluzioni di servizio senza stato. Hello prima uno è un servizio che rende persistente lo stato esternamente, ad esempio in un database SQL di Azure (ad esempio, un sito Web che archivia i dati e le informazioni sulla sessione hello). Hello secondo è solo calcolo servizi (come anteprima una calcolatrice o immagine) che non si gestiscono qualsiasi stato persistente.

In entrambi i casi, il partizionamento di un servizio senza stato è uno scenario molto raro e la scalabilità e la disponibilità in genere si ottengono aggiungendo altre istanze. Hello solo tempo tooconsider più partizioni per le istanze del servizio senza stato è quando è necessario toomeet speciali routing delle richieste.

ad esempio, quando gli utenti con ID compresi in un determinato intervallo devono essere gestiti solo da una particolare istanza del servizio. Un altro esempio di quando è possibile partizionare un servizio senza stato è quando si dispone di un back-end realmente partizionato (ad esempio un database SQL partizionato) e si desidera toocontrol quale istanza del servizio deve scrivere toohello partizioni di database, o eseguire altre operazioni di preparazione all'interno di Hello servizio senza stato che richiede hello stesso le informazioni di partizionamento come viene utilizzato nel back-end hello. Tali tipi di scenario possono essere risolti anche in modo diverso e non richiedono necessariamente il partizionamento del servizio.

resto Hello di questa procedura dettagliata si concentra sui servizi con stato.

### <a name="partition-service-fabric-stateful-services"></a>Partizionamento dei servizi con stato di Service Fabric
Service Fabric rende servizi con stato scalabili toodevelop facile offrendo un modo di prima classe toopartition stato (dati). Concettualmente, si pensi a una partizione di un servizio con stato come unità di scala che è altamente affidabile tramite [repliche](service-fabric-availability-services.md) che vengono distribuiti e bilanciati tra i nodi di hello in un cluster.

Il partizionamento nel contesto di hello di servizi di Service Fabric con stati, si riferisce toohello processo di individuazione che una partizione specifica del servizio è responsabile di una parte di hello stato completo nello stato del servizio hello. Come accennato in precedenza, la partizione è un set di [repliche](service-fabric-availability-services.md). Un aspetto interessante di Service Fabric è che le partizioni hello viene inserito in nodi diversi. In questo modo il limite di risorse del nodo di toogrow tooa. Quando sono necessari dati hello aumento delle dimensioni, partizioni di aumento delle dimensioni e Service Fabric eseguito il ribilanciamento delle partizioni tra i nodi. In questo modo hello continua utilizzo efficiente delle risorse hardware.

toogive ad esempio, affermare che iniziano con un cluster di 5 nodi e un servizio che viene configurato toohave 10 partizioni e una destinazione di tre repliche. In questo caso, Service Fabric potrebbe bilanciare repliche hello cluster hello - e distribuire alla fine si avrebbero primario due [repliche](service-fabric-availability-services.md) per ogni nodo.
Se è necessario ora tooscale out too10 i nodi del cluster di hello, Service Fabric sarebbe ribilanciare primario hello [repliche](service-fabric-availability-services.md) in tutti i nodi di 10. Analogamente, se è ridimensionata nodi too5 indietro, Service Fabric sarebbe ribilanciare tutte le repliche di hello nei nodi hello 5.  

Figura 2 mostra hello distribuzione 10 partizioni prima e dopo il ridimensionamento cluster hello.

![Servizio con stato](./media/service-fabric-concepts-partitioning/partitions.png)

Di conseguenza, hello scalabilità orizzontale è possibile ottenere poiché le richieste dai client vengono distribuite tra più computer, un miglioramento delle prestazioni complessive dell'applicazione hello e viene ridotto il conflitto su toochunks accesso dei dati.

## <a name="plan-for-partitioning"></a>Pianificazione del partizionamento
Prima di implementare un servizio, è necessario considerare sempre hello strategia che è necessario tooscale out di partizionamento. Esistono diversi modi, ma tutti gli elementi concentrarsi su quale applicazione hello deve tooachieve. Per il contesto di hello di questo articolo, si prendano in considerazione alcune hello aspetti più importanti.

Un buon approccio è toothink sulla struttura hello dello stato di hello necessarie toobe partizionata, come primo passaggio hello.

Un semplice esempio viene riportato di seguito. Se fosse un servizio per un sondaggio countywide toobuild, è possibile creare una partizione per ogni città regione hello. Quindi, si potrebbe archiviare hello voti per ogni persona città hello nella partizione hello corrispondente toothat città. Figura 3 viene illustrato un set di utenti e hello città in cui risiedono.

![Partizione semplice](./media/service-fabric-concepts-partitioning/cities.png)

Come il popolamento di città hello varia notevolmente, si rischia di con alcune partizioni che contengono una grande quantità di dati (ad esempio, Seattle) e le altre partizioni con stato molto piccolo (ad esempio Kirkland). Cos'è impatto hello della presenza di partizioni con una quantità non uniforme di stato?

Se si pensa esempio hello nuovamente, è possibile visualizzare facilmente che partizione hello contenente hello voti per Seattle consentirà di ottenere più traffico Kirkland hello uno. Per impostazione predefinita, Service Fabric garantisce che sia presente su hello stesso numero di repliche primarie e secondarie in ogni nodo. perciò si potrebbero avere nodi contenenti repliche che gestiscono più traffico e altre che gestiscono meno traffico. Preferibilmente si tooavoid a caldo e freddi aree come segue in un cluster.

In ordine tooavoid questo, è necessario eseguire due operazioni, da un punto di vista di partizionamento:

* Provare a stato hello toopartition in modo che viene distribuito uniformemente tra tutte le partizioni.
* Caricamento di report da ognuna delle repliche hello per servizio hello. Per informazioni su come fare, vedere l'articolo relativo a [metriche e carico](service-fabric-cluster-resource-manager-metrics.md). Service Fabric fornisce hello. funzionalità il carico di tooreport utilizzato da servizi, ad esempio quantità di memoria o un numero di record. In base alle metriche di hello segnalate, Service Fabric rileva che alcune partizioni servono carichi più elevati rispetto ad altri ed eseguito il ribilanciamento cluster hello mobile repliche toomore adatto nodi, in modo che complessivo non è sottoposto a overload alcun nodo.

A volte non è possibile sapere quanti dati saranno presenti in una determinata partizione Pertanto una raccomandazione generale è toodo entrambi - prima di tutto, adottando una strategia di partizionamento che distribuisce hello dati in modo uniforme tra partizioni hello e i secondi, dal carico di report.  primo metodo Hello impedisce situazioni descritte hello voto di esempio, anche se hello secondo consente di arrotondare i temporanee differenze in access o di carico nel tempo.

Un altro aspetto della pianificazione di partizione è numero corretto di hello toochoose di toobegin partizioni con.
Dal punto di vista di Service Fabric, nulla impedisce di iniziare con un numero di partizioni maggiore di quello anticipato per lo scenario.
In realtà, presupponendo che il numero massimo di hello di partizioni è un approccio valido.

Raramente saranno necessarie più partizioni di quelle scelte inizialmente. Come è possibile modificare il numero di partizioni hello dopo hello, sarebbe necessario tooapply alcuni approcci partizione avanzate, ad esempio la creazione di una nuova istanza del servizio di hello stesso tipo di servizio. È inoltre necessario tooimplement logica sul lato client che indirizza hello richiede l'istanza del servizio corretto toohello, in base alle informazioni sul lato client che il codice client deve gestire.

Un'altra considerazione per il partizionamento di pianificazione è risorse del computer disponibile hello. Quando lo stato di hello esigenze toobe accessibili e archiviati, si sta toofollow associato:

* Larghezza di banda della rete
* Memoria di sistema
* Archiviazione su disco

Ma cosa accade se si verificano i vincoli di risorse in un cluster in esecuzione? risposte Hello sono che è semplicemente possibile scalare orizzontalmente hello cluster tooaccommodate hello nuovi requisiti.

[Guida alla pianificazione della capacità di Hello](service-fabric-capacity-planning.md) offre indicazioni per il toodetermine il numero di nodi del cluster è necessario.

## <a name="get-started-with-partitioning"></a>Introduzione al partizionamento
In questa sezione viene descritto come tooget iniziare con il partizionamento del servizio.

In primo luogo Service Fabric consente di scegliere tra tre schemi di partizione:

* Partizionamento con intervallo (noto anche come UniformInt64Partition).
* Partizionamento denominato. Le applicazioni che usano questo modello in genere hanno dati che possono essere inseriti in un bucket, in un set associato. Aree, codici postali, gruppi di clienti o altri limiti aziendali sono alcuni esempi comuni di campi dati usati come chiavi di partizione denominata.
* Partizionamento singleton. Partizioni singleton vengono utilizzate in genere quando il servizio di hello non richiede alcun aggiuntive di routing. I servizi senza stato, ad esempio, usano questo schema di partizionamento per impostazione predefinita.

Gli schemi di partizionamento denominato e singleton sono forme particolari di partizioni con intervalli. Per impostazione predefinita, i modelli di Visual Studio hello per l'utilizzo di Service Fabric intervallo incluso il partizionamento, perché è hello uno più comune e utile. resto Hello di questo articolo illustra lo schema di partizionamento nell'intervallo di hello.

### <a name="ranged-partitioning-scheme"></a>Schema di partizionamento con intervallo
Si tratta di toospecify usato un numero intero intervalli (identificate da una chiave inferiore e chiave superiore) e un numero di partizioni (n). Crea partizioni n, ognuno responsabile di un intervallo secondario non sovrapposti di hello complessiva intervalli di chiavi di partizione. Ad esempio, uno schema di partizionamento con intervallo con una chiave minima 0, una chiave massima 99 e un conteggio pari a 4 creerà quattro partizioni come mostrato di seguito.

![Partizionamento per intervalli](./media/service-fabric-concepts-partitioning/range-partitioning.png)

Un approccio comune è un hash basato su una chiave univoca nel set di dati hello toocreate. Sono esempi comuni di chiavi un Vehicle Identification Number (VIN), l'ID di un dipendente o una stringa univoca. Usando questa chiave univoca, si potrebbe quindi generare un codice hash, l'intervallo di chiavi di modulo hello, toouse come chiave. È possibile specificare hello superiore e inferiore di hello chiave intervallo consentito.

### <a name="select-a-hash-algorithm"></a>Selezionare un algoritmo di hash
Una parte importante della generazione di un hash è rappresentata dalla selezione dell'algoritmo di hash. Una considerazione importante è se obiettivo hello toogroup chiavi simili vicini (sensibili hashing località), o se l'attività deve essere distribuito su vasta scala tra tutte le partizioni (distribuzione hash), che sono più comuni.

sono riportate le caratteristiche di Hello di un algoritmo di hash di distribuzione valido che è facile toocompute dispone di alcuni conflitti e distribuisce chiavi di hello in modo uniforme. Un buon esempio di un algoritmo hash efficiente è hello [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) algoritmo hash.

Un'ottima risorsa per le scelte di algoritmo di hash generale codice è hello [pagina di Wikipedia sulle funzioni hash](http://en.wikipedia.org/wiki/Hash_function).

## <a name="build-a-stateful-service-with-multiple-partitions"></a>Compilare un servizio con stato con più partizioni
Ora verrà creato il primo servizio con stato affidabile con più partizioni. In questo esempio, si creerà un'applicazione molto semplice in cui si desidera toostore tutti i cognomi che iniziano con hello stessa lettera di hello stessa partizione.

Prima di scrivere alcun codice, è necessario toothink sulle partizioni hello e le chiavi di partizione. È necessario 26 partizioni (uno per ogni lettera nell'alfabeto hello), ma su hello superiore e inferiore delle chiavi?
Come si desidera letteralmente toohave una partizione per ogni lettera, è possibile usare 0 come chiave bassa hello e 25 come chiave alta hello, ogni lettera è la propria chiave.

> [!NOTE]
> Si tratta di uno scenario semplificato, come in realtà distribuzione hello sarebbe non uniforme. Cognome inizia con la lettera di hello "S" o "M" sono più comuni di quelli hello a partire da "X" o "Y".
> 
> 

1. Aprire **Visual Studio** > **File** > **Nuovo** > **Progetto**.
2. In hello **nuovo progetto** finestra di dialogo, scegliere un'applicazione hello Service Fabric.
3. Denominare il progetto di hello "AlphabetPartitions".
4. In hello **creare un servizio** finestra di dialogo scegliere **Stateful** del servizio e chiamarlo "Alphabet.Processing", come illustrato nell'immagine di hello riportata di seguito.
       ![Finestra di dialogo Nuovo servizio in Visual Studio][1]

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. Impostare il numero di hello di partizioni. File ApplicationManifest XML hello aprire si trova in hello cartella ApplicationPackageRoot parametro hello AlphabetPartitions progetto e aggiornare hello Processing_PartitionCount too26 come illustrato di seguito.
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    È inoltre necessario hello tooupdate LowKey e le proprietà di HighKey elemento StatefulService hello in hello ApplicationManifest.xml come illustrato di seguito.
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. Per toobe servizio hello accessibile, aprire un endpoint su una porta aggiungendo l'elemento dell'endpoint hello di ServiceManifest.xml (che si trova nella cartella PackageRoot hello) per hello Alphabet.Processing servizio come illustrato di seguito:
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    Servizio hello è ora configurato toolisten tooan interno di endpoint con 26 partizioni.
7. Successivamente, è necessario toooverride hello `CreateServiceReplicaListeners()` metodo della classe di elaborazione hello.
   
   > [!NOTE]
   > Per questo esempio, si presume che venga usato un semplice oggetto HttpCommunicationListener. Per ulteriori informazioni sulla comunicazione affidabile di servizio, vedere [modello di comunicazione affidabile servizio hello](service-fabric-reliable-services-communication.md).
   > 
   > 
8. Un modello consigliato per l'URL di hello che una replica è in ascolto su è hello seguente formato: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.
    Pertanto si desidera tooconfigure il listener di comunicazione toolisten sugli endpoint corretto hello e con questo modello.
   
    Più repliche di questo servizio possono essere ospitate su hello stesso computer, quindi questo indirizzo deve toobe toohello univoco replica. Ecco perché l'ID di partizione + ID replica si trovano hello URL. HttpListener può restare in ascolto su più indirizzi in hello che stessa porta come prefisso di URL hello è univoco.
   
    Hello che GUID aggiuntiva è disponibile per un case avanzato in cui le repliche secondarie sono anche in attesa per le richieste di sola lettura. Quando è il caso di hello, è opportuno che un nuovo indirizzo univoco viene utilizzato durante la transizione da indirizzo di toosecondary primaria tooforce client toore risoluzione hello toomake. '+' viene utilizzato come indirizzo hello in modo che hello replica è in ascolto in tutto il codice hello (IP, FQDM, localhost e così via), gli host disponibili riportato di seguito viene illustrato un esempio.
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    È inoltre importante notare che hello pubblicati URL è leggermente diversa dal prefisso URL ascolto hello.
    URL di ascolto Hello viene tooHttpListener. Hello che URL pubblicato è hello URL pubblicato toohello servizio Naming Service Fabric, che viene utilizzato per l'individuazione del servizio. I client richiederanno questo indirizzo con questo servizio di individuazione. indirizzo Hello che i client recuperano esigenze toohave hello effettivo IP o nome di dominio completo del nodo hello in ordine tooconnect. Pertanto è necessario tooreplace '+' con hello del nodo IP o FQDN come illustrato sopra.
9. ultimo passaggio Hello è hello tooadd logica toohello servizio come illustrato di seguito di elaborazione.
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    `ProcessInternalRequest`i valori hello query stringa parametro utilizzato toocall hello partizione e chiamate di hello letture `AddUserAsync` dizionario affidabile toohello tooadd hello lastname `dictionary`.
10. Aggiungere un toosee di progetto di servizio senza stato toohello come chiamare una determinata partizione.
    
    Questo servizio funge da una semplice interfaccia web che accetta lastname hello come parametro di stringa di query, determina la chiave di partizione hello e invia toohello Alphabet.Processing servizio per l'elaborazione.
11. In hello **creare un servizio** finestra di dialogo scegliere **Stateless** del servizio e chiamarlo "Alphabet.Web", come illustrato di seguito.
    
    ![Schermata di servizio senza stato](./media/service-fabric-concepts-partitioning/createnewstateless.png).
12. Aggiornare le informazioni di endpoint hello in ServiceManifest.xml hello di hello Alphabet.WebApi servizio tooopen di una porta, come illustrato di seguito.
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. È necessario un insieme di ServiceInstanceListeners classe hello Web tooreturn. È possibile scegliere nuovamente tooimplement HttpCommunicationListener un semplice.
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. È ora necessario logica di elaborazione tooimplement hello. Hello chiamate HttpCommunicationListener `ProcessInputRequest` quando arriva una richiesta. Pertanto proseguire e aggiungere codice hello riportato di seguito.
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    Analisi dettagliata: codice Hello legge prima lettera di hello del parametro di stringa di query hello `lastname` in char. Quindi, determina la chiave di partizione hello per questa lettera sottraendo hello valore esadecimale `A` dal valore esadecimale hello prima lettera degli hello cognomi.
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    Si ricordi che in questo esempio si usano 26 partizioni con una chiave per ogni partizione.
    Successivamente, si ottiene partizione del servizio hello `partition` per questa chiave utilizzando hello `ResolveAsync` metodo hello `servicePartitionResolver` oggetto. `servicePartitionResolver` viene definito come mostrato di seguito.
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    Hello `ResolveAsync` metodo accetta hello URI del servizio, la chiave di partizione hello e un token di annullamento come parametri. Hello URI del servizio per il servizio di elaborazione hello è `fabric:/AlphabetPartitions/Processing`. Quindi, ci occuperemo endpoint hello della partizione hello.
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    Infine, è compilare l'URL dell'endpoint hello più querystring hello e chiamare hello servizio di elaborazione.
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    Al termine dell'elaborazione di hello, output di hello è write-back.
15. ultimo passaggio Hello è servizio di hello tootest. Visual Studio usa i parametri dell'applicazione per la distribuzione locale e cloud. servizio di hello tootest con 26 partizioni in locale, è necessario hello tooupdate `Local.xml` file nella cartella ApplicationParameters hello del progetto AlphabetPartitions hello, come illustrato di seguito:
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. Una volta terminata la distribuzione, è possibile controllare il servizio di hello e tutte le relative partizioni in hello Service Fabric Explorer.
    
    ![Schermata di Service Fabric Explorer](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. In un browser, è possibile testare la logica di partizionamento immettendo hello `http://localhost:8081/?lastname=somename`. Si noterà che ciascun cognome che inizia con hello stessa lettera di vengono archiviato in hello stessa partizione.
    
    ![Schermata del browser](./media/service-fabric-concepts-partitioning/samplerunning.png)

è disponibili sul Hello intero codice sorgente dell'esempio hello [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sui concetti di Service Fabric, vedere l'esempio hello:

* [Disponibilità dei servizi di Service Fabric](service-fabric-availability-services.md)
* [Scalabilità dei servizi di Service Fabric](service-fabric-concepts-scalability.md)
* [Pianificazione della capacità per le applicazioni Service Fabric](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png