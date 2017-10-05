---
title: 'Funzioni definite dall''utente di Python con Apache Hive e Pig: Azure HDInsight | Microsoft Docs'
description: Informazioni su come usare le funzioni definite dall'utente di Python da Hive e Pig in HDInsight, lo stack di tecnologie Hadoop in Azure.
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
ms.openlocfilehash: 9b67ded05a52f1e68580434667495cf6cf939871
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="a7d8a-103">Usare le funzioni definite dall'utente di Python (UDF) con Hive e Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a7d8a-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="a7d8a-104">Informazioni su come usare le funzioni definite dall'utente di Python con Apache Hive e Pig in Hadoop in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-104">Learn how to use Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="a7d8a-105"><a name="python"></a>Python in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a7d8a-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="a7d8a-106">Python 2.7 viene installato per impostazione predefinita in HDInsight 3.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="a7d8a-107">Apache Hive può essere usato con questa versione di Python per l'elaborazione di flussi.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="a7d8a-108">L'elaborazione di flussi usa STDOUT e STDIN per passare i dati tra Hive e la funzione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-108">Stream processing uses STDOUT and STDIN to pass data between Hive and the UDF.</span></span>

<span data-ttu-id="a7d8a-109">HDInsight include anche Jython, un'implementazione di Python scritta in Java.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="a7d8a-110">Jython viene eseguito direttamente in Java Virtual Machine e non usa lo streaming.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-110">Jython runs directly on the Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="a7d8a-111">Jython è l'interprete Python consigliato quando si usa Python con Pig.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-111">Jython is the recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="a7d8a-112">La procedura in questo documento parte dai presupposti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-112">The steps in this document make the following assumptions:</span></span> 
>
> * <span data-ttu-id="a7d8a-113">L'utente deve creare gli script Python in un ambiente di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-113">You create the Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="a7d8a-114">Caricare gli script in HDInsight usando il comando `scp` da una sessione Bash locale o lo script di PowerShell presente.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-114">You upload the scripts to HDInsight using either the `scp` command from a local Bash session or the provided PowerShell script.</span></span>
>
> <span data-ttu-id="a7d8a-115">Se si desidera usare l'anteprima [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) con HDInsight, è necessario:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-115">If you want to use the [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview to work with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="a7d8a-116">Creare gli script all'interno dell'ambiente Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-116">Create the scripts inside the cloud shell environment.</span></span>
> * <span data-ttu-id="a7d8a-117">Usare `scp` per caricare i file da Cloud Shell in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-117">Use `scp` to upload the files from the cloud shell to HDInsight.</span></span>
> * <span data-ttu-id="a7d8a-118">Usare `ssh` da Cloud Shell per connettersi a HDInsight ed eseguire gli esempi.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-118">Use `ssh` from the cloud shell to connect to HDInsight and run the examples.</span></span>

## <span data-ttu-id="a7d8a-119"><a name="hivepython"></a>UDF di Hive</span><span class="sxs-lookup"><span data-stu-id="a7d8a-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="a7d8a-120">Python può essere usato come funzione definita dall'utente da Hive tramite l'istruzione `TRANSFORM` di HiveQL.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-120">Python can be used as a UDF from Hive through the HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="a7d8a-121">Ad esempio, HiveQL seguente richiama il file `hiveudf.py` archiviato nell'account di archiviazione di Azure predefinito per il cluster.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-121">For example, the following HiveQL invokes the `hiveudf.py` file stored in the default Azure Storage account for the cluster.</span></span>

<span data-ttu-id="a7d8a-122">**HDInsight basato su Linux**</span><span class="sxs-lookup"><span data-stu-id="a7d8a-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="a7d8a-123">**HDInsight basato su Windows**</span><span class="sxs-lookup"><span data-stu-id="a7d8a-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="a7d8a-124">Nei cluster HDInsight basati su Windows la clausola `USING` deve specificare il percorso completo di python.exe.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-124">On Windows-based HDInsight clusters, the `USING` clause must specify the full path to python.exe.</span></span>

