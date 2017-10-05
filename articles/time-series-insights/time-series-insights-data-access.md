---
title: Criteri di accesso ai dati in Azure Time Series Insights | Microsoft Docs
description: Questa esercitazione illustra come gestire i criteri di accesso ai dati in Time Series Insights
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
ms.openlocfilehash: e975c6d8f217bc73948c0c046204b16b1a742bc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="grant-data-access-to-a-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="a5ec2-103">Concedere l'accesso ai dati in un ambiente Time Series Insights con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a5ec2-103">Grant data access to a Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="a5ec2-104">Gli ambienti Time Series Insights hanno due tipologie indipendenti di criteri di accesso:</span><span class="sxs-lookup"><span data-stu-id="a5ec2-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="a5ec2-105">Criteri di accesso di gestione</span><span class="sxs-lookup"><span data-stu-id="a5ec2-105">Management access policies</span></span>
* <span data-ttu-id="a5ec2-106">Criteri di accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="a5ec2-106">Data access policies</span></span>

<span data-ttu-id="a5ec2-107">Entrambi criteri concedono alle entità di sicurezza di Azure Active Directory (utenti e app) varie autorizzazioni per un determinato ambiente.</span><span class="sxs-lookup"><span data-stu-id="a5ec2-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="a5ec2-108">Le entità di sicurezza (utenti e app) devono appartenere all'istanza di Active Directory ("tenant di Azure") associata alla sottoscrizione contenente l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="a5ec2-108">The principals (users and apps) must belong to the active directory (or “Azure tenant”) associated with the subscription containing the environment.</span></span>

<span data-ttu-id="a5ec2-109">I criteri di accesso di gestione concedono le autorizzazioni relative alla configurazione dell'ambiente, che includono:</span><span class="sxs-lookup"><span data-stu-id="a5ec2-109">Management access policies grant permissions related to the configuration of the environment, such as</span></span>
*   <span data-ttu-id="a5ec2-110">Creazione ed eliminazione dell'ambiente, delle origini evento e dei set di dati di riferimento</span><span class="sxs-lookup"><span data-stu-id="a5ec2-110">Creation and deletion of the environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="a5ec2-111">Gestione dei criteri di accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="a5ec2-111">Management of the data access policies.</span></span>

<span data-ttu-id="a5ec2-112">I criteri di accesso ai dati concedono le autorizzazioni per eseguire query sui dati, modificare i dati di riferimento nell'ambiente e condividere le prospettive e le query salvate associate all'ambiente.</span><span class="sxs-lookup"><span data-stu-id="a5ec2-112">Data access policies grant permissions to issue data queries, manipulate reference data in the environment, and share saved queries and perspectives associated with the environment.</span></span>

<span data-ttu-id="a5ec2-113">Le due tipologie di criteri consentono una netta separazione tra l'accesso alla gestione dell'ambiente e l'accesso ai dati all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="a5ec2-113">The two kinds of policies allow clear separation between access to the management of the environment and access to the data inside the environment.</span></span> <span data-ttu-id="a5ec2-114">È ad esempio possibile configurare un ambiente in modo che il relativo proprietario/creatore sia rimosso dall'accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="a5ec2-114">For example, it is possible to setup an environment such that the owner/creator of the environment is removed from the data access.</span></span> <span data-ttu-id="a5ec2-115">Analogamente, a utenti e servizi a cui è consentita la lettura dei dati dell'ambiente può non essere concesso l'accesso alla configurazione dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="a5ec2-115">As well as users and services that are allowed to read data from the environment may be granted no access to the configuration of the environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="a5ec2-116">Concedere l'accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="a5ec2-116">Grant data access</span></span>
<span data-ttu-id="a5ec2-117">La procedura seguente illustra come concedere l'accesso ai dati per un'entità utente:</span><span class="sxs-lookup"><span data-stu-id="a5ec2-117">The following steps show how to grant data access for a user principal:</span></span>

1.  <span data-ttu-id="a5ec2-118">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5ec2-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="a5ec2-119">Fare clic su "Tutte le risorse" nel menu sul lato sinistro del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a5ec2-119">Click “All resources” in the menu on the left side of the Azure portal.</span></span>
3.  <span data-ttu-id="a5ec2-120">Selezionare l'ambiente Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="a5ec2-120">Select your Time Series Insights environment.</span></span>

  ![Gestire l'origine Time Series Insights: ambiente](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="a5ec2-122">Selezionare "Accesso al piano dati" e fare clic su "Aggiungi".</span><span class="sxs-lookup"><span data-stu-id="a5ec2-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Gestire l'origine Time Series Insights: aggiunta](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="a5ec2-124">Fare clic su "Seleziona utente".</span><span class="sxs-lookup"><span data-stu-id="a5ec2-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="a5ec2-125">Cercare e selezionare l'utente in base all'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="a5ec2-125">Search and select user by the email.</span></span>
7.  <span data-ttu-id="a5ec2-126">Fare clic su "Seleziona" nel pannello "Selezionare l'utente".</span><span class="sxs-lookup"><span data-stu-id="a5ec2-126">Click “Select” in “Select User” blade.</span></span>

  ![Gestire l'origine Time Series Insights: selezione dell'utente](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="a5ec2-128">Fare clic su "Seleziona ruolo".</span><span class="sxs-lookup"><span data-stu-id="a5ec2-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="a5ec2-129">Selezionare "Collaboratore" se si vuole consentire all'utente di modificare i dati di riferimento e condividere le prospettive e le query salvate con altri utenti dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="a5ec2-129">Select “Contributor” if you want to allow user to change reference data and share saved queries and perspectives with other users of the environment.</span></span> <span data-ttu-id="a5ec2-130">In alternativa, selezionare "Lettore" per consentire all'utente di eseguire query sui dati e salvare query personali (non condivise) nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="a5ec2-130">Otherwise select “Reader” to allow user query data in the environment and save personal (not shared) queries in the environment.</span></span>
10. <span data-ttu-id="a5ec2-131">Fare clic su "OK" nel pannello "Selezionare un ruolo".</span><span class="sxs-lookup"><span data-stu-id="a5ec2-131">Click “Ok” in the “Select Role” blade.</span></span>

  ![Gestire l'origine Time Series Insights: selezione del ruolo](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="a5ec2-133">Fare clic su "OK" nel pannello "Selezionare il ruolo utente".</span><span class="sxs-lookup"><span data-stu-id="a5ec2-133">Click “Ok” in the “Select User Role” blade.</span></span>
12. <span data-ttu-id="a5ec2-134">Dovrebbe essere visualizzato:</span><span class="sxs-lookup"><span data-stu-id="a5ec2-134">You should see:</span></span>

  ![Gestire l'origine Time Series Insights: risultati](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="a5ec2-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a5ec2-136">Next steps</span></span>

* [<span data-ttu-id="a5ec2-137">Creare un'origine evento</span><span class="sxs-lookup"><span data-stu-id="a5ec2-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="a5ec2-138">[Inviare eventi](time-series-insights-send-events.md) all'origine evento</span><span class="sxs-lookup"><span data-stu-id="a5ec2-138">[Send events](time-series-insights-send-events.md) to the event source</span></span>
* <span data-ttu-id="a5ec2-139">Visualizzare l'ambiente nel [portale di Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="a5ec2-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
