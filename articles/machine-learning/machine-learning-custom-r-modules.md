---
title: i moduli R personalizzati in Azure Machine Learning aaaAuthor | Documenti Microsoft
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
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="f6acc-103">Creare moduli R personalizzati in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f6acc-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="f6acc-104">Questo argomento viene descritto come tooauthor e distribuire un modulo R personalizzato in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f6acc-104">This topic describes how tooauthor and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="f6acc-105">Viene spiegato che cosa sono i moduli R personalizzati e quali sono i file toodefine utilizzato li.</span><span class="sxs-lookup"><span data-stu-id="f6acc-105">It explains what custom R modules are and what files are used toodefine them.</span></span> <span data-ttu-id="f6acc-106">Viene illustrato come tooconstruct hello file che definiscono un modulo e come tooregister hello modulo per la distribuzione in un'area di lavoro di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f6acc-106">It illustrates how tooconstruct hello files that define a module and how tooregister hello module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="f6acc-107">Hello elementi e attributi utilizzati nella definizione di hello del modulo personalizzata hello vengono descritti più dettagliatamente.</span><span class="sxs-lookup"><span data-stu-id="f6acc-107">hello elements and attributes used in hello definition of hello custom module are then described in more detail.</span></span> <span data-ttu-id="f6acc-108">Come viene anche illustrata toouse ausiliario funzionalità e i file e più output.</span><span class="sxs-lookup"><span data-stu-id="f6acc-108">How toouse auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="f6acc-109">In cosa consiste un modulo R personalizzato?</span><span class="sxs-lookup"><span data-stu-id="f6acc-109">What is a custom R module?</span></span>
<span data-ttu-id="f6acc-110">Oggetto **modulo personalizzato** è un modulo definito dall'utente che può essere caricato tooyour dell'area di lavoro ed eseguito come parte di un esperimento di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f6acc-110">A **custom module** is a user-defined module that can be uploaded tooyour workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="f6acc-111">Un **modulo R personalizzato** è un modulo personalizzato che esegue una funzione R definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="f6acc-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="f6acc-112">**R** è un linguaggio di programmazione per il calcolo e statistico e la grafica ampiamente usato in campo statistico e di analisi dei dati per l'implementazione degli algoritmi.</span><span class="sxs-lookup"><span data-stu-id="f6acc-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="f6acc-113">R è attualmente hello unica lingua supportata in moduli personalizzati, ma il supporto per lingue aggiuntive è pianificata per le versioni future.</span><span class="sxs-lookup"><span data-stu-id="f6acc-113">Currently, R is hello only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="f6acc-114">I moduli personalizzati hanno **stato di prima classe** in Azure Machine Learning nel senso hello che possono essere usati come qualsiasi altro modulo.</span><span class="sxs-lookup"><span data-stu-id="f6acc-114">Custom modules have **first-class status** in Azure Machine Learning in hello sense that they can be used just like any other module.</span></span> <span data-ttu-id="f6acc-115">Possono essere eseguiti con altri moduli, inclusi nelle visualizzazioni o negli esperimenti pubblicati.</span><span class="sxs-lookup"><span data-stu-id="f6acc-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="f6acc-116">È necessario controllare algoritmo hello implementato dal modulo hello, hello toobe porte di input e output utilizzati, hello modellazione parametri e altri comportamenti di runtime diversi.</span><span class="sxs-lookup"><span data-stu-id="f6acc-116">You have control over hello algorithm implemented by hello module, hello input and output ports toobe used, hello modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="f6acc-117">Un esperimento che contiene i moduli personalizzati può essere pubblicato anche in hello Cortana Intelligence Gallery per la condivisione semplice.</span><span class="sxs-lookup"><span data-stu-id="f6acc-117">An experiment that contains custom modules can also be published into hello Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="f6acc-118">File in un modulo R personalizzato</span><span class="sxs-lookup"><span data-stu-id="f6acc-118">Files in a custom R module</span></span>
<span data-ttu-id="f6acc-119">Un modulo R personalizzato viene definito da un file ZIP che contiene almeno due file:</span><span class="sxs-lookup"><span data-stu-id="f6acc-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="f6acc-120">Oggetto **file di origine** che implementa una funzione hello R esposta dal modulo hello</span><span class="sxs-lookup"><span data-stu-id="f6acc-120">A **source file** that implements hello R function exposed by hello module</span></span>
* <span data-ttu-id="f6acc-121">Un **file di definizione XML** che descrive l'interfaccia del modulo personalizzata hello</span><span class="sxs-lookup"><span data-stu-id="f6acc-121">An **XML definition file** that describes hello custom module interface</span></span>

