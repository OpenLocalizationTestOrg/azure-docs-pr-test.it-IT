---
title: risorse di automazione aaaAzure nelle soluzioni OMS | Documenti Microsoft
description: "Soluzioni in OMS includerà in genere i runbook in automazione di Azure tooautomate processi, ad esempio la raccolta e l'elaborazione dati di monitoraggio.  Questo articolo viene descritto come tooinclude runbook e le relative risorse in una soluzione."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a><span data-ttu-id="a12d3-104">Aggiunta di soluzione di gestione OMS tooan risorse automazione di Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="a12d3-104">Adding Azure Automation resources tooan OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="a12d3-105">Questa è una documentazione preliminare per la creazione di soluzioni di gestione in OMS attualmente disponibili in versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="a12d3-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="a12d3-106">Qualsiasi schema descritto di seguito è soggetto toochange.</span><span class="sxs-lookup"><span data-stu-id="a12d3-106">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="a12d3-107">[Soluzioni di gestione in OMS](operations-management-suite-solutions.md) includerà in genere i runbook in automazione di Azure tooautomate processi, ad esempio la raccolta e l'elaborazione dati di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="a12d3-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation tooautomate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="a12d3-108">Toorunbooks, gli account di automazione include inoltre risorse, ad esempio variabili e le pianificazioni che supportano i runbook di hello utilizzati nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-108">In addition toorunbooks, Automation accounts includes assets such as variables and schedules that support hello runbooks used in hello solution.</span></span>  <span data-ttu-id="a12d3-109">Questo articolo viene descritto come tooinclude runbook e le relative risorse in una soluzione.</span><span class="sxs-lookup"><span data-stu-id="a12d3-109">This article describes how tooinclude runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="a12d3-110">Hello esempi in questo articolo utilizzano parametri e variabili che sono entrambe soluzioni toomanagement necessarie o comuni e descritte in [la creazione di soluzioni di gestione in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="a12d3-110">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="a12d3-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a12d3-111">Prerequisites</span></span>
<span data-ttu-id="a12d3-112">Questo articolo si presuppone che si ha già familiarità con le seguenti informazioni hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-112">This article assumes that you're already familiar with hello following information.</span></span>

