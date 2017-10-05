---
title: Guida alla programmazione SCP.NET | Documentazione Microsoft
description: "Informazioni su come utilizzare SCP.NET per creare topologie Storm basate su .NET per l’utilizzo con Storm in HDInsight."
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
ms.openlocfilehash: 3d76aebd2a1fd729c8e0639e6afcbde4c3fb752b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="c1f54-103">Guida alla programmazione SCP</span><span class="sxs-lookup"><span data-stu-id="c1f54-103">SCP programming guide</span></span>
<span data-ttu-id="c1f54-104">SCP è una piattaforma per la compilazione di applicazioni di elaborazione dati dalle prestazioni elevate, affidabili, coerenti e in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-104">SCP is a platform to build real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="c1f54-105">È basata su [Apache Storm](http://storm.incubator.apache.org/) , un sistema di elaborazione dei flussi progettato dalle community di sviluppo di software open source (OSS).</span><span class="sxs-lookup"><span data-stu-id="c1f54-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by the OSS communities.</span></span> <span data-ttu-id="c1f54-106">Storm è stato progettato da Nathan Marz e reso open source da Twitter.</span><span class="sxs-lookup"><span data-stu-id="c1f54-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="c1f54-107">Il sistema si avvale di [Apache Zookeeper](http://zookeeper.apache.org/), un altro progetto Apache per il coordinamento e la gestione dello stato altamente affidabili delle applicazioni distribuite.</span><span class="sxs-lookup"><span data-stu-id="c1f54-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project to enable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="c1f54-108">Il progetto SCP ha reso portabile in Windows non solo Storm, ma anche le estensioni e le personalizzazioni aggiunte per l'ecosistema Windows.</span><span class="sxs-lookup"><span data-stu-id="c1f54-108">Not only the SCP project ported Storm on Windows but also the project added extensions and customization for the Windows ecosystem.</span></span> <span data-ttu-id="c1f54-109">Le estensioni includono l'esperienza di sviluppatore .NET e le relative librerie. Le personalizzazioni includono lo sviluppo basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="c1f54-109">The extensions include .NET developer experience, and libraries, the customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="c1f54-110">Le estensioni e le personalizzazioni sono compilate in modo tale che non sono necessari fork dei progetti OSS ed è possibile usare ecosistemi derivati basati su Storm.</span><span class="sxs-lookup"><span data-stu-id="c1f54-110">The extension and customization is done in such a way that we do not need to fork the OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="c1f54-111">Modello di elaborazione</span><span class="sxs-lookup"><span data-stu-id="c1f54-111">Processing model</span></span>
<span data-ttu-id="c1f54-112">In dati in SCP vengono modellati come flussi continui di tuple.</span><span class="sxs-lookup"><span data-stu-id="c1f54-112">The data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="c1f54-113">In genere le tuple vengono inviate a una coda, quindi prelevate e trasformate dalla logica di business ospitata in una topologia Storm. Infine, è possibile inoltrare l'output tramite pipe sotto forma di tuple o eseguirne il commit in archivi, come il file system distribuito, o database, come SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c1f54-113">Typically the tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally the output could be piped as tuples to another SCP system, or be committed to stores like distributed file system or databases like SQL Server.</span></span>

