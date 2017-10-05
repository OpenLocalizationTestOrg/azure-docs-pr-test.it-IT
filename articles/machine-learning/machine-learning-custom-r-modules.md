---
title: Creare moduli R personalizzati in Azure Machine Learning | Documentazione Microsoft
description: Guida introduttiva alla creazione di moduli R personalizzati in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 964ddb551a475243891abce8a2b835e65569a4ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="f812d-103">Creare moduli R personalizzati in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f812d-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="f812d-104">Questo argomento descrive come creare e distribuire un modulo R personalizzato in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f812d-104">This topic describes how to author and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="f812d-105">Viene descritto in cosa consistono i moduli R personalizzati e i file usati per definirli.</span><span class="sxs-lookup"><span data-stu-id="f812d-105">It explains what custom R modules are and what files are used to define them.</span></span> <span data-ttu-id="f812d-106">Viene illustrato come creare i file che definiscono un modulo e come registrare il modulo per la distribuzione in un'area di lavoro di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f812d-106">It illustrates how to construct the files that define a module and how to register the module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="f812d-107">Vengono quindi descritti in modo più dettagliato elementi e attributi utilizzati nella definizione del modulo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f812d-107">The elements and attributes used in the definition of the custom module are then described in more detail.</span></span> <span data-ttu-id="f812d-108">Viene inoltre illustrato come usare le funzionalità e i file ausiliari e gli output multipli.</span><span class="sxs-lookup"><span data-stu-id="f812d-108">How to use auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="f812d-109">In cosa consiste un modulo R personalizzato?</span><span class="sxs-lookup"><span data-stu-id="f812d-109">What is a custom R module?</span></span>
<span data-ttu-id="f812d-110">Un **modulo personalizzato** è un modulo definito dall'utente che può essere caricato nell'area di lavoro ed eseguito come parte di un esperimento di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f812d-110">A **custom module** is a user-defined module that can be uploaded to your workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="f812d-111">Un **modulo R personalizzato** è un modulo personalizzato che esegue una funzione R definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="f812d-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="f812d-112">**R** è un linguaggio di programmazione per il calcolo e statistico e la grafica ampiamente usato in campo statistico e di analisi dei dati per l'implementazione degli algoritmi.</span><span class="sxs-lookup"><span data-stu-id="f812d-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="f812d-113">R è attualmente l'unico linguaggio supportato nei moduli personalizzati, ma il supporto per altri linguaggi è previsto per le versioni future.</span><span class="sxs-lookup"><span data-stu-id="f812d-113">Currently, R is the only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="f812d-114">In Azure Machine Learning, i moduli personalizzati presentano uno **stato di prima classe** , nel senso che possono essere usati esattamente come qualsiasi altro modulo.</span><span class="sxs-lookup"><span data-stu-id="f812d-114">Custom modules have **first-class status** in Azure Machine Learning in the sense that they can be used just like any other module.</span></span> <span data-ttu-id="f812d-115">Possono essere eseguiti con altri moduli, inclusi nelle visualizzazioni o negli esperimenti pubblicati.</span><span class="sxs-lookup"><span data-stu-id="f812d-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="f812d-116">Gli utenti possono gestire l'algoritmo implementato dal modulo, le porte di input e output da usare, i parametri di modellazione e altri comportamenti di runtime.</span><span class="sxs-lookup"><span data-stu-id="f812d-116">You have control over the algorithm implemented by the module, the input and output ports to be used, the modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="f812d-117">Per una semplice condivisione è anche possibile pubblicare un esperimento contenente moduli personalizzati in Cortana Intelligence Gallery.</span><span class="sxs-lookup"><span data-stu-id="f812d-117">An experiment that contains custom modules can also be published into the Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="f812d-118">File in un modulo R personalizzato</span><span class="sxs-lookup"><span data-stu-id="f812d-118">Files in a custom R module</span></span>
<span data-ttu-id="f812d-119">Un modulo R personalizzato viene definito da un file ZIP che contiene almeno due file:</span><span class="sxs-lookup"><span data-stu-id="f812d-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="f812d-120">Un **file di origine** che implementa la funzione R esposta dal modulo</span><span class="sxs-lookup"><span data-stu-id="f812d-120">A **source file** that implements the R function exposed by the module</span></span>
* <span data-ttu-id="f812d-121">Un **file di definizione XML** che descrive l'interfaccia del modulo personalizzato</span><span class="sxs-lookup"><span data-stu-id="f812d-121">An **XML definition file** that describes the custom module interface</span></span>

