---
title: "aaaHow toouse Blitline per l'elaborazione di immagini - Guida alla funzionalità di Azure"
description: Informazioni su come toouse hello Blitline service tooprocess immagini all'interno di un'applicazione Azure.
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
ms.openlocfilehash: 328fd177e25f45f29f8ad8e142d02b46017a858e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="d10ca-103">Come toouse Blitline con Azure e archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d10ca-103">How toouse Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="d10ca-104">Questa guida viene illustrato come tooaccess Blitline come toosubmit tooBlitline dei processi e servizi.</span><span class="sxs-lookup"><span data-stu-id="d10ca-104">This guide will explain how tooaccess Blitline services and how toosubmit jobs tooBlitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="d10ca-105">Informazioni su Blitline</span><span class="sxs-lookup"><span data-stu-id="d10ca-105">What is Blitline?</span></span>
<span data-ttu-id="d10ca-106">Blitline è un'immagine basata su cloud servizio che consente l'elaborazione di immagini a livello enterprise a una frazione del prezzo di hello che toobuild al costo di elaborazione è manualmente.</span><span class="sxs-lookup"><span data-stu-id="d10ca-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of hello price that it would cost toobuild it yourself.</span></span>

<span data-ttu-id="d10ca-107">tabelle dei fatti Hello è che l'elaborazione di immagini sia stata eseguita più volte, in genere ricreato da zero hello per ogni sito Web.</span><span class="sxs-lookup"><span data-stu-id="d10ca-107">hello fact is that image processing has been done over and over again, usually rebuilt from hello ground up for each and every website.</span></span> <span data-ttu-id="d10ca-108">Ce ne rendiamo conto perché noi stessi le abbiamo create un milione di volte.</span><span class="sxs-lookup"><span data-stu-id="d10ca-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="d10ca-109">Ad un certo punto abbiamo deciso che era probabilmente arrivato il momento di farlo per tutti.</span><span class="sxs-lookup"><span data-stu-id="d10ca-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="d10ca-110">È noto come toodo è veloce e in modo efficiente e salvare tutti gli utenti funziona in hello frattempo toodo.</span><span class="sxs-lookup"><span data-stu-id="d10ca-110">We know how toodo it, toodo it fast and efficiently, and save everyone work in hello meantime.</span></span>