<span data-ttu-id="f6acc-122">I file ausiliari aggiuntivi possono essere inclusi anche nel file con estensione zip hello che fornisce funzionalità di cui è possibile accedere dal modulo personalizzato hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-122">Additional auxiliary files can also be included in hello .zip file that provides functionality that can be accessed from hello custom module.</span></span> <span data-ttu-id="f6acc-123">Questa opzione viene trattata in hello **argomenti** fa parte della sezione di riferimento hello **elementi nel file di definizione XML hello** hello avvio rapido esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="f6acc-123">This option is discussed in hello **Arguments** part of hello reference section **Elements in hello XML definition file** following hello quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="f6acc-124">Esempio di guida introduttiva: definire, creare un pacchetto e registrare un modulo R personalizzato</span><span class="sxs-lookup"><span data-stu-id="f6acc-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="f6acc-125">Questo esempio viene illustrato come tooconstruct hello i file necessari per un modulo R personalizzato, inserirle in un pacchetto in un file zip e quindi registrare hello modulo nell'area di lavoro di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f6acc-125">This example illustrates how tooconstruct hello files required by a custom R module, package them into a zip file, and then register hello module in your Machine Learning workspace.</span></span> <span data-ttu-id="f6acc-126">Hello esempio pacchetti di esempio con estensione zip può essere scaricato da [CustomAddRows.zip scaricare file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="f6acc-126">hello example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="hello-source-file"></a><span data-ttu-id="f6acc-127">file di origine Hello</span><span class="sxs-lookup"><span data-stu-id="f6acc-127">hello source file</span></span>
<span data-ttu-id="f6acc-128">Si consideri ad esempio hello un **personalizzato Add Rows** modulo che modifica l'implementazione standard di hello di hello **Add Rows** modulo utilizzato tooconcatenate righe (osservazioni) da due set di dati (frame di dati).</span><span class="sxs-lookup"><span data-stu-id="f6acc-128">Consider hello example of a **Custom Add Rows** module that modifies hello standard implementation of hello **Add Rows** module used tooconcatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="f6acc-129">Hello standard **Add Rows** modulo aggiunge righe hello di hello secondo set di dati input toohello fine hello primo input set di dati utilizzando hello `rbind` algoritmo.</span><span class="sxs-lookup"><span data-stu-id="f6acc-129">hello standard **Add Rows** module appends hello rows of hello second input dataset toohello end of hello first input dataset using hello `rbind` algorithm.</span></span> <span data-ttu-id="f6acc-130">Hello personalizzato `CustomAddRows` funzione Analogamente accetta due set di dati, ma accetta inoltre un parametro booleano swap come un input aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="f6acc-130">hello customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="f6acc-131">Se il parametro di scambio hello è troppo**FALSE**, restituisce hello stesso set di dati come hello implementazione standard.</span><span class="sxs-lookup"><span data-stu-id="f6acc-131">If hello swap parameter is set too**FALSE**, it returns hello same data set as hello standard implementation.</span></span> <span data-ttu-id="f6acc-132">Tuttavia, se il parametro di scambio hello è **TRUE**, la funzione hello aggiunge invece di righe del primo set di dati input toohello fine hello secondo set di dati.</span><span class="sxs-lookup"><span data-stu-id="f6acc-132">But if hello swap parameter is **TRUE**, hello function appends rows of first input dataset toohello end of hello second dataset instead.</span></span> <span data-ttu-id="f6acc-133">file CustomAddRows.R Hello che contiene l'implementazione di hello di hello R `CustomAddRows` funzione esposta da hello **personalizzato Add Rows** modulo ha hello seguente codice R.</span><span class="sxs-lookup"><span data-stu-id="f6acc-133">hello CustomAddRows.R file that contains hello implementation of hello R `CustomAddRows` function exposed by hello **Custom Add Rows** module has hello following R code.</span></span>

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

### <a name="hello-xml-definition-file"></a><span data-ttu-id="f6acc-134">file di definizione XML Hello</span><span class="sxs-lookup"><span data-stu-id="f6acc-134">hello XML definition file</span></span>
<span data-ttu-id="f6acc-135">tooexpose questo `CustomAddRows` funzione come un modulo di Azure Machine Learning, un file di definizione XML deve essere creato toospecify come hello **personalizzato Add Rows** modulo debba aspetto e comportamento.</span><span class="sxs-lookup"><span data-stu-id="f6acc-135">tooexpose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created toospecify how hello **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="f6acc-136">È toonote critici che hello valore hello **id** gli attributi di hello **Input** e **Arg** elementi nel file XML di hello devono corrispondere i nomi dei parametri di funzione hello di hello R codice nel file CustomAddRows.R hello esattamente: (*dataset1*, *dataset2*, e *scambio* nell'esempio hello).</span><span class="sxs-lookup"><span data-stu-id="f6acc-136">It is critical toonote that hello value of hello **id** attributes of hello **Input** and **Arg** elements in hello XML file must match hello function parameter names of hello R code in hello CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in hello example).</span></span> <span data-ttu-id="f6acc-137">Analogamente, hello valore hello **entryPoint** attributo di hello **Language** elemento deve corrispondere esattamente a nome hello della funzione hello nello script R hello: (*CustomAddRows* Nell'esempio hello).</span><span class="sxs-lookup"><span data-stu-id="f6acc-137">Similarly, hello value of hello **entryPoint** attribute of hello **Language** element must match hello name of hello function in hello R script EXACTLY: (*CustomAddRows* in hello example).</span></span> 

<span data-ttu-id="f6acc-138">Al contrario, hello **id** attributo per hello **Output** elemento non corrisponde a variabili tooany nello script R hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-138">In contrast, hello **id** attribute for hello **Output** element does not correspond tooany variables in hello R script.</span></span> <span data-ttu-id="f6acc-139">Quando più di un output è obbligatorio, restituire semplicemente un elenco dalla funzione hello R con risultati inseriti *in hello stesso ordine* come **output** elementi vengono dichiarati nel file XML di hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-139">When more than one output is required, simply return a list from hello R function with results placed *in hello same order* as **Outputs** elements are declared in hello XML file.</span></span>

### <a name="package-and-register-hello-module"></a><span data-ttu-id="f6acc-140">Pacchetto e registrare il modulo di hello</span><span class="sxs-lookup"><span data-stu-id="f6acc-140">Package and register hello module</span></span>
<span data-ttu-id="f6acc-141">Salvare questi file come due *CustomAddRows.R* e *CustomAddRows.xml* e quindi zip hello due file insieme in un *CustomAddRows.zip* file.</span><span class="sxs-lookup"><span data-stu-id="f6acc-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip hello two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="f6acc-142">Nell'area di lavoro Machine Learning, dell'area di lavoro tooyour andare in hello Machine Learning Studio, fare clic su hello tooregister **+ nuovo** pulsante nella parte inferiore di hello **modulo -> dal pacchetto ZIP** tooupload nuovo Hello **personalizzato Add Rows** modulo.</span><span class="sxs-lookup"><span data-stu-id="f6acc-142">tooregister them in your Machine Learning workspace, go tooyour workspace in hello Machine Learning Studio, click hello **+NEW** button on hello bottom and choose **MODULE -> FROM ZIP PACKAGE** tooupload hello new **Custom Add Rows** module.</span></span>

