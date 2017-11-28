---
title: aaaCreate elementi personalizzati per la macchina virtuale Labs DevTest | Documenti Microsoft
description: Informazioni su come tooauthor i propri elementi per utilizzano con DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="2fde4-103">Creare elementi personalizzati per le macchine virtuali di lab di sviluppo e test</span><span class="sxs-lookup"><span data-stu-id="2fde4-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="2fde4-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2fde4-104">Overview</span></span>
<span data-ttu-id="2fde4-105">**Elementi** vengono utilizzati toodeploy e configurare l'applicazione dopo il provisioning di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2fde4-105">**Artifacts** are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="2fde4-106">Un elemento è costituito da un file di definizione dell’elemento e altri file di script archiviati in una cartella in un archivio git.</span><span class="sxs-lookup"><span data-stu-id="2fde4-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="2fde4-107">I file di definizione degli elementi costituiti da JSON e le espressioni che è possibile utilizzare toospecify si desidera tooinstall in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2fde4-107">Artifact definition files consist of JSON and expressions that you can use toospecify what you want tooinstall on a VM.</span></span> <span data-ttu-id="2fde4-108">Ad esempio, è possibile definire il nome di hello artefatto, toorun comando e i parametri che vengono resi disponibili quando si esegue il comando hello.</span><span class="sxs-lookup"><span data-stu-id="2fde4-108">For example, you can define hello name of an artifact, command toorun, and parameters that are made available when hello command is run.</span></span> <span data-ttu-id="2fde4-109">È possibile fare riferimento a file di script tooother nel file di definizione di artefatto hello in base al nome.</span><span class="sxs-lookup"><span data-stu-id="2fde4-109">You can refer tooother script files within hello artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="2fde4-110">Formato del file di definizione dell’elemento</span><span class="sxs-lookup"><span data-stu-id="2fde4-110">Artifact definition file format</span></span>
<span data-ttu-id="2fde4-111">Hello riportato di seguito nelle sezioni hello che costituiscono hello struttura di base di un file di definizione:</span><span class="sxs-lookup"><span data-stu-id="2fde4-111">hello following example shows hello sections that make up hello basic structure of a definition file:</span></span>

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| <span data-ttu-id="2fde4-112">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="2fde4-112">Element name</span></span> | <span data-ttu-id="2fde4-113">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="2fde4-113">Required?</span></span> | <span data-ttu-id="2fde4-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2fde4-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fde4-115">$schema</span><span class="sxs-lookup"><span data-stu-id="2fde4-115">$schema</span></span> |<span data-ttu-id="2fde4-116">No</span><span class="sxs-lookup"><span data-stu-id="2fde4-116">No</span></span> |<span data-ttu-id="2fde4-117">Percorso del file di schema JSON hello che aiuta a test di validità hello hello del file di definizione.</span><span class="sxs-lookup"><span data-stu-id="2fde4-117">Location of hello JSON schema file that helps in testing hello validity of hello definition file.</span></span> |
| <span data-ttu-id="2fde4-118">title</span><span class="sxs-lookup"><span data-stu-id="2fde4-118">title</span></span> |<span data-ttu-id="2fde4-119">Sì</span><span class="sxs-lookup"><span data-stu-id="2fde4-119">Yes</span></span> |<span data-ttu-id="2fde4-120">Nome dell'elemento hello visualizzato in lab hello.</span><span class="sxs-lookup"><span data-stu-id="2fde4-120">Name of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="2fde4-121">description</span><span class="sxs-lookup"><span data-stu-id="2fde4-121">description</span></span> |<span data-ttu-id="2fde4-122">Sì</span><span class="sxs-lookup"><span data-stu-id="2fde4-122">Yes</span></span> |<span data-ttu-id="2fde4-123">Descrizione dell'elemento hello visualizzato in lab hello.</span><span class="sxs-lookup"><span data-stu-id="2fde4-123">Description of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="2fde4-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="2fde4-124">iconUri</span></span> |<span data-ttu-id="2fde4-125">No</span><span class="sxs-lookup"><span data-stu-id="2fde4-125">No</span></span> |<span data-ttu-id="2fde4-126">URI dell'icona hello visualizzata nell'ambiente lab hello.</span><span class="sxs-lookup"><span data-stu-id="2fde4-126">Uri of hello icon displayed in hello lab.</span></span> |
| <span data-ttu-id="2fde4-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="2fde4-127">targetOsType</span></span> |<span data-ttu-id="2fde4-128">Sì</span><span class="sxs-lookup"><span data-stu-id="2fde4-128">Yes</span></span> |<span data-ttu-id="2fde4-129">Sistema operativo della macchina virtuale in cui è installato artefatto hello.</span><span class="sxs-lookup"><span data-stu-id="2fde4-129">Operating system of hello VM where artifact is installed.</span></span> <span data-ttu-id="2fde4-130">Opzioni supportate: Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="2fde4-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="2fde4-131">parameters</span><span class="sxs-lookup"><span data-stu-id="2fde4-131">parameters</span></span> |<span data-ttu-id="2fde4-132">No</span><span class="sxs-lookup"><span data-stu-id="2fde4-132">No</span></span> |<span data-ttu-id="2fde4-133">Valori forniti quando viene eseguito il comando di installazione dell’elemento in un computer.</span><span class="sxs-lookup"><span data-stu-id="2fde4-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="2fde4-134">Ciò consente di personalizzare l'elemento.</span><span class="sxs-lookup"><span data-stu-id="2fde4-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="2fde4-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="2fde4-135">runCommand</span></span> |<span data-ttu-id="2fde4-136">Sì</span><span class="sxs-lookup"><span data-stu-id="2fde4-136">Yes</span></span> |<span data-ttu-id="2fde4-137">Il comando di installazione dell’elemento che viene eseguito in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2fde4-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="2fde4-138">Parametri dell'elemento</span><span class="sxs-lookup"><span data-stu-id="2fde4-138">Artifact parameters</span></span>
<span data-ttu-id="2fde4-139">Nella sezione parametri di hello hello del file di definizione, specificare i valori che un utente può immettere durante l'installazione di un elemento.</span><span class="sxs-lookup"><span data-stu-id="2fde4-139">In hello parameters section of hello definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="2fde4-140">È possibile fare riferimento a valori toothese nel comando di installazione di hello artefatto.</span><span class="sxs-lookup"><span data-stu-id="2fde4-140">You can refer toothese values in hello artifact install command.</span></span>

