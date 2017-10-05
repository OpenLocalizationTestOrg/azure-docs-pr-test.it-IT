---
title: Creare elementi personalizzati per le macchine virtuali di lab di sviluppo/test | Microsoft Docs
description: Informazioni su come creare i propri elementi per l'uso nei Lab di sviluppo/test
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
ms.openlocfilehash: 2412033daa1d97860dd9f380178622b1ddc590c0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="14742-103">Creare elementi personalizzati per le macchine virtuali di lab di sviluppo e test</span><span class="sxs-lookup"><span data-stu-id="14742-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="14742-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="14742-104">Overview</span></span>
<span data-ttu-id="14742-105">**Elementi** vengono utilizzati per distribuire e configurare l'applicazione dopo il provisioning di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14742-105">**Artifacts** are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="14742-106">Un elemento è costituito da un file di definizione dell’elemento e altri file di script archiviati in una cartella in un archivio git.</span><span class="sxs-lookup"><span data-stu-id="14742-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="14742-107">I file di definizione dell’elemento sono costituiti da JSON ed espressioni che è possibile utilizzare per specificare gli elementi da installare in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14742-107">Artifact definition files consist of JSON and expressions that you can use to specify what you want to install on a VM.</span></span> <span data-ttu-id="14742-108">Ad esempio, è possibile definire il nome dell'elemento, il comando da eseguire e i parametri che vengono resi disponibili quando si esegue il comando.</span><span class="sxs-lookup"><span data-stu-id="14742-108">For example, you can define the name of an artifact, command to run, and parameters that are made available when the command is run.</span></span> <span data-ttu-id="14742-109">È possibile fare riferimento ad altri file di script all'interno del file di definizione dell'elemento in base al nome.</span><span class="sxs-lookup"><span data-stu-id="14742-109">You can refer to other script files within the artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="14742-110">Formato del file di definizione dell’elemento</span><span class="sxs-lookup"><span data-stu-id="14742-110">Artifact definition file format</span></span>
<span data-ttu-id="14742-111">L'esempio seguente illustra le sezioni che compongono la struttura di base di un file di definizione:</span><span class="sxs-lookup"><span data-stu-id="14742-111">The following example shows the sections that make up the basic structure of a definition file:</span></span>

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

| <span data-ttu-id="14742-112">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="14742-112">Element name</span></span> | <span data-ttu-id="14742-113">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="14742-113">Required?</span></span> | <span data-ttu-id="14742-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="14742-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="14742-115">$schema</span><span class="sxs-lookup"><span data-stu-id="14742-115">$schema</span></span> |<span data-ttu-id="14742-116">No</span><span class="sxs-lookup"><span data-stu-id="14742-116">No</span></span> |<span data-ttu-id="14742-117">Percorso del file di schema JSON che aiuta a testare la validità del file di definizione.</span><span class="sxs-lookup"><span data-stu-id="14742-117">Location of the JSON schema file that helps in testing the validity of the definition file.</span></span> |
| <span data-ttu-id="14742-118">title</span><span class="sxs-lookup"><span data-stu-id="14742-118">title</span></span> |<span data-ttu-id="14742-119">Sì</span><span class="sxs-lookup"><span data-stu-id="14742-119">Yes</span></span> |<span data-ttu-id="14742-120">Nome dell'elemento visualizzato nel lab.</span><span class="sxs-lookup"><span data-stu-id="14742-120">Name of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="14742-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="14742-121">description</span></span> |<span data-ttu-id="14742-122">Sì</span><span class="sxs-lookup"><span data-stu-id="14742-122">Yes</span></span> |<span data-ttu-id="14742-123">Descrizione dell'elemento visualizzato nel lab.</span><span class="sxs-lookup"><span data-stu-id="14742-123">Description of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="14742-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="14742-124">iconUri</span></span> |<span data-ttu-id="14742-125">No</span><span class="sxs-lookup"><span data-stu-id="14742-125">No</span></span> |<span data-ttu-id="14742-126">URI dell'icona visualizzato nel lab.</span><span class="sxs-lookup"><span data-stu-id="14742-126">Uri of the icon displayed in the lab.</span></span> |
| <span data-ttu-id="14742-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="14742-127">targetOsType</span></span> |<span data-ttu-id="14742-128">Sì</span><span class="sxs-lookup"><span data-stu-id="14742-128">Yes</span></span> |<span data-ttu-id="14742-129">Sistema operativo della macchina virtuale in cui viene installato l'elemento.</span><span class="sxs-lookup"><span data-stu-id="14742-129">Operating system of the VM where artifact is installed.</span></span> <span data-ttu-id="14742-130">Opzioni supportate: Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="14742-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="14742-131">parameters</span><span class="sxs-lookup"><span data-stu-id="14742-131">parameters</span></span> |<span data-ttu-id="14742-132">No</span><span class="sxs-lookup"><span data-stu-id="14742-132">No</span></span> |<span data-ttu-id="14742-133">Valori forniti quando viene eseguito il comando di installazione dell’elemento in un computer.</span><span class="sxs-lookup"><span data-stu-id="14742-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="14742-134">Ciò consente di personalizzare l'elemento.</span><span class="sxs-lookup"><span data-stu-id="14742-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="14742-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="14742-135">runCommand</span></span> |<span data-ttu-id="14742-136">Sì</span><span class="sxs-lookup"><span data-stu-id="14742-136">Yes</span></span> |<span data-ttu-id="14742-137">Il comando di installazione dell’elemento che viene eseguito in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14742-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="14742-138">Parametri dell'elemento</span><span class="sxs-lookup"><span data-stu-id="14742-138">Artifact parameters</span></span>
<span data-ttu-id="14742-139">Nella sezione dei parametri del file di definizione è possibile specificare i valori che un utente può immettere durante l’installazione di un elemento.</span><span class="sxs-lookup"><span data-stu-id="14742-139">In the parameters section of the definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="14742-140">È possibile fare riferimento a questi valori nel comando di installazione dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="14742-140">You can refer to these values in the artifact install command.</span></span>

