---
title: Usare Power BI con SQL Data Warehouse | Documentazione Microsoft
description: Suggerimenti per l'uso di Power BI con Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 4b7609fc5d6ce7bf0e3bd3ebf6d8f52e93a40a75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="811cc-103">Usare Power BI con SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="811cc-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="811cc-104">Analogamente al database SQL di Azure, SQL Data Warehouse Direct Connect permette agli utenti di sfruttare le capacità avanzate di pushdown logico insieme alle capacità analitiche di Power BI.</span><span class="sxs-lookup"><span data-stu-id="811cc-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user to leverage powerful logical pushdown alongside the analytical capabilities of Power BI.</span></span>  <span data-ttu-id="811cc-105">Con Direct Connect le query vengono restituite ad Azure SQL Data Warehouse in tempo reale durante l'esplorazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="811cc-105">With Direct Connect, queries are sent back to your Azure SQL Data Warehouse in real time as you explore the data.</span></span>  <span data-ttu-id="811cc-106">Unitamente alla scalabilità di SQL Data Warehouse, ciò permette agli utenti di creare report dinamici in pochi minuti su terabyte di dati.</span><span class="sxs-lookup"><span data-stu-id="811cc-106">This, combined with the scale of SQL Data Warehouse, enables users to create dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="811cc-107">L'introduzione del pulsante Apri in Power BI permette agli utenti di connettere direttamente Power BI al proprio SQL Data Warehouse, senza raccogliere informazioni da altre parti di Azure.</span><span class="sxs-lookup"><span data-stu-id="811cc-107">In addition, the introduction of the Open in Power BI button allows users to directly connect Power BI to their SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="811cc-108">Quando si usa Direct Connect, occorre notare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="811cc-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="811cc-109">Specificare il nome completo del server durante la connessione. Per altri dettagli, vedere più avanti.</span><span class="sxs-lookup"><span data-stu-id="811cc-109">Specify the fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="811cc-110">Assicurarsi che le regole del firewall per il database siano configurate su "Consenti l'accesso a Servizi di Azure".</span><span class="sxs-lookup"><span data-stu-id="811cc-110">Ensure firewall rules for the database are configured to "Allow access to Azure services".</span></span>
* <span data-ttu-id="811cc-111">Ogni azione, ad esempio la selezione di una colonna o l'aggiunta di un filtro, eseguirà direttamente una query nel data warehouse.</span><span class="sxs-lookup"><span data-stu-id="811cc-111">Every action such as selecting a column or adding a filter will  directly query the data warehouse</span></span>
* <span data-ttu-id="811cc-112">I riquadri vengono aggiornati ogni 15 minuti circa. Non è necessario pianificare l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="811cc-112">Tiles are refreshed approximately every 15 minutes (refresh does not need to be scheduled)</span></span>
* <span data-ttu-id="811cc-113">Non sono disponibili domande e risposte per i set di dati di Direct Connect.</span><span class="sxs-lookup"><span data-stu-id="811cc-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="811cc-114">Le modifiche allo schema non vengono rilevate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="811cc-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="811cc-115">Tutte le query di Direct Connect scadranno dopo 2 minuti</span><span class="sxs-lookup"><span data-stu-id="811cc-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="811cc-116">Queste restrizioni e note sono soggette a modifiche nel corso del miglioramento delle esperienze.</span><span class="sxs-lookup"><span data-stu-id="811cc-116">These restrictions and notes may change as we continue to improve the experiences.</span></span> <span data-ttu-id="811cc-117">I passaggi per la connessione sono illustrati nel dettaglio più avanti.</span><span class="sxs-lookup"><span data-stu-id="811cc-117">The steps to connect are detailed below.</span></span>  

