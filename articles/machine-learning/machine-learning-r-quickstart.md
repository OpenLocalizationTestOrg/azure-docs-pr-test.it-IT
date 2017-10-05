---
title: Esercitazione con guida rapida per il linguaggio R per Azure Machine Learning | Documentazione Microsoft
description: Usare questa esercitazione sulla programmazione R per iniziare a usare rapidamente il linguaggio R con Azure Machine Learning Studio per creare una soluzione di previsione.
keywords: guida introduttiva, linguaggio r, linguaggio di programmazione r, esercitazione di programmazione r
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 598f5ce445e520b6cdc347c80f7f3dcbc9c2c9e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="quickstart-tutorial-for-the-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="998b3-104">Esercitazione con guida rapida per il linguaggio di programmazione R per Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="998b3-104">Quickstart tutorial for the R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="998b3-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="998b3-105">Introduction</span></span>
<span data-ttu-id="998b3-106">Questa esercitazione con guida rapida consente di iniziare rapidamente a estendere Azure Machine Learning usando il linguaggio di programmazione R.</span><span class="sxs-lookup"><span data-stu-id="998b3-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using the R programming language.</span></span> <span data-ttu-id="998b3-107">Seguire questa esercitazione sulla programmazione R per creare, testare ed eseguire il codice R in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="998b3-107">Follow this R programming tutorial to create, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="998b3-108">Usando questa esercitazione, sarà possibile creare una soluzione completa di previsione con il linguaggio R in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="998b3-108">As you work through tutorial, you will create a complete forecasting solution by using the R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="998b3-109">Microsoft Azure Machine Learning contiene molti moduli validi per Machine Learning e per la manipolazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="998b3-110">Il potente linguaggio R è stato definito come la lingua franca dell'analisi.</span><span class="sxs-lookup"><span data-stu-id="998b3-110">The powerful R language has been described as the lingua franca of analytics.</span></span> <span data-ttu-id="998b3-111">Per fortuna, le analisi e la manipolazione dei dati Azure Machine Learning possono essere estese usando R. Questa combinazione fornisce la scalabilità e la facilità di distribuzione di Azure Machine Learning con la flessibilità e l'analisi approfondita di R.</span><span class="sxs-lookup"><span data-stu-id="998b3-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides the scalability and ease of deployment of Azure Machine Learning with the flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-the-dataset"></a><span data-ttu-id="998b3-112">Previsione e set di dati</span><span class="sxs-lookup"><span data-stu-id="998b3-112">Forecasting and the dataset</span></span>
<span data-ttu-id="998b3-113">La previsione è un metodo analitico molto utile e ampiamente distribuito.</span><span class="sxs-lookup"><span data-stu-id="998b3-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="998b3-114">Viene comunemente usata per vari scopi, dalla previsione di vendita di articoli stagionali alla definizione dei livelli di scorte ottimali, fino alla previsione di variabili macroeconomiche.</span><span class="sxs-lookup"><span data-stu-id="998b3-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, to predicting macroeconomic variables.</span></span> <span data-ttu-id="998b3-115">In genere, inoltre, viene eseguita con modelli in serie temporale.</span><span class="sxs-lookup"><span data-stu-id="998b3-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="998b3-116">I dati delle serie temporali sono dati i cui valori contengono un indice temporale, che</span><span class="sxs-lookup"><span data-stu-id="998b3-116">Time series data is data in which the values have a time index.</span></span> <span data-ttu-id="998b3-117">può essere regolare, ad esempio ogni minuto od ogni mese, o irregolare.</span><span class="sxs-lookup"><span data-stu-id="998b3-117">The time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="998b3-118">Sui dati in serie temporale si basano i modelli in serie temporale.</span><span class="sxs-lookup"><span data-stu-id="998b3-118">A time series model is based on time series data.</span></span> <span data-ttu-id="998b3-119">Il linguaggio di programmazione R contiene un'architettura flessibile ed estese funzioni di analisi per i dati in serie temporale.</span><span class="sxs-lookup"><span data-stu-id="998b3-119">The R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="998b3-120">In questa esercitazione prenderemo in esame la produzione casearia in California, con i relativi dati sui prezzi.</span><span class="sxs-lookup"><span data-stu-id="998b3-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="998b3-121">Questi dati includono informazioni mensili sulla produzione di diversi prodotti caseari e il prezzo del latte intero, un materia prima di riferimento.</span><span class="sxs-lookup"><span data-stu-id="998b3-121">This data includes monthly information on the production of several dairy products and the price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="998b3-122">I dati usati nell'articolo, insieme agli script R, possono essere [scaricati qui][download].</span><span class="sxs-lookup"><span data-stu-id="998b3-122">The data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="998b3-123">Questi dati sono stati originariamente sintetizzati da informazioni pubblicate dalla University of Wisconsin all'indirizzo http://future.aae.wisc.edu/tab/production.html.</span><span class="sxs-lookup"><span data-stu-id="998b3-123">This data was originally synthesized from information available from the University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="998b3-124">Organizzazione</span><span class="sxs-lookup"><span data-stu-id="998b3-124">Organization</span></span>
<span data-ttu-id="998b3-125">La procedura sarà formata da diversi passaggi che consentiranno di apprendere come creare, testare ed eseguire il codice R per le analisi e la manipolazione dei dati nell'ambiente di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="998b3-125">We will progress through several steps as you learn how to create, test and execute analytics and data manipulation R code in the Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="998b3-126">Prima di tutto, verranno illustrate le nozioni di base dell'uso del linguaggio R nell'ambiente di Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="998b3-126">First we will explore the basics of using the R language in the Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="998b3-127">Quindi, verranno discussi diversi aspetti relativi all'I/O dei dati, del codice R e dei grafici nell'ambiente di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="998b3-127">Then we progress to discussing various aspects of I/O for data, R code and graphics in the Azure Machine Learning environment.</span></span>
* <span data-ttu-id="998b3-128">In seguito, verrà creata la prima parte della soluzione di previsione tramite la compilazione di codice per la pulizia e la trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-128">We will then construct the first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="998b3-129">Con i dati preparati verrà eseguita un'analisi delle correlazioni tra più variabili nel set di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-129">With our data prepared we will perform an analysis of the correlations between several of the variables in our dataset.</span></span>
* <span data-ttu-id="998b3-130">Infine, verrà creato un modello di previsione in serie temporale (stagionale) per la produzione di latte.</span><span class="sxs-lookup"><span data-stu-id="998b3-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="998b3-131"><a id="mlstudio"></a>Interagire con il linguaggio R in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="998b3-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="998b3-132">Questa sezione illustra alcune nozioni di base relative all'interazione con il linguaggio di programmazione R nell'ambiente di Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="998b3-132">This section takes you through some basics of interacting with the R programming language in the Machine Learning Studio environment.</span></span> <span data-ttu-id="998b3-133">Il linguaggio R fornisce uno strumento potente per creare moduli personalizzati di analisi e manipolazione di dati nell'ambiente di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="998b3-133">The R language provides a powerful tool to create customized analytics and data manipulation modules within the Azure Machine Learning environment.</span></span>

<span data-ttu-id="998b3-134">In questa guida useremo RStudio per sviluppare, testare ed eseguire il debug di codice R su piccola scala.</span><span class="sxs-lookup"><span data-stu-id="998b3-134">I will use RStudio to develop, test and debug R code on a small scale.</span></span> <span data-ttu-id="998b3-135">Questo codice viene quindi tagliato e incollato in un modulo [Execute R Script][execute-r-script] (Esegui script R) in Machine Learning Studio, pronto per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="998b3-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready to run.</span></span>  

### <a name="the-execute-r-script-module"></a><span data-ttu-id="998b3-136">Modulo Execute R Script</span><span class="sxs-lookup"><span data-stu-id="998b3-136">The Execute R Script module</span></span>
<span data-ttu-id="998b3-137">In Machine Learning Studio gli script R vengono eseguiti nel modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-137">Within Machine Learning Studio, R scripts are run within the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="998b3-138">Un esempio del modulo [Execute R Script][execute-r-script] in Machine Learning Studio è mostrato nella figura 1.</span><span class="sxs-lookup"><span data-stu-id="998b3-138">An example of the [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![Linguaggio di programmazione R: il modulo Execute R Script selezionato in Machine Learning Studio][1]

<span data-ttu-id="998b3-140">*Figura 1. Ambiente di Machine Learning Studio che mostra il modulo Execute R Script selezionato.*</span><span class="sxs-lookup"><span data-stu-id="998b3-140">*Figure 1. The Machine Learning Studio environment showing the Execute R Script module selected.*</span></span>