<span data-ttu-id="2fde4-141">Definire i parametri con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="2fde4-141">You define parameters with hello following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="2fde4-142">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="2fde4-142">Element name</span></span> | <span data-ttu-id="2fde4-143">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="2fde4-143">Required?</span></span> | <span data-ttu-id="2fde4-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2fde4-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fde4-145">type</span><span class="sxs-lookup"><span data-stu-id="2fde4-145">type</span></span> |<span data-ttu-id="2fde4-146">Sì</span><span class="sxs-lookup"><span data-stu-id="2fde4-146">Yes</span></span> |<span data-ttu-id="2fde4-147">Tipo di valore del parametro.</span><span class="sxs-lookup"><span data-stu-id="2fde4-147">Type of parameter value.</span></span> <span data-ttu-id="2fde4-148">Vedere hello seguente elenco di tipi consentito hello:</span><span class="sxs-lookup"><span data-stu-id="2fde4-148">See hello following list for hello allowed types:</span></span> |
| <span data-ttu-id="2fde4-149">displayName</span><span class="sxs-lookup"><span data-stu-id="2fde4-149">displayName</span></span> |<span data-ttu-id="2fde4-150">Sì</span><span class="sxs-lookup"><span data-stu-id="2fde4-150">Yes</span></span> |<span data-ttu-id="2fde4-151">Nome del parametro hello che viene visualizzato tooa utente nell'ambiente lab hello.</span><span class="sxs-lookup"><span data-stu-id="2fde4-151">Name of hello parameter that is displayed tooa user in hello lab.</span></span> | |
| <span data-ttu-id="2fde4-152">description</span><span class="sxs-lookup"><span data-stu-id="2fde4-152">description</span></span> |<span data-ttu-id="2fde4-153">Sì</span><span class="sxs-lookup"><span data-stu-id="2fde4-153">Yes</span></span> |<span data-ttu-id="2fde4-154">Descrizione del parametro hello che viene visualizzato nell'ambiente lab hello.</span><span class="sxs-lookup"><span data-stu-id="2fde4-154">Description of hello parameter that is displayed in hello lab.</span></span> |

