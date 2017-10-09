
<span data-ttu-id="90234-101">La diagnosi dei problemi con un servizio cloud di Microsoft Azure, è necessario raccogliere i file di log del servizio hello in macchine virtuali quando si verificano problemi di hello.</span><span class="sxs-lookup"><span data-stu-id="90234-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting hello service’s log files on virtual machines as hello issues occur.</span></span> <span data-ttu-id="90234-102">È possibile utilizzare raccolta occasionale di tooperfom hello estensione AzureLogCollector su richiesta di log da uno o più macchine virtuali del servizio Cloud (da ruoli web e ruoli di lavoro) e trasferimento hello raccolti file tooan account di archiviazione di Azure – senza dover accedere in remoto tooany di hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="90234-102">You can use hello AzureLogCollector extension on-demand tooperfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer hello collected files tooan Azure storage account – all without remotely logging on tooany of hello VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="90234-103">Le descrizioni per la maggior parte delle informazioni di hello registrata è reperibile all'http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span><span class="sxs-lookup"><span data-stu-id="90234-103">Descriptions for most of hello logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="90234-104">Sono disponibili due modalità di raccolta varia tipi hello toobe file raccolti.</span><span class="sxs-lookup"><span data-stu-id="90234-104">There are two modes of collection dependent on hello types of files toobe collected.</span></span>

* <span data-ttu-id="90234-105">Solo log di agenti guest di Azure (GA).</span><span class="sxs-lookup"><span data-stu-id="90234-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="90234-106">Questa modalità di raccolta include gli agenti guest tooAzure correlati registri hello tutti e altri componenti di Azure.</span><span class="sxs-lookup"><span data-stu-id="90234-106">This collection mode includes all hello logs related tooAzure guest agents and other Azure components.</span></span>
* <span data-ttu-id="90234-107">Tutti i log (Completa).</span><span class="sxs-lookup"><span data-stu-id="90234-107">All Logs (Full).</span></span> <span data-ttu-id="90234-108">Questa modalità di raccolta raccoglierà tutti i file in modalità Agenti guest, oltre a:</span><span class="sxs-lookup"><span data-stu-id="90234-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="90234-109">log eventi di sistema e dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="90234-109">system and application event logs</span></span>
  * <span data-ttu-id="90234-110">log degli errori HTTP</span><span class="sxs-lookup"><span data-stu-id="90234-110">HTTP error logs</span></span>
  * <span data-ttu-id="90234-111">log di IIS</span><span class="sxs-lookup"><span data-stu-id="90234-111">IIS Logs</span></span>
  * <span data-ttu-id="90234-112">log di installazione</span><span class="sxs-lookup"><span data-stu-id="90234-112">Setup logs</span></span>
  * <span data-ttu-id="90234-113">altri log di sistema</span><span class="sxs-lookup"><span data-stu-id="90234-113">other system logs</span></span>

<span data-ttu-id="90234-114">In entrambe le modalità di raccolta, è possono specificare le cartelle di raccolta dati aggiuntivi utilizzando una raccolta di hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="90234-114">In both collection modes, additional data collection folders can be specified by using a collection of hello following structure:</span></span>

