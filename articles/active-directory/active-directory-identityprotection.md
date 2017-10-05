---
title: Azure Active Directory Identity Protection | Microsoft Docs
description: "Informazioni su come Azure AD Identity Protection consente di limitare la possibilità di un utente malintenzionato di sfruttare un'identità o un dispositivo compromesso e di proteggere un'identità o un dispositivo che in precedenza è stato sospettato o ritenuto essere compromesso."
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
ms.openlocfilehash: 0c7a8d68c0df729441e3f7faa5cd06066db1261d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="5866a-104">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5866a-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="5866a-105">Azure Active Directory Identity Protection è una funzionalità dell'edizione Azure AD Premium P2 che consente di:</span><span class="sxs-lookup"><span data-stu-id="5866a-105">Azure Active Directory Identity Protection is a feature of the Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="5866a-106">Rilevare le potenziali vulnerabilità per le identità dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="5866a-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="5866a-107">Configurare risposte automatizzate alle azioni sospette rilevate correlate alle identità dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="5866a-107">Configure automated responses to detected suspicious actions that are related to your organization’s identities</span></span>  

- <span data-ttu-id="5866a-108">Esaminare gli eventi imprevisti sospetti ed eseguire l'azione appropriata per risolverli</span><span class="sxs-lookup"><span data-stu-id="5866a-108">Investigate suspicious incidents and take appropriate action to resolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="5866a-109">introduttiva</span><span class="sxs-lookup"><span data-stu-id="5866a-109">Getting started</span></span>

<span data-ttu-id="5866a-110">Microsoft protegge le identità basate sul cloud per oltre un decennio.</span><span class="sxs-lookup"><span data-stu-id="5866a-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="5866a-111">Con Azure Active Directory Identity Protection, è possibile usare nell'ambiente gli stessi sistemi di protezione usati da Microsoft per proteggere le identità.</span><span class="sxs-lookup"><span data-stu-id="5866a-111">With Azure Active Directory Identity Protection, in your environment, you can use the same protection systems Microsoft uses to secure identities.</span></span>

<span data-ttu-id="5866a-112">La maggior parte delle violazioni della sicurezza si verifica quando utenti malintenzionati ottengono l'accesso a un ambiente impadronendosi dell'identità di un utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-112">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span></span> <span data-ttu-id="5866a-113">Nel corso degli anni, gli utenti malintenzionati hanno messo a punto tecniche sempre più efficaci per sfruttare le violazioni di terze parti e sferrare sofisticati attacchi di phishing.</span><span class="sxs-lookup"><span data-stu-id="5866a-113">Over the years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="5866a-114">L'accesso a un account utente, anche quelli con privilegi limitati, permette agli utenti malintenzionati di accedere immediatamente a risorse aziendali importanti in modo relativamente semplice tramite il movimento laterale.</span><span class="sxs-lookup"><span data-stu-id="5866a-114">As soon as an attacker gains access to even low privileged user accounts, it is relatively easy for them to gain access to important company resources through lateral movement.</span></span>

<span data-ttu-id="5866a-115">Di conseguenza, è necessario:</span><span class="sxs-lookup"><span data-stu-id="5866a-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="5866a-116">Proteggere tutte le identità indipendentemente dal livello di privilegi</span><span class="sxs-lookup"><span data-stu-id="5866a-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="5866a-117">Impedire in modo proattivo l'uso improprio delle identità compromesse</span><span class="sxs-lookup"><span data-stu-id="5866a-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="5866a-118">Trovare le identità compromesse non è un compito facile.</span><span class="sxs-lookup"><span data-stu-id="5866a-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="5866a-119">Azure Active Directory usa l'euristica e gli algoritmi adattivi di apprendimento automatico per rilevare anomalie ed eventi imprevisti sospetti che indicano identità potenzialmente compromesse.</span><span class="sxs-lookup"><span data-stu-id="5866a-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="5866a-120">Sulla base di tali dati, Identity Protection genera report e avvisi che consentono di valutare i problemi rilevati e di adottare le azioni di correzione o mitigazione appropriate.</span><span class="sxs-lookup"><span data-stu-id="5866a-120">Using this data, Identity Protection generates reports and alerts that enable you to evaluate the detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="5866a-121">Azure Active Directory Identity Protection è ben più di un semplice strumento di monitoraggio e reporting.</span><span class="sxs-lookup"><span data-stu-id="5866a-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="5866a-122">Per proteggere le identità dell'organizzazione, è possibile configurare criteri basati sul rischio che rispondano automaticamente ai problemi rilevati quando viene raggiunto un livello di rischio specificato.</span><span class="sxs-lookup"><span data-stu-id="5866a-122">To protect your organization's identities, you can configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="5866a-123">Questi criteri, con altri controlli di accesso condizionale forniti da Azure Active Directory e da EMS, possono eseguire il blocco automatico o avviare azioni di correzione adattive, incluse la reimpostazione della password e l'applicazione dell'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="5866a-123">These policies, in addition to other conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="5866a-124">Funzionalità di Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5866a-124">Identity Protection capabilities</span></span>

<span data-ttu-id="5866a-125">**Rilevamento di vulnerabilità e di account rischiosi:**</span><span class="sxs-lookup"><span data-stu-id="5866a-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="5866a-126">Raccomandazioni personalizzate per migliorare il comportamento di sicurezza in generale evidenziando le vulnerabilità.</span><span class="sxs-lookup"><span data-stu-id="5866a-126">Providing custom recommendations to improve overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="5866a-127">Calcolo dei livelli di rischio di accesso.</span><span class="sxs-lookup"><span data-stu-id="5866a-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="5866a-128">Calcolo dei livelli di rischio utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-128">Calculating user risk levels</span></span>


<span data-ttu-id="5866a-129">**Analisi degli eventi di rischio:**</span><span class="sxs-lookup"><span data-stu-id="5866a-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="5866a-130">Invio di notifiche per gli eventi di rischio.</span><span class="sxs-lookup"><span data-stu-id="5866a-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="5866a-131">Analisi degli eventi di rischio con informazioni rilevanti e contestuali.</span><span class="sxs-lookup"><span data-stu-id="5866a-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="5866a-132">Flussi di lavoro di base per tenere traccia delle analisi.</span><span class="sxs-lookup"><span data-stu-id="5866a-132">Providing basic workflows to track investigations</span></span>
* <span data-ttu-id="5866a-133">Accesso semplificato ad azioni di correzione come la reimpostazione della password.</span><span class="sxs-lookup"><span data-stu-id="5866a-133">Providing easy access to remediation actions such as password reset</span></span>

