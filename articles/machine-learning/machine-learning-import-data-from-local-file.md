---
title: Importare dati da un file in Azure Machine Learning Studio | Microsoft Docs
description: Informazioni su come caricare un file di dati di training dal disco rigido in Azure Machine Learning Studio. Questa operazione crea un modulo set di dati nell'area di lavoro.
keywords: dati di importazione,formato dati,tipi di dati,origini dati,dati di training
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: 18010864160ceb2d76aea37196e6944bbe426457
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="735bd-105">Importare dati di training da un file sul disco rigido in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="735bd-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="735bd-106">Informazioni su come caricare un file di dati da utilizzare come dati di training dal disco rigido in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="735bd-106">Learn how to upload a data file from your hard drive to use as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="735bd-107">Importando il file di dati, si dispone di un modulo set di dati pronto per l'utilizzo nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="735bd-107">By importing the data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-to-import-data-from-a-local-file"></a><span data-ttu-id="735bd-108">Passaggi per importare dati da un file locale</span><span class="sxs-lookup"><span data-stu-id="735bd-108">Steps to import data from a local file</span></span>
<span data-ttu-id="735bd-109">Per importare dati da un disco rigido locale effettuare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="735bd-109">To import data from a local hard drive, do the following:</span></span>

1. <span data-ttu-id="735bd-110">Fare clic su **+ NEW** nella parte inferiore della finestra di Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="735bd-110">Click **+NEW** at the bottom of the Machine Learning Studio window.</span></span>
2. <span data-ttu-id="735bd-111">Selezionare **DATASET** (SET DI DATI) e **FROM LOCAL FILE** (DA FILE LOCALE).</span><span class="sxs-lookup"><span data-stu-id="735bd-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="735bd-112">Nella finestra di dialogo **Caricare un nuovo set di dati** selezionare il file da caricare</span><span class="sxs-lookup"><span data-stu-id="735bd-112">In the **Upload a new dataset** dialog, browse to the file you want to upload</span></span>
4. <span data-ttu-id="735bd-113">Immettere un nome, identificare il tipo di dati e immettere facoltativamente una descrizione.</span><span class="sxs-lookup"><span data-stu-id="735bd-113">Enter a name, identify the data type, and optionally enter a description.</span></span> <span data-ttu-id="735bd-114">Una descrizione è consigliabile perché consente di registrare tutte le caratteristiche relative ai dati da tenere presenti quando si useranno tali dati in futuro.</span><span class="sxs-lookup"><span data-stu-id="735bd-114">A description is recommended - it allows you to record any characteristics about the data that you want to remember when using the data in the future.</span></span>
5. <span data-ttu-id="735bd-115">La casella di controllo **Questa è la nuova versione di un set di dati esistente** consente di aggiornare un set di dati esistente con nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="735bd-115">The checkbox **This is the new version of an existing dataset** allows you to update an existing dataset with new data.</span></span> <span data-ttu-id="735bd-116">Fare clic su questa casella di controllo e quindi immettere il nome di un set di dati esistente.</span><span class="sxs-lookup"><span data-stu-id="735bd-116">Click this checkbox and then enter the name of an existing dataset.</span></span>

![Caricare un nuovo set di dati](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="735bd-118">Durante il caricamento, verrà visualizzato un messaggio che indica che il file è in fase di caricamento.</span><span class="sxs-lookup"><span data-stu-id="735bd-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="735bd-119">Il tempo di caricamento dipende dalle dimensioni dei dati e dalla velocità della connessione al servizio.</span><span class="sxs-lookup"><span data-stu-id="735bd-119">Upload time depends on the size of your data and the speed of your connection to the service.</span></span> <span data-ttu-id="735bd-120">Se è già noto che il file richiederà molto tempo, è possibile eseguire altre operazioni in Machine Learning Studio durante l'attesa.</span><span class="sxs-lookup"><span data-stu-id="735bd-120">If you know the file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="735bd-121">In caso di chiusura del browser, tuttavia, il caricamento dei dati avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="735bd-121">However, closing the browser causes the data upload to fail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="735bd-122">Il modulo set di dati è pronto per l'utilizzo</span><span class="sxs-lookup"><span data-stu-id="735bd-122">Dataset module is ready for use</span></span>
<span data-ttu-id="735bd-123">Una volta caricati, i dati vengono archiviati in un modulo di set di dati e sono disponibili per eventuali esperimenti nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="735bd-123">Once your data is uploaded, it's stored in a dataset module and is available to any experiment in your workspace.</span></span>

<span data-ttu-id="735bd-124">Durante la modifica di un esperimento, è possibile individuare i set di dati creati nell'elenco **My Datasets** (Set di dati personali) presente nell'elenco **Saved Datasets** (Set di dati salvati) nella tavolozza dei moduli.</span><span class="sxs-lookup"><span data-stu-id="735bd-124">When you're editing an experiment, you can find the datasets you've created in the **My Datasets** list under the **Saved Datasets** list in the module palette.</span></span> <span data-ttu-id="735bd-125">È possibile trascinare il set di dati nell'area di disegno dell'esperimento per usarlo per l'ulteriore analisi e l'apprendimento automatico.</span><span class="sxs-lookup"><span data-stu-id="735bd-125">You can drag and drop the dataset onto the experiment canvas when you want to use the dataset for further analytics and machine learning.</span></span>
