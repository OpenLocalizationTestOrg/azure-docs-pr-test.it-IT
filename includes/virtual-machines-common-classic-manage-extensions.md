


## <a name="using-vm-extensions"></a><span data-ttu-id="adf2b-101">Uso delle estensioni di macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="adf2b-101">Using VM Extensions</span></span>
<span data-ttu-id="adf2b-102">Le estensioni VM di Azure implementano comportamenti o funzionalità che consentono di altri programmi di lavorare su macchine virtuali di Azure (ad esempio, hello **WebDeployForVSDevTest** estensione consente tooWeb di Visual Studio distribuire soluzioni nella macchina virtuale di Azure) o fornire Hello possibilità per toointeract con hello VM toosupport alcuni altri comportamenti (ad esempio, è possibile utilizzare le estensioni di accesso alla VM hello da PowerShell, hello Azure CLI e tooreset client REST o modificare i valori di accesso remoto nella macchina virtuale di Azure).</span><span class="sxs-lookup"><span data-stu-id="adf2b-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, hello **WebDeployForVSDevTest** extension allows Visual Studio tooWeb Deploy solutions on your Azure VM) or provide hello ability for you toointeract with hello VM toosupport some other behavior (for example, you can use hello VM Access extensions from PowerShell, hello Azure CLI, and REST clients tooreset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="adf2b-103">Per un elenco completo delle estensioni in base che supportano le funzionalità di hello, vedere [estensioni VM di Azure e funzionalità](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="adf2b-103">For a complete list of extensions by hello features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="adf2b-104">Poiché ogni estensione della macchina virtuale supporta una funzionalità specifica, esattamente ciò che è possibile e non con un'estensione dipendono estensione hello.</span><span class="sxs-lookup"><span data-stu-id="adf2b-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on hello extension.</span></span> <span data-ttu-id="adf2b-105">Pertanto, prima di modificare la macchina virtuale, assicurarsi che hanno leggere hello documentazione per l'estensione della macchina virtuale si desidera toouse hello.</span><span class="sxs-lookup"><span data-stu-id="adf2b-105">Therefore, before modifying your VM, make sure you have read hello documentation for hello VM Extension you want toouse.</span></span> <span data-ttu-id="adf2b-106">La rimozione di alcune estensioni di macchina virtuale non è supportata, mentre altre includono proprietà che possono essere impostate e che modificano radicalmente il comportamento della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="adf2b-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="adf2b-107">Hello più comuni sono:</span><span class="sxs-lookup"><span data-stu-id="adf2b-107">hello most common tasks are:</span></span>

1. <span data-ttu-id="adf2b-108">Individuazione delle estensioni disponibili</span><span class="sxs-lookup"><span data-stu-id="adf2b-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="adf2b-109">Aggiornamento delle estensioni caricate</span><span class="sxs-lookup"><span data-stu-id="adf2b-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="adf2b-110">Aggiunta di estensioni</span><span class="sxs-lookup"><span data-stu-id="adf2b-110">Adding Extensions</span></span>
4. <span data-ttu-id="adf2b-111">Rimozione di estensioni</span><span class="sxs-lookup"><span data-stu-id="adf2b-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="adf2b-112">Individuare le estensioni disponibili</span><span class="sxs-lookup"><span data-stu-id="adf2b-112">Find Available Extensions</span></span>
<span data-ttu-id="adf2b-113">È possibile trovare l'estensione, insieme a informazioni estese, usando:</span><span class="sxs-lookup"><span data-stu-id="adf2b-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="adf2b-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="adf2b-114">PowerShell</span></span>
* <span data-ttu-id="adf2b-115">Interfaccia della riga di comando multipiattaforma di Azure (interfaccia della riga di comando di Azure)</span><span class="sxs-lookup"><span data-stu-id="adf2b-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="adf2b-116">API REST di gestione dei servizi</span><span class="sxs-lookup"><span data-stu-id="adf2b-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="adf2b-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="adf2b-117">Azure PowerShell</span></span>
<span data-ttu-id="adf2b-118">Alcune estensioni includono i cmdlet di PowerShell toothem specifico, che possono semplificare la configurazione da PowerShell; ma hello seguenti cmdlet funzionano per tutte le estensioni di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="adf2b-118">Some extensions have PowerShell cmdlets that are specific toothem, which may make their configuration from PowerShell easier; but hello following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="adf2b-119">È possibile utilizzare i seguenti cmdlet tooobtain informazioni sulle estensioni disponibili hello:</span><span class="sxs-lookup"><span data-stu-id="adf2b-119">You can use hello following cmdlets tooobtain information about available extensions:</span></span>