* <span data-ttu-id="90234-115">**Nome**: nome hello dell'insieme di hello, che verrà utilizzato come nome hello della sottocartella all'interno di hello zip file toobe raccolti.</span><span class="sxs-lookup"><span data-stu-id="90234-115">**Name**: hello name of hello collection, which will be used as hello name of subfolder inside hello zip file toobe collected.</span></span>
* <span data-ttu-id="90234-116">**Percorso**: hello toohello cartella percorso nella macchina virtuale hello in cui verrà raccolto il file.</span><span class="sxs-lookup"><span data-stu-id="90234-116">**Location**: hello path toohello folder on hello virtual machine where file will be collected.</span></span>
* <span data-ttu-id="90234-117">**SearchPattern**: modello hello di nomi di hello di toobe file raccolti.</span><span class="sxs-lookup"><span data-stu-id="90234-117">**SearchPattern**: hello pattern of hello names of files toobe collected.</span></span> <span data-ttu-id="90234-118">Il valore predefinito è "*".</span><span class="sxs-lookup"><span data-stu-id="90234-118">Default is “*”</span></span>
* <span data-ttu-id="90234-119">**Ricorsivo**: se il file hello verranno raccolti in modo ricorsivo nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="90234-119">**Recursive**: if hello files will be collected recursively under hello folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90234-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="90234-120">Prerequisites</span></span>
* <span data-ttu-id="90234-121">È necessario toohave un account di archiviazione per i file zip di estensione toosave generato.</span><span class="sxs-lookup"><span data-stu-id="90234-121">You need toohave a storage account for extension toosave generated zip files.</span></span>
* <span data-ttu-id="90234-122">È necessario assicurarsi che siano in uso i cmdlet di Azure PowerShell v0.8.0 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="90234-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="90234-123">Per altre informazioni, vedere la pagina relativa ai [Download di Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="90234-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-hello-extension"></a><span data-ttu-id="90234-124">Aggiungere l'estensione hello</span><span class="sxs-lookup"><span data-stu-id="90234-124">Add hello extension</span></span>
<span data-ttu-id="90234-125">È possibile utilizzare [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlet o [API REST di Gestione servizio](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello estensione AzureLogCollector.</span><span class="sxs-lookup"><span data-stu-id="90234-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector extension.</span></span>

<span data-ttu-id="90234-126">Per i servizi Cloud, i cmdlet Powershell di Azure esistente, hello **Set-AzureServiceExtension**, può essere utilizzato tooenable hello estensione nelle istanze del ruolo del servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="90234-126">For Cloud Services, hello existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used tooenable hello extension on Cloud Service role instances.</span></span> <span data-ttu-id="90234-127">Ogni volta che questa estensione viene abilitata tramite questo cmdlet, viene attivata la raccolta di log nelle istanze del ruolo selezionato hello dei ruoli selezionati.</span><span class="sxs-lookup"><span data-stu-id="90234-127">Every time this extension is enabled through this cmdlet, log collection is triggered on hello selected role instances of selected roles.</span></span>

<span data-ttu-id="90234-128">Per le macchine virtuali, i cmdlet Powershell di Azure esistente, hello **Set-AzureVMExtension**, può essere utilizzato tooenable hello estensione nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="90234-128">For Virtual Machines, hello existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used tooenable hello extension on Virtual Machines.</span></span> <span data-ttu-id="90234-129">Ogni volta che questa estensione viene abilitata tramite i cmdlet di hello, viene attivata la raccolta di log in ogni istanza.</span><span class="sxs-lookup"><span data-stu-id="90234-129">Every time this extension is enabled through hello cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="90234-130">Internamente, questa estensione Usa hello PublicConfiguration basata su JSON e PrivateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="90234-130">Internally, this extension uses hello JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="90234-131">di seguito Hello è layout hello di un file JSON di esempio per la configurazione pubblica e privata.</span><span class="sxs-lookup"><span data-stu-id="90234-131">hello following is hello layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="90234-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="90234-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a><span data-ttu-id="90234-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="90234-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="90234-134">Per questa estensione non richiede l'uso della configurazione **privateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="90234-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="90234-135">È possibile specificare solo una struttura vuota per hello **– PrivateConfiguration** argomento.</span><span class="sxs-lookup"><span data-stu-id="90234-135">You can just provide an empty structure for hello **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="90234-136">È possibile seguire una delle due hello seguendo i passaggi tooadd hello AzureLogCollector tooone o più istanze di un servizio Cloud o macchina virtuale di determinati ruoli, quali trigger hello raccolte su ogni toorun VM e inviare file raccolti hello tooAzure account specificato.</span><span class="sxs-lookup"><span data-stu-id="90234-136">You can follow one of hello two following steps tooadd hello AzureLogCollector tooone or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers hello collections on each VM toorun and send hello collected files tooAzure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="90234-137">Aggiunta come estensione del servizio</span><span class="sxs-lookup"><span data-stu-id="90234-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="90234-138">Seguire la sottoscrizione tooyour hello istruzioni tooconnect Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90234-138">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>
2. <span data-ttu-id="90234-139">Specificare nome del servizio hello, slot, ruoli e toowhich le istanze di ruolo desiderato tooadd e abilitare l'estensione AzureLogCollector hello.</span><span class="sxs-lookup"><span data-stu-id="90234-139">Specify hello service name, slot, roles, and role instances toowhich you want tooadd and enable hello AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="90234-140">Specificare hello cartella di dati aggiuntivi per il quale verranno raccolti i file (questo passaggio è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="90234-140">Specify hello additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="90234-141">È possibile utilizzare token `%roleroot%` toospecify hello unità radice del ruolo perché non viene usata un'unità fissa.</span><span class="sxs-lookup"><span data-stu-id="90234-141">You can use token `%roleroot%` toospecify hello role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="90234-142">Fornire nome account di archiviazione di Azure hello e i file di chiave toowhich raccolti verranno caricati.</span><span class="sxs-lookup"><span data-stu-id="90234-142">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="90234-143">Chiamare hello SetAzureServiceLogCollector.ps1 (incluso alla fine di hello dell'articolo hello) come estensione AzureLogCollector di hello tooenable indicato di seguito per un servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="90234-143">Call hello SetAzureServiceLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="90234-144">Una volta completata l'esecuzione di hello, è possibile trovare il file di hello caricato in`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="90234-144">Once hello execution is completed, you can find hello uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="90234-145">di seguito Hello è definizione hello di hello parametri script toohello.</span><span class="sxs-lookup"><span data-stu-id="90234-145">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="90234-146">(Copiati anche sotto.)</span><span class="sxs-lookup"><span data-stu-id="90234-146">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* <span data-ttu-id="90234-147">*ServiceName*: nome del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="90234-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="90234-148">*Roles*: elenco di ruoli, ad esempio "WebRole1" o "WorkerRole1".</span><span class="sxs-lookup"><span data-stu-id="90234-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="90234-149">*Istanze*: un elenco di nomi di istanze del ruolo di hello separati da virgola, utilizzare una stringa con caratteri jolly hello ("*") per tutte le istanze di ruolo.</span><span class="sxs-lookup"><span data-stu-id="90234-149">*Instances*: A list of hello names of role instances separated by comma -- use hello wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="90234-150">*Slot*: nome dello slot.</span><span class="sxs-lookup"><span data-stu-id="90234-150">*Slot*: Slot name.</span></span> <span data-ttu-id="90234-151">"Production" o "Staging".</span><span class="sxs-lookup"><span data-stu-id="90234-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="90234-152">*Mode*: modalità di raccolta.</span><span class="sxs-lookup"><span data-stu-id="90234-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="90234-153">"Full" o "GA".</span><span class="sxs-lookup"><span data-stu-id="90234-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="90234-154">*StorageAccountName*: nome dell'account di archiviazione di Azure per l'archiviazione dei dati raccolti.</span><span class="sxs-lookup"><span data-stu-id="90234-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="90234-155">*StorageAccountKey*: nome della chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="90234-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="90234-156">*AdditionalDataLocationList*: un elenco di hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="90234-156">*AdditionalDataLocationList*: A list of hello following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="90234-157">Aggiunta come estensione VM</span><span class="sxs-lookup"><span data-stu-id="90234-157">Adding as a VM Extension</span></span>
<span data-ttu-id="90234-158">Seguire la sottoscrizione tooyour hello istruzioni tooconnect Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90234-158">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>

1. <span data-ttu-id="90234-159">Specificare il nome di servizio hello, macchina virtuale e la modalità di raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="90234-159">Specify hello service name, VM, and hello collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="90234-160">Fornire nome account di archiviazione di Azure hello e i file di chiave toowhich raccolti verranno caricati.</span><span class="sxs-lookup"><span data-stu-id="90234-160">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="90234-161">Chiamare hello SetAzureVMLogCollector.ps1 (incluso alla fine di hello dell'articolo hello) come estensione AzureLogCollector di hello tooenable indicato di seguito per un servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="90234-161">Call hello SetAzureVMLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="90234-162">Una volta completata l'esecuzione di hello, è possibile trovare il file di hello caricato in https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span><span class="sxs-lookup"><span data-stu-id="90234-162">Once hello execution is completed, you can find hello uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="90234-163">di seguito Hello è definizione hello di hello parametri script toohello.</span><span class="sxs-lookup"><span data-stu-id="90234-163">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="90234-164">(Copiati anche sotto.)</span><span class="sxs-lookup"><span data-stu-id="90234-164">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* <span data-ttu-id="90234-165">ServiceName: nome del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="90234-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="90234-166">Nome di hello VMName di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="90234-166">VMName hello name of hello VM.</span></span>
* <span data-ttu-id="90234-167">Mode: modalità di raccolta.</span><span class="sxs-lookup"><span data-stu-id="90234-167">Mode: Collection mode.</span></span> <span data-ttu-id="90234-168">"Full" o "GA".</span><span class="sxs-lookup"><span data-stu-id="90234-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="90234-169">StorageAccountName: nome dell'account di archiviazione di Azure per l'archiviazione dei dati raccolti.</span><span class="sxs-lookup"><span data-stu-id="90234-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="90234-170">StorageAccountKey: nome della chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="90234-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="90234-171">AdditionalDataLocationList: Un elenco di hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="90234-171">AdditionalDataLocationList: A list of hello following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="90234-172">File script di PowerShell per l'estensione</span><span class="sxs-lookup"><span data-stu-id="90234-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="90234-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="90234-173">SetAzureServiceLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="90234-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="90234-174">SetAzureVMLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="90234-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90234-175">Next Steps</span></span>
<span data-ttu-id="90234-176">È ora possibile esaminare o copiare i log da una posizione semplificata.</span><span class="sxs-lookup"><span data-stu-id="90234-176">Now you can examine or copy your logs from one very simple location.</span></span>