<span data-ttu-id="5866a-134">**Criteri di accesso condizionale basati sul rischio:**</span><span class="sxs-lookup"><span data-stu-id="5866a-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="5866a-135">Criteri per mitigare gli accessi rischiosi con il blocco degli accessi o le richieste di autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="5866a-135">Policy to mitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="5866a-136">Criteri per bloccare o proteggere gli account utente rischiosi.</span><span class="sxs-lookup"><span data-stu-id="5866a-136">Policy to block or secure risky user accounts</span></span>
* <span data-ttu-id="5866a-137">Criteri per richiedere la registrazione degli utenti per l'autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="5866a-137">Policy to require users to register for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="5866a-138">Ruoli di Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5866a-138">Identity Protection roles</span></span>

<span data-ttu-id="5866a-139">Per bilanciare il carico delle attività di gestione per l'implementazione di Identity Protection, è possibile assegnare più ruoli.</span><span class="sxs-lookup"><span data-stu-id="5866a-139">To load balance the management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="5866a-140">Azure AD Identity Protection supporta 3 ruoli di directory:</span><span class="sxs-lookup"><span data-stu-id="5866a-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="5866a-141">Ruolo</span><span class="sxs-lookup"><span data-stu-id="5866a-141">Role</span></span>                         | <span data-ttu-id="5866a-142">Operazione consentita</span><span class="sxs-lookup"><span data-stu-id="5866a-142">Can do</span></span>                          | <span data-ttu-id="5866a-143">Operazione non consentita</span><span class="sxs-lookup"><span data-stu-id="5866a-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="5866a-144">Amministratore globale</span><span class="sxs-lookup"><span data-stu-id="5866a-144">Global administrator</span></span>         | <span data-ttu-id="5866a-145">Accesso completo a Identity Protection, implementazione di Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5866a-145">Full access to Identity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="5866a-146">Amministratore della sicurezza</span><span class="sxs-lookup"><span data-stu-id="5866a-146">Security administrator</span></span>       | <span data-ttu-id="5866a-147">Accesso completo a Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5866a-147">Full access to Identity Protection</span></span> | <span data-ttu-id="5866a-148">Implementazione di Identity Protection, reimpostazione delle password per un utente</span><span class="sxs-lookup"><span data-stu-id="5866a-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="5866a-149">Ruolo con autorizzazioni di lettura per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="5866a-149">Security reader</span></span>              | <span data-ttu-id="5866a-150">Accesso in sola lettura a Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5866a-150">Ready-only access to Identity Protection</span></span> | <span data-ttu-id="5866a-151">Implementazione di Identity Protection, correzione degli utenti, configurazione dei criteri, reimpostazione delle password</span><span class="sxs-lookup"><span data-stu-id="5866a-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="5866a-152">Per altri dettagli, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5866a-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="5866a-153">Rilevamento</span><span class="sxs-lookup"><span data-stu-id="5866a-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="5866a-154">Vulnerabilità</span><span class="sxs-lookup"><span data-stu-id="5866a-154">Vulnerabilities</span></span>