![Caricamento file ZIP](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="f6acc-144">Hello **personalizzato Add Rows** modulo è ora pronto toobe accedere tramite gli esperimenti di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f6acc-144">hello **Custom Add Rows** module is now ready toobe accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-hello-xml-definition-file"></a><span data-ttu-id="f6acc-145">Elementi nel file di definizione XML hello</span><span class="sxs-lookup"><span data-stu-id="f6acc-145">Elements in hello XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="f6acc-146">Elementi dei moduli</span><span class="sxs-lookup"><span data-stu-id="f6acc-146">Module elements</span></span>
<span data-ttu-id="f6acc-147">Hello **modulo** elemento è toodefine usato un modulo personalizzato nel file XML di hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-147">hello **Module** element is used toodefine a custom module in hello XML file.</span></span> <span data-ttu-id="f6acc-148">Si possono definire più moduli in un file XML usando più elementi **Module** .</span><span class="sxs-lookup"><span data-stu-id="f6acc-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="f6acc-149">Ogni modulo nell'area di lavoro deve avere un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="f6acc-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="f6acc-150">Registrare un modulo personalizzato con hello stesso nome di un modulo personalizzato esistente e sostituisce un modulo esistente hello con hello uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="f6acc-150">Register a custom module with hello same name as an existing custom module and it replaces hello existing module with hello new one.</span></span> <span data-ttu-id="f6acc-151">Moduli personalizzati, tuttavia, possono essere registrato con hello stesso nome di un modulo di Azure Machine Learning esistente.</span><span class="sxs-lookup"><span data-stu-id="f6acc-151">Custom modules can, however, be registered with hello same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="f6acc-152">Se in tal caso, sono visualizzate in hello **personalizzato** categoria della tavolozza modulo hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-152">If so, they appear in hello **Custom** category of hello module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


<span data-ttu-id="f6acc-153">All'interno di hello **modulo** elemento, è possibile specificare due elementi facoltativi aggiuntivi:</span><span class="sxs-lookup"><span data-stu-id="f6acc-153">Within hello **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="f6acc-154">un **proprietario** elemento che viene incorporata nel modulo hello</span><span class="sxs-lookup"><span data-stu-id="f6acc-154">an **Owner** element that is embedded into hello module</span></span>  
* <span data-ttu-id="f6acc-155">un **descrizione** elemento che contiene il testo che viene visualizzato nella Guida rapida per il modulo hello e quando si posiziona su modulo hello in hello dell'interfaccia utente di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f6acc-155">a **Description** element that contains text that is displayed in quick help for hello module and when you hover over hello module in hello Machine Learning UI.</span></span>

<span data-ttu-id="f6acc-156">Regole per i limiti di caratteri in elementi modulo hello:</span><span class="sxs-lookup"><span data-stu-id="f6acc-156">Rules for characters limits in hello Module elements:</span></span>

* <span data-ttu-id="f6acc-157">valore di hello Hello **nome** attributo hello **modulo** elemento non deve superare i 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f6acc-157">hello value of hello **name** attribute in hello **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="f6acc-158">contenuto di hello Hello **descrizione** elemento non deve superare i 128 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f6acc-158">hello content of hello **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="f6acc-159">contenuto di hello Hello **proprietario** elemento non deve superare i 32 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f6acc-159">hello content of hello **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="f6acc-160">I risultati di un modulo possono essere deterministici o nondeterministic.* * per impostazione predefinita, tutti i moduli vengono considerati toobe deterministica.</span><span class="sxs-lookup"><span data-stu-id="f6acc-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered toobe deterministic.</span></span> <span data-ttu-id="f6acc-161">Vale a dire, dato un set di parametri di input e di dati rimane invariato, modulo hello deve restituire hello stesso risultati eacRAND o functionh ora che viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="f6acc-161">That is, given an unchanging set of input parameters and data, hello module should return hello same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="f6acc-162">Questo comportamento, Azure Machine Learning Studio riesegue solo moduli contrassegnati come deterministica se un parametro o i dati di input hello sono stato modificato.</span><span class="sxs-lookup"><span data-stu-id="f6acc-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or hello input data has changed.</span></span> <span data-ttu-id="f6acc-163">Restituzione di risultati memorizzati nella cache di hello fornisce inoltre quantità velocizzare l'esecuzione di esperimenti.</span><span class="sxs-lookup"><span data-stu-id="f6acc-163">Returning hello cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="f6acc-164">Sono disponibili funzioni che sono non deterministiche, ad esempio RAND o una funzione che restituisce hello data o ora.</span><span class="sxs-lookup"><span data-stu-id="f6acc-164">There are functions that are nondeterministic, such as RAND or a function that returns hello current date or time.</span></span> <span data-ttu-id="f6acc-165">Se il modulo utilizza una funzione non deterministica, è possibile specificare tale modulo hello è non deterministico per l'impostazione facoltativa hello **isDeterministic** attributo troppo**FALSE**.</span><span class="sxs-lookup"><span data-stu-id="f6acc-165">If your module uses a nondeterministic function, you can specify that hello module is non-deterministic by setting hello optional **isDeterministic** attribute too**FALSE**.</span></span> <span data-ttu-id="f6acc-166">In questo modo si assicura che modulo hello viene eseguito di nuovo ogni volta che viene eseguito l'esperimento hello, anche se hello modulo parametri di input e non sono stati modificati.</span><span class="sxs-lookup"><span data-stu-id="f6acc-166">This insures that hello module is rerun whenever hello experiment is run, even if hello module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="f6acc-167">Definizione lingua</span><span class="sxs-lookup"><span data-stu-id="f6acc-167">Language Definition</span></span>
<span data-ttu-id="f6acc-168">Hello **Language** elemento nel file di definizione XML viene utilizzato toospecify hello modulo personalizzato language.</span><span class="sxs-lookup"><span data-stu-id="f6acc-168">hello **Language** element in your XML definition file is used toospecify hello custom module language.</span></span> <span data-ttu-id="f6acc-169">R è attualmente hello solo lingua supportata.</span><span class="sxs-lookup"><span data-stu-id="f6acc-169">Currently, R is hello only supported language.</span></span> <span data-ttu-id="f6acc-170">valore di hello Hello **sourceFile** attributo deve essere il nome di hello del file hello R contenente toocall funzione hello quando viene eseguito il modulo hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-170">hello value of hello **sourceFile** attribute must be hello name of hello R file that contains hello function toocall when hello module is run.</span></span> <span data-ttu-id="f6acc-171">Questo file deve essere parte del pacchetto zip hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-171">This file must be part of hello zip package.</span></span> <span data-ttu-id="f6acc-172">valore di hello Hello **entryPoint** attributo hello nome di funzione hello chiamata e deve corrispondere a una funzione valida definita con nel file di origine hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-172">hello value of hello **entryPoint** attribute is hello name of hello function being called and must match a valid function defined with in hello source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="f6acc-173">Porte</span><span class="sxs-lookup"><span data-stu-id="f6acc-173">Ports</span></span>
<span data-ttu-id="f6acc-174">Hello porte di input e outpue per un modulo personalizzato vengono specificate in elementi figlio di hello **porte** sezione del file di definizione XML di hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-174">hello input and output ports for a custom module are specified in child elements of hello **Ports** section of hello XML definition file.</span></span> <span data-ttu-id="f6acc-175">ordine di Hello di questi elementi determina hello layout esperti (UX) da parte degli utenti.</span><span class="sxs-lookup"><span data-stu-id="f6acc-175">hello order of these elements determines hello layout experienced (UX) by users.</span></span> <span data-ttu-id="f6acc-176">primo elemento figlio di Hello **input** o **output** elencati in hello **porte** elemento del file XML di hello diventa porta di input a sinistra hello in hello UX. di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f6acc-176">hello first child **input** or **output** listed in hello **Ports** element of hello XML file becomes hello left-most input port in hello Machine Learning UX.</span></span>
<span data-ttu-id="f6acc-177">Ogni input e output porta potrebbe essere facoltativa **descrizione** elemento figlio che specifica il testo di hello visualizzato quando si posiziona il cursore di mouse hello su porta hello in hello dell'interfaccia utente di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f6acc-177">Each input and output port may have an optional **Description** child element that specifies hello text shown when you hover hello mouse cursor over hello port in hello Machine Learning UI.</span></span>

<span data-ttu-id="f6acc-178">**Regole porte**:</span><span class="sxs-lookup"><span data-stu-id="f6acc-178">**Ports Rules**:</span></span>

* <span data-ttu-id="f6acc-179">Il numero massimo di **porte di input e di output** è 8 per ciascuno.</span><span class="sxs-lookup"><span data-stu-id="f6acc-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="f6acc-180">Elementi di input</span><span class="sxs-lookup"><span data-stu-id="f6acc-180">Input elements</span></span>
<span data-ttu-id="f6acc-181">Porte di input consentono di area di lavoro e la funzione di toopass dati tooyour R.</span><span class="sxs-lookup"><span data-stu-id="f6acc-181">Input ports allow you toopass data tooyour R function and workspace.</span></span> <span data-ttu-id="f6acc-182">Hello **tipi di dati** che sono supportati per le porte di input sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="f6acc-182">hello **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="f6acc-183">**DataTable:** questo tipo viene passato a funzione tooyour R come un data.frame.</span><span class="sxs-lookup"><span data-stu-id="f6acc-183">**DataTable:** This type is passed tooyour R function as a data.frame.</span></span> <span data-ttu-id="f6acc-184">In realtà, qualsiasi tipo (ad esempio, file CSV o i file ARFF) è supportati da Machine Learning e che è compatibili con **DataTable** sono data.frame tooa convertito automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f6acc-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted tooa data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="f6acc-185">Hello **id** associata a ogni attributo **DataTable** porta di input deve essere un valore univoco e questo valore deve corrispondere il parametro nella funzione di R denominato corrispondente.</span><span class="sxs-lookup"><span data-stu-id="f6acc-185">hello **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="f6acc-186">Parametro facoltativo **DataTable** le porte che non vengono passate come input in un esperimento avere valore hello **NULL** passato toohello R (funzione) e porte zip facoltativo vengono ignorate se hello input non è connesso.</span><span class="sxs-lookup"><span data-stu-id="f6acc-186">Optional **DataTable** ports that are not passed as input in an experiment have hello value **NULL** passed toohello R function and optional zip ports are ignored if hello input is not connected.</span></span> <span data-ttu-id="f6acc-187">Hello **isOptional** attributo è facoltativo per entrambi hello **DataTable** e **Zip** tipi e viene *false* per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f6acc-187">hello **isOptional** attribute is optional for both hello **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="f6acc-188">**Zip:** i moduli personalizzati possono accettare un file ZIP come input.</span><span class="sxs-lookup"><span data-stu-id="f6acc-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="f6acc-189">Questo input è decompresso nella directory di lavoro hello R della funzione</span><span class="sxs-lookup"><span data-stu-id="f6acc-189">This input is unpacked into hello R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

<span data-ttu-id="f6acc-190">Per i moduli R personalizzati, id hello per una porta di Zip è toomatch eventuali parametri della funzione hello R.</span><span class="sxs-lookup"><span data-stu-id="f6acc-190">For custom R modules, hello id for a Zip port does not have toomatch any parameters of hello R function.</span></span> <span data-ttu-id="f6acc-191">Infatti, file zip hello viene automaticamente estratto toohello R directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f6acc-191">This is because hello zip file is automatically extracted toohello R working directory.</span></span>

<span data-ttu-id="f6acc-192">**Regole di input:**</span><span class="sxs-lookup"><span data-stu-id="f6acc-192">**Input Rules:**</span></span>

* <span data-ttu-id="f6acc-193">valore di hello Hello **id** attributo di hello **Input** elemento deve essere un nome di variabile valido di R.</span><span class="sxs-lookup"><span data-stu-id="f6acc-193">hello value of hello **id** attribute of hello **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="f6acc-194">valore di hello Hello **id** attributo di hello **Input** elemento non deve essere più lungo di 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f6acc-194">hello value of hello **id** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="f6acc-195">valore di hello Hello **nome** attributo di hello **Input** elemento non deve essere più lungo di 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f6acc-195">hello value of hello **name** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="f6acc-196">contenuto di hello Hello **descrizione** elemento non deve essere più lungo di 128 caratteri</span><span class="sxs-lookup"><span data-stu-id="f6acc-196">hello content of hello **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="f6acc-197">valore di hello Hello **tipo** attributo di hello **Input** l'elemento deve essere *Zip* o *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="f6acc-197">hello value of hello **type** attribute of hello **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="f6acc-198">valore hello Hello **isOptional** attributo di hello **Input** elemento non è necessario (e *false* per impostazione predefinita, quando non è specificato); ma se viene specificato, deve essere *true* o *false*.</span><span class="sxs-lookup"><span data-stu-id="f6acc-198">hello value of hello **isOptional** attribute of hello **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="f6acc-199">Elementi di output</span><span class="sxs-lookup"><span data-stu-id="f6acc-199">Output elements</span></span>
<span data-ttu-id="f6acc-200">**Porte di output standard:** le porte di Output vengono mappate toohello i valori restituiti dalla funzione R, che può quindi essere usato dai moduli successivi.</span><span class="sxs-lookup"><span data-stu-id="f6acc-200">**Standard output ports:** Output ports are mapped toohello return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="f6acc-201">*DataTable* è tipo di porta di output standard solo hello attualmente supportato.</span><span class="sxs-lookup"><span data-stu-id="f6acc-201">*DataTable* is hello only standard output port type supported currently.</span></span> <span data-ttu-id="f6acc-202">Il supporto per *Learners* e *Transforms* è di prossima introduzione. Un output *DataTable* è definito come:</span><span class="sxs-lookup"><span data-stu-id="f6acc-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="f6acc-203">Per gli output in moduli R personalizzati, hello valore hello **id** attributo non è in uno script R hello toocorrespond con elementi, ma deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="f6acc-203">For outputs in custom R modules, hello value of hello **id** attribute does not have toocorrespond with anything in hello R script, but it must be unique.</span></span> <span data-ttu-id="f6acc-204">Per un output di un modulo singolo, valore restituito di hello dalla funzione hello R deve essere un *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="f6acc-204">For a single module output, hello return value from hello R function must be a *data.frame*.</span></span> <span data-ttu-id="f6acc-205">In ordine toooutput più di un oggetto di un tipo di dati supportati, porte di output appropriato hello necessario toobe specificato nel file di definizione XML hello e oggetti hello necessitano toobe restituito come un elenco.</span><span class="sxs-lookup"><span data-stu-id="f6acc-205">In order toooutput more than one object of a supported data type, hello appropriate output ports need toobe specified in hello XML definition file and hello objects need toobe returned as a list.</span></span> <span data-ttu-id="f6acc-206">gli oggetti di output di Hello vengono assegnati porte toooutput da tooright a sinistra, indicare l'ordine di hello in cui gli oggetti di hello vengono inseriti nell'elenco restituito hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-206">hello output objects are assigned toooutput ports from left tooright, reflecting hello order in which hello objects are placed in hello returned list.</span></span>

<span data-ttu-id="f6acc-207">Ad esempio, se si desidera hello toomodify **personalizzato Add Rows** toooutput modulo hello originale due set di dati, *dataset1* e *dataset2*, inoltre aggiunti a un nuovo toohello set di dati, *dataset*, (in ordine da sinistra tooright, come: *dataset*, *dataset1*, *dataset2*), quindi definire hello l'output nel file CustomAddRows.xml hello porte come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f6acc-207">For example, if you want toomodify hello **Custom Add Rows** module toooutput hello original two datasets, *dataset1* and *dataset2*, in addition toohello new joined dataset, *dataset*, (in an order, from left tooright, as: *dataset*, *dataset1*, *dataset2*), then define hello output ports in hello CustomAddRows.xml file as follows:</span></span>

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


<span data-ttu-id="f6acc-208">E restituire l'elenco di hello degli oggetti in un elenco nella sequenza corretta hello 'CustomAddRows.R':</span><span class="sxs-lookup"><span data-stu-id="f6acc-208">And return hello list of objects in a list in hello correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="f6acc-209">**Output di visualizzazione:** è inoltre possibile specificare una porta di output di tipo *visualizzazione*, visualizzare l'output di hello dall'output di console e dispositivo di grafica hello R.</span><span class="sxs-lookup"><span data-stu-id="f6acc-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays hello output from hello R graphics device and console output.</span></span> <span data-ttu-id="f6acc-210">Questa porta non fa parte dell'output di hello R funzione e non interferire con l'ordine di hello di hello altri tipi di porta di output.</span><span class="sxs-lookup"><span data-stu-id="f6acc-210">This port is not part of hello R function output and does not interfere with hello order of hello other output port types.</span></span> <span data-ttu-id="f6acc-211">aggiungere una visualizzazione porta toohello personalizzato i moduli, tooadd un **Output** elemento con un valore di *visualizzazione* per relativo **tipo** attributo:</span><span class="sxs-lookup"><span data-stu-id="f6acc-211">tooadd a visualization port toohello custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

<span data-ttu-id="f6acc-212">**Regole di output:**</span><span class="sxs-lookup"><span data-stu-id="f6acc-212">**Output Rules:**</span></span>

* <span data-ttu-id="f6acc-213">valore di hello Hello **id** attributo di hello **Output** elemento deve essere un nome di variabile valido di R.</span><span class="sxs-lookup"><span data-stu-id="f6acc-213">hello value of hello **id** attribute of hello **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="f6acc-214">valore di hello Hello **id** attributo di hello **Output** elemento non deve essere più di 32 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f6acc-214">hello value of hello **id** attribute of hello **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="f6acc-215">valore di hello Hello **nome** attributo di hello **Output** elemento non deve essere più lungo di 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f6acc-215">hello value of hello **name** attribute of hello **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="f6acc-216">valore di hello Hello **tipo** attributo di hello **Output** l'elemento deve essere *visualizzazione*.</span><span class="sxs-lookup"><span data-stu-id="f6acc-216">hello value of hello **type** attribute of hello **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="f6acc-217">Argomenti</span><span class="sxs-lookup"><span data-stu-id="f6acc-217">Arguments</span></span>
<span data-ttu-id="f6acc-218">Dati aggiuntivi possono essere passati toohello R funzione tramite i parametri di modulo che sono definiti in hello **argomenti** elemento.</span><span class="sxs-lookup"><span data-stu-id="f6acc-218">Additional data can be passed toohello R function via module parameters which are defined in hello **Arguments** element.</span></span> <span data-ttu-id="f6acc-219">Questi parametri vengono visualizzati nel riquadro delle proprietà all'estrema destra hello di hello dell'interfaccia utente di Machine Learning quando è selezionata modulo hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-219">These parameters appear in hello rightmost properties pane of hello Machine Learning UI when hello module is selected.</span></span> <span data-ttu-id="f6acc-220">Gli argomenti possono essere uno qualsiasi dei tipi di hello supportata o è possibile creare un enumeratore personalizzato quando necessario.</span><span class="sxs-lookup"><span data-stu-id="f6acc-220">Arguments can be any of hello supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="f6acc-221">Toohello simile **porte** elementi **argomenti** gli elementi possono avere un parametro facoltativo **descrizione** elemento che specifica il testo hello visualizzato quando si passa il mouse hello nel nome del parametro hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-221">Similar toohello **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies hello text that appears when you hover hello mouse over hello parameter name.</span></span>
<span data-ttu-id="f6acc-222">È possibile aggiungere proprietà facoltativa di un modulo, ad esempio defaultValue minValue e maxValue argomento tooany come attributi tooa **proprietà** elemento.</span><span class="sxs-lookup"><span data-stu-id="f6acc-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added tooany argument as attributes tooa **Properties** element.</span></span> <span data-ttu-id="f6acc-223">Proprietà valide per hello **proprietà** elemento dipendono dal tipo di argomento hello e sono descritti con tipi di argomento hello è supportato nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-223">Valid properties for hello **Properties** element depend on hello argument type and are described with hello supported argument types in hello next section.</span></span> <span data-ttu-id="f6acc-224">Gli argomenti con hello **isOptional** impostata troppo**"true"** non richiedono hello utente tooenter un valore.</span><span class="sxs-lookup"><span data-stu-id="f6acc-224">Arguments with hello **isOptional** property set too**"true"** do not require hello user tooenter a value.</span></span> <span data-ttu-id="f6acc-225">Se l'argomento toohello non viene fornito un valore, quindi hello argomento non viene passato toohello funzione di punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="f6acc-225">If a value is not provided toohello argument, then hello argument is not passed toohello entry point function.</span></span> <span data-ttu-id="f6acc-226">Gli argomenti della funzione di punto di ingresso hello toobe necessità facoltativo gestite in modo esplicito dalla funzione hello, ad esempio assegnato un valore predefinito null nella definizione di funzione di punto di ingresso hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-226">Arguments of hello entry point function that are optional need toobe explicitly handled by hello function, e.g. assigned a default value of NULL in hello entry point function definition.</span></span> <span data-ttu-id="f6acc-227">Un argomento facoltativo imporrà solo hello altri vincoli di argomento, ad esempio min o max, se viene fornito un valore dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-227">An optional argument will only enforce hello other argument constraints, i.e. min or max, if a value is provided by hello user.</span></span>
<span data-ttu-id="f6acc-228">Come con input e output, è fondamentale che ciascun parametro hello sono associati valori di id univoco.</span><span class="sxs-lookup"><span data-stu-id="f6acc-228">As with inputs and outputs, it is critical that each of hello parameters have unique id values associated with them.</span></span> <span data-ttu-id="f6acc-229">Nel nostro avvio rapido esempio hello associata/parametro id è stato *scambio*.</span><span class="sxs-lookup"><span data-stu-id="f6acc-229">In our quick start example hello associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="f6acc-230">Elemento Arg</span><span class="sxs-lookup"><span data-stu-id="f6acc-230">Arg element</span></span>
<span data-ttu-id="f6acc-231">Un parametro di modulo viene definito utilizzando hello **Arg** elemento figlio di hello **argomenti** sezione del file di definizione XML di hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-231">A module parameter is defined using hello **Arg** child element of hello **Arguments** section of hello XML definition file.</span></span> <span data-ttu-id="f6acc-232">Come con gli elementi figlio di hello in hello **porte** sezione, hello l'ordine dei parametri in hello **argomenti** sezione definisce il layout di hello rilevato in hello UX.</span><span class="sxs-lookup"><span data-stu-id="f6acc-232">As with hello child elements in hello **Ports** section, hello ordering of parameters in hello **Arguments** section defines hello layout encountered in hello UX.</span></span> <span data-ttu-id="f6acc-233">Hello parametri vengono visualizzati dall'alto verso il basso in hello dell'interfaccia utente in hello stesso ordine in cui sono definite nel file XML di hello.</span><span class="sxs-lookup"><span data-stu-id="f6acc-233">hello parameters appear from top down in hello UI in hello same order in which they are defined in hello XML file.</span></span> <span data-ttu-id="f6acc-234">tipi di Hello supportati da Machine Learning per i parametri sono elencati di seguito.</span><span class="sxs-lookup"><span data-stu-id="f6acc-234">hello types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="f6acc-235">**int** : parametro di tipo Integer (32 bit).</span><span class="sxs-lookup"><span data-stu-id="f6acc-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="f6acc-236">*Proprietà facoltative*: **min**, **max**, **default** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="f6acc-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="f6acc-237">**double** : parametro di tipo doppio.</span><span class="sxs-lookup"><span data-stu-id="f6acc-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="f6acc-238">*Proprietà facoltative*: **min**, **max**, **default** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="f6acc-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="f6acc-239">**bool** : parametro booleano rappresentato da una casella di controllo nell'esperienza utente.</span><span class="sxs-lookup"><span data-stu-id="f6acc-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="f6acc-240">*Proprietà facoltative*: **default** (false se non impostato)</span><span class="sxs-lookup"><span data-stu-id="f6acc-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="f6acc-241">**string**: stringa standard</span><span class="sxs-lookup"><span data-stu-id="f6acc-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="f6acc-242">*Proprietà facoltative*: **default** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="f6acc-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="f6acc-243">**ColumnPicker**: parametro di selezione della colonna.</span><span class="sxs-lookup"><span data-stu-id="f6acc-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="f6acc-244">Questo tipo come un selettore di colonna in hello UX.</span><span class="sxs-lookup"><span data-stu-id="f6acc-244">This type renders in hello UX as a column chooser.</span></span> <span data-ttu-id="f6acc-245">Hello **proprietà** elemento è utilizzato toospecify qui hello id della porta hello da cui vengono selezionate le colonne, in cui deve essere il tipo di porta di hello destinazione *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="f6acc-245">hello **Property** element is used here toospecify hello id of hello port from which columns are selected, where hello target port type must be *DataTable*.</span></span> <span data-ttu-id="f6acc-246">il risultato di Hello di selezione della colonna hello viene passato toohello R funzione come un elenco di stringhe contenente i nomi di colonna hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="f6acc-246">hello result of hello column selection is passed toohello R function as a list of strings containing hello selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="f6acc-247">*Proprietà obbligatorie*: **portId** -corrispondenze hello id di un elemento di Input con tipo *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="f6acc-247">*Required Properties*: **portId** - matches hello id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="f6acc-248">*Proprietà facoltative*:</span><span class="sxs-lookup"><span data-stu-id="f6acc-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="f6acc-249">**allowedTypes** -da cui è possibile selezionare i tipi di colonna hello filtri.</span><span class="sxs-lookup"><span data-stu-id="f6acc-249">**allowedTypes** - Filters hello column types from which you can pick.</span></span> <span data-ttu-id="f6acc-250">I valori validi includono:</span><span class="sxs-lookup"><span data-stu-id="f6acc-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="f6acc-251">Numeric</span><span class="sxs-lookup"><span data-stu-id="f6acc-251">Numeric</span></span>
    * <span data-ttu-id="f6acc-252">Boolean</span><span class="sxs-lookup"><span data-stu-id="f6acc-252">Boolean</span></span>
    * <span data-ttu-id="f6acc-253">Categorical</span><span class="sxs-lookup"><span data-stu-id="f6acc-253">Categorical</span></span>
    * <span data-ttu-id="f6acc-254">string</span><span class="sxs-lookup"><span data-stu-id="f6acc-254">String</span></span>
    * <span data-ttu-id="f6acc-255">Etichetta</span><span class="sxs-lookup"><span data-stu-id="f6acc-255">Label</span></span>
    * <span data-ttu-id="f6acc-256">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="f6acc-256">Feature</span></span>
    * <span data-ttu-id="f6acc-257">Score</span><span class="sxs-lookup"><span data-stu-id="f6acc-257">Score</span></span>
    * <span data-ttu-id="f6acc-258">Tutti</span><span class="sxs-lookup"><span data-stu-id="f6acc-258">All</span></span>
  * <span data-ttu-id="f6acc-259">**predefinito** -selezioni predefinito valido per il selettore di colonna hello includono:</span><span class="sxs-lookup"><span data-stu-id="f6acc-259">**default** - Valid default selections for hello column picker include:</span></span> 
    
    * <span data-ttu-id="f6acc-260">Nessuno</span><span class="sxs-lookup"><span data-stu-id="f6acc-260">None</span></span>
    * <span data-ttu-id="f6acc-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="f6acc-261">NumericFeature</span></span>
    * <span data-ttu-id="f6acc-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="f6acc-262">NumericLabel</span></span>
    * <span data-ttu-id="f6acc-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="f6acc-263">NumericScore</span></span>
    * <span data-ttu-id="f6acc-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="f6acc-264">NumericAll</span></span>
    * <span data-ttu-id="f6acc-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="f6acc-265">BooleanFeature</span></span>
    * <span data-ttu-id="f6acc-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="f6acc-266">BooleanLabel</span></span>
    * <span data-ttu-id="f6acc-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="f6acc-267">BooleanScore</span></span>
    * <span data-ttu-id="f6acc-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="f6acc-268">BooleanAll</span></span>
    * <span data-ttu-id="f6acc-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="f6acc-269">CategoricalFeature</span></span>
    * <span data-ttu-id="f6acc-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="f6acc-270">CategoricalLabel</span></span>
    * <span data-ttu-id="f6acc-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="f6acc-271">CategoricalScore</span></span>
    * <span data-ttu-id="f6acc-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="f6acc-272">CategoricalAll</span></span>
    * <span data-ttu-id="f6acc-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="f6acc-273">StringFeature</span></span>
    * <span data-ttu-id="f6acc-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="f6acc-274">StringLabel</span></span>
    * <span data-ttu-id="f6acc-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="f6acc-275">StringScore</span></span>
    * <span data-ttu-id="f6acc-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="f6acc-276">StringAll</span></span>
    * <span data-ttu-id="f6acc-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="f6acc-277">AllLabel</span></span>
    * <span data-ttu-id="f6acc-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="f6acc-278">AllFeature</span></span>
    * <span data-ttu-id="f6acc-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="f6acc-279">AllScore</span></span>
    * <span data-ttu-id="f6acc-280">Tutti</span><span class="sxs-lookup"><span data-stu-id="f6acc-280">All</span></span>

<span data-ttu-id="f6acc-281">**DropDown**: elenco enumerato specificato dall'utente (elenco a discesa).</span><span class="sxs-lookup"><span data-stu-id="f6acc-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="f6acc-282">gli elementi di elenco a discesa Hello vengono specificati all'interno di hello **proprietà** elemento utilizzando un **elemento** elemento.</span><span class="sxs-lookup"><span data-stu-id="f6acc-282">hello dropdown items are specified within hello **Properties** element using an **Item** element.</span></span> <span data-ttu-id="f6acc-283">Hello **id** per ogni **elemento** deve essere univoco e una variabile di R valida.</span><span class="sxs-lookup"><span data-stu-id="f6acc-283">hello **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="f6acc-284">valore di hello Hello **nome** di un **elemento** agisce come testo hello e valore hello che viene passato a funzione toohello R.</span><span class="sxs-lookup"><span data-stu-id="f6acc-284">hello value of hello **name** of an **Item** serves as both hello text that you see and hello value that is passed toohello R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="f6acc-285">*Proprietà facoltative*:</span><span class="sxs-lookup"><span data-stu-id="f6acc-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="f6acc-286">**predefinito** : hello valore per proprietà predefinita hello deve corrispondere a un valore di id da una delle hello **elemento** elementi.</span><span class="sxs-lookup"><span data-stu-id="f6acc-286">**default** - hello value for hello default property must correspond with an id value from one of hello **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="f6acc-287">File ausiliari</span><span class="sxs-lookup"><span data-stu-id="f6acc-287">Auxiliary Files</span></span>
<span data-ttu-id="f6acc-288">Qualsiasi file inserito nel file ZIP modulo personalizzato è toobe corso disponibile per l'utilizzo durante la fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f6acc-288">Any file that is placed in your custom module ZIP file is going toobe available for use during execution time.</span></span> <span data-ttu-id="f6acc-289">Vengono mantenute le strutture di directory presenti.</span><span class="sxs-lookup"><span data-stu-id="f6acc-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="f6acc-290">Ciò significa che funziona acquisti file hello stesso in locale e in esecuzione in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f6acc-290">This means that file sourcing works hello same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="f6acc-291">Si noti che tutti i file sono estratti too'src' directory in modo da tutti i percorsi devono avere ' src /' prefisso.</span><span class="sxs-lookup"><span data-stu-id="f6acc-291">Notice that all files are extracted too‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="f6acc-292">Si supponga, ad esempio, si desidera tooremove tutte le righe con NAs del set di dati hello e rimuovere anche tutte le righe duplicate, prima l'output in CustomAddRows e già creato una funzione di R che vengono eseguite in un file RemoveDupNARows.R:</span><span class="sxs-lookup"><span data-stu-id="f6acc-292">For example, say you want tooremove any rows with NAs from hello dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="f6acc-293">Si può ottenere file ausiliario hello RemoveDupNARows.R nella funzione CustomAddRows hello:</span><span class="sxs-lookup"><span data-stu-id="f6acc-293">You can source hello auxiliary file RemoveDupNARows.R in hello CustomAddRows function:</span></span>

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

<span data-ttu-id="f6acc-294">Quindi, caricare il file ZIP contenente 'CustomAddRows.R', 'CustomAddRows.xml' e 'RemoveDupNARows.R' come modulo R personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f6acc-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="f6acc-295">Ambiente di esecuzione</span><span class="sxs-lookup"><span data-stu-id="f6acc-295">Execution Environment</span></span>
<span data-ttu-id="f6acc-296">ambiente di esecuzione Hello per lo script R hello utilizza hello stessa versione di R hello **Execute R Script** modulo e può utilizzare hello stesso predefinito pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f6acc-296">hello execution environment for hello R script uses hello same version of R as hello **Execute R Script** module and can use hello same default packages.</span></span> <span data-ttu-id="f6acc-297">Inoltre, è possibile aggiungere ulteriori R pacchetti tooyour modulo personalizzato includendoli nel pacchetto zip di hello modulo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f6acc-297">You can also add additional R packages tooyour custom module by including them in hello custom module zip package.</span></span> <span data-ttu-id="f6acc-298">È sufficiente caricare i pacchetti nello script R come si farebbe nel proprio ambiente R.</span><span class="sxs-lookup"><span data-stu-id="f6acc-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="f6acc-299">**Limitazioni dell'ambiente di esecuzione hello** includono:</span><span class="sxs-lookup"><span data-stu-id="f6acc-299">**Limitations of hello execution environment** include:</span></span>

* <span data-ttu-id="f6acc-300">Sistema di file non-persistent: i file scritti quando viene eseguito il modulo personalizzato di hello non sono persistenti tra più esecuzioni di hello stesso modulo.</span><span class="sxs-lookup"><span data-stu-id="f6acc-300">Non-persistent file system: Files written when hello custom module is run are not persisted across multiple runs of hello same module.</span></span>
* <span data-ttu-id="f6acc-301">Nessun accesso alla rete</span><span class="sxs-lookup"><span data-stu-id="f6acc-301">No network access</span></span>

