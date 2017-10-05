---
title: Parametri di input dei runbook| Documentazione Microsoft
description: "I parametri di input dei runbook ne aumentano la flessibilità perché consentono di passare dati a un runbook al momento dell'avvio. Questo articolo descrive vari scenari in cui i parametri di input vengono usati nei runbook."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: 1ebf32338f5242e72eb2e2daa2da50d231f4b683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="1e74f-104">Parametri di input dei runbook</span><span class="sxs-lookup"><span data-stu-id="1e74f-104">Runbook input parameters</span></span>
<span data-ttu-id="1e74f-105">I parametri di input dei runbook ne aumentano la flessibilità perché consentono di passare dati a un runbook al momento dell'avvio.</span><span class="sxs-lookup"><span data-stu-id="1e74f-105">Runbook input parameters increase the flexibility of runbooks by allowing you to pass data to it when it is started.</span></span> <span data-ttu-id="1e74f-106">I parametri consentono di eseguire azioni runbook mirate per ambienti e scenari specifici.</span><span class="sxs-lookup"><span data-stu-id="1e74f-106">The parameters allow the runbook actions to be targeted for specific scenarios and environments.</span></span> <span data-ttu-id="1e74f-107">Questo articolo illustra vari scenari in cui i parametri di input vengono usati nei runbook.</span><span class="sxs-lookup"><span data-stu-id="1e74f-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="1e74f-108">Configurare i parametri di input</span><span class="sxs-lookup"><span data-stu-id="1e74f-108">Configure input parameters</span></span>
<span data-ttu-id="1e74f-109">È possibile configurare i parametri di input nei runbook grafici e in quelli di PowerShell e del flusso di lavoro PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e74f-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="1e74f-110">Un runbook può avere più parametri con tipi di dati diversi oppure non avere parametri.</span><span class="sxs-lookup"><span data-stu-id="1e74f-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="1e74f-111">I parametri di input possono essere obbligatori o facoltativi ed è possibile assegnare un valore predefinito per i parametri facoltativi.</span><span class="sxs-lookup"><span data-stu-id="1e74f-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="1e74f-112">È possibile assegnare valori ai parametri di input per un runbook quando viene avviato tramite uno dei metodi disponibili.</span><span class="sxs-lookup"><span data-stu-id="1e74f-112">You can assign values to the input parameters for a runbook when you start it through one of the available methods.</span></span> <span data-ttu-id="1e74f-113">Questi metodi includono l'avvio di un runbook dal portale o da un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="1e74f-113">These methods include starting  a runbook from the portal  or a web service.</span></span> <span data-ttu-id="1e74f-114">È inoltre possibile avviare un runbook come figlio, definito inline in un altro runbook.</span><span class="sxs-lookup"><span data-stu-id="1e74f-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="1e74f-115">Configurare i parametri di input nei runbook di PowerShell e nei runbook del flusso di lavoro PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e74f-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="1e74f-116">I [runbook del flusso di lavoro PowerShell](automation-first-runbook-textual.md) e i runbook di PowerShell in Automazione di Azure supportano parametri di input definiti tramite gli attributi seguenti.</span><span class="sxs-lookup"><span data-stu-id="1e74f-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through the following attributes.</span></span>  

