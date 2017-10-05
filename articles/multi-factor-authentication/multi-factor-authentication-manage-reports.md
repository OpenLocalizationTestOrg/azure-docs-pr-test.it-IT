---
title: Rapporto di accesso e uso per Azure MFA | Microsoft Docs
description: "Viene descritto come usare la funzionalità dei report di Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: f76e726c6a67de4b0472c0e97f9e72c31c14c4f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="8a6c3-103">Report in Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="8a6c3-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="8a6c3-104">Azure Multi-Factor Authentication offre diversi report che possono essere utilizzati dall'utente e dall'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="8a6c3-105">Questi rapporti sono accessibili tramite il portale di gestione Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-105">These reports can be accessed through the Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="8a6c3-106">Di seguito è riportato un elenco dei rapporti disponibili:</span><span class="sxs-lookup"><span data-stu-id="8a6c3-106">The following is a list of the available reports:</span></span>

| <span data-ttu-id="8a6c3-107">Report</span><span class="sxs-lookup"><span data-stu-id="8a6c3-107">Report</span></span> | <span data-ttu-id="8a6c3-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8a6c3-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8a6c3-109">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="8a6c3-109">Usage</span></span> |<span data-ttu-id="8a6c3-110">I rapporti di utilizzo consentono di visualizzare informazioni sull'uso generale, un riepilogo e dettagli sull'utente.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-110">The usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="8a6c3-111">Stato server</span><span class="sxs-lookup"><span data-stu-id="8a6c3-111">Server Status</span></span> |<span data-ttu-id="8a6c3-112">Questo report consente di visualizzare lo stato dei server di Multi-Factor Authentication associati all'account.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-112">This report displays the status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="8a6c3-113">Cronologia utenti bloccati</span><span class="sxs-lookup"><span data-stu-id="8a6c3-113">Blocked User History</span></span> |<span data-ttu-id="8a6c3-114">Questi report mostrano la cronologia delle richieste per bloccare o sbloccare gli utenti.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-114">These reports show the history of requests to block or unblock users.</span></span> |
| <span data-ttu-id="8a6c3-115">Cronologia utenti bypass</span><span class="sxs-lookup"><span data-stu-id="8a6c3-115">Bypassed User History</span></span> |<span data-ttu-id="8a6c3-116">Consente di visualizzare la cronologia delle richieste per disabilitare Multi-Factor Authentication per il numero di telefono dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-116">Shows the history of requests to bypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="8a6c3-117">Avviso di illecito</span><span class="sxs-lookup"><span data-stu-id="8a6c3-117">Fraud Alert</span></span> |<span data-ttu-id="8a6c3-118">Consente di visualizzare una cronologia di avvisi di illecito inviati durante l'intervallo di date specificato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-118">Shows a history of fraud alerts submitted during the date range you specified.</span></span> |
| <span data-ttu-id="8a6c3-119">Queued</span><span class="sxs-lookup"><span data-stu-id="8a6c3-119">Queued</span></span> |<span data-ttu-id="8a6c3-120">Consente di elencare i report accodati da elaborare e i relativi stati.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="8a6c3-121">Quando il report è completo, viene fornito un collegamento per scaricare o visualizzare il report.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-121">A link to download or view the report is provided when the report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="8a6c3-122">Visualizzazione dei report</span><span class="sxs-lookup"><span data-stu-id="8a6c3-122">View reports</span></span>
1. <span data-ttu-id="8a6c3-123">Accedere al [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8a6c3-123">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="8a6c3-124">A sinistra selezionare Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-124">On the left, select Active Directory.</span></span>
3. <span data-ttu-id="8a6c3-125">Attenersi a una di queste due opzioni, a seconda che vengano usati provider di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="8a6c3-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="8a6c3-126">**Option 1**: fare clic sulla scheda dei provider Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-126">**Option 1**: Click the Multi-Factor Auth Providers tab.</span></span> <span data-ttu-id="8a6c3-127">Selezionare il provider di MFA e fare clic sul pulsante **Gestisci** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-127">Select your MFA provider and click the **Manage** button at the bottom.</span></span>
   * <span data-ttu-id="8a6c3-128">**Opzione 2**: selezionare la directory e passare alla scheda **Configura**.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-128">**Option 2**: Select your directory and go to the **Configure** tab.</span></span> <span data-ttu-id="8a6c3-129">Nella sezione Multi-Factor Authentication selezionare **Gestisci impostazioni del servizio**.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-129">Under the multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="8a6c3-130">Nella parte inferiore della pagina delle impostazioni del servizio MFA, fare clic sul collegamento Vai al portale.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-130">At the bottom of the MFA Service Settings page, click the Go to the portal link.</span></span>
4. <span data-ttu-id="8a6c3-131">Nel portale di gestione Azure Multi-Factor Authentication, selezionare il tipo di rapporto desiderato dalla sezione **Visualizza un report** nel riquadro di navigazione a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8a6c3-131">In the Azure Multi-Factor Authentication Management Portal, select the type of report you want from the **View a Report** section in the left navigation.</span></span>

<span data-ttu-id="8a6c3-132"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="8a6c3-132"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="8a6c3-133">**Risorse aggiuntive**</span><span class="sxs-lookup"><span data-stu-id="8a6c3-133">**Additional Resources**</span></span>

* [<span data-ttu-id="8a6c3-134">Per gli utenti</span><span class="sxs-lookup"><span data-stu-id="8a6c3-134">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="8a6c3-135">Azure Multi-Factor Authentication su MSDN</span><span class="sxs-lookup"><span data-stu-id="8a6c3-135">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
