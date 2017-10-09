---
title: aaaSerialize dati in Hadoop - Microsoft Avro Library - Azure | Documenti Microsoft
description: Informazioni su come tooserialize e deserializzare i dati in Hadoop in HDInsight hello Microsoft Avro Library toopersist toomemory, un database o file.
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
ms.openlocfilehash: f364f8e855a54c0fc160e9a106ec8d5b30c6db23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a><span data-ttu-id="4f303-104">Serializzare i dati in Hadoop con hello Microsoft Avro Library</span><span class="sxs-lookup"><span data-stu-id="4f303-104">Serialize data in Hadoop with hello Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="4f303-105">Hello Avro SDK non è più supportata da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4f303-105">hello Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="4f303-106">libreria di Hello è community open source è supportato.</span><span class="sxs-lookup"><span data-stu-id="4f303-106">hello library is open source community supported.</span></span> <span data-ttu-id="4f303-107">le origini per la libreria hello Hello si trovano in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="4f303-107">hello sources for hello library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="4f303-108">Questo argomento viene illustrato come hello toouse [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) oggetti tooserialize e altri dati strutture in flussi toopersist li toomemory, un database o un file.</span><span class="sxs-lookup"><span data-stu-id="4f303-108">This topic shows how toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objects and other data structures into streams toopersist them toomemory, a database, or a file.</span></span> <span data-ttu-id="4f303-109">Viene inoltre illustrato come toodeserialize tali oggetti di toorecover hello originali.</span><span class="sxs-lookup"><span data-stu-id="4f303-109">It also shows how toodeserialize them toorecover hello original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="4f303-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="4f303-110">Apache Avro</span></span>
<span data-ttu-id="4f303-111">Hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implementa hello Apache Avro sistema di serializzazione dei dati per l'ambiente di Microsoft.NET hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-111">hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements hello Apache Avro data serialization system for hello Microsoft.NET environment.</span></span> <span data-ttu-id="4f303-112">Apache Avro offre un formato compatto di interscambio dei dati binari per la serializzazione</span><span class="sxs-lookup"><span data-stu-id="4f303-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="4f303-113">Usa <a href="http://www.json.org" target="_blank">JSON</a> toodefine uno schema indipendente dalla lingua che copra l'interoperabilità di linguaggio.</span><span class="sxs-lookup"><span data-stu-id="4f303-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> toodefine a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="4f303-114">I dati serializzati in un unico linguaggio possono essere letti in un altro linguaggio.</span><span class="sxs-lookup"><span data-stu-id="4f303-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="4f303-115">I formati attualmente supportati sono C, C++, C#, Java, PHP, Python e Ruby.</span><span class="sxs-lookup"><span data-stu-id="4f303-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="4f303-116">Informazioni dettagliate sul formato hello sono reperibile in hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro specifica</a>.</span><span class="sxs-lookup"><span data-stu-id="4f303-116">Detailed information on hello format can be found in hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="4f303-117">Hello Microsoft Avro Library non supporta hello procedura remota (RPC) le chiamate parte di questa specifica.</span><span class="sxs-lookup"><span data-stu-id="4f303-117">hello Microsoft Avro Library does not support hello remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="4f303-118">rappresentazione di Hello serializzato di un oggetto in hello sistema Avro è costituita da due parti: schema e il valore effettivo.</span><span class="sxs-lookup"><span data-stu-id="4f303-118">hello serialized representation of an object in hello Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="4f303-119">schema Avro Hello descrive il modello di dati di indipendente dal linguaggio hello dei dati di hello serializzato con JSON.</span><span class="sxs-lookup"><span data-stu-id="4f303-119">hello Avro schema describes hello language-independent data model of hello serialized data with JSON.</span></span> <span data-ttu-id="4f303-120">È presentato side-by-side con una rappresentazione binaria dei dati.</span><span class="sxs-lookup"><span data-stu-id="4f303-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="4f303-121">Con schema hello separato dalla rappresentazione binaria di hello consente toobe ogni oggetto scritti con alcun sovraccarico per ogni valore, eseguire la serializzazione veloce e hello rappresentazione piccole.</span><span class="sxs-lookup"><span data-stu-id="4f303-121">Having hello schema separate from hello binary representation permits each object toobe written with no per-value overheads, making serialization fast, and hello representation small.</span></span>

