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
# <a name="scp-programming-guide"></a><span data-ttu-id="b387a-103">Guida alla programmazione SCP</span><span class="sxs-lookup"><span data-stu-id="b387a-103">SCP programming guide</span></span>
<span data-ttu-id="b387a-104">SCP è una piattaforma toobuild in tempo reale, l'applicazione di elaborazione di dati affidabili, coerenti e a elevate prestazioni.</span><span class="sxs-lookup"><span data-stu-id="b387a-104">SCP is a platform toobuild real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="b387a-105">È compilato in cima [Apache Storm](http://storm.incubator.apache.org/) - un flusso di sistema progettato per community hello OSS di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b387a-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by hello OSS communities.</span></span> <span data-ttu-id="b387a-106">Storm è stato progettato da Nathan Marz e reso open source da Twitter.</span><span class="sxs-lookup"><span data-stu-id="b387a-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="b387a-107">Si avvale [ZooKeeper Apache](http://zookeeper.apache.org/), Apache un altro progetto di coordinamento distribuito in tooenable altamente affidabile e la gestione dello stato.</span><span class="sxs-lookup"><span data-stu-id="b387a-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project tooenable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="b387a-108">Non solo progetto hello SCP trasferita Storm in Windows, ma anche l'aggiunta di progetto hello estensioni e personalizzazione per l'ecosistema di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-108">Not only hello SCP project ported Storm on Windows but also hello project added extensions and customization for hello Windows ecosystem.</span></span> <span data-ttu-id="b387a-109">le estensioni di Hello includono esperienza dello sviluppatore .NET e librerie, hello personalizzazione comprende la distribuzione basata su Windows.</span><span class="sxs-lookup"><span data-stu-id="b387a-109">hello extensions include .NET developer experience, and libraries, hello customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="b387a-110">personalizzazione ed estensione hello viene eseguita in modo che i progetti OSS hello toofork non è necessaria, è possibile sfruttare tutte derivati ecosistemi basati su Storm.</span><span class="sxs-lookup"><span data-stu-id="b387a-110">hello extension and customization is done in such a way that we do not need toofork hello OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="b387a-111">Modello di elaborazione</span><span class="sxs-lookup"><span data-stu-id="b387a-111">Processing model</span></span>
<span data-ttu-id="b387a-112">dati Hello in SCP viene modellati come flussi continui di tuple.</span><span class="sxs-lookup"><span data-stu-id="b387a-112">hello data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="b387a-113">In genere hello tuple confluire alcuni coda prima di tutto, quindi prelevato e trasformati dalla logica di business ospitata all'interno di una topologia di Storm, infine output di hello possibile reindirizzare i dati come tuple tooanother SCP sistema oppure essere eseguito il commit toostores come file system distribuito o i database, ad esempio SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b387a-113">Typically hello tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally hello output could be piped as tuples tooanother SCP system, or be committed toostores like distributed file system or databases like SQL Server.</span></span>

