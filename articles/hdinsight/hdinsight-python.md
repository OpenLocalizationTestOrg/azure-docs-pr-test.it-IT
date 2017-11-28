---
title: funzione definita dall'utente con Apache Hive e Pig - Azure HDInsight aaaPython | Documenti Microsoft
description: Informazioni su come stack di chiamate toouse Python utente definite funzioni (UDF) dall'Hive e Pig in HDInsight, hello tecnologia di Hadoop su Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 26d8160cc6ed7fc22c3f06f7c1c9954c224b2366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="1c8a6-103">Usare le funzioni definite dall'utente di Python (UDF) con Hive e Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1c8a6-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="1c8a6-104">Informazioni su come toouse Python definito dall'utente (UDF) di funzioni con Apache Hive e Pig in Hadoop in HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-104">Learn how toouse Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="1c8a6-105"><a name="python"></a>Python in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1c8a6-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="1c8a6-106">Python 2.7 viene installato per impostazione predefinita in HDInsight 3.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="1c8a6-107">Apache Hive può essere usato con questa versione di Python per l'elaborazione di flussi.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="1c8a6-108">L'elaborazione di flusso Usa STDOUT e STDIN dati toopass tra Hive e hello funzione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-108">Stream processing uses STDOUT and STDIN toopass data between Hive and hello UDF.</span></span>