## <a name="hello-hadoop-scenario"></a><span data-ttu-id="4f303-122">scenario di Hadoop Hello</span><span class="sxs-lookup"><span data-stu-id="4f303-122">hello Hadoop scenario</span></span>
<span data-ttu-id="4f303-123">formato di serializzazione di Apache Avro Hello è ampiamente utilizzato in Azure HDInsight e altri ambienti di Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4f303-123">hello Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="4f303-124">Avro fornisce un modo pratico di toorepresent strutture di dati complessi all'interno di un processo Hadoop MapReduce.</span><span class="sxs-lookup"><span data-stu-id="4f303-124">Avro provides a convenient way toorepresent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="4f303-125">formato Hello di file Avro (file contenitore di oggetti Avro) è stato progettato toosupport hello distribuita MapReduce modello di programmazione.</span><span class="sxs-lookup"><span data-stu-id="4f303-125">hello format of Avro files (Avro object container file) has been designed toosupport hello distributed MapReduce programming model.</span></span> <span data-ttu-id="4f303-126">funzionalità chiave Hello che abilita la distribuzione di hello è che i file hello "divisibili" nel senso hello che uno può cercare qualsiasi punto in un file e avviare la lettura da un blocco specifico.</span><span class="sxs-lookup"><span data-stu-id="4f303-126">hello key feature that enables hello distribution is that hello files are “splittable” in hello sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="4f303-127">Serializzazione nella libreria Avro</span><span class="sxs-lookup"><span data-stu-id="4f303-127">Serialization in Avro Library</span></span>
<span data-ttu-id="4f303-128">Hello libreria .NET per Avro supporta due tipi di serializzare oggetti in:</span><span class="sxs-lookup"><span data-stu-id="4f303-128">hello .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="4f303-129">**Reflection** -schema JSON hello per i tipi di hello viene automaticamente creato da dati di hello attributi del contratto di toobe di tipi .NET hello serializzato.</span><span class="sxs-lookup"><span data-stu-id="4f303-129">**reflection** - hello JSON schema for hello types is automatically built from hello data contract attributes of hello .NET types toobe serialized.</span></span>
* <span data-ttu-id="4f303-130">**record generico** -schema A JSON è specificato in modo esplicito in un record rappresentato da hello [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) classe se nessun tipo .NET è presenti toodescribe hello lo schema per hello dati toobe serializzato.</span><span class="sxs-lookup"><span data-stu-id="4f303-130">**generic record** - A JSON schema is explicitly specified in a record represented by hello [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present toodescribe hello schema for hello data toobe serialized.</span></span>

<span data-ttu-id="4f303-131">Quando è noto schema dati hello tooboth hello scrittura e lettura del flusso di hello dati hello possono essere inviati senza schema.</span><span class="sxs-lookup"><span data-stu-id="4f303-131">When hello data schema is known tooboth hello writer and reader of hello stream, hello data can be sent without its schema.</span></span> <span data-ttu-id="4f303-132">In casi quando viene utilizzato un file di contenitore di oggetti Avro, hello schema viene archiviato nel file hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-132">In cases when an Avro object container file is used, hello schema is stored within hello file.</span></span> <span data-ttu-id="4f303-133">Altri parametri, ad esempio i codec hello usato per la compressione dei dati, possono essere specificati.</span><span class="sxs-lookup"><span data-stu-id="4f303-133">Other parameters, such as hello codec used for data compression, can be specified.</span></span> <span data-ttu-id="4f303-134">Questi scenari sono descritte in dettaglio e illustrati nella hello esempi di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="4f303-134">These scenarios are outlined in more detail and illustrated in hello following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="4f303-135">Installare la libreria Avro</span><span class="sxs-lookup"><span data-stu-id="4f303-135">Install Avro Library</span></span>
<span data-ttu-id="4f303-136">di seguito Hello sono necessari prima di installare la libreria hello:</span><span class="sxs-lookup"><span data-stu-id="4f303-136">hello following are required before you install hello library:</span></span>

* <span data-ttu-id="4f303-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="4f303-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="4f303-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (versione 6.0.4 o successive)</span><span class="sxs-lookup"><span data-stu-id="4f303-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="4f303-139">Si noti che la dipendenza Newtonsoft.Json.dll hello viene scaricata automaticamente con l'installazione di hello di hello Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="4f303-139">Note that hello Newtonsoft.Json.dll dependency is downloaded automatically with hello installation of hello Microsoft Avro Library.</span></span> <span data-ttu-id="4f303-140">Hello procedura nella seguente sezione hello:</span><span class="sxs-lookup"><span data-stu-id="4f303-140">hello procedure is provided in hello following section:</span></span>

<span data-ttu-id="4f303-141">Hello Microsoft Avro Library viene distribuito come pacchetto NuGet che può essere installato da Visual Studio tramite hello seguente procedura:</span><span class="sxs-lookup"><span data-stu-id="4f303-141">hello Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via hello following procedure:</span></span>

1. <span data-ttu-id="4f303-142">Seleziona hello **progetto** -> scheda **Gestisci pacchetti NuGet...**</span><span class="sxs-lookup"><span data-stu-id="4f303-142">Select hello **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="4f303-143">Ricerca di "Microsoft.Hadoop.Avro" in hello **ricerca Online** casella.</span><span class="sxs-lookup"><span data-stu-id="4f303-143">Search for "Microsoft.Hadoop.Avro" in hello **Search Online** box.</span></span>
3. <span data-ttu-id="4f303-144">Fare clic su hello **installare** accanto troppo**libreria Avro di Microsoft Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4f303-144">Click hello **Install** button next too**Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="4f303-145">Si noti che hello Newtonsoft.Json.dll (> = 6.0.4) dipendenza viene anche scaricata automaticamente con Microsoft Avro Library hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-145">Note that hello Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with hello Microsoft Avro Library.</span></span>

<span data-ttu-id="4f303-146">codice sorgente Microsoft Avro Library Hello è disponibile all'indirizzo [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="4f303-146">hello Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="4f303-147">Compilare schemi tramite la libreria Avro</span><span class="sxs-lookup"><span data-stu-id="4f303-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="4f303-148">Hello Microsoft Avro Library contiene una generazione di codice utilità che consente di creare i tipi c# automaticamente in base alle hello è definito in precedenza lo schema JSON.</span><span class="sxs-lookup"><span data-stu-id="4f303-148">hello Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on hello previously defined JSON schema.</span></span> <span data-ttu-id="4f303-149">utilità per la generazione di codice Hello non viene distribuita come un eseguibile binario, ma è possibile compilare facilmente tramite hello seguente procedura:</span><span class="sxs-lookup"><span data-stu-id="4f303-149">hello code generation utility is not distributed as a binary executable, but can be easily built via hello following procedure:</span></span>

1. <span data-ttu-id="4f303-150">Scaricare il file con estensione zip hello con la versione più recente di hello del codice sorgente di HDInsight SDK da <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK per Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="4f303-150">Download hello .zip file with hello latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="4f303-151">(Fare clic su hello **scaricare** icona, non hello **Scarica** scheda.)</span><span class="sxs-lookup"><span data-stu-id="4f303-151">(Click hello **Download** icon, not hello **Downloads** tab.)</span></span>
2. <span data-ttu-id="4f303-152">Estrarre hello directory tooa HDInsight SDK nel computer di hello con .NET Framework 4 è installato e connesso toohello Internet per scaricare i pacchetti NuGet dipendenze necessarie.</span><span class="sxs-lookup"><span data-stu-id="4f303-152">Extract hello HDInsight SDK tooa directory on hello machine with .NET Framework 4 installed and connected toohello Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="4f303-153">Di seguito, si presuppone che il codice sorgente hello è tooC:\SDK estratti.</span><span class="sxs-lookup"><span data-stu-id="4f303-153">Below, we assume that hello source code is extracted tooC:\SDK.</span></span>
3. <span data-ttu-id="4f303-154">Passare la cartella toohello C:\SDK\src\Microsoft.Hadoop.Avro.Tools ed eseguire build.bat.</span><span class="sxs-lookup"><span data-stu-id="4f303-154">Go toohello folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="4f303-155">(hello chiamate file MSBuild dalla distribuzione di hello 32 bit di .NET Framework hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-155">(hello file calls MSBuild from hello 32-bit distribution of hello .NET Framework.</span></span> <span data-ttu-id="4f303-156">Se si desidera una versione a 64 bit hello toouse, modifica Build. bat seguente hello commenti nel file hello.) Verificare che la compilazione hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="4f303-156">If you would like toouse hello 64-bit version, edit build.bat, following hello comments inside hello file.) Ensure that hello build is successful.</span></span> <span data-ttu-id="4f303-157">In alcuni sistemi MSBuild può generare avvisi,</span><span class="sxs-lookup"><span data-stu-id="4f303-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="4f303-158">Questi avvisi non influiscono utilità hello, purché non siano presenti errori di compilazione.)</span><span class="sxs-lookup"><span data-stu-id="4f303-158">These warnings do not affect hello utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="4f303-159">utilità Hello compilato si trova in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span><span class="sxs-lookup"><span data-stu-id="4f303-159">hello compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="4f303-160">tooget familiarità con la sintassi della riga di comando hello, eseguire comando seguente dalla cartella hello in cui si trova utilità per la generazione di codice hello hello:`Microsoft.Hadoop.Avro.Tools help /c:codegen`</span><span class="sxs-lookup"><span data-stu-id="4f303-160">tooget familiar with hello command-line syntax, execute hello following command from hello folder where hello code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="4f303-161">utilità di hello tootest, è possibile generare classi c# dal file dello schema JSON esempio hello fornito con il codice sorgente hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-161">tootest hello utility, you can generate C# classes from hello sample JSON schema file provided with hello source code.</span></span> <span data-ttu-id="4f303-162">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4f303-162">Execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="4f303-163">Questo dovrebbe tooproduce due file c# nella directory corrente hello: SensorData.cs e Location.cs.</span><span class="sxs-lookup"><span data-stu-id="4f303-163">This is supposed tooproduce two C# files in hello current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="4f303-164">la logica di hello toounderstand utilità per la generazione di codice hello è in uso durante la conversione di tipi tooC # hello JSON schema, vedere hello file GenerationVerification.feature nella C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span><span class="sxs-lookup"><span data-stu-id="4f303-164">toounderstand hello logic that hello code generation utility is using while converting hello JSON schema tooC# types, see hello file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="4f303-165">Spazi dei nomi vengono estratti dallo schema JSON hello, utilizzando la logica di hello descritta nel file hello menzionato nel paragrafo precedente hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-165">Namespaces are extracted from hello JSON schema, using hello logic described in hello file mentioned in hello previous paragraph.</span></span> <span data-ttu-id="4f303-166">Spazi dei nomi estratti dallo schema hello hanno la precedenza su qualsiasi viene fornito con il parametro /n hello hello utilità riga di comando.</span><span class="sxs-lookup"><span data-stu-id="4f303-166">Namespaces extracted from hello schema take precedence over whatever is provided with hello /n parameter in hello utility command line.</span></span> <span data-ttu-id="4f303-167">Se si desidera spazi dei nomi hello toooverride contenuti all'interno dello schema di hello, utilizzare il parametro /nf hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-167">If you want toooverride hello namespaces contained within hello schema, use hello /nf parameter.</span></span> <span data-ttu-id="4f303-168">Ad esempio, di eseguire tutti gli spazi dei nomi hello SampleJSONSchema.avsc toomy.own.nspace, di toochange hello il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="4f303-168">For example, toochange all namespaces from hello SampleJSONSchema.avsc toomy.own.nspace, execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a><span data-ttu-id="4f303-169">Sugli esempi di hello</span><span class="sxs-lookup"><span data-stu-id="4f303-169">About hello samples</span></span>
<span data-ttu-id="4f303-170">Sei esempi forniti in questo argomento vengono illustrati i diversi scenari supportati da Microsoft Avro Library hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-170">Six examples provided in this topic illustrate different scenarios supported by hello Microsoft Avro Library.</span></span> <span data-ttu-id="4f303-171">Hello Microsoft Avro Library è progettato toowork con qualsiasi flusso.</span><span class="sxs-lookup"><span data-stu-id="4f303-171">hello Microsoft Avro Library is designed toowork with any stream.</span></span> <span data-ttu-id="4f303-172">Per semplicità e coerenza, in questi esempi i dati vengono modificati usando flussi di memoria anziché flussi di file o database.</span><span class="sxs-lookup"><span data-stu-id="4f303-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="4f303-173">approccio Hello eseguita in un ambiente di produzione dipende dall'origine dati, i requisiti di scenario esatti hello e volume, vincoli relativi alle prestazioni e altri fattori.</span><span class="sxs-lookup"><span data-stu-id="4f303-173">hello approach taken in a production environment depends on hello exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="4f303-174">Hello come primo mostra due esempi tooserialize e deserializzare i dati nei buffer di flusso di memoria tramite la reflection e record di tipo generico.</span><span class="sxs-lookup"><span data-stu-id="4f303-174">hello first two examples show how tooserialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="4f303-175">Hello dello schema in questi due casi presuppone toobe condivisi tra hello lettori e writer fuori banda.</span><span class="sxs-lookup"><span data-stu-id="4f303-175">hello schema in these two cases is assumed toobe shared between hello readers and writers out-of-band.</span></span>

<span data-ttu-id="4f303-176">Hello terza e quarta esempi viene illustrato come tooserialize e deserializzare i dati utilizzando i file hello Avro oggetto contenitore.</span><span class="sxs-lookup"><span data-stu-id="4f303-176">hello third and fourth examples show how tooserialize and deserialize data by using hello Avro object container files.</span></span> <span data-ttu-id="4f303-177">Quando i dati vengono archiviati in un file contenitore Avro, lo schema viene sempre archiviato con quanto hello schema deve essere condiviso per la deserializzazione.</span><span class="sxs-lookup"><span data-stu-id="4f303-177">When data is stored in an Avro container file, its schema is always stored with it because hello schema must be shared for deserialization.</span></span>

<span data-ttu-id="4f303-178">Hello che contiene l'esempio hello primi quattro esempi possono essere scaricati dal hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure esempi di codice</a> sito.</span><span class="sxs-lookup"><span data-stu-id="4f303-178">hello sample containing hello first four examples can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="4f303-179">Hello quinto esempio viene illustrato come file contenitore dell'oggetto toouse un codec di compressione personalizzata per Avro.</span><span class="sxs-lookup"><span data-stu-id="4f303-179">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="4f303-180">Un esempio che contiene il codice hello per questo esempio può essere scaricato da hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure esempi di codice</a> sito.</span><span class="sxs-lookup"><span data-stu-id="4f303-180">A sample containing hello code for this example can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="4f303-181">esempio di sesto Hello viene illustrato come toouse Avro serializzazione tooupload dati tooAzure nell'archiviazione Blob e analizzarli tramite Hive con un cluster HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="4f303-181">hello sixth sample shows how toouse Avro serialization tooupload data tooAzure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="4f303-182">Può essere scaricato da hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure esempi di codice</a> sito.</span><span class="sxs-lookup"><span data-stu-id="4f303-182">It can be downloaded from hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="4f303-183">Di seguito sono collegamenti descritti nell'argomento hello toohello sei campioni:</span><span class="sxs-lookup"><span data-stu-id="4f303-183">Here are links toohello six samples discussed in hello topic:</span></span>

* <span data-ttu-id="4f303-184"><a href="#Scenario1">**Serializzazione con reflection** </a> -schema JSON hello per toobe tipi serializzati viene automaticamente creato da dati di hello attributi del contratto.</span><span class="sxs-lookup"><span data-stu-id="4f303-184"><a href="#Scenario1">**Serialization with reflection**</a> - hello JSON schema for types toobe serialized is automatically built from hello data contract attributes.</span></span>
* <span data-ttu-id="4f303-185"><a href="#Scenario2">**Serializzazione con record generico** </a> -schema JSON hello è specificato in modo esplicito in un record di alcun tipo .NET non è disponibile per la reflection.</span><span class="sxs-lookup"><span data-stu-id="4f303-185"><a href="#Scenario2">**Serialization with generic record**</a> - hello JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="4f303-186"><a href="#Scenario3">**Serializzazione utilizzando i file oggetto contenitore con reflection** </a> -schema JSON hello viene compilato automaticamente ed è condiviso con dati serializzato hello tramite un file di contenitore di oggetti Avro.</span><span class="sxs-lookup"><span data-stu-id="4f303-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - hello JSON schema is automatically built and shared together with hello serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="4f303-187"><a href="#Scenario4">**Serializzazione utilizzando i file oggetto contenitore con record generico** </a> -schema JSON hello in modo esplicito specificato prima della serializzazione hello e condivisi con i dati di hello tramite un file di contenitore di oggetti Avro.</span><span class="sxs-lookup"><span data-stu-id="4f303-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - hello JSON schema is explicitly specified before hello serialization and shared together with hello data via an Avro object container file.</span></span>
* <span data-ttu-id="4f303-188"><a href="#Scenario5">**Serializzazione utilizzando i file oggetto contenitore con un codec di compressione personalizzata** </a> -hello nell'esempio viene illustrato come un Avro toocreate oggetto file contenitore con un'implementazione personalizzata di .NET del codec di compressione dati hello Deflate.</span><span class="sxs-lookup"><span data-stu-id="4f303-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - hello example shows how toocreate an Avro object container file with a customized .NET implementation of hello Deflate data compression codec.</span></span>
* <span data-ttu-id="4f303-189"><a href="#Scenario6">**Utilizzando i dati di tooupload Avro per il servizio Microsoft Azure HDInsight hello** </a> -esempio hello viene illustrata l'interazione di serializzazione Avro con hello servizio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f303-189"><a href="#Scenario6">**Using Avro tooupload data for hello Microsoft Azure HDInsight service**</a> - hello example illustrates how Avro serialization interacts with hello HDInsight service.</span></span> <span data-ttu-id="4f303-190">Un attiva Azure sottoscrizione e accesso tooan Azure HDInsight cluster sono necessari toorun in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="4f303-190">An active Azure subscription and access tooan Azure HDInsight cluster are required toorun this example.</span></span>

## <span data-ttu-id="4f303-191"><a name="Scenario1"></a>Esempio 1: Serializzazione con reflection</span><span class="sxs-lookup"><span data-stu-id="4f303-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="4f303-192">schema JSON Hello per i tipi di hello può essere automaticamente generato da hello Microsoft Avro Library tramite reflection da dati hello attributi del contratto di hello c# oggetti toobe serializzato.</span><span class="sxs-lookup"><span data-stu-id="4f303-192">hello JSON schema for hello types can be automatically built by hello Microsoft Avro Library via reflection from hello data contract attributes of hello C# objects toobe serialized.</span></span> <span data-ttu-id="4f303-193">Hello Microsoft Avro Library consente di creare un [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello campi toobe serializzato.</span><span class="sxs-lookup"><span data-stu-id="4f303-193">hello Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello fields toobe serialized.</span></span>

<span data-ttu-id="4f303-194">In questo esempio, gli oggetti (un **SensorData** classe con un membro **percorso** struct) vengono serializzati tooa flusso di memoria e il flusso viene a sua volta deserializzato.</span><span class="sxs-lookup"><span data-stu-id="4f303-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized tooa memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="4f303-195">Hello risultato viene quindi confrontato toohello iniziale dell'istanza tooconfirm tale hello **SensorData** oggetto recuperato è identica toohello originale.</span><span class="sxs-lookup"><span data-stu-id="4f303-195">hello result is then compared toohello initial instance tooconfirm that hello **SensorData** object recovered is identical toohello original.</span></span>

<span data-ttu-id="4f303-196">schema di Hello in questo esempio si presuppone che toobe condivisi tra hello lettori e writer, quindi formato contenitore di oggetti Avro hello non è necessario.</span><span class="sxs-lookup"><span data-stu-id="4f303-196">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="4f303-197">Per un esempio di come tooserialize e deserializzare i dati nei buffer di memoria tramite reflection con formato di contenitore oggetto hello quando schema hello deve essere condivisi con i dati di hello, vedere <a href="#Scenario3">serializzazione utilizzando i file oggetto contenitore con reflection</a>.</span><span class="sxs-lookup"><span data-stu-id="4f303-197">For an example of how tooserialize and deserialize data into memory buffers by using reflection with hello object container format when hello schema must be shared with hello data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

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
        //hello usage of Microsoft Avro Library
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

                    //Serialize hello data toohello specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from hello stream and cast it toohello same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches hello original one
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

                //Serialization toomemory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="4f303-198">Esempio 2: Serializzazione con un record generico</span><span class="sxs-lookup"><span data-stu-id="4f303-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="4f303-199">Uno schema JSON può essere specificato in modo esplicito in un record generico quando la reflection non può essere utilizzata perché non è possibile rappresentare dati hello tramite le classi .NET con un contratto dati.</span><span class="sxs-lookup"><span data-stu-id="4f303-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because hello data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="4f303-200">Questo metodo risulta più lento rispetto all'uso della reflection.</span><span class="sxs-lookup"><span data-stu-id="4f303-200">This method is slower than using reflection.</span></span> <span data-ttu-id="4f303-201">In tali casi, lo schema di hello per hello dati può essere dinamico, vale a dire, non è noto in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="4f303-201">In such cases, hello schema for hello data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="4f303-202">Dati rappresentati come valori delimitati da virgole per i file (CSV) il cui schema è sconosciuto fino a quando non viene trasformato il formato Avro toohello in fase di esecuzione è riportato un esempio di questo tipo di scenario dinamico.</span><span class="sxs-lookup"><span data-stu-id="4f303-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed toohello Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="4f303-203">Questo esempio viene illustrato come toocreate e utilizzare un [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly specificare uno schema JSON, come toopopulate con dati hello e come quindi tooserialize e deserializzarlo.</span><span class="sxs-lookup"><span data-stu-id="4f303-203">This example shows how toocreate and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly specify a JSON schema, how toopopulate it with hello data, and then how tooserialize and deserialize it.</span></span> <span data-ttu-id="4f303-204">Hello risultato viene confrontato toohello tooconfirm di istanze iniziale che hello record recuperato è identica toohello originale.</span><span class="sxs-lookup"><span data-stu-id="4f303-204">hello result is then compared toohello initial instance tooconfirm that hello record recovered is identical toohello original.</span></span>

<span data-ttu-id="4f303-205">schema di Hello in questo esempio si presuppone che toobe condivisi tra hello lettori e writer, quindi formato contenitore di oggetti Avro hello non è necessario.</span><span class="sxs-lookup"><span data-stu-id="4f303-205">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="4f303-206">Per un esempio di come tooserialize e deserializzare i dati nei buffer di memoria usando un record generico con il formato di contenitore oggetto hello quando schema hello deve essere incluso con i dati serializzato hello, vedere hello <a href="#Scenario4">serializzazione utilizzando contenitore di oggetti i file con record generico</a> esempio.</span><span class="sxs-lookup"><span data-stu-id="4f303-206">For an example of how tooserialize and deserialize data into memory buffers by using a generic record with hello object container format when hello schema must be included with hello serialized data, see hello <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

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
    //hello usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with hello schema explicitly defined in JSON.
        //All serialized data should be mapped toohello fields of hello generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

            //Define hello schema in JSON
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

            //Create a generic serializer based on hello schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record toorepresent hello data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize hello data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize hello data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify hello results
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

            //Serialization toomemory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key tooexit.");
            Console.Read();
        }
    }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="4f303-207">Esempio 3: serializzazione mediante file contenitore di oggetti e serializzazione con reflection</span><span class="sxs-lookup"><span data-stu-id="4f303-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="4f303-208">Questo esempio è simile scenario toohello in hello <a href="#Scenario1"> primo esempio</a>, in cui schema hello è specificato in modo implicito tramite la reflection.</span><span class="sxs-lookup"><span data-stu-id="4f303-208">This example is similar toohello scenario in hello <a href="#Scenario1"> first example</a>, where hello schema is implicitly specified with reflection.</span></span> <span data-ttu-id="4f303-209">Hello differenza è che in questo caso, schema hello non viene considerato come toobe lettore toohello che deserializza noto.</span><span class="sxs-lookup"><span data-stu-id="4f303-209">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span> <span data-ttu-id="4f303-210">Hello **SensorData** toobe oggetti serializzati e lo schema specificato in modo implicito vengono archiviati in un file di contenitore di oggetti Avro rappresentato da hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="4f303-210">hello **SensorData** objects toobe serialized and their implicitly specified schema are stored in an Avro object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="4f303-211">in questo esempio con i dati di Hello vengono serializzati [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) e deserializzato con [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f303-211">hello data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="4f303-212">Hello risulta quindi confrontati toohello istanze iniziale tooensure identità.</span><span class="sxs-lookup"><span data-stu-id="4f303-212">hello result then is compared toohello initial instances tooensure identity.</span></span>

