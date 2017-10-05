---
title: Gestire le risorse con l'interfaccia della riga di comando di Azure | Documentazione Microsoft
description: Usare l'interfaccia della riga di comando di Azure per gestire le risorse e i gruppi di Azure
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3ad4e68b90979fd7f9d3ddf5278e65e19cb07152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-cli-to-manage-azure-resources-and-resource-groups"></a><span data-ttu-id="b46f3-103">Usare l'interfaccia della riga di comando di Azure per gestire risorse e gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="b46f3-103">Use the Azure CLI to manage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b46f3-104">Portale</span><span class="sxs-lookup"><span data-stu-id="b46f3-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="b46f3-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b46f3-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="b46f3-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b46f3-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="b46f3-107">API REST</span><span class="sxs-lookup"><span data-stu-id="b46f3-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="b46f3-108">L'interfaccia della riga di comando di Azure è uno degli strumenti che è possibile usare per distribuire e gestire le risorse con Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b46f3-108">The Azure Command-Line Interface (Azure CLI) is one of several tools you can use to deploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="b46f3-109">Questo articolo illustra i metodi comuni per gestire risorse e gruppi di risorse di Azure usando l'interfaccia della riga di comando di Azure in modalità Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b46f3-109">This article introduces common ways to manage Azure resources and resource groups by using the Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="b46f3-110">Per informazioni sull'uso dell'interfaccia della riga di comando per distribuire le risorse, vedere [Distribuire le risorse con i modelli di Azure Resource Manager e l'interfaccia della riga di comando di Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b46f3-110">For information about using the CLI to deploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="b46f3-111">Per informazioni sulle risorse di Azure e su Resource Manager, vedere [Panoramica di Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b46f3-111">For background about Azure resources and Resource Manager, visit the [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b46f3-112">Per gestire le risorse di Azure con l'interfaccia della riga di comando di Azure, è necessario [installare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md) e [accedere ad Azure](../xplat-cli-connect.md) usando il comando `azure login`.</span><span class="sxs-lookup"><span data-stu-id="b46f3-112">To manage Azure resources with the Azure CLI, you need to [install the Azure CLI](../cli-install-nodejs.md), and [log in to Azure](../xplat-cli-connect.md) by using the `azure login` command.</span></span> <span data-ttu-id="b46f3-113">Verificare che l'interfaccia della riga di comando sia in modalità Resource Manager eseguendo `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="b46f3-113">Make sure the CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="b46f3-114">Se queste operazioni sono già state eseguite, si è pronti per proseguire.</span><span class="sxs-lookup"><span data-stu-id="b46f3-114">If you've done these things, you're ready to go.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="b46f3-115">Ottenere le risorse e i gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="b46f3-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="b46f3-116">Gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="b46f3-116">Resource groups</span></span>
<span data-ttu-id="b46f3-117">Per ottenere un elenco di tutti i gruppi di risorse della sottoscrizione e delle rispettive posizioni, eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="b46f3-117">To get a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="b46f3-118">Risorse</span><span class="sxs-lookup"><span data-stu-id="b46f3-118">Resources</span></span>
 <span data-ttu-id="b46f3-119">Per elencare tutte le risorse in un gruppo, ad esempio nel gruppo con nome *testRG*, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b46f3-119">To list all resources in a group, such as one with name *testRG*, use the following command:</span></span>

    azure resource list testRG

<span data-ttu-id="b46f3-120">Per visualizzare una singola risorsa nel gruppo, ad esempio una VM denominata *MyUbuntuVM*, usare un comando come il seguente:</span><span class="sxs-lookup"><span data-stu-id="b46f3-120">To view an individual resource within the group, such as a VM named *MyUbuntuVM*, use a command like the following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="b46f3-121">Notare il parametro **Microsoft.Compute/virtualMachines**.</span><span class="sxs-lookup"><span data-stu-id="b46f3-121">Notice the **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="b46f3-122">Questo parametro indica il tipo di risorsa per il quale si stanno richiedendo informazioni.</span><span class="sxs-lookup"><span data-stu-id="b46f3-122">This parameter indicates the type of the resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="b46f3-123">Quando si usano i comandi **azure resource**, a eccezione di **list**, è necessario specificare la versione dell'API della risorsa con il parametro **-o**.</span><span class="sxs-lookup"><span data-stu-id="b46f3-123">When using the **azure resource** commands other than the **list** command, you must specify the API version of the resource with the **-o** parameter.</span></span> <span data-ttu-id="b46f3-124">Se non si è certi della versione dell'API, consultare il file modello e trovare il campo apiVersion relativo alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="b46f3-124">If you're unsure about the API version, consult the template file and find the apiVersion field for the resource.</span></span> <span data-ttu-id="b46f3-125">Per altre informazioni sulle versioni dell'API in Resource Manager, vedere [Provider e tipi di risorse](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="b46f3-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="b46f3-126">Quando si visualizzano i dettagli su una risorsa, è spesso utile utilizzare il parametro`--json`.</span><span class="sxs-lookup"><span data-stu-id="b46f3-126">When viewing details on a resource, it is often useful to use the `--json` parameter.</span></span> <span data-ttu-id="b46f3-127">Questo parametro rende l'output più leggibile perché alcuni valori sono strutture annidate o raccolte.</span><span class="sxs-lookup"><span data-stu-id="b46f3-127">This parameter makes the output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="b46f3-128">L'esempio seguente illustra come restituire i risultati del comando **show** come un documento JSON.</span><span class="sxs-lookup"><span data-stu-id="b46f3-128">The following example demonstrates returning the results of the **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="b46f3-129">Se necessario, salvare i dati JSON nel file usando il carattere &gt; per indirizzare l'output a un file.</span><span class="sxs-lookup"><span data-stu-id="b46f3-129">If you want, save the JSON data to file by using the &gt; character to direct the output to a file.</span></span> <span data-ttu-id="b46f3-130">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b46f3-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="b46f3-131">Tag</span><span class="sxs-lookup"><span data-stu-id="b46f3-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="b46f3-132">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="b46f3-132">Manage resources</span></span>
<span data-ttu-id="b46f3-133">Per aggiungere una risorsa, ad esempio un account di archiviazione, a un gruppo di risorse, eseguire un comando simile a:</span><span class="sxs-lookup"><span data-stu-id="b46f3-133">To add a resource such as a storage account to a resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="b46f3-134">Oltre a specificare la versione dell'API della risorsa con il parametro **-o**, usare il parametro **-p** per passare una stringa in formato JSON con le proprietà obbligatorie o aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="b46f3-134">In addition to specifying the API version of the resource with the **-o** parameter, use the **-p** parameter to pass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="b46f3-135">Per eliminare una risorsa esistente, ad esempio una macchina virtuale, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b46f3-135">To delete an existing resource such as a virtual machine resource, use a command like the following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="b46f3-136">Per spostare le risorse esistenti in un gruppo di risorse o una sottoscrizione diversa, usare il comando **azure resource move** .</span><span class="sxs-lookup"><span data-stu-id="b46f3-136">To move existing resources to another resource group or subscription, use the **azure resource move** command.</span></span> <span data-ttu-id="b46f3-137">Il seguente esempio illustra come spostare una cache Redis in un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b46f3-137">The following example shows how to move a Redis Cache to a new resource group.</span></span> <span data-ttu-id="b46f3-138">Nel parametro **-i** , fornire un elenco delimitato da virgole di id di risorsa da spostare.</span><span class="sxs-lookup"><span data-stu-id="b46f3-138">In the **-i** parameter, provide a comma-separated list of the resource id's to move.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-to-resources"></a><span data-ttu-id="b46f3-139">Controllare l'accesso alle risorse</span><span class="sxs-lookup"><span data-stu-id="b46f3-139">Control access to resources</span></span>
<span data-ttu-id="b46f3-140">È possibile usare l'interfaccia della riga di comando di Azure per creare e gestire i criteri per controllare l'accesso alle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b46f3-140">You can use the Azure CLI to create and manage policies to control access to Azure resources.</span></span> <span data-ttu-id="b46f3-141">Per informazioni sulle definizioni dei criteri e sull'assegnazione di criteri alle risorse, vedere [Usare i criteri per gestire le risorse e controllare l'accesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b46f3-141">For background about policy definitions and assigning policies to resources, see [Use policy to manage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="b46f3-142">Ad esempio, definire i criteri seguenti per rifiutare tutte le richieste in cui la località non è Stati Uniti occidentali o Stati Uniti centro-settentrionali e salvarli nel file di definizione dei criteri policy.json:</span><span class="sxs-lookup"><span data-stu-id="b46f3-142">For example, define the following policy to deny all requests where location is not West US or North Central US, and save it to the policy definition file policy.json:</span></span>

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

<span data-ttu-id="b46f3-143">Eseguire quindi il comando **policy definition create**:</span><span class="sxs-lookup"><span data-stu-id="b46f3-143">Then run the **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="b46f3-144">Questo comando ha un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b46f3-144">This command shows output similar to the following:</span></span>

    + <span data-ttu-id="b46f3-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="b46f3-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="b46f3-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="b46f3-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="b46f3-147">Per assegnare un criterio nell'ambito desiderato, usare il valore di **PolicyDefinitionId** restituito dal comando precedente.</span><span class="sxs-lookup"><span data-stu-id="b46f3-147">To assign a policy at the scope you want, use the **PolicyDefinitionId** returned from the previous command.</span></span> <span data-ttu-id="b46f3-148">Nell'esempio seguente, questo ambito è la sottoscrizione, ma è possibile impostare come ambito gruppi di risorse o singole risorse:</span><span class="sxs-lookup"><span data-stu-id="b46f3-148">In the following example, this scope is the subscription, but you can scope to resource groups or individual resources:</span></span>

    <span data-ttu-id="b46f3-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="b46f3-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="b46f3-150">È possibile ottenere, modificare o rimuovere le definizioni dei criteri usando i comandi **policy definition show**, **policy definition set** e **policy definition delete**.</span><span class="sxs-lookup"><span data-stu-id="b46f3-150">You can get, change, or remove policy definitions by using the **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="b46f3-151">Analogamente, è possibile ottenere, modificare o rimuovere le assegnazioni dei criteri usando i comandi **policy assignment show**, **policy assignment set** e **policy assignment delete**.</span><span class="sxs-lookup"><span data-stu-id="b46f3-151">Similarly, you can get, change, or remove policy assignments by using the **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="b46f3-152">Esportare un gruppo di risorse come modello</span><span class="sxs-lookup"><span data-stu-id="b46f3-152">Export a resource group as a template</span></span>
<span data-ttu-id="b46f3-153">È possibile visualizzare il modello di Resource Manager per un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="b46f3-153">For an existing resource group, you can view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="b46f3-154">L'esportazione del modello offre due vantaggi:</span><span class="sxs-lookup"><span data-stu-id="b46f3-154">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="b46f3-155">È possibile automatizzare le distribuzioni future della soluzione, perché tutti gli elementi dell'infrastruttura sono definiti nel modello.</span><span class="sxs-lookup"><span data-stu-id="b46f3-155">You can easily automate future deployments of the solution because all the infrastructure is defined in the template.</span></span>
2. <span data-ttu-id="b46f3-156">Per acquisire familiarità con la sintassi del modello, esaminare il codice JSON che rappresenta la soluzione.</span><span class="sxs-lookup"><span data-stu-id="b46f3-156">You can become familiar with template syntax by looking at the JSON that represents your solution.</span></span>

<span data-ttu-id="b46f3-157">Usando l'interfaccia della riga di comando di Azure, è possibile esportare un modello che rappresenta lo stato corrente del gruppo di risorse oppure scaricare il modello usato per una distribuzione specifica.</span><span class="sxs-lookup"><span data-stu-id="b46f3-157">Using the Azure CLI, you can either export a template that represents the current state of your resource group, or download the template that was used for a particular deployment.</span></span>

* <span data-ttu-id="b46f3-158">**Esportare il modello per un gruppo di risorse**: questa operazione è utile quando sono state apportate modifiche a un gruppo di risorse ed è necessario recuperare la rappresentazione JSON del rispettivo stato corrente.</span><span class="sxs-lookup"><span data-stu-id="b46f3-158">**Export the template for a resource group** - This is helpful when you made changes to a resource group, and need to retrieve the JSON representation of its current state.</span></span> <span data-ttu-id="b46f3-159">Il modello generato, tuttavia, contiene solo un numero minimo di parametri e nessuna variabile.</span><span class="sxs-lookup"><span data-stu-id="b46f3-159">However, the generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="b46f3-160">La maggior parte dei valori del modello è hardcoded.</span><span class="sxs-lookup"><span data-stu-id="b46f3-160">Most of the values in the template are hard-coded.</span></span> <span data-ttu-id="b46f3-161">Prima di distribuire il modello generato, è possibile che si voglia convertire altri valori in parametri, per potere personalizzare la distribuzione per diversi ambienti.</span><span class="sxs-lookup"><span data-stu-id="b46f3-161">Before deploying the generated template, you may wish to convert more of the values into parameters so you can customize the deployment for different environments.</span></span>
  
    <span data-ttu-id="b46f3-162">Per esportare il modello per un gruppo di risorse in una directory locale, eseguire il comando `azure group export`, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="b46f3-162">To export the template for a resource group to a local directory, run the `azure group export` command as shown in the following example.</span></span> <span data-ttu-id="b46f3-163">Usare una directory locale appropriata per l'ambiente del sistema operativo in uso.</span><span class="sxs-lookup"><span data-stu-id="b46f3-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="b46f3-164">**Scaricare il modello per una distribuzione specifica**: questa operazione è utile quando è necessario visualizzare il modello effettivo usato per distribuire le risorse.</span><span class="sxs-lookup"><span data-stu-id="b46f3-164">**Download the template for a particular deployment** -- This is helpful when you need to view the actual template that was used to deploy resources.</span></span> <span data-ttu-id="b46f3-165">Il modello include tutte le variabili e tutti i parametri definiti per la distribuzione originale.</span><span class="sxs-lookup"><span data-stu-id="b46f3-165">The template includes all parameters and variables defined for the original deployment.</span></span> <span data-ttu-id="b46f3-166">Se, tuttavia, un utente dell'organizzazione ha modificato il gruppo di risorse in modo diverso dalla definizione nel modello, questo modello non rappresenta lo stato corrente del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b46f3-166">However, if someone in your organization made changes to the resource group outside of the definition in the template, this template doesn't represent the current state of the resource group.</span></span>
  
    <span data-ttu-id="b46f3-167">Per scaricare in una directory locale il modello usato per una distribuzione specifica, eseguire il comando `azure group deployment template download`.</span><span class="sxs-lookup"><span data-stu-id="b46f3-167">To download the template used for a particular deployment to a local directory, run the `azure group deployment template download` command.</span></span> <span data-ttu-id="b46f3-168">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b46f3-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="b46f3-169">La funzionalità di esportazione del modello è disponibile in anteprima e non tutti i tipi di risorse supportano attualmente l'esportazione di un modello.</span><span class="sxs-lookup"><span data-stu-id="b46f3-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="b46f3-170">Quando si prova a esportare un modello, è possibile che venga visualizzato un errore che indica che alcune risorse non sono state esportate.</span><span class="sxs-lookup"><span data-stu-id="b46f3-170">When attempting to export a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="b46f3-171">Se necessario, definire manualmente queste risorse nel modello dopo averlo scaricato.</span><span class="sxs-lookup"><span data-stu-id="b46f3-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b46f3-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b46f3-172">Next steps</span></span>
* <span data-ttu-id="b46f3-173">Per ottenere i dettagli delle operazioni di distribuzione e risolvere i problemi relativi agli errori di distribuzione con l'interfaccia della riga di comando di Azure, vedere [View deployment operations](resource-manager-deployment-operations.md) (Visualizzare le operazioni di distribuzione).</span><span class="sxs-lookup"><span data-stu-id="b46f3-173">To get details of deployment operations and troubleshoot deployment errors with the Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="b46f3-174">Per usare l'interfaccia della riga di comando per configurare un'applicazione o uno script per accedere alle risorse, vedere [Usare l'interfaccia della riga di comando di Azure per creare un'entità servizio per accedere alle risorse](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b46f3-174">If you want to use the CLI to set up an application or script to access resources, see [Use Azure CLI to create a service principal to access resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="b46f3-175">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="b46f3-175">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