<span data-ttu-id="5866a-155">Azure Active Directory Identity Protection analizza la configurazione e rileva le vulnerabilità che possono avere effetto sulle identità dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="5866a-156">Per altri dettagli, vedere [Vulnerabilità rilevate da Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="5866a-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="5866a-157">Eventi di rischio</span><span class="sxs-lookup"><span data-stu-id="5866a-157">Risk events</span></span>

<span data-ttu-id="5866a-158">Azure Active Directory usa l'euristica e algoritmi adattivi di apprendimento automatico per rilevare azioni sospette correlate alle identità dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user's identities.</span></span> <span data-ttu-id="5866a-159">Il sistema crea un record per ogni azione sospetta rilevata.</span><span class="sxs-lookup"><span data-stu-id="5866a-159">The system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="5866a-160">Questi record sono denominati anche eventi di rischio.</span><span class="sxs-lookup"><span data-stu-id="5866a-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="5866a-161">Per altre informazioni, vedere [Eventi di rischio di Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="5866a-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="5866a-162">Analisi</span><span class="sxs-lookup"><span data-stu-id="5866a-162">Investigation</span></span>
<span data-ttu-id="5866a-163">L'esperienza con Identity Protection inizia in genere dal relativo dashboard.</span><span class="sxs-lookup"><span data-stu-id="5866a-163">Your journey through Identity Protection typically starts with the Identity Protection dashboard.</span></span>

<span data-ttu-id="5866a-164">![Correzione](./media/active-directory-identityprotection/1000.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="5866a-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="5866a-165">Il dashboard consente di accedere a:</span><span class="sxs-lookup"><span data-stu-id="5866a-165">The dashboard gives you access to:</span></span>

* <span data-ttu-id="5866a-166">Report, ad esempio **Utenti contrassegnati per il rischio**, **Eventi di rischio** e **Vulnerabilità**</span><span class="sxs-lookup"><span data-stu-id="5866a-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="5866a-167">Impostazioni come la configurazione dei **criteri di sicurezza**, delle **notifiche** e della **registrazione per l'autenticazione a più fattori**</span><span class="sxs-lookup"><span data-stu-id="5866a-167">Settings such as the configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="5866a-168">Si tratta in genere del punto di partenza dell'analisi, ovvero del processo di analisi di attività, log e altre informazioni rilevanti relative a un evento di rischio per decidere se sono necessarie procedure di correzione o mitigazione, se e come l'identità è stata compromessa e come è stata usata l'identità compromessa.</span><span class="sxs-lookup"><span data-stu-id="5866a-168">It is typically your starting point for investigation, which is the process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary,  and how the identity was compromised, and understand how the compromised identity was used.</span></span>

<span data-ttu-id="5866a-169">È possibile collegare le attività di analisi alle [notifiche](active-directory-identityprotection-notifications.md) che Azure Active Directory Protection invia per posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="5866a-169">You can tie your investigation activities to the [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="5866a-170">Le sezioni seguenti forniscono altre informazioni e i passaggi relativi a un'analisi.</span><span class="sxs-lookup"><span data-stu-id="5866a-170">The following sections provide you with more details and the steps that are related to an investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="5866a-171">Accessi a rischio</span><span class="sxs-lookup"><span data-stu-id="5866a-171">Risky sign-ins</span></span>

<span data-ttu-id="5866a-172">Azure Active Directory rileva i [tipi di eventi di rischio](active-directory-reporting-risk-events.md#risk-event-types) in tempo reale e offline.</span><span class="sxs-lookup"><span data-stu-id="5866a-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="5866a-173">Ogni evento di rischio in tempo reale rilevato per un accesso di un utente rientra nel concetto logico degli accessi a rischio.</span><span class="sxs-lookup"><span data-stu-id="5866a-173">Each risk event that has been detected for a sign-in of a user contributes to a logical concept called risky sign-in.</span></span> <span data-ttu-id="5866a-174">Un accesso a rischio è indicativo di un tentativo di accesso che potrebbe non essere stato eseguito dal legittimo proprietario di un account utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by the legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="5866a-175">Livello di rischio di un accesso</span><span class="sxs-lookup"><span data-stu-id="5866a-175">Sign-in risk level</span></span>

<span data-ttu-id="5866a-176">Il livello di rischio di un accesso è un'indicazione (Alto, Medio o Basso) della probabilità che un tentativo di accesso non sia stato eseguito dal legittimo proprietario di un account utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-176">A sign-in risk level is an indication (High, Medium, or Low) of the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="5866a-177">Mitigazione degli eventi di rischio di accesso</span><span class="sxs-lookup"><span data-stu-id="5866a-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="5866a-178">La mitigazione è un'azione che consente di limitare la possibilità che un utente malintenzionato sfrutti un'identità o un dispositivo compromesso senza ripristinare l'identità o il dispositivo a uno stato sicuro.</span><span class="sxs-lookup"><span data-stu-id="5866a-178">A mitigation is an action to limit the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="5866a-179">La mitigazione non risolve gli eventi di rischio di accesso precedenti associati all'identità o al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5866a-179">A mitigation does not resolve previous sign-in risk events associated with the identity or device.</span></span>

<span data-ttu-id="5866a-180">Per attenuare automaticamente gli accessi a rischio, è possibile configurare criteri di rischio per gli accessi.</span><span class="sxs-lookup"><span data-stu-id="5866a-180">To mitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="5866a-181">Usando questi criteri, si tiene conto del livello di rischio dell'utente o dell'accesso per bloccare gli accessi rischiosi o richiedere all'utente di eseguire l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="5866a-181">Using these policies, you consider the risk level of the user or the sign-in to block risky sign-ins or require the user to perform multi-factor authentication.</span></span> <span data-ttu-id="5866a-182">Queste azioni possono impedire a un utente malintenzionato di sfruttare un'identità rubata per causare danni e permettono di guadagnare tempo per proteggere l'identità.</span><span class="sxs-lookup"><span data-stu-id="5866a-182">These actions may prevent an attacker from exploiting a stolen identity to cause damage, and may give you some time to secure the identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="5866a-183">Criteri di sicurezza per il rischio di accesso</span><span class="sxs-lookup"><span data-stu-id="5866a-183">Sign-in risk security policy</span></span>
<span data-ttu-id="5866a-184">I criteri di rischio di accesso sono criteri di accesso condizionale che valutano il rischio associato a un accesso specifico e applicano le azioni di mitigazione in base a condizioni e regole predefinite.</span><span class="sxs-lookup"><span data-stu-id="5866a-184">A sign-in risk policy is a conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="5866a-185">![Criteri di rischio di accesso](./media/active-directory-identityprotection/1014.png "Criteri di rischio di accesso")</span><span class="sxs-lookup"><span data-stu-id="5866a-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="5866a-186">Azure AD Identity Protection consente di gestire le azioni di mitigazione degli accessi rischiosi seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5866a-186">Azure AD Identity Protection helps you manage the mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="5866a-187">Impostare gli utenti e i gruppi a cui vengono applicati i criteri:</span><span class="sxs-lookup"><span data-stu-id="5866a-187">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="5866a-188">![Criteri di rischio di accesso](./media/active-directory-identityprotection/1015.png "Criteri di rischio di accesso")</span><span class="sxs-lookup"><span data-stu-id="5866a-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="5866a-189">Impostare la soglia del livello di rischio di accesso, bassa, media o alta, che attiva il criterio:</span><span class="sxs-lookup"><span data-stu-id="5866a-189">Set the sign-in risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="5866a-190">![Criteri di rischio di accesso](./media/active-directory-identityprotection/1016.png "Criteri di rischio di accesso")</span><span class="sxs-lookup"><span data-stu-id="5866a-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="5866a-191">Impostare i controlli da applicare quando viene attivato il criterio:</span><span class="sxs-lookup"><span data-stu-id="5866a-191">Set the controls to be enforced when the policy triggers:</span></span>  

    <span data-ttu-id="5866a-192">![Criteri di rischio di accesso](./media/active-directory-identityprotection/1017.png "Criteri di rischio di accesso")</span><span class="sxs-lookup"><span data-stu-id="5866a-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="5866a-193">Cambiare lo stato dei criteri:</span><span class="sxs-lookup"><span data-stu-id="5866a-193">Switch the state of your policy:</span></span>

    <span data-ttu-id="5866a-194">![Registrazione MFA](./media/active-directory-identityprotection/403.png "Registrazione MFA")</span><span class="sxs-lookup"><span data-stu-id="5866a-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="5866a-195">Esaminare e valutare l'impatto di una modifica prima di attivarla:</span><span class="sxs-lookup"><span data-stu-id="5866a-195">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="5866a-196">![Criteri di rischio di accesso](./media/active-directory-identityprotection/1018.png "Criteri di rischio di accesso")</span><span class="sxs-lookup"><span data-stu-id="5866a-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-to-know"></a><span data-ttu-id="5866a-197">Informazioni importanti</span><span class="sxs-lookup"><span data-stu-id="5866a-197">What you need to know</span></span>
<span data-ttu-id="5866a-198">È possibile configurare un criterio di sicurezza per il rischio di accesso per richiedere l'autenticazione a più fattori:</span><span class="sxs-lookup"><span data-stu-id="5866a-198">You can configure a sign-in risk security policy to require multi-factor authentication:</span></span>

<span data-ttu-id="5866a-199">![Criteri di rischio di accesso](./media/active-directory-identityprotection/1017.png "Criteri di rischio di accesso")</span><span class="sxs-lookup"><span data-stu-id="5866a-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="5866a-200">Tuttavia, per motivi di sicurezza, questa impostazione funziona soltanto per gli utenti che sono già stati registrati per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="5866a-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="5866a-201">Se la condizione per richiedere l'autenticazione a più fattori risulta soddisfatta per un utente che non è ancora registrato per l'autenticazione a più fattori, tale utente viene bloccato.</span><span class="sxs-lookup"><span data-stu-id="5866a-201">If the condition to require multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, the user is blocked.</span></span>

<span data-ttu-id="5866a-202">Se si vuole richiedere l'autenticazione a più fattori per gli accessi rischiosi, è consigliabile procedere nel modo indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5866a-202">As a best practice, if you want to require multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="5866a-203">Abilitare il [criterio di registrazione per l'autenticazione a più fattori](#multi-factor-authentication-registration-policy) per gli utenti interessati.</span><span class="sxs-lookup"><span data-stu-id="5866a-203">Enable the [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for the affected users.</span></span>
2. <span data-ttu-id="5866a-204">Richiedere agli utenti interessati di accedere in una sessione non rischiosa per eseguire la registrazione per l'autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="5866a-204">Require the affected users to login in a non-risky session to perform a MFA registration</span></span>

<span data-ttu-id="5866a-205">L'esecuzione di questa procedura assicura che, in caso di accesso rischioso, venga richiesta l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="5866a-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="5866a-206">Procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="5866a-206">Best practices</span></span>
<span data-ttu-id="5866a-207">La scelta di una soglia **alta** riduce la frequenza di attivazione dei criteri e riduce al minimo l'impatto sugli utenti.</span><span class="sxs-lookup"><span data-stu-id="5866a-207">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>  

<span data-ttu-id="5866a-208">Tuttavia, esclude dai criteri gli accessi contrassegnati per il rischio con una soglia **bassa** o **media**. Questa scelta può non impedire a un utente malintenzionato di sfruttare un'identità compromessa.</span><span class="sxs-lookup"><span data-stu-id="5866a-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from the policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="5866a-209">Quando si impostano i criteri:</span><span class="sxs-lookup"><span data-stu-id="5866a-209">When setting the policy,</span></span>

* <span data-ttu-id="5866a-210">Escludere gli utenti non hanno o non possono avere l'autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="5866a-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="5866a-211">Escludere gli utenti con impostazioni locali in cui abilitare i criteri non è pratico, ad esempio per la mancanza di accesso al supporto tecnico</span><span class="sxs-lookup"><span data-stu-id="5866a-211">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="5866a-212">Escludere gli utenti che possono generare molti falsi positivi, ad esempio sviluppatori o analisti della sicurezza</span><span class="sxs-lookup"><span data-stu-id="5866a-212">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="5866a-213">Usare una soglia **alta** durante il rollout iniziale dei criteri o se è necessario ridurre al minimo gli avvisi visualizzati dagli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="5866a-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="5866a-214">Usare una soglia **bassa** se l'organizzazione richiede una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5866a-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="5866a-215">La scelta di una soglia **bassa** introduce richieste di accesso aggiuntive per l'utente, ma garantisce una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5866a-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="5866a-216">L'impostazione predefinita consigliata per la maggior parte delle organizzazioni è la configurazione di una regola per una soglia **media** , che permette di bilanciare usabilità e sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5866a-216">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="5866a-217">I criteri di rischio di accesso:</span><span class="sxs-lookup"><span data-stu-id="5866a-217">The sign-in risk policy is:</span></span>

* <span data-ttu-id="5866a-218">Vengono applicati a tutto il traffico tramite browser e agli accessi che usano l'autenticazione moderna.</span><span class="sxs-lookup"><span data-stu-id="5866a-218">Applied to all browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="5866a-219">Non vengono applicati alle applicazioni che usano protocolli di sicurezza meno recenti disabilitando l'endpoint WS-Trust in corrispondenza dell'IDP federato, ad esempio ADFS.</span><span class="sxs-lookup"><span data-stu-id="5866a-219">Not applied to applications using older security protocols by disabling the WS-Trust endpoint at the federated IDP, such as ADFS.</span></span>

<span data-ttu-id="5866a-220">La pagina **Eventi di rischio** nella console di Identity Protection contiene un elenco di tutti gli eventi:</span><span class="sxs-lookup"><span data-stu-id="5866a-220">The **Risk Events** page in the Identity Protection console lists all events:</span></span>

* <span data-ttu-id="5866a-221">Visualizzare a quali eventi sono stati applicati i criteri</span><span class="sxs-lookup"><span data-stu-id="5866a-221">This policy was applied to</span></span>
* <span data-ttu-id="5866a-222">Esaminare l'attività e determinare se l'azione è stata appropriata o meno</span><span class="sxs-lookup"><span data-stu-id="5866a-222">You can review the activity and determine whether the action was appropriate or not</span></span>

<span data-ttu-id="5866a-223">Per una panoramica dell'esperienza utente correlata, vedere:</span><span class="sxs-lookup"><span data-stu-id="5866a-223">For an overview of the related user experience, see:</span></span>

* [<span data-ttu-id="5866a-224">Ripristino di un accesso rischioso</span><span class="sxs-lookup"><span data-stu-id="5866a-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="5866a-225">Accesso rischioso bloccato</span><span class="sxs-lookup"><span data-stu-id="5866a-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="5866a-226">Esperienze di accesso con Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5866a-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="5866a-227">**Per aprire la relativa finestra di dialogo di configurazione**:</span><span class="sxs-lookup"><span data-stu-id="5866a-227">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="5866a-228">Nel pannello **Azure AD Identity Protection** fare clic su **Criteri di rischio di accesso** nella sezione **Configura**.</span><span class="sxs-lookup"><span data-stu-id="5866a-228">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="5866a-229">![Criteri di rischio utente](./media/active-directory-identityprotection/1014.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5866a-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="5866a-230">Utenti contrassegnati per il rischio</span><span class="sxs-lookup"><span data-stu-id="5866a-230">Users flagged for risk</span></span>

<span data-ttu-id="5866a-231">Tutti gli [eventi di rischio](active-directory-identity-protection-risk-events.md) attivi rilevati da Azure Active Directory per un utente rientrano nel concetto logico del rischio utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute to a logical concept called user risk.</span></span> <span data-ttu-id="5866a-232">Un utente contrassegnato per il rischio è indicativo di un account utente che potrebbe essere stato compromesso.</span><span class="sxs-lookup"><span data-stu-id="5866a-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Utenti contrassegnati per il rischio](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="5866a-234">Livello di rischio utente</span><span class="sxs-lookup"><span data-stu-id="5866a-234">User risk level</span></span>

<span data-ttu-id="5866a-235">Il livello di rischio utente può essere Alto, Medio o Basso e indica la probabilità che l'identità dell'utente sia stata compromessa.</span><span class="sxs-lookup"><span data-stu-id="5866a-235">A user risk level is an indication (High, Medium, or Low) of the likelihood that the user’s identity has been compromised.</span></span> <span data-ttu-id="5866a-236">Viene calcolato in base agli eventi di rischio utente associati all'identità di un utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-236">It is calculated based on the user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="5866a-237">Lo stato di un evento di rischio può essere **attivo** o **chiuso**.</span><span class="sxs-lookup"><span data-stu-id="5866a-237">The status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="5866a-238">Solo gli eventi di rischio **attivi** vengono conteggiati nel calcolo del livello di rischio utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-238">Only risk events that are **Active** contribute to the user risk level calculation.</span></span>

<span data-ttu-id="5866a-239">Il livello di rischio utente viene calcolato usando le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5866a-239">The user risk level is calculated using the following inputs:</span></span>

* <span data-ttu-id="5866a-240">Eventi di rischio attivi che interessano l'utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-240">Active risk events impacting the user</span></span>
* <span data-ttu-id="5866a-241">Livello di rischio di tali eventi.</span><span class="sxs-lookup"><span data-stu-id="5866a-241">Risk level of these events</span></span>
* <span data-ttu-id="5866a-242">Eventuali azioni di correzione intraprese o meno.</span><span class="sxs-lookup"><span data-stu-id="5866a-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="5866a-243">![Rischi utente](./media/active-directory-identityprotection/1031.png "Rischi utente")</span><span class="sxs-lookup"><span data-stu-id="5866a-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="5866a-244">È possibile usare i livelli di rischio utente per creare criteri di accesso condizionale che bloccano l'accesso degli utenti a rischio o per fare in modo che modifichino la password in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="5866a-244">You can use the user risk levels to create conditional access policies that block risky users from signing in, or force them to securely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="5866a-245">Chiusura manuale degli eventi di rischio</span><span class="sxs-lookup"><span data-stu-id="5866a-245">Closing risk events manually</span></span>

<span data-ttu-id="5866a-246">Nella maggior parte dei casi, per chiudere automaticamente gli eventi di rischio si procede con azioni di correzione come la reimpostazione della password di protezione.</span><span class="sxs-lookup"><span data-stu-id="5866a-246">In most cases, you will take remediation actions such as a secure password reset to automatically close risk events.</span></span> <span data-ttu-id="5866a-247">Tuttavia, questo potrebbe non essere sempre possibile.</span><span class="sxs-lookup"><span data-stu-id="5866a-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="5866a-248">Ad esempio quando:</span><span class="sxs-lookup"><span data-stu-id="5866a-248">This is, for example, the case, when:</span></span>

* <span data-ttu-id="5866a-249">Un utente con eventi di rischio attivi è stato eliminato</span><span class="sxs-lookup"><span data-stu-id="5866a-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="5866a-250">Un'analisi rivela che un evento di rischio segnalato è stato eseguito dall'utente legittimo</span><span class="sxs-lookup"><span data-stu-id="5866a-250">An investigation reveals that a reported risk event has been perform by the legitimate user</span></span>

<span data-ttu-id="5866a-251">Dal momento che gli eventi di rischio **attivi** vengono conteggiati nel calcolo del rischio utente, potrebbe essere necessario ridurre il livello di rischio chiudendo manualmente gli eventi di rischio.</span><span class="sxs-lookup"><span data-stu-id="5866a-251">Because risk events that are **Active** contribute to the user risk calculation, you may have to manually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="5866a-252">Nel corso dell'analisi è possibile eseguire una qualsiasi di queste azioni per modificare lo stato di un evento di rischio:</span><span class="sxs-lookup"><span data-stu-id="5866a-252">During the course of investigation, you can choose to take any of these actions to change the status of a risk event:</span></span>

<span data-ttu-id="5866a-253">![Azioni](./media/active-directory-identityprotection/34.png "Azioni")</span><span class="sxs-lookup"><span data-stu-id="5866a-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="5866a-254">**Risolvi** : se è stata eseguita l'azione di correzione appropriata all'esterno di Identity Protection dopo l'analisi di un evento di rischio e si ritiene che l'evento sia da considerare chiuso, contrassegnarlo come risolto.</span><span class="sxs-lookup"><span data-stu-id="5866a-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that the risk event should be considered closed, mark the event as Resolved.</span></span> <span data-ttu-id="5866a-255">Gli eventi risolti impostano lo stato dell'evento di rischio come chiuso e l'evento di rischio non viene più conteggiato nel rischio utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-255">Resolved events will set the risk event’s status to Closed and the risk event will no longer contribute to user risk.</span></span>
* <span data-ttu-id="5866a-256">**Contrassegna come falso positivo** : in alcuni casi è possibile analizzare un evento di rischio e scoprire che è stato erroneamente contrassegnato come rischioso.</span><span class="sxs-lookup"><span data-stu-id="5866a-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="5866a-257">È possibile ridurre il numero di tali occorrenze contrassegnando l'evento di rischio come falso positivo.</span><span class="sxs-lookup"><span data-stu-id="5866a-257">You can help reduce the number of such occurrences by marking the risk event as False-positive.</span></span> <span data-ttu-id="5866a-258">Questo permetterà agli algoritmi di Machine Learning di migliorare la classificazione di eventi simili in futuro.</span><span class="sxs-lookup"><span data-stu-id="5866a-258">This will help the machine learning algorithms to improve the classification of similar events in the future.</span></span> <span data-ttu-id="5866a-259">Lo stato dell'evento falso positivo viene impostato come **chiuso** e non viene più conteggiato nel rischio utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-259">The status of false-positive events is to **Closed** and they will no longer contribute to user risk.</span></span>
* <span data-ttu-id="5866a-260">**Ignora** : se non sono state intraprese azioni di correzione, ma si vuole rimuovere l'evento di rischio dall'elenco attivo, è possibile contrassegnarlo come da ignorare e il relativo stato verrà impostato come chiuso.</span><span class="sxs-lookup"><span data-stu-id="5866a-260">**Ignore** - If you have not taken any remediation action, but want the risk event to be removed from the active list, you can mark a risk event Ignore and the event status will be Closed.</span></span> <span data-ttu-id="5866a-261">Gli eventi ignorati non vengono conteggiati nel rischio utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-261">Ignored events do not contribute to user risk.</span></span> <span data-ttu-id="5866a-262">Questa opzione deve essere usata solo in circostanze particolari.</span><span class="sxs-lookup"><span data-stu-id="5866a-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="5866a-263">**Riattiva**: gli eventi di rischio che sono stati chiusi manualmente mediante **Risolvi**, **Contrassegna come falso positivo** o **Ignora**, possono essere riattivati impostando nuovamente lo stato dell'evento su **Attivo**.</span><span class="sxs-lookup"><span data-stu-id="5866a-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting the event status back to **Active**.</span></span> <span data-ttu-id="5866a-264">Gli eventi di rischio riattivati vengono conteggiati nel calcolo del livello di rischio utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-264">Reactivated risk events contribute to the user risk level calculation.</span></span> <span data-ttu-id="5866a-265">Gli eventi di rischio chiusi tramite correzione, ad esempio la reimpostazione della password di protezione, non possono essere riattivati.</span><span class="sxs-lookup"><span data-stu-id="5866a-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="5866a-266">**Per aprire la relativa finestra di dialogo di configurazione**:</span><span class="sxs-lookup"><span data-stu-id="5866a-266">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="5866a-267">Nel pannello **Azure AD Identity Protection** fare clic su **Eventi di rischio** in **Ricerca causa**.</span><span class="sxs-lookup"><span data-stu-id="5866a-267">On the **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="5866a-268">![Reimpostazione manuale della password](./media/active-directory-identityprotection/1002.png "Reimpostazione manuale della password")</span><span class="sxs-lookup"><span data-stu-id="5866a-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="5866a-269">Nell'elenco **Eventi di rischio** fare clic su un rischio.</span><span class="sxs-lookup"><span data-stu-id="5866a-269">In the **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="5866a-270">![Reimpostazione manuale della password](./media/active-directory-identityprotection/1003.png "Reimpostazione manuale della password")</span><span class="sxs-lookup"><span data-stu-id="5866a-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="5866a-271">Nel pannello dei rischi fare clic con il pulsante destro del mouse su un utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-271">On the risk blade, right-click a user.</span></span>

    <span data-ttu-id="5866a-272">![Reimpostazione manuale della password](./media/active-directory-identityprotection/1004.png "Reimpostazione manuale della password")</span><span class="sxs-lookup"><span data-stu-id="5866a-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="5866a-273">Chiusura manuale di tutti gli eventi di rischio per un utente</span><span class="sxs-lookup"><span data-stu-id="5866a-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="5866a-274">Invece di chiudere manualmente i singoli eventi di rischio per un utente, Azure Active Directory Identity Protection offre anche un metodo per chiudere tutti gli eventi per un utente con un solo clic.</span><span class="sxs-lookup"><span data-stu-id="5866a-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method to close all events for a user with one click.</span></span>

<span data-ttu-id="5866a-275">![Azioni](./media/active-directory-identityprotection/2222.png "Azioni")</span><span class="sxs-lookup"><span data-stu-id="5866a-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="5866a-276">Quando si fa clic su **Dismiss all events**(Ignora tutti gli eventi), tutti gli eventi vengono chiusi e l'utente interessato non è più a rischio.</span><span class="sxs-lookup"><span data-stu-id="5866a-276">When you click **Dismiss all events**, all events are closed and the affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="5866a-277">Correzione di eventi di rischio utente</span><span class="sxs-lookup"><span data-stu-id="5866a-277">Remediating user risk events</span></span>

<span data-ttu-id="5866a-278">Una correzione è un'azione che consente di proteggere un'identità o un dispositivo che in precedenza è stato sospettato o ritenuto essere compromesso.</span><span class="sxs-lookup"><span data-stu-id="5866a-278">A remediation is an action to secure an identity or a device that was previously suspected or known to be compromised.</span></span> <span data-ttu-id="5866a-279">Un'azione di correzione ripristina l'identità o il dispositivo a uno stato sicuro e risolve gli eventi di rischio precedenti associati all'identità o al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5866a-279">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

<span data-ttu-id="5866a-280">Per correggere gli eventi di rischio utente, è possibile:</span><span class="sxs-lookup"><span data-stu-id="5866a-280">To remediate user risk events, you can:</span></span>

* <span data-ttu-id="5866a-281">Eseguire una reimpostazione della password di protezione per correggere manualmente gli eventi di rischio utente</span><span class="sxs-lookup"><span data-stu-id="5866a-281">Perform a secure password reset to remediate user risk events manually</span></span>
* <span data-ttu-id="5866a-282">Configurare criteri di sicurezza per il rischio utente per mitigare o correggere automaticamente gli eventi di rischio utente</span><span class="sxs-lookup"><span data-stu-id="5866a-282">Configure a user risk security policy to mitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="5866a-283">Ricreare l'immagine del dispositivo infetto</span><span class="sxs-lookup"><span data-stu-id="5866a-283">Re-image the infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="5866a-284">Reimpostazione manuale della password di protezione</span><span class="sxs-lookup"><span data-stu-id="5866a-284">Manual secure password reset</span></span>
<span data-ttu-id="5866a-285">La reimpostazione della password di protezione un'azione di correzione efficace per molti eventi di rischio. Quando viene eseguita, permette di chiudere automaticamente gli eventi di rischio e ricalcolare il livello di rischio utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates the user risk level.</span></span> <span data-ttu-id="5866a-286">È possibile usare il dashboard di Identity Protection per avviare una reimpostazione della password per un utente rischioso.</span><span class="sxs-lookup"><span data-stu-id="5866a-286">You can use the Identity Protection dashboard to initiate a password reset for a risky user.</span></span>

<span data-ttu-id="5866a-287">La finestra di dialogo correlata fornisce due metodi diversi per reimpostare una password:</span><span class="sxs-lookup"><span data-stu-id="5866a-287">The related dialog provides two different methods to reset a password:</span></span>

<span data-ttu-id="5866a-288">**Reimposta password**: selezionare **Richiedi all'utente di reimpostare la password** per consentirgli di eseguire il ripristino automatico se è registrato per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="5866a-288">**Reset password** - Select **Require the user to reset their password** to allow the user to self-recover if the user has registered for multi-factor authentication.</span></span> <span data-ttu-id="5866a-289">Durante l'accesso successivo all'utente verrà richiesto di risolvere correttamente una richiesta di autenticazione a più fattori e quindi di modificare la password.</span><span class="sxs-lookup"><span data-stu-id="5866a-289">During the user's next sign-in, the user will be required to solve a multi-factor authentication challenge successfully and then, forced to change the password.</span></span> <span data-ttu-id="5866a-290">Questa opzione non è disponibile se l'account utente non è già registrato per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="5866a-290">This option isn't available if the user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="5866a-291">**Password provvisoria**: selezionare **Genera una password provvisoria** per annullare immediatamente la password esistente e creare una nuova password provvisoria per l'utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-291">**Temporary password** - Select **Generate a temporary password** to immediately invalidate the existing password, and create a new temporary password for the user.</span></span> <span data-ttu-id="5866a-292">Inviare la nuova password provvisoria a un indirizzo di posta elettronica alternativo dell'utente o al responsabile dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5866a-292">Send the new temporary password to an alternate email address for the user or to the user's manager.</span></span> <span data-ttu-id="5866a-293">La password è provvisoria, quindi verrà richiesto all'utente di modificarla al momento dell'accesso.</span><span class="sxs-lookup"><span data-stu-id="5866a-293">Because the password is temporary, the user will be prompted to change the password upon sign-in.</span></span>

<span data-ttu-id="5866a-294">![Criteri](./media/active-directory-identityprotection/1005.png "Criteri")</span><span class="sxs-lookup"><span data-stu-id="5866a-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="5866a-295">**Per aprire la relativa finestra di dialogo di configurazione**:</span><span class="sxs-lookup"><span data-stu-id="5866a-295">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="5866a-296">Nel pannello **Azure AD Identity Protection** fare clic su **Utenti contrassegnati per il rischio**.</span><span class="sxs-lookup"><span data-stu-id="5866a-296">On the **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="5866a-297">![Reimpostazione manuale della password](./media/active-directory-identityprotection/1006.png "Reimpostazione manuale della password")</span><span class="sxs-lookup"><span data-stu-id="5866a-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="5866a-298">Dall'elenco di utenti selezionare un utente con almeno un evento di rischio.</span><span class="sxs-lookup"><span data-stu-id="5866a-298">From the list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="5866a-299">![Reimpostazione manuale della password](./media/active-directory-identityprotection/1007.png "Reimpostazione manuale della password")</span><span class="sxs-lookup"><span data-stu-id="5866a-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="5866a-300">Nel pannello dell'utente fare clic su **Reimposta password**.</span><span class="sxs-lookup"><span data-stu-id="5866a-300">On the user blade, click **Reset password**.</span></span>

    <span data-ttu-id="5866a-301">![Reimpostazione manuale della password](./media/active-directory-identityprotection/1008.png "Reimpostazione manuale della password")</span><span class="sxs-lookup"><span data-stu-id="5866a-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="5866a-302">Criteri di sicurezza per il rischio utente</span><span class="sxs-lookup"><span data-stu-id="5866a-302">User risk security policy</span></span>
<span data-ttu-id="5866a-303">I criteri di sicurezza per il rischio utente sono criteri di accesso condizionale che valutano il livello di rischio per un utente specifico e applicano azioni di correzione e mitigazione dei rischi in base a regole e condizioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="5866a-303">A user risk security policy is a conditional access policy that evaluates the risk level to a specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="5866a-304">![Criteri di rischio utente](./media/active-directory-identityprotection/1009.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5866a-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="5866a-305">Azure AD Identity Protection consente di gestire le azioni di mitigazione e correzione per gli utenti contrassegnati per il rischio seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5866a-305">Azure AD Identity Protection helps you manage the mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="5866a-306">Impostare gli utenti e i gruppi a cui vengono applicati i criteri:</span><span class="sxs-lookup"><span data-stu-id="5866a-306">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="5866a-307">![Criteri di rischio utente](./media/active-directory-identityprotection/1010.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5866a-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="5866a-308">Impostare la soglia del livello di rischio utente, bassa, media o alta, che attiva il criterio:</span><span class="sxs-lookup"><span data-stu-id="5866a-308">Set the user risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="5866a-309">![Criteri di rischio utente](./media/active-directory-identityprotection/1011.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5866a-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="5866a-310">Impostare i controlli da applicare quando viene attivato il criterio:</span><span class="sxs-lookup"><span data-stu-id="5866a-310">Set the controls to be enforced when the policy triggers:</span></span>

    <span data-ttu-id="5866a-311">![Criteri di rischio utente](./media/active-directory-identityprotection/1012.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5866a-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="5866a-312">Cambiare lo stato dei criteri:</span><span class="sxs-lookup"><span data-stu-id="5866a-312">Switch the state of your policy:</span></span>

    <span data-ttu-id="5866a-313">![Criteri di rischio utente](./media/active-directory-identityprotection/403.png "Registrazione MFA")</span><span class="sxs-lookup"><span data-stu-id="5866a-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="5866a-314">Esaminare e valutare l'impatto di una modifica prima di attivarla:</span><span class="sxs-lookup"><span data-stu-id="5866a-314">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="5866a-315">![Criteri di rischio utente](./media/active-directory-identityprotection/1013.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5866a-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="5866a-316">La scelta di una soglia **alta** riduce la frequenza di attivazione dei criteri e riduce al minimo l'impatto sugli utenti.</span><span class="sxs-lookup"><span data-stu-id="5866a-316">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>
<span data-ttu-id="5866a-317">Esclude tuttavia dai criteri gli utenti contrassegnati per il rischio con una soglia **bassa** o **media**. Questa scelta può non garantire la protezione delle identità o dei dispositivi in precedenza sospettati di essere compromessi o noti come compromessi.</span><span class="sxs-lookup"><span data-stu-id="5866a-317">However, it excludes **Low** and **Medium** users flagged for risk from the policy, which may not secure identities or devices that were previously suspected or known to be compromised.</span></span>

<span data-ttu-id="5866a-318">Quando si impostano i criteri:</span><span class="sxs-lookup"><span data-stu-id="5866a-318">When setting the policy,</span></span>

* <span data-ttu-id="5866a-319">Escludere gli utenti che possono generare molti falsi positivi, ad esempio sviluppatori o analisti della sicurezza</span><span class="sxs-lookup"><span data-stu-id="5866a-319">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="5866a-320">Escludere gli utenti con impostazioni locali in cui abilitare i criteri non è pratico, ad esempio per la mancanza di accesso al supporto tecnico</span><span class="sxs-lookup"><span data-stu-id="5866a-320">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="5866a-321">Usare una soglia **alta** durante il rollout iniziale dei criteri o se è necessario ridurre al minimo gli avvisi visualizzati dagli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="5866a-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="5866a-322">Usare una soglia **bassa** se l'organizzazione richiede una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5866a-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="5866a-323">La scelta di una soglia **bassa** introduce richieste di accesso aggiuntive per l'utente, ma garantisce una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5866a-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="5866a-324">L'impostazione predefinita consigliata per la maggior parte delle organizzazioni è la configurazione di una regola per una soglia **media** , che permette di bilanciare usabilità e sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5866a-324">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="5866a-325">Per una panoramica dell'esperienza utente correlata, vedere:</span><span class="sxs-lookup"><span data-stu-id="5866a-325">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="5866a-326">[Flusso di ripristino di account compromessi](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="5866a-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="5866a-327">[Flusso di account compromessi bloccati](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="5866a-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="5866a-328">**Per aprire la relativa finestra di dialogo di configurazione**:</span><span class="sxs-lookup"><span data-stu-id="5866a-328">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="5866a-329">Nel pannello **Azure AD Identity Protection** fare clic su **Criteri di rischio utente** nella sezione **Configura**.</span><span class="sxs-lookup"><span data-stu-id="5866a-329">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="5866a-330">![Criteri di rischio utente](./media/active-directory-identityprotection/1009.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5866a-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="5866a-331">Mitigazione di eventi di rischio utente</span><span class="sxs-lookup"><span data-stu-id="5866a-331">Mitigating user risk events</span></span>
<span data-ttu-id="5866a-332">Gli amministratori possono impostare criteri di sicurezza per il rischio utente per bloccare gli utenti al momento dell'accesso in base al livello di rischio.</span><span class="sxs-lookup"><span data-stu-id="5866a-332">Administrators can set a user risk security policy to block users upon sign-in depending on the risk level.</span></span>

<span data-ttu-id="5866a-333">Il blocco dell'accesso:</span><span class="sxs-lookup"><span data-stu-id="5866a-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="5866a-334">Impedisce la generazione di nuovi eventi di rischio utente per l'utente interessato</span><span class="sxs-lookup"><span data-stu-id="5866a-334">Prevents the generation of new user risk events for the affected user</span></span>
* <span data-ttu-id="5866a-335">Consente agli amministratori di correggere manualmente gli eventi di rischio che interessano l'identità dell'utente e di ripristinarne lo stato protetto</span><span class="sxs-lookup"><span data-stu-id="5866a-335">Enables administrators to manually remediate the risk events affecting the user's identity and restore it to a secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="5866a-336">Criteri di registrazione per l'autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="5866a-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="5866a-337">Azure Multi-Factor Authentication è un metodo di verifica dell'identità dell'utente che richiede l'uso di più fattori, oltre a un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="5866a-337">Azure multi-factor authentication is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="5866a-338">Fornisce un secondo livello di sicurezza agli accessi e alle transazioni degli utenti.</span><span class="sxs-lookup"><span data-stu-id="5866a-338">It provides a second layer of security to user sign-ins and transactions.</span></span>  
<span data-ttu-id="5866a-339">È consigliabile richiedere l'autenticazione a più fattori per l'accesso degli utenti perché:</span><span class="sxs-lookup"><span data-stu-id="5866a-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="5866a-340">Offre un'autenticazione avanzata con una gamma di opzioni di verifica semplici</span><span class="sxs-lookup"><span data-stu-id="5866a-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="5866a-341">Svolge un ruolo chiave nella preparazione dell'organizzazione per le operazioni di protezione e ripristino in caso di compromissione degli account</span><span class="sxs-lookup"><span data-stu-id="5866a-341">Plays a key role in preparing your organization to protect and recover from account compromises</span></span>

<span data-ttu-id="5866a-342">![Criteri di rischio utente](./media/active-directory-identityprotection/1019.png "Criteri di rischio utente")</span><span class="sxs-lookup"><span data-stu-id="5866a-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="5866a-343">Per altre informazioni, vedere la pagina relativa ad [Informazioni su Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="5866a-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="5866a-344">Azure AD Identity Protection permette di gestire il rollout della registrazione per l'autenticazione a più fattori con la configurazione di criteri che consentono di:</span><span class="sxs-lookup"><span data-stu-id="5866a-344">Azure AD Identity Protection helps you manage the roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="5866a-345">Impostare gli utenti e i gruppi a cui vengono applicati i criteri:</span><span class="sxs-lookup"><span data-stu-id="5866a-345">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="5866a-346">![Criteri MFA](./media/active-directory-identityprotection/1020.png "Criteri MFA")</span><span class="sxs-lookup"><span data-stu-id="5866a-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="5866a-347">Impostare i controlli da applicare quando viene attivato il criterio:</span><span class="sxs-lookup"><span data-stu-id="5866a-347">Set the controls to be enforced when the policy triggers::</span></span>  

    <span data-ttu-id="5866a-348">![Criteri MFA](./media/active-directory-identityprotection/1021.png "Criteri MFA")</span><span class="sxs-lookup"><span data-stu-id="5866a-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="5866a-349">Cambiare lo stato dei criteri:</span><span class="sxs-lookup"><span data-stu-id="5866a-349">Switch the state of your policy:</span></span>

    <span data-ttu-id="5866a-350">![Criteri MFA](./media/active-directory-identityprotection/403.png "Criteri MFA")</span><span class="sxs-lookup"><span data-stu-id="5866a-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="5866a-351">Visualizzare lo stato di registrazione corrente:</span><span class="sxs-lookup"><span data-stu-id="5866a-351">View the current registration status:</span></span>

    <span data-ttu-id="5866a-352">![Criteri MFA](./media/active-directory-identityprotection/1022.png "Criteri MFA")</span><span class="sxs-lookup"><span data-stu-id="5866a-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="5866a-353">Per una panoramica dell'esperienza utente correlata, vedere:</span><span class="sxs-lookup"><span data-stu-id="5866a-353">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="5866a-354">[Flusso di registrazione per l'autenticazione a più fattori](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="5866a-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="5866a-355">[Esperienze di accesso con Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="5866a-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="5866a-356">**Per aprire la relativa finestra di dialogo di configurazione**:</span><span class="sxs-lookup"><span data-stu-id="5866a-356">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="5866a-357">Nel pannello **Azure AD Identity Protection** fare clic su **Criteri di registrazione per l'autenticazione a più fattori** nella sezione **Configura**.</span><span class="sxs-lookup"><span data-stu-id="5866a-357">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="5866a-358">![Criteri MFA](./media/active-directory-identityprotection/1019.png "Criteri MFA")</span><span class="sxs-lookup"><span data-stu-id="5866a-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="5866a-359">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5866a-359">Next steps</span></span>
* [<span data-ttu-id="5866a-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span><span class="sxs-lookup"><span data-stu-id="5866a-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="5866a-361">Abilitazione di Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5866a-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="5866a-362">Vulnerabilità rilevate da Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5866a-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="5866a-363">Eventi di rischio di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5866a-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="5866a-364">Notifiche di Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5866a-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="5866a-365">Studio di Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5866a-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="5866a-366">Glossario di Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5866a-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="5866a-367">Esperienze di accesso con Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5866a-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="5866a-368">Azure Active Directory Identity Protection: come sbloccare gli utenti</span><span class="sxs-lookup"><span data-stu-id="5866a-368">Azure Active Directory Identity Protection - How to unblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="5866a-369">Introduzione ad Azure Active Directory Identity Protection e a Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="5866a-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
