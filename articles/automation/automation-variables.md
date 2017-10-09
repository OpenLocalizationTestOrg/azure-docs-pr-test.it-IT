---
title: Asset aaaVariable in automazione di Azure | Documenti Microsoft
description: Gli asset variabili sono i valori disponibili tooall runbook e le configurazioni DSC in automazione di Azure.  In questo articolo vengono illustrati i dettagli di hello delle variabili e come toowork con essi in creazione grafica e testuale.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="e248a-104">Asset di tipo variabile in Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e248a-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="e248a-105">Gli asset variabili sono i valori disponibili tooall runbook e le configurazioni DSC nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="e248a-105">Variable assets are values that are available tooall runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="e248a-106">Può essere creati, modificati e recuperati dal hello portale di Azure, Windows PowerShell e da un runbook o una configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="e248a-106">They can be created, modified, and retrieved from hello Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="e248a-107">Le variabili di automazione sono utili per hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="e248a-107">Automation variables are useful for hello following scenarios:</span></span>

- <span data-ttu-id="e248a-108">Condivisione di un valore tra più runbook o configurazioni DSC.</span><span class="sxs-lookup"><span data-stu-id="e248a-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="e248a-109">Condividere un valore tra più processi da hello stesso runbook o la configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="e248a-109">Share a value between multiple jobs from hello same runbook or DSC configuration.</span></span>

- <span data-ttu-id="e248a-110">Gestire un valore dal portale hello o dalla riga di comando di Windows PowerShell hello utilizzato dal runbook o le configurazioni DSC, ad esempio un set comune di elementi di configurazione come elenco specifico di nomi di macchina virtuale, un gruppo di risorse specifico, un nome di dominio Active Directory e così via.</span><span class="sxs-lookup"><span data-stu-id="e248a-110">Manage a value from hello portal or from hello Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="e248a-111">Le variabili di automazione sono persistenti in modo da continuare toobe disponibile anche se il runbook hello o configurazione DSC non riesce.</span><span class="sxs-lookup"><span data-stu-id="e248a-111">Automation variables are persisted so that they continue toobe available even if hello runbook or DSC configuration fails.</span></span>  <span data-ttu-id="e248a-112">Ciò consente anche di toobe un valore impostato da un runbook che viene quindi utilizzato da un altro, o da hello stesso runbook o hello configurazione DSC prossima volta che viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="e248a-112">This also allows a value toobe set by one runbook that is then used by another, or is used by hello same runbook or DSC configuration hello next time that it is run.</span></span>

<span data-ttu-id="e248a-113">Quando si crea una variabile, è possibile specificare che venga archiviata in modalità crittografata.</span><span class="sxs-lookup"><span data-stu-id="e248a-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="e248a-114">Quando una variabile è crittografata, viene archiviato in modo sicuro in automazione di Azure e il relativo valore non è possibile recuperare da hello [Get AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet fornito come parte del modulo Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="e248a-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of hello Azure PowerShell module.</span></span>  <span data-ttu-id="e248a-115">Hello unico modo che sia possibile recuperare un valore crittografato è dall'hello **Get-AutomationVariable** attività in un runbook o di una configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="e248a-115">hello only way that an encrypted value can be retrieved is from hello **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="e248a-116">Gli asset sicuri in Automazione di Azure includono credenziali, certificati, connessioni e variabili crittografate.</span><span class="sxs-lookup"><span data-stu-id="e248a-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="e248a-117">Questi asset vengono crittografati e archiviati in automazione di Azure con una chiave univoca generata per ogni account di automazione hello.</span><span class="sxs-lookup"><span data-stu-id="e248a-117">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="e248a-118">La chiave viene crittografata da un certificato master e archiviata in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e248a-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="e248a-119">Prima di archiviare un bene sicuro, chiave hello per account di automazione hello viene decrittografato tramite certificato master hello e quindi asset hello tooencrypt.</span><span class="sxs-lookup"><span data-stu-id="e248a-119">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="e248a-120">Tipi di variabile</span><span class="sxs-lookup"><span data-stu-id="e248a-120">Variable types</span></span>

