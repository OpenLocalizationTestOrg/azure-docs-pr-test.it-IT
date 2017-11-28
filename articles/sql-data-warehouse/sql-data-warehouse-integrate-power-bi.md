---
title: Power BI con SQL Data Warehouse aaaUse | Documenti Microsoft
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
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="71e2d-103">Usare Power BI con SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="71e2d-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="71e2d-104">Come con Database SQL di Azure SQL Data Warehouse diretto Connect consente utente tooleverage potente logico distribuzione insieme alle funzionalità analitiche di hello di Power BI.</span><span class="sxs-lookup"><span data-stu-id="71e2d-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user tooleverage powerful logical pushdown alongside hello analytical capabilities of Power BI.</span></span>  <span data-ttu-id="71e2d-105">Con la connessione diretta le query vengono inviate tooyour indietro Azure SQL Data Warehouse in tempo reale durante l'esplorazione dati hello.</span><span class="sxs-lookup"><span data-stu-id="71e2d-105">With Direct Connect, queries are sent back tooyour Azure SQL Data Warehouse in real time as you explore hello data.</span></span>  <span data-ttu-id="71e2d-106">Questa operazione, combinati con scala hello di SQL Data Warehouse, consente agli utenti report dinamici toocreate in minuti per terabyte di dati.</span><span class="sxs-lookup"><span data-stu-id="71e2d-106">This, combined with hello scale of SQL Data Warehouse, enables users toocreate dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="71e2d-107">Inoltre, introduzione hello di hello Apri nel pulsante di Power BI consente agli utenti toodirectly connettere Power BI tootheir SQL Data Warehouse senza la raccolta di informazioni da altre parti di Azure.</span><span class="sxs-lookup"><span data-stu-id="71e2d-107">In addition, hello introduction of hello Open in Power BI button allows users toodirectly connect Power BI tootheir SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="71e2d-108">Quando si usa Direct Connect, occorre notare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="71e2d-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="71e2d-109">Specificare hello nome completo del server durante la connessione (vedere di seguito per altri dettagli)</span><span class="sxs-lookup"><span data-stu-id="71e2d-109">Specify hello fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="71e2d-110">Verificare le regole del firewall per database hello configurati troppo "consentono accesso tooAzure servizi".</span><span class="sxs-lookup"><span data-stu-id="71e2d-110">Ensure firewall rules for hello database are configured too"Allow access tooAzure services".</span></span>
* <span data-ttu-id="71e2d-111">Ogni azione, ad esempio la selezione di una colonna o l'aggiunta di un filtro direttamente eseguirà una query data warehouse di hello</span><span class="sxs-lookup"><span data-stu-id="71e2d-111">Every action such as selecting a column or adding a filter will  directly query hello data warehouse</span></span>
* <span data-ttu-id="71e2d-112">Riquadri vengono aggiornati all'incirca ogni 15 minuti (aggiornamento non è necessario toobe pianificata)</span><span class="sxs-lookup"><span data-stu-id="71e2d-112">Tiles are refreshed approximately every 15 minutes (refresh does not need toobe scheduled)</span></span>
* <span data-ttu-id="71e2d-113">Non sono disponibili domande e risposte per i set di dati di Direct Connect.</span><span class="sxs-lookup"><span data-stu-id="71e2d-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="71e2d-114">Le modifiche allo schema non vengono rilevate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="71e2d-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="71e2d-115">Tutte le query di Direct Connect scadranno dopo 2 minuti</span><span class="sxs-lookup"><span data-stu-id="71e2d-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="71e2d-116">Queste restrizioni e note possono cambiare mentre continuiamo tooimprove hello esperienze.</span><span class="sxs-lookup"><span data-stu-id="71e2d-116">These restrictions and notes may change as we continue tooimprove hello experiences.</span></span> <span data-ttu-id="71e2d-117">Hello passaggi tooconnect è illustrata di seguito.</span><span class="sxs-lookup"><span data-stu-id="71e2d-117">hello steps tooconnect are detailed below.</span></span>  