* <span data-ttu-id="adf2b-120">Per le istanze dei ruoli web o ruoli di lavoro, è possibile utilizzare hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="adf2b-120">For instances of web roles or worker roles, you can use hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="adf2b-121">Per le istanze di macchine virtuali, è possibile utilizzare hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="adf2b-121">For instances of Virtual Machines, you can use hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="adf2b-122">Ad esempio, hello seguente esempio di codice viene illustrato come le informazioni per hello toolist **IaaSDiagnostics** estensione utilizzando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="adf2b-122">For example, hello following code example shows how toolist the information for hello **IaaSDiagnostics** extension using PowerShell.</span></span>
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="adf2b-123">Interfaccia della riga di comando di Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="adf2b-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="adf2b-124">Alcune estensioni includono comandi CLI di Azure specifico toothem (hello estensione della macchina virtuale Docker è un esempio), che possono semplificarne la configurazione; ma seguente hello dei comandi per tutte le estensioni di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="adf2b-124">Some extensions have Azure CLI commands that are specific toothem (hello Docker VM Extension is one example), which may make their configuration easier; but hello following commands work for all VM extensions.</span></span>

<span data-ttu-id="adf2b-125">È possibile utilizzare hello **elenco di estensioni di macchina virtuale di azure** comando tooobtain informazioni sulle estensioni disponibili e utilizzare hello **–-json** opzione toodisplay tutte le informazioni disponibili su una o più estensioni.</span><span class="sxs-lookup"><span data-stu-id="adf2b-125">You can use hello **azure vm extension list** command tooobtain information about available extensions, and use hello **–-json** option toodisplay all available information about one or more extensions.</span></span> <span data-ttu-id="adf2b-126">Se non si utilizza un nome di estensione, il comando hello restituisce una descrizione JSON di tutte le estensioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="adf2b-126">If you do not use an extension name, hello command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="adf2b-127">Ad esempio, hello esempio di codice seguente viene illustrato come toolist hello informazioni per hello **IaaSDiagnostics** estensione usando hello Azure CLI **elenco di estensioni di macchina virtuale di azure** comando e Usa hello **–-json** opzione tooreturn di informazioni complete.</span><span class="sxs-lookup"><span data-stu-id="adf2b-127">For example, hello following code example shows how toolist hello information for hello **IaaSDiagnostics** extension using hello Azure CLI **azure vm extension list** command and uses hello **–-json** option tooreturn complete information.</span></span>

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a><span data-ttu-id="adf2b-128">API REST di gestione dei servizi</span><span class="sxs-lookup"><span data-stu-id="adf2b-128">Service Management REST APIs</span></span>
<span data-ttu-id="adf2b-129">È possibile utilizzare le seguenti API REST tooobtain informazioni sulle estensioni disponibili hello:</span><span class="sxs-lookup"><span data-stu-id="adf2b-129">You can use hello following REST APIs tooobtain information about available extensions:</span></span>

