---
title: gruppo di connettori lavoro aaaNo trovato per un'applicazione Proxy dell'applicazione | Documenti Microsoft
description: "Risolvere i problemi riscontrati quando è presente alcun lavoro connettore in un gruppo di connettori per l'applicazione con hello Proxy dell'applicazione Azure Active"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="1aa2f-103">Nessun gruppo di connettori funzionante trovato per un'applicazione Proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="1aa2f-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="1aa2f-104">La Guida di questo articolo è tooresolve hello comuni problemi quando non vi è un connettore per un'applicazione Proxy di applicazione integrata con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-104">This article help you tooresolve hello common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="1aa2f-105">Panoramica dei passaggi</span><span class="sxs-lookup"><span data-stu-id="1aa2f-105">Overview of steps</span></span>
<span data-ttu-id="1aa2f-106">Se è presente alcun lavoro connettore in un gruppo di connettori per l'applicazione, esistono alcuni problemi di hello tooresolve modi:</span><span class="sxs-lookup"><span data-stu-id="1aa2f-106">If there is no working Connector in a Connector Group for your application, there are a few ways tooresolve hello problem:</span></span>

-   <span data-ttu-id="1aa2f-107">Se non si dispone di alcun connettori nel gruppo di hello, è possibile:</span><span class="sxs-lookup"><span data-stu-id="1aa2f-107">If you have no connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="1aa2f-108">Scaricare un nuovo connettore nel server locale destra hello e assegnare a questo gruppo toothis</span><span class="sxs-lookup"><span data-stu-id="1aa2f-108">Download a new Connector on hello right on-prem server, and assign it toothis group</span></span>

    -   <span data-ttu-id="1aa2f-109">Spostare un connettore attivo nel gruppo di hello</span><span class="sxs-lookup"><span data-stu-id="1aa2f-109">Move an active Connector into hello group</span></span>

-   <span data-ttu-id="1aa2f-110">Se non si dispone di alcun connettore attivo nel gruppo di hello, è possibile:</span><span class="sxs-lookup"><span data-stu-id="1aa2f-110">If you have no active connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="1aa2f-111">Identificare il motivo di hello che il connettore è inattivo e risolvere</span><span class="sxs-lookup"><span data-stu-id="1aa2f-111">Identify hello reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="1aa2f-112">Spostare un connettore attivo nel gruppo di hello</span><span class="sxs-lookup"><span data-stu-id="1aa2f-112">Move an active Connector into hello group</span></span>

<span data-ttu-id="1aa2f-113">tooknow quale di questi problemi hello, aprire il menu di "Proxy dell'applicazione" hello nell'applicazione, confrontando il messaggio di avviso gruppo di connettori hello.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-113">tooknow which of these is hello issue, open hello “Application Proxy” menu in your Application, and look at hello Connector Group warning message.</span></span> <span data-ttu-id="1aa2f-114">Può specificare entrambi i gruppi che hello è necessario almeno un connettore (si dispone di nessuna gruppo hello) o che non dispone di alcun connettore attivo (anche se probabilmente si dispone di connettori inattivi).</span><span class="sxs-lookup"><span data-stu-id="1aa2f-114">It specify either that hello group needs at least one Connector (you have none in hello group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Selezione del gruppo di connettori nel portale di Azure](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="1aa2f-116">Per informazioni dettagliate su ognuna di queste opzioni, sezione hello corrispondente riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-116">For details on each of these options, see hello corresponding section below.</span></span> <span data-ttu-id="1aa2f-117">Ognuna di queste si presuppone che si inizi dalla pagina di gestione di hello connettore.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-117">Each of these assumes that you are starting from hello Connector management page.</span></span> <span data-ttu-id="1aa2f-118">Se si sta esaminando i messaggio di errore hello sopra riportato, è possibile passare toothis pagina facendo clic sul messaggio di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-118">If you are looking at hello error message above, you can go toothis page by clicking on hello warning message.</span></span> <span data-ttu-id="1aa2f-119">In caso contrario disponibile selezionando troppo**Azure Active Directory**, fare clic su **applicazioni aziendali**, quindi **Proxy dell'applicazione.**</span><span class="sxs-lookup"><span data-stu-id="1aa2f-119">Otherwise this can be found by going too**Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Gestione del gruppo di connettori nel portale di Azure](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="1aa2f-121">Scaricare un nuovo connettore</span><span class="sxs-lookup"><span data-stu-id="1aa2f-121">Download a new Connector</span></span>

<span data-ttu-id="1aa2f-122">toodownload un nuovo connettore, utilizzare pulsante "Scarica connettore" hello nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-122">toodownload a new Connector, use hello “Download Connector” button at hello top of hello page.</span></span>

<span data-ttu-id="1aa2f-123">esigenze del connettore hello nota toobe installato in un computer con l'applicazione di back-end toohello of di visibilità diretto e si trova in genere hello applicazione hello nello stesso server.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-123">note hello Connector needs toobe installed on a machine with direct line of sight toohello backend application, and is typically placed on hello same server as hello application.</span></span> <span data-ttu-id="1aa2f-124">Dopo aver scaricato, hello connettore dovrebbe essere visualizzato in questo menu.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-124">After downloading, hello Connector should appear in this menu.</span></span> <span data-ttu-id="1aa2f-125">Fare clic su hello connettore e utilizzare hello "Gruppo di connettori" elenco a discesa toomake che appartiene a gruppo corretto toohello.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-125">click hello Connector, and use hello “Connector Group” drop-down toomake sure it belongs toohello right group.</span></span> <span data-ttu-id="1aa2f-126">Salvare modifiche hello.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-126">Save hello change.</span></span>

   ![Scaricare il connettore hello da hello portale di Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="1aa2f-128">Spostare un connettore attivo</span><span class="sxs-lookup"><span data-stu-id="1aa2f-128">Move an Active Connector</span></span>

<span data-ttu-id="1aa2f-129">Se si dispone di un connettore attivo che deve appartenere toohello gruppo e che dispone di visibilità toohello l'applicazione back-end di destinazione, è possibile spostare hello connettore nel gruppo hello assegnato.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-129">If you have an active Connector that should belong toohello group and has line of sight toohello target backend application, you can move hello Connector into hello assigned group.</span></span> <span data-ttu-id="1aa2f-130">toodo questa operazione, scegliere hello connettore.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-130">toodo so, click hello Connector.</span></span> <span data-ttu-id="1aa2f-131">Nel campo "Gruppo di connettori" hello, utilizzare il gruppo corretto hello tooselect elenco a discesa hello e fare clic su Salva.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-131">In hello “Connector Group” field, use hello drop-down tooselect hello correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="1aa2f-132">Risolvere un connettore inattivo</span><span class="sxs-lookup"><span data-stu-id="1aa2f-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="1aa2f-133">Se hello solo connettori hello del gruppo sono inattivi, sono probabilmente su un computer che non sono stati sbloccati tutte le porte necessarie hello.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-133">If hello only Connectors in hello group are inactive, they are likely on a machine that does not have all hello necessary ports unblocked.</span></span>

<span data-ttu-id="1aa2f-134">Vedere porte hello documento di risoluzione dei problemi per informazioni dettagliate su questo problema in corso.</span><span class="sxs-lookup"><span data-stu-id="1aa2f-134">see hello ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1aa2f-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1aa2f-135">Next steps</span></span>
[<span data-ttu-id="1aa2f-136">Comprendere i connettori del proxy applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="1aa2f-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


