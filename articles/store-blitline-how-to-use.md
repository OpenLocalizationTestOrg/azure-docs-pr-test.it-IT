---
title: "Come usare Blitline per l'elaborazione delle immagini - Guida alle funzionalità di Azure"
description: Informazioni su come usare il servizio Blitline per elaborare immagini all'interno di un'applicazione Azure.
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 1d90599e028b3407a513b04b878e3aefc39928a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="b9584-103">Come utilizzare Blitline con Azure e l'archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b9584-103">How to use Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="b9584-104">In questa guida verrà descritto come accedere ai servizi Blitline e come inviare i processi a Blitline.</span><span class="sxs-lookup"><span data-stu-id="b9584-104">This guide will explain how to access Blitline services and how to submit jobs to Blitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="b9584-105">Informazioni su Blitline</span><span class="sxs-lookup"><span data-stu-id="b9584-105">What is Blitline?</span></span>
<span data-ttu-id="b9584-106">Blitline è un servizio di elaborazione a livello aziendale delle immagini basate su cloud, dal costo nettamente inferiore a quello che comporterebbe la creazione autonoma delle stesse.</span><span class="sxs-lookup"><span data-stu-id="b9584-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of the price that it would cost to build it yourself.</span></span>

<span data-ttu-id="b9584-107">Il fatto è che l'elaborazione delle immagini è un'operazione ripetuta di continuo, di solito creandole da zero per ciascun sito Web.</span><span class="sxs-lookup"><span data-stu-id="b9584-107">The fact is that image processing has been done over and over again, usually rebuilt from the ground up for each and every website.</span></span> <span data-ttu-id="b9584-108">Ce ne rendiamo conto perché noi stessi le abbiamo create un milione di volte.</span><span class="sxs-lookup"><span data-stu-id="b9584-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="b9584-109">Ad un certo punto abbiamo deciso che era probabilmente arrivato il momento di farlo per tutti.</span><span class="sxs-lookup"><span data-stu-id="b9584-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="b9584-110">Disponiamo delle opportune competenze, della velocità e dell'efficienza necessaria, che ci consentono di offrire a tutti un enorme risparmio del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b9584-110">We know how to do it, to do it fast and efficiently, and save everyone work in the meantime.</span></span>

