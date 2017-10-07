---
title: "Funzionalità in anteprima di Azure AD Connect | Documentazione Microsoft"
description: "Questo argomento descrive in maggiore dettaglio le funzionalità in anteprima di Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="f257e-103">Altre informazioni sulle funzionalità in anteprima</span><span class="sxs-lookup"><span data-stu-id="f257e-103">More details about features in preview</span></span>
<span data-ttu-id="f257e-104">In questo argomento viene descritto come toouse funzionalità attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="f257e-104">This topic describes how toouse features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="f257e-105">Writeback dei gruppi</span><span class="sxs-lookup"><span data-stu-id="f257e-105">Group writeback</span></span>
<span data-ttu-id="f257e-106">opzione Hello per writeback dei gruppi di funzionalità facoltative consente toowriteback **gruppi di Office 365** tooa foresta con Exchange installato.</span><span class="sxs-lookup"><span data-stu-id="f257e-106">hello option for group writeback in optional features allows you toowriteback **Office 365 Groups** tooa forest with Exchange installed.</span></span> <span data-ttu-id="f257e-107">Si tratta di un gruppo che è sempre gestito nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="f257e-107">This is a group that is always mastered in hello cloud.</span></span> <span data-ttu-id="f257e-108">Se si dispone di Exchange locale, quindi è possibile scrivere nuovamente locale tooon questi gruppi in modo da inviare e ricevere messaggi di posta elettronica da questi gruppi di utenti con una cassetta postale di Exchange locale.</span><span class="sxs-lookup"><span data-stu-id="f257e-108">If you have Exchange on-premises, then you can write back these groups tooon-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="f257e-109">Ulteriori informazioni sui gruppi di Office 365 e come toouse li può essere trovati [qui](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="f257e-109">More information about Office 365 Groups and how toouse them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="f257e-110">Un gruppo di Office 365 viene rappresentato come gruppo di distribuzione in AD DS locale.</span><span class="sxs-lookup"><span data-stu-id="f257e-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="f257e-111">Exchange server locale deve trovarsi in Exchange 2013 aggiornamento cumulativo 8 (rilasciato nel marzo 2015) o Exchange 2016 toorecognize questo nuovo tipo di gruppo.</span><span class="sxs-lookup"><span data-stu-id="f257e-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 toorecognize this new group type.</span></span>

<span data-ttu-id="f257e-112">**Note durante l'anteprima di hello**</span><span class="sxs-lookup"><span data-stu-id="f257e-112">**Notes during hello preview**</span></span>

* <span data-ttu-id="f257e-113">attributo di Hello address book attualmente non viene popolata in anteprima hello.</span><span class="sxs-lookup"><span data-stu-id="f257e-113">hello address book attribute is currently not populated in hello preview.</span></span> <span data-ttu-id="f257e-114">Senza questo attributo, il gruppo di hello non è visibile nell'elenco indirizzi globale hello.</span><span class="sxs-lookup"><span data-stu-id="f257e-114">Without this attribute, hello group is not visible in hello GAL.</span></span> <span data-ttu-id="f257e-115">Hello toopopulate modo più semplice l'attributo è di cmdlet di Exchange PowerShell hello toouse `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="f257e-115">hello easiest way toopopulate this attribute is toouse hello Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="f257e-116">Solo le foreste con uno schema di Exchange hello sono destinazioni valide per i gruppi.</span><span class="sxs-lookup"><span data-stu-id="f257e-116">Only forests with hello Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="f257e-117">Se è stato rilevato alcun Exchange, quindi writeback dei gruppi non è possibile tooenable.</span><span class="sxs-lookup"><span data-stu-id="f257e-117">If no Exchange was detected, then group writeback is not possible tooenable.</span></span>
* <span data-ttu-id="f257e-118">Attualmente sono supportate solo le distribuzioni in organizzazioni di Exchange a foresta singola.</span><span class="sxs-lookup"><span data-stu-id="f257e-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="f257e-119">Se si dispone di più di Exchange dell'organizzazione locale, è necessario una soluzione GALSync locale per questi gruppi tooappear le altre foreste.</span><span class="sxs-lookup"><span data-stu-id="f257e-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups tooappear in your other forests.</span></span>
* <span data-ttu-id="f257e-120">funzionalità di writeback gruppo Hello non gestisce i gruppi di protezione o gruppi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f257e-120">hello Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="f257e-121">TooAzure una sottoscrizione AD Premium è necessario per il writeback di gruppo.</span><span class="sxs-lookup"><span data-stu-id="f257e-121">A subscription tooAzure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="f257e-122">Writeback degli utenti</span><span class="sxs-lookup"><span data-stu-id="f257e-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f257e-123">Hello writeback anteprima funzionalità utente è stata rimossa in tooAzure di aggiornamento di agosto 2015 hello AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f257e-123">hello user writeback preview feature was removed in hello August 2015 update tooAzure AD Connect.</span></span> <span data-ttu-id="f257e-124">Se questa funzionalità è stata abilitata, è necessario disabilitarla.</span><span class="sxs-lookup"><span data-stu-id="f257e-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="f257e-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f257e-125">Next steps</span></span>
<span data-ttu-id="f257e-126">Continuare l'[Installazione personalizzata di Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="f257e-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="f257e-127">Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="f257e-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
