---
title: Risorse di automazione di Azure nelle soluzioni OMS | Microsoft Docs
description: Le soluzioni in OMS contengono in genere runbook in Automazione di Azure per automatizzare i processi, ad esempio la raccolta e l'elaborazione dei dati di monitoraggio.  Questo articolo descrive come includere i runbook e le risorse correlate in una soluzione.
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
ms.openlocfilehash: c1909183a33ed03d8165671cff25cc8b83b77733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="adding-azure-automation-resources-to-an-oms-management-solution-preview"></a><span data-ttu-id="fca6b-104">Aggiunta di risorse di automazione di Azure a una soluzione di gestione OMS (anteprima)</span><span class="sxs-lookup"><span data-stu-id="fca6b-104">Adding Azure Automation resources to an OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="fca6b-105">Questa è una documentazione preliminare per la creazione di soluzioni di gestione in OMS attualmente disponibili in versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="fca6b-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="fca6b-106">Qualsiasi schema descritto di seguito è soggetto a modifiche.</span><span class="sxs-lookup"><span data-stu-id="fca6b-106">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="fca6b-107">Le [soluzioni di gestione in OMS](operations-management-suite-solutions.md) contengono in genere runbook in Automazione di Azure per automatizzare i processi, ad esempio la raccolta e l'elaborazione dei dati di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="fca6b-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="fca6b-108">Oltre ai runbook, gli account di Automazione includono asset come le variabili e le pianificazioni che supportano i runbook usati nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-108">In addition to runbooks, Automation accounts includes assets such as variables and schedules that support the runbooks used in the solution.</span></span>  <span data-ttu-id="fca6b-109">Questo articolo descrive come includere i runbook e le risorse correlate in una soluzione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-109">This article describes how to include runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="fca6b-110">Gli esempi in questo articolo usano parametri e variabili che sono richiesti o comuni nelle soluzioni di gestione e che sono descritti in [Creazione di soluzioni di gestione in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="fca6b-110">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="fca6b-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fca6b-111">Prerequisites</span></span>
<span data-ttu-id="fca6b-112">Nell'articolo si presuppone che il lettore abbia già familiarità con le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fca6b-112">This article assumes that you're already familiar with the following information.</span></span>

- <span data-ttu-id="fca6b-113">Come [creare una soluzione di gestione](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="fca6b-113">How to [create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="fca6b-114">La struttura di un [file di soluzione](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="fca6b-114">The structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="fca6b-115">Come [creare modelli di Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="fca6b-115">How to [author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="fca6b-116">Account di Automazione</span><span class="sxs-lookup"><span data-stu-id="fca6b-116">Automation account</span></span>
<span data-ttu-id="fca6b-117">Tutte le risorse di Automazione di Azure sono contenute in un [account di Automazione](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="fca6b-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="fca6b-118">Come descritto in [Area di lavoro OMS e account di Automazione](operations-management-suite-solutions.md#oms-workspace-and-automation-account), l'account di Automazione non è incluso nella soluzione di gestione, ma deve essere presente prima dell'installazione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the Automation account isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="fca6b-119">Se non è disponibile, l'installazione della soluzione non riuscirà.</span><span class="sxs-lookup"><span data-stu-id="fca6b-119">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="fca6b-120">Il nome di ogni risorsa di automazione include il nome del rispettivo account di automazione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-120">The name of each Automation resource includes the name of its Automation account.</span></span>  <span data-ttu-id="fca6b-121">Questa operazione viene eseguita nella soluzione con il parametro **accountName** come nell'esempio seguente di una risorsa runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-121">This is done in the solution with the **accountName** parameter as in the following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="fca6b-122">Runbook</span><span class="sxs-lookup"><span data-stu-id="fca6b-122">Runbooks</span></span>
<span data-ttu-id="fca6b-123">È consigliabile includere nel file di soluzione eventuali runbook usati dalla soluzione, in modo che vengano creati nel momento in cui viene installata la soluzione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-123">You should include any runbooks used by the solution in the solution file so that they're created when the solution is installed.</span></span>  <span data-ttu-id="fca6b-124">Non è possibile, tuttavia, contenere il corpo del runbook nel modello ed è quindi necessario pubblicare il runbook in una posizione pubblica a cui può accedere qualsiasi utente che installa la soluzione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-124">You cannot contain the body of the runbook in the template though, so you should publish the runbook to a public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="fca6b-125">Le risorse [runbook di automazione di Azure](../automation/automation-runbook-types.md) sono di tipo **Microsoft.Automation/automationAccounts/runbooks** e presentano la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have the following structure.</span></span> <span data-ttu-id="fca6b-126">Nella struttura sono inclusi parametri e variabili comuni ed è quindi possibile copiare e incollare questo frammento di codice nel file della soluzione e, se necessario, modificare i nomi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="fca6b-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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


<span data-ttu-id="fca6b-127">Le proprietà dei runbook sono descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-127">The properties for runbooks are described in the following table.</span></span>

| <span data-ttu-id="fca6b-128">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fca6b-128">Property</span></span> | <span data-ttu-id="fca6b-129">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fca6b-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fca6b-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="fca6b-130">runbookType</span></span> |<span data-ttu-id="fca6b-131">Specifica il tipo del runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-131">Specifies the types of the runbook.</span></span> <br><br> <span data-ttu-id="fca6b-132">Script - Script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="fca6b-132">Script - PowerShell script</span></span> <br><span data-ttu-id="fca6b-133">PowerShell - Flusso di lavoro di PowerShell</span><span class="sxs-lookup"><span data-stu-id="fca6b-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="fca6b-134">GraphPowerShell - Runbook di script di PowerShell grafico</span><span class="sxs-lookup"><span data-stu-id="fca6b-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="fca6b-135">GraphPowerShellWorkflow - Runbook di flusso di lavoro di PowerShell grafico</span><span class="sxs-lookup"><span data-stu-id="fca6b-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="fca6b-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="fca6b-136">logProgress</span></span> |<span data-ttu-id="fca6b-137">Specifica se devono essere generati [record di avanzamento](../automation/automation-runbook-output-and-messages.md) per il runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="fca6b-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="fca6b-138">logVerbose</span></span> |<span data-ttu-id="fca6b-139">Specifica se devono essere generati [record dettagliati](../automation/automation-runbook-output-and-messages.md) per il runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="fca6b-140">description</span><span class="sxs-lookup"><span data-stu-id="fca6b-140">description</span></span> |<span data-ttu-id="fca6b-141">Descrizione facoltativa per il runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-141">Optional description for the runbook.</span></span> |
| <span data-ttu-id="fca6b-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="fca6b-142">publishContentLink</span></span> |<span data-ttu-id="fca6b-143">Specifica il contenuto del runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-143">Specifies the content of the runbook.</span></span> <br><br><span data-ttu-id="fca6b-144">uri - URI del contenuto del runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-144">uri - Uri to the content of the runbook.</span></span>  <span data-ttu-id="fca6b-145">Si tratterà di un file con estensione ps1 per i runbook di PowerShell e di script e di un file di runbook grafico esportato per un runbook di Graph.</span><span class="sxs-lookup"><span data-stu-id="fca6b-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="fca6b-146">version - Versione del runbook per il monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="fca6b-146">version - Version of the runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="fca6b-147">Processi di Automazione</span><span class="sxs-lookup"><span data-stu-id="fca6b-147">Automation jobs</span></span>
<span data-ttu-id="fca6b-148">Quando si avvia un runbook in Automazione di Azure, viene creato un processo di automazione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="fca6b-149">È possibile aggiungere una risorsa "processo di automazione" alla soluzione per consentire l'avvio automatico di un runbook nel momento in cui viene installata la soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-149">You can add an automation job resource to your solution to automatically start a runbook when the management solution is installed.</span></span>  <span data-ttu-id="fca6b-150">Questo metodo, in genere, viene adottato per avviare i runbook usati per la configurazione iniziale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-150">This method is typically used to start runbooks that are used for initial configuration of the solution.</span></span>  <span data-ttu-id="fca6b-151">Per avviare un runbook a intervalli regolari, creare una [pianificazione](#schedules) e una [pianificazione processi](#job-schedules).</span><span class="sxs-lookup"><span data-stu-id="fca6b-151">To start a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="fca6b-152">Le risorse "processo" sono di tipo **Microsoft.Automation/automationAccounts/jobs** e presentano la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have the following structure.</span></span>  <span data-ttu-id="fca6b-153">Nella struttura sono inclusi parametri e variabili comuni ed è quindi possibile copiare e incollare questo frammento di codice nel file della soluzione e, se necessario, modificare i nomi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="fca6b-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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

<span data-ttu-id="fca6b-154">Le proprietà dei processi di automazione sono descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-154">The properties for automation jobs are described in the following table.</span></span>

| <span data-ttu-id="fca6b-155">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fca6b-155">Property</span></span> | <span data-ttu-id="fca6b-156">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fca6b-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fca6b-157">runbook</span><span class="sxs-lookup"><span data-stu-id="fca6b-157">runbook</span></span> |<span data-ttu-id="fca6b-158">Entità name singola con il nome del runbook da avviare.</span><span class="sxs-lookup"><span data-stu-id="fca6b-158">Single name entity with the name of the runbook to start.</span></span> |
| <span data-ttu-id="fca6b-159">parameters</span><span class="sxs-lookup"><span data-stu-id="fca6b-159">parameters</span></span> |<span data-ttu-id="fca6b-160">Entità relativa ad ogni valore di parametro richiesto dal runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-160">Entity for each parameter value required by the runbook.</span></span> |

<span data-ttu-id="fca6b-161">Il processo include il nome del runbook e i valori dei parametri da inviare al runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-161">The job includes the runbook name and any parameter values to be sent to the runbook.</span></span>  <span data-ttu-id="fca6b-162">Il processo deve [dipendere](operations-management-suite-solutions-solution-file.md#resources) dal runbook in fase di avvio, poiché questo deve essere creato prima del processo.</span><span class="sxs-lookup"><span data-stu-id="fca6b-162">The job should [depend on](operations-management-suite-solutions-solution-file.md#resources) the runbook that it's starting since the runbook must be created before the job.</span></span>  <span data-ttu-id="fca6b-163">Se sono presenti più runbook da avviare, è possibile definire l'ordine di avvio impostando un processo in modo che dipenda da un altro processo che deve essere eseguito prima.</span><span class="sxs-lookup"><span data-stu-id="fca6b-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="fca6b-164">Il nome di una risorsa processo deve contenere un GUID che viene in genere assegnato da un parametro.</span><span class="sxs-lookup"><span data-stu-id="fca6b-164">The name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="fca6b-165">Altre informazioni sui parametri GUID sono disponibili in [Creazione di soluzioni di gestione in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="fca6b-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="fca6b-166">Certificati</span><span class="sxs-lookup"><span data-stu-id="fca6b-166">Certificates</span></span>
<span data-ttu-id="fca6b-167">I [certificati di automazione di Azure](../automation/automation-certificates.md) sono di tipo **Microsoft.Automation/automationAccounts/certificates** e presentano la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have the following structure.</span></span> <span data-ttu-id="fca6b-168">Nella struttura sono inclusi parametri e variabili comuni ed è quindi possibile copiare e incollare questo frammento di codice nel file della soluzione e, se necessario, modificare i nomi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="fca6b-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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



<span data-ttu-id="fca6b-169">Le proprietà delle risorse "certificati" sono descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-169">The properties for Certificates resources are described in the following table.</span></span>

| <span data-ttu-id="fca6b-170">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fca6b-170">Property</span></span> | <span data-ttu-id="fca6b-171">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fca6b-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fca6b-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="fca6b-172">base64Value</span></span> |<span data-ttu-id="fca6b-173">Valore Base 64 per il certificato.</span><span class="sxs-lookup"><span data-stu-id="fca6b-173">Base 64 value for the certificate.</span></span> |
| <span data-ttu-id="fca6b-174">thumbprint</span><span class="sxs-lookup"><span data-stu-id="fca6b-174">thumbprint</span></span> |<span data-ttu-id="fca6b-175">Identificazione personale del certificato.</span><span class="sxs-lookup"><span data-stu-id="fca6b-175">Thumbprint for the certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="fca6b-176">Credenziali</span><span class="sxs-lookup"><span data-stu-id="fca6b-176">Credentials</span></span>
<span data-ttu-id="fca6b-177">Le [credenziali di automazione di Azure](../automation/automation-credentials.md) sono di tipo **Microsoft.Automation/automationAccounts/credentials** e presentano la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have the following structure.</span></span>  <span data-ttu-id="fca6b-178">Nella struttura sono inclusi parametri e variabili comuni ed è quindi possibile copiare e incollare questo frammento di codice nel file della soluzione e, se necessario, modificare i nomi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="fca6b-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


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

<span data-ttu-id="fca6b-179">Le proprietà delle risorse "credenziali" sono descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-179">The properties for Credential resources are described in the following table.</span></span>

| <span data-ttu-id="fca6b-180">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fca6b-180">Property</span></span> | <span data-ttu-id="fca6b-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fca6b-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fca6b-182">userName</span><span class="sxs-lookup"><span data-stu-id="fca6b-182">userName</span></span> |<span data-ttu-id="fca6b-183">Nome utente per la credenziale.</span><span class="sxs-lookup"><span data-stu-id="fca6b-183">User name for the credential.</span></span> |
| <span data-ttu-id="fca6b-184">password</span><span class="sxs-lookup"><span data-stu-id="fca6b-184">password</span></span> |<span data-ttu-id="fca6b-185">Password per la credenziale.</span><span class="sxs-lookup"><span data-stu-id="fca6b-185">Password for the credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="fca6b-186">Pianificazioni</span><span class="sxs-lookup"><span data-stu-id="fca6b-186">Schedules</span></span>
<span data-ttu-id="fca6b-187">Le [pianificazioni di automazione di Azure](../automation/automation-schedules.md) sono di tipo **Microsoft.Automation/automationAccounts/schedules** e presentano la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have the the following structure.</span></span> <span data-ttu-id="fca6b-188">Nella struttura sono inclusi parametri e variabili comuni ed è quindi possibile copiare e incollare questo frammento di codice nel file della soluzione e, se necessario, modificare i nomi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="fca6b-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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

<span data-ttu-id="fca6b-189">Le proprietà delle risorse pianificazione sono descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-189">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="fca6b-190">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fca6b-190">Property</span></span> | <span data-ttu-id="fca6b-191">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fca6b-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fca6b-192">description</span><span class="sxs-lookup"><span data-stu-id="fca6b-192">description</span></span> |<span data-ttu-id="fca6b-193">Descrizione facoltativa per la pianificazione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-193">Optional description for the schedule.</span></span> |
| <span data-ttu-id="fca6b-194">startTime</span><span class="sxs-lookup"><span data-stu-id="fca6b-194">startTime</span></span> |<span data-ttu-id="fca6b-195">Specifica l'ora di inizio di una pianificazione come oggetto DateTime.</span><span class="sxs-lookup"><span data-stu-id="fca6b-195">Specifies the start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="fca6b-196">È possibile fornire una stringa, se può essere convertita in un oggetto DateTime valido.</span><span class="sxs-lookup"><span data-stu-id="fca6b-196">A string can be provided if it can be converted to a valid DateTime.</span></span> |
| <span data-ttu-id="fca6b-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="fca6b-197">isEnabled</span></span> |<span data-ttu-id="fca6b-198">Specifica se la pianificazione è abilitata.</span><span class="sxs-lookup"><span data-stu-id="fca6b-198">Specifies whether the schedule is enabled.</span></span> |
| <span data-ttu-id="fca6b-199">interval</span><span class="sxs-lookup"><span data-stu-id="fca6b-199">interval</span></span> |<span data-ttu-id="fca6b-200">Tipo di intervallo per la pianificazione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-200">The type of interval for the schedule.</span></span><br><br><span data-ttu-id="fca6b-201">day</span><span class="sxs-lookup"><span data-stu-id="fca6b-201">day</span></span><br><span data-ttu-id="fca6b-202">hour</span><span class="sxs-lookup"><span data-stu-id="fca6b-202">hour</span></span> |
| <span data-ttu-id="fca6b-203">frequency</span><span class="sxs-lookup"><span data-stu-id="fca6b-203">frequency</span></span> |<span data-ttu-id="fca6b-204">Frequenza con cui la pianificazione deve essere attivata, in numero di ore o giorni.</span><span class="sxs-lookup"><span data-stu-id="fca6b-204">Frequency that the schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="fca6b-205">Per le pianificazioni deve essere definita un'ora di avvio con un valore successivo all'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-205">Schedules must have a start time with a value greater than the current time.</span></span>  <span data-ttu-id="fca6b-206">Non è possibile specificare questo valore con una variabile poiché non è possibile sapere quando verrà installata la soluzione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-206">You cannot provide this value with a variable since you would have no way of knowing when it's going to be installed.</span></span>

<span data-ttu-id="fca6b-207">Applicare una delle due strategie seguenti quando si usano risorse di pianificazione in una soluzione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-207">Use one of the following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="fca6b-208">Usare un parametro per l'ora di avvio della pianificazione:</span><span class="sxs-lookup"><span data-stu-id="fca6b-208">Use a parameter for the start time of the schedule.</span></span>  <span data-ttu-id="fca6b-209">all'utente verrà richiesto di specificare un valore durante l'installazione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-209">This will prompt the user to provide a value when they install the solution.</span></span>  <span data-ttu-id="fca6b-210">In caso di più pianificazioni, è possibile usare un unico valore di parametro anche per più di esse.</span><span class="sxs-lookup"><span data-stu-id="fca6b-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="fca6b-211">Creare le pianificazioni usando un runbook che viene avviato al momento dell'installazione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-211">Create the schedules using a runbook that starts when the solution is installed.</span></span>  <span data-ttu-id="fca6b-212">In questo modo viene eliminata la necessità per l'utente di specificare un'ora, ma la pianificazione non potrà essere contenuta nella soluzione e verrà quindi rimossa con l'eliminazione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-212">This removes the requirement of the user to specify a time, but you can't contain the schedule in your solution so it will be removed when the solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="fca6b-213">Pianificazioni dei processi</span><span class="sxs-lookup"><span data-stu-id="fca6b-213">Job schedules</span></span>
<span data-ttu-id="fca6b-214">Le risorse "pianificazione dei processi" collegano un runbook a una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="fca6b-215">Sono di tipo **Microsoft.Automation/automationAccounts/jobSchedules** e presentano la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have the the following structure.</span></span>  <span data-ttu-id="fca6b-216">Nella struttura sono inclusi parametri e variabili comuni ed è quindi possibile copiare e incollare questo frammento di codice nel file della soluzione e, se necessario, modificare i nomi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="fca6b-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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


<span data-ttu-id="fca6b-217">Le proprietà delle pianificazioni dei processi sono descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-217">The properties for job schedules are described in the following table.</span></span>

| <span data-ttu-id="fca6b-218">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fca6b-218">Property</span></span> | <span data-ttu-id="fca6b-219">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fca6b-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fca6b-220">schedule name</span><span class="sxs-lookup"><span data-stu-id="fca6b-220">schedule name</span></span> |<span data-ttu-id="fca6b-221">Entità **name** singola con il nome della pianificazione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-221">Single **name** entity with the name of the schedule.</span></span> |
| <span data-ttu-id="fca6b-222">runbook name</span><span class="sxs-lookup"><span data-stu-id="fca6b-222">runbook name</span></span>  |<span data-ttu-id="fca6b-223">Entità **name** singola con il nome del runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-223">Single **name** entity with the name of the runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="fca6b-224">Variabili</span><span class="sxs-lookup"><span data-stu-id="fca6b-224">Variables</span></span>
<span data-ttu-id="fca6b-225">Le [variabili di automazione di Azure](../automation/automation-variables.md) sono di tipo **Microsoft.Automation/automationAccounts/variables** e presentano la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have the following structure.</span></span>  <span data-ttu-id="fca6b-226">Nella struttura sono inclusi parametri e variabili comuni ed è quindi possibile copiare e incollare questo frammento di codice nel file della soluzione e, se necessario, modificare i nomi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="fca6b-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

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

<span data-ttu-id="fca6b-227">Le proprietà delle risorse "variabile" sono descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-227">The properties for variable resources are described in the following table.</span></span>

| <span data-ttu-id="fca6b-228">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fca6b-228">Property</span></span> | <span data-ttu-id="fca6b-229">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fca6b-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fca6b-230">description</span><span class="sxs-lookup"><span data-stu-id="fca6b-230">description</span></span> | <span data-ttu-id="fca6b-231">Descrizione facoltativa per la variabile.</span><span class="sxs-lookup"><span data-stu-id="fca6b-231">Optional description for the variable.</span></span> |
| <span data-ttu-id="fca6b-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="fca6b-232">isEncrypted</span></span> | <span data-ttu-id="fca6b-233">Specifica se la variabile deve essere crittografata.</span><span class="sxs-lookup"><span data-stu-id="fca6b-233">Specifies whether the variable should be encrypted.</span></span> |
| <span data-ttu-id="fca6b-234">type</span><span class="sxs-lookup"><span data-stu-id="fca6b-234">type</span></span> | <span data-ttu-id="fca6b-235">Questa proprietà attualmente non ha alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="fca6b-235">This property currently has no effect.</span></span>  <span data-ttu-id="fca6b-236">Il tipo di dati della variabile verrà determinato dal valore iniziale.</span><span class="sxs-lookup"><span data-stu-id="fca6b-236">The data type of the variable will be determined by the initial value.</span></span> |
| <span data-ttu-id="fca6b-237">value</span><span class="sxs-lookup"><span data-stu-id="fca6b-237">value</span></span> | <span data-ttu-id="fca6b-238">Valore per la variabile.</span><span class="sxs-lookup"><span data-stu-id="fca6b-238">Value for the variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="fca6b-239">La proprietà **type** attualmente non ha alcun effetto sulla variabile che viene creata.</span><span class="sxs-lookup"><span data-stu-id="fca6b-239">The **type** property currently has no effect on the variable being created.</span></span>  <span data-ttu-id="fca6b-240">Il tipo di dati per la variabile verrà determinato dal valore.</span><span class="sxs-lookup"><span data-stu-id="fca6b-240">The data type for the variable will be determined by the value.</span></span>  

<span data-ttu-id="fca6b-241">Se si imposta il valore iniziale per la variabile, è necessario configurarla come tipo di dati corretto.</span><span class="sxs-lookup"><span data-stu-id="fca6b-241">If you set the initial value for the variable, it must be configured as the correct data type.</span></span>  <span data-ttu-id="fca6b-242">La tabella seguente elenca i diversi tipi di dati disponibili e la rispettiva sintassi.</span><span class="sxs-lookup"><span data-stu-id="fca6b-242">The following table provides the different data types allowable and their syntax.</span></span>  <span data-ttu-id="fca6b-243">Si noti che i valori in JSON devono essere sempre racchiusi tra virgolette con qualsiasi carattere speciale tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="fca6b-243">Note that values in JSON are expected to always be enclosed in quotes with any special characters within the quotes.</span></span>  <span data-ttu-id="fca6b-244">Un valore di stringa, ad esempio, verrà specificato dalle virgolette all'inizio e alla fine della stringa, usando il carattere di escape (\\), mentre un valore numerico verrà specificato con un set di virgolette.</span><span class="sxs-lookup"><span data-stu-id="fca6b-244">For example, a string value would be specified by quotes around the string (using the escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="fca6b-245">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="fca6b-245">Data type</span></span> | <span data-ttu-id="fca6b-246">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fca6b-246">Description</span></span> | <span data-ttu-id="fca6b-247">Esempio</span><span class="sxs-lookup"><span data-stu-id="fca6b-247">Example</span></span> | <span data-ttu-id="fca6b-248">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="fca6b-248">Resolves to</span></span> |
|:--|:--|:--|:--|
| <span data-ttu-id="fca6b-249">string</span><span class="sxs-lookup"><span data-stu-id="fca6b-249">string</span></span>   | <span data-ttu-id="fca6b-250">Racchiude il valore tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="fca6b-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="fca6b-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="fca6b-251">"\"Hello world\""</span></span> | <span data-ttu-id="fca6b-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="fca6b-252">"Hello world"</span></span> |
| <span data-ttu-id="fca6b-253">numeric</span><span class="sxs-lookup"><span data-stu-id="fca6b-253">numeric</span></span>  | <span data-ttu-id="fca6b-254">Valore numerico con virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="fca6b-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="fca6b-255">"64"</span><span class="sxs-lookup"><span data-stu-id="fca6b-255">"64"</span></span> | <span data-ttu-id="fca6b-256">64</span><span class="sxs-lookup"><span data-stu-id="fca6b-256">64</span></span> |
| <span data-ttu-id="fca6b-257">boolean</span><span class="sxs-lookup"><span data-stu-id="fca6b-257">boolean</span></span>  | <span data-ttu-id="fca6b-258">**true** o **false** tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="fca6b-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="fca6b-259">Si noti che questo valore deve essere minuscolo.</span><span class="sxs-lookup"><span data-stu-id="fca6b-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="fca6b-260">"true"</span><span class="sxs-lookup"><span data-stu-id="fca6b-260">"true"</span></span> | <span data-ttu-id="fca6b-261">true</span><span class="sxs-lookup"><span data-stu-id="fca6b-261">true</span></span> |
| <span data-ttu-id="fca6b-262">datetime</span><span class="sxs-lookup"><span data-stu-id="fca6b-262">datetime</span></span> | <span data-ttu-id="fca6b-263">Valore di data serializzato.</span><span class="sxs-lookup"><span data-stu-id="fca6b-263">Serialized date value.</span></span><br><span data-ttu-id="fca6b-264">È possibile usare il cmdlet ConvertTo-Json in PowerShell per generare questo valore per una particolare data.</span><span class="sxs-lookup"><span data-stu-id="fca6b-264">You can use the ConvertTo-Json cmdlet in PowerShell to generate this value for a particular date.</span></span><br><span data-ttu-id="fca6b-265">Esempio: get-date "5/24/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="fca6b-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="fca6b-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="fca6b-266">ConvertTo-Json</span></span> | <span data-ttu-id="fca6b-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="fca6b-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="fca6b-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="fca6b-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="fca6b-269">Moduli</span><span class="sxs-lookup"><span data-stu-id="fca6b-269">Modules</span></span>
<span data-ttu-id="fca6b-270">La soluzione di gestione non deve necessariamente definire i [moduli globali](../automation/automation-integration-modules.md) usati dai runbook, poiché saranno sempre disponibili nel proprio account di automazione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-270">Your management solution does not need to define [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="fca6b-271">È tuttavia necessario includere una risorsa per qualsiasi altro modulo usato dai runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-271">You do need to include a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="fca6b-272">I [moduli di integrazione](../automation/automation-integration-modules.md) sono di tipo **Microsoft.Automation/automationAccounts/modules** e presentano la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have the following structure.</span></span>  <span data-ttu-id="fca6b-273">Nella struttura sono inclusi parametri e variabili comuni ed è quindi possibile copiare e incollare questo frammento di codice nel file della soluzione e, se necessario, modificare i nomi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="fca6b-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

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


<span data-ttu-id="fca6b-274">Le proprietà delle risorse "modulo" sono descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-274">The properties for module resources are described in the following table.</span></span>

| <span data-ttu-id="fca6b-275">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fca6b-275">Property</span></span> | <span data-ttu-id="fca6b-276">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fca6b-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fca6b-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="fca6b-277">contentLink</span></span> |<span data-ttu-id="fca6b-278">Specifica il contenuto del modulo.</span><span class="sxs-lookup"><span data-stu-id="fca6b-278">Specifies the content of the module.</span></span> <br><br><span data-ttu-id="fca6b-279">uri - URI del contenuto del modulo.</span><span class="sxs-lookup"><span data-stu-id="fca6b-279">uri - Uri to the content of the module.</span></span>  <span data-ttu-id="fca6b-280">Si tratterà di un file con estensione ps1 per i runbook di PowerShell e di script e di un file di runbook grafico esportato per un runbook di Graph.</span><span class="sxs-lookup"><span data-stu-id="fca6b-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="fca6b-281">version - Versione del modulo per il monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="fca6b-281">version - Version of the module for your own tracking.</span></span> |

<span data-ttu-id="fca6b-282">Il runbook deve dipendere dalla risorsa "modulo" affinché la risorsa venga creata prima del runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-282">The runbook should depend on the module resource to ensure that it's created before the runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="fca6b-283">Aggiornamento dei moduli</span><span class="sxs-lookup"><span data-stu-id="fca6b-283">Updating modules</span></span>
<span data-ttu-id="fca6b-284">Se si aggiorna una soluzione di gestione che include un runbook che usa una pianificazione e la nuova versione della soluzione ha un nuovo modulo usato dal runbook, il runbook potrebbe usare la versione precedente del modulo.</span><span class="sxs-lookup"><span data-stu-id="fca6b-284">If you update a management solution that includes a runbook that uses a schedule, and the new version of your solution has a new module used by that runbook, then the runbook may use the old version of the module.</span></span>  <span data-ttu-id="fca6b-285">È necessario includere i runbook seguenti nella soluzione e creare un processo per eseguirli prima di qualsiasi altro runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-285">You should include the following runbooks in your solution and create a job to run them before any other runbooks.</span></span>  <span data-ttu-id="fca6b-286">In questo modo, tutti i moduli verranno aggiornati come necessario prima del caricamento del runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-286">This will ensure that any modules are updated as required before the runbooks are loaded.</span></span>

* <span data-ttu-id="fca6b-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) garantisce che tutti i moduli usati dal runbook nella soluzione siano della versione più recente.</span><span class="sxs-lookup"><span data-stu-id="fca6b-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of the modules used by runbooks in your solution are the latest version.</span></span>  
* <span data-ttu-id="fca6b-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) esegue nuovamente la registrazione di tutte le risorse pianificazione per garantire che i runbook collegati useranno i moduli più recenti.</span><span class="sxs-lookup"><span data-stu-id="fca6b-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of the schedule resources to ensure that the runbooks linked to them with use the latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="fca6b-289">Esempio</span><span class="sxs-lookup"><span data-stu-id="fca6b-289">Sample</span></span>
<span data-ttu-id="fca6b-290">Di seguito è riportato un esempio di soluzione che include le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="fca6b-290">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="fca6b-291">Runbook.</span><span class="sxs-lookup"><span data-stu-id="fca6b-291">Runbook.</span></span>  <span data-ttu-id="fca6b-292">Si tratta di un runbook di esempio archiviato in un repository GitHub pubblico.</span><span class="sxs-lookup"><span data-stu-id="fca6b-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="fca6b-293">Processo di automazione che avvia il runbook quando viene installata la soluzione.</span><span class="sxs-lookup"><span data-stu-id="fca6b-293">Automation job that starts the runbook when the solution is installed.</span></span>
- <span data-ttu-id="fca6b-294">Pianificazione e pianificazione dei processi per avviare il runbook a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="fca6b-294">Schedule and job schedule to start the runbook at regular intervals.</span></span>
- <span data-ttu-id="fca6b-295">Certificato.</span><span class="sxs-lookup"><span data-stu-id="fca6b-295">Certificate.</span></span>
- <span data-ttu-id="fca6b-296">Credenziali.</span><span class="sxs-lookup"><span data-stu-id="fca6b-296">Credential.</span></span>
- <span data-ttu-id="fca6b-297">Variabile.</span><span class="sxs-lookup"><span data-stu-id="fca6b-297">Variable.</span></span>
- <span data-ttu-id="fca6b-298">Modulo.</span><span class="sxs-lookup"><span data-stu-id="fca6b-298">Module.</span></span>  <span data-ttu-id="fca6b-299">Si tratta del [modulo OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) per la scrittura di dati in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fca6b-299">This is the [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data to Log Analytics.</span></span> 

<span data-ttu-id="fca6b-300">L'esempio usa variabili dei [parametri di soluzione standard](operations-management-suite-solutions-solution-file.md#parameters) comunemente usate in una soluzione, anziché impostare i valori come hardcoded nelle definizioni delle risorse.</span><span class="sxs-lookup"><span data-stu-id="fca6b-300">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>


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
            "description": "GUID for the schedule link to runbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the runbook job.",
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




## <a name="next-steps"></a><span data-ttu-id="fca6b-301">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fca6b-301">Next steps</span></span>
* <span data-ttu-id="fca6b-302">[Aggiungere una vista alla soluzione](operations-management-suite-solutions-resources-views.md) per visualizzare i dati raccolti.</span><span class="sxs-lookup"><span data-stu-id="fca6b-302">[Add a view to your solution](operations-management-suite-solutions-resources-views.md) to visualize collected data.</span></span>
