---
title: formati aaaFile e compressione nella Data Factory di Azure | Documenti Microsoft
description: "Informazioni sui formati di file hello è supportati da Azure Data Factory."
keywords: dati blob, copia di blob di azure
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="57a3f-104">Informazioni sui formati di compressione e sui file supportati da Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="57a3f-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="57a3f-105">*Questo argomento si applica toohello segue connettori: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Blob di Azure](data-factory-azure-blob-connector.md), [archivio Azure Data Lake](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), e [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="57a3f-105">*This topic applies toohello following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="57a3f-106">Data Factory di Azure supporta i seguenti tipi di formato di file hello:</span><span class="sxs-lookup"><span data-stu-id="57a3f-106">Azure Data Factory supports hello following file format types:</span></span>

* [<span data-ttu-id="57a3f-107">Formato testo</span><span class="sxs-lookup"><span data-stu-id="57a3f-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="57a3f-108">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="57a3f-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="57a3f-109">Formato Avro</span><span class="sxs-lookup"><span data-stu-id="57a3f-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="57a3f-110">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="57a3f-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="57a3f-111">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="57a3f-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="57a3f-112">Formato testo</span><span class="sxs-lookup"><span data-stu-id="57a3f-112">Text format</span></span>
<span data-ttu-id="57a3f-113">Se si desidera tooread da un file di testo o scrivere file di testo tooa, impostare hello `type` proprietà hello `format` sezione del set di dati hello troppo**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="57a3f-113">If you want tooread from a text file or write tooa text file, set hello `type` property in hello `format` section of hello dataset too**TextFormat**.</span></span> <span data-ttu-id="57a3f-114">È inoltre possibile specificare i seguenti hello **facoltativo** proprietà hello `format` sezione.</span><span class="sxs-lookup"><span data-stu-id="57a3f-114">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="57a3f-115">Vedere [esempio TextFormat](#textformat-example) sezione su come tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="57a3f-115">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="57a3f-116">Proprietà</span><span class="sxs-lookup"><span data-stu-id="57a3f-116">Property</span></span> | <span data-ttu-id="57a3f-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57a3f-117">Description</span></span> | <span data-ttu-id="57a3f-118">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="57a3f-118">Allowed values</span></span> | <span data-ttu-id="57a3f-119">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="57a3f-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="57a3f-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="57a3f-120">columnDelimiter</span></span> |<span data-ttu-id="57a3f-121">carattere Hello usato tooseparate colonne in un file.</span><span class="sxs-lookup"><span data-stu-id="57a3f-121">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="57a3f-122">È possibile considerare toouse un carattere non stampabile raro che potrebbero essere probabilmente non esiste nei dati.</span><span class="sxs-lookup"><span data-stu-id="57a3f-122">You can consider toouse a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="57a3f-123">Ad esempio, specificare "\u0001", che rappresenta l'inizio intestazione (SOH).</span><span class="sxs-lookup"><span data-stu-id="57a3f-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="57a3f-124">È consentito un solo carattere.</span><span class="sxs-lookup"><span data-stu-id="57a3f-124">Only one character is allowed.</span></span> <span data-ttu-id="57a3f-125">Hello **predefinito** valore **virgola (',')**.</span><span class="sxs-lookup"><span data-stu-id="57a3f-125">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="57a3f-126">toouse un carattere Unicode, vedere troppo[caratteri Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello codice corrispondente per tale.</span><span class="sxs-lookup"><span data-stu-id="57a3f-126">toouse a Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="57a3f-127">No</span><span class="sxs-lookup"><span data-stu-id="57a3f-127">No</span></span> |
| <span data-ttu-id="57a3f-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="57a3f-128">rowDelimiter</span></span> |<span data-ttu-id="57a3f-129">carattere Hello usato tooseparate righe in un file.</span><span class="sxs-lookup"><span data-stu-id="57a3f-129">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="57a3f-130">È consentito un solo carattere.</span><span class="sxs-lookup"><span data-stu-id="57a3f-130">Only one character is allowed.</span></span> <span data-ttu-id="57a3f-131">Hello **predefinito** valore è uno dei seguenti valori in lettura hello: **["\r\n", "\r", "\n"]** e **"\r\n"** durante la scrittura.</span><span class="sxs-lookup"><span data-stu-id="57a3f-131">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="57a3f-132">No</span><span class="sxs-lookup"><span data-stu-id="57a3f-132">No</span></span> |
| <span data-ttu-id="57a3f-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="57a3f-133">escapeChar</span></span> |<span data-ttu-id="57a3f-134">carattere speciale di Hello utilizzato tooescape un delimitatore di colonna nel contenuto di hello del file di input.</span><span class="sxs-lookup"><span data-stu-id="57a3f-134">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="57a3f-135">Per una tabella, è possibile specificare sia escapeChar che quoteChar.</span><span class="sxs-lookup"><span data-stu-id="57a3f-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="57a3f-136">È consentito un solo carattere.</span><span class="sxs-lookup"><span data-stu-id="57a3f-136">Only one character is allowed.</span></span> <span data-ttu-id="57a3f-137">Nessun valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="57a3f-137">No default value.</span></span> <br/><br/><span data-ttu-id="57a3f-138">Esempio: se è presente una virgola (', ') come delimitatore di colonna hello ma si desidera aggiungere un carattere virgola toohave hello in testo hello (esempio: "Hello, world"), è possibile definire '$' come carattere di escape hello e utilizzare una stringa "Hello$, world" nell'origine hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-138">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="57a3f-139">No</span><span class="sxs-lookup"><span data-stu-id="57a3f-139">No</span></span> |
| <span data-ttu-id="57a3f-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="57a3f-140">quoteChar</span></span> |<span data-ttu-id="57a3f-141">carattere di Hello utilizzato tooquote un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="57a3f-141">hello character used tooquote a string value.</span></span> <span data-ttu-id="57a3f-142">delimitatori di colonna e riga Hello all'interno di virgolette singole hello verrebbero considerati come parte del valore di stringa hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-142">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="57a3f-143">Questa proprietà è applicabile tooboth input e output di set di dati.</span><span class="sxs-lookup"><span data-stu-id="57a3f-143">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="57a3f-144">Per una tabella, è possibile specificare sia escapeChar che quoteChar.</span><span class="sxs-lookup"><span data-stu-id="57a3f-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="57a3f-145">È consentito un solo carattere.</span><span class="sxs-lookup"><span data-stu-id="57a3f-145">Only one character is allowed.</span></span> <span data-ttu-id="57a3f-146">Nessun valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="57a3f-146">No default value.</span></span> <br/><br/><span data-ttu-id="57a3f-147">Ad esempio, se è presente una virgola (', ') come delimitatore di colonna hello ma si desidera assegnare il carattere virgola toohave nel testo hello (esempio: < Hello, world >), è possibile definire "(virgolette doppie) come hello virgolette e utilizzare la stringa hello"Hello, world"nell'origine hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-147">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="57a3f-148">No</span><span class="sxs-lookup"><span data-stu-id="57a3f-148">No</span></span> |
| <span data-ttu-id="57a3f-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="57a3f-149">nullValue</span></span> |<span data-ttu-id="57a3f-150">Uno o più caratteri utilizzati toorepresent un valore null.</span><span class="sxs-lookup"><span data-stu-id="57a3f-150">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="57a3f-151">Uno o più caratteri.</span><span class="sxs-lookup"><span data-stu-id="57a3f-151">One or more characters.</span></span> <span data-ttu-id="57a3f-152">Hello **predefinito** i valori sono **"\N" e "NULL"** in lettura e **"\N"** durante la scrittura.</span><span class="sxs-lookup"><span data-stu-id="57a3f-152">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="57a3f-153">No</span><span class="sxs-lookup"><span data-stu-id="57a3f-153">No</span></span> |
| <span data-ttu-id="57a3f-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="57a3f-154">encodingName</span></span> |<span data-ttu-id="57a3f-155">Specificare il nome della codifica di hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-155">Specify hello encoding name.</span></span> |<span data-ttu-id="57a3f-156">Un nome di codifica valido.</span><span class="sxs-lookup"><span data-stu-id="57a3f-156">A valid encoding name.</span></span> <span data-ttu-id="57a3f-157">Vedere [Proprietà Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="57a3f-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="57a3f-158">Esempio: windows-1250 o shift_jis.</span><span class="sxs-lookup"><span data-stu-id="57a3f-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="57a3f-159">Hello **predefinito** valore **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="57a3f-159">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="57a3f-160">No</span><span class="sxs-lookup"><span data-stu-id="57a3f-160">No</span></span> |
| <span data-ttu-id="57a3f-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="57a3f-161">firstRowAsHeader</span></span> |<span data-ttu-id="57a3f-162">Specifica se tooconsider hello prima riga come intestazione.</span><span class="sxs-lookup"><span data-stu-id="57a3f-162">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="57a3f-163">In un set di dati di input Data factory legge la prima riga come intestazione.</span><span class="sxs-lookup"><span data-stu-id="57a3f-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="57a3f-164">In un set di dati di output Data factory scrive la prima riga come intestazione.</span><span class="sxs-lookup"><span data-stu-id="57a3f-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="57a3f-165">Vedere [Scenari per l'uso di `firstRowAsHeader` e `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) per gli scenari di esempio.</span><span class="sxs-lookup"><span data-stu-id="57a3f-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="57a3f-166">True</span><span class="sxs-lookup"><span data-stu-id="57a3f-166">True</span></span><br/><span data-ttu-id="57a3f-167"><b>False (impostazione predefinita)</b></span><span class="sxs-lookup"><span data-stu-id="57a3f-167"><b>False (default)</b></span></span> |<span data-ttu-id="57a3f-168">No</span><span class="sxs-lookup"><span data-stu-id="57a3f-168">No</span></span> |
| <span data-ttu-id="57a3f-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="57a3f-169">skipLineCount</span></span> |<span data-ttu-id="57a3f-170">Indica il numero di hello di tooskip righe durante la lettura di dati da file di input.</span><span class="sxs-lookup"><span data-stu-id="57a3f-170">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="57a3f-171">Se vengono specificati sia skipLineCount e prima riga come intestazione, le righe di hello vengono ignorate prima e quindi le informazioni di intestazione hello viene letto dal file di input hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-171">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="57a3f-172">Vedere [Scenari per l'uso di `firstRowAsHeader` e `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) per gli scenari di esempio.</span><span class="sxs-lookup"><span data-stu-id="57a3f-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="57a3f-173">Integer</span><span class="sxs-lookup"><span data-stu-id="57a3f-173">Integer</span></span> |<span data-ttu-id="57a3f-174">No</span><span class="sxs-lookup"><span data-stu-id="57a3f-174">No</span></span> |
| <span data-ttu-id="57a3f-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="57a3f-175">treatEmptyAsNull</span></span> |<span data-ttu-id="57a3f-176">Consente di specificare se una stringa vuota o null tootreat come un valore null durante la lettura dei dati da un file di input.</span><span class="sxs-lookup"><span data-stu-id="57a3f-176">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="57a3f-177">**True (impostazione predefinita)**</span><span class="sxs-lookup"><span data-stu-id="57a3f-177">**True (default)**</span></span><br/><span data-ttu-id="57a3f-178">False</span><span class="sxs-lookup"><span data-stu-id="57a3f-178">False</span></span> |<span data-ttu-id="57a3f-179">No</span><span class="sxs-lookup"><span data-stu-id="57a3f-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="57a3f-180">Esempio di TextFormat</span><span class="sxs-lookup"><span data-stu-id="57a3f-180">TextFormat example</span></span>
<span data-ttu-id="57a3f-181">In hello seguente definizione JSON per un set di dati, alcune delle proprietà facoltative hello vengono specificati.</span><span class="sxs-lookup"><span data-stu-id="57a3f-181">In hello following JSON definition for a dataset, some of hello optional properties are specified.</span></span>

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

<span data-ttu-id="57a3f-182">toouse un `escapeChar` anziché `quoteChar`, sostituire la riga hello con `quoteChar` con hello escapeChar seguenti:</span><span class="sxs-lookup"><span data-stu-id="57a3f-182">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="57a3f-183">Scenari di utilizzo di firstRowAsHeader e skipLineCount</span><span class="sxs-lookup"><span data-stu-id="57a3f-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="57a3f-184">Si sta copiando un file di testo di origine file non tooa e tooadd una riga di intestazione che contiene i metadati dello schema hello (ad esempio: schema SQL).</span><span class="sxs-lookup"><span data-stu-id="57a3f-184">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="57a3f-185">Specificare `firstRowAsHeader` come true nel set di dati per questo scenario di output di hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-185">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="57a3f-186">Si sta copiando un file di testo contenente un sink non basate su file di intestazione riga tooa e toodrop che riga.</span><span class="sxs-lookup"><span data-stu-id="57a3f-186">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="57a3f-187">Specificare `firstRowAsHeader` come true nella hello di un set di dati dell'input.</span><span class="sxs-lookup"><span data-stu-id="57a3f-187">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="57a3f-188">Si sta copiando un file di testo e si desiderano tooskip alcune righe all'inizio di hello che non contengono dati o intestazione informazioni.</span><span class="sxs-lookup"><span data-stu-id="57a3f-188">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="57a3f-189">Specificare `skipLineCount` tooindicate hello numero di righe toobe ignorati.</span><span class="sxs-lookup"><span data-stu-id="57a3f-189">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="57a3f-190">Se il resto di hello del file hello contiene una riga di intestazione, è inoltre possibile specificare `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="57a3f-190">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="57a3f-191">Se entrambi `skipLineCount` e `firstRowAsHeader` sono specificate, le righe di hello vengono ignorate prima e quindi le informazioni di intestazione hello viene letto dal file di input hello</span><span class="sxs-lookup"><span data-stu-id="57a3f-191">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

## <a name="json-format"></a><span data-ttu-id="57a3f-192">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="57a3f-192">JSON format</span></span>
<span data-ttu-id="57a3f-193">troppo**importazione/esportazione di un file JSON come-è in/da Azure Cosmos DB**, vedere hello [documenti JSON di importazione/esportazione](data-factory-azure-documentdb-connector.md#importexport-json-documents) sezione [spostare i dati da e verso Azure Cosmos DB](data-factory-azure-documentdb-connector.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="57a3f-193">too**import/export a JSON file as-is into/from Azure Cosmos DB**, hello see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="57a3f-194">Se si desidera che i file JSON hello tooparse o scrivono dati hello in formato JSON, impostare hello `type` proprietà hello `format` sezione troppo**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="57a3f-194">If you want tooparse hello JSON files or write hello data in JSON format, set hello `type` property in hello `format` section too**JsonFormat**.</span></span> <span data-ttu-id="57a3f-195">È inoltre possibile specificare i seguenti hello **facoltativo** proprietà hello `format` sezione.</span><span class="sxs-lookup"><span data-stu-id="57a3f-195">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="57a3f-196">Vedere [JsonFormat esempio](#jsonformat-example) sezione su come tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="57a3f-196">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="57a3f-197">Proprietà</span><span class="sxs-lookup"><span data-stu-id="57a3f-197">Property</span></span> | <span data-ttu-id="57a3f-198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57a3f-198">Description</span></span> | <span data-ttu-id="57a3f-199">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="57a3f-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="57a3f-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="57a3f-200">filePattern</span></span> |<span data-ttu-id="57a3f-201">Indicano il motivo di hello dei dati archiviati in ogni file JSON.</span><span class="sxs-lookup"><span data-stu-id="57a3f-201">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="57a3f-202">I valori consentiti sono: **setOfObjects** e **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="57a3f-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="57a3f-203">Hello **predefinito** valore **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="57a3f-203">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="57a3f-204">Vedere la sezione [Modelli di file JSON](#json-file-patterns) per i dettagli su questi modelli.</span><span class="sxs-lookup"><span data-stu-id="57a3f-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="57a3f-205">No</span><span class="sxs-lookup"><span data-stu-id="57a3f-205">No</span></span> |
| <span data-ttu-id="57a3f-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="57a3f-206">jsonNodeReference</span></span> | <span data-ttu-id="57a3f-207">Se si desidera tooiterate ed estrarre i dati da oggetti hello all'interno di una matrice di un campo con hello stesso schema, specificare il percorso JSON hello della matrice.</span><span class="sxs-lookup"><span data-stu-id="57a3f-207">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="57a3f-208">Questa proprietà è supportata solo quando si copiano i dati dai file JSON.</span><span class="sxs-lookup"><span data-stu-id="57a3f-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="57a3f-209">No</span><span class="sxs-lookup"><span data-stu-id="57a3f-209">No</span></span> |
| <span data-ttu-id="57a3f-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="57a3f-210">jsonPathDefinition</span></span> | <span data-ttu-id="57a3f-211">Specificare l'espressione di percorso JSON hello per ogni mapping di colonna con un nome di colonna personalizzati (inizia con lettere minuscole).</span><span class="sxs-lookup"><span data-stu-id="57a3f-211">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="57a3f-212">Questa proprietà è supportata solo quando si copiano i dati dai file JSON ed è possibile estrarre i dati dall'oggetto o dalla matrice.</span><span class="sxs-lookup"><span data-stu-id="57a3f-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="57a3f-213">Per i campi nell'oggetto radice, iniziare con $ radice; per i campi nella matrice hello scelto da `jsonNodeReference` proprietà inizio dall'elemento di matrice hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-213">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="57a3f-214">Vedere [JsonFormat esempio](#jsonformat-example) sezione su come tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="57a3f-214">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="57a3f-215">No</span><span class="sxs-lookup"><span data-stu-id="57a3f-215">No</span></span> |
| <span data-ttu-id="57a3f-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="57a3f-216">encodingName</span></span> |<span data-ttu-id="57a3f-217">Specificare il nome della codifica di hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-217">Specify hello encoding name.</span></span> <span data-ttu-id="57a3f-218">Per hello l'elenco di nomi di codifica validi, vedere: [EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) proprietà.</span><span class="sxs-lookup"><span data-stu-id="57a3f-218">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="57a3f-219">Ad esempio: windows-1250 o shift_jis.</span><span class="sxs-lookup"><span data-stu-id="57a3f-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="57a3f-220">Hello **predefinito** valore: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="57a3f-220">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="57a3f-221">No</span><span class="sxs-lookup"><span data-stu-id="57a3f-221">No</span></span> |
| <span data-ttu-id="57a3f-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="57a3f-222">nestingSeparator</span></span> |<span data-ttu-id="57a3f-223">Carattere usato tooseparate livelli di annidamento.</span><span class="sxs-lookup"><span data-stu-id="57a3f-223">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="57a3f-224">valore predefinito di Hello è '.' (punto).</span><span class="sxs-lookup"><span data-stu-id="57a3f-224">hello default value is '.' (dot).</span></span> |<span data-ttu-id="57a3f-225">No</span><span class="sxs-lookup"><span data-stu-id="57a3f-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="57a3f-226">Modelli di file JSON</span><span class="sxs-lookup"><span data-stu-id="57a3f-226">JSON file patterns</span></span>

<span data-ttu-id="57a3f-227">Attività di copia può analizzare hello seguito modelli di file JSON:</span><span class="sxs-lookup"><span data-stu-id="57a3f-227">Copy activity can parse hello following patterns of JSON files:</span></span>

- <span data-ttu-id="57a3f-228">**Tipo I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="57a3f-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="57a3f-229">Ogni file contiene un solo oggetto o più oggetti con delimitatori di riga/concatenati.</span><span class="sxs-lookup"><span data-stu-id="57a3f-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="57a3f-230">Quando si sceglie questa opzione in un set di dati di output, l'attività di copia produce un singolo file JSON con un oggetto per riga (delimitato da riga).</span><span class="sxs-lookup"><span data-stu-id="57a3f-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="57a3f-231">**Esempio di JSON a oggetto singolo**</span><span class="sxs-lookup"><span data-stu-id="57a3f-231">**single object JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * <span data-ttu-id="57a3f-232">**Esempio di JSON con delimitatori di riga**</span><span class="sxs-lookup"><span data-stu-id="57a3f-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="57a3f-233">**Esempio di JSON concatenati**</span><span class="sxs-lookup"><span data-stu-id="57a3f-233">**concatenated JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- <span data-ttu-id="57a3f-234">**Tipo II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="57a3f-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="57a3f-235">Ogni file contiene una matrice di oggetti.</span><span class="sxs-lookup"><span data-stu-id="57a3f-235">Each file contains an array of objects.</span></span>

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

### <a name="jsonformat-example"></a><span data-ttu-id="57a3f-236">Esempio JsonFormat</span><span class="sxs-lookup"><span data-stu-id="57a3f-236">JsonFormat example</span></span>

<span data-ttu-id="57a3f-237">**Caso 1: Copia di dati dai file JSON**</span><span class="sxs-lookup"><span data-stu-id="57a3f-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="57a3f-238">Vedere hello seguito due esempi di quando si copiano dati da file JSON.</span><span class="sxs-lookup"><span data-stu-id="57a3f-238">See hello following two samples when copying data from JSON files.</span></span> <span data-ttu-id="57a3f-239">Hello toonote punti generico:</span><span class="sxs-lookup"><span data-stu-id="57a3f-239">hello generic points toonote:</span></span>

<span data-ttu-id="57a3f-240">**Esempio 1: Estrarre i dati dall'oggetto e dalla matrice**</span><span class="sxs-lookup"><span data-stu-id="57a3f-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="57a3f-241">In questo esempio, si prevede un oggetto JSON radice esegue il mapping di record toosingle risultati tabulari.</span><span class="sxs-lookup"><span data-stu-id="57a3f-241">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="57a3f-242">Se si dispone di un file JSON con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="57a3f-242">If you have a JSON file with hello following content:</span></span>  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
<span data-ttu-id="57a3f-243">e si desidera toocopy in una tabella SQL di Azure seguenti hello formattare, estrarre dati da entrambi gli oggetti e di matrice:</span><span class="sxs-lookup"><span data-stu-id="57a3f-243">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="57a3f-244">id</span><span class="sxs-lookup"><span data-stu-id="57a3f-244">id</span></span> | <span data-ttu-id="57a3f-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="57a3f-245">deviceType</span></span> | <span data-ttu-id="57a3f-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="57a3f-246">targetResourceType</span></span> | <span data-ttu-id="57a3f-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="57a3f-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="57a3f-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="57a3f-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="57a3f-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="57a3f-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="57a3f-250">PC</span><span class="sxs-lookup"><span data-stu-id="57a3f-250">PC</span></span> | <span data-ttu-id="57a3f-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="57a3f-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="57a3f-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="57a3f-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="57a3f-253">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="57a3f-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="57a3f-254">set di dati input Hello con **JsonFormat** tipo viene definito come segue: (definizione parziale con solo parti pertinenti di hello).</span><span class="sxs-lookup"><span data-stu-id="57a3f-254">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="57a3f-255">Più in particolare:</span><span class="sxs-lookup"><span data-stu-id="57a3f-255">More specifically:</span></span>

- <span data-ttu-id="57a3f-256">`structure`Definisce i nomi di colonna hello personalizzato e il tipo di dati corrispondente hello durante la conversione dei dati tootabular.</span><span class="sxs-lookup"><span data-stu-id="57a3f-256">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="57a3f-257">Questa sezione è **facoltativo** a meno che non è necessario toodo mapping della colonna.</span><span class="sxs-lookup"><span data-stu-id="57a3f-257">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="57a3f-258">Vedere [eseguire il mapping di colonne di set di dati di origine del dataset colonne toodestination](data-factory-map-columns.md) sezione per ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="57a3f-258">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="57a3f-259">`jsonPathDefinition`Specifica il percorso JSON hello per ogni colonna che indica dove tooextract hello dati.</span><span class="sxs-lookup"><span data-stu-id="57a3f-259">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="57a3f-260">dati toocopy dalla matrice, è possibile utilizzare **Property matrice [x]** tooextract valore hello data proprietà dall'oggetto x hello oppure è possibile utilizzare  **matrice [*] Property** toofind valore di Hello da qualsiasi oggetto che contiene questo tipo proprietà.</span><span class="sxs-lookup"><span data-stu-id="57a3f-260">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

<span data-ttu-id="57a3f-261">**Esempio 2:: applicare più oggetti con hello stesso modello di matrice**</span><span class="sxs-lookup"><span data-stu-id="57a3f-261">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="57a3f-262">In questo esempio, si prevede un oggetto tootransform JSON radice in più record nel risultato tabulare.</span><span class="sxs-lookup"><span data-stu-id="57a3f-262">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="57a3f-263">Se si dispone di un file JSON con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="57a3f-263">If you have a JSON file with hello following content:</span></span>  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
<span data-ttu-id="57a3f-264">e si desidera toocopy in una tabella SQL di Azure seguenti hello formatta, per rendere bidimensionali i dati di hello all'interno di matrice hello e cross join con informazioni radice comune hello:</span><span class="sxs-lookup"><span data-stu-id="57a3f-264">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="57a3f-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="57a3f-265">ordernumber</span></span> | <span data-ttu-id="57a3f-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="57a3f-266">orderdate</span></span> | <span data-ttu-id="57a3f-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="57a3f-267">order_pd</span></span> | <span data-ttu-id="57a3f-268">order_price</span><span class="sxs-lookup"><span data-stu-id="57a3f-268">order_price</span></span> | <span data-ttu-id="57a3f-269">city</span><span class="sxs-lookup"><span data-stu-id="57a3f-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="57a3f-270">01</span><span class="sxs-lookup"><span data-stu-id="57a3f-270">01</span></span> | <span data-ttu-id="57a3f-271">20170122</span><span class="sxs-lookup"><span data-stu-id="57a3f-271">20170122</span></span> | <span data-ttu-id="57a3f-272">P1</span><span class="sxs-lookup"><span data-stu-id="57a3f-272">P1</span></span> | <span data-ttu-id="57a3f-273">23</span><span class="sxs-lookup"><span data-stu-id="57a3f-273">23</span></span> | <span data-ttu-id="57a3f-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="57a3f-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="57a3f-275">01</span><span class="sxs-lookup"><span data-stu-id="57a3f-275">01</span></span> | <span data-ttu-id="57a3f-276">20170122</span><span class="sxs-lookup"><span data-stu-id="57a3f-276">20170122</span></span> | <span data-ttu-id="57a3f-277">P2</span><span class="sxs-lookup"><span data-stu-id="57a3f-277">P2</span></span> | <span data-ttu-id="57a3f-278">13</span><span class="sxs-lookup"><span data-stu-id="57a3f-278">13</span></span> | <span data-ttu-id="57a3f-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="57a3f-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="57a3f-280">01</span><span class="sxs-lookup"><span data-stu-id="57a3f-280">01</span></span> | <span data-ttu-id="57a3f-281">20170122</span><span class="sxs-lookup"><span data-stu-id="57a3f-281">20170122</span></span> | <span data-ttu-id="57a3f-282">P3</span><span class="sxs-lookup"><span data-stu-id="57a3f-282">P3</span></span> | <span data-ttu-id="57a3f-283">231</span><span class="sxs-lookup"><span data-stu-id="57a3f-283">231</span></span> | <span data-ttu-id="57a3f-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="57a3f-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="57a3f-285">set di dati input Hello con **JsonFormat** tipo viene definito come segue: (definizione parziale con solo parti pertinenti di hello).</span><span class="sxs-lookup"><span data-stu-id="57a3f-285">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="57a3f-286">Più in particolare:</span><span class="sxs-lookup"><span data-stu-id="57a3f-286">More specifically:</span></span>

- <span data-ttu-id="57a3f-287">`structure`Definisce i nomi di colonna hello personalizzato e il tipo di dati corrispondente hello durante la conversione dei dati tootabular.</span><span class="sxs-lookup"><span data-stu-id="57a3f-287">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="57a3f-288">Questa sezione è **facoltativo** a meno che non è necessario toodo mapping della colonna.</span><span class="sxs-lookup"><span data-stu-id="57a3f-288">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="57a3f-289">Vedere [eseguire il mapping di colonne di set di dati di origine del dataset colonne toodestination](data-factory-map-columns.md) sezione per ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="57a3f-289">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="57a3f-290">`jsonNodeReference`indica tooiterate ed estrarre i dati da oggetti hello con hello stesso modello in **matrice** orderlines.</span><span class="sxs-lookup"><span data-stu-id="57a3f-290">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="57a3f-291">`jsonPathDefinition`Specifica il percorso JSON hello per ogni colonna che indica dove tooextract hello dati.</span><span class="sxs-lookup"><span data-stu-id="57a3f-291">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="57a3f-292">In questo esempio, "ordernumber", "orderdate" e "city" sono in oggetto di primo livello con JSON inizi con "$"., mentre "order_pd" e "order_price" sono definiti con percorso derivata dall'elemento di matrice hello senza "$"..</span><span class="sxs-lookup"><span data-stu-id="57a3f-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

<span data-ttu-id="57a3f-293">**Si noti hello seguenti punti:**</span><span class="sxs-lookup"><span data-stu-id="57a3f-293">**Note hello following points:**</span></span>

* <span data-ttu-id="57a3f-294">Se hello `structure` e `jsonPathDefinition` non sono definiti nel set di dati con Data Factory di hello hello attività di copia rileva hello schema dal primo oggetto hello e rendere flat intero oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-294">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="57a3f-295">Se l'input JSON hello dispone di una matrice, per impostazione predefinita hello attività di copia converte il valore di matrice intera hello in una stringa.</span><span class="sxs-lookup"><span data-stu-id="57a3f-295">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="57a3f-296">È possibile scegliere i dati tooextract tramite `jsonNodeReference` e/o `jsonPathDefinition`, o ignorarlo se non viene specificata in `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="57a3f-296">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="57a3f-297">Se sono presenti duplicati nomi hello allo stesso livello, hello attività di copia selezioni hello ultimo.</span><span class="sxs-lookup"><span data-stu-id="57a3f-297">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="57a3f-298">I nomi delle proprietà distinguono tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="57a3f-298">Property names are case-sensitive.</span></span> <span data-ttu-id="57a3f-299">Due proprietà con lo stesso nome ma con una combinazione differente di maiuscole e minuscole vengono considerate come due proprietà diverse.</span><span class="sxs-lookup"><span data-stu-id="57a3f-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="57a3f-300">**Caso 2: Scrittura del file di dati tooJSON**</span><span class="sxs-lookup"><span data-stu-id="57a3f-300">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="57a3f-301">Se si dispone di hello in Database SQL nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="57a3f-301">If you have hello following table in SQL Database:</span></span>

| <span data-ttu-id="57a3f-302">id</span><span class="sxs-lookup"><span data-stu-id="57a3f-302">id</span></span> | <span data-ttu-id="57a3f-303">order_date</span><span class="sxs-lookup"><span data-stu-id="57a3f-303">order_date</span></span> | <span data-ttu-id="57a3f-304">order_price</span><span class="sxs-lookup"><span data-stu-id="57a3f-304">order_price</span></span> | <span data-ttu-id="57a3f-305">order_by</span><span class="sxs-lookup"><span data-stu-id="57a3f-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="57a3f-306">1</span><span class="sxs-lookup"><span data-stu-id="57a3f-306">1</span></span> | <span data-ttu-id="57a3f-307">20170119</span><span class="sxs-lookup"><span data-stu-id="57a3f-307">20170119</span></span> | <span data-ttu-id="57a3f-308">2000</span><span class="sxs-lookup"><span data-stu-id="57a3f-308">2000</span></span> | <span data-ttu-id="57a3f-309">David</span><span class="sxs-lookup"><span data-stu-id="57a3f-309">David</span></span> |
| <span data-ttu-id="57a3f-310">2</span><span class="sxs-lookup"><span data-stu-id="57a3f-310">2</span></span> | <span data-ttu-id="57a3f-311">20170120</span><span class="sxs-lookup"><span data-stu-id="57a3f-311">20170120</span></span> | <span data-ttu-id="57a3f-312">3500</span><span class="sxs-lookup"><span data-stu-id="57a3f-312">3500</span></span> | <span data-ttu-id="57a3f-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="57a3f-313">Patrick</span></span> |
| <span data-ttu-id="57a3f-314">3</span><span class="sxs-lookup"><span data-stu-id="57a3f-314">3</span></span> | <span data-ttu-id="57a3f-315">20170121</span><span class="sxs-lookup"><span data-stu-id="57a3f-315">20170121</span></span> | <span data-ttu-id="57a3f-316">4000</span><span class="sxs-lookup"><span data-stu-id="57a3f-316">4000</span></span> | <span data-ttu-id="57a3f-317">Jason</span><span class="sxs-lookup"><span data-stu-id="57a3f-317">Jason</span></span> |

<span data-ttu-id="57a3f-318">e per ogni record, si supponga che oggetto JSON di toowrite tooa hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="57a3f-318">and for each record, you expect toowrite tooa JSON object in hello following format:</span></span>
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

<span data-ttu-id="57a3f-319">set di dati con output di Hello **JsonFormat** tipo viene definito come segue: (definizione parziale con solo parti pertinenti di hello).</span><span class="sxs-lookup"><span data-stu-id="57a3f-319">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="57a3f-320">In particolare, `structure` sezione definisce i nomi delle proprietà hello personalizzata nel file di destinazione, `nestingSeparator` (valore predefinito è ".") sono a livello di nidificazione hello tooidentify utilizzato dal nome hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-320">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") are used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="57a3f-321">Questa sezione è **facoltativo** a meno che si desidera toochange hello proprietà nome, il confronto con il nome di colonna di origine o annidare alcune proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-321">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

## <a name="avro-format"></a><span data-ttu-id="57a3f-322">Formato AVRO</span><span class="sxs-lookup"><span data-stu-id="57a3f-322">AVRO format</span></span>
<span data-ttu-id="57a3f-323">Se si desidera tooparse hello Avro file o scrivono dati hello in formato Avro, impostare hello `format` `type` proprietà troppo**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="57a3f-323">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="57a3f-324">Non è necessario toospecify delle proprietà nella sezione formato hello nella sezione typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-324">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="57a3f-325">Esempio:</span><span class="sxs-lookup"><span data-stu-id="57a3f-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="57a3f-326">formato Avro di toouse in una tabella Hive, è possibile fare riferimento troppo[esercitazione su Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="57a3f-326">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="57a3f-327">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="57a3f-327">Note hello following points:</span></span>  

* <span data-ttu-id="57a3f-328">I [tipi di dati complessi](http://avro.apache.org/docs/current/spec.html#schema_complex) non sono supportati (record, enumerazioni, matrici, mappe, unioni e dati fissi).</span><span class="sxs-lookup"><span data-stu-id="57a3f-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="57a3f-329">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="57a3f-329">ORC format</span></span>
<span data-ttu-id="57a3f-330">Se si desidera tooparse hello ORC file o scrivono dati hello in formato ORC, impostare hello `format` `type` proprietà troppo**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="57a3f-330">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="57a3f-331">Non è necessario toospecify delle proprietà nella sezione formato hello nella sezione typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-331">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="57a3f-332">Esempio:</span><span class="sxs-lookup"><span data-stu-id="57a3f-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="57a3f-333">Se non si desidera copiare i file ORC **come-è** tra sedi locali e cloud archivi dati, è necessario tooinstall hello 8 JRE (Java Runtime Environment) nel computer gateway.</span><span class="sxs-lookup"><span data-stu-id="57a3f-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="57a3f-334">Per un gateway a 64 bit è necessario JRE a 64 bit, mentre per un gateway a 32 bit è necessario JRE a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="57a3f-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="57a3f-335">Entrambe le versioni sono disponibili [qui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="57a3f-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="57a3f-336">Scegliere hello più appropriato.</span><span class="sxs-lookup"><span data-stu-id="57a3f-336">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="57a3f-337">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="57a3f-337">Note hello following points:</span></span>

* <span data-ttu-id="57a3f-338">Tipi di dati complessi non sono supportati (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="57a3f-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="57a3f-339">Il file ORC dispone di tre [opzioni relative alla compressione](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="57a3f-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="57a3f-340">Data Factory supporta la lettura dei dati dal file ORC in uno di questi formati compressi.</span><span class="sxs-lookup"><span data-stu-id="57a3f-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="57a3f-341">Usa compressione hello codec è nei dati di hello metadati tooread hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-341">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="57a3f-342">Tuttavia, durante la scrittura di file ORC tooan, Data Factory sceglie ZLIB, hello predefinito per ORC.</span><span class="sxs-lookup"><span data-stu-id="57a3f-342">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="57a3f-343">Attualmente non è disponibile alcuna opzione toooverride questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="57a3f-343">Currently, there is no option toooverride this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="57a3f-344">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="57a3f-344">Parquet format</span></span>
<span data-ttu-id="57a3f-345">Se si desidera tooparse hello Parquet file o scrivono dati hello in formato Parquet, impostare hello `format` `type` proprietà troppo**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="57a3f-345">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="57a3f-346">Non è necessario toospecify delle proprietà nella sezione formato hello nella sezione typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-346">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="57a3f-347">Esempio:</span><span class="sxs-lookup"><span data-stu-id="57a3f-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="57a3f-348">Se non si desidera copiare i file Parquet **come-è** tra sedi locali e cloud archivi dati, è necessario tooinstall hello 8 JRE (Java Runtime Environment) nel computer gateway.</span><span class="sxs-lookup"><span data-stu-id="57a3f-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="57a3f-349">Per un gateway a 64 bit è necessario JRE a 64 bit, mentre per un gateway a 32 bit è necessario JRE a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="57a3f-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="57a3f-350">Entrambe le versioni sono disponibili [qui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="57a3f-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="57a3f-351">Scegliere hello più appropriato.</span><span class="sxs-lookup"><span data-stu-id="57a3f-351">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="57a3f-352">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="57a3f-352">Note hello following points:</span></span>

* <span data-ttu-id="57a3f-353">Tipi di dati complessi non sono supportati (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="57a3f-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="57a3f-354">Dispone di file parquet hello relativi alla compressione le opzioni seguenti: NONE, SNAPPY GZIP e LZO.</span><span class="sxs-lookup"><span data-stu-id="57a3f-354">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="57a3f-355">Data Factory supporta la lettura dei dati dal file ORC in uno di questi formati compressi.</span><span class="sxs-lookup"><span data-stu-id="57a3f-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="57a3f-356">Usa il codec di compressione hello nei dati di hello metadati tooread hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-356">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="57a3f-357">Tuttavia, durante la scrittura di file Parquet tooa, Data Factory sceglie SNAPPY, hello predefinito per il formato Parquet.</span><span class="sxs-lookup"><span data-stu-id="57a3f-357">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="57a3f-358">Attualmente non è disponibile alcuna opzione toooverride questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="57a3f-358">Currently, there is no option toooverride this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="57a3f-359">Supporto della compressione</span><span class="sxs-lookup"><span data-stu-id="57a3f-359">Compression support</span></span>
<span data-ttu-id="57a3f-360">L'elaborazione di set di dati di grandi dimensioni può causare colli di bottiglia I/O e di rete.</span><span class="sxs-lookup"><span data-stu-id="57a3f-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="57a3f-361">Di conseguenza, i dati compressi in archivi possano non solo velocizzare il trasferimento dei dati attraverso la rete hello e risparmiare spazio su disco, ma anche visualizzare miglioramenti significativi delle prestazioni di elaborazione di big data.</span><span class="sxs-lookup"><span data-stu-id="57a3f-361">Therefore, compressed data in stores can not only speed up data transfer across hello network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="57a3f-362">Attualmente, la compressione è supportata per gli archivi di dati basati su file, ad esempio BLOB di Azure o il file system locale.</span><span class="sxs-lookup"><span data-stu-id="57a3f-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="57a3f-363">la compressione toospecify per un set di dati, utilizzare hello **compressione** proprietà hello set di dati JSON come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="57a3f-363">toospecify compression for a dataset, use hello **compression** property in hello dataset JSON as in hello following example:</span></span>   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

<span data-ttu-id="57a3f-364">Si supponga che il set di dati di hello esempio viene utilizzato come output di hello di un'attività di copia, hello Copia attività comprime hello i dati di output con i codec GZIP con rapporto ottimale e quindi scrivere dati hello compresso in un file denominato pagecounts.csv.gz in hello archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="57a3f-364">Suppose hello sample dataset is used as hello output of a copy activity, hello copy activity compresses hello output data with GZIP codec using optimal ratio and then write hello compressed data into a file named pagecounts.csv.gz in hello Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="57a3f-365">Le impostazioni di compressione non sono supportate per i dati in hello **AvroFormat**, **OrcFormat**, o **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="57a3f-365">Compression settings are not supported for data in hello **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="57a3f-366">Durante la lettura di file in tali formati, Data Factory rileva e utilizza il codec di compressione hello nei metadati hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-366">When reading files in these formats, Data Factory detects and uses hello compression codec in hello metadata.</span></span> <span data-ttu-id="57a3f-367">Quando si scrivono toofiles in questi formati, Data Factory sceglie codec di compressione hello predefinito per tale formato.</span><span class="sxs-lookup"><span data-stu-id="57a3f-367">When writing toofiles in these formats, Data Factory chooses hello default compression codec for that format.</span></span> <span data-ttu-id="57a3f-368">ad esempio ZLIB per OrcFormat e SNAPPY per ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="57a3f-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="57a3f-369">Hello **compressione** sezione ha due proprietà:</span><span class="sxs-lookup"><span data-stu-id="57a3f-369">hello **compression** section has two properties:</span></span>  

* <span data-ttu-id="57a3f-370">**Tipo:** codec di compressione hello, che può essere **GZIP**, **Deflate**, **BZIP2**, o **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="57a3f-370">**Type:** hello compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="57a3f-371">**Livello:** rapporto di compressione hello, che può essere **ottimale** o **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="57a3f-371">**Level:** hello compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="57a3f-372">**Più veloce:** hello compressione deve completare l'operazione più rapidamente possibile, anche se non viene compresso in modo ottimale file risultante hello.</span><span class="sxs-lookup"><span data-stu-id="57a3f-372">**Fastest:** hello compression operation should complete as quickly as possible, even if hello resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="57a3f-373">**Ottimale**: operazione di compressione hello deve essere in modo ottimale compresso, anche se l'operazione di hello accetta un toocomplete di tempo più lungo.</span><span class="sxs-lookup"><span data-stu-id="57a3f-373">**Optimal**: hello compression operation should be optimally compressed, even if hello operation takes a longer time toocomplete.</span></span>

    <span data-ttu-id="57a3f-374">Per maggiori informazioni, vedere l'argomento relativo al [livello di compressione](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) .</span><span class="sxs-lookup"><span data-stu-id="57a3f-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="57a3f-375">Quando si specifica `compression` proprietà in un set di dati input JSON, pipeline hello può leggere dati compressi di origine di hello e quando si specificano proprietà hello in un set di dati di output JSON, l'attività di copia hello può scrivere destinazione toohello dati compressi.</span><span class="sxs-lookup"><span data-stu-id="57a3f-375">When you specify `compression` property in an input dataset JSON, hello pipeline can read compressed data from hello source; and when you specify hello property in an output dataset JSON, hello copy activity can write compressed data toohello destination.</span></span> <span data-ttu-id="57a3f-376">Di seguito vengono forniti alcuni scenari di esempio:</span><span class="sxs-lookup"><span data-stu-id="57a3f-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="57a3f-377">Leggere i dati compressi GZIP da un blob di Azure, decomprimono e scrivere i database SQL di Azure tooan dati dei risultati.</span><span class="sxs-lookup"><span data-stu-id="57a3f-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data tooan Azure SQL database.</span></span> <span data-ttu-id="57a3f-378">Definire i set di dati input per i Blob di Azure hello con hello `compression` `type` proprietà JSON come GZIP.</span><span class="sxs-lookup"><span data-stu-id="57a3f-378">You define hello input Azure Blob dataset with hello `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="57a3f-379">Leggere dati da un file di testo dal File System di on-premise, comprimere utilizzando il formato GZip e scrivere hello compresso tooan di dati blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="57a3f-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write hello compressed data tooan Azure blob.</span></span> <span data-ttu-id="57a3f-380">Si definisce un set di dati di output Blob di Azure con hello `compression` `type` proprietà JSON come GZip.</span><span class="sxs-lookup"><span data-stu-id="57a3f-380">You define an output Azure Blob dataset with hello `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="57a3f-381">File con estensione zip di lettura dal server FTP, decomprimono i file hello tooget all'interno e inserite tali file in archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="57a3f-381">Read .zip file from FTP server, decompress it tooget hello files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="57a3f-382">Si definisce un set di dati input FTP con hello `compression` `type` proprietà JSON come ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="57a3f-382">You define an input FTP dataset with hello `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="57a3f-383">Leggere i dati compressi GZIP da un blob di Azure, decomprimono, comprimerlo BZIP2 e scrivere dati di risultati tooan blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="57a3f-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data tooan Azure blob.</span></span> <span data-ttu-id="57a3f-384">Definire i set di dati input per i Blob di Azure hello con `compression` `type` impostare tooGZIP e set di dati di output con hello `compression` `type` impostare tooBZIP2 in questo caso.</span><span class="sxs-lookup"><span data-stu-id="57a3f-384">You define hello input Azure Blob dataset with `compression` `type` set tooGZIP and hello output dataset with `compression` `type` set tooBZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="57a3f-385">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="57a3f-385">Next steps</span></span>
<span data-ttu-id="57a3f-386">Vedere i seguenti articoli per gli archivi di dati basati su file supportati da Azure Data Factory hello:</span><span class="sxs-lookup"><span data-stu-id="57a3f-386">See hello following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="57a3f-387">Archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="57a3f-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="57a3f-388">Archivio Data Lake di Azure</span><span class="sxs-lookup"><span data-stu-id="57a3f-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="57a3f-389">FTP</span><span class="sxs-lookup"><span data-stu-id="57a3f-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="57a3f-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="57a3f-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="57a3f-391">File system</span><span class="sxs-lookup"><span data-stu-id="57a3f-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="57a3f-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="57a3f-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
