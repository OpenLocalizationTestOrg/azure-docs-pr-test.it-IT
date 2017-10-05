---
title: Convertire i dati XML con le trasformazioni - App per la logica di Azure | Microsoft Docs
description: Creare trasformazioni o mappe per convertire i dati XML da un formato a un altro nelle app per la logica con l'SDK di Enterprise Integration
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: fb6027769377b3527b11f7831dab3bb8d7061c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="7fb48-103">Enterprise Integration con trasformazioni XML</span><span class="sxs-lookup"><span data-stu-id="7fb48-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="7fb48-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7fb48-104">Overview</span></span>
<span data-ttu-id="7fb48-105">Il connettore di trasformazione di Enterprise Integration converte i dati da un formato a un altro.</span><span class="sxs-lookup"><span data-stu-id="7fb48-105">The Enterprise integration Transform connector converts data from one format to another format.</span></span> <span data-ttu-id="7fb48-106">Ad esempio, si è ricevuto un messaggio contenente la data corrente nel formato YearMonthDay.</span><span class="sxs-lookup"><span data-stu-id="7fb48-106">For example, you may have an incoming message that contains the current date in the YearMonthDay format.</span></span> <span data-ttu-id="7fb48-107">È possibile usare una trasformazione per riformattare la data nel formato MonthDayYear.</span><span class="sxs-lookup"><span data-stu-id="7fb48-107">You can use a transform to reformat the date to be in the MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="7fb48-108">Funzioni della trasformazione</span><span class="sxs-lookup"><span data-stu-id="7fb48-108">What does a transform do?</span></span>
<span data-ttu-id="7fb48-109">Un'app per le API Transform, conosciuta anche come Map, consiste in uno schema XML di origine (input) e in uno schema XML di destinazione (output).</span><span class="sxs-lookup"><span data-stu-id="7fb48-109">A Transform, which is also known as a map, consists of a Source XML schema (the input) and a Target XML schema (the output).</span></span> <span data-ttu-id="7fb48-110">È possibile usare diverse funzioni predefinite per contribuire a gestire o controllare i dati, incluse la modifica di stringhe, le operazioni Conditional Assignment, le espressioni aritmetiche, i formattatori di data/ora e persino i costrutti a ciclo continuo.</span><span class="sxs-lookup"><span data-stu-id="7fb48-110">You can use different built-in functions to help manipulate or control the data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-to-create-a-transform"></a><span data-ttu-id="7fb48-111">Procedura: Creare una trasformazione</span><span class="sxs-lookup"><span data-stu-id="7fb48-111">How to create a transform?</span></span>
<span data-ttu-id="7fb48-112">È possibile creare una mappa/trasformazione tramite l' [SDK di Enterprise Integration](https://aka.ms/vsmapsandschemas)di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7fb48-112">You can create a transform/map by using the Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="7fb48-113">Al termine della creazione e del testing della trasformazione, caricare la trasformazione nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="7fb48-113">When you are finished creating and testing the transform, you upload the transform into your integration account.</span></span> 

## <a name="how-to-use-a-transform"></a><span data-ttu-id="7fb48-114">Procedura: Usare una trasformazione</span><span class="sxs-lookup"><span data-stu-id="7fb48-114">How to use a transform</span></span>
<span data-ttu-id="7fb48-115">Dopo aver caricato il file della trasformazione/mappa nell'account di integrazione, è possibile usarlo per creare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="7fb48-115">After you upload the transform/map into your integration account, you can use it to create a Logic app.</span></span> <span data-ttu-id="7fb48-116">L'app per la logica esegue le trasformazioni a ogni attivazione dell'app, con la relativa trasformazione del contenuto immesso.</span><span class="sxs-lookup"><span data-stu-id="7fb48-116">The Logic app runs your transformations whenever the Logic app is triggered (and there is input content that needs to be transformed).</span></span>

<span data-ttu-id="7fb48-117">**Di seguito è riportata la procedura per l'uso di una trasformazione**:</span><span class="sxs-lookup"><span data-stu-id="7fb48-117">**Here are the steps to use a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="7fb48-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7fb48-118">Prerequisites</span></span>

* <span data-ttu-id="7fb48-119">Creare un account di integrazione e aggiungervi una mappa</span><span class="sxs-lookup"><span data-stu-id="7fb48-119">Create an integration account and add a map to it</span></span>  

<span data-ttu-id="7fb48-120">Una volta soddisfatti i requisiti, è ora di creare l'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="7fb48-120">Now that you've taken care of the prerequisites, it's time to create your Logic app:</span></span>  

