---
title: implementazione di Mobile Engagement aaaAzure per App di gioco
description: "Modalità di gioco app scenario tooimplement Azure Mobile Engagement"
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
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="5d46c-103">Implementare Mobile Engagement con app di gioco</span><span class="sxs-lookup"><span data-stu-id="5d46c-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="5d46c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="5d46c-104">Overview</span></span>
<span data-ttu-id="5d46c-105">Una startup del settore gaming ha lanciato una nuova app di gioco di ruolo e strategia ispirata al mondo della pesca.</span><span class="sxs-lookup"><span data-stu-id="5d46c-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="5d46c-106">gioco di Hello è stato installato e in esecuzione per 6 mesi.</span><span class="sxs-lookup"><span data-stu-id="5d46c-106">hello game has been up and running for 6 months.</span></span> <span data-ttu-id="5d46c-107">Il gioco è enorme esito positivo, include milioni di download e memorizzazione hello è molto elevato tooother confrontati avvio gioco app.</span><span class="sxs-lookup"><span data-stu-id="5d46c-107">This game is a huge success, and it has millions of downloads and hello retention is very high compared tooother start-up game apps.</span></span> <span data-ttu-id="5d46c-108">Riunione di revisione trimestrale hello, le parti interessate accettano che devono tooincrease Ricavi medi per utente (ARPU).</span><span class="sxs-lookup"><span data-stu-id="5d46c-108">At hello quarterly review meeting, stakeholders agree they need tooincrease average revenue per user (ARPU).</span></span> <span data-ttu-id="5d46c-109">All'interno del gioco sono disponibili pacchetti Premium come offerte speciali.</span><span class="sxs-lookup"><span data-stu-id="5d46c-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="5d46c-110">Questi pacchetti di giochi consentono aspetto hello tooupgrade di utenti e le prestazioni delle loro righe pesca e ami da o tackles nel gioco hello.</span><span class="sxs-lookup"><span data-stu-id="5d46c-110">These game packs allow users tooupgrade hello appearance and performance of their fishing lines and lures or tackles in hello game.</span></span> <span data-ttu-id="5d46c-111">Le vendite di pacchetti, però, sono molto basse.</span><span class="sxs-lookup"><span data-stu-id="5d46c-111">However, package sales are very low.</span></span> <span data-ttu-id="5d46c-112">Pertanto si decide prima tooanalyze hello analisi con uno strumento di analitica e quindi toodevelop un coinvolgimento programma tooincrease delle vendite tramite avanzate segmentazione.</span><span class="sxs-lookup"><span data-stu-id="5d46c-112">So they decide first tooanalyze hello customer experience with an analytics tool, and then toodevelop an engagement program tooincrease sales using advanced segmentation.</span></span>

<span data-ttu-id="5d46c-113">In base a hello [Azure Mobile Engagement - Guida introduttiva alle procedure consigliate](mobile-engagement-getting-started-best-practices.md) la compilazione di una strategia di assunzione.</span><span class="sxs-lookup"><span data-stu-id="5d46c-113">Based on hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="5d46c-114">Obiettivi e indicatori KPI</span><span class="sxs-lookup"><span data-stu-id="5d46c-114">Objectives and KPIs</span></span>
<span data-ttu-id="5d46c-115">Principali parti interessate per gioco hello soddisfano.</span><span class="sxs-lookup"><span data-stu-id="5d46c-115">Key stakeholders for hello game meet.</span></span> <span data-ttu-id="5d46c-116">Tutti concordano un obiettivo principale - vendite di pacchetto premium tooincrease del 15%.</span><span class="sxs-lookup"><span data-stu-id="5d46c-116">All agree on one main objective - tooincrease premium package sales by 15%.</span></span> <span data-ttu-id="5d46c-117">Vengono creati unità e toomeasure Business indicatori di prestazioni chiave (KPI), questo obiettivo</span><span class="sxs-lookup"><span data-stu-id="5d46c-117">They create Business Key Performance Indicators (KPIs) toomeasure and drive this objective</span></span>

* <span data-ttu-id="5d46c-118">Il livello di gioco hello vengono acquistati questi pacchetti</span><span class="sxs-lookup"><span data-stu-id="5d46c-118">On which level of hello game are these packages purchased?</span></span>
* <span data-ttu-id="5d46c-119">Che cos'è ricavi hello per ogni utente, sessione, settimana e mese?</span><span class="sxs-lookup"><span data-stu-id="5d46c-119">What is hello revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="5d46c-120">Quali sono i tipi di acquisto Preferiti hello?</span><span class="sxs-lookup"><span data-stu-id="5d46c-120">What are hello favorite purchase types?</span></span>

<span data-ttu-id="5d46c-121">Parte 1 di hello [Guida introduttiva](mobile-engagement-getting-started-best-practices.md) spiega come toodefine hello obiettivi e indicatori KPI.</span><span class="sxs-lookup"><span data-stu-id="5d46c-121">Part 1 of hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how toodefine hello objectives and KPIs.</span></span> 

<span data-ttu-id="5d46c-122">Con hello che KPI aziendali ora definiti, hello Mobile prodotto Manager crea tendenze di indicatori KPI di Engagement toodetermine nuovo utente e di memorizzazione.</span><span class="sxs-lookup"><span data-stu-id="5d46c-122">With hello Business KPIs now defined, hello Mobile Product Manager creates Engagement KPIs toodetermine new user trends and retention.</span></span>