<span data-ttu-id="14742-141">I parametri vengono definiti con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="14742-141">You define parameters with the following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="14742-142">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="14742-142">Element name</span></span> | <span data-ttu-id="14742-143">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="14742-143">Required?</span></span> | <span data-ttu-id="14742-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="14742-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="14742-145">type</span><span class="sxs-lookup"><span data-stu-id="14742-145">type</span></span> |<span data-ttu-id="14742-146">Sì</span><span class="sxs-lookup"><span data-stu-id="14742-146">Yes</span></span> |<span data-ttu-id="14742-147">Tipo di valore del parametro.</span><span class="sxs-lookup"><span data-stu-id="14742-147">Type of parameter value.</span></span> <span data-ttu-id="14742-148">Vedere l'elenco seguente dei tipi consentiti:</span><span class="sxs-lookup"><span data-stu-id="14742-148">See the following list for the allowed types:</span></span> |
| <span data-ttu-id="14742-149">displayName</span><span class="sxs-lookup"><span data-stu-id="14742-149">displayName</span></span> |<span data-ttu-id="14742-150">Sì</span><span class="sxs-lookup"><span data-stu-id="14742-150">Yes</span></span> |<span data-ttu-id="14742-151">Nome del parametro che viene visualizzato a un utente nel lab.</span><span class="sxs-lookup"><span data-stu-id="14742-151">Name of the parameter that is displayed to a user in the lab.</span></span> | |
| <span data-ttu-id="14742-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="14742-152">description</span></span> |<span data-ttu-id="14742-153">Sì</span><span class="sxs-lookup"><span data-stu-id="14742-153">Yes</span></span> |<span data-ttu-id="14742-154">Descrizione del parametro che viene visualizzato nel lab.</span><span class="sxs-lookup"><span data-stu-id="14742-154">Description of the parameter that is displayed in the lab.</span></span> |

<span data-ttu-id="14742-155">I tipi consentiti sono:</span><span class="sxs-lookup"><span data-stu-id="14742-155">The allowed types are:</span></span>