<span data-ttu-id="a7d8a-125">Ecco cosa fa l'esempio:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-125">Here's what this example does:</span></span>

1. <span data-ttu-id="a7d8a-126">L'istruzione `add file` all'inizio del file aggiunge il file `hiveudf.py` alla cache distribuita ed è quindi accessibile a tutti i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-126">The `add file` statement at the beginning of the file adds the `hiveudf.py` file to the distributed cache, so it's accessible by all nodes in the cluster.</span></span>
2. <span data-ttu-id="a7d8a-127">L'istruzione `SELECT TRANSFORM ... USING` seleziona i dati da `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-127">The `SELECT TRANSFORM ... USING` statement selects data from the `hivesampletable`.</span></span> <span data-ttu-id="a7d8a-128">Passa anche i valori clientid, devicemake e devicemodel nello script `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-128">It also passes the clientid, devicemake, and devicemodel values to the `hiveudf.py` script.</span></span>
3. <span data-ttu-id="a7d8a-129">La clausola `AS` descrive i campi restituiti da `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-129">The `AS` clause describes the fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-the-hiveudfpy-file"></a><span data-ttu-id="a7d8a-130">Creare il file hiveudf.py</span><span class="sxs-lookup"><span data-stu-id="a7d8a-130">Create the hiveudf.py file</span></span>


<span data-ttu-id="a7d8a-131">Nell'ambiente di sviluppo creare un file di testo denominato `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="a7d8a-132">Usare il codice seguente come contenuto del file:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-132">Use the following code as the contents of the file:</span></span>

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

<span data-ttu-id="a7d8a-133">Lo script esegue le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-133">This script performs the following actions:</span></span>

1. <span data-ttu-id="a7d8a-134">Leggere una riga di dati da STDIN.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="a7d8a-135">Il carattere di nuova riga finale viene rimosso con `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-135">The trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="a7d8a-136">Durante l'elaborazione di flussi tutti i valori sono contenuti in un'unica riga sono separati da un carattere di tabulazione.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-136">When doing stream processing, a single line contains all the values with a tab character between each value.</span></span> <span data-ttu-id="a7d8a-137">Si può quindi usare `string.split(line, "\t")` per dividere l'input in corrispondenza di ogni tabulazione, in modo da restituire solo i campi.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-137">So `string.split(line, "\t")` can be used to split the input at each tab, returning just the fields.</span></span>
4. <span data-ttu-id="a7d8a-138">Al termine dell'elaborazione, l'output deve essere scritto in STDOUT in un'unica riga, con i campi separati da tabulazioni.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-138">When processing is complete, the output must be written to STDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="a7d8a-139">Ad esempio, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="a7d8a-140">Il ciclo `while` si ripete finché non viene letta alcuna `line`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-140">The `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="a7d8a-141">Lo script di output è una concatenazione di valori di input per `devicemake` e `devicemodel` e un hash del valore concatenato.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-141">The script output is a concatenation of the input values for `devicemake` and `devicemodel`, and a hash of the concatenated value.</span></span>