<span data-ttu-id="2fde4-155">Hello tipi consentiti sono:</span><span class="sxs-lookup"><span data-stu-id="2fde4-155">hello allowed types are:</span></span>

* <span data-ttu-id="2fde4-156">string: tutte le stringhe JSON valide</span><span class="sxs-lookup"><span data-stu-id="2fde4-156">string – any valid JSON string</span></span>
* <span data-ttu-id="2fde4-157">int: tutti i valori integer JSON validi</span><span class="sxs-lookup"><span data-stu-id="2fde4-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="2fde4-158">bool: tutti i valori booleani JSON validi</span><span class="sxs-lookup"><span data-stu-id="2fde4-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="2fde4-159">array: tutte le matrici JSON valide</span><span class="sxs-lookup"><span data-stu-id="2fde4-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="2fde4-160">Espressioni e funzioni dell’elemento</span><span class="sxs-lookup"><span data-stu-id="2fde4-160">Artifact expressions and functions</span></span>
<span data-ttu-id="2fde4-161">È possibile utilizzare l'espressione e artefatto hello tooconstruct di funzioni di comando di installazione.</span><span class="sxs-lookup"><span data-stu-id="2fde4-161">You can use expression and functions tooconstruct hello artifact install command.</span></span>
<span data-ttu-id="2fde4-162">Le espressioni sono racchiusi tra parentesi quadre ([e]) e vengono valutate quando l'elemento hello è installato.</span><span class="sxs-lookup"><span data-stu-id="2fde4-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when hello artifact is installed.</span></span> <span data-ttu-id="2fde4-163">Le espressioni possono trovarsi in qualsiasi punto in un valore stringa JSON e restituiscono sempre un altro valore JSON.</span><span class="sxs-lookup"><span data-stu-id="2fde4-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="2fde4-164">Se è necessario che una stringa letterale che inizia con una parentesi quadra toouse [, è necessario utilizzare due parentesi quadre [[.</span><span class="sxs-lookup"><span data-stu-id="2fde4-164">If you need toouse a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="2fde4-165">In genere, si usano espressioni con funzioni tooconstruct un valore.</span><span class="sxs-lookup"><span data-stu-id="2fde4-165">Typically, you use expressions with functions tooconstruct a value.</span></span> <span data-ttu-id="2fde4-166">Proprio come in JavaScript, le chiamate di funzione sono formattate come functionName(arg1,arg2,arg3).</span><span class="sxs-lookup"><span data-stu-id="2fde4-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="2fde4-167">Hello elenco seguente mostra le funzioni comuni:</span><span class="sxs-lookup"><span data-stu-id="2fde4-167">hello following list shows common functions:</span></span>