1. <span data-ttu-id="7fb48-121">Creare un'app per la logica e [collegarla all'account di integrazione](../logic-apps/logic-apps-enterprise-integration-accounts.md "Informazioni su come collegare un account di integrazione a un'app per la logica") che contiene la mappa.</span><span class="sxs-lookup"><span data-stu-id="7fb48-121">Create a Logic app and [link it to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that contains the map.</span></span>
2. <span data-ttu-id="7fb48-122">Aggiungere un trigger **Richiesta** all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="7fb48-122">Add a **Request** trigger to your Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="7fb48-123">Aggiungere l'azione **Trasforma XML** selezionando prima **Aggiungi un'azione** </span><span class="sxs-lookup"><span data-stu-id="7fb48-123">Add the **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="7fb48-124">Immettere la parola *trasforma* nella casella di ricerca per filtrare tutte le azioni e ottenere quella che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="7fb48-124">Enter the word *transform* in the search box to filter all the actions to the one that you want to use</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="7fb48-125">Selezionare l'azione **Trasforma XML**</span><span class="sxs-lookup"><span data-stu-id="7fb48-125">Select the **Transform XML** action</span></span>   
6. <span data-ttu-id="7fb48-126">Aggiungere il **CONTENUTO** XML da trasformare.</span><span class="sxs-lookup"><span data-stu-id="7fb48-126">Add the XML **CONTENT** that you transform.</span></span> <span data-ttu-id="7fb48-127">È possibile usare tutti i dati XML ricevuti nella richiesta HTTP come **CONTENUTO**.</span><span class="sxs-lookup"><span data-stu-id="7fb48-127">You can use any XML data you receive in the HTTP request as the **CONTENT**.</span></span> <span data-ttu-id="7fb48-128">In questo esempio selezionare il corpo della richiesta HTTP che ha attivato l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="7fb48-128">In this example, select the body of the HTTP request that triggered the Logic app.</span></span>
7. <span data-ttu-id="7fb48-129">Selezionare il nome della **MAPPA** che si vuole usare per eseguire la trasformazione.</span><span class="sxs-lookup"><span data-stu-id="7fb48-129">Select the name of the **MAP** that you want to use to perform the transformation.</span></span> <span data-ttu-id="7fb48-130">La mappa deve essere già presente nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="7fb48-130">The map must already be in your integration account.</span></span> <span data-ttu-id="7fb48-131">In un passaggio precedente è stato concesso l'accesso dell'app per la logica all'account di integrazione che contiene la mappa.</span><span class="sxs-lookup"><span data-stu-id="7fb48-131">In an earlier step, you already gave your Logic app access to your integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="7fb48-132">Salvare il lavoro </span><span class="sxs-lookup"><span data-stu-id="7fb48-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="7fb48-133">A questo punto, la configurazione della mappa è completa.</span><span class="sxs-lookup"><span data-stu-id="7fb48-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="7fb48-134">In un'applicazione reale è possibile archiviare i dati trasformati in un'applicazione LOB, ad esempio SalesForce.</span><span class="sxs-lookup"><span data-stu-id="7fb48-134">In a real world application, you may want to store the transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="7fb48-135">È possibile eseguire facilmente questa azione inviando l'output della trasformazione a Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7fb48-135">You can easily as an action to send the output of the transform to Salesforce.</span></span> 

<span data-ttu-id="7fb48-136">È ora possibile testare la trasformazione eseguendo una richiesta all'endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="7fb48-136">You can now test your transform by making a request to the HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="7fb48-137">Funzionalità e casi d'uso</span><span class="sxs-lookup"><span data-stu-id="7fb48-137">Features and use cases</span></span>
* <span data-ttu-id="7fb48-138">La trasformazione creata in una mappa può essere semplice, come ad esempio la copia di un nome e di un indirizzo da un documento a un altro.</span><span class="sxs-lookup"><span data-stu-id="7fb48-138">The transformation created in a map can be simple, such as copying a name and address from one document to another.</span></span> <span data-ttu-id="7fb48-139">In alternativa, è possibile creare trasformazioni più complesse usando operazioni di mapping predefinite.</span><span class="sxs-lookup"><span data-stu-id="7fb48-139">Or, you can create more complex transformations using the out-of-the-box map operations.</span></span>  
* <span data-ttu-id="7fb48-140">Sono già disponibili più operazioni o funzioni di mapping, incluse stringhe, funzioni data/ora e così via.</span><span class="sxs-lookup"><span data-stu-id="7fb48-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="7fb48-141">È possibile eseguire una copia diretta dei dati tra gli schemi.</span><span class="sxs-lookup"><span data-stu-id="7fb48-141">You can do a direct data copy between the schemas.</span></span> <span data-ttu-id="7fb48-142">Nel mapper incluso nell'SDK, questa operazione è semplice quanto tracciare una linea che colleghi gli elementi nello schema di origine con le relative controparti nello schema di destinazione.</span><span class="sxs-lookup"><span data-stu-id="7fb48-142">In the Mapper included in the SDK, this is as simple as drawing a line that connects the elements in the source schema with their counterparts in the destination schema.</span></span>  
* <span data-ttu-id="7fb48-143">Durante la creazione di una mappa viene visualizzata la relativa rappresentazione grafica, che mostra tutte le relazioni e i collegamenti creati dall'utente.</span><span class="sxs-lookup"><span data-stu-id="7fb48-143">When creating a map, you view a graphical representation of the map, which shows all the relationships and links you create.</span></span>
* <span data-ttu-id="7fb48-144">Usare la funzione Mappa di test per aggiungere un messaggio XML di esempio.</span><span class="sxs-lookup"><span data-stu-id="7fb48-144">Use the Test Map feature to add a sample XML message.</span></span> <span data-ttu-id="7fb48-145">Con un semplice clic, è possibile testare la mappa creata e visualizzare l'output generato.</span><span class="sxs-lookup"><span data-stu-id="7fb48-145">With a simple click, you can test the map you created, and see the generated output.</span></span>  
* <span data-ttu-id="7fb48-146">Caricare le mappe esistenti</span><span class="sxs-lookup"><span data-stu-id="7fb48-146">Upload existing maps</span></span>  
* <span data-ttu-id="7fb48-147">Include il supporto per il formato XML.</span><span class="sxs-lookup"><span data-stu-id="7fb48-147">Includes support for the XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="7fb48-148">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="7fb48-148">Learn more</span></span>
* [<span data-ttu-id="7fb48-149">Altre informazioni su Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="7fb48-149">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Informazioni su Enterprise Integration Pack")  
* [<span data-ttu-id="7fb48-150">Altre informazioni sulle mappe</span><span class="sxs-lookup"><span data-stu-id="7fb48-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Informazioni sulle mappe di Enterprise Integration")  

