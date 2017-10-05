---
title: Serializzare dati in Hadoop con la libreria Microsoft Avro | Microsoft Docs
description: Informazioni su come serializzare e deserializzare i dati in Hadoop in HDInsight con la libreria Microsoft Avro in modo permanente in memoria, in un database o in un file.
keywords: avro, avro hadoop
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: d06bf8ff4a21e4f4b29593bac32bfa2b32601fc4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="serialize-data-in-hadoop-with-the-microsoft-avro-library"></a><span data-ttu-id="044bd-104">Serializzare i dati con la libreria Microsoft Avro</span><span class="sxs-lookup"><span data-stu-id="044bd-104">Serialize data in Hadoop with the Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="044bd-105">L'SDK Avro non è più supportato da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="044bd-105">The Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="044bd-106">La libreria è supportata dalla community open source.</span><span class="sxs-lookup"><span data-stu-id="044bd-106">The library is open source community supported.</span></span> <span data-ttu-id="044bd-107">Le origini per la libreria si trovano in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="044bd-107">The sources for the library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="044bd-108">Questo argomento illustra come usare la [libreria Microsoft Avro](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) per serializzare oggetti e altre strutture di dati in flussi, in modo da renderli permanenti in memoria, in un database o in un file.</span><span class="sxs-lookup"><span data-stu-id="044bd-108">This topic shows how to use the [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) to serialize objects and other data structures into streams to persist them to memory, a database, or a file.</span></span> <span data-ttu-id="044bd-109">Viene anche illustrato come deserializzarli in modo da ripristinare gli oggetti originali.</span><span class="sxs-lookup"><span data-stu-id="044bd-109">It also shows how to deserialize them to recover the original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="044bd-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="044bd-110">Apache Avro</span></span>
<span data-ttu-id="044bd-111">La <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">libreria Microsoft Avro</a> implementa il sistema di serializzazione dei dati Apache Avro per l'ambiente Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="044bd-111">The <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements the Apache Avro data serialization system for the Microsoft.NET environment.</span></span> <span data-ttu-id="044bd-112">Apache Avro offre un formato compatto di interscambio dei dati binari per la serializzazione</span><span class="sxs-lookup"><span data-stu-id="044bd-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="044bd-113">e usa <a href="http://www.json.org" target="_blank">JSON</a> per definire lo schema indipendente dal linguaggio che assicura l'interoperabilità dei linguaggi.</span><span class="sxs-lookup"><span data-stu-id="044bd-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> to define a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="044bd-114">I dati serializzati in un unico linguaggio possono essere letti in un altro linguaggio.</span><span class="sxs-lookup"><span data-stu-id="044bd-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="044bd-115">I formati attualmente supportati sono C, C++, C#, Java, PHP, Python e Ruby.</span><span class="sxs-lookup"><span data-stu-id="044bd-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="044bd-116">Informazioni dettagliate sul formato sono disponibili nelle <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">specifiche di Apache Avro</a>.</span><span class="sxs-lookup"><span data-stu-id="044bd-116">Detailed information on the format can be found in the <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="044bd-117">La libreria Microsoft Avro non supporta la parte relativa alle RPC (Remote Procedure Call) di queste specifiche.</span><span class="sxs-lookup"><span data-stu-id="044bd-117">The Microsoft Avro Library does not support the remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="044bd-118">La rappresentazione serializzata di un oggetto nel sistema Avro è costituita da due parti: schema e valore effettivo.</span><span class="sxs-lookup"><span data-stu-id="044bd-118">The serialized representation of an object in the Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="044bd-119">Lo schema Avro descrive il modello di dati indipendente dal linguaggio dei dati serializzati con JSON.</span><span class="sxs-lookup"><span data-stu-id="044bd-119">The Avro schema describes the language-independent data model of the serialized data with JSON.</span></span> <span data-ttu-id="044bd-120">È presentato side-by-side con una rappresentazione binaria dei dati.</span><span class="sxs-lookup"><span data-stu-id="044bd-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="044bd-121">La separazione dello schema dalla rappresentazione binaria permette di scrivere ciascun oggetto senza sovraccarichi per ogni valore, velocizzando la serializzazione e riducendo le dimensioni della rappresentazione.</span><span class="sxs-lookup"><span data-stu-id="044bd-121">Having the schema separate from the binary representation permits each object to be written with no per-value overheads, making serialization fast, and the representation small.</span></span>