<span data-ttu-id="d10ca-111">Per ulteriori informazioni, visitare il sito [http://www.blitline.com](http://www.blitline.com).</span><span class="sxs-lookup"><span data-stu-id="d10ca-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="d10ca-112">Operazioni NON eseguite da Blitline</span><span class="sxs-lookup"><span data-stu-id="d10ca-112">What Blitline is NOT...</span></span>
<span data-ttu-id="d10ca-113">tooclarify cosa Blitline è utile per, è spesso più facile tooidentify Blitline non operazioni prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="d10ca-113">tooclarify what Blitline is useful for, it is often easier tooidentify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="d10ca-114">Blitline non dispone di immagini di tooupload widget HTML.</span><span class="sxs-lookup"><span data-stu-id="d10ca-114">Blitline does NOT have HTML widgets tooupload images.</span></span> <span data-ttu-id="d10ca-115">È necessario disporre le immagini disponibili pubblicamente o con autorizzazioni limitate per Blitline tooreach.</span><span class="sxs-lookup"><span data-stu-id="d10ca-115">You must have images available publicly or with restricted permissions available for Blitline tooreach.</span></span>
* <span data-ttu-id="d10ca-116">Blitline NON esegue l'elaborazione delle immagini attive come Aviary.com</span><span class="sxs-lookup"><span data-stu-id="d10ca-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="d10ca-117">Blitline non accetta un caricamento di immagini, è Impossibile eseguire il push del tooBlitline immagini direttamente.</span><span class="sxs-lookup"><span data-stu-id="d10ca-117">Blitline does NOT accept image uploads, you cannot push your images tooBlitline directly.</span></span> <span data-ttu-id="d10ca-118">È necessario effettuare il push tooAzure archiviazione o altre posizioni che blitline supporta e quindi indicare Blitline dove toogo ottenerli.</span><span class="sxs-lookup"><span data-stu-id="d10ca-118">You must push them tooAzure Storage or other places Blitline supports and then tell Blitline where toogo get them.</span></span>
* <span data-ttu-id="d10ca-119">Blitline opera principalmente in parallelo e NON esegue alcuna elaborazione sincrona;</span><span class="sxs-lookup"><span data-stu-id="d10ca-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="d10ca-120">vale a dire che l'utente deve comunicare un postback_url affinché sia possibile avvisarlo del termine dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="d10ca-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="d10ca-121">Creare un account Blitline</span><span class="sxs-lookup"><span data-stu-id="d10ca-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a><span data-ttu-id="d10ca-122">Come un processo Blitline toocreate</span><span class="sxs-lookup"><span data-stu-id="d10ca-122">How toocreate a Blitline job</span></span>
<span data-ttu-id="d10ca-123">Blitline utilizza JSON toodefine hello le azioni da tootake in un'immagine.</span><span class="sxs-lookup"><span data-stu-id="d10ca-123">Blitline uses JSON toodefine hello actions you want tootake on an image.</span></span> <span data-ttu-id="d10ca-124">Il codice JSON è composto da alcuni semplici campi:</span><span class="sxs-lookup"><span data-stu-id="d10ca-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="d10ca-125">Hello più semplice esempio è la seguente:</span><span class="sxs-lookup"><span data-stu-id="d10ca-125">hello simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="d10ca-126">Qui abbiamo JSON che eseguirà un'immagine "src" "... boys.jpeg" e quindi ridimensionare too240x140 tale immagine.</span><span class="sxs-lookup"><span data-stu-id="d10ca-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image too240x140.</span></span>

<span data-ttu-id="d10ca-127">ID applicazione Hello è un elemento in cui è possibile trovare il **le informazioni di connessione** o **GESTISCI** scheda in Azure.</span><span class="sxs-lookup"><span data-stu-id="d10ca-127">hello Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="d10ca-128">È l'identificatore di segreto che consente di processi toorun su Blitline.</span><span class="sxs-lookup"><span data-stu-id="d10ca-128">It is your secret identifier that allows you toorun jobs on Blitline.</span></span>

<span data-ttu-id="d10ca-129">Hello "Salva" parametro identifica informazioni in cui si desidera che tooput hello immagine dopo che è stata eseguita l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="d10ca-129">hello "save" parameter identifies information about where you want tooput hello image once we have processed it.</span></span> <span data-ttu-id="d10ca-130">In questo caso, la posizione non è stata definita.</span><span class="sxs-lookup"><span data-stu-id="d10ca-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="d10ca-131">Se non viene definita alcuna posizione, Blitline archivierà l'immagine in locale (temporaneamente) in una posizione univoca sul cloud.</span><span class="sxs-lookup"><span data-stu-id="d10ca-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="d10ca-132">Si sarà in grado di tooget che percorso da hello JSON restituito dalla Blitline quando si apportata hello Blitline.</span><span class="sxs-lookup"><span data-stu-id="d10ca-132">You will be able tooget that location from hello JSON returned by Blitline when you make hello Blitline.</span></span> <span data-ttu-id="d10ca-133">identificatore "image" Hello è obbligatorio e viene restituito tooyou quando tooidentify questa particolare salvata l'immagine.</span><span class="sxs-lookup"><span data-stu-id="d10ca-133">hello "image" identifier is required and is returned tooyou when tooidentify this particular saved image.</span></span>

<span data-ttu-id="d10ca-134">È possibile trovare ulteriori informazioni su hello *funzioni* è qui il supporto: <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="d10ca-134">You can find more information about hello *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="d10ca-135">È anche possibile trovare documentazione su hello qui le opzioni di processo: <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="d10ca-135">You can also find documentation about hello job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="d10ca-136">Una volta ottenuto il file JSON è sufficiente toodo **POST** è troppo`http://api.blitline.com/job`</span><span class="sxs-lookup"><span data-stu-id="d10ca-136">Once you have your JSON all you need toodo is **POST** it too`http://api.blitline.com/job`</span></span>

<span data-ttu-id="d10ca-137">Si otterrà un codice JSON che avrà più o meno l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="d10ca-137">You will get JSON back that looks something like this:</span></span>

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


<span data-ttu-id="d10ca-138">In questo modo si Blitline ha ricevuto la richiesta, ha inserito nella coda di elaborazione e al termine dell'immagine di hello è disponibile in: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID /CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="d10ca-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed hello image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a><span data-ttu-id="d10ca-139">Come toosave un tooyour immagine account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d10ca-139">How toosave an image tooyour Azure Storage account</span></span>
<span data-ttu-id="d10ca-140">Se si dispone di un account di archiviazione di Azure, è possibile disporre facilmente immagini di hello elaborato push Blitline nel contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="d10ca-140">If you have an Azure Storage account, you can easily have Blitline push hello processed images into your Azure container.</span></span> <span data-ttu-id="d10ca-141">Aggiungendo un "azure_destination" definire percorso hello e le autorizzazioni per toopush Blitline per.</span><span class="sxs-lookup"><span data-stu-id="d10ca-141">By adding an "azure_destination" you define hello location and permissions for Blitline toopush to.</span></span>

<span data-ttu-id="d10ca-142">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="d10ca-142">Here is an example:</span></span>

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


<span data-ttu-id="d10ca-143">Compilando hello CAPITALIZED valori con valori personalizzati, è possibile inviare questa toohttp://api.blitline.com/job JSON e verrà elaborati con un filtro di sfocatura hello "src" immagine e quindi inseriti tooyou destinazione Azure.</span><span class="sxs-lookup"><span data-stu-id="d10ca-143">By filling in hello CAPITALIZED values with your own, you can submit this JSON toohttp://api.blitline.com/job and hello "src" image will be processed with a blur filter and then pushed tooyou Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="d10ca-144">Nota bene:</span><span class="sxs-lookup"><span data-stu-id="d10ca-144">Please note:</span></span>
<span data-ttu-id="d10ca-145">Hello SAS deve contenere l'url SAS intera hello, incluso il nome file hello del file di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="d10ca-145">hello SAS must contain hello entire SAS url, including hello filename of hello destination file.</span></span>

<span data-ttu-id="d10ca-146">Esempio:</span><span class="sxs-lookup"><span data-stu-id="d10ca-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="d10ca-147">È inoltre possibile leggere l'edizione più recente di hello di documenti di archiviazione di Azure del Blitline [qui](http://www.blitline.com/docs/azure_storage).</span><span class="sxs-lookup"><span data-stu-id="d10ca-147">You can also read hello latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d10ca-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d10ca-148">Next Steps</span></span>
<span data-ttu-id="d10ca-149">Visitare tooread blitline.com su tutte le altre funzionalità:</span><span class="sxs-lookup"><span data-stu-id="d10ca-149">Visit blitline.com tooread about all our other features:</span></span>

* <span data-ttu-id="d10ca-150">Documenti sugli endpoint API di Blitline <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="d10ca-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="d10ca-151">Funzioni delle API di Blitline <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="d10ca-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="d10ca-152">Esempi delle API di Blitline <http://www.blitline.com/docs/examples></span><span class="sxs-lookup"><span data-stu-id="d10ca-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="d10ca-153">Libreria NuGet di terze parti <http://nuget.org/packages/Blitline.Net></span><span class="sxs-lookup"><span data-stu-id="d10ca-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

