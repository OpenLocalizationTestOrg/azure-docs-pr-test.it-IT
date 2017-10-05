---
title: File e formati di compressione in Azure Data Factory | Documentazione Microsoft
description: Informazioni sui formati di file supportati da Azure Data Factory.
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
ms.openlocfilehash: f4746e0dd249e417b8077a9bc733d2886daafdf2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="000db-104">Informazioni sui formati di compressione e sui file supportati da Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="000db-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="000db-105">*Questo argomento si applica ai connettori seguenti: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [BLOB di Azure](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [file system](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md) e [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="000db-105">*This topic applies to the following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="000db-106">Azure Data Factory supporta i tipi di formato di file seguenti:</span><span class="sxs-lookup"><span data-stu-id="000db-106">Azure Data Factory supports the following file format types:</span></span>

* [<span data-ttu-id="000db-107">Formato testo</span><span class="sxs-lookup"><span data-stu-id="000db-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="000db-108">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="000db-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="000db-109">Formato Avro</span><span class="sxs-lookup"><span data-stu-id="000db-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="000db-110">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="000db-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="000db-111">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="000db-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="000db-112">Formato testo</span><span class="sxs-lookup"><span data-stu-id="000db-112">Text format</span></span>
<span data-ttu-id="000db-113">Se si vuole leggere da un file di testo o scrivere in un file di testo, impostare la proprietà `type` nella sezione `format` del set di dati **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="000db-113">If you want to read from a text file or write to a text file, set the `type` property in the `format` section of the dataset to **TextFormat**.</span></span> <span data-ttu-id="000db-114">È anche possibile specificare le proprietà **facoltative** seguenti nella sezione `format`.</span><span class="sxs-lookup"><span data-stu-id="000db-114">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="000db-115">Vedere la sezione [Esempio di TextFormat](#textformat-example) sulla configurazione.</span><span class="sxs-lookup"><span data-stu-id="000db-115">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="000db-116">Proprietà</span><span class="sxs-lookup"><span data-stu-id="000db-116">Property</span></span> | <span data-ttu-id="000db-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="000db-117">Description</span></span> | <span data-ttu-id="000db-118">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="000db-118">Allowed values</span></span> | <span data-ttu-id="000db-119">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="000db-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="000db-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="000db-120">columnDelimiter</span></span> |<span data-ttu-id="000db-121">Il carattere usato per separare le colonne in un file.</span><span class="sxs-lookup"><span data-stu-id="000db-121">The character used to separate columns in a file.</span></span> <span data-ttu-id="000db-122">È possibile usare un carattere non stampabile raro che è probabile non esista nei dati.</span><span class="sxs-lookup"><span data-stu-id="000db-122">You can consider to use a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="000db-123">Ad esempio, specificare "\u0001", che rappresenta l'inizio intestazione (SOH).</span><span class="sxs-lookup"><span data-stu-id="000db-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="000db-124">È consentito un solo carattere.</span><span class="sxs-lookup"><span data-stu-id="000db-124">Only one character is allowed.</span></span> <span data-ttu-id="000db-125">Il valore **predefinito** è la **virgola (",")**.</span><span class="sxs-lookup"><span data-stu-id="000db-125">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="000db-126">Per usare un carattere Unicode, vedere i [caratteri Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) per ottenere il codice corrispondente.</span><span class="sxs-lookup"><span data-stu-id="000db-126">To use a Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="000db-127">No</span><span class="sxs-lookup"><span data-stu-id="000db-127">No</span></span> |
| <span data-ttu-id="000db-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="000db-128">rowDelimiter</span></span> |<span data-ttu-id="000db-129">Il carattere usato per separare le righe in un file.</span><span class="sxs-lookup"><span data-stu-id="000db-129">The character used to separate rows in a file.</span></span> |<span data-ttu-id="000db-130">È consentito un solo carattere.</span><span class="sxs-lookup"><span data-stu-id="000db-130">Only one character is allowed.</span></span> <span data-ttu-id="000db-131">Sono consentiti i seguenti valori **predefiniti** in lettura: **["\r\n", "\r", "\n"]** e **"\r\n"** in scrittura.</span><span class="sxs-lookup"><span data-stu-id="000db-131">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="000db-132">No</span><span class="sxs-lookup"><span data-stu-id="000db-132">No</span></span> |
| <span data-ttu-id="000db-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="000db-133">escapeChar</span></span> |<span data-ttu-id="000db-134">Carattere speciale usato per eseguire l'escape di un delimitatore di colonna nel contenuto del file di input.</span><span class="sxs-lookup"><span data-stu-id="000db-134">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="000db-135">Per una tabella, è possibile specificare sia escapeChar che quoteChar.</span><span class="sxs-lookup"><span data-stu-id="000db-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="000db-136">È consentito un solo carattere.</span><span class="sxs-lookup"><span data-stu-id="000db-136">Only one character is allowed.</span></span> <span data-ttu-id="000db-137">Nessun valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="000db-137">No default value.</span></span> <br/><br/><span data-ttu-id="000db-138">Ad esempio, se è presente una virgola (",") come delimitatore di colonna, ma si desidera inserire un carattere virgola nel testo (ad esempio: "Hello, world"), è possibile definire "$" come carattere di escape e usare la stringa "Hello$, world" nell'origine.</span><span class="sxs-lookup"><span data-stu-id="000db-138">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="000db-139">No</span><span class="sxs-lookup"><span data-stu-id="000db-139">No</span></span> |
| <span data-ttu-id="000db-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="000db-140">quoteChar</span></span> |<span data-ttu-id="000db-141">Carattere usato per delimitare tra virgolette un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="000db-141">The character used to quote a string value.</span></span> <span data-ttu-id="000db-142">I delimitatori di colonne e righe tra virgolette sono considerati parte del valore stringa.</span><span class="sxs-lookup"><span data-stu-id="000db-142">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="000db-143">Questa proprietà è applicabile sia ai set di dati di input che a quelli di output.</span><span class="sxs-lookup"><span data-stu-id="000db-143">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="000db-144">Per una tabella, è possibile specificare sia escapeChar che quoteChar.</span><span class="sxs-lookup"><span data-stu-id="000db-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="000db-145">È consentito un solo carattere.</span><span class="sxs-lookup"><span data-stu-id="000db-145">Only one character is allowed.</span></span> <span data-ttu-id="000db-146">Nessun valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="000db-146">No default value.</span></span> <br/><br/><span data-ttu-id="000db-147">Ad esempio, se è presente una virgola (",") come delimitatore di colonna, ma si desidera inserire un carattere virgola nel testo (ad esempio: <Hello, world>), è possibile definire " (virgolette doppie) come carattere di virgolette e usare la stringa "Hello, world" nell'origine.</span><span class="sxs-lookup"><span data-stu-id="000db-147">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="000db-148">No</span><span class="sxs-lookup"><span data-stu-id="000db-148">No</span></span> |
| <span data-ttu-id="000db-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="000db-149">nullValue</span></span> |<span data-ttu-id="000db-150">Uno o più caratteri usati per rappresentare un valore null.</span><span class="sxs-lookup"><span data-stu-id="000db-150">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="000db-151">Uno o più caratteri.</span><span class="sxs-lookup"><span data-stu-id="000db-151">One or more characters.</span></span> <span data-ttu-id="000db-152">I valori **predefiniti** sono **"\N" e "NULL"** in lettura e **"\N"** in scrittura.</span><span class="sxs-lookup"><span data-stu-id="000db-152">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="000db-153">No</span><span class="sxs-lookup"><span data-stu-id="000db-153">No</span></span> |
| <span data-ttu-id="000db-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="000db-154">encodingName</span></span> |<span data-ttu-id="000db-155">Specificare il nome della codifica.</span><span class="sxs-lookup"><span data-stu-id="000db-155">Specify the encoding name.</span></span> |<span data-ttu-id="000db-156">Un nome di codifica valido.</span><span class="sxs-lookup"><span data-stu-id="000db-156">A valid encoding name.</span></span> <span data-ttu-id="000db-157">Vedere [Proprietà Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="000db-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="000db-158">Esempio: windows-1250 o shift_jis.</span><span class="sxs-lookup"><span data-stu-id="000db-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="000db-159">Il valore **predefinito** è **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="000db-159">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="000db-160">No</span><span class="sxs-lookup"><span data-stu-id="000db-160">No</span></span> |
| <span data-ttu-id="000db-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="000db-161">firstRowAsHeader</span></span> |<span data-ttu-id="000db-162">Specifica se considerare la prima riga come intestazione.</span><span class="sxs-lookup"><span data-stu-id="000db-162">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="000db-163">In un set di dati di input Data factory legge la prima riga come intestazione.</span><span class="sxs-lookup"><span data-stu-id="000db-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="000db-164">In un set di dati di output Data factory scrive la prima riga come intestazione.</span><span class="sxs-lookup"><span data-stu-id="000db-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="000db-165">Vedere [Scenari per l'uso di `firstRowAsHeader` e `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) per gli scenari di esempio.</span><span class="sxs-lookup"><span data-stu-id="000db-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="000db-166">True</span><span class="sxs-lookup"><span data-stu-id="000db-166">True</span></span><br/><span data-ttu-id="000db-167"><b>False (impostazione predefinita)</b></span><span class="sxs-lookup"><span data-stu-id="000db-167"><b>False (default)</b></span></span> |<span data-ttu-id="000db-168">No</span><span class="sxs-lookup"><span data-stu-id="000db-168">No</span></span> |
| <span data-ttu-id="000db-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="000db-169">skipLineCount</span></span> |<span data-ttu-id="000db-170">Indica il numero di righe da ignorare durante la lettura di dati da file di input.</span><span class="sxs-lookup"><span data-stu-id="000db-170">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="000db-171">Se sono specificati sia skipLineCount che firstRowAsHeader, le righe vengono ignorate e le informazioni di intestazione vengono lette dal file di input.</span><span class="sxs-lookup"><span data-stu-id="000db-171">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="000db-172">Vedere [Scenari per l'uso di `firstRowAsHeader` e `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) per gli scenari di esempio.</span><span class="sxs-lookup"><span data-stu-id="000db-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="000db-173">Integer</span><span class="sxs-lookup"><span data-stu-id="000db-173">Integer</span></span> |<span data-ttu-id="000db-174">No</span><span class="sxs-lookup"><span data-stu-id="000db-174">No</span></span> |
| <span data-ttu-id="000db-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="000db-175">treatEmptyAsNull</span></span> |<span data-ttu-id="000db-176">Specifica se considerare una stringa vuota o null come valore null durante la lettura di dati da un file di input.</span><span class="sxs-lookup"><span data-stu-id="000db-176">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="000db-177">**True (impostazione predefinita)**</span><span class="sxs-lookup"><span data-stu-id="000db-177">**True (default)**</span></span><br/><span data-ttu-id="000db-178">False</span><span class="sxs-lookup"><span data-stu-id="000db-178">False</span></span> |<span data-ttu-id="000db-179">No</span><span class="sxs-lookup"><span data-stu-id="000db-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="000db-180">Esempio di TextFormat</span><span class="sxs-lookup"><span data-stu-id="000db-180">TextFormat example</span></span>
<span data-ttu-id="000db-181">Nella definizione JSON seguente per un set di dati sono specificate alcune proprietà facoltative.</span><span class="sxs-lookup"><span data-stu-id="000db-181">In the following JSON definition for a dataset, some of the optional properties are specified.</span></span>

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

<span data-ttu-id="000db-182">Per usare `escapeChar` invece di `quoteChar`, sostituire la riga con `quoteChar` con l'elemento escapeChar seguente:</span><span class="sxs-lookup"><span data-stu-id="000db-182">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="000db-183">Scenari di utilizzo di firstRowAsHeader e skipLineCount</span><span class="sxs-lookup"><span data-stu-id="000db-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="000db-184">Si desidera copiare da un'origine non basata su file in un file di testo e aggiungere una riga di intestazione contenente i metadati dello schema (ad esempio: schema SQL).</span><span class="sxs-lookup"><span data-stu-id="000db-184">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="000db-185">Per questo scenario specificare `firstRowAsHeader` come true nel set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="000db-185">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="000db-186">Si desidera copiare da un file di testo contenente una riga di intestazione a un sink non basato su file ed eliminare tale riga.</span><span class="sxs-lookup"><span data-stu-id="000db-186">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="000db-187">Specificare `firstRowAsHeader` come true nel set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="000db-187">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="000db-188">Si desidera copiare da un file di testo e ignorare alcune righe all'inizio che non contengono né dati né un'intestazione.</span><span class="sxs-lookup"><span data-stu-id="000db-188">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="000db-189">Specificare `skipLineCount` per indicare il numero di righe da ignorare.</span><span class="sxs-lookup"><span data-stu-id="000db-189">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="000db-190">Se il resto del file contiene una riga di intestazione, è anche possibile specificare `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="000db-190">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="000db-191">Se sono specificati sia `skipLineCount` che `firstRowAsHeader`, le righe vengono ignorate e le informazioni di intestazione vengono lette dal file di input.</span><span class="sxs-lookup"><span data-stu-id="000db-191">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

## <a name="json-format"></a><span data-ttu-id="000db-192">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="000db-192">JSON format</span></span>
<span data-ttu-id="000db-193">Per **importare/esportare un file JSON senza modifiche in/da Azure Cosmos DB**, vedere la sezione [Importare/Esportare documenti JSON](data-factory-azure-documentdb-connector.md#importexport-json-documents) nell'articolo [Spostare dati da e verso Azure Cosmos DB](data-factory-azure-documentdb-connector.md).</span><span class="sxs-lookup"><span data-stu-id="000db-193">To **import/export a JSON file as-is into/from Azure Cosmos DB**, the see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="000db-194">Per analizzare i file JSON o scrivere i dati in formato JSON, impostare la proprietà `type` nella sezione `format` su **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="000db-194">If you want to parse the JSON files or write the data in JSON format, set the `type` property in the `format` section to **JsonFormat**.</span></span> <span data-ttu-id="000db-195">È anche possibile specificare le proprietà **facoltative** seguenti nella sezione `format`.</span><span class="sxs-lookup"><span data-stu-id="000db-195">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="000db-196">Vedere la sezione [Esempio JsonFormat](#jsonformat-example) sulla configurazione.</span><span class="sxs-lookup"><span data-stu-id="000db-196">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="000db-197">Proprietà</span><span class="sxs-lookup"><span data-stu-id="000db-197">Property</span></span> | <span data-ttu-id="000db-198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="000db-198">Description</span></span> | <span data-ttu-id="000db-199">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="000db-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="000db-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="000db-200">filePattern</span></span> |<span data-ttu-id="000db-201">Indicare il modello dei dati archiviati in ogni file JSON.</span><span class="sxs-lookup"><span data-stu-id="000db-201">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="000db-202">I valori consentiti sono: **setOfObjects** e **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="000db-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="000db-203">Il valore **predefinito** è **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="000db-203">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="000db-204">Vedere la sezione [Modelli di file JSON](#json-file-patterns) per i dettagli su questi modelli.</span><span class="sxs-lookup"><span data-stu-id="000db-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="000db-205">No</span><span class="sxs-lookup"><span data-stu-id="000db-205">No</span></span> |
| <span data-ttu-id="000db-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="000db-206">jsonNodeReference</span></span> | <span data-ttu-id="000db-207">Per eseguire l'iterazione dei dati ed estrarli dagli oggetti presenti nel campo di una matrice con lo stesso modello, specificare il percorso JSON di tale matrice.</span><span class="sxs-lookup"><span data-stu-id="000db-207">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="000db-208">Questa proprietà è supportata solo quando si copiano i dati dai file JSON.</span><span class="sxs-lookup"><span data-stu-id="000db-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="000db-209">No</span><span class="sxs-lookup"><span data-stu-id="000db-209">No</span></span> |
| <span data-ttu-id="000db-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="000db-210">jsonPathDefinition</span></span> | <span data-ttu-id="000db-211">Specificare l'espressione del percorso JSON per ogni mapping colonne con un nome di colonna personalizzato. Iniziare con una lettera minuscola.</span><span class="sxs-lookup"><span data-stu-id="000db-211">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="000db-212">Questa proprietà è supportata solo quando si copiano i dati dai file JSON ed è possibile estrarre i dati dall'oggetto o dalla matrice.</span><span class="sxs-lookup"><span data-stu-id="000db-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="000db-213">Per i campi sotto l'oggetto radice, iniziare con la radice $. Per i campi nella matrice scelta dalla proprietà `jsonNodeReference`, iniziare dall'elemento matrice.</span><span class="sxs-lookup"><span data-stu-id="000db-213">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="000db-214">Vedere la sezione [Esempio JsonFormat](#jsonformat-example) sulla configurazione.</span><span class="sxs-lookup"><span data-stu-id="000db-214">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="000db-215">No</span><span class="sxs-lookup"><span data-stu-id="000db-215">No</span></span> |
| <span data-ttu-id="000db-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="000db-216">encodingName</span></span> |<span data-ttu-id="000db-217">Specificare il nome della codifica.</span><span class="sxs-lookup"><span data-stu-id="000db-217">Specify the encoding name.</span></span> <span data-ttu-id="000db-218">Per l'elenco di nomi di codifica validi, vedere: Proprietà [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) .</span><span class="sxs-lookup"><span data-stu-id="000db-218">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="000db-219">Ad esempio: windows-1250 o shift_jis.</span><span class="sxs-lookup"><span data-stu-id="000db-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="000db-220">Il valore **predefinito** è **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="000db-220">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="000db-221">No</span><span class="sxs-lookup"><span data-stu-id="000db-221">No</span></span> |
| <span data-ttu-id="000db-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="000db-222">nestingSeparator</span></span> |<span data-ttu-id="000db-223">Carattere utilizzato per separare i livelli di nidificazione.</span><span class="sxs-lookup"><span data-stu-id="000db-223">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="000db-224">Il valore predefinito è "." (punto).</span><span class="sxs-lookup"><span data-stu-id="000db-224">The default value is '.' (dot).</span></span> |<span data-ttu-id="000db-225">No</span><span class="sxs-lookup"><span data-stu-id="000db-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="000db-226">Modelli di file JSON</span><span class="sxs-lookup"><span data-stu-id="000db-226">JSON file patterns</span></span>

<span data-ttu-id="000db-227">L'attività di copia può eseguire l'analisi dei seguenti modelli di file JSON:</span><span class="sxs-lookup"><span data-stu-id="000db-227">Copy activity can parse the following patterns of JSON files:</span></span>

- <span data-ttu-id="000db-228">**Tipo I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="000db-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="000db-229">Ogni file contiene un solo oggetto o più oggetti con delimitatori di riga/concatenati.</span><span class="sxs-lookup"><span data-stu-id="000db-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="000db-230">Quando si sceglie questa opzione in un set di dati di output, l'attività di copia produce un singolo file JSON con un oggetto per riga (delimitato da riga).</span><span class="sxs-lookup"><span data-stu-id="000db-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="000db-231">**Esempio di JSON a oggetto singolo**</span><span class="sxs-lookup"><span data-stu-id="000db-231">**single object JSON example**</span></span>

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

    * <span data-ttu-id="000db-232">**Esempio di JSON con delimitatori di riga**</span><span class="sxs-lookup"><span data-stu-id="000db-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="000db-233">**Esempio di JSON concatenati**</span><span class="sxs-lookup"><span data-stu-id="000db-233">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="000db-234">**Tipo II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="000db-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="000db-235">Ogni file contiene una matrice di oggetti.</span><span class="sxs-lookup"><span data-stu-id="000db-235">Each file contains an array of objects.</span></span>

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

### <a name="jsonformat-example"></a><span data-ttu-id="000db-236">Esempio JsonFormat</span><span class="sxs-lookup"><span data-stu-id="000db-236">JsonFormat example</span></span>

<span data-ttu-id="000db-237">**Caso 1: Copia di dati dai file JSON**</span><span class="sxs-lookup"><span data-stu-id="000db-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="000db-238">Quando si copiano dati da file JSON, vedere i seguenti due esempi.</span><span class="sxs-lookup"><span data-stu-id="000db-238">See the following two samples when copying data from JSON files.</span></span> <span data-ttu-id="000db-239">Punti generali da notare:</span><span class="sxs-lookup"><span data-stu-id="000db-239">The generic points to note:</span></span>

<span data-ttu-id="000db-240">**Esempio 1: Estrarre i dati dall'oggetto e dalla matrice**</span><span class="sxs-lookup"><span data-stu-id="000db-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="000db-241">In questo esempio si prevede che un oggetto JSON radice esegua il mapping a un singolo record in un risultato tabulare.</span><span class="sxs-lookup"><span data-stu-id="000db-241">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="000db-242">Se si dispone di un file JSON con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="000db-242">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="000db-243">e lo si vuole copiare in una tabella SQL di Azure nel formato seguente, estraendo i dati sia dagli oggetti che dalla matrice:</span><span class="sxs-lookup"><span data-stu-id="000db-243">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="000db-244">id</span><span class="sxs-lookup"><span data-stu-id="000db-244">id</span></span> | <span data-ttu-id="000db-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="000db-245">deviceType</span></span> | <span data-ttu-id="000db-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="000db-246">targetResourceType</span></span> | <span data-ttu-id="000db-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="000db-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="000db-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="000db-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="000db-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="000db-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="000db-250">PC</span><span class="sxs-lookup"><span data-stu-id="000db-250">PC</span></span> | <span data-ttu-id="000db-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="000db-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="000db-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="000db-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="000db-253">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="000db-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="000db-254">Il set di dati di input con il tipo **JsonFormat** è definito come segue (definizione parziale che include solo le parti pertinenti).</span><span class="sxs-lookup"><span data-stu-id="000db-254">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="000db-255">Più in particolare:</span><span class="sxs-lookup"><span data-stu-id="000db-255">More specifically:</span></span>

- <span data-ttu-id="000db-256">La sezione `structure` definisce i nomi di colonna personalizzati e il tipo di dati corrispondente durante la conversione in dati tabulari.</span><span class="sxs-lookup"><span data-stu-id="000db-256">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="000db-257">Questa sezione è **facoltativa** a meno che non sia necessario eseguire il mapping colonne.</span><span class="sxs-lookup"><span data-stu-id="000db-257">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="000db-258">Per altri dettagli, vedere [Eseguire il mapping delle colonne del set di dati di origine alle colonne del set di dati di destinazione](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="000db-258">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="000db-259">`jsonPathDefinition` specifica il percorso JSON per ogni colonna indicante da dove estrarre i dati.</span><span class="sxs-lookup"><span data-stu-id="000db-259">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="000db-260">Per copiare i dati dalla matrice, è possibile usare **array[x].property** per estrarre il valore della proprietà specificata dall'oggetto xth oppure è possibile usare **array[*].property** per trovare il valore in qualsiasi oggetto contenente tale proprietà.</span><span class="sxs-lookup"><span data-stu-id="000db-260">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[*].property** to find the value from any object containing such property.</span></span>

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

<span data-ttu-id="000db-261">**Esempio 2: applicazione incrociata di più oggetti con lo stesso modello dalla matrice**</span><span class="sxs-lookup"><span data-stu-id="000db-261">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="000db-262">In questo esempio si prevede di trasformare un oggetto JSON radice in più record in risultato tabulare.</span><span class="sxs-lookup"><span data-stu-id="000db-262">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="000db-263">Se si dispone di un file JSON con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="000db-263">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="000db-264">e lo si vuole copiare in una tabella SQL di Azure nel formato seguente, rendendo flat i dati nella matrice e nel crossjoin con le informazioni radice comuni:</span><span class="sxs-lookup"><span data-stu-id="000db-264">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="000db-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="000db-265">ordernumber</span></span> | <span data-ttu-id="000db-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="000db-266">orderdate</span></span> | <span data-ttu-id="000db-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="000db-267">order_pd</span></span> | <span data-ttu-id="000db-268">order_price</span><span class="sxs-lookup"><span data-stu-id="000db-268">order_price</span></span> | <span data-ttu-id="000db-269">city</span><span class="sxs-lookup"><span data-stu-id="000db-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="000db-270">01</span><span class="sxs-lookup"><span data-stu-id="000db-270">01</span></span> | <span data-ttu-id="000db-271">20170122</span><span class="sxs-lookup"><span data-stu-id="000db-271">20170122</span></span> | <span data-ttu-id="000db-272">P1</span><span class="sxs-lookup"><span data-stu-id="000db-272">P1</span></span> | <span data-ttu-id="000db-273">23</span><span class="sxs-lookup"><span data-stu-id="000db-273">23</span></span> | <span data-ttu-id="000db-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="000db-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="000db-275">01</span><span class="sxs-lookup"><span data-stu-id="000db-275">01</span></span> | <span data-ttu-id="000db-276">20170122</span><span class="sxs-lookup"><span data-stu-id="000db-276">20170122</span></span> | <span data-ttu-id="000db-277">P2</span><span class="sxs-lookup"><span data-stu-id="000db-277">P2</span></span> | <span data-ttu-id="000db-278">13</span><span class="sxs-lookup"><span data-stu-id="000db-278">13</span></span> | <span data-ttu-id="000db-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="000db-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="000db-280">01</span><span class="sxs-lookup"><span data-stu-id="000db-280">01</span></span> | <span data-ttu-id="000db-281">20170122</span><span class="sxs-lookup"><span data-stu-id="000db-281">20170122</span></span> | <span data-ttu-id="000db-282">P3</span><span class="sxs-lookup"><span data-stu-id="000db-282">P3</span></span> | <span data-ttu-id="000db-283">231</span><span class="sxs-lookup"><span data-stu-id="000db-283">231</span></span> | <span data-ttu-id="000db-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="000db-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="000db-285">Il set di dati di input con il tipo **JsonFormat** è definito come segue (definizione parziale che include solo le parti pertinenti).</span><span class="sxs-lookup"><span data-stu-id="000db-285">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="000db-286">Più in particolare:</span><span class="sxs-lookup"><span data-stu-id="000db-286">More specifically:</span></span>

- <span data-ttu-id="000db-287">La sezione `structure` definisce i nomi di colonna personalizzati e il tipo di dati corrispondente durante la conversione in dati tabulari.</span><span class="sxs-lookup"><span data-stu-id="000db-287">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="000db-288">Questa sezione è **facoltativa** a meno che non sia necessario eseguire il mapping colonne.</span><span class="sxs-lookup"><span data-stu-id="000db-288">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="000db-289">Per altri dettagli, vedere [Eseguire il mapping delle colonne del set di dati di origine alle colonne del set di dati di destinazione](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="000db-289">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="000db-290">`jsonNodeReference` indica di seguire l'iterazione dei dati e di estrarli dagli oggetti con lo stesso modello sotto le righe ordine della **matrice**.</span><span class="sxs-lookup"><span data-stu-id="000db-290">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="000db-291">`jsonPathDefinition` specifica il percorso JSON per ogni colonna indicante da dove estrarre i dati.</span><span class="sxs-lookup"><span data-stu-id="000db-291">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="000db-292">In questo esempio "ordernumber", "orderdate" e "city" sono sotto l'oggetto radice con il percorso JSON che inizia con "$.", mentre "order_pd" e "order_price" sono definiti con il percorso derivato dall'elemento matrice senza "$.".</span><span class="sxs-lookup"><span data-stu-id="000db-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

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

<span data-ttu-id="000db-293">**Tenere presente quanto segue:**</span><span class="sxs-lookup"><span data-stu-id="000db-293">**Note the following points:**</span></span>

* <span data-ttu-id="000db-294">Se `structure` e `jsonPathDefinition` non sono definite nel set di dati della data factory, l'attività di copia rileva lo schema dal primo oggetto e rende flat l'intero oggetto.</span><span class="sxs-lookup"><span data-stu-id="000db-294">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="000db-295">Se l'input JSON presenta una matrice, per impostazione predefinita, l'attività di copia converte l'intero valore della matrice in una stringa.</span><span class="sxs-lookup"><span data-stu-id="000db-295">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="000db-296">È possibile scegliere di estrarre i dati usando `jsonNodeReference` e/o `jsonPathDefinition` oppure di ignorarlo non specificandolo in `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="000db-296">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="000db-297">Se ci sono nomi duplicati allo stesso livello, l'attività di copia sceglie quello più recente.</span><span class="sxs-lookup"><span data-stu-id="000db-297">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="000db-298">I nomi delle proprietà distinguono tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="000db-298">Property names are case-sensitive.</span></span> <span data-ttu-id="000db-299">Due proprietà con lo stesso nome ma con una combinazione differente di maiuscole e minuscole vengono considerate come due proprietà diverse.</span><span class="sxs-lookup"><span data-stu-id="000db-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="000db-300">**Caso 2: Scrittura dei dati nel file JSON**</span><span class="sxs-lookup"><span data-stu-id="000db-300">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="000db-301">Se nel database SQL è presente la tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="000db-301">If you have the following table in SQL Database:</span></span>

| <span data-ttu-id="000db-302">id</span><span class="sxs-lookup"><span data-stu-id="000db-302">id</span></span> | <span data-ttu-id="000db-303">order_date</span><span class="sxs-lookup"><span data-stu-id="000db-303">order_date</span></span> | <span data-ttu-id="000db-304">order_price</span><span class="sxs-lookup"><span data-stu-id="000db-304">order_price</span></span> | <span data-ttu-id="000db-305">order_by</span><span class="sxs-lookup"><span data-stu-id="000db-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="000db-306">1</span><span class="sxs-lookup"><span data-stu-id="000db-306">1</span></span> | <span data-ttu-id="000db-307">20170119</span><span class="sxs-lookup"><span data-stu-id="000db-307">20170119</span></span> | <span data-ttu-id="000db-308">2000</span><span class="sxs-lookup"><span data-stu-id="000db-308">2000</span></span> | <span data-ttu-id="000db-309">David</span><span class="sxs-lookup"><span data-stu-id="000db-309">David</span></span> |
| <span data-ttu-id="000db-310">2</span><span class="sxs-lookup"><span data-stu-id="000db-310">2</span></span> | <span data-ttu-id="000db-311">20170120</span><span class="sxs-lookup"><span data-stu-id="000db-311">20170120</span></span> | <span data-ttu-id="000db-312">3500</span><span class="sxs-lookup"><span data-stu-id="000db-312">3500</span></span> | <span data-ttu-id="000db-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="000db-313">Patrick</span></span> |
| <span data-ttu-id="000db-314">3</span><span class="sxs-lookup"><span data-stu-id="000db-314">3</span></span> | <span data-ttu-id="000db-315">20170121</span><span class="sxs-lookup"><span data-stu-id="000db-315">20170121</span></span> | <span data-ttu-id="000db-316">4000</span><span class="sxs-lookup"><span data-stu-id="000db-316">4000</span></span> | <span data-ttu-id="000db-317">Jason</span><span class="sxs-lookup"><span data-stu-id="000db-317">Jason</span></span> |

<span data-ttu-id="000db-318">e per ogni record si prevede di scrivere in un oggetto JSON nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="000db-318">and for each record, you expect to write to a JSON object in the following format:</span></span>
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

<span data-ttu-id="000db-319">Il set di dati di output con il tipo **JsonFormat** è definito come segue (definizione parziale che include solo le parti pertinenti).</span><span class="sxs-lookup"><span data-stu-id="000db-319">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="000db-320">Più in particolare, la sezione `structure` definisce i nomi di proprietà personalizzati nel file di destinazione e viene usato `nestingSeparator` (il valore predefinito è ".") per identificare il livello di annidamento dal nome.</span><span class="sxs-lookup"><span data-stu-id="000db-320">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") are used to identify the nest layer from the name.</span></span> <span data-ttu-id="000db-321">Questa sezione è **facoltativa** a meno che non si voglia modificare il nome della proprietà confrontandolo con il nome della colonna di origine o annidare alcune delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="000db-321">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

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

## <a name="avro-format"></a><span data-ttu-id="000db-322">Formato AVRO</span><span class="sxs-lookup"><span data-stu-id="000db-322">AVRO format</span></span>
<span data-ttu-id="000db-323">Per analizzare i file Avro o scrivere i dati in formato Avro, impostare la proprietà `format` `type` su **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="000db-323">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="000db-324">Non è necessario specificare le proprietà nella sezione Format all'interno della sezione typeProperties.</span><span class="sxs-lookup"><span data-stu-id="000db-324">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="000db-325">Esempio:</span><span class="sxs-lookup"><span data-stu-id="000db-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="000db-326">Per usare il formato Avro in una tabella Hive, fare riferimento all' [esercitazione su Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="000db-326">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="000db-327">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="000db-327">Note the following points:</span></span>  

* <span data-ttu-id="000db-328">I [tipi di dati complessi](http://avro.apache.org/docs/current/spec.html#schema_complex) non sono supportati (record, enumerazioni, matrici, mappe, unioni e dati fissi).</span><span class="sxs-lookup"><span data-stu-id="000db-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="000db-329">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="000db-329">ORC format</span></span>
<span data-ttu-id="000db-330">Per analizzare i file ORC o scrivere i dati in formato ORC, impostare la proprietà `format` `type` su **OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="000db-330">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="000db-331">Non è necessario specificare le proprietà nella sezione Format all'interno della sezione typeProperties.</span><span class="sxs-lookup"><span data-stu-id="000db-331">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="000db-332">Esempio:</span><span class="sxs-lookup"><span data-stu-id="000db-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="000db-333">Se non si esegue una copia **identica** dei file ORC tra l'archivio dati locale e quello nel cloud, nel computer gateway è necessario installare JRE 8 (Java Runtime Environment).</span><span class="sxs-lookup"><span data-stu-id="000db-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="000db-334">Per un gateway a 64 bit è necessario JRE a 64 bit, mentre per un gateway a 32 bit è necessario JRE a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="000db-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="000db-335">Entrambe le versioni sono disponibili [qui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="000db-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="000db-336">Scegliere la versione appropriata.</span><span class="sxs-lookup"><span data-stu-id="000db-336">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="000db-337">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="000db-337">Note the following points:</span></span>

* <span data-ttu-id="000db-338">Tipi di dati complessi non sono supportati (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="000db-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="000db-339">Il file ORC dispone di tre [opzioni relative alla compressione](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="000db-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="000db-340">Data Factory supporta la lettura dei dati dal file ORC in uno di questi formati compressi.</span><span class="sxs-lookup"><span data-stu-id="000db-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="000db-341">Per leggere i dati, Data Factoy usa la compressione codec dei metadati.</span><span class="sxs-lookup"><span data-stu-id="000db-341">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="000db-342">Tuttavia, durante la scrittura in un file ORC, Data Factory sceglie ZLIB che è il valore predefinito per ORC.</span><span class="sxs-lookup"><span data-stu-id="000db-342">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="000db-343">Al momento non esiste alcuna opzione per ignorare tale comportamento.</span><span class="sxs-lookup"><span data-stu-id="000db-343">Currently, there is no option to override this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="000db-344">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="000db-344">Parquet format</span></span>
<span data-ttu-id="000db-345">Per analizzare i file Parquet o scrivere i dati in formato Parquet, impostare la proprietà `format` `type` su **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="000db-345">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="000db-346">Non è necessario specificare le proprietà nella sezione Format all'interno della sezione typeProperties.</span><span class="sxs-lookup"><span data-stu-id="000db-346">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="000db-347">Esempio:</span><span class="sxs-lookup"><span data-stu-id="000db-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="000db-348">Se non si esegue una copia **identica** dei file Parquet tra l'archivio dati locale e quello nel cloud, nel computer gateway è necessario installare JRE 8 (Java Runtime Environment).</span><span class="sxs-lookup"><span data-stu-id="000db-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="000db-349">Per un gateway a 64 bit è necessario JRE a 64 bit, mentre per un gateway a 32 bit è necessario JRE a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="000db-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="000db-350">Entrambe le versioni sono disponibili [qui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="000db-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="000db-351">Scegliere la versione appropriata.</span><span class="sxs-lookup"><span data-stu-id="000db-351">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="000db-352">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="000db-352">Note the following points:</span></span>

* <span data-ttu-id="000db-353">Tipi di dati complessi non sono supportati (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="000db-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="000db-354">Un file Parquet ha le seguenti opzioni relative alla compressione: NONE, SNAPPY, GZIP e LZO.</span><span class="sxs-lookup"><span data-stu-id="000db-354">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="000db-355">Data Factory supporta la lettura dei dati dal file ORC in uno di questi formati compressi.</span><span class="sxs-lookup"><span data-stu-id="000db-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="000db-356">Per la lettura dei dati usa il codec di compressione nei metadati.</span><span class="sxs-lookup"><span data-stu-id="000db-356">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="000db-357">Tuttavia, durante la scrittura in un file Parquet, Data Factory sceglie SNAPPY, cioè il valore predefinito per il formato Parquet.</span><span class="sxs-lookup"><span data-stu-id="000db-357">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="000db-358">Al momento non esiste alcuna opzione per ignorare tale comportamento.</span><span class="sxs-lookup"><span data-stu-id="000db-358">Currently, there is no option to override this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="000db-359">Supporto della compressione</span><span class="sxs-lookup"><span data-stu-id="000db-359">Compression support</span></span>
<span data-ttu-id="000db-360">L'elaborazione di set di dati di grandi dimensioni può causare colli di bottiglia I/O e di rete.</span><span class="sxs-lookup"><span data-stu-id="000db-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="000db-361">Pertanto, i dati compressi negli archivi possono non solo velocizzare il trasferimento dei dati attraverso la rete e risparmiare spazio su disco, ma apportare anche miglioramenti significativi delle prestazioni nell'elaborazione di dati di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="000db-361">Therefore, compressed data in stores can not only speed up data transfer across the network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="000db-362">Attualmente, la compressione è supportata per gli archivi di dati basati su file, ad esempio BLOB di Azure o il file system locale.</span><span class="sxs-lookup"><span data-stu-id="000db-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="000db-363">Per specificare la compressione per un set di dati, usare la proprietà **compression** nel set di dati JSON come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="000db-363">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span></span>   

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

<span data-ttu-id="000db-364">Si supponga che il set di dati di esempio venga usato come output di un'attività di copia, l'attività di copia comprime i dati di output con il codec GZIP usando un rapporto ottimale e quindi scrive i dati compressi in un file denominato pagecounts.csv.gz in Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="000db-364">Suppose the sample dataset is used as the output of a copy activity, the copy activity compresses the output data with GZIP codec using optimal ratio and then write the compressed data into a file named pagecounts.csv.gz in the Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="000db-365">Le impostazioni di compressione non sono attualmente supportate per i dati in **AvroFormat**, **OrcFormat** o **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="000db-365">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="000db-366">Quando si leggono file in questi formati, Data Factory rileva e usa il codec di compressione nei metadati.</span><span class="sxs-lookup"><span data-stu-id="000db-366">When reading files in these formats, Data Factory detects and uses the compression codec in the metadata.</span></span> <span data-ttu-id="000db-367">Quando si scrive in un file che si presenta in uno di questi formati, Data Factory sceglie il codice di compressione predefinito per il formato specifico.</span><span class="sxs-lookup"><span data-stu-id="000db-367">When writing to files in these formats, Data Factory chooses the default compression codec for that format.</span></span> <span data-ttu-id="000db-368">ad esempio ZLIB per OrcFormat e SNAPPY per ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="000db-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="000db-369">La sezione **compression** ha due proprietà:</span><span class="sxs-lookup"><span data-stu-id="000db-369">The **compression** section has two properties:</span></span>  

* <span data-ttu-id="000db-370">**Type:** codec di compressione, che può essere **GZIP**, **Deflate**, **BZIP2** o **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="000db-370">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="000db-371">**Level:** rapporto di compressione, che può essere **Optimal** o **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="000db-371">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="000db-372">**Fastest:** l'operazione di compressione deve essere completata il più rapidamente possibile, anche se il file risultante non viene compresso in modo ottimale.</span><span class="sxs-lookup"><span data-stu-id="000db-372">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="000db-373">**Optimal**: l'operazione di compressione deve comprimere il file in modo ottimale, anche se il completamento richiede più tempo.</span><span class="sxs-lookup"><span data-stu-id="000db-373">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span></span>

    <span data-ttu-id="000db-374">Per maggiori informazioni, vedere l'argomento relativo al [livello di compressione](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) .</span><span class="sxs-lookup"><span data-stu-id="000db-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="000db-375">Quando si specifica una proprietà `compression` in un set di dati di input JSON, la pipeline può leggere i dati compressi dall'origine. Quando si specifica la proprietà in un set di dati di output JSON, l'attività di copia può scrivere i dati compressi nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="000db-375">When you specify `compression` property in an input dataset JSON, the pipeline can read compressed data from the source; and when you specify the property in an output dataset JSON, the copy activity can write compressed data to the destination.</span></span> <span data-ttu-id="000db-376">Di seguito vengono forniti alcuni scenari di esempio:</span><span class="sxs-lookup"><span data-stu-id="000db-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="000db-377">Leggere i dati compressi GZIP da un BLOB di Azure, decomprimerli e scrivere i dati del risultato in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="000db-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span></span> <span data-ttu-id="000db-378">Definire il set di dati di input del BLOB di Azure con la proprietà JSON `compression` `type` impostata su GZIP.</span><span class="sxs-lookup"><span data-stu-id="000db-378">You define the input Azure Blob dataset with the `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="000db-379">Leggere i dati da un file di testo normale dal file system locale, comprimerli usando il formato GZIP e scrivere i dati compressi in un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="000db-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span></span> <span data-ttu-id="000db-380">Definire un set di dati di output del BLOB di Azure con la proprietà JSON `compression` `type` impostata su GZIP.</span><span class="sxs-lookup"><span data-stu-id="000db-380">You define an output Azure Blob dataset with the `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="000db-381">Leggere il file ZIP dal server FTP, decomprimerlo per ottenere i file all'interno e inserire i file in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="000db-381">Read .zip file from FTP server, decompress it to get the files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="000db-382">Definire un set di dati FTP di input con la proprietà JSON `compression` `type` impostata su ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="000db-382">You define an input FTP dataset with the `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="000db-383">Leggere i dati compressi GZIP da un BLOB di Azure, decomprimerli, comprimerli usando BZIP2 e scrivere i dati del risultato in un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="000db-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span></span> <span data-ttu-id="000db-384">In questo caso, il set di dati di input del BLOB di Azure viene definito con `compression` `type` impostato su GZIP e il set di dati di output viene definito con `compression` `type` impostato su BZIP2.</span><span class="sxs-lookup"><span data-stu-id="000db-384">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="000db-385">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="000db-385">Next steps</span></span>
<span data-ttu-id="000db-386">Per gli archivi dati basati su file supportati da Azure Data Factory, vedere i seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="000db-386">See the following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="000db-387">Archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="000db-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="000db-388">Archivio Data Lake di Azure</span><span class="sxs-lookup"><span data-stu-id="000db-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="000db-389">FTP</span><span class="sxs-lookup"><span data-stu-id="000db-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="000db-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="000db-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="000db-391">File system</span><span class="sxs-lookup"><span data-stu-id="000db-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="000db-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="000db-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
