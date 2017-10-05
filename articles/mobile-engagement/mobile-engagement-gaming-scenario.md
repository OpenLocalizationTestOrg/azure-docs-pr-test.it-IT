---
title: Implementazione di Azure Mobile Engagement per app di gioco
description: Scenario di app di gioco per l'implementazione di Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0ca35a3d634db8eb5c63afacba046a35b8a3e7ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="f669e-103">Implementare Mobile Engagement con app di gioco</span><span class="sxs-lookup"><span data-stu-id="f669e-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="f669e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="f669e-104">Overview</span></span>
<span data-ttu-id="f669e-105">Una startup del settore gaming ha lanciato una nuova app di gioco di ruolo e strategia ispirata al mondo della pesca.</span><span class="sxs-lookup"><span data-stu-id="f669e-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="f669e-106">Il gioco è operativo da sei mesi.</span><span class="sxs-lookup"><span data-stu-id="f669e-106">The game has been up and running for 6 months.</span></span> <span data-ttu-id="f669e-107">Sta registrando un grande successo, con milioni di download, e il tasso di conservazione è molto alto rispetto alle app di gioco di altre startup.</span><span class="sxs-lookup"><span data-stu-id="f669e-107">This game is a huge success, and it has millions of downloads and the retention is very high compared to other start-up game apps.</span></span> <span data-ttu-id="f669e-108">Durante la riunione di revisione trimestrale, le parti interessate concordano sulla necessità di aumentare i ricavi medi per utente (ARPU).</span><span class="sxs-lookup"><span data-stu-id="f669e-108">At the quarterly review meeting, stakeholders agree they need to increase average revenue per user (ARPU).</span></span> <span data-ttu-id="f669e-109">All'interno del gioco sono disponibili pacchetti Premium come offerte speciali.</span><span class="sxs-lookup"><span data-stu-id="f669e-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="f669e-110">Questi pacchetti permettono agli utenti di migliorare l'aspetto e le prestazioni delle lenze, delle esche o dell'attrezzatura da pesca all'interno del gioco.</span><span class="sxs-lookup"><span data-stu-id="f669e-110">These game packs allow users to upgrade the appearance and performance of their fishing lines and lures or tackles in the game.</span></span> <span data-ttu-id="f669e-111">Le vendite di pacchetti, però, sono molto basse.</span><span class="sxs-lookup"><span data-stu-id="f669e-111">However, package sales are very low.</span></span> <span data-ttu-id="f669e-112">Si decide quindi di analizzare prima di tutto l'esperienza degli utenti con uno strumento di analisi e di sviluppare poi un programma di engagement per aumentare le vendite attraverso la segmentazione avanzata.</span><span class="sxs-lookup"><span data-stu-id="f669e-112">So they decide first to analyze the customer experience with an analytics tool, and then to develop an engagement program to increase sales using advanced segmentation.</span></span>

<span data-ttu-id="f669e-113">Sulla base dell'articolo [Azure Mobile Engagement - Guida introduttiva con procedure consigliate](mobile-engagement-getting-started-best-practices.md) , viene costruita una strategia di engagement.</span><span class="sxs-lookup"><span data-stu-id="f669e-113">Based on the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="f669e-114">Obiettivi e indicatori KPI</span><span class="sxs-lookup"><span data-stu-id="f669e-114">Objectives and KPIs</span></span>
<span data-ttu-id="f669e-115">Le principali parti interessate dal gioco si incontrano.</span><span class="sxs-lookup"><span data-stu-id="f669e-115">Key stakeholders for the game meet.</span></span> <span data-ttu-id="f669e-116">Tutti concordano su un obiettivo primario: aumentare del 15% le vendite di pacchetti Premium.</span><span class="sxs-lookup"><span data-stu-id="f669e-116">All agree on one main objective - to increase premium package sales by 15%.</span></span> <span data-ttu-id="f669e-117">Vengono creati indicatori di prestazioni chiave aziendali per misurare e supportare questo obiettivo:</span><span class="sxs-lookup"><span data-stu-id="f669e-117">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span></span>

* <span data-ttu-id="f669e-118">Livello di gioco in cui vengono acquistati i pacchetti</span><span class="sxs-lookup"><span data-stu-id="f669e-118">On which level of the game are these packages purchased?</span></span>
* <span data-ttu-id="f669e-119">Definizione dei ricavi per utente, per sessione, alla settimana e al mese</span><span class="sxs-lookup"><span data-stu-id="f669e-119">What is the revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="f669e-120">Tipi di acquisto preferiti</span><span class="sxs-lookup"><span data-stu-id="f669e-120">What are the favorite purchase types?</span></span>

