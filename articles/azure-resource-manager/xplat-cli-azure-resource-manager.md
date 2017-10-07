---
title: risorse aaaManage con hello CLI di Azure | Documenti Microsoft
description: Utilizzare hello Azure interfaccia della riga di comando (CLI) toomanage Azure risorse e dei gruppi
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
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a><span data-ttu-id="b0d9a-103">Utilizzare toomanage CLI di Azure hello Azure le risorse e gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="b0d9a-103">Use hello Azure CLI toomanage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0d9a-104">Portale</span><span class="sxs-lookup"><span data-stu-id="b0d9a-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="b0d9a-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b0d9a-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="b0d9a-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0d9a-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="b0d9a-107">API REST</span><span class="sxs-lookup"><span data-stu-id="b0d9a-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="b0d9a-108">Hello interfaccia della riga di comando di Azure (Azure CLI) è uno dei vari strumenti è possibile utilizzare toodeploy e gestire le risorse con Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-108">hello Azure Command-Line Interface (Azure CLI) is one of several tools you can use toodeploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="b0d9a-109">Questo articolo descrive toomanage modi comuni Azure le risorse e gruppi di risorse utilizzando hello CLI di Azure in modalità di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-109">This article introduces common ways toomanage Azure resources and resource groups by using hello Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="b0d9a-110">Per informazioni sull'utilizzo delle risorse di toodeploy hello CLI, vedere [distribuire le risorse con i modelli di gestione risorse e CLI di Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b0d9a-110">For information about using hello CLI toodeploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="b0d9a-111">Per informazioni generali sulle risorse di Azure e Gestione risorse, visitare hello [Panoramica di gestione risorse di Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b0d9a-111">For background about Azure resources and Resource Manager, visit hello [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b0d9a-112">toomanage Azure le risorse con hello CLI di Azure, è necessario troppo[installare hello Azure CLI](../cli-install-nodejs.md), e [Accedi tooAzure](../xplat-cli-connect.md) utilizzando hello `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-112">toomanage Azure resources with hello Azure CLI, you need too[install hello Azure CLI](../cli-install-nodejs.md), and [log in tooAzure](../xplat-cli-connect.md) by using hello `azure login` command.</span></span> <span data-ttu-id="b0d9a-113">Assicurarsi hello che CLI è in modalità di gestione risorse (eseguire `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="b0d9a-113">Make sure hello CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="b0d9a-114">Se aver eseguito queste operazioni, è possibile toogo pronto.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-114">If you've done these things, you're ready toogo.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="b0d9a-115">Ottenere le risorse e i gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="b0d9a-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="b0d9a-116">Gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="b0d9a-116">Resource groups</span></span>
<span data-ttu-id="b0d9a-117">tooget un elenco di tutti i gruppi di risorse nella sottoscrizione e i relativi percorsi, eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-117">tooget a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="b0d9a-118">Risorse</span><span class="sxs-lookup"><span data-stu-id="b0d9a-118">Resources</span></span>
 <span data-ttu-id="b0d9a-119">nome di tutte le risorse in un gruppo, ad esempio un oggetto con toolist *testRG*, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b0d9a-119">toolist all resources in a group, such as one with name *testRG*, use hello following command:</span></span>

    azure resource list testRG

<span data-ttu-id="b0d9a-120">una singola risorsa all'interno di un gruppo di hello, ad esempio una macchina virtuale denominata tooview *MyUbuntuVM*, utilizzare un comando simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="b0d9a-120">tooview an individual resource within hello group, such as a VM named *MyUbuntuVM*, use a command like hello following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="b0d9a-121">Hello preavviso **Microsoft.Compute/virtualMachines** parametro.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-121">Notice hello **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="b0d9a-122">Questo parametro indica il tipo di hello della risorsa hello su che si siano richiedendo informazioni.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-122">This parameter indicates hello type of hello resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="b0d9a-123">Quando si utilizza hello **risorse di azure** comandi diversi dai hello **elenco** comando, è necessario specificare una versione di hello API di risorsa hello con hello **-o** parametro.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-123">When using hello **azure resource** commands other than hello **list** command, you must specify hello API version of hello resource with hello **-o** parameter.</span></span> <span data-ttu-id="b0d9a-124">In caso di dubbi sulla versione di hello API, consultare il file di modello hello e trovare il campo apiVersion hello per risorse hello.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-124">If you're unsure about hello API version, consult hello template file and find hello apiVersion field for hello resource.</span></span> <span data-ttu-id="b0d9a-125">Per altre informazioni sulle versioni dell'API in Resource Manager, vedere [Provider e tipi di risorse](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="b0d9a-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="b0d9a-126">Quando si visualizzano i dettagli su una risorsa, è spesso utile toouse hello `--json` parametro.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-126">When viewing details on a resource, it is often useful toouse hello `--json` parameter.</span></span> <span data-ttu-id="b0d9a-127">Questo parametro consente di hello output più leggibile, perché alcuni valori sono strutture annidate o raccolte.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-127">This parameter makes hello output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="b0d9a-128">esempio Hello illustra la restituzione di risultati hello di hello **Mostra** comando come un documento JSON.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-128">hello following example demonstrates returning hello results of hello **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="b0d9a-129">Se si desidera, salvare hello JSON dati toofile tramite hello &gt; tooa di output di caratteri toodirect hello.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-129">If you want, save hello JSON data toofile by using hello &gt; character toodirect hello output tooa file.</span></span> <span data-ttu-id="b0d9a-130">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b0d9a-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="b0d9a-131">Tag</span><span class="sxs-lookup"><span data-stu-id="b0d9a-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="b0d9a-132">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="b0d9a-132">Manage resources</span></span>
<span data-ttu-id="b0d9a-133">tooadd una risorsa, ad esempio un gruppo di risorse tooa account di archiviazione, eseguire un comando simile a:</span><span class="sxs-lookup"><span data-stu-id="b0d9a-133">tooadd a resource such as a storage account tooa resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="b0d9a-134">Inoltre toospecifying hello versione dell'API di risorsa hello con hello **-o** parametro, utilizzare hello **-p** toopass JSON in formato stringa del parametro con le necessarie o proprietà aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-134">In addition toospecifying hello API version of hello resource with hello **-o** parameter, use hello **-p** parameter toopass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="b0d9a-135">toodelete una risorsa esistente, ad esempio una risorsa di macchina virtuale, utilizzare un comando simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="b0d9a-135">toodelete an existing resource such as a virtual machine resource, use a command like hello following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="b0d9a-136">esistente toomove gruppo di risorse tooanother risorse o una sottoscrizione, utilizzare hello **dello spostamento delle risorse azure** comando.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-136">toomove existing resources tooanother resource group or subscription, use hello **azure resource move** command.</span></span> <span data-ttu-id="b0d9a-137">Hello seguente esempio viene illustrato come toomove Cache Redis tooa nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-137">hello following example shows how toomove a Redis Cache tooa new resource group.</span></span> <span data-ttu-id="b0d9a-138">In hello **-i** parametro, fornire un elenco delimitato da virgole di toomove dell'id di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-138">In hello **-i** parameter, provide a comma-separated list of hello resource id's toomove.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a><span data-ttu-id="b0d9a-139">Controllo accesso tooresources</span><span class="sxs-lookup"><span data-stu-id="b0d9a-139">Control access tooresources</span></span>
<span data-ttu-id="b0d9a-140">È possibile utilizzare hello Azure CLI toocreate e gestire criteri toocontrol accedere tooAzure alle risorse.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-140">You can use hello Azure CLI toocreate and manage policies toocontrol access tooAzure resources.</span></span> <span data-ttu-id="b0d9a-141">Per informazioni generali sulle definizioni dei criteri e tooresources l'assegnazione di criteri, vedere [utilizzare criteri toomanage risorse e controllare l'accesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b0d9a-141">For background about policy definitions and assigning policies tooresources, see [Use policy toomanage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="b0d9a-142">Ad esempio, definire hello seguente criteri toodeny tutte le richieste in cui si non trova Stati Uniti occidentali o North Central US e salvarlo toohello criteri definizione file policy.json:</span><span class="sxs-lookup"><span data-stu-id="b0d9a-142">For example, define hello following policy toodeny all requests where location is not West US or North Central US, and save it toohello policy definition file policy.json:</span></span>

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

<span data-ttu-id="b0d9a-143">Eseguire quindi hello **creare una definizione di criteri** comando:</span><span class="sxs-lookup"><span data-stu-id="b0d9a-143">Then run hello **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="b0d9a-144">Questo comando Mostra il seguente toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="b0d9a-144">This command shows output similar toohello following:</span></span>

    + <span data-ttu-id="b0d9a-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="b0d9a-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="b0d9a-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="b0d9a-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="b0d9a-147">un criterio nell'ambito di hello desiderato, utilizzare hello tooassign **PolicyDefinitionId** restituito dal comando precedente hello.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-147">tooassign a policy at hello scope you want, use hello **PolicyDefinitionId** returned from hello previous command.</span></span> <span data-ttu-id="b0d9a-148">Nell'esempio seguente di hello, questo ambito è sottoscrizione hello, ma è possibile definire l'ambito tooresource gruppi o singole risorse:</span><span class="sxs-lookup"><span data-stu-id="b0d9a-148">In hello following example, this scope is hello subscription, but you can scope tooresource groups or individual resources:</span></span>

    <span data-ttu-id="b0d9a-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="b0d9a-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="b0d9a-150">È possibile ottenere, modificare o rimuovere le definizioni dei criteri utilizzando hello **Mostra definizione criteri**, **set di definizione dei criteri**, e **definizione dei criteri di eliminazione** comandi.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-150">You can get, change, or remove policy definitions by using hello **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="b0d9a-151">Allo stesso modo, è possibile ottenere, modificare o rimuovere le assegnazioni di criteri con hello **Mostra assegnazione criteri**, **set assegnazione criteri**, e **eliminare l'assegnazione dei criteri** comandi .</span><span class="sxs-lookup"><span data-stu-id="b0d9a-151">Similarly, you can get, change, or remove policy assignments by using hello **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="b0d9a-152">Esportare un gruppo di risorse come modello</span><span class="sxs-lookup"><span data-stu-id="b0d9a-152">Export a resource group as a template</span></span>
<span data-ttu-id="b0d9a-153">Per un gruppo di risorse esistente, è possibile visualizzare il modello di gestione risorse hello per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-153">For an existing resource group, you can view hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="b0d9a-154">Esportazione modello hello offre due vantaggi:</span><span class="sxs-lookup"><span data-stu-id="b0d9a-154">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="b0d9a-155">È possibile automatizzare facilmente le distribuzioni future di soluzione hello perché tutta l'infrastruttura hello è definito nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-155">You can easily automate future deployments of hello solution because all hello infrastructure is defined in hello template.</span></span>
2. <span data-ttu-id="b0d9a-156">È possibile acquisire familiarità con la sintassi dei modelli esaminando hello JSON che rappresenta la soluzione.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-156">You can become familiar with template syntax by looking at hello JSON that represents your solution.</span></span>

<span data-ttu-id="b0d9a-157">Utilizza hello CLI di Azure, è possibile esportare un modello che rappresenta lo stato corrente di hello del gruppo di risorse, o scaricare il modello di hello che è stato utilizzato per una particolare distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-157">Using hello Azure CLI, you can either export a template that represents hello current state of your resource group, or download hello template that was used for a particular deployment.</span></span>

* <span data-ttu-id="b0d9a-158">**Esportare il modello di hello per un gruppo di risorse** -ciò risulta utile quando il gruppo di risorse tooa le modifiche apportate e necessario tooretrieve hello rappresentazione JSON del relativo stato corrente.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-158">**Export hello template for a resource group** - This is helpful when you made changes tooa resource group, and need tooretrieve hello JSON representation of its current state.</span></span> <span data-ttu-id="b0d9a-159">Modello generato hello contiene tuttavia solo un numero minimo di parametri e non variabili.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-159">However, hello generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="b0d9a-160">La maggior parte dei valori hello hello modello sono hardcoded.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-160">Most of hello values in hello template are hard-coded.</span></span> <span data-ttu-id="b0d9a-161">Prima di distribuire il modello di hello generato, è preferibile tooconvert più valori hello nei parametri in modo da personalizzare la distribuzione di hello per ambienti diversi.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-161">Before deploying hello generated template, you may wish tooconvert more of hello values into parameters so you can customize hello deployment for different environments.</span></span>
  
    <span data-ttu-id="b0d9a-162">modello di hello tooexport per una risorsa gruppo tooa directory locale, eseguire hello `azure group export` comando come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-162">tooexport hello template for a resource group tooa local directory, run hello `azure group export` command as shown in hello following example.</span></span> <span data-ttu-id="b0d9a-163">Usare una directory locale appropriata per l'ambiente del sistema operativo in uso.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="b0d9a-164">**Scaricare il modello di hello per una particolare distribuzione** -questo è utile quando è necessario tooview hello modello effettivo che è stato utilizzato toodeploy risorse.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-164">**Download hello template for a particular deployment** -- This is helpful when you need tooview hello actual template that was used toodeploy resources.</span></span> <span data-ttu-id="b0d9a-165">modello di Hello include tutti i parametri e variabili definite per la distribuzione originale hello.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-165">hello template includes all parameters and variables defined for hello original deployment.</span></span> <span data-ttu-id="b0d9a-166">Tuttavia, se un utente nell'organizzazione apportate gruppo di risorse toohello le modifiche apportate all'esterno di definizione hello nel modello di hello, questo modello non rappresenta lo stato corrente di hello hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-166">However, if someone in your organization made changes toohello resource group outside of hello definition in hello template, this template doesn't represent hello current state of hello resource group.</span></span>
  
    <span data-ttu-id="b0d9a-167">modello di hello toodownload utilizzato per una particolare tooa locale directory di distribuzione, eseguire hello `azure group deployment template download` comando.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-167">toodownload hello template used for a particular deployment tooa local directory, run hello `azure group deployment template download` command.</span></span> <span data-ttu-id="b0d9a-168">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b0d9a-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="b0d9a-169">La funzionalità di esportazione del modello è disponibile in anteprima e non tutti i tipi di risorse supportano attualmente l'esportazione di un modello.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="b0d9a-170">Durante il tentativo di tooexport un modello, si verifichi un errore che indica che alcune risorse non sono state esportate.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-170">When attempting tooexport a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="b0d9a-171">Se necessario, definire manualmente queste risorse nel modello dopo averlo scaricato.</span><span class="sxs-lookup"><span data-stu-id="b0d9a-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b0d9a-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b0d9a-172">Next steps</span></span>
* <span data-ttu-id="b0d9a-173">Dettagli tooget delle operazioni di distribuzione e risolvere gli errori di distribuzione con hello CLI di Azure, vedere [per visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="b0d9a-173">tooget details of deployment operations and troubleshoot deployment errors with hello Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="b0d9a-174">Se si desidera toouse hello CLI tooset risorse tooaccess script o da un'applicazione, vedere [toocreate CLI di Azure di utilizzare un'entità servizio tooaccess risorse](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b0d9a-174">If you want toouse hello CLI tooset up an application or script tooaccess resources, see [Use Azure CLI toocreate a service principal tooaccess resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="b0d9a-175">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="b0d9a-175">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

