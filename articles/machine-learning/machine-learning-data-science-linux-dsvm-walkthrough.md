---
title: Scienza aaaData nella macchina virtuale di analisi scientifica dei dati di Linux hello | Documenti Microsoft
description: "Modalità tooperform diversi analisi scientifica dei dati comuni di attività con hello VM Linux di analisi scientifica dei dati."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a><span data-ttu-id="b8ab4-103">Analisi scientifica dei dati su hello macchina virtuale di analisi scientifica dei dati di Linux</span><span class="sxs-lookup"><span data-stu-id="b8ab4-103">Data science on hello Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="b8ab4-104">Questa procedura dettagliata viene illustrato come tooperform attività più comuni analisi scientifica dei dati con hello VM Linux di analisi scientifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-104">This walkthrough shows you how tooperform several common data science tasks with hello Linux Data Science VM.</span></span> <span data-ttu-id="b8ab4-105">Hello Linux Data Science macchina virtuale (DSVM) è un'immagine di macchina virtuale disponibile in Azure che sia già installato con una raccolta di strumenti utilizzati per analitica dei dati e machine learning.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-105">hello Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="b8ab4-106">i componenti software chiave Hello vengono classificati in hello [hello provisioning macchina virtuale di analisi scientifica dei dati di Linux](machine-learning-data-science-linux-dsvm-intro.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-106">hello key software components are itemized in hello [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="b8ab4-107">Hello immagine di macchina virtuale rende facile tooget avviato esegue l'analisi scientifica dei dati in minuti, senza dovere tooinstall e configurare ognuno di strumenti hello singolarmente.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-107">hello VM image makes it easy tooget started doing data science in minutes, without having tooinstall and configure each of hello tools individually.</span></span> <span data-ttu-id="b8ab4-108">È possibile facilmente scalabilità verticale hello macchina virtuale, se necessario e arrestare quando non è in uso.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-108">You can easily scale up hello VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="b8ab4-109">caratteristiche che rendono questa risorsa flessibile e conveniente.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="b8ab4-110">attività di analisi scientifica dei dati illustrate in questa procedura dettagliata Hello seguire passaggi hello illustrati in hello [processo di analisi scientifica dei dati di Team](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-110">hello data science tasks demonstrated in this walkthrough follow hello steps outlined in hello [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="b8ab4-111">Questo processo fornisce un approccio sistematico toodata dell'analisi scientifica dei che consente ai team di esperti di dati tooeffectively collaborare in hello del ciclo di vita di compilazione di applicazioni intelligenti.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-111">This process provides a systematic approach toodata science that enables teams of data scientists tooeffectively collaborate over hello lifecycle of building intelligent applications.</span></span> <span data-ttu-id="b8ab4-112">processo di analisi scientifica dei dati Hello fornisce inoltre un framework iterativo di analisi scientifica dei dati che può essere seguito da un singolo.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-112">hello data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="b8ab4-113">Consente di analizzare hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) set di dati in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-113">We analyze hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="b8ab4-114">Si tratta di un set di messaggi di posta elettronica sono contrassegnati come posta indesiderata o ham (ovvero non sono posta indesiderata), nonché alcune statistiche per il contenuto di hello di messaggi di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on hello content of hello emails.</span></span> <span data-ttu-id="b8ab4-115">statistiche Hello inclusione verranno esaminate in hello successivamente ma una sezione.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-115">hello statistics included are discussed in hello next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8ab4-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b8ab4-116">Prerequisites</span></span>
<span data-ttu-id="b8ab4-117">Prima di poter utilizzare una macchina di virtuale analisi scientifica dei dati di Linux, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-117">Before you can use a Linux Data Science Virtual Machine, you must have hello following:</span></span>

* <span data-ttu-id="b8ab4-118">Una **sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-118">An **Azure subscription**.</span></span> <span data-ttu-id="b8ab4-119">Se non è già disponibile, vedere [Crea subito il tuo account Azure gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="b8ab4-120">Una [**macchina virtuale Linux per l'analisi scientifica dei dati**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="b8ab4-121">Per informazioni sul provisioning di questa macchina virtuale, vedere [hello provisioning macchina virtuale di analisi scientifica dei dati di Linux](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-121">For information on provisioning this VM, see [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="b8ab4-122">[X2Go](http://wiki.x2go.org/doku.php) installato nel computer con una sessione di XFCE aperta.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="b8ab4-123">Per informazioni sull'installazione e la configurazione di un **client X2Go**, vedere [Installazione e configurazione del client X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="b8ab4-124">Un **account Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-124">An **AzureML account**.</span></span> <span data-ttu-id="b8ab4-125">Se si dispone già di uno, iscriversi a uno nuovo in hello [home page di Azure ml](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-125">If you don't already have one, sign up for new one at hello [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="b8ab4-126">Non vi è un toohelp di livello di utilizzo gratuita iniziare.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-126">There is a free usage tier toohelp you get started.</span></span>

## <a name="download-hello-spambase-dataset"></a><span data-ttu-id="b8ab4-127">Scaricare hello spambase set di dati</span><span class="sxs-lookup"><span data-stu-id="b8ab4-127">Download hello spambase dataset</span></span>
<span data-ttu-id="b8ab4-128">Hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) set di dati è un numero relativamente ridotto di dati che contiene solo 4601 esempi.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-128">hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="b8ab4-129">Si tratta di un toouse dimensioni pratico per dimostrare che alcune delle funzionalità chiave di hello di hello VM di analisi scientifica dei dati che mantiene i requisiti di risorse hello adeguato.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-129">This is a convenient size toouse when demonstrating that some of hello key features of hello Data Science VM as it keeps hello resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="b8ab4-130">Questa procedura dettagliata è stata creata in una macchina virtuale Linux per l'analisi scientifica dei dati di dimensioni D2 v2.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="b8ab4-131">La dimensione DSVM è in grado di gestire procedure hello in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-131">This size DSVM is capable of handling hello procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="b8ab4-132">Se è necessario più spazio di archiviazione, è possibile creare ulteriori dischi e collegarli tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-132">If you need more storage space, you can create additional disks and attach them tooyour VM.</span></span> <span data-ttu-id="b8ab4-133">Questi dischi utilizzano permanente archiviazione di Azure, pertanto i relativi dati vengono mantenuti anche quando reprovisioning server hello scadenza tooresizing o è stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-133">These disks use persistent Azure storage, so their data is preserved even when hello server is reprovisioned due tooresizing or is shut down.</span></span> <span data-ttu-id="b8ab4-134">tooadd un disco e collegarlo tooyour macchina virtuale, seguire le istruzioni hello [aggiungere una VM Linux di tooa disco](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-134">tooadd a disk and attach it tooyour VM, follow hello instructions in [Add a disk tooa Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b8ab4-135">Questi passaggi utilizzano l'interfaccia della riga di comando Azure (Azure CLI), che è già installato in hello DSVM hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-135">These steps use hello Azure Command-Line Interface (Azure CLI), which is already installed on hello DSVM.</span></span> <span data-ttu-id="b8ab4-136">Pertanto, queste procedure possono essere eseguite interamente da hello macchina virtuale stessa.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-136">So these procedures can be done entirely from hello VM itself.</span></span> <span data-ttu-id="b8ab4-137">Un'altra opzione tooincrease trovi toouse [file di Azure](../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-137">Another option tooincrease storage is toouse [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="b8ab4-138">dati hello toodownload, aprire una finestra terminale ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-138">toodownload hello data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="b8ab4-139">file scaricato Hello non dispone di una riga di intestazione, pertanto è necessario creare un altro file con un'intestazione.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-139">hello downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="b8ab4-140">Eseguire toocreate questo comando di un file con le intestazioni appropriate hello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-140">Run this command toocreate a file with hello appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="b8ab4-141">Quindi concatenare due file con il comando hello di hello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-141">Then concatenate hello two files together with hello command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="b8ab4-142">set di dati Hello dispone di diversi tipi di statistiche su ogni messaggio di posta elettronica:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-142">hello dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="b8ab4-143">Ad esempio colonne ***word\_freq\_WORD*** indicare hello percentuale di parole nel messaggio di posta elettronica hello che corrispondono a *WORD*.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-143">Columns like ***word\_freq\_WORD*** indicate hello percentage of words in hello email that match *WORD*.</span></span> <span data-ttu-id="b8ab4-144">Ad esempio, se *word\_freq\_rendere* è 1, quindi sono stati % 1 di tutte le parole nel messaggio di posta elettronica hello *rendere*.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-144">For example, if *word\_freq\_make* is 1, then 1% of all words in hello email were *make*.</span></span>
* <span data-ttu-id="b8ab4-145">Ad esempio colonne ***char\_freq\_CHAR*** indicare hello percentuale di tutti i caratteri nel messaggio di posta elettronica hello che sono stati *CHAR*.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-145">Columns like ***char\_freq\_CHAR*** indicate hello percentage of all characters in hello email that were *CHAR*.</span></span>
* <span data-ttu-id="b8ab4-146">***capitale\_eseguire\_lunghezza\_più lunga*** hello la lunghezza massima di una sequenza di lettere maiuscole.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-146">***capital\_run\_length\_longest*** is hello longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="b8ab4-147">***capitale\_eseguire\_lunghezza\_Media*** hello lunghezza media di tutte le sequenze di lettere maiuscole.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-147">***capital\_run\_length\_average*** is hello average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="b8ab4-148">***capitale\_eseguire\_lunghezza\_totale*** è hello lunghezza totale di tutte le sequenze di lettere maiuscole.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-148">***capital\_run\_length\_total*** is hello total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="b8ab4-149">***posta indesiderata*** indica se posta elettronica hello è stato considerato posta indesiderata o non (1 = posta indesiderata, 0 = non spam).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-149">***spam*** indicates whether hello email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-hello-dataset-with-microsoft-r-open"></a><span data-ttu-id="b8ab4-150">Esplorare hello set di dati con Microsoft R Open</span><span class="sxs-lookup"><span data-stu-id="b8ab4-150">Explore hello dataset with Microsoft R Open</span></span>
<span data-ttu-id="b8ab4-151">Di seguito esaminare i dati di hello ed eseguire alcune learning macchina di base con r. hello VM di analisi scientifica dei dati viene fornito con [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installato.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-151">Let's examine hello data and do some basic machine learning with R. hello Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="b8ab4-152">Hello librerie matematiche multithreading in questa versione di R offrono prestazioni migliori rispetto alle versioni diverse a thread singolo.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-152">hello multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="b8ab4-153">Microsoft R Open fornisce inoltre la riproducibilità utilizzando uno snapshot del repository di pacchetti CRAN hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-153">Microsoft R Open also provides reproducibility by using a snapshot of hello CRAN package repository.</span></span>

<span data-ttu-id="b8ab4-154">gli esempi utilizzati in questa procedura dettagliata, hello clone di codice tooget copie di hello **Azure-Machine-Learning--analisi scientifica dei dati** repository tramite git, di cui è preinstallato in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-154">tooget copies of hello code samples used in this walkthrough, clone hello **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on hello VM.</span></span> <span data-ttu-id="b8ab4-155">Dalla riga di comando git hello, eseguire:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-155">From hello git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="b8ab4-156">Aprire una finestra terminale e avviare una nuova sessione di R con la console interattiva hello R.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-156">Open a terminal window and start a new R session with hello R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="b8ab4-157">È anche possibile utilizzare RStudio per hello seguire le procedure seguenti.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-157">You can also use RStudio for hello following procedures.</span></span> <span data-ttu-id="b8ab4-158">tooinstall RStudio, eseguire il comando seguente in un terminal:`./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="b8ab4-158">tooinstall RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="b8ab4-159">dati hello tooimport e configurare l'ambiente di hello, eseguire:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-159">tooimport hello data and set up hello environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="b8ab4-160">toosee le statistiche di riepilogo su ogni colonna:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-160">toosee summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="b8ab4-161">Per una visualizzazione diversa dei dati hello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-161">For a different view of hello data:</span></span>

    str(data)

<span data-ttu-id="b8ab4-162">Questo mostra è hello tipo di ogni variabile e hello innanzitutto alcuni valori nel set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-162">This shows you hello type of each variable and hello first few values in hello dataset.</span></span>

<span data-ttu-id="b8ab4-163">Hello *posta indesiderata* colonna è stato letto come un numero intero, ma è effettivamente un categorico variabile (o fattore).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-163">hello *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="b8ab4-164">tooset il relativo tipo:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-164">tooset its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="b8ab4-165">toodo alcune analisi esplorativa, utilizzare hello [ggplot2](http://ggplot2.org/) del pacchetto, una libreria grafica diffusa per R che è già installata nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-165">toodo some exploratory analysis, use hello [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on hello VM.</span></span> <span data-ttu-id="b8ab4-166">Si noti, dai dati di riepilogo hello visualizzati in precedenza, la presenza di statistiche di riepilogo sulla frequenza di hello del carattere punto esclamativo hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-166">Note, from hello summary data displayed earlier, that we have summary statistics on hello frequency of hello exclamation mark character.</span></span> <span data-ttu-id="b8ab4-167">Si tracciare le frequenze qui con hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-167">Let's plot those frequencies here with hello following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="b8ab4-168">Poiché la barra hello zero è inclinazione tracciato hello, consente la rimozione:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-168">Since hello zero bar is skewing hello plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="b8ab4-169">La densità non semplice superiore a 1 sembra interessante.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="b8ab4-170">Per esaminare solo quei dati, eseguire:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="b8ab4-171">Per dividere quindi i dati in posta indesiderata e non indesiderata, eseguire:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="b8ab4-172">Questi esempi dovrebbero consentire di toomake grafici simili di hello tooexplore altre colonne hello dati in essi contenuti.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-172">These examples should enable you toomake similar plots of hello other columns tooexplore hello data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="b8ab4-173">Eseguire il training di un modello ML e testarlo</span><span class="sxs-lookup"><span data-stu-id="b8ab4-173">Train and test an ML model</span></span>
<span data-ttu-id="b8ab4-174">Ora si train un paio di machine learning modelli di messaggi di posta elettronica hello tooclassify nel set di dati hello come contenente span o ham.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-174">Now let's train a couple of machine learning models tooclassify hello emails in hello dataset as containing either span or ham.</span></span> <span data-ttu-id="b8ab4-175">Questa sezione illustra come eseguire il training di un modello di albero delle decisioni e di un modello di foresta casuale e quindi testarne la correttezza delle previsioni.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="b8ab4-176">Hello rpart (partizionamento ricorsivo e alberi di regressione) utilizzato nel seguente codice hello è già installato su hello VM di analisi scientifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-176">hello rpart (Recursive Partitioning and Regression Trees) package used in hello following code is already installed on hello Data Science VM.</span></span>
>
>

<span data-ttu-id="b8ab4-177">In primo luogo, si suddividere hello set di dati in set di training e di test:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-177">First, let's split hello dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="b8ab4-178">Creare quindi un hello tooclassify di albero delle decisioni messaggi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-178">And then create a decision tree tooclassify hello emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="b8ab4-179">Di seguito è riportato il risultato di hello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-179">Here is hello result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="b8ab4-181">toodetermine sulle prestazioni per la formazione di hello impostato, utilizzare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-181">toodetermine how well it performs on hello training set, use hello following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="b8ab4-182">il grado di toodetermine che esegue nel set di test hello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-182">toodetermine how well it performs on hello test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="b8ab4-183">Viene ora esaminato un modello di foresta casuale.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-183">Let's also try a random forest model.</span></span> <span data-ttu-id="b8ab4-184">Foreste casuali eseguire il training di una grande varietà di alberi delle decisioni e di output di una classe che è la modalità di hello di classificazioni hello da tutti gli alberi delle decisioni singoli di hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-184">Random forests train a multitude of decision trees and output a class that is hello mode of hello classifications from all of hello individual decision trees.</span></span> <span data-ttu-id="b8ab4-185">Forniscono un computer più potente apprendimento approccio come saranno corretti per la tendenza hello di un toooverfit modello di albero delle decisioni un set di dati di training.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-185">They provide a more powerful machine learning approach as they correct for hello tendency of a decision tree model toooverfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a><span data-ttu-id="b8ab4-186">Distribuire un tooAzure modello ML</span><span class="sxs-lookup"><span data-stu-id="b8ab4-186">Deploy a model tooAzure ML</span></span>
<span data-ttu-id="b8ab4-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (Azure ml) è un servizio cloud che rende facile toobuild e distribuisce modelli analitica predittiva.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy toobuild and deploy predictive analytics models.</span></span> <span data-ttu-id="b8ab4-188">Una delle funzionalità di nice hello di Azure ml è toopublish il possibilità qualsiasi R funzione come un servizio web.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-188">One of hello nice features of AzureML is its ability toopublish any R function as a web service.</span></span> <span data-ttu-id="b8ab4-189">Hello pacchetto R AzureML rende toodo di facile distribuzione direttamente dal nostro sessione R per hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-189">hello AzureML R package makes deployment easy toodo right from our R session on hello DSVM.</span></span>

<span data-ttu-id="b8ab4-190">toodeploy codice albero delle decisioni di hello dalla sezione precedente di hello, è necessario toosign in tooAzure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-190">toodeploy hello decision tree code from hello previous section, you need toosign in tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="b8ab4-191">È necessario l'ID dell'area di lavoro e un toosign del token di autorizzazione in.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-191">You need your workspace ID and an authorization token toosign in.</span></span> <span data-ttu-id="b8ab4-192">toofind i valori e inizializzare le variabili di Azure ml hello con essi:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-192">toofind these values and initialize hello AzureML variables with them:</span></span>

<span data-ttu-id="b8ab4-193">Selezionare **impostazioni** dal menu a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-193">Select **Settings** on hello left-hand menu.</span></span> <span data-ttu-id="b8ab4-194">Prendere nota del valore **WORKSPACE ID**(ID area di lavoro).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="b8ab4-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="b8ab4-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="b8ab4-196">Selezionare **token di autorizzazione** dal menu overhead hello e prendere nota del **primario Token di autorizzazione**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="b8ab4-196">Select **Authorization Tokens** from hello overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="b8ab4-197">Hello carico **Azure ml** del pacchetto e quindi impostare i valori delle variabili di hello con l'ID di token e l'area di lavoro nella sessione di R in hello DSVM:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-197">Load hello **AzureML** package and then set values of hello variables with your token and workspace ID in your R session on hello DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="b8ab4-198">Consente di semplificare hello modello toomake tooimplement di più facile questa dimostrazione.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-198">Let's simplify hello model toomake this demonstration easier tooimplement.</span></span> <span data-ttu-id="b8ab4-199">Selezionare hello tre variabili nella radice toohello più vicino di hello decisione dell'albero e compilare un nuovo albero utilizzando solo le tre variabili:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-199">Pick hello three variables in hello decision tree closest toohello root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="b8ab4-200">Abbiamo bisogno di una funzione di stima che utilizza le funzionalità di hello come input e restituisce hello valori stimati:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-200">We need a prediction function that takes hello features as an input and returns hello predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="b8ab4-201">Pubblicare hello predictSpam funzione tooAzureML utilizzando hello **publishWebService** funzione:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-201">Publish hello predictSpam function tooAzureML using hello **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="b8ab4-202">Questa funzione accetta hello **predictSpam** di funzione, viene creato un servizio web denominato **spamWebService** con definito input e output e restituisce informazioni sul nuovo endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-202">This function takes hello **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about hello new endpoint.</span></span>

<span data-ttu-id="b8ab4-203">Visualizzazione dei dettagli di hello ha pubblicato il servizio, incluse le chiavi di accesso e l'endpoint API con il comando hello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-203">View details of hello published web service, including its API endpoint and access keys with hello command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="b8ab4-204">tootry impostarlo su hello prime 10 righe del set di test hello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-204">tootry it out on hello first 10 rows of hello test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="b8ab4-205">Usare altri strumenti disponibili</span><span class="sxs-lookup"><span data-stu-id="b8ab4-205">Use other tools available</span></span>
<span data-ttu-id="b8ab4-206">nelle restanti sezioni Hello mostrano come toouse alcuni degli strumenti hello installato hello VM Linux di analisi scientifica dei dati. Ecco hello elenco degli strumenti illustrati:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-206">hello remaining sections show how toouse some of hello tools installed on hello Linux Data Science VM.Here is hello list of tools discussed:</span></span>

* <span data-ttu-id="b8ab4-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="b8ab4-207">XGBoost</span></span>
* <span data-ttu-id="b8ab4-208">Python</span><span class="sxs-lookup"><span data-stu-id="b8ab4-208">Python</span></span>
* <span data-ttu-id="b8ab4-209">JupyterHub</span><span class="sxs-lookup"><span data-stu-id="b8ab4-209">Jupyterhub</span></span>
* <span data-ttu-id="b8ab4-210">Rattle</span><span class="sxs-lookup"><span data-stu-id="b8ab4-210">Rattle</span></span>
* <span data-ttu-id="b8ab4-211">PostgreSQL e Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="b8ab4-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="b8ab4-212">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b8ab4-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="b8ab4-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="b8ab4-213">XGBoost</span></span>
<span data-ttu-id="b8ab4-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) è uno strumento che consente un'implementazione di albero con boosting rapida e accurata.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

<span data-ttu-id="b8ab4-215">XGBoost permette anche di eseguire chiamate da Python o da una riga di comando.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="b8ab4-216">Python</span><span class="sxs-lookup"><span data-stu-id="b8ab4-216">Python</span></span>
<span data-ttu-id="b8ab4-217">Per lo sviluppo usando Python, distribuzioni di hello Anaconda Python 2.7 e 3.5 sono state installate in hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-217">For development using Python, hello Anaconda Python distributions 2.7 and 3.5 have been installed in hello DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="b8ab4-218">include Hello distribuzione Anaconda [Condas](http://conda.pydata.org/docs/index.html), che può essere utilizzato toocreate ambienti personalizzati per Python con diverse versioni e/o i pacchetti installati in essi contenuti.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-218">hello Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used toocreate custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="b8ab4-219">Consente di lettura in alcuni set di dati spambase hello e classificare i messaggi di posta elettronica hello con macchine a vettori di supporto in scikit-informazioni su:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-219">Let's read in some of hello spambase dataset and classify hello emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="b8ab4-220">toomake stime:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-220">toomake predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="b8ab4-221">tooshow come toopublish un endpoint di Azure ml, si crea un modello più semplice hello tre variabili come abbiamo quando è pubblicato il modello R hello in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-221">tooshow how toopublish an AzureML endpoint, let's make a simpler model hello three variables as we did when we published hello R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="b8ab4-222">toopublish hello modello tooAzureML:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-222">toopublish hello model tooAzureML:</span></span>

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="b8ab4-223">È disponibile solo per Python 2.7 e non è ancora supportato nella versione 3.5.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="b8ab4-224">Eseguire con **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="b8ab4-225">JupyterHub</span><span class="sxs-lookup"><span data-stu-id="b8ab4-225">Jupyterhub</span></span>
<span data-ttu-id="b8ab4-226">distribuzione Anaconda Hello in hello DSVM viene fornito con un server Jupyter notebook, un codice di Julia, Python o R tooshare ambiente multipiattaforma e analisi.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-226">hello Anaconda distribution in hello DSVM comes with a Jupyter notebook, a cross-platform environment tooshare Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="b8ab4-227">notebook Jupyter Hello è accessibile tramite JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-227">hello Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="b8ab4-228">Per eseguire l'accesso, usare il nome utente e la password locali di ***https://\<Nome DNS o indirizzo IP della VM\>:8000/***.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="b8ab4-229">Tutti i file di configurazione per JupyterHub si trovano nella directory **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="b8ab4-230">Numerosi blocchi appunti di esempio sono già installati nel hello VM:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-230">Several sample notebooks are already installed on hello VM:</span></span>

* <span data-ttu-id="b8ab4-231">Vedere hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) per un raccoglitore di Python di esempio.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-231">See hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="b8ab4-232">Per un notebook di [R](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) di esempio, vedere **IntroTutorialinR** .</span><span class="sxs-lookup"><span data-stu-id="b8ab4-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="b8ab4-233">Vedere hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) per un altro esempio **Python** notebook.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-233">See hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="b8ab4-234">linguaggio Julia Hello è disponibile anche dalla riga di comando hello in hello VM Linux di analisi scientifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-234">hello Julia language is also available from hello command line on hello Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="b8ab4-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="b8ab4-235">Rattle</span></span>
<span data-ttu-id="b8ab4-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (strumento di analisi R tooLearn hello facilmente) è uno strumento grafico R per il data mining.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (hello R Analytical Tool tooLearn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="b8ab4-237">Ha un'interfaccia intuitiva che rende facile tooload, esplorare e trasformare i dati e compilare e valutare i modelli.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-237">It has an intuitive interface that makes it easy tooload, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="b8ab4-238">articolo Hello [Rattle: GUI di Data Mining dati A per R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) fornisce una procedura dettagliata che illustra le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-238">hello article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="b8ab4-239">Installare e avviare sonagli con hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-239">Install and start Rattle with hello following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="b8ab4-240">Su hello DSVM non è necessaria l'installazione.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-240">Installation is not required on hello DSVM.</span></span> <span data-ttu-id="b8ab4-241">Ma sonagli venga chiesto di pacchetti aggiuntivi tooinstall durante il caricamento.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-241">But Rattle may prompt you tooinstall additional packages when it loads.</span></span>
>
>

<span data-ttu-id="b8ab4-242">Rattle usa un'interfaccia basata su schede.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="b8ab4-243">La maggior parte delle schede hello corrisponde toosteps in hello [il processo di analisi scientifica dei dati](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), ad esempio il caricamento dei dati o esplorazione.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-243">Most of hello tabs correspond toosteps in hello [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="b8ab4-244">processo di analisi scientifica dei dati Hello flusso da sinistra tooright tramite schede hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-244">hello data science process flows from left tooright through hello tabs.</span></span> <span data-ttu-id="b8ab4-245">Ma l'ultima scheda hello contiene un log di comandi hello R eseguiti da sonagli.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-245">But hello last tab contains a log of hello R commands run by Rattle.</span></span>

<span data-ttu-id="b8ab4-246">tooload e configurare i set di dati hello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-246">tooload and configure hello dataset:</span></span>

* <span data-ttu-id="b8ab4-247">file hello tooload, seleziona hello **dati** scheda, quindi</span><span class="sxs-lookup"><span data-stu-id="b8ab4-247">tooload hello file, select hello **Data** tab, then</span></span>
* <span data-ttu-id="b8ab4-248">Scegliere il selettore di hello successivo troppo**Filename** e scegliere **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-248">Choose hello selector next too**Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="b8ab4-249">file hello tooload.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-249">tooload hello file.</span></span> <span data-ttu-id="b8ab4-250">Selezionare **Execute** nella riga superiore di hello dei pulsanti.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-250">select **Execute** in hello top row of buttons.</span></span> <span data-ttu-id="b8ab4-251">Verrà visualizzato un riepilogo di ogni colonna, incluso il tipo di dati identificato, se si tratta di un input, una destinazione o altro tipo di variabile e il numero di hello di valori univoci.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and hello number of unique values.</span></span>
* <span data-ttu-id="b8ab4-252">Sonaglio ha identificato correttamente hello **posta indesiderata** colonna come destinazione di hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-252">Rattle has correctly identified hello **spam** column as hello target.</span></span> <span data-ttu-id="b8ab4-253">Colonna di hello selezionare posta indesiderata, quindi hello set **il tipo di dati di destinazione** troppo**Categoric**.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-253">Select hello spam column, then set hello **Target Data Type** too**Categoric**.</span></span>

<span data-ttu-id="b8ab4-254">dati hello tooexplore:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-254">tooexplore hello data:</span></span>

* <span data-ttu-id="b8ab4-255">Seleziona hello **Esplora** scheda.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-255">Select hello **Explore** tab.</span></span>
* <span data-ttu-id="b8ab4-256">Fare clic su **riepilogo**, quindi **Execute**, toosee alcune informazioni sui tipi di variabile hello e alcune statistiche di riepilogo.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-256">Click **Summary**, then **Execute**, toosee some information about hello variable types and some summary statistics.</span></span>
* <span data-ttu-id="b8ab4-257">tooview altri tipi di statistiche relative a ogni variabile, selezionare altre opzioni come **descrizione** o **nozioni di base**.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-257">tooview other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="b8ab4-258">Hello **Esplora** scheda consente anche toogenerate molti dettagliati vengono tracciati.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-258">hello **Explore** tab also allows you toogenerate many insightful plots.</span></span> <span data-ttu-id="b8ab4-259">un istogramma che mostra i dati di hello tooplot:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-259">tooplot a histogram of hello data:</span></span>

* <span data-ttu-id="b8ab4-260">Scegliere **Distributions**(Distribuzioni).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-260">Select **Distributions**.</span></span>
* <span data-ttu-id="b8ab4-261">Selezionare **Histogram** (Istogramma) per **word_freq_remove** e **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="b8ab4-262">Scegliere **Execute**(Esegui).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-262">Select **Execute**.</span></span> <span data-ttu-id="b8ab4-263">Dovrebbe essere che entrambi densità è rappresentata in un'unica area grafica, in cui è possibile determinare tale parola hello "si" viene visualizzato più spesso in messaggi di posta elettronica di "Rimuovi".</span><span class="sxs-lookup"><span data-stu-id="b8ab4-263">You should see both density plots in a single graph window, where it is clear that hello word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="b8ab4-264">grafici di correlazione Hello sono interessanti.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-264">hello Correlation plots are also interesting.</span></span> <span data-ttu-id="b8ab4-265">toocreate uno:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-265">toocreate one:</span></span>

* <span data-ttu-id="b8ab4-266">Scegliere **correlazione** come hello **tipo**, quindi</span><span class="sxs-lookup"><span data-stu-id="b8ab4-266">Choose **Correlation** as hello **Type**, then</span></span>
* <span data-ttu-id="b8ab4-267">Scegliere **Execute**(Esegui).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-267">Select **Execute**.</span></span>
* <span data-ttu-id="b8ab4-268">Rattle avvisa l'utente che è consigliabile usare un massimo di 40 variabili.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="b8ab4-269">Selezionare **Sì** tracciato hello tooview.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-269">Select **Yes** tooview hello plot.</span></span>

<span data-ttu-id="b8ab4-270">Esistono alcune correlazioni interessanti che sono: "la tecnologia" è strettamente correlata troppo "HP" e "lab", ad esempio.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-270">There are some interesting correlations that come up: "technology" is strongly correlated too"HP" and "labs", for example.</span></span> <span data-ttu-id="b8ab4-271">Si è anche strettamente correlato troppo "650", perché il codice di area hello donatori di set di dati hello è 650.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-271">It is also strongly correlated too"650", because hello area code of hello dataset donors is 650.</span></span>

<span data-ttu-id="b8ab4-272">i valori numerici Hello per le correlazioni hello tra le parole sono disponibili nella finestra Esplora hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-272">hello numeric values for hello correlations between words are available in hello Explore window.</span></span> <span data-ttu-id="b8ab4-273">È interessante toonote, ad esempio, che "tecnologia" negativamente sia correlata con "i" e "money".</span><span class="sxs-lookup"><span data-stu-id="b8ab4-273">It is interesting toonote, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="b8ab4-274">Sonaglio può trasformare hello dataset toohandle alcuni problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-274">Rattle can transform hello dataset toohandle some common issues.</span></span> <span data-ttu-id="b8ab4-275">Ad esempio, consente la funzionalità toorescale, attribuire valori mancanti, gestire gli outlier e rimuovere le variabili o le osservazioni con i dati mancanti.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-275">For example, it allows you toorescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="b8ab4-276">Rattle può anche identificare le regole di associazione tra le osservazioni e/o le variabili.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="b8ab4-277">Queste schede non rientrano nell'ambito di questa procedura dettagliata introduttiva.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="b8ab4-278">Rattle permette anche di eseguire l'analisi a cluster.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="b8ab4-279">Consente di escludere alcuni tooread più facilmente funzionalità toomake hello output.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-279">Let's exclude some features toomake hello output easier tooread.</span></span> <span data-ttu-id="b8ab4-280">In hello **dati** scegliere **ignora** tooeach successivo delle variabili di hello ad eccezione di questi dieci elementi:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-280">On hello **Data** tab, choose **Ignore** next tooeach of hello variables except these ten items:</span></span>

* <span data-ttu-id="b8ab4-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="b8ab4-281">word_freq_hp</span></span>
* <span data-ttu-id="b8ab4-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="b8ab4-282">word_freq_technology</span></span>
* <span data-ttu-id="b8ab4-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="b8ab4-283">word_freq_george</span></span>
* <span data-ttu-id="b8ab4-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="b8ab4-284">word_freq_remove</span></span>
* <span data-ttu-id="b8ab4-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="b8ab4-285">word_freq_your</span></span>
* <span data-ttu-id="b8ab4-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="b8ab4-286">word_freq_dollar</span></span>
* <span data-ttu-id="b8ab4-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="b8ab4-287">word_freq_money</span></span>
* <span data-ttu-id="b8ab4-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="b8ab4-288">capital_run_length_longest</span></span>
* <span data-ttu-id="b8ab4-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="b8ab4-289">word_freq_business</span></span>
* <span data-ttu-id="b8ab4-290">spam</span><span class="sxs-lookup"><span data-stu-id="b8ab4-290">spam</span></span>

<span data-ttu-id="b8ab4-291">Tornare toohello **Cluster** scegliere **KMeans**e set hello *numero di cluster* too4.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-291">Then go back toohello **Cluster** tab, choose **KMeans**, and set hello *Number of clusters* too4.</span></span> <span data-ttu-id="b8ab4-292">Scegliere **Execute**(Esegui).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-292">Then **Execute**.</span></span> <span data-ttu-id="b8ab4-293">Hello risultati vengono visualizzati nella finestra di output di hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-293">hello results are displayed in hello output window.</span></span> <span data-ttu-id="b8ab4-294">Un cluster ha una frequenza elevata di "george" e "hp" ed è probabilmente un messaggio di lavoro legittimo.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="b8ab4-295">un modello di machine learning di albero decisionale toobuild:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-295">toobuild a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="b8ab4-296">Seleziona hello **modello** scheda</span><span class="sxs-lookup"><span data-stu-id="b8ab4-296">Select hello **Model** tab,</span></span>
* <span data-ttu-id="b8ab4-297">Scegliere **albero** come hello **tipo**.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-297">Choose **Tree** as hello **Type**.</span></span>
* <span data-ttu-id="b8ab4-298">Selezionare **Execute** albero hello toodisplay forma testo hello nella finestra di output.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-298">Select **Execute** toodisplay hello tree in text form in hello output window.</span></span>
* <span data-ttu-id="b8ab4-299">Seleziona hello **disegnare** pulsante tooview una versione con interfaccia grafica.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-299">Select hello **Draw** button tooview a graphical version.</span></span> <span data-ttu-id="b8ab4-300">Questa è molto simile a quello dell'albero toohello sono stati ottenuti in precedenza mediante *rpart*.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-300">This looks quite similar toohello tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="b8ab4-301">Una delle funzionalità di nice hello di sonagli è toorun il possibilità di apprendimento diversi metodi e valutarli rapidamente.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-301">One of hello nice features of Rattle is its ability toorun several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="b8ab4-302">Ecco la procedura hello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-302">Here is hello procedure:</span></span>

* <span data-ttu-id="b8ab4-303">Scegliere **tutti** per hello **tipo**.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-303">Choose **All** for hello **Type**.</span></span>
* <span data-ttu-id="b8ab4-304">Scegliere **Execute**(Esegui).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-304">Select **Execute**.</span></span>
* <span data-ttu-id="b8ab4-305">Al termine è possibile fare clic su ogni singolo **tipo**, ad esempio **SVM**e visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-305">After it finishes you can click any single **Type**, like **SVM**, and view hello results.</span></span>
* <span data-ttu-id="b8ab4-306">È inoltre possibile confrontare le prestazioni di hello dei modelli di hello sulla convalida hello impostato utilizzando hello **Evaluate** scheda. Ad esempio, hello **errore matrice** selezione Mostra la matrice di confusione hello, errore generale e di errore di classe Media per ogni modello nel set convalida hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-306">You can also compare hello performance of hello models on hello validation set using hello **Evaluate** tab. For example, hello **Error Matrix** selection shows you hello confusion matrix, overall error, and averaged class error for each model on hello validation set.</span></span>
* <span data-ttu-id="b8ab4-307">È anche possibile tracciare le curve ROC, eseguire analisi di sensibilità e altri tipi di valutazioni del modello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="b8ab4-308">Dopo aver terminato la compilazione di modelli, selezionare hello **Log** scheda codice hello R tooview eseguito da sonagli durante la sessione.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-308">Once you're finished building models, select hello **Log** tab tooview hello R code run by Rattle during your session.</span></span> <span data-ttu-id="b8ab4-309">È possibile selezionare hello **esportare** toosave pulsante è.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-309">You can select hello **Export** button toosave it.</span></span>

> [!NOTE]
> <span data-ttu-id="b8ab4-310">La versione corrente di Rattle contiene un bug.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="b8ab4-311">toomodify hello script o utilizzarla toorepeat i passaggi in un secondo momento, è necessario inserire un carattere # davanti * esportare questo file di registro... * nel testo hello del log hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-311">toomodify hello script or use it toorepeat your steps later, you must insert a # character in front of *Export this log ... * in hello text of hello log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="b8ab4-312">PostgreSQL e Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="b8ab4-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="b8ab4-313">Hello DSVM include PostgreSQL installato.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-313">hello DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="b8ab4-314">PostgreSQL è un sofisticato database relazionale open source.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="b8ab4-315">Questa sezione viene illustrato come tooload il set di dati di posta indesiderata in PostgreSQL e quindi eseguire una query.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-315">This section shows how tooload our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="b8ab4-316">Prima di caricare dati hello, è necessario l'autenticazione di password tooallow da hello localhost.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-316">Before you can load hello data, you need tooallow password authentication from hello localhost.</span></span> <span data-ttu-id="b8ab4-317">Al prompt dei comandi, eseguire:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="b8ab4-318">Nella parte inferiore di hello hello del file di configurazione sono più righe in cui vengono hello connessioni consentita:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-318">Near hello bottom of hello config file are several lines that detail hello allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="b8ab4-319">Modificare hello "IPv4 le connessioni locali" riga toouse md5 anziché ident, pertanto è possibile accedere con un nome utente e password:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-319">Change hello "IPv4 local connections" line toouse md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="b8ab4-320">E riavviare il servizio di postgres hello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-320">And restart hello postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="b8ab4-321">toolaunch psql, un terminale interactive per PostgreSQL, come utente postgres incorporato hello, eseguire hello comando seguente da un prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-321">toolaunch psql, an interactive terminal for PostgreSQL, as hello built-in postgres user, run hello following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="b8ab4-322">Creare un nuovo account utente, utilizzando hello stesso nome utente come account Linux attualmente si è connessi come hello e assegnare una password:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-322">Create a new user account, using hello same username as hello Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="b8ab4-323">Accedere quindi toopsql come l'utente:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-323">Then log in toopsql as your user:</span></span>

    psql

<span data-ttu-id="b8ab4-324">E l'importazione di dati di hello in un nuovo database:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-324">And import hello data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="b8ab4-325">A questo punto, consente di esplorare i dati di hello ed eseguire alcune query utilizzando **esce SQL**, uno strumento grafico che consente di interagire con i database tramite un driver JDBC.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-325">Now, let's explore hello data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="b8ab4-326">tooget avviato, avviare SQL esce dal menu di applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-326">tooget started, launch Squirrel SQL from hello Applications menu.</span></span> <span data-ttu-id="b8ab4-327">tooset driver hello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-327">tooset up hello driver:</span></span>

* <span data-ttu-id="b8ab4-328">Selezionare **Windows** e quindi **View Drivers** (Visualizza driver).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="b8ab4-329">Fare clic con il pulsante destro del mouse su **PostgreSQL** e selezionare **Modify Driver** (Modifica driver).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="b8ab4-330">Selezionare **Extra Class Path** (Percorso classe extra) e quindi **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="b8ab4-331">Immettere ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** per hello **nome File** e</span><span class="sxs-lookup"><span data-stu-id="b8ab4-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for hello **File Name** and</span></span>
* <span data-ttu-id="b8ab4-332">Scegliere **Open**(Apri).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-332">Select **Open**.</span></span>
* <span data-ttu-id="b8ab4-333">Scegliere List Drivers (Elenca driver), selezionare **org.postgresql.Driver** in **Class Name** (Nome classe) e quindi scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="b8ab4-334">tooset di server locali di hello connessione toohello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-334">tooset up hello connection toohello local server:</span></span>

* <span data-ttu-id="b8ab4-335">Selezionare **Windows** e quindi **View Aliases** (Visualizza alias).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="b8ab4-336">Scegliere hello  **+**  pulsante toomake un nuovo alias.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-336">Choose hello **+** button toomake a new alias.</span></span>
* <span data-ttu-id="b8ab4-337">Il nome *database posta indesiderata*, scegliere **PostgreSQL** in hello **Driver** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-337">Name it *Spam database*, choose **PostgreSQL** in hello **Driver** drop-down.</span></span>
* <span data-ttu-id="b8ab4-338">Impostare l'URL di hello troppo*jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-338">Set hello URL too*jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="b8ab4-339">Immettere il proprio *nome utente* e la *password*.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="b8ab4-340">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-340">Click **OK**.</span></span>
* <span data-ttu-id="b8ab4-341">hello tooopen **connessione** finestra, fare doppio clic su hello ***database posta indesiderata*** alias.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-341">tooopen hello **Connection** window, double-click hello ***Spam database*** alias.</span></span>
* <span data-ttu-id="b8ab4-342">Selezionare **Connessione**.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-342">Select **Connect**.</span></span>

<span data-ttu-id="b8ab4-343">toorun alcune query:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-343">toorun some queries:</span></span>

* <span data-ttu-id="b8ab4-344">Seleziona hello **SQL** scheda.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-344">Select hello **SQL** tab.</span></span>
* <span data-ttu-id="b8ab4-345">Immettere una query semplice, ad esempio `SELECT * from data;` nella casella di testo query hello nella parte superiore di hello della scheda SQL hello.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-345">Enter a simple query such as `SELECT * from data;` in hello query textbox at hello top of hello SQL tab.</span></span>
* <span data-ttu-id="b8ab4-346">Premere **Ctrl-Invio** toorun è.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-346">Press **Ctrl-Enter** toorun it.</span></span> <span data-ttu-id="b8ab4-347">Per impostazione predefinita esce SQL restituisce hello prime 100 righe della query.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-347">By default Squirrel SQL returns hello first 100 rows from your query.</span></span>

<span data-ttu-id="b8ab4-348">Esistono numerose altre query che è possibile eseguire tooexplore questi dati.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-348">There are many more queries you could run tooexplore this data.</span></span> <span data-ttu-id="b8ab4-349">Ad esempio, funzionamento hello frequenza della parola hello *rendere* differiscono tra posta indesiderata e ham?</span><span class="sxs-lookup"><span data-stu-id="b8ab4-349">For example, how does hello frequency of hello word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="b8ab4-350">O le caratteristiche di hello di posta elettronica che contengono spesso *3d*?</span><span class="sxs-lookup"><span data-stu-id="b8ab4-350">Or what are hello characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="b8ab4-351">La maggior parte dei messaggi di posta elettronica dispone di un'occorrenza elevata di *3d* sono apparentemente inviare posta indesiderata, pertanto potrebbe essere una funzionalità utile per la creazione di messaggi di posta elettronica un hello tooclassify modello predittivo.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model tooclassify hello emails.</span></span>

<span data-ttu-id="b8ab4-352">Se si desidera tooperform l'apprendimento con i dati archiviati in un database PostgreSQL, è consigliabile utilizzare [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-352">If you wanted tooperform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="b8ab4-353">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b8ab4-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="b8ab4-354">Azure SQL Data Warehouse è un database basato sul cloud, con possibilità di aumentare il numero di istanze, che può elaborare volumi massivi di dati sia relazionali che non relazionali.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="b8ab4-355">Per altre informazioni, vedere [Informazioni su Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="b8ab4-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="b8ab4-356">tooconnect toohello dati del data warehouse e creazione tabella hello hello esecuzione seguente comando al prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-356">tooconnect toohello data warehouse and create hello table, run hello following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="b8ab4-357">Al prompt dei comandi sqlcmd hello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-357">Then at hello sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="b8ab4-358">Per copiare dati con bcp, eseguire:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="b8ab4-359">bcp prevista di tipo UNIX, perciò dobbiamo bcp tootell che con il flag - r hello terminazioni riga Hello file scaricato hello sono stile di Windows.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-359">hello line endings in hello downloaded file are Windows-style, but bcp expects UNIX-style, so we need tootell bcp that with hello -r flag.</span></span>
>
>

<span data-ttu-id="b8ab4-360">Eseguire query con sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="b8ab4-361">È anche possibile eseguire query con Squirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="b8ab4-362">Ripetere i passaggi simili per PostgreSQL, tramite il quale è reperibile in hello Microsoft MSSQL Server JDBC Driver ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-362">Follow similar steps for PostgreSQL, using hello Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8ab4-363">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8ab4-363">Next steps</span></span>
<span data-ttu-id="b8ab4-364">Per una panoramica degli argomenti che consentono di eseguire attività di hello che costituiscono il processo di analisi scientifica dei dati hello in Azure, vedere [processo di analisi scientifica dei dati di Team](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-364">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="b8ab4-365">Per una descrizione di altre procedure dettagliate end-to-end che illustrano i passaggi hello hello Team processo di analisi scientifica dei dati per scenari specifici, vedere [procedure dettagliate di processo di analisi scientifica dei dati di Team](data-science-process-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-365">For a description of other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="b8ab4-366">procedure dettagliate di Hello anche illustrano come toocombine cloud e locali strumenti e servizi in un flusso di lavoro o la pipeline di toocreate un'applicazione intelligente.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-366">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>
