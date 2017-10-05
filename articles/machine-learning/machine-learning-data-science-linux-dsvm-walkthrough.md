---
title: Analisi scientifica dei dati in una macchina virtuale Linux per l'analisi scientifica dei dati | Documentazione Microsoft
description: "Come eseguire varie attività comuni di analisi scientifica dei dati con la macchina virtuale Linux per l'analisi scientifica dei dati."
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
ms.openlocfilehash: 6da9a8e3f9f8ac851c2a8deb861ac1d0b3ec5874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="data-science-on-the-linux-data-science-virtual-machine"></a><span data-ttu-id="5c539-103">Analisi scientifica dei dati in una macchina virtuale Linux per l'analisi scientifica dei dati</span><span class="sxs-lookup"><span data-stu-id="5c539-103">Data science on the Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="5c539-104">Questa procedura dettagliata illustra come eseguire varie attività comuni di analisi scientifica dei dati con la macchina virtuale Linux per l'analisi scientifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="5c539-104">This walkthrough shows you how to perform several common data science tasks with the Linux Data Science VM.</span></span> <span data-ttu-id="5c539-105">La macchina virtuale Linux per l'analisi scientifica dei dati (DSVM) è un'immagine di macchina virtuale, disponibile in Azure, in cui è preinstallata una raccolta di strumenti usati comunemente per l'analisi dei dati e l'apprendimento automatico.</span><span class="sxs-lookup"><span data-stu-id="5c539-105">The Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="5c539-106">I componenti software principali sono elencati nell'argomento [Effettuare il provisioning di una macchina virtuale Linux per l'analisi scientifica dei dati](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="5c539-106">The key software components are itemized in the [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="5c539-107">L'immagine di macchina virtuale permette di iniziare le attività di analisi scientifica dei dati in pochi minuti, senza dover installare e configurare ogni strumento singolarmente.</span><span class="sxs-lookup"><span data-stu-id="5c539-107">The VM image makes it easy to get started doing data science in minutes, without having to install and configure each of the tools individually.</span></span> <span data-ttu-id="5c539-108">Se necessario, è possibile aumentare facilmente le prestazioni della macchina virtuale e arrestarla quando non viene usata,</span><span class="sxs-lookup"><span data-stu-id="5c539-108">You can easily scale up the VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="5c539-109">caratteristiche che rendono questa risorsa flessibile e conveniente.</span><span class="sxs-lookup"><span data-stu-id="5c539-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="5c539-110">Le attività di analisi scientifica dei dati illustrate in questa procedura dettagliata seguono i passaggi descritti nel [Processo di analisi scientifica dei dati per i team](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="5c539-110">The data science tasks demonstrated in this walkthrough follow the steps outlined in the [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="5c539-111">Questo processo offre un approccio sistematico all'analisi scientifica dei dati, che permette ai team di data scientist di collaborare in modo efficace al ciclo di vita della compilazione di applicazioni intelligenti.</span><span class="sxs-lookup"><span data-stu-id="5c539-111">This process provides a systematic approach to data science that enables teams of data scientists to effectively collaborate over the lifecycle of building intelligent applications.</span></span> <span data-ttu-id="5c539-112">Il processo di analisi scientifica dei dati fornisce anche un framework iterativo di analisi scientifica dei dati da seguire.</span><span class="sxs-lookup"><span data-stu-id="5c539-112">The data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="5c539-113">Questa procedura dettagliata illustra il set di dati [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) .</span><span class="sxs-lookup"><span data-stu-id="5c539-113">We analyze the [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="5c539-114">Si tratta di un set di messaggi di posta elettronica contrassegnati come posta indesiderata o ham, ovvero non indesiderata.</span><span class="sxs-lookup"><span data-stu-id="5c539-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on the content of the emails.</span></span> <span data-ttu-id="5c539-115">Il set contiene anche alcune statistiche sul contenuto dei messaggi di posta elettronica che verranno illustrate più avanti in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="5c539-115">The statistics included are discussed in the next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c539-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5c539-116">Prerequisites</span></span>
<span data-ttu-id="5c539-117">Prima di usare una macchina virtuale Linux per l'analisi scientifica dei dati, è necessario avere a disposizione quanto segue:</span><span class="sxs-lookup"><span data-stu-id="5c539-117">Before you can use a Linux Data Science Virtual Machine, you must have the following:</span></span>

* <span data-ttu-id="5c539-118">Una **sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="5c539-118">An **Azure subscription**.</span></span> <span data-ttu-id="5c539-119">Se non è già disponibile, vedere [Crea subito il tuo account Azure gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="5c539-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="5c539-120">Una [**macchina virtuale Linux per l'analisi scientifica dei dati**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="5c539-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="5c539-121">Per informazioni sul provisioning di questa macchina virtuale, vedere [Effettuare il provisioning di una macchina virtuale Linux per l'analisi scientifica dei dati](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="5c539-121">For information on provisioning this VM, see [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="5c539-122">[X2Go](http://wiki.x2go.org/doku.php) installato nel computer con una sessione di XFCE aperta.</span><span class="sxs-lookup"><span data-stu-id="5c539-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="5c539-123">Per informazioni sull'installazione e la configurazione di un **client X2Go**, vedere [Installazione e configurazione del client X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="5c539-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="5c539-124">Un **account Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="5c539-124">An **AzureML account**.</span></span> <span data-ttu-id="5c539-125">Se non è già disponibile, è possibile iscriversi e ottenere un nuovo account nella [home page di Azure ML](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5c539-125">If you don't already have one, sign up for new one at the [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="5c539-126">Il livello di utilizzo gratuito permette di iniziare.</span><span class="sxs-lookup"><span data-stu-id="5c539-126">There is a free usage tier to help you get started.</span></span>

## <a name="download-the-spambase-dataset"></a><span data-ttu-id="5c539-127">Scaricare il set di dati spambase</span><span class="sxs-lookup"><span data-stu-id="5c539-127">Download the spambase dataset</span></span>
<span data-ttu-id="5c539-128">Il set di dati [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) è un set di dati relativamente piccolo che contiene solo 4601 esempi.</span><span class="sxs-lookup"><span data-stu-id="5c539-128">The [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="5c539-129">Grazie alle dimensioni ridotte può essere usato per dimostrare alcune delle funzionalità principali della macchina virtuale per l'analisi scientifica dei dati, perché i requisiti in termini di risorse rimangono contenuti.</span><span class="sxs-lookup"><span data-stu-id="5c539-129">This is a convenient size to use when demonstrating that some of the key features of the Data Science VM as it keeps the resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="5c539-130">Questa procedura dettagliata è stata creata in una macchina virtuale Linux per l'analisi scientifica dei dati di dimensioni D2 v2.</span><span class="sxs-lookup"><span data-stu-id="5c539-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="5c539-131">Le dimensioni della DSVM permettono di gestire le procedure descritte in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="5c539-131">This size DSVM is capable of handling the procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="5c539-132">Se è necessario più spazio di archiviazione, è possibile creare altri dischi e collegarli alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5c539-132">If you need more storage space, you can create additional disks and attach them to your VM.</span></span> <span data-ttu-id="5c539-133">Dato che questi dischi usano l'archiviazione di Azure persistente, i relativi dati vengono conservati anche quando il server viene arrestato o sottoposto a un nuovo provisioning in seguito a un ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="5c539-133">These disks use persistent Azure storage, so their data is preserved even when the server is reprovisioned due to resizing or is shut down.</span></span> <span data-ttu-id="5c539-134">Per aggiungere un disco e collegarlo alla macchina virtuale, seguire le istruzioni in [Aggiungere un disco a una VM Linux](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c539-134">To add a disk and attach it to your VM, follow the instructions in [Add a disk to a Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="5c539-135">Questa procedura usa l'interfaccia della riga di comando di Azure, già installata nella DSVM,</span><span class="sxs-lookup"><span data-stu-id="5c539-135">These steps use the Azure Command-Line Interface (Azure CLI), which is already installed on the DSVM.</span></span> <span data-ttu-id="5c539-136">e può quindi essere eseguita interamente dalla macchina virtuale stessa.</span><span class="sxs-lookup"><span data-stu-id="5c539-136">So these procedures can be done entirely from the VM itself.</span></span> <span data-ttu-id="5c539-137">Per aumentare lo spazio di archiviazione, è anche possibile usare l'[archiviazione file di Azure](../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5c539-137">Another option to increase storage is to use [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="5c539-138">Per scaricare i dati, aprire una finestra del terminale ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="5c539-138">To download the data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="5c539-139">Il file scaricato non ha una riga di intestazione. È quindi necessario creare un altro file che abbia un'intestazione.</span><span class="sxs-lookup"><span data-stu-id="5c539-139">The downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="5c539-140">Eseguire questo comando per creare un file con le intestazioni appropriate:</span><span class="sxs-lookup"><span data-stu-id="5c539-140">Run this command to create a file with the appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="5c539-141">Quindi, concatenare i due file usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5c539-141">Then concatenate the two files together with the command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="5c539-142">Il set di dati include diversi tipi di statistiche per ogni messaggio di posta elettronica:</span><span class="sxs-lookup"><span data-stu-id="5c539-142">The dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="5c539-143">Le colonne come ***word\_freq\_WORD*** indicano la percentuale di parole nel messaggio di posta elettronica che corrispondono a *WORD*.</span><span class="sxs-lookup"><span data-stu-id="5c539-143">Columns like ***word\_freq\_WORD*** indicate the percentage of words in the email that match *WORD*.</span></span> <span data-ttu-id="5c539-144">Ad esempio, se *word\_freq\_make* è 1, l'1% di tutte le parole nel messaggio di posta elettronica è costituito dalla parola *make*.</span><span class="sxs-lookup"><span data-stu-id="5c539-144">For example, if *word\_freq\_make* is 1, then 1% of all words in the email were *make*.</span></span>
* <span data-ttu-id="5c539-145">Le colonne come ***char\_freq\_CHAR*** indicano la percentuale di caratteri *CHAR* nel messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="5c539-145">Columns like ***char\_freq\_CHAR*** indicate the percentage of all characters in the email that were *CHAR*.</span></span>
* <span data-ttu-id="5c539-146">***capital\_run\_length\_longest*** è la lunghezza massima di una sequenza di lettere maiuscole.</span><span class="sxs-lookup"><span data-stu-id="5c539-146">***capital\_run\_length\_longest*** is the longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="5c539-147">***capital\_run\_length\_average*** è la lunghezza media di tutte le sequenze di lettere maiuscole.</span><span class="sxs-lookup"><span data-stu-id="5c539-147">***capital\_run\_length\_average*** is the average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="5c539-148">***capital\_run\_length\_total*** è la lunghezza totale di tutte le sequenze di lettere maiuscole.</span><span class="sxs-lookup"><span data-stu-id="5c539-148">***capital\_run\_length\_total*** is the total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="5c539-149">***spam*** indica se il messaggio di posta elettronica è stato considerato posta indesiderata o meno: 1 = posta indesiderata, 0 = posta non indesiderata.</span><span class="sxs-lookup"><span data-stu-id="5c539-149">***spam*** indicates whether the email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-the-dataset-with-microsoft-r-open"></a><span data-ttu-id="5c539-150">Esplorare il set di dati con Microsoft R Open</span><span class="sxs-lookup"><span data-stu-id="5c539-150">Explore the dataset with Microsoft R Open</span></span>
<span data-ttu-id="5c539-151">Si passa ora all'esame dei dati e all'esecuzione di alcune attività di apprendimento automatico di base con R. La macchina virtuale per l'analisi scientifica dei dati viene fornita con [Microsoft R Open](https://mran.revolutionanalytics.com/open/) preinstallato.</span><span class="sxs-lookup"><span data-stu-id="5c539-151">Let's examine the data and do some basic machine learning with R. The Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="5c539-152">Le librerie matematiche multithreading in questa versione di R offrono prestazioni migliori rispetto a diverse versioni a thread singolo.</span><span class="sxs-lookup"><span data-stu-id="5c539-152">The multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="5c539-153">Microsoft R Open garantisce anche la riproducibilità grazie all'uso di uno snapshot del repository dei pacchetti CRAN.</span><span class="sxs-lookup"><span data-stu-id="5c539-153">Microsoft R Open also provides reproducibility by using a snapshot of the CRAN package repository.</span></span>

<span data-ttu-id="5c539-154">Per ottenere copie degli esempi di codice usati in questa procedura dettagliata, clonare il repository **Azure-Machine-Learning-Data-Science** usando Git, che è preinstallato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5c539-154">To get copies of the code samples used in this walkthrough, clone the **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on the VM.</span></span> <span data-ttu-id="5c539-155">Dalla riga di comando di Git, eseguire:</span><span class="sxs-lookup"><span data-stu-id="5c539-155">From the git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="5c539-156">Aprire una finestra del terminale e avviare una nuova sessione di R con la console interattiva di R.</span><span class="sxs-lookup"><span data-stu-id="5c539-156">Open a terminal window and start a new R session with the R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="5c539-157">Per le procedure seguenti è possibile usare anche RStudio.</span><span class="sxs-lookup"><span data-stu-id="5c539-157">You can also use RStudio for the following procedures.</span></span> <span data-ttu-id="5c539-158">Per installare RStudio, eseguire questo comando a un terminale: `./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="5c539-158">To install RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="5c539-159">Per importare i dati e configurare l'ambiente, eseguire:</span><span class="sxs-lookup"><span data-stu-id="5c539-159">To import the data and set up the environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="5c539-160">Per visualizzare le statistiche di riepilogo relative a ogni colonna, usare:</span><span class="sxs-lookup"><span data-stu-id="5c539-160">To see summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="5c539-161">Per una visualizzazione diversa dei dati, usare:</span><span class="sxs-lookup"><span data-stu-id="5c539-161">For a different view of the data:</span></span>

    str(data)

<span data-ttu-id="5c539-162">Questa visualizzazione mostra il tipo di ogni variabile e i primi valori nel set di dati.</span><span class="sxs-lookup"><span data-stu-id="5c539-162">This shows you the type of each variable and the first few values in the dataset.</span></span>

<span data-ttu-id="5c539-163">La colonna *spam* è stata letta come Integer, ma in realtà si tratta di un fattore o una variabile categorica.</span><span class="sxs-lookup"><span data-stu-id="5c539-163">The *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="5c539-164">Per impostarne il tipo, usare:</span><span class="sxs-lookup"><span data-stu-id="5c539-164">To set its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="5c539-165">Per effettuare alcune analisi esplorative, usare il pacchetto [ggplot2](http://ggplot2.org/) , una diffusa libreria grafica per R già installata nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5c539-165">To do some exploratory analysis, use the [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on the VM.</span></span> <span data-ttu-id="5c539-166">Grazie ai dati di riepilogo visualizzati in precedenza, sono disponibili statistiche di riepilogo sulla frequenza del carattere punto esclamativo.</span><span class="sxs-lookup"><span data-stu-id="5c539-166">Note, from the summary data displayed earlier, that we have summary statistics on the frequency of the exclamation mark character.</span></span> <span data-ttu-id="5c539-167">I comandi seguenti permettono di tracciare tali frequenze:</span><span class="sxs-lookup"><span data-stu-id="5c539-167">Let's plot those frequencies here with the following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="5c539-168">Per eliminare l'alterazione causata dalla barra dello zero, usare:</span><span class="sxs-lookup"><span data-stu-id="5c539-168">Since the zero bar is skewing the plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="5c539-169">La densità non semplice superiore a 1 sembra interessante.</span><span class="sxs-lookup"><span data-stu-id="5c539-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="5c539-170">Per esaminare solo quei dati, eseguire:</span><span class="sxs-lookup"><span data-stu-id="5c539-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="5c539-171">Per dividere quindi i dati in posta indesiderata e non indesiderata, eseguire:</span><span class="sxs-lookup"><span data-stu-id="5c539-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="5c539-172">In base a questi esempi è possibile creare tracciati simili delle altre colonne per esplorare i dati in esse contenuti.</span><span class="sxs-lookup"><span data-stu-id="5c539-172">These examples should enable you to make similar plots of the other columns to explore the data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="5c539-173">Eseguire il training di un modello ML e testarlo</span><span class="sxs-lookup"><span data-stu-id="5c539-173">Train and test an ML model</span></span>
<span data-ttu-id="5c539-174">A questo punto è possibile eseguire il training di un paio di modelli di apprendimento automatico per classificare i messaggi di posta elettronica nel set di dati come posta indesiderata o non indesiderata.</span><span class="sxs-lookup"><span data-stu-id="5c539-174">Now let's train a couple of machine learning models to classify the emails in the dataset as containing either span or ham.</span></span> <span data-ttu-id="5c539-175">Questa sezione illustra come eseguire il training di un modello di albero delle decisioni e di un modello di foresta casuale e quindi testarne la correttezza delle previsioni.</span><span class="sxs-lookup"><span data-stu-id="5c539-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="5c539-176">Il pacchetto rpart, che sta per partizionamento ricorsivo e alberi di regressione, usato nel codice seguente è già installato nella macchina virtuale per l'analisi scientifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="5c539-176">The rpart (Recursive Partitioning and Regression Trees) package used in the following code is already installed on the Data Science VM.</span></span>
>
>

<span data-ttu-id="5c539-177">Dividere prima di tutto il set di dati in set di training e set di test:</span><span class="sxs-lookup"><span data-stu-id="5c539-177">First, let's split the dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="5c539-178">Quindi, creare un albero delle decisioni per classificare i messaggi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="5c539-178">And then create a decision tree to classify the emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="5c539-179">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="5c539-179">Here is the result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="5c539-181">Per determinarne le prestazioni sul set di training, usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="5c539-181">To determine how well it performs on the training set, use the following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="5c539-182">Per determinarne le prestazioni sul set di test, eseguire:</span><span class="sxs-lookup"><span data-stu-id="5c539-182">To determine how well it performs on the test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="5c539-183">Viene ora esaminato un modello di foresta casuale.</span><span class="sxs-lookup"><span data-stu-id="5c539-183">Let's also try a random forest model.</span></span> <span data-ttu-id="5c539-184">Le foreste casuali permettono di eseguire il training di numerosi alberi delle decisioni e restituiscono una classe che rappresenta la modalità delle classificazioni da tutti i singoli alberi delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="5c539-184">Random forests train a multitude of decision trees and output a class that is the mode of the classifications from all of the individual decision trees.</span></span> <span data-ttu-id="5c539-185">Offrono un approccio più efficace all'apprendimento automatico perché compensano la tendenza all'overfitting del set di dati di training da parte del modello di albero delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="5c539-185">They provide a more powerful machine learning approach as they correct for the tendency of a decision tree model to overfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-to-azure-ml"></a><span data-ttu-id="5c539-186">Distribuire un modello in Azure ML</span><span class="sxs-lookup"><span data-stu-id="5c539-186">Deploy a model to Azure ML</span></span>
<span data-ttu-id="5c539-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (Azure ML) è un servizio cloud che semplifica la compilazione e la distribuzione di modelli di analisi predittiva.</span><span class="sxs-lookup"><span data-stu-id="5c539-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy to build and deploy predictive analytics models.</span></span> <span data-ttu-id="5c539-188">Una funzionalità interessante di Azure ML è la possibilità di pubblicare qualsiasi funzione R come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="5c539-188">One of the nice features of AzureML is its ability to publish any R function as a web service.</span></span> <span data-ttu-id="5c539-189">Il pacchetto R di Azure ML permette di eseguire la distribuzione direttamente dalla sessione di R nella macchina virtuale per l'analisi scientifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="5c539-189">The AzureML R package makes deployment easy to do right from our R session on the DSVM.</span></span>

<span data-ttu-id="5c539-190">Per distribuire il codice dell'albero delle decisioni della sezione precedente, occorre eseguire l'accesso ad Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5c539-190">To deploy the decision tree code from the previous section, you need to sign in to Azure Machine Learning Studio.</span></span> <span data-ttu-id="5c539-191">A tale scopo sono necessari l'ID dell'area di lavoro e un token di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="5c539-191">You need your workspace ID and an authorization token to sign in.</span></span> <span data-ttu-id="5c539-192">Per trovare questi valori e usarli per inizializzare le variabili di Azure ML, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="5c539-192">To find these values and initialize the AzureML variables with them:</span></span>

<span data-ttu-id="5c539-193">Selezionare **SETTINGS** (Impostazioni) dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="5c539-193">Select **Settings** on the left-hand menu.</span></span> <span data-ttu-id="5c539-194">Prendere nota del valore **WORKSPACE ID**(ID area di lavoro).</span><span class="sxs-lookup"><span data-stu-id="5c539-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="5c539-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="5c539-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="5c539-196">Selezionare **Authorization Tokens** (Token di autorizzazione) dal menu in alto e prendere nota del valore di **Primary Authorization Token** (Token di autorizzazione primario).![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="5c539-196">Select **Authorization Tokens** from the overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="5c539-197">Caricare il pacchetto di **Azure ML** e quindi impostare i valori delle variabili con il token e l'ID area di lavoro nella sessione di R nella DSVM:</span><span class="sxs-lookup"><span data-stu-id="5c539-197">Load the **AzureML** package and then set values of the variables with your token and workspace ID in your R session on the DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="5c539-198">Il modello viene semplificato per agevolare l'implementazione di questa dimostrazione.</span><span class="sxs-lookup"><span data-stu-id="5c539-198">Let's simplify the model to make this demonstration easier to implement.</span></span> <span data-ttu-id="5c539-199">Nell'albero delle decisioni selezionare le tre variabili più vicine alla radice e compilare un nuovo albero usando solo quelle tre variabili:</span><span class="sxs-lookup"><span data-stu-id="5c539-199">Pick the three variables in the decision tree closest to the root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="5c539-200">È necessaria una funzione di previsione che usa le funzionalità come input e restituisce i valori previsti:</span><span class="sxs-lookup"><span data-stu-id="5c539-200">We need a prediction function that takes the features as an input and returns the predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="5c539-201">Pubblicare la funzione predictSpam in Azure ML usando la funzione **publishWebService** :</span><span class="sxs-lookup"><span data-stu-id="5c539-201">Publish the predictSpam function to AzureML using the **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="5c539-202">Questa funzione accetta la funzione **predictSpam**, crea un servizio Web denominato **spamWebService** con gli input e gli output definiti e restituisce informazioni relative al nuovo endpoint.</span><span class="sxs-lookup"><span data-stu-id="5c539-202">This function takes the **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about the new endpoint.</span></span>

<span data-ttu-id="5c539-203">Per visualizzare i dettagli del servizio Web pubblicato, inclusi l'endpoint API e le chiavi di accesso, usare il comando:</span><span class="sxs-lookup"><span data-stu-id="5c539-203">View details of the published web service, including its API endpoint and access keys with the command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="5c539-204">Per fare una prova sulle prime dieci righe del set di test, eseguire:</span><span class="sxs-lookup"><span data-stu-id="5c539-204">To try it out on the first 10 rows of the test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="5c539-205">Usare altri strumenti disponibili</span><span class="sxs-lookup"><span data-stu-id="5c539-205">Use other tools available</span></span>
<span data-ttu-id="5c539-206">Le sezioni seguenti illustrano come usare alcuni degli strumenti installati nella macchina virtuale Linux per l'analisi scientifica dei dati. Gli strumenti descritti sono elencati di seguito:</span><span class="sxs-lookup"><span data-stu-id="5c539-206">The remaining sections show how to use some of the tools installed on the Linux Data Science VM.Here is the list of tools discussed:</span></span>

* <span data-ttu-id="5c539-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="5c539-207">XGBoost</span></span>
* <span data-ttu-id="5c539-208">Python</span><span class="sxs-lookup"><span data-stu-id="5c539-208">Python</span></span>
* <span data-ttu-id="5c539-209">JupyterHub</span><span class="sxs-lookup"><span data-stu-id="5c539-209">Jupyterhub</span></span>
* <span data-ttu-id="5c539-210">Rattle</span><span class="sxs-lookup"><span data-stu-id="5c539-210">Rattle</span></span>
* <span data-ttu-id="5c539-211">PostgreSQL e Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="5c539-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="5c539-212">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5c539-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="5c539-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="5c539-213">XGBoost</span></span>
<span data-ttu-id="5c539-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) è uno strumento che consente un'implementazione di albero con boosting rapida e accurata.</span><span class="sxs-lookup"><span data-stu-id="5c539-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

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

<span data-ttu-id="5c539-215">XGBoost permette anche di eseguire chiamate da Python o da una riga di comando.</span><span class="sxs-lookup"><span data-stu-id="5c539-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="5c539-216">Python</span><span class="sxs-lookup"><span data-stu-id="5c539-216">Python</span></span>
<span data-ttu-id="5c539-217">Per lo sviluppo tramite Python, nella DSVM sono installate le distribuzioni Anaconda Python 2.7 e 3.5.</span><span class="sxs-lookup"><span data-stu-id="5c539-217">For development using Python, the Anaconda Python distributions 2.7 and 3.5 have been installed in the DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="5c539-218">La distribuzione Anaconda include [Condas](http://conda.pydata.org/docs/index.html), che può essere usato per creare ambienti personalizzati per Python in cui sono installati pacchetti diversi e/o versioni diverse.</span><span class="sxs-lookup"><span data-stu-id="5c539-218">The Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used to create custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="5c539-219">Leggere una parte del set di dati spambase e classificare i messaggi di posta elettronica con macchine a vettori di supporto in scikit-learn:</span><span class="sxs-lookup"><span data-stu-id="5c539-219">Let's read in some of the spambase dataset and classify the emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="5c539-220">Per eseguire previsioni, usare:</span><span class="sxs-lookup"><span data-stu-id="5c539-220">To make predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="5c539-221">Per illustrare la pubblicazione di un endpoint di Azure ML viene creato un modello più semplice con tre variabili, come si è fatto in precedenza per la pubblicazione del modello R.</span><span class="sxs-lookup"><span data-stu-id="5c539-221">To show how to publish an AzureML endpoint, let's make a simpler model the three variables as we did when we published the R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="5c539-222">Per pubblicare il modello in Azure ML, eseguire:</span><span class="sxs-lookup"><span data-stu-id="5c539-222">To publish the model to AzureML:</span></span>

    # Publish the model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about the resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call the model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="5c539-223">È disponibile solo per Python 2.7 e non è ancora supportato nella versione 3.5.</span><span class="sxs-lookup"><span data-stu-id="5c539-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="5c539-224">Eseguire con **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="5c539-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="5c539-225">JupyterHub</span><span class="sxs-lookup"><span data-stu-id="5c539-225">Jupyterhub</span></span>
<span data-ttu-id="5c539-226">La distribuzione Anaconda nella DSVM include un notebook di Jupyter, un ambiente multipiattaforma per la condivisione di analisi e codice Python, R o Julia.</span><span class="sxs-lookup"><span data-stu-id="5c539-226">The Anaconda distribution in the DSVM comes with a Jupyter notebook, a cross-platform environment to share Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="5c539-227">Notebook di Jupyter è accessibile tramite JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="5c539-227">The Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="5c539-228">Per eseguire l'accesso, usare il nome utente e la password locali di ***https://\<Nome DNS o indirizzo IP della VM\>:8000/***.</span><span class="sxs-lookup"><span data-stu-id="5c539-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="5c539-229">Tutti i file di configurazione per JupyterHub si trovano nella directory **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="5c539-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="5c539-230">Nella macchina virtuale sono già installati diversi notebook di esempio:</span><span class="sxs-lookup"><span data-stu-id="5c539-230">Several sample notebooks are already installed on the VM:</span></span>

* <span data-ttu-id="5c539-231">Per un notebook di Python di esempio, vedere [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) .</span><span class="sxs-lookup"><span data-stu-id="5c539-231">See the [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="5c539-232">Per un notebook di [R](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) di esempio, vedere **IntroTutorialinR** .</span><span class="sxs-lookup"><span data-stu-id="5c539-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="5c539-233">Per un altro notebook di [Python](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) di esempio, vedere **IrisClassifierPyMLWebService** .</span><span class="sxs-lookup"><span data-stu-id="5c539-233">See the [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="5c539-234">Il linguaggio Julia è disponibile anche dalla riga di comando nella macchina virtuale Linux per l'analisi scientifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="5c539-234">The Julia language is also available from the command line on the Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="5c539-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="5c539-235">Rattle</span></span>
<span data-ttu-id="5c539-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) , acronimo di R Analytical Tool To Learn Easily, è uno strumento grafico di R per il data mining.</span><span class="sxs-lookup"><span data-stu-id="5c539-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (the R Analytical Tool To Learn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="5c539-237">È dotato di un'interfaccia intuitiva che permette di caricare, esplorare e trasformare i dati e di creare e valutare i modelli in modo molto semplice.</span><span class="sxs-lookup"><span data-stu-id="5c539-237">It has an intuitive interface that makes it easy to load, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="5c539-238">Per una procedura dettagliata che ne illustra le funzionalità, vedere l'articolo [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) (Rattle: un'interfaccia utente grafica di data mining per R).</span><span class="sxs-lookup"><span data-stu-id="5c539-238">The article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="5c539-239">Installare e avviare Rattle con i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5c539-239">Install and start Rattle with the following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="5c539-240">L'installazione nella DSVM non è obbligatoria,</span><span class="sxs-lookup"><span data-stu-id="5c539-240">Installation is not required on the DSVM.</span></span> <span data-ttu-id="5c539-241">ma Rattle può richiedere di installare pacchetti aggiuntivi al momento del caricamento.</span><span class="sxs-lookup"><span data-stu-id="5c539-241">But Rattle may prompt you to install additional packages when it loads.</span></span>
>
>

<span data-ttu-id="5c539-242">Rattle usa un'interfaccia basata su schede.</span><span class="sxs-lookup"><span data-stu-id="5c539-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="5c539-243">La maggior parte delle schede corrisponde ai passaggi del [Processo di analisi scientifica dei dati](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), come il caricamento dei dati o l'esplorazione.</span><span class="sxs-lookup"><span data-stu-id="5c539-243">Most of the tabs correspond to steps in the [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="5c539-244">Il processo di analisi scientifica dei dati va da sinistra a destra nelle schede,</span><span class="sxs-lookup"><span data-stu-id="5c539-244">The data science process flows from left to right through the tabs.</span></span> <span data-ttu-id="5c539-245">ma l'ultima scheda contiene un log dei comandi R eseguiti da Rattle.</span><span class="sxs-lookup"><span data-stu-id="5c539-245">But the last tab contains a log of the R commands run by Rattle.</span></span>

<span data-ttu-id="5c539-246">Per caricare e configurare il set di dati:</span><span class="sxs-lookup"><span data-stu-id="5c539-246">To load and configure the dataset:</span></span>

* <span data-ttu-id="5c539-247">Per caricare il file, selezionare la scheda **Data** (Dati).</span><span class="sxs-lookup"><span data-stu-id="5c539-247">To load the file, select the **Data** tab, then</span></span>
* <span data-ttu-id="5c539-248">Fare clic sul selettore accanto a **Filename** (Nome file) e scegliere **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="5c539-248">Choose the selector next to **Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="5c539-249">Per caricare il file,</span><span class="sxs-lookup"><span data-stu-id="5c539-249">To load the file.</span></span> <span data-ttu-id="5c539-250">selezionare **Execute** (Esegui) nella riga superiore dei pulsanti.</span><span class="sxs-lookup"><span data-stu-id="5c539-250">select **Execute** in the top row of buttons.</span></span> <span data-ttu-id="5c539-251">Verrà visualizzato un riepilogo di ogni colonna, incluso il tipo di dati identificato, se si tratta di un input, una destinazione o un altro tipo di variabile e il numero di valori univoci.</span><span class="sxs-lookup"><span data-stu-id="5c539-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and the number of unique values.</span></span>
* <span data-ttu-id="5c539-252">Rattle ha identificato correttamente la colonna **spam** come destinazione.</span><span class="sxs-lookup"><span data-stu-id="5c539-252">Rattle has correctly identified the **spam** column as the target.</span></span> <span data-ttu-id="5c539-253">Selezionare la colonna e quindi impostare **Target Data Type** (Tipo di dati di destinazione) su **Categoric** (Categorico).</span><span class="sxs-lookup"><span data-stu-id="5c539-253">Select the spam column, then set the **Target Data Type** to **Categoric**.</span></span>

<span data-ttu-id="5c539-254">Per esplorare i dati:</span><span class="sxs-lookup"><span data-stu-id="5c539-254">To explore the data:</span></span>

* <span data-ttu-id="5c539-255">Selezionare la scheda **Explore** (Esplora).</span><span class="sxs-lookup"><span data-stu-id="5c539-255">Select the **Explore** tab.</span></span>
* <span data-ttu-id="5c539-256">Fare clic su **Summary** (Riepilogo) e quindi su **Execute** (Esegui) per visualizzare alcune informazioni sui tipi di variabili e le statistiche di riepilogo.</span><span class="sxs-lookup"><span data-stu-id="5c539-256">Click **Summary**, then **Execute**, to see some information about the variable types and some summary statistics.</span></span>
* <span data-ttu-id="5c539-257">Per visualizzare altri tipi di statistiche sulle singole variabili, selezionare altre opzioni, ad esempio **Describe** (Descrizione) o **Basics** (Informazioni di base).</span><span class="sxs-lookup"><span data-stu-id="5c539-257">To view other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="5c539-258">La scheda **Explore** (Esplora) permette anche di generare molti tracciati dettagliati.</span><span class="sxs-lookup"><span data-stu-id="5c539-258">The **Explore** tab also allows you to generate many insightful plots.</span></span> <span data-ttu-id="5c539-259">Per tracciare un istogramma dei dati:</span><span class="sxs-lookup"><span data-stu-id="5c539-259">To plot a histogram of the data:</span></span>

* <span data-ttu-id="5c539-260">Scegliere **Distributions**(Distribuzioni).</span><span class="sxs-lookup"><span data-stu-id="5c539-260">Select **Distributions**.</span></span>
* <span data-ttu-id="5c539-261">Selezionare **Histogram** (Istogramma) per **word_freq_remove** e **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="5c539-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="5c539-262">Scegliere **Execute**(Esegui).</span><span class="sxs-lookup"><span data-stu-id="5c539-262">Select **Execute**.</span></span> <span data-ttu-id="5c539-263">Entrambi i tracciati di densità verranno visualizzati in un'unica area grafica, in cui appare chiaro che nei messaggi di posta elettronica la parola "you" è molto più frequente della parola "remove".</span><span class="sxs-lookup"><span data-stu-id="5c539-263">You should see both density plots in a single graph window, where it is clear that the word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="5c539-264">Anche i tracciati di correlazione sono interessanti.</span><span class="sxs-lookup"><span data-stu-id="5c539-264">The Correlation plots are also interesting.</span></span> <span data-ttu-id="5c539-265">Per crearne uno:</span><span class="sxs-lookup"><span data-stu-id="5c539-265">To create one:</span></span>

* <span data-ttu-id="5c539-266">Scegliere **Correlation** (Correlazione) per **Type** (Tipo).</span><span class="sxs-lookup"><span data-stu-id="5c539-266">Choose **Correlation** as the **Type**, then</span></span>
* <span data-ttu-id="5c539-267">Scegliere **Execute**(Esegui).</span><span class="sxs-lookup"><span data-stu-id="5c539-267">Select **Execute**.</span></span>
* <span data-ttu-id="5c539-268">Rattle avvisa l'utente che è consigliabile usare un massimo di 40 variabili.</span><span class="sxs-lookup"><span data-stu-id="5c539-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="5c539-269">Scegliere **Yes** (Sì) per visualizzare il tracciato.</span><span class="sxs-lookup"><span data-stu-id="5c539-269">Select **Yes** to view the plot.</span></span>

<span data-ttu-id="5c539-270">Vengono evidenziate alcune correlazioni interessanti. Ad esempio, la parola "technology" è strettamente correlata a "HP" e "labs".</span><span class="sxs-lookup"><span data-stu-id="5c539-270">There are some interesting correlations that come up: "technology" is strongly correlated to "HP" and "labs", for example.</span></span> <span data-ttu-id="5c539-271">È strettamente correlata anche a "650", perché l'indicativo di località dei donatori di set di dati è 650.</span><span class="sxs-lookup"><span data-stu-id="5c539-271">It is also strongly correlated to "650", because the area code of the dataset donors is 650.</span></span>

<span data-ttu-id="5c539-272">I valori numerici per le correlazioni tra le parole sono disponibili nella finestra di esplorazione.</span><span class="sxs-lookup"><span data-stu-id="5c539-272">The numeric values for the correlations between words are available in the Explore window.</span></span> <span data-ttu-id="5c539-273">È interessante notare, ad esempio, che la parola "technology" è correlata negativamente a "your" e "money".</span><span class="sxs-lookup"><span data-stu-id="5c539-273">It is interesting to note, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="5c539-274">Rattle può trasformare il set di dati per gestire alcuni problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="5c539-274">Rattle can transform the dataset to handle some common issues.</span></span> <span data-ttu-id="5c539-275">Ad esempio, permette di ridimensionare le funzionalità, attribuire valori mancanti, gestire gli outlier e rimuovere variabili o osservazioni con dati mancanti.</span><span class="sxs-lookup"><span data-stu-id="5c539-275">For example, it allows you to rescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="5c539-276">Rattle può anche identificare le regole di associazione tra le osservazioni e/o le variabili.</span><span class="sxs-lookup"><span data-stu-id="5c539-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="5c539-277">Queste schede non rientrano nell'ambito di questa procedura dettagliata introduttiva.</span><span class="sxs-lookup"><span data-stu-id="5c539-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="5c539-278">Rattle permette anche di eseguire l'analisi a cluster.</span><span class="sxs-lookup"><span data-stu-id="5c539-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="5c539-279">Escludere ora alcune funzionalità per migliorare la leggibilità dell'output.</span><span class="sxs-lookup"><span data-stu-id="5c539-279">Let's exclude some features to make the output easier to read.</span></span> <span data-ttu-id="5c539-280">Nella scheda **Data** (Dati) scegliere **Ignore** (Ignora) accanto a ogni variabile, a eccezione di questi dieci elementi:</span><span class="sxs-lookup"><span data-stu-id="5c539-280">On the **Data** tab, choose **Ignore** next to each of the variables except these ten items:</span></span>

* <span data-ttu-id="5c539-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="5c539-281">word_freq_hp</span></span>
* <span data-ttu-id="5c539-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="5c539-282">word_freq_technology</span></span>
* <span data-ttu-id="5c539-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="5c539-283">word_freq_george</span></span>
* <span data-ttu-id="5c539-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="5c539-284">word_freq_remove</span></span>
* <span data-ttu-id="5c539-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="5c539-285">word_freq_your</span></span>
* <span data-ttu-id="5c539-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="5c539-286">word_freq_dollar</span></span>
* <span data-ttu-id="5c539-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="5c539-287">word_freq_money</span></span>
* <span data-ttu-id="5c539-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="5c539-288">capital_run_length_longest</span></span>
* <span data-ttu-id="5c539-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="5c539-289">word_freq_business</span></span>
* <span data-ttu-id="5c539-290">spam</span><span class="sxs-lookup"><span data-stu-id="5c539-290">spam</span></span>

<span data-ttu-id="5c539-291">Tornare quindi alla scheda **Cluster**, scegliere **KMeans** e impostare *Number of clusters* (Numero di cluster) su 4.</span><span class="sxs-lookup"><span data-stu-id="5c539-291">Then go back to the **Cluster** tab, choose **KMeans**, and set the *Number of clusters* to 4.</span></span> <span data-ttu-id="5c539-292">Scegliere **Execute**(Esegui).</span><span class="sxs-lookup"><span data-stu-id="5c539-292">Then **Execute**.</span></span> <span data-ttu-id="5c539-293">I risultati verranno visualizzati nella finestra di output.</span><span class="sxs-lookup"><span data-stu-id="5c539-293">The results are displayed in the output window.</span></span> <span data-ttu-id="5c539-294">Un cluster ha una frequenza elevata di "george" e "hp" ed è probabilmente un messaggio di lavoro legittimo.</span><span class="sxs-lookup"><span data-stu-id="5c539-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="5c539-295">Per compilare un modello di apprendimento automatico ad albero decisionale:</span><span class="sxs-lookup"><span data-stu-id="5c539-295">To build a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="5c539-296">Scegliere la scheda **Model** (Modello).</span><span class="sxs-lookup"><span data-stu-id="5c539-296">Select the **Model** tab,</span></span>
* <span data-ttu-id="5c539-297">Selezionare **Tree** (Albero) per **Type** (Tipo).</span><span class="sxs-lookup"><span data-stu-id="5c539-297">Choose **Tree** as the **Type**.</span></span>
* <span data-ttu-id="5c539-298">Selezionare **Execute** (Esegui) per visualizzare l'albero in formato testo nella finestra di output.</span><span class="sxs-lookup"><span data-stu-id="5c539-298">Select **Execute** to display the tree in text form in the output window.</span></span>
* <span data-ttu-id="5c539-299">Fare clic sul pulsante **Draw** (Disegna) per visualizzarne una versione grafica.</span><span class="sxs-lookup"><span data-stu-id="5c539-299">Select the **Draw** button to view a graphical version.</span></span> <span data-ttu-id="5c539-300">Il risultato è simile all'albero ottenuto in precedenza con *rpart*.</span><span class="sxs-lookup"><span data-stu-id="5c539-300">This looks quite similar to the tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="5c539-301">Una delle funzionalità interessanti di Rattle è la possibilità di eseguire diversi metodi di apprendimento automatico e valutarli rapidamente.</span><span class="sxs-lookup"><span data-stu-id="5c539-301">One of the nice features of Rattle is its ability to run several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="5c539-302">Di seguito è riportata la procedura:</span><span class="sxs-lookup"><span data-stu-id="5c539-302">Here is the procedure:</span></span>

* <span data-ttu-id="5c539-303">Scegliere **All** (Tutti) per **Type** (Tipo).</span><span class="sxs-lookup"><span data-stu-id="5c539-303">Choose **All** for the **Type**.</span></span>
* <span data-ttu-id="5c539-304">Scegliere **Execute**(Esegui).</span><span class="sxs-lookup"><span data-stu-id="5c539-304">Select **Execute**.</span></span>
* <span data-ttu-id="5c539-305">Al termine è possibile fare clic sul singolo **tipo**, ad esempio **SVM**, e visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="5c539-305">After it finishes you can click any single **Type**, like **SVM**, and view the results.</span></span>
* <span data-ttu-id="5c539-306">È anche possibile confrontare le prestazioni dei modelli nel set di convalida usando la scheda **Evaluate** (Valuta). Ad esempio, la selezione **Error Matrix** (Matrice degli errori) mostra la matrice di confusione, l'errore generale e l'errore medio di classe per ogni modello nel set di convalida.</span><span class="sxs-lookup"><span data-stu-id="5c539-306">You can also compare the performance of the models on the validation set using the **Evaluate** tab. For example, the **Error Matrix** selection shows you the confusion matrix, overall error, and averaged class error for each model on the validation set.</span></span>
* <span data-ttu-id="5c539-307">È anche possibile tracciare le curve ROC, eseguire analisi di sensibilità e altri tipi di valutazioni del modello.</span><span class="sxs-lookup"><span data-stu-id="5c539-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="5c539-308">Al termine della compilazione dei modelli, selezionare la scheda **Log** per visualizzare il codice R eseguito da Rattle durante la sessione.</span><span class="sxs-lookup"><span data-stu-id="5c539-308">Once you're finished building models, select the **Log** tab to view the R code run by Rattle during your session.</span></span> <span data-ttu-id="5c539-309">Per salvarlo, è possibile usare il pulsante **Export** (Esporta).</span><span class="sxs-lookup"><span data-stu-id="5c539-309">You can select the **Export** button to save it.</span></span>

> [!NOTE]
> <span data-ttu-id="5c539-310">La versione corrente di Rattle contiene un bug.</span><span class="sxs-lookup"><span data-stu-id="5c539-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="5c539-311">Per modificare lo script o usarlo per ripetere i passaggi in un secondo momento, è necessario inserire un carattere # davanti a *Export this log ...* (Esporta questo log) nel testo del log.</span><span class="sxs-lookup"><span data-stu-id="5c539-311">To modify the script or use it to repeat your steps later, you must insert a # character in front of *Export this log ... * in the text of the log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="5c539-312">PostgreSQL e Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="5c539-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="5c539-313">La DSVM viene fornita con PostgreSQL installato.</span><span class="sxs-lookup"><span data-stu-id="5c539-313">The DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="5c539-314">PostgreSQL è un sofisticato database relazionale open source.</span><span class="sxs-lookup"><span data-stu-id="5c539-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="5c539-315">Questa sezione illustra come eseguire query sul set di dati di posta indesiderata dopo averlo caricato in PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="5c539-315">This section shows how to load our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="5c539-316">Prima di caricare i dati è necessario consentire l'autenticazione della password da localhost.</span><span class="sxs-lookup"><span data-stu-id="5c539-316">Before you can load the data, you need to allow password authentication from the localhost.</span></span> <span data-ttu-id="5c539-317">Al prompt dei comandi, eseguire:</span><span class="sxs-lookup"><span data-stu-id="5c539-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="5c539-318">Verso la fine del file di configurazione sono presenti diverse righe con informazioni dettagliate sulle connessioni consentite:</span><span class="sxs-lookup"><span data-stu-id="5c539-318">Near the bottom of the config file are several lines that detail the allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="5c539-319">Modificare la riga "IPv4 local connections" per l'uso di md5 anziché ident, per poter eseguire l'accesso con un nome utente e una password:</span><span class="sxs-lookup"><span data-stu-id="5c539-319">Change the "IPv4 local connections" line to use md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="5c539-320">Riavviare il servizio postgres:</span><span class="sxs-lookup"><span data-stu-id="5c539-320">And restart the postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="5c539-321">Per avviare psql, il terminale interattivo per PostgreSQL, come l'utente postgres predefinito, eseguire questo comando da un prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="5c539-321">To launch psql, an interactive terminal for PostgreSQL, as the built-in postgres user, run the following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="5c539-322">Creare un nuovo account utente usando lo stesso nome utente dell'account Linux a cui si è connessi e assegnare una password:</span><span class="sxs-lookup"><span data-stu-id="5c539-322">Create a new user account, using the same username as the Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="5c539-323">Accedere a psql come utente:</span><span class="sxs-lookup"><span data-stu-id="5c539-323">Then log in to psql as your user:</span></span>

    psql

<span data-ttu-id="5c539-324">Quindi, importare i dati in un nuovo database:</span><span class="sxs-lookup"><span data-stu-id="5c539-324">And import the data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="5c539-325">Si passa ora all'elaborazione dei dati e all'esecuzione di query con **Squirrel SQL**, uno strumento grafico che permette di interagire con i database tramite un driver JDBC.</span><span class="sxs-lookup"><span data-stu-id="5c539-325">Now, let's explore the data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="5c539-326">Per iniziare, avviare Squirrel SQL dal menu delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5c539-326">To get started, launch Squirrel SQL from the Applications menu.</span></span> <span data-ttu-id="5c539-327">Per configurare il driver:</span><span class="sxs-lookup"><span data-stu-id="5c539-327">To set up the driver:</span></span>

* <span data-ttu-id="5c539-328">Selezionare **Windows** e quindi **View Drivers** (Visualizza driver).</span><span class="sxs-lookup"><span data-stu-id="5c539-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="5c539-329">Fare clic con il pulsante destro del mouse su **PostgreSQL** e selezionare **Modify Driver** (Modifica driver).</span><span class="sxs-lookup"><span data-stu-id="5c539-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="5c539-330">Selezionare **Extra Class Path** (Percorso classe extra) e quindi **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="5c539-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="5c539-331">Immettere ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** per **File Name** (Nome file).</span><span class="sxs-lookup"><span data-stu-id="5c539-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for the **File Name** and</span></span>
* <span data-ttu-id="5c539-332">Scegliere **Open**(Apri).</span><span class="sxs-lookup"><span data-stu-id="5c539-332">Select **Open**.</span></span>
* <span data-ttu-id="5c539-333">Scegliere List Drivers (Elenca driver), selezionare **org.postgresql.Driver** in **Class Name** (Nome classe) e quindi scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c539-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="5c539-334">Per configurare la connessione al server locale:</span><span class="sxs-lookup"><span data-stu-id="5c539-334">To set up the connection to the local server:</span></span>

* <span data-ttu-id="5c539-335">Selezionare **Windows** e quindi **View Aliases** (Visualizza alias).</span><span class="sxs-lookup"><span data-stu-id="5c539-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="5c539-336">Fare clic sul pulsante **+** per creare un nuovo alias.</span><span class="sxs-lookup"><span data-stu-id="5c539-336">Choose the **+** button to make a new alias.</span></span>
* <span data-ttu-id="5c539-337">Denominare l'alias *Spam database* (Database di posta indesiderata) e scegliere **PostgreSQL** nell'elenco a discesa **Driver**.</span><span class="sxs-lookup"><span data-stu-id="5c539-337">Name it *Spam database*, choose **PostgreSQL** in the **Driver** drop-down.</span></span>
* <span data-ttu-id="5c539-338">Impostare l'URL su *jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="5c539-338">Set the URL to *jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="5c539-339">Immettere il proprio *nome utente* e la *password*.</span><span class="sxs-lookup"><span data-stu-id="5c539-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="5c539-340">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c539-340">Click **OK**.</span></span>
* <span data-ttu-id="5c539-341">Per aprire la finestra **Connection** (Connessione), fare doppio clic sull'alias ***Spam database*** (Database di posta indesiderata).</span><span class="sxs-lookup"><span data-stu-id="5c539-341">To open the **Connection** window, double-click the ***Spam database*** alias.</span></span>
* <span data-ttu-id="5c539-342">Selezionare **Connessione**.</span><span class="sxs-lookup"><span data-stu-id="5c539-342">Select **Connect**.</span></span>

<span data-ttu-id="5c539-343">Per eseguire alcune query:</span><span class="sxs-lookup"><span data-stu-id="5c539-343">To run some queries:</span></span>

* <span data-ttu-id="5c539-344">Selezionare la scheda **SQL** .</span><span class="sxs-lookup"><span data-stu-id="5c539-344">Select the **SQL** tab.</span></span>
* <span data-ttu-id="5c539-345">Immettere una query semplice, ad esempio `SELECT * from data;` , nella casella di testo della query nella parte superiore della scheda SQL.</span><span class="sxs-lookup"><span data-stu-id="5c539-345">Enter a simple query such as `SELECT * from data;` in the query textbox at the top of the SQL tab.</span></span>
* <span data-ttu-id="5c539-346">Premere **CTRL + INVIO** per eseguirla.</span><span class="sxs-lookup"><span data-stu-id="5c539-346">Press **Ctrl-Enter** to run it.</span></span> <span data-ttu-id="5c539-347">Per impostazione predefinita, Squirrel SQL restituisce le prime 100 righe della query.</span><span class="sxs-lookup"><span data-stu-id="5c539-347">By default Squirrel SQL returns the first 100 rows from your query.</span></span>

<span data-ttu-id="5c539-348">È possibile eseguire molte altre query per esplorare questi dati.</span><span class="sxs-lookup"><span data-stu-id="5c539-348">There are many more queries you could run to explore this data.</span></span> <span data-ttu-id="5c539-349">Ad esempio, in cosa differisce la frequenza della parola *make* tra posta indesiderata e non indesiderata?</span><span class="sxs-lookup"><span data-stu-id="5c539-349">For example, how does the frequency of the word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="5c539-350">Oppure, quali sono le caratteristiche dei messaggi di posta elettronica che contengono spesso *3d*?</span><span class="sxs-lookup"><span data-stu-id="5c539-350">Or what are the characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="5c539-351">La maggior parte dei messaggi con un'occorrenza elevata della parola *3d* sembra essere posta indesiderata. Questa funzionalità potrebbe quindi essere utile per compilare un modello predittivo per la classificazione dei messaggi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="5c539-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model to classify the emails.</span></span>

<span data-ttu-id="5c539-352">Per eseguire l'apprendimento automatico con dati archiviati in un database PostgreSQL, è consigliabile usare [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="5c539-352">If you wanted to perform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="5c539-353">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5c539-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="5c539-354">Azure SQL Data Warehouse è un database basato sul cloud, con possibilità di aumentare il numero di istanze, che può elaborare volumi massivi di dati sia relazionali che non relazionali.</span><span class="sxs-lookup"><span data-stu-id="5c539-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="5c539-355">Per altre informazioni, vedere [Informazioni su Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="5c539-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="5c539-356">Per connettersi al data warehouse e creare la tabella, eseguire questo comando al prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="5c539-356">To connect to the data warehouse and create the table, run the following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="5c539-357">Al prompt di sqlcmd, eseguire:</span><span class="sxs-lookup"><span data-stu-id="5c539-357">Then at the sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="5c539-358">Per copiare dati con bcp, eseguire:</span><span class="sxs-lookup"><span data-stu-id="5c539-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="5c539-359">Le terminazioni di riga nel file scaricato sono in stile Windows, mentre bcp prevede lo stile UNIX. È quindi necessario segnalarlo a bcp con il flag -r.</span><span class="sxs-lookup"><span data-stu-id="5c539-359">The line endings in the downloaded file are Windows-style, but bcp expects UNIX-style, so we need to tell bcp that with the -r flag.</span></span>
>
>

<span data-ttu-id="5c539-360">Eseguire query con sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="5c539-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="5c539-361">È anche possibile eseguire query con Squirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="5c539-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="5c539-362">Seguire una procedura simile per PostgreSQL usando Microsoft JDBC Driver per SQL Server, disponibile in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="5c539-362">Follow similar steps for PostgreSQL, using the Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c539-363">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c539-363">Next steps</span></span>
<span data-ttu-id="5c539-364">Per una panoramica degli argomenti che forniscono informazioni dettagliate sulle attività che costituiscono il processo di analisi scientifica dei dati in Azure, vedere [Processo di analisi scientifica dei dati per i team](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="5c539-364">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="5c539-365">Per una descrizione di altre procedure dettagliate complete che illustrano i passaggi del processo per scenari specifici, vedere [Procedure dettagliate del Processo di analisi scientifica dei dati per i team](data-science-process-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="5c539-365">For a description of other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="5c539-366">Le procedure dettagliate illustrano anche come combinare strumenti cloud, strumenti locali e servizi in un flusso di lavoro o in una pipeline per creare un'applicazione intelligente.</span><span class="sxs-lookup"><span data-stu-id="5c539-366">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>