| <span data-ttu-id="1e74f-117">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="1e74f-117">**Property**</span></span> | <span data-ttu-id="1e74f-118">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="1e74f-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="1e74f-119">Type</span><span class="sxs-lookup"><span data-stu-id="1e74f-119">Type</span></span> |<span data-ttu-id="1e74f-120">Obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="1e74f-120">Required.</span></span> <span data-ttu-id="1e74f-121">Tipo di dati previsto per il valore del parametro.</span><span class="sxs-lookup"><span data-stu-id="1e74f-121">The data type expected for the parameter value.</span></span> <span data-ttu-id="1e74f-122">Qualsiasi tipo .NET è valido.</span><span class="sxs-lookup"><span data-stu-id="1e74f-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="1e74f-123">Nome</span><span class="sxs-lookup"><span data-stu-id="1e74f-123">Name</span></span> |<span data-ttu-id="1e74f-124">Obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="1e74f-124">Required.</span></span> <span data-ttu-id="1e74f-125">Nome del parametro.</span><span class="sxs-lookup"><span data-stu-id="1e74f-125">The name of the parameter.</span></span> <span data-ttu-id="1e74f-126">Questo valore deve essere univoco all'interno del runbook e può contenere solo lettere, numeri o caratteri di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="1e74f-126">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="1e74f-127">Deve iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="1e74f-127">It must start with a letter.</span></span> |
| <span data-ttu-id="1e74f-128">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1e74f-128">Mandatory</span></span> |<span data-ttu-id="1e74f-129">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="1e74f-129">Optional.</span></span> <span data-ttu-id="1e74f-130">Specifica se è necessario specificare un valore per il parametro.</span><span class="sxs-lookup"><span data-stu-id="1e74f-130">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="1e74f-131">Se la proprietà è impostata su **$true**, è necessario specificare un valore quando viene avviato il runbook.</span><span class="sxs-lookup"><span data-stu-id="1e74f-131">If you set this to **$true**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="1e74f-132">Se la proprietà è impostata su **$false**, il valore è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1e74f-132">If you set this to **$false**, then a value is optional.</span></span> |
| <span data-ttu-id="1e74f-133">Default value</span><span class="sxs-lookup"><span data-stu-id="1e74f-133">Default value</span></span> |<span data-ttu-id="1e74f-134">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="1e74f-134">Optional.</span></span>  <span data-ttu-id="1e74f-135">Specifica un valore che verrà usato per il parametro se non viene passato un valore all'avvio del runbook.</span><span class="sxs-lookup"><span data-stu-id="1e74f-135">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="1e74f-136">È possibile impostare un valore predefinito per qualsiasi parametro, rendendolo automaticamente facoltativo indipendentemente dall'impostazione della proprietà Mandatory.</span><span class="sxs-lookup"><span data-stu-id="1e74f-136">A default value can be set for any parameter and will automatically make the parameter optional regardless of the Mandatory setting.</span></span> |

<span data-ttu-id="1e74f-137">Windows PowerShell supporta più attributi dei parametri di input di quelli elencati di seguito, ad esempio la convalida, gli alias e i set di parametri.</span><span class="sxs-lookup"><span data-stu-id="1e74f-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="1e74f-138">Tuttavia, Automazione di Azure attualmente supporta solo i parametri di input sopra elencati.</span><span class="sxs-lookup"><span data-stu-id="1e74f-138">However, Azure Automation currently supports only the input parameters listed above.</span></span>

<span data-ttu-id="1e74f-139">Una definizione di parametri nei runbook del flusso di lavoro PowerShell ha il formato generale seguente, in cui più parametri sono separati da virgole.</span><span class="sxs-lookup"><span data-stu-id="1e74f-139">A parameter definition in PowerShell Workflow runbooks has the following general form, where multiple parameters are separated by commas.</span></span>

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> <span data-ttu-id="1e74f-140">Quando si definiscono i parametri, se non si specifica l'attributo **Mandatory** , il parametro è considerato facoltativo per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1e74f-140">When you're defining parameters, if you don’t specify the **Mandatory** attribute, then by default, the parameter is considered optional.</span></span> <span data-ttu-id="1e74f-141">Se si imposta un valore predefinito per un parametro nei runbook del flusso di lavoro PowerShell, il parametro verrà considerato come facoltativo da PowerShell, indipendentemente dal valore dell'attributo **Mandatory**.</span><span class="sxs-lookup"><span data-stu-id="1e74f-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of the **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="1e74f-142">Come esempio, di seguito vengono configurati i parametri di input per un runbook del flusso di lavoro PowerShell che restituisce informazioni dettagliate su macchine virtuali, che si tratti di una singola VM o di tutte le VM all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1e74f-142">As an example, let’s configure the input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="1e74f-143">Questo runbook ha due parametri, come illustrato nella schermata seguente: il nome della macchina virtuale e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1e74f-143">This runbook has two parameters as shown in the following screenshot: the name of virtual machine and the name of the resource group.</span></span>