<span data-ttu-id="1c8a6-109">HDInsight include anche Jython, un'implementazione di Python scritta in Java.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="1c8a6-110">Jython viene eseguito direttamente sulla macchina virtuale Java hello e non utilizzare il flusso.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-110">Jython runs directly on hello Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="1c8a6-111">Jython è hello consigliato interprete Python quando si usa Python con Pig.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-111">Jython is hello recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="1c8a6-112">passaggi di Hello in questo documento si hello seguenti presupposti:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-112">hello steps in this document make hello following assumptions:</span></span> 
>
> * <span data-ttu-id="1c8a6-113">Script Python hello è creare nell'ambiente di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-113">You create hello Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="1c8a6-114">Caricare tooHDInsight script hello utilizzando entrambi hello `scp` comando da una sessione Bash locale o hello fornito uno script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-114">You upload hello scripts tooHDInsight using either hello `scp` command from a local Bash session or hello provided PowerShell script.</span></span>
>
> <span data-ttu-id="1c8a6-115">Se si desidera hello toouse [Shell di Cloud di Azure (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) anteprima toowork con HDInsight, è necessario:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-115">If you want toouse hello [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview toowork with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="1c8a6-116">Creare script hello all'interno di ambiente della shell hello cloud.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-116">Create hello scripts inside hello cloud shell environment.</span></span>
> * <span data-ttu-id="1c8a6-117">Utilizzare `scp` file hello tooupload hello cloud tooHDInsight shell.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-117">Use `scp` tooupload hello files from hello cloud shell tooHDInsight.</span></span>
> * <span data-ttu-id="1c8a6-118">Utilizzare `ssh` da hello cloud shell tooconnect tooHDInsight ed esempi di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-118">Use `ssh` from hello cloud shell tooconnect tooHDInsight and run hello examples.</span></span>

## <span data-ttu-id="1c8a6-119"><a name="hivepython"></a>UDF di Hive</span><span class="sxs-lookup"><span data-stu-id="1c8a6-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="1c8a6-120">Python può essere utilizzato come una funzione definita dall'utente dall'Hive tramite HiveQL hello `TRANSFORM` istruzione.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-120">Python can be used as a UDF from Hive through hello HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="1c8a6-121">Ad esempio, hello HiveQL seguente richiama hello `hiveudf.py` file archiviato nell'account di archiviazione di Azure hello predefinito per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-121">For example, hello following HiveQL invokes hello `hiveudf.py` file stored in hello default Azure Storage account for hello cluster.</span></span>

<span data-ttu-id="1c8a6-122">**HDInsight basato su Linux**</span><span class="sxs-lookup"><span data-stu-id="1c8a6-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="1c8a6-123">**HDInsight basato su Windows**</span><span class="sxs-lookup"><span data-stu-id="1c8a6-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="1c8a6-124">Nei cluster HDInsight basati su Windows, hello `USING` clausola deve specificare toopython.exe percorso completo hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-124">On Windows-based HDInsight clusters, hello `USING` clause must specify hello full path toopython.exe.</span></span>

<span data-ttu-id="1c8a6-125">Ecco cosa fa l'esempio:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-125">Here's what this example does:</span></span>

1. <span data-ttu-id="1c8a6-126">Hello `add file` istruzione all'inizio di hello del file hello aggiunge hello `hiveudf.py` toohello file distribuito cache, in modo che sia accessibile da tutti i nodi nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-126">hello `add file` statement at hello beginning of hello file adds hello `hiveudf.py` file toohello distributed cache, so it's accessible by all nodes in hello cluster.</span></span>
2. <span data-ttu-id="1c8a6-127">Hello `SELECT TRANSFORM ... USING` istruzione vengono selezionati dati hello `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-127">hello `SELECT TRANSFORM ... USING` statement selects data from hello `hivesampletable`.</span></span> <span data-ttu-id="1c8a6-128">Passa inoltre clientid hello e devicemake devicemodel valori toohello `hiveudf.py` script.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-128">It also passes hello clientid, devicemake, and devicemodel values toohello `hiveudf.py` script.</span></span>
3. <span data-ttu-id="1c8a6-129">Hello `AS` clausola descrive campi hello restituiti da `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-129">hello `AS` clause describes hello fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a><span data-ttu-id="1c8a6-130">Creare file hiveudf.py hello</span><span class="sxs-lookup"><span data-stu-id="1c8a6-130">Create hello hiveudf.py file</span></span>


<span data-ttu-id="1c8a6-131">Nell'ambiente di sviluppo creare un file di testo denominato `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="1c8a6-132">Utilizzare hello seguente di codice come contenuto di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-132">Use hello following code as hello contents of hello file:</span></span>

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

<span data-ttu-id="1c8a6-133">Questo script esegue hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-133">This script performs hello following actions:</span></span>

1. <span data-ttu-id="1c8a6-134">Leggere una riga di dati da STDIN.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="1c8a6-135">Hello carattere di nuova riga finale viene rimosso mediante `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-135">hello trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="1c8a6-136">Quando si esegue l'elaborazione del flusso, una singola riga contiene tutti i valori hello con un carattere di tabulazione tra ogni valore.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-136">When doing stream processing, a single line contains all hello values with a tab character between each value.</span></span> <span data-ttu-id="1c8a6-137">Pertanto, `string.split(line, "\t")` può essere utilizzato toosplit hello l'input in ogni scheda, restituendo solo i campi di hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-137">So `string.split(line, "\t")` can be used toosplit hello input at each tab, returning just hello fields.</span></span>
4. <span data-ttu-id="1c8a6-138">Una volta completata l'elaborazione, è possibile che l'output di hello deve scritto tooSTDOUT come una singola riga, con una scheda tra ogni campo.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-138">When processing is complete, hello output must be written tooSTDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="1c8a6-139">ad esempio `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="1c8a6-140">Hello `while` ciclo si ripete fino a quando non `line` è di lettura.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-140">hello `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="1c8a6-141">output di Hello dello script è una concatenazione di valori di input per hello `devicemake` e `devicemodel`, e un hash di hello valore concatenato.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-141">hello script output is a concatenation of hello input values for `devicemake` and `devicemodel`, and a hash of hello concatenated value.</span></span>

<span data-ttu-id="1c8a6-142">Vedere [esecuzione esempi hello](#running) come toorun in questo esempio il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-142">See [Running hello examples](#running) for how toorun this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="1c8a6-143"><a name="pigpython"></a>UDF di Pig</span><span class="sxs-lookup"><span data-stu-id="1c8a6-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="1c8a6-144">Script Python può essere utilizzato come una funzione definita dall'utente da Pig tramite hello `GENERATE` istruzione.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-144">A Python script can be used as a UDF from Pig through hello `GENERATE` statement.</span></span> <span data-ttu-id="1c8a6-145">È possibile eseguire script hello utilizzando Jython o Python C.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-145">You can run hello script using either Jython or C Python.</span></span>

* <span data-ttu-id="1c8a6-146">Jython viene eseguito su hello JVM e può essere chiamato in modo nativo da Pig.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-146">Jython runs on hello JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="1c8a6-147">C Python è un processo esterno, pertanto dati hello Pig in hello JVM viene inviato toohello script in esecuzione in un processo di Python.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-147">C Python is an external process, so hello data from Pig on hello JVM is sent out toohello script running in a Python process.</span></span> <span data-ttu-id="1c8a6-148">output di Hello di script Python hello viene inviato nuovamente nel Pig.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-148">hello output of hello Python script is sent back into Pig.</span></span>

<span data-ttu-id="1c8a6-149">interprete Python di hello toospecify, utilizzare `register` quando si fa riferimento a script Python hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-149">toospecify hello Python interpreter, use `register` when referencing hello Python script.</span></span> <span data-ttu-id="1c8a6-150">Hello negli esempi seguenti registrarsi script Pig come `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-150">hello following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="1c8a6-151">**toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="1c8a6-151">**toouse Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="1c8a6-152">**toouse Python C**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="1c8a6-152">**toouse C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c8a6-153">Quando si utilizza Jython, hello percorso toohello pig_jython file può essere un percorso locale o un WASB: / / percorso.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-153">When using Jython, hello path toohello pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="1c8a6-154">Tuttavia, quando si usa Python C, è necessario fare riferimento un file hello file System locale del nodo hello che si sta utilizzando un processo Pig di hello toosubmit.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-154">However, when using C Python, you must reference a file on hello local file system of hello node that you are using toosubmit hello Pig job.</span></span>

<span data-ttu-id="1c8a6-155">Una volta dopo la registrazione, hello latino Pig per questo esempio hello stesso per entrambi:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-155">Once past registration, hello Pig Latin for this example is hello same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="1c8a6-156">Ecco cosa fa l'esempio:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-156">Here's what this example does:</span></span>

1. <span data-ttu-id="1c8a6-157">Hello prima riga Carica file di dati di esempio hello, `sample.log` in `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-157">hello first line loads hello sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="1c8a6-158">Definisce anche ogni record come `chararray`.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="1c8a6-159">riga successiva Hello esclude tramite filtro i valori null, archiviando hello risultato dell'operazione di hello in `LOG`.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-159">hello next line filters out any null values, storing hello result of hello operation into `LOG`.</span></span>
3. <span data-ttu-id="1c8a6-160">Successivamente, scorre record hello `LOG` e utilizza `GENERATE` tooinvoke hello `create_structure` metodo contenuto nello script Python/Jython hello caricato come `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-160">Next, it iterates over hello records in `LOG` and uses `GENERATE` tooinvoke hello `create_structure` method contained in hello Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="1c8a6-161">`LINE`viene utilizzato toopass funzione toohello record corrente hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-161">`LINE` is used toopass hello current record toohello function.</span></span>
4. <span data-ttu-id="1c8a6-162">Infine, gli output di hello sono tooSTDOUT dumping tramite hello `DUMP` comando.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-162">Finally, hello outputs are dumped tooSTDOUT using hello `DUMP` command.</span></span> <span data-ttu-id="1c8a6-163">Questo comando Visualizza i risultati di hello al termine dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-163">This command displays hello results after hello operation completes.</span></span>

### <a name="create-hello-pigudfpy-file"></a><span data-ttu-id="1c8a6-164">Creare file pigudf.py hello</span><span class="sxs-lookup"><span data-stu-id="1c8a6-164">Create hello pigudf.py file</span></span>

<span data-ttu-id="1c8a6-165">Nell'ambiente di sviluppo creare un file di testo denominato `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="1c8a6-166">Utilizzare hello seguente di codice come contenuto di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-166">Use hello following code as hello contents of hello file:</span></span>

<a name="streamingpy"></a>

```python
# Uncomment hello following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

<span data-ttu-id="1c8a6-167">Nell'esempio Pig latino hello è definito hello `LINE` di input come un chararray perché nessuno schema coerente per l'input hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-167">In hello Pig Latin example, we defined hello `LINE` input as a chararray because there is no consistent schema for hello input.</span></span> <span data-ttu-id="1c8a6-168">Hello script Python Trasforma dati hello in uno schema coerente per l'output.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-168">hello Python script transforms hello data into a consistent schema for output.</span></span>

1. <span data-ttu-id="1c8a6-169">Hello `@outputSchema` istruzione definisce il formato di hello dei dati di hello restituito tooPig.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-169">hello `@outputSchema` statement defines hello format of hello data that is returned tooPig.</span></span> <span data-ttu-id="1c8a6-170">In questo caso si tratta di un **contenitore di dati**, ovvero un tipo di dati Pig.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="1c8a6-171">contenitore Hello contiene hello seguenti campi, ognuno dei quali sono chararray (stringhe):</span><span class="sxs-lookup"><span data-stu-id="1c8a6-171">hello bag contains hello following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="1c8a6-172">Data - hello data hello voce del log è stata creata</span><span class="sxs-lookup"><span data-stu-id="1c8a6-172">date - hello date hello log entry was created</span></span>
   * <span data-ttu-id="1c8a6-173">ora - hello voce di log hello è stato creato</span><span class="sxs-lookup"><span data-stu-id="1c8a6-173">time - hello time hello log entry was created</span></span>
   * <span data-ttu-id="1c8a6-174">ClassName - voce hello nome di classe hello è stato creato per</span><span class="sxs-lookup"><span data-stu-id="1c8a6-174">classname - hello class name hello entry was created for</span></span>
   * <span data-ttu-id="1c8a6-175">livello - hello log</span><span class="sxs-lookup"><span data-stu-id="1c8a6-175">level - hello log level</span></span>
   * <span data-ttu-id="1c8a6-176">voce di log dettagliate per hello - dettagli</span><span class="sxs-lookup"><span data-stu-id="1c8a6-176">detail - verbose details for hello log entry</span></span>

2. <span data-ttu-id="1c8a6-177">Successivamente, hello `def create_structure(input)` definisce una funzione hello Pig passa voci.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-177">Next, hello `def create_structure(input)` defines hello function that Pig passes line items to.</span></span>

3. <span data-ttu-id="1c8a6-178">dati di esempio, Hello `sample.log`, principalmente toohello data, ora, NomeClasse, livello, è conforme e schema desideriamo tooreturn in dettaglio.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-178">hello example data, `sample.log`, mostly conforms toohello date, time, classname, level, and detail schema we want tooreturn.</span></span> <span data-ttu-id="1c8a6-179">Contengono tuttavia alcune righe che iniziano con `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="1c8a6-180">Queste righe devono essere schema hello toomatch modificato.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-180">These lines must be modified toomatch hello schema.</span></span> <span data-ttu-id="1c8a6-181">Hello `if` istruzione verifica la presenza di quelli quindi terapeutici hello hello toomove dati di input `*java.lang.Exception*` fine toohello stringa, riportare hello dati in linea con il nostro schema output previsto.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-181">hello `if` statement checks for those, then massages hello input data toomove hello `*java.lang.Exception*` string toohello end, bringing hello data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="1c8a6-182">Successivamente, hello `split` comando è utilizzati toosplit hello dati hello prima quattro spazi.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-182">Next, hello `split` command is used toosplit hello data at hello first four space characters.</span></span> <span data-ttu-id="1c8a6-183">output di Hello viene assegnato in `date`, `time`, `classname`, `level`, e `detail`.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-183">hello output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="1c8a6-184">Infine, i valori hello vengono restituiti tooPig.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-184">Finally, hello values are returned tooPig.</span></span>

<span data-ttu-id="1c8a6-185">Quando vengono restituiti i dati di hello tooPig ha uno schema coerente, come definito in hello `@outputSchema` istruzione.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-185">When hello data is returned tooPig, it has a consistent schema as defined in hello `@outputSchema` statement.</span></span>

## <span data-ttu-id="1c8a6-186"><a name="running"></a>Caricare ed eseguire gli esempi di hello</span><span class="sxs-lookup"><span data-stu-id="1c8a6-186"><a name="running"></a>Upload and run hello examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c8a6-187">Hello **SSH** procedura funziona solo con un cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-187">hello **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="1c8a6-188">Hello **PowerShell** passaggi lavorare con i cluster HDInsight basati su Windows o Linux, ma richiede un client di Windows.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-188">hello **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="1c8a6-189">SSH</span><span class="sxs-lookup"><span data-stu-id="1c8a6-189">SSH</span></span>

<span data-ttu-id="1c8a6-190">Per altre informazioni sull'uso di SSH, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1c8a6-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="1c8a6-191">Utilizzare `scp` cluster di HDInsight tooyour file hello toocopy.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-191">Use `scp` toocopy hello files tooyour HDInsight cluster.</span></span> <span data-ttu-id="1c8a6-192">Ad esempio, hello comando copie hello cluster tooa file denominato seguente **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-192">For example, hello following command copies hello files tooa cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="1c8a6-193">Usare SSH tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-193">Use SSH tooconnect toohello cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="1c8a6-194">Dalla sessione SSH hello, aggiungere i file di python hello caricato precedentemente archiviazione WASB toohello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-194">From hello SSH session, add hello python files uploaded previously toohello WASB storage for hello cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="1c8a6-195">Dopo aver caricato il file hello, seguente hello utilizzare passaggi toorun hello Hive e processi Pig.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-195">After uploading hello files, use hello following steps toorun hello Hive and Pig jobs.</span></span>

#### <a name="use-hello-hive-udf"></a><span data-ttu-id="1c8a6-196">Utilizzare hello Hive definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="1c8a6-196">Use hello Hive UDF</span></span>

1. <span data-ttu-id="1c8a6-197">Hello utilizzare `hive` toostart hello hive shell dei comandi.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-197">Use hello `hive` command toostart hello hive shell.</span></span> <span data-ttu-id="1c8a6-198">Verrà visualizzato un `hive>` richiedere una volta caricate shell hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-198">You should see a `hive>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="1c8a6-199">Immettere hello seguente query hello `hive>` prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-199">Enter hello following query at hello `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="1c8a6-200">Dopo aver immesso l'ultima riga hello, deve iniziare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-200">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="1c8a6-201">Al termine del processo di hello, verrà restituito toohello simili di output esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-201">Once hello job completes, it returns output similar toohello following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a><span data-ttu-id="1c8a6-202">Utilizzare hello Pig funzione definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="1c8a6-202">Use hello Pig UDF</span></span>

1. <span data-ttu-id="1c8a6-203">Hello utilizzare `pig` toostart hello shell dei comandi.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-203">Use hello `pig` command toostart hello shell.</span></span> <span data-ttu-id="1c8a6-204">Viene visualizzato un `grunt>` richiedere una volta caricate shell hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-204">You see a `grunt>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="1c8a6-205">Immettere hello seguendo le istruzioni nel hello `grunt>` prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-205">Enter hello following statements at hello `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="1c8a6-206">Dopo aver immesso hello successiva riga, deve iniziare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-206">After entering hello following line, hello job should start.</span></span> <span data-ttu-id="1c8a6-207">Al termine del processo di hello, verrà restituito toohello simili di output dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-207">Once hello job completes, it returns output similar toohello following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="1c8a6-208">Utilizzare `quit` tooexit hello shell Grunt e quindi utilizzare hello seguenti tooedit hello pigudf.py file hello file System locale:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-208">Use `quit` tooexit hello Grunt shell, and then use hello following tooedit hello pigudf.py file on hello local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="1c8a6-209">Una volta nell'editor di hello, rimuovere il commento hello successiva riga rimuovendo hello `#` caratteri dall'inizio di hello della riga hello:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-209">Once in hello editor, uncomment hello following line by removing hello `#` character from hello beginning of hello line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="1c8a6-210">Una volta effettuato modifica hello, utilizzare l'editor di hello tooexit Ctrl + X.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-210">Once hello change has been made, use Ctrl+X tooexit hello editor.</span></span> <span data-ttu-id="1c8a6-211">Selezionare Y e quindi immettere toosave hello modifiche.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-211">Select Y, and then enter toosave hello changes.</span></span>

6. <span data-ttu-id="1c8a6-212">Hello utilizzare `pig` toostart hello shell dei comandi nuovamente.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-212">Use hello `pig` command toostart hello shell again.</span></span> <span data-ttu-id="1c8a6-213">Una volta visualizzato hello `grunt>` prompt, usare lo script Python di hello toorun usando interprete Python C hello seguente hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-213">Once you are at hello `grunt>` prompt, use hello following toorun hello Python script using hello C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="1c8a6-214">Dopo aver completato questo processo, dovrebbe essere stesso output di hello come quando è stato precedentemente eseguito script hello utilizzando Jython.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-214">Once this job completes, you should see hello same output as when you previously ran hello script using Jython.</span></span>

### <a name="powershell-upload-hello-files"></a><span data-ttu-id="1c8a6-215">PowerShell: Caricare i file di hello</span><span class="sxs-lookup"><span data-stu-id="1c8a6-215">PowerShell: Upload hello files</span></span>

<span data-ttu-id="1c8a6-216">È possibile utilizzare PowerShell tooupload hello file toohello HDInsight per il server.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-216">You can use PowerShell tooupload hello files toohello HDInsight server.</span></span> <span data-ttu-id="1c8a6-217">Utilizzare i seguenti file di script tooupload hello Python hello:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-217">Use hello following script tooupload hello Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="1c8a6-218">passaggi di Hello in questa sezione utilizzano Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-218">hello steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="1c8a6-219">Per ulteriori informazioni sull'utilizzo di Azure PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1c8a6-219">For more information on using Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
# Change hello path toomatch hello file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

Set-AzureStorageBlobContent `
    -File $pathToStreamingFile `
    -Blob "hiveudf.py" `
    -Container $container `
    -Context $context

Set-AzureStorageBlobContent `
    -File $pathToJythonFile `
    -Blob "pigudf.py" `
    -Container $container `
    -Context $context
```
> [!IMPORTANT]
> <span data-ttu-id="1c8a6-220">Hello modifica `C:\path\to` toohello percorso toohello file nell'ambiente di sviluppo di valore.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-220">Change hello `C:\path\to` value toohello path toohello files on your development environment.</span></span>

<span data-ttu-id="1c8a6-221">Questo script recupera le informazioni per il cluster HDInsight, quindi estrae account hello e una chiave per l'account di archiviazione predefinito hello e caricamenti hello radice toohello file contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-221">This script retrieves information for your HDInsight cluster, then extracts hello account and key for hello default storage account, and uploads hello files toohello root of hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="1c8a6-222">Per ulteriori informazioni sul caricamento di file, vedere hello [caricare dati per i processi di Hadoop in HDInsight](hdinsight-upload-data.md) documento.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-222">For more information on uploading files, see hello [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-hello-hive-udf"></a><span data-ttu-id="1c8a6-223">PowerShell: Utilizzo hello Hive definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="1c8a6-223">PowerShell: Use hello Hive UDF</span></span>

<span data-ttu-id="1c8a6-224">PowerShell può essere anche le query Hive tooremotely utilizzati eseguire.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-224">PowerShell can also be used tooremotely run Hive queries.</span></span> <span data-ttu-id="1c8a6-225">Hello utilizzare seguente script di PowerShell toorun una query Hive che utilizza **hiveudf.py** script:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-225">Use hello following PowerShell script toorun a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c8a6-226">Prima dell'esecuzione, script hello chiede hello HTTPs/Admin informazioni dell'account per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-226">Before running, hello script prompts you for hello HTTPs/Admin account information for your HDInsight cluster.</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

# If using a Windows-based HDInsight cluster, change hello USING statement to:
# "USING 'D:\Python27\python.exe hiveudf.py' AS " +
$HiveQuery = "add file wasb:///hiveudf.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python hiveudf.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for hello Hive job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="1c8a6-227">output di hello Hello **Hive** processo compariranno simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-227">hello output for hello **Hive** job should appear similar toohello following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="1c8a6-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="1c8a6-228">Pig (Jython)</span></span>

<span data-ttu-id="1c8a6-229">PowerShell può essere anche usato toorun latino Pig processi.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-229">PowerShell can also be used toorun Pig Latin jobs.</span></span> <span data-ttu-id="1c8a6-230">un processo Pig latino che utilizza hello toorun **pigudf.py** script, utilizzare hello lo script di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-230">toorun a Pig Latin job that uses hello **pigudf.py** script, use hello following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="1c8a6-231">Quando si inviano in remoto un processo tramite PowerShell, non è possibile toouse Python C come interprete hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-231">When remotely submitting a job using PowerShell, it is not possible toouse C Python as hello interpreter.</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

$PigQuery = "Register wasb:///pigudf.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for hello Pig job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="1c8a6-232">output di hello Hello **Pig** processo compariranno simile toohello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-232">hello output for hello **Pig** job should appear similar toohello following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="1c8a6-233"><a name="troubleshooting"></a>Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="1c8a6-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="1c8a6-234">Errori durante l'esecuzione di processi</span><span class="sxs-lookup"><span data-stu-id="1c8a6-234">Errors when running jobs</span></span>

<span data-ttu-id="1c8a6-235">Quando si esegue il processo di hive hello, è possibile riscontrare un toohello simile di errore seguente testo:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-235">When running hello hive job, you may encounter an error similar toohello following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

<span data-ttu-id="1c8a6-236">Questo problema può essere causato da file Python hello terminazioni di riga hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-236">This problem may be caused by hello line endings in hello Python file.</span></span> <span data-ttu-id="1c8a6-237">Molti editor di Windows predefinito toousing CR/LF come terminazione di riga hello, ma le applicazioni Linux prevedono in genere LF.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-237">Many Windows editors default toousing CRLF as hello line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="1c8a6-238">È possibile utilizzare i caratteri di hello CR tooremove di PowerShell istruzioni prima di caricare tooHDInsight file hello hello:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-238">You can use hello following PowerShell statements tooremove hello CR characters before uploading hello file tooHDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="1c8a6-239">Script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c8a6-239">PowerShell scripts</span></span>

<span data-ttu-id="1c8a6-240">Entrambi hello esempio gli script di PowerShell utilizzati esempi hello toorun contiene una riga di commento che viene visualizzato l'output di errore per il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-240">Both of hello example PowerShell scripts used toorun hello examples contain a commented line that displays error output for hello job.</span></span> <span data-ttu-id="1c8a6-241">Se non viene visualizzato l'output di hello previsto per il processo di hello, rimuovere il commento seguente hello di riga e visualizzare informazioni sull'errore hello indica un problema relativo.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-241">If you are not seeing hello expected output for hello job, uncomment hello following line and see if hello error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="1c8a6-242">informazioni sull'errore Hello (STDERR) e il risultato di hello del processo di hello (STDOUT) vengono anche registrati tooyour HDInsight archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1c8a6-242">hello error information (STDERR) and hello result of hello job (STDOUT) are also logged tooyour HDInsight storage.</span></span>

| <span data-ttu-id="1c8a6-243">Processo</span><span class="sxs-lookup"><span data-stu-id="1c8a6-243">For this job...</span></span> | <span data-ttu-id="1c8a6-244">Esaminare questi file nel contenitore blob hello</span><span class="sxs-lookup"><span data-stu-id="1c8a6-244">Look at these files in hello blob container</span></span> |
| --- | --- |
| <span data-ttu-id="1c8a6-245">Hive</span><span class="sxs-lookup"><span data-stu-id="1c8a6-245">Hive</span></span> |<span data-ttu-id="1c8a6-246">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="1c8a6-246">/HivePython/stderr</span></span><p><span data-ttu-id="1c8a6-247">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="1c8a6-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="1c8a6-248">Pig</span><span class="sxs-lookup"><span data-stu-id="1c8a6-248">Pig</span></span> |<span data-ttu-id="1c8a6-249">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="1c8a6-249">/PigPython/stderr</span></span><p><span data-ttu-id="1c8a6-250">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="1c8a6-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="1c8a6-251"><a name="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1c8a6-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="1c8a6-252">Se è necessario moduli Python tooload che non sono disponibili per impostazione predefinita, vedere [come toodeploy tooAzure un modulo HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c8a6-252">If you need tooload Python modules that aren't provided by default, see [How toodeploy a module tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="1c8a6-253">Per altri modi toouse Pig, Hive e toolearn sull'utilizzo di MapReduce, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="1c8a6-253">For other ways toouse Pig, Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="1c8a6-254">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="1c8a6-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1c8a6-255">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="1c8a6-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="1c8a6-256">Usare MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="1c8a6-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