* <span data-ttu-id="adf2b-130">Per le istanze dei ruoli web o ruoli di lavoro, è possibile utilizzare hello [elenco delle estensioni disponibili](https://msdn.microsoft.com/library/dn169559.aspx) operazione.</span><span class="sxs-lookup"><span data-stu-id="adf2b-130">For instances of web roles or worker roles, you can use hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="adf2b-131">versioni di hello toolist delle estensioni disponibili, è possibile utilizzare [elenco delle versioni dell'estensione](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="adf2b-131">toolist hello versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="adf2b-132">Per le istanze di macchine virtuali, è possibile utilizzare hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operazione.</span><span class="sxs-lookup"><span data-stu-id="adf2b-132">For instances of Virtual Machines, you can use hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="adf2b-133">versioni di hello toolist delle estensioni disponibili, è possibile utilizzare [elenco delle versioni dell'estensione risorsa](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="adf2b-133">toolist hello versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="adf2b-134">Aggiungere, aggiornare o disabilitare le estensioni</span><span class="sxs-lookup"><span data-stu-id="adf2b-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="adf2b-135">È possibile aggiungere estensioni quando viene creata un'istanza o possono essere aggiunti tooa esegue l'istanza.</span><span class="sxs-lookup"><span data-stu-id="adf2b-135">Extensions can be added when an instance is created or they can be added tooa running instance.</span></span> <span data-ttu-id="adf2b-136">Le estensioni possono essere aggiornate, disabilitate o rimosse.</span><span class="sxs-lookup"><span data-stu-id="adf2b-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="adf2b-137">È possibile eseguire queste azioni utilizzando i cmdlet PowerShell di Azure o utilizzando le operazioni API REST di gestione di hello.</span><span class="sxs-lookup"><span data-stu-id="adf2b-137">You can perform these actions by using Azure PowerShell cmdlets or by using hello Service Management REST API operations.</span></span> <span data-ttu-id="adf2b-138">I parametri sono necessari tooinstall e configurare alcune estensioni.</span><span class="sxs-lookup"><span data-stu-id="adf2b-138">Parameters are required tooinstall and set up some extensions.</span></span> <span data-ttu-id="adf2b-139">Per le estensioni sono supportati parametri pubblici e privati.</span><span class="sxs-lookup"><span data-stu-id="adf2b-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="adf2b-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="adf2b-140">Azure PowerShell</span></span>
<span data-ttu-id="adf2b-141">Tramite i cmdlet PowerShell di Azure è hello più semplice modo tooadd e aggiornare le estensioni.</span><span class="sxs-lookup"><span data-stu-id="adf2b-141">Using Azure PowerShell cmdlets is hello easiest way tooadd and update extensions.</span></span> <span data-ttu-id="adf2b-142">Quando si usano i cmdlet di estensione hello, viene eseguita la maggior parte della configurazione di hello dell'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="adf2b-142">When you use hello extension cmdlets, most of hello configuration of hello extension is done for you.</span></span> <span data-ttu-id="adf2b-143">In alcuni casi, potrebbe essere necessario tooprogrammatically aggiungere un'estensione.</span><span class="sxs-lookup"><span data-stu-id="adf2b-143">At times, you may need tooprogrammatically add an extension.</span></span> <span data-ttu-id="adf2b-144">Quando è necessario questo toodo, è necessario fornire la configurazione hello dell'estensione di hello.</span><span class="sxs-lookup"><span data-stu-id="adf2b-144">When you need toodo this, you must provide hello configuration of hello extension.</span></span>

<span data-ttu-id="adf2b-145">È possibile utilizzare i seguenti cmdlet tooknow se un'estensione richiede una configurazione di parametri pubblici e privati hello:</span><span class="sxs-lookup"><span data-stu-id="adf2b-145">You can use hello following cmdlets tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="adf2b-146">Per le istanze dei ruoli web o ruoli di lavoro, è possibile utilizzare hello **Get-AzureServiceAvailableExtension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="adf2b-146">For instances of web roles or worker roles, you can use hello **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="adf2b-147">Per le istanze di macchine virtuali, è possibile utilizzare hello **Get-AzureVMAvailableExtension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="adf2b-147">For instances of Virtual Machines, you can use hello **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="adf2b-148">API REST di gestione dei servizi</span><span class="sxs-lookup"><span data-stu-id="adf2b-148">Service Management REST APIs</span></span>
<span data-ttu-id="adf2b-149">Quando si recupera un elenco di estensioni disponibili tramite le API REST di hello, si ottengono informazioni su come estensione hello è toobe configurato.</span><span class="sxs-lookup"><span data-stu-id="adf2b-149">When you retrieve a listing of available extensions by using hello REST APIs, you receive information about how hello extension is toobe configured.</span></span> <span data-ttu-id="adf2b-150">informazioni restituite Hello potrebbero visualizzare informazioni sui parametri, rappresentati da uno schema pubblico e privato dello schema.</span><span class="sxs-lookup"><span data-stu-id="adf2b-150">hello information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="adf2b-151">I valori dei parametri pubblici vengono restituiti in query sulle istanze di hello.</span><span class="sxs-lookup"><span data-stu-id="adf2b-151">Public parameter values are returned in queries about hello instances.</span></span> <span data-ttu-id="adf2b-152">I valori dei parametri privati non vengono restituiti.</span><span class="sxs-lookup"><span data-stu-id="adf2b-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="adf2b-153">È possibile utilizzare i seguenti API REST tooknow se un'estensione richiede una configurazione di parametri pubblici e privati hello:</span><span class="sxs-lookup"><span data-stu-id="adf2b-153">You can use hello following REST APIs tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="adf2b-154">Per le istanze dei ruoli web o ruoli di lavoro, hello **PublicConfigurationSchema** e **PrivateConfigurationSchema** elementi contengono informazioni hello in risposta hello hello [elenco Le estensioni disponibili](https://msdn.microsoft.com/library/dn169559.aspx) operazione.</span><span class="sxs-lookup"><span data-stu-id="adf2b-154">For instances of web roles or worker roles, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="adf2b-155">Per le istanze di macchine virtuali, hello **PublicConfigurationSchema** e **PrivateConfigurationSchema** elementi contengono informazioni hello in risposta hello hello [elenco Le estensioni di risorsa](https://msdn.microsoft.com/library/dn495441.aspx) operazione.</span><span class="sxs-lookup"><span data-stu-id="adf2b-155">For instances of Virtual Machines, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="adf2b-156">Le estensioni possono anche usare configurazioni definite con JSON.</span><span class="sxs-lookup"><span data-stu-id="adf2b-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="adf2b-157">Quando vengono utilizzati questi tipi di estensioni, hello solo **SampleConfig** viene utilizzato l'elemento.</span><span class="sxs-lookup"><span data-stu-id="adf2b-157">When these types of extensions are used, only hello **SampleConfig** element is used.</span></span>
> 
> 

