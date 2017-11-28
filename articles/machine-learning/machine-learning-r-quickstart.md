---
title: esercitazione aaaQuickstart per il linguaggio R per Machine Learning | Documenti Microsoft
description: Utilizzare questa esercitazione tooget avviato rapidamente utilizzando il linguaggio R hello con Azure Machine Learning Studio toocreate una soluzione di previsione di programmazione R.
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
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="8fae4-104">Esercitazione di avvio rapido per linguaggio di programmazione hello R per Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8fae4-104">Quickstart tutorial for hello R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="8fae4-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="8fae4-105">Introduction</span></span>
<span data-ttu-id="8fae4-106">Questa esercitazione rapida consente di avviare rapidamente l'estensione Azure Machine Learning tramite linguaggio di programmazione hello R.</span><span class="sxs-lookup"><span data-stu-id="8fae4-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using hello R programming language.</span></span> <span data-ttu-id="8fae4-107">Seguire questa esercitazione toocreate di programmazione R, testare ed eseguire codice R in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8fae4-107">Follow this R programming tutorial toocreate, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="8fae4-108">Quando si utilizza l'esercitazione, si creerà una soluzione completa di previsione utilizzando il linguaggio R hello in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8fae4-108">As you work through tutorial, you will create a complete forecasting solution by using hello R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="8fae4-109">Microsoft Azure Machine Learning contiene molti moduli validi per Machine Learning e per la manipolazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="8fae4-110">viene descritto il linguaggio R potente di Hello come hello lingua franca del analitica.</span><span class="sxs-lookup"><span data-stu-id="8fae4-110">hello powerful R language has been described as hello lingua franca of analytics.</span></span> <span data-ttu-id="8fae4-111">Fortunatamente, analitica e modifica dei dati in Azure Machine Learning può essere esteso con R. Questa combinazione fornisce hello scalabilità e facilità di distribuzione di Azure Machine Learning con flessibilità hello e analitica complete di R.</span><span class="sxs-lookup"><span data-stu-id="8fae4-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides hello scalability and ease of deployment of Azure Machine Learning with hello flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a><span data-ttu-id="8fae4-112">Set di dati di previsione e hello</span><span class="sxs-lookup"><span data-stu-id="8fae4-112">Forecasting and hello dataset</span></span>
<span data-ttu-id="8fae4-113">La previsione è un metodo analitico molto utile e ampiamente distribuito.</span><span class="sxs-lookup"><span data-stu-id="8fae4-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="8fae4-114">Intervallo da elaborare stime di vendita degli elementi stagionali, determinare i livelli di inventario ottimale, variabili macroeconomiche toopredicting utilizzi comuni.</span><span class="sxs-lookup"><span data-stu-id="8fae4-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, toopredicting macroeconomic variables.</span></span> <span data-ttu-id="8fae4-115">In genere, inoltre, viene eseguita con modelli in serie temporale.</span><span class="sxs-lookup"><span data-stu-id="8fae4-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="8fae4-116">Dati della serie temporale sono dati in cui i valori hello dispone di un indice di tempo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-116">Time series data is data in which hello values have a time index.</span></span> <span data-ttu-id="8fae4-117">indice di fase Hello può essere regolare, ad esempio, ogni mese o ogni minuto o irregolari.</span><span class="sxs-lookup"><span data-stu-id="8fae4-117">hello time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="8fae4-118">Sui dati in serie temporale si basano i modelli in serie temporale.</span><span class="sxs-lookup"><span data-stu-id="8fae4-118">A time series model is based on time series data.</span></span> <span data-ttu-id="8fae4-119">linguaggio di programmazione Hello R contiene un framework flessibile e completa analitica per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="8fae4-119">hello R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="8fae4-120">In questa esercitazione prenderemo in esame la produzione casearia in California, con i relativi dati sui prezzi.</span><span class="sxs-lookup"><span data-stu-id="8fae4-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="8fae4-121">Questi dati includono informazioni mensile sul prezzo hello del file System fat latte, una merce benchmark e di produzione hello di diversi prodotti da latte.</span><span class="sxs-lookup"><span data-stu-id="8fae4-121">This data includes monthly information on hello production of several dairy products and hello price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="8fae4-122">dati Hello usati in questo articolo, insieme a script R, possono essere [scaricato da qui][download].</span><span class="sxs-lookup"><span data-stu-id="8fae4-122">hello data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="8fae4-123">Questi dati è stato originariamente sintetizzati utilizzando le informazioni disponibili da hello università di Wisconsin in http://future.aae.wisc.edu/tab/production.html.</span><span class="sxs-lookup"><span data-stu-id="8fae4-123">This data was originally synthesized from information available from hello University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="8fae4-124">Organizzazione</span><span class="sxs-lookup"><span data-stu-id="8fae4-124">Organization</span></span>
<span data-ttu-id="8fae4-125">Abbiamo avanzamento attraverso diversi passaggi per comprendere come toocreate, test e di eseguire codice di manipolazione R analitica e i dati nell'ambiente di Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-125">We will progress through several steps as you learn how toocreate, test and execute analytics and data manipulation R code in hello Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="8fae4-126">Innanzitutto verrà illustrato l'utilizzo di linguaggio hello R nell'ambiente Azure Machine Learning Studio hello base hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-126">First we will explore hello basics of using hello R language in hello Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="8fae4-127">Quindi è stato toodiscussing vari aspetti dei / o per dati, il codice R e grafica nell'ambiente di Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-127">Then we progress toodiscussing various aspects of I/O for data, R code and graphics in hello Azure Machine Learning environment.</span></span>
* <span data-ttu-id="8fae4-128">Prima parte di hello della nostra soluzione previsione verrà quindi creato tramite la creazione di codice per la pulizia dei dati e la trasformazione.</span><span class="sxs-lookup"><span data-stu-id="8fae4-128">We will then construct hello first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="8fae4-129">Con i dati preparati si eseguirà un'analisi delle correlazioni hello tra diverse variabili hello nel set di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-129">With our data prepared we will perform an analysis of hello correlations between several of hello variables in our dataset.</span></span>
* <span data-ttu-id="8fae4-130">Infine, verrà creato un modello di previsione in serie temporale (stagionale) per la produzione di latte.</span><span class="sxs-lookup"><span data-stu-id="8fae4-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="8fae4-131"><a id="mlstudio"></a>Interagire con il linguaggio R in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="8fae4-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="8fae4-132">In questa sezione vengono illustrati alcuni concetti di base dell'interazione con il linguaggio di programmazione hello R nell'ambiente di Machine Learning Studio hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-132">This section takes you through some basics of interacting with hello R programming language in hello Machine Learning Studio environment.</span></span> <span data-ttu-id="8fae4-133">il linguaggio R Hello offre un potente strumento toocreate personalizzato analitica e dati Modifica moduli nell'ambiente Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-133">hello R language provides a powerful tool toocreate customized analytics and data manipulation modules within hello Azure Machine Learning environment.</span></span>

<span data-ttu-id="8fae4-134">Si utilizzerà codice R toodevelop, test e debug di RStudio su una scala di piccole dimensioni.</span><span class="sxs-lookup"><span data-stu-id="8fae4-134">I will use RStudio toodevelop, test and debug R code on a small scale.</span></span> <span data-ttu-id="8fae4-135">Questo codice viene quindi Taglia e Incolla in un [Execute R Script] [ execute-r-script] modulo in Machine Learning Studio pronto toorun.</span><span class="sxs-lookup"><span data-stu-id="8fae4-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready toorun.</span></span>  

### <a name="hello-execute-r-script-module"></a><span data-ttu-id="8fae4-136">modulo Execute R Script Hello</span><span class="sxs-lookup"><span data-stu-id="8fae4-136">hello Execute R Script module</span></span>
<span data-ttu-id="8fae4-137">All'interno di Machine Learning Studio, gli script di R vengono eseguiti all'interno di hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-137">Within Machine Learning Studio, R scripts are run within hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="8fae4-138">Un esempio di hello [Execute R Script] [ execute-r-script] modulo in Machine Learning Studio è illustrato nella figura 1.</span><span class="sxs-lookup"><span data-stu-id="8fae4-138">An example of hello [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![Linguaggio di programmazione R: modulo Execute R Script hello selezionato in Machine Learning Studio][1]

<span data-ttu-id="8fae4-140">*Figura 1. ambiente di Machine Learning Studio Hello con modulo Execute R Script hello selezionato.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-140">*Figure 1. hello Machine Learning Studio environment showing hello Execute R Script module selected.*</span></span>

