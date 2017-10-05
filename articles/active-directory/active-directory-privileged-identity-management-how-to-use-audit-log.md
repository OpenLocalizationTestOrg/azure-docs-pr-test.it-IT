---
title: Come usare il log di controllo in Azure AD Privileged Identity Management | Documentazione Microsoft
description: Informazioni su come usare il log di controllo nell'estensione Azure Privileged Identity Management.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 7d9a5255a64d46c1388d328a606b3f297d61262b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-audit-log-in-pim"></a><span data-ttu-id="a0aa2-103">Uso del log di controllo in PIM</span><span class="sxs-lookup"><span data-stu-id="a0aa2-103">Using the audit log in PIM</span></span>
<span data-ttu-id="a0aa2-104">È possibile usare il log di controllo di Privileged Identity Management (PIM) per visualizzare tutte le assegnazioni utente e le attivazioni per un periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-104">You can use the Privileged Identity Management (PIM) audit log to see all the user assignments and activations within a given time period.</span></span> <span data-ttu-id="a0aa2-105">Se si desidera visualizzare la cronologia di controllo completa dell'attività nel tenant, inclusi amministratore, utente finale e attività di sincronizzazione, è possibile usare i [report di accesso e utilizzo di Azure Active Directory.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="a0aa2-105">If you want to see the full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use the [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-to-the-audit-log"></a><span data-ttu-id="a0aa2-106">Accedere al log di controllo</span><span class="sxs-lookup"><span data-stu-id="a0aa2-106">Navigate to the audit log</span></span>
<span data-ttu-id="a0aa2-107">Nel dashboard del [portale di Azure](https://portal.azure.com) selezionare l'app **Azure AD Privileged Identity Management** .</span><span class="sxs-lookup"><span data-stu-id="a0aa2-107">From the [Azure portal](https://portal.azure.com) dashboard, select the **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="a0aa2-108">Da qui è possibile accedere al log di controllo facendo clic su **Gestione dei ruoli con privilegi** > **Cronologia dei controlli** nel dashboard di PIM.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-108">From there, access the audit log by clicking **Manage privileged roles** > **Audit history** in the PIM dashboard.</span></span>

## <a name="the-audit-log-graph"></a><span data-ttu-id="a0aa2-109">Grafico del log di controllo</span><span class="sxs-lookup"><span data-stu-id="a0aa2-109">The audit log graph</span></span>
<span data-ttu-id="a0aa2-110">È possibile usare il log di controllo per visualizzare il totale delle attivazioni, il numero massimo di attivazioni per giorno e il numero medio di attivazioni per giorno in un grafico a linee.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-110">You can use the audit log to view the total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="a0aa2-111">È anche possibile filtrare i dati per ruolo se sono presenti più ruoli nella cronologia di controlli.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-111">You can also filter the data by role if there is more than one role in the audit history.</span></span>

<span data-ttu-id="a0aa2-112">Usare i pulsanti relativi a **ora**, **azione** e **ruolo** per ordinare il log.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-112">Use the **time**, **action**, and **role** buttons to sort the log.</span></span>

## <a name="the-audit-log-list"></a><span data-ttu-id="a0aa2-113">Elenco del log di controllo</span><span class="sxs-lookup"><span data-stu-id="a0aa2-113">The audit log list</span></span>
<span data-ttu-id="a0aa2-114">Le colonne nell'elenco del log di controllo sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0aa2-114">The columns in the audit log list are:</span></span>

* <span data-ttu-id="a0aa2-115">**Richiedente** : utente che ha richiesto l'attivazione o la modifica del ruolo.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-115">**Requestor** - the user who requested the role activation or change.</span></span>  <span data-ttu-id="a0aa2-116">Se il valore è "Azure System", vedere il log di controllo di Azure per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-116">If the value is "Azure System", check the Azure audit log for more information.</span></span>
* <span data-ttu-id="a0aa2-117">**Utente** : utente che esegue l'attivazione o che è assegnato a un ruolo.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-117">**User** - the user who is activating or assigned to a role.</span></span>
* <span data-ttu-id="a0aa2-118">**Ruolo** : ruolo assegnato o attivato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-118">**Role** - the role assigned or activated by the user.</span></span>
* <span data-ttu-id="a0aa2-119">**Azione** : azioni eseguite dal richiedente.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-119">**Action** - the actions taken by the requestor.</span></span> <span data-ttu-id="a0aa2-120">Le azioni possono includere assegnazione, annullamento dell'assegnazione, attivazione o disattivazione.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="a0aa2-121">**Ora** : quando si è verificata l'azione.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-121">**Time** - when the action occurred.</span></span>
* <span data-ttu-id="a0aa2-122">**Motivo** : eventuale testo immesso nel campo del motivo durante l'attivazione.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-122">**Reasoning** - if any text was entered into the reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="a0aa2-123">**Scadenza** : rilevante solo per l'attivazione dei ruoli.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-the-audit-log"></a><span data-ttu-id="a0aa2-124">Filtrare il log di controllo</span><span class="sxs-lookup"><span data-stu-id="a0aa2-124">Filter the audit log</span></span>
<span data-ttu-id="a0aa2-125">È possibile filtrare le informazioni visualizzate nel log di controllo facendo clic sul pulsante **Filtro** .</span><span class="sxs-lookup"><span data-stu-id="a0aa2-125">You can filter the information that shows up in the audit log by clicking the **Filter** button.</span></span>  <span data-ttu-id="a0aa2-126">Verrà visualizzato il pannello **Aggiorna parametri grafico** .</span><span class="sxs-lookup"><span data-stu-id="a0aa2-126">The **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="a0aa2-127">Dopo aver impostato i filtri, fare clic su **Aggiorna** per filtrare i dati del log.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-127">After you set the filters, click **Update** to filter the data in the log.</span></span>  <span data-ttu-id="a0aa2-128">Se i dati non vengono visualizzati immediatamente, aggiornare la pagina.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-128">If the data doesn't appear right away, refresh the page.</span></span>

### <a name="change-the-date-range"></a><span data-ttu-id="a0aa2-129">Modificare l'intervallo di date</span><span class="sxs-lookup"><span data-stu-id="a0aa2-129">Change the date range</span></span>
<span data-ttu-id="a0aa2-130">Usare i pulsanti **Oggi**, **Settimana precedente**, **Mese precedente** o **Personalizzato** per modificare l'intervallo di tempo del log di controllo.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-130">Use the **Today**, **Past Week**, **Past Month**, or **Custom** buttons to change the time range of the audit log.</span></span>

<span data-ttu-id="a0aa2-131">Se si sceglie il pulsante **Personalizzato**, vengono visualizzati i campi di data **Da** e **A** per specificare un intervallo di date per il log.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-131">When you choose the **Custom** button, you will be given a **From** date field and a **To** date field to specify a range of dates for the log.</span></span>  <span data-ttu-id="a0aa2-132">È possibile immettere le date nel formato MM/GG/AAAA o fare clic sull'icona **calendario** e scegliere la data da un calendario.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-132">You can either enter the dates in MM/DD/YYYY format or click on the **calendar** icon and choose the date from a calendar.</span></span>

### <a name="change-the-roles-included-in-the-log"></a><span data-ttu-id="a0aa2-133">Modificare i ruoli inclusi nel log</span><span class="sxs-lookup"><span data-stu-id="a0aa2-133">Change the roles included in the log</span></span>
<span data-ttu-id="a0aa2-134">Selezionare o deselezionare la casella di controllo **Ruolo** accanto a ogni ruolo per includerlo o escluderlo dal log.</span><span class="sxs-lookup"><span data-stu-id="a0aa2-134">Check or uncheck the **Role** checkbox next to each role to include or exclude it from the log.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="a0aa2-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a0aa2-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