- <span data-ttu-id="a12d3-113">Come troppo[creare una soluzione di gestione](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="a12d3-113">How too[create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="a12d3-114">struttura di Hello un [file di soluzione](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="a12d3-114">hello structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="a12d3-115">Come troppo[creare modelli di gestione risorse](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="a12d3-115">How too[author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="a12d3-116">Account di Automazione</span><span class="sxs-lookup"><span data-stu-id="a12d3-116">Automation account</span></span>
<span data-ttu-id="a12d3-117">Tutte le risorse di Automazione di Azure sono contenute in un [account di Automazione](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="a12d3-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="a12d3-118">Come descritto in [OMS dell'area di lavoro e account di automazione](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello account di automazione non è incluso nella soluzione di gestione di hello ma deve essere presente prima di installata la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello Automation account isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="a12d3-119">Se non è disponibile, l'installazione di soluzioni hello avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a12d3-119">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="a12d3-120">nome di Hello di ogni risorsa automazione include nome hello del relativo account di automazione.</span><span class="sxs-lookup"><span data-stu-id="a12d3-120">hello name of each Automation resource includes hello name of its Automation account.</span></span>  <span data-ttu-id="a12d3-121">Questa operazione viene eseguita nella soluzione hello con hello **accountName** parametro come hello seguente esempio di una risorsa di runbook.</span><span class="sxs-lookup"><span data-stu-id="a12d3-121">This is done in hello solution with hello **accountName** parameter as in hello following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="a12d3-122">Runbook</span><span class="sxs-lookup"><span data-stu-id="a12d3-122">Runbooks</span></span>
<span data-ttu-id="a12d3-123">È consigliabile includere tutti i runbook utilizzati dalla soluzione hello nel file di soluzione hello in modo che vengono creati quando si installa la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-123">You should include any runbooks used by hello solution in hello solution file so that they're created when hello solution is installed.</span></span>  <span data-ttu-id="a12d3-124">È non possono contenere corpo hello del runbook hello nel modello di hello, pertanto è consigliabile pubblicare hello runbook tooa percorso pubblico in modo da essere accessibile da qualsiasi utente che installa la soluzione.</span><span class="sxs-lookup"><span data-stu-id="a12d3-124">You cannot contain hello body of hello runbook in hello template though, so you should publish hello runbook tooa public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="a12d3-125">[Runbook di automazione di Azure](../automation/automation-runbook-types.md) risorse hanno un tipo di **Microsoft.Automation/automationAccounts/runbooks** e hello seguente struttura.</span><span class="sxs-lookup"><span data-stu-id="a12d3-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have hello following structure.</span></span> <span data-ttu-id="a12d3-126">Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


<span data-ttu-id="a12d3-127">in hello nella tabella seguente vengono descritte le proprietà di Hello per runbook.</span><span class="sxs-lookup"><span data-stu-id="a12d3-127">hello properties for runbooks are described in hello following table.</span></span>

| <span data-ttu-id="a12d3-128">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a12d3-128">Property</span></span> | <span data-ttu-id="a12d3-129">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a12d3-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a12d3-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="a12d3-130">runbookType</span></span> |<span data-ttu-id="a12d3-131">Specifica i tipi di hello di hello runbook.</span><span class="sxs-lookup"><span data-stu-id="a12d3-131">Specifies hello types of hello runbook.</span></span> <br><br> <span data-ttu-id="a12d3-132">Script - Script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="a12d3-132">Script - PowerShell script</span></span> <br><span data-ttu-id="a12d3-133">PowerShell - Flusso di lavoro di PowerShell</span><span class="sxs-lookup"><span data-stu-id="a12d3-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="a12d3-134">GraphPowerShell - Runbook di script di PowerShell grafico</span><span class="sxs-lookup"><span data-stu-id="a12d3-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="a12d3-135">GraphPowerShellWorkflow - Runbook di flusso di lavoro di PowerShell grafico</span><span class="sxs-lookup"><span data-stu-id="a12d3-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="a12d3-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="a12d3-136">logProgress</span></span> |<span data-ttu-id="a12d3-137">Specifica se [stato record](../automation/automation-runbook-output-and-messages.md) devono essere generati per hello runbook.</span><span class="sxs-lookup"><span data-stu-id="a12d3-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="a12d3-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="a12d3-138">logVerbose</span></span> |<span data-ttu-id="a12d3-139">Specifica se [record dettagliati](../automation/automation-runbook-output-and-messages.md) devono essere generati per hello runbook.</span><span class="sxs-lookup"><span data-stu-id="a12d3-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="a12d3-140">description</span><span class="sxs-lookup"><span data-stu-id="a12d3-140">description</span></span> |<span data-ttu-id="a12d3-141">Descrizione facoltativa per il runbook hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-141">Optional description for hello runbook.</span></span> |
| <span data-ttu-id="a12d3-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="a12d3-142">publishContentLink</span></span> |<span data-ttu-id="a12d3-143">Specifica il contenuto di hello di hello runbook.</span><span class="sxs-lookup"><span data-stu-id="a12d3-143">Specifies hello content of hello runbook.</span></span> <br><br><span data-ttu-id="a12d3-144">URI - Uri toohello contenuto del runbook hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-144">uri - Uri toohello content of hello runbook.</span></span>  <span data-ttu-id="a12d3-145">Si tratterà di un file con estensione ps1 per i runbook di PowerShell e di script e di un file di runbook grafico esportato per un runbook di Graph.</span><span class="sxs-lookup"><span data-stu-id="a12d3-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="a12d3-146">versione - versione di hello runbook per il proprio rilevamento.</span><span class="sxs-lookup"><span data-stu-id="a12d3-146">version - Version of hello runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="a12d3-147">Processi di Automazione</span><span class="sxs-lookup"><span data-stu-id="a12d3-147">Automation jobs</span></span>
<span data-ttu-id="a12d3-148">Quando si avvia un runbook in Automazione di Azure, viene creato un processo di automazione.</span><span class="sxs-lookup"><span data-stu-id="a12d3-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="a12d3-149">È possibile aggiungere un'automazione processo risorse tooyour soluzione tooautomatically-inizio un runbook quando la soluzione di gestione hello è installata.</span><span class="sxs-lookup"><span data-stu-id="a12d3-149">You can add an automation job resource tooyour solution tooautomatically start a runbook when hello management solution is installed.</span></span>  <span data-ttu-id="a12d3-150">Questo metodo è runbook toostart utilizzati in genere utilizzati per la configurazione iniziale della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-150">This method is typically used toostart runbooks that are used for initial configuration of hello solution.</span></span>  <span data-ttu-id="a12d3-151">creare un runbook a intervalli regolari, toostart un [pianificazione](#schedules) e [pianificazione del processo](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="a12d3-151">toostart a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="a12d3-152">Risorse di processo hanno un tipo di **Microsoft.Automation/automationAccounts/jobs** e hello seguente struttura.</span><span class="sxs-lookup"><span data-stu-id="a12d3-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have hello following structure.</span></span>  <span data-ttu-id="a12d3-153">Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

<span data-ttu-id="a12d3-154">in hello nella tabella seguente vengono descritte le proprietà di Hello per processi di automazione.</span><span class="sxs-lookup"><span data-stu-id="a12d3-154">hello properties for automation jobs are described in hello following table.</span></span>

| <span data-ttu-id="a12d3-155">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a12d3-155">Property</span></span> | <span data-ttu-id="a12d3-156">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a12d3-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a12d3-157">runbook</span><span class="sxs-lookup"><span data-stu-id="a12d3-157">runbook</span></span> |<span data-ttu-id="a12d3-158">Entità di un nome singolo con nome hello di hello runbook toostart.</span><span class="sxs-lookup"><span data-stu-id="a12d3-158">Single name entity with hello name of hello runbook toostart.</span></span> |
| <span data-ttu-id="a12d3-159">parameters</span><span class="sxs-lookup"><span data-stu-id="a12d3-159">parameters</span></span> |<span data-ttu-id="a12d3-160">Entità per ogni valore di parametro richiesto da runbook hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-160">Entity for each parameter value required by hello runbook.</span></span> |

<span data-ttu-id="a12d3-161">il processo di Hello include il nome del runbook hello e qualsiasi toobe di valori di parametro inviati toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="a12d3-161">hello job includes hello runbook name and any parameter values toobe sent toohello runbook.</span></span>  <span data-ttu-id="a12d3-162">processo Hello deve [dipendono](operations-management-suite-solutions-solution-file.md#resources) hello runbook che viene avviato dall'hello runbook, è necessario creare prima il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-162">hello job should [depend on](operations-management-suite-solutions-solution-file.md#resources) hello runbook that it's starting since hello runbook must be created before hello job.</span></span>  <span data-ttu-id="a12d3-163">Se sono presenti più runbook da avviare, è possibile definire l'ordine di avvio impostando un processo in modo che dipenda da un altro processo che deve essere eseguito prima.</span><span class="sxs-lookup"><span data-stu-id="a12d3-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="a12d3-164">nome Hello di una risorsa di processo deve contenere un GUID che viene in genere assegnato da un parametro.</span><span class="sxs-lookup"><span data-stu-id="a12d3-164">hello name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="a12d3-165">Altre informazioni sui parametri GUID sono disponibili in [Creazione di soluzioni di gestione in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="a12d3-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="a12d3-166">Certificati</span><span class="sxs-lookup"><span data-stu-id="a12d3-166">Certificates</span></span>
<span data-ttu-id="a12d3-167">[Certificati di automazione di Azure](../automation/automation-certificates.md) dispone di un tipo di **Microsoft.Automation/automationAccounts/certificates** e hello seguente struttura.</span><span class="sxs-lookup"><span data-stu-id="a12d3-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have hello following structure.</span></span> <span data-ttu-id="a12d3-168">Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



<span data-ttu-id="a12d3-169">Nella hello nella tabella seguente sono descritte le proprietà di Hello per le risorse di certificati.</span><span class="sxs-lookup"><span data-stu-id="a12d3-169">hello properties for Certificates resources are described in hello following table.</span></span>

| <span data-ttu-id="a12d3-170">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a12d3-170">Property</span></span> | <span data-ttu-id="a12d3-171">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a12d3-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a12d3-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="a12d3-172">base64Value</span></span> |<span data-ttu-id="a12d3-173">Valore base 64 hello certificato.</span><span class="sxs-lookup"><span data-stu-id="a12d3-173">Base 64 value for hello certificate.</span></span> |
| <span data-ttu-id="a12d3-174">thumbprint</span><span class="sxs-lookup"><span data-stu-id="a12d3-174">thumbprint</span></span> |<span data-ttu-id="a12d3-175">Identificazione personale certificato hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-175">Thumbprint for hello certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="a12d3-176">Credenziali</span><span class="sxs-lookup"><span data-stu-id="a12d3-176">Credentials</span></span>
<span data-ttu-id="a12d3-177">[Le credenziali di automazione Azure](../automation/automation-credentials.md) dispone di un tipo di **Microsoft.Automation/automationAccounts/credentials** e hello seguente struttura.</span><span class="sxs-lookup"><span data-stu-id="a12d3-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have hello following structure.</span></span>  <span data-ttu-id="a12d3-178">Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

<span data-ttu-id="a12d3-179">Nella hello nella tabella seguente sono descritte le proprietà di Hello per le risorse di credenziali.</span><span class="sxs-lookup"><span data-stu-id="a12d3-179">hello properties for Credential resources are described in hello following table.</span></span>

| <span data-ttu-id="a12d3-180">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a12d3-180">Property</span></span> | <span data-ttu-id="a12d3-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a12d3-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a12d3-182">userName</span><span class="sxs-lookup"><span data-stu-id="a12d3-182">userName</span></span> |<span data-ttu-id="a12d3-183">Nome utente per le credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-183">User name for hello credential.</span></span> |
| <span data-ttu-id="a12d3-184">password</span><span class="sxs-lookup"><span data-stu-id="a12d3-184">password</span></span> |<span data-ttu-id="a12d3-185">Password per le credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-185">Password for hello credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="a12d3-186">Pianificazioni</span><span class="sxs-lookup"><span data-stu-id="a12d3-186">Schedules</span></span>
<span data-ttu-id="a12d3-187">[Le pianificazioni di automazione Azure](../automation/automation-schedules.md) dispone di un tipo di **Microsoft.Automation/automationAccounts/schedules** e hello hello seguente struttura.</span><span class="sxs-lookup"><span data-stu-id="a12d3-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have hello hello following structure.</span></span> <span data-ttu-id="a12d3-188">Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

<span data-ttu-id="a12d3-189">Nella hello nella tabella seguente sono descritte le proprietà di Hello per le risorse di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="a12d3-189">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="a12d3-190">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a12d3-190">Property</span></span> | <span data-ttu-id="a12d3-191">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a12d3-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a12d3-192">description</span><span class="sxs-lookup"><span data-stu-id="a12d3-192">description</span></span> |<span data-ttu-id="a12d3-193">Descrizione facoltativa per la pianificazione di hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-193">Optional description for hello schedule.</span></span> |
| <span data-ttu-id="a12d3-194">startTime</span><span class="sxs-lookup"><span data-stu-id="a12d3-194">startTime</span></span> |<span data-ttu-id="a12d3-195">Specifica l'ora di inizio hello di una pianificazione come oggetto DateTime.</span><span class="sxs-lookup"><span data-stu-id="a12d3-195">Specifies hello start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="a12d3-196">È possibile fornire una stringa se può essere convertito tooa DateTime valido.</span><span class="sxs-lookup"><span data-stu-id="a12d3-196">A string can be provided if it can be converted tooa valid DateTime.</span></span> |
| <span data-ttu-id="a12d3-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="a12d3-197">isEnabled</span></span> |<span data-ttu-id="a12d3-198">Specifica se la pianificazione hello è abilitata.</span><span class="sxs-lookup"><span data-stu-id="a12d3-198">Specifies whether hello schedule is enabled.</span></span> |
| <span data-ttu-id="a12d3-199">interval</span><span class="sxs-lookup"><span data-stu-id="a12d3-199">interval</span></span> |<span data-ttu-id="a12d3-200">tipo di Hello di intervallo per la pianificazione di hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-200">hello type of interval for hello schedule.</span></span><br><br><span data-ttu-id="a12d3-201">day</span><span class="sxs-lookup"><span data-stu-id="a12d3-201">day</span></span><br><span data-ttu-id="a12d3-202">hour</span><span class="sxs-lookup"><span data-stu-id="a12d3-202">hour</span></span> |
| <span data-ttu-id="a12d3-203">frequency</span><span class="sxs-lookup"><span data-stu-id="a12d3-203">frequency</span></span> |<span data-ttu-id="a12d3-204">Frequenza di pianificazione di hello deve generare in numero di ore o giorni.</span><span class="sxs-lookup"><span data-stu-id="a12d3-204">Frequency that hello schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="a12d3-205">Pianifica deve disporre di un'ora di inizio con un valore maggiore di hello ora corrente.</span><span class="sxs-lookup"><span data-stu-id="a12d3-205">Schedules must have a start time with a value greater than hello current time.</span></span>  <span data-ttu-id="a12d3-206">Poiché non è in alcun modo di sapere quando è toobe corso installato, è possibile fornire questo valore con una variabile.</span><span class="sxs-lookup"><span data-stu-id="a12d3-206">You cannot provide this value with a variable since you would have no way of knowing when it's going toobe installed.</span></span>

<span data-ttu-id="a12d3-207">Utilizzare uno dei seguenti due strategie di utilizzo delle risorse di pianificazione in una soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-207">Use one of hello following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="a12d3-208">Usare un parametro per l'ora di inizio hello della pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-208">Use a parameter for hello start time of hello schedule.</span></span>  <span data-ttu-id="a12d3-209">Questo richiederà hello utente tooprovide un valore quando installano la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-209">This will prompt hello user tooprovide a value when they install hello solution.</span></span>  <span data-ttu-id="a12d3-210">In caso di più pianificazioni, è possibile usare un unico valore di parametro anche per più di esse.</span><span class="sxs-lookup"><span data-stu-id="a12d3-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="a12d3-211">Creare pianificazioni hello usando un runbook che inizia quando si installa la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-211">Create hello schedules using a runbook that starts when hello solution is installed.</span></span>  <span data-ttu-id="a12d3-212">Ciò consente di rimuovere il requisito di hello di hello utente toospecify non può contenere un'ora, ma si pianificazione hello nella soluzione in modo verrà rimosso quando viene rimossa la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-212">This removes hello requirement of hello user toospecify a time, but you can't contain hello schedule in your solution so it will be removed when hello solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="a12d3-213">Pianificazioni dei processi</span><span class="sxs-lookup"><span data-stu-id="a12d3-213">Job schedules</span></span>
<span data-ttu-id="a12d3-214">Le risorse "pianificazione dei processi" collegano un runbook a una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="a12d3-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="a12d3-215">Hanno un tipo di **Microsoft.Automation/automationAccounts/jobSchedules** e hello hello seguente struttura.</span><span class="sxs-lookup"><span data-stu-id="a12d3-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have hello hello following structure.</span></span>  <span data-ttu-id="a12d3-216">Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


<span data-ttu-id="a12d3-217">in hello nella tabella seguente vengono descritte le proprietà di Hello per le pianificazioni dei processi.</span><span class="sxs-lookup"><span data-stu-id="a12d3-217">hello properties for job schedules are described in hello following table.</span></span>

| <span data-ttu-id="a12d3-218">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a12d3-218">Property</span></span> | <span data-ttu-id="a12d3-219">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a12d3-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a12d3-220">schedule name</span><span class="sxs-lookup"><span data-stu-id="a12d3-220">schedule name</span></span> |<span data-ttu-id="a12d3-221">Singolo **nome** entità con nome hello della pianificazione di hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-221">Single **name** entity with hello name of hello schedule.</span></span> |
| <span data-ttu-id="a12d3-222">runbook name</span><span class="sxs-lookup"><span data-stu-id="a12d3-222">runbook name</span></span>  |<span data-ttu-id="a12d3-223">Singolo **nome** entità con nome hello di hello runbook.</span><span class="sxs-lookup"><span data-stu-id="a12d3-223">Single **name** entity with hello name of hello runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="a12d3-224">variables</span><span class="sxs-lookup"><span data-stu-id="a12d3-224">Variables</span></span>
<span data-ttu-id="a12d3-225">[Le variabili di automazione Azure](../automation/automation-variables.md) dispone di un tipo di **Microsoft.Automation/automationAccounts/variables** e hello seguente struttura.</span><span class="sxs-lookup"><span data-stu-id="a12d3-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have hello following structure.</span></span>  <span data-ttu-id="a12d3-226">Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

<span data-ttu-id="a12d3-227">Nella hello nella tabella seguente sono descritte le proprietà di Hello per le risorse di variabile.</span><span class="sxs-lookup"><span data-stu-id="a12d3-227">hello properties for variable resources are described in hello following table.</span></span>

| <span data-ttu-id="a12d3-228">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a12d3-228">Property</span></span> | <span data-ttu-id="a12d3-229">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a12d3-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a12d3-230">description</span><span class="sxs-lookup"><span data-stu-id="a12d3-230">description</span></span> | <span data-ttu-id="a12d3-231">Descrizione facoltativa per la variabile hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-231">Optional description for hello variable.</span></span> |
| <span data-ttu-id="a12d3-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="a12d3-232">isEncrypted</span></span> | <span data-ttu-id="a12d3-233">Specifica se la variabile hello deve essere crittografata.</span><span class="sxs-lookup"><span data-stu-id="a12d3-233">Specifies whether hello variable should be encrypted.</span></span> |
| <span data-ttu-id="a12d3-234">type</span><span class="sxs-lookup"><span data-stu-id="a12d3-234">type</span></span> | <span data-ttu-id="a12d3-235">Questa proprietà attualmente non ha alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="a12d3-235">This property currently has no effect.</span></span>  <span data-ttu-id="a12d3-236">tipo di dati Hello della variabile hello verrà determinato dal valore iniziale di hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-236">hello data type of hello variable will be determined by hello initial value.</span></span> |
| <span data-ttu-id="a12d3-237">value</span><span class="sxs-lookup"><span data-stu-id="a12d3-237">value</span></span> | <span data-ttu-id="a12d3-238">Valore variabile hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-238">Value for hello variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="a12d3-239">Hello **tipo** proprietà attualmente non ha effetto sulla variabile hello viene creato.</span><span class="sxs-lookup"><span data-stu-id="a12d3-239">hello **type** property currently has no effect on hello variable being created.</span></span>  <span data-ttu-id="a12d3-240">il tipo di dati Hello per variabile hello verrà determinato dal valore hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-240">hello data type for hello variable will be determined by hello value.</span></span>  

<span data-ttu-id="a12d3-241">Se si imposta hello valore iniziale per la variabile di hello, deve essere configurato come tipo di dati corretto hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-241">If you set hello initial value for hello variable, it must be configured as hello correct data type.</span></span>  <span data-ttu-id="a12d3-242">Hello nella tabella seguente fornisce hello diversi tipi di dati consentiti e la relativa sintassi.</span><span class="sxs-lookup"><span data-stu-id="a12d3-242">hello following table provides hello different data types allowable and their syntax.</span></span>  <span data-ttu-id="a12d3-243">Si noti che i valori in JSON sono previsti tooalways essere racchiusi tra virgolette con i caratteri speciali all'interno di virgolette hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-243">Note that values in JSON are expected tooalways be enclosed in quotes with any special characters within hello quotes.</span></span>  <span data-ttu-id="a12d3-244">Ad esempio, sarebbe specificato un valore stringa per le virgolette per racchiudere la stringa hello (utilizzando il carattere di escape hello (\\)) mentre un valore numerico verrà specificato con un set di virgolette.</span><span class="sxs-lookup"><span data-stu-id="a12d3-244">For example, a string value would be specified by quotes around hello string (using hello escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="a12d3-245">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="a12d3-245">Data type</span></span> | <span data-ttu-id="a12d3-246">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a12d3-246">Description</span></span> | <span data-ttu-id="a12d3-247">Esempio</span><span class="sxs-lookup"><span data-stu-id="a12d3-247">Example</span></span> | <span data-ttu-id="a12d3-248">Risolve troppo</span><span class="sxs-lookup"><span data-stu-id="a12d3-248">Resolves too</span></span>|
|:--|:--|:--|:--|
| <span data-ttu-id="a12d3-249">string</span><span class="sxs-lookup"><span data-stu-id="a12d3-249">string</span></span>   | <span data-ttu-id="a12d3-250">Racchiude il valore tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="a12d3-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="a12d3-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="a12d3-251">"\"Hello world\""</span></span> | <span data-ttu-id="a12d3-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="a12d3-252">"Hello world"</span></span> |
| <span data-ttu-id="a12d3-253">numeric</span><span class="sxs-lookup"><span data-stu-id="a12d3-253">numeric</span></span>  | <span data-ttu-id="a12d3-254">Valore numerico con virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="a12d3-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="a12d3-255">"64"</span><span class="sxs-lookup"><span data-stu-id="a12d3-255">"64"</span></span> | <span data-ttu-id="a12d3-256">64</span><span class="sxs-lookup"><span data-stu-id="a12d3-256">64</span></span> |
| <span data-ttu-id="a12d3-257">boolean</span><span class="sxs-lookup"><span data-stu-id="a12d3-257">boolean</span></span>  | <span data-ttu-id="a12d3-258">**true** o **false** tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="a12d3-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="a12d3-259">Si noti che questo valore deve essere minuscolo.</span><span class="sxs-lookup"><span data-stu-id="a12d3-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="a12d3-260">"true"</span><span class="sxs-lookup"><span data-stu-id="a12d3-260">"true"</span></span> | <span data-ttu-id="a12d3-261">true</span><span class="sxs-lookup"><span data-stu-id="a12d3-261">true</span></span> |
| <span data-ttu-id="a12d3-262">datetime</span><span class="sxs-lookup"><span data-stu-id="a12d3-262">datetime</span></span> | <span data-ttu-id="a12d3-263">Valore di data serializzato.</span><span class="sxs-lookup"><span data-stu-id="a12d3-263">Serialized date value.</span></span><br><span data-ttu-id="a12d3-264">È possibile utilizzare il cmdlet ConvertTo-Json hello in PowerShell toogenerate questo valore per una determinata data.</span><span class="sxs-lookup"><span data-stu-id="a12d3-264">You can use hello ConvertTo-Json cmdlet in PowerShell toogenerate this value for a particular date.</span></span><br><span data-ttu-id="a12d3-265">Esempio: get-date "5/24/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="a12d3-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="a12d3-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="a12d3-266">ConvertTo-Json</span></span> | <span data-ttu-id="a12d3-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="a12d3-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="a12d3-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="a12d3-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="a12d3-269">Moduli</span><span class="sxs-lookup"><span data-stu-id="a12d3-269">Modules</span></span>
<span data-ttu-id="a12d3-270">La soluzione di gestione non è necessario toodefine [moduli globali](../automation/automation-integration-modules.md) utilizzato dal runbook, poiché sarà sempre disponibile nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="a12d3-270">Your management solution does not need toodefine [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="a12d3-271">È necessario tooinclude una risorsa per qualsiasi altro modulo utilizzato dal runbook.</span><span class="sxs-lookup"><span data-stu-id="a12d3-271">You do need tooinclude a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="a12d3-272">[I moduli di integrazione](../automation/automation-integration-modules.md) dispone di un tipo di **Microsoft.Automation/automationAccounts/modules** e hello seguente struttura.</span><span class="sxs-lookup"><span data-stu-id="a12d3-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have hello following structure.</span></span>  <span data-ttu-id="a12d3-273">Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


<span data-ttu-id="a12d3-274">Nella hello nella tabella seguente sono descritte le proprietà di Hello per le risorse di modulo.</span><span class="sxs-lookup"><span data-stu-id="a12d3-274">hello properties for module resources are described in hello following table.</span></span>

| <span data-ttu-id="a12d3-275">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a12d3-275">Property</span></span> | <span data-ttu-id="a12d3-276">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a12d3-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a12d3-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="a12d3-277">contentLink</span></span> |<span data-ttu-id="a12d3-278">Specifica il contenuto di hello del modulo hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-278">Specifies hello content of hello module.</span></span> <br><br><span data-ttu-id="a12d3-279">URI - Uri toohello contenuto del modulo hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-279">uri - Uri toohello content of hello module.</span></span>  <span data-ttu-id="a12d3-280">Si tratterà di un file con estensione ps1 per i runbook di PowerShell e di script e di un file di runbook grafico esportato per un runbook di Graph.</span><span class="sxs-lookup"><span data-stu-id="a12d3-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="a12d3-281">versione: versione del modulo di hello per il propria rilevamento.</span><span class="sxs-lookup"><span data-stu-id="a12d3-281">version - Version of hello module for your own tracking.</span></span> |

<span data-ttu-id="a12d3-282">runbook Hello dovrebbero dipendere hello modulo risorsa tooensure che ha creato prima di hello runbook.</span><span class="sxs-lookup"><span data-stu-id="a12d3-282">hello runbook should depend on hello module resource tooensure that it's created before hello runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="a12d3-283">Aggiornamento dei moduli</span><span class="sxs-lookup"><span data-stu-id="a12d3-283">Updating modules</span></span>
<span data-ttu-id="a12d3-284">Se si aggiorna una soluzione di gestione che include un runbook che utilizza una pianificazione e hello nuova versione della soluzione ha un nuovo modulo utilizzato dal runbook, runbook hello può utilizzare versione precedente di hello del modulo hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-284">If you update a management solution that includes a runbook that uses a schedule, and hello new version of your solution has a new module used by that runbook, then hello runbook may use hello old version of hello module.</span></span>  <span data-ttu-id="a12d3-285">Si dovrebbero includere hello seguendo i runbook nella soluzione e toorun un processo prima di eventuali altri runbook.</span><span class="sxs-lookup"><span data-stu-id="a12d3-285">You should include hello following runbooks in your solution and create a job toorun them before any other runbooks.</span></span>  <span data-ttu-id="a12d3-286">Ciò garantisce che tutti i moduli vengono aggiornati come hello necessario per i runbook vengono caricati.</span><span class="sxs-lookup"><span data-stu-id="a12d3-286">This will ensure that any modules are updated as required before hello runbooks are loaded.</span></span>

* <span data-ttu-id="a12d3-287">[Aggiornamento ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) verrà verificato che tutti i moduli di hello usati dai runbook nella soluzione siano la versione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of hello modules used by runbooks in your solution are hello latest version.</span></span>  
* <span data-ttu-id="a12d3-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) verrà registrare di nuovo tutti hello pianificazione risorse tooensure che hello runbook collegati toothem con moduli di utilizzare hello più recenti.</span><span class="sxs-lookup"><span data-stu-id="a12d3-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of hello schedule resources tooensure that hello runbooks linked toothem with use hello latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="a12d3-289">Esempio</span><span class="sxs-lookup"><span data-stu-id="a12d3-289">Sample</span></span>
<span data-ttu-id="a12d3-290">Ecco un esempio di una soluzione che includono che include hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="a12d3-290">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="a12d3-291">Runbook.</span><span class="sxs-lookup"><span data-stu-id="a12d3-291">Runbook.</span></span>  <span data-ttu-id="a12d3-292">Si tratta di un runbook di esempio archiviato in un repository GitHub pubblico.</span><span class="sxs-lookup"><span data-stu-id="a12d3-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="a12d3-293">Processo di automazione che avvia runbook hello quando si installa la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-293">Automation job that starts hello runbook when hello solution is installed.</span></span>
- <span data-ttu-id="a12d3-294">Pianificazione e processo pianificato toostart hello runbook a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="a12d3-294">Schedule and job schedule toostart hello runbook at regular intervals.</span></span>
- <span data-ttu-id="a12d3-295">Certificato.</span><span class="sxs-lookup"><span data-stu-id="a12d3-295">Certificate.</span></span>
- <span data-ttu-id="a12d3-296">Credenziali.</span><span class="sxs-lookup"><span data-stu-id="a12d3-296">Credential.</span></span>
- <span data-ttu-id="a12d3-297">Variabile.</span><span class="sxs-lookup"><span data-stu-id="a12d3-297">Variable.</span></span>
- <span data-ttu-id="a12d3-298">Modulo.</span><span class="sxs-lookup"><span data-stu-id="a12d3-298">Module.</span></span>  <span data-ttu-id="a12d3-299">Si tratta di hello [OMSIngestionAPI modulo](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) per la scrittura di dati tooLog Analitica.</span><span class="sxs-lookup"><span data-stu-id="a12d3-299">This is hello [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data tooLog Analytics.</span></span> 

<span data-ttu-id="a12d3-300">esempio utilizza Hello [parametri soluzione standard](operations-management-suite-solutions-solution-file.md#parameters) variabili comunemente utilizzati in una soluzione come anziché valori toohardcoding nelle definizioni di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="a12d3-300">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a><span data-ttu-id="a12d3-301">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a12d3-301">Next steps</span></span>
* <span data-ttu-id="a12d3-302">[Aggiunta di una soluzione di visualizzazione tooyour](operations-management-suite-solutions-resources-views.md) toovisualize raccolti dati.</span><span class="sxs-lookup"><span data-stu-id="a12d3-302">[Add a view tooyour solution](operations-management-suite-solutions-resources-views.md) toovisualize collected data.</span></span>
