## <a name="repeatability-during-copy"></a><span data-ttu-id="9a68c-101">Ripetibilità durante la copia</span><span class="sxs-lookup"><span data-stu-id="9a68c-101">Repeatability during Copy</span></span>
<span data-ttu-id="9a68c-102">Quando la copia di dati tooAzure SQL di SQL Server da altri dati archivia uno esigenze tookeep ripetibilità in presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="9a68c-102">When copying data tooAzure SQL/SQL Server from other data stores one needs tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="9a68c-103">Quando si copiano dati tooAzure Database SQL o SQL Server, attività di copia verrà tabella di sink toohello predefinita APPEND hello set di dati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="9a68c-103">When copying data tooAzure SQL/SQL Server Database, copy activity will by default APPEND hello data set toohello sink table by default.</span></span> <span data-ttu-id="9a68c-104">La copia dei dati da un'origine di file CSV (dati di valori separati da virgole) che contiene due record tooAzure Database SQL o SQL Server, ad esempio, questo è quale tabella hello ha un aspetto simile:</span><span class="sxs-lookup"><span data-stu-id="9a68c-104">For example, when copying data from a CSV (comma separated values data) file source containing two records tooAzure SQL/SQL Server Database, this is what hello table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="9a68c-105">Si supponga che si trovati errori nel file di origine e la quantità di hello aggiornato di Tube verso il basso dalla too4 2 nel file di origine hello.</span><span class="sxs-lookup"><span data-stu-id="9a68c-105">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4 in hello source file.</span></span> <span data-ttu-id="9a68c-106">Se si esegue nuovamente la sezione dati hello durante tale periodo, sono disponibili due nuovi record accodato tooAzure Database SQL o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9a68c-106">If you re-run hello data slice for that period, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="9a68c-107">Hello seguente si presuppone che nessuna delle colonne hello nella tabella hello è il vincolo di chiave primaria di hello.</span><span class="sxs-lookup"><span data-stu-id="9a68c-107">hello below assumes none of hello columns in hello table have hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="9a68c-108">tooavoid, sarà necessario semantica UPSERT toospecify mediante l'utilizzo di uno di hello seguito 2 meccanismi indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9a68c-108">tooavoid this, you will need toospecify UPSERT semantics by leveraging one of hello below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="9a68c-109">Una sezione può essere nuovamente eseguita automaticamente in Data Factory di Azure in base ai criteri di ripetizione hello specificato.</span><span class="sxs-lookup"><span data-stu-id="9a68c-109">A slice can be re-run automatically in Azure Data Factory as per hello retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="9a68c-110">Meccanismo 1</span><span class="sxs-lookup"><span data-stu-id="9a68c-110">Mechanism 1</span></span>
<span data-ttu-id="9a68c-111">È possibile sfruttare **sqlWriterCleanupScript** toofirst proprietà eseguire l'azione di pulizia quando viene eseguita una sezione.</span><span class="sxs-lookup"><span data-stu-id="9a68c-111">You can leverage **sqlWriterCleanupScript** property toofirst perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="9a68c-112">Hello script di pulizia verrà eseguito prima durante la copia di una sezione specificata in cui verrà eliminati dati hello dall'intervallo di toothat hello tabella SQL corrispondente.</span><span class="sxs-lookup"><span data-stu-id="9a68c-112">hello cleanup script would be executed first during copy for a given slice which would delete hello data from hello SQL Table corresponding toothat slice.</span></span> <span data-ttu-id="9a68c-113">attività Hello verrà successivamente inserire dati hello hello tabella SQL.</span><span class="sxs-lookup"><span data-stu-id="9a68c-113">hello activity will subsequently insert hello data into hello SQL Table.</span></span> 

