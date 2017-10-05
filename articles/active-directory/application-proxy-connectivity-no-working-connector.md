---
title: Nessun gruppo di connettori funzionante trovato per un'applicazione Proxy di applicazione | Microsoft Docs
description: Risoluzione dei problemi riscontrati quando non esiste alcun connettore funzionante in un gruppo di connettori per l'applicazione con Proxy di applicazione di Azure AD
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
ms.openlocfilehash: 4945958deedc8a1d9989ff901192c03a5363b4dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="39070-103">Nessun gruppo di connettori funzionante trovato per un'applicazione Proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="39070-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="39070-104">Questo articolo fornisce istruzioni sulla risoluzione di problemi comuni riscontrati quando non viene rilevato un connettore per un'applicazione Proxy di applicazione integrata con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="39070-104">This article help you to resolve the common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="39070-105">Panoramica dei passaggi</span><span class="sxs-lookup"><span data-stu-id="39070-105">Overview of steps</span></span>
<span data-ttu-id="39070-106">Se nella propria applicazione non è presente alcun connettore funzionante in un gruppo di connettori, il problema può essere risolto in diversi modi:</span><span class="sxs-lookup"><span data-stu-id="39070-106">If there is no working Connector in a Connector Group for your application, there are a few ways to resolve the problem:</span></span>

-   <span data-ttu-id="39070-107">Se il gruppo non contiene connettori, è possibile:</span><span class="sxs-lookup"><span data-stu-id="39070-107">If you have no connectors in the group, you can:</span></span>

    -   <span data-ttu-id="39070-108">Scaricare un nuovo connettore sul server locale corretto e assegnarlo a questo gruppo</span><span class="sxs-lookup"><span data-stu-id="39070-108">Download a new Connector on the right on-prem server, and assign it to this group</span></span>

    -   <span data-ttu-id="39070-109">Spostare un connettore attivo nel gruppo</span><span class="sxs-lookup"><span data-stu-id="39070-109">Move an active Connector into the group</span></span>

-   <span data-ttu-id="39070-110">Se il gruppo non contiene connettori attivi, è possibile:</span><span class="sxs-lookup"><span data-stu-id="39070-110">If you have no active connectors in the group, you can:</span></span>

    -   <span data-ttu-id="39070-111">Identificare il motivo per cui il connettore è inattivo e risolvere il problema</span><span class="sxs-lookup"><span data-stu-id="39070-111">Identify the reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="39070-112">Spostare un connettore attivo nel gruppo</span><span class="sxs-lookup"><span data-stu-id="39070-112">Move an active Connector into the group</span></span>

<span data-ttu-id="39070-113">Per sapere quale di questi è il problema riscontrato, aprire il menu "Proxy di applicazione" nell'applicazione, quindi cercare il messaggio di avviso del gruppo di connettori.</span><span class="sxs-lookup"><span data-stu-id="39070-113">To know which of these is the issue, open the “Application Proxy” menu in your Application, and look at the Connector Group warning message.</span></span> <span data-ttu-id="39070-114">Specifica che il gruppo deve contenere almeno un connettore (se il gruppo non ne contiene alcuno) o che non vi sono connettori attivi (anche se sono inclusi probabilmente connettori inattivi).</span><span class="sxs-lookup"><span data-stu-id="39070-114">It specify either that the group needs at least one Connector (you have none in the group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Selezione del gruppo di connettori nel portale di Azure](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="39070-116">Per informazioni dettagliate su ognuna di queste opzioni, vedere la sezione corrispondente riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="39070-116">For details on each of these options, see the corresponding section below.</span></span> <span data-ttu-id="39070-117">Ognuno di questi passaggi presuppone che si inizi dalla pagina di gestione del connettore.</span><span class="sxs-lookup"><span data-stu-id="39070-117">Each of these assumes that you are starting from the Connector management page.</span></span> <span data-ttu-id="39070-118">Se si sta analizzando il messaggio di errore sopra riportato, è possibile passare a questa pagina facendo clic sul messaggio di avviso.</span><span class="sxs-lookup"><span data-stu-id="39070-118">If you are looking at the error message above, you can go to this page by clicking on the warning message.</span></span> <span data-ttu-id="39070-119">In alternativa, passare a **Azure Active Directory**, fare clic su **Applicazioni aziendali** e quindi su **Proxy di applicazione.**</span><span class="sxs-lookup"><span data-stu-id="39070-119">Otherwise this can be found by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Gestione del gruppo di connettori nel portale di Azure](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="39070-121">Scaricare un nuovo connettore</span><span class="sxs-lookup"><span data-stu-id="39070-121">Download a new Connector</span></span>