<span data-ttu-id="a7d8a-142">Per informazioni su come eseguire questo esempio nel cluster HDInsight, vedere [Esecuzione degli esempi](#running) .</span><span class="sxs-lookup"><span data-stu-id="a7d8a-142">See [Running the examples](#running) for how to run this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="a7d8a-143"><a name="pigpython"></a>UDF di Pig</span><span class="sxs-lookup"><span data-stu-id="a7d8a-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="a7d8a-144">Si può usare uno script di Python come funzione definita dall'utente da Pig tramite l'istruzione `GENERATE`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-144">A Python script can be used as a UDF from Pig through the `GENERATE` statement.</span></span> <span data-ttu-id="a7d8a-145">È possibile eseguire lo script usando Jython o C Python.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-145">You can run the script using either Jython or C Python.</span></span>

* <span data-ttu-id="a7d8a-146">Jython viene eseguito su JVM e può essere chiamato in modo nativo da Pig.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-146">Jython runs on the JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="a7d8a-147">C Python è un processo esterno, pertanto i dati di Pig su JVM vengono inviati allo script in esecuzione in un processo di Python.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-147">C Python is an external process, so the data from Pig on the JVM is sent out to the script running in a Python process.</span></span> <span data-ttu-id="a7d8a-148">Quindi l'output dello script di Python viene inviato in Pig.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-148">The output of the Python script is sent back into Pig.</span></span>

<span data-ttu-id="a7d8a-149">Per specificare l'interprete Python, usare `register` quando si fa riferimento allo script di Python.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-149">To specify the Python interpreter, use `register` when referencing the Python script.</span></span> <span data-ttu-id="a7d8a-150">Negli esempi seguenti gli script vengono registrati con Pig come `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-150">The following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="a7d8a-151">**Per usare Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="a7d8a-151">**To use Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="a7d8a-152">**Per usare C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="a7d8a-152">**To use C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7d8a-153">Quando si usa Jython, il percorso al file pig_jython può essere un percorso locale o un percorso WASB://.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-153">When using Jython, the path to the pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="a7d8a-154">Tuttavia, quando si usa C Python, è necessario fare riferimento un file nel file system locale del nodo che si usa per inviare il processo Pig.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-154">However, when using C Python, you must reference a file on the local file system of the node that you are using to submit the Pig job.</span></span>

<span data-ttu-id="a7d8a-155">Una volta trascorsa la registrazione, Pig Latin per questo esempio è lo stesso per entrambi:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-155">Once past registration, the Pig Latin for this example is the same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="a7d8a-156">Ecco cosa fa l'esempio:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-156">Here's what this example does:</span></span>

1. <span data-ttu-id="a7d8a-157">La prima riga carica il file di dati di esempio `sample.log` in `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-157">The first line loads the sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="a7d8a-158">Definisce anche ogni record come `chararray`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="a7d8a-159">La riga successiva esclude tutti i valori Null, archiviando il risultato dell'operazione in `LOG`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-159">The next line filters out any null values, storing the result of the operation into `LOG`.</span></span>
3. <span data-ttu-id="a7d8a-160">Esegue quindi l'iterazione sui record in `LOG` e usa `GENERATE` per richiamare il metodo `create_structure` contenuto nello script di Python/Jython caricato come `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-160">Next, it iterates over the records in `LOG` and uses `GENERATE` to invoke the `create_structure` method contained in the Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="a7d8a-161">`LINE` viene usato per passare il record corrente alla funzione.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-161">`LINE` is used to pass the current record to the function.</span></span>
4. <span data-ttu-id="a7d8a-162">Viene infine eseguito il dump degli output in STDOUT con il comando `DUMP`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-162">Finally, the outputs are dumped to STDOUT using the `DUMP` command.</span></span> <span data-ttu-id="a7d8a-163">Questo comando visualizza i risultati al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-163">This command displays the results after the operation completes.</span></span>

### <a name="create-the-pigudfpy-file"></a><span data-ttu-id="a7d8a-164">Creare il file pigudf.py</span><span class="sxs-lookup"><span data-stu-id="a7d8a-164">Create the pigudf.py file</span></span>

<span data-ttu-id="a7d8a-165">Nell'ambiente di sviluppo creare un file di testo denominato `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="a7d8a-166">Usare il codice seguente come contenuto del file:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-166">Use the following code as the contents of the file:</span></span>

<a name="streamingpy"></a>

```python
# Uncomment the following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

<span data-ttu-id="a7d8a-167">Nell'esempio Pig Latin l'input di `LINE` è stato definito come chararray perché non contiene uno schema coerente.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-167">In the Pig Latin example, we defined the `LINE` input as a chararray because there is no consistent schema for the input.</span></span> <span data-ttu-id="a7d8a-168">Con lo script Python i dati vengono trasformati in uno schema coerente per l'output.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-168">The Python script transforms the data into a consistent schema for output.</span></span>

1. <span data-ttu-id="a7d8a-169">L'istruzione `@outputSchema` definisce il formato dei dati che verranno restituiti a Pig.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-169">The `@outputSchema` statement defines the format of the data that is returned to Pig.</span></span> <span data-ttu-id="a7d8a-170">In questo caso si tratta di un **contenitore di dati**, ovvero un tipo di dati Pig.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="a7d8a-171">Il contenitore include i seguenti campi, che sono tutti chararray (stringhe):</span><span class="sxs-lookup"><span data-stu-id="a7d8a-171">The bag contains the following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="a7d8a-172">date - data di creazione della voce del log</span><span class="sxs-lookup"><span data-stu-id="a7d8a-172">date - the date the log entry was created</span></span>
   * <span data-ttu-id="a7d8a-173">time - ora di creazione della voce del log</span><span class="sxs-lookup"><span data-stu-id="a7d8a-173">time - the time the log entry was created</span></span>
   * <span data-ttu-id="a7d8a-174">classname - nome della classe per cui è stata creata la voce</span><span class="sxs-lookup"><span data-stu-id="a7d8a-174">classname - the class name the entry was created for</span></span>
   * <span data-ttu-id="a7d8a-175">level - livello del log</span><span class="sxs-lookup"><span data-stu-id="a7d8a-175">level - the log level</span></span>
   * <span data-ttu-id="a7d8a-176">detail - dettagli relativi alla voce di log</span><span class="sxs-lookup"><span data-stu-id="a7d8a-176">detail - verbose details for the log entry</span></span>

2. <span data-ttu-id="a7d8a-177">Successivamente `def create_structure(input)` definisce la funzione a cui Pig passerà le voci.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-177">Next, the `def create_structure(input)` defines the function that Pig passes line items to.</span></span>

3. <span data-ttu-id="a7d8a-178">I dati di esempio in `sample.log` sono per lo più conformi allo schema date, time, classname, level e detail che si intende restituire.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-178">The example data, `sample.log`, mostly conforms to the date, time, classname, level, and detail schema we want to return.</span></span> <span data-ttu-id="a7d8a-179">Contengono tuttavia alcune righe che iniziano con `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="a7d8a-180">Queste righe devono essere modificate in modo che corrispondano allo schema.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-180">These lines must be modified to match the schema.</span></span> <span data-ttu-id="a7d8a-181">L'istruzione `if` verifica la presenza di queste righe, quindi forza i dati di input a spostare la stringa `*java.lang.Exception*` alla fine, portando i dati in linea con lo schema di output previsto.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-181">The `if` statement checks for those, then massages the input data to move the `*java.lang.Exception*` string to the end, bringing the data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="a7d8a-182">Viene quindi usato il comando `split` per dividere i dati in corrispondenza dei primi quattro spazi.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-182">Next, the `split` command is used to split the data at the first four space characters.</span></span> <span data-ttu-id="a7d8a-183">L'output viene assegnato in `date`, `time`, `classname`, `level` e `detail`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-183">The output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="a7d8a-184">I valori vengono infine restituiti a Pig.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-184">Finally, the values are returned to Pig.</span></span>

<span data-ttu-id="a7d8a-185">Quando i dati vengono restituiti a Pig, lo schema sarà coerente, come definito nell'istruzione `@outputSchema`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-185">When the data is returned to Pig, it has a consistent schema as defined in the `@outputSchema` statement.</span></span>

## <span data-ttu-id="a7d8a-186"><a name="running"></a>Caricare ed eseguire gli esempi</span><span class="sxs-lookup"><span data-stu-id="a7d8a-186"><a name="running"></a>Upload and run the examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7d8a-187">La procedura per **SSH** può essere eseguita solo con un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-187">The **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="a7d8a-188">La procedura per **PowerShell** può essere eseguita con un cluster HDInsight basato su Linux o su Windows, ma è necessario un client Windows.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-188">The **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="a7d8a-189">SSH</span><span class="sxs-lookup"><span data-stu-id="a7d8a-189">SSH</span></span>

<span data-ttu-id="a7d8a-190">Per altre informazioni sull'uso di SSH, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a7d8a-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="a7d8a-191">Usare `scp` per copiare i file nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-191">Use `scp` to copy the files to your HDInsight cluster.</span></span> <span data-ttu-id="a7d8a-192">Ad esempio, il comando seguente copia i file in un cluster denominato **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-192">For example, the following command copies the files to a cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="a7d8a-193">Usare SSH per connettersi al cluster.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-193">Use SSH to connect to the cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="a7d8a-194">Dalla sessione SSH, aggiungere i file python caricati in precedenza nell'archivio WASB per il cluster.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-194">From the SSH session, add the python files uploaded previously to the WASB storage for the cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="a7d8a-195">Dopo il caricamento dei file, usare la procedura seguente per eseguire i processi Hive e Pig.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-195">After uploading the files, use the following steps to run the Hive and Pig jobs.</span></span>

#### <a name="use-the-hive-udf"></a><span data-ttu-id="a7d8a-196">Usare l'UDF di Hive</span><span class="sxs-lookup"><span data-stu-id="a7d8a-196">Use the Hive UDF</span></span>

1. <span data-ttu-id="a7d8a-197">Usare il comando `hive` per avviare la shell di Hive.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-197">Use the `hive` command to start the hive shell.</span></span> <span data-ttu-id="a7d8a-198">Una volta caricata la shell, verrà visualizzato un prompt `hive>` .</span><span class="sxs-lookup"><span data-stu-id="a7d8a-198">You should see a `hive>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="a7d8a-199">Immettere la query seguente al prompt `hive>`:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-199">Enter the following query at the `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="a7d8a-200">Dopo l'immissione dell'ultima riga il processo dovrebbe essere avviato.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-200">After entering the last line, the job should start.</span></span> <span data-ttu-id="a7d8a-201">Al termine del processo, restituisce un output simile al seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-201">Once the job completes, it returns output similar to the following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-the-pig-udf"></a><span data-ttu-id="a7d8a-202">Usare l'UDF di Pig</span><span class="sxs-lookup"><span data-stu-id="a7d8a-202">Use the Pig UDF</span></span>

1. <span data-ttu-id="a7d8a-203">Usare il comando `pig` per avviare la shell.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-203">Use the `pig` command to start the shell.</span></span> <span data-ttu-id="a7d8a-204">Dopo il caricamento della shell, viene visualizzato un prompt `grunt>`.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-204">You see a `grunt>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="a7d8a-205">Al prompt `grunt>` immettere le istruzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-205">Enter the following statements at the `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="a7d8a-206">Dopo l'immissione della riga seguente, il processo dovrebbe essere avviato.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-206">After entering the following line, the job should start.</span></span> <span data-ttu-id="a7d8a-207">Al termine del processo, restituisce un output simile ai dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-207">Once the job completes, it returns output similar to the following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="a7d8a-208">Usare `quit` per chiudere la shell Grunt e quindi il prompt seguente per modificare il file pigudf.py nel file system locale:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-208">Use `quit` to exit the Grunt shell, and then use the following to edit the pigudf.py file on the local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="a7d8a-209">Una volta nell'editor, rimuovere i simboli di commenti dalla riga seguente rimuovendo il carattere `#` dall'inizio della riga:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-209">Once in the editor, uncomment the following line by removing the `#` character from the beginning of the line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="a7d8a-210">Una volta apportata la modifica, usare Ctrl + X per uscire dall'editor.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-210">Once the change has been made, use Ctrl+X to exit the editor.</span></span> <span data-ttu-id="a7d8a-211">Selezionare Y e quindi INVIO per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-211">Select Y, and then enter to save the changes.</span></span>

6. <span data-ttu-id="a7d8a-212">Usare il comando `pig` per avviare di nuovo la shell.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-212">Use the `pig` command to start the shell again.</span></span> <span data-ttu-id="a7d8a-213">Una volta al prompt `grunt>` usare la riga seguente per eseguire il script di Python con l'interprete C Python.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-213">Once you are at the `grunt>` prompt, use the following to run the Python script using the C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="a7d8a-214">Una volta completato questo processo, si dovrebbe vedere lo stesso risultato di quando è stato eseguito lo script in precedenza con Jython.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-214">Once this job completes, you should see the same output as when you previously ran the script using Jython.</span></span>

### <a name="powershell-upload-the-files"></a><span data-ttu-id="a7d8a-215">PowerShell: Caricare i file</span><span class="sxs-lookup"><span data-stu-id="a7d8a-215">PowerShell: Upload the files</span></span>

<span data-ttu-id="a7d8a-216">È possibile usare PowerShell per caricare i file nel server di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-216">You can use PowerShell to upload the files to the HDInsight server.</span></span> <span data-ttu-id="a7d8a-217">Usare lo script seguente per caricare i file di Python:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-217">Use the following script to upload the Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a7d8a-218">I passaggi descritti in questa sezione usano Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-218">The steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="a7d8a-219">Per altre informazioni sull'uso di Azure PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a7d8a-219">For more information on using Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
# Change the path to match the file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload the file
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
> <span data-ttu-id="a7d8a-220">Modifica il valore `C:\path\to` per il percorso dei file in un ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-220">Change the `C:\path\to` value to the path to the files on your development environment.</span></span>

<span data-ttu-id="a7d8a-221">Questo script recupera le informazioni relative al cluster HDInsight, quindi estrae l'account e la chiave dell'account di archiviazione predefinito e carica i file nella radice del contenitore.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-221">This script retrieves information for your HDInsight cluster, then extracts the account and key for the default storage account, and uploads the files to the root of the container.</span></span>

> [!NOTE]
> <span data-ttu-id="a7d8a-222">Per altre informazioni sul caricamento dei file, vedere il documento [Caricare dati per processi Hadoop in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="a7d8a-222">For more information on uploading files, see the [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-the-hive-udf"></a><span data-ttu-id="a7d8a-223">PowerShell: usare l'UDF di Hive</span><span class="sxs-lookup"><span data-stu-id="a7d8a-223">PowerShell: Use the Hive UDF</span></span>

<span data-ttu-id="a7d8a-224">PowerShell può essere usato anche per eseguire in remoto le query Hive.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-224">PowerShell can also be used to remotely run Hive queries.</span></span> <span data-ttu-id="a7d8a-225">Usare lo script di PowerShell seguente per eseguire una query di Hive che usa lo script **hiveudf.py**:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-225">Use the following PowerShell script to run a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7d8a-226">Prima dell'esecuzione, lo script richiede le informazioni sull'account HTTPS/Amministratore per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-226">Before running, the script prompts you for the HTTPs/Admin account information for your HDInsight cluster.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

# If using a Windows-based HDInsight cluster, change the USING statement to:
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
Write-Host "Wait for the Hive job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="a7d8a-227">L'output del processo **Hive** sarà simile al seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-227">The output for the **Hive** job should appear similar to the following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="a7d8a-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="a7d8a-228">Pig (Jython)</span></span>

<span data-ttu-id="a7d8a-229">PowerShell può essere usato anche per eseguire processi di Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-229">PowerShell can also be used to run Pig Latin jobs.</span></span> <span data-ttu-id="a7d8a-230">Per eseguire un processo di Pig Latin che usa lo script **pigudf.py**, usare lo script di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-230">To run a Pig Latin job that uses the **pigudf.py** script, use the following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="a7d8a-231">Durante l'invio remoto di un processo con PowerShell, non è possibile usare C Python come interprete.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-231">When remotely submitting a job using PowerShell, it is not possible to use C Python as the interpreter.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

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

Write-Host "Wait for the Pig job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="a7d8a-232">L'output del processo **Pig** sarà simile ai dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-232">The output for the **Pig** job should appear similar to the following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="a7d8a-233"><a name="troubleshooting"></a>Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="a7d8a-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="a7d8a-234">Errori durante l'esecuzione di processi</span><span class="sxs-lookup"><span data-stu-id="a7d8a-234">Errors when running jobs</span></span>

<span data-ttu-id="a7d8a-235">Quando si esegue il processo hive, è possibile riscontrare un errore simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-235">When running the hive job, you may encounter an error similar to the following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing to your custom script. It may have crashed with an error.

<span data-ttu-id="a7d8a-236">Questo problema potrebbe essere causato dalle terminazioni di riga nel file di Python.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-236">This problem may be caused by the line endings in the Python file.</span></span> <span data-ttu-id="a7d8a-237">Molti editor di Windows usano per impostazione predefinita CRLF come terminazione di riga, mentre le applicazioni Linux prevedono in genere LF.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-237">Many Windows editors default to using CRLF as the line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="a7d8a-238">È possibile usare le istruzioni di PowerShell seguenti per rimuovere i caratteri CR prima di caricare il file in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-238">You can use the following PowerShell statements to remove the CR characters before uploading the file to HDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="a7d8a-239">Script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7d8a-239">PowerShell scripts</span></span>

<span data-ttu-id="a7d8a-240">Entrambi gli script di esempio di PowerShell usati per eseguire gli esempi contengono una riga impostata come commento che mostra l'output degli errori relativi al processo.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-240">Both of the example PowerShell scripts used to run the examples contain a commented line that displays error output for the job.</span></span> <span data-ttu-id="a7d8a-241">Se l'output previsto per il processo non viene visualizzato, rimuovere i simboli di commento dalla riga seguente e verificare se le informazioni di errore indicano un problema.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-241">If you are not seeing the expected output for the job, uncomment the following line and see if the error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="a7d8a-242">Le informazioni sull'errore (STDERR) e il risultato del processo (STDOUT) vengono anche registrati nell'archivio di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7d8a-242">The error information (STDERR) and the result of the job (STDOUT) are also logged to your HDInsight storage.</span></span>

| <span data-ttu-id="a7d8a-243">Processo</span><span class="sxs-lookup"><span data-stu-id="a7d8a-243">For this job...</span></span> | <span data-ttu-id="a7d8a-244">File nel contenitore BLOB da verificare</span><span class="sxs-lookup"><span data-stu-id="a7d8a-244">Look at these files in the blob container</span></span> |
| --- | --- |
| <span data-ttu-id="a7d8a-245">Hive</span><span class="sxs-lookup"><span data-stu-id="a7d8a-245">Hive</span></span> |<span data-ttu-id="a7d8a-246">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="a7d8a-246">/HivePython/stderr</span></span><p><span data-ttu-id="a7d8a-247">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="a7d8a-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="a7d8a-248">Pig</span><span class="sxs-lookup"><span data-stu-id="a7d8a-248">Pig</span></span> |<span data-ttu-id="a7d8a-249">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="a7d8a-249">/PigPython/stderr</span></span><p><span data-ttu-id="a7d8a-250">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="a7d8a-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="a7d8a-251"><a name="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a7d8a-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="a7d8a-252">Se è necessario caricare moduli Python non forniti per impostazione predefinita, vedere [Come distribuire un modulo in Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="a7d8a-252">If you need to load Python modules that aren't provided by default, see [How to deploy a module to Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="a7d8a-253">Per altre modalità d'uso di Pig e Hive e per informazioni su come usare MapReduce, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7d8a-253">For other ways to use Pig, Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="a7d8a-254">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="a7d8a-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a7d8a-255">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="a7d8a-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="a7d8a-256">Usare MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="a7d8a-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