## <a name="the-hadoop-scenario"></a><span data-ttu-id="044bd-122">Scenario Hadoop</span><span class="sxs-lookup"><span data-stu-id="044bd-122">The Hadoop scenario</span></span>
<span data-ttu-id="044bd-123">Il formato di serializzazione Apache Avro è ampiamente usato in Azure HDInsight e in altri ambienti Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="044bd-123">The Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="044bd-124">Avro rappresenta un modo pratico per rappresentare le strutture di dati complesse con un processo MapReduce di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="044bd-124">Avro provides a convenient way to represent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="044bd-125">Il formato dei file Avro (file contenitore di oggetti Avro) è stato progettato per supportare il modello di programmazione MapReduce distribuito.</span><span class="sxs-lookup"><span data-stu-id="044bd-125">The format of Avro files (Avro object container file) has been designed to support the distributed MapReduce programming model.</span></span> <span data-ttu-id="044bd-126">La funzione chiave che abilita la distribuzione è la possibilità di suddividere i file, rendendo possibile iniziare la lettura da un particolare blocco in qualsiasi punto di un file.</span><span class="sxs-lookup"><span data-stu-id="044bd-126">The key feature that enables the distribution is that the files are “splittable” in the sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="044bd-127">Serializzazione nella libreria Avro</span><span class="sxs-lookup"><span data-stu-id="044bd-127">Serialization in Avro Library</span></span>
<span data-ttu-id="044bd-128">La libreria .NET per Avro supporta due modalità di serializzazione degli oggetti:</span><span class="sxs-lookup"><span data-stu-id="044bd-128">The .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="044bd-129">**Reflection** : lo schema JSON per i tipi viene automaticamente creato dagli attributi del contratto dati dei tipi .NET da serializzare.</span><span class="sxs-lookup"><span data-stu-id="044bd-129">**reflection** - The JSON schema for the types is automatically built from the data contract attributes of the .NET types to be serialized.</span></span>
* <span data-ttu-id="044bd-130">**Record generico**: uno schema JSON viene specificato in modo esplicito in un record rappresentato dalla classe [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) quando non è presente alcun tipo .NET per descrivere lo schema dei dati da serializzare.</span><span class="sxs-lookup"><span data-stu-id="044bd-130">**generic record** - A JSON schema is explicitly specified in a record represented by the [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present to describe the schema for the data to be serialized.</span></span>

<span data-ttu-id="044bd-131">Quando lo schema di dati è noto sia al writer che al lettore del flusso, sarà possibile inviare i dati senza il relativo schema.</span><span class="sxs-lookup"><span data-stu-id="044bd-131">When the data schema is known to both the writer and reader of the stream, the data can be sent without its schema.</span></span> <span data-ttu-id="044bd-132">Se si usa un file contenitore di oggetti Avro, lo schema viene archiviato all'interno del file.</span><span class="sxs-lookup"><span data-stu-id="044bd-132">In cases when an Avro object container file is used, the schema is stored within the file.</span></span> <span data-ttu-id="044bd-133">È anche possibile specificare altri parametri, come il codec usato per la compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="044bd-133">Other parameters, such as the codec used for data compression, can be specified.</span></span> <span data-ttu-id="044bd-134">Questi scenari vengono delineati più dettagliatamente e illustrati negli esempi di codice riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="044bd-134">These scenarios are outlined in more detail and illustrated in the following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="044bd-135">Installare la libreria Avro</span><span class="sxs-lookup"><span data-stu-id="044bd-135">Install Avro Library</span></span>
<span data-ttu-id="044bd-136">Per installare la libreria sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="044bd-136">The following are required before you install the library:</span></span>

* <span data-ttu-id="044bd-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="044bd-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="044bd-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (versione 6.0.4 o successive)</span><span class="sxs-lookup"><span data-stu-id="044bd-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="044bd-139">La dipendenza Newtonsoft.Json.dll viene scaricata automaticamente insieme all'installazione della libreria Microsoft Avro.</span><span class="sxs-lookup"><span data-stu-id="044bd-139">Note that the Newtonsoft.Json.dll dependency is downloaded automatically with the installation of the Microsoft Avro Library.</span></span> <span data-ttu-id="044bd-140">La procedura è disponibile nella sezione seguente:</span><span class="sxs-lookup"><span data-stu-id="044bd-140">The procedure is provided in the following section:</span></span>

<span data-ttu-id="044bd-141">La libreria Microsoft Avro viene distribuita come pacchetto NuGet che può essere installato da Visual Studio con la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="044bd-141">The Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via the following procedure:</span></span>

1. <span data-ttu-id="044bd-142">Selezionare la scheda **Progetto** -> **Gestisci pacchetti NuGet...**</span><span class="sxs-lookup"><span data-stu-id="044bd-142">Select the **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="044bd-143">Cercare "Microsoft.Hadoop.Avro" nella casella **Cerca online** .</span><span class="sxs-lookup"><span data-stu-id="044bd-143">Search for "Microsoft.Hadoop.Avro" in the **Search Online** box.</span></span>
3. <span data-ttu-id="044bd-144">Fare clic sul pulsante **Installa** accanto a **Microsoft Azure HDInsight Avro Library**.</span><span class="sxs-lookup"><span data-stu-id="044bd-144">Click the **Install** button next to **Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="044bd-145">Anche la dipendenza Newtonsoft.Json.dll (>= .6.0.4) viene scaricata automaticamente assieme alla libreria Microsoft Avro.</span><span class="sxs-lookup"><span data-stu-id="044bd-145">Note that the Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with the Microsoft Avro Library.</span></span>

<span data-ttu-id="044bd-146">Il codice sorgente della libreria Microsoft Avro è disponibile in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="044bd-146">The Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="044bd-147">Compilare schemi tramite la libreria Avro</span><span class="sxs-lookup"><span data-stu-id="044bd-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="044bd-148">La libreria Microsoft Avro contiene un'utilità di generazione del codice con cui è possibile creare tipi C# in modo automatico, in base allo schema JSON definito in precedenza.</span><span class="sxs-lookup"><span data-stu-id="044bd-148">The Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on the previously defined JSON schema.</span></span> <span data-ttu-id="044bd-149">Questa utilità non viene distribuita come eseguibile binario, ma può essere facilmente compilata usando la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="044bd-149">The code generation utility is not distributed as a binary executable, but can be easily built via the following procedure:</span></span>

1. <span data-ttu-id="044bd-150">Scaricare il file ZIP con la versione più recente del codice sorgente di HDInsight SDK da <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK per Hadoop</a></span><span class="sxs-lookup"><span data-stu-id="044bd-150">Download the .zip file with the latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="044bd-151">Fare clic sull'icona **Scarica** e non sulla scheda **Download**.</span><span class="sxs-lookup"><span data-stu-id="044bd-151">(Click the **Download** icon, not the **Downloads** tab.)</span></span>
2. <span data-ttu-id="044bd-152">Estrarre HDInsight SDK in una directory nel computer in cui .NET Framework 4 è installato e connesso a Internet per scaricare i necessari pacchetti NuGet della dipendenza.</span><span class="sxs-lookup"><span data-stu-id="044bd-152">Extract the HDInsight SDK to a directory on the machine with .NET Framework 4 installed and connected to the Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="044bd-153">Di seguito si presuppone che il codice sorgente venga estratto in C:\SDK.</span><span class="sxs-lookup"><span data-stu-id="044bd-153">Below, we assume that the source code is extracted to C:\SDK.</span></span>
3. <span data-ttu-id="044bd-154">Passare alla cartella C:\SDK\src\Microsoft.Hadoop.Avro.Tools ed eseguire build.bat</span><span class="sxs-lookup"><span data-stu-id="044bd-154">Go to the folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="044bd-155">Il file chiamerà MSBuild dalla distribuzione a 32 bit di .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="044bd-155">(The file calls MSBuild from the 32-bit distribution of the .NET Framework.</span></span> <span data-ttu-id="044bd-156">Se si vuole usare la versione a 64 bit, modificare build.bat seguendo i commenti contenuti nel file. Assicurarsi che la compilazione venga completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="044bd-156">If you would like to use the 64-bit version, edit build.bat, following the comments inside the file.) Ensure that the build is successful.</span></span> <span data-ttu-id="044bd-157">In alcuni sistemi MSBuild può generare avvisi,</span><span class="sxs-lookup"><span data-stu-id="044bd-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="044bd-158">che tuttavia non influiscono sull'utilità purché non vi siano errori di compilazione.</span><span class="sxs-lookup"><span data-stu-id="044bd-158">These warnings do not affect the utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="044bd-159">L'utilità compilata si trova in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span><span class="sxs-lookup"><span data-stu-id="044bd-159">The compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="044bd-160">Per acquisire familiarità con la sintassi della riga di comando, eseguire il comando seguente dalla cartella in cui si trova l'utilità di generazione del codice: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span><span class="sxs-lookup"><span data-stu-id="044bd-160">To get familiar with the command-line syntax, execute the following command from the folder where the code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="044bd-161">Per testare l'utilità, è possibile generare classi C# dal file dello schema JSON di esempio fornito con il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="044bd-161">To test the utility, you can generate C# classes from the sample JSON schema file provided with the source code.</span></span> <span data-ttu-id="044bd-162">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="044bd-162">Execute the following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="044bd-163">Il comando dovrebbe creare due file C# nella directory corrente, SensorData.cs e Location.cs.</span><span class="sxs-lookup"><span data-stu-id="044bd-163">This is supposed to produce two C# files in the current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="044bd-164">Per determinare la logica usata dall'utilità di generazione del codice durante la conversione dello schema JSON in tipi C#, vedere il file GenerationVerification.feature, che si trova in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span><span class="sxs-lookup"><span data-stu-id="044bd-164">To understand the logic that the code generation utility is using while converting the JSON schema to C# types, see the file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="044bd-165">Gli spazi dei nomi vengono estratti dallo schema JSON usando la logica descritta nel file indicato nel paragrafo precedente.</span><span class="sxs-lookup"><span data-stu-id="044bd-165">Namespaces are extracted from the JSON schema, using the logic described in the file mentioned in the previous paragraph.</span></span> <span data-ttu-id="044bd-166">Gli spazi dei nomi estratti dallo schema hanno la precedenza su qualsiasi altro elemento specificato con il parametro /n nella riga di comando dell'utilità.</span><span class="sxs-lookup"><span data-stu-id="044bd-166">Namespaces extracted from the schema take precedence over whatever is provided with the /n parameter in the utility command line.</span></span> <span data-ttu-id="044bd-167">Se si vuole eseguire l'override degli spazi dei nomi contenuti nello schema, usare il parametro /nf.</span><span class="sxs-lookup"><span data-stu-id="044bd-167">If you want to override the namespaces contained within the schema, use the /nf parameter.</span></span> <span data-ttu-id="044bd-168">Ad esempio, per cambiare tutti gli spazi dei nomi da SampleJSONSchema.avsc a my.own.nspace, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="044bd-168">For example, to change all namespaces from the SampleJSONSchema.avsc to my.own.nspace, execute the following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-the-samples"></a><span data-ttu-id="044bd-169">Informazioni sugli esempi</span><span class="sxs-lookup"><span data-stu-id="044bd-169">About the samples</span></span>
<span data-ttu-id="044bd-170">I sei esempi forniti in questo argomento illustrano ciascuno diversi scenari supportati dalla libreria Microsoft Avro.</span><span class="sxs-lookup"><span data-stu-id="044bd-170">Six examples provided in this topic illustrate different scenarios supported by the Microsoft Avro Library.</span></span> <span data-ttu-id="044bd-171">La libreria Microsoft Avro è progettata per funzionare con qualsiasi flusso.</span><span class="sxs-lookup"><span data-stu-id="044bd-171">The Microsoft Avro Library is designed to work with any stream.</span></span> <span data-ttu-id="044bd-172">Per semplicità e coerenza, in questi esempi i dati vengono modificati usando flussi di memoria anziché flussi di file o database.</span><span class="sxs-lookup"><span data-stu-id="044bd-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="044bd-173">L'approccio adottato in un ambiente di produzione dipenderà dagli esatti requisiti dello scenario, dall'origine dati e dal volume, dai vincoli di prestazioni e da altri fattori.</span><span class="sxs-lookup"><span data-stu-id="044bd-173">The approach taken in a production environment depends on the exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="044bd-174">I primi due esempi mostrano come serializzare e deserializzare dati nei buffer del flusso di memoria mediante reflection e record generici.</span><span class="sxs-lookup"><span data-stu-id="044bd-174">The first two examples show how to serialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="044bd-175">In questi due casi si presuppone che lo schema sia condiviso tra lettori e writer fuori programma.</span><span class="sxs-lookup"><span data-stu-id="044bd-175">The schema in these two cases is assumed to be shared between the readers and writers out-of-band.</span></span>

<span data-ttu-id="044bd-176">Il terzo e il quarto esempio mostrano come serializzare e deserializzare dati usando i file contenitore di oggetti Avro.</span><span class="sxs-lookup"><span data-stu-id="044bd-176">The third and fourth examples show how to serialize and deserialize data by using the Avro object container files.</span></span> <span data-ttu-id="044bd-177">Quando i dati vengono archiviati in un file contenitore di Avro, il relativo schema verrà sempre archiviato assieme ad essi, perché per completare la deserializzazione è necessario condividere lo schema.</span><span class="sxs-lookup"><span data-stu-id="044bd-177">When data is stored in an Avro container file, its schema is always stored with it because the schema must be shared for deserialization.</span></span>

<span data-ttu-id="044bd-178">È possibile scaricare i primi quattro esempi dal sito degli <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">esempi di codice di Azure</a> .</span><span class="sxs-lookup"><span data-stu-id="044bd-178">The sample containing the first four examples can be downloaded from the <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="044bd-179">Il quinto esempio mostra come usare un codec di compressione personalizzato per i file contenitore di oggetti Avro.</span><span class="sxs-lookup"><span data-stu-id="044bd-179">The fifth example shows how to use a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="044bd-180">È possibile scaricare questo esempio di codice dal sito degli <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">esempi di codice di Azure</a> .</span><span class="sxs-lookup"><span data-stu-id="044bd-180">A sample containing the code for this example can be downloaded from the <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="044bd-181">Il sesto esempio mostra come usare la serializzazione Avro per caricare dati nell'archivio BLOB di Azure e quindi analizzarli usando Hive con un cluster HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="044bd-181">The sixth sample shows how to use Avro serialization to upload data to Azure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="044bd-182">È possibile scaricare questo esempio dal sito degli <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">esempi di codice di Azure</a> .</span><span class="sxs-lookup"><span data-stu-id="044bd-182">It can be downloaded from the <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="044bd-183">Di seguito sono riportati i sei esempi contenuti nel presente argomento:</span><span class="sxs-lookup"><span data-stu-id="044bd-183">Here are links to the six samples discussed in the topic:</span></span>

* <span data-ttu-id="044bd-184"><a href="#Scenario1">**Serializzazione con reflection**</a>: lo schema JSON per i tipi da serializzare viene compilato automaticamente dagli attributi del contratto dati.</span><span class="sxs-lookup"><span data-stu-id="044bd-184"><a href="#Scenario1">**Serialization with reflection**</a> - The JSON schema for types to be serialized is automatically built from the data contract attributes.</span></span>
* <span data-ttu-id="044bd-185"><a href="#Scenario2">**Serializzazione con un record generico**</a>: lo schema JSON viene specificato in modo esplicito in un record quando non è disponibile alcun tipo .NET per la reflection.</span><span class="sxs-lookup"><span data-stu-id="044bd-185"><a href="#Scenario2">**Serialization with generic record**</a> - The JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="044bd-186"><a href="#Scenario3">**Serializzazione mediante file contenitore di oggetti con reflection**</a>: lo schema JSON viene compilato automaticamente e condiviso insieme ai dati serializzati mediante un file contenitore di oggetti Avro.</span><span class="sxs-lookup"><span data-stu-id="044bd-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - The JSON schema is automatically built and shared together with the serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="044bd-187"><a href="#Scenario4">**Serializzazione mediante file contenitore di oggetti con un record generico**</a>: lo schema JSON viene specificato in modo esplicito prima della serializzazione e viene condiviso insieme ai dati mediante un file contenitore di oggetti Avro.</span><span class="sxs-lookup"><span data-stu-id="044bd-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - The JSON schema is explicitly specified before the serialization and shared together with the data via an Avro object container file.</span></span>
* <span data-ttu-id="044bd-188"><a href="#Scenario5">**Serializzazione mediante file contenitore di oggetti con un codec di compressione personalizzato**</a>: questo esempio mostra come creare un file contenitore di oggetti Avro con un'implementazione .NET personalizzata del codec di compressione dati Deflate.</span><span class="sxs-lookup"><span data-stu-id="044bd-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - The example shows how to create an Avro object container file with a customized .NET implementation of the Deflate data compression codec.</span></span>
* <span data-ttu-id="044bd-189"><a href="#Scenario6">**Uso di Avro per caricare dati per il servizio Microsoft Azure HDInsight**</a>: questo esempio mostra il modo in cui la serializzazione Avro interagisce con il servizio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="044bd-189"><a href="#Scenario6">**Using Avro to upload data for the Microsoft Azure HDInsight service**</a> - The example illustrates how Avro serialization interacts with the HDInsight service.</span></span> <span data-ttu-id="044bd-190">Per eseguire questo esempio, sono necessari una sottoscrizione di Azure attiva e l'accesso a un cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="044bd-190">An active Azure subscription and access to an Azure HDInsight cluster are required to run this example.</span></span>

## <span data-ttu-id="044bd-191"><a name="Scenario1"></a>Esempio 1: Serializzazione con reflection</span><span class="sxs-lookup"><span data-stu-id="044bd-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="044bd-192">Lo schema JSON per i tipi può essere automaticamente compilato dalla libreria Microsoft Avro mediante reflection dagli attributi del contratto dati degli oggetti C# da serializzare.</span><span class="sxs-lookup"><span data-stu-id="044bd-192">The JSON schema for the types can be automatically built by the Microsoft Avro Library via reflection from the data contract attributes of the C# objects to be serialized.</span></span> <span data-ttu-id="044bd-193">La libreria Microsoft Avro crea un oggetto [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) per identificare i campi da serializzare.</span><span class="sxs-lookup"><span data-stu-id="044bd-193">The Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) to identify the fields to be serialized.</span></span>

<span data-ttu-id="044bd-194">In questo esempio vengono serializzati oggetti, in particolare una classe **SensorData** con uno struct **Location** del membro, in un flusso di memoria che viene deserializzato a sua volta.</span><span class="sxs-lookup"><span data-stu-id="044bd-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized to a memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="044bd-195">Il risultato viene quindi confrontato con l'istanza iniziale per confermare che l'oggetto **SensorData** recuperato sia identico all'originale.</span><span class="sxs-lookup"><span data-stu-id="044bd-195">The result is then compared to the initial instance to confirm that the **SensorData** object recovered is identical to the original.</span></span>

<span data-ttu-id="044bd-196">Si suppone che lo schema in questo esempio venga condiviso tra lettore e writer, in modo che il formato del contenitore di oggetti di Avro non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="044bd-196">The schema in this example is assumed to be shared between the readers and writers, so the Avro object container format is not required.</span></span> <span data-ttu-id="044bd-197">Per un esempio di come serializzare e deserializzare i dati nei buffer di memoria mediante reflection con il formato di contenitore di oggetti quando lo schema deve essere condiviso con i dati, vedere <a href="#Scenario3">Serializzazione mediante file contenitore di oggetti con reflection</a>.</span><span class="sxs-lookup"><span data-stu-id="044bd-197">For an example of how to serialize and deserialize data into memory buffers by using reflection with the object container format when the schema must be shared with the data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize the data to the specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from the stream and cast it to the same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches the original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization to memory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="044bd-198">Esempio 2: Serializzazione con un record generico</span><span class="sxs-lookup"><span data-stu-id="044bd-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="044bd-199">È possibile specificare in modo esplicito uno schema JSON in un record generico quando non è possibile usare la reflection perché i dati non possono essere rappresentati attraverso classi .NET con un contratto dati.</span><span class="sxs-lookup"><span data-stu-id="044bd-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because the data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="044bd-200">Questo metodo risulta più lento rispetto all'uso della reflection.</span><span class="sxs-lookup"><span data-stu-id="044bd-200">This method is slower than using reflection.</span></span> <span data-ttu-id="044bd-201">In questi casi, lo schema per i dati può anche essere dinamico, ovvero non noto in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="044bd-201">In such cases, the schema for the data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="044bd-202">I dati rappresentati come file con valori delimitati da virgole (con estensione csv) il cui schema è sconosciuto fino alla sua trasformazione in formato Avro in fase di esecuzione costituiscono un esempio di questo tipo di scenario dinamico.</span><span class="sxs-lookup"><span data-stu-id="044bd-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed to the Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="044bd-203">Questo esempio mostra come creare e usare un oggetto [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) per specificare in modo esplicito uno schema JSON, come inserirvi i dati e quindi come serializzarlo e deserializzarlo.</span><span class="sxs-lookup"><span data-stu-id="044bd-203">This example shows how to create and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) to explicitly specify a JSON schema, how to populate it with the data, and then how to serialize and deserialize it.</span></span> <span data-ttu-id="044bd-204">Il risultato viene quindi confrontato con l'istanza iniziale per confermare che il record recuperato sia identico all'originale.</span><span class="sxs-lookup"><span data-stu-id="044bd-204">The result is then compared to the initial instance to confirm that the record recovered is identical to the original.</span></span>

<span data-ttu-id="044bd-205">Si suppone che lo schema in questo esempio venga condiviso tra lettore e writer, in modo che il formato del contenitore di oggetti di Avro non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="044bd-205">The schema in this example is assumed to be shared between the readers and writers, so the Avro object container format is not required.</span></span> <span data-ttu-id="044bd-206">Per un esempio di come serializzare e deserializzare i dati nei buffer di memoria usando un record generico con il formato di contenitore di oggetti quando lo schema deve essere incluso con i dati serializzati, vedere l'esempio <a href="#Scenario4">Serializzazione mediante file contenitore di oggetti con un record generico</a>.</span><span class="sxs-lookup"><span data-stu-id="044bd-206">For an example of how to serialize and deserialize data into memory buffers by using a generic record with the object container format when the schema must be included with the serialized data, see the <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //the usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with the schema explicitly defined in JSON.
        //All serialized data should be mapped to the fields of the generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining the Schema and creating Sample Data Set...");

            //Define the schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on the schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record to represent the data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize the data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize the data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify the results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization to memory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key to exit.");
            Console.Read();
        }
    }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining the Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="044bd-207">Esempio 3: serializzazione mediante file contenitore di oggetti e serializzazione con reflection</span><span class="sxs-lookup"><span data-stu-id="044bd-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="044bd-208">Questo esempio è simile allo scenario descritto nel <a href="#Scenario1">primo esempio</a>, in cui lo schema viene specificato in modo implicito mediante reflection.</span><span class="sxs-lookup"><span data-stu-id="044bd-208">This example is similar to the scenario in the <a href="#Scenario1"> first example</a>, where the schema is implicitly specified with reflection.</span></span> <span data-ttu-id="044bd-209">La differenza è che in questo esempio non si presuppone che lo schema sia noto al reader che lo deserializza.</span><span class="sxs-lookup"><span data-stu-id="044bd-209">The difference is that here, the schema is not assumed to be known to the reader that deserializes it.</span></span> <span data-ttu-id="044bd-210">Gli oggetti **SensorData** da deserializzare e il rispettivo schema specificato in modo implicito vengono archiviati in un file contenitore di oggetti Avro rappresentato dalla classe [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx).</span><span class="sxs-lookup"><span data-stu-id="044bd-210">The **SensorData** objects to be serialized and their implicitly specified schema are stored in an Avro object container file represented by the [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="044bd-211">In questo esempio i dati vengono serializzati con [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) e deserializzati con [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span><span class="sxs-lookup"><span data-stu-id="044bd-211">The data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="044bd-212">Il risultato viene quindi confrontato con le istanze iniziali per verificare l'identità.</span><span class="sxs-lookup"><span data-stu-id="044bd-212">The result then is compared to the initial instances to ensure identity.</span></span>

