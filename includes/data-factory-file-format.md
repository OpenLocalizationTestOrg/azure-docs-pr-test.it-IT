## <a name="specifying-formats"></a><span data-ttu-id="24e7e-101">Specifica dei formati</span><span class="sxs-lookup"><span data-stu-id="24e7e-101">Specifying formats</span></span>
<span data-ttu-id="24e7e-102">Data Factory di Azure supporta i seguenti tipi di formato hello:</span><span class="sxs-lookup"><span data-stu-id="24e7e-102">Azure Data Factory supports hello following format types:</span></span>

* [<span data-ttu-id="24e7e-103">Formato testo</span><span class="sxs-lookup"><span data-stu-id="24e7e-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="24e7e-104">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="24e7e-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="24e7e-105">Formato Avro</span><span class="sxs-lookup"><span data-stu-id="24e7e-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="24e7e-106">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="24e7e-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="24e7e-107">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="24e7e-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="24e7e-108">Specifica di TextFormat</span><span class="sxs-lookup"><span data-stu-id="24e7e-108">Specifying TextFormat</span></span>
<span data-ttu-id="24e7e-109">Se si desidera che i file di testo hello tooparse o scrivono dati hello in formato testo, impostare hello `format` `type` proprietà troppo**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="24e7e-109">If you want tooparse hello text files or write hello data in text format, set hello `format` `type` property too**TextFormat**.</span></span> <span data-ttu-id="24e7e-110">È inoltre possibile specificare i seguenti hello **facoltativo** proprietà hello `format` sezione.</span><span class="sxs-lookup"><span data-stu-id="24e7e-110">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="24e7e-111">Vedere [esempio TextFormat](#textformat-example) sezione su come tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="24e7e-111">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="24e7e-112">Proprietà</span><span class="sxs-lookup"><span data-stu-id="24e7e-112">Property</span></span> | <span data-ttu-id="24e7e-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="24e7e-113">Description</span></span> | <span data-ttu-id="24e7e-114">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="24e7e-114">Allowed values</span></span> | <span data-ttu-id="24e7e-115">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="24e7e-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="24e7e-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="24e7e-116">columnDelimiter</span></span> |<span data-ttu-id="24e7e-117">carattere Hello usato tooseparate colonne in un file.</span><span class="sxs-lookup"><span data-stu-id="24e7e-117">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="24e7e-118">È possibile prendere in considerazione toouse un carattere non stampabile raro che probabilmente non esiste nei dati: ad esempio, specificare "\u0001" che rappresenta l'avvio di intestazione (SOH).</span><span class="sxs-lookup"><span data-stu-id="24e7e-118">You can consider toouse a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="24e7e-119">È consentito un solo carattere.</span><span class="sxs-lookup"><span data-stu-id="24e7e-119">Only one character is allowed.</span></span> <span data-ttu-id="24e7e-120">Hello **predefinito** valore **virgola (',')**.</span><span class="sxs-lookup"><span data-stu-id="24e7e-120">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="24e7e-121">toouse un carattere Unicode, vedere troppo[caratteri Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello codice corrispondente per tale.</span><span class="sxs-lookup"><span data-stu-id="24e7e-121">toouse an Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="24e7e-122">No</span><span class="sxs-lookup"><span data-stu-id="24e7e-122">No</span></span> |
| <span data-ttu-id="24e7e-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="24e7e-123">rowDelimiter</span></span> |<span data-ttu-id="24e7e-124">carattere Hello usato tooseparate righe in un file.</span><span class="sxs-lookup"><span data-stu-id="24e7e-124">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="24e7e-125">È consentito un solo carattere.</span><span class="sxs-lookup"><span data-stu-id="24e7e-125">Only one character is allowed.</span></span> <span data-ttu-id="24e7e-126">Hello **predefinito** valore è uno dei seguenti valori in lettura hello: **["\r\n", "\r", "\n"]** e **"\r\n"** durante la scrittura.</span><span class="sxs-lookup"><span data-stu-id="24e7e-126">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="24e7e-127">No</span><span class="sxs-lookup"><span data-stu-id="24e7e-127">No</span></span> |
| <span data-ttu-id="24e7e-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="24e7e-128">escapeChar</span></span> |<span data-ttu-id="24e7e-129">carattere speciale di Hello utilizzato tooescape un delimitatore di colonna nel contenuto di hello del file di input.</span><span class="sxs-lookup"><span data-stu-id="24e7e-129">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="24e7e-130">Per una tabella, è possibile specificare sia escapeChar che quoteChar.</span><span class="sxs-lookup"><span data-stu-id="24e7e-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="24e7e-131">È consentito un solo carattere.</span><span class="sxs-lookup"><span data-stu-id="24e7e-131">Only one character is allowed.</span></span> <span data-ttu-id="24e7e-132">Nessun valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="24e7e-132">No default value.</span></span> <br/><br/><span data-ttu-id="24e7e-133">Esempio: se è presente una virgola (', ') come delimitatore di colonna hello ma si desidera aggiungere un carattere virgola toohave hello in testo hello (esempio: "Hello, world"), è possibile definire '$' come carattere di escape hello e utilizzare una stringa "Hello$, world" nell'origine hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-133">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="24e7e-134">No</span><span class="sxs-lookup"><span data-stu-id="24e7e-134">No</span></span> |
| <span data-ttu-id="24e7e-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="24e7e-135">quoteChar</span></span> |<span data-ttu-id="24e7e-136">carattere di Hello utilizzato tooquote un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="24e7e-136">hello character used tooquote a string value.</span></span> <span data-ttu-id="24e7e-137">delimitatori di colonna e riga Hello all'interno di virgolette singole hello verrebbero considerati come parte del valore di stringa hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-137">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="24e7e-138">Questa proprietà è applicabile tooboth input e output di set di dati.</span><span class="sxs-lookup"><span data-stu-id="24e7e-138">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="24e7e-139">Per una tabella, è possibile specificare sia escapeChar che quoteChar.</span><span class="sxs-lookup"><span data-stu-id="24e7e-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="24e7e-140">È consentito un solo carattere.</span><span class="sxs-lookup"><span data-stu-id="24e7e-140">Only one character is allowed.</span></span> <span data-ttu-id="24e7e-141">Nessun valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="24e7e-141">No default value.</span></span> <br/><br/><span data-ttu-id="24e7e-142">Ad esempio, se è presente una virgola (', ') come delimitatore di colonna hello ma si desidera assegnare il carattere virgola toohave nel testo hello (esempio: < Hello, world >), è possibile definire "(virgolette doppie) come hello virgolette e utilizzare la stringa hello"Hello, world"nell'origine hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-142">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="24e7e-143">No</span><span class="sxs-lookup"><span data-stu-id="24e7e-143">No</span></span> |
| <span data-ttu-id="24e7e-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="24e7e-144">nullValue</span></span> |<span data-ttu-id="24e7e-145">Uno o più caratteri utilizzati toorepresent un valore null.</span><span class="sxs-lookup"><span data-stu-id="24e7e-145">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="24e7e-146">Uno o più caratteri.</span><span class="sxs-lookup"><span data-stu-id="24e7e-146">One or more characters.</span></span> <span data-ttu-id="24e7e-147">Hello **predefinito** i valori sono **"\N" e "NULL"** in lettura e **"\N"** durante la scrittura.</span><span class="sxs-lookup"><span data-stu-id="24e7e-147">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="24e7e-148">No</span><span class="sxs-lookup"><span data-stu-id="24e7e-148">No</span></span> |
| <span data-ttu-id="24e7e-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="24e7e-149">encodingName</span></span> |<span data-ttu-id="24e7e-150">Specificare il nome della codifica di hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-150">Specify hello encoding name.</span></span> |<span data-ttu-id="24e7e-151">Un nome di codifica valido.</span><span class="sxs-lookup"><span data-stu-id="24e7e-151">A valid encoding name.</span></span> <span data-ttu-id="24e7e-152">Vedere [Proprietà Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="24e7e-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="24e7e-153">Esempio: windows-1250 o shift_jis.</span><span class="sxs-lookup"><span data-stu-id="24e7e-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="24e7e-154">Hello **predefinito** valore **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="24e7e-154">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="24e7e-155">No</span><span class="sxs-lookup"><span data-stu-id="24e7e-155">No</span></span> |
| <span data-ttu-id="24e7e-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="24e7e-156">firstRowAsHeader</span></span> |<span data-ttu-id="24e7e-157">Specifica se tooconsider hello prima riga come intestazione.</span><span class="sxs-lookup"><span data-stu-id="24e7e-157">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="24e7e-158">In un set di dati di input Data factory legge la prima riga come intestazione.</span><span class="sxs-lookup"><span data-stu-id="24e7e-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="24e7e-159">In un set di dati di output Data factory scrive la prima riga come intestazione.</span><span class="sxs-lookup"><span data-stu-id="24e7e-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="24e7e-160">Vedere [Scenari per l'uso di `firstRowAsHeader` e `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) per gli scenari di esempio.</span><span class="sxs-lookup"><span data-stu-id="24e7e-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="24e7e-161">True</span><span class="sxs-lookup"><span data-stu-id="24e7e-161">True</span></span><br/><span data-ttu-id="24e7e-162">**False (impostazione predefinita)**</span><span class="sxs-lookup"><span data-stu-id="24e7e-162">**False (default)**</span></span> |<span data-ttu-id="24e7e-163">No</span><span class="sxs-lookup"><span data-stu-id="24e7e-163">No</span></span> |
| <span data-ttu-id="24e7e-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="24e7e-164">skipLineCount</span></span> |<span data-ttu-id="24e7e-165">Indica il numero di hello di tooskip righe durante la lettura di dati da file di input.</span><span class="sxs-lookup"><span data-stu-id="24e7e-165">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="24e7e-166">Se vengono specificati sia skipLineCount e prima riga come intestazione, le righe di hello vengono ignorate prima e quindi le informazioni di intestazione hello viene letto dal file di input hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-166">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="24e7e-167">Vedere [Scenari per l'uso di `firstRowAsHeader` e `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) per gli scenari di esempio.</span><span class="sxs-lookup"><span data-stu-id="24e7e-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="24e7e-168">Integer</span><span class="sxs-lookup"><span data-stu-id="24e7e-168">Integer</span></span> |<span data-ttu-id="24e7e-169">No</span><span class="sxs-lookup"><span data-stu-id="24e7e-169">No</span></span> |
| <span data-ttu-id="24e7e-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="24e7e-170">treatEmptyAsNull</span></span> |<span data-ttu-id="24e7e-171">Consente di specificare se una stringa vuota o null tootreat come un valore null durante la lettura dei dati da un file di input.</span><span class="sxs-lookup"><span data-stu-id="24e7e-171">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="24e7e-172">**True (impostazione predefinita)**</span><span class="sxs-lookup"><span data-stu-id="24e7e-172">**True (default)**</span></span><br/><span data-ttu-id="24e7e-173">False</span><span class="sxs-lookup"><span data-stu-id="24e7e-173">False</span></span> |<span data-ttu-id="24e7e-174">No</span><span class="sxs-lookup"><span data-stu-id="24e7e-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="24e7e-175">Esempio di TextFormat</span><span class="sxs-lookup"><span data-stu-id="24e7e-175">TextFormat example</span></span>
<span data-ttu-id="24e7e-176">Hello seguenti vengono illustrate alcune delle proprietà relative al formato hello per TextFormat.</span><span class="sxs-lookup"><span data-stu-id="24e7e-176">hello following sample shows some of hello format properties for TextFormat.</span></span>

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

<span data-ttu-id="24e7e-177">toouse un `escapeChar` anziché `quoteChar`, sostituire la riga hello con `quoteChar` con hello escapeChar seguenti:</span><span class="sxs-lookup"><span data-stu-id="24e7e-177">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="24e7e-178">Scenari di utilizzo di firstRowAsHeader e skipLineCount</span><span class="sxs-lookup"><span data-stu-id="24e7e-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="24e7e-179">Si sta copiando un file di testo di origine file non tooa e tooadd una riga di intestazione che contiene i metadati dello schema hello (ad esempio: schema SQL).</span><span class="sxs-lookup"><span data-stu-id="24e7e-179">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="24e7e-180">Specificare `firstRowAsHeader` come true nel set di dati per questo scenario di output di hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-180">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="24e7e-181">Si sta copiando un file di testo contenente un sink non basate su file di intestazione riga tooa e toodrop che riga.</span><span class="sxs-lookup"><span data-stu-id="24e7e-181">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="24e7e-182">Specificare `firstRowAsHeader` come true nella hello di un set di dati dell'input.</span><span class="sxs-lookup"><span data-stu-id="24e7e-182">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="24e7e-183">Si sta copiando un file di testo e si desiderano tooskip alcune righe all'inizio di hello che non contengono dati o intestazione informazioni.</span><span class="sxs-lookup"><span data-stu-id="24e7e-183">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="24e7e-184">Specificare `skipLineCount` tooindicate hello numero di righe toobe ignorati.</span><span class="sxs-lookup"><span data-stu-id="24e7e-184">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="24e7e-185">Se il resto di hello del file hello contiene una riga di intestazione, è inoltre possibile specificare `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="24e7e-185">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="24e7e-186">Se entrambi `skipLineCount` e `firstRowAsHeader` sono specificate, le righe di hello vengono ignorate prima e quindi le informazioni di intestazione hello viene letto dal file di input hello</span><span class="sxs-lookup"><span data-stu-id="24e7e-186">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="24e7e-187">Impostazione di JsonFormat</span><span class="sxs-lookup"><span data-stu-id="24e7e-187">Specifying JsonFormat</span></span>
<span data-ttu-id="24e7e-188">troppo**importazione/esportazione di file JSON come-è in/da Azure Cosmos DB**, vedere [documenti JSON di importazione/esportazione](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) sezione nel connettore di Azure Cosmos DB hello con i dettagli.</span><span class="sxs-lookup"><span data-stu-id="24e7e-188">too**import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in hello Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="24e7e-189">Se si desidera che i file JSON hello tooparse o scrivono dati hello in formato JSON, impostare hello `format` `type` proprietà troppo**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="24e7e-189">If you want tooparse hello JSON files or write hello data in JSON format, set hello `format` `type` property too**JsonFormat**.</span></span> <span data-ttu-id="24e7e-190">È inoltre possibile specificare i seguenti hello **facoltativo** proprietà hello `format` sezione.</span><span class="sxs-lookup"><span data-stu-id="24e7e-190">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="24e7e-191">Vedere [JsonFormat esempio](#jsonformat-example) sezione su come tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="24e7e-191">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="24e7e-192">Proprietà</span><span class="sxs-lookup"><span data-stu-id="24e7e-192">Property</span></span> | <span data-ttu-id="24e7e-193">Descrizione</span><span class="sxs-lookup"><span data-stu-id="24e7e-193">Description</span></span> | <span data-ttu-id="24e7e-194">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="24e7e-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24e7e-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="24e7e-195">filePattern</span></span> |<span data-ttu-id="24e7e-196">Indicano il motivo di hello dei dati archiviati in ogni file JSON.</span><span class="sxs-lookup"><span data-stu-id="24e7e-196">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="24e7e-197">I valori consentiti sono: **setOfObjects** e **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="24e7e-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="24e7e-198">Hello **predefinito** valore **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="24e7e-198">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="24e7e-199">Vedere la sezione [Modelli di file JSON](#json-file-patterns) per i dettagli su questi modelli.</span><span class="sxs-lookup"><span data-stu-id="24e7e-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="24e7e-200">No</span><span class="sxs-lookup"><span data-stu-id="24e7e-200">No</span></span> |
| <span data-ttu-id="24e7e-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="24e7e-201">jsonNodeReference</span></span> | <span data-ttu-id="24e7e-202">Se si desidera tooiterate ed estrarre i dati da oggetti hello all'interno di una matrice di un campo con hello stesso schema, specificare il percorso JSON hello della matrice.</span><span class="sxs-lookup"><span data-stu-id="24e7e-202">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="24e7e-203">Questa proprietà è supportata solo quando si copiano i dati dai file JSON.</span><span class="sxs-lookup"><span data-stu-id="24e7e-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="24e7e-204">No</span><span class="sxs-lookup"><span data-stu-id="24e7e-204">No</span></span> |
| <span data-ttu-id="24e7e-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="24e7e-205">jsonPathDefinition</span></span> | <span data-ttu-id="24e7e-206">Specificare l'espressione di percorso JSON hello per ogni mapping di colonna con un nome di colonna personalizzati (inizia con lettere minuscole).</span><span class="sxs-lookup"><span data-stu-id="24e7e-206">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="24e7e-207">Questa proprietà è supportata solo quando si copiano i dati dai file JSON ed è possibile estrarre i dati dall'oggetto o dalla matrice.</span><span class="sxs-lookup"><span data-stu-id="24e7e-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="24e7e-208">Per i campi nell'oggetto radice, iniziare con $ radice; per i campi nella matrice hello scelto da `jsonNodeReference` proprietà inizio dall'elemento di matrice hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-208">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="24e7e-209">Vedere [JsonFormat esempio](#jsonformat-example) sezione su come tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="24e7e-209">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="24e7e-210">No</span><span class="sxs-lookup"><span data-stu-id="24e7e-210">No</span></span> |
| <span data-ttu-id="24e7e-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="24e7e-211">encodingName</span></span> |<span data-ttu-id="24e7e-212">Specificare il nome della codifica di hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-212">Specify hello encoding name.</span></span> <span data-ttu-id="24e7e-213">Per hello l'elenco di nomi di codifica validi, vedere: [EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) proprietà.</span><span class="sxs-lookup"><span data-stu-id="24e7e-213">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="24e7e-214">Ad esempio: windows-1250 o shift_jis.</span><span class="sxs-lookup"><span data-stu-id="24e7e-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="24e7e-215">Hello **predefinito** valore: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="24e7e-215">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="24e7e-216">No</span><span class="sxs-lookup"><span data-stu-id="24e7e-216">No</span></span> |
| <span data-ttu-id="24e7e-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="24e7e-217">nestingSeparator</span></span> |<span data-ttu-id="24e7e-218">Carattere usato tooseparate livelli di annidamento.</span><span class="sxs-lookup"><span data-stu-id="24e7e-218">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="24e7e-219">valore predefinito di Hello è '.' (punto).</span><span class="sxs-lookup"><span data-stu-id="24e7e-219">hello default value is '.' (dot).</span></span> |<span data-ttu-id="24e7e-220">No</span><span class="sxs-lookup"><span data-stu-id="24e7e-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="24e7e-221">Modelli di file JSON</span><span class="sxs-lookup"><span data-stu-id="24e7e-221">JSON file patterns</span></span>

<span data-ttu-id="24e7e-222">L'attività di copia può eseguire l'analisi al di sotto dei modelli di file JSON:</span><span class="sxs-lookup"><span data-stu-id="24e7e-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="24e7e-223">**Tipo I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="24e7e-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="24e7e-224">Ogni file contiene un solo oggetto o più oggetti con delimitatori di riga/concatenati.</span><span class="sxs-lookup"><span data-stu-id="24e7e-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="24e7e-225">Quando si sceglie questa opzione in un set di dati di output, l'attività di copia produce un singolo file JSON con un oggetto per riga (delimitato da riga).</span><span class="sxs-lookup"><span data-stu-id="24e7e-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="24e7e-226">**Esempio di JSON a oggetto singolo**</span><span class="sxs-lookup"><span data-stu-id="24e7e-226">**single object JSON example**</span></span>

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

    * <span data-ttu-id="24e7e-227">**Esempio di JSON con delimitatori di riga**</span><span class="sxs-lookup"><span data-stu-id="24e7e-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="24e7e-228">**Esempio di JSON concatenati**</span><span class="sxs-lookup"><span data-stu-id="24e7e-228">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="24e7e-229">**Tipo II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="24e7e-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="24e7e-230">Ogni file contiene una matrice di oggetti.</span><span class="sxs-lookup"><span data-stu-id="24e7e-230">Each file contains an array of objects.</span></span>

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

#### <a name="jsonformat-example"></a><span data-ttu-id="24e7e-231">Esempio JsonFormat</span><span class="sxs-lookup"><span data-stu-id="24e7e-231">JsonFormat example</span></span>

<span data-ttu-id="24e7e-232">**Caso 1: Copia di dati dai file JSON**</span><span class="sxs-lookup"><span data-stu-id="24e7e-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="24e7e-233">Vedere di seguito due tipi di esempi di quando si copiano dati da file JSON e hello toonote punti generico:</span><span class="sxs-lookup"><span data-stu-id="24e7e-233">See below two types of samples when copying data from JSON files, and hello generic points toonote:</span></span>

<span data-ttu-id="24e7e-234">**Esempio 1: Estrarre i dati dall'oggetto e dalla matrice**</span><span class="sxs-lookup"><span data-stu-id="24e7e-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="24e7e-235">In questo esempio, si prevede un oggetto JSON radice esegue il mapping di record toosingle risultati tabulari.</span><span class="sxs-lookup"><span data-stu-id="24e7e-235">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="24e7e-236">Se si dispone di un file JSON con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="24e7e-236">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="24e7e-237">e si desidera toocopy in una tabella SQL di Azure seguenti hello formattare, estrarre dati da entrambi gli oggetti e di matrice:</span><span class="sxs-lookup"><span data-stu-id="24e7e-237">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="24e7e-238">id</span><span class="sxs-lookup"><span data-stu-id="24e7e-238">id</span></span> | <span data-ttu-id="24e7e-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="24e7e-239">deviceType</span></span> | <span data-ttu-id="24e7e-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="24e7e-240">targetResourceType</span></span> | <span data-ttu-id="24e7e-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="24e7e-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="24e7e-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="24e7e-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="24e7e-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="24e7e-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="24e7e-244">PC</span><span class="sxs-lookup"><span data-stu-id="24e7e-244">PC</span></span> | <span data-ttu-id="24e7e-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="24e7e-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="24e7e-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="24e7e-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="24e7e-247">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="24e7e-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="24e7e-248">set di dati input Hello con **JsonFormat** tipo viene definito come segue: (definizione parziale con solo parti pertinenti di hello).</span><span class="sxs-lookup"><span data-stu-id="24e7e-248">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="24e7e-249">Più in particolare:</span><span class="sxs-lookup"><span data-stu-id="24e7e-249">More specifically:</span></span>

- <span data-ttu-id="24e7e-250">`structure`Definisce i nomi di colonna hello personalizzato e il tipo di dati corrispondente hello durante la conversione dei dati tootabular.</span><span class="sxs-lookup"><span data-stu-id="24e7e-250">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="24e7e-251">Questa sezione è **facoltativo** a meno che non è necessario toodo mapping della colonna.</span><span class="sxs-lookup"><span data-stu-id="24e7e-251">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="24e7e-252">Vedere la sezione [Definizione della struttura per i set di dati rettangolari](#specifying-structure-definition-for-rectangular-datasets) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="24e7e-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="24e7e-253">`jsonPathDefinition`Specifica il percorso JSON hello per ogni colonna che indica dove tooextract hello dati.</span><span class="sxs-lookup"><span data-stu-id="24e7e-253">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="24e7e-254">dati toocopy dalla matrice, è possibile utilizzare **Property matrice [x]** tooextract valore hello data proprietà dall'oggetto x hello oppure è possibile utilizzare  **matrice [*] Property** toofind valore di Hello da qualsiasi oggetto che contiene questo tipo proprietà.</span><span class="sxs-lookup"><span data-stu-id="24e7e-254">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

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

<span data-ttu-id="24e7e-255">**Esempio 2:: applicare più oggetti con hello stesso modello di matrice**</span><span class="sxs-lookup"><span data-stu-id="24e7e-255">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="24e7e-256">In questo esempio, si prevede un oggetto tootransform JSON radice in più record nel risultato tabulare.</span><span class="sxs-lookup"><span data-stu-id="24e7e-256">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="24e7e-257">Se si dispone di un file JSON con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="24e7e-257">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="24e7e-258">e si desidera toocopy in una tabella SQL di Azure seguenti hello formatta, per rendere bidimensionali i dati di hello all'interno di matrice hello e cross join con informazioni radice comune hello:</span><span class="sxs-lookup"><span data-stu-id="24e7e-258">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="24e7e-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="24e7e-259">ordernumber</span></span> | <span data-ttu-id="24e7e-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="24e7e-260">orderdate</span></span> | <span data-ttu-id="24e7e-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="24e7e-261">order_pd</span></span> | <span data-ttu-id="24e7e-262">order_price</span><span class="sxs-lookup"><span data-stu-id="24e7e-262">order_price</span></span> | <span data-ttu-id="24e7e-263">city</span><span class="sxs-lookup"><span data-stu-id="24e7e-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="24e7e-264">01</span><span class="sxs-lookup"><span data-stu-id="24e7e-264">01</span></span> | <span data-ttu-id="24e7e-265">20170122</span><span class="sxs-lookup"><span data-stu-id="24e7e-265">20170122</span></span> | <span data-ttu-id="24e7e-266">P1</span><span class="sxs-lookup"><span data-stu-id="24e7e-266">P1</span></span> | <span data-ttu-id="24e7e-267">23</span><span class="sxs-lookup"><span data-stu-id="24e7e-267">23</span></span> | <span data-ttu-id="24e7e-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="24e7e-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="24e7e-269">01</span><span class="sxs-lookup"><span data-stu-id="24e7e-269">01</span></span> | <span data-ttu-id="24e7e-270">20170122</span><span class="sxs-lookup"><span data-stu-id="24e7e-270">20170122</span></span> | <span data-ttu-id="24e7e-271">P2</span><span class="sxs-lookup"><span data-stu-id="24e7e-271">P2</span></span> | <span data-ttu-id="24e7e-272">13</span><span class="sxs-lookup"><span data-stu-id="24e7e-272">13</span></span> | <span data-ttu-id="24e7e-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="24e7e-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="24e7e-274">01</span><span class="sxs-lookup"><span data-stu-id="24e7e-274">01</span></span> | <span data-ttu-id="24e7e-275">20170122</span><span class="sxs-lookup"><span data-stu-id="24e7e-275">20170122</span></span> | <span data-ttu-id="24e7e-276">P3</span><span class="sxs-lookup"><span data-stu-id="24e7e-276">P3</span></span> | <span data-ttu-id="24e7e-277">231</span><span class="sxs-lookup"><span data-stu-id="24e7e-277">231</span></span> | <span data-ttu-id="24e7e-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="24e7e-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="24e7e-279">set di dati input Hello con **JsonFormat** tipo viene definito come segue: (definizione parziale con solo parti pertinenti di hello).</span><span class="sxs-lookup"><span data-stu-id="24e7e-279">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="24e7e-280">Più in particolare:</span><span class="sxs-lookup"><span data-stu-id="24e7e-280">More specifically:</span></span>

- <span data-ttu-id="24e7e-281">`structure`Definisce i nomi di colonna hello personalizzato e il tipo di dati corrispondente hello durante la conversione dei dati tootabular.</span><span class="sxs-lookup"><span data-stu-id="24e7e-281">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="24e7e-282">Questa sezione è **facoltativo** a meno che non è necessario toodo mapping della colonna.</span><span class="sxs-lookup"><span data-stu-id="24e7e-282">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="24e7e-283">Vedere la sezione [Definizione della struttura per i set di dati rettangolari](#specifying-structure-definition-for-rectangular-datasets) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="24e7e-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="24e7e-284">`jsonNodeReference`indica tooiterate ed estrarre i dati da oggetti hello con hello stesso modello in **matrice** orderlines.</span><span class="sxs-lookup"><span data-stu-id="24e7e-284">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="24e7e-285">`jsonPathDefinition`Specifica il percorso JSON hello per ogni colonna che indica dove tooextract hello dati.</span><span class="sxs-lookup"><span data-stu-id="24e7e-285">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="24e7e-286">In questo esempio, "ordernumber", "orderdate" e "city" sono in oggetto di primo livello con JSON inizi con "$"., mentre "order_pd" e "order_price" sono definiti con percorso derivata dall'elemento di matrice hello senza "$"..</span><span class="sxs-lookup"><span data-stu-id="24e7e-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

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

<span data-ttu-id="24e7e-287">**Si noti hello seguenti punti:**</span><span class="sxs-lookup"><span data-stu-id="24e7e-287">**Note hello following points:**</span></span>

* <span data-ttu-id="24e7e-288">Se hello `structure` e `jsonPathDefinition` non sono definiti nel set di dati con Data Factory di hello hello attività di copia rileva hello schema dal primo oggetto hello e rendere flat intero oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-288">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="24e7e-289">Se l'input JSON hello dispone di una matrice, per impostazione predefinita hello attività di copia converte il valore di matrice intera hello in una stringa.</span><span class="sxs-lookup"><span data-stu-id="24e7e-289">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="24e7e-290">È possibile scegliere i dati tooextract tramite `jsonNodeReference` e/o `jsonPathDefinition`, o ignorarlo se non viene specificata in `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="24e7e-290">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="24e7e-291">Se sono presenti duplicati nomi hello allo stesso livello, hello attività di copia selezioni hello ultimo.</span><span class="sxs-lookup"><span data-stu-id="24e7e-291">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="24e7e-292">I nomi delle proprietà distinguono tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="24e7e-292">Property names are case-sensitive.</span></span> <span data-ttu-id="24e7e-293">Due proprietà con lo stesso nome ma con una combinazione differente di maiuscole e minuscole vengono considerate come due proprietà diverse.</span><span class="sxs-lookup"><span data-stu-id="24e7e-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="24e7e-294">**Caso 2: Scrittura del file di dati tooJSON**</span><span class="sxs-lookup"><span data-stu-id="24e7e-294">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="24e7e-295">Se nel database SQL è presente la tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="24e7e-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="24e7e-296">id</span><span class="sxs-lookup"><span data-stu-id="24e7e-296">id</span></span> | <span data-ttu-id="24e7e-297">order_date</span><span class="sxs-lookup"><span data-stu-id="24e7e-297">order_date</span></span> | <span data-ttu-id="24e7e-298">order_price</span><span class="sxs-lookup"><span data-stu-id="24e7e-298">order_price</span></span> | <span data-ttu-id="24e7e-299">order_by</span><span class="sxs-lookup"><span data-stu-id="24e7e-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="24e7e-300">1</span><span class="sxs-lookup"><span data-stu-id="24e7e-300">1</span></span> | <span data-ttu-id="24e7e-301">20170119</span><span class="sxs-lookup"><span data-stu-id="24e7e-301">20170119</span></span> | <span data-ttu-id="24e7e-302">2000</span><span class="sxs-lookup"><span data-stu-id="24e7e-302">2000</span></span> | <span data-ttu-id="24e7e-303">David</span><span class="sxs-lookup"><span data-stu-id="24e7e-303">David</span></span> |
| <span data-ttu-id="24e7e-304">2</span><span class="sxs-lookup"><span data-stu-id="24e7e-304">2</span></span> | <span data-ttu-id="24e7e-305">20170120</span><span class="sxs-lookup"><span data-stu-id="24e7e-305">20170120</span></span> | <span data-ttu-id="24e7e-306">3500</span><span class="sxs-lookup"><span data-stu-id="24e7e-306">3500</span></span> | <span data-ttu-id="24e7e-307">Patrick</span><span class="sxs-lookup"><span data-stu-id="24e7e-307">Patrick</span></span> |
| <span data-ttu-id="24e7e-308">3</span><span class="sxs-lookup"><span data-stu-id="24e7e-308">3</span></span> | <span data-ttu-id="24e7e-309">20170121</span><span class="sxs-lookup"><span data-stu-id="24e7e-309">20170121</span></span> | <span data-ttu-id="24e7e-310">4000</span><span class="sxs-lookup"><span data-stu-id="24e7e-310">4000</span></span> | <span data-ttu-id="24e7e-311">Jason</span><span class="sxs-lookup"><span data-stu-id="24e7e-311">Jason</span></span> |

<span data-ttu-id="24e7e-312">e, per ogni record, si prevede di toowrite tooa oggetto JSON nel seguente formato:</span><span class="sxs-lookup"><span data-stu-id="24e7e-312">and for each record, you expect toowrite tooa JSON object in below format:</span></span>
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

<span data-ttu-id="24e7e-313">set di dati con output di Hello **JsonFormat** tipo viene definito come segue: (definizione parziale con solo parti pertinenti di hello).</span><span class="sxs-lookup"><span data-stu-id="24e7e-313">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="24e7e-314">In particolare, `structure` sezione definisce i nomi delle proprietà hello personalizzata nel file di destinazione, `nestingSeparator` (valore predefinito è ".") saranno a livello di nidificazione hello tooidentify utilizzato dal nome hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-314">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") will be used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="24e7e-315">Questa sezione è **facoltativo** a meno che si desidera toochange hello proprietà nome, il confronto con il nome di colonna di origine o annidare alcune proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-315">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

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

### <a name="specifying-avroformat"></a><span data-ttu-id="24e7e-316">Specifica di AvroFormat</span><span class="sxs-lookup"><span data-stu-id="24e7e-316">Specifying AvroFormat</span></span>
<span data-ttu-id="24e7e-317">Se si desidera tooparse hello Avro file o scrivono dati hello in formato Avro, impostare hello `format` `type` proprietà troppo**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="24e7e-317">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="24e7e-318">Non è necessario toospecify delle proprietà nella sezione formato hello nella sezione typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-318">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="24e7e-319">Esempio:</span><span class="sxs-lookup"><span data-stu-id="24e7e-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="24e7e-320">formato Avro di toouse in una tabella Hive, è possibile fare riferimento troppo[esercitazione su Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="24e7e-320">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="24e7e-321">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="24e7e-321">Note hello following points:</span></span>  

* <span data-ttu-id="24e7e-322">I [tipi di dati complessi](http://avro.apache.org/docs/current/spec.html#schema_complex) non sono supportati (record, enumerazioni, matrici, mappe, unioni e dati fissi).</span><span class="sxs-lookup"><span data-stu-id="24e7e-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="24e7e-323">Impostazione di OrcFormat</span><span class="sxs-lookup"><span data-stu-id="24e7e-323">Specifying OrcFormat</span></span>
<span data-ttu-id="24e7e-324">Se si desidera tooparse hello ORC file o scrivono dati hello in formato ORC, impostare hello `format` `type` proprietà troppo**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="24e7e-324">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="24e7e-325">Non è necessario toospecify delle proprietà nella sezione formato hello nella sezione typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-325">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="24e7e-326">Esempio:</span><span class="sxs-lookup"><span data-stu-id="24e7e-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="24e7e-327">Se non si desidera copiare i file ORC **come-è** tra sedi locali e cloud archivi dati, è necessario tooinstall hello 8 JRE (Java Runtime Environment) nel computer gateway.</span><span class="sxs-lookup"><span data-stu-id="24e7e-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="24e7e-328">Per un gateway a 64 bit è necessario JRE a 64 bit, mentre per un gateway a 32 bit è necessario JRE a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="24e7e-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="24e7e-329">Entrambe le versioni sono disponibili [qui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="24e7e-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="24e7e-330">Scegliere hello più appropriato.</span><span class="sxs-lookup"><span data-stu-id="24e7e-330">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="24e7e-331">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="24e7e-331">Note hello following points:</span></span>

* <span data-ttu-id="24e7e-332">Tipi di dati complessi non sono supportati (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="24e7e-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="24e7e-333">Il file ORC dispone di tre [opzioni relative alla compressione](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="24e7e-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="24e7e-334">Data Factory supporta la lettura dei dati dal file ORC in uno di questi formati compressi.</span><span class="sxs-lookup"><span data-stu-id="24e7e-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="24e7e-335">Usa compressione hello codec è nei dati di hello metadati tooread hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-335">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="24e7e-336">Tuttavia, durante la scrittura di file ORC tooan, Data Factory sceglie ZLIB, hello predefinito per ORC.</span><span class="sxs-lookup"><span data-stu-id="24e7e-336">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="24e7e-337">Attualmente non è disponibile alcuna opzione toooverride questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="24e7e-337">Currently, there is no option toooverride this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="24e7e-338">Specificare ParquetFormat</span><span class="sxs-lookup"><span data-stu-id="24e7e-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="24e7e-339">Se si desidera tooparse hello Parquet file o scrivono dati hello in formato Parquet, impostare hello `format` `type` proprietà troppo**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="24e7e-339">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="24e7e-340">Non è necessario toospecify delle proprietà nella sezione formato hello nella sezione typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-340">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="24e7e-341">Esempio:</span><span class="sxs-lookup"><span data-stu-id="24e7e-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="24e7e-342">Se non si desidera copiare i file Parquet **come-è** tra sedi locali e cloud archivi dati, è necessario tooinstall hello 8 JRE (Java Runtime Environment) nel computer gateway.</span><span class="sxs-lookup"><span data-stu-id="24e7e-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="24e7e-343">Per un gateway a 64 bit è necessario JRE a 64 bit, mentre per un gateway a 32 bit è necessario JRE a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="24e7e-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="24e7e-344">Entrambe le versioni sono disponibili [qui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="24e7e-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="24e7e-345">Scegliere hello più appropriato.</span><span class="sxs-lookup"><span data-stu-id="24e7e-345">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="24e7e-346">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="24e7e-346">Note hello following points:</span></span>

* <span data-ttu-id="24e7e-347">Tipi di dati complessi non sono supportati (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="24e7e-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="24e7e-348">Dispone di file parquet hello relativi alla compressione le opzioni seguenti: NONE, SNAPPY GZIP e LZO.</span><span class="sxs-lookup"><span data-stu-id="24e7e-348">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="24e7e-349">Data Factory supporta la lettura dei dati dal file ORC in uno di questi formati compressi.</span><span class="sxs-lookup"><span data-stu-id="24e7e-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="24e7e-350">Usa il codec di compressione hello nei dati di hello metadati tooread hello.</span><span class="sxs-lookup"><span data-stu-id="24e7e-350">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="24e7e-351">Tuttavia, durante la scrittura di file Parquet tooa, Data Factory sceglie SNAPPY, hello predefinito per il formato Parquet.</span><span class="sxs-lookup"><span data-stu-id="24e7e-351">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="24e7e-352">Attualmente non è disponibile alcuna opzione toooverride questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="24e7e-352">Currently, there is no option toooverride this behavior.</span></span>