* <span data-ttu-id="14742-156">string: tutte le stringhe JSON valide</span><span class="sxs-lookup"><span data-stu-id="14742-156">string – any valid JSON string</span></span>
* <span data-ttu-id="14742-157">int: tutti i valori integer JSON validi</span><span class="sxs-lookup"><span data-stu-id="14742-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="14742-158">bool: tutti i valori booleani JSON validi</span><span class="sxs-lookup"><span data-stu-id="14742-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="14742-159">array: tutte le matrici JSON valide</span><span class="sxs-lookup"><span data-stu-id="14742-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="14742-160">Espressioni e funzioni dell’elemento</span><span class="sxs-lookup"><span data-stu-id="14742-160">Artifact expressions and functions</span></span>
<span data-ttu-id="14742-161">È possibile utilizzare espressioni e funzioni per la creazione del comando di installazione dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="14742-161">You can use expression and functions to construct the artifact install command.</span></span>
<span data-ttu-id="14742-162">Le espressioni sono racchiuse tra parentesi quadre ([ e ]) e vengono valutate al momento dell’installazione dell’elemento.</span><span class="sxs-lookup"><span data-stu-id="14742-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when the artifact is installed.</span></span> <span data-ttu-id="14742-163">Le espressioni possono trovarsi in qualsiasi punto in un valore stringa JSON e restituiscono sempre un altro valore JSON.</span><span class="sxs-lookup"><span data-stu-id="14742-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="14742-164">Se è necessario usare una stringa letterale che inizia con una parentesi quadra [, usare due parentesi quadre [[.</span><span class="sxs-lookup"><span data-stu-id="14742-164">If you need to use a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="14742-165">In genere, si usano espressioni con funzioni per costruire un valore.</span><span class="sxs-lookup"><span data-stu-id="14742-165">Typically, you use expressions with functions to construct a value.</span></span> <span data-ttu-id="14742-166">Proprio come in JavaScript, le chiamate di funzione sono formattate come functionName(arg1,arg2,arg3).</span><span class="sxs-lookup"><span data-stu-id="14742-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="14742-167">L'elenco seguente riporta le funzioni comuni:</span><span class="sxs-lookup"><span data-stu-id="14742-167">The following list shows common functions:</span></span>

* <span data-ttu-id="14742-168">parameters(parameterName) - restituisce un valore di parametro fornito quando viene eseguito il comando dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="14742-168">parameters(parameterName) - Returns a parameter value that is provided when the artifact command is run.</span></span>
* <span data-ttu-id="14742-169">concat(arg1,arg2,arg3, …..) -     Combina più valori di stringa.</span><span class="sxs-lookup"><span data-stu-id="14742-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="14742-170">Questa funzione può accettare qualsiasi numero di argomenti.</span><span class="sxs-lookup"><span data-stu-id="14742-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="14742-171">L'esempio seguente illustra come utilizzare espressioni e funzioni per costruire un valore:</span><span class="sxs-lookup"><span data-stu-id="14742-171">The following example shows how to use expression and functions to construct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="14742-172">Creare un elemento personalizzato</span><span class="sxs-lookup"><span data-stu-id="14742-172">Create a custom artifact</span></span>
<span data-ttu-id="14742-173">Creare l'elemento personalizzato eseguendo questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="14742-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="14742-174">Installare un editor JSON: è necessario un editor JSON per lavorare con i file di definizione dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="14742-174">Install a JSON editor - You need a JSON editor to work with artifact definition files.</span></span> <span data-ttu-id="14742-175">Si consiglia di utilizzare [Visual Studio Code](https://code.visualstudio.com/), che è disponibile per Windows, Linux e OS X.</span><span class="sxs-lookup"><span data-stu-id="14742-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="14742-176">Ottenere un esempio di artifactfile.json: controllare gli elementi creati dal team di Lab di sviluppo e test di Azure nell' [archivio GitHub](https://github.com/Azure/azure-devtestlab) in cui è stata creata una libreria completa degli elementi che aiuta nella creazione dei propri elementi.</span><span class="sxs-lookup"><span data-stu-id="14742-176">Get a sample artifactfile.json - Check out the artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="14742-177">Scaricare un file di definizione dell’elemento e apportare modifiche al codice per creare i propri elementi.</span><span class="sxs-lookup"><span data-stu-id="14742-177">Download an artifact definition file and make changes to it to create your own artifacts.</span></span>
3. <span data-ttu-id="14742-178">Utilizzo di IntelliSense - utilizzare IntelliSense per visualizzare elementi validi che possono essere utilizzati per costruire un file di definizione dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="14742-178">Make use of IntelliSense - Leverage IntelliSense to see valid elements that can be used to construct an artifact definition file.</span></span> <span data-ttu-id="14742-179">È inoltre possibile visualizzare le diverse opzioni per i valori di un elemento.</span><span class="sxs-lookup"><span data-stu-id="14742-179">You can also see the different options for values of an element.</span></span> <span data-ttu-id="14742-180">Ad esempio, IntelliSense mostra le due opzioni di Windows o Linux quando si modifica l’elemento **targetOsType** .</span><span class="sxs-lookup"><span data-stu-id="14742-180">For example, IntelliSense show you the two choices of Windows or Linux when editing the **targetOsType** element.</span></span>
4. <span data-ttu-id="14742-181">Archiviare l'elemento in un [archivio git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="14742-181">Store the artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="14742-182">Creare una directory distinta per ogni elemento in cui il nome della directory è identico al nome dell’elemento.</span><span class="sxs-lookup"><span data-stu-id="14742-182">Create a separate directory for each artifact where the directory name is the same as the artifact name.</span></span>
   2. <span data-ttu-id="14742-183">Archiviare il file di definizione dell’elemento (artifactfile.json) nella directory che è stato creata.</span><span class="sxs-lookup"><span data-stu-id="14742-183">Store the artifact definition file (artifactfile.json) in the directory you created.</span></span>
   3. <span data-ttu-id="14742-184">Archiviare gli script a cui viene fatto riferimento tramite il comando di installazione dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="14742-184">Store the scripts that are referenced from the artifact install command.</span></span>
      
      <span data-ttu-id="14742-185">Di seguito è riportato un esempio di come potrebbe apparire una cartella di elementi:</span><span class="sxs-lookup"><span data-stu-id="14742-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Esempio di archivio git dell’elemento](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="14742-187">Aggiungere l'archivio elementi al lab. Vedere l'articolo [Aggiungere un archivio Git per elementi e modelli](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="14742-187">Add the artifacts repository to the lab - Refer to the article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="14742-188">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="14742-188">Related articles</span></span>
* [<span data-ttu-id="14742-189">Come diagnosticare gli errori di elemento in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="14742-189">How to diagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="14742-190">Aggiungere una VM a un dominio di AD esistente usando un modello di Resource Manager in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="14742-190">Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="14742-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="14742-191">Next steps</span></span>
* <span data-ttu-id="14742-192">Informazioni su come [Aggiungere un archivio elementi Git a un lab](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="14742-192">Learn how to [add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>