<span data-ttu-id="998b3-141">Nella figura 1 è possibile osservare alcuni dei componenti principali dell'ambiente di Machine Learning Studio per l'uso con il modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-141">Referring to Figure 1, let's look at some of the key parts of the Machine Learning Studio environment for working with the [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="998b3-142">I moduli dell'esperimento vengono visualizzati nel riquadro centrale.</span><span class="sxs-lookup"><span data-stu-id="998b3-142">The modules in the experiment are shown in the center pane.</span></span>
* <span data-ttu-id="998b3-143">La finestra presente nella parte superiore del riquadro di destra consente di visualizzare e modificare gli script R,</span><span class="sxs-lookup"><span data-stu-id="998b3-143">The upper part of the right pane contains a window to view and edit your R scripts.</span></span>  
* <span data-ttu-id="998b3-144">La parte inferiore del riquadro di destra mostra alcune proprietà di [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-144">The lower part of right pane shows some properties of the [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="998b3-145">È possibile visualizzare e i log degli errori e di output facendo clic sulle rispettive opzioni di questo riquadro.</span><span class="sxs-lookup"><span data-stu-id="998b3-145">You can view the error and output logs by clicking on the appropriate spots of this pane.</span></span>

<span data-ttu-id="998b3-146">Il modulo [Execute R Script][execute-r-script] verrà descritto dettagliatamente nelle parti successive di questo documento.</span><span class="sxs-lookup"><span data-stu-id="998b3-146">We will, of course, be discussing the [Execute R Script][execute-r-script] in greater detail in the rest of this document.</span></span>

<span data-ttu-id="998b3-147">Quando si usano funzioni R complesse, è preferibile effettuare le operazioni di modifica, test e debug in RStudio.</span><span class="sxs-lookup"><span data-stu-id="998b3-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="998b3-148">Come con qualsiasi altro software di sviluppo, inoltre, è opportuno estendere il codice in modo incrementale, così da poterlo verificare in piccoli e semplici casi di test.</span><span class="sxs-lookup"><span data-stu-id="998b3-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="998b3-149">Quindi tagliare e incollare le funzioni nella finestra dello script R del modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-149">Then cut and paste your functions into the R script window of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="998b3-150">Questo approccio consente di sfruttare sia l'ambiente di sviluppo integrato (IDE) di RStudio che la potenza di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="998b3-150">This approach allows you to harness both the RStudio integrated development environment (IDE) and the power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="998b3-151">Eseguire il codice R</span><span class="sxs-lookup"><span data-stu-id="998b3-151">Execute R code</span></span>
<span data-ttu-id="998b3-152">Qualsiasi codice R nel modulo [Execute R Script][execute-r-script] verrà eseguito quando si esegue l'esperimento facendo clic sul pulsante **Run** (Esegui).</span><span class="sxs-lookup"><span data-stu-id="998b3-152">Any R code in the [Execute R Script][execute-r-script] module will execute when you run the experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="998b3-153">Al termine dell'esecuzione, accanto all'icona [Execute R Script][execute-r-script] verrà visualizzato un segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="998b3-153">When execution has completed, a check mark will appear on the [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="998b3-154">Codice R difensivo per Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="998b3-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="998b3-155">Se si sviluppa un codice R per, ad esempio, un servizio Web usando Azure Machine Learning, è necessario pianificare in che modo il codice R gestirà gli input di dati imprevisti e le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="998b3-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="998b3-156">Per maggiore chiarezza, per gli esempi di codice riportati in questa guida non tratterò in modo approfondito le modalità di verifica e gestione delle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="998b3-156">To maintain clarity, I have not included much in the way of checking or exception handling in most of the code examples shown.</span></span> <span data-ttu-id="998b3-157">Tuttavia, verranno forniti diversi esempi di funzioni che prevedono l'uso della capacità di gestione delle eccezioni di R.</span><span class="sxs-lookup"><span data-stu-id="998b3-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="998b3-158">Per informazioni più complete sulla gestione delle eccezioni di R, si consiglia di leggere le sezioni rilevanti del libro di Wickham elencate in [Appendice B - Letture di approfondimento](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="998b3-158">If you need a more complete treatment of R exception handling, I recommend you read the applicable sections of the book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="998b3-159">Eseguire il debug e testare R in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="998b3-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="998b3-160">Come già anticipato, in genere è consigliabile eseguire il test e il debug del codice R creato su scala ridotta in RStudio.</span><span class="sxs-lookup"><span data-stu-id="998b3-160">To reiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="998b3-161">Tuttavia, in alcuni casi è necessario tenere traccia dei problemi relativi al codice R nel modulo [Execute R Script][execute-r-script] stesso.</span><span class="sxs-lookup"><span data-stu-id="998b3-161">However, there are cases where you will need to track down R code problems in the [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="998b3-162">Inoltre, si consiglia di controllare i risultati in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="998b3-162">In addition, it is good practice to check your results in Machine Learning Studio.</span></span>

<span data-ttu-id="998b3-163">L'output dell'esecuzione del codice R e della piattaforma di Azure Machine Learning è disponibile principalmente in output.log,</span><span class="sxs-lookup"><span data-stu-id="998b3-163">Output from the execution of your R code and on the Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="998b3-164">ma alcune informazioni aggiuntive possono essere presenti in error.log.</span><span class="sxs-lookup"><span data-stu-id="998b3-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="998b3-165">Se si verifica un errore in Machine Learning Studio mentre si esegue il codice R, è necessario innanzitutto analizzare error.log.</span><span class="sxs-lookup"><span data-stu-id="998b3-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be to look at error.log.</span></span> <span data-ttu-id="998b3-166">Questo file può contenere messaggi di errore utili a comprendere e correggere l'errore.</span><span class="sxs-lookup"><span data-stu-id="998b3-166">This file can contain useful error messages to help you understand and correct your error.</span></span> <span data-ttu-id="998b3-167">Per visualizzare il file error.log, fare clic su **View error log** (Visualizza log degli errori) nel **riquadro delle proprietà** per il modulo [Execute R Script][execute-r-script] che contiene l'errore.</span><span class="sxs-lookup"><span data-stu-id="998b3-167">To view error.log, click on **View error log** on the **properties pane** for the [Execute R Script][execute-r-script] containing the error.</span></span>

<span data-ttu-id="998b3-168">In questo esempio è stato eseguito il codice R seguente con una variabile y non definita in un modulo [Execute R Script][execute-r-script]:</span><span class="sxs-lookup"><span data-stu-id="998b3-168">For example, I ran the following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="998b3-169">L'esecuzione del codice non riesce, generando così una condizione di errore.</span><span class="sxs-lookup"><span data-stu-id="998b3-169">This code fails to execute, resulting in an error condition.</span></span> <span data-ttu-id="998b3-170">Facendo clic su **View error log** (Visualizza log degli errori) nel **riquadro delle proprietà**, viene visualizzato quanto mostrato nella figura 2.</span><span class="sxs-lookup"><span data-stu-id="998b3-170">Clicking on **View error log** on the **properties pane** produces the display shown in Figure 2.</span></span>

  ![Finestra di popup con messaggio di errore][2]

<span data-ttu-id="998b3-172">*Figura 2. Finestra di popup con il messaggio di errore.*</span><span class="sxs-lookup"><span data-stu-id="998b3-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="998b3-173">Per visualizzare il messaggio di errore di R, è necessario usare output.log.</span><span class="sxs-lookup"><span data-stu-id="998b3-173">It looks like we need to look in output.log to see the R error message.</span></span> <span data-ttu-id="998b3-174">Fare clic su [Execute R Script][execute-r-script] e quindi fare clic sull'elemento **View output log** (Visualizza log di output) nel **riquadro delle proprietà** a destra.</span><span class="sxs-lookup"><span data-stu-id="998b3-174">Click on the [Execute R Script][execute-r-script] and then click on the **View output.log** item on the **properties pane** to the right.</span></span> <span data-ttu-id="998b3-175">Viene aperta una nuova finestra del browser e viene visualizzato quanto segue.</span><span class="sxs-lookup"><span data-stu-id="998b3-175">A new browser window opens, and I see the following.</span></span>

    [Critical]     Error: Error 0063: The following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="998b3-176">Questo messaggio di errore non contiene sorprese e identifica chiaramente il problema.</span><span class="sxs-lookup"><span data-stu-id="998b3-176">This error message contains no surprises and clearly identifies the problem.</span></span>

<span data-ttu-id="998b3-177">Per ispezionare il valore dei singoli oggetti in R; è possibile stampare i valori nel file output.log.</span><span class="sxs-lookup"><span data-stu-id="998b3-177">To inspect the value of any object in R, you can print these values to the output.log file.</span></span> <span data-ttu-id="998b3-178">Le regole per l'analisi dei valori di oggetto sono essenzialmente le stesse di una sessione R interattiva.</span><span class="sxs-lookup"><span data-stu-id="998b3-178">The rules for examining object values are essentially the same as in an interactive R session.</span></span> <span data-ttu-id="998b3-179">Se, ad esempio, si digita un nome di variabile in una riga, il valore dell'oggetto verrà stampato nel file output.log.</span><span class="sxs-lookup"><span data-stu-id="998b3-179">For example, if you type a variable name on a line, the value of the object will be printed to the output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="998b3-180">Pacchetti in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="998b3-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="998b3-181">Azure Machine Learning viene fornito con più di 350 pacchetti di linguaggio R preinstallati.</span><span class="sxs-lookup"><span data-stu-id="998b3-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="998b3-182">Per recuperare un elenco dei pacchetti preinstallati, è possibile usare il codice seguente nel modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-182">You can use the following code in the [Execute R Script][execute-r-script] module to retrieve a list of the preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="998b3-183">Se al momento non si riesce a comprendere l'ultima riga del codice, continuare a leggere.</span><span class="sxs-lookup"><span data-stu-id="998b3-183">If you don't understand the last line of this code at the moment, read on.</span></span> <span data-ttu-id="998b3-184">Nel resto del documento vengono discussi diversi aspetti dell'uso di R nell'ambiente di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="998b3-184">In the rest of this document we will extensively discuss using R in the Azure Machine Learning environment.</span></span>

### <a name="introduction-to-rstudio"></a><span data-ttu-id="998b3-185">Introduzione a RStudio</span><span class="sxs-lookup"><span data-stu-id="998b3-185">Introduction to RStudio</span></span>
<span data-ttu-id="998b3-186">RStudio è un ambiente IDE molto usato per R. RStudio verrà usato per la modifica, i test e il debug di alcuni codici R usati in questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="998b3-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of the R code used in this quick start guide.</span></span> <span data-ttu-id="998b3-187">Dopo il test, quando il codice R è pronto, è sufficiente tagliarlo e incollarlo dall'editor di RStudio a un modulo [Execute R Script][execute-r-script] di Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="998b3-187">Once R code is tested and ready, you simply cut and paste from the RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="998b3-188">Se il linguaggio di programmazione R non è installato nel computer desktop, eseguirne ora l'installazione.</span><span class="sxs-lookup"><span data-stu-id="998b3-188">If you do not have the R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="998b3-189">Download gratuiti del linguaggio di programmazione R open source sono disponibili nel sistema CRAN (Comprehensive R Archive Network) all'indirizzo [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="998b3-189">Free downloads of open source R language are available at the Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="998b3-190">Sono disponibili anche download per Windows, Mac OS e Linux/UNIX.</span><span class="sxs-lookup"><span data-stu-id="998b3-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="998b3-191">Scegliere un mirror vicino e seguire le istruzioni di download.</span><span class="sxs-lookup"><span data-stu-id="998b3-191">Choose a nearby mirror and follow the download directions.</span></span> <span data-ttu-id="998b3-192">Il sistema CRAN contiene anche una serie di utili pacchetti di analisi e manipolazione di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="998b3-193">Se non si ha familiarità con RStudio, è consigliabile scaricare e installare la versione desktop.</span><span class="sxs-lookup"><span data-stu-id="998b3-193">If you are new to RStudio, you should download and install the desktop version.</span></span> <span data-ttu-id="998b3-194">I download di RStudio per Windows, Mac OS e Linux/UNIX sono disponibili all'indirizzo http://www.rstudio.com/products/RStudio/.</span><span class="sxs-lookup"><span data-stu-id="998b3-194">You can find the RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="998b3-195">Seguire le indicazioni fornite per installare RStudio sul proprio desktop.</span><span class="sxs-lookup"><span data-stu-id="998b3-195">Follow the directions provided to install RStudio on your desktop machine.</span></span>  

<span data-ttu-id="998b3-196">Un'esercitazione introduttiva a RStudio è disponibile all'indirizzo https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span><span class="sxs-lookup"><span data-stu-id="998b3-196">A tutorial introduction to RStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="998b3-197">Altre informazioni sull'uso di RStudio sono disponibili nell'[Appendice A][appendixa].</span><span class="sxs-lookup"><span data-stu-id="998b3-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="998b3-198"><a id="scriptmodule"></a>Input e output dei dati nel modulo Execute R Script</span><span class="sxs-lookup"><span data-stu-id="998b3-198"><a id="scriptmodule"></a>Get data in and out of the Execute R Script module</span></span>
<span data-ttu-id="998b3-199">Questa sezione descrive come eseguire l'input e l'output di dati nel modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-199">In this section we will discuss how you get data into and out of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="998b3-200">Viene inoltre esaminato come gestire i diversi tipi di dati di input e output nel modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-200">We will review how to handle various data types read into and out of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="998b3-201">Il codice completo per questa sezione è contenuto nel file con estensione zip scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="998b3-201">The complete code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="998b3-202">Caricare e controllare i dati in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="998b3-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="998b3-203"><a id="loading"></a>Caricare il set di dati</span><span class="sxs-lookup"><span data-stu-id="998b3-203"><a id="loading"></a>Load the dataset</span></span>
<span data-ttu-id="998b3-204">Prima di tutto, caricare il file **csdairydata.csv** in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="998b3-204">We will start by loading the **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="998b3-205">Avviare l'ambiente di Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="998b3-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="998b3-206">Fare clic su **+ NEW** (+ NUOVO) nell'angolo in basso a sinistra dello schermo e selezionare **Dataset** (Set di dati).</span><span class="sxs-lookup"><span data-stu-id="998b3-206">Click on **+ NEW** at the lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="998b3-207">Fare clic su **From Local File** (Da file locale) e quindi su **Browse** (Sfoglia) per selezionare il file.</span><span class="sxs-lookup"><span data-stu-id="998b3-207">Select **From Local File**, and then **Browse** to select the file.</span></span>
* <span data-ttu-id="998b3-208">Verificare di aver selezionato **Generic CSV file with header (.csv)** come tipo per il set di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-208">Make sure you have selected **Generic CSV file with header (.csv)** as the type for the dataset.</span></span>
* <span data-ttu-id="998b3-209">Fare clic sul segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="998b3-209">Click the check mark.</span></span>
* <span data-ttu-id="998b3-210">Dopo aver caricato il set di dati, il nuovo set di dati viene visualizzato facendo clic sulla scheda **Set di dati** .</span><span class="sxs-lookup"><span data-stu-id="998b3-210">After the dataset has been uploaded, you should see the new dataset by clicking on the **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="998b3-211">Creare un esperimento</span><span class="sxs-lookup"><span data-stu-id="998b3-211">Create an experiment</span></span>
<span data-ttu-id="998b3-212">Ora che sono presenti dei dati in Machine Learning Studio, è necessario creare un esperimento per eseguire l'analisi.</span><span class="sxs-lookup"><span data-stu-id="998b3-212">Now that we have some data in Machine Learning Studio, we need to create an experiment to do the analysis.</span></span>  

* <span data-ttu-id="998b3-213">Fare clic su **+ NEW** (+ NUOVO) in basso a sinistra e selezionare **Experiment** (Esperimento), quindi **Blank Experiment** (Esperimento vuoto).</span><span class="sxs-lookup"><span data-stu-id="998b3-213">Click on **+ NEW** at the lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="998b3-214">È possibile denominare l'esperimento selezionandolo e modificando il titolo **Experiment created on...** nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="998b3-214">You can name your experiment by selecting, and modifying, the **Experiment created on ...** title at the top of the page.</span></span> <span data-ttu-id="998b3-215">Ad esempio, è possibile modificare il titolo in **CA Dairy Analysis**.</span><span class="sxs-lookup"><span data-stu-id="998b3-215">For example, changing it to **CA Dairy Analysis**.</span></span>
* <span data-ttu-id="998b3-216">A sinistra della pagina dell'esperimento espandere **Saved Datasets** (Set di dati salvati) e quindi **My Datasets** (Set di dati personali).</span><span class="sxs-lookup"><span data-stu-id="998b3-216">On the left of the experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="998b3-217">Verrà visualizzato il set di dati **cadairydata.csv** caricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="998b3-217">You should see the **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="998b3-218">Trascinare **csdairydata.csv set di dati** nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="998b3-218">Drag and drop the **csdairydata.csv dataset** onto the experiment.</span></span>
* <span data-ttu-id="998b3-219">Nella casella **Search experiment items** (Cerca elementi esperimento) nella parte superiore del riquadro sinistro digitare [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-219">In the **Search experiment items** box on the top of the left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="998b3-220">Nell'elenco di ricerca viene visualizzato il modulo corrispondente.</span><span class="sxs-lookup"><span data-stu-id="998b3-220">You will see the module appear in the search list.</span></span>
* <span data-ttu-id="998b3-221">Trascinare il modulo [Execute R Script][execute-r-script] nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="998b3-221">Drag and drop the [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="998b3-222">Connettere l'output del **set di dati csdairydata.csv** all'input più a sinistra (**Dataset1**) del modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-222">Connect the output of the **csdairydata.csv dataset** to the leftmost input (**Dataset1**) of the [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="998b3-223">**Non dimenticare di fare clic su 'Save'.**</span><span class="sxs-lookup"><span data-stu-id="998b3-223">**Don't forget to click on 'Save'!**</span></span>  

<span data-ttu-id="998b3-224">A questo punto, l'esperimento dovrebbe essere simile a quanto riportato nella Figura 3.</span><span class="sxs-lookup"><span data-stu-id="998b3-224">At this point your experiment should look something like Figure 3.</span></span>

![L'esperimento CA Dairy Analysis con il set di dati e il modulo Execute R Script][3]

<span data-ttu-id="998b3-226">*Figura 3. Esperimento CA Dairy Analysis con il set di dati e il modulo Execute R Script.*</span><span class="sxs-lookup"><span data-stu-id="998b3-226">*Figure 3. The CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-the-data"></a><span data-ttu-id="998b3-227">Controllo dei dati</span><span class="sxs-lookup"><span data-stu-id="998b3-227">Check on the data</span></span>
<span data-ttu-id="998b3-228">Diamo ora un'occhiata ai dati caricati nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="998b3-228">Let's have a look at the data we have loaded into our experiment.</span></span> <span data-ttu-id="998b3-229">Nell'esperimento fare clic sull'output del **set di dati cadairydata.csv** e selezionare **Visualize** (Visualizza).</span><span class="sxs-lookup"><span data-stu-id="998b3-229">In the experiment, click on the output of the **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="998b3-230">Dovrebbe apparire una tabella simile a quella riportata nella Figura 4.</span><span class="sxs-lookup"><span data-stu-id="998b3-230">You should see something like Figure 4.</span></span>  

![Riepilogo del set di dati cadairydata.csv][4]

<span data-ttu-id="998b3-232">*Figura 4. Riepilogo del set di dati cadairydata.csv.*</span><span class="sxs-lookup"><span data-stu-id="998b3-232">*Figure 4. Summary of the cadairydata.csv dataset.*</span></span>

<span data-ttu-id="998b3-233">In questa tabella sono presenti numerose informazioni utili.</span><span class="sxs-lookup"><span data-stu-id="998b3-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="998b3-234">Vengono visualizzate diverse righe del set di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-234">We can see the first several rows of that dataset.</span></span> <span data-ttu-id="998b3-235">Se si seleziona una colonna, nella sezione relativa alle statistiche vengono visualizzate altre informazioni sulla colonna.</span><span class="sxs-lookup"><span data-stu-id="998b3-235">If we select a column, the Statistics section shows more information about the column.</span></span> <span data-ttu-id="998b3-236">La riga Tipo di funzionalità mostra ad esempio i tipi di dati che Azure Machine Learning Studio ha assegnato alla colonna.</span><span class="sxs-lookup"><span data-stu-id="998b3-236">For example, the Feature Type row shows us what data types Azure Machine Learning Studio assigned to the column.</span></span> <span data-ttu-id="998b3-237">Avere un quadro d'insieme può essere di grande aiuto prima di iniziare la fase di analisi vera e propria.</span><span class="sxs-lookup"><span data-stu-id="998b3-237">Having a quick look like this is a good sanity check before we start to do any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="998b3-238">Primo script R</span><span class="sxs-lookup"><span data-stu-id="998b3-238">First R script</span></span>
<span data-ttu-id="998b3-239">Creare un primo, semplice script R da provare con Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="998b3-239">Let's create a simple first R script to experiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="998b3-240">Lo script seguente è stato creato e testato in RStudio.</span><span class="sxs-lookup"><span data-stu-id="998b3-240">I have created and tested the following script in RStudio.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="998b3-241">Ora è necessario trasferirlo in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="998b3-241">Now I need to transfer this script to Azure Machine Learning Studio.</span></span> <span data-ttu-id="998b3-242">Potrei semplicemente eseguire un'operazione di copia e incolla,</span><span class="sxs-lookup"><span data-stu-id="998b3-242">I could simply cut and paste.</span></span> <span data-ttu-id="998b3-243">ma in questo caso trasferirò lo script R tramite un file con estensione zip.</span><span class="sxs-lookup"><span data-stu-id="998b3-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-to-the-execute-r-script-module"></a><span data-ttu-id="998b3-244">Input di dati nel modulo Execute R Script</span><span class="sxs-lookup"><span data-stu-id="998b3-244">Data input to the Execute R Script module</span></span>
<span data-ttu-id="998b3-245">Osservare ora gli input per il modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-245">Let's have a look at the inputs to the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="998b3-246">In questo esempio vengono letti i dati caseari della California nel modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-246">In this example we will read the California dairy data into the [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="998b3-247">Esistono tre possibili input per il modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-247">There are three possible inputs for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="998b3-248">È possibile usarne una o tutte, in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="998b3-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="998b3-249">È anche possibile usare uno script R senza alcun input.</span><span class="sxs-lookup"><span data-stu-id="998b3-249">It is also perfectly reasonable to use an R script that takes no input at all.</span></span>  

<span data-ttu-id="998b3-250">Di seguito vengono esaminati i singoli input, da sinistra a destra.</span><span class="sxs-lookup"><span data-stu-id="998b3-250">Let's look at each of these inputs, going from left to right.</span></span> <span data-ttu-id="998b3-251">È possibile visualizzare i nomi di ciascun input posizionando il cursore sull'input e leggendo la descrizione comando.</span><span class="sxs-lookup"><span data-stu-id="998b3-251">You can see the names of each of the inputs by placing your cursor over the input and reading the tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="998b3-252">Script Bundle</span><span class="sxs-lookup"><span data-stu-id="998b3-252">Script Bundle</span></span>
<span data-ttu-id="998b3-253">L'input Script Bundle consente di spostare il contenuto di un file con estensione zip nel modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-253">The Script Bundle input allows you to pass the contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="998b3-254">È possibile usare uno dei seguenti comandi per leggere i contenuti del file con estensione zip nel codice R.</span><span class="sxs-lookup"><span data-stu-id="998b3-254">You can use one of the following commands to read the contents of the zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="998b3-255">Azure Machine Learning gestisce i file nel pacchetto con estensione zip come se fossero nella directory src/, quindi è necessario inserire questo nome della directory come prefisso nei nomi file.</span><span class="sxs-lookup"><span data-stu-id="998b3-255">Azure Machine Learning treats files in the zip as if they are in the src/ directory, so you need to prefix your file names with this directory name.</span></span> <span data-ttu-id="998b3-256">Ad esempio, se il file con estensione zip contiene i file `yourfile.R` e `yourData.rdata` nella radice del file con estensione zip, è necessario risolvere questi come `src/yourfile.R` e `src/yourData.rdata` quando si usano `source` e `load`.</span><span class="sxs-lookup"><span data-stu-id="998b3-256">For example, if the zip contains the files `yourfile.R` and `yourData.rdata` in the root of the zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="998b3-257">Il caricamento dei set di dati è già stato discusso in [Caricamento del set di dati](#loading).</span><span class="sxs-lookup"><span data-stu-id="998b3-257">We already discussed loading datasets in [Loading the dataset](#loading).</span></span> <span data-ttu-id="998b3-258">Dopo aver creato e testato lo script R mostrato nella sezione precedente, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="998b3-258">Once you have created and tested the R script shown in the previous section, do the following:</span></span>

1. <span data-ttu-id="998b3-259">Salvare lo script R in un file .R.</span><span class="sxs-lookup"><span data-stu-id="998b3-259">Save the R script into a .R file.</span></span> <span data-ttu-id="998b3-260">Chiamerò il mio file di script "simpleplot.R".</span><span class="sxs-lookup"><span data-stu-id="998b3-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="998b3-261">Ecco il contenuto.</span><span class="sxs-lookup"><span data-stu-id="998b3-261">Here's the contents.</span></span>
   
        ## Only one of the following two lines should be used
        ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
        ## If in RStudio, use the second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## The following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="998b3-262">Creare un file con estensione zip e copiare al suo interno lo script creato.</span><span class="sxs-lookup"><span data-stu-id="998b3-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="998b3-263">In Windows è possibile fare clic con il pulsante destro del mouse sul file, scegliere **Invia a** e quindi **Cartella compressa**.</span><span class="sxs-lookup"><span data-stu-id="998b3-263">On Windows, you can right-click on the file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="998b3-264">Verrà creato un nuovo file con estensione zip contenente il file "simpleplot.R".</span><span class="sxs-lookup"><span data-stu-id="998b3-264">This will create a new zip file containing the "simpleplot.R" file.</span></span>
3. <span data-ttu-id="998b3-265">Aggiungere il file ai **set di dati** in Machine Learning Studio, specificando il tipo **zip**.</span><span class="sxs-lookup"><span data-stu-id="998b3-265">Add your file to the **datasets** in Machine Learning Studio, specifying the type as **zip**.</span></span> <span data-ttu-id="998b3-266">Dovrebbe essere visualizzato il file con estensione zip nei set di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-266">You should now see the zip file in your datasets.</span></span>
4. <span data-ttu-id="998b3-267">Trascinare il file ZIP dai **set di dati** all'**area di disegno di ML Studio**.</span><span class="sxs-lookup"><span data-stu-id="998b3-267">Drag and drop the zip file from **datasets** onto the **ML Studio canvas**.</span></span>
5. <span data-ttu-id="998b3-268">Connettere l'output dell'icona dei **dati zip** all'input **Script Bundle** del modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-268">Connect the output of the **zip data** icon to the **Script Bundle** input of the [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="998b3-269">Digitare la funzione `source()` con il nome del file con estensione zip nella finestra del codice per il modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-269">Type the `source()` function with your zip file name into the code window for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="998b3-270">In questo caso, digitare `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="998b3-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="998b3-271">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="998b3-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="998b3-272">Dopo aver completato questi passaggi, il modulo [Execute R Script][execute-r-script] eseguirà lo script R nel file con estensione zip durante l'esecuzione dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="998b3-272">Once these steps are complete, the [Execute R Script][execute-r-script] module will execute the R script in the zip file when the experiment is run.</span></span> <span data-ttu-id="998b3-273">A questo punto l'esperimento dovrebbe avere un aspetto simile a quello riportato nella Figura 5.</span><span class="sxs-lookup"><span data-stu-id="998b3-273">At this point your experiment should look something like Figure 5.</span></span>

![Esperimento con script R compresso][6]

<span data-ttu-id="998b3-275">*Figura 5. Esperimento con script R compresso.*</span><span class="sxs-lookup"><span data-stu-id="998b3-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="998b3-276">Dataset1</span><span class="sxs-lookup"><span data-stu-id="998b3-276">Dataset1</span></span>
<span data-ttu-id="998b3-277">È possibile passare una tabella di dati rettangolare al codice R usando l'input Dataset1.</span><span class="sxs-lookup"><span data-stu-id="998b3-277">You can pass a rectangular table of data to your R code by using the Dataset1 input.</span></span> <span data-ttu-id="998b3-278">Nello script semplice descritto, la funzione `maml.mapInputPort(1)` legge i dati dalla porta 1.</span><span class="sxs-lookup"><span data-stu-id="998b3-278">In our simple script the `maml.mapInputPort(1)` function reads the data from port 1.</span></span> <span data-ttu-id="998b3-279">I dati vengono poi assegnati a un nome di variabile del frame di dati nel codice.</span><span class="sxs-lookup"><span data-stu-id="998b3-279">This data is then assigned to a dataframe variable name in your code.</span></span> <span data-ttu-id="998b3-280">Nel nostro script semplice è la prima riga del codice a effettuare l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="998b3-280">In our simple script the first line of code performs the assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="998b3-281">Eseguire l'esperimento facendo clic sul pulsante **Run** .</span><span class="sxs-lookup"><span data-stu-id="998b3-281">Execute your experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="998b3-282">Al termine dell'esecuzione, fare clic sul modulo [Execute R Script][execute-r-script] e quindi su **View output log** (Visualizza log di output) nel riquadro delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="998b3-282">When the execution finishes, click on the [Execute R Script][execute-r-script] module and then click **View output log** on the properties pane.</span></span> <span data-ttu-id="998b3-283">Viene visualizzata una nuova pagina del browser che mostra i contenuti del file output.log.</span><span class="sxs-lookup"><span data-stu-id="998b3-283">A new page should appear in your browser showing the contents of the output.log file.</span></span> <span data-ttu-id="998b3-284">Scorrendo la pagina, dovrebbe essere visualizzato quanto segue.</span><span class="sxs-lookup"><span data-stu-id="998b3-284">When you scroll down you should see something like the following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="998b3-285">Più in basso nella pagina sono disponibili altre informazioni sulle colonne, che avranno un aspetto simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="998b3-285">Farther down the page is more detailed information on the columns, which will look something like the following.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

<span data-ttu-id="998b3-286">Questi risultati sono essenzialmente quelli previsti, con 228 osservazioni e 9 colonne nel frame di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-286">These results are mostly as expected, with 228 observations and 9 columns in the dataframe.</span></span> <span data-ttu-id="998b3-287">Sono riportati i nomi delle colonne, il tipo di dati R e un esempio di ciascuna colonna.</span><span class="sxs-lookup"><span data-stu-id="998b3-287">We can see the column names, the R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="998b3-288">Lo stesso output stampato è disponibile anche dall'output R Device del modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-288">This same printed output is conveniently available from the R Device output of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="998b3-289">Gli output del modulo [Execute R Script][execute-r-script] verranno descritti nella prossima sezione.</span><span class="sxs-lookup"><span data-stu-id="998b3-289">We will discuss the outputs of the [Execute R Script][execute-r-script] module in the next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="998b3-290">Dataset2</span><span class="sxs-lookup"><span data-stu-id="998b3-290">Dataset2</span></span>
<span data-ttu-id="998b3-291">Il comportamento della modalità di input Dataset2 è identico a quello di Dataset1.</span><span class="sxs-lookup"><span data-stu-id="998b3-291">The behavior of the Dataset2 input is identical to that of Dataset1.</span></span> <span data-ttu-id="998b3-292">Consente infatti di passare nel codice R creato una seconda tabella rettangolare di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="998b3-293">La funzione `maml.mapInputPort(2)`, con l'argomento 2, viene usata per passare questi dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-293">The function `maml.mapInputPort(2)`, with the argument 2, is used to pass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="998b3-294">Output del modulo Execute R Script</span><span class="sxs-lookup"><span data-stu-id="998b3-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="998b3-295">Output di un frame di dati</span><span class="sxs-lookup"><span data-stu-id="998b3-295">Output a dataframe</span></span>
<span data-ttu-id="998b3-296">È possibile eseguire l'output dei contenuti di un frame di dati R come tabella rettangolare dalla porta Result Dataset1 usando la funzione `maml.mapOutputPort()` .</span><span class="sxs-lookup"><span data-stu-id="998b3-296">You can output the contents of an R dataframe as a rectangular table through the Result Dataset1 port by using the `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="998b3-297">Nello script R semplice descritto, questa operazione viene eseguita dalla riga seguente.</span><span class="sxs-lookup"><span data-stu-id="998b3-297">In our simple R script this is performed by the following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="998b3-298">Dopo aver eseguito l'esperimento, fare clic sulla porta di output Result Dataset1, quindi scegliere **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="998b3-298">After running the experiment, click on the Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="998b3-299">I risultati dovrebbero essere simili a quanto visualizzato nella Figura 6.</span><span class="sxs-lookup"><span data-stu-id="998b3-299">You should see something like Figure 6.</span></span>

![Visualizzazione dell'output dei dati caseari della California][7]

<span data-ttu-id="998b3-301">*Figura 6. Visualizzazione dell'output dei dati caseari della California.*</span><span class="sxs-lookup"><span data-stu-id="998b3-301">*Figure 6. The visualization of the output of the California dairy data.*</span></span>

<span data-ttu-id="998b3-302">In questo caso l'output è identico all'input, come previsto.</span><span class="sxs-lookup"><span data-stu-id="998b3-302">This output looks identical to the input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="998b3-303">Output R Device</span><span class="sxs-lookup"><span data-stu-id="998b3-303">R Device output</span></span>
<span data-ttu-id="998b3-304">L'output Device del modulo [Execute R Script][execute-r-script] contiene messaggi e output grafico.</span><span class="sxs-lookup"><span data-stu-id="998b3-304">The Device output of the [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="998b3-305">Alla porta di output R Device vengono inviati da R sia l'output standard sia i messaggi di errore standard.</span><span class="sxs-lookup"><span data-stu-id="998b3-305">Both standard output and standard error messages from R are sent to the R Device output port.</span></span>  

<span data-ttu-id="998b3-306">Per visualizzare l' output R Device, fare clic sulla porta e su **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="998b3-306">To view the R Device output, click on the port and then on **Visualize**.</span></span> <span data-ttu-id="998b3-307">Nella Figura 7 sono riportati l'output standard e i messaggi di errore standard generati dallo script R.</span><span class="sxs-lookup"><span data-stu-id="998b3-307">We see the standard output and standard error from the R script in Figure 7.</span></span>

![Output ed errore standard dalla porta R Device][8]

<span data-ttu-id="998b3-309">*Figura 7. Output ed errore standard dalla porta R Device.*</span><span class="sxs-lookup"><span data-stu-id="998b3-309">*Figure 7. Standard output and standard error from the R Device port.*</span></span>

<span data-ttu-id="998b3-310">Scorrendo verso il basso è possibile visualizzare l'output grafico generato dallo script R, riportato nella Figura 8.</span><span class="sxs-lookup"><span data-stu-id="998b3-310">Scrolling down we see the graphics output from our R script in Figure 8.</span></span>  

![Output dei grafici dalla porta R Device][9]

<span data-ttu-id="998b3-312">*Figura 8. Output dei grafici dalla porta R Device.*</span><span class="sxs-lookup"><span data-stu-id="998b3-312">*Figure 8. Graphics output from the R Device port.*</span></span>  

## <span data-ttu-id="998b3-313"><a id="filtering"></a>Filtraggio e trasformazione dei dati</span><span class="sxs-lookup"><span data-stu-id="998b3-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="998b3-314">In questa sezione effettueremo alcune operazioni di filtraggio e trasformazione di base sui dati caseari della California.</span><span class="sxs-lookup"><span data-stu-id="998b3-314">In this section we will perform some basic data filtering and transformation operations on the California dairy data.</span></span> <span data-ttu-id="998b3-315">Al termine di questa sezione i dati saranno disponibili in un formato adatto alla creazione di un modello di analisi.</span><span class="sxs-lookup"><span data-stu-id="998b3-315">By the end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="998b3-316">In particolare, in questa sezione vengono eseguite diverse attività comuni di pulizia e trasformazione dei dati: trasformazione del tipo, filtraggio nei frame di dati, aggiunta di nuove colonne elaborate e trasformazioni dei valori.</span><span class="sxs-lookup"><span data-stu-id="998b3-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="998b3-317">Queste procedure di base potrebbero essere utili per affrontare le numerose variazioni che spesso si generano nei problemi della vita reale.</span><span class="sxs-lookup"><span data-stu-id="998b3-317">This background should help you deal with the many variations encountered in real-world problems.</span></span>

<span data-ttu-id="998b3-318">Il codice R completo per questa sezione è disponibile nel file con estensione zip scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="998b3-318">The complete R code for this section is available in the zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="998b3-319">Trasformazioni di tipi</span><span class="sxs-lookup"><span data-stu-id="998b3-319">Type transformations</span></span>
<span data-ttu-id="998b3-320">Ora che è possibile leggere i dati caseari della California nel codice R del modulo [Execute R Script][execute-r-script], è necessario verificare che i dati nelle colonne abbiano il tipo e il formato previsti.</span><span class="sxs-lookup"><span data-stu-id="998b3-320">Now that we can read the California dairy data into the R code in the [Execute R Script][execute-r-script] module, we need to ensure that the data in the columns has the intended type and format.</span></span>  

<span data-ttu-id="998b3-321">R è un linguaggio tipizzato dinamicamente, in cui i tipi di dati vengono assegnati l'uno all'altro in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="998b3-321">R is a dynamically typed language, which means that data types are coerced from one to another as required.</span></span> <span data-ttu-id="998b3-322">Nel linguaggio R, i dati atomic possono essere di tipo numerico, logico e Char.</span><span class="sxs-lookup"><span data-stu-id="998b3-322">The atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="998b3-323">Il tipo fattore viene usato invece per archiviare in modo compatto i dati relativi alle categorie.</span><span class="sxs-lookup"><span data-stu-id="998b3-323">The factor type is used to compactly store categorical data.</span></span> <span data-ttu-id="998b3-324">Altre informazioni sui tipi di dati sono disponibili nei riferimenti dell' [Appendice B - Letture di approfondimento](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="998b3-324">You can find much more information on data types in the references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="998b3-325">Quando i dati tabulari vengono letti in R da un'origine esterna, è sempre opportuno controllare nelle colonne i tipi risultanti.</span><span class="sxs-lookup"><span data-stu-id="998b3-325">When tabular data is read into R from an external source, it is always a good idea to check the resulting types in the columns.</span></span> <span data-ttu-id="998b3-326">È possibile, ad esempio, che una colonna che sarebbe dovuta essere di tipo Char in realtà risulti di tipo fattore, o viceversa.</span><span class="sxs-lookup"><span data-stu-id="998b3-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="998b3-327">In altri casi, una colonna che si pensa debba essere numerica viene rappresentata da dati di tipo carattere, ad esempio '1,23' anziché 1,23 come numero a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="998b3-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="998b3-328">Fortunatamente, convertire un tipo in un altro tipo è piuttosto semplice, purché sia possibile il mapping.</span><span class="sxs-lookup"><span data-stu-id="998b3-328">Fortunately, it is easy to convert one type to another, as long as mapping is possible.</span></span> <span data-ttu-id="998b3-329">Ad esempio, non è possibile convertire "Nevada" in un valore numerico, ma è possibile convertirlo in un fattore (variabile di categoria).</span><span class="sxs-lookup"><span data-stu-id="998b3-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it to a factor (categorical variable).</span></span> <span data-ttu-id="998b3-330">Un valore numerico 1, invece, può essere convertito sia nel carattere "1" sia in un fattore.</span><span class="sxs-lookup"><span data-stu-id="998b3-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="998b3-331">La sintassi di queste conversioni è semplice: `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="998b3-331">The syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="998b3-332">Queste funzioni di conversione del tipo includono quanto segue.</span><span class="sxs-lookup"><span data-stu-id="998b3-332">These type conversion functions include the following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="998b3-333">Considerando i tipi di dati delle colonne di cui è stato eseguito l'input nella sezione precedente: tutte le colonne sono di tipo numerico, tranne quella etichettata 'Month', che è di tipo character.</span><span class="sxs-lookup"><span data-stu-id="998b3-333">Looking at the data types of the columns we input in the previous section: all columns are of type numeric, except for the column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="998b3-334">Proviamo quindi a convertire questa colonna in tipo fattore e controlliamo i risultati.</span><span class="sxs-lookup"><span data-stu-id="998b3-334">Let's convert this to a factor and test the results.</span></span>  

<span data-ttu-id="998b3-335">La riga con cui è stata creata la matrice del grafico a dispersione è stata eliminata ed è stata aggiunta un riga per la conversione della colonna 'Month' in un fattore.</span><span class="sxs-lookup"><span data-stu-id="998b3-335">I have deleted the line that created the scatterplot matrix and added a line converting the 'Month' column to a factor.</span></span> <span data-ttu-id="998b3-336">Nell'esperimento è sufficiente tagliare e incollare il codice R nella finestra del codice del modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-336">In my experiment I will just cut and paste the R code into the code window of the [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="998b3-337">È anche possibile aggiornare il file con estensione zip e caricarlo in Azure Machine Learning Studio, ma sono necessari diversi passaggi.</span><span class="sxs-lookup"><span data-stu-id="998b3-337">You could also update the zip file and upload it to Azure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check the result
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="998b3-338">Eseguiamo il codice e analizziamo il log di output per lo script R.</span><span class="sxs-lookup"><span data-stu-id="998b3-338">Let's execute this code and look at the output log for the R script.</span></span> <span data-ttu-id="998b3-339">I dati rilevanti del log sono illustrati nella Figura 9.</span><span class="sxs-lookup"><span data-stu-id="998b3-339">The relevant data from the log is shown in Figure 9.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="998b3-340">*Figura 9. Riepilogo del frame di dati con una variabile di fattore.*</span><span class="sxs-lookup"><span data-stu-id="998b3-340">*Figure 9. Summary of the dataframe with a factor variable.*</span></span>

<span data-ttu-id="998b3-341">Il tipo per Month sarà: '**Factor w/ 14 levels**'.</span><span class="sxs-lookup"><span data-stu-id="998b3-341">The type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="998b3-342">Questo è ovviamente un problema poiché in un anno ci sono solo 12 mesi.</span><span class="sxs-lookup"><span data-stu-id="998b3-342">This is a problem since there are only 12 months in the year.</span></span> <span data-ttu-id="998b3-343">È anche possibile controllare che in **Visualize** (Visualizza) il tipo della porta Result Dataset (Set di dati risultati) sia '**Categorical**' (Categorie).</span><span class="sxs-lookup"><span data-stu-id="998b3-343">You can also check to see that the type in **Visualize** of the Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="998b3-344">Il problema è che la colonna "Month" non è stata codificata in modo sistematico.</span><span class="sxs-lookup"><span data-stu-id="998b3-344">The problem is that the 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="998b3-345">Un mese può essere denominato Aprile in alcuni casi e abbreviato in Apr. in altri. Per risolvere il problema, è possibile ridurre la stringa a tre caratteri.</span><span class="sxs-lookup"><span data-stu-id="998b3-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming the string to 3 characters.</span></span> <span data-ttu-id="998b3-346">La riga di codice dovrebbe ora apparire così:</span><span class="sxs-lookup"><span data-stu-id="998b3-346">The line of code now looks like the following:</span></span>

    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="998b3-347">Eseguire nuovamente l'esperimento e visualizzare il log di output.</span><span class="sxs-lookup"><span data-stu-id="998b3-347">Rerun the experiment and view the output log.</span></span> <span data-ttu-id="998b3-348">I risultati previsti sono illustrati nella Figura 10.</span><span class="sxs-lookup"><span data-stu-id="998b3-348">The expected results are shown in Figure 10.</span></span>  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="998b3-349">*Figura 10. Riepilogo del frame di dati con il numero corretto di livelli di fattore.*</span><span class="sxs-lookup"><span data-stu-id="998b3-349">*Figure 10. Summary of the dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="998b3-350">La variabile di fattore contiene ora 12 livelli.</span><span class="sxs-lookup"><span data-stu-id="998b3-350">Our factor variable now has the desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="998b3-351">Filtraggio di frame di dati di base</span><span class="sxs-lookup"><span data-stu-id="998b3-351">Basic data frame filtering</span></span>
<span data-ttu-id="998b3-352">I frame di dati R supportano avanzate funzionalità di filtraggio.</span><span class="sxs-lookup"><span data-stu-id="998b3-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="998b3-353">I set di dati, infatti, possono essere suddivisi in sottoinsiemi usando filtri logici su righe o colonne.</span><span class="sxs-lookup"><span data-stu-id="998b3-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="998b3-354">In molto casi, tuttavia, sono necessari complessi criteri di filtro.</span><span class="sxs-lookup"><span data-stu-id="998b3-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="998b3-355">I riferimenti nell' [Appendice B - Letture di approfondimento](#appendixb) contengono numerosi esempi di filtraggio dei frame di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-355">The references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="998b3-356">Possiamo eseguire semplici operazioni di filtraggio anche sul nostro set di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="998b3-357">Se si guardano le colonne nel frame di dati cadairydata, si può vedere che ci sono due colonne superflue.</span><span class="sxs-lookup"><span data-stu-id="998b3-357">If you look at the columns in the cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="998b3-358">La prima colonna contiene solo un numero di riga, non molto utile.</span><span class="sxs-lookup"><span data-stu-id="998b3-358">The first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="998b3-359">La seconda colonna, Year.Month, contiene le informazioni ridondanti.</span><span class="sxs-lookup"><span data-stu-id="998b3-359">The second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="998b3-360">È possibile escludere facilmente queste colonne usando il seguente codice R.</span><span class="sxs-lookup"><span data-stu-id="998b3-360">We can easily exclude these columns by using the following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="998b3-361">Nel resto di questa sezione verrà mostrato solo il codice aggiuntivo inserito nel modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-361">From now on in this section, I will just show you the additional code I am adding in the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="998b3-362">Ogni nuova riga verrà aggiunta **prima** della funzione `str()`.</span><span class="sxs-lookup"><span data-stu-id="998b3-362">I will add each new line **before** the `str()` function.</span></span> <span data-ttu-id="998b3-363">Questa funzione viene usata per verificare i risultati in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="998b3-363">I use this function to verify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="998b3-364">Viene quindi aggiunta la riga seguente al codice R nel modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-364">I add the following line to my R code in the [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="998b3-365">Eseguire questo codice nell'esperimento e verificare il risultato del log di output.</span><span class="sxs-lookup"><span data-stu-id="998b3-365">Run this code in your experiment and check the result from the output log.</span></span> <span data-ttu-id="998b3-366">Questi risultati vengono mostrati nella Figura 11.</span><span class="sxs-lookup"><span data-stu-id="998b3-366">These results are shown in Figure 11.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="998b3-367">*Figura 11. Riepilogo del frame di dati con due colonne rimosse.*</span><span class="sxs-lookup"><span data-stu-id="998b3-367">*Figure 11. Summary of the dataframe with two columns removed.*</span></span>

<span data-ttu-id="998b3-368">Ottime notizie!</span><span class="sxs-lookup"><span data-stu-id="998b3-368">Good news!</span></span> <span data-ttu-id="998b3-369">I risultati ottenuti sono quelli previsti.</span><span class="sxs-lookup"><span data-stu-id="998b3-369">We get the expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="998b3-370">Aggiungere una nuova colonna</span><span class="sxs-lookup"><span data-stu-id="998b3-370">Add a new column</span></span>
<span data-ttu-id="998b3-371">Per la creazione di modelli in serie temporale sarà utile disporre di una colonna contenente i nomi dei mesi a partire dall'inizio della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="998b3-371">To create time series models it will be convenient to have a column containing the months since the start of the time series.</span></span> <span data-ttu-id="998b3-372">Creeremo quindi una nuova colonna denominata "Month.Count".</span><span class="sxs-lookup"><span data-stu-id="998b3-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="998b3-373">Per organizzare il codice, è necessario creare una prima funzione semplice, `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="998b3-373">To help organize the code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="998b3-374">La funzione verrà quindi applicata per creare una nuova colonna nel frame di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-374">We will then apply this function to create a new column in the dataframe.</span></span> <span data-ttu-id="998b3-375">Il nuovo codice è il seguente.</span><span class="sxs-lookup"><span data-stu-id="998b3-375">The new code is as follows.</span></span>

    ## Create a new column with the month count
    ## Function to find the number of months from the first
    ## month of the time series
    num.month <- function(Year, Month) {
      ## Find the starting year
      min.year  <- min(Year)

      ## Compute the number of months from the start of the time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute the new column for the dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="998b3-376">Eseguire l'esperimento aggiornato e usare il log di output per visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="998b3-376">Now run the updated experiment and use the output log to view the results.</span></span> <span data-ttu-id="998b3-377">I risultati previsti sono illustrati nella Figura 12.</span><span class="sxs-lookup"><span data-stu-id="998b3-377">These results are shown in Figure 12.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="998b3-378">*Figura 12. Riepilogo del frame di dati con la colonna aggiuntiva.*</span><span class="sxs-lookup"><span data-stu-id="998b3-378">*Figure 12. Summary of the dataframe with the additional column.*</span></span>

<span data-ttu-id="998b3-379">Sembra che tutto stia funzionando perfettamente.</span><span class="sxs-lookup"><span data-stu-id="998b3-379">It looks like everything is working.</span></span> <span data-ttu-id="998b3-380">La nuova colonna con i valori previsti è stata creata correttamente nel frame di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-380">We have the new column with the expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="998b3-381">Trasformazioni di valori</span><span class="sxs-lookup"><span data-stu-id="998b3-381">Value transformations</span></span>
<span data-ttu-id="998b3-382">In questa sezione eseguiremo semplici operazioni di trasformazione sui valori di alcune delle colonne del frame di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-382">In this section we will perform some simple transformations on the values in some of the columns of our dataframe.</span></span> <span data-ttu-id="998b3-383">Il linguaggio R supporta trasformazioni di dati pressoché arbitrarie.</span><span class="sxs-lookup"><span data-stu-id="998b3-383">The R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="998b3-384">I riferimenti nell' [Appendice B - Letture di approfondimento](#appendixb) contengono numerosi esempi.</span><span class="sxs-lookup"><span data-stu-id="998b3-384">The references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="998b3-385">Se si guardano i valori nei riepiloghi del frame di dati, si nota qualcosa di strano.</span><span class="sxs-lookup"><span data-stu-id="998b3-385">If you look at the values in the summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="998b3-386">In California si produce più gelato che latte?</span><span class="sxs-lookup"><span data-stu-id="998b3-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="998b3-387">No, ovviamente no, sfortunatamente per gli amanti del gelato.</span><span class="sxs-lookup"><span data-stu-id="998b3-387">No, of course not, as this makes no sense, sad as this fact may be to some of us ice cream lovers.</span></span> <span data-ttu-id="998b3-388">Le unità di misura sono diverse.</span><span class="sxs-lookup"><span data-stu-id="998b3-388">The units are different.</span></span> <span data-ttu-id="998b3-389">Il prezzo è espresso in unità di libbre statunitensi, il latte è espresso in unità da un milione di libbre statunitensi, il gelato in unità da 1000 galloni statunitensi e i fiocchi di latte in unità da 1000 libbre statunitensi.</span><span class="sxs-lookup"><span data-stu-id="998b3-389">The price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="998b3-390">Supponendo che il gelato pesi circa 6,5 libbre al gallone, è facile eseguire la moltiplicazione per convertire questi valori in modo che siano espressi in unità da 1000 libbre.</span><span class="sxs-lookup"><span data-stu-id="998b3-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do the multiplication to convert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="998b3-391">Per il modello di previsione viene usato un modello moltiplicativo per le tendenze e l'adattamento stagionale dei dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="998b3-392">Una trasformazione logaritmica, infine, ci consente di usare un modello lineare, semplificando notevolmente il processo.</span><span class="sxs-lookup"><span data-stu-id="998b3-392">A log transformation allows us to use a linear model, simplifying this process.</span></span> <span data-ttu-id="998b3-393">Possiamo applicare la trasformazione logaritmica alla stessa funzione a cui è stato applicato il moltiplicatore.</span><span class="sxs-lookup"><span data-stu-id="998b3-393">We can apply the log transformation in the same function where the multiplier is applied.</span></span>

<span data-ttu-id="998b3-394">Nel codice seguente viene definita una nuova funzione `log.transform()`, che viene poi applicata alle righe che contengono i valori numerici.</span><span class="sxs-lookup"><span data-stu-id="998b3-394">In the following code, I define a new function, `log.transform()`, and apply it to the rows containing the numerical values.</span></span> <span data-ttu-id="998b3-395">La funzione R `Map()` viene usata per applicare la funzione `log.transform()` alle colonne selezionate del frame di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-395">The R `Map()` function is used to apply the `log.transform()` function to the selected columns of the dataframe.</span></span> <span data-ttu-id="998b3-396">`Map()` è simile a `apply()`, ma permette l'uso di più di un elenco di argomenti nella funzione.</span><span class="sxs-lookup"><span data-stu-id="998b3-396">`Map()` is similar to `apply()` but allows for more than one list of arguments to the function.</span></span> <span data-ttu-id="998b3-397">Un elenco di moltiplicatori fornisce il secondo argomento alla funzione `log.transform()` .</span><span class="sxs-lookup"><span data-stu-id="998b3-397">Note that a list of multipliers supplies the second argument to the `log.transform()` function.</span></span> <span data-ttu-id="998b3-398">La funzione `na.omit()` viene usata come strumento di pulizia per assicurare che non ci siano valori mancanti o non definiti nel frame di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-398">The `na.omit()` function is used as a bit of cleanup to ensure we do not have missing or undefined values in the dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for the transformation, which is the log
      ## of the input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments to function log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier to funcition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check the input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap the multiplication in tryCatch
      ## If there is an exception, print the warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply the transformation function to the 4 columns
    ## of the dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="998b3-399">La funzione `log.transform()` espleta quindi numerose operazioni.</span><span class="sxs-lookup"><span data-stu-id="998b3-399">There is quite a bit happening in the `log.transform()` function.</span></span> <span data-ttu-id="998b3-400">Gran parte del codice è progettato per controllare la presenza di potenziali problemi con gli argomenti o per gestire le eccezioni, che possono sempre verificarsi durante i calcoli.</span><span class="sxs-lookup"><span data-stu-id="998b3-400">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="998b3-401">Solo poche righe del codice, quindi, eseguono effettivamente i calcoli.</span><span class="sxs-lookup"><span data-stu-id="998b3-401">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="998b3-402">L'obiettivo della programmazione difensiva consiste nel prevenire errori in una singola funzione che potrebbero bloccare l'intera elaborazione.</span><span class="sxs-lookup"><span data-stu-id="998b3-402">The goal of the defensive programming is to prevent the failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="998b3-403">Un errore improvviso in un'analisi di lunga durata può essere piuttosto frustrante per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="998b3-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="998b3-404">Per evitare questa situazione, è necessario scegliere valori restituiti predefiniti in grado di limitare i danni nell'elaborazione a valle.</span><span class="sxs-lookup"><span data-stu-id="998b3-404">To avoid this situation, default return values must be chosen that will limit damage to downstream processing.</span></span> <span data-ttu-id="998b3-405">Viene inoltre generato un messaggio di avviso per informare gli utenti che si è verificato un errore.</span><span class="sxs-lookup"><span data-stu-id="998b3-405">A message is also produced to alert users that something has gone wrong.</span></span>

<span data-ttu-id="998b3-406">Se non si ha familiarità con la programmazione difensiva in R, questo codice può sembrare eccessivamente complesso.</span><span class="sxs-lookup"><span data-stu-id="998b3-406">If you are not used to defensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="998b3-407">Affronteremo di seguito i passaggi principali:</span><span class="sxs-lookup"><span data-stu-id="998b3-407">I will walk you through the major steps:</span></span>

1. <span data-ttu-id="998b3-408">Viene definito un vettore di quattro messaggi.</span><span class="sxs-lookup"><span data-stu-id="998b3-408">A vector of four messages is defined.</span></span> <span data-ttu-id="998b3-409">Questi messaggi vengono usati per comunicare informazioni relative a errori ed eccezioni che possono verificarsi nel codice.</span><span class="sxs-lookup"><span data-stu-id="998b3-409">These messages are used to communicate information about some of the possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="998b3-410">Per ciascun caso restituirò il valore NA.</span><span class="sxs-lookup"><span data-stu-id="998b3-410">I return a value of NA for each case.</span></span> <span data-ttu-id="998b3-411">Esistono diverse altre possibilità che potrebbero avere un minor numero di effetti collaterali.</span><span class="sxs-lookup"><span data-stu-id="998b3-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="998b3-412">Ad esempio, potrei restituire un vettore di zeri o il vettore di input originale.</span><span class="sxs-lookup"><span data-stu-id="998b3-412">I could return a vector of zeroes, or the original input vector, for example.</span></span>
3. <span data-ttu-id="998b3-413">Vengono eseguiti controlli sugli argomenti alla funzione.</span><span class="sxs-lookup"><span data-stu-id="998b3-413">Checks are run on the arguments to the function.</span></span> <span data-ttu-id="998b3-414">In ogni caso, se viene rilevato un errore, la funzione `warning()` restituisce un valore predefinito e un messaggio.</span><span class="sxs-lookup"><span data-stu-id="998b3-414">In each case, if an error is detected, a default value is returned and a message is produced by the `warning()` function.</span></span> <span data-ttu-id="998b3-415">In questo caso viene usato `warning()` e non `stop()` perché quest'ultimo comporta l'arresto dell'esecuzione, che si vuole evitare.</span><span class="sxs-lookup"><span data-stu-id="998b3-415">I am using `warning()` rather than `stop()` as the latter will terminate execution, exactly what I am trying to avoid.</span></span> <span data-ttu-id="998b3-416">Osservare come abbia scritto questo codice in stile procedurale: un approccio funzionale sarebbe apparso in questo caso eccessivamente complesso e oscuro.</span><span class="sxs-lookup"><span data-stu-id="998b3-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="998b3-417">I calcoli del log vengono inclusi in `tryCatch()` in modo che le eccezioni non causino un arresto improvviso dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="998b3-417">The log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt to processing.</span></span> <span data-ttu-id="998b3-418">Senza `tryCatch()` , la maggior parte degli errori generati dalle funzioni R producono un segnale di arresto, che interrompe l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="998b3-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="998b3-419">Eseguire questo codice R nel proprio esperimento e osservare l'output generato nel file output.log.</span><span class="sxs-lookup"><span data-stu-id="998b3-419">Execute this R code in your experiment and have a look at the printed output in the output.log file.</span></span> <span data-ttu-id="998b3-420">Verranno visualizzati i valori trasformati delle quattro colonne nel log, come illustrato nella Figura 13.</span><span class="sxs-lookup"><span data-stu-id="998b3-420">You will now see the transformed values of the four columns in the log, as shown in Figure 13.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="998b3-421">*Figura 13. Riepilogo dei valori trasformati nel frame di dati.*</span><span class="sxs-lookup"><span data-stu-id="998b3-421">*Figure 13. Summary of the transformed values in the dataframe.*</span></span>

<span data-ttu-id="998b3-422">I valori sono stati trasformati correttamente.</span><span class="sxs-lookup"><span data-stu-id="998b3-422">We see the values have been transformed.</span></span> <span data-ttu-id="998b3-423">La produzione di latte supera ora di gran lunga la produzione di tutti gli altri prodotti caseari, ricordandoci come si stia ora usando una scala logaritmica .</span><span class="sxs-lookup"><span data-stu-id="998b3-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="998b3-424">A questo punto i nostri dati sono puliti e siamo pronti per qualche operazione di modeling.</span><span class="sxs-lookup"><span data-stu-id="998b3-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="998b3-425">Osservando il riepilogo della visualizzazione per l'output Result Dataset del modulo [Execute R Script][execute-r-script], si può notare che la colonna 'Month' è 'Categorical' con 12 valori univoci, ovvero il risultato desiderato.</span><span class="sxs-lookup"><span data-stu-id="998b3-425">Looking at the visualization summary for the Result Dataset output of our [Execute R Script][execute-r-script] module, you will see the 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="998b3-426"><a id="timeseries"></a>Oggetti della serie temporale e analisi delle correlazioni</span><span class="sxs-lookup"><span data-stu-id="998b3-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="998b3-427">In questa sezione analizzeremo alcuni oggetti serie temporale di R e analizzeremo le correlazioni tra alcune delle variabili.</span><span class="sxs-lookup"><span data-stu-id="998b3-427">In this section we will explore a few basic R time series objects and analyze the correlations between some of the variables.</span></span> <span data-ttu-id="998b3-428">Il nostro obiettivo è generare un frame di dati contenente informazioni di correlazione pairwise a vari intervalli.</span><span class="sxs-lookup"><span data-stu-id="998b3-428">Our goal is to output a dataframe containing the pairwise correlation information at several lags.</span></span>

<span data-ttu-id="998b3-429">Il codice R completo per questa sezione è disponibile nel file con estensione zip scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="998b3-429">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="998b3-430">Oggetti della serie temporale in R</span><span class="sxs-lookup"><span data-stu-id="998b3-430">Time series objects in R</span></span>
<span data-ttu-id="998b3-431">Come già accennato, le serie temporali sono costituite da una serie di valori di dati indicizzati per data e ora.</span><span class="sxs-lookup"><span data-stu-id="998b3-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="998b3-432">Gli oggetti serie temporale vengono usati in R per creare e gestire l'indice temporale.</span><span class="sxs-lookup"><span data-stu-id="998b3-432">R time series objects are used to create and manage the time index.</span></span> <span data-ttu-id="998b3-433">Questi oggetti offrono infatti una serie di vantaggi.</span><span class="sxs-lookup"><span data-stu-id="998b3-433">There are several advantages to using time series objects.</span></span> <span data-ttu-id="998b3-434">Gli oggetti della serie temporale consentono di liberarsi delle numerose attività di gestione dei valori di indice della serie temporale incapsulati nell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="998b3-434">Time series objects free you from the many details of managing the time series index values that are encapsulated in the object.</span></span> <span data-ttu-id="998b3-435">Consentono inoltre di usare i vari metodi messi a disposizione dalle serie temporali per operazioni di tracciamento, stampa, modeling, ecc.</span><span class="sxs-lookup"><span data-stu-id="998b3-435">In addition, time series objects allow you to use the many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="998b3-436">In genere viene usata la classe di serie temporale POSIXct poiché è relativamente semplice</span><span class="sxs-lookup"><span data-stu-id="998b3-436">The POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="998b3-437">e permette di misurare il tempo a partire dal 1° gennaio 1970.</span><span class="sxs-lookup"><span data-stu-id="998b3-437">This time series class measures time from the start of the epoch, January 1, 1970.</span></span> <span data-ttu-id="998b3-438">In questo esempio useremo quindi oggetti serie temporale di tipo POSIXct.</span><span class="sxs-lookup"><span data-stu-id="998b3-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="998b3-439">Altre classi di oggetti serie temporale comunemente usate in R includono zoo e xts, serie temporali estensibili.</span><span class="sxs-lookup"><span data-stu-id="998b3-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in the references in Section 5.7. [commenting because this section doesn't exist, even in the original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="998b3-440">Esempio di oggetto della serie temporale</span><span class="sxs-lookup"><span data-stu-id="998b3-440">Time series object example</span></span>
<span data-ttu-id="998b3-441">Iniziamo con il nostro esempio.</span><span class="sxs-lookup"><span data-stu-id="998b3-441">Let's get started with our example.</span></span> <span data-ttu-id="998b3-442">Trascinare un **nuovo** modulo [Execute R Script][execute-r-script] nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="998b3-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="998b3-443">Connettere la porta di output Result Dataset1 del modulo [Execute R Script][execute-r-script] esistente alla porta di input Dataset1 del nuovo modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-443">Connect the Result Dataset1 output port of the existing [Execute R Script][execute-r-script] module to the Dataset1 input port of the new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="998b3-444">Come nei primi esempi, man mano che si va avanti, in determinati punti verranno mostrate solo le righe aggiuntive incrementali del codice R per ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="998b3-444">As I did for the first examples, as we progress through the example, at some points I will show only the incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-the-dataframe"></a><span data-ttu-id="998b3-445">Lettura del frame di dati</span><span class="sxs-lookup"><span data-stu-id="998b3-445">Reading the dataframe</span></span>
<span data-ttu-id="998b3-446">Come prima operazione, eseguiamo la lettura in un frame di dati e accertiamoci di ottenere i risultati previsti.</span><span class="sxs-lookup"><span data-stu-id="998b3-446">As a first step, let's read in a dataframe and make sure we get the expected results.</span></span> <span data-ttu-id="998b3-447">A questo scopo, usare il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="998b3-447">The following code should do the job.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check the results

<span data-ttu-id="998b3-448">Eseguiamo ora l'esperimento.</span><span class="sxs-lookup"><span data-stu-id="998b3-448">Now, run the experiment.</span></span> <span data-ttu-id="998b3-449">Il log della nuova forma Execute R Script dovrebbe essere simile a quello riportato nella Figura 14.</span><span class="sxs-lookup"><span data-stu-id="998b3-449">The log of the new Execute R Script shape should look like Figure 14.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

<span data-ttu-id="998b3-450">*Figura 14. Riepilogo del frame di dati nel modulo Execute R Script.*</span><span class="sxs-lookup"><span data-stu-id="998b3-450">*Figure 14. Summary of the dataframe in the Execute R Script module.*</span></span>

<span data-ttu-id="998b3-451">I dati sono dei tipi e nel formato previsti.</span><span class="sxs-lookup"><span data-stu-id="998b3-451">This data is of the expected types and format.</span></span> <span data-ttu-id="998b3-452">Osservare come la colonna "Month" sia di tipo fattore e contenga il numero di livelli previsto.</span><span class="sxs-lookup"><span data-stu-id="998b3-452">Note that the 'Month' column is of type factor and has the expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="998b3-453">Creazione di un oggetto della serie temporale</span><span class="sxs-lookup"><span data-stu-id="998b3-453">Creating a time series object</span></span>
<span data-ttu-id="998b3-454">È necessario aggiungere un oggetto serie temporale al nostro frame di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-454">We need to add a time series object to our dataframe.</span></span> <span data-ttu-id="998b3-455">Sostituire il codice corrente con il seguente, che aggiunge una nuova colonna della classe POSIXct.</span><span class="sxs-lookup"><span data-stu-id="998b3-455">Replace the current code with the following, which adds a new column of class POSIXct.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check the results

<span data-ttu-id="998b3-456">A questo punto, controllare il log.</span><span class="sxs-lookup"><span data-stu-id="998b3-456">Now, check the log.</span></span> <span data-ttu-id="998b3-457">Dovrebbe essere simile a quello riportato nella Figura 15.</span><span class="sxs-lookup"><span data-stu-id="998b3-457">It should look like Figure 15.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="998b3-458">*Figura 15. Riepilogo del frame di dati con un oggetto della serie temporale.*</span><span class="sxs-lookup"><span data-stu-id="998b3-458">*Figure 15. Summary of the dataframe with a time series object.*</span></span>

<span data-ttu-id="998b3-459">Dal riepilogo è possibile notare come la nuova colonna sia effettivamente di classe POSIXct.</span><span class="sxs-lookup"><span data-stu-id="998b3-459">We can see from the summary that the new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-the-data"></a><span data-ttu-id="998b3-460">Esplorazione e trasformazione dei dati</span><span class="sxs-lookup"><span data-stu-id="998b3-460">Exploring and transforming the data</span></span>
<span data-ttu-id="998b3-461">In questa sezione vengono descritte alcune delle variabili in questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-461">Let's explore some of the variables in this dataset.</span></span> <span data-ttu-id="998b3-462">A questo scopo ci avvarremo di una matrice di grafici a dispersione.</span><span class="sxs-lookup"><span data-stu-id="998b3-462">A scatterplot matrix is a good way to produce a quick look.</span></span> <span data-ttu-id="998b3-463">La funzione `str()` nel codice R precedente viene sostituita con la riga seguente.</span><span class="sxs-lookup"><span data-stu-id="998b3-463">I am replacing the `str()` function in the previous R code with the following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="998b3-464">Eseguiamo il codice e vediamo cosa succede.</span><span class="sxs-lookup"><span data-stu-id="998b3-464">Run this code and see what happens.</span></span> <span data-ttu-id="998b3-465">Il grafico generato per la porta R Device dovrebbe essere simile a quello riportato nella Figura 16.</span><span class="sxs-lookup"><span data-stu-id="998b3-465">The plot produced at the R Device port should look like Figure 16.</span></span>

![Matrice del grafico a dispersione delle variabili selezionate][17]

<span data-ttu-id="998b3-467">*Figura 16. Matrice del grafico a dispersione delle variabili selezionate.*</span><span class="sxs-lookup"><span data-stu-id="998b3-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="998b3-468">È presente una struttura insolita nelle relazioni tra queste variabili.</span><span class="sxs-lookup"><span data-stu-id="998b3-468">There is some odd-looking structure in the relationships between these variables.</span></span> <span data-ttu-id="998b3-469">Questo può essere dovuto ad alcune tendenze nei dati o al fatto che le variabili non sono state standardizzate.</span><span class="sxs-lookup"><span data-stu-id="998b3-469">Perhaps this arises from trends in the data and from the fact that we have not standardized the variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="998b3-470">Analisi delle correlazioni</span><span class="sxs-lookup"><span data-stu-id="998b3-470">Correlation analysis</span></span>
<span data-ttu-id="998b3-471">Per eseguire un'analisi di correlazione è necessario detrendizzare le variabili e standardizzarle.</span><span class="sxs-lookup"><span data-stu-id="998b3-471">To perform correlation analysis we need to both de-trend and standardize the variables.</span></span> <span data-ttu-id="998b3-472">È possibile usare semplicemente la funzione `scale()` di R, che centra e scala le variabili</span><span class="sxs-lookup"><span data-stu-id="998b3-472">We could simply use the R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="998b3-473">e può essere eseguita più velocemente.</span><span class="sxs-lookup"><span data-stu-id="998b3-473">This function might well run faster.</span></span> <span data-ttu-id="998b3-474">In questo caso, tuttavia, preferisco mostrare un esempio di programmazione difensiva in R.</span><span class="sxs-lookup"><span data-stu-id="998b3-474">However, I want to show you an example of defensive programing in R.</span></span>

<span data-ttu-id="998b3-475">La funzione `ts.detrend()` mostrata di seguito esegue entrambe le operazioni.</span><span class="sxs-lookup"><span data-stu-id="998b3-475">The `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="998b3-476">Le due seguenti righe di codice consentono di detrendizzare i dati e standardizzare i valori.</span><span class="sxs-lookup"><span data-stu-id="998b3-476">The following two lines of code de-trend the data and then standardize the values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function to de-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time to have the same length',
                    'ERROR: ts.detrend requires argument ts to be of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros to return as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # The input arguments are not of the same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If the ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If the ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that the Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend the time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply the detrend.ts function to the variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot the results to look at the relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="998b3-477">La funzione `ts.detrend()` espleta quindi numerose operazioni.</span><span class="sxs-lookup"><span data-stu-id="998b3-477">There is quite a bit happening in the `ts.detrend()` function.</span></span> <span data-ttu-id="998b3-478">Gran parte del codice è progettato per controllare la presenza di potenziali problemi con gli argomenti o per gestire le eccezioni, che possono sempre verificarsi durante i calcoli.</span><span class="sxs-lookup"><span data-stu-id="998b3-478">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="998b3-479">Solo poche righe del codice, quindi, eseguono effettivamente i calcoli.</span><span class="sxs-lookup"><span data-stu-id="998b3-479">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="998b3-480">Un esempio di programmazione difensiva è già stato illustrato in [Trasformazioni di valori](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="998b3-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="998b3-481">Entrambi i blocchi di calcolo vengono inclusi in `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="998b3-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="998b3-482">Per alcuni errori è opportuno restituire il vettore di input originale, per altri è preferibile un vettore di zeri.</span><span class="sxs-lookup"><span data-stu-id="998b3-482">For some errors it makes sense to return the original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="998b3-483">Osservare come la regressione lineare usata per il detrending sia una regressione in serie temporale</span><span class="sxs-lookup"><span data-stu-id="998b3-483">Note that the linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="998b3-484">e la variabile indipendente un oggetto serie temporale.</span><span class="sxs-lookup"><span data-stu-id="998b3-484">The predictor variable is a time series object.</span></span>  

<span data-ttu-id="998b3-485">Una volta definito `ts.detrend()` , viene applicato alle variabili di interesse nel frame di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-485">Once `ts.detrend()` is defined we apply it to the variables of interest in our dataframe.</span></span> <span data-ttu-id="998b3-486">È necessario forzare l'elenco risultante creato da `lapply()` nel frame di dati usando `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="998b3-486">We must coerce the resulting list created by `lapply()` to data dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="998b3-487">A causa degli aspetti difensivi di `ts.detrend()`, la mancata elaborazione di una delle variabili non impedisce la corretto elaborazione delle altre.</span><span class="sxs-lookup"><span data-stu-id="998b3-487">Because of defensive aspects of `ts.detrend()`, failure to process one of the variables will not prevent correct processing of the others.</span></span>  

<span data-ttu-id="998b3-488">La riga di codice finale crea un grafico a dispersione pairwise.</span><span class="sxs-lookup"><span data-stu-id="998b3-488">The final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="998b3-489">Dopo aver eseguito il codice R, i risultati del grafico a dispersione vengono mostrati nella Figura 17.</span><span class="sxs-lookup"><span data-stu-id="998b3-489">After running the R code, the results of the scatterplot are shown in Figure 17.</span></span>

![Grafico a dispersione pairwise della serie temporale detrendizzata e standardizzata][18]

<span data-ttu-id="998b3-491">*Figura 17. Grafico a dispersione pairwise della serie temporale detrendizzata e standardizzata.*</span><span class="sxs-lookup"><span data-stu-id="998b3-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="998b3-492">È possibile confrontare questi risultati con quelli mostrati nella figura 16.</span><span class="sxs-lookup"><span data-stu-id="998b3-492">You can compare these results to those shown in Figure 16.</span></span> <span data-ttu-id="998b3-493">Dopo aver eseguito il detrending e standardizzato le variabili, la struttura che rappresenta le relazioni tra le variabili è notevolmente semplificata.</span><span class="sxs-lookup"><span data-stu-id="998b3-493">With the trend removed and the variables standardized, we see a lot less structure in the relationships between these variables.</span></span>

<span data-ttu-id="998b3-494">Il codice per calcolare le correlazioni come oggetti CCF di R è il seguente.</span><span class="sxs-lookup"><span data-stu-id="998b3-494">The code to compute the correlations as R ccf objects is as follows.</span></span>

    ## A function to compute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of the pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute the list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="998b3-495">L'esecuzione di questo codice produce il log mostrato nella Figura 18.</span><span class="sxs-lookup"><span data-stu-id="998b3-495">Running this code produces the log shown in Figure 18.</span></span>

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

<span data-ttu-id="998b3-496">*Figura 18. Elenco di oggetti CCF dall'analisi delle correlazioni pairwise.*</span><span class="sxs-lookup"><span data-stu-id="998b3-496">*Figure 18. List of ccf objects from the pairwise correlation analysis.*</span></span>

<span data-ttu-id="998b3-497">Per ogni intervallo è presente un valore di correlazione.</span><span class="sxs-lookup"><span data-stu-id="998b3-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="998b3-498">Nessuno di essi, tuttavia, è abbastanza grande da essere significativo.</span><span class="sxs-lookup"><span data-stu-id="998b3-498">None of these correlation values is large enough to be significant.</span></span> <span data-ttu-id="998b3-499">Possiamo quindi concludere che ciascuna variabile può essere modellata in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="998b3-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="998b3-500">Output di un frame di dati</span><span class="sxs-lookup"><span data-stu-id="998b3-500">Output a dataframe</span></span>
<span data-ttu-id="998b3-501">Abbiamo elaborato le correlazioni pairwise come elenco di oggetti R ccf.</span><span class="sxs-lookup"><span data-stu-id="998b3-501">We have computed the pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="998b3-502">Questo determina tuttavia un piccolo problema poiché la porta di output Result Dataset richiede inevitabilmente un frame di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-502">This presents a bit of a problem as the Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="998b3-503">Inoltre, l'oggetto CCF stesso è un elenco e sono richiesti solo i valori nel primo elemento di questo elenco, le correlazioni nei vari intervalli.</span><span class="sxs-lookup"><span data-stu-id="998b3-503">Further, the ccf object is itself a list and we want only the values in the first element of this list, the correlations at the various lags.</span></span>

<span data-ttu-id="998b3-504">Il codice seguente estrae i valori di intervallo dall'elenco di oggetti CCF, che sono essi stessi degli elenchi.</span><span class="sxs-lookup"><span data-stu-id="998b3-504">The following code extracts the lag values from the list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with the row names column and the
    ## correlation data frame and assign the column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## The following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="998b3-505">La prima riga di codice è un po' complessa da comprendere, quindi viene spiegata qui di seguito.</span><span class="sxs-lookup"><span data-stu-id="998b3-505">The first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="998b3-506">Dall'interno verso l'esterno incontriamo:</span><span class="sxs-lookup"><span data-stu-id="998b3-506">Working from the inside out we have the following:</span></span>

1. <span data-ttu-id="998b3-507">L'operatore '**[[**' con l'argomento '**1**' seleziona il vettore delle correlazioni negli intervalli dal primo elemento dell'elenco di oggetti CCF.</span><span class="sxs-lookup"><span data-stu-id="998b3-507">The '**[[**' operator with the argument '**1**' selects the vector of correlations at the lags from the first element of the ccf object list.</span></span>
2. <span data-ttu-id="998b3-508">La funzione `do.call()` applica la funzione `rbind()` agli elementi dell'elenco restituito da `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="998b3-508">The `do.call()` function applies the `rbind()` function over the elements of the list returns by `lapply()`.</span></span>
3. <span data-ttu-id="998b3-509">La funzione `data.frame()` forza il risultato prodotto da `do.call()` in un frame di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-509">The `data.frame()` function coerces the result produced by `do.call()` to a dataframe.</span></span>

<span data-ttu-id="998b3-510">I nomi di riga sono in una colonna del frame di dati.</span><span class="sxs-lookup"><span data-stu-id="998b3-510">Note that the row names are in a column of the dataframe.</span></span> <span data-ttu-id="998b3-511">In questo modo, vengono preservati durante l'output dal modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="998b3-511">Doing so preserves the row names when they are output from the [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="998b3-512">L'esecuzione del codice produce l'output mostrato nella Figura 19 quando si **visualizza** l'output nella porta Result Dataset.</span><span class="sxs-lookup"><span data-stu-id="998b3-512">Running the code produces the output shown in Figure 19 when I **Visualize** the output at the Result Dataset port.</span></span> <span data-ttu-id="998b3-513">I nomi di riga sono nella prima colonna, come previsto.</span><span class="sxs-lookup"><span data-stu-id="998b3-513">The row names are in the first column, as intended.</span></span>

![Output dei risultati dall'analisi delle correlazioni][20]

<span data-ttu-id="998b3-515">*Figura 19. Output dei risultati dall'analisi delle correlazioni.*</span><span class="sxs-lookup"><span data-stu-id="998b3-515">*Figure 19. Results output from the correlation analysis.*</span></span>

## <span data-ttu-id="998b3-516"><a id="seasonalforecasting"></a>Esempio di serie temporale: previsione stagionale</span><span class="sxs-lookup"><span data-stu-id="998b3-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="998b3-517">Ora i dati sono in un formato adatto all'analisi ed è stato stabilito che non sono presenti correlazioni significative tra le variabili.</span><span class="sxs-lookup"><span data-stu-id="998b3-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between the variables.</span></span> <span data-ttu-id="998b3-518">Passiamo quindi alla creazione di un modello di previsione in serie temporale,</span><span class="sxs-lookup"><span data-stu-id="998b3-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="998b3-519">che ci permetterà di prevedere la produzione di latte in California nei 12 mesi del 2013.</span><span class="sxs-lookup"><span data-stu-id="998b3-519">Using this model we will forecast California milk production for the 12 months of 2013.</span></span>

<span data-ttu-id="998b3-520">Il nostro modello previsionale sarà costituito da due componenti: trend e stagionale.</span><span class="sxs-lookup"><span data-stu-id="998b3-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="998b3-521">La previsione completa è data dal prodotto di queste due componenti.</span><span class="sxs-lookup"><span data-stu-id="998b3-521">The complete forecast is the product of these two components.</span></span> <span data-ttu-id="998b3-522">Questo tipo di modello prende il nome di modello moltiplicativo,</span><span class="sxs-lookup"><span data-stu-id="998b3-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="998b3-523">alternativo al modello additivo.</span><span class="sxs-lookup"><span data-stu-id="998b3-523">The alternative is an additive model.</span></span> <span data-ttu-id="998b3-524">Una trasformazione logaritmica è stata già applicata alle variabili di interesse, quindi l'analisi diventa più gestibile.</span><span class="sxs-lookup"><span data-stu-id="998b3-524">We have already applied a log transformation to the variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="998b3-525">Il codice R completo per questa sezione è disponibile nel file con estensione zip scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="998b3-525">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="creating-the-dataframe-for-analysis"></a><span data-ttu-id="998b3-526">Creazione del frame di dati per l'analisi</span><span class="sxs-lookup"><span data-stu-id="998b3-526">Creating the dataframe for analysis</span></span>
<span data-ttu-id="998b3-527">Per iniziare, aggiungere un **nuovo** modulo [Execute R Script][execute-r-script] all'esperimento.</span><span class="sxs-lookup"><span data-stu-id="998b3-527">Start by adding a **new** [Execute R Script][execute-r-script] module to your experiment.</span></span> <span data-ttu-id="998b3-528">Connettere l'output **Result Dataset** del modulo [Execute R Script][execute-r-script] all'input **Dataset1** del nuovo modulo.</span><span class="sxs-lookup"><span data-stu-id="998b3-528">Connect the **Result Dataset** output of the existing [Execute R Script][execute-r-script] module to the **Dataset1** input of the new module.</span></span> <span data-ttu-id="998b3-529">Il risultato dovrebbe essere simile al contenuto della Figura 20.</span><span class="sxs-lookup"><span data-stu-id="998b3-529">The result should look something like Figure 20.</span></span>

![Esperimento con l'aggiunta del nuovo modulo Execute R Script][21]

<span data-ttu-id="998b3-531">*Figura 20. Esperimento con l'aggiunta del nuovo modulo Execute R Script.*</span><span class="sxs-lookup"><span data-stu-id="998b3-531">*Figure 20. The experiment with the new Execute R Script module added.*</span></span>

<span data-ttu-id="998b3-532">Come per l'analisi di correlazione appena completata, dobbiamo aggiungere una colonna con oggetto serie temporale POSIXct.</span><span class="sxs-lookup"><span data-stu-id="998b3-532">As with the correlation analysis we just completed, we need to add a column with a POSIXct time series object.</span></span> <span data-ttu-id="998b3-533">A questo scopo, usare il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="998b3-533">The following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment the first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="998b3-534">Eseguire il codice ed esaminare il log.</span><span class="sxs-lookup"><span data-stu-id="998b3-534">Run this code and look at the log.</span></span> <span data-ttu-id="998b3-535">Il risultato dovrebbe essere simile alla Figura 21.</span><span class="sxs-lookup"><span data-stu-id="998b3-535">The result should look like Figure 21.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="998b3-536">*Figura 21. Riepilogo del frame di dati.*</span><span class="sxs-lookup"><span data-stu-id="998b3-536">*Figure 21. A summary of the dataframe.*</span></span>

<span data-ttu-id="998b3-537">Con questo risultato siamo pronti per avviare l'analisi.</span><span class="sxs-lookup"><span data-stu-id="998b3-537">With this result, we are ready to start our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="998b3-538">Creare un set di dati di training</span><span class="sxs-lookup"><span data-stu-id="998b3-538">Create a training dataset</span></span>
<span data-ttu-id="998b3-539">Con il frame di dati costruito dobbiamo creare un set di dati di addestramento,</span><span class="sxs-lookup"><span data-stu-id="998b3-539">With the dataframe constructed we need to create a training dataset.</span></span> <span data-ttu-id="998b3-540">che comprenderà tutte le osservazioni, ad eccezione delle ultime 12, relative al 2013, che corrispondono al nostro set di dati di test.</span><span class="sxs-lookup"><span data-stu-id="998b3-540">This data will include all of the observations except the last 12, of the year 2013, which is our test dataset.</span></span> <span data-ttu-id="998b3-541">Il codice seguente suddivide il frame di dati in sottoinsiemi e crea grafici della produzione casearia e delle variabili di prezzo.</span><span class="sxs-lookup"><span data-stu-id="998b3-541">The following code subsets the dataframe and creates plots of the dairy production and price variables.</span></span> <span data-ttu-id="998b3-542">Creerò quindi dei grafici per le quattro variabili di produzione e di prezzo.</span><span class="sxs-lookup"><span data-stu-id="998b3-542">I then create plots of the four production and price variables.</span></span> <span data-ttu-id="998b3-543">Una funzione anonima viene usata per definire alcuni argomenti per il tracciato e quindi eseguire l'iterazione nell'elenco degli altri due argomenti con `Map()`.</span><span class="sxs-lookup"><span data-stu-id="998b3-543">An anonymous function is used to define some augments for plot, and then iterate over the list of the other two arguments with `Map()`.</span></span> <span data-ttu-id="998b3-544">Se pensate che un ciclo For sarebbe stato appropriato, avete ragione.</span><span class="sxs-lookup"><span data-stu-id="998b3-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="998b3-545">Tuttavia, poiché R è un linguaggio funzionale, adotterò un approccio funzionale.</span><span class="sxs-lookup"><span data-stu-id="998b3-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="998b3-546">L'esecuzione di questo codice produce la serie di grafici in serie temporale ottenuto dall'output R Device mostrato nella Figura 22.</span><span class="sxs-lookup"><span data-stu-id="998b3-546">Running the code produces the series of time series plots from the R Device output shown in Figure 22.</span></span> <span data-ttu-id="998b3-547">Notare che l'asse temporale è espresso in unità di date, uno dei vantaggi offerti dal metodo del grafico in serie temporale.</span><span class="sxs-lookup"><span data-stu-id="998b3-547">Note that the time axis is in units of dates, a nice benefit of the time series plot method.</span></span>

![Primo tracciato della serie temporale della produzione casearia in California e dei dati sui prezzi](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Secondo tracciato della serie temporale della produzione casearia in California e dei dati sui prezzi](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Terzo tracciato della serie temporale della produzione casearia in California e dei dati sui prezzi](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Quarto tracciato della serie temporale della produzione casearia in California e dei dati sui prezzi](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="998b3-552">*Figura 22. Tracciati della serie temporale della produzione casearia in California e dei dati sui prezzi.*</span><span class="sxs-lookup"><span data-stu-id="998b3-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="998b3-553">Modello di tendenza</span><span class="sxs-lookup"><span data-stu-id="998b3-553">A trend model</span></span>
<span data-ttu-id="998b3-554">Dopo aver creato un oggetto serie temporale e aver esaminato i dati, iniziamo a costruire un modello di trend per i dati di produzione di latte in California.</span><span class="sxs-lookup"><span data-stu-id="998b3-554">Having created a time series object and having had a look at the data, let's start to construct a trend model for the California milk production data.</span></span> <span data-ttu-id="998b3-555">A questo scopo, usiamo una regressione in serie temporale.</span><span class="sxs-lookup"><span data-stu-id="998b3-555">We can do this with a time series regression.</span></span> <span data-ttu-id="998b3-556">Tuttavia, è chiaro dal tracciato che è necessario più di una pendenza e di un intercetta per modellare in modo accurato la tendenza osservata nei dati di training.</span><span class="sxs-lookup"><span data-stu-id="998b3-556">However, it is clear from the plot that we will need more than a slope and intercept to accurately model the observed trend in the training data.</span></span>

<span data-ttu-id="998b3-557">Considerata la scala ridotta dei dati, il modello per la tendenza verrà compilato in RStudio, quindi il modello risultante verrà tagliato e incollato in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="998b3-557">Given the small scale of the data, I will build the model for trend in RStudio and then cut and paste the resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="998b3-558">RStudio fornisce infatti un ambiente interattivo adatto a questo tipo di analisi interattiva.</span><span class="sxs-lookup"><span data-stu-id="998b3-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="998b3-559">Come primo tentativo, eseguirò una regressione polinomiale con valori di potenza fino a 3.</span><span class="sxs-lookup"><span data-stu-id="998b3-559">As a first attempt, I will try a polynomial regression with powers up to 3.</span></span> <span data-ttu-id="998b3-560">Esiste un pericolo reale di overfitting per questi tipi di modelli.</span><span class="sxs-lookup"><span data-stu-id="998b3-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="998b3-561">È opportuno quindi evitare termini di ordine superiore.</span><span class="sxs-lookup"><span data-stu-id="998b3-561">Therefore, it is best to avoid high order terms.</span></span> <span data-ttu-id="998b3-562">La funzione `I()` inibisce l'interpretazione dei contenuti (interpreta i contenuti così come sono) e consente di scrivere una funzione con interpretazione letterale in un'equazione di regressione.</span><span class="sxs-lookup"><span data-stu-id="998b3-562">The `I()` function inhibits interpretation of the contents (interprets the contents 'as is') and allows you to write a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="998b3-563">Viene generato quanto segue.</span><span class="sxs-lookup"><span data-stu-id="998b3-563">This generates the following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

<span data-ttu-id="998b3-564">Dai valori P (Pr(>|t|)) presenti in questo output possiamo osservare come il termine al quadrato possa non essere significativo.</span><span class="sxs-lookup"><span data-stu-id="998b3-564">From P values (Pr(>|t|)) in this output, we can see that the squared term may not be significant.</span></span> <span data-ttu-id="998b3-565">Verrà usata la funzione `update()` per modificare il modello eliminando il termine al quadrato.</span><span class="sxs-lookup"><span data-stu-id="998b3-565">I will use the `update()` function to modify this model by dropping the squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="998b3-566">Viene generato quanto segue.</span><span class="sxs-lookup"><span data-stu-id="998b3-566">This generates the following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

<span data-ttu-id="998b3-567">L'aspetto è decisamente migliore adesso.</span><span class="sxs-lookup"><span data-stu-id="998b3-567">This looks better.</span></span> <span data-ttu-id="998b3-568">Tutti i termini sono significativi.</span><span class="sxs-lookup"><span data-stu-id="998b3-568">All of the terms are significant.</span></span> <span data-ttu-id="998b3-569">Il valore 2e-16, tuttavia, è un valore predefinito e non dovrebbe essere preso troppo sul serio</span><span class="sxs-lookup"><span data-stu-id="998b3-569">However, the 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="998b3-570">Come test di integrità, effettueremo un grafico in serie temporale dei dati della produzione casearia in California con la curva di trend mostrata di seguito.</span><span class="sxs-lookup"><span data-stu-id="998b3-570">As a sanity test, let's make a time series plot of the California dairy production data with the trend curve shown.</span></span> <span data-ttu-id="998b3-571">È stato aggiunto il codice seguente nel modello [Execute R Script][execute-r-script] di Azure Machine Learning (non in RStudio) per creare il modello ed eseguire un tracciato.</span><span class="sxs-lookup"><span data-stu-id="998b3-571">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) to create the model and make a plot.</span></span> <span data-ttu-id="998b3-572">Il risultato viene mostrato nella Figura 23.</span><span class="sxs-lookup"><span data-stu-id="998b3-572">The result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Dati sulla produzione di latte in California con il modello di tendenza visualizzato](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="998b3-574">*Figura 23. Dati sulla produzione di latte in California con il modello di tendenza visualizzato.*</span><span class="sxs-lookup"><span data-stu-id="998b3-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="998b3-575">Sembra che il modello di trend si adatti perfettamente.</span><span class="sxs-lookup"><span data-stu-id="998b3-575">It looks like the trend model fits the data fairly well.</span></span> <span data-ttu-id="998b3-576">Inoltre, non sembra che ci siano tracce di overfitting, ad esempio strani ondulamenti nella curva del modello.</span><span class="sxs-lookup"><span data-stu-id="998b3-576">Further, there does not seem to be evidence of over-fitting, such as odd wiggles in the model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="998b3-577">Modello con stagionalità</span><span class="sxs-lookup"><span data-stu-id="998b3-577">Seasonal model</span></span>
<span data-ttu-id="998b3-578">Con un modello di tendenza disponibile, è necessario proseguire includendo gli effetti stagionali.</span><span class="sxs-lookup"><span data-stu-id="998b3-578">With a trend model in hand, we need to push on and include the seasonal effects.</span></span> <span data-ttu-id="998b3-579">Verrà usato il mese dell'anno come variabile fittizia nel modello lineare per acquisire l'effetto mese per mese.</span><span class="sxs-lookup"><span data-stu-id="998b3-579">We will use the month of the year as a dummy variable in the linear model to capture the month-by-month effect.</span></span> <span data-ttu-id="998b3-580">Tenere presente che, quando si introducono variabili di fattore in un modello, l'intercetta non deve essere elaborata.</span><span class="sxs-lookup"><span data-stu-id="998b3-580">Note that when you introduce factor variables into a model, the intercept must not be computed.</span></span> <span data-ttu-id="998b3-581">In caso contrario, la formula risulta eccessivamente specificata ed R eliminerà i fattori desiderati, lasciando invece il termine dell'intercetta.</span><span class="sxs-lookup"><span data-stu-id="998b3-581">If you do not do this, the formula is over-specified and R will drop one of the desired factors but keep the intercept term.</span></span>

<span data-ttu-id="998b3-582">Poiché il modello di tendenza è soddisfacente, è possibile usare la funzione `update()` per aggiungere i nuovi termini al modello esistente.</span><span class="sxs-lookup"><span data-stu-id="998b3-582">Since we have a satisfactory trend model we can use the `update()` function to add the new terms to the existing model.</span></span> <span data-ttu-id="998b3-583">Nella formula di aggiornamento, il valore -1 elimina il termine dell'intercetta.</span><span class="sxs-lookup"><span data-stu-id="998b3-583">The -1 in the update formula drops the intercept term.</span></span> <span data-ttu-id="998b3-584">Continuiamo ora in RStudio.</span><span class="sxs-lookup"><span data-stu-id="998b3-584">Continuing in RStudio for the moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="998b3-585">Viene generato quanto segue.</span><span class="sxs-lookup"><span data-stu-id="998b3-585">This generates the following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

<span data-ttu-id="998b3-586">Vediamo come nel modello non sia più presente un termine dell'intercetta ma siano inclusi 12 fattori mese,</span><span class="sxs-lookup"><span data-stu-id="998b3-586">We see that the model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="998b3-587">proprio come ci aspettavamo.</span><span class="sxs-lookup"><span data-stu-id="998b3-587">This is exactly what we wanted to see.</span></span>

<span data-ttu-id="998b3-588">Creiamo adesso un altro grafico in serie temporale dei dati di produzione casearia in California per verificare l'effettivo funzionamento del modello con stagionalità.</span><span class="sxs-lookup"><span data-stu-id="998b3-588">Let's make another time series plot of the California dairy production data to see how well the seasonal model is working.</span></span> <span data-ttu-id="998b3-589">È stato aggiunto il codice seguente nel modello [Execute R Script][execute-r-script] di Azure Machine Learning per creare il modello ed eseguire un tracciato.</span><span class="sxs-lookup"><span data-stu-id="998b3-589">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] to create the model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="998b3-590">L'esecuzione di questo codice in Azure Machine Learning produce il tracciato mostrato nella Figura 24.</span><span class="sxs-lookup"><span data-stu-id="998b3-590">Running this code in Azure Machine Learning produces the plot shown in Figure 24.</span></span>

![Produzione di latte in California con un modello che include gli effetti stagionali](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="998b3-592">*Figura 24. Produzione di latte in California con un modello che include gli effetti stagionali.*</span><span class="sxs-lookup"><span data-stu-id="998b3-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="998b3-593">La corrispondenza con i dati mostrati nella Figura 24 è piuttosto incoraggiante.</span><span class="sxs-lookup"><span data-stu-id="998b3-593">The fit to the data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="998b3-594">Sia il trend sia l'effetto stagionale (variazione mensile) sembrano ragionevoli.</span><span class="sxs-lookup"><span data-stu-id="998b3-594">Both the trend and the seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="998b3-595">Come ulteriore verifica sul mostro modello, esaminiamo i valori residui.</span><span class="sxs-lookup"><span data-stu-id="998b3-595">As another check on our model, let's have a look at the residuals.</span></span> <span data-ttu-id="998b3-596">Il codice seguente calcola i valori previsti da due modelli, calcola i valori residui per il modello stagionale e infine esegue il traccia di tali valori per i dati di training.</span><span class="sxs-lookup"><span data-stu-id="998b3-596">The following code computes the predicted values from our two models, computes the residuals for the seasonal model, and then plots these residuals for the training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot the residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="998b3-597">Il grafico dei residui è illustrato nella Figura 25.</span><span class="sxs-lookup"><span data-stu-id="998b3-597">The residual plot is shown in Figure 25.</span></span>

![Valori residui del modello stagionale per i dati di training](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="998b3-599">*Figura 25. Valori residui del modello stagionale per i dati di training.*</span><span class="sxs-lookup"><span data-stu-id="998b3-599">*Figure 25. Residuals of the seasonal model for the training data.*</span></span>

<span data-ttu-id="998b3-600">Questi valori residui sembrano ragionevoli.</span><span class="sxs-lookup"><span data-stu-id="998b3-600">These residuals look reasonable.</span></span> <span data-ttu-id="998b3-601">Non risalta alcuna struttura particolare, ad eccezione dell'effetto della recessione del biennio 2008-2009, che il nostro modello non riesce a rappresentare particolarmente bene.</span><span class="sxs-lookup"><span data-stu-id="998b3-601">There is no particular structure, except the effect of the 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="998b3-602">Il tracciato mostrato nella Figura 25 è utile per rilevare i modelli dipendenti dal tempo nei valori residui.</span><span class="sxs-lookup"><span data-stu-id="998b3-602">The plot shown in Figure 25 is useful for detecting any time-dependent patterns in the residuals.</span></span> <span data-ttu-id="998b3-603">L'approccio esplicito di elaborare e tracciare graficamente i valori residui consente di metterli in ordine temporale nel grafico.</span><span class="sxs-lookup"><span data-stu-id="998b3-603">The explicit approach of computing and plotting the residuals I used places the residuals in time order on the plot.</span></span> <span data-ttu-id="998b3-604">D'altra parte, se fosse stato eseguito il tracciato di `milk.lm$residuals`, questo tracciato non sarebbe stato in ordine temporale.</span><span class="sxs-lookup"><span data-stu-id="998b3-604">If, on the other hand, I had plotted `milk.lm$residuals`, the plot would not have been in time order.</span></span>

<span data-ttu-id="998b3-605">È anche possibile usare `plot.lm()` per produrre una serie di tracciati diagnostici.</span><span class="sxs-lookup"><span data-stu-id="998b3-605">You can also use `plot.lm()` to produce a series of diagnostic plots.</span></span>

    ## Show the diagnostic plots for the model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="998b3-606">Questo codice produce una serie di tracciati diagnostici mostrati nella Figura 26.</span><span class="sxs-lookup"><span data-stu-id="998b3-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![Primo tracciato diagnostico per il modello stagionale](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Secondo tracciato diagnostico per il modello stagionale](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Terzo tracciato diagnostico per il modello stagionale](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Quarto tracciato diagnostico per il modello stagionale](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="998b3-611">*Figura 26. Tracciati diagnostici per il modello stagionale.*</span><span class="sxs-lookup"><span data-stu-id="998b3-611">*Figure 26. Diagnostic plots for the seasonal model.*</span></span>

<span data-ttu-id="998b3-612">In questi grafici sono presenti alcuni punti di alta influenza, ma niente di particolarmente preoccupante.</span><span class="sxs-lookup"><span data-stu-id="998b3-612">There are a few highly influential points identified in these plots, but nothing to cause great concern.</span></span> <span data-ttu-id="998b3-613">Nel grafico Normal Q-Q, inoltre, possiamo vedere come i valori residuali siano distribuiti in modo pressoché normale, presupposto importante per i modelli lineari.</span><span class="sxs-lookup"><span data-stu-id="998b3-613">Further, we can see from the Normal Q-Q plot that the residuals are close to normally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="998b3-614">Previsione e valutazione del modello</span><span class="sxs-lookup"><span data-stu-id="998b3-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="998b3-615">È rimasta un'ultima cosa da fare per poter completare il nostro esempio:</span><span class="sxs-lookup"><span data-stu-id="998b3-615">There is just one more thing to do to complete our example.</span></span> <span data-ttu-id="998b3-616">elaborare le previsioni e valutare il grado di errore rispetto ai dati effettivi.</span><span class="sxs-lookup"><span data-stu-id="998b3-616">We need to compute forecasts and measure the error against the actual data.</span></span> <span data-ttu-id="998b3-617">La nostra previsione riguarda i 12 mesi del 2013.</span><span class="sxs-lookup"><span data-stu-id="998b3-617">Our forecast will be for the 12 months of 2013.</span></span> <span data-ttu-id="998b3-618">È possibile calcolare una misura di errore per questa previsione nei dati effettivi non compresi nel set di dati di training.</span><span class="sxs-lookup"><span data-stu-id="998b3-618">We can compute an error measure for this forecast to the actual data that is not part of our training dataset.</span></span> <span data-ttu-id="998b3-619">Possiamo inoltre confrontare le prestazioni dei 18 anni di dati di addestramento con i 12 mesi dei dati di test.</span><span class="sxs-lookup"><span data-stu-id="998b3-619">Additionally, we can compare performance on the 18 years of training data to the 12 months of test data.</span></span>  

<span data-ttu-id="998b3-620">Per misurare le prestazioni di modelli in serie temporale viene usata, in genere, una serie di parametri.</span><span class="sxs-lookup"><span data-stu-id="998b3-620">A number of metrics are used to measure the performance of time series models.</span></span> <span data-ttu-id="998b3-621">In questo caso verrà usata la radice dell'errore quadratico medio (RMS).</span><span class="sxs-lookup"><span data-stu-id="998b3-621">In our case we will use the root mean square (RMS) error.</span></span> <span data-ttu-id="998b3-622">La funzione seguente calcola l'errore RMS tra due serie.</span><span class="sxs-lookup"><span data-stu-id="998b3-622">The following function computes the RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function to compute the RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments to function RMS.error of wrong type encountered",
                    "ERROR: Input vector to function RMS.error is too short",
                    "ERROR: Input vectors to function RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check the arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate the values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute the RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="998b3-623">Analogamente alla funzione `log.transform()` discussa nella sezione "Trasformazioni di valori", in questa funzione è presente molto codice per il controllo degli errori e per il ripristino delle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="998b3-623">As with the `log.transform()` function we discussed in the "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="998b3-624">I principi usati sono gli stessi.</span><span class="sxs-lookup"><span data-stu-id="998b3-624">The principles employed are the same.</span></span> <span data-ttu-id="998b3-625">Il lavoro viene eseguito in due posizioni incluse in `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="998b3-625">The work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="998b3-626">Poiché stiamo usando i logaritmi dei valori, eseguiremo in primo luogo l'esponenziazione delle serie temporali.</span><span class="sxs-lookup"><span data-stu-id="998b3-626">First, the time series are exponentiated, since we have been working with the logs of the values.</span></span> <span data-ttu-id="998b3-627">Passeremo quindi all'elaborazione della deviazione standard.</span><span class="sxs-lookup"><span data-stu-id="998b3-627">Second, the actual RMS error is computed.</span></span>  

<span data-ttu-id="998b3-628">Muniti di una funzione per calcolare la deviazione standard, creiamo ed eseguiamo l'output di un frame di dati contenente le deviazioni standard.</span><span class="sxs-lookup"><span data-stu-id="998b3-628">Equipped with a function to measure the RMS error, let's build and output a dataframe containing the RMS errors.</span></span> <span data-ttu-id="998b3-629">Includiamo quindi i termini relativi al modello con trend e completiamo il modello con fattori stagionali.</span><span class="sxs-lookup"><span data-stu-id="998b3-629">We will include terms for the trend model alone and the complete model with seasonal factors.</span></span> <span data-ttu-id="998b3-630">Il codice seguente esegue l'operazione usando i due modelli lineari costruiti.</span><span class="sxs-lookup"><span data-stu-id="998b3-630">The following code does the job by using the two linear models we have constructed.</span></span>

    ## Compute the RMS error in a dataframe
    ## Include the row names in the first column so they will
    ## appear in the output of the Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="998b3-631">L'esecuzione di questo codice produce nella porta di output Result Dataset il contenuto illustrato nella Figura 27.</span><span class="sxs-lookup"><span data-stu-id="998b3-631">Running this code produces the output shown in Figure 27 at the Result Dataset output port.</span></span>

![Confronto di errori RMS per i modelli][26]

<span data-ttu-id="998b3-633">*Figura 27. Confronto di errori RMS per i modelli.*</span><span class="sxs-lookup"><span data-stu-id="998b3-633">*Figure 27. Comparison of RMS errors for the models.*</span></span>

<span data-ttu-id="998b3-634">Da questi risultati si evince che l'aggiunta di fattori stagionali al modello riduce in modo significativo l'errore RMS.</span><span class="sxs-lookup"><span data-stu-id="998b3-634">From these results, we see that adding the seasonal factors to the model reduces the RMS error significantly.</span></span> <span data-ttu-id="998b3-635">Come previsto, inoltre, la deviazione standard per i dati di addestramento è leggermente inferiore rispetto alla previsione.</span><span class="sxs-lookup"><span data-stu-id="998b3-635">Not too surprisingly, the RMS error for the training data is a bit less than for the forecast.</span></span>

## <span data-ttu-id="998b3-636"><a id="appendixa"></a>APPENDICE A: Guida a RStudio</span><span class="sxs-lookup"><span data-stu-id="998b3-636"><a id="appendixa"></a>APPENDIX A: Guide to RStudio</span></span>
<span data-ttu-id="998b3-637">RStudio viene fornito con una documentazione molto dettagliata. In questa appendice mi limiterò quindi a fornire alcuni link alle sezioni principali della documentazione RStudio, utili per acquisire familiarità con questo prodotto.</span><span class="sxs-lookup"><span data-stu-id="998b3-637">RStudio is quite well documented, so in this appendix I will provide some links to the key sections of the RStudio documentation to get you started.</span></span>

1. <span data-ttu-id="998b3-638">Creazione di progetti</span><span class="sxs-lookup"><span data-stu-id="998b3-638">Creating projects</span></span>
   
   <span data-ttu-id="998b3-639">È possibile organizzare e gestire il codice R nei progetti usando RStudio.</span><span class="sxs-lookup"><span data-stu-id="998b3-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="998b3-640">La documentazione sull'uso dei progetti è disponibile all'indirizzo https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span><span class="sxs-lookup"><span data-stu-id="998b3-640">The documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="998b3-641">Consiglio di seguire queste indicazioni e creare un progetto per gli esempi di codice R riportati in questo documento.</span><span class="sxs-lookup"><span data-stu-id="998b3-641">I recommend that you follow these directions and create a project for the R code examples in this document.</span></span>  
2. <span data-ttu-id="998b3-642">Modifica ed esecuzione di codice R</span><span class="sxs-lookup"><span data-stu-id="998b3-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="998b3-643">RStudio offre un ambiente integrato per la modifica e l'esecuzione di codice R.</span><span class="sxs-lookup"><span data-stu-id="998b3-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="998b3-644">La documentazione è disponibile all'indirizzo https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span><span class="sxs-lookup"><span data-stu-id="998b3-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="998b3-645">Debug</span><span class="sxs-lookup"><span data-stu-id="998b3-645">Debugging</span></span>
   
   <span data-ttu-id="998b3-646">RStudio include avanzate funzionalità di debug.</span><span class="sxs-lookup"><span data-stu-id="998b3-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="998b3-647">La documentazione su queste funzionalità è disponibile all'indirizzo https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span><span class="sxs-lookup"><span data-stu-id="998b3-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="998b3-648">La documentazione sulle funzionalità di risoluzione dei problemi relativi ai punti di interruzione è disponibile all'indirizzo https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="998b3-648">The breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="998b3-649"><a id="appendixb"></a>APPENDICE B: Letture di approfondimento</span><span class="sxs-lookup"><span data-stu-id="998b3-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="998b3-650">Questa esercitazione sulla programmazione R illustra le nozioni di base sull'ambito di utilizzo del linguaggio R con Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="998b3-650">This R programming tutorial covers the basics of what you need to use the R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="998b3-651">Se non si ha familiarità con R, in CRAN sono disponibili due introduzioni:</span><span class="sxs-lookup"><span data-stu-id="998b3-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="998b3-652">"R for Beginners" di Emmanuel Paradis, un ottimo punto di inizio: http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span><span class="sxs-lookup"><span data-stu-id="998b3-652">R for Beginners by Emmanuel Paradis is a good place to start at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="998b3-653">An Introduction to R di W. N.</span><span class="sxs-lookup"><span data-stu-id="998b3-653">An Introduction to R by W. N.</span></span> <span data-ttu-id="998b3-654">Venables et.</span><span class="sxs-lookup"><span data-stu-id="998b3-654">Venables et.</span></span> <span data-ttu-id="998b3-655">al.</span><span class="sxs-lookup"><span data-stu-id="998b3-655">al.</span></span> <span data-ttu-id="998b3-656">fornisce informazioni più approfondite all'indirizzo http://cran.r-project.org/doc/manuals/R-intro.html.</span><span class="sxs-lookup"><span data-stu-id="998b3-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="998b3-657">Sono disponibili molti libri con informazioni introduttive su R.</span><span class="sxs-lookup"><span data-stu-id="998b3-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="998b3-658">Di seguito sono elencati quelli che ritengo più utili:</span><span class="sxs-lookup"><span data-stu-id="998b3-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="998b3-659">The Art of R Programming: A Tour of Statistical Software Design di Norman Matloff, un'eccellente introduzione alla programmazione in R.</span><span class="sxs-lookup"><span data-stu-id="998b3-659">The Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction to programming in R.</span></span>  
* <span data-ttu-id="998b3-660">R Cookbook di Paul Teetor, che offre un approccio problema-soluzione all'uso di R.</span><span class="sxs-lookup"><span data-stu-id="998b3-660">R Cookbook by Paul Teetor provides a problem and solution approach to using R.</span></span>  
* <span data-ttu-id="998b3-661">R in Action di Robert Kabacoff, un altro libro introduttivo valido.</span><span class="sxs-lookup"><span data-stu-id="998b3-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="998b3-662">Il sito Web Quick R costituisce inoltre una risorsa di grande utilità: http://www.statmethods.net/.</span><span class="sxs-lookup"><span data-stu-id="998b3-662">The companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="998b3-663">R Inferno di Patrick Burns è un libro sorprendentemente divertente che si occupa di diversi argomenti complessi in cui ci si può imbattere durante la programmazione in R. Il libro è disponibile gratuitamente all'indirizzo http://www.burns-stat.com/documents/books/the-r-inferno/.</span><span class="sxs-lookup"><span data-stu-id="998b3-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. The book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="998b3-664">Per informazioni più dettagliate sugli argomenti avanzati relativi a R, vedere il libro Advanced R di Hadley Wickham.</span><span class="sxs-lookup"><span data-stu-id="998b3-664">If you want a deep dive into advanced topics in R, have a look at the book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="998b3-665">La versione online del libro è disponibile all'indirizzo http://adv-r.had.co.nz/.</span><span class="sxs-lookup"><span data-stu-id="998b3-665">The online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="998b3-666">Un catalogo dei pacchetti delle serie temporali R è disponibile in CRAN Task View per l'analisi delle serie temporali: http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="998b3-666">A catalogue of R time series packages can be found in the CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="998b3-667">Per informazioni su specifici pacchetti di oggetti della serie temporale, fare riferimento alla documentazione dei singoli pacchetti.</span><span class="sxs-lookup"><span data-stu-id="998b3-667">For information on specific time series object packages, you should refer to the documentation for that package.</span></span>

<span data-ttu-id="998b3-668">Il libro Introductory Time Series with R di Paul Cowpertwait e Andrew Metcalfe fornisce un'introduzione all'uso di R per l'analisi delle serie temporali.</span><span class="sxs-lookup"><span data-stu-id="998b3-668">The book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction to using R for time series analysis.</span></span> <span data-ttu-id="998b3-669">Numerosi esempi di R sono infine disponibili in una grande quantità di testi teorici.</span><span class="sxs-lookup"><span data-stu-id="998b3-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="998b3-670">Alcune importanti risorse su Internet:</span><span class="sxs-lookup"><span data-stu-id="998b3-670">Some great internet resources:</span></span>

* <span data-ttu-id="998b3-671">DataCamp: DataCamp insegna a usare R dal proprio browser con lezioni video ed esercizi sulla codifica.</span><span class="sxs-lookup"><span data-stu-id="998b3-671">DataCamp: DataCamp teaches R in the comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="998b3-672">Sono disponibili anche esercitazioni interattive sulle ultime tecniche e pacchetti di R.</span><span class="sxs-lookup"><span data-stu-id="998b3-672">There are interactive tutorials on the latest R techniques and packages.</span></span> <span data-ttu-id="998b3-673">È possibile partecipare alle esercitazioni interattive e gratuite su R all'indirizzo https://www.datacamp.com/courses/introduction-to-r</span><span class="sxs-lookup"><span data-stu-id="998b3-673">Take the free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="998b3-674">Una Guida introduttiva alla programmazione con R da Programiz https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="998b3-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="998b3-675">Una rapida esercitazione su R di Kelly Black della Clarkson University è disponibile all'indirizzo http://www.cyclismo.org/tutorial/R/</span><span class="sxs-lookup"><span data-stu-id="998b3-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="998b3-676">Oltre 60 risorse su R sono elencate all'indirizzo http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span><span class="sxs-lookup"><span data-stu-id="998b3-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