<span data-ttu-id="f669e-121">La parte 1 della [Guida introduttiva](mobile-engagement-getting-started-best-practices.md) illustra come definire gli obiettivi e gli indicatori KPI.</span><span class="sxs-lookup"><span data-stu-id="f669e-121">Part 1 of the [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how to define the objectives and KPIs.</span></span> 

<span data-ttu-id="f669e-122">Con gli indicatori KPI aziendali appena definiti, il Mobile Product Manager crea gli indicatori KPI di engagement per determinare le tendenze dei nuovi utenti e il tasso di conservazione.</span><span class="sxs-lookup"><span data-stu-id="f669e-122">With the Business KPIs now defined, the Mobile Product Manager creates Engagement KPIs to determine new user trends and retention.</span></span>

* <span data-ttu-id="f669e-123">Monitoraggio del tasso di conservazione e dell'uso nei seguenti intervalli: ogni giorno, ogni 2 giorni, ogni settimana, ogni mese e ogni 3 mesi</span><span class="sxs-lookup"><span data-stu-id="f669e-123">Monitor retention and use across the following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="f669e-124">Conteggio degli utenti attivi</span><span class="sxs-lookup"><span data-stu-id="f669e-124">Active user counts</span></span>
* <span data-ttu-id="f669e-125">Classificazione dell'app nello store</span><span class="sxs-lookup"><span data-stu-id="f669e-125">The app rating in the store</span></span>

<span data-ttu-id="f669e-126">In base ai suggerimenti del team IT, vengono aggiunti gli indicatori KPI tecnici riportati di seguito per rispondere alle domande seguenti:</span><span class="sxs-lookup"><span data-stu-id="f669e-126">Based on recommendations from the IT team, the following technical KPIs were added to answer the following questions:</span></span>

* <span data-ttu-id="f669e-127">Percorso utente (pagina visitata e tempo dedicato alla pagina dall'utente)</span><span class="sxs-lookup"><span data-stu-id="f669e-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="f669e-128">Numero di arresti anomali o bug rilevati per sessione</span><span class="sxs-lookup"><span data-stu-id="f669e-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="f669e-129">Versione del sistema operativo degli utenti</span><span class="sxs-lookup"><span data-stu-id="f669e-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="f669e-130">Dimensione media dello schermo degli utenti</span><span class="sxs-lookup"><span data-stu-id="f669e-130">What is the average size of screen for my users?</span></span>
* <span data-ttu-id="f669e-131">Tipo di connessione Internet degli utenti</span><span class="sxs-lookup"><span data-stu-id="f669e-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="f669e-132">Per ogni indicatore KPI, il Mobile Product Manager specifica i dati necessari e la loro posizione nello schema di progetto.</span><span class="sxs-lookup"><span data-stu-id="f669e-132">For each KPI the Mobile Product Manager specifies the data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="f669e-133">Programma di engagement e integrazione</span><span class="sxs-lookup"><span data-stu-id="f669e-133">Engagement program and integration</span></span>
<span data-ttu-id="f669e-134">Prima di creare un programma di engagement avanzato, il Mobile Project Manager responsabile del progetto dovrebbe conoscere a fondo le modalità e i tempi di utilizzo dei prodotti da parte degli utenti.</span><span class="sxs-lookup"><span data-stu-id="f669e-134">Before building an advanced engagement program, the Mobile Project Director in charge of the project should have a deep understanding of how and when products are consumed by the users.</span></span>

<span data-ttu-id="f669e-135">Dopo 3 mesi, il Mobile Project Manager ha raccolto dati sufficienti per migliorare le vendite delle notifiche push all'interno dell'app.</span><span class="sxs-lookup"><span data-stu-id="f669e-135">After 3 months, the Mobile Project Director has collected enough data to enhance his in-app push notification sales.</span></span> <span data-ttu-id="f669e-136">Informazioni raccolte:</span><span class="sxs-lookup"><span data-stu-id="f669e-136">He learns that:</span></span>

* <span data-ttu-id="f669e-137">Il primo acquisto si verifica in genere al livello 14 del gioco.</span><span class="sxs-lookup"><span data-stu-id="f669e-137">The first purchase generally happens at the level 14.</span></span> <span data-ttu-id="f669e-138">Nel 90% dei casi, vengono acquistate nuove armi leggendarie da 3 dollari.</span><span class="sxs-lookup"><span data-stu-id="f669e-138">For 90% of those cases, the purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="f669e-139">Nell'80% dei casi, gli utenti che hanno fatto un acquisto continuano a usare il prodotto e fanno altri acquisti.</span><span class="sxs-lookup"><span data-stu-id="f669e-139">In 80 % of those cases, users who have made a purchase, continue with the product and make more purchases.</span></span>
* <span data-ttu-id="f669e-140">Gli utenti che hanno superato il livello 20 iniziano a spendere oltre 10 dollari alla settimana.</span><span class="sxs-lookup"><span data-stu-id="f669e-140">Users who have passed the level 20, start to spend more than $10/week.</span></span>
* <span data-ttu-id="f669e-141">Gli utenti tendono ad acquistare pacchetti Premium ai livelli 16, 24 e 32.</span><span class="sxs-lookup"><span data-stu-id="f669e-141">Users tend to buy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="f669e-142">Grazie a questa analisi il Mobile Project Manager decide di creare sequenze di notifiche push specifiche per aumentare le vendite all'interno dell'app.</span><span class="sxs-lookup"><span data-stu-id="f669e-142">Thanks to this analysis the Mobile Project Director decides to create specific push notification sequences to increase in app sales.</span></span> <span data-ttu-id="f669e-143">Crea tre sequenze push denominate: programma di benvenuto, programma di vendita e programma utenti inattivi.</span><span class="sxs-lookup"><span data-stu-id="f669e-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="f669e-144">Per ulteriori informazioni consultare il [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="f669e-144">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
