---
title: aaaImport dati da un file in Azure Machine Learning Studio | Documenti Microsoft
description: Informazioni su come il tooAzure rigido Machine Learning Studio file tooupload dati di training. Consente di creare un modulo di set di dati nell'area di lavoro hello.
keywords: dati di importazione, formato dati, tipi di dati, origini dati, dati di training
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
ms.openlocfilehash: 636facd9042145382c953a1c75969149ede6f6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="e1090-105">Importare dati di training da un file sul disco rigido in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="e1090-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="e1090-106">Informazioni su come tooupload un tipo di dati di file da toouse il disco rigido come dati di training in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e1090-106">Learn how tooupload a data file from your hard drive toouse as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="e1090-107">Tramite l'importazione di file di dati hello, si dispone di un modulo di set di dati pronto per l'utilizzo nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e1090-107">By importing hello data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-tooimport-data-from-a-local-file"></a><span data-ttu-id="e1090-108">Dati tooimport i passaggi da un file locale</span><span class="sxs-lookup"><span data-stu-id="e1090-108">Steps tooimport data from a local file</span></span>
<span data-ttu-id="e1090-109">tooimport dati da un disco rigido locale, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="e1090-109">tooimport data from a local hard drive, do hello following:</span></span>

1. <span data-ttu-id="e1090-110">Fare clic su **+ nuovo** nella parte inferiore di hello della finestra di Machine Learning Studio hello.</span><span class="sxs-lookup"><span data-stu-id="e1090-110">Click **+NEW** at hello bottom of hello Machine Learning Studio window.</span></span>
2. <span data-ttu-id="e1090-111">Selezionare **DATASET** (SET DI DATI) e **FROM LOCAL FILE** (DA FILE LOCALE).</span><span class="sxs-lookup"><span data-stu-id="e1090-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="e1090-112">In hello **caricare un nuovo set di dati** finestra di dialogo Sfoglia toohello file da tooupload</span><span class="sxs-lookup"><span data-stu-id="e1090-112">In hello **Upload a new dataset** dialog, browse toohello file you want tooupload</span></span>
4. <span data-ttu-id="e1090-113">Immettere un nome, identificare il tipo di dati hello e immettere facoltativamente una descrizione.</span><span class="sxs-lookup"><span data-stu-id="e1090-113">Enter a name, identify hello data type, and optionally enter a description.</span></span> <span data-ttu-id="e1090-114">È consigliabile una descrizione: consente toorecord qualsiasi caratteristica sui dati hello che si desidera tooremember quando si utilizzano dati hello in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="e1090-114">A description is recommended - it allows you toorecord any characteristics about hello data that you want tooremember when using hello data in hello future.</span></span>
5. <span data-ttu-id="e1090-115">casella di controllo di Hello **si tratta hello nuova versione di un set di dati esistente** consente tooupdate un set di dati esistente con nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="e1090-115">hello checkbox **This is hello new version of an existing dataset** allows you tooupdate an existing dataset with new data.</span></span> <span data-ttu-id="e1090-116">Fare clic su questa casella di controllo e quindi immettere il nome di hello di un set di dati esistente.</span><span class="sxs-lookup"><span data-stu-id="e1090-116">Click this checkbox and then enter hello name of an existing dataset.</span></span>

![Caricare un nuovo set di dati](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="e1090-118">Durante il caricamento, verrà visualizzato un messaggio che indica che il file è in fase di caricamento.</span><span class="sxs-lookup"><span data-stu-id="e1090-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="e1090-119">Caricare tempo dipende dalle dimensioni hello la velocità di hello e dati del servizio toohello connessione.</span><span class="sxs-lookup"><span data-stu-id="e1090-119">Upload time depends on hello size of your data and hello speed of your connection toohello service.</span></span> <span data-ttu-id="e1090-120">Se si conosce il file hello richiederà molto tempo, è possibile eseguire altre operazioni all'interno di Machine Learning Studio durante l'attesa.</span><span class="sxs-lookup"><span data-stu-id="e1090-120">If you know hello file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="e1090-121">Tuttavia, chiudere il browser hello determina toofail di caricamento dati hello.</span><span class="sxs-lookup"><span data-stu-id="e1090-121">However, closing hello browser causes hello data upload toofail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="e1090-122">Il modulo set di dati è pronto per l'utilizzo</span><span class="sxs-lookup"><span data-stu-id="e1090-122">Dataset module is ready for use</span></span>
<span data-ttu-id="e1090-123">Dopo aver caricati i dati, viene archiviato in un modulo di set di dati e viene esperimento tooany disponibile nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e1090-123">Once your data is uploaded, it's stored in a dataset module and is available tooany experiment in your workspace.</span></span>

<span data-ttu-id="e1090-124">Quando si modifica un esperimento, è possibile trovare hello set di dati sono stati creati in hello **set di dati personali** elenco hello **Saved Datasets** elenco tavolozza modulo hello.</span><span class="sxs-lookup"><span data-stu-id="e1090-124">When you're editing an experiment, you can find hello datasets you've created in hello **My Datasets** list under hello **Saved Datasets** list in hello module palette.</span></span> <span data-ttu-id="e1090-125">È possibile trascinare e rilasciare hello set di dati nell'area di disegno esperimento hello quando si desidera toouse hello set di dati per un'ulteriore analitica e machine learning.</span><span class="sxs-lookup"><span data-stu-id="e1090-125">You can drag and drop hello dataset onto hello experiment canvas when you want toouse hello dataset for further analytics and machine learning.</span></span>