![Un diagramma di una coda di alimentazione tooprocessing di dati, quale un archivio dati feed](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="b387a-115">In Storm, una topologia applicazione definisce un grafo di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b387a-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="b387a-116">Ogni nodo in una topologia contiene logica di elaborazione e i collegamenti tra i nodi indicano il flusso dei dati.</span><span class="sxs-lookup"><span data-stu-id="b387a-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="b387a-117">Hello nodi tooinject dati di input nella topologia hello vengono chiamati Spouts, che può essere utilizzato toosequence hello dati.</span><span class="sxs-lookup"><span data-stu-id="b387a-117">hello nodes tooinject input data into hello topology are called Spouts, which can be used toosequence hello data.</span></span> <span data-ttu-id="b387a-118">Hello dati di input può risiedere nel file log, database transazionale, contatore delle prestazioni di sistema vengono chiamati nodi hello e così via con entrambi i flussi di dati di input e output dadi, quale hello filtrare i dati effettivi e le selezioni e aggregazione.</span><span class="sxs-lookup"><span data-stu-id="b387a-118">hello input data could reside in file logs, transactional database, system performance counter etc. hello nodes with both input and output data flows are called Bolts, which do hello actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="b387a-119">SCP supporta l'elaborazione dati di tipo best effort, at-least-once ed exactly-once.</span><span class="sxs-lookup"><span data-stu-id="b387a-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="b387a-120">In un'applicazione di elaborazione di streaming distribuita, possono verificarsi diversi errori durante l'elaborazione di dati, ad esempio un'interruzione di rete, un errore del computer o del codice utente e così via. L'elaborazione di at-least-once garantisce verranno elaborati tutti i dati almeno una volta riproducendo automaticamente hello stessi dati in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="b387a-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically hello same data when error happens.</span></span> <span data-ttu-id="b387a-121">L'elaborazione at-least-once è semplice e affidabile e offre risultati positivi in molte applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b387a-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="b387a-122">Tuttavia, quando un'applicazione hello richiede il conteggio esatto, ad esempio, l'elaborazione di at-least-once è insufficiente poiché hello stessi dati potrebbero potenzialmente essere riprodotto nella topologia applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-122">However, when hello application requires exact counting, for example, at-least-once processing is insufficient since hello same data could potentially be played in hello application topology.</span></span> <span data-ttu-id="b387a-123">In tal caso, esattamente-dopo l'elaborazione è progettata risultato hello che toomake sia corretto, anche quando i dati di hello possono essere riprodotti ed elaborati più volte.</span><span class="sxs-lookup"><span data-stu-id="b387a-123">In that case, exactly-once processing is designed toomake sure hello result is correct even when hello data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="b387a-124">SCP consente alle applicazioni di processo di .NET sviluppatori toodevelop in tempo reale dati hello usare Java Virtual Machine (JVM) basata su Storm sotto coperchio hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-124">SCP enables .NET developers toodevelop real time data process applications while leverage hello Java Virtual Machine (JVM) based Storm under hello cover.</span></span> <span data-ttu-id="b387a-125">.NET Hello e JVM comunicano tramite socket locale TCP.</span><span class="sxs-lookup"><span data-stu-id="b387a-125">hello .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="b387a-126">Ogni beccuccio/fulmine è fondamentalmente una coppia di processo .net/Java, in cui viene eseguita la logica di hello utente nel processo .net come un plug-in.</span><span class="sxs-lookup"><span data-stu-id="b387a-126">Basically each Spout/Bolt is a .Net/Java process pair, where hello user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="b387a-127">toobuild un'applicazione nella parte superiore di SCP per l'elaborazione di dati, sono necessari diversi passaggi:</span><span class="sxs-lookup"><span data-stu-id="b387a-127">toobuild a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="b387a-128">Progettare e implementare toopull Spouts hello nei dati dalla coda.</span><span class="sxs-lookup"><span data-stu-id="b387a-128">Design and implement hello Spouts toopull in data from queue.</span></span>
* <span data-ttu-id="b387a-129">Progettare e implementare i dati di input di bulloni tooprocess hello e salvare dati tooexternal archivi, ad esempio Database.</span><span class="sxs-lookup"><span data-stu-id="b387a-129">Design and implement Bolts tooprocess hello input data, and save data tooexternal stores such as Database.</span></span>
* <span data-ttu-id="b387a-130">Progettare la topologia di hello, inviare ed eseguire topologia hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-130">Design hello topology, then submit and run hello topology.</span></span> <span data-ttu-id="b387a-131">Hello topologia definisce vertici e dati hello flussi tra vertici hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-131">hello topology defines vertexes and hello data flows between hello vertexes.</span></span> <span data-ttu-id="b387a-132">SCP verrà richiedere specifica topologia hello e distribuirlo in un cluster Storm in cui ogni vertice viene eseguito in un nodo logico.</span><span class="sxs-lookup"><span data-stu-id="b387a-132">SCP will take hello topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="b387a-133">failover Hello e ridimensionamento verrà essere preso in considerazione di hello Storm utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="b387a-133">hello failover and scaling will be taken care of by hello Storm task scheduler.</span></span>

<span data-ttu-id="b387a-134">Questo documento verrà utilizzato toowalk alcuni semplici esempi come applicazione di elaborazione dei dati toobuild con SCP.</span><span class="sxs-lookup"><span data-stu-id="b387a-134">This document will use some simple examples toowalk through how toobuild data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="b387a-135">Interfaccia del plug-in SCP</span><span class="sxs-lookup"><span data-stu-id="b387a-135">SCP Plugin Interface</span></span>
<span data-ttu-id="b387a-136">SCP i plug-in o le applicazioni sono file exe autonomo che possono entrambi in esecuzione all'interno di Visual Studio durante la fase di sviluppo hello ed essere collegati alla pipeline Storm hello dopo la distribuzione nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="b387a-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during hello development phase, and be plugged into hello Storm pipeline after deployment in production.</span></span> <span data-ttu-id="b387a-137">Scrittura di plug-in hello SCP è appena hello stesso come la scrittura di eventuali altre applicazioni Windows standard console.</span><span class="sxs-lookup"><span data-stu-id="b387a-137">Writing hello SCP plugin is just hello same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="b387a-138">Piattaforma SCP.NET dichiara un tipo di interfaccia per beccuccio/fulmine e codice di plug-in di hello utente deve implementare queste interfacce.</span><span class="sxs-lookup"><span data-stu-id="b387a-138">SCP.NET platform declares some interface for spout/bolt, and hello user plugin code should implement these interfaces.</span></span> <span data-ttu-id="b387a-139">scopo principale di Hello di questa progettazione è che l'utente hello può concentrarsi sulla propria logica di business e lasciando toobe altri elementi gestiti dalla piattaforma SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="b387a-139">hello main purpose of this design is that hello user can focus on their own business logics, and leaving other things toobe handled by SCP.NET platform.</span></span>

<span data-ttu-id="b387a-140">codice di plug-in di Hello utente deve implementare una delle interfacce seguenti hello, a seconda se la topologia hello è transazionale o non transazionale e se il componente hello è beccuccio o fulmine.</span><span class="sxs-lookup"><span data-stu-id="b387a-140">hello user plugin code should implement one of hello followings interfaces, depends on whether hello topology is transactional or non-transactional, and whether hello component is spout or bolt.</span></span>

* <span data-ttu-id="b387a-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="b387a-141">ISCPSpout</span></span>
* <span data-ttu-id="b387a-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="b387a-142">ISCPBolt</span></span>
* <span data-ttu-id="b387a-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="b387a-143">ISCPTxSpout</span></span>
* <span data-ttu-id="b387a-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="b387a-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="b387a-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="b387a-145">ISCPPlugin</span></span>
<span data-ttu-id="b387a-146">ISCPPlugin è l'interfaccia di hello comune per tutti i tipi di plug-in.</span><span class="sxs-lookup"><span data-stu-id="b387a-146">ISCPPlugin is hello common interface for all kinds of plugins.</span></span> <span data-ttu-id="b387a-147">Attualmente è un'interfaccia fittizia.</span><span class="sxs-lookup"><span data-stu-id="b387a-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="b387a-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="b387a-148">ISCPSpout</span></span>
<span data-ttu-id="b387a-149">ISCPSpout è interfaccia hello per beccuccio non transazionale.</span><span class="sxs-lookup"><span data-stu-id="b387a-149">ISCPSpout is hello interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="b387a-150">Quando `NextTuple()` viene chiamato, hello C\# codice utente può creare uno o più tuple.</span><span class="sxs-lookup"><span data-stu-id="b387a-150">When `NextTuple()` is called, hello C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="b387a-151">Se non c'è niente tooemit, questo metodo deve restituire senza la creazione di qualsiasi elemento.</span><span class="sxs-lookup"><span data-stu-id="b387a-151">If there is nothing tooemit, this method should return without emitting anything.</span></span> <span data-ttu-id="b387a-152">Si noti che `NextTuple()`, `Ack()` e `Fail()` vengono chiamati in un ciclo ridotto in un singolo thread nel processo C\#.</span><span class="sxs-lookup"><span data-stu-id="b387a-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="b387a-153">Quando sono non presenti alcun tooemit tuple, è toohave cortesia NextTuple sospensione per un breve periodo di tempo (ad esempio 10 millisecondi) in modo da non toowaste una quantità eccessiva della CPU.</span><span class="sxs-lookup"><span data-stu-id="b387a-153">When there are no tuples tooemit, it is courteous toohave NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="b387a-154">`Ack()` e `Fail()` verranno chiamati solo se il meccanismo di acknowledgement è abilitato nel file delle specifiche.</span><span class="sxs-lookup"><span data-stu-id="b387a-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="b387a-155">Hello `seqId` tooidentify utilizzati hello tupla che non è riconosciuto o non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="b387a-155">hello `seqId` is used tooidentify hello tuple which is acked or failed.</span></span> <span data-ttu-id="b387a-156">Pertanto se ack è abilitato nella topologia non transazionale, hello seguono questa funzione deve essere utilizzata in beccuccio:</span><span class="sxs-lookup"><span data-stu-id="b387a-156">So if ack is enabled in non-transactional topology, hello following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="b387a-157">Se ack non è supportato nella topologia non transazionale, hello `Ack()` e `Fail()` può essere lasciato come funzione vuoto.</span><span class="sxs-lookup"><span data-stu-id="b387a-157">If ack is not supported in non-transactional topology, hello `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="b387a-158">Hello `parms` parametri di input in queste funzioni sono dizionario appena vuoto, riservati per utilizzi futuri.</span><span class="sxs-lookup"><span data-stu-id="b387a-158">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="b387a-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="b387a-159">ISCPBolt</span></span>
<span data-ttu-id="b387a-160">ISCPBolt è interfaccia hello per fulmine non transazionale.</span><span class="sxs-lookup"><span data-stu-id="b387a-160">ISCPBolt is hello interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="b387a-161">Quando sono disponibili nuove tuple hello `Execute()` funzione verrà chiamata tooprocess è.</span><span class="sxs-lookup"><span data-stu-id="b387a-161">When new tuple is available, hello `Execute()` function will be called tooprocess it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="b387a-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="b387a-162">ISCPTxSpout</span></span>
<span data-ttu-id="b387a-163">ISCPTxSpout è interfaccia hello per beccuccio transazionale.</span><span class="sxs-lookup"><span data-stu-id="b387a-163">ISCPTxSpout is hello interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="b387a-164">Come avviene per la controparte non transazionale, `NextTx()`, `Ack()` e `Fail()` vengono chiamati in un ciclo ridotto in un singolo thread nel processo C\#.</span><span class="sxs-lookup"><span data-stu-id="b387a-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="b387a-165">Quando sono non presenti tooemit alcun dati, è toohave cortesia `NextTx` sospensione per un breve periodo di tempo (10 millisecondi) in modo da non toowaste una quantità eccessiva della CPU.</span><span class="sxs-lookup"><span data-stu-id="b387a-165">When there are no data tooemit, it is courteous toohave `NextTx` sleep for a short amount of time (10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="b387a-166">`NextTx()`viene chiamato toostart una nuova transazione hello parametro out `seqId` è usato tooidentify hello transazione, viene utilizzato anche in `Ack()` e `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="b387a-166">`NextTx()` is called toostart a new transaction, hello out parameter `seqId` is used tooidentify hello transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="b387a-167">In `NextTx()`, generare lato tooJava dati utente.</span><span class="sxs-lookup"><span data-stu-id="b387a-167">In `NextTx()`, user can emit data tooJava side.</span></span> <span data-ttu-id="b387a-168">riproduzione toosupport ZooKeeper verranno archiviati dati Hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-168">hello data will be stored in ZooKeeper toosupport replay.</span></span> <span data-ttu-id="b387a-169">Poiché la capacità di hello di ZooKeeper è molto limitata, l'utente deve creare solo metadati, non i dati di massa beccuccio transazionale.</span><span class="sxs-lookup"><span data-stu-id="b387a-169">Because hello capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="b387a-170">Storm riprodurrà automaticamente una transazione in caso di errore, dunque in un caso normale `Fail()` non dovrebbe essere chiamato.</span><span class="sxs-lookup"><span data-stu-id="b387a-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="b387a-171">Ma se SCP è possibile archiviare metadati hello emesso beccuccio transazionale, può chiamare `Fail()` quando hello metadati non sono valido.</span><span class="sxs-lookup"><span data-stu-id="b387a-171">But if SCP can check hello metadata emitted by transactional spout, it can call `Fail()` when hello metadata is invalid.</span></span>

<span data-ttu-id="b387a-172">Hello `parms` parametri di input in queste funzioni sono dizionario appena vuoto, riservati per utilizzi futuri.</span><span class="sxs-lookup"><span data-stu-id="b387a-172">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="b387a-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="b387a-173">ISCPBatchBolt</span></span>
<span data-ttu-id="b387a-174">ISCPBatchBolt è interfaccia hello per fulmine transazionale.</span><span class="sxs-lookup"><span data-stu-id="b387a-174">ISCPBatchBolt is hello interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="b387a-175">`Execute()`viene chiamato quando è presente una nuova tupla che pervengono a fulmine hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-175">`Execute()` is called when there is new tuple arriving at hello bolt.</span></span> <span data-ttu-id="b387a-176">`FinishBatch()` viene chiamato al termine di questa transazione.</span><span class="sxs-lookup"><span data-stu-id="b387a-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="b387a-177">Hello `parms` parametro di input è riservato per utilizzi futuri.</span><span class="sxs-lookup"><span data-stu-id="b387a-177">hello `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="b387a-178">Per la topologia transazionale esiste un concetto importante, `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="b387a-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="b387a-179">Ha due campi, `TxId` e `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="b387a-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="b387a-180">`TxId`è tooidentify utilizzati una transazione specifica e per una determinata transazione, se potrebbero essere presenti più tentativo ha esito negativo e transazione hello riprodotti.</span><span class="sxs-lookup"><span data-stu-id="b387a-180">`TxId` is used tooidentify a specific transaction, and for a given transaction, there may be multiple attempt if hello transaction fails and is replayed.</span></span> <span data-ttu-id="b387a-181">SCP.NET nuovo sarà un diverso ISCPBatchBolt oggetto tooprocess ogni `StormTxAttempt`, analogamente a cosa Storm sul lato di Java.</span><span class="sxs-lookup"><span data-stu-id="b387a-181">SCP.NET will new a different ISCPBatchBolt object tooprocess each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="b387a-182">scopo di Hello di questa struttura è l'elaborazione delle transazioni parallele toosupport.</span><span class="sxs-lookup"><span data-stu-id="b387a-182">hello purpose of this design is toosupport parallel transactions processing.</span></span> <span data-ttu-id="b387a-183">Utente necessario mantenerla tenga presente che se il tentativo di transazione è terminato, hello corrispondente ISCPBatchBolt oggetto verrà eliminato e raccolti nel Garbage Collector.</span><span class="sxs-lookup"><span data-stu-id="b387a-183">User should keep it in mind that if transaction attempt is finished, hello corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="b387a-184">Modello a oggetti</span><span class="sxs-lookup"><span data-stu-id="b387a-184">Object Model</span></span>
<span data-ttu-id="b387a-185">SCP.NET fornisce inoltre un semplice set di oggetti chiave per gli sviluppatori tooprogram con.</span><span class="sxs-lookup"><span data-stu-id="b387a-185">SCP.NET also provides a simple set of key objects for developers tooprogram with.</span></span> <span data-ttu-id="b387a-186">Si tratta degli oggetti **Context**, **StateStore** e **SCPRuntime**,</span><span class="sxs-lookup"><span data-stu-id="b387a-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="b387a-187">Essi verranno descritte in questa sezione parte rest hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-187">They will be discussed in hello rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="b387a-188">Context</span><span class="sxs-lookup"><span data-stu-id="b387a-188">Context</span></span>
<span data-ttu-id="b387a-189">Contesto fornisce un'applicazione toohello ambiente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b387a-189">Context provides a running environment toohello application.</span></span> <span data-ttu-id="b387a-190">Ogni istanza di ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) dispone di un'istanza Context corrispondente.</span><span class="sxs-lookup"><span data-stu-id="b387a-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="b387a-191">funzionalità di Hello fornita dal contesto possono essere suddivisi in due parti: parte statica di hello (1) disponibile in hello C intero\# elaborare, parte dinamica di hello (2) che è disponibile solo per l'istanza contesto hello specifico.</span><span class="sxs-lookup"><span data-stu-id="b387a-191">hello functionality provided by Context can be divided into two parts: (1) hello static part which is available in hello whole C\# process, (2) hello dynamic part which is only available for hello specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="b387a-192">Parte statica</span><span class="sxs-lookup"><span data-stu-id="b387a-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="b387a-193">`Logger` è fornito a scopi di log.</span><span class="sxs-lookup"><span data-stu-id="b387a-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="b387a-194">`pluginType`viene utilizzato tooindicate hello plug-in tipo di hello C\# processo.</span><span class="sxs-lookup"><span data-stu-id="b387a-194">`pluginType` is used tooindicate hello plugin type of hello C\# process.</span></span> <span data-ttu-id="b387a-195">Se hello C\# processo viene eseguito in modalità test locale (senza Java), il tipo di plug-in di hello è `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="b387a-195">If hello C\# process is run in local test mode (without Java), hello plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="b387a-196">`Config`viene fornito tooget i parametri di configurazione da parte di Java.</span><span class="sxs-lookup"><span data-stu-id="b387a-196">`Config` is provided tooget configuration parameters from Java side.</span></span> <span data-ttu-id="b387a-197">Hello parametri vengono passati dal lato Java quando C\# plug-in è stato inizializzato.</span><span class="sxs-lookup"><span data-stu-id="b387a-197">hello parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="b387a-198">Hello `Config` i parametri sono suddivisi in due parti: `stormConf` e `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="b387a-198">hello `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="b387a-199">`stormConf`è definiti dall'elevato numero di parametri e `pluginConf` è parametri hello definiti dal SCP.</span><span class="sxs-lookup"><span data-stu-id="b387a-199">`stormConf` is parameters defined by Storm and `pluginConf` is hello parameters defined by SCP.</span></span> <span data-ttu-id="b387a-200">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b387a-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="b387a-201">`TopologyContext`viene fornito il contesto di topologia hello tooget, risulta maggiormente utile per i componenti con più di parallelismo.</span><span class="sxs-lookup"><span data-stu-id="b387a-201">`TopologyContext` is provided tooget hello topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="b387a-202">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="b387a-202">Here is an example:</span></span>

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

### <a name="dynamic-part"></a><span data-ttu-id="b387a-203">Parte dinamica</span><span class="sxs-lookup"><span data-stu-id="b387a-203">Dynamic Part</span></span>
<span data-ttu-id="b387a-204">Hello seguenti interfacce sono pertinente tooa determinato contesto dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="b387a-204">hello following interfaces are pertinent tooa certain Context instance.</span></span> <span data-ttu-id="b387a-205">l'istanza contesto Hello creato dal SCP.NET piattaforma e codice utente toohello passato:</span><span class="sxs-lookup"><span data-stu-id="b387a-205">hello Context instance is created by SCP.NET platform and passed toohello user code:</span></span>

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="b387a-206">Per non transazionale beccuccio supporto ack, verrà fornita al metodo hello:</span><span class="sxs-lookup"><span data-stu-id="b387a-206">For non-transactional spout supporting ack, hello following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="b387a-207">Per non transazionale fulmine supporto ack, dovrebbe essere in modo esplicito `Ack()` o `Fail()` hello tupla ricevuto.</span><span class="sxs-lookup"><span data-stu-id="b387a-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` hello tuple it received.</span></span> <span data-ttu-id="b387a-208">E per la creazione dei nuovi tupla, è necessario specificare anche Anchor hello di hello nuova tupla.</span><span class="sxs-lookup"><span data-stu-id="b387a-208">And when emitting new tuple, it must also specify hello anchors of hello new tuple.</span></span> <span data-ttu-id="b387a-209">viene fornito Hello dei seguenti metodi.</span><span class="sxs-lookup"><span data-stu-id="b387a-209">hello following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="b387a-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="b387a-210">StateStore</span></span>
<span data-ttu-id="b387a-211">`StateStore` fornisce servizi metadati, generazione di sequenze monotone e coordinamento senza attesa.</span><span class="sxs-lookup"><span data-stu-id="b387a-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="b387a-212">`StateStore`consente di creare astrazioni di concorrenza distribuite di livello superiore, tra cui blocchi distribuiti, code distribuite e servizi di transazione.</span><span class="sxs-lookup"><span data-stu-id="b387a-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="b387a-213">SCP applicazioni utilizzano hello `State` oggetto toopersist alcune informazioni riportate in ZooKeeper, soprattutto per topologia transazionale.</span><span class="sxs-lookup"><span data-stu-id="b387a-213">SCP applications may use hello `State` object toopersist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="b387a-214">In questo modo, se si blocca beccuccio transazionale e si riavvia, può recuperare le informazioni necessarie hello ZooKeeper e riavviare pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-214">Doing so, if transactional spout crashes and restart, it can retrieve hello necessary information from ZooKeeper and restart hello pipeline.</span></span>

<span data-ttu-id="b387a-215">Hello `StateStore` principalmente oggetto dispone di questi metodi:</span><span class="sxs-lookup"><span data-stu-id="b387a-215">hello `StateStore` object mainly has these methods:</span></span>

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

<span data-ttu-id="b387a-216">Hello `State` principalmente oggetto dispone di questi metodi:</span><span class="sxs-lookup"><span data-stu-id="b387a-216">hello `State` object mainly has these methods:</span></span>

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

<span data-ttu-id="b387a-217">Per hello `Commit()` metodo, quando simpleMode è impostato tootrue, semplicemente eliminerà hello ZNode in ZooKeeper corrispondente.</span><span class="sxs-lookup"><span data-stu-id="b387a-217">For hello `Commit()` method, when simpleMode is set tootrue, it will simply delete hello corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="b387a-218">In caso contrario, verrà eliminata hello ZNode corrente e l'aggiunta di un nuovo nodo in hello COMMITTED\_percorso.</span><span class="sxs-lookup"><span data-stu-id="b387a-218">Otherwise, it will delete hello current ZNode, and adding a new node in hello COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="b387a-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="b387a-219">SCPRuntime</span></span>
<span data-ttu-id="b387a-220">SCPRuntime fornisce hello due metodi seguenti.</span><span class="sxs-lookup"><span data-stu-id="b387a-220">SCPRuntime provides hello following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="b387a-221">`Initialize()`è l'ambiente di runtime di tooinitialize utilizzati hello SCP.</span><span class="sxs-lookup"><span data-stu-id="b387a-221">`Initialize()` is used tooinitialize hello SCP runtime environment.</span></span> <span data-ttu-id="b387a-222">In questo metodo, hello C\# processo si connetterà lato Java toohello e ottiene i parametri di configurazione e il contesto di topologia.</span><span class="sxs-lookup"><span data-stu-id="b387a-222">In this method, hello C\# process will connect toohello Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="b387a-223">`LaunchPlugin()`è tookick utilizzato dal messaggio hello l'elaborazione del ciclo.</span><span class="sxs-lookup"><span data-stu-id="b387a-223">`LaunchPlugin()` is used tookick off hello message processing loop.</span></span> <span data-ttu-id="b387a-224">In questo ciclo, hello C\# plug-in verrà visualizzato il modulo di messaggi sul lato di Java (compresi i segnali tuple e controllo), e quindi elaborare i messaggi hello, ad esempio chiamando il metodo di interfaccia hello forniscono codice utente hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-224">In this loop, hello C\# plugin will receive messages form Java side (including tuples and control signals), and then process hello messages, perhaps calling hello interface method provide by hello user code.</span></span> <span data-ttu-id="b387a-225">parametro di input per il metodo Hello `LaunchPlugin()` è un delegato che può restituire un oggetto che implementa l'interfaccia ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.</span><span class="sxs-lookup"><span data-stu-id="b387a-225">hello input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="b387a-226">Per ISCPBatchBolt, è possibile ottenere `StormTxAttempt` da `parms`e utilizzare toojudge se si tratta di un tentativo di riproduzione.</span><span class="sxs-lookup"><span data-stu-id="b387a-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it toojudge whether it is a replayed attempt.</span></span> <span data-ttu-id="b387a-227">Questa operazione viene in genere eseguita in fulmine commit hello e viene fornita in hello `HelloWorldTx` esempio.</span><span class="sxs-lookup"><span data-stu-id="b387a-227">This is usually done at hello commit bolt, and it is demonstrated in hello `HelloWorldTx` example.</span></span>

<span data-ttu-id="b387a-228">In generale, hello SCP i plug-in possono essere eseguite in due modalità di seguito:</span><span class="sxs-lookup"><span data-stu-id="b387a-228">Generally speaking, hello SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="b387a-229">Modalità di Test locale: In questa modalità, hello SCP i plug-in (hello C\# codice utente) eseguiti in Visual Studio durante la fase di sviluppo hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-229">Local Test Mode: In this mode, hello SCP plugins (hello C\# user code) run inside Visual Studio during hello development phase.</span></span> <span data-ttu-id="b387a-230">`LocalContext`può essere utilizzato in questa modalità, che fornisce i metodo tooserialize hello generato tuple toolocal file e rileggerle toomemory.</span><span class="sxs-lookup"><span data-stu-id="b387a-230">`LocalContext` can be used in this mode, which provides method tooserialize hello emitted tuples toolocal files, and read them back toomemory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="b387a-231">Modalità normale: In questa modalità, i plug-in di hello SCP vengono avviati dal processo java storm.</span><span class="sxs-lookup"><span data-stu-id="b387a-231">Regular Mode: In this mode, hello SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="b387a-232">Di seguito è riportato un esempio di avvio del plug-in SCP:</span><span class="sxs-lookup"><span data-stu-id="b387a-232">Here is an example of launching SCP plugin:</span></span>
   
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

## <a name="topology-specification-language"></a><span data-ttu-id="b387a-233">Linguaggio di specifica della topologia</span><span class="sxs-lookup"><span data-stu-id="b387a-233">Topology Specification Language</span></span>
<span data-ttu-id="b387a-234">SCP Topology Specification è un linguaggio specifico di dominio (DSL) per la descrizione e la configurazione di topologie SCP.</span><span class="sxs-lookup"><span data-stu-id="b387a-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="b387a-235">È basato sul DSL di Storm in linguaggio Clojure (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) ed esteso da SCP.</span><span class="sxs-lookup"><span data-stu-id="b387a-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="b387a-236">Specifiche di topologia possono essere inviate direttamente toostorm cluster per l'esecuzione tramite hello ***runspec*** comando.</span><span class="sxs-lookup"><span data-stu-id="b387a-236">Topology specifications can be submitted directly toostorm cluster for execution via hello ***runspec*** command.</span></span>

<span data-ttu-id="b387a-237">SCP.NET add seguire funzioni toodefine hello transazionale topologia:</span><span class="sxs-lookup"><span data-stu-id="b387a-237">SCP.NET has add follow functions toodefine hello Transactional Topology:</span></span>

| <span data-ttu-id="b387a-238">**Nuove funzioni**</span><span class="sxs-lookup"><span data-stu-id="b387a-238">**New Functions**</span></span> | <span data-ttu-id="b387a-239">**Parametri**</span><span class="sxs-lookup"><span data-stu-id="b387a-239">**Parameters**</span></span> | <span data-ttu-id="b387a-240">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="b387a-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b387a-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="b387a-241">**tx-topolopy**</span></span> |<span data-ttu-id="b387a-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="b387a-242">topology-name</span></span><br /><span data-ttu-id="b387a-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="b387a-243">spout-map</span></span><br /><span data-ttu-id="b387a-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="b387a-244">bolt-map</span></span> |<span data-ttu-id="b387a-245">Definire una topologia transazionale con il nome di topologia hello, &nbsp;spouts mappa definizione e hello bulloni definizione mappa</span><span class="sxs-lookup"><span data-stu-id="b387a-245">Define a transactional topology with hello topology name, &nbsp;spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="b387a-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="b387a-246">**scp-tx-spout**</span></span> |<span data-ttu-id="b387a-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="b387a-247">exec-name</span></span><br /><span data-ttu-id="b387a-248">args</span><span class="sxs-lookup"><span data-stu-id="b387a-248">args</span></span><br /><span data-ttu-id="b387a-249">fields</span><span class="sxs-lookup"><span data-stu-id="b387a-249">fields</span></span> |<span data-ttu-id="b387a-250">Consente di definire uno Spout transazionale.</span><span class="sxs-lookup"><span data-stu-id="b387a-250">Define a transactional spout.</span></span> <span data-ttu-id="b387a-251">Verrà eseguito con un'applicazione hello ***exec nome*** utilizzando ***args***.</span><span class="sxs-lookup"><span data-stu-id="b387a-251">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="b387a-252">Hello ***campi*** campi di Output di hello per beccuccio</span><span class="sxs-lookup"><span data-stu-id="b387a-252">hello ***fields*** is hello Output Fields for spout</span></span> |
| <span data-ttu-id="b387a-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="b387a-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="b387a-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="b387a-254">exec-name</span></span><br /><span data-ttu-id="b387a-255">args</span><span class="sxs-lookup"><span data-stu-id="b387a-255">args</span></span><br /><span data-ttu-id="b387a-256">fields</span><span class="sxs-lookup"><span data-stu-id="b387a-256">fields</span></span> |<span data-ttu-id="b387a-257">Consente di definire un Bolt batch transazionale.</span><span class="sxs-lookup"><span data-stu-id="b387a-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="b387a-258">Verrà eseguito con un'applicazione hello ***exec nome*** utilizzando ***args.***</span><span class="sxs-lookup"><span data-stu-id="b387a-258">It will run hello application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="b387a-259">Hello campi sono hello campi di Output per fulmine.</span><span class="sxs-lookup"><span data-stu-id="b387a-259">hello Fields is hello Output Fields for bolt.</span></span> |
| <span data-ttu-id="b387a-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="b387a-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="b387a-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="b387a-261">exec-name</span></span><br /><span data-ttu-id="b387a-262">args</span><span class="sxs-lookup"><span data-stu-id="b387a-262">args</span></span><br /><span data-ttu-id="b387a-263">fields</span><span class="sxs-lookup"><span data-stu-id="b387a-263">fields</span></span> |<span data-ttu-id="b387a-264">Consente di definire un Bolt di commit transazionale.</span><span class="sxs-lookup"><span data-stu-id="b387a-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="b387a-265">Verrà eseguito con un'applicazione hello ***exec nome*** utilizzando ***args***.</span><span class="sxs-lookup"><span data-stu-id="b387a-265">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="b387a-266">Hello ***campi*** campi di Output di hello per fulmine</span><span class="sxs-lookup"><span data-stu-id="b387a-266">hello ***fields*** is hello Output Fields for bolt</span></span> |
| <span data-ttu-id="b387a-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="b387a-267">**nontx-topolopy**</span></span> |<span data-ttu-id="b387a-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="b387a-268">topology-name</span></span><br /><span data-ttu-id="b387a-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="b387a-269">spout-map</span></span><br /><span data-ttu-id="b387a-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="b387a-270">bolt-map</span></span> |<span data-ttu-id="b387a-271">Definire una topologia non transazionale con il nome di topologia hello,&nbsp; spouts mappa definizione e hello bulloni definizione mappa</span><span class="sxs-lookup"><span data-stu-id="b387a-271">Define a nontransactional topology with hello topology name,&nbsp; spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="b387a-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="b387a-272">**scp-spout**</span></span> |<span data-ttu-id="b387a-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="b387a-273">exec-name</span></span><br /><span data-ttu-id="b387a-274">args</span><span class="sxs-lookup"><span data-stu-id="b387a-274">args</span></span><br /><span data-ttu-id="b387a-275">fields</span><span class="sxs-lookup"><span data-stu-id="b387a-275">fields</span></span><br /><span data-ttu-id="b387a-276">Parametri</span><span class="sxs-lookup"><span data-stu-id="b387a-276">parameters</span></span> |<span data-ttu-id="b387a-277">Consente di definire uno Spout non transazionale.</span><span class="sxs-lookup"><span data-stu-id="b387a-277">Define a nontransactional spout.</span></span> <span data-ttu-id="b387a-278">Verrà eseguito con un'applicazione hello ***exec nome*** utilizzando ***args***.</span><span class="sxs-lookup"><span data-stu-id="b387a-278">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="b387a-279">Hello ***campi*** campi di Output di hello per beccuccio</span><span class="sxs-lookup"><span data-stu-id="b387a-279">hello ***fields*** is hello Output Fields for spout</span></span><br /><br /><span data-ttu-id="b387a-280">Hello ***parametri*** è facoltativo, utilizzarlo toospecify alcuni parametri, ad esempio "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="b387a-280">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="b387a-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="b387a-281">**scp-bolt**</span></span> |<span data-ttu-id="b387a-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="b387a-282">exec-name</span></span><br /><span data-ttu-id="b387a-283">args</span><span class="sxs-lookup"><span data-stu-id="b387a-283">args</span></span><br /><span data-ttu-id="b387a-284">fields</span><span class="sxs-lookup"><span data-stu-id="b387a-284">fields</span></span><br /><span data-ttu-id="b387a-285">Parametri</span><span class="sxs-lookup"><span data-stu-id="b387a-285">parameters</span></span> |<span data-ttu-id="b387a-286">Consente di definire un Bolt non transazionale.</span><span class="sxs-lookup"><span data-stu-id="b387a-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="b387a-287">Verrà eseguito con un'applicazione hello ***exec nome*** utilizzando ***args***.</span><span class="sxs-lookup"><span data-stu-id="b387a-287">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="b387a-288">Hello ***campi*** campi di Output di hello per fulmine</span><span class="sxs-lookup"><span data-stu-id="b387a-288">hello ***fields*** is hello Output Fields for bolt</span></span><br /><br /><span data-ttu-id="b387a-289">Hello ***parametri*** è facoltativo, utilizzarlo toospecify alcuni parametri, ad esempio "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="b387a-289">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="b387a-290">In SCP.NET sono disponibili le parole chiave seguenti:</span><span class="sxs-lookup"><span data-stu-id="b387a-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="b387a-291">**Parole chiave**</span><span class="sxs-lookup"><span data-stu-id="b387a-291">**Key Words**</span></span> | <span data-ttu-id="b387a-292">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="b387a-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="b387a-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="b387a-293">**:name**</span></span> |<span data-ttu-id="b387a-294">Definire nome topologia hello</span><span class="sxs-lookup"><span data-stu-id="b387a-294">Define hello Topology Name</span></span> |
| <span data-ttu-id="b387a-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="b387a-295">**:topology**</span></span> |<span data-ttu-id="b387a-296">Definire topologia con hello sopra le funzioni hello e in quelli di compilazione.</span><span class="sxs-lookup"><span data-stu-id="b387a-296">Define hello Topology using hello above functions and build in ones.</span></span> |
| <span data-ttu-id="b387a-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="b387a-297">**:p**</span></span> |<span data-ttu-id="b387a-298">Definire l'hint di parallelismo hello per ogni beccuccio o di un fulmine.</span><span class="sxs-lookup"><span data-stu-id="b387a-298">Define hello parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="b387a-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="b387a-299">**:config**</span></span> |<span data-ttu-id="b387a-300">Definire configurare parametri o aggiornamento hello quelli esistenti</span><span class="sxs-lookup"><span data-stu-id="b387a-300">Define configure parameter or update hello existing ones</span></span> |
| <span data-ttu-id="b387a-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="b387a-301">**:schema**</span></span> |<span data-ttu-id="b387a-302">Definire hello dello Schema del flusso.</span><span class="sxs-lookup"><span data-stu-id="b387a-302">Define hello Schema of Stream.</span></span> |

<span data-ttu-id="b387a-303">E i parametri di uso frequente seguenti:</span><span class="sxs-lookup"><span data-stu-id="b387a-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="b387a-304">**Parametro**</span><span class="sxs-lookup"><span data-stu-id="b387a-304">**Parameter**</span></span> | <span data-ttu-id="b387a-305">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="b387a-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="b387a-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="b387a-306">**"plugin.name"**</span></span> |<span data-ttu-id="b387a-307">nome di file exe di plug-in hello c#</span><span class="sxs-lookup"><span data-stu-id="b387a-307">exe file name of hello C# plugin</span></span> |
| <span data-ttu-id="b387a-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="b387a-308">**"plugin.args"**</span></span> |<span data-ttu-id="b387a-309">Argomenti del plug-in.</span><span class="sxs-lookup"><span data-stu-id="b387a-309">plugin args</span></span> |
| <span data-ttu-id="b387a-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="b387a-310">**"output.schema"**</span></span> |<span data-ttu-id="b387a-311">Schema di output.</span><span class="sxs-lookup"><span data-stu-id="b387a-311">Output schema</span></span> |
| <span data-ttu-id="b387a-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="b387a-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="b387a-313">Abilitazione o meno dell'acknowledgement per la topologia non transazionale.</span><span class="sxs-lookup"><span data-stu-id="b387a-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="b387a-314">comando runspec Hello verrà distribuito insieme a bits hello, utilizzo di hello è ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b387a-314">hello runspec command will be deployed together with hello bits, hello usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="b387a-315">Hello ***risorse dir*** parametro è facoltativo, è necessario toospecify quando si desidera tooplug C\# applicazione e la directory conterrà un'applicazione hello, le dipendenze di hello e configurazioni.</span><span class="sxs-lookup"><span data-stu-id="b387a-315">hello ***resource-dir*** parameter is optional, you need toospecify it when you want tooplug a C\# application, and this directory will contain hello application, hello dependencies and configurations.</span></span>

<span data-ttu-id="b387a-316">Hello ***classpath*** parametro è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="b387a-316">hello ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="b387a-317">È utilizzato toospecify hello Java classpath se file specifica hello contiene Spout Java o fulmine.</span><span class="sxs-lookup"><span data-stu-id="b387a-317">It is used toospecify hello Java classpath if hello spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="b387a-318">Funzionalità varie</span><span class="sxs-lookup"><span data-stu-id="b387a-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="b387a-319">Dichiarazione dello schema di input e di output</span><span class="sxs-lookup"><span data-stu-id="b387a-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="b387a-320">utente Hello può generare una tupla in C\# elaborare, hello piattaforma deve essere tooserialize hello tupla in byte [], trasferimento tooJava lato, e Storm trasferirà questo destinazioni toohello tupla.</span><span class="sxs-lookup"><span data-stu-id="b387a-320">hello user can emit tuple in C\# process, hello platform needs tooserialize hello tuple into byte[], transfer tooJava side, and Storm will transfer this tuple toohello targets.</span></span> <span data-ttu-id="b387a-321">Nel frattempo nel componente a valle, hello C\# processo ricevere tupla dal lato java e convertirlo tipi originali toohello dalla piattaforma, tutte queste operazioni sono nascosti da hello piattaforma.</span><span class="sxs-lookup"><span data-stu-id="b387a-321">Meanwhile in downstream component, hello C\# process will receive tuple back from java side, and convert it toohello original types by platform, all these operations are hidden by hello Platform.</span></span>

<span data-ttu-id="b387a-322">serializzazione di hello toosupport e la deserializzazione, il codice utente deve schema hello toodeclare di hello input e output.</span><span class="sxs-lookup"><span data-stu-id="b387a-322">toosupport hello serialization and deserialization, user code needs toodeclare hello schema of hello inputs and outputs.</span></span>

<span data-ttu-id="b387a-323">schema di flusso di input/output di Hello è definito come un dizionario, hello è hello StreamId e il valore di hello è hello tipi di colonne hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-323">hello input/output stream schema is defined as a dictionary, hello key is hello StreamId and hello value is hello Types of hello columns.</span></span> <span data-ttu-id="b387a-324">componente Hello può avere più flussi dichiarati.</span><span class="sxs-lookup"><span data-stu-id="b387a-324">hello component can have multi-streams declared.</span></span>

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


<span data-ttu-id="b387a-325">Nell'oggetto di contesto, abbiamo hello aggiunto API seguente:</span><span class="sxs-lookup"><span data-stu-id="b387a-325">In Context object, we have hello following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="b387a-326">Il codice utente deve assicurarsi che le tuple hello generate rispettano schema hello definito per il flusso, o hello verrà generata un'eccezione di runtime.</span><span class="sxs-lookup"><span data-stu-id="b387a-326">User code must make sure hello tuples emitted obey hello schema defined for that stream, or hello system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="b387a-327">Supporto di più flussi</span><span class="sxs-lookup"><span data-stu-id="b387a-327">Multi-Stream Support</span></span>
<span data-ttu-id="b387a-328">Utente supporta SCP codice tooemit o ricevere da più flussi distinti a hello stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="b387a-328">SCP supports user code tooemit or receive from multiple distinct streams at hello same time.</span></span> <span data-ttu-id="b387a-329">supporto di Hello riflette nell'oggetto di contesto hello hello Emit metodo accetta un parametro di ID flusso facoltativo.</span><span class="sxs-lookup"><span data-stu-id="b387a-329">hello support reflects in hello Context object as hello Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="b387a-330">Sono stati aggiunti due metodi nell'oggetto di contesto SCP.NET hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-330">Two methods in hello SCP.NET Context object have been added.</span></span> <span data-ttu-id="b387a-331">Sono utilizzati tooemit toospecify StreamId tupla o tuple.</span><span class="sxs-lookup"><span data-stu-id="b387a-331">They are used tooemit Tuple or Tuples toospecify StreamId.</span></span> <span data-ttu-id="b387a-332">Hello StreamId è una stringa e deve toobe coerente in entrambi C\# e hello specifica definizione di topologia.</span><span class="sxs-lookup"><span data-stu-id="b387a-332">hello StreamId is a string and it needs toobe consistent in both C\# and hello Topology Definition Spec.</span></span>

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="b387a-333">Hello concessioni tooa inesistente flusso causerà le eccezioni di runtime.</span><span class="sxs-lookup"><span data-stu-id="b387a-333">hello emitting tooa non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="b387a-334">Raggruppamento dei campi</span><span class="sxs-lookup"><span data-stu-id="b387a-334">Fields Grouping</span></span>
<span data-ttu-id="b387a-335">Hello compilazione aggiuntivo raggruppamento di campi in Strom non funziona correttamente in SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="b387a-335">hello build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="b387a-336">Sul lato di Java Proxy hello, tutti i tipi di dati di campi di hello sono effettivamente byte [] e i campi di hello raggruppamento utilizza hello byte [] oggetto hash tooperform hello raggruppamento di codice.</span><span class="sxs-lookup"><span data-stu-id="b387a-336">On hello Java Proxy side, all hello fields data types are actually byte[], and hello fields grouping uses hello byte[] object hash code tooperform hello grouping.</span></span> <span data-ttu-id="b387a-337">codice hash dell'oggetto Hello byte [] è l'indirizzo di hello di questo oggetto in memoria.</span><span class="sxs-lookup"><span data-stu-id="b387a-337">hello byte[] object hash code is hello address of this object in memory.</span></span> <span data-ttu-id="b387a-338">Il raggruppamento di hello sarà errato per due byte [] oggetti hello tale condivisione di contenuto ma non hello stesso indirizzo.</span><span class="sxs-lookup"><span data-stu-id="b387a-338">So hello grouping will be wrong for two byte[] objects that share hello same content but not hello same address.</span></span>

<span data-ttu-id="b387a-339">SCP.NET aggiunge un metodo di raggruppamento personalizzati e verrà utilizzato il contenuto di hello di raggruppamento hello toodo di hello byte [].</span><span class="sxs-lookup"><span data-stu-id="b387a-339">SCP.NET adds a customized grouping method, and it will use hello content of hello byte[] toodo hello grouping.</span></span> <span data-ttu-id="b387a-340">In **SPEC** file, la sintassi di hello è ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b387a-340">In **SPEC** file, hello syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="b387a-341">Qui</span><span class="sxs-lookup"><span data-stu-id="b387a-341">Here,</span></span>

1. <span data-ttu-id="b387a-342">"scp-field-group" vuol dire "raggruppamento campi personalizzato implementato da SCP".</span><span class="sxs-lookup"><span data-stu-id="b387a-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="b387a-343">":tx" o ":non-tx" indica se si tratta o meno di una topologia transazionale.</span><span class="sxs-lookup"><span data-stu-id="b387a-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="b387a-344">Queste informazioni è necessario poiché hello indice iniziale è diversa in tx e topologie non tx.</span><span class="sxs-lookup"><span data-stu-id="b387a-344">We need this information since hello starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="b387a-345">[0,1] indica un hashset di Id campo, che parte da 0.</span><span class="sxs-lookup"><span data-stu-id="b387a-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="b387a-346">Topologia ibrida</span><span class="sxs-lookup"><span data-stu-id="b387a-346">Hybrid topology</span></span>
<span data-ttu-id="b387a-347">Hello che Storm native viene scritta in Java.</span><span class="sxs-lookup"><span data-stu-id="b387a-347">hello native Storm is written in Java.</span></span> <span data-ttu-id="b387a-348">E SCP.Net è migliorato è tooenable nostri toowrite doganali C\# toohandle di codice la logica di business.</span><span class="sxs-lookup"><span data-stu-id="b387a-348">And SCP.Net has enhanced it tooenable our customs toowrite C\# code toohandle their business logic.</span></span> <span data-ttu-id="b387a-349">SCP supporta però anche le topologie ibride, che contengono spout/bolt sia in linguaggio Java sia in C\#.</span><span class="sxs-lookup"><span data-stu-id="b387a-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="b387a-350">Specificare gli Spout e i Bolt Java nel file delle specifiche</span><span class="sxs-lookup"><span data-stu-id="b387a-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="b387a-351">Nel file specifica, "scp beccuccio" e "scp fulmine" può essere anche usato toospecify Java Spouts e le viti, di seguito è riportato un esempio:</span><span class="sxs-lookup"><span data-stu-id="b387a-351">In spec file, "scp-spout" and "scp-bolt" can also be used toospecify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="b387a-352">Qui `microsoft.scp.example.HybridTopology.Generator` hello nome di classe Java Spout hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-352">Here `microsoft.scp.example.HybridTopology.Generator` is hello name of hello Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="b387a-353">Specificare il classpath Java nel comando runSpec</span><span class="sxs-lookup"><span data-stu-id="b387a-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="b387a-354">Se si desidera topologia toosubmit contenente Spouts Java o bulloni, necessario toofirst compilazione hello Spouts Java o bulloni e ricevere i file Jar hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-354">If you want toosubmit topology containing Java Spouts or Bolts, you need toofirst compile hello Java Spouts or Bolts and get hello Jar files.</span></span> <span data-ttu-id="b387a-355">Quindi è necessario specificare il classpath java hello che contiene i file Jar hello durante l'invio di topologia.</span><span class="sxs-lookup"><span data-stu-id="b387a-355">Then you should specify hello java classpath that contains hello Jar files when submitting topology.</span></span> <span data-ttu-id="b387a-356">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="b387a-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="b387a-357">Qui **esempi\\HybridTopology\\java\\destinazione\\**  è la cartella hello contenente file Jar di Java beccuccio/fulmine hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-357">Here **examples\\HybridTopology\\java\\target\\** is hello folder containing hello Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="b387a-358">Serializzazione e deserializzazione tra Java e C\\</span><span class="sxs-lookup"><span data-stu-id="b387a-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="b387a-359">Il componente SCP include il lato Java e il lato C\#.</span><span class="sxs-lookup"><span data-stu-id="b387a-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="b387a-360">In ordine toointeract con bulloni/Spouts Java native, serializzazione/deserializzazione devono essere effettuata tra il lato di Java e C\# sul lato, come illustrato nel seguente grafico hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-360">In order toointeract with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in hello following graph.</span></span>

![diagramma del componente java invio componente tooSCP invio tooJava componente](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="b387a-362">**Serializzazione sul lato Java e deserializzazione sul lato C#\#**</span><span class="sxs-lookup"><span data-stu-id="b387a-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="b387a-363">Prima di tutto è necessario fornire l'implementazione predefinita per la serializzazione sul lato Java e la deserializzazione sul lato C\#.</span><span class="sxs-lookup"><span data-stu-id="b387a-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="b387a-364">metodo di serializzazione Hello sul lato di Java può essere specificato nel file specifica:</span><span class="sxs-lookup"><span data-stu-id="b387a-364">hello serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="b387a-365">metodo di deserializzazione in C Hello\# lato deve essere specificato in C\# codice utente:</span><span class="sxs-lookup"><span data-stu-id="b387a-365">hello deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="b387a-366">Questa implementazione predefinita deve gestire la maggior parte dei casi, se il tipo di dati di hello non è troppo complesso.</span><span class="sxs-lookup"><span data-stu-id="b387a-366">This default implementation should handle most cases if hello data type is not too complex.</span></span> <span data-ttu-id="b387a-367">In alcuni casi, sia perché hello tipo di dati utente è troppo complessa o perché hello prestazioni dell'implementazione predefinita non soddisfano hello requisito dell'utente, è possibile plug-nella propria implementazione.</span><span class="sxs-lookup"><span data-stu-id="b387a-367">For certain cases, either because hello user data type is too complex, or because hello performance of our default implementation does not meet hello user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="b387a-368">interfaccia di serializzazione Hello in java lato è definito come:</span><span class="sxs-lookup"><span data-stu-id="b387a-368">hello serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="b387a-369">Hello deserializzare interfaccia c\# lato è definito come:</span><span class="sxs-lookup"><span data-stu-id="b387a-369">hello deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="b387a-370">interfaccia pubblica ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="b387a-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="b387a-371">**Serializzazione sul lato C\# e deserializzazione sul lato Java**</span><span class="sxs-lookup"><span data-stu-id="b387a-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="b387a-372">metodo di serializzazione in C Hello\# lato deve essere specificato in C\# codice utente:</span><span class="sxs-lookup"><span data-stu-id="b387a-372">hello serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="b387a-373">metodo di deserializzazione nel lato Java Hello deve essere specificato nel file specifica:</span><span class="sxs-lookup"><span data-stu-id="b387a-373">hello Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="b387a-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="b387a-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="b387a-375">Ecco di nome hello del deserializzatore "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" e "microsoft.scp.example.HybridTopology.Person" è dati hello classe di destinazione hello vengano deserializzati.</span><span class="sxs-lookup"><span data-stu-id="b387a-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is hello name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is hello target class hello data is deserialized to.</span></span>
   
   <span data-ttu-id="b387a-376">L'utente può anche collegare una propria implementazione del serializzatore C\# e del deserializzatore Java.</span><span class="sxs-lookup"><span data-stu-id="b387a-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="b387a-377">Si tratta dell'interfaccia hello per C\# serializzatore:</span><span class="sxs-lookup"><span data-stu-id="b387a-377">This is hello interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="b387a-378">Questa è l'interfaccia di hello deserializzatore Java:</span><span class="sxs-lookup"><span data-stu-id="b387a-378">This is hello interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="b387a-379">Modalità host di SCP</span><span class="sxs-lookup"><span data-stu-id="b387a-379">SCP Host Mode</span></span>
<span data-ttu-id="b387a-380">In questa modalità, utente possa compilare tooDLL i codici e utilizzare SCPHost.exe fornito dalla topologia toosubmit SCP.</span><span class="sxs-lookup"><span data-stu-id="b387a-380">In this mode, user can compile their codes tooDLL, and use SCPHost.exe provided by SCP toosubmit topology.</span></span> <span data-ttu-id="b387a-381">file di specifiche Hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b387a-381">hello spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="b387a-382">Qui `plugin.name` viene specificato come file `SCPHost.exe` fornito dall’SDK di SCP.</span><span class="sxs-lookup"><span data-stu-id="b387a-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="b387a-383">SCPHost.exe accetta esattamente tre parametri:</span><span class="sxs-lookup"><span data-stu-id="b387a-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="b387a-384">Hello prima uno è il nome DLL hello, ovvero `"HelloWorld.dll"` in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="b387a-384">hello first one is hello DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="b387a-385">Hello secondo è il nome classe hello, ovvero `"Scp.App.HelloWorld.Generator"` in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="b387a-385">hello second one is hello Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="b387a-386">Hello terzo uno è hello nome di un metodo statico pubblico, che può essere richiamato tooget un'istanza di ISCPPlugin.</span><span class="sxs-lookup"><span data-stu-id="b387a-386">hello third one is hello name of a public static method, which can be invoked tooget an instance of ISCPPlugin.</span></span>

<span data-ttu-id="b387a-387">In modalità host il codice utente viene compilato come DLL e richiamato dalla piattaforma SCP.</span><span class="sxs-lookup"><span data-stu-id="b387a-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="b387a-388">Pertanto piattaforma SCP possibile ottenere il controllo completo della logica di elaborazione intero hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-388">So SCP platform can get full control of hello whole processing logic.</span></span> <span data-ttu-id="b387a-389">Pertanto si consiglia ai clienti toosubmit topologia in modalità di host SCP poiché può semplificare l'esperienza di sviluppo hello e fine di rendere più flessibilità e una migliore compatibilità con le versioni precedenti per e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="b387a-389">So we recommend our customers toosubmit topology in SCP host mode since it can simplify hello development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="b387a-390">Esempi di programmazione SCP</span><span class="sxs-lookup"><span data-stu-id="b387a-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="b387a-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="b387a-391">HelloWorld</span></span>
<span data-ttu-id="b387a-392">**HelloWorld** è un esempio molto semplice di tooshow un'idea di SCP.Net.</span><span class="sxs-lookup"><span data-stu-id="b387a-392">**HelloWorld** is a very simple example tooshow a taste of SCP.Net.</span></span> <span data-ttu-id="b387a-393">Usa una topologia non transazionale con uno spout denominato **generator** e due bolt denominati **splitter** e **counter**.</span><span class="sxs-lookup"><span data-stu-id="b387a-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="b387a-394">beccuccio Hello **generatore** verrà generare alcune frasi in modo casuale e generare le frasi troppo**divisione**.</span><span class="sxs-lookup"><span data-stu-id="b387a-394">hello spout **generator** will randomly generate some sentences, and emit these sentences too**splitter**.</span></span> <span data-ttu-id="b387a-395">fulmine Hello **divisione** verrà suddiviso toowords frasi hello e generare queste parole troppo**contatore** fulmine.</span><span class="sxs-lookup"><span data-stu-id="b387a-395">hello bolt **splitter** will split hello sentences toowords and emit these words too**counter** bolt.</span></span> <span data-ttu-id="b387a-396">Hello fulmine "counter" utilizza un numero di occorrenze dizionario toorecord hello di ogni parola.</span><span class="sxs-lookup"><span data-stu-id="b387a-396">hello bolt "counter" uses a dictionary toorecord hello occurrence number of each word.</span></span>

<span data-ttu-id="b387a-397">Per questo esempio sono presenti due file di specifiche, **HelloWorld.spec** e **HelloWorld\_EnableAck.spec**.</span><span class="sxs-lookup"><span data-stu-id="b387a-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="b387a-398">In C hello\# codice, è possibile scoprire se ack è abilitato tramite il recupero pluginConf hello da parte di Java.</span><span class="sxs-lookup"><span data-stu-id="b387a-398">In hello C\# code, it can find out whether ack is enabled by getting hello pluginConf from Java side.</span></span>

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="b387a-399">In beccuccio hello, se ack è abilitato, un dizionario è usato toocache hello tuple che non sono stato riconosciuto.</span><span class="sxs-lookup"><span data-stu-id="b387a-399">In hello spout, if ack is enabled, a dictionary is used toocache hello tuples that have not been acked.</span></span> <span data-ttu-id="b387a-400">Se viene chiamato Fail(), hello tupla verrà riprodotta:</span><span class="sxs-lookup"><span data-stu-id="b387a-400">If Fail() is called, hello failed tuple will be replayed:</span></span>

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

### <a name="helloworldtx"></a><span data-ttu-id="b387a-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="b387a-401">HelloWorldTx</span></span>
<span data-ttu-id="b387a-402">Hello **HelloWorldTx** nell'esempio viene illustrato come tooimplement transazionale topologia.</span><span class="sxs-lookup"><span data-stu-id="b387a-402">hello **HelloWorldTx** example demonstrates how tooimplement transactional topology.</span></span> <span data-ttu-id="b387a-403">Contiene uno spout denominato **generator**, un bolt batch denominato **partial-count** e un bolt di commit denominato **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="b387a-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="b387a-404">Sono presenti anche tre file txt già creati: **DataSource0.txt**, **DataSource1.txt** e **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="b387a-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="b387a-405">In ogni transazione, hello beccuccio **generatore** verrà selezionare due file hello tre file creato in precedenza in modo casuale e generare hello due file nomi toohello **conteggio parziale** fulmine.</span><span class="sxs-lookup"><span data-stu-id="b387a-405">In each transaction, hello spout **generator** will randomly choose two files from hello pre-created three files, and emit hello two file names toohello **partial-count** bolt.</span></span> <span data-ttu-id="b387a-406">fulmine Hello **conteggio parziale** verrà innanzitutto ottenere il nome di file hello dalla tupla hello ricevuto, hello Apri file e conteggio hello il numero di parole in questo file e infine creare hello word numero toohello **conteggio, somma**fulmine.</span><span class="sxs-lookup"><span data-stu-id="b387a-406">hello bolt **partial-count** will first get hello file name from hello received tuple, then open hello file and count hello number of words in this file, and finally emit hello word number toohello **count-sum** bolt.</span></span> <span data-ttu-id="b387a-407">Hello **conteggio somma** fulmine riepiloga il numero totale di hello.</span><span class="sxs-lookup"><span data-stu-id="b387a-407">hello **count-sum** bolt will summarize hello total count.</span></span>

<span data-ttu-id="b387a-408">tooachieve **esattamente una volta** semantica, fulmine commit hello **conteggio somma** toojudge è necessario se si tratta di una transazione di riproduzione.</span><span class="sxs-lookup"><span data-stu-id="b387a-408">tooachieve **exactly once** semantics, hello commit bolt **count-sum** need toojudge whether it is a replayed transaction.</span></span> <span data-ttu-id="b387a-409">In questo esempio, contiene una variabile membro statica:</span><span class="sxs-lookup"><span data-stu-id="b387a-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="b387a-410">Quando viene creata un'istanza di ISCPBatchBolt, otterrà hello `txAttempt` da parametri di input:</span><span class="sxs-lookup"><span data-stu-id="b387a-410">When an ISCPBatchBolt instance is created, it will get hello `txAttempt` from input parameters:</span></span>

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

<span data-ttu-id="b387a-411">Quando `FinishBatch()` viene chiamato, hello `lastCommittedTxId` sarà update se non è una transazione di riproduzione.</span><span class="sxs-lookup"><span data-stu-id="b387a-411">When `FinishBatch()` is called, hello `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

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


### <a name="hybridtopology"></a><span data-ttu-id="b387a-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="b387a-412">HybridTopology</span></span>
<span data-ttu-id="b387a-413">Questa topologia contiene uno spout Java e un bolt C\#.</span><span class="sxs-lookup"><span data-stu-id="b387a-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="b387a-414">Usa hello la serializzazione e deserializzazione l'implementazione predefinita fornita dalla piattaforma SCP.</span><span class="sxs-lookup"><span data-stu-id="b387a-414">It uses hello default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="b387a-415">Eseguire hello ref **HybridTopology.spec** in **esempi\\HybridTopology** cartella hello specifica dettagli dei file, e **SubmitTopology.bat** per informazioni su come classpath Java toospecify.</span><span class="sxs-lookup"><span data-stu-id="b387a-415">Please ref hello **HybridTopology.spec** in **examples\\HybridTopology** folder for hello spec file details, and **SubmitTopology.bat** for how toospecify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="b387a-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="b387a-416">SCPHostDemo</span></span>
<span data-ttu-id="b387a-417">In pratica, questo esempio è hello come HelloWorld.</span><span class="sxs-lookup"><span data-stu-id="b387a-417">This example is hello same as HelloWorld in essence.</span></span> <span data-ttu-id="b387a-418">Hello unica differenza è che il codice utente hello viene compilato come DLL e topologia hello viene inviata tramite SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="b387a-418">hello only difference is that hello user code is compiled as DLL and hello topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="b387a-419">Fare riferimento hello sezione "SCP Host alla modalità" per informazioni più dettagliate.</span><span class="sxs-lookup"><span data-stu-id="b387a-419">Please ref hello section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b387a-420">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b387a-420">Next Steps</span></span>
<span data-ttu-id="b387a-421">Per esempi di topologie di Storm create utilizzando SCP, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="b387a-421">For examples of Storm topologies created using SCP, see hello following:</span></span>

* [<span data-ttu-id="b387a-422">Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b387a-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="b387a-423">Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b387a-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="b387a-424">Creare più flussi di dati in una topologia Storm C#</span><span class="sxs-lookup"><span data-stu-id="b387a-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="b387a-425">Utilizzare i dati di Power Bi toovisualize da una topologia di Storm</span><span class="sxs-lookup"><span data-stu-id="b387a-425">Use Power Bi toovisualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="b387a-426">Elaborare i dati del sensore veicolo dall'hub di eventi usando Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b387a-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="b387a-427">Estrazione, trasformazione e caricamento (ETL) da tooHBase hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="b387a-427">Extract, Transform, and Load (ETL) from Azure Event Hubs tooHBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="b387a-428">Correlare gli eventi  con Storm e HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b387a-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