![Flusso di lavoro PowerShell di Automazione](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="1e74f-145">In questa definizione di parametro i parametri **$VMName** e **$resourceGroupName** sono semplici parametri di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="1e74f-145">In this parameter definition, the parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="1e74f-146">I runbook di PowerShell e del flusso di lavoro PowerShell supportano tuttavia tutti i tipi semplici e complessi, ad esempio **object** o **PSCredential** per i parametri di input.</span><span class="sxs-lookup"><span data-stu-id="1e74f-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="1e74f-147">Se il runbook include un parametro di input di tipo object, per passare un valore è necessario usare una tabella hash di PowerShell con coppie (nome/valore).</span><span class="sxs-lookup"><span data-stu-id="1e74f-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs to pass in a value.</span></span> <span data-ttu-id="1e74f-148">Ad esempio, se si ha questo parametro in un runbook:</span><span class="sxs-lookup"><span data-stu-id="1e74f-148">For example, if you have the following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="1e74f-149">è possibile passare il valore seguente al parametro:</span><span class="sxs-lookup"><span data-stu-id="1e74f-149">Then you can pass the following value to the parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="1e74f-150">Configurare i parametri di input in runbook grafici</span><span class="sxs-lookup"><span data-stu-id="1e74f-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="1e74f-151">Per [configurare un runbook grafico](automation-first-runbook-graphical.md) con parametri di input, verrà creato un runbook grafico che restituisce informazioni dettagliate su macchine virtuali, che si tratti di una singola macchina virtuale o di tutte le macchine virtuali all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1e74f-151">To [configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="1e74f-152">La configurazione di un runbook è costituita da due attività principali, come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="1e74f-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="1e74f-153">[**Autenticare runbook con account RunAs di Azure**](automation-sec-configure-azure-runas-account.md) per l'autenticazione con Azure.</span><span class="sxs-lookup"><span data-stu-id="1e74f-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) to authenticate with Azure.</span></span>

<span data-ttu-id="1e74f-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) per leggere le proprietà di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1e74f-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) to get the properties of a virtual machines.</span></span>

<span data-ttu-id="1e74f-155">È possibile usare l'attività [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) per restituire i nomi delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1e74f-155">You can use the [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity to output the names of virtual machines.</span></span> <span data-ttu-id="1e74f-156">L'attività **Get-AzureRmVm** accetta due parametri: il **nome della macchina virtuale** and the **nome del gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="1e74f-156">The activity **Get-AzureRmVm** accepts two parameters, the **virtual machine name** and the **resource group name**.</span></span> <span data-ttu-id="1e74f-157">Dal momento che questi parametri potrebbero richiedere valori diversi ogni volta che si avvia il runbook, è possibile aggiungere parametri di input al runbook.</span><span class="sxs-lookup"><span data-stu-id="1e74f-157">Since these parameters could require different values each time you start the runbook, you can add input parameters to your runbook.</span></span> <span data-ttu-id="1e74f-158">Per aggiungere parametri di input, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1e74f-158">Here are the steps to add input parameters:</span></span>

1. <span data-ttu-id="1e74f-159">Selezionare il runbook grafico nel pannello **Runbook** e fare clic su [**Modifica**](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="1e74f-159">Select the graphical runbook from the **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="1e74f-160">Nell'editor dei runbook fare clic su **Input e output** per aprire il pannello **Input e output**.</span><span class="sxs-lookup"><span data-stu-id="1e74f-160">From the runbook editor, click **Input and output** to open the **Input and output** blade.</span></span>
   
    ![Runbook grafico di Automazione](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="1e74f-162">Il pannello **Input e output** mostra un elenco di parametri di input definiti per il runbook.</span><span class="sxs-lookup"><span data-stu-id="1e74f-162">The **Input and output** blade displays a list of input parameters that are defined for the runbook.</span></span> <span data-ttu-id="1e74f-163">In questo pannello è possibile aggiungere un nuovo parametro di input o modificare la configurazione di un parametro di input esistente.</span><span class="sxs-lookup"><span data-stu-id="1e74f-163">On this blade, you can either add a new input parameter or edit the configuration of an existing input parameter.</span></span> <span data-ttu-id="1e74f-164">Per aggiungere un nuovo parametro per il runbook, fare clic su **Aggiungi input** per aprire il pannello **Parametro di input runbook**,</span><span class="sxs-lookup"><span data-stu-id="1e74f-164">To add a new parameter for the runbook, click **Add input** to open the **Runbook input parameter** blade.</span></span> <span data-ttu-id="1e74f-165">in cui è possibile configurare i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="1e74f-165">There, you can configure the following parameters:</span></span>
   
   | <span data-ttu-id="1e74f-166">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="1e74f-166">**Property**</span></span> | <span data-ttu-id="1e74f-167">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="1e74f-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="1e74f-168">Nome</span><span class="sxs-lookup"><span data-stu-id="1e74f-168">Name</span></span> |<span data-ttu-id="1e74f-169">Obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="1e74f-169">Required.</span></span>  <span data-ttu-id="1e74f-170">Nome del parametro.</span><span class="sxs-lookup"><span data-stu-id="1e74f-170">The name of the parameter.</span></span> <span data-ttu-id="1e74f-171">Questo valore deve essere univoco all'interno del runbook e può contenere solo lettere, numeri o caratteri di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="1e74f-171">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="1e74f-172">Deve iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="1e74f-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="1e74f-173">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1e74f-173">Description</span></span> |<span data-ttu-id="1e74f-174">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="1e74f-174">Optional.</span></span> <span data-ttu-id="1e74f-175">Descrizione dello scopo del parametro di input.</span><span class="sxs-lookup"><span data-stu-id="1e74f-175">Description about the purpose of input parameter.</span></span> |
   | <span data-ttu-id="1e74f-176">Type</span><span class="sxs-lookup"><span data-stu-id="1e74f-176">Type</span></span> |<span data-ttu-id="1e74f-177">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="1e74f-177">Optional.</span></span> <span data-ttu-id="1e74f-178">Tipo di dati previsto per il valore del parametro.</span><span class="sxs-lookup"><span data-stu-id="1e74f-178">The data type that's expected for the parameter value.</span></span> <span data-ttu-id="1e74f-179">I tipi di parametro supportati sono **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime** e **Object**.</span><span class="sxs-lookup"><span data-stu-id="1e74f-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="1e74f-180">Se non è selezionato un tipo di dati, l'impostazione predefinita è **String**.</span><span class="sxs-lookup"><span data-stu-id="1e74f-180">If a data type is not selected, it defaults to **String**.</span></span> |
   | <span data-ttu-id="1e74f-181">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1e74f-181">Mandatory</span></span> |<span data-ttu-id="1e74f-182">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="1e74f-182">Optional.</span></span> <span data-ttu-id="1e74f-183">Specifica se è necessario specificare un valore per il parametro.</span><span class="sxs-lookup"><span data-stu-id="1e74f-183">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="1e74f-184">Se si sceglie **Sì**, è necessario specificare un valore quando viene avviato il runbook.</span><span class="sxs-lookup"><span data-stu-id="1e74f-184">If you choose **yes**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="1e74f-185">Se si sceglie **No**, non è necessario specificare un valore all'avvio del runbook ed è possibile impostare un valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="1e74f-185">If you choose **no**, then a value is not required when the runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="1e74f-186">Default value</span><span class="sxs-lookup"><span data-stu-id="1e74f-186">Default Value</span></span> |<span data-ttu-id="1e74f-187">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="1e74f-187">Optional.</span></span> <span data-ttu-id="1e74f-188">Specifica un valore che verrà usato per il parametro se non viene passato un valore all'avvio del runbook.</span><span class="sxs-lookup"><span data-stu-id="1e74f-188">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="1e74f-189">È possibile impostare un valore predefinito per un parametro non obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1e74f-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="1e74f-190">Per impostare un valore predefinito, scegliere **Personalizzato**.</span><span class="sxs-lookup"><span data-stu-id="1e74f-190">To set a default value, choose **Custom**.</span></span> <span data-ttu-id="1e74f-191">Questo valore viene usato a meno che non venga specificato un altro valore all'avvio del runbook.</span><span class="sxs-lookup"><span data-stu-id="1e74f-191">This value is used unless another value is provided when the runbook is started.</span></span> <span data-ttu-id="1e74f-192">Scegliere **Nessuno** se non si vuole specificare alcun valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="1e74f-192">Choose **None** if you don’t want to provide any default value.</span></span> |
   
    ![Aggiunta di nuovo input](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="1e74f-194">Creare due parametri con le proprietà seguenti che verranno usate dall'attività **Get-AzureRmVm**:</span><span class="sxs-lookup"><span data-stu-id="1e74f-194">Create two parameters with the following properties that will be used by the **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="1e74f-195">**Parametro 1:**</span><span class="sxs-lookup"><span data-stu-id="1e74f-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="1e74f-196">Nome: VMName</span><span class="sxs-lookup"><span data-stu-id="1e74f-196">Name - VMName</span></span>
     * <span data-ttu-id="1e74f-197">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="1e74f-197">Type - String</span></span>
     * <span data-ttu-id="1e74f-198">Obbligatorio: no</span><span class="sxs-lookup"><span data-stu-id="1e74f-198">Mandatory - No</span></span>
   * <span data-ttu-id="1e74f-199">**Parametro2:**</span><span class="sxs-lookup"><span data-stu-id="1e74f-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="1e74f-200">Nome: resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="1e74f-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="1e74f-201">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="1e74f-201">Type - String</span></span>
     * <span data-ttu-id="1e74f-202">Obbligatorio: no</span><span class="sxs-lookup"><span data-stu-id="1e74f-202">Mandatory - No</span></span>
     * <span data-ttu-id="1e74f-203">Valore predefinito: personalizzato</span><span class="sxs-lookup"><span data-stu-id="1e74f-203">Default value - Custom</span></span>
     * <span data-ttu-id="1e74f-204">Valore predefinito personalizzato: \< nome del gruppo di risorse che contiene le macchine virtuali>.</span><span class="sxs-lookup"><span data-stu-id="1e74f-204">Custom default value - \<Name of the resource group that contains the virtual machines></span></span>
5. <span data-ttu-id="1e74f-205">Dopo aver aggiunto i parametri, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1e74f-205">Once you add the parameters, click **OK**.</span></span>  <span data-ttu-id="1e74f-206">Ora è possibile visualizzarli nel pannello **Input e output**.</span><span class="sxs-lookup"><span data-stu-id="1e74f-206">You can now view them in the **Input and output blade**.</span></span> <span data-ttu-id="1e74f-207">Fare nuovamente clic su **OK**, quindi su **Salva** e **pubblicare** il runbook.</span><span class="sxs-lookup"><span data-stu-id="1e74f-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-to-input-parameters-in-runbooks"></a><span data-ttu-id="1e74f-208">Assegnare valori ai parametri di input nei runbook</span><span class="sxs-lookup"><span data-stu-id="1e74f-208">Assign values to input parameters in runbooks</span></span>
<span data-ttu-id="1e74f-209">È possibile passare valori ai parametri di input nei runbook negli scenari illustrati di seguito.</span><span class="sxs-lookup"><span data-stu-id="1e74f-209">You can pass values to input parameters in runbooks in the following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="1e74f-210">Avviare un runbook e assegnare parametri</span><span class="sxs-lookup"><span data-stu-id="1e74f-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="1e74f-211">Ci sono diversi modi per avviare un runbook: dal portale di Azure, con un webhook, con i cmdlet di PowerShell, con l'API REST o con l'SDK.</span><span class="sxs-lookup"><span data-stu-id="1e74f-211">A runbook can be started many ways: through the Azure portal, with a webhook, with PowerShell cmdlets, with the REST API, or with the SDK.</span></span> <span data-ttu-id="1e74f-212">Di seguito vengono illustrati vari metodi per avviare un runbook e assegnare parametri.</span><span class="sxs-lookup"><span data-stu-id="1e74f-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-the-azure-portal-and-assign-parameters"></a><span data-ttu-id="1e74f-213">Avviare un runbook pubblicato usando il portale di Azure e assegnare parametri</span><span class="sxs-lookup"><span data-stu-id="1e74f-213">Start a published runbook by using the Azure portal and assign parameters</span></span>
<span data-ttu-id="1e74f-214">Quando si [avvia il runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), viene aperto il pannello **Avvia runbook** ed è possibile configurare i valori per i parametri appena creati.</span><span class="sxs-lookup"><span data-stu-id="1e74f-214">When you [start the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), the **Start Runbook** blade opens and you can configure values for the parameters that you just created.</span></span>

![Attività iniziali con il portale](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="1e74f-216">Nell'etichetta sotto la casella di input è possibile visualizzare gli attributi impostati per il parametro.</span><span class="sxs-lookup"><span data-stu-id="1e74f-216">In the label beneath the input box, you can see the attributes that have been set for the parameter.</span></span> <span data-ttu-id="1e74f-217">Gli attributi includono obbligatorio o facoltativo, tipo e valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="1e74f-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="1e74f-218">Nel fumetto della Guida accanto al nome del parametro sono disponibili tutte le informazioni chiave necessarie per scegliere i valori dei parametri di input,</span><span class="sxs-lookup"><span data-stu-id="1e74f-218">In the help balloon next to the parameter name, you can see all the key information you need to make decisions about parameter input values.</span></span> <span data-ttu-id="1e74f-219">Queste informazioni indicano se un parametro è obbligatorio o facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1e74f-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="1e74f-220">Includono inoltre il tipo e il valore predefinito (se presente) e altre note utili.</span><span class="sxs-lookup"><span data-stu-id="1e74f-220">It also includes the type and default value (if any), and other helpful notes.</span></span>

![Fumetto della Guida](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="1e74f-222">I parametri di tipo String supportano valori di stringa **vuoti** .</span><span class="sxs-lookup"><span data-stu-id="1e74f-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="1e74f-223">Immettendo **[EmptyString]** nella casella del parametro di input viene passata una stringa vuota al parametro.</span><span class="sxs-lookup"><span data-stu-id="1e74f-223">Entering **[EmptyString]** in the input parameter box will pass an empty string to the parameter.</span></span> <span data-ttu-id="1e74f-224">I parametri di tipo String non supportano il passaggio di valori **Null** .</span><span class="sxs-lookup"><span data-stu-id="1e74f-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="1e74f-225">Se non viene passato alcun valore al parametro String, PowerShell lo interpreterà come Null.</span><span class="sxs-lookup"><span data-stu-id="1e74f-225">If you don’t pass any value to the String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="1e74f-226">Avviare un runbook pubblicato usando i cmdlet di PowerShell e assegnare parametri</span><span class="sxs-lookup"><span data-stu-id="1e74f-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="1e74f-227">**Cmdlet di Azure Resource Manager:** è possibile avviare un runbook di Automazione creato in un gruppo di risorse usando [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e74f-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="1e74f-228">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="1e74f-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="1e74f-229">**Cmdlet di Gestione dei servizi di Azure:** è possibile avviare un runbook di automazione creato in un gruppo di risorse predefinito usando [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e74f-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="1e74f-230">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="1e74f-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="1e74f-231">Quando si avvia un runbook con i cmdlet di PowerShell viene creato un parametro predefinito, **MicrosoftApplicationManagementStartedBy**, con il valore **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="1e74f-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with the value **PowerShell**.</span></span> <span data-ttu-id="1e74f-232">Questo parametro può essere visualizzato nel pannello **Dettagli processo** .</span><span class="sxs-lookup"><span data-stu-id="1e74f-232">You can view this parameter in the **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="1e74f-233">Avviare un runbook usando un SDK e assegnare parametri</span><span class="sxs-lookup"><span data-stu-id="1e74f-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="1e74f-234">**Metodo di Azure Resource Manager:** è possibile avviare un runbook usando l'SDK di un linguaggio di programmazione.</span><span class="sxs-lookup"><span data-stu-id="1e74f-234">**Azure Resource Manager method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="1e74f-235">Di seguito è riportato un frammento di codice C# per l'avvio di un runbook nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="1e74f-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="1e74f-236">È possibile visualizzare tutto il codice nel [repository GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="1e74f-236">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* <span data-ttu-id="1e74f-237">**Metodo di gestione del servizio Azure:** è possibile avviare un runbook usando l'SDK di un linguaggio di programmazione.</span><span class="sxs-lookup"><span data-stu-id="1e74f-237">**Azure Service Management method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="1e74f-238">Di seguito è riportato un frammento di codice C# per l'avvio di un runbook nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="1e74f-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="1e74f-239">È possibile visualizzare tutto il codice nel [repository GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="1e74f-239">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  <span data-ttu-id="1e74f-240">Per avviare questo metodo, creare un dizionario per archiviare i parametri del runbook, **VMName** e **resourceGroupName**, e i relativi valori.</span><span class="sxs-lookup"><span data-stu-id="1e74f-240">To start this method, create a dictionary to store the runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="1e74f-241">Avviare quindi il runbook.</span><span class="sxs-lookup"><span data-stu-id="1e74f-241">Then start the runbook.</span></span> <span data-ttu-id="1e74f-242">Di seguito è riportato un frammento di codice C# per chiamare il metodo definito in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1e74f-242">Below is the C# code snippet for calling the method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters to the dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call the StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-the-rest-api-and-assign-parameters"></a><span data-ttu-id="1e74f-243">Avviare un runbook usando l'API REST e assegnare parametri</span><span class="sxs-lookup"><span data-stu-id="1e74f-243">Start a runbook by using the REST API and assign parameters</span></span>
<span data-ttu-id="1e74f-244">È possibile creare e avviare un processo del runbook con l'API REST di Automazione di Azure usando il metodo **PUT** con l'URI della richiesta seguente.</span><span class="sxs-lookup"><span data-stu-id="1e74f-244">A runbook job can be created and started with the Azure Automation REST API by using the **PUT** method with the following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="1e74f-245">Nell'URI della richiesta sostituire i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="1e74f-245">In the request URI, replace the following parameters:</span></span>

* <span data-ttu-id="1e74f-246">**subscription-id:** ID della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e74f-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="1e74f-247">**cloud-service-name:** nome del servizio cloud a cui deve essere inviata la richiesta.</span><span class="sxs-lookup"><span data-stu-id="1e74f-247">**cloud-service-name:** The name of the cloud service to which the request should be sent.</span></span>  
* <span data-ttu-id="1e74f-248">**automation-account-name:** nome dell'account di Automazione ospitato nel servizio cloud specificato.</span><span class="sxs-lookup"><span data-stu-id="1e74f-248">**automation-account-name:** The name of your automation account that's hosted within the specified cloud service.</span></span>  
* <span data-ttu-id="1e74f-249">**job-id:** GUID del processo.</span><span class="sxs-lookup"><span data-stu-id="1e74f-249">**job-id:** The GUID for the job.</span></span> <span data-ttu-id="1e74f-250">Per creare GUID in PowerShell è possibile usare il comando **[GUID]::NewGuid().ToString()** .</span><span class="sxs-lookup"><span data-stu-id="1e74f-250">GUIDs in PowerShell can be created by using the **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="1e74f-251">Per passare parametri al processo del runbook, usare il corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="1e74f-251">In order to pass parameters to the runbook job, use the request body.</span></span> <span data-ttu-id="1e74f-252">Vengono usate le due proprietà seguenti, specificate in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="1e74f-252">It takes the following two properties provided in JSON format:</span></span>

* <span data-ttu-id="1e74f-253">**Nome del runbook:** obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1e74f-253">**Runbook name:** Required.</span></span> <span data-ttu-id="1e74f-254">Nome del runbook per il processo da avviare.</span><span class="sxs-lookup"><span data-stu-id="1e74f-254">The name of the runbook for the job to start.</span></span>  
* <span data-ttu-id="1e74f-255">**Parametri del runbook:** facoltativi.</span><span class="sxs-lookup"><span data-stu-id="1e74f-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="1e74f-256">Dizionario dell'elenco dei parametri in formato (nome, valore) in cui il nome deve essere di tipo String e il valore può essere qualsiasi valore JSON valido.</span><span class="sxs-lookup"><span data-stu-id="1e74f-256">A dictionary of the parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="1e74f-257">Per avviare il runbook **Get-AzureVMTextual** creato in precedenza con **VMName** e **resourceGroupName** come parametri, usare il formato JSON seguente per il corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="1e74f-257">If you want to start the **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use the following JSON format for the request body.</span></span>

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

<span data-ttu-id="1e74f-258">Se il processo è stato creato, viene restituito un codice di stato HTTP 201.</span><span class="sxs-lookup"><span data-stu-id="1e74f-258">A HTTP status code 201 is returned if the job is successfully created.</span></span> <span data-ttu-id="1e74f-259">Per altre informazioni su intestazioni di risposta e sul corpo della risposta, vedere l'articolo relativo alla [creazione di un processo del runbook tramite l'API REST.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="1e74f-259">For more information on response headers and the response body, refer to the article about how to [create a runbook job by using the REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="1e74f-260">Eseguire il test di un runbook e assegnare parametri</span><span class="sxs-lookup"><span data-stu-id="1e74f-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="1e74f-261">Quando si esegue il [test della versione bozza del runbook](automation-testing-runbook.md) con l'opzione di test, viene visualizzato il pannello **Test** in cui è possibile configurare i valori per i parametri appena creati.</span><span class="sxs-lookup"><span data-stu-id="1e74f-261">When you [test the draft version of your runbook](automation-testing-runbook.md) by using the test option, the **Test** blade opens and you can configure values for the parameters that you just created.</span></span>

![Esecuzione di test e assegnazione di parametri](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-to-a-runbook-and-assign-parameters"></a><span data-ttu-id="1e74f-263">Collegare una pianificazione a un runbook e assegnare parametri</span><span class="sxs-lookup"><span data-stu-id="1e74f-263">Link a schedule to a runbook and assign parameters</span></span>
<span data-ttu-id="1e74f-264">È possibile [collegare una pianificazione](automation-schedules.md) al runbook in modo che venga avviato in un momento specifico.</span><span class="sxs-lookup"><span data-stu-id="1e74f-264">You can [link a schedule](automation-schedules.md) to your runbook so that the runbook starts at a specific time.</span></span> <span data-ttu-id="1e74f-265">Assegnare i parametri di input durante la creazione della pianificazione. Il runbook usa questi valori quando viene avviato dalla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="1e74f-265">You assign input parameters when you create the schedule, and the runbook will use these values when it is started by the schedule.</span></span> <span data-ttu-id="1e74f-266">Fino a quando non vengono forniti tutti i valori dei parametri obbligatori non è possibile salvare la pianificazione.</span><span class="sxs-lookup"><span data-stu-id="1e74f-266">You can’t save the schedule until all mandatory parameter values are provided.</span></span>

![Pianificazione e assegnazione di parametri](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="1e74f-268">Creare un webhook per un runbook e assegnare parametri</span><span class="sxs-lookup"><span data-stu-id="1e74f-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="1e74f-269">È possibile creare un [webhook](automation-webhooks.md) per il runbook e configurare i parametri di input del runbook.</span><span class="sxs-lookup"><span data-stu-id="1e74f-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="1e74f-270">Fino a quando non vengono forniti tutti i valori dei parametri obbligatori non è possibile salvare il webhook.</span><span class="sxs-lookup"><span data-stu-id="1e74f-270">You can’t save the webhook until all mandatory parameter values are provided.</span></span>

![Creazione di webhook e assegnazione di parametri](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="1e74f-272">Quando si esegue un runbook con un webhook, insieme ai parametri di input definiti viene inviato il parametro di input predefinito **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** .</span><span class="sxs-lookup"><span data-stu-id="1e74f-272">When you execute a runbook by using a webhook, the predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with the input parameters that you defined.</span></span> <span data-ttu-id="1e74f-273">È possibile fare clic per espandere il parametro **WebhookData** e visualizzarne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="1e74f-273">You can click to expand the **WebhookData** parameter for more details.</span></span>

![Parametro WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="1e74f-275">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e74f-275">Next steps</span></span>
* <span data-ttu-id="1e74f-276">Per altre informazioni su input e output dei runbook, vedere l'articolo [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/)(Automazione di Azure: input e output del runbook e runbook nidificati).</span><span class="sxs-lookup"><span data-stu-id="1e74f-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="1e74f-277">Per informazioni dettagliate sulle diverse modalità di avvio dei runbook, vedere [Avvio di un Runbook in Automazione di Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="1e74f-277">For details about different ways to start a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="1e74f-278">Per modificare un runbook testuale, vedere [Modifica di runbook testuali in Automazione di Azure](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="1e74f-278">To edit a textual runbook, refer to [Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="1e74f-279">Per modificare un runbook grafico, vedere [Creazione grafica in Automazione di Azure](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="1e74f-279">To edit a graphical runbook, refer to [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

