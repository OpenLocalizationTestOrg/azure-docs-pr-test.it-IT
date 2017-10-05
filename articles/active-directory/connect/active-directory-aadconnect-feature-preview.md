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
ms.openlocfilehash: cbf8f729d0ebfb271bb0d8702ac043442b42c262
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="bba4c-103">Altre informazioni sulle funzionalità in anteprima</span><span class="sxs-lookup"><span data-stu-id="bba4c-103">More details about features in preview</span></span>
<span data-ttu-id="bba4c-104">Questo argomento descrive come usare le funzionalità attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="bba4c-104">This topic describes how to use features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="bba4c-105">Writeback dei gruppi</span><span class="sxs-lookup"><span data-stu-id="bba4c-105">Group writeback</span></span>
<span data-ttu-id="bba4c-106">L'opzione per il writeback dei gruppi nelle funzionalità facoltative consente il writeback dei **gruppi di Office 365** in una foresta in cui è installato Exchange.</span><span class="sxs-lookup"><span data-stu-id="bba4c-106">The option for group writeback in optional features allows you to writeback **Office 365 Groups** to a forest with Exchange installed.</span></span> <span data-ttu-id="bba4c-107">Si tratta di un gruppo che viene sempre gestito nel cloud.</span><span class="sxs-lookup"><span data-stu-id="bba4c-107">This is a group that is always mastered in the cloud.</span></span> <span data-ttu-id="bba4c-108">Se Exchange è disponibile in locale, è possibile eseguire il writeback di questi gruppi in locale in modo che gli utenti con una cassetta postale di Exchange locale possano inviare e ricevere messaggi di posta elettronica da questi gruppi.</span><span class="sxs-lookup"><span data-stu-id="bba4c-108">If you have Exchange on-premises, then you can write back these groups to on-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="bba4c-109">Altre informazioni sui gruppi di Office 365 e su come usarli sono disponibili [qui](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="bba4c-109">More information about Office 365 Groups and how to use them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="bba4c-110">Un gruppo di Office 365 viene rappresentato come gruppo di distribuzione in AD DS locale.</span><span class="sxs-lookup"><span data-stu-id="bba4c-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="bba4c-111">Per riconoscere questo nuovo tipo di gruppo, nel server di Exchange locale deve essere installato l'aggiornamento cumulativo 8 di Exchange 2013 (rilasciato a marzo 2015) o Exchange 2016.</span><span class="sxs-lookup"><span data-stu-id="bba4c-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 to recognize this new group type.</span></span>

<span data-ttu-id="bba4c-112">**Note durante l'anteprima**</span><span class="sxs-lookup"><span data-stu-id="bba4c-112">**Notes during the preview**</span></span>

* <span data-ttu-id="bba4c-113">Attualmente l'attributo della rubrica non è popolato nell'anteprima.</span><span class="sxs-lookup"><span data-stu-id="bba4c-113">The address book attribute is currently not populated in the preview.</span></span> <span data-ttu-id="bba4c-114">Senza questo attributo, il gruppo non è visibile nell'elenco indirizzi globale.</span><span class="sxs-lookup"><span data-stu-id="bba4c-114">Without this attribute, the group is not visible in the GAL.</span></span> <span data-ttu-id="bba4c-115">Il modo più semplice per popolare questo attributo consiste nell'usare il cmdlet di PowerShell per Exchange `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="bba4c-115">The easiest way to populate this attribute is to use the Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="bba4c-116">Solo le foreste con lo schema di Exchange sono destinazioni valide per i gruppi.</span><span class="sxs-lookup"><span data-stu-id="bba4c-116">Only forests with the Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="bba4c-117">Se non è stata rilevata alcuna versione di Exchange, il writeback dei gruppi non può essere abilitato.</span><span class="sxs-lookup"><span data-stu-id="bba4c-117">If no Exchange was detected, then group writeback is not possible to enable.</span></span>
* <span data-ttu-id="bba4c-118">Attualmente sono supportate solo le distribuzioni in organizzazioni di Exchange a foresta singola.</span><span class="sxs-lookup"><span data-stu-id="bba4c-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="bba4c-119">Se sono presenti più organizzazioni di Exchange locali, è necessaria una soluzione GALSync locale per visualizzare questi gruppi nelle altre foreste.</span><span class="sxs-lookup"><span data-stu-id="bba4c-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups to appear in your other forests.</span></span>
* <span data-ttu-id="bba4c-120">La funzionalità di writeback dei gruppi non gestisce gruppi di protezione o gruppi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="bba4c-120">The Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="bba4c-121">Per il writeback dei gruppi è necessaria una sottoscrizione di Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="bba4c-121">A subscription to Azure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="bba4c-122">Writeback degli utenti</span><span class="sxs-lookup"><span data-stu-id="bba4c-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bba4c-123">La funzionalità di anteprima di writeback degli utenti è stata rimossa nell'aggiornamento di agosto 2015 di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="bba4c-123">The user writeback preview feature was removed in the August 2015 update to Azure AD Connect.</span></span> <span data-ttu-id="bba4c-124">Se questa funzionalità è stata abilitata, è necessario disabilitarla.</span><span class="sxs-lookup"><span data-stu-id="bba4c-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="bba4c-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bba4c-125">Next steps</span></span>
<span data-ttu-id="bba4c-126">Continuare l'[Installazione personalizzata di Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="bba4c-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="bba4c-127">Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="bba4c-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