<span data-ttu-id="39070-122">Per scaricare un nuovo connettore, usare il pulsante "Scaricare il connettore" nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="39070-122">To download a new Connector, use the “Download Connector” button at the top of the page.</span></span>

<span data-ttu-id="39070-123">Si noti che il connettore deve essere installato su un computer che abbia una linea di visuale diretta all'applicazione back-end e si trova in genere sullo stesso server dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="39070-123">note the Connector needs to be installed on a machine with direct line of sight to the backend application, and is typically placed on the same server as the application.</span></span> <span data-ttu-id="39070-124">Dopo essere stato scaricato, il connettore viene visualizzato in questo menu.</span><span class="sxs-lookup"><span data-stu-id="39070-124">After downloading, the Connector should appear in this menu.</span></span> <span data-ttu-id="39070-125">Fare clic sul connettore e usare l'elenco a discesa "Gruppo di connettori" per assicurarsi che appartenga al gruppo corretto.</span><span class="sxs-lookup"><span data-stu-id="39070-125">click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group.</span></span> <span data-ttu-id="39070-126">Salvare la modifica.</span><span class="sxs-lookup"><span data-stu-id="39070-126">Save the change.</span></span>

   ![Scaricare il connettore dal portale di Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="39070-128">Spostare un connettore attivo</span><span class="sxs-lookup"><span data-stu-id="39070-128">Move an Active Connector</span></span>

<span data-ttu-id="39070-129">Se si dispone di un connettore attivo che deve appartenere a questo gruppo e ha una linea di visuale sull'applicazione back-end, è possibile spostare il connettore nel gruppo assegnato.</span><span class="sxs-lookup"><span data-stu-id="39070-129">If you have an active Connector that should belong to the group and has line of sight to the target backend application, you can move the Connector into the assigned group.</span></span> <span data-ttu-id="39070-130">A tale scopo, fare clic sul connettore.</span><span class="sxs-lookup"><span data-stu-id="39070-130">To do so, click the Connector.</span></span> <span data-ttu-id="39070-131">Nel campo "Gruppo di connettori", usare l'elenco a discesa per selezionare il gruppo corretto e fare clic su Salva.</span><span class="sxs-lookup"><span data-stu-id="39070-131">In the “Connector Group” field, use the drop-down to select the correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="39070-132">Risolvere un connettore inattivo</span><span class="sxs-lookup"><span data-stu-id="39070-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="39070-133">Se il gruppo include solo connettori inattivi, sono probabilmente in un computer che non dispone di tutte le porte necessarie sbloccate.</span><span class="sxs-lookup"><span data-stu-id="39070-133">If the only Connectors in the group are inactive, they are likely on a machine that does not have all the necessary ports unblocked.</span></span>

<span data-ttu-id="39070-134">Vedere il documento di risoluzione dei problemi relativi alle porte per informazioni dettagliate sull'analisi di questo problema.</span><span class="sxs-lookup"><span data-stu-id="39070-134">see the ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39070-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="39070-135">Next steps</span></span>
[<span data-ttu-id="39070-136">Comprendere i connettori del proxy applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="39070-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