<span data-ttu-id="e248a-121">Quando si crea una variabile con hello portale di Azure, è necessario specificare un tipo di dati dall'elenco a discesa hello in modo da portale hello può visualizzare controllo appropriato di hello per immettere il valore della variabile hello.</span><span class="sxs-lookup"><span data-stu-id="e248a-121">When you create a variable with hello Azure portal, you must specify a data type from hello drop-down list so hello portal can display hello appropriate control for entering hello variable value.</span></span> <span data-ttu-id="e248a-122">la variabile di Hello non è limitato toothis dati tipo, ma è necessario impostare la variabile di hello tramite Windows PowerShell se si desidera toospecify un valore di un tipo diverso.</span><span class="sxs-lookup"><span data-stu-id="e248a-122">hello variable is not restricted toothis data type, but you must set hello variable using Windows PowerShell if you want toospecify a value of a different type.</span></span> <span data-ttu-id="e248a-123">Se si specifica **non definito**, quindi verrà impostato il valore di hello della variabile hello troppo**$null**, ed è necessario impostare il valore di hello con hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet o **Set-AutomationVariable** attività.</span><span class="sxs-lookup"><span data-stu-id="e248a-123">If you specify **Not defined**, then hello value of hello variable will be set too**$null**, and you must set hello value with hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="e248a-124">È possibile creare o modificare il valore di hello per un tipo di variabile complessa nel portale di hello, ma è possibile fornire un valore di qualsiasi tipo di utilizzo di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e248a-124">You cannot create or change hello value for a complex variable type in hello portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="e248a-125">I tipi complessi verranno restituiti come [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="e248a-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="e248a-126">È possibile archiviare più singola variabile tooa valori mediante la creazione di una matrice o una tabella hash e salvandola toohello variabile.</span><span class="sxs-lookup"><span data-stu-id="e248a-126">You can store multiple values tooa single variable by creating an array or hashtable and saving it toohello variable.</span></span>

