---
title: Usare Analisi di flusso di Azure con SQL Data Warehouse | Documentazione Microsoft
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
ms.openlocfilehash: 14783f0464764a11d7f03a5db1c2d63728a4cb50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="9491e-103">Usare Analisi di flusso di Azure con SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9491e-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="9491e-104">Analisi di flusso di Azure è un servizio completamente gestito che consente l'elaborazione di eventi complessi con bassa latenza, elevata disponibilità e scalabilità per lo streaming di dati nel cloud.</span><span class="sxs-lookup"><span data-stu-id="9491e-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="9491e-105">Per informazioni di base, vedere [Introduzione ad Analisi di flusso di Azure][Introduction to Azure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="9491e-105">You can learn the basics by reading [Introduction to Azure Stream Analytics][Introduction to Azure Stream Analytics].</span></span> <span data-ttu-id="9491e-106">È possibile apprendere come creare una soluzione end-to-end con Analisi di flusso seguendo l'esercitazione [Introduzione all'uso di Analisi di flusso di Azure][Get started using Azure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="9491e-106">You can then learn how to create an end-to-end solution with Stream Analytics by following the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="9491e-107">In questo articolo si apprenderà come usare il database di Azure SQL Data Warehouse come un sink di output per i processi di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="9491e-107">In this article, you will learn how to use your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9491e-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9491e-108">Prerequisites</span></span>
<span data-ttu-id="9491e-109">Eseguire prima di tutto questa procedura nell'esercitazione [Introduzione all'uso di Analisi di flusso di Azure][Get started using Azure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="9491e-109">First, run through the following steps in the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="9491e-110">Creare un input dell'hub eventi</span><span class="sxs-lookup"><span data-stu-id="9491e-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="9491e-111">Configurare e avviare l'applicazione di generazione di eventi</span><span class="sxs-lookup"><span data-stu-id="9491e-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="9491e-112">Eseguire il provisioning di un processo di Analisi dei flussi</span><span class="sxs-lookup"><span data-stu-id="9491e-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="9491e-113">Specificare la query e l'input del processo</span><span class="sxs-lookup"><span data-stu-id="9491e-113">Specify job input and query</span></span>

<span data-ttu-id="9491e-114">Creare quindi un database di Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9491e-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="9491e-115">Specificare l'output del processo: database di Azure SQL Warehouse</span><span class="sxs-lookup"><span data-stu-id="9491e-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="9491e-116">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="9491e-116">Step 1</span></span>
<span data-ttu-id="9491e-117">Nel processo di Analisi di flusso fare clic su **OUTPUT** nella parte superiore della pagina e quindi scegliere **AGGIUNGI OUTPUT**.</span><span class="sxs-lookup"><span data-stu-id="9491e-117">In your Stream Analytics job click **OUTPUT** from the top of the page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="9491e-118">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="9491e-118">Step 2</span></span>
<span data-ttu-id="9491e-119">Selezionare il Database SQL e fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="9491e-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="9491e-120">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="9491e-120">Step 3</span></span>
<span data-ttu-id="9491e-121">Immettere i valori seguenti nella pagina successiva:</span><span class="sxs-lookup"><span data-stu-id="9491e-121">Enter the following values on the next page:</span></span>

* <span data-ttu-id="9491e-122">*Alias di output*: immettere un nome descrittivo per l'output del processo.</span><span class="sxs-lookup"><span data-stu-id="9491e-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="9491e-123">*Sottoscrizione*</span><span class="sxs-lookup"><span data-stu-id="9491e-123">*Subscription*:</span></span>
  * <span data-ttu-id="9491e-124">Se il database SQL Data Warehouse esiste nella stessa sottoscrizione del processo di analisi di flusso, selezionare Usare il database SQL dalla sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="9491e-124">If your SQL Data Warehouse database is in the same subscription as the Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="9491e-125">Se il database è in una sottoscrizione diversa, selezionare Usare il database SQL da un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9491e-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="9491e-126">*Database*: specificare il nome di un database di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9491e-126">*Database*: Specify the name of a destination database.</span></span>
* <span data-ttu-id="9491e-127">*Nome server*: specificare il nome del server per il database specificato.</span><span class="sxs-lookup"><span data-stu-id="9491e-127">*Server Name*: Specify the server name for the database you just specified.</span></span> <span data-ttu-id="9491e-128">Per trovarlo, è possibile usare il portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="9491e-128">You can use the Azure Classic Portal to find this.</span></span>

![][server-name]

* <span data-ttu-id="9491e-129">*Nome utente*: digitare il nome utente di un account con autorizzazioni di scrittura nel database.</span><span class="sxs-lookup"><span data-stu-id="9491e-129">*User Name*: Specify the user name of an account that has write permissions for the database.</span></span>
* <span data-ttu-id="9491e-130">*Password*: fornire la password per l'account utente specificato.</span><span class="sxs-lookup"><span data-stu-id="9491e-130">*Password*: Provide the password for the specified user account.</span></span>
* <span data-ttu-id="9491e-131">*Tabella*: specificare il nome della tabella di destinazione nel database.</span><span class="sxs-lookup"><span data-stu-id="9491e-131">*Table*: Specify the name of the target table in the database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="9491e-132">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="9491e-132">Step 4</span></span>
<span data-ttu-id="9491e-133">Fare clic sul pulsante con il segno di spunta per aggiungere l'output del processo e per verificare che Analisi di flusso possa connettersi al database.</span><span class="sxs-lookup"><span data-stu-id="9491e-133">Click the check button to add this job output and to verify that Stream Analytics can successfully connect to the database.</span></span>

![][test-connection]

<span data-ttu-id="9491e-134">Quando la connessione al database riesce, verrà visualizzata una notifica nella parte inferiore del portale.</span><span class="sxs-lookup"><span data-stu-id="9491e-134">When the connection to the database succeeds, you will see a notification at the bottom of the portal.</span></span> <span data-ttu-id="9491e-135">È possibile scegliere Test connessione nella parte inferiore per testare la connessione al database.</span><span class="sxs-lookup"><span data-stu-id="9491e-135">You can click Test Connection at the bottom to test the connection to the database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9491e-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9491e-136">Next steps</span></span>
<span data-ttu-id="9491e-137">Per una panoramica dell'integrazione, vedere [Panoramica dell'integrazione di SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="9491e-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="9491e-138">Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="9491e-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction to Azure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