<span data-ttu-id="f812d-122">Nel file ZIP è possibile includere anche altri file ausiliari che forniscono funzionalità a cui è possibile accedere dal modulo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f812d-122">Additional auxiliary files can also be included in the .zip file that provides functionality that can be accessed from the custom module.</span></span> <span data-ttu-id="f812d-123">Questa opzione viene trattata nella parte **Argomenti** della sezione di riferimento **Elementi nel file di definizione .xml** dopo l'esempio introduttivo.</span><span class="sxs-lookup"><span data-stu-id="f812d-123">This option is discussed in the **Arguments** part of the reference section **Elements in the XML definition file** following the quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="f812d-124">Esempio di guida introduttiva: definire, creare un pacchetto e registrare un modulo R personalizzato</span><span class="sxs-lookup"><span data-stu-id="f812d-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="f812d-125">In questo esempio viene illustrato come costruire i file richiesti da un modulo R personalizzato, inserirli in un file ZIP e quindi registrare il modulo nell'area di lavoro di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f812d-125">This example illustrates how to construct the files required by a custom R module, package them into a zip file, and then register the module in your Machine Learning workspace.</span></span> <span data-ttu-id="f812d-126">I file e il pacchetto ZIP di esempio possono essere scaricati da [Scarica file CustomAddRows.zip](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="f812d-126">The example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="the-source-file"></a><span data-ttu-id="f812d-127">File di origine</span><span class="sxs-lookup"><span data-stu-id="f812d-127">The source file</span></span>
<span data-ttu-id="f812d-128">Considerare l'esempio di un modulo **Add Rows** (Aggiungi righe) personalizzato che modifica l'implementazione standard del modulo **Add Rows** usato per concatenare le righe (osservazioni) da due set di dati (frame di dati).</span><span class="sxs-lookup"><span data-stu-id="f812d-128">Consider the example of a **Custom Add Rows** module that modifies the standard implementation of the **Add Rows** module used to concatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="f812d-129">Il modulo **Add Rows** standard aggiunge le righe del secondo set di dati di input alla fine del primo set di dati di input usando l'algoritmo `rbind`.</span><span class="sxs-lookup"><span data-stu-id="f812d-129">The standard **Add Rows** module appends the rows of the second input dataset to the end of the first input dataset using the `rbind` algorithm.</span></span> <span data-ttu-id="f812d-130">Analogamente, la funzione `CustomAddRows` personalizzata accetta due set di dati, ma accetta anche un parametro di scambio booleano come input aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="f812d-130">The customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="f812d-131">Se il parametro di scambio è impostato su **FALSE**, restituisce lo stesso set di dati come implementazione standard.</span><span class="sxs-lookup"><span data-stu-id="f812d-131">If the swap parameter is set to **FALSE**, it returns the same data set as the standard implementation.</span></span> <span data-ttu-id="f812d-132">Se tuttavia il parametro di scambio è **TRUE**, la funzione aggiunge righe del primo set di dati di input alla fine del secondo set di dati.</span><span class="sxs-lookup"><span data-stu-id="f812d-132">But if the swap parameter is **TRUE**, the function appends rows of first input dataset to the end of the second dataset instead.</span></span> <span data-ttu-id="f812d-133">Il file CustomAddRows.R che contiene l'implementazione della funzione R `CustomAddRows` , esposta dal modulo **Add Rows personalizzato** , ha il codice R seguente.</span><span class="sxs-lookup"><span data-stu-id="f812d-133">The CustomAddRows.R file that contains the implementation of the R `CustomAddRows` function exposed by the **Custom Add Rows** module has the following R code.</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="the-xml-definition-file"></a><span data-ttu-id="f812d-134">File di definizione XML</span><span class="sxs-lookup"><span data-stu-id="f812d-134">The XML definition file</span></span>
<span data-ttu-id="f812d-135">Per esporre la funzione `CustomAddRows` come modulo di Azure Machine Learning, è necessario creare un file di definizione XML per specificare l'aspetto e il comportamento del modulo **Add Rows personalizzato** .</span><span class="sxs-lookup"><span data-stu-id="f812d-135">To expose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created to specify how the **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another. Dataset 2 is concatenated to Dataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify the base language, script file and R function to use for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: The values of the id attributes in the Input and Arg elements must match the parameter names in the R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>The combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="f812d-136">È essenziale notare che il valore degli attributi **id** degli elementi **Input** e **Arg** nel file XML deve corrispondere ESATTAMENTE ai nomi dei parametri di funzione del codice R nel file CustomAddRows.R (*dataset1*, *dataset2* e *swap* nell'esempio).</span><span class="sxs-lookup"><span data-stu-id="f812d-136">It is critical to note that the value of the **id** attributes of the **Input** and **Arg** elements in the XML file must match the function parameter names of the R code in the CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in the example).</span></span> <span data-ttu-id="f812d-137">Analogamente, il valore dell'attributo **entryPoint** dell'elemento **Language** deve corrispondere ESATTAMENTE al nome della funzione nello script R (*CustomAddRows* nell'esempio).</span><span class="sxs-lookup"><span data-stu-id="f812d-137">Similarly, the value of the **entryPoint** attribute of the **Language** element must match the name of the function in the R script EXACTLY: (*CustomAddRows* in the example).</span></span> 

<span data-ttu-id="f812d-138">Al contrario, l'attributo **id** per l'elemento **Output** non corrisponde ad alcuna variabile nello script R.</span><span class="sxs-lookup"><span data-stu-id="f812d-138">In contrast, the **id** attribute for the **Output** element does not correspond to any variables in the R script.</span></span> <span data-ttu-id="f812d-139">Quando è necessario più di un output, restituire semplicemente un elenco dalla funzione R con i risultati disposti *nello stesso ordine* in cui sono dichiarati gli elementi **Output** nel file XML.</span><span class="sxs-lookup"><span data-stu-id="f812d-139">When more than one output is required, simply return a list from the R function with results placed *in the same order* as **Outputs** elements are declared in the XML file.</span></span>

### <a name="package-and-register-the-module"></a><span data-ttu-id="f812d-140">Creare il pacchetto del modulo e registrarlo</span><span class="sxs-lookup"><span data-stu-id="f812d-140">Package and register the module</span></span>
<span data-ttu-id="f812d-141">Salvare questi due file come *CustomAddRows.R* e *CustomAddRows.xml* e quindi comprimerli insieme nel file *CustomAddRows.zip*.</span><span class="sxs-lookup"><span data-stu-id="f812d-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip the two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="f812d-142">Per registrarli nell'area di lavoro di Machine Learning, accedere all'area di lavoro in Machine Learning Studio, fare clic sul pulsante **+NEW** (+NUOVO) in basso e scegliere **MODULE -> FROM ZIP PACKAGE** (MODULO -> DA PACCHETTO ZIP) per caricare il nuovo modulo **Add Rows personalizzato**.</span><span class="sxs-lookup"><span data-stu-id="f812d-142">To register them in your Machine Learning workspace, go to your workspace in the Machine Learning Studio, click the **+NEW** button on the bottom and choose **MODULE -> FROM ZIP PACKAGE** to upload the new **Custom Add Rows** module.</span></span>

![Caricamento file ZIP](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="f812d-144">Ora è possibile accedere al modulo **Add Rows personalizzato** con gli esperimenti di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f812d-144">The **Custom Add Rows** module is now ready to be accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-the-xml-definition-file"></a><span data-ttu-id="f812d-145">Elementi nel file di definizione .xml</span><span class="sxs-lookup"><span data-stu-id="f812d-145">Elements in the XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="f812d-146">Elementi dei moduli</span><span class="sxs-lookup"><span data-stu-id="f812d-146">Module elements</span></span>
<span data-ttu-id="f812d-147">L'elemento **Module** viene usato per definire un modulo personalizzato nel file XML.</span><span class="sxs-lookup"><span data-stu-id="f812d-147">The **Module** element is used to define a custom module in the XML file.</span></span> <span data-ttu-id="f812d-148">Si possono definire più moduli in un file XML usando più elementi **Module** .</span><span class="sxs-lookup"><span data-stu-id="f812d-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="f812d-149">Ogni modulo nell'area di lavoro deve avere un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="f812d-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="f812d-150">La registrazione di un modulo personalizzato con lo stesso nome di un modulo personalizzato esistente sostituisce il modulo esistente con quello nuovo.</span><span class="sxs-lookup"><span data-stu-id="f812d-150">Register a custom module with the same name as an existing custom module and it replaces the existing module with the new one.</span></span> <span data-ttu-id="f812d-151">I moduli personalizzati possono essere tuttavia registrati con lo stesso nome di un modulo di Azure Machine Learning esistente.</span><span class="sxs-lookup"><span data-stu-id="f812d-151">Custom modules can, however, be registered with the same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="f812d-152">In questo caso verranno visualizzati nella categoria **Custom** (Personalizzati) del pannello dei moduli.</span><span class="sxs-lookup"><span data-stu-id="f812d-152">If so, they appear in the **Custom** category of the module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another...</Description>/> 


<span data-ttu-id="f812d-153">All'interno dell'elemento **Module** è possibile specificare altri due elementi facoltativi:</span><span class="sxs-lookup"><span data-stu-id="f812d-153">Within the **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="f812d-154">un elemento **Owner** che viene incorporato nel modulo</span><span class="sxs-lookup"><span data-stu-id="f812d-154">an **Owner** element that is embedded into the module</span></span>  
* <span data-ttu-id="f812d-155">un elemento **Description** il cui testo viene visualizzato nella Guida rapida per il modulo e quando si passa il mouse sul modulo nell'interfaccia utente di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f812d-155">a **Description** element that contains text that is displayed in quick help for the module and when you hover over the module in the Machine Learning UI.</span></span>

<span data-ttu-id="f812d-156">Regole per i limiti di caratteri negli elementi Module:</span><span class="sxs-lookup"><span data-stu-id="f812d-156">Rules for characters limits in the Module elements:</span></span>

* <span data-ttu-id="f812d-157">Il valore dell'attributo **name** nell'elemento **Module** non deve superare i 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f812d-157">The value of the **name** attribute in the **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="f812d-158">Il contenuto dell'elemento **Description** non deve superare i 128 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f812d-158">The content of the **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="f812d-159">Il contenuto dell'elemento **Owner** non deve superare i 32 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f812d-159">The content of the **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="f812d-160">I risultati di un modulo possono essere deterministici o non deterministici.* * Per impostazione predefinita, tutti i moduli sono considerati deterministici.</span><span class="sxs-lookup"><span data-stu-id="f812d-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered to be deterministic.</span></span> <span data-ttu-id="f812d-161">In altre parole, dato un set di parametri e dati di input non modificabile, il modulo deve restituire gli stessi risultati ogni volta che viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="f812d-161">That is, given an unchanging set of input parameters and data, the module should return the same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="f812d-162">In base a questo comportamento, Azure Machine Learning Studio esegue nuovamente i moduli contrassegnati come deterministici solo in caso di modifica di un parametro o dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="f812d-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or the input data has changed.</span></span> <span data-ttu-id="f812d-163">La restituzione dei risultati memorizzati nella cache offre anche un'esecuzione molto più rapida degli esperimenti.</span><span class="sxs-lookup"><span data-stu-id="f812d-163">Returning the cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="f812d-164">Sono disponibili funzioni non deterministiche, ad esempio RAND o una funzione che restituisce la data o l'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="f812d-164">There are functions that are nondeterministic, such as RAND or a function that returns the current date or time.</span></span> <span data-ttu-id="f812d-165">Se il modulo usa una funzione non deterministica, è possibile indicare che il modulo è non deterministico impostando l'attributo facoltativo **isDeterministic** su **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="f812d-165">If your module uses a nondeterministic function, you can specify that the module is non-deterministic by setting the optional **isDeterministic** attribute to **FALSE**.</span></span> <span data-ttu-id="f812d-166">Il modulo verrà così eseguito nuovamente ogni volta che verrà eseguito l'esperimento, anche se l'input e i parametri del modulo non sono stati modificati.</span><span class="sxs-lookup"><span data-stu-id="f812d-166">This insures that the module is rerun whenever the experiment is run, even if the module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="f812d-167">Definizione lingua</span><span class="sxs-lookup"><span data-stu-id="f812d-167">Language Definition</span></span>
<span data-ttu-id="f812d-168">L'elemento **Language** nel file di definizione XML viene usato per specificare il linguaggio del modulo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f812d-168">The **Language** element in your XML definition file is used to specify the custom module language.</span></span> <span data-ttu-id="f812d-169">R attualmente è l'unico linguaggio supportato.</span><span class="sxs-lookup"><span data-stu-id="f812d-169">Currently, R is the only supported language.</span></span> <span data-ttu-id="f812d-170">Il valore dell'attributo **sourceFile** deve corrispondere al nome del file R che contiene la funzione da chiamare quando viene eseguito il modulo.</span><span class="sxs-lookup"><span data-stu-id="f812d-170">The value of the **sourceFile** attribute must be the name of the R file that contains the function to call when the module is run.</span></span> <span data-ttu-id="f812d-171">Questo file deve far parte del pacchetto zip.</span><span class="sxs-lookup"><span data-stu-id="f812d-171">This file must be part of the zip package.</span></span> <span data-ttu-id="f812d-172">Il valore dell'attributo **entryPoint** è il nome della funzione chiamata e deve corrispondere a una funzione valida definita nel file di origine.</span><span class="sxs-lookup"><span data-stu-id="f812d-172">The value of the **entryPoint** attribute is the name of the function being called and must match a valid function defined with in the source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="f812d-173">Porte</span><span class="sxs-lookup"><span data-stu-id="f812d-173">Ports</span></span>
<span data-ttu-id="f812d-174">Le porte di input e di output per un modulo personalizzato vengono specificate negli elementi figlio della sezione **Ports** del file di definizione XML.</span><span class="sxs-lookup"><span data-stu-id="f812d-174">The input and output ports for a custom module are specified in child elements of the **Ports** section of the XML definition file.</span></span> <span data-ttu-id="f812d-175">L'ordine di questi elementi determina il layout visualizzato (UX) dagli utenti.</span><span class="sxs-lookup"><span data-stu-id="f812d-175">The order of these elements determines the layout experienced (UX) by users.</span></span> <span data-ttu-id="f812d-176">Il primo **input** o **output** figlio elencato nell'elemento **Ports** del file XML diventa la porta di input più a sinistra nell'esperienza utente di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f812d-176">The first child **input** or **output** listed in the **Ports** element of the XML file becomes the left-most input port in the Machine Learning UX.</span></span>
<span data-ttu-id="f812d-177">Ogni porta di input e di output può avere un elemento figlio **Description** facoltativo che specifica il testo visualizzato quando si passa il cursore del mouse sulla porta nell'interfaccia utente di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f812d-177">Each input and output port may have an optional **Description** child element that specifies the text shown when you hover the mouse cursor over the port in the Machine Learning UI.</span></span>

<span data-ttu-id="f812d-178">**Regole porte**:</span><span class="sxs-lookup"><span data-stu-id="f812d-178">**Ports Rules**:</span></span>

* <span data-ttu-id="f812d-179">Il numero massimo di **porte di input e di output** è 8 per ciascuno.</span><span class="sxs-lookup"><span data-stu-id="f812d-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="f812d-180">Elementi di input</span><span class="sxs-lookup"><span data-stu-id="f812d-180">Input elements</span></span>
<span data-ttu-id="f812d-181">Le porte di input consentono di passare i dati all'area di lavoro e alla funzione R.</span><span class="sxs-lookup"><span data-stu-id="f812d-181">Input ports allow you to pass data to your R function and workspace.</span></span> <span data-ttu-id="f812d-182">I **tipi di dati** supportati dalle porte di input e output sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="f812d-182">The **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="f812d-183">**DataTable:** questo tipo viene passato alla funzione R come data.frame.</span><span class="sxs-lookup"><span data-stu-id="f812d-183">**DataTable:** This type is passed to your R function as a data.frame.</span></span> <span data-ttu-id="f812d-184">Infatti tutti i tipi (ad esempio, i file CSV o i file ARFF) supportati da Machine Learning e compatibili con **DataTable** vengono convertiti automaticamente in data.frame.</span><span class="sxs-lookup"><span data-stu-id="f812d-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted to a data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="f812d-185">L'attributo **id** associato a ogni porta di input **DataTable** deve avere un valore univoco che deve corrispondere al relativo parametro denominato nella funzione R.</span><span class="sxs-lookup"><span data-stu-id="f812d-185">The **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="f812d-186">Le porte **DataTable** facoltative che non vengono passate come input in un esperimento passano un valore **NULL** alla funzione R e le porte ZIP facoltative vengono ignorate se l'input non è connesso.</span><span class="sxs-lookup"><span data-stu-id="f812d-186">Optional **DataTable** ports that are not passed as input in an experiment have the value **NULL** passed to the R function and optional zip ports are ignored if the input is not connected.</span></span> <span data-ttu-id="f812d-187">L'attributo **isOptional** è facoltativo per i tipi **DataTable** e **Zip** ed è *false* per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f812d-187">The **isOptional** attribute is optional for both the **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="f812d-188">**Zip:** i moduli personalizzati possono accettare un file ZIP come input.</span><span class="sxs-lookup"><span data-stu-id="f812d-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="f812d-189">Tale input viene decompresso in una directory di esecuzione R della funzione</span><span class="sxs-lookup"><span data-stu-id="f812d-189">This input is unpacked into the R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files to be extracted to the R working directory.</Description>
           </Input>

<span data-ttu-id="f812d-190">Per i moduli R personalizzati non è necessario che l'ID di una porta ZIP corrisponda ai parametri della funzione R</span><span class="sxs-lookup"><span data-stu-id="f812d-190">For custom R modules, the id for a Zip port does not have to match any parameters of the R function.</span></span> <span data-ttu-id="f812d-191">perché il file ZIP viene estratto automaticamente nella directory di lavoro R.</span><span class="sxs-lookup"><span data-stu-id="f812d-191">This is because the zip file is automatically extracted to the R working directory.</span></span>

<span data-ttu-id="f812d-192">**Regole di input:**</span><span class="sxs-lookup"><span data-stu-id="f812d-192">**Input Rules:**</span></span>

* <span data-ttu-id="f812d-193">Il valore dell'attributo **id** dell'elemento **Input** deve essere un nome di variabile R valido.</span><span class="sxs-lookup"><span data-stu-id="f812d-193">The value of the **id** attribute of the **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="f812d-194">Il valore dell'attributo **id** dell'elemento **Input** non deve superare i 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f812d-194">The value of the **id** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="f812d-195">Il valore dell'attributo **name** dell'elemento **Input** non deve superare i 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f812d-195">The value of the **name** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="f812d-196">Il contenuto dell'elemento **Description** non deve superare i 128 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f812d-196">The content of the **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="f812d-197">Il valore dell'attributo **type** dell'elemento **Input** deve essere *Zip* o *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="f812d-197">The value of the **type** attribute of the **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="f812d-198">Il valore dell'attributo **isOptional** dell'elemento **Input** non è obbligatorio (ed è *false* per impostazione predefinita quando non è specificato), ma, se è specificato, deve essere *true* o *false*.</span><span class="sxs-lookup"><span data-stu-id="f812d-198">The value of the **isOptional** attribute of the **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="f812d-199">Elementi di output</span><span class="sxs-lookup"><span data-stu-id="f812d-199">Output elements</span></span>
<span data-ttu-id="f812d-200">**Porte di output standard:** le porte di output corrispondono ai valori restituiti dalla funzione R, che può quindi essere usata dai moduli successivi.</span><span class="sxs-lookup"><span data-stu-id="f812d-200">**Standard output ports:** Output ports are mapped to the return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="f812d-201">*DataTable* è l'unico tipo di porta di output standard attualmente supportato.</span><span class="sxs-lookup"><span data-stu-id="f812d-201">*DataTable* is the only standard output port type supported currently.</span></span> <span data-ttu-id="f812d-202">Il supporto per *Learners* e *Transforms* è di prossima introduzione. Un output *DataTable* è definito come:</span><span class="sxs-lookup"><span data-stu-id="f812d-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="f812d-203">Per gli output in moduli R personalizzati, il valore dell'attributo **id** non deve corrispondere ad alcun elemento nello script R, ma deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="f812d-203">For outputs in custom R modules, the value of the **id** attribute does not have to correspond with anything in the R script, but it must be unique.</span></span> <span data-ttu-id="f812d-204">Per l'output di un modulo singolo, il valore restituito dalla funzione R deve essere un *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="f812d-204">For a single module output, the return value from the R function must be a *data.frame*.</span></span> <span data-ttu-id="f812d-205">Per poter restituire più di un oggetto di un tipo di dati supportato, è necessario specificare le porte di output appropriate nel file di definizione XML e restituire gli oggetti come elenco.</span><span class="sxs-lookup"><span data-stu-id="f812d-205">In order to output more than one object of a supported data type, the appropriate output ports need to be specified in the XML definition file and the objects need to be returned as a list.</span></span> <span data-ttu-id="f812d-206">Gli oggetti di output vengono assegnati alle porte di output da sinistra a destra, in base all'ordine in cui gli oggetti vengono inseriti nell'elenco restituito.</span><span class="sxs-lookup"><span data-stu-id="f812d-206">The output objects are assigned to output ports from left to right, reflecting the order in which the objects are placed in the returned list.</span></span>

<span data-ttu-id="f812d-207">Se ad esempio si vuole modificare il modulo **Add rows personalizzato** per l'output dei due set di dati originali, *dataset1* e *dataset2*, oltre al nuovo set di dati *dataset* unito (in un ordine da sinistra a destra, del tipo *dataset*, *dataset1*, *dataset2*), definire le porte di output nel file CustomAddRows.xml come segue:</span><span class="sxs-lookup"><span data-stu-id="f812d-207">For example, if you want to modify the **Custom Add Rows** module to output the original two datasets, *dataset1* and *dataset2*, in addition to the new joined dataset, *dataset*, (in an order, from left to right, as: *dataset*, *dataset1*, *dataset2*), then define the output ports in the CustomAddRows.xml file as follows:</span></span>

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


<span data-ttu-id="f812d-208">Restituire quindi gli oggetti in un elenco con l'ordine corretto in 'CustomAddRows.R':</span><span class="sxs-lookup"><span data-stu-id="f812d-208">And return the list of objects in a list in the correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="f812d-209">**Output di visualizzazione:** è anche possibile specificare una porta di output di tipo *Visualization*che consente di visualizzare l'output del dispositivo e della console grafica R.</span><span class="sxs-lookup"><span data-stu-id="f812d-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays the output from the R graphics device and console output.</span></span> <span data-ttu-id="f812d-210">Questa porta non fa parte dell'output della funzione R e non interferisce con l'ordine degli altri tipi di porta di output.</span><span class="sxs-lookup"><span data-stu-id="f812d-210">This port is not part of the R function output and does not interfere with the order of the other output port types.</span></span> <span data-ttu-id="f812d-211">Per aggiungere una porta di visualizzazione ai moduli personalizzati, aggiungere un elemento **Output** con un valore *Visualization* per il relativo attributo **type**:</span><span class="sxs-lookup"><span data-stu-id="f812d-211">To add a visualization port to the custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View the R console graphics device output.</Description>
    </Output>

<span data-ttu-id="f812d-212">**Regole di output:**</span><span class="sxs-lookup"><span data-stu-id="f812d-212">**Output Rules:**</span></span>

* <span data-ttu-id="f812d-213">Il valore dell'attributo **id** dell'elemento **Output** deve essere un nome di variabile R valido.</span><span class="sxs-lookup"><span data-stu-id="f812d-213">The value of the **id** attribute of the **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="f812d-214">Il valore dell'attributo **id** dell'elemento **Output** non deve superare i 32 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f812d-214">The value of the **id** attribute of the **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="f812d-215">Il valore dell'attributo **name** dell'elemento **Output** non deve superare i 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f812d-215">The value of the **name** attribute of the **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="f812d-216">Il valore dell'attributo **type** dell'elemento **Output** deve essere *Visualization*.</span><span class="sxs-lookup"><span data-stu-id="f812d-216">The value of the **type** attribute of the **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="f812d-217">Argomenti</span><span class="sxs-lookup"><span data-stu-id="f812d-217">Arguments</span></span>
<span data-ttu-id="f812d-218">Dati aggiuntivi possono essere passati alla funzione R con i parametri del modulo definiti nell'elemento **Arguments**.</span><span class="sxs-lookup"><span data-stu-id="f812d-218">Additional data can be passed to the R function via module parameters which are defined in the **Arguments** element.</span></span> <span data-ttu-id="f812d-219">Questi parametri vengono visualizzati nel riquadro delle proprietà più a destra dell'interfaccia utente di Machine Learning quando viene selezionato il modulo.</span><span class="sxs-lookup"><span data-stu-id="f812d-219">These parameters appear in the rightmost properties pane of the Machine Learning UI when the module is selected.</span></span> <span data-ttu-id="f812d-220">Gli argomenti possono essere uno qualsiasi dei tipi supportati. In alternativa, è possibile creare un enumeratore personalizzato, se necessario.</span><span class="sxs-lookup"><span data-stu-id="f812d-220">Arguments can be any of the supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="f812d-221">Analogamente agli elementi **Ports**, gli elementi **Arguments** possono presentare un elemento **Description** facoltativo che specifica il testo visualizzato quando si posiziona il mouse sul nome del parametro.</span><span class="sxs-lookup"><span data-stu-id="f812d-221">Similar to the **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies the text that appears when you hover the mouse over the parameter name.</span></span>
<span data-ttu-id="f812d-222">Le proprietà facoltative per un modulo, quali defaultValue, minValue e maxValue, possono essere aggiunte a qualsiasi argomento come attributi di un elemento **Properties**.</span><span class="sxs-lookup"><span data-stu-id="f812d-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added to any argument as attributes to a **Properties** element.</span></span> <span data-ttu-id="f812d-223">Le proprietà valide per l'elemento **Properties** dipendono dal tipo di argomento e vengono descritte con i tipi di argomento supportati nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="f812d-223">Valid properties for the **Properties** element depend on the argument type and are described with the supported argument types in the next section.</span></span> <span data-ttu-id="f812d-224">Gli argomenti con la proprietà **isOptional** impostata su **"true"** non richiedono che l'utente immetta un valore.</span><span class="sxs-lookup"><span data-stu-id="f812d-224">Arguments with the **isOptional** property set to **"true"** do not require the user to enter a value.</span></span> <span data-ttu-id="f812d-225">Se non viene fornito un valore per l'argomento, l'argomento non verrà passato alla funzione del punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="f812d-225">If a value is not provided to the argument, then the argument is not passed to the entry point function.</span></span> <span data-ttu-id="f812d-226">Gli argomenti della funzione del punto di ingresso facoltativi devono essere gestiti in modo esplicito dalla funzione, ad esempio viene assegnato un valore predefinito NULL nella definizione della funzione del punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="f812d-226">Arguments of the entry point function that are optional need to be explicitly handled by the function, e.g. assigned a default value of NULL in the entry point function definition.</span></span> <span data-ttu-id="f812d-227">Un argomento facoltativo imporrà gli altri vincoli dell'argomento, ad esempio min o max, solo se l'utente fornisce un valore.</span><span class="sxs-lookup"><span data-stu-id="f812d-227">An optional argument will only enforce the other argument constraints, i.e. min or max, if a value is provided by the user.</span></span>
<span data-ttu-id="f812d-228">Così come con input e output, è fondamentale che ogni parametro presenti valori ID univoci associati.</span><span class="sxs-lookup"><span data-stu-id="f812d-228">As with inputs and outputs, it is critical that each of the parameters have unique id values associated with them.</span></span> <span data-ttu-id="f812d-229">Nell'esempio di avvio rapido il parametro/id associato era *swap*.</span><span class="sxs-lookup"><span data-stu-id="f812d-229">In our quick start example the associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="f812d-230">Elemento Arg</span><span class="sxs-lookup"><span data-stu-id="f812d-230">Arg element</span></span>
<span data-ttu-id="f812d-231">Un parametro del modulo viene definito con l'elemento figlio **Arg** della sezione **Arguments** del file di definizione XML.</span><span class="sxs-lookup"><span data-stu-id="f812d-231">A module parameter is defined using the **Arg** child element of the **Arguments** section of the XML definition file.</span></span> <span data-ttu-id="f812d-232">Come con gli elementi figlio nella sezione **Ports**, l'ordine dei parametri nella sezione **Arguments** definisce il layout riscontrato nell'esperienza utente.</span><span class="sxs-lookup"><span data-stu-id="f812d-232">As with the child elements in the **Ports** section, the ordering of parameters in the **Arguments** section defines the layout encountered in the UX.</span></span> <span data-ttu-id="f812d-233">I parametri vengono visualizzati dall'alto verso il basso nell'interfaccia utente nello stesso ordine in cui sono definiti nel file XML.</span><span class="sxs-lookup"><span data-stu-id="f812d-233">The parameters appear from top down in the UI in the same order in which they are defined in the XML file.</span></span> <span data-ttu-id="f812d-234">I tipi supportati da Machine Learning per i parametri sono elencati di seguito.</span><span class="sxs-lookup"><span data-stu-id="f812d-234">The types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="f812d-235">**int** : parametro di tipo Integer (32 bit).</span><span class="sxs-lookup"><span data-stu-id="f812d-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="f812d-236">*Proprietà facoltative*: **min**, **max**, **default** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="f812d-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="f812d-237">**double** : parametro di tipo doppio.</span><span class="sxs-lookup"><span data-stu-id="f812d-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="f812d-238">*Proprietà facoltative*: **min**, **max**, **default** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="f812d-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="f812d-239">**bool** : parametro booleano rappresentato da una casella di controllo nell'esperienza utente.</span><span class="sxs-lookup"><span data-stu-id="f812d-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="f812d-240">*Proprietà facoltative*: **default** (false se non impostato)</span><span class="sxs-lookup"><span data-stu-id="f812d-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="f812d-241">**string**: stringa standard</span><span class="sxs-lookup"><span data-stu-id="f812d-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="f812d-242">*Proprietà facoltative*: **default** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="f812d-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="f812d-243">**ColumnPicker**: parametro di selezione della colonna.</span><span class="sxs-lookup"><span data-stu-id="f812d-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="f812d-244">Questo tipo esegue il rendering in UX come selezione di colonne.</span><span class="sxs-lookup"><span data-stu-id="f812d-244">This type renders in the UX as a column chooser.</span></span> <span data-ttu-id="f812d-245">L'elemento **Property** viene usato per specificare l'ID della porta dal quale verranno selezionate le colonne, in cui il tipo di porta di destinazione deve essere *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="f812d-245">The **Property** element is used here to specify the id of the port from which columns are selected, where the target port type must be *DataTable*.</span></span> <span data-ttu-id="f812d-246">Il risultato della selezione delle colonne verrà passato alla funzione R come elenco di stringhe contenenti i nomi di colonna selezionati.</span><span class="sxs-lookup"><span data-stu-id="f812d-246">The result of the column selection is passed to the R function as a list of strings containing the selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="f812d-247">*Proprietà obbligatorie*: **portId**. Corrisponde all'ID di un elemento Input di tipo *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="f812d-247">*Required Properties*: **portId** - matches the id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="f812d-248">*Proprietà facoltative*:</span><span class="sxs-lookup"><span data-stu-id="f812d-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="f812d-249">**allowedTypes** : filtra i tipi di colonna tra cui è possibile scegliere.</span><span class="sxs-lookup"><span data-stu-id="f812d-249">**allowedTypes** - Filters the column types from which you can pick.</span></span> <span data-ttu-id="f812d-250">I valori validi includono:</span><span class="sxs-lookup"><span data-stu-id="f812d-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="f812d-251">Numeric</span><span class="sxs-lookup"><span data-stu-id="f812d-251">Numeric</span></span>
    * <span data-ttu-id="f812d-252">Boolean</span><span class="sxs-lookup"><span data-stu-id="f812d-252">Boolean</span></span>
    * <span data-ttu-id="f812d-253">Categorical</span><span class="sxs-lookup"><span data-stu-id="f812d-253">Categorical</span></span>
    * <span data-ttu-id="f812d-254">string</span><span class="sxs-lookup"><span data-stu-id="f812d-254">String</span></span>
    * <span data-ttu-id="f812d-255">Etichetta</span><span class="sxs-lookup"><span data-stu-id="f812d-255">Label</span></span>
    * <span data-ttu-id="f812d-256">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="f812d-256">Feature</span></span>
    * <span data-ttu-id="f812d-257">Score</span><span class="sxs-lookup"><span data-stu-id="f812d-257">Score</span></span>
    * <span data-ttu-id="f812d-258">Tutti</span><span class="sxs-lookup"><span data-stu-id="f812d-258">All</span></span>
  * <span data-ttu-id="f812d-259">**default** : le selezioni predefinite valide per il selettore di colonna includono:</span><span class="sxs-lookup"><span data-stu-id="f812d-259">**default** - Valid default selections for the column picker include:</span></span> 
    
    * <span data-ttu-id="f812d-260">None</span><span class="sxs-lookup"><span data-stu-id="f812d-260">None</span></span>
    * <span data-ttu-id="f812d-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="f812d-261">NumericFeature</span></span>
    * <span data-ttu-id="f812d-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="f812d-262">NumericLabel</span></span>
    * <span data-ttu-id="f812d-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="f812d-263">NumericScore</span></span>
    * <span data-ttu-id="f812d-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="f812d-264">NumericAll</span></span>
    * <span data-ttu-id="f812d-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="f812d-265">BooleanFeature</span></span>
    * <span data-ttu-id="f812d-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="f812d-266">BooleanLabel</span></span>
    * <span data-ttu-id="f812d-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="f812d-267">BooleanScore</span></span>
    * <span data-ttu-id="f812d-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="f812d-268">BooleanAll</span></span>
    * <span data-ttu-id="f812d-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="f812d-269">CategoricalFeature</span></span>
    * <span data-ttu-id="f812d-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="f812d-270">CategoricalLabel</span></span>
    * <span data-ttu-id="f812d-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="f812d-271">CategoricalScore</span></span>
    * <span data-ttu-id="f812d-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="f812d-272">CategoricalAll</span></span>
    * <span data-ttu-id="f812d-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="f812d-273">StringFeature</span></span>
    * <span data-ttu-id="f812d-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="f812d-274">StringLabel</span></span>
    * <span data-ttu-id="f812d-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="f812d-275">StringScore</span></span>
    * <span data-ttu-id="f812d-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="f812d-276">StringAll</span></span>
    * <span data-ttu-id="f812d-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="f812d-277">AllLabel</span></span>
    * <span data-ttu-id="f812d-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="f812d-278">AllFeature</span></span>
    * <span data-ttu-id="f812d-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="f812d-279">AllScore</span></span>
    * <span data-ttu-id="f812d-280">Tutti</span><span class="sxs-lookup"><span data-stu-id="f812d-280">All</span></span>

<span data-ttu-id="f812d-281">**DropDown**: elenco enumerato specificato dall'utente (elenco a discesa).</span><span class="sxs-lookup"><span data-stu-id="f812d-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="f812d-282">Gli elementi dell'elenco a discesa vengono specificati all'interno dell'elemento **Properties** usando un elemento **Item**.</span><span class="sxs-lookup"><span data-stu-id="f812d-282">The dropdown items are specified within the **Properties** element using an **Item** element.</span></span> <span data-ttu-id="f812d-283">L'**id** di ciascun elemento **Item** deve essere univoco e una variabile R valida.</span><span class="sxs-lookup"><span data-stu-id="f812d-283">The **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="f812d-284">Il valore di **name** di un elemento **Item** rappresenta sia il testo visualizzato che il valore passato alla funzione R.</span><span class="sxs-lookup"><span data-stu-id="f812d-284">The value of the **name** of an **Item** serves as both the text that you see and the value that is passed to the R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="f812d-285">*Proprietà facoltative*:</span><span class="sxs-lookup"><span data-stu-id="f812d-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="f812d-286">**default**: il valore della proprietà predefinita deve corrispondere a un valore ID di uno degli elementi **Item**.</span><span class="sxs-lookup"><span data-stu-id="f812d-286">**default** - The value for the default property must correspond with an id value from one of the **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="f812d-287">File ausiliari</span><span class="sxs-lookup"><span data-stu-id="f812d-287">Auxiliary Files</span></span>
<span data-ttu-id="f812d-288">Qualsiasi file inserito nel file ZIP del modulo personalizzato sarà disponibile per l'uso durante la fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f812d-288">Any file that is placed in your custom module ZIP file is going to be available for use during execution time.</span></span> <span data-ttu-id="f812d-289">Vengono mantenute le strutture di directory presenti.</span><span class="sxs-lookup"><span data-stu-id="f812d-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="f812d-290">Ciò significa che l'esecuzione del file funziona nello stesso modo sia localmente che in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f812d-290">This means that file sourcing works the same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="f812d-291">Si noti che tutti i file vengono estratti nella directory 'src', quindi tutti i percorsi avranno il prefisso 'src /'.</span><span class="sxs-lookup"><span data-stu-id="f812d-291">Notice that all files are extracted to ‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="f812d-292">Ad esempio, si supponga di voler rimuovere tutte le righe con NAs e tutte le righe duplicate nel set di dati prima di eseguire l'output in CustomAddRows e di avere già scritto una funzione R che esegue tale operazione in un file RemoveDupNARows.R:</span><span class="sxs-lookup"><span data-stu-id="f812d-292">For example, say you want to remove any rows with NAs from the dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="f812d-293">È possibile usare il file ausiliario RemoveDupNARows.R nella funzione CustomAddRows:</span><span class="sxs-lookup"><span data-stu-id="f812d-293">You can source the auxiliary file RemoveDupNARows.R in the CustomAddRows function:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

<span data-ttu-id="f812d-294">Quindi, caricare il file ZIP contenente 'CustomAddRows.R', 'CustomAddRows.xml' e 'RemoveDupNARows.R' come modulo R personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f812d-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="f812d-295">Ambiente di esecuzione</span><span class="sxs-lookup"><span data-stu-id="f812d-295">Execution Environment</span></span>
<span data-ttu-id="f812d-296">L'ambiente di esecuzione dello script R usa la stessa versione di R del modulo **Esegui script R** e può usare gli stessi pacchetti predefiniti.</span><span class="sxs-lookup"><span data-stu-id="f812d-296">The execution environment for the R script uses the same version of R as the **Execute R Script** module and can use the same default packages.</span></span> <span data-ttu-id="f812d-297">È anche possibile aggiungere altri pacchetti R al modulo personalizzato includendoli nel pacchetto ZIP del modulo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f812d-297">You can also add additional R packages to your custom module by including them in the custom module zip package.</span></span> <span data-ttu-id="f812d-298">È sufficiente caricare i pacchetti nello script R come si farebbe nel proprio ambiente R.</span><span class="sxs-lookup"><span data-stu-id="f812d-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="f812d-299">**limitazioni dell'ambiente di esecuzione** includono:</span><span class="sxs-lookup"><span data-stu-id="f812d-299">**Limitations of the execution environment** include:</span></span>

* <span data-ttu-id="f812d-300">File system non persistente: i file scritti quando viene eseguito il modulo personalizzato non vengono mantenuti in più esecuzioni dello stesso modulo.</span><span class="sxs-lookup"><span data-stu-id="f812d-300">Non-persistent file system: Files written when the custom module is run are not persisted across multiple runs of the same module.</span></span>
* <span data-ttu-id="f812d-301">Nessun accesso alla rete</span><span class="sxs-lookup"><span data-stu-id="f812d-301">No network access</span></span>