<span data-ttu-id="b9584-111">Per ulteriori informazioni, visitare il sito [http://www.blitline.com](http://www.blitline.com).</span><span class="sxs-lookup"><span data-stu-id="b9584-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="b9584-112">Operazioni NON eseguite da Blitline</span><span class="sxs-lookup"><span data-stu-id="b9584-112">What Blitline is NOT...</span></span>
<span data-ttu-id="b9584-113">Allo scopo di chiarire l'utilità di Blitline è spesso più semplice identificare le operazioni che Blitline NON esegue prima di procedere oltre.</span><span class="sxs-lookup"><span data-stu-id="b9584-113">To clarify what Blitline is useful for, it is often easier to identify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="b9584-114">Blitline NON dispone di widget HTML per caricare le immagini.</span><span class="sxs-lookup"><span data-stu-id="b9584-114">Blitline does NOT have HTML widgets to upload images.</span></span> <span data-ttu-id="b9584-115">Affinché Blitline possa ottenerle, le immagini devono essere disponibili pubblicamente oppure con autorizzazioni limitate.</span><span class="sxs-lookup"><span data-stu-id="b9584-115">You must have images available publicly or with restricted permissions available for Blitline to reach.</span></span>
* <span data-ttu-id="b9584-116">Blitline NON esegue l'elaborazione delle immagini attive come Aviary.com</span><span class="sxs-lookup"><span data-stu-id="b9584-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="b9584-117">Blitline NON accetta i caricamenti delle immagini; non è possibile eseguire il push delle immagini direttamente su Blitline.</span><span class="sxs-lookup"><span data-stu-id="b9584-117">Blitline does NOT accept image uploads, you cannot push your images to Blitline directly.</span></span> <span data-ttu-id="b9584-118">È necessario eseguire il push delle immagini nell'archiviazione di Azure o in altri luoghi supportati da Blitline, quindi informare il software della posizione in cui recuperarle.</span><span class="sxs-lookup"><span data-stu-id="b9584-118">You must push them to Azure Storage or other places Blitline supports and then tell Blitline where to go get them.</span></span>
* <span data-ttu-id="b9584-119">Blitline opera principalmente in parallelo e NON esegue alcuna elaborazione sincrona;</span><span class="sxs-lookup"><span data-stu-id="b9584-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="b9584-120">vale a dire che l'utente deve comunicare un postback_url affinché sia possibile avvisarlo del termine dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b9584-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="b9584-121">Creare un account Blitline</span><span class="sxs-lookup"><span data-stu-id="b9584-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-to-create-a-blitline-job"></a><span data-ttu-id="b9584-122">Come creare un processo di Blitline</span><span class="sxs-lookup"><span data-stu-id="b9584-122">How to create a Blitline job</span></span>
<span data-ttu-id="b9584-123">Blitline utilizza JSON per definire le azioni da intraprendere riguardo un'immagine.</span><span class="sxs-lookup"><span data-stu-id="b9584-123">Blitline uses JSON to define the actions you want to take on an image.</span></span> <span data-ttu-id="b9584-124">Il codice JSON è composto da alcuni semplici campi:</span><span class="sxs-lookup"><span data-stu-id="b9584-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="b9584-125">L'esempio più semplice è riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b9584-125">The simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="b9584-126">In questo caso, il codice JSON prende un'immagine "src" ("...boys.jpeg") e la ridimensiona a 240x140.</span><span class="sxs-lookup"><span data-stu-id="b9584-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image to 240x140.</span></span>

<span data-ttu-id="b9584-127">L'ID applicazione è un elemento reperibile nella scheda **INFORMAZIONI DI CONNESSIONE** o **GESTISCI** in Azure.</span><span class="sxs-lookup"><span data-stu-id="b9584-127">The Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="b9584-128">È l'identificatore segreto che consente di eseguire i processi su Blitline.</span><span class="sxs-lookup"><span data-stu-id="b9584-128">It is your secret identifier that allows you to run jobs on Blitline.</span></span>

<span data-ttu-id="b9584-129">Il parametro "save" consente di identificare le informazioni sulla posizione in cui si desidera inserire l'immagine dopo che è stata elaborata.</span><span class="sxs-lookup"><span data-stu-id="b9584-129">The "save" parameter identifies information about where you want to put the image once we have processed it.</span></span> <span data-ttu-id="b9584-130">In questo caso, la posizione non è stata definita.</span><span class="sxs-lookup"><span data-stu-id="b9584-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="b9584-131">Se non viene definita alcuna posizione, Blitline archivierà l'immagine in locale (temporaneamente) in una posizione univoca sul cloud.</span><span class="sxs-lookup"><span data-stu-id="b9584-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="b9584-132">Sarà possibile ottenere tale posizione dal codice JSON restituito da Blitline.</span><span class="sxs-lookup"><span data-stu-id="b9584-132">You will be able to get that location from the JSON returned by Blitline when you make the Blitline.</span></span> <span data-ttu-id="b9584-133">Per identificare questa particolare immagine salvata è necessario l'identificatore "image" che viene restituito all'utente.</span><span class="sxs-lookup"><span data-stu-id="b9584-133">The "image" identifier is required and is returned to you when to identify this particular saved image.</span></span>

<span data-ttu-id="b9584-134">Altre informazioni sulle *funzioni* supportate sono disponibili qui: <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="b9584-134">You can find more information about the *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="b9584-135">Inoltre la documentazione sulle opzioni dei processi è disponibile qui: <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="b9584-135">You can also find documentation about the job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="b9584-136">Dopo aver ottenuto il codice JSON, basta solo pubblicarlo come **POST** su `http://api.blitline.com/job`</span><span class="sxs-lookup"><span data-stu-id="b9584-136">Once you have your JSON all you need to do is **POST** it to `http://api.blitline.com/job`</span></span>

<span data-ttu-id="b9584-137">Si otterrà un codice JSON che avrà più o meno l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="b9584-137">You will get JSON back that looks something like this:</span></span>

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


<span data-ttu-id="b9584-138">Il codice informa che Blitline ha ricevuto la richiesta, l'ha inserita in una coda di elaborazione e al termine dell'operazione l'immagine sarà disponibile all'indirizzo: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="b9584-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed the image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-to-save-an-image-to-your-azure-storage-account"></a><span data-ttu-id="b9584-139">Come salvare un'immagine nell'account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b9584-139">How to save an image to your Azure Storage account</span></span>
<span data-ttu-id="b9584-140">Se si dispone di un account di archiviazione di Azure è possibile eseguire facilmente il push delle immagini elaborate in Blitline nel contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9584-140">If you have an Azure Storage account, you can easily have Blitline push the processed images into your Azure container.</span></span> <span data-ttu-id="b9584-141">Aggiungendo il frammento "azure_destination" è possibile definire la posizione e le autorizzazioni per il push di Blitline.</span><span class="sxs-lookup"><span data-stu-id="b9584-141">By adding an "azure_destination" you define the location and permissions for Blitline to push to.</span></span>

<span data-ttu-id="b9584-142">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="b9584-142">Here is an example:</span></span>

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


<span data-ttu-id="b9584-143">Sostituendo i valori IN MAIUSCOLO con i propri, sarà possibile inviare questo codice JSON a http://api.blitline.com/job; l'immagine "src" verrà elaborata con un filtro sfocatura, quindi sottoposta a push verso la destinazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9584-143">By filling in the CAPITALIZED values with your own, you can submit this JSON to http://api.blitline.com/job and the "src" image will be processed with a blur filter and then pushed to you Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="b9584-144">Nota bene:</span><span class="sxs-lookup"><span data-stu-id="b9584-144">Please note:</span></span>
<span data-ttu-id="b9584-145">SAS deve contenere l'intero URL di SAS, incluso il nome file del file di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b9584-145">The SAS must contain the entire SAS url, including the filename of the destination file.</span></span>

<span data-ttu-id="b9584-146">Esempio:</span><span class="sxs-lookup"><span data-stu-id="b9584-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="b9584-147">È anche possibile leggere l'ultima edizione dei documenti sull'archiviazione di Azure di Blitline [qui](http://www.blitline.com/docs/azure_storage).</span><span class="sxs-lookup"><span data-stu-id="b9584-147">You can also read the latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9584-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b9584-148">Next Steps</span></span>
<span data-ttu-id="b9584-149">Visitare blitline.com per informazioni su tutte le altre funzionalità:</span><span class="sxs-lookup"><span data-stu-id="b9584-149">Visit blitline.com to read about all our other features:</span></span>

* <span data-ttu-id="b9584-150">Documenti sugli endpoint API di Blitline <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="b9584-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="b9584-151">Funzioni delle API di Blitline <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="b9584-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="b9584-152">Esempi delle API di Blitline <http://www.blitline.com/docs/examples></span><span class="sxs-lookup"><span data-stu-id="b9584-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="b9584-153">Libreria NuGet di terze parti <http://nuget.org/packages/Blitline.Net></span><span class="sxs-lookup"><span data-stu-id="b9584-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

