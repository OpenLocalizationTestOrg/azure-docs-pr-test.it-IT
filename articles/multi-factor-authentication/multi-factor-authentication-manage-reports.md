---
title: report di utilizzo e aaaAccess per Azure MFA | Documenti Microsoft
description: "Descrive come toouse hello funzionalità di Azure multi-Factor Authentication - report."
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
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="b67b2-103">Report in Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="b67b2-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="b67b2-104">Azure Multi-Factor Authentication offre diversi report che possono essere utilizzati dall'utente e dall'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="b67b2-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="b67b2-105">Questi report sono accessibili tramite il portale di gestione di multi-Factor Authentication hello.</span><span class="sxs-lookup"><span data-stu-id="b67b2-105">These reports can be accessed through hello Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="b67b2-106">Hello seguito è riportato un elenco di report disponibili hello:</span><span class="sxs-lookup"><span data-stu-id="b67b2-106">hello following is a list of hello available reports:</span></span>

| <span data-ttu-id="b67b2-107">Report</span><span class="sxs-lookup"><span data-stu-id="b67b2-107">Report</span></span> | <span data-ttu-id="b67b2-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b67b2-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b67b2-109">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="b67b2-109">Usage</span></span> |<span data-ttu-id="b67b2-110">utilizzo di Hello report visualizza informazioni sull'utilizzo complessivo, riepilogo utenti e i dettagli dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b67b2-110">hello usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="b67b2-111">Stato server</span><span class="sxs-lookup"><span data-stu-id="b67b2-111">Server Status</span></span> |<span data-ttu-id="b67b2-112">Questo report visualizza lo stato di hello dei server di multi-Factor Authentication associati all'account.</span><span class="sxs-lookup"><span data-stu-id="b67b2-112">This report displays hello status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="b67b2-113">Cronologia utenti bloccati</span><span class="sxs-lookup"><span data-stu-id="b67b2-113">Blocked User History</span></span> |<span data-ttu-id="b67b2-114">Questi report mostrano la cronologia di hello di richieste tooblock o sblocco degli utenti.</span><span class="sxs-lookup"><span data-stu-id="b67b2-114">These reports show hello history of requests tooblock or unblock users.</span></span> |
| <span data-ttu-id="b67b2-115">Cronologia utenti bypass</span><span class="sxs-lookup"><span data-stu-id="b67b2-115">Bypassed User History</span></span> |<span data-ttu-id="b67b2-116">Mostra la cronologia hello di richieste toobypass multi-Factor Authentication per il numero di telefono dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b67b2-116">Shows hello history of requests toobypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="b67b2-117">Avviso di illecito</span><span class="sxs-lookup"><span data-stu-id="b67b2-117">Fraud Alert</span></span> |<span data-ttu-id="b67b2-118">Mostra una cronologia degli avvisi di illecito inviati durante l'intervallo di date hello specificato.</span><span class="sxs-lookup"><span data-stu-id="b67b2-118">Shows a history of fraud alerts submitted during hello date range you specified.</span></span> |
| <span data-ttu-id="b67b2-119">Queued</span><span class="sxs-lookup"><span data-stu-id="b67b2-119">Queued</span></span> |<span data-ttu-id="b67b2-120">Consente di elencare i report accodati da elaborare e i relativi stati.</span><span class="sxs-lookup"><span data-stu-id="b67b2-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="b67b2-121">Un report di hello toodownload o della vista di collegamento è disponibile quando viene completata hello del report.</span><span class="sxs-lookup"><span data-stu-id="b67b2-121">A link toodownload or view hello report is provided when hello report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="b67b2-122">Visualizzazione dei report</span><span class="sxs-lookup"><span data-stu-id="b67b2-122">View reports</span></span>
1. <span data-ttu-id="b67b2-123">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b67b2-123">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b67b2-124">Hello sinistra, selezionare Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b67b2-124">On hello left, select Active Directory.</span></span>
3. <span data-ttu-id="b67b2-125">Attenersi a una di queste due opzioni, a seconda che vengano usati provider di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="b67b2-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="b67b2-126">**Opzione 1**: fare clic sulla scheda provider multi-Factor Authentication hello. Selezionare il provider di autenticazione a più fattori e fare clic su hello **Gestisci** pulsante nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b67b2-126">**Option 1**: Click hello Multi-Factor Auth Providers tab. Select your MFA provider and click hello **Manage** button at hello bottom.</span></span>
   * <span data-ttu-id="b67b2-127">**Opzione 2**: selezionare il toohello directory e andare **configura** scheda. Hello multi-factor authentication, selezionare nella sezione **Gestisci impostazioni servizio**.</span><span class="sxs-lookup"><span data-stu-id="b67b2-127">**Option 2**: Select your directory and go toohello **Configure** tab. Under hello multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="b67b2-128">Nella parte inferiore di hello della pagina di impostazioni di servizio di autenticazione a più fattori hello, fare clic su hello Go toohello collegamento del portale.</span><span class="sxs-lookup"><span data-stu-id="b67b2-128">At hello bottom of hello MFA Service Settings page, click hello Go toohello portal link.</span></span>
4. <span data-ttu-id="b67b2-129">Nel portale di gestione di Azure multi-Factor Authentication hello, selezionare il tipo di hello di report che si desidera hello **visualizzare un Report** sezione hello riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b67b2-129">In hello Azure Multi-Factor Authentication Management Portal, select hello type of report you want from hello **View a Report** section in hello left navigation.</span></span>

<span data-ttu-id="b67b2-130"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="b67b2-130"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="b67b2-131">**Risorse aggiuntive**</span><span class="sxs-lookup"><span data-stu-id="b67b2-131">**Additional Resources**</span></span>

* [<span data-ttu-id="b67b2-132">Per gli utenti</span><span class="sxs-lookup"><span data-stu-id="b67b2-132">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="b67b2-133">Azure Multi-Factor Authentication su MSDN</span><span class="sxs-lookup"><span data-stu-id="b67b2-133">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