* <span data-ttu-id="2fde4-168">Parameters(ParameterName) - restituisce un valore di parametro fornito durante l'esecuzione del comando artefatto hello.</span><span class="sxs-lookup"><span data-stu-id="2fde4-168">parameters(parameterName) - Returns a parameter value that is provided when hello artifact command is run.</span></span>
* <span data-ttu-id="2fde4-169">concat(arg1,arg2,arg3, …..) -     Combina più valori di stringa.</span><span class="sxs-lookup"><span data-stu-id="2fde4-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="2fde4-170">Questa funzione può accettare qualsiasi numero di argomenti.</span><span class="sxs-lookup"><span data-stu-id="2fde4-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="2fde4-171">Hello seguente esempio viene illustrato come toouse tooconstruct un valore di espressione e funzioni:</span><span class="sxs-lookup"><span data-stu-id="2fde4-171">hello following example shows how toouse expression and functions tooconstruct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="2fde4-172">Creare un elemento personalizzato</span><span class="sxs-lookup"><span data-stu-id="2fde4-172">Create a custom artifact</span></span>
<span data-ttu-id="2fde4-173">Creare l'elemento personalizzato eseguendo questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="2fde4-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="2fde4-174">Installare un editor di JSON, è necessario un toowork editor JSON con i file di definizione degli elementi.</span><span class="sxs-lookup"><span data-stu-id="2fde4-174">Install a JSON editor - You need a JSON editor toowork with artifact definition files.</span></span> <span data-ttu-id="2fde4-175">Si consiglia di utilizzare [Visual Studio Code](https://code.visualstudio.com/), che è disponibile per Windows, Linux e OS X.</span><span class="sxs-lookup"><span data-stu-id="2fde4-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="2fde4-176">Get artifactfile.json un esempio - estrazione degli elementi di hello creati dal team di Azure DevTest Labs al nostro [repository GitHub](https://github.com/Azure/azure-devtestlab), in cui è stata creata una libreria completa di elementi che consentono di creano i propri elementi.</span><span class="sxs-lookup"><span data-stu-id="2fde4-176">Get a sample artifactfile.json - Check out hello artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="2fde4-177">Scaricare un file di definizione di artefatto e apportare le modifiche tooit toocreate i propri elementi.</span><span class="sxs-lookup"><span data-stu-id="2fde4-177">Download an artifact definition file and make changes tooit toocreate your own artifacts.</span></span>
3. <span data-ttu-id="2fde4-178">Avvalersi di IntelliSense - usare IntelliSense toosee elementi validi che possono essere utilizzati tooconstruct un file di definizione dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="2fde4-178">Make use of IntelliSense - Leverage IntelliSense toosee valid elements that can be used tooconstruct an artifact definition file.</span></span> <span data-ttu-id="2fde4-179">È inoltre possibile visualizzare diverse opzioni hello per i valori di un elemento.</span><span class="sxs-lookup"><span data-stu-id="2fde4-179">You can also see hello different options for values of an element.</span></span> <span data-ttu-id="2fde4-180">Ad esempio, IntelliSense Mostra, si hello disponibili due opzioni di Windows o Linux durante la modifica di hello **targetOsType** elemento.</span><span class="sxs-lookup"><span data-stu-id="2fde4-180">For example, IntelliSense show you hello two choices of Windows or Linux when editing hello **targetOsType** element.</span></span>
4. <span data-ttu-id="2fde4-181">Elemento hello Store in un [repository git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="2fde4-181">Store hello artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="2fde4-182">Creare una directory distinta per ogni elemento in cui il nome di directory hello è hello stesso come il nome dell'artefatto hello.</span><span class="sxs-lookup"><span data-stu-id="2fde4-182">Create a separate directory for each artifact where hello directory name is hello same as hello artifact name.</span></span>
   2. <span data-ttu-id="2fde4-183">Archiviare i file di definizione di artefatto hello (artifactfile.json) nella directory di hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="2fde4-183">Store hello artifact definition file (artifactfile.json) in hello directory you created.</span></span>
   3. <span data-ttu-id="2fde4-184">Comando di installazione script hello archivio che fanno riferimento all'elemento hello.</span><span class="sxs-lookup"><span data-stu-id="2fde4-184">Store hello scripts that are referenced from hello artifact install command.</span></span>
      
      <span data-ttu-id="2fde4-185">Di seguito è riportato un esempio di come potrebbe apparire una cartella di elementi:</span><span class="sxs-lookup"><span data-stu-id="2fde4-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Esempio di archivio git dell’elemento](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="2fde4-187">Aggiungere lab toohello repository di artefatti hello - vedere l'articolo toohello [aggiungere un repository Git per gli elementi e i modelli](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="2fde4-187">Add hello artifacts repository toohello lab - Refer toohello article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="2fde4-188">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="2fde4-188">Related articles</span></span>
* [<span data-ttu-id="2fde4-189">Modalità errori artefatto toodiagnose in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2fde4-189">How toodiagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="2fde4-190">Aggiungere un dominio di Active Directory utilizzando un modello di gestione delle risorse in Azure DevTest Labs di tooexisting VM</span><span class="sxs-lookup"><span data-stu-id="2fde4-190">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="2fde4-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2fde4-191">Next steps</span></span>
* <span data-ttu-id="2fde4-192">Informazioni su come troppo[aggiungere laboratorio tooa repository Git artefatto](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="2fde4-192">Learn how too[add a Git artifact repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

