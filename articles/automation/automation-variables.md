---
title: Asset di tipo variabile in Automazione di Azure | Documentazione Microsoft
description: Gli asset di tipo variabile sono valori disponibili per tutti i runbook e le configurazioni DSC in Automazione di Azure.  Questo articolo illustra nel dettaglio le variabili e spiega come usarle nella creazione testuale e grafica.
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
ms.openlocfilehash: dc00e1e5fa8df5cb55e7e2672137d1df44133773
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="e11a3-104">Asset di tipo variabile in Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e11a3-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="e11a3-105">Gli asset di tipo variabile sono valori disponibili per tutti i runbook e le configurazioni DSC nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="e11a3-105">Variable assets are values that are available to all runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="e11a3-106">Possono essere creati, modificati e recuperati dal portale di Azure, da Windows PowerShell e dall'interno di un runbook o di una configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="e11a3-106">They can be created, modified, and retrieved from the Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="e11a3-107">Le variabili di automazione sono utili per gli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="e11a3-107">Automation variables are useful for the following scenarios:</span></span>

- <span data-ttu-id="e11a3-108">Condivisione di un valore tra più runbook o configurazioni DSC.</span><span class="sxs-lookup"><span data-stu-id="e11a3-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="e11a3-109">Condivisione di un valore tra più processi dello stesso runbook o configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="e11a3-109">Share a value between multiple jobs from the same runbook or DSC configuration.</span></span>

- <span data-ttu-id="e11a3-110">Gestione di un valore dal portale o dalla riga di comando di Windows PowerShell usata da runbook o configurazioni DSC, ad esempio un set di elementi di configurazione comuni come un elenco specifico di nomi di VM, un gruppo di risorse specifico, un nome di dominio AD e così via.</span><span class="sxs-lookup"><span data-stu-id="e11a3-110">Manage a value from the portal or from the Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="e11a3-111">Le variabili di automazione vengono salvate in maniera permanente in modo da continuare a essere disponibili anche in caso di errore del runbook o della configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="e11a3-111">Automation variables are persisted so that they continue to be available even if the runbook or DSC configuration fails.</span></span>  <span data-ttu-id="e11a3-112">In tal modo, è anche possibile impostare in un runbook un valore che verrà quindi usato da un altro runbook oppure dallo stesso runbook o configurazione DSC alla successiva esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e11a3-112">This also allows a value to be set by one runbook that is then used by another, or is used by the same runbook or DSC configuration the next time that it is run.</span></span>

<span data-ttu-id="e11a3-113">Quando si crea una variabile, è possibile specificare che venga archiviata in modalità crittografata.</span><span class="sxs-lookup"><span data-stu-id="e11a3-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="e11a3-114">Se una variabile viene crittografata, viene archiviata in modo sicuro in Automazione di Azure e non è possibile recuperarne il valore con il cmdlet [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) incluso nel modulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e11a3-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from the [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of the Azure PowerShell module.</span></span>  <span data-ttu-id="e11a3-115">L'unico modo in cui è possibile recuperare un valore crittografato è dall'attività **Get-AutomationVariable** in un runbook o configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="e11a3-115">The only way that an encrypted value can be retrieved is from the **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="e11a3-116">Gli asset sicuri in Automazione di Azure includono credenziali, certificati, connessioni e variabili crittografate.</span><span class="sxs-lookup"><span data-stu-id="e11a3-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="e11a3-117">Questi asset vengono crittografati e archiviati in Automazione di Azure tramite una chiave univoca generata per ogni account di automazione.</span><span class="sxs-lookup"><span data-stu-id="e11a3-117">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="e11a3-118">La chiave viene crittografata da un certificato master e archiviata in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e11a3-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="e11a3-119">Prima dell'archiviazione di un asset sicuro, la chiave per l'account di automazione viene decrittografata mediante il certificato master e viene quindi usata per crittografare l'asset.</span><span class="sxs-lookup"><span data-stu-id="e11a3-119">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="e11a3-120">Tipi di variabile</span><span class="sxs-lookup"><span data-stu-id="e11a3-120">Variable types</span></span>