<span data-ttu-id="9a68c-114">Se la sezione hello è ora eseguire di nuovo, quindi si troverà quantità hello viene aggiornata come desiderato.</span><span class="sxs-lookup"><span data-stu-id="9a68c-114">If hello slice is now re-run, then you will find hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="9a68c-115">Si supponga che hello record rondellapiatta viene rimosso da file csv originale hello.</span><span class="sxs-lookup"><span data-stu-id="9a68c-115">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="9a68c-116">Quindi eseguire di nuovo sezione hello produrrebbe hello seguente risultato:</span><span class="sxs-lookup"><span data-stu-id="9a68c-116">Then re-running hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="9a68c-117">Non è una novità era toobe eseguita.</span><span class="sxs-lookup"><span data-stu-id="9a68c-117">Nothing new had toobe done.</span></span> <span data-ttu-id="9a68c-118">esecuzione dell'attività di copia Hello hello pulizia dati dello script toodelete hello corrispondente per tale sezione.</span><span class="sxs-lookup"><span data-stu-id="9a68c-118">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="9a68c-119">Quindi leggere l'input di hello da file csv hello (contenute quindi solo 1 record) e viene inserita nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="9a68c-119">Then it read hello input from hello csv (which then contained only 1 record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="9a68c-120">Meccanismo 2</span><span class="sxs-lookup"><span data-stu-id="9a68c-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9a68c-121">Attualmente sliceIdentifierColumnName non è supportato per SQL Data Warehouse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9a68c-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="9a68c-122">Ripetibilità di tooachieve un altro meccanismo consiste nel disporre di una colonna dedicata (**sliceIdentifierColumnName**) in hello tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9a68c-122">Another mechanism tooachieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in hello target Table.</span></span> <span data-ttu-id="9a68c-123">Questa colonna verrà usata dalla Data Factory di Azure tooensure hello origine e destinazione la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="9a68c-123">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="9a68c-124">Questo approccio funziona quando è disponibile una flessibilità nella modifica o la definizione di schema di tabella SQL di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="9a68c-124">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="9a68c-125">Questa colonna viene utilizzata da Data Factory di Azure per scopi di ripetibilità e nel processo di hello Azure Data Factory non apporterà qualsiasi schema cambia toohello tabella.</span><span class="sxs-lookup"><span data-stu-id="9a68c-125">This column would be used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory will not make any schema changes toohello Table.</span></span> <span data-ttu-id="9a68c-126">Modo toouse questo approccio:</span><span class="sxs-lookup"><span data-stu-id="9a68c-126">Way toouse this approach:</span></span>

1. <span data-ttu-id="9a68c-127">Definire una colonna di tipo binary (32) di destinazione hello tabella SQL.</span><span class="sxs-lookup"><span data-stu-id="9a68c-127">Define a column of type binary (32) in hello destination SQL Table.</span></span> <span data-ttu-id="9a68c-128">in cui non sia presente alcun vincolo.</span><span class="sxs-lookup"><span data-stu-id="9a68c-128">There should be no constraints on this column.</span></span> <span data-ttu-id="9a68c-129">Ai fini di questo esempio, la colonna viene denominata "ColumnForADFuseOnly".</span><span class="sxs-lookup"><span data-stu-id="9a68c-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="9a68c-130">Utilizzarlo nell'attività di copia hello come segue:</span><span class="sxs-lookup"><span data-stu-id="9a68c-130">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="9a68c-131">Azure Data Factory popola questa colonna in base alle necessità tooensure hello origine e destinazione mantenere la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="9a68c-131">Azure Data Factory will populate this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="9a68c-132">i valori Hello di questa colonna non utilizzare di fuori di questo contesto utente hello.</span><span class="sxs-lookup"><span data-stu-id="9a68c-132">hello values of this column should not be used outside of this context by hello user.</span></span> 

<span data-ttu-id="9a68c-133">Toomechanism simile 1, verrà di attività di copia automaticamente prima pulizia dei dati di hello per hello assegnato slice dalla destinazione hello tabella SQL e quindi eseguire attività di copia hello in genere dati hello tooinsert toodestination di origine per tale sezione.</span><span class="sxs-lookup"><span data-stu-id="9a68c-133">Similar toomechanism 1, Copy Activity will automatically first clean up hello data for hello given slice from hello destination SQL Table and then run hello copy activity normally tooinsert hello data from source toodestination for that slice.</span></span> 

