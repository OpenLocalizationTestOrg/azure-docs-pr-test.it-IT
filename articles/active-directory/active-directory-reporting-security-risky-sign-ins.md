---
title: report accessi aaaRisky nel portale di Azure Active Directory hello | Documenti Microsoft
description: Informazioni su report accessi rischiosa hello nel portale di Azure Active Directory hello
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="26d7c-103">Report accessi rischiosa nel portale di Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="26d7c-103">Risky sign-ins report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="26d7c-104">I report di sicurezza hello in Azure Active Directory (Azure AD) è possibile ottenere informazioni approfondite probabilità hello di account utente compromessi nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="26d7c-104">With hello security reports in Azure Active Directory (Azure AD) you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="26d7c-105">Azure Active Directory rileva sospette azioni che sono account utente tooyour correlati.</span><span class="sxs-lookup"><span data-stu-id="26d7c-105">Azure AD detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="26d7c-106">Per ogni azione rilevati viene creato un record denominato *evento di rischio*.</span><span class="sxs-lookup"><span data-stu-id="26d7c-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="26d7c-107">Per altre informazioni, vedere [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md) (Eventi di rischio di Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="26d7c-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="26d7c-108">Hello rilevato gli eventi di rischio sono utilizzati toocalculate:</span><span class="sxs-lookup"><span data-stu-id="26d7c-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="26d7c-109">**Accessi rischiosi** -un rischiosa l'accesso è un indicatore per un tentativo di accesso che siano stato eseguito da un utente che non è proprietario di legittimo hello di un account utente.</span><span class="sxs-lookup"><span data-stu-id="26d7c-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="26d7c-110">Per informazioni dettagliate, vedere [Accessi a rischio](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="26d7c-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="26d7c-111">**Utenti contrassegnati per il rischio**. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso.</span><span class="sxs-lookup"><span data-stu-id="26d7c-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="26d7c-112">Per informazioni dettagliate, vedere [Utenti contrassegnati per il rischio](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="26d7c-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="26d7c-113">In [hello Azure portal](https://portal.azure.com), è possibile trovare sicurezza hello segnala hello **Azure Active Directory** pannello in hello **sicurezza** sezione.</span><span class="sxs-lookup"><span data-stu-id="26d7c-113">In [hello Azure portal](https://portal.azure.com), you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span> 

![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="26d7c-115">Licenza Azure AD è necessario tooaccess un report di sicurezza?</span><span class="sxs-lookup"><span data-stu-id="26d7c-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="26d7c-116">Tutte le edizioni di Azure Active Directory offrono report relativi agli accessi a rischio.</span><span class="sxs-lookup"><span data-stu-id="26d7c-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="26d7c-117">Tuttavia, il livello di hello di granularità dei report varia tra le edizioni di hello:</span><span class="sxs-lookup"><span data-stu-id="26d7c-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="26d7c-118">In hello **le edizioni di Azure Active Directory Free e Basic**, già un elenco degli accessi rischiosi.</span><span class="sxs-lookup"><span data-stu-id="26d7c-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="26d7c-119">Hello **Azure Active Directory Premium 1** edition estende questo modello, consentendo anche tooexamine alcune hello sottostante gli eventi di rischio che sono stati rilevati per ogni report.</span><span class="sxs-lookup"><span data-stu-id="26d7c-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="26d7c-120">Hello **Azure Active Directory Premium 2** edition fornisce all'hello più informazioni dettagliate su tutti gli eventi di rischio sottostante e consente inoltre di criteri di sicurezza tooconfigure rispondono automaticamente tooconfigured livelli di rischio.</span><span class="sxs-lookup"><span data-stu-id="26d7c-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="26d7c-121">Versione gratuita e di base di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26d7c-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="26d7c-122">Hello Azure Active Directory gratuita e base edizioni offrono un elenco di rischiosi accessi che sono state rilevate per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="26d7c-122">hello Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="26d7c-123">Questo report elenca quanto riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="26d7c-123">This report lists:</span></span>

- <span data-ttu-id="26d7c-124">**Utente** : hello nome dell'utente hello utilizzato durante l'operazione di accesso hello</span><span class="sxs-lookup"><span data-stu-id="26d7c-124">**User** - hello name of hello user that was used during hello sign-in operation</span></span>
- <span data-ttu-id="26d7c-125">**IP** -hello indirizzo IP del dispositivo hello che tooAzure tooconnect utilizzato Active Directory</span><span class="sxs-lookup"><span data-stu-id="26d7c-125">**IP** - hello IP address of hello device that was used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="26d7c-126">**Percorso** -percorso hello utilizzato tooconnect tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26d7c-126">**Location** - hello location used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="26d7c-127">**Ora di accesso** -hello ora quando accedi hello è stata eseguita</span><span class="sxs-lookup"><span data-stu-id="26d7c-127">**Sign-in time** - hello time when hello sign-in was performed</span></span>
- <span data-ttu-id="26d7c-128">**Stato** -hello stato Accedi hello</span><span class="sxs-lookup"><span data-stu-id="26d7c-128">**Status** - hello status of hello sign-in</span></span>


![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="26d7c-130">In base l'analisi dell'hello rischiosa sign-in, è possibile fornire commenti e suggerimenti tooAzure Active Directory sotto forma di hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="26d7c-130">Based on your investigation of hello risky sign-in, you can provide feedback tooAzure Active Directory in form of hello following actions:</span></span>

- <span data-ttu-id="26d7c-131">Risolvi</span><span class="sxs-lookup"><span data-stu-id="26d7c-131">Resolve</span></span>
- <span data-ttu-id="26d7c-132">Contrassegna come falso positivo</span><span class="sxs-lookup"><span data-stu-id="26d7c-132">Mark as false positive</span></span>
- <span data-ttu-id="26d7c-133">Ignora</span><span class="sxs-lookup"><span data-stu-id="26d7c-133">Ignore</span></span>
- <span data-ttu-id="26d7c-134">Riattiva</span><span class="sxs-lookup"><span data-stu-id="26d7c-134">Reactivate</span></span>

![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="26d7c-136">Per informazioni dettagliate, vedere [Chiusura manuale degli eventi di rischio](active-directory-identityprotection.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="26d7c-136">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="26d7c-137">Questo report offre la possibilità di:</span><span class="sxs-lookup"><span data-stu-id="26d7c-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="26d7c-138">Eseguire ricerche sulle risorse</span><span class="sxs-lookup"><span data-stu-id="26d7c-138">Searh resources</span></span>
- <span data-ttu-id="26d7c-139">Scaricare i dati del report hello</span><span class="sxs-lookup"><span data-stu-id="26d7c-139">Download hello report data</span></span>


![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="26d7c-141">Versione Premium di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26d7c-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="26d7c-142">report accessi rischiosa Hello nelle edizioni premium di Azure Active Directory hello offre:</span><span class="sxs-lookup"><span data-stu-id="26d7c-142">hello risky sign-ins report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="26d7c-143">Aggregare informazioni hello [tipi di eventi di rischio](active-directory-identity-protection-risk-events.md) che sono stati rilevati</span><span class="sxs-lookup"><span data-stu-id="26d7c-143">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="26d7c-144">Un report di hello toodownload opzione</span><span class="sxs-lookup"><span data-stu-id="26d7c-144">An option toodownload hello report</span></span>


![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="26d7c-146">Quando si seleziona un evento di rischio, si ottiene la visualizzazione di un report dettagliato per questo evento di rischio che consente di:</span><span class="sxs-lookup"><span data-stu-id="26d7c-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="26d7c-147">Un'opzione tooconfigure un [criteri di monitoraggio e aggiornamento utente dei rischi](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="26d7c-147">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="26d7c-148">Sequenza temporale di rilevamento hello di revisione per l'evento di rischio hello</span><span class="sxs-lookup"><span data-stu-id="26d7c-148">Review hello detection timeline for hello risk event</span></span>  

- <span data-ttu-id="26d7c-149">esaminare l'elenco di utenti per cui è stato rilevato l'evento di rischio</span><span class="sxs-lookup"><span data-stu-id="26d7c-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="26d7c-150">[chiudere manualmente gli eventi di rischio](active-directory-identityprotection.md#closing-risk-events-manually) o riattivare un evento di rischio chiuso manualmente.</span><span class="sxs-lookup"><span data-stu-id="26d7c-150">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="26d7c-152">Quando si seleziona un utente, si ottiene la visualizzazione di un report dettagliato per questo utente che consente di:</span><span class="sxs-lookup"><span data-stu-id="26d7c-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="26d7c-153">Aprire hello che visualizzare tutti gli accessi</span><span class="sxs-lookup"><span data-stu-id="26d7c-153">Open hello All sign-ins view</span></span>

- <span data-ttu-id="26d7c-154">Reimpostare la password dell'utente hello</span><span class="sxs-lookup"><span data-stu-id="26d7c-154">Reset hello user's password</span></span>

- <span data-ttu-id="26d7c-155">eliminare tutti gli eventi</span><span class="sxs-lookup"><span data-stu-id="26d7c-155">Dismiss all events</span></span>

- <span data-ttu-id="26d7c-156">Ricercare gli eventi di rischio segnalati per utente hello.</span><span class="sxs-lookup"><span data-stu-id="26d7c-156">Investigate reported risk events for hello user.</span></span> 


![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="26d7c-158">tooinvestigate un evento di rischio, selezionarne uno dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="26d7c-158">tooinvestigate a risk event, select one from hello list.</span></span>  
<span data-ttu-id="26d7c-159">Verrà visualizzata hello **dettagli** pannello per questo evento di rischio.</span><span class="sxs-lookup"><span data-stu-id="26d7c-159">This opens hello **Details** blade for this risk event.</span></span> <span data-ttu-id="26d7c-160">In hello **dettagli** pannello è hello opzione tooeither [chiudere manualmente un evento di rischio](active-directory-identityprotection.md#closing-risk-events-manually) o riattivare un evento di rischio chiuso manualmente.</span><span class="sxs-lookup"><span data-stu-id="26d7c-160">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="26d7c-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="26d7c-162">Next steps</span></span>

- <span data-ttu-id="26d7c-163">Per altre informazioni in merito, vedere [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="26d7c-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

