---
title: aaaUsers contrassegnati per il report protezione rischi nel portale di Azure Active Directory hello | Documenti Microsoft
description: Informazioni sugli utenti hello contrassegnati per il report protezione rischi nel portale di Azure Active Directory hello
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="10f63-103">Utenti contrassegnati per il report protezione rischi nel portale di Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="10f63-103">Users flagged for risk security report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="10f63-104">I report di sicurezza hello in hello Azure Active Directory (Azure AD), è possibile ottenere informazioni approfondite probabilità hello di account utente compromessi nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="10f63-104">With hello security reports in hello Azure Active Directory (Azure AD), you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="10f63-105">Azure Active Directory rileva sospette azioni che sono account utente tooyour correlati.</span><span class="sxs-lookup"><span data-stu-id="10f63-105">Azure Active Directory detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="10f63-106">Per ogni azione rilevati viene creato un record denominato *evento di rischio*.</span><span class="sxs-lookup"><span data-stu-id="10f63-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="10f63-107">Per altre informazioni, vedere [Eventi di rischio di Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="10f63-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="10f63-108">Hello rilevato gli eventi di rischio sono utilizzati toocalculate:</span><span class="sxs-lookup"><span data-stu-id="10f63-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="10f63-109">**Accessi rischiosi** -un rischiosa l'accesso è un indicatore per un tentativo di accesso che siano stato eseguito da un utente che non è proprietario di legittimo hello di un account utente.</span><span class="sxs-lookup"><span data-stu-id="10f63-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="10f63-110">Per altre informazioni, vedere [Accessi a rischio](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="10f63-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="10f63-111">**Utenti contrassegnati per il rischio**. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso.</span><span class="sxs-lookup"><span data-stu-id="10f63-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="10f63-112">Per altre informazioni, vedere [Utenti contrassegnati per il rischio](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="10f63-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="10f63-113">Nel portale di Azure hello, è possibile trovare sicurezza hello segnala hello **Azure Active Directory** pannello in hello **sicurezza** sezione.</span><span class="sxs-lookup"><span data-stu-id="10f63-113">In hello Azure portal, you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span>  

![Accessi a rischio](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="10f63-115">Licenza Azure AD è necessario tooaccess un report di sicurezza?</span><span class="sxs-lookup"><span data-stu-id="10f63-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="10f63-116">Tutte le edizioni di Azure Active Directory offrono report sugli utenti contrassegnati per il rischio.</span><span class="sxs-lookup"><span data-stu-id="10f63-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="10f63-117">Tuttavia, il livello di hello di granularità dei report varia tra le edizioni di hello:</span><span class="sxs-lookup"><span data-stu-id="10f63-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="10f63-118">In hello **le edizioni di Azure Active Directory Free e Basic**, già un elenco di utenti contrassegnati i rischi.</span><span class="sxs-lookup"><span data-stu-id="10f63-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="10f63-119">Hello **Azure Active Directory Premium 1** edition estende questo modello, consentendo anche tooexamine alcune hello sottostante gli eventi di rischio che sono stati rilevati per ogni report.</span><span class="sxs-lookup"><span data-stu-id="10f63-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="10f63-120">Hello **Azure Active Directory Premium 2** edition offre informazioni più dettagliate su tutti gli eventi di rischio sottostante hello e consente di criteri di sicurezza tooconfigure rispondono automaticamente tooconfigured rischio livelli.</span><span class="sxs-lookup"><span data-stu-id="10f63-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="10f63-121">Versione gratuita e di base di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="10f63-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="10f63-122">gli utenti di Hello contrassegnati per il report di rischio nelle edizioni free e base di Azure Active Directory hello fornisce un elenco di account utente che sono stati compromessi.</span><span class="sxs-lookup"><span data-stu-id="10f63-122">hello users flagged for risk report in hello Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![Accessi a rischio](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="10f63-124">Se si seleziona un utente apre il pannello di dati utente correlato hello.</span><span class="sxs-lookup"><span data-stu-id="10f63-124">Selecting a user opens hello related user data blade.</span></span>
<span data-ttu-id="10f63-125">Per gli utenti che sono a rischio, è possibile esaminare una cronologia di accesso dell'utente di hello e reimpostare la password di hello se necessario.</span><span class="sxs-lookup"><span data-stu-id="10f63-125">For users that are at risk, you can review hello user’s sign-in history and reset hello password if necessary.</span></span>

![Accessi a rischio](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="10f63-127">Questa finestra di dialogo offre la possibilità di:</span><span class="sxs-lookup"><span data-stu-id="10f63-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="10f63-128">Scaricare report hello</span><span class="sxs-lookup"><span data-stu-id="10f63-128">Download hello report</span></span>

- <span data-ttu-id="10f63-129">Cercare gli utenti</span><span class="sxs-lookup"><span data-stu-id="10f63-129">Search users</span></span>

![Accessi a rischio](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="10f63-131">Versione Premium di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="10f63-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="10f63-132">gli utenti di Hello contrassegnati per il report di rischio nelle edizioni premium di Azure Active Directory hello offre:</span><span class="sxs-lookup"><span data-stu-id="10f63-132">hello users flagged for risk report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="10f63-133">Un [elenco di account di utenti](active-directory-identityprotection.md#users-flagged-for-risk) che potrebbero essere stati compromessi</span><span class="sxs-lookup"><span data-stu-id="10f63-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="10f63-134">Aggregare informazioni hello [tipi di eventi di rischio](active-directory-identity-protection-risk-events.md) che sono stati rilevati</span><span class="sxs-lookup"><span data-stu-id="10f63-134">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="10f63-135">Un report di hello toodownload opzione</span><span class="sxs-lookup"><span data-stu-id="10f63-135">An option toodownload hello report</span></span>

- <span data-ttu-id="10f63-136">Un'opzione tooconfigure un [criteri di monitoraggio e aggiornamento utente dei rischi](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="10f63-136">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![Accessi a rischio](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="10f63-138">Quando si seleziona un utente, si ottiene la visualizzazione di un report dettagliato per questo utente che consente di:</span><span class="sxs-lookup"><span data-stu-id="10f63-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="10f63-139">Aprire hello che visualizzare tutti gli accessi</span><span class="sxs-lookup"><span data-stu-id="10f63-139">Open hello All sign-ins view</span></span>

- <span data-ttu-id="10f63-140">Reimpostare la password dell'utente hello</span><span class="sxs-lookup"><span data-stu-id="10f63-140">Reset hello user's password</span></span>

- <span data-ttu-id="10f63-141">eliminare tutti gli eventi</span><span class="sxs-lookup"><span data-stu-id="10f63-141">Dismiss all events</span></span>

- <span data-ttu-id="10f63-142">Ricercare gli eventi di rischio segnalati per utente hello.</span><span class="sxs-lookup"><span data-stu-id="10f63-142">Investigate reported risk events for hello user.</span></span> 


![Accessi a rischio](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="10f63-144">tooinvestigate un evento di rischio, selezionarne uno dall'hello di hello elenco tooopen **dettagli** pannello per questo evento di rischio.</span><span class="sxs-lookup"><span data-stu-id="10f63-144">tooinvestigate a risk event, select one from hello list tooopen hello **Details** blade for this risk event.</span></span> <span data-ttu-id="10f63-145">In hello **dettagli** pannello è hello opzione tooeither [chiudere manualmente un evento di rischio](active-directory-identityprotection.md#closing-risk-events-manually) o riattivare un evento di rischio chiuso manualmente.</span><span class="sxs-lookup"><span data-stu-id="10f63-145">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Accessi a rischio](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="10f63-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10f63-147">Next steps</span></span>

- <span data-ttu-id="10f63-148">Per altre informazioni in merito, vedere [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="10f63-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