<span data-ttu-id="4f303-213">Hello in hello oggetto dati file contenitore è compresso tramite predefinito hello [ **Deflate** ] [ deflate-100] codec di compressione da .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="4f303-213">hello data in hello object container file is compressed via hello default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="4f303-214">Vedere hello <a href="#Scenario5"> quinto esempio</a> in toolearn in questo argomento come una versione più recente e superiore di hello toouse [ **Deflate** ] [ deflate-110] compressione codec disponibili in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="4f303-214">See hello <a href="#Scenario5"> fifth example</a> in this topic toolearn how toouse a more recent and superior version of hello [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

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
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes hello sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello Deflate codec.
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

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is compressed using hello Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
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

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
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

                //Delete hello file
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

            //Saving memory stream tooa new file with hello given path
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
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
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

            //Reading a file content by using hello given path tooa memory stream
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
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
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
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
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

                //Serialization using reflection tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="4f303-215">Esempio 4: serializzazione mediante file contenitore di oggetti e serializzazione con un record generico</span><span class="sxs-lookup"><span data-stu-id="4f303-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="4f303-216">Questo esempio è simile scenario toohello in hello <a href="#Scenario2"> secondo esempio</a>, in schema di hello è specificato in modo esplicito con JSON.</span><span class="sxs-lookup"><span data-stu-id="4f303-216">This example is similar toohello scenario in hello <a href="#Scenario2"> second example</a>, where hello schema is explicitly specified with JSON.</span></span> <span data-ttu-id="4f303-217">Hello differenza è che in questo caso, schema hello non viene considerato come toobe lettore toohello che deserializza noto.</span><span class="sxs-lookup"><span data-stu-id="4f303-217">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span>

<span data-ttu-id="4f303-218">Hello set di dati di test vengono raccolti in un elenco di [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) oggetti tramite uno schema definito in modo esplicito di JSON e quindi archiviati in un file contenitore oggetto rappresentato da hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="4f303-218">hello test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="4f303-219">Questo file contenitore crea un writer che sono utilizzati tooserialize hello dati, non compressi, flusso di memoria tooa che viene quindi salvato tooa file.</span><span class="sxs-lookup"><span data-stu-id="4f303-219">This container file creates a writer that is used tooserialize hello data, uncompressed, tooa memory stream that is then saved tooa file.</span></span> <span data-ttu-id="4f303-220">Hello [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parametro utilizzato per creare il lettore di hello specifica che i dati non sono compressi.</span><span class="sxs-lookup"><span data-stu-id="4f303-220">hello [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating hello reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="4f303-221">dati Hello viene quindi in grado di leggere dal file hello e deserializzati in una raccolta di oggetti.</span><span class="sxs-lookup"><span data-stu-id="4f303-221">hello data is then read from hello file and deserialized into a collection of objects.</span></span> <span data-ttu-id="4f303-222">Questa raccolta è toohello confrontati elenco iniziale di tooconfirm record Avro che siano identici.</span><span class="sxs-lookup"><span data-stu-id="4f303-222">This collection is compared toohello initial list of Avro records tooconfirm that they are identical.</span></span>

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
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

                //Define hello schema in JSON
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

                //Create a generic serializer based on hello schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record toorepresent hello data
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

                //Serializing and saving data toofile.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data toofile...");

                    //Save stream toofile
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing hello data.
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

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify hello results
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

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream tooa new file with hello given path
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
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
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

            //Reading a file content by using hello given path tooa memory stream
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
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using hello given path
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
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
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

                //Create an instance of hello AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="4f303-223">Esempio 5: serializzazione mediante file contenitore di oggetti con un codec di compressione personalizzato</span><span class="sxs-lookup"><span data-stu-id="4f303-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="4f303-224">Hello quinto esempio viene illustrato come file contenitore dell'oggetto toouse un codec di compressione personalizzata per Avro.</span><span class="sxs-lookup"><span data-stu-id="4f303-224">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="4f303-225">Un esempio che contiene il codice hello per questo esempio può essere scaricato da hello [Azure esempi di codice](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) sito.</span><span class="sxs-lookup"><span data-stu-id="4f303-225">A sample containing hello code for this example can be downloaded from hello [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="4f303-226">Hello [Avro specifica](http://avro.apache.org/docs/current/spec.html#Required+Codecs) consente l'utilizzo di un codec di compressione facoltativo (inoltre troppo**Null** e **Deflate** impostazioni predefinite).</span><span class="sxs-lookup"><span data-stu-id="4f303-226">hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition too**Null** and **Deflate** defaults).</span></span> <span data-ttu-id="4f303-227">In questo esempio non implementa un nuovo codec, ad esempio Snappy (indicato come un codec supportato facoltativo in hello [Avro specifica](http://avro.apache.org/docs/current/spec.html#snappy)).</span><span class="sxs-lookup"><span data-stu-id="4f303-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="4f303-228">Viene illustrato come toouse hello implementazione di .NET Framework 4.5 di hello [ **Deflate** ] [ deflate-110] codec, che fornisce un algoritmo di compressione migliore in base a hello [zlib](http://zlib.net/) libreria di compressione di una versione di .NET Framework 4 hello predefinita.</span><span class="sxs-lookup"><span data-stu-id="4f303-228">It shows how toouse hello .NET Framework 4.5 implementation of hello [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on hello [zlib](http://zlib.net/) compression library than hello default .NET Framework 4 version.</span></span>

    //
    // This code needs toobe compiled with hello parameter Target Framework set as ".NET Framework 4.5"
    // tooensure hello desired implementation of hello Deflate compression algorithm is used.
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
        //which are hello key ones for data compression.
        //tooenable a custom codec, one needs tooimplement these methods for hello required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs tooimplement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed toobe null.");

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
        //Define hello actual codec class containing hello required methods for manipulating streams:
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
        //Define modified codec factory toobe used in hello reader.
        //It catches hello attempt toouse "Deflate" and provide  a custom codec.
        //For all other cases, it relies on hello base class (CodecFactory).
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
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related tooserialization, deserialization and
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

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Here hello custom codec is introduced. For convenience, hello next commented code line shows how toouse built-in Deflate.
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
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

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment hello line below if you want toouse built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    //Here hello custom codec factory is introduced.
                    //For convenience, hello next commented code line shows how toouse built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
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

                //Delete hello file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
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
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
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

            //Reading file content by using hello given path tooa memory stream
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
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
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
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
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

                //Serialization using reflection tooAvro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a><span data-ttu-id="4f303-229">Esempio 6: Utilizzo di dati di tooupload Avro per hello servizio Microsoft Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f303-229">Sample 6: Using Avro tooupload data for hello Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="4f303-230">esempio di sesto Hello illustra alcuni toointeracting correlati tecniche programmazione con il servizio di Azure HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-230">hello sixth example illustrates some programming techniques related toointeracting with hello Azure HDInsight service.</span></span> <span data-ttu-id="4f303-231">Un esempio che contiene il codice hello per questo esempio può essere scaricato da hello [Azure esempi di codice](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) sito.</span><span class="sxs-lookup"><span data-stu-id="4f303-231">A sample containing hello code for this example can be downloaded from hello [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="4f303-232">esempio Hello hello quanto segue:</span><span class="sxs-lookup"><span data-stu-id="4f303-232">hello sample does hello following tasks:</span></span>

* <span data-ttu-id="4f303-233">Si connette tooan cluster del servizio HDInsight esistente.</span><span class="sxs-lookup"><span data-stu-id="4f303-233">Connects tooan existing HDInsight service cluster.</span></span>
* <span data-ttu-id="4f303-234">Serializza i diversi file CSV e il caricamento di archiviazione Blob di hello risultato tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4f303-234">Serializes several CSV files and uploads hello result tooAzure Blob storage.</span></span> <span data-ttu-id="4f303-235">(file CSV hello distribuiti insieme: esempio hello e rappresentano un estratto i dati cronologici AMEX Stock distribuiti da [Infochimps](http://www.infochimps.com/) per il periodo di hello 1970-2010.</span><span class="sxs-lookup"><span data-stu-id="4f303-235">(hello CSV files are distributed together with hello sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for hello period 1970-2010.</span></span> <span data-ttu-id="4f303-236">esempio Hello legge i dati di file CSV, converte hello tooinstances record di hello **Stock** classe e quindi li serializza tramite reflection.</span><span class="sxs-lookup"><span data-stu-id="4f303-236">hello sample reads CSV file data, converts hello records tooinstances of hello **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="4f303-237">Definizione di tipo azionario viene creato da uno schema JSON tramite hello utilità per la generazione di codice Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="4f303-237">Stock type definition is created from a JSON schema via hello Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="4f303-238">Crea una nuova tabella esterna denominata **scorte** nell'Hive e lo collega toohello dati caricati nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-238">Creates a new external table called **Stocks** in Hive, and links it toohello data uploaded in hello previous step.</span></span>
* <span data-ttu-id="4f303-239">Esegue una query Hive tramite hello **scorte** tabella.</span><span class="sxs-lookup"><span data-stu-id="4f303-239">Executes a query by using Hive over hello **Stocks** table.</span></span>

<span data-ttu-id="4f303-240">Esempio hello, inoltre, esegue una procedura di pulizia prima e dopo le operazioni principali.</span><span class="sxs-lookup"><span data-stu-id="4f303-240">In addition, hello sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="4f303-241">Durante hello pulizia tutti hello relative cartelle e i dati Blob di Azure vengono rimossi tabella Hive hello viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="4f303-241">During hello clean-up, all of hello related Azure Blob data and folders are removed, and hello Hive table is dropped.</span></span> <span data-ttu-id="4f303-242">È inoltre possibile richiamare una stored procedure di pulizia hello dalla riga di comando di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-242">You can also invoke hello clean-up procedure from hello sample command line.</span></span>

<span data-ttu-id="4f303-243">esempio Hello è hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="4f303-243">hello sample has hello following prerequisites:</span></span>

* <span data-ttu-id="4f303-244">Una sottoscrizione di Microsoft Azure attiva con il relativo ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4f303-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="4f303-245">Un certificato di gestione per la sottoscrizione di hello con chiave privata corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-245">A management certificate for hello subscription with hello corresponding private key.</span></span> <span data-ttu-id="4f303-246">Hello certificato deve essere installato in hello corrente utente privato archiviazione nel computer utilizzato hello toorun: esempio hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-246">hello certificate should be installed in hello current user private storage on hello machine used toorun hello sample.</span></span>
* <span data-ttu-id="4f303-247">Un cluster HDInsight attivo.</span><span class="sxs-lookup"><span data-stu-id="4f303-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="4f303-248">Un account di archiviazione di Azure collegati cluster HDInsight toohello da prerequisito precedente hello, con chiave di accesso primaria o secondaria corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-248">An Azure Storage account linked toohello HDInsight cluster from hello previous prerequisite, together with hello corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="4f303-249">Le informazioni di hello dai prerequisiti hello deve essere immesso toohello file di configurazione di esempio prima di eseguita l'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-249">All of hello information from hello prerequisites should be entered toohello sample configuration file before hello sample is run.</span></span> <span data-ttu-id="4f303-250">Esistono due modi possibili toodo è:</span><span class="sxs-lookup"><span data-stu-id="4f303-250">There are two possible ways toodo it:</span></span>

* <span data-ttu-id="4f303-251">Modificare il file app. config hello nella directory radice di esempio hello e quindi compilare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="4f303-251">Edit hello app.config file in hello sample root directory and then build hello sample</span></span>
* <span data-ttu-id="4f303-252">Innanzitutto compilare l'esempio hello e quindi modificare AvroHDISample.exe.config nella directory di compilazione hello</span><span class="sxs-lookup"><span data-stu-id="4f303-252">First build hello sample, and then edit AvroHDISample.exe.config in hello build directory</span></span>

<span data-ttu-id="4f303-253">In entrambi i casi, è necessario eseguire tutte le modifiche in hello  **<appSettings>**  sezione Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="4f303-253">In both cases, all edits should be done in hello **<appSettings>** settings section.</span></span> <span data-ttu-id="4f303-254">Seguire i commenti di hello nel file hello.</span><span class="sxs-lookup"><span data-stu-id="4f303-254">Follow hello comments in hello file.</span></span>
<span data-ttu-id="4f303-255">Hello esempio viene eseguito dalla riga di comando hello eseguendo hello comando seguente (dove hello file ZIP con l'esempio hello presupposto tooC:\AvroHDISample toobe estratti; se in caso contrario, utilizzare hello rilevanti percorso file):</span><span class="sxs-lookup"><span data-stu-id="4f303-255">hello sample is run from hello command line by executing hello following command (where hello .zip file with hello sample was assumed toobe extracted tooC:\AvroHDISample; if otherwise, use hello relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="4f303-256">tooclean di cluster hello, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4f303-256">tooclean up hello cluster, run hello following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