<span data-ttu-id="044bd-213">I dati nel file contenitore di oggetti vengono compressi mediante il codec di compressione [**Deflate**][deflate-100] predefinito di .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="044bd-213">The data in the object container file is compressed via the default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="044bd-214">Vedere il <a href="#Scenario5">quinto esempio</a> in questo argomento per informazioni su come usare una versione superiore e più recente del codec di compressione [**Deflate**][deflate-110] disponibile in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="044bd-214">See the <a href="#Scenario5"> fifth example</a> in this topic to learn how to use a more recent and superior version of the [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes the sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with the Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data to file.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Data is compressed using the Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize the data to stream by using the sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream to file
                    Console.WriteLine("Saving serialized data to file...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches the original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete the file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream to a new file with the given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using the given path to a memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection to Avro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="044bd-215">Esempio 4: serializzazione mediante file contenitore di oggetti e serializzazione con un record generico</span><span class="sxs-lookup"><span data-stu-id="044bd-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="044bd-216">Questo esempio è simile allo scenario descritto nel <a href="#Scenario2">secondo esempio</a>, in cui lo schema viene specificato in modo esplicito con JSON.</span><span class="sxs-lookup"><span data-stu-id="044bd-216">This example is similar to the scenario in the <a href="#Scenario2"> second example</a>, where the schema is explicitly specified with JSON.</span></span> <span data-ttu-id="044bd-217">La differenza è che in questo esempio non si presuppone che lo schema sia noto al reader che lo deserializza.</span><span class="sxs-lookup"><span data-stu-id="044bd-217">The difference is that here, the schema is not assumed to be known to the reader that deserializes it.</span></span>

<span data-ttu-id="044bd-218">Il set di dati di test viene raccolto in un elenco di oggetti [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) usando uno schema JSON definito in modo esplicito, quindi archiviato in un file contenitore di oggetti rappresentato dalla classe [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx).</span><span class="sxs-lookup"><span data-stu-id="044bd-218">The test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by the [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="044bd-219">Questo file contenitore crea un writer che viene usato per serializzare i dati, non compressi, in un flusso di memoria che verrà quindi salvato su file.</span><span class="sxs-lookup"><span data-stu-id="044bd-219">This container file creates a writer that is used to serialize the data, uncompressed, to a memory stream that is then saved to a file.</span></span> <span data-ttu-id="044bd-220">Il parametro [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) usato per creare il reader specifica che questi dati non sono compressi.</span><span class="sxs-lookup"><span data-stu-id="044bd-220">The [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating the reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="044bd-221">I dati vengono quindi letti dal file e deserializzati in una raccolta di oggetti,</span><span class="sxs-lookup"><span data-stu-id="044bd-221">The data is then read from the file and deserialized into a collection of objects.</span></span> <span data-ttu-id="044bd-222">che viene quindi confrontata con l'elenco iniziale di record Avro per confermare che sono identici.</span><span class="sxs-lookup"><span data-stu-id="044bd-222">This collection is compared to the initial list of Avro records to confirm that they are identical.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining the Schema and creating Sample Data Set...");

                //Define the schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on the schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record to represent the data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data to file.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize the data to stream by using the sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data to file...");

                    //Save stream to file
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing the data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify the results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete the file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream to a new file with the given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using the given path to a memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using the given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of the AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record to Avro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining the Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="044bd-223">Esempio 5: serializzazione mediante file contenitore di oggetti con un codec di compressione personalizzato</span><span class="sxs-lookup"><span data-stu-id="044bd-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="044bd-224">Il quinto esempio mostra come usare un codec di compressione personalizzato per i file contenitore di oggetti Avro.</span><span class="sxs-lookup"><span data-stu-id="044bd-224">The fifth example shows how to use a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="044bd-225">È possibile scaricare questo esempio di codice dal sito degli [esempi di codice di Azure](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) .</span><span class="sxs-lookup"><span data-stu-id="044bd-225">A sample containing the code for this example can be downloaded from the [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="044bd-226">Le [specifiche di Avro](http://avro.apache.org/docs/current/spec.html#Required+Codecs) consentono l'uso di un codec di compressione facoltativo, in aggiunta ai codec predefiniti **Null** e **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="044bd-226">The [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition to **Null** and **Deflate** defaults).</span></span> <span data-ttu-id="044bd-227">In questo esempio non viene implementato un codec nuovo come Snappy (indicato come codec facoltativo supportato nelle [specifiche di Avro](http://avro.apache.org/docs/current/spec.html#snappy)).</span><span class="sxs-lookup"><span data-stu-id="044bd-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in the [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="044bd-228">L'esempio mostra invece come usare l'implementazione del codec [**Deflate**][deflate-110] di .NET Framework 4.5, che offre un migliore algoritmo di compressione basato sulla libreria di compressione [zlib](http://zlib.net/) rispetto alla versione predefinita di .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="044bd-228">It shows how to use the .NET Framework 4.5 implementation of the [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on the [zlib](http://zlib.net/) compression library than the default .NET Framework 4 version.</span></span>

    //
    // This code needs to be compiled with the parameter Target Framework set as ".NET Framework 4.5"
    // to ensure the desired implementation of the Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are the key ones for data compression.
        //To enable a custom codec, one needs to implement these methods for the required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs to implement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed to be null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define the actual codec class containing the required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory to be used in the reader.
        //It catches the attempt to use "Deflate" and provide  a custom codec.
        //For all other cases, it relies on the base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with the custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related to serialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data to file.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Here the custom codec is introduced. For convenience, the next commented code line shows how to use built-in Deflate.
                    //Note that because the sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize the data to stream using the sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream to file
                    Console.WriteLine("Saving serialized data to file...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment the line below if you want to use built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    //Here the custom codec factory is introduced.
                    //For convenience, the next commented code line shows how to use built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because the sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches the original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete the file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream to a new file with the given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using the given path to a memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection to Avro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.

## <a name="sample-6-using-avro-to-upload-data-for-the-microsoft-azure-hdinsight-service"></a><span data-ttu-id="044bd-229">Esempio 6: uso di Avro per caricare dati per il servizio Microsoft Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="044bd-229">Sample 6: Using Avro to upload data for the Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="044bd-230">Il sesto esempio mostra alcune tecniche di programmazione correlate all'interazione con il servizio Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="044bd-230">The sixth example illustrates some programming techniques related to interacting with the Azure HDInsight service.</span></span> <span data-ttu-id="044bd-231">È possibile scaricare questo esempio di codice dal sito degli [esempi di codice di Azure](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) .</span><span class="sxs-lookup"><span data-stu-id="044bd-231">A sample containing the code for this example can be downloaded from the [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="044bd-232">L'esempio esegue le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="044bd-232">The sample does the following tasks:</span></span>

* <span data-ttu-id="044bd-233">Connessione a un cluster esistente del servizio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="044bd-233">Connects to an existing HDInsight service cluster.</span></span>
* <span data-ttu-id="044bd-234">Serializzazione di diversi file con estensione csv e caricamento dei risultati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="044bd-234">Serializes several CSV files and uploads the result to Azure Blob storage.</span></span> <span data-ttu-id="044bd-235">I file CSV vengono distribuiti insieme all'esempio e rappresentano un estratto dei dati cronologici relativi ai titoli AMEX distribuiti da [Infochimps](http://www.infochimps.com/) per il periodo 1970-2010.</span><span class="sxs-lookup"><span data-stu-id="044bd-235">(The CSV files are distributed together with the sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for the period 1970-2010.</span></span> <span data-ttu-id="044bd-236">L'esempio legge i dati del file CSV, converte i record in istanze della classe **Stock** e quindi li serializza mediante reflection.</span><span class="sxs-lookup"><span data-stu-id="044bd-236">The sample reads CSV file data, converts the records to instances of the **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="044bd-237">Viene creata la definizione di tipo Stock da uno schema JSON tramite l'utilità di generazione del codice della libreria Microsoft Avro.</span><span class="sxs-lookup"><span data-stu-id="044bd-237">Stock type definition is created from a JSON schema via the Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="044bd-238">Viene creata una nuova tabella esterna chiamata **Stocks** in Hive, che viene quindi collegata ai dati caricati nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="044bd-238">Creates a new external table called **Stocks** in Hive, and links it to the data uploaded in the previous step.</span></span>
* <span data-ttu-id="044bd-239">Usando Hive, viene eseguita una query sulla tabella **Stocks** .</span><span class="sxs-lookup"><span data-stu-id="044bd-239">Executes a query by using Hive over the **Stocks** table.</span></span>

<span data-ttu-id="044bd-240">L'esempio esegue inoltre una procedura di pulizia prima e dopo l'esecuzione delle operazioni principali.</span><span class="sxs-lookup"><span data-stu-id="044bd-240">In addition, the sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="044bd-241">Durante la pulizia, tutte le cartelle e i dati BLOB di Azure correlati vengono rimossi e la tabella Hive viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="044bd-241">During the clean-up, all of the related Azure Blob data and folders are removed, and the Hive table is dropped.</span></span> <span data-ttu-id="044bd-242">È anche possibile richiamare la procedura di pulizia dalla riga di comando dell'esempio.</span><span class="sxs-lookup"><span data-stu-id="044bd-242">You can also invoke the clean-up procedure from the sample command line.</span></span>

<span data-ttu-id="044bd-243">Per eseguire questo esempio, è necessario disporre dei prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="044bd-243">The sample has the following prerequisites:</span></span>

* <span data-ttu-id="044bd-244">Una sottoscrizione di Microsoft Azure attiva con il relativo ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="044bd-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="044bd-245">Un certificato di gestione per la sottoscrizione con la chiave privata corrispondente.</span><span class="sxs-lookup"><span data-stu-id="044bd-245">A management certificate for the subscription with the corresponding private key.</span></span> <span data-ttu-id="044bd-246">Il certificato deve essere installato nell'archiviazione privata dell'utente corrente, nel computer usato per eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="044bd-246">The certificate should be installed in the current user private storage on the machine used to run the sample.</span></span>
* <span data-ttu-id="044bd-247">Un cluster HDInsight attivo.</span><span class="sxs-lookup"><span data-stu-id="044bd-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="044bd-248">Un account di archiviazione di Azure collegato al cluster HDInsight dal prerequisito precedente, insieme alla chiave di accesso primaria o secondaria corrispondente.</span><span class="sxs-lookup"><span data-stu-id="044bd-248">An Azure Storage account linked to the HDInsight cluster from the previous prerequisite, together with the corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="044bd-249">Tutte le informazioni dei prerequisiti devono essere immesse nel file di configurazione dell'esempio prima di eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="044bd-249">All of the information from the prerequisites should be entered to the sample configuration file before the sample is run.</span></span> <span data-ttu-id="044bd-250">È possibile procedere in due modi:</span><span class="sxs-lookup"><span data-stu-id="044bd-250">There are two possible ways to do it:</span></span>

* <span data-ttu-id="044bd-251">Modificare il file app.config nella directory radice dell'esempio, quindi compilare l'esempio.</span><span class="sxs-lookup"><span data-stu-id="044bd-251">Edit the app.config file in the sample root directory and then build the sample</span></span>
* <span data-ttu-id="044bd-252">Compilare prima di tutto l'esempio e quindi modificare AvroHDISample.exe.config nella directory di compilazione.</span><span class="sxs-lookup"><span data-stu-id="044bd-252">First build the sample, and then edit AvroHDISample.exe.config in the build directory</span></span>

<span data-ttu-id="044bd-253">In entrambi i casi, tutte le modifiche devono essere apportate nella sezione delle impostazioni **<appSettings>**.</span><span class="sxs-lookup"><span data-stu-id="044bd-253">In both cases, all edits should be done in the **<appSettings>** settings section.</span></span> <span data-ttu-id="044bd-254">Seguire i commenti inclusi nel file.</span><span class="sxs-lookup"><span data-stu-id="044bd-254">Follow the comments in the file.</span></span>
<span data-ttu-id="044bd-255">L'esempio viene eseguito dalla riga di comando mediante il comando seguente (presupponendo che il file ZIP dell'esempio sia stato estratto in C:\AvroHDISample; in caso contrario usare il percorso appropriato):</span><span class="sxs-lookup"><span data-stu-id="044bd-255">The sample is run from the command line by executing the following command (where the .zip file with the sample was assumed to be extracted to C:\AvroHDISample; if otherwise, use the relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="044bd-256">Per pulire il cluster, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="044bd-256">To clean up the cluster, run the following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
