---
title: i criteri di accesso aaaData in Azure ora serie Insights | Documenti Microsoft
description: "In questa esercitazione, è illustrato toomanage criteri di accesso ai dati in fase di Insights di serie"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="2fab2-103">Concedere l'ambiente di data access tooa Insights serie ora tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2fab2-103">Grant data access tooa Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="2fab2-104">Gli ambienti Time Series Insights hanno due tipologie indipendenti di criteri di accesso:</span><span class="sxs-lookup"><span data-stu-id="2fab2-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="2fab2-105">Criteri di accesso di gestione</span><span class="sxs-lookup"><span data-stu-id="2fab2-105">Management access policies</span></span>
* <span data-ttu-id="2fab2-106">Criteri di accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="2fab2-106">Data access policies</span></span>

<span data-ttu-id="2fab2-107">Entrambi criteri concedono alle entità di sicurezza di Azure Active Directory (utenti e app) varie autorizzazioni per un determinato ambiente.</span><span class="sxs-lookup"><span data-stu-id="2fab2-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="2fab2-108">salve le entità (utenti e applicazioni) devono appartenere toohello active directory (o "Tenant di Azure") associato alla sottoscrizione hello contenente ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="2fab2-108">hello principals (users and apps) must belong toohello active directory (or “Azure tenant”) associated with hello subscription containing hello environment.</span></span>

<span data-ttu-id="2fab2-109">I criteri di accesso Gestione concedono configurazione toohello correlate le autorizzazioni dell'ambiente di hello, ad esempio</span><span class="sxs-lookup"><span data-stu-id="2fab2-109">Management access policies grant permissions related toohello configuration of hello environment, such as</span></span>
*   <span data-ttu-id="2fab2-110">Creazione e l'eliminazione dell'ambiente di hello, origini eventi, fare riferimento a set di dati, e</span><span class="sxs-lookup"><span data-stu-id="2fab2-110">Creation and deletion of hello environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="2fab2-111">Gestione dei criteri di accesso ai dati hello.</span><span class="sxs-lookup"><span data-stu-id="2fab2-111">Management of hello data access policies.</span></span>

<span data-ttu-id="2fab2-112">Criteri di accesso ai dati concedono le autorizzazioni di query di data tooissue, modificano i dati di riferimento nell'ambiente di hello e condividono le query salvate e alle prospettive associate ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="2fab2-112">Data access policies grant permissions tooissue data queries, manipulate reference data in hello environment, and share saved queries and perspectives associated with hello environment.</span></span>

<span data-ttu-id="2fab2-113">due tipi di Hello di criteri consentono una netta separazione tra la gestione dell'ambiente hello toohello di accesso e accedere ai dati toohello hello ambiente.</span><span class="sxs-lookup"><span data-stu-id="2fab2-113">hello two kinds of policies allow clear separation between access toohello management of hello environment and access toohello data inside hello environment.</span></span> <span data-ttu-id="2fab2-114">Ad esempio, è possibile toosetup un ambiente tale proprietario hello/creatore dell'ambiente hello viene rimosso dall'accesso ai dati hello.</span><span class="sxs-lookup"><span data-stu-id="2fab2-114">For example, it is possible toosetup an environment such that hello owner/creator of hello environment is removed from hello data access.</span></span> <span data-ttu-id="2fab2-115">Oltre a utenti e servizi che sono consentiti dati tooread hello ambiente non può essere concessa alcuna configurazione di accesso toohello dell'ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="2fab2-115">As well as users and services that are allowed tooread data from hello environment may be granted no access toohello configuration of hello environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="2fab2-116">Concedere l'accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="2fab2-116">Grant data access</span></span>
<span data-ttu-id="2fab2-117">Hello passaggi seguenti viene illustrato come accedere a dati toogrant per un'entità utente:</span><span class="sxs-lookup"><span data-stu-id="2fab2-117">hello following steps show how toogrant data access for a user principal:</span></span>

1.  <span data-ttu-id="2fab2-118">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2fab2-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="2fab2-119">Fare clic su "Tutte le risorse" nel menu hello sul lato sinistro di hello di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fab2-119">Click “All resources” in hello menu on hello left side of hello Azure portal.</span></span>
3.  <span data-ttu-id="2fab2-120">Selezionare l'ambiente Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="2fab2-120">Select your Time Series Insights environment.</span></span>

  ![Gestire l'origine ora serie Insights hello - ambiente](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="2fab2-122">Selezionare "Accesso al piano dati" e fare clic su "Aggiungi".</span><span class="sxs-lookup"><span data-stu-id="2fab2-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Gestire l'origine ora serie Insights hello - Aggiungi](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="2fab2-124">Fare clic su "Seleziona utente".</span><span class="sxs-lookup"><span data-stu-id="2fab2-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="2fab2-125">Ricerca e selezionare l'utente tramite posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="2fab2-125">Search and select user by hello email.</span></span>
7.  <span data-ttu-id="2fab2-126">Fare clic su "Seleziona" nel pannello "Selezionare l'utente".</span><span class="sxs-lookup"><span data-stu-id="2fab2-126">Click “Select” in “Select User” blade.</span></span>

  ![Gestire l'origine ora serie Insights hello - selezionare l'utente](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="2fab2-128">Fare clic su "Seleziona ruolo".</span><span class="sxs-lookup"><span data-stu-id="2fab2-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="2fab2-129">Se si desidera che i dati di riferimento tooallow utente toochange condividere query salvate e prospettive con altri utenti dell'ambiente di hello, selezionare "Collaboratore".</span><span class="sxs-lookup"><span data-stu-id="2fab2-129">Select “Contributor” if you want tooallow user toochange reference data and share saved queries and perspectives with other users of hello environment.</span></span> <span data-ttu-id="2fab2-130">In caso contrario, selezionare i dati di query di "Lettura" tooallow utente nell'ambiente di hello e salvare query (non condivisa) personali nell'ambiente di hello.</span><span class="sxs-lookup"><span data-stu-id="2fab2-130">Otherwise select “Reader” tooallow user query data in hello environment and save personal (not shared) queries in hello environment.</span></span>
10. <span data-ttu-id="2fab2-131">Nel pannello "Selezionare il ruolo" hello, fare clic su "Ok".</span><span class="sxs-lookup"><span data-stu-id="2fab2-131">Click “Ok” in hello “Select Role” blade.</span></span>

  ![Gestire origine ora serie Insights hello - selezione ruolo](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="2fab2-133">Nel pannello "Selezionare il ruolo utente" hello, fare clic su "Ok".</span><span class="sxs-lookup"><span data-stu-id="2fab2-133">Click “Ok” in hello “Select User Role” blade.</span></span>
12. <span data-ttu-id="2fab2-134">Dovrebbe essere visualizzato:</span><span class="sxs-lookup"><span data-stu-id="2fab2-134">You should see:</span></span>

  ![Gestire l'origine ora serie Insights hello - risultati](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="2fab2-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2fab2-136">Next steps</span></span>

* [<span data-ttu-id="2fab2-137">Creare un'origine evento</span><span class="sxs-lookup"><span data-stu-id="2fab2-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="2fab2-138">[Invio di eventi](time-series-insights-send-events.md) origine evento toohello</span><span class="sxs-lookup"><span data-stu-id="2fab2-138">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="2fab2-139">Visualizzare l'ambiente nel [portale di Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="2fab2-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
