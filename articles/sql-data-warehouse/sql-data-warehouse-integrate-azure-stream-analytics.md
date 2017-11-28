---
title: aaaUse Analitica di flusso di Azure con SQL Data Warehouse | Documenti Microsoft
description: Suggerimenti per l'uso di Analisi di flusso di Azure con Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="3f939-103">Usare Analisi di flusso di Azure con SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3f939-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="3f939-104">Analitica di flusso di Azure è un servizio completamente gestito che fornisce l'elaborazione a bassa latenza, elevata disponibilità e scalabile di eventi complessi nel flusso di dati nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="3f939-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="3f939-105">È possibile nozioni di base hello leggendo [tooAzure introduzione Analitica flusso][Introduction tooAzure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="3f939-105">You can learn hello basics by reading [Introduction tooAzure Stream Analytics][Introduction tooAzure Stream Analytics].</span></span> <span data-ttu-id="3f939-106">Sarà possibile apprendere come una soluzione end-to-end con flusso Analitica seguendo toocreate hello [iniziare a usare Azure flusso Analitica] [ Get started using Azure Stream Analytics] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3f939-106">You can then learn how toocreate an end-to-end solution with Stream Analytics by following hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="3f939-107">In questo articolo si apprenderà come toouse database Azure SQL Data Warehouse come sink di output per i processi di flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="3f939-107">In this article, you will learn how toouse your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f939-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3f939-108">Prerequisites</span></span>
<span data-ttu-id="3f939-109">In primo luogo, eseguire i passaggi hello hello [iniziare a usare Azure flusso Analitica] [ Get started using Azure Stream Analytics] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3f939-109">First, run through hello following steps in hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="3f939-110">Creare un input dell'hub eventi</span><span class="sxs-lookup"><span data-stu-id="3f939-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="3f939-111">Configurare e avviare l'applicazione di generazione di eventi</span><span class="sxs-lookup"><span data-stu-id="3f939-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="3f939-112">Eseguire il provisioning di un processo di Analisi dei flussi</span><span class="sxs-lookup"><span data-stu-id="3f939-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="3f939-113">Specificare la query e l'input del processo</span><span class="sxs-lookup"><span data-stu-id="3f939-113">Specify job input and query</span></span>

<span data-ttu-id="3f939-114">Creare quindi un database di Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3f939-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="3f939-115">Specificare l'output del processo: database di Azure SQL Warehouse</span><span class="sxs-lookup"><span data-stu-id="3f939-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="3f939-116">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="3f939-116">Step 1</span></span>
<span data-ttu-id="3f939-117">Selezionare il processo di flusso Analitica **OUTPUT** dall'alto hello della pagina hello e quindi fare clic su **Aggiungi OUTPUT**.</span><span class="sxs-lookup"><span data-stu-id="3f939-117">In your Stream Analytics job click **OUTPUT** from hello top of hello page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="3f939-118">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="3f939-118">Step 2</span></span>
<span data-ttu-id="3f939-119">Selezionare il Database SQL e fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="3f939-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="3f939-120">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="3f939-120">Step 3</span></span>
<span data-ttu-id="3f939-121">Immettere i seguenti valori nella pagina successiva hello hello:</span><span class="sxs-lookup"><span data-stu-id="3f939-121">Enter hello following values on hello next page:</span></span>

* <span data-ttu-id="3f939-122">*Alias di output*: immettere un nome descrittivo per l'output del processo.</span><span class="sxs-lookup"><span data-stu-id="3f939-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="3f939-123">*Sottoscrizione*</span><span class="sxs-lookup"><span data-stu-id="3f939-123">*Subscription*:</span></span>
  * <span data-ttu-id="3f939-124">Se il database di SQL Data Warehouse è in hello stessa sottoscrizione come processo di flusso Analitica hello, selezionare Usa Database SQL dalla sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="3f939-124">If your SQL Data Warehouse database is in hello same subscription as hello Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="3f939-125">Se il database è in una sottoscrizione diversa, selezionare Usare il database SQL da un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3f939-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="3f939-126">*Database*: specificare il nome di hello di un database di destinazione.</span><span class="sxs-lookup"><span data-stu-id="3f939-126">*Database*: Specify hello name of a destination database.</span></span>
* <span data-ttu-id="3f939-127">*Nome del server*: specificare il nome di server hello per database hello è stato specificato.</span><span class="sxs-lookup"><span data-stu-id="3f939-127">*Server Name*: Specify hello server name for hello database you just specified.</span></span> <span data-ttu-id="3f939-128">È possibile utilizzare hello portale di Azure classico toofind questo.</span><span class="sxs-lookup"><span data-stu-id="3f939-128">You can use hello Azure Classic Portal toofind this.</span></span>

![][server-name]

* <span data-ttu-id="3f939-129">*Nome utente*: specificare il nome utente hello di un account che disponga di autorizzazioni di scrittura per il database di hello.</span><span class="sxs-lookup"><span data-stu-id="3f939-129">*User Name*: Specify hello user name of an account that has write permissions for hello database.</span></span>
* <span data-ttu-id="3f939-130">*Password*: specificare la password di hello per hello l'account utente specificato.</span><span class="sxs-lookup"><span data-stu-id="3f939-130">*Password*: Provide hello password for hello specified user account.</span></span>
* <span data-ttu-id="3f939-131">*Tabella*: specificare il nome di hello della tabella di destinazione hello nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="3f939-131">*Table*: Specify hello name of hello target table in hello database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="3f939-132">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="3f939-132">Step 4</span></span>
<span data-ttu-id="3f939-133">Fare clic su hello controllo pulsante tooadd l'output del processo e tooverify Analitica di flusso che può connettersi toohello database.</span><span class="sxs-lookup"><span data-stu-id="3f939-133">Click hello check button tooadd this job output and tooverify that Stream Analytics can successfully connect toohello database.</span></span>

![][test-connection]

<span data-ttu-id="3f939-134">Quando il database di toohello hello connessione ha esito positivo, si vedrà una notifica nella parte inferiore di hello del portale hello.</span><span class="sxs-lookup"><span data-stu-id="3f939-134">When hello connection toohello database succeeds, you will see a notification at hello bottom of hello portal.</span></span> <span data-ttu-id="3f939-135">È possibile fare clic su Verifica connessione nel database di hello inferiore tootest hello connessione toohello.</span><span class="sxs-lookup"><span data-stu-id="3f939-135">You can click Test Connection at hello bottom tootest hello connection toohello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f939-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3f939-136">Next steps</span></span>
<span data-ttu-id="3f939-137">Per una panoramica dell'integrazione, vedere [Panoramica dell'integrazione di SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="3f939-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="3f939-138">Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="3f939-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
