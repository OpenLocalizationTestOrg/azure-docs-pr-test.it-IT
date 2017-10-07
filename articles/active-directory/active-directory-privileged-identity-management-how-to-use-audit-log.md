---
title: log di controllo di aaaHow toouse hello in Azure AD Privileged Identity Management | Documenti Microsoft
description: Informazioni su come di log di controllo di hello toouse nell'estensione di hello Azure Privileged Identity Management.
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
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a><span data-ttu-id="d6f48-103">Utilizzo di log di controllo hello in PIM</span><span class="sxs-lookup"><span data-stu-id="d6f48-103">Using hello audit log in PIM</span></span>
<span data-ttu-id="d6f48-104">È possibile utilizzare tutte le assegnazioni utente hello e attivazioni hello Privileged Identity Management (PIM) audit log toosee all'interno di un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="d6f48-104">You can use hello Privileged Identity Management (PIM) audit log toosee all hello user assignments and activations within a given time period.</span></span> <span data-ttu-id="d6f48-105">Se si desidera cronologia di controllo completo hello toosee dell'attività nel tenant, tra cui l'amministratore, l'utente finale e attività di sincronizzazione, è possibile utilizzare hello [report di utilizzo e di accesso di Azure Active Directory.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="d6f48-105">If you want toosee hello full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use hello [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-toohello-audit-log"></a><span data-ttu-id="d6f48-106">Passare il log di controllo toohello</span><span class="sxs-lookup"><span data-stu-id="d6f48-106">Navigate toohello audit log</span></span>
<span data-ttu-id="d6f48-107">Da hello [portale di Azure](https://portal.azure.com) dashboard, seleziona hello **Azure AD Privileged Identity Management** app.</span><span class="sxs-lookup"><span data-stu-id="d6f48-107">From hello [Azure portal](https://portal.azure.com) dashboard, select hello **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="d6f48-108">Da qui, accedere ai log di controllo hello facendo clic **gestire i ruoli con privilegi** > **cronologia controlli** nel dashboard PIM hello.</span><span class="sxs-lookup"><span data-stu-id="d6f48-108">From there, access hello audit log by clicking **Manage privileged roles** > **Audit history** in hello PIM dashboard.</span></span>

## <a name="hello-audit-log-graph"></a><span data-ttu-id="d6f48-109">grafico di log di controllo Hello</span><span class="sxs-lookup"><span data-stu-id="d6f48-109">hello audit log graph</span></span>
<span data-ttu-id="d6f48-110">È possibile utilizzare attivazioni totali di hello audit log tooview hello attivazioni max al giorno e attivazioni medie al giorno in un grafico a linee.</span><span class="sxs-lookup"><span data-stu-id="d6f48-110">You can use hello audit log tooview hello total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="d6f48-111">È anche possibile filtrare i dati hello dal ruolo se è presente più di un ruolo nella cronologia di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="d6f48-111">You can also filter hello data by role if there is more than one role in hello audit history.</span></span>

<span data-ttu-id="d6f48-112">Hello utilizzare **ora**, **azione**, e **ruolo** pulsanti toosort hello log.</span><span class="sxs-lookup"><span data-stu-id="d6f48-112">Use hello **time**, **action**, and **role** buttons toosort hello log.</span></span>

## <a name="hello-audit-log-list"></a><span data-ttu-id="d6f48-113">elenco di log di controllo Hello</span><span class="sxs-lookup"><span data-stu-id="d6f48-113">hello audit log list</span></span>
<span data-ttu-id="d6f48-114">Hello colonne nell'elenco di log di controllo hello sono:</span><span class="sxs-lookup"><span data-stu-id="d6f48-114">hello columns in hello audit log list are:</span></span>

* <span data-ttu-id="d6f48-115">**Richiedente** -utente hello che ha richiesto l'attivazione del ruolo hello o modifica.</span><span class="sxs-lookup"><span data-stu-id="d6f48-115">**Requestor** - hello user who requested hello role activation or change.</span></span>  <span data-ttu-id="d6f48-116">Se il valore di hello è di tipo "Sistema Azure", vedere il log di controllo di Azure di hello per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="d6f48-116">If hello value is "Azure System", check hello Azure audit log for more information.</span></span>
* <span data-ttu-id="d6f48-117">**Utente** -utente hello in fase di attivazione o tooa ruolo.</span><span class="sxs-lookup"><span data-stu-id="d6f48-117">**User** - hello user who is activating or assigned tooa role.</span></span>
* <span data-ttu-id="d6f48-118">**Ruolo** -ruolo hello assegnato o attivato dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="d6f48-118">**Role** - hello role assigned or activated by hello user.</span></span>
* <span data-ttu-id="d6f48-119">**Azione** - azioni hello dal richiedente hello.</span><span class="sxs-lookup"><span data-stu-id="d6f48-119">**Action** - hello actions taken by hello requestor.</span></span> <span data-ttu-id="d6f48-120">Le azioni possono includere assegnazione, annullamento dell'assegnazione, attivazione o disattivazione.</span><span class="sxs-lookup"><span data-stu-id="d6f48-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="d6f48-121">**Tempo** : quando si è verificata hello azione.</span><span class="sxs-lookup"><span data-stu-id="d6f48-121">**Time** - when hello action occurred.</span></span>
* <span data-ttu-id="d6f48-122">**Ragionamento** -se il testo è stato immesso nel campo motivo hello durante l'attivazione, verrà visualizzato.</span><span class="sxs-lookup"><span data-stu-id="d6f48-122">**Reasoning** - if any text was entered into hello reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="d6f48-123">**Scadenza** : rilevante solo per l'attivazione dei ruoli.</span><span class="sxs-lookup"><span data-stu-id="d6f48-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-hello-audit-log"></a><span data-ttu-id="d6f48-124">Log di controllo di filtro hello</span><span class="sxs-lookup"><span data-stu-id="d6f48-124">Filter hello audit log</span></span>
<span data-ttu-id="d6f48-125">È possibile filtrare le informazioni di hello che viene visualizzato nel log di controllo hello facendo hello **filtro** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d6f48-125">You can filter hello information that shows up in hello audit log by clicking hello **Filter** button.</span></span>  <span data-ttu-id="d6f48-126">Hello **blade di parametri di aggiornamento grafico** verranno visualizzati.</span><span class="sxs-lookup"><span data-stu-id="d6f48-126">hello **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="d6f48-127">Dopo aver impostato i filtri di hello, fare clic su **aggiornamento** dati hello toofilter nel registro hello.</span><span class="sxs-lookup"><span data-stu-id="d6f48-127">After you set hello filters, click **Update** toofilter hello data in hello log.</span></span>  <span data-ttu-id="d6f48-128">Se non viene visualizzato immediatamente dati hello, aggiornare la pagina hello.</span><span class="sxs-lookup"><span data-stu-id="d6f48-128">If hello data doesn't appear right away, refresh hello page.</span></span>

### <a name="change-hello-date-range"></a><span data-ttu-id="d6f48-129">Modificare l'intervallo di date hello</span><span class="sxs-lookup"><span data-stu-id="d6f48-129">Change hello date range</span></span>
<span data-ttu-id="d6f48-130">Hello utilizzare **oggi**, **settimana precedente**, **mese scorso**, o **personalizzato** i pulsanti di intervallo di tempo toochange hello del log di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="d6f48-130">Use hello **Today**, **Past Week**, **Past Month**, or **Custom** buttons toochange hello time range of hello audit log.</span></span>

<span data-ttu-id="d6f48-131">Quando si sceglie di hello **personalizzato** pulsante, verrà assegnato un **da** campo Data e un **a** data toospecify campo un intervallo di date per il log di hello.</span><span class="sxs-lookup"><span data-stu-id="d6f48-131">When you choose hello **Custom** button, you will be given a **From** date field and a **To** date field toospecify a range of dates for hello log.</span></span>  <span data-ttu-id="d6f48-132">È possibile immettere date hello in formato MM/gg/aaaa o fare clic su hello **calendario** icona e scegliere Data hello da un calendario.</span><span class="sxs-lookup"><span data-stu-id="d6f48-132">You can either enter hello dates in MM/DD/YYYY format or click on hello **calendar** icon and choose hello date from a calendar.</span></span>

### <a name="change-hello-roles-included-in-hello-log"></a><span data-ttu-id="d6f48-133">Modificare i ruoli di hello inclusi nel registro hello</span><span class="sxs-lookup"><span data-stu-id="d6f48-133">Change hello roles included in hello log</span></span>
<span data-ttu-id="d6f48-134">Selezionare o deselezionare hello **ruolo** casella di controllo successivo tooeach ruolo tooinclude o escludere dalla hello del log.</span><span class="sxs-lookup"><span data-stu-id="d6f48-134">Check or uncheck hello **Role** checkbox next tooeach role tooinclude or exclude it from hello log.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="d6f48-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d6f48-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

