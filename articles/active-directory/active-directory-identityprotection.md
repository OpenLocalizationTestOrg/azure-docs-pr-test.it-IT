---
title: "la protezione dell'identità di Active Directory aaaAzure | Documenti Microsoft"
description: "Informazioni su come Azure AD Identity Protection consenta il possibilità hello toolimit di un tooexploit malintenzionato un'identità compromessa o il dispositivo e toosecure un'identità o un dispositivo che in precedenza era noto o sospetta toobe compromesso."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestione applicazioni, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="5fc39-104">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5fc39-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="5fc39-105">Azure Active Directory Identity Protection è una funzionalità dell'edizione di Azure AD Premium P2 hello che consente di:</span><span class="sxs-lookup"><span data-stu-id="5fc39-105">Azure Active Directory Identity Protection is a feature of hello Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="5fc39-106">Rilevare le potenziali vulnerabilità per le identità dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="5fc39-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="5fc39-107">Configurare le risposte automatiche toodetected sospette azioni sono le identità dell'organizzazione tooyour correlati</span><span class="sxs-lookup"><span data-stu-id="5fc39-107">Configure automated responses toodetected suspicious actions that are related tooyour organization’s identities</span></span>  

- <span data-ttu-id="5fc39-108">Esaminare gli eventi imprevisti sospetti e richiedere l'azione appropriata tooresolve li</span><span class="sxs-lookup"><span data-stu-id="5fc39-108">Investigate suspicious incidents and take appropriate action tooresolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="5fc39-109">introduttiva</span><span class="sxs-lookup"><span data-stu-id="5fc39-109">Getting started</span></span>

<span data-ttu-id="5fc39-110">Microsoft protegge le identità basate sul cloud per oltre un decennio.</span><span class="sxs-lookup"><span data-stu-id="5fc39-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="5fc39-111">Protezione dell'identità di Azure Active Directory, nel proprio ambiente, è possibile utilizzare hello stessi sistemi di protezione Microsoft utilizza le identità toosecure.</span><span class="sxs-lookup"><span data-stu-id="5fc39-111">With Azure Active Directory Identity Protection, in your environment, you can use hello same protection systems Microsoft uses toosecure identities.</span></span>

<span data-ttu-id="5fc39-112">Posizionare Hello gran parte richiedere violazioni della sicurezza degli utenti malintenzionati ad ambiente tooan accesso dal furto di identità dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5fc39-112">hello vast majority of security breaches take place when attackers gain access tooan environment by stealing a user’s identity.</span></span> <span data-ttu-id="5fc39-113">Negli anni hello, gli utenti malintenzionati sono diventate sempre più efficaci per sfruttare violazioni della sicurezza di terze parti e l'utilizzo di attacchi di phishing sofisticate.</span><span class="sxs-lookup"><span data-stu-id="5fc39-113">Over hello years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="5fc39-114">Non appena un utente malintenzionato ottenga l'accesso degli account utente con privilegi limitati tooeven, è relativamente facile relativa toogain accedere tooimportant alle risorse aziendali tramite il movimento laterale.</span><span class="sxs-lookup"><span data-stu-id="5fc39-114">As soon as an attacker gains access tooeven low privileged user accounts, it is relatively easy for them toogain access tooimportant company resources through lateral movement.</span></span>

<span data-ttu-id="5fc39-115">Di conseguenza, è necessario:</span><span class="sxs-lookup"><span data-stu-id="5fc39-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="5fc39-116">Proteggere tutte le identità indipendentemente dal livello di privilegi</span><span class="sxs-lookup"><span data-stu-id="5fc39-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="5fc39-117">Impedire in modo proattivo l'uso improprio delle identità compromesse</span><span class="sxs-lookup"><span data-stu-id="5fc39-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="5fc39-118">Trovare le identità compromesse non è un compito facile.</span><span class="sxs-lookup"><span data-stu-id="5fc39-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="5fc39-119">Azure Active Directory Usa algoritmi di apprendimento automatico adattivo e anomalie toodetect euristica e gli eventi imprevisti sospetti indicano potenzialmente compromessi identità.</span><span class="sxs-lookup"><span data-stu-id="5fc39-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="5fc39-120">Con questi dati, la protezione dell'identità genera report e gli avvisi che consentono di tooevaluate hello ha rilevato dei problemi e richiedere di attenuazione appropriati o azioni correttive.</span><span class="sxs-lookup"><span data-stu-id="5fc39-120">Using this data, Identity Protection generates reports and alerts that enable you tooevaluate hello detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="5fc39-121">Azure Active Directory Identity Protection è ben più di un semplice strumento di monitoraggio e reporting.</span><span class="sxs-lookup"><span data-stu-id="5fc39-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="5fc39-122">tooprotect identità dell'organizzazione, è possibile configurare criteri basati sui rischi di rispondere automaticamente toodetected problemi quando viene raggiunto un livello di rischio specificato.</span><span class="sxs-lookup"><span data-stu-id="5fc39-122">tooprotect your organization's identities, you can configure risk-based policies that automatically respond toodetected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="5fc39-123">Questi criteri, inoltre tooother condizionale accedere ai controlli forniti da Azure Active Directory ed EMS, può bloccare automaticamente oppure avviare azioni di correzione adattivo inclusi la reimpostazione della password e l'applicazione multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="5fc39-123">These policies, in addition tooother conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="5fc39-124">Funzionalità di Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5fc39-124">Identity Protection capabilities</span></span>

<span data-ttu-id="5fc39-125">**Rilevamento di vulnerabilità e di account rischiosi:**</span><span class="sxs-lookup"><span data-stu-id="5fc39-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="5fc39-126">Fornire consigli personalizzati tooimprove generali di sicurezza, evidenziando le vulnerabilità</span><span class="sxs-lookup"><span data-stu-id="5fc39-126">Providing custom recommendations tooimprove overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="5fc39-127">Calcolo dei livelli di rischio di accesso.</span><span class="sxs-lookup"><span data-stu-id="5fc39-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="5fc39-128">Calcolo dei livelli di rischio utente.</span><span class="sxs-lookup"><span data-stu-id="5fc39-128">Calculating user risk levels</span></span>


<span data-ttu-id="5fc39-129">**Analisi degli eventi di rischio:**</span><span class="sxs-lookup"><span data-stu-id="5fc39-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="5fc39-130">Invio di notifiche per gli eventi di rischio.</span><span class="sxs-lookup"><span data-stu-id="5fc39-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="5fc39-131">Analisi degli eventi di rischio con informazioni rilevanti e contestuali.</span><span class="sxs-lookup"><span data-stu-id="5fc39-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="5fc39-132">Fornisce i flussi di lavoro di base indagini tootrack</span><span class="sxs-lookup"><span data-stu-id="5fc39-132">Providing basic workflows tootrack investigations</span></span>
* <span data-ttu-id="5fc39-133">Fornendo un accesso semplice tooremediation azioni, ad esempio la reimpostazione della password</span><span class="sxs-lookup"><span data-stu-id="5fc39-133">Providing easy access tooremediation actions such as password reset</span></span>