<span data-ttu-id="e248a-127">di seguito Hello sono un elenco dei tipi di variabili disponibili in automazione di:</span><span class="sxs-lookup"><span data-stu-id="e248a-127">hello following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="e248a-128">String</span><span class="sxs-lookup"><span data-stu-id="e248a-128">String</span></span>
* <span data-ttu-id="e248a-129">Integer</span><span class="sxs-lookup"><span data-stu-id="e248a-129">Integer</span></span>
* <span data-ttu-id="e248a-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="e248a-130">DateTime</span></span>
* <span data-ttu-id="e248a-131">Boolean</span><span class="sxs-lookup"><span data-stu-id="e248a-131">Boolean</span></span>
* <span data-ttu-id="e248a-132">Null</span><span class="sxs-lookup"><span data-stu-id="e248a-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="e248a-133">Cmdlet e attività flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="e248a-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="e248a-134">cmdlet di Hello in hello nella tabella seguente vengono utilizzati toocreate e gestire le variabili di automazione con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e248a-134">hello cmdlets in hello following table are used toocreate and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="e248a-135">Vengono forniti come parte di hello [modulo Azure PowerShell](../powershell-install-configure.md) che è possibile utilizzare nei runbook di automazione e la configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="e248a-135">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="e248a-136">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e248a-136">Cmdlets</span></span>|<span data-ttu-id="e248a-137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e248a-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="e248a-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="e248a-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="e248a-139">Recupera il valore di hello di una variabile esistente.</span><span class="sxs-lookup"><span data-stu-id="e248a-139">Retrieves hello value of an existing variable.</span></span>|
|[<span data-ttu-id="e248a-140">New-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="e248a-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="e248a-141">Crea una nuova variabile e ne imposta il valore.</span><span class="sxs-lookup"><span data-stu-id="e248a-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="e248a-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="e248a-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="e248a-143">Rimuove una variabile esistente.</span><span class="sxs-lookup"><span data-stu-id="e248a-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="e248a-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="e248a-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="e248a-145">Imposta il valore di hello per una variabile esistente.</span><span class="sxs-lookup"><span data-stu-id="e248a-145">Sets hello value for an existing variable.</span></span>|

<span data-ttu-id="e248a-146">le attività del flusso di lavoro Hello in hello nella tabella seguente vengono utilizzati tooaccess le variabili di automazione in un runbook.</span><span class="sxs-lookup"><span data-stu-id="e248a-146">hello workflow activities in hello following table are used tooaccess Automation variables in a runbook.</span></span> <span data-ttu-id="e248a-147">Sono disponibili solo per l'utilizzo in un runbook o di una configurazione DSC e non vengono fornite come parte del modulo Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="e248a-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of hello Azure PowerShell module.</span></span>

|<span data-ttu-id="e248a-148">Attività flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="e248a-148">Workflow Activities</span></span>|<span data-ttu-id="e248a-149">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e248a-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="e248a-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="e248a-150">Get-AutomationVariable</span></span>|<span data-ttu-id="e248a-151">Recupera il valore di hello di una variabile esistente.</span><span class="sxs-lookup"><span data-stu-id="e248a-151">Retrieves hello value of an existing variable.</span></span>|
|<span data-ttu-id="e248a-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="e248a-152">Set-AutomationVariable</span></span>|<span data-ttu-id="e248a-153">Imposta il valore di hello per una variabile esistente.</span><span class="sxs-lookup"><span data-stu-id="e248a-153">Sets hello value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="e248a-154">È consigliabile evitare l'uso delle variabili nel hello – parametro Name di **Get-AutomationVariable** in un runbook o di una configurazione DSC, poiché ciò può complicare l'individuazione delle dipendenze tra i runbook o configurazione DSC e automazione variabili in fase di progettazione.</span><span class="sxs-lookup"><span data-stu-id="e248a-154">You should avoid using variables in hello –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="e248a-155">Creazione di una nuova variabile di automazione</span><span class="sxs-lookup"><span data-stu-id="e248a-155">Creating a new Automation variable</span></span>

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a><span data-ttu-id="e248a-156">toocreate una nuova variabile con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e248a-156">toocreate a new variable with hello Azure portal</span></span>

1. <span data-ttu-id="e248a-157">Scegliere l'account di automazione, hello **asset** riquadro e quindi su hello **asset** pannello seleziona **variabili**.</span><span class="sxs-lookup"><span data-stu-id="e248a-157">From your Automation account, click hello **Assets** tile and then on hello **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="e248a-158">In hello **variabili** riquadro, seleziona **aggiungere una variabile**.</span><span class="sxs-lookup"><span data-stu-id="e248a-158">On hello **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="e248a-159">Completare le opzioni di hello in hello **nuova variabile** pannello e fare clic su **crea** Salva hello nuova variabile.</span><span class="sxs-lookup"><span data-stu-id="e248a-159">Complete hello options on hello **New Variable** blade and click **Create** save hello new variable.</span></span>

### <a name="toocreate-a-new-variable-with-windows-powershell"></a><span data-ttu-id="e248a-160">toocreate una nuova variabile con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e248a-160">toocreate a new variable with Windows PowerShell</span></span>

<span data-ttu-id="e248a-161">Hello [New AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet crea una nuova variabile e imposta il valore iniziale.</span><span class="sxs-lookup"><span data-stu-id="e248a-161">hello [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="e248a-162">È possibile recuperare il valore hello utilizzando [Get AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="e248a-162">You can retrieve hello value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="e248a-163">Se il valore di hello è un tipo semplice, viene restituito lo stesso tipo.</span><span class="sxs-lookup"><span data-stu-id="e248a-163">If hello value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="e248a-164">Se è di tipo complesso, verrà restituito un **PSCustomObject** .</span><span class="sxs-lookup"><span data-stu-id="e248a-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="e248a-165">Mostra i comandi di esempio seguente Hello come toocreate una variabile di tipo stringa e restituirne il valore.</span><span class="sxs-lookup"><span data-stu-id="e248a-165">hello following sample commands show how toocreate a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="e248a-166">Mostra i comandi di esempio Hello seguente come una variabile con un oggetto complesso toocreate digitare e quindi restituire le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="e248a-166">hello following sample commands show how toocreate a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="e248a-167">In questo caso, viene usato un oggetto macchina virtuale recuperato da **Get-AzureRmVm**.</span><span class="sxs-lookup"><span data-stu-id="e248a-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="e248a-168">Uso di una variabile in un Runbook o in una configurazione DSC</span><span class="sxs-lookup"><span data-stu-id="e248a-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="e248a-169">Hello utilizzare **Set-AutomationVariable** tooset hello valore dell'attività di una variabile di automazione in un runbook o una configurazione DSC e hello **Get-AutomationVariable** tooretrieve è.</span><span class="sxs-lookup"><span data-stu-id="e248a-169">Use hello **Set-AutomationVariable** activity tooset hello value of an Automation variable in a runbook or DSC configuration, and hello **Get-AutomationVariable** tooretrieve it.</span></span>  <span data-ttu-id="e248a-170">È consigliabile utilizzare hello **Set-AzureAutomationVariable** o **Get-AzureAutomationVariable** cmdlet in una configurazione di DSC, perché sono meno efficiente dell'attività flusso di lavoro hello o un runbook.</span><span class="sxs-lookup"><span data-stu-id="e248a-170">You shouldn't use hello **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than hello workflow activities.</span></span>  <span data-ttu-id="e248a-171">È inoltre Impossibile recuperare il valore di hello delle variabili sicura con **Get-AzureAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="e248a-171">You also cannot retrieve hello value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="e248a-172">Hello solo modo toocreate una variabile dall'interno di un runbook o configurazione di DSC è hello toouse [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e248a-172">hello only way toocreate a new variable from within a runbook or DSC configuration is toouse hello [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="e248a-173">Esempi di runbook testuali</span><span class="sxs-lookup"><span data-stu-id="e248a-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="e248a-174">Impostazione e recupero di un valore semplice da una variabile</span><span class="sxs-lookup"><span data-stu-id="e248a-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="e248a-175">Mostra i comandi di esempio seguente Hello come tooset e recuperare una variabile in un runbook testuale.</span><span class="sxs-lookup"><span data-stu-id="e248a-175">hello following sample commands show how tooset and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="e248a-176">In questo esempio si presuppone che siano già state create variabili di tipo integer denominate *NumberOfIterations* e *NumberOfRunnings* e una variabile di tipo stringa denominata *SampleMessage*.</span><span class="sxs-lookup"><span data-stu-id="e248a-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="e248a-177">Impostazione e recupero di un oggetto complesso in una variabile</span><span class="sxs-lookup"><span data-stu-id="e248a-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="e248a-178">Mostra codice di esempio seguente Hello come tooupdate una variabile con un valore complesso in un runbook testuale.</span><span class="sxs-lookup"><span data-stu-id="e248a-178">hello following sample code shows how tooupdate a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="e248a-179">In questo esempio, una macchina virtuale di Azure viene recuperata con **Get-AzureVM** e salvato tooan variabile di automazione esistente.</span><span class="sxs-lookup"><span data-stu-id="e248a-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="e248a-180">Come illustrato in [Tipi di variabile](#variable-types), viene archiviata come PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="e248a-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="e248a-181">Nel seguente codice di hello, il valore di hello viene recuperato dalla macchina virtuale di hello toostart variabile e usato hello.</span><span class="sxs-lookup"><span data-stu-id="e248a-181">In hello following code, hello value is retrieved from hello variable and used toostart hello virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="e248a-182">Impostazione e recupero di una raccolta in una variabile</span><span class="sxs-lookup"><span data-stu-id="e248a-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="e248a-183">Mostra codice di esempio seguente Hello come toouse una variabile con una raccolta di valori complessi in un runbook testuale.</span><span class="sxs-lookup"><span data-stu-id="e248a-183">hello following sample code shows how toouse a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="e248a-184">In questo esempio, vengono recuperate più macchine virtuali di Azure con **Get-AzureVM** e salvato tooan variabile di automazione esistente.</span><span class="sxs-lookup"><span data-stu-id="e248a-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="e248a-185">Come illustrato in [Tipi di variabile](#variable-types), viene archiviata una raccolta di PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="e248a-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="e248a-186">Nel seguente codice di hello, raccolta hello viene recuperato dalla variabile hello e utilizzato toostart ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e248a-186">In hello following code, hello collection is retrieved from hello variable and used toostart each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="e248a-187">Esempi di runbook grafici</span><span class="sxs-lookup"><span data-stu-id="e248a-187">Graphical runbook samples</span></span>

<span data-ttu-id="e248a-188">In un runbook con interfaccia grafico, aggiungere hello **Get-AutomationVariable** o **Set-AutomationVariable** facendo clic sulla variabile hello nel riquadro libreria hello dell'editor grafico hello e selezionando hello attività desiderata.</span><span class="sxs-lookup"><span data-stu-id="e248a-188">In a graphical runbook, you add hello **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on hello variable in hello Library pane of hello graphical editor and selecting hello activity you want.</span></span>

![Aggiungere variabili toocanvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="e248a-190">Impostazione dei valori in una variabile</span><span class="sxs-lookup"><span data-stu-id="e248a-190">Setting values in a variable</span></span>
<span data-ttu-id="e248a-191">Hello immagine seguente mostra tooupdate le attività di esempio una variabile con un valore semplice in un runbook grafico.</span><span class="sxs-lookup"><span data-stu-id="e248a-191">hello following image shows sample activities tooupdate a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="e248a-192">In questo esempio, una singola macchina virtuale di Azure viene recuperata con **Get AzureRmVM** e nome del computer hello salvata tooan variabile di automazione esistente con un tipo di stringa.</span><span class="sxs-lookup"><span data-stu-id="e248a-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and hello computer name is saved tooan existing Automation variable with a type of String.</span></span>  <span data-ttu-id="e248a-193">Non è rilevante se hello [collegamento è una pipeline o sequenza](automation-graphical-authoring-intro.md#links-and-workflow) poiché è probabile che solo un singolo oggetto nell'output di hello.</span><span class="sxs-lookup"><span data-stu-id="e248a-193">It doesn't matter whether hello [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in hello output.</span></span>

![Impostare una variabile semplice](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="e248a-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e248a-195">Next Steps</span></span>

* <span data-ttu-id="e248a-196">toolearn più sulla connessione delle attività tra loro in grafici per la modifica, vedere [collegamenti nella creazione di grafici](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="e248a-196">toolearn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="e248a-197">tooget avviato con runbook grafici, vedere [il primo runbook grafico](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="e248a-197">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

