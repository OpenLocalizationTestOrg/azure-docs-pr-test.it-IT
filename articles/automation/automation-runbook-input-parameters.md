---
title: i parametri di input aaaRunbook | Documenti Microsoft
description: "Parametri di input runbook aumentare la flessibilità di hello dei runbook, consentendo toopass dati tooa runbook quando viene avviata. Questo articolo descrive vari scenari in cui i parametri di input vengono usati nei runbook."
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
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="487b8-104">Parametri di input dei runbook</span><span class="sxs-lookup"><span data-stu-id="487b8-104">Runbook input parameters</span></span>
<span data-ttu-id="487b8-105">Parametri di input runbook aumentare la flessibilità di hello dei runbook, consentendo toopass dati tooit quando viene avviata.</span><span class="sxs-lookup"><span data-stu-id="487b8-105">Runbook input parameters increase hello flexibility of runbooks by allowing you toopass data tooit when it is started.</span></span> <span data-ttu-id="487b8-106">i parametri di Hello consentono hello runbook azioni toobe di destinazione per gli ambienti e scenari specifici.</span><span class="sxs-lookup"><span data-stu-id="487b8-106">hello parameters allow hello runbook actions toobe targeted for specific scenarios and environments.</span></span> <span data-ttu-id="487b8-107">Questo articolo illustra vari scenari in cui i parametri di input vengono usati nei runbook.</span><span class="sxs-lookup"><span data-stu-id="487b8-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="487b8-108">Configurare i parametri di input</span><span class="sxs-lookup"><span data-stu-id="487b8-108">Configure input parameters</span></span>
<span data-ttu-id="487b8-109">È possibile configurare i parametri di input nei runbook grafici e in quelli di PowerShell e del flusso di lavoro PowerShell.</span><span class="sxs-lookup"><span data-stu-id="487b8-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="487b8-110">Un runbook può avere più parametri con tipi di dati diversi oppure non avere parametri.</span><span class="sxs-lookup"><span data-stu-id="487b8-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="487b8-111">I parametri di input possono essere obbligatori o facoltativi ed è possibile assegnare un valore predefinito per i parametri facoltativi.</span><span class="sxs-lookup"><span data-stu-id="487b8-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="487b8-112">È possibile assegnare valori toohello i parametri di input per un runbook quando viene avviato tramite uno dei metodi disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-112">You can assign values toohello input parameters for a runbook when you start it through one of hello available methods.</span></span> <span data-ttu-id="487b8-113">Questi metodi includono l'avvio di un runbook dal portale di hello o un servizio web.</span><span class="sxs-lookup"><span data-stu-id="487b8-113">These methods include starting  a runbook from hello portal  or a web service.</span></span> <span data-ttu-id="487b8-114">È inoltre possibile avviare un runbook come figlio, definito inline in un altro runbook.</span><span class="sxs-lookup"><span data-stu-id="487b8-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="487b8-115">Configurare i parametri di input nei runbook di PowerShell e nei runbook del flusso di lavoro PowerShell</span><span class="sxs-lookup"><span data-stu-id="487b8-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="487b8-116">PowerShell e [runbook del flusso di lavoro di PowerShell](automation-first-runbook-textual.md) in automazione di Azure supporta i parametri di input che vengono definiti tramite hello gli attributi seguenti.</span><span class="sxs-lookup"><span data-stu-id="487b8-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through hello following attributes.</span></span>  