<span data-ttu-id="5fc39-134">**Criteri di accesso condizionale basati sul rischio:**</span><span class="sxs-lookup"><span data-stu-id="5fc39-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="5fc39-135">Criteri toomitigate rischiosi accessi da accessi di blocco o la richiesta di richieste di autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="5fc39-135">Policy toomitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="5fc39-136">Criteri tooblock o gli account utente di rischiosa sicura</span><span class="sxs-lookup"><span data-stu-id="5fc39-136">Policy tooblock or secure risky user accounts</span></span>
* <span data-ttu-id="5fc39-137">Criteri toorequire utenti tooregister multi-factor Authentication</span><span class="sxs-lookup"><span data-stu-id="5fc39-137">Policy toorequire users tooregister for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="5fc39-138">Ruoli di Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5fc39-138">Identity Protection roles</span></span>

<span data-ttu-id="5fc39-139">tooload saldo hello Gestione attività per l'implementazione di Identity Protection, è possibile assegnare più ruoli.</span><span class="sxs-lookup"><span data-stu-id="5fc39-139">tooload balance hello management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="5fc39-140">Azure AD Identity Protection supporta 3 ruoli di directory:</span><span class="sxs-lookup"><span data-stu-id="5fc39-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="5fc39-141">Ruolo</span><span class="sxs-lookup"><span data-stu-id="5fc39-141">Role</span></span>                         | <span data-ttu-id="5fc39-142">Operazione consentita</span><span class="sxs-lookup"><span data-stu-id="5fc39-142">Can do</span></span>                          | <span data-ttu-id="5fc39-143">Operazione non consentita</span><span class="sxs-lookup"><span data-stu-id="5fc39-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="5fc39-144">Amministratore globale</span><span class="sxs-lookup"><span data-stu-id="5fc39-144">Global administrator</span></span>         | <span data-ttu-id="5fc39-145">Accesso completo tooIdentity, protezione, caricare Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5fc39-145">Full access tooIdentity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="5fc39-146">Amministratore della sicurezza</span><span class="sxs-lookup"><span data-stu-id="5fc39-146">Security administrator</span></span>       | <span data-ttu-id="5fc39-147">Accesso completo tooIdentity protezione</span><span class="sxs-lookup"><span data-stu-id="5fc39-147">Full access tooIdentity Protection</span></span> | <span data-ttu-id="5fc39-148">Implementazione di Identity Protection, reimpostazione delle password per un utente</span><span class="sxs-lookup"><span data-stu-id="5fc39-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="5fc39-149">Ruolo con autorizzazioni di lettura per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="5fc39-149">Security reader</span></span>              | <span data-ttu-id="5fc39-150">Accesso in sola lettura tooIdentity protezione</span><span class="sxs-lookup"><span data-stu-id="5fc39-150">Ready-only access tooIdentity Protection</span></span> | <span data-ttu-id="5fc39-151">Implementazione di Identity Protection, correzione degli utenti, configurazione dei criteri, reimpostazione delle password</span><span class="sxs-lookup"><span data-stu-id="5fc39-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="5fc39-152">Per altri dettagli, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5fc39-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="5fc39-153">Rilevamento</span><span class="sxs-lookup"><span data-stu-id="5fc39-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="5fc39-154">Vulnerabilità</span><span class="sxs-lookup"><span data-stu-id="5fc39-154">Vulnerabilities</span></span>