![Diagramma di una coda che invia dati all'elaborazione, che a sua volta li invia a un archivio dati](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="c1f54-115">In Storm, una topologia applicazione definisce un grafo di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="c1f54-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="c1f54-116">Ogni nodo in una topologia contiene logica di elaborazione e i collegamenti tra i nodi indicano il flusso dei dati.</span><span class="sxs-lookup"><span data-stu-id="c1f54-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="c1f54-117">I nodi per l'inserimento dei dati di input nella topologia sono denominati Spout e possono essere usati per porre in sequenza i dati.</span><span class="sxs-lookup"><span data-stu-id="c1f54-117">The nodes to inject input data into the topology are called Spouts, which can be used to sequence the data.</span></span> <span data-ttu-id="c1f54-118">I dati di input possono risiedere in log di file, database transazionali, contatore delle prestazioni del sistema e così via. I nodi con entrambi i flussi di dati di input e output sono denominati Bolt ed eseguono il filtraggio, la selezione e l’aggregazione dei dati effettivi.</span><span class="sxs-lookup"><span data-stu-id="c1f54-118">The input data could reside in file logs, transactional database, system performance counter etc. The nodes with both input and output data flows are called Bolts, which do the actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="c1f54-119">SCP supporta l'elaborazione dati di tipo best effort, at-least-once ed exactly-once.</span><span class="sxs-lookup"><span data-stu-id="c1f54-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="c1f54-120">In un'applicazione di elaborazione di streaming distribuita, possono verificarsi diversi errori durante l'elaborazione di dati, ad esempio un'interruzione di rete, un errore del computer o del codice utente e così via. L'elaborazione at-least-once assicura che tutti i dati vengano elaborati almeno una volta, riproducendo automaticamente gli stessi dati in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="c1f54-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically the same data when error happens.</span></span> <span data-ttu-id="c1f54-121">L'elaborazione at-least-once è semplice e affidabile e offre risultati positivi in molte applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c1f54-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="c1f54-122">In alcuni casi tuttavia, ad esempio quando l'applicazione richiede il conteggio esatto, l'elaborazione at-least-once è insufficiente, perché potenzialmente nella topologia dell'applicazione potrebbero essere riprodotti gli stessi dati.</span><span class="sxs-lookup"><span data-stu-id="c1f54-122">However, when the application requires exact counting, for example, at-least-once processing is insufficient since the same data could potentially be played in the application topology.</span></span> <span data-ttu-id="c1f54-123">In questi casi si può usare l'elaborazione exactly-once, progettata per garantire che i risultati siano corretti anche se è possibile che i dati vengano riprodotti ed elaborati più volte.</span><span class="sxs-lookup"><span data-stu-id="c1f54-123">In that case, exactly-once processing is designed to make sure the result is correct even when the data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="c1f54-124">SCP consente agli sviluppatori .NET di sviluppare applicazioni di elaborazione dati in tempo reale usando in modo invisibile Storm in una JVM (Java Virtual Machine).</span><span class="sxs-lookup"><span data-stu-id="c1f54-124">SCP enables .NET developers to develop real time data process applications while leverage the Java Virtual Machine (JVM) based Storm under the cover.</span></span> <span data-ttu-id="c1f54-125">.NET e la JVM comunicano tramite un socket locale TCP.</span><span class="sxs-lookup"><span data-stu-id="c1f54-125">The .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="c1f54-126">Essenzialmente, ogni Spout/Bolt è una coppia di processi .Net/Java, in cui la logica utente viene eseguita nel processo .Net come plug-in.</span><span class="sxs-lookup"><span data-stu-id="c1f54-126">Basically each Spout/Bolt is a .Net/Java process pair, where the user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="c1f54-127">Per compilare un'applicazione di elaborazione dati in SCP sono necessari diversi passaggi:</span><span class="sxs-lookup"><span data-stu-id="c1f54-127">To build a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="c1f54-128">Progettare e implementare gli Spout per l'inserimento dei dati provenienti dalla coda.</span><span class="sxs-lookup"><span data-stu-id="c1f54-128">Design and implement the Spouts to pull in data from queue.</span></span>
* <span data-ttu-id="c1f54-129">Progettare e implementare Bolt per l'elaborazione dei dati di input e il salvataggio dei dati in archivi esterni, ad esempio database.</span><span class="sxs-lookup"><span data-stu-id="c1f54-129">Design and implement Bolts to process the input data, and save data to external stores such as Database.</span></span>
* <span data-ttu-id="c1f54-130">Progettare la topologia, quindi inviarla ed eseguirla.</span><span class="sxs-lookup"><span data-stu-id="c1f54-130">Design the topology, then submit and run the topology.</span></span> <span data-ttu-id="c1f54-131">La topologia definisce i vertici e i flussi di dati tra i vertici.</span><span class="sxs-lookup"><span data-stu-id="c1f54-131">The topology defines vertexes and the data flows between the vertexes.</span></span> <span data-ttu-id="c1f54-132">SCP recupererà le specifiche della topologia e le implementerà in un cluster Storm, in cui ogni vertice viene eseguito in un nodo logico.</span><span class="sxs-lookup"><span data-stu-id="c1f54-132">SCP will take the topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="c1f54-133">Il failover e la scalabilità saranno gestiti dall'utilità di pianificazione di Storm.</span><span class="sxs-lookup"><span data-stu-id="c1f54-133">The failover and scaling will be taken care of by the Storm task scheduler.</span></span>

<span data-ttu-id="c1f54-134">In questo documento verranno usati alcuni semplici esempi per illustrare in dettaglio come compilare un'applicazione di elaborazione dati con SCP.</span><span class="sxs-lookup"><span data-stu-id="c1f54-134">This document will use some simple examples to walk through how to build data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="c1f54-135">Interfaccia del plug-in SCP</span><span class="sxs-lookup"><span data-stu-id="c1f54-135">SCP Plugin Interface</span></span>
<span data-ttu-id="c1f54-136">I plug-in SCP (o applicazioni) sono file eseguibili autonomi che possono essere eseguiti in Visual Studio nella fase di sviluppo e anche collegati alla pipeline di Storm dopo la distribuzione in produzione.</span><span class="sxs-lookup"><span data-stu-id="c1f54-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during the development phase, and be plugged into the Storm pipeline after deployment in production.</span></span> <span data-ttu-id="c1f54-137">Scrivere il plug-in SCP è come scrivere qualsiasi altra applicazione console Windows standard.</span><span class="sxs-lookup"><span data-stu-id="c1f54-137">Writing the SCP plugin is just the same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="c1f54-138">La piattaforma SCP.NET dichiara le interfacce per gli Spout e i Bolt e il codice del plug-in utente dovrebbe implementare tali interfacce.</span><span class="sxs-lookup"><span data-stu-id="c1f54-138">SCP.NET platform declares some interface for spout/bolt, and the user plugin code should implement these interfaces.</span></span> <span data-ttu-id="c1f54-139">Lo scopo principale di questo progetto è fare in modo che l'utente possa concentrarsi sulla propria logica di business, lasciando il resto della gestione alla piattaforma SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="c1f54-139">The main purpose of this design is that the user can focus on their own business logics, and leaving other things to be handled by SCP.NET platform.</span></span>

<span data-ttu-id="c1f54-140">Il codice del plug-in utente deve implementare una delle interfacce seguenti in base al tipo di topologia (transazionale o non transazionale) e al tipo di componente (Spout o Bolt).</span><span class="sxs-lookup"><span data-stu-id="c1f54-140">The user plugin code should implement one of the followings interfaces, depends on whether the topology is transactional or non-transactional, and whether the component is spout or bolt.</span></span>

* <span data-ttu-id="c1f54-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="c1f54-141">ISCPSpout</span></span>
* <span data-ttu-id="c1f54-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="c1f54-142">ISCPBolt</span></span>
* <span data-ttu-id="c1f54-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="c1f54-143">ISCPTxSpout</span></span>
* <span data-ttu-id="c1f54-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="c1f54-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="c1f54-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="c1f54-145">ISCPPlugin</span></span>
<span data-ttu-id="c1f54-146">ISCPPlugin è l'interfaccia comune per tutti i tipi di plug-in.</span><span class="sxs-lookup"><span data-stu-id="c1f54-146">ISCPPlugin is the common interface for all kinds of plugins.</span></span> <span data-ttu-id="c1f54-147">Attualmente è un'interfaccia fittizia.</span><span class="sxs-lookup"><span data-stu-id="c1f54-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="c1f54-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="c1f54-148">ISCPSpout</span></span>
<span data-ttu-id="c1f54-149">ISCPSpout è l'interfaccia per lo Spout non transazionale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-149">ISCPSpout is the interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="c1f54-150">Quando viene chiamato `NextTuple()`, il codice utente C\# può emettere una o più tuple.</span><span class="sxs-lookup"><span data-stu-id="c1f54-150">When `NextTuple()` is called, the C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="c1f54-151">Se non ci sono tuple da emettere, il metodo deve essere restituito senza emettere alcunché.</span><span class="sxs-lookup"><span data-stu-id="c1f54-151">If there is nothing to emit, this method should return without emitting anything.</span></span> <span data-ttu-id="c1f54-152">Si noti che `NextTuple()`, `Ack()` e `Fail()` vengono chiamati in un ciclo ridotto in un singolo thread nel processo C\#.</span><span class="sxs-lookup"><span data-stu-id="c1f54-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="c1f54-153">Quando non ci sono tuple da emettere, è utile una breve sospensione del metodo NextTuple (ad esempio 10 millisecondi), in modo da limitare il consumo di CPU.</span><span class="sxs-lookup"><span data-stu-id="c1f54-153">When there are no tuples to emit, it is courteous to have NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="c1f54-154">`Ack()` e `Fail()` verranno chiamati solo se il meccanismo di acknowledgement è abilitato nel file delle specifiche.</span><span class="sxs-lookup"><span data-stu-id="c1f54-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="c1f54-155">`seqId` identifica la tupla confermata o non confermata.</span><span class="sxs-lookup"><span data-stu-id="c1f54-155">The `seqId` is used to identify the tuple which is acked or failed.</span></span> <span data-ttu-id="c1f54-156">Dunque, se l'acknowledgement è abilitato in una topologia non transazionale, nello Spout deve essere usata la funzione di emissione seguente:</span><span class="sxs-lookup"><span data-stu-id="c1f54-156">So if ack is enabled in non-transactional topology, the following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="c1f54-157">Se l'acknowledgment non è supportato in una topologia non transazionale, `Ack()` e `Fail()` possono essere lasciati come funzione vuota.</span><span class="sxs-lookup"><span data-stu-id="c1f54-157">If ack is not supported in non-transactional topology, the `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="c1f54-158">I parametri di input `parms` in queste funzioni sono semplicemente un dizionario vuoto e sono riservati per l'utilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="c1f54-158">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="c1f54-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="c1f54-159">ISCPBolt</span></span>
<span data-ttu-id="c1f54-160">ISCPBolt è l'interfaccia per il Bolt non transazionale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-160">ISCPBolt is the interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="c1f54-161">Quando sarà disponibile una nuova tupla, verrà chiamata la funzione `Execute()` per elaborarla.</span><span class="sxs-lookup"><span data-stu-id="c1f54-161">When new tuple is available, the `Execute()` function will be called to process it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="c1f54-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="c1f54-162">ISCPTxSpout</span></span>
<span data-ttu-id="c1f54-163">ISCPTxSpout è l'interfaccia per lo Spout transazionale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-163">ISCPTxSpout is the interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="c1f54-164">Come avviene per la controparte non transazionale, `NextTx()`, `Ack()` e `Fail()` vengono chiamati in un ciclo ridotto in un singolo thread nel processo C\#.</span><span class="sxs-lookup"><span data-stu-id="c1f54-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="c1f54-165">Quando non ci sono dati da emettere, è utile una breve sospensione del metodo `NextTx` (ad esempio 10 millisecondi), in modo da limitare il consumo di CPU.</span><span class="sxs-lookup"><span data-stu-id="c1f54-165">When there are no data to emit, it is courteous to have `NextTx` sleep for a short amount of time (10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="c1f54-166">`NextTx()` viene chiamato per avviare una nuova transazione. Il parametro di output `seqId`, usato per identificare la transazione, viene usato anche in `Ack()` e `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="c1f54-166">`NextTx()` is called to start a new transaction, the out parameter `seqId` is used to identify the transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="c1f54-167">In `NextTx()`, l'utente può emettere dati verso il lato Java.</span><span class="sxs-lookup"><span data-stu-id="c1f54-167">In `NextTx()`, user can emit data to Java side.</span></span> <span data-ttu-id="c1f54-168">I dati verranno archiviati in ZooKeeper per supportare la riproduzione.</span><span class="sxs-lookup"><span data-stu-id="c1f54-168">The data will be stored in ZooKeeper to support replay.</span></span> <span data-ttu-id="c1f54-169">Poiché la capacità di ZooKeeper è molto limitata, nello Spout transazionale l'utente deve emettere solo metadati e non dati in blocco.</span><span class="sxs-lookup"><span data-stu-id="c1f54-169">Because the capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="c1f54-170">Storm riprodurrà automaticamente una transazione in caso di errore, dunque in un caso normale `Fail()` non dovrebbe essere chiamato.</span><span class="sxs-lookup"><span data-stu-id="c1f54-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="c1f54-171">Se SCP può verificare i metadati emessi dallo Spout transazionale, tuttavia, può chiamare `Fail()` quando i metadati non sono validi.</span><span class="sxs-lookup"><span data-stu-id="c1f54-171">But if SCP can check the metadata emitted by transactional spout, it can call `Fail()` when the metadata is invalid.</span></span>

<span data-ttu-id="c1f54-172">I parametri di input `parms` in queste funzioni sono semplicemente un dizionario vuoto e sono riservati per l'utilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="c1f54-172">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="c1f54-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="c1f54-173">ISCPBatchBolt</span></span>
<span data-ttu-id="c1f54-174">ISCPBatchBolt è l'interfaccia per il Bolt transazionale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-174">ISCPBatchBolt is the interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="c1f54-175">`Execute()` viene chiamato quando al Bolt arriva una nuova tupla.</span><span class="sxs-lookup"><span data-stu-id="c1f54-175">`Execute()` is called when there is new tuple arriving at the bolt.</span></span> <span data-ttu-id="c1f54-176">`FinishBatch()` viene chiamato al termine di questa transazione.</span><span class="sxs-lookup"><span data-stu-id="c1f54-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="c1f54-177">Il parametro di output `parms` è riservato per l'utilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="c1f54-177">The `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="c1f54-178">Per la topologia transazionale esiste un concetto importante, `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="c1f54-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="c1f54-179">Ha due campi, `TxId` e `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="c1f54-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="c1f54-180">`TxId` viene usato per identificare una specifica transazione e per una data transazione possono essere eseguiti più tentativi in caso di errore e riproduzione della transazione.</span><span class="sxs-lookup"><span data-stu-id="c1f54-180">`TxId` is used to identify a specific transaction, and for a given transaction, there may be multiple attempt if the transaction fails and is replayed.</span></span> <span data-ttu-id="c1f54-181">SCP.NET creerà un nuovo oggetto ISCPBatchBolt diverso per elaborare ogni `StormTxAttempt`, la stessa operazione eseguita da Storm sul lato Java.</span><span class="sxs-lookup"><span data-stu-id="c1f54-181">SCP.NET will new a different ISCPBatchBolt object to process each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="c1f54-182">Lo scopo di questo progetto è supportare l'elaborazione di transazioni parallele.</span><span class="sxs-lookup"><span data-stu-id="c1f54-182">The purpose of this design is to support parallel transactions processing.</span></span> <span data-ttu-id="c1f54-183">Tenere a mente che, se il tentativo di transazione viene completato, l'oggetto ISCPBatchBolt corrispondente verrà distrutto e sottoposto a un'operazione di Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="c1f54-183">User should keep it in mind that if transaction attempt is finished, the corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="c1f54-184">Modello a oggetti</span><span class="sxs-lookup"><span data-stu-id="c1f54-184">Object Model</span></span>
<span data-ttu-id="c1f54-185">In SCP.NET è disponibile un semplice set di oggetti chiave che gli sviluppatori possono usare per la programmazione.</span><span class="sxs-lookup"><span data-stu-id="c1f54-185">SCP.NET also provides a simple set of key objects for developers to program with.</span></span> <span data-ttu-id="c1f54-186">Si tratta degli oggetti **Context**, **StateStore** e **SCPRuntime**,</span><span class="sxs-lookup"><span data-stu-id="c1f54-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="c1f54-187">che verranno illustrati nella parte rimanente di questa sezione.</span><span class="sxs-lookup"><span data-stu-id="c1f54-187">They will be discussed in the rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="c1f54-188">Context</span><span class="sxs-lookup"><span data-stu-id="c1f54-188">Context</span></span>
<span data-ttu-id="c1f54-189">Context fornisce un ambiente di esecuzione per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c1f54-189">Context provides a running environment to the application.</span></span> <span data-ttu-id="c1f54-190">Ogni istanza di ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) dispone di un'istanza Context corrispondente.</span><span class="sxs-lookup"><span data-stu-id="c1f54-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="c1f54-191">Le funzionalità fornite da Context possono essere suddivise in due parti: (1) la parte statica, disponibile nell'intero processo C\#, (2) la parte dinamica, disponibile solo per la specifica istanza Context.</span><span class="sxs-lookup"><span data-stu-id="c1f54-191">The functionality provided by Context can be divided into two parts: (1) the static part which is available in the whole C\# process, (2) the dynamic part which is only available for the specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="c1f54-192">Parte statica</span><span class="sxs-lookup"><span data-stu-id="c1f54-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="c1f54-193">`Logger` è fornito a scopi di log.</span><span class="sxs-lookup"><span data-stu-id="c1f54-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="c1f54-194">`pluginType` viene usato per indicare il tipo di plug-in del processo C\#.</span><span class="sxs-lookup"><span data-stu-id="c1f54-194">`pluginType` is used to indicate the plugin type of the C\# process.</span></span> <span data-ttu-id="c1f54-195">Se il processo C\# viene eseguito in modalità di test locale (senza Java), il tipo di plug-in è `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="c1f54-195">If the C\# process is run in local test mode (without Java), the plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="c1f54-196">`Config` consente di ottenere i parametri di configurazione dal lato Java.</span><span class="sxs-lookup"><span data-stu-id="c1f54-196">`Config` is provided to get configuration parameters from Java side.</span></span> <span data-ttu-id="c1f54-197">I parametri vengono passati dal lato Java al momento dell'inizializzazione del plug-in C\#.</span><span class="sxs-lookup"><span data-stu-id="c1f54-197">The parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="c1f54-198">I parametri `Config` sono divisi in due parti: `stormConf` e `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="c1f54-198">The `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="c1f54-199">`stormConf` corrisponde ai parametri definiti da Storm e `pluginConf` ai parametri definiti da SCP.</span><span class="sxs-lookup"><span data-stu-id="c1f54-199">`stormConf` is parameters defined by Storm and `pluginConf` is the parameters defined by SCP.</span></span> <span data-ttu-id="c1f54-200">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c1f54-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="c1f54-201">`TopologyContext` consente di ottenere il contesto della topologia ed è particolarmente utile per i componenti con più operatori di parallelismo.</span><span class="sxs-lookup"><span data-stu-id="c1f54-201">`TopologyContext` is provided to get the topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="c1f54-202">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="c1f54-202">Here is an example:</span></span>

    //demo how to get TopologyContext info
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

### <a name="dynamic-part"></a><span data-ttu-id="c1f54-203">Parte dinamica</span><span class="sxs-lookup"><span data-stu-id="c1f54-203">Dynamic Part</span></span>
<span data-ttu-id="c1f54-204">Le interfacce seguenti sono pertinenti a una specifica istanza di Context.</span><span class="sxs-lookup"><span data-stu-id="c1f54-204">The following interfaces are pertinent to a certain Context instance.</span></span> <span data-ttu-id="c1f54-205">L'istanza di Context viene creata dalla piattaforma SCP.NET e passata al codice utente:</span><span class="sxs-lookup"><span data-stu-id="c1f54-205">The Context instance is created by SCP.NET platform and passed to the user code:</span></span>

    // Declare the Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple to default stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple to the specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="c1f54-206">Per lo Spout non transazionale che supporta l'acknowledgement, viene fornito il metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="c1f54-206">For non-transactional spout supporting ack, the following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="c1f54-207">Per il Bolt non transazionale che supporta l'acknowledgement, deve indicare esplicitamente `Ack()` o `Fail()` per la tupla ricevuta.</span><span class="sxs-lookup"><span data-stu-id="c1f54-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` the tuple it received.</span></span> <span data-ttu-id="c1f54-208">Quando viene emessa una nuova tupla, deve inoltre specificarne gli ancoraggi.</span><span class="sxs-lookup"><span data-stu-id="c1f54-208">And when emitting new tuple, it must also specify the anchors of the new tuple.</span></span> <span data-ttu-id="c1f54-209">Sono forniti i metodi seguenti.</span><span class="sxs-lookup"><span data-stu-id="c1f54-209">The following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="c1f54-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="c1f54-210">StateStore</span></span>
<span data-ttu-id="c1f54-211">`StateStore` fornisce servizi metadati, generazione di sequenze monotone e coordinamento senza attesa.</span><span class="sxs-lookup"><span data-stu-id="c1f54-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="c1f54-212">`StateStore`consente di creare astrazioni di concorrenza distribuite di livello superiore, tra cui blocchi distribuiti, code distribuite e servizi di transazione.</span><span class="sxs-lookup"><span data-stu-id="c1f54-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="c1f54-213">Le applicazioni SCP possono usare l'oggetto `State` per rendere persistenti alcune informazioni in ZooKeeper, in particolare per la topologia transazionale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-213">SCP applications may use the `State` object to persist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="c1f54-214">In questo modo, in caso di arresto anomalo e riavvio dello Spout, è possibile recuperare le informazioni necessarie da ZooKeeper e riavviare la pipeline.</span><span class="sxs-lookup"><span data-stu-id="c1f54-214">Doing so, if transactional spout crashes and restart, it can retrieve the necessary information from ZooKeeper and restart the pipeline.</span></span>

<span data-ttu-id="c1f54-215">L'oggetto `StateStore` fornisce principalmente i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c1f54-215">The `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method to retrieve a state store of the given path and connStr 
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
    /// Get all the States in the StateStore
    /// </summary>
    /// <returns>All the States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all the committed states
    /// </summary>
    /// <returns>Registries contain the Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all the Aborted State in the StateStore
    /// </summary>
    /// <returns>Registries contain the Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of the State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="c1f54-216">L'oggetto `State` fornisce principalmente i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c1f54-216">The `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set the status of the state object to commit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set the status of the state object to abort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under the give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get the attribute value associated with the given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="c1f54-217">Per il metodo `Commit()` , quando simpleMode è impostato su true verrà semplicemente eliminato il ZNode corrispondente in ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="c1f54-217">For the `Commit()` method, when simpleMode is set to true, it will simply delete the corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="c1f54-218">In caso contrario, l'elemento ZNode corrente verrà eliminato e verrà aggiunto un nuovo nodo in COMMITTED\_PATH.</span><span class="sxs-lookup"><span data-stu-id="c1f54-218">Otherwise, it will delete the current ZNode, and adding a new node in the COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="c1f54-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="c1f54-219">SCPRuntime</span></span>
<span data-ttu-id="c1f54-220">SCPRuntime fornisce i due metodi seguenti.</span><span class="sxs-lookup"><span data-stu-id="c1f54-220">SCPRuntime provides the following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="c1f54-221">`Initialize()` viene usato per inizializzare l'ambiente di runtime SCP.</span><span class="sxs-lookup"><span data-stu-id="c1f54-221">`Initialize()` is used to initialize the SCP runtime environment.</span></span> <span data-ttu-id="c1f54-222">In questo metodo, il processo C\# si connette al lato Java per ottenere i parametri di configurazione e il contesto della topologia.</span><span class="sxs-lookup"><span data-stu-id="c1f54-222">In this method, the C\# process will connect to the Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="c1f54-223">`LaunchPlugin()` viene usato per avviare il ciclo di elaborazione dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="c1f54-223">`LaunchPlugin()` is used to kick off the message processing loop.</span></span> <span data-ttu-id="c1f54-224">In questo ciclo il plug-in C\# riceve messaggi dal lato Java (incluse tuple e segnali di controllo) e quindi li elabora, probabilmente chiamando il metodo di interfaccia fornito dal codice utente.</span><span class="sxs-lookup"><span data-stu-id="c1f54-224">In this loop, the C\# plugin will receive messages form Java side (including tuples and control signals), and then process the messages, perhaps calling the interface method provide by the user code.</span></span> <span data-ttu-id="c1f54-225">Il parametro di input per il metodo `LaunchPlugin()` è un delegato che può restituire un oggetto che implementa l'interfaccia ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.</span><span class="sxs-lookup"><span data-stu-id="c1f54-225">The input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="c1f54-226">Per ISCPBatchBolt, è possibile ottenere `StormTxAttempt` da `parms` e usarlo per verificare se si tratta di un tentativo riprodotto.</span><span class="sxs-lookup"><span data-stu-id="c1f54-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it to judge whether it is a replayed attempt.</span></span> <span data-ttu-id="c1f54-227">Questa operazione viene in genere eseguita nel Bolt di commit ed è dimostrata nell'esempio `HelloWorldTx` .</span><span class="sxs-lookup"><span data-stu-id="c1f54-227">This is usually done at the commit bolt, and it is demonstrated in the `HelloWorldTx` example.</span></span>

<span data-ttu-id="c1f54-228">In generale, i plug-in SCP possono essere eseguiti in due modalità:</span><span class="sxs-lookup"><span data-stu-id="c1f54-228">Generally speaking, the SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="c1f54-229">Modalità test locale: in questa modalità i plug-in SCP (il codice utente C\#) vengono eseguiti in Visual Studio durante la fase di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="c1f54-229">Local Test Mode: In this mode, the SCP plugins (the C\# user code) run inside Visual Studio during the development phase.</span></span> <span data-ttu-id="c1f54-230">`LocalContext` , che fornisce metodi per serializzare le tuple emesse in file locali e rileggerle nella memoria.</span><span class="sxs-lookup"><span data-stu-id="c1f54-230">`LocalContext` can be used in this mode, which provides method to serialize the emitted tuples to local files, and read them back to memory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="c1f54-231">Modalità normale: in questa modalità, i plug-in SCP vengono avviati dal processo Java Storm.</span><span class="sxs-lookup"><span data-stu-id="c1f54-231">Regular Mode: In this mode, the SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="c1f54-232">Di seguito è riportato un esempio di avvio del plug-in SCP:</span><span class="sxs-lookup"><span data-stu-id="c1f54-232">Here is an example of launching SCP plugin:</span></span>
   
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
            /* Setting the environment variable here can change the log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="c1f54-233">Linguaggio di specifica della topologia</span><span class="sxs-lookup"><span data-stu-id="c1f54-233">Topology Specification Language</span></span>
<span data-ttu-id="c1f54-234">SCP Topology Specification è un linguaggio specifico di dominio (DSL) per la descrizione e la configurazione di topologie SCP.</span><span class="sxs-lookup"><span data-stu-id="c1f54-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="c1f54-235">È basato sul DSL di Storm in linguaggio Clojure (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) ed esteso da SCP.</span><span class="sxs-lookup"><span data-stu-id="c1f54-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="c1f54-236">Le specifiche della topologia possono essere inviate direttamente al cluster Storm per l'esecuzione mediante il comando ***runspec***.</span><span class="sxs-lookup"><span data-stu-id="c1f54-236">Topology specifications can be submitted directly to storm cluster for execution via the ***runspec*** command.</span></span>

<span data-ttu-id="c1f54-237">SCP.NET ha aggiunto le funzioni seguenti per la definizione della topologia transazionale:</span><span class="sxs-lookup"><span data-stu-id="c1f54-237">SCP.NET has add follow functions to define the Transactional Topology:</span></span>

| <span data-ttu-id="c1f54-238">**Nuove funzioni**</span><span class="sxs-lookup"><span data-stu-id="c1f54-238">**New Functions**</span></span> | <span data-ttu-id="c1f54-239">**Parametri**</span><span class="sxs-lookup"><span data-stu-id="c1f54-239">**Parameters**</span></span> | <span data-ttu-id="c1f54-240">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="c1f54-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c1f54-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="c1f54-241">**tx-topolopy**</span></span> |<span data-ttu-id="c1f54-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="c1f54-242">topology-name</span></span><br /><span data-ttu-id="c1f54-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="c1f54-243">spout-map</span></span><br /><span data-ttu-id="c1f54-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="c1f54-244">bolt-map</span></span> |<span data-ttu-id="c1f54-245">Consente di definire una topologia transazionale con il nome della topologia,&nbsp;la mappa di definizione degli spout e la mappa di definizione dei bolt.</span><span class="sxs-lookup"><span data-stu-id="c1f54-245">Define a transactional topology with the topology name, &nbsp;spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="c1f54-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="c1f54-246">**scp-tx-spout**</span></span> |<span data-ttu-id="c1f54-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="c1f54-247">exec-name</span></span><br /><span data-ttu-id="c1f54-248">args</span><span class="sxs-lookup"><span data-stu-id="c1f54-248">args</span></span><br /><span data-ttu-id="c1f54-249">fields</span><span class="sxs-lookup"><span data-stu-id="c1f54-249">fields</span></span> |<span data-ttu-id="c1f54-250">Consente di definire uno Spout transazionale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-250">Define a transactional spout.</span></span> <span data-ttu-id="c1f54-251">Eseguirà l'applicazione con ***exec-name*** usando ***args***.</span><span class="sxs-lookup"><span data-stu-id="c1f54-251">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="c1f54-252">***fields*** corrisponde ai campi di output per lo Spout.</span><span class="sxs-lookup"><span data-stu-id="c1f54-252">The ***fields*** is the Output Fields for spout</span></span> |
| <span data-ttu-id="c1f54-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="c1f54-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="c1f54-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="c1f54-254">exec-name</span></span><br /><span data-ttu-id="c1f54-255">args</span><span class="sxs-lookup"><span data-stu-id="c1f54-255">args</span></span><br /><span data-ttu-id="c1f54-256">fields</span><span class="sxs-lookup"><span data-stu-id="c1f54-256">fields</span></span> |<span data-ttu-id="c1f54-257">Consente di definire un Bolt batch transazionale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="c1f54-258">Eseguirà l'applicazione con ***exec-name*** usando ***args***.</span><span class="sxs-lookup"><span data-stu-id="c1f54-258">It will run the application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="c1f54-259">Il parametro Fields corrisponde ai campi di output per il Bolt.</span><span class="sxs-lookup"><span data-stu-id="c1f54-259">The Fields is the Output Fields for bolt.</span></span> |
| <span data-ttu-id="c1f54-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="c1f54-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="c1f54-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="c1f54-261">exec-name</span></span><br /><span data-ttu-id="c1f54-262">args</span><span class="sxs-lookup"><span data-stu-id="c1f54-262">args</span></span><br /><span data-ttu-id="c1f54-263">fields</span><span class="sxs-lookup"><span data-stu-id="c1f54-263">fields</span></span> |<span data-ttu-id="c1f54-264">Consente di definire un Bolt di commit transazionale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="c1f54-265">Eseguirà l'applicazione con ***exec-name*** usando ***args***.</span><span class="sxs-lookup"><span data-stu-id="c1f54-265">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="c1f54-266">***fields*** corrisponde ai campi di output per il Bolt.</span><span class="sxs-lookup"><span data-stu-id="c1f54-266">The ***fields*** is the Output Fields for bolt</span></span> |
| <span data-ttu-id="c1f54-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="c1f54-267">**nontx-topolopy**</span></span> |<span data-ttu-id="c1f54-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="c1f54-268">topology-name</span></span><br /><span data-ttu-id="c1f54-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="c1f54-269">spout-map</span></span><br /><span data-ttu-id="c1f54-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="c1f54-270">bolt-map</span></span> |<span data-ttu-id="c1f54-271">Consente di definire una topologia non transazionale con il nome della topologia,&nbsp;la mappa di definizione degli spout e la mappa di definizione dei bolt.</span><span class="sxs-lookup"><span data-stu-id="c1f54-271">Define a nontransactional topology with the topology name,&nbsp; spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="c1f54-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="c1f54-272">**scp-spout**</span></span> |<span data-ttu-id="c1f54-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="c1f54-273">exec-name</span></span><br /><span data-ttu-id="c1f54-274">args</span><span class="sxs-lookup"><span data-stu-id="c1f54-274">args</span></span><br /><span data-ttu-id="c1f54-275">fields</span><span class="sxs-lookup"><span data-stu-id="c1f54-275">fields</span></span><br /><span data-ttu-id="c1f54-276">Parametri</span><span class="sxs-lookup"><span data-stu-id="c1f54-276">parameters</span></span> |<span data-ttu-id="c1f54-277">Consente di definire uno Spout non transazionale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-277">Define a nontransactional spout.</span></span> <span data-ttu-id="c1f54-278">Eseguirà l'applicazione con ***exec-name*** usando ***args***.</span><span class="sxs-lookup"><span data-stu-id="c1f54-278">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="c1f54-279">***fields*** corrisponde ai campi di output per lo Spout.</span><span class="sxs-lookup"><span data-stu-id="c1f54-279">The ***fields*** is the Output Fields for spout</span></span><br /><br /><span data-ttu-id="c1f54-280">***parameters*** è facoltativo, può essere usato per specificare parametri come ad esempio "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="c1f54-280">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="c1f54-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="c1f54-281">**scp-bolt**</span></span> |<span data-ttu-id="c1f54-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="c1f54-282">exec-name</span></span><br /><span data-ttu-id="c1f54-283">args</span><span class="sxs-lookup"><span data-stu-id="c1f54-283">args</span></span><br /><span data-ttu-id="c1f54-284">fields</span><span class="sxs-lookup"><span data-stu-id="c1f54-284">fields</span></span><br /><span data-ttu-id="c1f54-285">Parametri</span><span class="sxs-lookup"><span data-stu-id="c1f54-285">parameters</span></span> |<span data-ttu-id="c1f54-286">Consente di definire un Bolt non transazionale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="c1f54-287">Eseguirà l'applicazione con ***exec-name*** usando ***args***.</span><span class="sxs-lookup"><span data-stu-id="c1f54-287">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="c1f54-288">***fields*** corrisponde ai campi di output per il Bolt.</span><span class="sxs-lookup"><span data-stu-id="c1f54-288">The ***fields*** is the Output Fields for bolt</span></span><br /><br /><span data-ttu-id="c1f54-289">***parameters*** è facoltativo, può essere usato per specificare parametri come ad esempio "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="c1f54-289">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="c1f54-290">In SCP.NET sono disponibili le parole chiave seguenti:</span><span class="sxs-lookup"><span data-stu-id="c1f54-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="c1f54-291">**Parole chiave**</span><span class="sxs-lookup"><span data-stu-id="c1f54-291">**Key Words**</span></span> | <span data-ttu-id="c1f54-292">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="c1f54-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c1f54-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="c1f54-293">**:name**</span></span> |<span data-ttu-id="c1f54-294">Consente di definire il nome della topologia.</span><span class="sxs-lookup"><span data-stu-id="c1f54-294">Define the Topology Name</span></span> |
| <span data-ttu-id="c1f54-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="c1f54-295">**:topology**</span></span> |<span data-ttu-id="c1f54-296">Consente di definire la topologia usando le funzioni precedenti e quelle predefinite.</span><span class="sxs-lookup"><span data-stu-id="c1f54-296">Define the Topology using the above functions and build in ones.</span></span> |
| <span data-ttu-id="c1f54-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="c1f54-297">**:p**</span></span> |<span data-ttu-id="c1f54-298">Consente di definire l'hint di parallelismo per ogni Spout o Bolt.</span><span class="sxs-lookup"><span data-stu-id="c1f54-298">Define the parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="c1f54-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="c1f54-299">**:config**</span></span> |<span data-ttu-id="c1f54-300">Consente di definire i parametri di configurazione o aggiornare quelli esistenti</span><span class="sxs-lookup"><span data-stu-id="c1f54-300">Define configure parameter or update the existing ones</span></span> |
| <span data-ttu-id="c1f54-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="c1f54-301">**:schema**</span></span> |<span data-ttu-id="c1f54-302">Consente di definire lo schema del flusso.</span><span class="sxs-lookup"><span data-stu-id="c1f54-302">Define the Schema of Stream.</span></span> |

<span data-ttu-id="c1f54-303">E i parametri di uso frequente seguenti:</span><span class="sxs-lookup"><span data-stu-id="c1f54-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="c1f54-304">**Parametro**</span><span class="sxs-lookup"><span data-stu-id="c1f54-304">**Parameter**</span></span> | <span data-ttu-id="c1f54-305">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="c1f54-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c1f54-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="c1f54-306">**"plugin.name"**</span></span> |<span data-ttu-id="c1f54-307">Nome del file eseguibile del plug-in C#.</span><span class="sxs-lookup"><span data-stu-id="c1f54-307">exe file name of the C# plugin</span></span> |
| <span data-ttu-id="c1f54-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="c1f54-308">**"plugin.args"**</span></span> |<span data-ttu-id="c1f54-309">Argomenti del plug-in.</span><span class="sxs-lookup"><span data-stu-id="c1f54-309">plugin args</span></span> |
| <span data-ttu-id="c1f54-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="c1f54-310">**"output.schema"**</span></span> |<span data-ttu-id="c1f54-311">Schema di output.</span><span class="sxs-lookup"><span data-stu-id="c1f54-311">Output schema</span></span> |
| <span data-ttu-id="c1f54-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="c1f54-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="c1f54-313">Abilitazione o meno dell'acknowledgement per la topologia non transazionale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="c1f54-314">Il comando runspec verrà implementato insieme ai bit, l'utilizzo è il seguente:</span><span class="sxs-lookup"><span data-stu-id="c1f54-314">The runspec command will be deployed together with the bits, the usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="c1f54-315">Il parametro ***resource-dir*** è facoltativo. È necessario specificarlo quando si vuole collegare un'applicazione C\# e questa directory conterrà l'applicazione, le dipendenze e le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="c1f54-315">The ***resource-dir*** parameter is optional, you need to specify it when you want to plug a C\# application, and this directory will contain the application, the dependencies and configurations.</span></span>

<span data-ttu-id="c1f54-316">Anche il parametro ***classpath*** è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="c1f54-316">The ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="c1f54-317">Si usa per specificare il classpath Java se il file delle specifiche contiene Spout o Bolt Java.</span><span class="sxs-lookup"><span data-stu-id="c1f54-317">It is used to specify the Java classpath if the spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="c1f54-318">Funzionalità varie</span><span class="sxs-lookup"><span data-stu-id="c1f54-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="c1f54-319">Dichiarazione dello schema di input e di output</span><span class="sxs-lookup"><span data-stu-id="c1f54-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="c1f54-320">L'utente può emettere la tupla nel processo C\#, la piattaforma deve serializzare la tupla in byte[] e trasferirla sul lato Java, quindi Storm trasferirà la tupla alle destinazioni.</span><span class="sxs-lookup"><span data-stu-id="c1f54-320">The user can emit tuple in C\# process, the platform needs to serialize the tuple into byte[], transfer to Java side, and Storm will transfer this tuple to the targets.</span></span> <span data-ttu-id="c1f54-321">Nel frattempo, nel componente downstream, il processo C\# riceverà nuovamente la tupla dal lato Java e la convertirà nei tipi originali in base alla piattaforma. Tutte queste operazioni sono nascoste dalla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="c1f54-321">Meanwhile in downstream component, the C\# process will receive tuple back from java side, and convert it to the original types by platform, all these operations are hidden by the Platform.</span></span>

<span data-ttu-id="c1f54-322">Per supportare la serializzazione e la deserializzazione, il codice utente deve dichiarare lo schema degli input e degli output.</span><span class="sxs-lookup"><span data-stu-id="c1f54-322">To support the serialization and deserialization, user code needs to declare the schema of the inputs and outputs.</span></span>

<span data-ttu-id="c1f54-323">Lo schema del flusso di input/output viene definito come un dizionario, la chiave è lo StreamId e il valore corrisponde ai tipi delle colonne.</span><span class="sxs-lookup"><span data-stu-id="c1f54-323">The input/output stream schema is defined as a dictionary, the key is the StreamId and the value is the Types of the columns.</span></span> <span data-ttu-id="c1f54-324">Nel componente possono essere dichiarati più flussi.</span><span class="sxs-lookup"><span data-stu-id="c1f54-324">The component can have multi-streams declared.</span></span>

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


<span data-ttu-id="c1f54-325">Nell'oggetto Context è stata aggiunta l'API seguente:</span><span class="sxs-lookup"><span data-stu-id="c1f54-325">In Context object, we have the following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="c1f54-326">Il codice utente deve assicurare che le tuple emesse obbediscano allo schema definito per il flusso, o il sistema genererà un'eccezione di runtime.</span><span class="sxs-lookup"><span data-stu-id="c1f54-326">User code must make sure the tuples emitted obey the schema defined for that stream, or the system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="c1f54-327">Supporto di più flussi</span><span class="sxs-lookup"><span data-stu-id="c1f54-327">Multi-Stream Support</span></span>
<span data-ttu-id="c1f54-328">SCP supporta codice utente per l'emissione o la ricezione simultanea da più flussi distinti.</span><span class="sxs-lookup"><span data-stu-id="c1f54-328">SCP supports user code to emit or receive from multiple distinct streams at the same time.</span></span> <span data-ttu-id="c1f54-329">Questo supporto è riflesso nell'oggetto Context dal fatto che il metodo Emit accetta un parametro StreamId facoltativo.</span><span class="sxs-lookup"><span data-stu-id="c1f54-329">The support reflects in the Context object as the Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="c1f54-330">Nell'oggetto Context SCP.NET sono stati aggiunti due metodi.</span><span class="sxs-lookup"><span data-stu-id="c1f54-330">Two methods in the SCP.NET Context object have been added.</span></span> <span data-ttu-id="c1f54-331">Vengono usati per l'emissione di una o più tuple per specificare StreamId.</span><span class="sxs-lookup"><span data-stu-id="c1f54-331">They are used to emit Tuple or Tuples to specify StreamId.</span></span> <span data-ttu-id="c1f54-332">StreamId è una stringa e deve essere coerente in C\# e nelle specifiche di definizione della topologia.</span><span class="sxs-lookup"><span data-stu-id="c1f54-332">The StreamId is a string and it needs to be consistent in both C\# and the Topology Definition Spec.</span></span>

        /* Emit tuple to the specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="c1f54-333">L'emissione in un flusso non esistente causerà eccezioni di runtime.</span><span class="sxs-lookup"><span data-stu-id="c1f54-333">The emitting to a non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="c1f54-334">Raggruppamento dei campi</span><span class="sxs-lookup"><span data-stu-id="c1f54-334">Fields Grouping</span></span>
<span data-ttu-id="c1f54-335">Il raggruppamento dei campi predefinito di Storm non funziona correttamente in SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="c1f54-335">The build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="c1f54-336">Sul lato Proxy Java tutti i dati dei campi sono in effetti di tipo byte[] e per il raggruppamento dei campi viene usato il codice hash dell'oggetto byte[].</span><span class="sxs-lookup"><span data-stu-id="c1f54-336">On the Java Proxy side, all the fields data types are actually byte[], and the fields grouping uses the byte[] object hash code to perform the grouping.</span></span> <span data-ttu-id="c1f54-337">Il codice hash dell'oggetto byte[] corrisponde all'indirizzo dell'oggetto in memoria.</span><span class="sxs-lookup"><span data-stu-id="c1f54-337">The byte[] object hash code is the address of this object in memory.</span></span> <span data-ttu-id="c1f54-338">Per questo motivo, il raggruppamento di due oggetti byte[] che condividono lo stesso contenuto, ma non lo stesso indirizzo, sarà errato.</span><span class="sxs-lookup"><span data-stu-id="c1f54-338">So the grouping will be wrong for two byte[] objects that share the same content but not the same address.</span></span>

<span data-ttu-id="c1f54-339">SCP.NET aggiunge un metodo di raggruppamento personalizzato e userà il contenuto di byte[] per eseguire il raggruppamento.</span><span class="sxs-lookup"><span data-stu-id="c1f54-339">SCP.NET adds a customized grouping method, and it will use the content of the byte[] to do the grouping.</span></span> <span data-ttu-id="c1f54-340">Nel file **SPEC** la sintassi è come segue:</span><span class="sxs-lookup"><span data-stu-id="c1f54-340">In **SPEC** file, the syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="c1f54-341">Qui</span><span class="sxs-lookup"><span data-stu-id="c1f54-341">Here,</span></span>

1. <span data-ttu-id="c1f54-342">"scp-field-group" vuol dire "raggruppamento campi personalizzato implementato da SCP".</span><span class="sxs-lookup"><span data-stu-id="c1f54-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="c1f54-343">":tx" o ":non-tx" indica se si tratta o meno di una topologia transazionale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="c1f54-344">Questa informazione è necessaria in quanto l'indice di inizio è diverso nei due tipi di topologie.</span><span class="sxs-lookup"><span data-stu-id="c1f54-344">We need this information since the starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="c1f54-345">[0,1] indica un hashset di Id campo, che parte da 0.</span><span class="sxs-lookup"><span data-stu-id="c1f54-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="c1f54-346">Topologia ibrida</span><span class="sxs-lookup"><span data-stu-id="c1f54-346">Hybrid topology</span></span>
<span data-ttu-id="c1f54-347">Il sistema Storm nativo è scritto in Java.</span><span class="sxs-lookup"><span data-stu-id="c1f54-347">The native Storm is written in Java.</span></span> <span data-ttu-id="c1f54-348">E SCP.Net lo ha migliorato per consentire di scrivere codice C\# per gestire la logica di business.</span><span class="sxs-lookup"><span data-stu-id="c1f54-348">And SCP.Net has enhanced it to enable our customs to write C\# code to handle their business logic.</span></span> <span data-ttu-id="c1f54-349">SCP supporta però anche le topologie ibride, che contengono spout/bolt sia in linguaggio Java sia in C\#.</span><span class="sxs-lookup"><span data-stu-id="c1f54-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="c1f54-350">Specificare gli Spout e i Bolt Java nel file delle specifiche</span><span class="sxs-lookup"><span data-stu-id="c1f54-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="c1f54-351">Nel file delle specifiche è possibile usare "scp-spout" e "scp-bolt" anche per specificare gli Spout e i Bolt Java. Di seguito è riportato un esempio:</span><span class="sxs-lookup"><span data-stu-id="c1f54-351">In spec file, "scp-spout" and "scp-bolt" can also be used to specify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="c1f54-352">Qui `microsoft.scp.example.HybridTopology.Generator` è il nome della classe Spout Java.</span><span class="sxs-lookup"><span data-stu-id="c1f54-352">Here `microsoft.scp.example.HybridTopology.Generator` is the name of the Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="c1f54-353">Specificare il classpath Java nel comando runSpec</span><span class="sxs-lookup"><span data-stu-id="c1f54-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="c1f54-354">Per inviare una topologia che contiene Spout o Bolt Java, è necessario prima compilare gli Spout o Bolt Java e ottenere i file Jar.</span><span class="sxs-lookup"><span data-stu-id="c1f54-354">If you want to submit topology containing Java Spouts or Bolts, you need to first compile the Java Spouts or Bolts and get the Jar files.</span></span> <span data-ttu-id="c1f54-355">Quindi, è necessario specificare il classpath Java che contiene i file Jar al momento dell'invio della topologia.</span><span class="sxs-lookup"><span data-stu-id="c1f54-355">Then you should specify the java classpath that contains the Jar files when submitting topology.</span></span> <span data-ttu-id="c1f54-356">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="c1f54-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="c1f54-357">Qui **examples\\HybridTopology\\java\\target\\** è la cartella che contiene il file JAR degli spout/bolt Java.</span><span class="sxs-lookup"><span data-stu-id="c1f54-357">Here **examples\\HybridTopology\\java\\target\\** is the folder containing the Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="c1f54-358">Serializzazione e deserializzazione tra Java e C\\</span><span class="sxs-lookup"><span data-stu-id="c1f54-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="c1f54-359">Il componente SCP include il lato Java e il lato C\#.</span><span class="sxs-lookup"><span data-stu-id="c1f54-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="c1f54-360">Per interagire con spout/bolt Java nativi, la serializzazione/deserializzazione deve essere effettuata tra il lato Java e il lato C\#, come illustrato nel grafico seguente.</span><span class="sxs-lookup"><span data-stu-id="c1f54-360">In order to interact with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in the following graph.</span></span>

![Diagramma del componente Java che invia al componente SCP che invia al componente Java](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="c1f54-362">**Serializzazione sul lato Java e deserializzazione sul lato C#\#**</span><span class="sxs-lookup"><span data-stu-id="c1f54-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="c1f54-363">Prima di tutto è necessario fornire l'implementazione predefinita per la serializzazione sul lato Java e la deserializzazione sul lato C\#.</span><span class="sxs-lookup"><span data-stu-id="c1f54-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="c1f54-364">Il metodo di serializzazione sul lato Java può essere specificato nel file SPEC:</span><span class="sxs-lookup"><span data-stu-id="c1f54-364">The serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="c1f54-365">Il metodo di deserializzazione sul lato C\# può essere specificato nel codice utente C\#:</span><span class="sxs-lookup"><span data-stu-id="c1f54-365">The deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="c1f54-366">Questa implementazione predefinita consente di gestire la maggior parte dei casi, se il tipo di dati non è troppo complesso.</span><span class="sxs-lookup"><span data-stu-id="c1f54-366">This default implementation should handle most cases if the data type is not too complex.</span></span> <span data-ttu-id="c1f54-367">Per alcuni casi, se il tipo di dati dell'utente è troppo complesso o se le prestazioni dell'implementazione predefinita non soddisfano i requisiti dell'utente, è possibile collegare una propria implementazione.</span><span class="sxs-lookup"><span data-stu-id="c1f54-367">For certain cases, either because the user data type is too complex, or because the performance of our default implementation does not meet the user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="c1f54-368">L'interfaccia di serializzazione sul lato Java viene definita nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="c1f54-368">The serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="c1f54-369">L'interfaccia di deserializzazione sul lato C\# viene definita nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="c1f54-369">The deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="c1f54-370">interfaccia pubblica ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="c1f54-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="c1f54-371">**Serializzazione sul lato C\# e deserializzazione sul lato Java**</span><span class="sxs-lookup"><span data-stu-id="c1f54-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="c1f54-372">Il metodo di serializzazione sul lato C\# può essere specificato nel codice utente C\#:</span><span class="sxs-lookup"><span data-stu-id="c1f54-372">The serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="c1f54-373">Il metodo di deserializzazione sul lato Java può essere specificato nel file SPEC:</span><span class="sxs-lookup"><span data-stu-id="c1f54-373">The Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="c1f54-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="c1f54-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="c1f54-375">Qui "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" è il nome del deserializzatore e "microsoft.scp.example.HybridTopology.Person" è la classe di destinazione dei dati deserializzati.</span><span class="sxs-lookup"><span data-stu-id="c1f54-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is the name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is the target class the data is deserialized to.</span></span>
   
   <span data-ttu-id="c1f54-376">L'utente può anche collegare una propria implementazione del serializzatore C\# e del deserializzatore Java.</span><span class="sxs-lookup"><span data-stu-id="c1f54-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="c1f54-377">Interfaccia per il serializzatore C\#:</span><span class="sxs-lookup"><span data-stu-id="c1f54-377">This is the interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="c1f54-378">Interfaccia per il deserializzatore Java:</span><span class="sxs-lookup"><span data-stu-id="c1f54-378">This is the interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="c1f54-379">Modalità host di SCP</span><span class="sxs-lookup"><span data-stu-id="c1f54-379">SCP Host Mode</span></span>
<span data-ttu-id="c1f54-380">In questa modalità l'utente può compilare il suo codice in DLL e usare il file SCPHost.exe fornito da SCP per inviare la topologia.</span><span class="sxs-lookup"><span data-stu-id="c1f54-380">In this mode, user can compile their codes to DLL, and use SCPHost.exe provided by SCP to submit topology.</span></span> <span data-ttu-id="c1f54-381">Il file delle specifiche ha un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c1f54-381">The spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="c1f54-382">Qui `plugin.name` viene specificato come file `SCPHost.exe` fornito dall’SDK di SCP.</span><span class="sxs-lookup"><span data-stu-id="c1f54-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="c1f54-383">SCPHost.exe accetta esattamente tre parametri:</span><span class="sxs-lookup"><span data-stu-id="c1f54-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="c1f54-384">Il primo è il nome della DLL, che in questo esempio è `"HelloWorld.dll"` .</span><span class="sxs-lookup"><span data-stu-id="c1f54-384">The first one is the DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="c1f54-385">Il secondo è il nome della classe, che in questo esempio è `"Scp.App.HelloWorld.Generator"` .</span><span class="sxs-lookup"><span data-stu-id="c1f54-385">The second one is the Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="c1f54-386">Il terzo è il nome di un metodo statico pubblico, che può essere richiamato per ottenere un'istanza di ISCPPlugin.</span><span class="sxs-lookup"><span data-stu-id="c1f54-386">The third one is the name of a public static method, which can be invoked to get an instance of ISCPPlugin.</span></span>

<span data-ttu-id="c1f54-387">In modalità host il codice utente viene compilato come DLL e richiamato dalla piattaforma SCP.</span><span class="sxs-lookup"><span data-stu-id="c1f54-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="c1f54-388">In questo modo, la piattaforma SCP può ottenere il controllo completo dell'intera logica di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="c1f54-388">So SCP platform can get full control of the whole processing logic.</span></span> <span data-ttu-id="c1f54-389">È quindi consigliabile inviare la topologia nella modalità host di SCP, poiché questo consente di semplificare l'esperienza di sviluppo e offre una maggiore flessibilità e una migliore compatibilità con le versioni precedenti per le versioni successive.</span><span class="sxs-lookup"><span data-stu-id="c1f54-389">So we recommend our customers to submit topology in SCP host mode since it can simplify the development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="c1f54-390">Esempi di programmazione SCP</span><span class="sxs-lookup"><span data-stu-id="c1f54-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="c1f54-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="c1f54-391">HelloWorld</span></span>
<span data-ttu-id="c1f54-392">**HelloWorld** è un esempio molto semplice di utilizzo di SCP.Net.</span><span class="sxs-lookup"><span data-stu-id="c1f54-392">**HelloWorld** is a very simple example to show a taste of SCP.Net.</span></span> <span data-ttu-id="c1f54-393">Usa una topologia non transazionale con uno spout denominato **generator** e due bolt denominati **splitter** e **counter**.</span><span class="sxs-lookup"><span data-stu-id="c1f54-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="c1f54-394">Lo spout **generator** genererà frasi casuali e le emetterà verso **splitter**.</span><span class="sxs-lookup"><span data-stu-id="c1f54-394">The spout **generator** will randomly generate some sentences, and emit these sentences to **splitter**.</span></span> <span data-ttu-id="c1f54-395">Il bolt **splitter** dividerà le frasi in parole ed emetterà le parole verso il bolt **counter**.</span><span class="sxs-lookup"><span data-stu-id="c1f54-395">The bolt **splitter** will split the sentences to words and emit these words to **counter** bolt.</span></span> <span data-ttu-id="c1f54-396">Il Bolt “counter” usa un dizionario per registrare il numero di occorrenze di ogni parola.</span><span class="sxs-lookup"><span data-stu-id="c1f54-396">The bolt "counter" uses a dictionary to record the occurrence number of each word.</span></span>

<span data-ttu-id="c1f54-397">Per questo esempio sono presenti due file di specifiche, **HelloWorld.spec** e **HelloWorld\_EnableAck.spec**.</span><span class="sxs-lookup"><span data-stu-id="c1f54-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="c1f54-398">Nel codice C\# può determinare se il meccanismo di acknowledgement è abilitato ottenendo pluginConf dal lato Java.</span><span class="sxs-lookup"><span data-stu-id="c1f54-398">In the C\# code, it can find out whether ack is enabled by getting the pluginConf from Java side.</span></span>

    /* demo how to get pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="c1f54-399">Nello Spout, se l'acknowledgement è abilitato viene usato un dizionario per memorizzare nella cache le tuple non confermate.</span><span class="sxs-lookup"><span data-stu-id="c1f54-399">In the spout, if ack is enabled, a dictionary is used to cache the tuples that have not been acked.</span></span> <span data-ttu-id="c1f54-400">Se viene chiamato Fail() la tupla in errore verrà riprodotta:</span><span class="sxs-lookup"><span data-stu-id="c1f54-400">If Fail() is called, the failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get the cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay the failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="c1f54-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="c1f54-401">HelloWorldTx</span></span>
<span data-ttu-id="c1f54-402">L'esempio **HelloWorldTx** illustra come implementare la topologia transazionale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-402">The **HelloWorldTx** example demonstrates how to implement transactional topology.</span></span> <span data-ttu-id="c1f54-403">Contiene uno spout denominato **generator**, un bolt batch denominato **partial-count** e un bolt di commit denominato **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="c1f54-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="c1f54-404">Sono presenti anche tre file txt già creati: **DataSource0.txt**, **DataSource1.txt** e **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="c1f54-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="c1f54-405">In ogni transazione lo spout **generator** sceglierà casualmente due dei tre file già creati ed emetterà i nomi dei due file verso il bolt **partial-count**.</span><span class="sxs-lookup"><span data-stu-id="c1f54-405">In each transaction, the spout **generator** will randomly choose two files from the pre-created three files, and emit the two file names to the **partial-count** bolt.</span></span> <span data-ttu-id="c1f54-406">Il bolt **partial-count** come prima cosa otterrà il nome del file dalla tupla ricevuta, quindi aprirà il file e conterà il numero di parole al suo interno. Infine, emetterà il numero di parole verso il bolt **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="c1f54-406">The bolt **partial-count** will first get the file name from the received tuple, then open the file and count the number of words in this file, and finally emit the word number to the **count-sum** bolt.</span></span> <span data-ttu-id="c1f54-407">Il bolt **count-sum** riepilogherà il conteggio totale.</span><span class="sxs-lookup"><span data-stu-id="c1f54-407">The **count-sum** bolt will summarize the total count.</span></span>

<span data-ttu-id="c1f54-408">Per ottenere una semantica di tipo **exactly once**, il bolt di commit **count-sum** deve stabilire se si tratta di una transazione riprodotta.</span><span class="sxs-lookup"><span data-stu-id="c1f54-408">To achieve **exactly once** semantics, the commit bolt **count-sum** need to judge whether it is a replayed transaction.</span></span> <span data-ttu-id="c1f54-409">In questo esempio, contiene una variabile membro statica:</span><span class="sxs-lookup"><span data-stu-id="c1f54-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="c1f54-410">Quando viene creata un'istanza di ISCPBatchBolt, otterrà il valore `txAttempt` dai parametri di input:</span><span class="sxs-lookup"><span data-stu-id="c1f54-410">When an ISCPBatchBolt instance is created, it will get the `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from the input parms */
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

<span data-ttu-id="c1f54-411">Quando viene chiamato `FinishBatch()`, se non si tratta di una transazione riprodotta il valore `lastCommittedTxId` verrà aggiornato.</span><span class="sxs-lookup"><span data-stu-id="c1f54-411">When `FinishBatch()` is called, the `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update the toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="c1f54-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="c1f54-412">HybridTopology</span></span>
<span data-ttu-id="c1f54-413">Questa topologia contiene uno spout Java e un bolt C\#.</span><span class="sxs-lookup"><span data-stu-id="c1f54-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="c1f54-414">Usa l'implementazione di serializzazione e deserializzazione predefinita fornita dalla piattaforma SCP.</span><span class="sxs-lookup"><span data-stu-id="c1f54-414">It uses the default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="c1f54-415">Fare riferimento al file **HybridTopology.spec** nella cartella **examples\\HybridTopology** per dettagli specifici sul file e a **SubmitTopology.bat** per informazioni su come specificare il classpath Java.</span><span class="sxs-lookup"><span data-stu-id="c1f54-415">Please ref the **HybridTopology.spec** in **examples\\HybridTopology** folder for the spec file details, and **SubmitTopology.bat** for how to specify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="c1f54-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="c1f54-416">SCPHostDemo</span></span>
<span data-ttu-id="c1f54-417">In sostanza, questo esempio è uguale a HelloWorld.</span><span class="sxs-lookup"><span data-stu-id="c1f54-417">This example is the same as HelloWorld in essence.</span></span> <span data-ttu-id="c1f54-418">L'unica differenza è che il codice utente viene compilato come DLL e la topologia viene inviata usando SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="c1f54-418">The only difference is that the user code is compiled as DLL and the topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="c1f54-419">Per una spiegazione più dettagliata, fare riferimento alla sezione “Modalità host di SCP”.</span><span class="sxs-lookup"><span data-stu-id="c1f54-419">Please ref the section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1f54-420">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c1f54-420">Next Steps</span></span>
<span data-ttu-id="c1f54-421">Per esempi di topologie Storm create con SCP, vedere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c1f54-421">For examples of Storm topologies created using SCP, see the following:</span></span>

* [<span data-ttu-id="c1f54-422">Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c1f54-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="c1f54-423">Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c1f54-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="c1f54-424">Creare più flussi di dati in una topologia Storm C#</span><span class="sxs-lookup"><span data-stu-id="c1f54-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="c1f54-425">Usare Power BI per visualizzare i dati dalla topologia Storm</span><span class="sxs-lookup"><span data-stu-id="c1f54-425">Use Power Bi to visualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="c1f54-426">Elaborare i dati del sensore veicolo dall'hub di eventi usando Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c1f54-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="c1f54-427">Estrarre, trasformare e caricare dagli hub eventi di Azure in HBase</span><span class="sxs-lookup"><span data-stu-id="c1f54-427">Extract, Transform, and Load (ETL) from Azure Event Hubs to HBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="c1f54-428">Correlare gli eventi  con Storm e HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c1f54-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