## <a name="using-the-open-in-power-bi-button"></a><span data-ttu-id="811cc-118">Uso del pulsante "Apri in Power BI"</span><span class="sxs-lookup"><span data-stu-id="811cc-118">Using the ‘Open in Power BI’ button</span></span>
<span data-ttu-id="811cc-119">Il modo più semplice per spostarsi tra SQL Data Warehouse e Power BI consiste nell'usare il pulsante Apri in Power BI.</span><span class="sxs-lookup"><span data-stu-id="811cc-119">The easiest way to move between your SQL Data Warehouse and Power BI is with the Open in Power BI button.</span></span> <span data-ttu-id="811cc-120">Questo pulsante permette di creare con facilità nuovi dashboard in Power BI.</span><span class="sxs-lookup"><span data-stu-id="811cc-120">This button allows you to seamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="811cc-121">Per iniziare, passare all'istanza di SQL Data Warehouse nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="811cc-121">To get started navigate to your SQL Data Warehouse instance in the Azure Classic Portal.</span></span>
2. <span data-ttu-id="811cc-122">Fare clic sul pulsante Apri in Power BI.</span><span class="sxs-lookup"><span data-stu-id="811cc-122">Click the 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="811cc-123">Se non è possibile accedere direttamente o se non si ha un account di Power BI, sarà necessario effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="811cc-123">If we are not able to sign you in directly, or if you do not have a Power BI account, you will need to sign-in.</span></span>  
4. <span data-ttu-id="811cc-124">Si verrà indirizzati alla pagina di connessione di SQL Data Warehouse, con le informazioni di SQL Data Warehouse pre-popolate.</span><span class="sxs-lookup"><span data-stu-id="811cc-124">You will be directed to the SQL Data Warehouse connection page, with the information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="811cc-125">Dopo l'immissione delle credenziali, si sarà completamente connessi a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="811cc-125">After entering your credentials you will be fully connected to your SQL Data Warehouse.</span></span>

## <a name="connecting-through-the-power-bi-portal"></a><span data-ttu-id="811cc-126">Connessione tramite il portale di Power BI</span><span class="sxs-lookup"><span data-stu-id="811cc-126">Connecting through the Power BI portal</span></span>
<span data-ttu-id="811cc-127">Oltre a usare il pulsante Apri in Power BI, gli utenti possono connettersi a SQL Data Warehouse anche tramite il portale di Power BI.</span><span class="sxs-lookup"><span data-stu-id="811cc-127">In addition to using the Open in Power BI button, users can also connect to their SQL Data Warehouse through the Power BI Portal.</span></span>

1. <span data-ttu-id="811cc-128">Fare clic su ’Recupera dati’ nella parte inferiore del pannello di navigazione.</span><span class="sxs-lookup"><span data-stu-id="811cc-128">Click 'Get Data' at the bottom of the navigation pane.</span></span>
2. <span data-ttu-id="811cc-129">Selezionare 'Database'.</span><span class="sxs-lookup"><span data-stu-id="811cc-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="811cc-130">Una volta nella pagina database selezionare 'SQL Azure Data Warehouse' e poi fare clic su ’Connetti’.</span><span class="sxs-lookup"><span data-stu-id="811cc-130">Once on the Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="811cc-131">Immettere le informazioni di connessione necessarie.</span><span class="sxs-lookup"><span data-stu-id="811cc-131">Enter the necessary connection information.</span></span>  <span data-ttu-id="811cc-132">Il nome del server e il nome del database sono disponibili nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="811cc-132">Your server name and database name can be found in the Azure Portal.</span></span>
5. <span data-ttu-id="811cc-133">Si verrà indirizzati di nuovo alla pagina principale di Power BI e dopo che la connessione viene stabilita, verrà visualizzata una nuova voce in 'set di dati con il nome dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="811cc-133">You will be directed back to the main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with the name of your instance.</span></span>  
6. <span data-ttu-id="811cc-134">È possibile fare clic sul nuovo set di dati per esplorare tutte le tabelle e le visualizzazioni del database.</span><span class="sxs-lookup"><span data-stu-id="811cc-134">You can click on the new dataset to explore all of the tables and views in your database.</span></span> <span data-ttu-id="811cc-135">Se si seleziona una colonna, una query verrà restituita all'origine, creando dinamicamente l'oggetto visivo.</span><span class="sxs-lookup"><span data-stu-id="811cc-135">Selecting a column will send a query back to the source, dynamically creating your visual.</span></span> <span data-ttu-id="811cc-136">Gli oggetti visivi possono essere salvati in un nuovo report e aggiunti nuovamente al dashboard.</span><span class="sxs-lookup"><span data-stu-id="811cc-136">These visuals can be saved in a new report and pinned back to your dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