| <span data-ttu-id="487b8-117">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="487b8-117">**Property**</span></span> | <span data-ttu-id="487b8-118">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="487b8-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="487b8-119">Type</span><span class="sxs-lookup"><span data-stu-id="487b8-119">Type</span></span> |<span data-ttu-id="487b8-120">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="487b8-120">Required.</span></span> <span data-ttu-id="487b8-121">tipo di dati Hello previsto per il valore di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-121">hello data type expected for hello parameter value.</span></span> <span data-ttu-id="487b8-122">Qualsiasi tipo .NET è valido.</span><span class="sxs-lookup"><span data-stu-id="487b8-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="487b8-123">Nome</span><span class="sxs-lookup"><span data-stu-id="487b8-123">Name</span></span> |<span data-ttu-id="487b8-124">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="487b8-124">Required.</span></span> <span data-ttu-id="487b8-125">nome di Hello del parametro hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-125">hello name of hello parameter.</span></span> <span data-ttu-id="487b8-126">Questo deve essere univoco all'interno di runbook hello e può contenere solo lettere, numeri o caratteri di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="487b8-126">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="487b8-127">Deve iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="487b8-127">It must start with a letter.</span></span> |
| <span data-ttu-id="487b8-128">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="487b8-128">Mandatory</span></span> |<span data-ttu-id="487b8-129">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="487b8-129">Optional.</span></span> <span data-ttu-id="487b8-130">Specifica se è necessario specificare un valore per il parametro hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-130">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="487b8-131">Se si imposta questa troppo**$true**, quindi è necessario fornire un valore alla hello runbook viene avviato.</span><span class="sxs-lookup"><span data-stu-id="487b8-131">If you set this too**$true**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="487b8-132">Se si imposta questa troppo**$false**, quindi un valore è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="487b8-132">If you set this too**$false**, then a value is optional.</span></span> |
| <span data-ttu-id="487b8-133">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="487b8-133">Default value</span></span> |<span data-ttu-id="487b8-134">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="487b8-134">Optional.</span></span>  <span data-ttu-id="487b8-135">Specifica un valore che verrà utilizzato per il parametro hello se un valore non sia stato passato quando hello runbook viene avviato.</span><span class="sxs-lookup"><span data-stu-id="487b8-135">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="487b8-136">Un valore predefinito può essere impostato per qualsiasi parametro e verrà apportate automaticamente il parametro hello facoltativo indipendentemente dall'impostazione obbligatoria hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-136">A default value can be set for any parameter and will automatically make hello parameter optional regardless of hello Mandatory setting.</span></span> |

<span data-ttu-id="487b8-137">Windows PowerShell supporta più attributi dei parametri di input di quelli elencati di seguito, ad esempio la convalida, gli alias e i set di parametri.</span><span class="sxs-lookup"><span data-stu-id="487b8-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="487b8-138">Tuttavia, automazione di Azure supporta attualmente solo hello parametri di input elencati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="487b8-138">However, Azure Automation currently supports only hello input parameters listed above.</span></span>

<span data-ttu-id="487b8-139">Una definizione di parametro nei runbook del flusso di lavoro di PowerShell ha hello seguente formato generale, in cui più parametri sono separati da virgole.</span><span class="sxs-lookup"><span data-stu-id="487b8-139">A parameter definition in PowerShell Workflow runbooks has hello following general form, where multiple parameters are separated by commas.</span></span>

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
> <span data-ttu-id="487b8-140">Quando si definiscono i parametri, se non si specifica hello **obbligatorio** attributo, per impostazione predefinita, il parametro hello è considerato facoltativo.</span><span class="sxs-lookup"><span data-stu-id="487b8-140">When you're defining parameters, if you don’t specify hello **Mandatory** attribute, then by default, hello parameter is considered optional.</span></span> <span data-ttu-id="487b8-141">Inoltre, se si imposta un valore predefinito per un parametro nei runbook del flusso di lavoro di PowerShell, verrà considerato da PowerShell come un parametro facoltativo, indipendentemente dal hello **obbligatorio** valore dell'attributo.</span><span class="sxs-lookup"><span data-stu-id="487b8-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of hello **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="487b8-142">Ad esempio, è possibile configurare parametri di input hello per un runbook del flusso di lavoro di PowerShell che restituisce informazioni dettagliate su macchine virtuali, una singola macchina virtuale o tutte le macchine virtuali all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="487b8-142">As an example, let’s configure hello input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="487b8-143">Questo runbook ha due parametri, come illustrato nella seguente schermata hello: nome hello della macchina virtuale e il nome di hello hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="487b8-143">This runbook has two parameters as shown in hello following screenshot: hello name of virtual machine and hello name of hello resource group.</span></span>