* <span data-ttu-id="5d46c-123">Memorizzazione di monitoraggio e l'uso in hello seguenti intervalli: ogni giorno, ogni 2 giorni, ogni settimana, mese e ogni 3 mesi</span><span class="sxs-lookup"><span data-stu-id="5d46c-123">Monitor retention and use across hello following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="5d46c-124">Conteggio degli utenti attivi</span><span class="sxs-lookup"><span data-stu-id="5d46c-124">Active user counts</span></span>
* <span data-ttu-id="5d46c-125">classificazione app Hello in hello archiviare</span><span class="sxs-lookup"><span data-stu-id="5d46c-125">hello app rating in hello store</span></span>

<span data-ttu-id="5d46c-126">In base alle raccomandazioni del team IT hello, hello seguenti tecnici indicatori KPI sono state aggiunte hello tooanswer seguenti domande:</span><span class="sxs-lookup"><span data-stu-id="5d46c-126">Based on recommendations from hello IT team, hello following technical KPIs were added tooanswer hello following questions:</span></span>

* <span data-ttu-id="5d46c-127">Percorso utente (pagina visitata e tempo dedicato alla pagina dall'utente)</span><span class="sxs-lookup"><span data-stu-id="5d46c-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="5d46c-128">Numero di arresti anomali o bug rilevati per sessione</span><span class="sxs-lookup"><span data-stu-id="5d46c-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="5d46c-129">Versione del sistema operativo degli utenti</span><span class="sxs-lookup"><span data-stu-id="5d46c-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="5d46c-130">Che cos'è di dimensioni medie di hello dello schermo per gli utenti?</span><span class="sxs-lookup"><span data-stu-id="5d46c-130">What is hello average size of screen for my users?</span></span>
* <span data-ttu-id="5d46c-131">Tipo di connessione Internet degli utenti</span><span class="sxs-lookup"><span data-stu-id="5d46c-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="5d46c-132">Per ogni indicatore KPI hello Mobile prodotto Manager specifica dati hello ha bisogno e in cui si trova nel proprio playbook.</span><span class="sxs-lookup"><span data-stu-id="5d46c-132">For each KPI hello Mobile Product Manager specifies hello data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="5d46c-133">Programma di engagement e integrazione</span><span class="sxs-lookup"><span data-stu-id="5d46c-133">Engagement program and integration</span></span>
<span data-ttu-id="5d46c-134">Prima di compilare un programma engagement avanzate, hello Mobile progetto Director responsabile di progetto hello deve avere una conoscenza approfondita di come e quando i prodotti vengono utilizzati dagli utenti di hello.</span><span class="sxs-lookup"><span data-stu-id="5d46c-134">Before building an advanced engagement program, hello Mobile Project Director in charge of hello project should have a deep understanding of how and when products are consumed by hello users.</span></span>

<span data-ttu-id="5d46c-135">Dopo 3 mesi, hello Director progetto Mobile è state raccolte sufficiente tooenhance dati le proprie vendite di notifica push all'interno dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5d46c-135">After 3 months, hello Mobile Project Director has collected enough data tooenhance his in-app push notification sales.</span></span> <span data-ttu-id="5d46c-136">Informazioni raccolte:</span><span class="sxs-lookup"><span data-stu-id="5d46c-136">He learns that:</span></span>

* <span data-ttu-id="5d46c-137">primo acquisto Hello in genere si verifica a livello di hello 14.</span><span class="sxs-lookup"><span data-stu-id="5d46c-137">hello first purchase generally happens at hello level 14.</span></span> <span data-ttu-id="5d46c-138">Per 90% di questi casi, acquisto hello è nuove armi erede per $3.</span><span class="sxs-lookup"><span data-stu-id="5d46c-138">For 90% of those cases, hello purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="5d46c-139">80% di questi casi, gli utenti che hanno effettuato un acquisto, continuare con il prodotto hello e rendere più acquisti.</span><span class="sxs-lookup"><span data-stu-id="5d46c-139">In 80 % of those cases, users who have made a purchase, continue with hello product and make more purchases.</span></span>
* <span data-ttu-id="5d46c-140">Gli utenti che hanno superato il livello di hello 20, avviare toospend maggiore di $10/ settimana.</span><span class="sxs-lookup"><span data-stu-id="5d46c-140">Users who have passed hello level 20, start toospend more than $10/week.</span></span>
* <span data-ttu-id="5d46c-141">Gli utenti tendono a pacchetti premium toobuy livello 16, 24 e 32.</span><span class="sxs-lookup"><span data-stu-id="5d46c-141">Users tend toobuy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="5d46c-142">Ringrazia analysis toothis hello Mobile progetto Director decide toocreate push specifici notifica sequenze tooincrease nella vendita di app.</span><span class="sxs-lookup"><span data-stu-id="5d46c-142">Thanks toothis analysis hello Mobile Project Director decides toocreate specific push notification sequences tooincrease in app sales.</span></span> <span data-ttu-id="5d46c-143">Crea tre sequenze push denominate: programma di benvenuto, programma di vendita e programma utenti inattivi.</span><span class="sxs-lookup"><span data-stu-id="5d46c-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="5d46c-144">Per ulteriori informazioni consultare toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="5d46c-144">For more information refer toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