<span data-ttu-id="e11a3-121">Quando si crea una variabile con il portale di Azure, è necessario selezionare un tipo di dati nell'elenco a discesa, in modo che nel portale possa essere visualizzato il controllo appropriato per immettere il valore della variabile.</span><span class="sxs-lookup"><span data-stu-id="e11a3-121">When you create a variable with the Azure portal, you must specify a data type from the drop-down list so the portal can display the appropriate control for entering the variable value.</span></span> <span data-ttu-id="e11a3-122">La variabile non è limitata a questo tipo di dati, ma è necessario impostarla usando Windows PowerShell se si intende specificare un valore di tipo diverso.</span><span class="sxs-lookup"><span data-stu-id="e11a3-122">The variable is not restricted to this data type, but you must set the variable using Windows PowerShell if you want to specify a value of a different type.</span></span> <span data-ttu-id="e11a3-123">Se si specifica **Non definito**, il valore della variabile verrà impostato su **$null** e sarà necessario impostare il valore con il cmdlet [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) o l'attività **Set-AutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="e11a3-123">If you specify **Not defined**, then the value of the variable will be set to **$null**, and you must set the value with the [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="e11a3-124">Non è possibile creare o modificare il valore per un tipo di variabile complesso nel portale, ma è possibile indicare un valore di qualsiasi tipo usando Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e11a3-124">You cannot create or change the value for a complex variable type in the portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="e11a3-125">I tipi complessi verranno restituiti come [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="e11a3-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="e11a3-126">È possibile archiviare più valori in una singola variabile creando una matrice o una tabella hash e salvandola nella variabile.</span><span class="sxs-lookup"><span data-stu-id="e11a3-126">You can store multiple values to a single variable by creating an array or hashtable and saving it to the variable.</span></span>

<span data-ttu-id="e11a3-127">Di seguito è riportato un elenco dei tipi di variabile disponibili in Automazione:</span><span class="sxs-lookup"><span data-stu-id="e11a3-127">The following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="e11a3-128">String</span><span class="sxs-lookup"><span data-stu-id="e11a3-128">String</span></span>
* <span data-ttu-id="e11a3-129">Integer</span><span class="sxs-lookup"><span data-stu-id="e11a3-129">Integer</span></span>
* <span data-ttu-id="e11a3-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="e11a3-130">DateTime</span></span>
* <span data-ttu-id="e11a3-131">Boolean</span><span class="sxs-lookup"><span data-stu-id="e11a3-131">Boolean</span></span>
* <span data-ttu-id="e11a3-132">Null</span><span class="sxs-lookup"><span data-stu-id="e11a3-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="e11a3-133">Cmdlet e attività flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="e11a3-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="e11a3-134">I cmdlet della tabella seguente vengono usati per creare e gestire variabili di automazione con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e11a3-134">The cmdlets in the following table are used to create and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="e11a3-135">Sono inclusi nel [modulo Azure PowerShell](../powershell-install-configure.md) , disponibile per l'uso nei runbook di Automazione e nella configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="e11a3-135">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="e11a3-136">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="e11a3-136">Cmdlets</span></span>|<span data-ttu-id="e11a3-137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e11a3-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="e11a3-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="e11a3-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="e11a3-139">Recupera il valore di una variabile esistente.</span><span class="sxs-lookup"><span data-stu-id="e11a3-139">Retrieves the value of an existing variable.</span></span>|
|[<span data-ttu-id="e11a3-140">New-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="e11a3-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="e11a3-141">Crea una nuova variabile e ne imposta il valore.</span><span class="sxs-lookup"><span data-stu-id="e11a3-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="e11a3-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="e11a3-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="e11a3-143">Rimuove una variabile esistente.</span><span class="sxs-lookup"><span data-stu-id="e11a3-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="e11a3-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="e11a3-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="e11a3-145">Imposta il valore di una variabile esistente.</span><span class="sxs-lookup"><span data-stu-id="e11a3-145">Sets the value for an existing variable.</span></span>|

<span data-ttu-id="e11a3-146">Le attività flusso di lavoro incluse nella tabella seguente vengono usate per accedere alle variabili di automazione in un runbook.</span><span class="sxs-lookup"><span data-stu-id="e11a3-146">The workflow activities in the following table are used to access Automation variables in a runbook.</span></span> <span data-ttu-id="e11a3-147">Sono disponibili per l'uso solo in un runbook o configurazione DSC e non vengono fornite come parte del modulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e11a3-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of the Azure PowerShell module.</span></span>

|<span data-ttu-id="e11a3-148">Attività flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="e11a3-148">Workflow Activities</span></span>|<span data-ttu-id="e11a3-149">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e11a3-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="e11a3-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="e11a3-150">Get-AutomationVariable</span></span>|<span data-ttu-id="e11a3-151">Recupera il valore di una variabile esistente.</span><span class="sxs-lookup"><span data-stu-id="e11a3-151">Retrieves the value of an existing variable.</span></span>|
|<span data-ttu-id="e11a3-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="e11a3-152">Set-AutomationVariable</span></span>|<span data-ttu-id="e11a3-153">Imposta il valore di una variabile esistente.</span><span class="sxs-lookup"><span data-stu-id="e11a3-153">Sets the value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="e11a3-154">È consigliabile evitare di usare le variabili nel parametro –Name di **Get-AutomationVariable** in un runbook o una configurazione DSC perché ciò può complicare l'individuazione delle dipendenze tra i runbook o la configurazione DSC e le variabili di automazione in fase di progettazione.</span><span class="sxs-lookup"><span data-stu-id="e11a3-154">You should avoid using variables in the –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="e11a3-155">Creazione di una nuova variabile di automazione</span><span class="sxs-lookup"><span data-stu-id="e11a3-155">Creating a new Automation variable</span></span>

### <a name="to-create-a-new-variable-with-the-azure-portal"></a><span data-ttu-id="e11a3-156">Per creare una nuova variabile con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e11a3-156">To create a new variable with the Azure portal</span></span>

1. <span data-ttu-id="e11a3-157">Dall'account di automazione fare clic sul riquadro **Asset** e poi sul pannello **Asset** selezionare **Variabili**.</span><span class="sxs-lookup"><span data-stu-id="e11a3-157">From your Automation account, click the **Assets** tile and then on the **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="e11a3-158">Nel riquadro **Variabili** selezionare **Aggiungi variabile**.</span><span class="sxs-lookup"><span data-stu-id="e11a3-158">On the **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="e11a3-159">Completare le opzioni nel pannello **Nuova variabile**, fare clic su **Crea** e salvare la nuova variabile.</span><span class="sxs-lookup"><span data-stu-id="e11a3-159">Complete the options on the **New Variable** blade and click **Create** save the new variable.</span></span>

### <a name="to-create-a-new-variable-with-windows-powershell"></a><span data-ttu-id="e11a3-160">Per creare una nuova variabile con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e11a3-160">To create a new variable with Windows PowerShell</span></span>

<span data-ttu-id="e11a3-161">Il cmdlet [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) crea una nuova variabile e ne imposta il valore iniziale.</span><span class="sxs-lookup"><span data-stu-id="e11a3-161">The [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="e11a3-162">È possibile recuperare il valore usando [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="e11a3-162">You can retrieve the value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="e11a3-163">Se il valore è di tipo semplice, verrà restituito lo stesso tipo.</span><span class="sxs-lookup"><span data-stu-id="e11a3-163">If the value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="e11a3-164">Se è di tipo complesso, verrà restituito un **PSCustomObject** .</span><span class="sxs-lookup"><span data-stu-id="e11a3-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="e11a3-165">I comandi di esempio seguenti mostrano come creare una variabile di tipo stringa e restituirne il valore.</span><span class="sxs-lookup"><span data-stu-id="e11a3-165">The following sample commands show how to create a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="e11a3-166">I comandi di esempio seguenti mostrano come creare una variabile di tipo complesso e restituirne le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="e11a3-166">The following sample commands show how to create a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="e11a3-167">In questo caso, viene usato un oggetto macchina virtuale recuperato da **Get-AzureRmVm**.</span><span class="sxs-lookup"><span data-stu-id="e11a3-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="e11a3-168">Uso di una variabile in un Runbook o in una configurazione DSC</span><span class="sxs-lookup"><span data-stu-id="e11a3-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="e11a3-169">Usare l'attività **Set-AutomationVariable** per impostare il valore di una variabile di automazione in un runbook o una configurazione DSC e **Get-AutomationVariable** per recuperarlo.</span><span class="sxs-lookup"><span data-stu-id="e11a3-169">Use the **Set-AutomationVariable** activity to set the value of an Automation variable in a runbook or DSC configuration, and the **Get-AutomationVariable** to retrieve it.</span></span>  <span data-ttu-id="e11a3-170">Non è consigliabile usare i cmdlet **Set-AzureAutomationVariable** o **Get-AzureAutomationVariable** in un runbook o una configurazione DSC perché sono meno efficienti rispetto alle attività flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e11a3-170">You shouldn't use the **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than the workflow activities.</span></span>  <span data-ttu-id="e11a3-171">Non è inoltre possibile recuperare il valore delle variabili sicure con **Get-AzureAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="e11a3-171">You also cannot retrieve the value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="e11a3-172">L'unico modo per creare una nuova variabile dall'interno di un runbook o una configurazione DSC consiste nell'usare il cmdlet [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx).</span><span class="sxs-lookup"><span data-stu-id="e11a3-172">The only way to create a new variable from within a runbook or DSC configuration is to use the [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="e11a3-173">Esempi di runbook testuali</span><span class="sxs-lookup"><span data-stu-id="e11a3-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="e11a3-174">Impostazione e recupero di un valore semplice da una variabile</span><span class="sxs-lookup"><span data-stu-id="e11a3-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="e11a3-175">I comandi di esempio seguenti mostrano come impostare e recuperare una variabile in un runbook testuale.</span><span class="sxs-lookup"><span data-stu-id="e11a3-175">The following sample commands show how to set and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="e11a3-176">In questo esempio si presuppone che siano già state create variabili di tipo integer denominate *NumberOfIterations* e *NumberOfRunnings* e una variabile di tipo stringa denominata *SampleMessage*.</span><span class="sxs-lookup"><span data-stu-id="e11a3-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="e11a3-177">Impostazione e recupero di un oggetto complesso in una variabile</span><span class="sxs-lookup"><span data-stu-id="e11a3-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="e11a3-178">Il codice di esempio seguente mostra come aggiornare una variabile con un valore complesso in un runbook testuale.</span><span class="sxs-lookup"><span data-stu-id="e11a3-178">The following sample code shows how to update a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="e11a3-179">In questo esempio una macchina virtuale di Azure viene recuperata con **Get-AzureVM** e salvata in una variabile di automazione esistente.</span><span class="sxs-lookup"><span data-stu-id="e11a3-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="e11a3-180">Come illustrato in [Tipi di variabile](#variable-types), viene archiviata come PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="e11a3-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="e11a3-181">Nel codice seguente il valore viene recuperato dalla variabile e usato per avviare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e11a3-181">In the following code, the value is retrieved from the variable and used to start the virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="e11a3-182">Impostazione e recupero di una raccolta in una variabile</span><span class="sxs-lookup"><span data-stu-id="e11a3-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="e11a3-183">Il codice di esempio seguente mostra come usare una variabile con una raccolta di valori complessi in un runbook testuale.</span><span class="sxs-lookup"><span data-stu-id="e11a3-183">The following sample code shows how to use a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="e11a3-184">In questo esempio più macchine virtuali di Azure vengono recuperate con **Get-AzureVM** e salvate in una variabile di automazione esistente.</span><span class="sxs-lookup"><span data-stu-id="e11a3-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="e11a3-185">Come illustrato in [Tipi di variabile](#variable-types), viene archiviata una raccolta di PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="e11a3-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="e11a3-186">Nel codice seguente la raccolta viene recuperata dalla variabile e usata per avviare ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e11a3-186">In the following code, the collection is retrieved from the variable and used to start each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="e11a3-187">Esempi di runbook grafici</span><span class="sxs-lookup"><span data-stu-id="e11a3-187">Graphical runbook samples</span></span>

<span data-ttu-id="e11a3-188">In un runbook grafico è possibile aggiungere **Get-AutomationVariable** o **Set-AutomationVariable** facendo clic con il pulsante destro del mouse sulla variabile nel riquadro della libreria dell'editor grafico e scegliendo l'attività desiderata.</span><span class="sxs-lookup"><span data-stu-id="e11a3-188">In a graphical runbook, you add the **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on the variable in the Library pane of the graphical editor and selecting the activity you want.</span></span>

![Aggiungere una variabile al canvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="e11a3-190">Impostazione dei valori in una variabile</span><span class="sxs-lookup"><span data-stu-id="e11a3-190">Setting values in a variable</span></span>
<span data-ttu-id="e11a3-191">La figura seguente illustra attività di esempio per aggiornare una variabile con un valore semplice in un runbook grafico.</span><span class="sxs-lookup"><span data-stu-id="e11a3-191">The following image shows sample activities to update a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="e11a3-192">In questo esempio viene recuperata una singola macchina virtuale di Azure con **Get-AzureRmVM** e il nome computer viene salvato in una variabile di automazione esistente di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="e11a3-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and the computer name is saved to an existing Automation variable with a type of String.</span></span>  <span data-ttu-id="e11a3-193">Non è importante se il [collegamento è una pipeline o una sequenza](automation-graphical-authoring-intro.md#links-and-workflow) poiché è previsto solo un singolo oggetto nell'output.</span><span class="sxs-lookup"><span data-stu-id="e11a3-193">It doesn't matter whether the [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in the output.</span></span>

![Impostare una variabile semplice](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="e11a3-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e11a3-195">Next Steps</span></span>

* <span data-ttu-id="e11a3-196">Per altre informazioni su come collegare attività nella creazione grafica, vedere [Creazione grafica in Automazione di Azure](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="e11a3-196">To learn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="e11a3-197">Per iniziare a usare runbook grafici, vedere [Il primo runbook grafico](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="e11a3-197">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