![Flusso di lavoro PowerShell di Automazione](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="487b8-145">In questa definizione di parametro hello parametri **$VMName** e **$resourceGroupName** semplice ai parametri di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="487b8-145">In this parameter definition, hello parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="487b8-146">I runbook di PowerShell e del flusso di lavoro PowerShell supportano tuttavia tutti i tipi semplici e complessi, ad esempio **object** o **PSCredential** per i parametri di input.</span><span class="sxs-lookup"><span data-stu-id="487b8-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="487b8-147">Se il runbook include un parametro di input di tipo di oggetto, quindi utilizzare una tabella hash di PowerShell con (nome, valore) coppie toopass in un valore.</span><span class="sxs-lookup"><span data-stu-id="487b8-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs toopass in a value.</span></span> <span data-ttu-id="487b8-148">Ad esempio, se si dispone di hello segue parametro in un runbook:</span><span class="sxs-lookup"><span data-stu-id="487b8-148">For example, if you have hello following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="487b8-149">È quindi possibile passare hello segue valore toohello parametro:</span><span class="sxs-lookup"><span data-stu-id="487b8-149">Then you can pass hello following value toohello parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="487b8-150">Configurare i parametri di input in runbook grafici</span><span class="sxs-lookup"><span data-stu-id="487b8-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="487b8-151">troppo[configurare un runbook grafico](automation-first-runbook-graphical.md) con parametri di input, creare un runbook con interfaccia grafico che restituisce informazioni dettagliate sulle macchine virtuali, ovvero una singola macchina virtuale o tutte le macchine virtuali all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="487b8-151">too[configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="487b8-152">La configurazione di un runbook è costituita da due attività principali, come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="487b8-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="487b8-153">[**L'autenticazione di runbook con account RunAs di Azure** ](automation-sec-configure-azure-runas-account.md) tooauthenticate con Azure.</span><span class="sxs-lookup"><span data-stu-id="487b8-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) tooauthenticate with Azure.</span></span>

<span data-ttu-id="487b8-154">[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) proprietà hello tooget di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="487b8-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello properties of a virtual machines.</span></span>

<span data-ttu-id="487b8-155">È possibile utilizzare hello [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) nomi hello toooutput delle attività delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="487b8-155">You can use hello [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity toooutput hello names of virtual machines.</span></span> <span data-ttu-id="487b8-156">Hello attività **Get AzureRmVm** accetta due parametri, hello **nome della macchina virtuale** hello e **nome gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="487b8-156">hello activity **Get-AzureRmVm** accepts two parameters, hello **virtual machine name** and hello **resource group name**.</span></span> <span data-ttu-id="487b8-157">Poiché questi parametri potrebbero richiedere valori diversi a ogni avvio di runbook hello, è possibile aggiungere parametri di input tooyour runbook.</span><span class="sxs-lookup"><span data-stu-id="487b8-157">Since these parameters could require different values each time you start hello runbook, you can add input parameters tooyour runbook.</span></span> <span data-ttu-id="487b8-158">Di seguito sono parametri di input tooadd hello passaggi:</span><span class="sxs-lookup"><span data-stu-id="487b8-158">Here are hello steps tooadd input parameters:</span></span>

1. <span data-ttu-id="487b8-159">Selezionare hello runbook grafico da hello **runbook** blade e quindi fare clic su [ **modifica** ](automation-graphical-authoring-intro.md) è.</span><span class="sxs-lookup"><span data-stu-id="487b8-159">Select hello graphical runbook from hello **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="487b8-160">Nell'editor di runbook hello, fare clic su **Input e output** tooopen hello **Input e output** blade.</span><span class="sxs-lookup"><span data-stu-id="487b8-160">From hello runbook editor, click **Input and output** tooopen hello **Input and output** blade.</span></span>
   
    ![Runbook grafico di Automazione](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="487b8-162">Hello **Input e output** pannello viene visualizzato un elenco di parametri di input definiti per il runbook hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-162">hello **Input and output** blade displays a list of input parameters that are defined for hello runbook.</span></span> <span data-ttu-id="487b8-163">In questo pannello, è possibile aggiungere un nuovo parametro di input o modificare la configurazione di hello di un parametro di input esistente.</span><span class="sxs-lookup"><span data-stu-id="487b8-163">On this blade, you can either add a new input parameter or edit hello configuration of an existing input parameter.</span></span> <span data-ttu-id="487b8-164">tooadd un nuovo parametro per hello runbook, fare clic su **aggiungere input** tooopen hello **parametro di input Runbook** blade.</span><span class="sxs-lookup"><span data-stu-id="487b8-164">tooadd a new parameter for hello runbook, click **Add input** tooopen hello **Runbook input parameter** blade.</span></span> <span data-ttu-id="487b8-165">Non esiste, è possibile configurare hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="487b8-165">There, you can configure hello following parameters:</span></span>
   
   | <span data-ttu-id="487b8-166">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="487b8-166">**Property**</span></span> | <span data-ttu-id="487b8-167">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="487b8-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="487b8-168">Nome</span><span class="sxs-lookup"><span data-stu-id="487b8-168">Name</span></span> |<span data-ttu-id="487b8-169">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="487b8-169">Required.</span></span>  <span data-ttu-id="487b8-170">nome di Hello del parametro hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-170">hello name of hello parameter.</span></span> <span data-ttu-id="487b8-171">Questo deve essere univoco all'interno di runbook hello e può contenere solo lettere, numeri o caratteri di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="487b8-171">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="487b8-172">Deve iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="487b8-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="487b8-173">Descrizione</span><span class="sxs-lookup"><span data-stu-id="487b8-173">Description</span></span> |<span data-ttu-id="487b8-174">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="487b8-174">Optional.</span></span> <span data-ttu-id="487b8-175">Descrizione dello scopo hello del parametro di input.</span><span class="sxs-lookup"><span data-stu-id="487b8-175">Description about hello purpose of input parameter.</span></span> |
   | <span data-ttu-id="487b8-176">Tipo</span><span class="sxs-lookup"><span data-stu-id="487b8-176">Type</span></span> |<span data-ttu-id="487b8-177">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="487b8-177">Optional.</span></span> <span data-ttu-id="487b8-178">tipo di dati Hello prevista per il valore del parametro hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-178">hello data type that's expected for hello parameter value.</span></span> <span data-ttu-id="487b8-179">I tipi di parametro supportati sono **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime** e **Object**.</span><span class="sxs-lookup"><span data-stu-id="487b8-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="487b8-180">Se un tipo di dati non è selezionato, il valore predefinito troppo**stringa**.</span><span class="sxs-lookup"><span data-stu-id="487b8-180">If a data type is not selected, it defaults too**String**.</span></span> |
   | <span data-ttu-id="487b8-181">Mandatory</span><span class="sxs-lookup"><span data-stu-id="487b8-181">Mandatory</span></span> |<span data-ttu-id="487b8-182">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="487b8-182">Optional.</span></span> <span data-ttu-id="487b8-183">Specifica se è necessario specificare un valore per il parametro hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-183">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="487b8-184">Se si sceglie **Sì**, quindi è necessario fornire un valore alla hello runbook viene avviato.</span><span class="sxs-lookup"><span data-stu-id="487b8-184">If you choose **yes**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="487b8-185">Se si sceglie **non**, un valore non è necessario quando hello runbook viene avviato e può essere impostato un valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="487b8-185">If you choose **no**, then a value is not required when hello runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="487b8-186">Default Value</span><span class="sxs-lookup"><span data-stu-id="487b8-186">Default Value</span></span> |<span data-ttu-id="487b8-187">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="487b8-187">Optional.</span></span> <span data-ttu-id="487b8-188">Specifica un valore che verrà utilizzato per il parametro hello se un valore non sia stato passato quando hello runbook viene avviato.</span><span class="sxs-lookup"><span data-stu-id="487b8-188">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="487b8-189">È possibile impostare un valore predefinito per un parametro non obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="487b8-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="487b8-190">Scegliere un valore predefinito, tooset **personalizzato**.</span><span class="sxs-lookup"><span data-stu-id="487b8-190">tooset a default value, choose **Custom**.</span></span> <span data-ttu-id="487b8-191">Questo valore viene utilizzato a meno che un altro valore viene fornito quando hello runbook viene avviato.</span><span class="sxs-lookup"><span data-stu-id="487b8-191">This value is used unless another value is provided when hello runbook is started.</span></span> <span data-ttu-id="487b8-192">Scegliere **Nessuno** se non si desidera tooprovide qualsiasi valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="487b8-192">Choose **None** if you don’t want tooprovide any default value.</span></span> |
   
    ![Aggiunta di nuovo input](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="487b8-194">Creare due parametri con le proprietà che verranno utilizzate da hello seguenti hello **Get AzureRmVm** attività:</span><span class="sxs-lookup"><span data-stu-id="487b8-194">Create two parameters with hello following properties that will be used by hello **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="487b8-195">**Parametro 1:**</span><span class="sxs-lookup"><span data-stu-id="487b8-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="487b8-196">Nome: VMName</span><span class="sxs-lookup"><span data-stu-id="487b8-196">Name - VMName</span></span>
     * <span data-ttu-id="487b8-197">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="487b8-197">Type - String</span></span>
     * <span data-ttu-id="487b8-198">Obbligatorio: no</span><span class="sxs-lookup"><span data-stu-id="487b8-198">Mandatory - No</span></span>
   * <span data-ttu-id="487b8-199">**Parametro2:**</span><span class="sxs-lookup"><span data-stu-id="487b8-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="487b8-200">Nome: resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="487b8-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="487b8-201">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="487b8-201">Type - String</span></span>
     * <span data-ttu-id="487b8-202">Obbligatorio: no</span><span class="sxs-lookup"><span data-stu-id="487b8-202">Mandatory - No</span></span>
     * <span data-ttu-id="487b8-203">Valore predefinito: personalizzato</span><span class="sxs-lookup"><span data-stu-id="487b8-203">Default value - Custom</span></span>
     * <span data-ttu-id="487b8-204">Il valore predefinito personalizzato - \<nome hello del gruppo di risorse contenente le macchine virtuali hello ></span><span class="sxs-lookup"><span data-stu-id="487b8-204">Custom default value - \<Name of hello resource group that contains hello virtual machines></span></span>
5. <span data-ttu-id="487b8-205">Dopo aver aggiunto i parametri di hello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="487b8-205">Once you add hello parameters, click **OK**.</span></span>  <span data-ttu-id="487b8-206">È ora possibile visualizzarli in hello **Input e output blade**.</span><span class="sxs-lookup"><span data-stu-id="487b8-206">You can now view them in hello **Input and output blade**.</span></span> <span data-ttu-id="487b8-207">Fare nuovamente clic su **OK**, quindi su **Salva** e **pubblicare** il runbook.</span><span class="sxs-lookup"><span data-stu-id="487b8-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-tooinput-parameters-in-runbooks"></a><span data-ttu-id="487b8-208">Assegnare valori tooinput parametri nei runbook</span><span class="sxs-lookup"><span data-stu-id="487b8-208">Assign values tooinput parameters in runbooks</span></span>
<span data-ttu-id="487b8-209">È possibile passare valori tooinput parametri nei runbook in hello seguenti scenari.</span><span class="sxs-lookup"><span data-stu-id="487b8-209">You can pass values tooinput parameters in runbooks in hello following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="487b8-210">Avviare un runbook e assegnare parametri</span><span class="sxs-lookup"><span data-stu-id="487b8-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="487b8-211">Un runbook può essere avviato molti modi: tramite hello portale di Azure con un webhook, con i cmdlet di PowerShell, con l'API REST hello o con hello SDK.</span><span class="sxs-lookup"><span data-stu-id="487b8-211">A runbook can be started many ways: through hello Azure portal, with a webhook, with PowerShell cmdlets, with hello REST API, or with hello SDK.</span></span> <span data-ttu-id="487b8-212">Di seguito vengono illustrati vari metodi per avviare un runbook e assegnare parametri.</span><span class="sxs-lookup"><span data-stu-id="487b8-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a><span data-ttu-id="487b8-213">Avviare un runbook pubblicato tramite il portale di Azure hello e assegnare i parametri</span><span class="sxs-lookup"><span data-stu-id="487b8-213">Start a published runbook by using hello Azure portal and assign parameters</span></span>
<span data-ttu-id="487b8-214">Quando si [avviare runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **avvia Runbook** pannello viene aperto ed è possibile configurare i valori per parametri hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="487b8-214">When you [start hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Start Runbook** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Iniziare a usare il portale di hello](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="487b8-216">In etichetta hello sotto la casella di hello input, è possibile visualizzare gli attributi di hello che sono stati impostati per il parametro hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-216">In hello label beneath hello input box, you can see hello attributes that have been set for hello parameter.</span></span> <span data-ttu-id="487b8-217">Gli attributi includono obbligatorio o facoltativo, tipo e valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="487b8-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="487b8-218">Nella hello Guida fumetto toohello parametro nome successivo, è possibile visualizzare tutte le informazioni chiave hello è necessario toomake decisioni sui valori dei parametri input.</span><span class="sxs-lookup"><span data-stu-id="487b8-218">In hello help balloon next toohello parameter name, you can see all hello key information you need toomake decisions about parameter input values.</span></span> <span data-ttu-id="487b8-219">Queste informazioni indicano se un parametro è obbligatorio o facoltativo.</span><span class="sxs-lookup"><span data-stu-id="487b8-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="487b8-220">Include inoltre il tipo di hello e il valore predefinito (se presente) e ad altre note utili.</span><span class="sxs-lookup"><span data-stu-id="487b8-220">It also includes hello type and default value (if any), and other helpful notes.</span></span>

![Fumetto della Guida](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="487b8-222">I parametri di tipo String supportano valori di stringa **vuoti** .</span><span class="sxs-lookup"><span data-stu-id="487b8-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="487b8-223">Immissione **[EmptyString]** nel parametro di input hello casella verrà passato un parametro di toohello una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="487b8-223">Entering **[EmptyString]** in hello input parameter box will pass an empty string toohello parameter.</span></span> <span data-ttu-id="487b8-224">I parametri di tipo String non supportano il passaggio di valori **Null** .</span><span class="sxs-lookup"><span data-stu-id="487b8-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="487b8-225">Se si non passa qualsiasi parametro di stringa di valore toohello, quindi PowerShell verrà interpretarlo come null.</span><span class="sxs-lookup"><span data-stu-id="487b8-225">If you don’t pass any value toohello String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="487b8-226">Avviare un runbook pubblicato usando i cmdlet di PowerShell e assegnare parametri</span><span class="sxs-lookup"><span data-stu-id="487b8-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="487b8-227">**Cmdlet di Azure Resource Manager:** è possibile avviare un runbook di Automazione creato in un gruppo di risorse usando [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="487b8-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="487b8-228">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="487b8-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="487b8-229">**Cmdlet di Gestione dei servizi di Azure:** è possibile avviare un runbook di automazione creato in un gruppo di risorse predefinito usando [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span><span class="sxs-lookup"><span data-stu-id="487b8-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="487b8-230">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="487b8-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="487b8-231">Quando si avvia un runbook con i cmdlet di PowerShell, un parametro predefinito, **MicrosoftApplicationManagementStartedBy** creato con il valore di hello **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="487b8-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with hello value **PowerShell**.</span></span> <span data-ttu-id="487b8-232">È possibile visualizzare questo parametro in hello **processo dettagli** blade.</span><span class="sxs-lookup"><span data-stu-id="487b8-232">You can view this parameter in hello **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="487b8-233">Avviare un runbook usando un SDK e assegnare parametri</span><span class="sxs-lookup"><span data-stu-id="487b8-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="487b8-234">**Metodo di gestione delle risorse Azure:** è possibile avviare un runbook tramite hello SDK di un linguaggio di programmazione.</span><span class="sxs-lookup"><span data-stu-id="487b8-234">**Azure Resource Manager method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="487b8-235">Di seguito è riportato un frammento di codice C# per l'avvio di un runbook nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="487b8-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="487b8-236">È possibile visualizzare tutto il codice hello al nostro [repository GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="487b8-236">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
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
* <span data-ttu-id="487b8-237">**Metodo di gestione dei servizi Azure:** è possibile avviare un runbook tramite hello SDK di un linguaggio di programmazione.</span><span class="sxs-lookup"><span data-stu-id="487b8-237">**Azure Service Management method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="487b8-238">Di seguito è riportato un frammento di codice C# per l'avvio di un runbook nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="487b8-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="487b8-239">È possibile visualizzare tutto il codice hello al nostro [repository GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="487b8-239">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
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
  
  <span data-ttu-id="487b8-240">toostart questo metodo, creare un hello toostore dizionario di parametri del runbook, **VMName** e **resourceGroupName**e i relativi valori.</span><span class="sxs-lookup"><span data-stu-id="487b8-240">toostart this method, create a dictionary toostore hello runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="487b8-241">Quindi, avviare runbook hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-241">Then start hello runbook.</span></span> <span data-ttu-id="487b8-242">Di seguito è hello c# frammento di codice per chiamare il metodo hello è definito in precedenza.</span><span class="sxs-lookup"><span data-stu-id="487b8-242">Below is hello C# code snippet for calling hello method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a><span data-ttu-id="487b8-243">Avviare un runbook tramite l'API REST hello e assegnare i parametri</span><span class="sxs-lookup"><span data-stu-id="487b8-243">Start a runbook by using hello REST API and assign parameters</span></span>
<span data-ttu-id="487b8-244">Un processo del runbook può essere creato e avviato con hello API REST di automazione di Azure tramite hello **inserire** metodo con hello seguente URI della richiesta.</span><span class="sxs-lookup"><span data-stu-id="487b8-244">A runbook job can be created and started with hello Azure Automation REST API by using hello **PUT** method with hello following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="487b8-245">Nell'URI della richiesta hello, sostituire hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="487b8-245">In hello request URI, replace hello following parameters:</span></span>

* <span data-ttu-id="487b8-246">**subscription-id:** ID della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="487b8-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="487b8-247">**cloud-service-name:** hello Nome richiesta hello cloud servizio toowhich hello deve essere inviati.</span><span class="sxs-lookup"><span data-stu-id="487b8-247">**cloud-service-name:** hello name of hello cloud service toowhich hello request should be sent.</span></span>  
* <span data-ttu-id="487b8-248">**Automation-account-name:** hello dell'account di automazione che viene ospitato all'interno di hello Nome servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="487b8-248">**automation-account-name:** hello name of your automation account that's hosted within hello specified cloud service.</span></span>  
* <span data-ttu-id="487b8-249">**id processo:** hello GUID per il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-249">**job-id:** hello GUID for hello job.</span></span> <span data-ttu-id="487b8-250">GUID in PowerShell possono essere create usando hello **[GUID]::NewGuid(). ToString ()** comando.</span><span class="sxs-lookup"><span data-stu-id="487b8-250">GUIDs in PowerShell can be created by using hello **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="487b8-251">Nel processo del runbook toohello parametri toopass ordine, utilizzare il corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-251">In order toopass parameters toohello runbook job, use hello request body.</span></span> <span data-ttu-id="487b8-252">Avrà hello seguenti due proprietà fornita in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="487b8-252">It takes hello following two properties provided in JSON format:</span></span>

* <span data-ttu-id="487b8-253">**Nome del runbook:** obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="487b8-253">**Runbook name:** Required.</span></span> <span data-ttu-id="487b8-254">nome Hello del runbook hello toostart processo hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-254">hello name of hello runbook for hello job toostart.</span></span>  
* <span data-ttu-id="487b8-255">**Parametri del runbook:** facoltativi.</span><span class="sxs-lookup"><span data-stu-id="487b8-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="487b8-256">Un dizionario di elenco di parametri hello (nome, valore) formato in cui nome deve essere di tipo stringa e può essere qualsiasi valore JSON valido.</span><span class="sxs-lookup"><span data-stu-id="487b8-256">A dictionary of hello parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="487b8-257">Se si desidera hello toostart **Get AzureVMTextual** runbook che è stato creato in precedenza con **VMName** e **resourceGroupName** come parametri, utilizzare hello seguendo il formato JSON Per corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-257">If you want toostart hello **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use hello following JSON format for hello request body.</span></span>

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

<span data-ttu-id="487b8-258">Se il processo di hello è stato creato, viene restituito un codice di stato HTTP 201.</span><span class="sxs-lookup"><span data-stu-id="487b8-258">A HTTP status code 201 is returned if hello job is successfully created.</span></span> <span data-ttu-id="487b8-259">Per ulteriori informazioni su intestazioni e corpo della risposta hello, fare riferimento toohello articolo su come troppo[creare un processo del runbook con hello API REST.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="487b8-259">For more information on response headers and hello response body, refer toohello article about how too[create a runbook job by using hello REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="487b8-260">Eseguire il test di un runbook e assegnare parametri</span><span class="sxs-lookup"><span data-stu-id="487b8-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="487b8-261">Quando si [test hello versione bozza del runbook](automation-testing-runbook.md) utilizzando l'opzione di verifica hello, hello **Test** pannello viene aperto ed è possibile configurare i valori per parametri hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="487b8-261">When you [test hello draft version of your runbook](automation-testing-runbook.md) by using hello test option, hello **Test** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Esecuzione di test e assegnazione di parametri](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a><span data-ttu-id="487b8-263">Collega un runbook tooa pianificazione e assegnare i parametri</span><span class="sxs-lookup"><span data-stu-id="487b8-263">Link a schedule tooa runbook and assign parameters</span></span>
<span data-ttu-id="487b8-264">È possibile [collegare una pianificazione](automation-schedules.md) tooyour runbook in modo tale runbook hello viene avviato in un momento specifico.</span><span class="sxs-lookup"><span data-stu-id="487b8-264">You can [link a schedule](automation-schedules.md) tooyour runbook so that hello runbook starts at a specific time.</span></span> <span data-ttu-id="487b8-265">Assegnare i parametri di input quando si crea una pianificazione hello e hello runbook userà questi valori quando viene avviato dalla pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="487b8-265">You assign input parameters when you create hello schedule, and hello runbook will use these values when it is started by hello schedule.</span></span> <span data-ttu-id="487b8-266">È possibile salvare la pianificazione hello fino a quando non vengono forniti tutti i valori di parametro obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="487b8-266">You can’t save hello schedule until all mandatory parameter values are provided.</span></span>

![Pianificazione e assegnazione di parametri](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="487b8-268">Creare un webhook per un runbook e assegnare parametri</span><span class="sxs-lookup"><span data-stu-id="487b8-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="487b8-269">È possibile creare un [webhook](automation-webhooks.md) per il runbook e configurare i parametri di input del runbook.</span><span class="sxs-lookup"><span data-stu-id="487b8-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="487b8-270">Impossibile salvare il webhook hello fino a quando non vengono forniti tutti i valori di parametro obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="487b8-270">You can’t save hello webhook until all mandatory parameter values are provided.</span></span>

![Creazione di webhook e assegnazione di parametri](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="487b8-272">Quando si eseguirà un runbook tramite un webhook hello predefiniti di parametro di input  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  viene inviato, insieme ai parametri di input di hello è definito.</span><span class="sxs-lookup"><span data-stu-id="487b8-272">When you execute a runbook by using a webhook, hello predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with hello input parameters that you defined.</span></span> <span data-ttu-id="487b8-273">È possibile fare clic su hello tooexpand **WebhookData** parametro per maggiori dettagli.</span><span class="sxs-lookup"><span data-stu-id="487b8-273">You can click tooexpand hello **WebhookData** parameter for more details.</span></span>

![Parametro WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="487b8-275">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="487b8-275">Next steps</span></span>
* <span data-ttu-id="487b8-276">Per altre informazioni su input e output dei runbook, vedere l'articolo [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/)(Automazione di Azure: input e output del runbook e runbook nidificati).</span><span class="sxs-lookup"><span data-stu-id="487b8-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="487b8-277">Per informazioni dettagliate sui diversi modi toostart un runbook, vedere [avvio di un runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="487b8-277">For details about different ways toostart a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="487b8-278">tooedit un runbook testuale, fare riferimento troppo[modifica runbook testuale](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="487b8-278">tooedit a textual runbook, refer too[Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="487b8-279">tooedit un runbook grafico, fare riferimento troppo[grafici per la modifica in automazione di Azure](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="487b8-279">tooedit a graphical runbook, refer too[Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