<span data-ttu-id="8fae4-141">Riferimento tooFigure 1, ecco alcuni dei componenti chiave di hello dell'ambiente di Machine Learning Studio hello per l'utilizzo di hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-141">Referring tooFigure 1, let's look at some of hello key parts of hello Machine Learning Studio environment for working with hello [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="8fae4-142">i moduli di Hello nell'esperimento hello vengono visualizzati nel riquadro centrale hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-142">hello modules in hello experiment are shown in hello center pane.</span></span>
* <span data-ttu-id="8fae4-143">parte superiore di Hello del riquadro di destra hello contiene tooview una finestra e modificare gli script R.</span><span class="sxs-lookup"><span data-stu-id="8fae4-143">hello upper part of hello right pane contains a window tooview and edit your R scripts.</span></span>  
* <span data-ttu-id="8fae4-144">parte inferiore di Hello del riquadro di destra vengono mostrate alcune proprietà di hello [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="8fae4-144">hello lower part of right pane shows some properties of hello [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="8fae4-145">È possibile visualizzare i registri errori e l'output di hello facendo clic su aree sensibili appropriato hello di questo riquadro.</span><span class="sxs-lookup"><span data-stu-id="8fae4-145">You can view hello error and output logs by clicking on hello appropriate spots of this pane.</span></span>

<span data-ttu-id="8fae4-146">Verrà, naturalmente, preso hello [Execute R Script] [ execute-r-script] più dettagliatamente nel resto di hello di questo documento.</span><span class="sxs-lookup"><span data-stu-id="8fae4-146">We will, of course, be discussing hello [Execute R Script][execute-r-script] in greater detail in hello rest of this document.</span></span>

<span data-ttu-id="8fae4-147">Quando si usano funzioni R complesse, è preferibile effettuare le operazioni di modifica, test e debug in RStudio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="8fae4-148">Come con qualsiasi altro software di sviluppo, inoltre, è opportuno estendere il codice in modo incrementale, così da poterlo verificare in piccoli e semplici casi di test.</span><span class="sxs-lookup"><span data-stu-id="8fae4-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="8fae4-149">Tagliare e incollare le funzioni nella finestra di script R hello di hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-149">Then cut and paste your functions into hello R script window of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="8fae4-150">Questo approccio consente tooharness sia hello RStudio ambiente di sviluppo integrato (IDE) e hello potenza di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8fae4-150">This approach allows you tooharness both hello RStudio integrated development environment (IDE) and hello power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="8fae4-151">Eseguire il codice R</span><span class="sxs-lookup"><span data-stu-id="8fae4-151">Execute R code</span></span>
<span data-ttu-id="8fae4-152">Qualsiasi codice R in hello [Execute R Script] [ execute-r-script] modulo verrà eseguito quando si esegue l'esperimento hello facendo clic su hello **eseguire** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8fae4-152">Any R code in hello [Execute R Script][execute-r-script] module will execute when you run hello experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="8fae4-153">Al termine dell'esecuzione, un segno di spunta verrà visualizzato nella hello [Execute R Script] [ execute-r-script] icona.</span><span class="sxs-lookup"><span data-stu-id="8fae4-153">When execution has completed, a check mark will appear on hello [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="8fae4-154">Codice R difensivo per Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8fae4-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="8fae4-155">Se si sviluppa un codice R per, ad esempio, un servizio Web usando Azure Machine Learning, è necessario pianificare in che modo il codice R gestirà gli input di dati imprevisti e le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="8fae4-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="8fae4-156">toomaintain chiarezza, non ho incluso perlopiù in modo hello di controllo o nella maggior parte degli esempi di codice hello illustrati di gestione delle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="8fae4-156">toomaintain clarity, I have not included much in hello way of checking or exception handling in most of hello code examples shown.</span></span> <span data-ttu-id="8fae4-157">Tuttavia, verranno forniti diversi esempi di funzioni che prevedono l'uso della capacità di gestione delle eccezioni di R.</span><span class="sxs-lookup"><span data-stu-id="8fae4-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="8fae4-158">Se è necessario un trattamento più completato di gestione delle eccezioni di R, è consigliabile leggere le sezioni applicabili hello del libro hello da Wickham elencati nella [appendice B - approfondimento](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="8fae4-158">If you need a more complete treatment of R exception handling, I recommend you read hello applicable sections of hello book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="8fae4-159">Eseguire il debug e testare R in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="8fae4-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="8fae4-160">tooreiterate, consiglia di test e debug del codice R su una scala di piccole dimensioni in RStudio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-160">tooreiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="8fae4-161">Tuttavia, vi sono casi in cui è necessario tootrack i problemi di codice R in hello [Execute R Script] [ execute-r-script] stesso.</span><span class="sxs-lookup"><span data-stu-id="8fae4-161">However, there are cases where you will need tootrack down R code problems in hello [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="8fae4-162">Inoltre, è buona norma toocheck i risultati in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-162">In addition, it is good practice toocheck your results in Machine Learning Studio.</span></span>

<span data-ttu-id="8fae4-163">Output dell'esecuzione di hello del codice R e sulla piattaforma Azure Machine Learning hello si trova principalmente nel log.</span><span class="sxs-lookup"><span data-stu-id="8fae4-163">Output from hello execution of your R code and on hello Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="8fae4-164">ma alcune informazioni aggiuntive possono essere presenti in error.log.</span><span class="sxs-lookup"><span data-stu-id="8fae4-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="8fae4-165">Se si verifica un errore in Machine Learning Studio durante l'esecuzione del codice R, la prima linea di condotta deve essere toolook in error.log.</span><span class="sxs-lookup"><span data-stu-id="8fae4-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be toolook at error.log.</span></span> <span data-ttu-id="8fae4-166">Questo file può contenere toohelp i messaggi di errore utile per comprendere e correggere l'errore.</span><span class="sxs-lookup"><span data-stu-id="8fae4-166">This file can contain useful error messages toohelp you understand and correct your error.</span></span> <span data-ttu-id="8fae4-167">tooview error.log, fare clic su **Visualizza log degli errori** su hello **riquadro proprietà** per hello [Execute R Script] [ execute-r-script] contenente l'errore hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-167">tooview error.log, click on **View error log** on hello **properties pane** for hello [Execute R Script][execute-r-script] containing hello error.</span></span>

<span data-ttu-id="8fae4-168">Ad esempio, è stata eseguita hello seguente codice R, con una variabile y non definito in un [Execute R Script] [ execute-r-script] modulo:</span><span class="sxs-lookup"><span data-stu-id="8fae4-168">For example, I ran hello following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="8fae4-169">Questo codice non tooexecute, causando una condizione di errore.</span><span class="sxs-lookup"><span data-stu-id="8fae4-169">This code fails tooexecute, resulting in an error condition.</span></span> <span data-ttu-id="8fae4-170">Facendo clic su **Visualizza log degli errori** su hello **riquadro proprietà** produce hello visualizzazione illustrato nella figura 2.</span><span class="sxs-lookup"><span data-stu-id="8fae4-170">Clicking on **View error log** on hello **properties pane** produces hello display shown in Figure 2.</span></span>

  ![Finestra di popup con messaggio di errore][2]

<span data-ttu-id="8fae4-172">*Figura 2. Finestra di popup con il messaggio di errore.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="8fae4-173">Sembra che è necessario toolook nel messaggio di errore di log toosee hello R.</span><span class="sxs-lookup"><span data-stu-id="8fae4-173">It looks like we need toolook in output.log toosee hello R error message.</span></span> <span data-ttu-id="8fae4-174">Fare clic su hello [Execute R Script] [ execute-r-script] e quindi fare clic su hello **visualizzare log** elemento hello **riquadro proprietà** toohello destra.</span><span class="sxs-lookup"><span data-stu-id="8fae4-174">Click on hello [Execute R Script][execute-r-script] and then click on hello **View output.log** item on hello **properties pane** toohello right.</span></span> <span data-ttu-id="8fae4-175">Verrà visualizzata una nuova finestra del browser e viene visualizzato il seguente hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-175">A new browser window opens, and I see hello following.</span></span>

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="8fae4-176">Questo messaggio di errore non contiene avere sorprese e consente di identificare chiaramente il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-176">This error message contains no surprises and clearly identifies hello problem.</span></span>

<span data-ttu-id="8fae4-177">valore di hello tooinspect di qualsiasi oggetto in R, è possibile stampare file di log toohello questi valori.</span><span class="sxs-lookup"><span data-stu-id="8fae4-177">tooinspect hello value of any object in R, you can print these values toohello output.log file.</span></span> <span data-ttu-id="8fae4-178">le regole di Hello per esaminare l'oggetto valori sono essenzialmente hello stesso come in una sessione interattiva di R.</span><span class="sxs-lookup"><span data-stu-id="8fae4-178">hello rules for examining object values are essentially hello same as in an interactive R session.</span></span> <span data-ttu-id="8fae4-179">Ad esempio, se si digita un nome di variabile in una riga, il valore di hello dell'oggetto hello sarà stampato toohello file di log.</span><span class="sxs-lookup"><span data-stu-id="8fae4-179">For example, if you type a variable name on a line, hello value of hello object will be printed toohello output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="8fae4-180">Pacchetti in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="8fae4-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="8fae4-181">Azure Machine Learning viene fornito con più di 350 pacchetti di linguaggio R preinstallati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="8fae4-182">È possibile utilizzare hello seguente di codice hello [Execute R Script] [ execute-r-script] tooretrieve modulo un elenco di hello preinstallato pacchetti.</span><span class="sxs-lookup"><span data-stu-id="8fae4-182">You can use hello following code in hello [Execute R Script][execute-r-script] module tooretrieve a list of hello preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="8fae4-183">Se non si capiscono hello ultimo line-of-questo codice di un determinato momento hello, continuare a leggere.</span><span class="sxs-lookup"><span data-stu-id="8fae4-183">If you don't understand hello last line of this code at hello moment, read on.</span></span> <span data-ttu-id="8fae4-184">Nel resto di hello di questo documento verranno ampiamente illustrati l'uso di R nell'ambiente di Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-184">In hello rest of this document we will extensively discuss using R in hello Azure Machine Learning environment.</span></span>

### <a name="introduction-toorstudio"></a><span data-ttu-id="8fae4-185">Introduzione tooRStudio</span><span class="sxs-lookup"><span data-stu-id="8fae4-185">Introduction tooRStudio</span></span>
<span data-ttu-id="8fae4-186">RStudio è un diffuso dell'IDE per R. Si utilizzerà RStudio per la modifica, test e debug di parte di codice hello R usati in questa Guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="8fae4-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of hello R code used in this quick start guide.</span></span> <span data-ttu-id="8fae4-187">Dopo aver testato ed è pronto codice R, tagliare e incollare un Machine Learning Studio dall'editor RStudio hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-187">Once R code is tested and ready, you simply cut and paste from hello RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="8fae4-188">Se non si dispone di linguaggio di programmazione hello R installato nel computer desktop, è consigliabile che eseguire questa operazione ora.</span><span class="sxs-lookup"><span data-stu-id="8fae4-188">If you do not have hello R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="8fae4-189">Per il download gratuito di linguaggio open source R è disponibile in rete di archiviazione completa R (CRAN) hello in [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="8fae4-189">Free downloads of open source R language are available at hello Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="8fae4-190">Sono disponibili anche download per Windows, Mac OS e Linux/UNIX.</span><span class="sxs-lookup"><span data-stu-id="8fae4-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="8fae4-191">Scegliere un mirror nelle vicinanze e seguire le direzioni di download di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-191">Choose a nearby mirror and follow hello download directions.</span></span> <span data-ttu-id="8fae4-192">Il sistema CRAN contiene anche una serie di utili pacchetti di analisi e manipolazione di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="8fae4-193">Se si tooRStudio nuovo, si deve scaricare e installare la versione desktop di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-193">If you are new tooRStudio, you should download and install hello desktop version.</span></span> <span data-ttu-id="8fae4-194">È possibile trovare hello che rstudio Scarica per Windows, Mac OS e Linux/UNIX all'http://www.rstudio.com/products/RStudio/.</span><span class="sxs-lookup"><span data-stu-id="8fae4-194">You can find hello RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="8fae4-195">Seguire le istruzioni di hello fornite tooinstall RStudio sul computer desktop.</span><span class="sxs-lookup"><span data-stu-id="8fae4-195">Follow hello directions provided tooinstall RStudio on your desktop machine.</span></span>  

<span data-ttu-id="8fae4-196">TooRStudio un'introduzione all'esercitazione è disponibile all'indirizzo https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-196">A tutorial introduction tooRStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="8fae4-197">Altre informazioni sull'uso di RStudio sono disponibili nell'[Appendice A][appendixa].</span><span class="sxs-lookup"><span data-stu-id="8fae4-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="8fae4-198"><a id="scriptmodule"></a>Ottenere dati da e verso modulo Execute R Script hello</span><span class="sxs-lookup"><span data-stu-id="8fae4-198"><a id="scriptmodule"></a>Get data in and out of hello Execute R Script module</span></span>
<span data-ttu-id="8fae4-199">In questa sezione verranno trattati come ottenere dati dentro e fuori da hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-199">In this section we will discuss how you get data into and out of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="8fae4-200">Verranno esaminate come toohandle vari tipi di dati letto in e da hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-200">We will review how toohandle various data types read into and out of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="8fae4-201">codice completo di Hello per questa sezione è nel file zip hello scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8fae4-201">hello complete code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="8fae4-202">Caricare e controllare i dati in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="8fae4-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="8fae4-203"><a id="loading"></a>Caricare set di dati hello</span><span class="sxs-lookup"><span data-stu-id="8fae4-203"><a id="loading"></a>Load hello dataset</span></span>
<span data-ttu-id="8fae4-204">Si inizierà caricando hello **csdairydata.csv** file in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-204">We will start by loading hello **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="8fae4-205">Avviare l'ambiente di Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="8fae4-206">Fare clic su **+ nuovo** in hello inferiore sinistro della schermata e selezionare **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="8fae4-206">Click on **+ NEW** at hello lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="8fae4-207">Selezionare **dal File locale**e quindi **Sfoglia** file hello tooselect.</span><span class="sxs-lookup"><span data-stu-id="8fae4-207">Select **From Local File**, and then **Browse** tooselect hello file.</span></span>
* <span data-ttu-id="8fae4-208">Assicurarsi di avere selezionato **file CSV generico con intestazione (. csv)** come tipo hello per hello set di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-208">Make sure you have selected **Generic CSV file with header (.csv)** as hello type for hello dataset.</span></span>
* <span data-ttu-id="8fae4-209">Fare clic su hello segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="8fae4-209">Click hello check mark.</span></span>
* <span data-ttu-id="8fae4-210">Dopo che sono stati caricati i set di dati hello, si otterranno hello nuovo set di dati facendo clic su hello **set di dati** scheda.</span><span class="sxs-lookup"><span data-stu-id="8fae4-210">After hello dataset has been uploaded, you should see hello new dataset by clicking on hello **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="8fae4-211">Creare un esperimento</span><span class="sxs-lookup"><span data-stu-id="8fae4-211">Create an experiment</span></span>
<span data-ttu-id="8fae4-212">Ora che si dispongono di alcuni dati in Machine Learning Studio, è necessario toocreate un'analisi di hello toodo esperimento.</span><span class="sxs-lookup"><span data-stu-id="8fae4-212">Now that we have some data in Machine Learning Studio, we need toocreate an experiment toodo hello analysis.</span></span>  

* <span data-ttu-id="8fae4-213">Fare clic su **+ nuovo** hello basso a sinistra e selezionare **esperimento**, quindi **esperimento vuoto**.</span><span class="sxs-lookup"><span data-stu-id="8fae4-213">Click on **+ NEW** at hello lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="8fae4-214">È possibile assegnare un nome all'esperimento selezionando e modifica, hello **esperimento creato in...**  titolo nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-214">You can name your experiment by selecting, and modifying, hello **Experiment created on ...** title at hello top of hello page.</span></span> <span data-ttu-id="8fae4-215">Ad esempio, può essere modificato troppo**CA Latticini Analysis**.</span><span class="sxs-lookup"><span data-stu-id="8fae4-215">For example, changing it too**CA Dairy Analysis**.</span></span>
* <span data-ttu-id="8fae4-216">A sinistra hello della pagina esperimento hello, espandere **Saved Datasets**e quindi **set di dati personali**.</span><span class="sxs-lookup"><span data-stu-id="8fae4-216">On hello left of hello experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="8fae4-217">Dovrebbe essere hello **cadairydata.csv** caricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8fae4-217">You should see hello **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="8fae4-218">Trascinamento della selezione hello **csdairydata.csv dataset** nella sperimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-218">Drag and drop hello **csdairydata.csv dataset** onto hello experiment.</span></span>
* <span data-ttu-id="8fae4-219">In hello **ricerca sperimentare elementi** casella in alto di hello del riquadro di sinistra hello, tipo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="8fae4-219">In hello **Search experiment items** box on hello top of hello left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="8fae4-220">Verrà visualizzato il modulo hello visualizzate nell'elenco di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-220">You will see hello module appear in hello search list.</span></span>
* <span data-ttu-id="8fae4-221">Trascinamento della selezione hello [Execute R Script] [ execute-r-script] modulo sulla tavolozza.</span><span class="sxs-lookup"><span data-stu-id="8fae4-221">Drag and drop hello [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="8fae4-222">Connettere l'output di hello di hello **csdairydata.csv dataset** input all'estrema sinistra toohello (**Dataset1**) di hello [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="8fae4-222">Connect hello output of hello **csdairydata.csv dataset** toohello leftmost input (**Dataset1**) of hello [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="8fae4-223">**Non dimenticare tooclick su 'Salva'!**</span><span class="sxs-lookup"><span data-stu-id="8fae4-223">**Don't forget tooclick on 'Save'!**</span></span>  

<span data-ttu-id="8fae4-224">A questo punto, l'esperimento dovrebbe essere simile a quanto riportato nella Figura 3.</span><span class="sxs-lookup"><span data-stu-id="8fae4-224">At this point your experiment should look something like Figure 3.</span></span>

![Hello CA Latticini Analysis sperimentare set di dati e il modulo Execute R Script][3]

<span data-ttu-id="8fae4-226">*Figura 3. Hello CA Latticini Analysis sperimentare dal set di dati e il modulo Execute R Script.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-226">*Figure 3. hello CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-hello-data"></a><span data-ttu-id="8fae4-227">Controllo sui dati hello</span><span class="sxs-lookup"><span data-stu-id="8fae4-227">Check on hello data</span></span>
<span data-ttu-id="8fae4-228">Di seguito hanno un aspetto dati hello che è stato caricato l'esperimento.</span><span class="sxs-lookup"><span data-stu-id="8fae4-228">Let's have a look at hello data we have loaded into our experiment.</span></span> <span data-ttu-id="8fae4-229">Nell'esperimento hello, fare clic su output di hello di hello **cadairydata.csv dataset** e selezionare **visualizzare**.</span><span class="sxs-lookup"><span data-stu-id="8fae4-229">In hello experiment, click on hello output of hello **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="8fae4-230">Dovrebbe apparire una tabella simile a quella riportata nella Figura 4.</span><span class="sxs-lookup"><span data-stu-id="8fae4-230">You should see something like Figure 4.</span></span>  

![Riepilogo dei set di dati cadairydata.csv hello][4]

<span data-ttu-id="8fae4-232">*Figura 4. Riepilogo dei set di dati cadairydata.csv hello.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-232">*Figure 4. Summary of hello cadairydata.csv dataset.*</span></span>

<span data-ttu-id="8fae4-233">In questa tabella sono presenti numerose informazioni utili.</span><span class="sxs-lookup"><span data-stu-id="8fae4-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="8fae4-234">Possiamo vedere hello prima diverse righe del set di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-234">We can see hello first several rows of that dataset.</span></span> <span data-ttu-id="8fae4-235">Se si seleziona una colonna, hello sezione relativa alle statistiche Mostra ulteriori informazioni sulla colonna hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-235">If we select a column, hello Statistics section shows more information about hello column.</span></span> <span data-ttu-id="8fae4-236">Ad esempio, riga del tipo di funzionalità hello Mostra quali tipi di dati di Azure Machine Learning Studio assegnato toohello colonna.</span><span class="sxs-lookup"><span data-stu-id="8fae4-236">For example, hello Feature Type row shows us what data types Azure Machine Learning Studio assigned toohello column.</span></span> <span data-ttu-id="8fae4-237">Disporre di un rapido controllo di questo è un controllo di integrità valido prima di iniziare toodo qualsiasi lavoro grave.</span><span class="sxs-lookup"><span data-stu-id="8fae4-237">Having a quick look like this is a good sanity check before we start toodo any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="8fae4-238">Primo script R</span><span class="sxs-lookup"><span data-stu-id="8fae4-238">First R script</span></span>
<span data-ttu-id="8fae4-239">Creare un semplice primo tooexperiment di script R con in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-239">Let's create a simple first R script tooexperiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="8fae4-240">Dichiaro di aver creato e testato hello lo script in RStudio seguente.</span><span class="sxs-lookup"><span data-stu-id="8fae4-240">I have created and tested hello following script in RStudio.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="8fae4-241">A questo punto è necessario tootransfer questo tooAzure script Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-241">Now I need tootransfer this script tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="8fae4-242">Potrei semplicemente eseguire un'operazione di copia e incolla,</span><span class="sxs-lookup"><span data-stu-id="8fae4-242">I could simply cut and paste.</span></span> <span data-ttu-id="8fae4-243">ma in questo caso trasferirò lo script R tramite un file con estensione zip.</span><span class="sxs-lookup"><span data-stu-id="8fae4-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-toohello-execute-r-script-module"></a><span data-ttu-id="8fae4-244">Modulo Execute R Script toohello input di dati</span><span class="sxs-lookup"><span data-stu-id="8fae4-244">Data input toohello Execute R Script module</span></span>
<span data-ttu-id="8fae4-245">Si dispone di un'occhiata hello input toohello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-245">Let's have a look at hello inputs toohello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="8fae4-246">In questo esempio si leggerà i dati per California hello in hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-246">In this example we will read hello California dairy data into hello [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="8fae4-247">Esistono tre possibili input per hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-247">There are three possible inputs for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="8fae4-248">È possibile usarne una o tutte, in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="8fae4-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="8fae4-249">È inoltre possibile toouse una R script che non accetta alcun input.</span><span class="sxs-lookup"><span data-stu-id="8fae4-249">It is also perfectly reasonable toouse an R script that takes no input at all.</span></span>  

<span data-ttu-id="8fae4-250">Diamo un'occhiata ognuno di questi input, da tooright a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8fae4-250">Let's look at each of these inputs, going from left tooright.</span></span> <span data-ttu-id="8fae4-251">È possibile visualizzare i nomi di hello di ogni input hello posizionando il cursore sull'input hello e durante la lettura della descrizione comando hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-251">You can see hello names of each of hello inputs by placing your cursor over hello input and reading hello tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="8fae4-252">Script Bundle</span><span class="sxs-lookup"><span data-stu-id="8fae4-252">Script Bundle</span></span>
<span data-ttu-id="8fae4-253">Hello input Script Bundle consente si toopass hello del contenuto di un file zip in [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-253">hello Script Bundle input allows you toopass hello contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="8fae4-254">È possibile utilizzare uno dei seguenti comandi tooread hello contenuto file zip hello nel codice R hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-254">You can use one of hello following commands tooread hello contents of hello zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="8fae4-255">Azure Machine Learning considera i file ZIP hello come se fossero in hello src / directory, pertanto è necessario tooprefix nei nomi di file con questo nome di directory.</span><span class="sxs-lookup"><span data-stu-id="8fae4-255">Azure Machine Learning treats files in hello zip as if they are in hello src/ directory, so you need tooprefix your file names with this directory name.</span></span> <span data-ttu-id="8fae4-256">Ad esempio, se hello zip contiene file hello `yourfile.R` e `yourData.rdata` nella radice di zip hello hello sarebbe risolvere queste informazioni come `src/yourfile.R` e `src/yourData.rdata` quando si utilizza `source` e `load`.</span><span class="sxs-lookup"><span data-stu-id="8fae4-256">For example, if hello zip contains hello files `yourfile.R` and `yourData.rdata` in hello root of hello zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="8fae4-257">Set di dati di caricamento in già descritto [caricamento dataset hello](#loading).</span><span class="sxs-lookup"><span data-stu-id="8fae4-257">We already discussed loading datasets in [Loading hello dataset](#loading).</span></span> <span data-ttu-id="8fae4-258">Dopo aver creato e testato script hello R illustrato nella sezione precedente di hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8fae4-258">Once you have created and tested hello R script shown in hello previous section, do hello following:</span></span>

1. <span data-ttu-id="8fae4-259">Salva script hello R in un. File di R.</span><span class="sxs-lookup"><span data-stu-id="8fae4-259">Save hello R script into a .R file.</span></span> <span data-ttu-id="8fae4-260">Chiamerò il mio file di script "simpleplot.R".</span><span class="sxs-lookup"><span data-stu-id="8fae4-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="8fae4-261">Di seguito è riportato il contenuto di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-261">Here's hello contents.</span></span>
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="8fae4-262">Creare un file con estensione zip e copiare al suo interno lo script creato.</span><span class="sxs-lookup"><span data-stu-id="8fae4-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="8fae4-263">In Windows, è possibile fare clic sul file hello e selezionare **inviare**e quindi **cartella**.</span><span class="sxs-lookup"><span data-stu-id="8fae4-263">On Windows, you can right-click on hello file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="8fae4-264">Si creerà un nuovo file zip contenente hello "simpleplot. File R".</span><span class="sxs-lookup"><span data-stu-id="8fae4-264">This will create a new zip file containing hello "simpleplot.R" file.</span></span>
3. <span data-ttu-id="8fae4-265">Aggiungere il file toohello **set di dati** in Machine Learning Studio, che specifica il tipo di hello come **zip**.</span><span class="sxs-lookup"><span data-stu-id="8fae4-265">Add your file toohello **datasets** in Machine Learning Studio, specifying hello type as **zip**.</span></span> <span data-ttu-id="8fae4-266">Dovrebbe essere file zip hello nel DataSet.</span><span class="sxs-lookup"><span data-stu-id="8fae4-266">You should now see hello zip file in your datasets.</span></span>
4. <span data-ttu-id="8fae4-267">Trascinare e rilasciare file zip hello da **set di dati** su hello **area di lavoro di Machine Learning Studio**.</span><span class="sxs-lookup"><span data-stu-id="8fae4-267">Drag and drop hello zip file from **datasets** onto hello **ML Studio canvas**.</span></span>
5. <span data-ttu-id="8fae4-268">Connettere l'output di hello di hello **zip dati** icona toohello **Script Bundle** input di hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-268">Connect hello output of hello **zip data** icon toohello **Script Bundle** input of hello [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="8fae4-269">Hello tipo `source()` funzione con il nome del file zip nella finestra di codice hello per hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-269">Type hello `source()` function with your zip file name into hello code window for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="8fae4-270">In questo caso, digitare `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="8fae4-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="8fae4-271">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="8fae4-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="8fae4-272">Dopo aver completati questi passaggi, hello [Execute R Script] [ execute-r-script] modulo verrà eseguiti script R hello in file con estensione zip hello quando viene eseguito l'esperimento hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-272">Once these steps are complete, hello [Execute R Script][execute-r-script] module will execute hello R script in hello zip file when hello experiment is run.</span></span> <span data-ttu-id="8fae4-273">A questo punto l'esperimento dovrebbe avere un aspetto simile a quello riportato nella Figura 5.</span><span class="sxs-lookup"><span data-stu-id="8fae4-273">At this point your experiment should look something like Figure 5.</span></span>

![Esperimento con script R compresso][6]

<span data-ttu-id="8fae4-275">*Figura 5. Esperimento con script R compresso.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="8fae4-276">Dataset1</span><span class="sxs-lookup"><span data-stu-id="8fae4-276">Dataset1</span></span>
<span data-ttu-id="8fae4-277">È possibile passare una tabella rettangolare di dati R tooyour codice usando input hello Dataset1.</span><span class="sxs-lookup"><span data-stu-id="8fae4-277">You can pass a rectangular table of data tooyour R code by using hello Dataset1 input.</span></span> <span data-ttu-id="8fae4-278">Nel nostro hello uno script semplice `maml.mapInputPort(1)` funzione legge i dati di hello dalla porta 1.</span><span class="sxs-lookup"><span data-stu-id="8fae4-278">In our simple script hello `maml.mapInputPort(1)` function reads hello data from port 1.</span></span> <span data-ttu-id="8fae4-279">Questi dati viene quindi assegnati tooa nome variabile di frame di dati nel codice.</span><span class="sxs-lookup"><span data-stu-id="8fae4-279">This data is then assigned tooa dataframe variable name in your code.</span></span> <span data-ttu-id="8fae4-280">Nello script semplice prima riga di hello del codice esegue l'assegnazione hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-280">In our simple script hello first line of code performs hello assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="8fae4-281">Eseguire l'esperimento facendo clic su hello **eseguire** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8fae4-281">Execute your experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="8fae4-282">Al termine dell'esecuzione di hello, fare clic su hello [Execute R Script] [ execute-r-script] modulo e quindi fare clic su **Visualizza log di output** nel riquadro Proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-282">When hello execution finishes, click on hello [Execute R Script][execute-r-script] module and then click **View output log** on hello properties pane.</span></span> <span data-ttu-id="8fae4-283">Una nuova pagina da visualizzare nel browser che mostra il contenuto di hello del file di log hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-283">A new page should appear in your browser showing hello contents of hello output.log file.</span></span> <span data-ttu-id="8fae4-284">Quando si scorre verso il basso dovrebbe essere simile alla seguente hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-284">When you scroll down you should see something like hello following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="8fae4-285">Più lontano verso il basso hello pagina è informazioni più dettagliate sulle colonne hello, che avrà un aspetto simile alla seguente hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-285">Farther down hello page is more detailed information on hello columns, which will look something like hello following.</span></span>

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

<span data-ttu-id="8fae4-286">Questi risultati sono principalmente come previsto, con 228 osservazioni e 9 colonne nel frame di dati hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-286">These results are mostly as expected, with 228 observations and 9 columns in hello dataframe.</span></span> <span data-ttu-id="8fae4-287">È possibile vedere i nomi di colonna hello, tipo di dati R hello e un esempio di ogni colonna.</span><span class="sxs-lookup"><span data-stu-id="8fae4-287">We can see hello column names, hello R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="8fae4-288">Questo stesso output di stampa è facilmente disponibile hello output dispositivo R di hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-288">This same printed output is conveniently available from hello R Device output of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="8fae4-289">Si parlerà di output di hello di hello [Execute R Script] [ execute-r-script] modulo nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-289">We will discuss hello outputs of hello [Execute R Script][execute-r-script] module in hello next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="8fae4-290">Dataset2</span><span class="sxs-lookup"><span data-stu-id="8fae4-290">Dataset2</span></span>
<span data-ttu-id="8fae4-291">Hello comportamento dell'input hello Dataset2 è identica toothat di Dataset1.</span><span class="sxs-lookup"><span data-stu-id="8fae4-291">hello behavior of hello Dataset2 input is identical toothat of Dataset1.</span></span> <span data-ttu-id="8fae4-292">Consente infatti di passare nel codice R creato una seconda tabella rettangolare di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="8fae4-293">funzione Hello `maml.mapInputPort(2)`, con argomento hello 2, viene utilizzato toopass questi dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-293">hello function `maml.mapInputPort(2)`, with hello argument 2, is used toopass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="8fae4-294">Output del modulo Execute R Script</span><span class="sxs-lookup"><span data-stu-id="8fae4-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="8fae4-295">Output di un frame di dati</span><span class="sxs-lookup"><span data-stu-id="8fae4-295">Output a dataframe</span></span>
<span data-ttu-id="8fae4-296">È possibile creare contenuto hello di un frame di dati R come una tabella tramite la porta hello Dataset1 risultati rettangolare utilizzando hello `maml.mapOutputPort()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="8fae4-296">You can output hello contents of an R dataframe as a rectangular table through hello Result Dataset1 port by using hello `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="8fae4-297">Viene eseguita da hello successiva riga nello script R semplice.</span><span class="sxs-lookup"><span data-stu-id="8fae4-297">In our simple R script this is performed by hello following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="8fae4-298">Dopo aver esperimento hello in esecuzione, fare clic su una porta di output risultati Dataset1 hello e quindi fare clic su **Visualizza**.</span><span class="sxs-lookup"><span data-stu-id="8fae4-298">After running hello experiment, click on hello Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="8fae4-299">I risultati dovrebbero essere simili a quanto visualizzato nella Figura 6.</span><span class="sxs-lookup"><span data-stu-id="8fae4-299">You should see something like Figure 6.</span></span>

![visualizzazione di Hello dell'output di hello di dati per California hello][7]

<span data-ttu-id="8fae4-301">*Figura 6. visualizzazione di Hello dell'output di hello di hello dati per California.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-301">*Figure 6. hello visualization of hello output of hello California dairy data.*</span></span>

<span data-ttu-id="8fae4-302">Questo output è input toohello identici, esattamente come è previsto.</span><span class="sxs-lookup"><span data-stu-id="8fae4-302">This output looks identical toohello input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="8fae4-303">Output R Device</span><span class="sxs-lookup"><span data-stu-id="8fae4-303">R Device output</span></span>
<span data-ttu-id="8fae4-304">output di dispositivo di hello Hello [Execute R Script] [ execute-r-script] modulo contiene i messaggi e output della grafica.</span><span class="sxs-lookup"><span data-stu-id="8fae4-304">hello Device output of hello [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="8fae4-305">Messaggi di errore standard e di output standard da R vengono inviati toohello R Device porta di output.</span><span class="sxs-lookup"><span data-stu-id="8fae4-305">Both standard output and standard error messages from R are sent toohello R Device output port.</span></span>  

<span data-ttu-id="8fae4-306">hello tooview R dispositivo di output, fare clic sulla porta hello e quindi su **Visualizza**.</span><span class="sxs-lookup"><span data-stu-id="8fae4-306">tooview hello R Device output, click on hello port and then on **Visualize**.</span></span> <span data-ttu-id="8fae4-307">Viene illustrato l'output di hello standard e l'errore standard dallo script R hello nella figura 7.</span><span class="sxs-lookup"><span data-stu-id="8fae4-307">We see hello standard output and standard error from hello R script in Figure 7.</span></span>

![Output standard e l'errore standard da hello porta dispositivo R][8]

<span data-ttu-id="8fae4-309">*Figura 7. Output standard e l'errore standard da hello porta dispositivo R.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-309">*Figure 7. Standard output and standard error from hello R Device port.*</span></span>

<span data-ttu-id="8fae4-310">Scorrendo verso il basso è visualizzato l'output grafico hello script R nella figura 8.</span><span class="sxs-lookup"><span data-stu-id="8fae4-310">Scrolling down we see hello graphics output from our R script in Figure 8.</span></span>  

![Output di grafica da hello porta dispositivo R][9]

<span data-ttu-id="8fae4-312">*Figura 8. L'output di hello porta R dispositivo di grafica.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-312">*Figure 8. Graphics output from hello R Device port.*</span></span>  

## <span data-ttu-id="8fae4-313"><a id="filtering"></a>Filtraggio e trasformazione dei dati</span><span class="sxs-lookup"><span data-stu-id="8fae4-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="8fae4-314">In questa sezione verranno eseguiti alcuni filtro dei dati di base e operazioni di trasformazione in hello dati per California.</span><span class="sxs-lookup"><span data-stu-id="8fae4-314">In this section we will perform some basic data filtering and transformation operations on hello California dairy data.</span></span> <span data-ttu-id="8fae4-315">Completamento hello di questa sezione verrà abbiamo dati in un formato appropriato per la creazione di un modello analitico.</span><span class="sxs-lookup"><span data-stu-id="8fae4-315">By hello end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="8fae4-316">In particolare, in questa sezione vengono eseguite diverse attività comuni di pulizia e trasformazione dei dati: trasformazione del tipo, filtraggio nei frame di dati, aggiunta di nuove colonne elaborate e trasformazioni dei valori.</span><span class="sxs-lookup"><span data-stu-id="8fae4-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="8fae4-317">Lo sfondo consentono di gestire hello numerose variazioni rilevate in problemi reali.</span><span class="sxs-lookup"><span data-stu-id="8fae4-317">This background should help you deal with hello many variations encountered in real-world problems.</span></span>

<span data-ttu-id="8fae4-318">codice R completo Hello per questa sezione è disponibile nel file zip hello scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8fae4-318">hello complete R code for this section is available in hello zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="8fae4-319">Trasformazioni di tipi</span><span class="sxs-lookup"><span data-stu-id="8fae4-319">Type transformations</span></span>
<span data-ttu-id="8fae4-320">Ora che è possibile leggere i dati di hello California per codice hello R nel hello [Execute R Script] [ execute-r-script] modulo, è necessario che i dati di hello nelle colonne hello sono hello previsto tipo e il formato tooensure.</span><span class="sxs-lookup"><span data-stu-id="8fae4-320">Now that we can read hello California dairy data into hello R code in hello [Execute R Script][execute-r-script] module, we need tooensure that hello data in hello columns has hello intended type and format.</span></span>  

<span data-ttu-id="8fae4-321">R è un linguaggio tipizzato in modo dinamico, il che significa che i tipi di dati vengono assegnati forzatamente da uno tooanother come richiesto.</span><span class="sxs-lookup"><span data-stu-id="8fae4-321">R is a dynamically typed language, which means that data types are coerced from one tooanother as required.</span></span> <span data-ttu-id="8fae4-322">i tipi di dati atomic Hello in R includono numerici, logici e caratteri.</span><span class="sxs-lookup"><span data-stu-id="8fae4-322">hello atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="8fae4-323">tipo di fattore Hello è usato toocompactly archiviare i dati categorici.</span><span class="sxs-lookup"><span data-stu-id="8fae4-323">hello factor type is used toocompactly store categorical data.</span></span> <span data-ttu-id="8fae4-324">È possibile trovare molte più informazioni sui tipi di dati nei riferimenti hello in [appendice B - approfondimento](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="8fae4-324">You can find much more information on data types in hello references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="8fae4-325">Quando i dati in formato tabulare viene letto in R da un'origine esterna, è sempre un hello toocheck buona risultante tipi nelle colonne hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-325">When tabular data is read into R from an external source, it is always a good idea toocheck hello resulting types in hello columns.</span></span> <span data-ttu-id="8fae4-326">È possibile, ad esempio, che una colonna che sarebbe dovuta essere di tipo Char in realtà risulti di tipo fattore, o viceversa.</span><span class="sxs-lookup"><span data-stu-id="8fae4-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="8fae4-327">In altri casi, una colonna che si pensa debba essere numerica viene rappresentata da dati di tipo carattere, ad esempio '1,23' anziché 1,23 come numero a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="8fae4-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="8fae4-328">Fortunatamente, è facile tooconvert uno tooanother di tipo, purché il mapping è possibile.</span><span class="sxs-lookup"><span data-stu-id="8fae4-328">Fortunately, it is easy tooconvert one type tooanother, as long as mapping is possible.</span></span> <span data-ttu-id="8fae4-329">Ad esempio, non è possibile convertire 'Nevada' in un valore numerico, ma è possibile convertirlo tooa fattore (variabile categorica).</span><span class="sxs-lookup"><span data-stu-id="8fae4-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it tooa factor (categorical variable).</span></span> <span data-ttu-id="8fae4-330">Un valore numerico 1, invece, può essere convertito sia nel carattere "1" sia in un fattore.</span><span class="sxs-lookup"><span data-stu-id="8fae4-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="8fae4-331">sintassi di Hello per queste conversioni è semplice: `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="8fae4-331">hello syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="8fae4-332">Queste funzioni di conversione di tipo includono seguente hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-332">These type conversion functions include hello following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="8fae4-333">Esaminando i tipi di dati delle colonne di hello è di input nella sezione precedente hello hello: tutte le colonne sono di tipo numerico, ad eccezione di hello colonna con etichettata 'Month', che è di tipo carattere di tipo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-333">Looking at hello data types of hello columns we input in hello previous section: all columns are of type numeric, except for hello column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="8fae4-334">Di seguito convertire questo fattore tooa e hello risultati dei test.</span><span class="sxs-lookup"><span data-stu-id="8fae4-334">Let's convert this tooa factor and test hello results.</span></span>  

<span data-ttu-id="8fae4-335">Riga hello matrice scatterplot hello creato e aggiunto una linea di conversione tooa fattore di hello 'Month' colonna eliminato.</span><span class="sxs-lookup"><span data-stu-id="8fae4-335">I have deleted hello line that created hello scatterplot matrix and added a line converting hello 'Month' column tooa factor.</span></span> <span data-ttu-id="8fae4-336">In my esperimento verrà semplicemente tagliare e incollare il codice R hello nella finestra di codice hello di hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-336">In my experiment I will just cut and paste hello R code into hello code window of hello [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="8fae4-337">È inoltre possibile aggiornare il file zip hello e caricarlo tooAzure Machine Learning Studio, ma questo richiede diversi passaggi.</span><span class="sxs-lookup"><span data-stu-id="8fae4-337">You could also update hello zip file and upload it tooAzure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="8fae4-338">Consente di eseguire questo codice ed esaminare per hello script R i log di output di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-338">Let's execute this code and look at hello output log for hello R script.</span></span> <span data-ttu-id="8fae4-339">dati rilevanti Hello dal log hello sono illustrati nella figura 9.</span><span class="sxs-lookup"><span data-stu-id="8fae4-339">hello relevant data from hello log is shown in Figure 9.</span></span>

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="8fae4-340">*Figura 9. Riepilogo dei frame di dati di hello con una variabile di fattore.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-340">*Figure 9. Summary of hello dataframe with a factor variable.*</span></span>

<span data-ttu-id="8fae4-341">tipo di Hello per mese dovrebbe ora essere visualizzato '**fattore con 14 livelli**'.</span><span class="sxs-lookup"><span data-stu-id="8fae4-341">hello type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="8fae4-342">Si tratta di un problema, poiché esistono solo 12 mesi nell'anno hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-342">This is a problem since there are only 12 months in hello year.</span></span> <span data-ttu-id="8fae4-343">È inoltre possibile verificare toosee che tipo di hello in **Visualizza** di hello set di risultati è la porta '**Categorical**'.</span><span class="sxs-lookup"><span data-stu-id="8fae4-343">You can also check toosee that hello type in **Visualize** of hello Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="8fae4-344">problema di Hello è tale colonna non è stata codificata sistematicamente ' Month' hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-344">hello problem is that hello 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="8fae4-345">Un mese può essere denominato Aprile in alcuni casi e abbreviato in Apr. in altri. È possibile risolvere il problema, trimming too3 caratteri della stringa hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming hello string too3 characters.</span></span> <span data-ttu-id="8fae4-346">la riga Hello di codice è ora simile hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8fae4-346">hello line of code now looks like hello following:</span></span>

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="8fae4-347">Eseguire di nuovo esperimento hello e visualizzare il log di output di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-347">Rerun hello experiment and view hello output log.</span></span> <span data-ttu-id="8fae4-348">Hello previsto i risultati vengono visualizzati nella figura 10.</span><span class="sxs-lookup"><span data-stu-id="8fae4-348">hello expected results are shown in Figure 10.</span></span>  

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="8fae4-349">*Figura 10. Riepilogo dei frame di dati di hello con numero di livelli di fattore corretto.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-349">*Figure 10. Summary of hello dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="8fae4-350">La variabile di fattore dispone ora 12 livelli hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="8fae4-350">Our factor variable now has hello desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="8fae4-351">Filtraggio di frame di dati di base</span><span class="sxs-lookup"><span data-stu-id="8fae4-351">Basic data frame filtering</span></span>
<span data-ttu-id="8fae4-352">I frame di dati R supportano avanzate funzionalità di filtraggio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="8fae4-353">I set di dati, infatti, possono essere suddivisi in sottoinsiemi usando filtri logici su righe o colonne.</span><span class="sxs-lookup"><span data-stu-id="8fae4-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="8fae4-354">In molto casi, tuttavia, sono necessari complessi criteri di filtro.</span><span class="sxs-lookup"><span data-stu-id="8fae4-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="8fae4-355">fa riferimento a Hello in [appendice B - approfondimento](#appendixb) contengono esempi dettagliati di filtro frame di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-355">hello references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="8fae4-356">Possiamo eseguire semplici operazioni di filtraggio anche sul nostro set di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="8fae4-357">Se si osserva colonne hello hello cadairydata frame di dati, si noterà due colonne non necessarie.</span><span class="sxs-lookup"><span data-stu-id="8fae4-357">If you look at hello columns in hello cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="8fae4-358">prima colonna Hello contiene solo un numero di riga, non è molto utile.</span><span class="sxs-lookup"><span data-stu-id="8fae4-358">hello first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="8fae4-359">Hello seconda colonna, Year.Month, contiene le informazioni ridondanti.</span><span class="sxs-lookup"><span data-stu-id="8fae4-359">hello second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="8fae4-360">È possibile escludere facilmente queste colonne tramite hello seguente codice R.</span><span class="sxs-lookup"><span data-stu-id="8fae4-360">We can easily exclude these columns by using hello following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="8fae4-361">Da ora in questa sezione verrà semplicemente visualizzare si hello codice aggiuntivo che si sta aggiungendo in hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-361">From now on in this section, I will just show you hello additional code I am adding in hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="8fae4-362">Ogni nuova riga verranno aggiunte **prima** hello `str()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="8fae4-362">I will add each new line **before** hello `str()` function.</span></span> <span data-ttu-id="8fae4-363">Utilizzare questo tooverify funzione i risultati in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-363">I use this function tooverify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="8fae4-364">È possibile aggiungere hello seguente codice R toomy riga hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-364">I add hello following line toomy R code in hello [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="8fae4-365">Eseguire questo codice nell'esperimento e controllare il risultato di hello dal log di output di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-365">Run this code in your experiment and check hello result from hello output log.</span></span> <span data-ttu-id="8fae4-366">Questi risultati vengono mostrati nella Figura 11.</span><span class="sxs-lookup"><span data-stu-id="8fae4-366">These results are shown in Figure 11.</span></span>

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="8fae4-367">*Figura 11. Riepilogo dei frame di dati di hello con due colonne è stato rimosso.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-367">*Figure 11. Summary of hello dataframe with two columns removed.*</span></span>

<span data-ttu-id="8fae4-368">Ottime notizie!</span><span class="sxs-lookup"><span data-stu-id="8fae4-368">Good news!</span></span> <span data-ttu-id="8fae4-369">Si ottengono i risultati di hello previsto.</span><span class="sxs-lookup"><span data-stu-id="8fae4-369">We get hello expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="8fae4-370">Aggiungere una nuova colonna</span><span class="sxs-lookup"><span data-stu-id="8fae4-370">Add a new column</span></span>
<span data-ttu-id="8fae4-371">i modelli time series toocreate sarà utile toohave una colonna che contiene hello mesi dall'inizio di hello della serie temporale hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-371">toocreate time series models it will be convenient toohave a column containing hello months since hello start of hello time series.</span></span> <span data-ttu-id="8fae4-372">Creeremo quindi una nuova colonna denominata "Month.Count".</span><span class="sxs-lookup"><span data-stu-id="8fae4-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="8fae4-373">toohelp organizzare codice hello verrà creata la prima funzione semplice, `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="8fae4-373">toohelp organize hello code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="8fae4-374">Quindi si applicherà questa toocreate funzione una nuova colonna in hello frame di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-374">We will then apply this function toocreate a new column in hello dataframe.</span></span> <span data-ttu-id="8fae4-375">nuovo codice Hello è come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8fae4-375">hello new code is as follows.</span></span>

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="8fae4-376">Esegui esperimento hello aggiornato e utilizzare hello output log tooview hello risultati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-376">Now run hello updated experiment and use hello output log tooview hello results.</span></span> <span data-ttu-id="8fae4-377">I risultati previsti sono illustrati nella Figura 12.</span><span class="sxs-lookup"><span data-stu-id="8fae4-377">These results are shown in Figure 12.</span></span>

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="8fae4-378">*Figura 12. Riepilogo dei frame di dati di hello con la colonna aggiuntiva hello.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-378">*Figure 12. Summary of hello dataframe with hello additional column.*</span></span>

<span data-ttu-id="8fae4-379">Sembra che tutto stia funzionando perfettamente.</span><span class="sxs-lookup"><span data-stu-id="8fae4-379">It looks like everything is working.</span></span> <span data-ttu-id="8fae4-380">Abbiamo hello nuova colonna i valori previsti hello nel frame di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-380">We have hello new column with hello expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="8fae4-381">Trasformazioni di valori</span><span class="sxs-lookup"><span data-stu-id="8fae4-381">Value transformations</span></span>
<span data-ttu-id="8fae4-382">In questa sezione si eseguirà alcune trasformazioni semplici valori hello in alcune delle colonne hello il frame di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-382">In this section we will perform some simple transformations on hello values in some of hello columns of our dataframe.</span></span> <span data-ttu-id="8fae4-383">il linguaggio R Hello supporta le trasformazioni di valore quasi arbitrario.</span><span class="sxs-lookup"><span data-stu-id="8fae4-383">hello R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="8fae4-384">fa riferimento a Hello in [appendice B - approfondimento](#appendixb) contengono esempi di estensione.</span><span class="sxs-lookup"><span data-stu-id="8fae4-384">hello references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="8fae4-385">Se si esamina i valori hello nei riepiloghi di hello di questo frame di dati che verrà visualizzato un valore dispari qui.</span><span class="sxs-lookup"><span data-stu-id="8fae4-385">If you look at hello values in hello summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="8fae4-386">In California si produce più gelato che latte?</span><span class="sxs-lookup"><span data-stu-id="8fae4-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="8fae4-387">No, naturalmente, non come ciò non ha senso, sad come ciò potrebbe essere toosome noi amanti gelato.</span><span class="sxs-lookup"><span data-stu-id="8fae4-387">No, of course not, as this makes no sense, sad as this fact may be toosome of us ice cream lovers.</span></span> <span data-ttu-id="8fae4-388">unità di Hello sono diverse.</span><span class="sxs-lookup"><span data-stu-id="8fae4-388">hello units are different.</span></span> <span data-ttu-id="8fae4-389">prezzo Hello è espressa in unità di noi libbre, latte è espressa in unità di 1 milione libbre Stati Uniti, gelato è in unità pari a 1.000 ci vernice e fiocchi cheese è espressa in unità di 1.000 libbre Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="8fae4-389">hello price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="8fae4-390">Presupponendo un peso di gelato circa 6,5 libbre al gallone, si può facilmente hello tooconvert moltiplicazione questi valori in modo che siano tutti in unità uguale di 1.000 euro.</span><span class="sxs-lookup"><span data-stu-id="8fae4-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do hello multiplication tooconvert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="8fae4-391">Per il modello di previsione viene usato un modello moltiplicativo per le tendenze e l'adattamento stagionale dei dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="8fae4-392">Una trasformazione di log consente toouse un modello lineare, semplificando il processo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-392">A log transformation allows us toouse a linear model, simplifying this process.</span></span> <span data-ttu-id="8fae4-393">È possibile applicare una trasformazione log hello nella stessa funzione in cui viene applicato il moltiplicatore hello hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-393">We can apply hello log transformation in hello same function where hello multiplier is applied.</span></span>

<span data-ttu-id="8fae4-394">Nel seguente codice di hello, definire una nuova funzione `log.transform()`e applicarlo toohello righe contenenti valori numerici hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-394">In hello following code, I define a new function, `log.transform()`, and apply it toohello rows containing hello numerical values.</span></span> <span data-ttu-id="8fae4-395">Hello R `Map()` funzione è utilizzata tooapply hello `log.transform()` toohello funzione selezionate le colonne di hello frame di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-395">hello R `Map()` function is used tooapply hello `log.transform()` function toohello selected columns of hello dataframe.</span></span> <span data-ttu-id="8fae4-396">`Map()`è simile troppo`apply()` ma consente più di un elenco di funzione toohello argomenti.</span><span class="sxs-lookup"><span data-stu-id="8fae4-396">`Map()` is similar too`apply()` but allows for more than one list of arguments toohello function.</span></span> <span data-ttu-id="8fae4-397">Si noti che un elenco di moltiplicatori fornisce hello secondo argomento toohello `log.transform()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="8fae4-397">Note that a list of multipliers supplies hello second argument toohello `log.transform()` function.</span></span> <span data-ttu-id="8fae4-398">Hello `na.omit()` funzione viene utilizzata come un po' di pulizia tooensure non è mancante o valori non definiti in hello frame di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-398">hello `na.omit()` function is used as a bit of cleanup tooensure we do not have missing or undefined values in hello dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="8fae4-399">È presente un problema di bit in hello `log.transform()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="8fae4-399">There is quite a bit happening in hello `log.transform()` function.</span></span> <span data-ttu-id="8fae4-400">La maggior parte di questo codice è il controllo per individuare potenziali problemi con gli argomenti di hello o gestione delle eccezioni, che possono ancora verificarsi durante i calcoli di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-400">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="8fae4-401">Solo alcune righe di codice effettivamente hello calcoli.</span><span class="sxs-lookup"><span data-stu-id="8fae4-401">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="8fae4-402">obiettivo di Hello della programmazione difensivo hello è errore hello tooprevent di una singola funzione che impedisce l'elaborazione di continuare.</span><span class="sxs-lookup"><span data-stu-id="8fae4-402">hello goal of hello defensive programming is tooprevent hello failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="8fae4-403">Un errore improvviso in un'analisi di lunga durata può essere piuttosto frustrante per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="8fae4-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="8fae4-404">Questa situazione, l'impostazione predefinita, i valori restituiti devono essere scelte che limiteranno tooavoid danni toodownstream elaborazione.</span><span class="sxs-lookup"><span data-stu-id="8fae4-404">tooavoid this situation, default return values must be chosen that will limit damage toodownstream processing.</span></span> <span data-ttu-id="8fae4-405">Un messaggio è anche gli utenti tooalert prodotti che si sono verificato errato.</span><span class="sxs-lookup"><span data-stu-id="8fae4-405">A message is also produced tooalert users that something has gone wrong.</span></span>

<span data-ttu-id="8fae4-406">Se non si è programmatori toodefensive usati in R, tutto il codice può sembrare piuttosto complesso.</span><span class="sxs-lookup"><span data-stu-id="8fae4-406">If you are not used toodefensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="8fae4-407">Assiste passaggi principali hello:</span><span class="sxs-lookup"><span data-stu-id="8fae4-407">I will walk you through hello major steps:</span></span>

1. <span data-ttu-id="8fae4-408">Viene definito un vettore di quattro messaggi.</span><span class="sxs-lookup"><span data-stu-id="8fae4-408">A vector of four messages is defined.</span></span> <span data-ttu-id="8fae4-409">Questi messaggi sono utilizzati toocommunicate informazioni su alcuni dei possibili errori di hello e le eccezioni che possono verificarsi con questo codice.</span><span class="sxs-lookup"><span data-stu-id="8fae4-409">These messages are used toocommunicate information about some of hello possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="8fae4-410">Per ciascun caso restituirò il valore NA.</span><span class="sxs-lookup"><span data-stu-id="8fae4-410">I return a value of NA for each case.</span></span> <span data-ttu-id="8fae4-411">Esistono diverse altre possibilità che potrebbero avere un minor numero di effetti collaterali.</span><span class="sxs-lookup"><span data-stu-id="8fae4-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="8fae4-412">Potrebbe restituire un vettore di zeri o input originale, vettore di hello, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-412">I could return a vector of zeroes, or hello original input vector, for example.</span></span>
3. <span data-ttu-id="8fae4-413">Nella funzione di hello argomenti toohello vengono eseguiti i controlli.</span><span class="sxs-lookup"><span data-stu-id="8fae4-413">Checks are run on hello arguments toohello function.</span></span> <span data-ttu-id="8fae4-414">In ogni caso, se viene rilevato un errore, viene restituito un valore predefinito e viene generato un messaggio per hello `warning()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="8fae4-414">In each case, if an error is detected, a default value is returned and a message is produced by hello `warning()` function.</span></span> <span data-ttu-id="8fae4-415">Utilizzo di `warning()` anziché `stop()` come hello quest'ultimo verrà terminare l'esecuzione, esattamente ciò che si sta tentando di tooavoid.</span><span class="sxs-lookup"><span data-stu-id="8fae4-415">I am using `warning()` rather than `stop()` as hello latter will terminate execution, exactly what I am trying tooavoid.</span></span> <span data-ttu-id="8fae4-416">Osservare come abbia scritto questo codice in stile procedurale: un approccio funzionale sarebbe apparso in questo caso eccessivamente complesso e oscuro.</span><span class="sxs-lookup"><span data-stu-id="8fae4-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="8fae4-417">i calcoli di Hello log vengono eseguito il wrapping `tryCatch()` in modo che le eccezioni non causino tooprocessing un arresto improvviso.</span><span class="sxs-lookup"><span data-stu-id="8fae4-417">hello log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt tooprocessing.</span></span> <span data-ttu-id="8fae4-418">Senza `tryCatch()` , la maggior parte degli errori generati dalle funzioni R producono un segnale di arresto, che interrompe l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8fae4-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="8fae4-419">Eseguire questo codice R nell'esperimento e un'occhiata hello stampate output nel file di log hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-419">Execute this R code in your experiment and have a look at hello printed output in hello output.log file.</span></span> <span data-ttu-id="8fae4-420">È ora verranno visualizzati i valori di hello trasformato di hello quattro colonne in hello log, come illustrato nella figura 13.</span><span class="sxs-lookup"><span data-stu-id="8fae4-420">You will now see hello transformed values of hello four columns in hello log, as shown in Figure 13.</span></span>

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="8fae4-421">*Figura 13. Riepilogo di hello trasformati valori hello frame di dati.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-421">*Figure 13. Summary of hello transformed values in hello dataframe.*</span></span>

<span data-ttu-id="8fae4-422">È possibile notare i valori hello sono stati trasformati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-422">We see hello values have been transformed.</span></span> <span data-ttu-id="8fae4-423">La produzione di latte supera ora di gran lunga la produzione di tutti gli altri prodotti caseari, ricordandoci come si stia ora usando una scala logaritmica .</span><span class="sxs-lookup"><span data-stu-id="8fae4-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="8fae4-424">A questo punto i nostri dati sono puliti e siamo pronti per qualche operazione di modeling.</span><span class="sxs-lookup"><span data-stu-id="8fae4-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="8fae4-425">Osservando la visualizzazione di hello riepilogo per i set di risultati di output di hello nostri [Execute R Script] [ execute-r-script] modulo, si noterà colonna 'Month' hello è 'Categorie' con 12 valori univoci, nuovo, esattamente come si voleva .</span><span class="sxs-lookup"><span data-stu-id="8fae4-425">Looking at hello visualization summary for hello Result Dataset output of our [Execute R Script][execute-r-script] module, you will see hello 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="8fae4-426"><a id="timeseries"></a>Oggetti della serie temporale e analisi delle correlazioni</span><span class="sxs-lookup"><span data-stu-id="8fae4-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="8fae4-427">In questa sezione verrà alcuni oggetti serie tempo base di R di esplorare e analizzare le correlazioni hello tra alcune delle variabili di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-427">In this section we will explore a few basic R time series objects and analyze hello correlations between some of hello variables.</span></span> <span data-ttu-id="8fae4-428">L'obiettivo è toooutput un frame di dati contenente hello correlazione pairwise informazioni in diversi ritardi.</span><span class="sxs-lookup"><span data-stu-id="8fae4-428">Our goal is toooutput a dataframe containing hello pairwise correlation information at several lags.</span></span>

<span data-ttu-id="8fae4-429">codice R completo Hello per questa sezione è nel file zip hello scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8fae4-429">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="8fae4-430">Oggetti della serie temporale in R</span><span class="sxs-lookup"><span data-stu-id="8fae4-430">Time series objects in R</span></span>
<span data-ttu-id="8fae4-431">Come già accennato, le serie temporali sono costituite da una serie di valori di dati indicizzati per data e ora.</span><span class="sxs-lookup"><span data-stu-id="8fae4-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="8fae4-432">Oggetti della serie R vengono utilizzati toocreate e gestire un indice ora hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-432">R time series objects are used toocreate and manage hello time index.</span></span> <span data-ttu-id="8fae4-433">Esistono diversi vantaggi toousing serie oggetti.</span><span class="sxs-lookup"><span data-stu-id="8fae4-433">There are several advantages toousing time series objects.</span></span> <span data-ttu-id="8fae4-434">Oggetti della serie evitano di hello molti dettagli della gestione di hello serie indice i valori che sono incapsulati nell'oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-434">Time series objects free you from hello many details of managing hello time series index values that are encapsulated in hello object.</span></span> <span data-ttu-id="8fae4-435">Inoltre, oggetti di time series consentono toouse hello molti metodi di serie del tempo per il tracciato, stampa, modellazione e così via.</span><span class="sxs-lookup"><span data-stu-id="8fae4-435">In addition, time series objects allow you toouse hello many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="8fae4-436">classe serie in fase di POSIXct Hello viene comunemente utilizzato ed è relativamente semplice.</span><span class="sxs-lookup"><span data-stu-id="8fae4-436">hello POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="8fae4-437">Questa classe serie in fase di misura di tempo dall'inizio di hello del periodo di hello, 1 gennaio 1970.</span><span class="sxs-lookup"><span data-stu-id="8fae4-437">This time series class measures time from hello start of hello epoch, January 1, 1970.</span></span> <span data-ttu-id="8fae4-438">In questo esempio useremo quindi oggetti serie temporale di tipo POSIXct.</span><span class="sxs-lookup"><span data-stu-id="8fae4-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="8fae4-439">Altre classi di oggetti serie temporale comunemente usate in R includono zoo e xts, serie temporali estensibili.</span><span class="sxs-lookup"><span data-stu-id="8fae4-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="8fae4-440">Esempio di oggetto della serie temporale</span><span class="sxs-lookup"><span data-stu-id="8fae4-440">Time series object example</span></span>
<span data-ttu-id="8fae4-441">Iniziamo con il nostro esempio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-441">Let's get started with our example.</span></span> <span data-ttu-id="8fae4-442">Trascinare un **nuovo** modulo [Execute R Script][execute-r-script] nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="8fae4-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="8fae4-443">Connettere hello risultato Dataset1 porta di output di hello esistente [Execute R Script] [ execute-r-script] toohello modulo Dataset1 hello nuova porta di input [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-443">Connect hello Result Dataset1 output port of hello existing [Execute R Script][execute-r-script] module toohello Dataset1 input port of hello new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="8fae4-444">Come per gli esempi prima hello, come è stato di avanzamento tramite l'esempio hello, in alcuni momenti verrà hello solo incrementale ulteriori righe di codice R a ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-444">As I did for hello first examples, as we progress through hello example, at some points I will show only hello incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-hello-dataframe"></a><span data-ttu-id="8fae4-445">Lettura hello frame di dati</span><span class="sxs-lookup"><span data-stu-id="8fae4-445">Reading hello dataframe</span></span>
<span data-ttu-id="8fae4-446">Come primo passaggio, di lettura in un frame di dati e assicurarsi che si ottengono i risultati di hello previsto.</span><span class="sxs-lookup"><span data-stu-id="8fae4-446">As a first step, let's read in a dataframe and make sure we get hello expected results.</span></span> <span data-ttu-id="8fae4-447">Hello seguente il codice deve eseguire il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-447">hello following code should do hello job.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

<span data-ttu-id="8fae4-448">A questo punto, eseguire esperimento hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-448">Now, run hello experiment.</span></span> <span data-ttu-id="8fae4-449">log Hello della nuova forma di Execute R Script hello dovrebbe essere simile figura 14.</span><span class="sxs-lookup"><span data-stu-id="8fae4-449">hello log of hello new Execute R Script shape should look like Figure 14.</span></span>

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

<span data-ttu-id="8fae4-450">*Figura 14. Riepilogo dei frame di dati di hello nel modulo Execute R Script hello.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-450">*Figure 14. Summary of hello dataframe in hello Execute R Script module.*</span></span>

<span data-ttu-id="8fae4-451">Questi dati sono di tipi di hello previsto e formato.</span><span class="sxs-lookup"><span data-stu-id="8fae4-451">This data is of hello expected types and format.</span></span> <span data-ttu-id="8fae4-452">Notare che il fattore di tipo di colonna 'Month' hello e hello previsto è numero di livelli.</span><span class="sxs-lookup"><span data-stu-id="8fae4-452">Note that hello 'Month' column is of type factor and has hello expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="8fae4-453">Creazione di un oggetto della serie temporale</span><span class="sxs-lookup"><span data-stu-id="8fae4-453">Creating a time series object</span></span>
<span data-ttu-id="8fae4-454">È necessario tooadd un frame di dati tooour di oggetto serie di tempo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-454">We need tooadd a time series object tooour dataframe.</span></span> <span data-ttu-id="8fae4-455">Sostituire codice corrente hello con seguente hello, che aggiunge una nuova colonna della classe POSIXct.</span><span class="sxs-lookup"><span data-stu-id="8fae4-455">Replace hello current code with hello following, which adds a new column of class POSIXct.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

<span data-ttu-id="8fae4-456">A questo punto, controllare il Registro di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-456">Now, check hello log.</span></span> <span data-ttu-id="8fae4-457">Dovrebbe essere simile a quello riportato nella Figura 15.</span><span class="sxs-lookup"><span data-stu-id="8fae4-457">It should look like Figure 15.</span></span>

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

<span data-ttu-id="8fae4-458">*Figura 15. Riepilogo dei frame di dati di hello con un oggetto della serie.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-458">*Figure 15. Summary of hello dataframe with a time series object.*</span></span>

<span data-ttu-id="8fae4-459">Possiamo vedere da hello riepilogo che tale nuova colonna hello è in realtà di classe POSIXct.</span><span class="sxs-lookup"><span data-stu-id="8fae4-459">We can see from hello summary that hello new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-hello-data"></a><span data-ttu-id="8fae4-460">Esplorazione e la trasformazione dei dati hello</span><span class="sxs-lookup"><span data-stu-id="8fae4-460">Exploring and transforming hello data</span></span>
<span data-ttu-id="8fae4-461">Vediamo alcune delle variabili di hello in questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-461">Let's explore some of hello variables in this dataset.</span></span> <span data-ttu-id="8fae4-462">Una matrice scatterplot è tooproduce un modo efficace un rapido controllo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-462">A scatterplot matrix is a good way tooproduce a quick look.</span></span> <span data-ttu-id="8fae4-463">È sostituendo hello `str()` funzione nel codice R precedente hello con hello successiva riga.</span><span class="sxs-lookup"><span data-stu-id="8fae4-463">I am replacing hello `str()` function in hello previous R code with hello following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="8fae4-464">Eseguiamo il codice e vediamo cosa succede.</span><span class="sxs-lookup"><span data-stu-id="8fae4-464">Run this code and see what happens.</span></span> <span data-ttu-id="8fae4-465">tracciato di Hello prodotta alle hello porta dispositivo R dovrebbe essere simile figura 16.</span><span class="sxs-lookup"><span data-stu-id="8fae4-465">hello plot produced at hello R Device port should look like Figure 16.</span></span>

![Matrice del grafico a dispersione delle variabili selezionate][17]

<span data-ttu-id="8fae4-467">*Figura 16. Matrice del grafico a dispersione delle variabili selezionate.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="8fae4-468">È una struttura insolita relazioni hello tra queste variabili.</span><span class="sxs-lookup"><span data-stu-id="8fae4-468">There is some odd-looking structure in hello relationships between these variables.</span></span> <span data-ttu-id="8fae4-469">Ad esempio nasce da tendenze nei dati hello e da tabelle dei fatti hello che non è stato standardizzato variabili hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-469">Perhaps this arises from trends in hello data and from hello fact that we have not standardized hello variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="8fae4-470">Analisi delle correlazioni</span><span class="sxs-lookup"><span data-stu-id="8fae4-470">Correlation analysis</span></span>
<span data-ttu-id="8fae4-471">analisi di correlazione tooperform dobbiamo tooboth la tendenza e standardizzare le variabili di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-471">tooperform correlation analysis we need tooboth de-trend and standardize hello variables.</span></span> <span data-ttu-id="8fae4-472">È possibile usare semplicemente hello R `scale()` (funzione), che consente di centrare e ridimensiona le variabili.</span><span class="sxs-lookup"><span data-stu-id="8fae4-472">We could simply use hello R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="8fae4-473">e può essere eseguita più velocemente.</span><span class="sxs-lookup"><span data-stu-id="8fae4-473">This function might well run faster.</span></span> <span data-ttu-id="8fae4-474">Tuttavia, si desidera tooshow è riportato un esempio di programmazione dei difensivo in R.</span><span class="sxs-lookup"><span data-stu-id="8fae4-474">However, I want tooshow you an example of defensive programing in R.</span></span>

<span data-ttu-id="8fae4-475">Hello `ts.detrend()` funzione illustrata di seguito esegue entrambe queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="8fae4-475">hello `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="8fae4-476">Hello due righe di codice seguenti deallocare tendenza dati hello e quindi standardizzare i valori hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-476">hello following two lines of code de-trend hello data and then standardize hello values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="8fae4-477">È presente un problema di bit in hello `ts.detrend()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="8fae4-477">There is quite a bit happening in hello `ts.detrend()` function.</span></span> <span data-ttu-id="8fae4-478">La maggior parte di questo codice è il controllo per individuare potenziali problemi con gli argomenti di hello o gestione delle eccezioni, che possono ancora verificarsi durante i calcoli di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-478">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="8fae4-479">Solo alcune righe di codice effettivamente hello calcoli.</span><span class="sxs-lookup"><span data-stu-id="8fae4-479">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="8fae4-480">Un esempio di programmazione difensiva è già stato illustrato in [Trasformazioni di valori](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="8fae4-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="8fae4-481">Entrambi i blocchi di calcolo vengono inclusi in `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="8fae4-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="8fae4-482">Per alcuni errori effettua vettore input originale hello senso tooreturn e in altri casi, restituisce un vettore di zeri.</span><span class="sxs-lookup"><span data-stu-id="8fae4-482">For some errors it makes sense tooreturn hello original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="8fae4-483">Si noti che la regressione lineare hello utilizzata per la tendenza una regressione serie di tempo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-483">Note that hello linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="8fae4-484">variabile predittiva Hello è un oggetto della serie.</span><span class="sxs-lookup"><span data-stu-id="8fae4-484">hello predictor variable is a time series object.</span></span>  

<span data-ttu-id="8fae4-485">Una volta `ts.detrend()` è definito si applicano variabili toohello di interesse per il frame di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-485">Once `ts.detrend()` is defined we apply it toohello variables of interest in our dataframe.</span></span> <span data-ttu-id="8fae4-486">È necessario forzare l'elenco risultante di hello creato da `lapply()` toodata frame di dati tramite `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="8fae4-486">We must coerce hello resulting list created by `lapply()` toodata dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="8fae4-487">A causa di aspetti difensivo `ts.detrend()`, tooprocess di errore non impedirà a una delle variabili di hello corretta elaborazione di hello ad altri utenti.</span><span class="sxs-lookup"><span data-stu-id="8fae4-487">Because of defensive aspects of `ts.detrend()`, failure tooprocess one of hello variables will not prevent correct processing of hello others.</span></span>  

<span data-ttu-id="8fae4-488">riga finale di Hello di codice crea un scatterplot pairwise.</span><span class="sxs-lookup"><span data-stu-id="8fae4-488">hello final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="8fae4-489">Dopo l'esecuzione di codice hello R, i risultati di hello di hello scatterplot sono illustrati nella figura 17.</span><span class="sxs-lookup"><span data-stu-id="8fae4-489">After running hello R code, hello results of hello scatterplot are shown in Figure 17.</span></span>

![Grafico a dispersione pairwise della serie temporale detrendizzata e standardizzata][18]

<span data-ttu-id="8fae4-491">*Figura 17. Grafico a dispersione pairwise della serie temporale detrendizzata e standardizzata.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="8fae4-492">È possibile confrontare questi toothose risultati illustrato nella figura 16.</span><span class="sxs-lookup"><span data-stu-id="8fae4-492">You can compare these results toothose shown in Figure 16.</span></span> <span data-ttu-id="8fae4-493">Con hello tendenza rimosso e hello variabili standardizzate, vediamo molto meno strutturato nelle relazioni di hello tra queste variabili.</span><span class="sxs-lookup"><span data-stu-id="8fae4-493">With hello trend removed and hello variables standardized, we see a lot less structure in hello relationships between these variables.</span></span>

<span data-ttu-id="8fae4-494">Hello codice toocompute hello set correlazioni come oggetti ccf R è come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8fae4-494">hello code toocompute hello correlations as R ccf objects is as follows.</span></span>

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="8fae4-495">Esecuzione del codice genera log hello illustrato nella figura 18.</span><span class="sxs-lookup"><span data-stu-id="8fae4-495">Running this code produces hello log shown in Figure 18.</span></span>

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

<span data-ttu-id="8fae4-496">*Figura 18. Elenco di ccf oggetti dall'analisi di correlazione pairwise hello.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-496">*Figure 18. List of ccf objects from hello pairwise correlation analysis.*</span></span>

<span data-ttu-id="8fae4-497">Per ogni intervallo è presente un valore di correlazione.</span><span class="sxs-lookup"><span data-stu-id="8fae4-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="8fae4-498">Nessuno di questi valori di correlazione è sufficientemente grande toobe significativo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-498">None of these correlation values is large enough toobe significant.</span></span> <span data-ttu-id="8fae4-499">Possiamo quindi concludere che ciascuna variabile può essere modellata in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="8fae4-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="8fae4-500">Output di un frame di dati</span><span class="sxs-lookup"><span data-stu-id="8fae4-500">Output a dataframe</span></span>
<span data-ttu-id="8fae4-501">È stato calcolato correlazioni pairwise hello come un elenco di oggetti R ccf.</span><span class="sxs-lookup"><span data-stu-id="8fae4-501">We have computed hello pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="8fae4-502">Questa operazione presenta un bit di un problema come porta di output di set di risultati hello necessita di un frame di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-502">This presents a bit of a problem as hello Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="8fae4-503">Inoltre, oggetto ccf hello è a sua volta un elenco e si vuole solo i valori hello nell'elemento di primo hello di questo elenco, correlazioni hello in hello ritardi diversi.</span><span class="sxs-lookup"><span data-stu-id="8fae4-503">Further, hello ccf object is itself a list and we want only hello values in hello first element of this list, hello correlations at hello various lags.</span></span>

<span data-ttu-id="8fae4-504">Hello seguenti valori di ritardo hello estratti di codice dall'elenco di hello di oggetti ccf, che sono a loro volta gli elenchi.</span><span class="sxs-lookup"><span data-stu-id="8fae4-504">hello following code extracts hello lag values from hello list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="8fae4-505">Hello prima riga di codice è difficile e alcune spiegazioni possono aiutarti a capire.</span><span class="sxs-lookup"><span data-stu-id="8fae4-505">hello first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="8fae4-506">Partendo dall'interno hello abbiamo seguente hello:</span><span class="sxs-lookup"><span data-stu-id="8fae4-506">Working from hello inside out we have hello following:</span></span>

1. <span data-ttu-id="8fae4-507">Hello '**[[**'operator con argomento hello'**1**' Seleziona hello vettore di correlazioni a ritardi hello dal primo elemento di hello hello ccf elenco di oggetti.</span><span class="sxs-lookup"><span data-stu-id="8fae4-507">hello '**[[**' operator with hello argument '**1**' selects hello vector of correlations at hello lags from hello first element of hello ccf object list.</span></span>
2. <span data-ttu-id="8fae4-508">Hello `do.call()` funzione applica hello `rbind()` funzione degli elementi dell'elenco di hello di hello restituisce eseguendo `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="8fae4-508">hello `do.call()` function applies hello `rbind()` function over hello elements of hello list returns by `lapply()`.</span></span>
3. <span data-ttu-id="8fae4-509">Hello `data.frame()` funzione assegna il risultato di hello prodotto da `do.call()` tooa frame di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-509">hello `data.frame()` function coerces hello result produced by `do.call()` tooa dataframe.</span></span>

<span data-ttu-id="8fae4-510">Si noti che i nomi di riga hello in una colonna di hello frame di dati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-510">Note that hello row names are in a column of hello dataframe.</span></span> <span data-ttu-id="8fae4-511">In questo modo consente di mantenere i nomi di riga hello quando vengono restituiti da hello [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="8fae4-511">Doing so preserves hello row names when they are output from hello [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="8fae4-512">Esecuzione di codice hello produce l'output di hello mostrato nella figura 19 quando si **Visualizza** hello output hello porta set di risultati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-512">Running hello code produces hello output shown in Figure 19 when I **Visualize** hello output at hello Result Dataset port.</span></span> <span data-ttu-id="8fae4-513">i nomi di riga Hello sono nella prima colonna hello, come previsto.</span><span class="sxs-lookup"><span data-stu-id="8fae4-513">hello row names are in hello first column, as intended.</span></span>

![Output dei risultati dall'analisi di correlazione hello][20]

<span data-ttu-id="8fae4-515">*Figura 19. Risultati di output dall'analisi di correlazione hello.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-515">*Figure 19. Results output from hello correlation analysis.*</span></span>

## <span data-ttu-id="8fae4-516"><a id="seasonalforecasting"></a>Esempio di serie temporale: previsione stagionale</span><span class="sxs-lookup"><span data-stu-id="8fae4-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="8fae4-517">I dati sono ora in un formato adatto per l'analisi e abbiamo determinato che non esistono significative correlazioni tra le variabili di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between hello variables.</span></span> <span data-ttu-id="8fae4-518">Passiamo quindi alla creazione di un modello di previsione in serie temporale,</span><span class="sxs-lookup"><span data-stu-id="8fae4-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="8fae4-519">Utilizzando questo modello è verrà prevedere la produzione di latte California per hello di 2013 12 mesi.</span><span class="sxs-lookup"><span data-stu-id="8fae4-519">Using this model we will forecast California milk production for hello 12 months of 2013.</span></span>

<span data-ttu-id="8fae4-520">Il nostro modello previsionale sarà costituito da due componenti: trend e stagionale.</span><span class="sxs-lookup"><span data-stu-id="8fae4-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="8fae4-521">previsione completo Hello è prodotto hello di questi due componenti.</span><span class="sxs-lookup"><span data-stu-id="8fae4-521">hello complete forecast is hello product of these two components.</span></span> <span data-ttu-id="8fae4-522">Questo tipo di modello prende il nome di modello moltiplicativo,</span><span class="sxs-lookup"><span data-stu-id="8fae4-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="8fae4-523">In alternativa Hello è un modello di addizione.</span><span class="sxs-lookup"><span data-stu-id="8fae4-523">hello alternative is an additive model.</span></span> <span data-ttu-id="8fae4-524">Abbiamo già applicate variabili registro trasformazione toohello di interesse, rendendo questa analisi gestibile.</span><span class="sxs-lookup"><span data-stu-id="8fae4-524">We have already applied a log transformation toohello variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="8fae4-525">codice R completo Hello per questa sezione è nel file zip hello scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8fae4-525">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="creating-hello-dataframe-for-analysis"></a><span data-ttu-id="8fae4-526">Creazione di hello frame di dati per l'analisi</span><span class="sxs-lookup"><span data-stu-id="8fae4-526">Creating hello dataframe for analysis</span></span>
<span data-ttu-id="8fae4-527">Per iniziare, aggiungere un **nuova** [Execute R Script] [ execute-r-script] esperimento tooyour modulo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-527">Start by adding a **new** [Execute R Script][execute-r-script] module tooyour experiment.</span></span> <span data-ttu-id="8fae4-528">Connettersi hello **set di risultati** output di hello esistente [Execute R Script] [ execute-r-script] modulo toohello **Dataset1** input del nuovo modulo hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-528">Connect hello **Result Dataset** output of hello existing [Execute R Script][execute-r-script] module toohello **Dataset1** input of hello new module.</span></span> <span data-ttu-id="8fae4-529">risultato Hello dovrebbe essere simile alla figura 20.</span><span class="sxs-lookup"><span data-stu-id="8fae4-529">hello result should look something like Figure 20.</span></span>

![Hello sperimentare hello nuovo Execute R Script modulo aggiunto][21]

<span data-ttu-id="8fae4-531">*Figura 20. Hello sperimentare dal modulo Execute R Script nuovo hello aggiunto.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-531">*Figure 20. hello experiment with hello new Execute R Script module added.*</span></span>

<span data-ttu-id="8fae4-532">Come con l'analisi di correlazione hello che è completati, è necessario tooadd una colonna con un oggetto della serie POSIXct.</span><span class="sxs-lookup"><span data-stu-id="8fae4-532">As with hello correlation analysis we just completed, we need tooadd a column with a POSIXct time series object.</span></span> <span data-ttu-id="8fae4-533">Hello seguente codice verrà eseguita solo questo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-533">hello following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="8fae4-534">Eseguire il codice ed esaminare i log di hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-534">Run this code and look at hello log.</span></span> <span data-ttu-id="8fae4-535">risultato Hello dovrebbe essere simile figura 21.</span><span class="sxs-lookup"><span data-stu-id="8fae4-535">hello result should look like Figure 21.</span></span>

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

<span data-ttu-id="8fae4-536">*Figura 21. Un riepilogo dei frame di dati hello.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-536">*Figure 21. A summary of hello dataframe.*</span></span>

<span data-ttu-id="8fae4-537">Con questo risultato, siamo toostart pronto l'analisi.</span><span class="sxs-lookup"><span data-stu-id="8fae4-537">With this result, we are ready toostart our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="8fae4-538">Creare un set di dati di training</span><span class="sxs-lookup"><span data-stu-id="8fae4-538">Create a training dataset</span></span>
<span data-ttu-id="8fae4-539">Con i frame di dati hello costruito dobbiamo toocreate un set di dati di training.</span><span class="sxs-lookup"><span data-stu-id="8fae4-539">With hello dataframe constructed we need toocreate a training dataset.</span></span> <span data-ttu-id="8fae4-540">Questi dati verranno incluse tutte le osservazioni hello ad eccezione del fatto hello ultime 12, dell'anno hello 2013, ovvero il set di dati di test.</span><span class="sxs-lookup"><span data-stu-id="8fae4-540">This data will include all of hello observations except hello last 12, of hello year 2013, which is our test dataset.</span></span> <span data-ttu-id="8fae4-541">esempio Hello subset hello frame di dati del codice e crea i tracciati delle variabili di produzione e il prezzo per hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-541">hello following code subsets hello dataframe and creates plots of hello dairy production and price variables.</span></span> <span data-ttu-id="8fae4-542">Quindi creare grafici di hello quattro variabili di produzione e prezzo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-542">I then create plots of hello four production and price variables.</span></span> <span data-ttu-id="8fae4-543">Una funzione anonima viene utilizzato toodefine alcuni consente per i grafici e quindi scorrere elenco hello di hello altri due argomenti con `Map()`.</span><span class="sxs-lookup"><span data-stu-id="8fae4-543">An anonymous function is used toodefine some augments for plot, and then iterate over hello list of hello other two arguments with `Map()`.</span></span> <span data-ttu-id="8fae4-544">Se pensate che un ciclo For sarebbe stato appropriato, avete ragione.</span><span class="sxs-lookup"><span data-stu-id="8fae4-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="8fae4-545">Tuttavia, poiché R è un linguaggio funzionale, adotterò un approccio funzionale.</span><span class="sxs-lookup"><span data-stu-id="8fae4-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="8fae4-546">L'esecuzione di codice hello produce hello serie di serie temporale è rappresentata dall'output di hello dispositivo R illustrato nella figura 22.</span><span class="sxs-lookup"><span data-stu-id="8fae4-546">Running hello code produces hello series of time series plots from hello R Device output shown in Figure 22.</span></span> <span data-ttu-id="8fae4-547">Si noti che asse temporale hello è espressa in unità di date, un vantaggio del tempo di hello serie tracciare metodo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-547">Note that hello time axis is in units of dates, a nice benefit of hello time series plot method.</span></span>

![Primo tracciato della serie temporale della produzione casearia in California e dei dati sui prezzi](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Secondo tracciato della serie temporale della produzione casearia in California e dei dati sui prezzi](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Terzo tracciato della serie temporale della produzione casearia in California e dei dati sui prezzi](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Quarto tracciato della serie temporale della produzione casearia in California e dei dati sui prezzi](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="8fae4-552">*Figura 22. Tracciati della serie temporale della produzione casearia in California e dei dati sui prezzi.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="8fae4-553">Modello di tendenza</span><span class="sxs-lookup"><span data-stu-id="8fae4-553">A trend model</span></span>
<span data-ttu-id="8fae4-554">Dopo aver creato un oggetto di time series e avere esaminato i dati di hello, iniziamo tooconstruct un modello di tendenza per hello dati di produzione di latte California.</span><span class="sxs-lookup"><span data-stu-id="8fae4-554">Having created a time series object and having had a look at hello data, let's start tooconstruct a trend model for hello California milk production data.</span></span> <span data-ttu-id="8fae4-555">A questo scopo, usiamo una regressione in serie temporale.</span><span class="sxs-lookup"><span data-stu-id="8fae4-555">We can do this with a time series regression.</span></span> <span data-ttu-id="8fae4-556">Tuttavia, è evidente in base al tracciato hello che si sarà necessario più di un tooaccurately pendenza e intercetta modello hello osservato tendenza nei dati di training hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-556">However, it is clear from hello plot that we will need more than a slope and intercept tooaccurately model hello observed trend in hello training data.</span></span>

<span data-ttu-id="8fae4-557">Dato su scala ridotta hello dei dati di hello, si verrà compilare hello modello per la tendenza di RStudio e quindi copia e Incolla modello risultante hello in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8fae4-557">Given hello small scale of hello data, I will build hello model for trend in RStudio and then cut and paste hello resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="8fae4-558">RStudio fornisce infatti un ambiente interattivo adatto a questo tipo di analisi interattiva.</span><span class="sxs-lookup"><span data-stu-id="8fae4-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="8fae4-559">Come primo tentativo, si passerà una regressione polinomiale con accensione too3.</span><span class="sxs-lookup"><span data-stu-id="8fae4-559">As a first attempt, I will try a polynomial regression with powers up too3.</span></span> <span data-ttu-id="8fae4-560">Esiste un pericolo reale di overfitting per questi tipi di modelli.</span><span class="sxs-lookup"><span data-stu-id="8fae4-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="8fae4-561">È pertanto termini di ordine superiore tooavoid migliore.</span><span class="sxs-lookup"><span data-stu-id="8fae4-561">Therefore, it is best tooavoid high order terms.</span></span> <span data-ttu-id="8fae4-562">Hello `I()` funzione impedisce l'interpretazione del contenuto di hello (interpreta contenuto hello 'così com'è") e consente una funzione interpretata letteralmente toowrite in un'equazione di regressione.</span><span class="sxs-lookup"><span data-stu-id="8fae4-562">hello `I()` function inhibits interpretation of hello contents (interprets hello contents 'as is') and allows you toowrite a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="8fae4-563">Questo genera l'errore seguente hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-563">This generates hello following.</span></span>

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

<span data-ttu-id="8fae4-564">Dai valori di P (Pr (> | t |)) nell'output, possiamo vedere che hello termine al quadrato potrebbe non essere significativo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-564">From P values (Pr(>|t|)) in this output, we can see that hello squared term may not be significant.</span></span> <span data-ttu-id="8fae4-565">Si utilizzerà hello `update()` funzione toomodify questo modello da hello di eliminazione al quadrato termine.</span><span class="sxs-lookup"><span data-stu-id="8fae4-565">I will use hello `update()` function toomodify this model by dropping hello squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="8fae4-566">Questo genera l'errore seguente hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-566">This generates hello following.</span></span>

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

<span data-ttu-id="8fae4-567">L'aspetto è decisamente migliore adesso.</span><span class="sxs-lookup"><span data-stu-id="8fae4-567">This looks better.</span></span> <span data-ttu-id="8fae4-568">Tutti i termini di hello sono significativi.</span><span class="sxs-lookup"><span data-stu-id="8fae4-568">All of hello terms are significant.</span></span> <span data-ttu-id="8fae4-569">Tuttavia, il valore di 2e-16 hello è un valore predefinito e non deve essere eseguito troppo grave.</span><span class="sxs-lookup"><span data-stu-id="8fae4-569">However, hello 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="8fae4-570">Come un test di integrità, questo punto, eseguire il tracciato di serie tempo dei dati di produzione per California hello con curva tendenza hello illustrata.</span><span class="sxs-lookup"><span data-stu-id="8fae4-570">As a sanity test, let's make a time series plot of hello California dairy production data with hello trend curve shown.</span></span> <span data-ttu-id="8fae4-571">Ho aggiunto hello seguente di codice in Azure Machine Learning hello [Execute R Script] [ execute-r-script] toocreate modello (non RStudio) hello modello ed effettuare un tracciato.</span><span class="sxs-lookup"><span data-stu-id="8fae4-571">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) toocreate hello model and make a plot.</span></span> <span data-ttu-id="8fae4-572">il risultato di Hello è illustrato nella figura 23.</span><span class="sxs-lookup"><span data-stu-id="8fae4-572">hello result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Dati sulla produzione di latte in California con il modello di tendenza visualizzato](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="8fae4-574">*Figura 23. Dati sulla produzione di latte in California con il modello di tendenza visualizzato.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="8fae4-575">Sembra che il modello di tendenza hello adatta dati hello abbastanza bene.</span><span class="sxs-lookup"><span data-stu-id="8fae4-575">It looks like hello trend model fits hello data fairly well.</span></span> <span data-ttu-id="8fae4-576">Inoltre, non sembra toobe evidenza di adattamento in eccesso, ad esempio si deforma dispari nella curva modello hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-576">Further, there does not seem toobe evidence of over-fitting, such as odd wiggles in hello model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="8fae4-577">Modello con stagionalità</span><span class="sxs-lookup"><span data-stu-id="8fae4-577">Seasonal model</span></span>
<span data-ttu-id="8fae4-578">Con un modello di tendenza in mano, è necessario toopush in e gli effetti stagionali hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-578">With a trend model in hand, we need toopush on and include hello seasonal effects.</span></span> <span data-ttu-id="8fae4-579">Si utilizzerà il mese di hello hello anno come una variabile fittizia attivo di hello modello lineare toocapture hello mese per mese.</span><span class="sxs-lookup"><span data-stu-id="8fae4-579">We will use hello month of hello year as a dummy variable in hello linear model toocapture hello month-by-month effect.</span></span> <span data-ttu-id="8fae4-580">Si noti che quando si introducono le variabili di fattore in un modello, intercetta hello necessario non è stato calcolato.</span><span class="sxs-lookup"><span data-stu-id="8fae4-580">Note that when you introduce factor variables into a model, hello intercept must not be computed.</span></span> <span data-ttu-id="8fae4-581">Se non eseguire questa operazione, formula hello è eccessiva specificato e R eliminerà uno di hello desiderato fattori ma mantenere il termine di intercept hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-581">If you do not do this, hello formula is over-specified and R will drop one of hello desired factors but keep hello intercept term.</span></span>

<span data-ttu-id="8fae4-582">Poiché si dispone di un modello di tendenza soddisfacenti, è possibile utilizzare hello `update()` hello tooadd funzione nuovi termini toohello di modello esistente.</span><span class="sxs-lookup"><span data-stu-id="8fae4-582">Since we have a satisfactory trend model we can use hello `update()` function tooadd hello new terms toohello existing model.</span></span> <span data-ttu-id="8fae4-583">Hello -1 nella formula di aggiornamento hello Elimina termine intercetta hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-583">hello -1 in hello update formula drops hello intercept term.</span></span> <span data-ttu-id="8fae4-584">Continuare a RStudio per il momento hello:</span><span class="sxs-lookup"><span data-stu-id="8fae4-584">Continuing in RStudio for hello moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="8fae4-585">Questo genera l'errore seguente hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-585">This generates hello following.</span></span>

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

<span data-ttu-id="8fae4-586">Vediamo che hello e del modello di non è più un termine di intercept ha fattori significativi mese 12.</span><span class="sxs-lookup"><span data-stu-id="8fae4-586">We see that hello model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="8fae4-587">Questo è esattamente ciò che si voleva toosee.</span><span class="sxs-lookup"><span data-stu-id="8fae4-587">This is exactly what we wanted toosee.</span></span>

<span data-ttu-id="8fae4-588">Verifichiamo un altro tracciato di serie di tempo di hello California produzione per dati toosee funziona bene modello stagionali hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-588">Let's make another time series plot of hello California dairy production data toosee how well hello seasonal model is working.</span></span> <span data-ttu-id="8fae4-589">Ho aggiunto hello seguente di codice in Azure Machine Learning hello [Execute R Script] [ execute-r-script] toocreate hello modello ed effettuare un tracciato.</span><span class="sxs-lookup"><span data-stu-id="8fae4-589">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] toocreate hello model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="8fae4-590">Esecuzione del codice in Azure Machine Learning genera tracciato hello illustrato nella figura 24.</span><span class="sxs-lookup"><span data-stu-id="8fae4-590">Running this code in Azure Machine Learning produces hello plot shown in Figure 24.</span></span>

![Produzione di latte in California con un modello che include gli effetti stagionali](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="8fae4-592">*Figura 24. Produzione di latte in California con un modello che include gli effetti stagionali.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="8fae4-593">Hello toohello adatta dati illustrati nella figura 24 sono piuttosto incoraggianti.</span><span class="sxs-lookup"><span data-stu-id="8fae4-593">hello fit toohello data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="8fae4-594">L'aspetto ragionevole sia tendenza hello e stagionali hello (variazione mensile).</span><span class="sxs-lookup"><span data-stu-id="8fae4-594">Both hello trend and hello seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="8fae4-595">Come un altro controllo sul nostro modello, si hanno un'occhiata residui hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-595">As another check on our model, let's have a look at hello residuals.</span></span> <span data-ttu-id="8fae4-596">Hello calcola di codice seguente hello valori stimati tra i due modelli, consente di calcolare residui hello per modello stagionali hello e quindi vengono tracciati tali residui per i dati di training hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-596">hello following code computes hello predicted values from our two models, computes hello residuals for hello seasonal model, and then plots these residuals for hello training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="8fae4-597">tracciato residuo Hello è illustrato nella figura 25.</span><span class="sxs-lookup"><span data-stu-id="8fae4-597">hello residual plot is shown in Figure 25.</span></span>

![Residui del modello di stagionali hello per dati di training hello](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="8fae4-599">*Figura 25. Residui del modello di stagionali hello per dati di training hello.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-599">*Figure 25. Residuals of hello seasonal model for hello training data.*</span></span>

<span data-ttu-id="8fae4-600">Questi valori residui sembrano ragionevoli.</span><span class="sxs-lookup"><span data-stu-id="8fae4-600">These residuals look reasonable.</span></span> <span data-ttu-id="8fae4-601">È presente alcuna struttura specifico, ad eccezione di effetto hello di recessione hello 2008 2009, che il nostro modello non tiene conto di particolarmente appropriata.</span><span class="sxs-lookup"><span data-stu-id="8fae4-601">There is no particular structure, except hello effect of hello 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="8fae4-602">tracciato di Hello mostrato nella figura 25 è utile per rilevare eventuali modelli dipendenti dal tempo in residui hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-602">hello plot shown in Figure 25 is useful for detecting any time-dependent patterns in hello residuals.</span></span> <span data-ttu-id="8fae4-603">approccio esplicito di Hello di calcolo e di tracciatura residui hello utilizzato inserisce residui hello in ordine temporale in tracciato hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-603">hello explicit approach of computing and plotting hello residuals I used places hello residuals in time order on hello plot.</span></span> <span data-ttu-id="8fae4-604">Se, in hello invece avevo tracciati `milk.lm$residuals`, non sarebbe stato tracciato hello in ordine temporale.</span><span class="sxs-lookup"><span data-stu-id="8fae4-604">If, on hello other hand, I had plotted `milk.lm$residuals`, hello plot would not have been in time order.</span></span>

<span data-ttu-id="8fae4-605">È inoltre possibile utilizzare `plot.lm()` tooproduce una serie di grafici di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="8fae4-605">You can also use `plot.lm()` tooproduce a series of diagnostic plots.</span></span>

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="8fae4-606">Questo codice produce una serie di tracciati diagnostici mostrati nella Figura 26.</span><span class="sxs-lookup"><span data-stu-id="8fae4-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![Prima di grafici di diagnostica per il modello stagionali hello](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Secondo di grafici di diagnostica per il modello di stagionali hello](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Terzo di grafici di diagnostica per il modello stagionali hello](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Quarto di grafici di diagnostica per il modello stagionali hello](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="8fae4-611">*Figura 26. Traccia di diagnostica per il modello stagionali hello.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-611">*Figure 26. Diagnostic plots for hello seasonal model.*</span></span>

<span data-ttu-id="8fae4-612">Esistono alcuni punti reparti identificati in questi grafici, ma niente di grande interesse toocause.</span><span class="sxs-lookup"><span data-stu-id="8fae4-612">There are a few highly influential points identified in these plots, but nothing toocause great concern.</span></span> <span data-ttu-id="8fae4-613">Inoltre, si noterà dal tracciato normale Q-Q hello che residui hello sono distribuiti, toonormally Chiudi presupposto importante per modelli lineari.</span><span class="sxs-lookup"><span data-stu-id="8fae4-613">Further, we can see from hello Normal Q-Q plot that hello residuals are close toonormally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="8fae4-614">Previsione e valutazione del modello</span><span class="sxs-lookup"><span data-stu-id="8fae4-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="8fae4-615">Non sussiste toocomplete di toodo cosa ulteriori solo un esempio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-615">There is just one more thing toodo toocomplete our example.</span></span> <span data-ttu-id="8fae4-616">È necessaria toocompute previsioni e misurare le errore hello rispetto ai dati effettivi hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-616">We need toocompute forecasts and measure hello error against hello actual data.</span></span> <span data-ttu-id="8fae4-617">La previsione sarà per hello di 2013 12 mesi.</span><span class="sxs-lookup"><span data-stu-id="8fae4-617">Our forecast will be for hello 12 months of 2013.</span></span> <span data-ttu-id="8fae4-618">È possibile calcolare una misura di errore per questi dati di previsione toohello effettivo che non fa parte di questo set di dati di training.</span><span class="sxs-lookup"><span data-stu-id="8fae4-618">We can compute an error measure for this forecast toohello actual data that is not part of our training dataset.</span></span> <span data-ttu-id="8fae4-619">Inoltre, è possibile confrontare le prestazioni in hello 18 anni di toohello di dati di training 12 mesi di dati di test.</span><span class="sxs-lookup"><span data-stu-id="8fae4-619">Additionally, we can compare performance on hello 18 years of training data toohello 12 months of test data.</span></span>  

<span data-ttu-id="8fae4-620">Viene utilizzato un numero di metriche delle prestazioni di hello toomeasure di modelli time series.</span><span class="sxs-lookup"><span data-stu-id="8fae4-620">A number of metrics are used toomeasure hello performance of time series models.</span></span> <span data-ttu-id="8fae4-621">In questo caso si utilizzerà hello radice errore quadratico medio (RMS).</span><span class="sxs-lookup"><span data-stu-id="8fae4-621">In our case we will use hello root mean square (RMS) error.</span></span> <span data-ttu-id="8fae4-622">Hello funzione seguente calcola errore hello RMS tra due serie.</span><span class="sxs-lookup"><span data-stu-id="8fae4-622">hello following function computes hello RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
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

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="8fae4-623">Come con hello `log.transform()` illustrato nella funzione hello "Valore trasformazioni" sezione, è molto di codice di recupero di controllo e l'eccezione Errore in questa funzione.</span><span class="sxs-lookup"><span data-stu-id="8fae4-623">As with hello `log.transform()` function we discussed in hello "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="8fae4-624">principi di Hello utilizzati sono hello stesso.</span><span class="sxs-lookup"><span data-stu-id="8fae4-624">hello principles employed are hello same.</span></span> <span data-ttu-id="8fae4-625">Hello lavoro viene eseguito in due posizioni racchiuso `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="8fae4-625">hello work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="8fae4-626">In primo luogo, serie temporale hello sono exponentiated, poiché sono stati trattati i registri di hello valori hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-626">First, hello time series are exponentiated, since we have been working with hello logs of hello values.</span></span> <span data-ttu-id="8fae4-627">In secondo luogo, errore RMS di hello effettivo viene calcolato.</span><span class="sxs-lookup"><span data-stu-id="8fae4-627">Second, hello actual RMS error is computed.</span></span>  

<span data-ttu-id="8fae4-628">Dotato di un hello toomeasure funzione errore RMS, compilare e consente l'output di un frame di dati contenenti errori hello RMS.</span><span class="sxs-lookup"><span data-stu-id="8fae4-628">Equipped with a function toomeasure hello RMS error, let's build and output a dataframe containing hello RMS errors.</span></span> <span data-ttu-id="8fae4-629">Si includerà termini hello tendenza solo per modello e modello completo di hello con fattori stagionali.</span><span class="sxs-lookup"><span data-stu-id="8fae4-629">We will include terms for hello trend model alone and hello complete model with seasonal factors.</span></span> <span data-ttu-id="8fae4-630">Hello codice hello processo utilizzando hello due modelli lineare che è stata costruita.</span><span class="sxs-lookup"><span data-stu-id="8fae4-630">hello following code does hello job by using hello two linear models we have constructed.</span></span>

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
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

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="8fae4-631">L'esecuzione del codice produce l'output di hello mostrato nella figura 27 all'hello porta di output di set di risultati.</span><span class="sxs-lookup"><span data-stu-id="8fae4-631">Running this code produces hello output shown in Figure 27 at hello Result Dataset output port.</span></span>

![Confronto di errori di RMS per i modelli di hello][26]

<span data-ttu-id="8fae4-633">*Figura 27. Confronto tra gli errori di RMS per i modelli di hello.*</span><span class="sxs-lookup"><span data-stu-id="8fae4-633">*Figure 27. Comparison of RMS errors for hello models.*</span></span>

<span data-ttu-id="8fae4-634">Da questi risultati, viene illustrato che l'aggiunta di hello fattori stagionali toohello modello riduce errore RMS hello in modo significativo.</span><span class="sxs-lookup"><span data-stu-id="8fae4-634">From these results, we see that adding hello seasonal factors toohello model reduces hello RMS error significantly.</span></span> <span data-ttu-id="8fae4-635">Troppo ovviamente errore hello RMS per i dati di training hello è un bit minore per hello previsione.</span><span class="sxs-lookup"><span data-stu-id="8fae4-635">Not too surprisingly, hello RMS error for hello training data is a bit less than for hello forecast.</span></span>

## <span data-ttu-id="8fae4-636"><a id="appendixa"></a>Appendice a: Guida tooRStudio</span><span class="sxs-lookup"><span data-stu-id="8fae4-636"><a id="appendixa"></a>APPENDIX A: Guide tooRStudio</span></span>
<span data-ttu-id="8fae4-637">RStudio sia molto ben documentato, pertanto in questa appendice verranno fornite alcune toohello collegamenti sezioni principali di hello RStudio documentazione tooget che è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="8fae4-637">RStudio is quite well documented, so in this appendix I will provide some links toohello key sections of hello RStudio documentation tooget you started.</span></span>

1. <span data-ttu-id="8fae4-638">Creazione di progetti</span><span class="sxs-lookup"><span data-stu-id="8fae4-638">Creating projects</span></span>
   
   <span data-ttu-id="8fae4-639">È possibile organizzare e gestire il codice R nei progetti usando RStudio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="8fae4-640">documentazione di Hello che usa i progetti è reperibile all'https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span><span class="sxs-lookup"><span data-stu-id="8fae4-640">hello documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="8fae4-641">Consiglia di seguire queste istruzioni e creare un progetto per esempi di codice hello R in questo documento.</span><span class="sxs-lookup"><span data-stu-id="8fae4-641">I recommend that you follow these directions and create a project for hello R code examples in this document.</span></span>  
2. <span data-ttu-id="8fae4-642">Modifica ed esecuzione di codice R</span><span class="sxs-lookup"><span data-stu-id="8fae4-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="8fae4-643">RStudio offre un ambiente integrato per la modifica e l'esecuzione di codice R.</span><span class="sxs-lookup"><span data-stu-id="8fae4-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="8fae4-644">La documentazione è disponibile all'indirizzo https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span><span class="sxs-lookup"><span data-stu-id="8fae4-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="8fae4-645">Debug</span><span class="sxs-lookup"><span data-stu-id="8fae4-645">Debugging</span></span>
   
   <span data-ttu-id="8fae4-646">RStudio include avanzate funzionalità di debug.</span><span class="sxs-lookup"><span data-stu-id="8fae4-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="8fae4-647">La documentazione su queste funzionalità è disponibile all'indirizzo https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="8fae4-648">funzionalità di risoluzione dei problemi di Hello punto di interruzione sono documentate in https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="8fae4-648">hello breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="8fae4-649"><a id="appendixb"></a>APPENDICE B: Letture di approfondimento</span><span class="sxs-lookup"><span data-stu-id="8fae4-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="8fae4-650">Questa esercitazione include nozioni fondamentali di hello di programmazione di R dei risultati che è necessario toouse hello linguaggio R in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8fae4-650">This R programming tutorial covers hello basics of what you need toouse hello R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="8fae4-651">Se non si ha familiarità con R, in CRAN sono disponibili due introduzioni:</span><span class="sxs-lookup"><span data-stu-id="8fae4-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="8fae4-652">R per utenti meno esperti per Emmanuel Paradis è un ottimo strumento toostart in http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span><span class="sxs-lookup"><span data-stu-id="8fae4-652">R for Beginners by Emmanuel Paradis is a good place toostart at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="8fae4-653">Un tooR introduzione da W. N.</span><span class="sxs-lookup"><span data-stu-id="8fae4-653">An Introduction tooR by W. N.</span></span> <span data-ttu-id="8fae4-654">Venables et.</span><span class="sxs-lookup"><span data-stu-id="8fae4-654">Venables et.</span></span> <span data-ttu-id="8fae4-655">al.</span><span class="sxs-lookup"><span data-stu-id="8fae4-655">al.</span></span> <span data-ttu-id="8fae4-656">fornisce informazioni più approfondite all'indirizzo http://cran.r-project.org/doc/manuals/R-intro.html.</span><span class="sxs-lookup"><span data-stu-id="8fae4-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="8fae4-657">Sono disponibili molti libri con informazioni introduttive su R.</span><span class="sxs-lookup"><span data-stu-id="8fae4-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="8fae4-658">Di seguito sono elencati quelli che ritengo più utili:</span><span class="sxs-lookup"><span data-stu-id="8fae4-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="8fae4-659">Immagine di programmazione R Hello: una presentazione di statistiche Software Design Norman Matloff è tooprogramming un'eccellente introduzione in R.</span><span class="sxs-lookup"><span data-stu-id="8fae4-659">hello Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction tooprogramming in R.</span></span>  
* <span data-ttu-id="8fae4-660">Guida di riferimento di R da Paul Teetor fornisce un toousing approccio problemi e soluzioni R.</span><span class="sxs-lookup"><span data-stu-id="8fae4-660">R Cookbook by Paul Teetor provides a problem and solution approach toousing R.</span></span>  
* <span data-ttu-id="8fae4-661">R in Action di Robert Kabacoff, un altro libro introduttivo valido.</span><span class="sxs-lookup"><span data-stu-id="8fae4-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="8fae4-662">sito Web di R rapido complementare Hello è una risorsa utile http://www.statmethods.net/.</span><span class="sxs-lookup"><span data-stu-id="8fae4-662">hello companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="8fae4-663">R da Patrick Burns è un libro sorprendentemente divertente che gestisce un numero di argomenti complesso e difficile che possono essere rilevati durante la programmazione in libro hello r. è disponibile gratuitamente a http://www.burns-stat.com/documents/books/the-r-inferno/.</span><span class="sxs-lookup"><span data-stu-id="8fae4-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. hello book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="8fae4-664">Se si desidera un approfondimento argomenti avanzati in R, hanno un'occhiata libro hello avanzate R da Hadley Wickham.</span><span class="sxs-lookup"><span data-stu-id="8fae4-664">If you want a deep dive into advanced topics in R, have a look at hello book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="8fae4-665">versione online di Hello questa guida è disponibile gratuitamente in http://adv-r.had.co.nz/.</span><span class="sxs-lookup"><span data-stu-id="8fae4-665">hello online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="8fae4-666">Un catalogo di pacchetti di R ora serie sono reperibili hello CRAN visualizzazione delle attività per l'analisi delle serie temporali: http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="8fae4-666">A catalogue of R time series packages can be found in hello CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="8fae4-667">Per informazioni sui pacchetti oggetto serie di tempo specifico, è consigliabile consultare la documentazione di toohello per tale pacchetto.</span><span class="sxs-lookup"><span data-stu-id="8fae4-667">For information on specific time series object packages, you should refer toohello documentation for that package.</span></span>

<span data-ttu-id="8fae4-668">libro Hello introduttivo Time Series con R Paul Cowpertwait e Andrew Metcalfe fornisce un'introduzione toousing R, per l'analisi delle serie temporali.</span><span class="sxs-lookup"><span data-stu-id="8fae4-668">hello book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction toousing R for time series analysis.</span></span> <span data-ttu-id="8fae4-669">Numerosi esempi di R sono infine disponibili in una grande quantità di testi teorici.</span><span class="sxs-lookup"><span data-stu-id="8fae4-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="8fae4-670">Alcune importanti risorse su Internet:</span><span class="sxs-lookup"><span data-stu-id="8fae4-670">Some great internet resources:</span></span>

* <span data-ttu-id="8fae4-671">DataCamp: DataCamp illustra R in comfort hello del browser con lezioni video e gli esercizi di codifica.</span><span class="sxs-lookup"><span data-stu-id="8fae4-671">DataCamp: DataCamp teaches R in hello comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="8fae4-672">Sono disponibili esercitazioni interattive su tecniche di hello più recente R e pacchetti.</span><span class="sxs-lookup"><span data-stu-id="8fae4-672">There are interactive tutorials on hello latest R techniques and packages.</span></span> <span data-ttu-id="8fae4-673">Eseguire hello libero interattivo esercitazione su R a https://www.datacamp.com/courses/introduction-to-r</span><span class="sxs-lookup"><span data-stu-id="8fae4-673">Take hello free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="8fae4-674">Una Guida introduttiva alla programmazione con R da Programiz https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="8fae4-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="8fae4-675">Una rapida esercitazione su R di Kelly Black della Clarkson University è disponibile all'indirizzo http://www.cyclismo.org/tutorial/R/</span><span class="sxs-lookup"><span data-stu-id="8fae4-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="8fae4-676">Oltre 60 risorse su R sono elencate all'indirizzo http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span><span class="sxs-lookup"><span data-stu-id="8fae4-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

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