<span data-ttu-id="5fc39-155">Azure Active Directory Identity Protection analizza la configurazione e rileva le vulnerabilità che possono avere effetto sulle identità dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5fc39-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="5fc39-156">Per altri dettagli, vedere [Vulnerabilità rilevate da Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="5fc39-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="5fc39-157">Eventi di rischio</span><span class="sxs-lookup"><span data-stu-id="5fc39-157">Risk events</span></span>

<span data-ttu-id="5fc39-158">Azure Active Directory Usa adattivo di machine learning algoritmi euristica toodetect sospette azioni e che sono le identità dell'utente tooyour correlati.</span><span class="sxs-lookup"><span data-stu-id="5fc39-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user's identities.</span></span> <span data-ttu-id="5fc39-159">sistema di Hello crea un record per ogni azione sospetti rilevato.</span><span class="sxs-lookup"><span data-stu-id="5fc39-159">hello system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="5fc39-160">Questi record sono denominati anche eventi di rischio.</span><span class="sxs-lookup"><span data-stu-id="5fc39-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="5fc39-161">Per altre informazioni, vedere [Eventi di rischio di Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="5fc39-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="5fc39-162">Analisi</span><span class="sxs-lookup"><span data-stu-id="5fc39-162">Investigation</span></span>
<span data-ttu-id="5fc39-163">Il trasporto tramite la protezione dell'identità in genere inizia con dashboard Identity Protection hello.</span><span class="sxs-lookup"><span data-stu-id="5fc39-163">Your journey through Identity Protection typically starts with hello Identity Protection dashboard.</span></span>

<span data-ttu-id="5fc39-164">![Correzione](./media/active-directory-identityprotection/1000.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="5fc39-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="5fc39-165">dashboard Hello consente di accedere a:</span><span class="sxs-lookup"><span data-stu-id="5fc39-165">hello dashboard gives you access to:</span></span>

* <span data-ttu-id="5fc39-166">Report, ad esempio **Utenti contrassegnati per il rischio**, **Eventi di rischio** e **Vulnerabilità**</span><span class="sxs-lookup"><span data-stu-id="5fc39-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="5fc39-167">Le impostazioni come configurazione hello del **criteri di sicurezza**, **notifiche** e **registrazione con l'autenticazione a più fattori**</span><span class="sxs-lookup"><span data-stu-id="5fc39-167">Settings such as hello configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="5fc39-168">In genere è il punto di partenza per l'analisi, ovvero il processo di hello di revisione hello attività, i registri e altre informazioni rilevanti tooa correlato rischio toodecide evento se sono necessarie operazioni di correzione o riduzione, e come è stato identità hello compromesso e comprendere come hello compromesso identità è stata utilizzata.</span><span class="sxs-lookup"><span data-stu-id="5fc39-168">It is typically your starting point for investigation, which is hello process of reviewing hello activities, logs, and other relevant information related tooa risk event toodecide whether remediation or mitigation steps are necessary,  and how hello identity was compromised, and understand how hello compromised identity was used.</span></span>

<span data-ttu-id="5fc39-169">È possibile collegare il toohello le attività di analisi [notifiche](active-directory-identityprotection-notifications.md) protezione di Azure Active Directory invia per posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="5fc39-169">You can tie your investigation activities toohello [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="5fc39-170">Hello nelle sezioni seguenti offrono altre informazioni e i passaggi di hello analisi tooan correlati.</span><span class="sxs-lookup"><span data-stu-id="5fc39-170">hello following sections provide you with more details and hello steps that are related tooan investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="5fc39-171">Accessi a rischio</span><span class="sxs-lookup"><span data-stu-id="5fc39-171">Risky sign-ins</span></span>

<span data-ttu-id="5fc39-172">Azure Active Directory rileva i [tipi di eventi di rischio](active-directory-reporting-risk-events.md#risk-event-types) in tempo reale e offline.</span><span class="sxs-lookup"><span data-stu-id="5fc39-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="5fc39-173">Ogni evento di rischio rilevati per un accesso di un utente contribuisce tooa concetto logico Accedi rischiosa.</span><span class="sxs-lookup"><span data-stu-id="5fc39-173">Each risk event that has been detected for a sign-in of a user contributes tooa logical concept called risky sign-in.</span></span> <span data-ttu-id="5fc39-174">Un rischiosa Accedi sono un indicatore per un tentativo di accesso che è possibile che non siano eseguito dal legittimo proprietario di hello di un account utente.</span><span class="sxs-lookup"><span data-stu-id="5fc39-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by hello legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="5fc39-175">Livello di rischio di un accesso</span><span class="sxs-lookup"><span data-stu-id="5fc39-175">Sign-in risk level</span></span>

<span data-ttu-id="5fc39-176">Un livello di rischio di accesso è un'indicazione (alta, Media o bassa) di probabilità hello che un tentativo di accesso non è stato eseguito dal legittimo proprietario di hello di un account utente.</span><span class="sxs-lookup"><span data-stu-id="5fc39-176">A sign-in risk level is an indication (High, Medium, or Low) of hello likelihood that a sign-in attempt was not performed by hello legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="5fc39-177">Mitigazione degli eventi di rischio di accesso</span><span class="sxs-lookup"><span data-stu-id="5fc39-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="5fc39-178">Una riduzione dei rischi è la capacità di hello toolimit azione di un utente malintenzionato tooexploit un'identità compromessa o un dispositivo senza ripristino hello identità o un dispositivo tooa sicuri dello stato.</span><span class="sxs-lookup"><span data-stu-id="5fc39-178">A mitigation is an action toolimit hello ability of an attacker tooexploit a compromised identity or device without restoring hello identity or device tooa safe state.</span></span> <span data-ttu-id="5fc39-179">Una mitigazione non viene risolto precedente Accedi rischio gli eventi associati identità hello o un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5fc39-179">A mitigation does not resolve previous sign-in risk events associated with hello identity or device.</span></span>

<span data-ttu-id="5fc39-180">accessi toomitigate, rischiosa automaticamente, è possibile configurare l'accesso rischio sicurezza policicies.</span><span class="sxs-lookup"><span data-stu-id="5fc39-180">toomitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="5fc39-181">Grazie a questi criteri, prendere in considerazione il livello di rischio hello dell'utente di hello o hello Accedi tooblock accessi rischiosi o richiedere hello utente tooperform multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="5fc39-181">Using these policies, you consider hello risk level of hello user or hello sign-in tooblock risky sign-ins or require hello user tooperform multi-factor authentication.</span></span> <span data-ttu-id="5fc39-182">Queste azioni possono impedire a un utente malintenzionato di sfruttare un danno toocause furto di identità e possono generare un'identità di hello toosecure ora.</span><span class="sxs-lookup"><span data-stu-id="5fc39-182">These actions may prevent an attacker from exploiting a stolen identity toocause damage, and may give you some time toosecure hello identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="5fc39-183">Criteri di sicurezza per il rischio di accesso</span><span class="sxs-lookup"><span data-stu-id="5fc39-183">Sign-in risk security policy</span></span>
<span data-ttu-id="5fc39-184">Un criterio di accesso rischi è un criterio di accesso condizionale che valuta hello rischio tooa specifico Accedi e applica le misure di attenuazione in base alle regole e condizioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="5fc39-184">A sign-in risk policy is a conditional access policy that evaluates hello risk tooa specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="5fc39-185">![Criteri di rischio di accesso](./media/active-directory-identityprotection/1014.png "Criteri di rischio di accesso")</span><span class="sxs-lookup"><span data-stu-id="5fc39-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="5fc39-186">Azure AD Identity Protection consente di gestire attenuazione hello di accessi rischiosi poiché consente di:</span><span class="sxs-lookup"><span data-stu-id="5fc39-186">Azure AD Identity Protection helps you manage hello mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="5fc39-187">Hello utenti e gruppi hello criterio di impostazione si applica a:</span><span class="sxs-lookup"><span data-stu-id="5fc39-187">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="5fc39-188">![Criteri di rischio di accesso](./media/active-directory-identityprotection/1015.png "Criteri di rischio di accesso")</span><span class="sxs-lookup"><span data-stu-id="5fc39-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="5fc39-189">Impostare hello Accedi rischio soglia (low, medium o high) che attiva i criteri di hello:</span><span class="sxs-lookup"><span data-stu-id="5fc39-189">Set hello sign-in risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="5fc39-190">![Criteri di rischio di accesso](./media/active-directory-identityprotection/1016.png "Criteri di rischio di accesso")</span><span class="sxs-lookup"><span data-stu-id="5fc39-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="5fc39-191">Set hello controlli toobe applicato quando i criteri di hello attiva:</span><span class="sxs-lookup"><span data-stu-id="5fc39-191">Set hello controls toobe enforced when hello policy triggers:</span></span>  

    <span data-ttu-id="5fc39-192">![Criteri di rischio di accesso](./media/active-directory-identityprotection/1017.png "Criteri di rischio di accesso")</span><span class="sxs-lookup"><span data-stu-id="5fc39-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="5fc39-193">Stato di hello commutatore dei criteri:</span><span class="sxs-lookup"><span data-stu-id="5fc39-193">Switch hello state of your policy:</span></span>

    <span data-ttu-id="5fc39-194">![Registrazione MFA](./media/active-directory-identityprotection/403.png "Registrazione MFA")</span><span class="sxs-lookup"><span data-stu-id="5fc39-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="5fc39-195">Rivedere e valutare l'impatto di hello di una modifica prima di attivarlo:</span><span class="sxs-lookup"><span data-stu-id="5fc39-195">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="5fc39-196">![Criteri di rischio di accesso](./media/active-directory-identityprotection/1018.png "Criteri di rischio di accesso")</span><span class="sxs-lookup"><span data-stu-id="5fc39-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-tooknow"></a><span data-ttu-id="5fc39-197">È necessario tooknow</span><span class="sxs-lookup"><span data-stu-id="5fc39-197">What you need tooknow</span></span>
<span data-ttu-id="5fc39-198">È possibile configurare l'autenticazione a più fattori toorequire un rischio di accesso sicurezza criteri:</span><span class="sxs-lookup"><span data-stu-id="5fc39-198">You can configure a sign-in risk security policy toorequire multi-factor authentication:</span></span>

<span data-ttu-id="5fc39-199">![Criteri di rischio di accesso](./media/active-directory-identityprotection/1017.png "Criteri di rischio di accesso")</span><span class="sxs-lookup"><span data-stu-id="5fc39-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="5fc39-200">Tuttavia, per motivi di sicurezza, questa impostazione funziona soltanto per gli utenti che sono già stati registrati per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="5fc39-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="5fc39-201">Se l'autenticazione a più fattori toorequire hello condizione è soddisfatta per gli utenti che non sono ancora registrato per l'autenticazione a più fattori, l'utente hello è bloccato.</span><span class="sxs-lookup"><span data-stu-id="5fc39-201">If hello condition toorequire multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, hello user is blocked.</span></span>

<span data-ttu-id="5fc39-202">Come procedura consigliata, se si desidera toorequire multi-factor authentication per accessi rischiosi, è necessario:</span><span class="sxs-lookup"><span data-stu-id="5fc39-202">As a best practice, if you want toorequire multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="5fc39-203">Abilitare hello [criteri di autenticazione a più fattori registrazione](#multi-factor-authentication-registration-policy) per hello utenti interessati.</span><span class="sxs-lookup"><span data-stu-id="5fc39-203">Enable hello [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for hello affected users.</span></span>
2. <span data-ttu-id="5fc39-204">Richiedi hello interessati toologin gli utenti in una sessione non rischioso di tooperform una registrazione di autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="5fc39-204">Require hello affected users toologin in a non-risky session tooperform a MFA registration</span></span>

<span data-ttu-id="5fc39-205">L'esecuzione di questa procedura assicura che, in caso di accesso rischioso, venga richiesta l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="5fc39-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="5fc39-206">Procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="5fc39-206">Best practices</span></span>
<span data-ttu-id="5fc39-207">Scelta di un **elevata** soglia riduce il numero di hello di volte in cui un criterio viene attivato e riduce al minimo toousers impatto hello.</span><span class="sxs-lookup"><span data-stu-id="5fc39-207">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>  

<span data-ttu-id="5fc39-208">Tuttavia, esclude **bassa** e **Media** accessi contrassegno i rischi dai criteri di hello, che non potrebbero bloccare un utente malintenzionato di sfruttare un'identità compromessa.</span><span class="sxs-lookup"><span data-stu-id="5fc39-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from hello policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="5fc39-209">Quando impostazione hello criteri,</span><span class="sxs-lookup"><span data-stu-id="5fc39-209">When setting hello policy,</span></span>

* <span data-ttu-id="5fc39-210">Escludere gli utenti non hanno o non possono avere l'autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="5fc39-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="5fc39-211">Escludere gli utenti con impostazioni locali in cui l'abilitazione di hello criterio non è pratico (ad esempio toohelpdesk alcun accesso)</span><span class="sxs-lookup"><span data-stu-id="5fc39-211">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="5fc39-212">Escludere gli utenti che sono probabilmente toogenerate numerosi falsi positivi (sviluppatori, agli analisti della sicurezza)</span><span class="sxs-lookup"><span data-stu-id="5fc39-212">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="5fc39-213">Usare una soglia **alta** durante il rollout iniziale dei criteri o se è necessario ridurre al minimo gli avvisi visualizzati dagli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="5fc39-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="5fc39-214">Usare una soglia **bassa** se l'organizzazione richiede una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5fc39-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="5fc39-215">La scelta di una soglia **bassa** introduce richieste di accesso aggiuntive per l'utente, ma garantisce una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5fc39-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="5fc39-216">impostazione predefinita consigliata per la maggior parte delle organizzazioni è tooconfigure una regola per Hello un **Media** soglia toostrike un equilibrio tra usabilità e sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5fc39-216">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="5fc39-217">i criteri di accesso rischio Hello sono:</span><span class="sxs-lookup"><span data-stu-id="5fc39-217">hello sign-in risk policy is:</span></span>

* <span data-ttu-id="5fc39-218">Il traffico del browser tooall applicato e accesso tramite l'autenticazione moderna.</span><span class="sxs-lookup"><span data-stu-id="5fc39-218">Applied tooall browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="5fc39-219">Non applicato tooapplications utilizzando protocolli di sicurezza meno recenti, disabilitare endpoint WS-Trust hello IDP hello federato, ad esempio ADFS.</span><span class="sxs-lookup"><span data-stu-id="5fc39-219">Not applied tooapplications using older security protocols by disabling hello WS-Trust endpoint at hello federated IDP, such as ADFS.</span></span>

<span data-ttu-id="5fc39-220">Hello **eventi di rischio** pagina hello Identity Protection console Elenca tutti gli eventi:</span><span class="sxs-lookup"><span data-stu-id="5fc39-220">hello **Risk Events** page in hello Identity Protection console lists all events:</span></span>

* <span data-ttu-id="5fc39-221">Visualizzare a quali eventi sono stati applicati i criteri</span><span class="sxs-lookup"><span data-stu-id="5fc39-221">This policy was applied to</span></span>
* <span data-ttu-id="5fc39-222">È possibile esaminare l'attività hello e determinare se l'azione hello era appropriato o non</span><span class="sxs-lookup"><span data-stu-id="5fc39-222">You can review hello activity and determine whether hello action was appropriate or not</span></span>

<span data-ttu-id="5fc39-223">Per una panoramica di hello correlate esperienza utente, vedere:</span><span class="sxs-lookup"><span data-stu-id="5fc39-223">For an overview of hello related user experience, see:</span></span>

* [<span data-ttu-id="5fc39-224">Ripristino di un accesso rischioso</span><span class="sxs-lookup"><span data-stu-id="5fc39-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="5fc39-225">Accesso rischioso bloccato</span><span class="sxs-lookup"><span data-stu-id="5fc39-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="5fc39-226">Esperienze di accesso con Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5fc39-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="5fc39-227">**finestra di dialogo di configurazione correlato hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="5fc39-227">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="5fc39-228">In hello **Azure AD Identity Protection** pannello in hello **configura** fare clic su **Sign-in Criteri di rischio**.</span><span class="sxs-lookup"><span data-stu-id="5fc39-228">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="5fc39-229">![Criteri di rischio utente](./media/active-directory-identityprotection/1014.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5fc39-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="5fc39-230">Utenti contrassegnati per il rischio</span><span class="sxs-lookup"><span data-stu-id="5fc39-230">Users flagged for risk</span></span>

<span data-ttu-id="5fc39-231">Tutte attive [gli eventi di rischio](active-directory-identity-protection-risk-events.md) che sono stati rilevati da Azure Active Directory per un utente contribuiscono tooa concetto logico chiamato rischio utente.</span><span class="sxs-lookup"><span data-stu-id="5fc39-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute tooa logical concept called user risk.</span></span> <span data-ttu-id="5fc39-232">Un utente contrassegnato per il rischio è indicativo di un account utente che potrebbe essere stato compromesso.</span><span class="sxs-lookup"><span data-stu-id="5fc39-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Utenti contrassegnati per il rischio](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="5fc39-234">Livello di rischio utente</span><span class="sxs-lookup"><span data-stu-id="5fc39-234">User risk level</span></span>

<span data-ttu-id="5fc39-235">Livello di rischio un utente è un'indicazione (alta, Media o bassa) di probabilità hello che l'identità dell'utente hello sia stato compromesso.</span><span class="sxs-lookup"><span data-stu-id="5fc39-235">A user risk level is an indication (High, Medium, or Low) of hello likelihood that hello user’s identity has been compromised.</span></span> <span data-ttu-id="5fc39-236">Viene calcolato in base sugli eventi di rischio utente hello associati con l'identità dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5fc39-236">It is calculated based on hello user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="5fc39-237">Hello stato di un evento di rischio può essere **Active** o **chiuso**.</span><span class="sxs-lookup"><span data-stu-id="5fc39-237">hello status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="5fc39-238">Solo gli eventi di rischio **Active** contribuiscono calcolo livello di toohello utente dei rischi.</span><span class="sxs-lookup"><span data-stu-id="5fc39-238">Only risk events that are **Active** contribute toohello user risk level calculation.</span></span>

<span data-ttu-id="5fc39-239">livello di rischio utente Hello viene calcolato mediante hello seguenti input:</span><span class="sxs-lookup"><span data-stu-id="5fc39-239">hello user risk level is calculated using hello following inputs:</span></span>

* <span data-ttu-id="5fc39-240">Eventi di rischio attivo conseguenze utente hello</span><span class="sxs-lookup"><span data-stu-id="5fc39-240">Active risk events impacting hello user</span></span>
* <span data-ttu-id="5fc39-241">Livello di rischio di tali eventi.</span><span class="sxs-lookup"><span data-stu-id="5fc39-241">Risk level of these events</span></span>
* <span data-ttu-id="5fc39-242">Eventuali azioni di correzione intraprese o meno.</span><span class="sxs-lookup"><span data-stu-id="5fc39-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="5fc39-243">![Rischi utente](./media/active-directory-identityprotection/1031.png "Rischi utente")</span><span class="sxs-lookup"><span data-stu-id="5fc39-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="5fc39-244">È possibile utilizzare hello utente dei rischi livelli toocreate criteri di accesso condizionale che bloccano l'accesso degli utenti rischiosi o forzarne toosecurely cambiare la password.</span><span class="sxs-lookup"><span data-stu-id="5fc39-244">You can use hello user risk levels toocreate conditional access policies that block risky users from signing in, or force them toosecurely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="5fc39-245">Chiusura manuale degli eventi di rischio</span><span class="sxs-lookup"><span data-stu-id="5fc39-245">Closing risk events manually</span></span>

<span data-ttu-id="5fc39-246">Nella maggior parte dei casi, si avrà azioni correttive, ad esempio gli eventi di rischio Chiudi tooautomatically la reimpostazione della password sicura.</span><span class="sxs-lookup"><span data-stu-id="5fc39-246">In most cases, you will take remediation actions such as a secure password reset tooautomatically close risk events.</span></span> <span data-ttu-id="5fc39-247">Tuttavia, questo potrebbe non essere sempre possibile.</span><span class="sxs-lookup"><span data-stu-id="5fc39-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="5fc39-248">Ciò accade, ad esempio, hello, quando:</span><span class="sxs-lookup"><span data-stu-id="5fc39-248">This is, for example, hello case, when:</span></span>

* <span data-ttu-id="5fc39-249">Un utente con eventi di rischio attivi è stato eliminato</span><span class="sxs-lookup"><span data-stu-id="5fc39-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="5fc39-250">Un'analisi rivela che è stato eseguire un evento di rischio segnalati da utente legittimo hello</span><span class="sxs-lookup"><span data-stu-id="5fc39-250">An investigation reveals that a reported risk event has been perform by hello legitimate user</span></span>

<span data-ttu-id="5fc39-251">Poiché gli eventi di rischio che sono **Active** collaborazione calcolo del rischio di toohello utente, è possibile toomanually abbassare il livello di rischio chiudendo gli eventi di rischio manualmente.</span><span class="sxs-lookup"><span data-stu-id="5fc39-251">Because risk events that are **Active** contribute toohello user risk calculation, you may have toomanually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="5fc39-252">Corso hello dell'analisi, è possibile scegliere tootake uno stato di hello toochange queste azioni di un evento di rischio:</span><span class="sxs-lookup"><span data-stu-id="5fc39-252">During hello course of investigation, you can choose tootake any of these actions toochange hello status of a risk event:</span></span>

<span data-ttu-id="5fc39-253">![Azioni](./media/active-directory-identityprotection/34.png "Azioni")</span><span class="sxs-lookup"><span data-stu-id="5fc39-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="5fc39-254">**Risolvere** : se dopo aver esaminato un evento di rischio, è stata eseguita un'azione di correzione appropriata all'esterno di protezione dell'identità, e si ritiene che l'evento rischio hello deve essere considerato chiuso, evento hello contrassegna come risolto.</span><span class="sxs-lookup"><span data-stu-id="5fc39-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that hello risk event should be considered closed, mark hello event as Resolved.</span></span> <span data-ttu-id="5fc39-255">Eventi risolti imposterà tooClosed lo stato dell'evento di rischio hello ed evento rischio hello non contribuirà toouser rischio.</span><span class="sxs-lookup"><span data-stu-id="5fc39-255">Resolved events will set hello risk event’s status tooClosed and hello risk event will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="5fc39-256">**Contrassegna come falso positivo** : in alcuni casi è possibile analizzare un evento di rischio e scoprire che è stato erroneamente contrassegnato come rischioso.</span><span class="sxs-lookup"><span data-stu-id="5fc39-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="5fc39-257">È possibile ridurre il numero di hello di tali occorrenze contrassegnando l'evento di rischio hello come falsi positivi.</span><span class="sxs-lookup"><span data-stu-id="5fc39-257">You can help reduce hello number of such occurrences by marking hello risk event as False-positive.</span></span> <span data-ttu-id="5fc39-258">Ciò consentirà di classificazione di hello tooimprove algoritmi di eventi simili in futuro hello di apprendimento automatico hello.</span><span class="sxs-lookup"><span data-stu-id="5fc39-258">This will help hello machine learning algorithms tooimprove hello classification of similar events in hello future.</span></span> <span data-ttu-id="5fc39-259">stato Hello di eventi di falsi positivi è troppo**chiuso** e non contribuiscono non è più toouser rischio.</span><span class="sxs-lookup"><span data-stu-id="5fc39-259">hello status of false-positive events is too**Closed** and they will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="5fc39-260">**Ignora** : se non si è diventate qualsiasi azione di correzione, ma si desidera hello rischio evento toobe rimosso dall'elenco attivo hello, è possibile contrassegnare un evento di rischio Ignora e lo stato dell'evento hello verrà chiuso.</span><span class="sxs-lookup"><span data-stu-id="5fc39-260">**Ignore** - If you have not taken any remediation action, but want hello risk event toobe removed from hello active list, you can mark a risk event Ignore and hello event status will be Closed.</span></span> <span data-ttu-id="5fc39-261">Eventi ignorati non contribuiscono toouser rischio.</span><span class="sxs-lookup"><span data-stu-id="5fc39-261">Ignored events do not contribute toouser risk.</span></span> <span data-ttu-id="5fc39-262">Questa opzione deve essere usata solo in circostanze particolari.</span><span class="sxs-lookup"><span data-stu-id="5fc39-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="5fc39-263">**Riattivare** -eventi che sono stati chiusi manualmente dei rischi (scegliendo **risolvere**, **falso positivo**, o **ignora**) possono essere riattivati, impostazione hello lo stato di evento nuovo troppo**Active**.</span><span class="sxs-lookup"><span data-stu-id="5fc39-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting hello event status back too**Active**.</span></span> <span data-ttu-id="5fc39-264">Eventi di rischio riattivati contribuiscono calcolo livello di toohello utente dei rischi.</span><span class="sxs-lookup"><span data-stu-id="5fc39-264">Reactivated risk events contribute toohello user risk level calculation.</span></span> <span data-ttu-id="5fc39-265">Gli eventi di rischio chiusi tramite correzione, ad esempio la reimpostazione della password di protezione, non possono essere riattivati.</span><span class="sxs-lookup"><span data-stu-id="5fc39-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="5fc39-266">**finestra di dialogo di configurazione correlato hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="5fc39-266">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="5fc39-267">In hello **Azure AD Identity Protection** pannello, in **indagare**, fare clic su **gli eventi di rischio**.</span><span class="sxs-lookup"><span data-stu-id="5fc39-267">On hello **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="5fc39-268">![Reimpostazione manuale della password](./media/active-directory-identityprotection/1002.png "Reimpostazione manuale della password")</span><span class="sxs-lookup"><span data-stu-id="5fc39-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="5fc39-269">In hello **gli eventi di rischio** elenco, fare clic su un rischio.</span><span class="sxs-lookup"><span data-stu-id="5fc39-269">In hello **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="5fc39-270">![Reimpostazione manuale della password](./media/active-directory-identityprotection/1003.png "Reimpostazione manuale della password")</span><span class="sxs-lookup"><span data-stu-id="5fc39-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="5fc39-271">Nel Pannello di rischio hello, fare doppio clic su un utente.</span><span class="sxs-lookup"><span data-stu-id="5fc39-271">On hello risk blade, right-click a user.</span></span>

    <span data-ttu-id="5fc39-272">![Reimpostazione manuale della password](./media/active-directory-identityprotection/1004.png "Reimpostazione manuale della password")</span><span class="sxs-lookup"><span data-stu-id="5fc39-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="5fc39-273">Chiusura manuale di tutti gli eventi di rischio per un utente</span><span class="sxs-lookup"><span data-stu-id="5fc39-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="5fc39-274">Invece di chiuderla manualmente gli eventi di rischio per un utente singolarmente, la protezione dell'identità Azure Active Directory offre più tooclose un metodo tutti gli eventi per un utente con un solo clic.</span><span class="sxs-lookup"><span data-stu-id="5fc39-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method tooclose all events for a user with one click.</span></span>

<span data-ttu-id="5fc39-275">![Azioni](./media/active-directory-identityprotection/2222.png "Azioni")</span><span class="sxs-lookup"><span data-stu-id="5fc39-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="5fc39-276">Quando fa clic su **chiudere tutti gli eventi**, vengono chiusi tutti gli eventi e hello interessata utente non è più a rischio.</span><span class="sxs-lookup"><span data-stu-id="5fc39-276">When you click **Dismiss all events**, all events are closed and hello affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="5fc39-277">Correzione di eventi di rischio utente</span><span class="sxs-lookup"><span data-stu-id="5fc39-277">Remediating user risk events</span></span>

<span data-ttu-id="5fc39-278">Un monitoraggio e aggiornamento è un'azione toosecure un'identità o un dispositivo che è stato in precedenza o sospettato toobe compromesso.</span><span class="sxs-lookup"><span data-stu-id="5fc39-278">A remediation is an action toosecure an identity or a device that was previously suspected or known toobe compromised.</span></span> <span data-ttu-id="5fc39-279">Un'azione correttiva Ripristina hello identità o un dispositivo tooa sicuro lo stato e risolve i precedenti eventi di rischio associati all'identità hello o un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5fc39-279">A remediation action restores hello identity or device tooa safe state, and resolves previous risk events associated with hello identity or device.</span></span>

<span data-ttu-id="5fc39-280">eventi di rischio tooremediate utente, è possibile:</span><span class="sxs-lookup"><span data-stu-id="5fc39-280">tooremediate user risk events, you can:</span></span>

* <span data-ttu-id="5fc39-281">Eseguire manualmente gli eventi di rischio una password sicura reimpostazione tooremediate utente</span><span class="sxs-lookup"><span data-stu-id="5fc39-281">Perform a secure password reset tooremediate user risk events manually</span></span>
* <span data-ttu-id="5fc39-282">Configurare un toomitigate di criteri utente rischio per la sicurezza o correggere automaticamente gli eventi di rischio dell'utente</span><span class="sxs-lookup"><span data-stu-id="5fc39-282">Configure a user risk security policy toomitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="5fc39-283">Ricreare l'immagine dispositivo hello infettato</span><span class="sxs-lookup"><span data-stu-id="5fc39-283">Re-image hello infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="5fc39-284">Reimpostazione manuale della password di protezione</span><span class="sxs-lookup"><span data-stu-id="5fc39-284">Manual secure password reset</span></span>
<span data-ttu-id="5fc39-285">Per reimpostare la password sicura è un monitoraggio efficace per molti eventi di rischio e, quando eseguita, automaticamente chiude questi eventi di rischio e ricalcola a livello di rischio utente hello.</span><span class="sxs-lookup"><span data-stu-id="5fc39-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates hello user risk level.</span></span> <span data-ttu-id="5fc39-286">È possibile utilizzare hello Identity Protection dashboard tooinitiate una reimpostazione della password per un utente rischioso.</span><span class="sxs-lookup"><span data-stu-id="5fc39-286">You can use hello Identity Protection dashboard tooinitiate a password reset for a risky user.</span></span>

<span data-ttu-id="5fc39-287">finestra di dialogo correlate Hello fornisce due metodi diversi tooreset una password:</span><span class="sxs-lookup"><span data-stu-id="5fc39-287">hello related dialog provides two different methods tooreset a password:</span></span>

<span data-ttu-id="5fc39-288">**Reimpostazione della password** : selezionare questa opzione **richiedono hello utente tooreset la propria password** tooallow hello utente tooself-ripristina se hello utente ha registrato per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="5fc39-288">**Reset password** - Select **Require hello user tooreset their password** tooallow hello user tooself-recover if hello user has registered for multi-factor authentication.</span></span> <span data-ttu-id="5fc39-289">Durante l'hello utente successivo accesso, utente hello sarà necessario toosolve richiesta di autenticazione a più fattori completata e la password di hello toochange forzato, quindi.</span><span class="sxs-lookup"><span data-stu-id="5fc39-289">During hello user's next sign-in, hello user will be required toosolve a multi-factor authentication challenge successfully and then, forced toochange hello password.</span></span> <span data-ttu-id="5fc39-290">Questa opzione non è disponibile se l'account utente di hello non è già registrato multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="5fc39-290">This option isn't available if hello user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="5fc39-291">**Password temporanea** : selezionare questa opzione **generare una password temporanea** tooimmediately invalidare la password esistente hello e creare una nuova password temporanea per l'utente hello.</span><span class="sxs-lookup"><span data-stu-id="5fc39-291">**Temporary password** - Select **Generate a temporary password** tooimmediately invalidate hello existing password, and create a new temporary password for hello user.</span></span> <span data-ttu-id="5fc39-292">Inviare hello nuova password temporanea tooan indirizzo e-mail alternativo per utente hello o un responsabile dell'utente toohello.</span><span class="sxs-lookup"><span data-stu-id="5fc39-292">Send hello new temporary password tooan alternate email address for hello user or toohello user's manager.</span></span> <span data-ttu-id="5fc39-293">Poiché la password di hello è temporanea, utente hello sarà password hello toochange richiesto al momento dell'accesso.</span><span class="sxs-lookup"><span data-stu-id="5fc39-293">Because hello password is temporary, hello user will be prompted toochange hello password upon sign-in.</span></span>

<span data-ttu-id="5fc39-294">![Criteri](./media/active-directory-identityprotection/1005.png "Criteri")</span><span class="sxs-lookup"><span data-stu-id="5fc39-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="5fc39-295">**finestra di dialogo di configurazione correlato hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="5fc39-295">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="5fc39-296">In hello **Azure AD Identity Protection** pannello, fare clic su **utenti contrassegno i rischi**.</span><span class="sxs-lookup"><span data-stu-id="5fc39-296">On hello **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="5fc39-297">![Reimpostazione manuale della password](./media/active-directory-identityprotection/1006.png "Reimpostazione manuale della password")</span><span class="sxs-lookup"><span data-stu-id="5fc39-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="5fc39-298">Hello l'elenco di utenti, selezionare un utente con gli eventi di almeno un rischio.</span><span class="sxs-lookup"><span data-stu-id="5fc39-298">From hello list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="5fc39-299">![Reimpostazione manuale della password](./media/active-directory-identityprotection/1007.png "Reimpostazione manuale della password")</span><span class="sxs-lookup"><span data-stu-id="5fc39-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="5fc39-300">Nel Pannello di hello utente, fare clic su **reimpostazione password**.</span><span class="sxs-lookup"><span data-stu-id="5fc39-300">On hello user blade, click **Reset password**.</span></span>

    <span data-ttu-id="5fc39-301">![Reimpostazione manuale della password](./media/active-directory-identityprotection/1008.png "Reimpostazione manuale della password")</span><span class="sxs-lookup"><span data-stu-id="5fc39-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="5fc39-302">Criteri di sicurezza per il rischio utente</span><span class="sxs-lookup"><span data-stu-id="5fc39-302">User risk security policy</span></span>
<span data-ttu-id="5fc39-303">Un criterio di sicurezza utente dei rischi è un criterio di accesso condizionale che valuta utente specifico di hello rischio tooa livello e applica le azioni di attenuazione e monitoraggio e aggiornamento in base alle regole e condizioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="5fc39-303">A user risk security policy is a conditional access policy that evaluates hello risk level tooa specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="5fc39-304">![Criteri di rischio utente](./media/active-directory-identityprotection/1009.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5fc39-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="5fc39-305">Azure AD Identity Protection consente di gestire attenuazione hello e monitoraggio e aggiornamento di utenti contrassegnati i rischi grazie alla possibilità di:</span><span class="sxs-lookup"><span data-stu-id="5fc39-305">Azure AD Identity Protection helps you manage hello mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="5fc39-306">Hello utenti e gruppi hello criterio di impostazione si applica a:</span><span class="sxs-lookup"><span data-stu-id="5fc39-306">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="5fc39-307">![Criteri di rischio utente](./media/active-directory-identityprotection/1010.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5fc39-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="5fc39-308">Impostare hello utente dei rischi soglia (low, medium o high) che attiva i criteri di hello:</span><span class="sxs-lookup"><span data-stu-id="5fc39-308">Set hello user risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="5fc39-309">![Criteri di rischio utente](./media/active-directory-identityprotection/1011.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5fc39-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="5fc39-310">Set hello controlli toobe applicato quando i criteri di hello attiva:</span><span class="sxs-lookup"><span data-stu-id="5fc39-310">Set hello controls toobe enforced when hello policy triggers:</span></span>

    <span data-ttu-id="5fc39-311">![Criteri di rischio utente](./media/active-directory-identityprotection/1012.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5fc39-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="5fc39-312">Stato di hello commutatore dei criteri:</span><span class="sxs-lookup"><span data-stu-id="5fc39-312">Switch hello state of your policy:</span></span>

    <span data-ttu-id="5fc39-313">![Criteri di rischio utente](./media/active-directory-identityprotection/403.png "Registrazione MFA")</span><span class="sxs-lookup"><span data-stu-id="5fc39-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="5fc39-314">Rivedere e valutare l'impatto di hello di una modifica prima di attivarlo:</span><span class="sxs-lookup"><span data-stu-id="5fc39-314">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="5fc39-315">![Criteri di rischio utente](./media/active-directory-identityprotection/1013.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5fc39-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="5fc39-316">Scelta di un **elevata** soglia riduce il numero di hello di volte in cui un criterio viene attivato e riduce al minimo toousers impatto hello.</span><span class="sxs-lookup"><span data-stu-id="5fc39-316">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>
<span data-ttu-id="5fc39-317">Tuttavia, esclude **bassa** e **Media** utenti contrassegnati per rischi da criteri di hello, che potrebbero non sicuro identità o i dispositivi che sono state in precedenza o sospettati toobe compromesso.</span><span class="sxs-lookup"><span data-stu-id="5fc39-317">However, it excludes **Low** and **Medium** users flagged for risk from hello policy, which may not secure identities or devices that were previously suspected or known toobe compromised.</span></span>

<span data-ttu-id="5fc39-318">Quando impostazione hello criteri,</span><span class="sxs-lookup"><span data-stu-id="5fc39-318">When setting hello policy,</span></span>

* <span data-ttu-id="5fc39-319">Escludere gli utenti che sono probabilmente toogenerate numerosi falsi positivi (sviluppatori, agli analisti della sicurezza)</span><span class="sxs-lookup"><span data-stu-id="5fc39-319">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="5fc39-320">Escludere gli utenti con impostazioni locali in cui l'abilitazione di hello criterio non è pratico (ad esempio toohelpdesk alcun accesso)</span><span class="sxs-lookup"><span data-stu-id="5fc39-320">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="5fc39-321">Usare una soglia **alta** durante il rollout iniziale dei criteri o se è necessario ridurre al minimo gli avvisi visualizzati dagli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="5fc39-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="5fc39-322">Usare una soglia **bassa** se l'organizzazione richiede una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5fc39-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="5fc39-323">La scelta di una soglia **bassa** introduce richieste di accesso aggiuntive per l'utente, ma garantisce una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5fc39-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="5fc39-324">impostazione predefinita consigliata per la maggior parte delle organizzazioni è tooconfigure una regola per Hello un **Media** soglia toostrike un equilibrio tra usabilità e sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5fc39-324">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="5fc39-325">Per una panoramica di hello correlate esperienza utente, vedere:</span><span class="sxs-lookup"><span data-stu-id="5fc39-325">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="5fc39-326">[Flusso di ripristino di account compromessi](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="5fc39-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="5fc39-327">[Flusso di account compromessi bloccati](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="5fc39-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="5fc39-328">**finestra di dialogo di configurazione correlato hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="5fc39-328">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="5fc39-329">In hello **Azure AD Identity Protection** pannello in hello **configura** fare clic su **rischio utente**.</span><span class="sxs-lookup"><span data-stu-id="5fc39-329">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="5fc39-330">![Criteri di rischio utente](./media/active-directory-identityprotection/1009.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5fc39-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="5fc39-331">Mitigazione di eventi di rischio utente</span><span class="sxs-lookup"><span data-stu-id="5fc39-331">Mitigating user risk events</span></span>
<span data-ttu-id="5fc39-332">Gli amministratori possono impostare un utente dei rischi sicurezza criteri tooblock utenti al momento dell'accesso in base al livello di rischio hello.</span><span class="sxs-lookup"><span data-stu-id="5fc39-332">Administrators can set a user risk security policy tooblock users upon sign-in depending on hello risk level.</span></span>

<span data-ttu-id="5fc39-333">Il blocco dell'accesso:</span><span class="sxs-lookup"><span data-stu-id="5fc39-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="5fc39-334">Impedisce la generazione di hello del nuovo utente di eventi di rischio per l'utente interessato hello</span><span class="sxs-lookup"><span data-stu-id="5fc39-334">Prevents hello generation of new user risk events for hello affected user</span></span>
* <span data-ttu-id="5fc39-335">Consente agli amministratori toomanually risolvere gli eventi di rischio hello influire sull'identità dell'utente hello e ripristinarlo stato protetto tooa</span><span class="sxs-lookup"><span data-stu-id="5fc39-335">Enables administrators toomanually remediate hello risk events affecting hello user's identity and restore it tooa secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="5fc39-336">Criteri di registrazione per l'autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="5fc39-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="5fc39-337">Azure multi-factor authentication è un metodo di verifica dell'identità dell'utente che richiede l'uso di hello di molto più di un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="5fc39-337">Azure multi-factor authentication is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="5fc39-338">Fornisce un secondo livello di sicurezza toouser accessi e le transazioni.</span><span class="sxs-lookup"><span data-stu-id="5fc39-338">It provides a second layer of security toouser sign-ins and transactions.</span></span>  
<span data-ttu-id="5fc39-339">È consigliabile richiedere l'autenticazione a più fattori per l'accesso degli utenti perché:</span><span class="sxs-lookup"><span data-stu-id="5fc39-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="5fc39-340">Offre un'autenticazione avanzata con una gamma di opzioni di verifica semplici</span><span class="sxs-lookup"><span data-stu-id="5fc39-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="5fc39-341">Svolge un ruolo chiave nella preparazione tooprotect l'organizzazione e il ripristino da compromette account</span><span class="sxs-lookup"><span data-stu-id="5fc39-341">Plays a key role in preparing your organization tooprotect and recover from account compromises</span></span>

<span data-ttu-id="5fc39-342">![Criteri di rischio utente](./media/active-directory-identityprotection/1019.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5fc39-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="5fc39-343">Per altre informazioni, vedere la pagina relativa ad [Informazioni su Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="5fc39-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="5fc39-344">Azure AD Identity Protection consente di gestire hello roll-out della registrazione di autenticazione a più fattori tramite la configurazione di un criterio che consente di:</span><span class="sxs-lookup"><span data-stu-id="5fc39-344">Azure AD Identity Protection helps you manage hello roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="5fc39-345">Hello utenti e gruppi hello criterio di impostazione si applica a:</span><span class="sxs-lookup"><span data-stu-id="5fc39-345">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="5fc39-346">![Criteri MFA](./media/active-directory-identityprotection/1020.png "Criteri MFA")</span><span class="sxs-lookup"><span data-stu-id="5fc39-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="5fc39-347">Set hello controlli toobe applicato quando i criteri di hello attiva:</span><span class="sxs-lookup"><span data-stu-id="5fc39-347">Set hello controls toobe enforced when hello policy triggers::</span></span>  

    <span data-ttu-id="5fc39-348">![Criteri MFA](./media/active-directory-identityprotection/1021.png "Criteri MFA")</span><span class="sxs-lookup"><span data-stu-id="5fc39-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="5fc39-349">Stato di hello commutatore dei criteri:</span><span class="sxs-lookup"><span data-stu-id="5fc39-349">Switch hello state of your policy:</span></span>

    <span data-ttu-id="5fc39-350">![Criteri MFA](./media/active-directory-identityprotection/403.png "Criteri MFA")</span><span class="sxs-lookup"><span data-stu-id="5fc39-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="5fc39-351">Visualizzare lo stato della registrazione corrente hello:</span><span class="sxs-lookup"><span data-stu-id="5fc39-351">View hello current registration status:</span></span>

    <span data-ttu-id="5fc39-352">![Criteri MFA](./media/active-directory-identityprotection/1022.png "Criteri MFA")</span><span class="sxs-lookup"><span data-stu-id="5fc39-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="5fc39-353">Per una panoramica di hello correlate esperienza utente, vedere:</span><span class="sxs-lookup"><span data-stu-id="5fc39-353">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="5fc39-354">[Flusso di registrazione per l'autenticazione a più fattori](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="5fc39-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="5fc39-355">[Esperienze di accesso con Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="5fc39-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="5fc39-356">**finestra di dialogo di configurazione correlato hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="5fc39-356">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="5fc39-357">In hello **Azure AD Identity Protection** pannello in hello **configura** fare clic su **registrazione a multi-factor authentication**.</span><span class="sxs-lookup"><span data-stu-id="5fc39-357">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="5fc39-358">![Criteri MFA](./media/active-directory-identityprotection/1019.png "Criteri MFA")</span><span class="sxs-lookup"><span data-stu-id="5fc39-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fc39-359">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5fc39-359">Next steps</span></span>
* [<span data-ttu-id="5fc39-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span><span class="sxs-lookup"><span data-stu-id="5fc39-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="5fc39-361">Abilitazione di Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5fc39-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="5fc39-362">Vulnerabilità rilevate da Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5fc39-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="5fc39-363">Eventi di rischio di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fc39-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="5fc39-364">Notifiche di Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5fc39-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="5fc39-365">Studio di Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5fc39-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="5fc39-366">Glossario di Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5fc39-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="5fc39-367">Esperienze di accesso con Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5fc39-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="5fc39-368">Azure Active Directory la protezione dell'identità, come gli utenti toounblock</span><span class="sxs-lookup"><span data-stu-id="5fc39-368">Azure Active Directory Identity Protection - How toounblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="5fc39-369">Introduzione ad Azure Active Directory Identity Protection e a Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="5fc39-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