## <a name="using-hello-open-in-power-bi-button"></a><span data-ttu-id="71e2d-118">Pulsante 'Apri in Power BI' hello</span><span class="sxs-lookup"><span data-stu-id="71e2d-118">Using hello ‘Open in Power BI’ button</span></span>
<span data-ttu-id="71e2d-119">toomove modo più semplice di Hello tra SQL Data Warehouse e Power BI è hello Apri nel pulsante di Power BI.</span><span class="sxs-lookup"><span data-stu-id="71e2d-119">hello easiest way toomove between your SQL Data Warehouse and Power BI is with hello Open in Power BI button.</span></span> <span data-ttu-id="71e2d-120">Questo pulsante consente tooseamlessly iniziare a creare nuovi dashboard in Power BI.</span><span class="sxs-lookup"><span data-stu-id="71e2d-120">This button allows you tooseamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="71e2d-121">tooget avviato passare l'istanza di SQL Data Warehouse tooyour nel portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="71e2d-121">tooget started navigate tooyour SQL Data Warehouse instance in hello Azure Classic Portal.</span></span>
2. <span data-ttu-id="71e2d-122">Fare clic su pulsante 'Apri in Power BI' hello.</span><span class="sxs-lookup"><span data-stu-id="71e2d-122">Click hello 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="71e2d-123">Se non è in grado di toosign in direttamente, o se non si dispone di un account Power BI, sarà necessario toosign-in.</span><span class="sxs-lookup"><span data-stu-id="71e2d-123">If we are not able toosign you in directly, or if you do not have a Power BI account, you will need toosign-in.</span></span>  
4. <span data-ttu-id="71e2d-124">Si verrà reindirizzati pre-popolati toohello pagina connessione a SQL Data Warehouse, con informazioni hello del proprio SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="71e2d-124">You will be directed toohello SQL Data Warehouse connection page, with hello information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="71e2d-125">Dopo aver immesso le credenziali sarà completamente connesso tooyour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="71e2d-125">After entering your credentials you will be fully connected tooyour SQL Data Warehouse.</span></span>

## <a name="connecting-through-hello-power-bi-portal"></a><span data-ttu-id="71e2d-126">Connessione tramite il portale di Power BI hello</span><span class="sxs-lookup"><span data-stu-id="71e2d-126">Connecting through hello Power BI portal</span></span>
<span data-ttu-id="71e2d-127">In aggiunta toousing Ciao Apri pulsante Power BI, gli utenti possono connettersi tootheir SQL Data Warehouse tramite hello portale di Power BI.</span><span class="sxs-lookup"><span data-stu-id="71e2d-127">In addition toousing hello Open in Power BI button, users can also connect tootheir SQL Data Warehouse through hello Power BI Portal.</span></span>

1. <span data-ttu-id="71e2d-128">Fare clic su "Dati" nella parte inferiore di hello del riquadro di spostamento hello.</span><span class="sxs-lookup"><span data-stu-id="71e2d-128">Click 'Get Data' at hello bottom of hello navigation pane.</span></span>
2. <span data-ttu-id="71e2d-129">Selezionare 'Database'.</span><span class="sxs-lookup"><span data-stu-id="71e2d-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="71e2d-130">Una volta nella pagina database hello, selezionare "Azure SQL Data Warehouse" e quindi fare clic su 'Connetti'.</span><span class="sxs-lookup"><span data-stu-id="71e2d-130">Once on hello Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="71e2d-131">Immettere le informazioni di connessione necessarie hello.</span><span class="sxs-lookup"><span data-stu-id="71e2d-131">Enter hello necessary connection information.</span></span>  <span data-ttu-id="71e2d-132">Nome del server e nome del database è reperibile nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="71e2d-132">Your server name and database name can be found in hello Azure Portal.</span></span>
5. <span data-ttu-id="71e2d-133">Nuovo si verrà reindirizzati verrà visualizzata la pagina principale di toohello di Power BI e dopo la connessione viene stabilita una nuova voce in 'set di dati con nome hello dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="71e2d-133">You will be directed back toohello main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with hello name of your instance.</span></span>  
6. <span data-ttu-id="71e2d-134">È possibile fare clic su hello nuovo set di dati tooexplore tutti hello tabelle e viste nel database.</span><span class="sxs-lookup"><span data-stu-id="71e2d-134">You can click on hello new dataset tooexplore all of hello tables and views in your database.</span></span> <span data-ttu-id="71e2d-135">Selezione di una colonna invierà un'origine toohello indietro di query, creando dinamicamente l'oggetto visivo.</span><span class="sxs-lookup"><span data-stu-id="71e2d-135">Selecting a column will send a query back toohello source, dynamically creating your visual.</span></span> <span data-ttu-id="71e2d-136">Gli oggetti visivi possono essere salvati in un nuovo report e riaggiunti tooyour dashboard.</span><span class="sxs-lookup"><span data-stu-id="71e2d-136">These visuals can be saved in a new report and pinned back tooyour dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
