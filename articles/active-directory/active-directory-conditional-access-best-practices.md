---
title: Procedure consigliate per l'accesso condizionale in Azure Active Directory | Microsoft Docs
description: "Informazioni sugli aspetti da conoscere e su ciò che è consigliabile evitare quando si configurano i criteri di accesso condizionale."
services: active-directory
keywords: accesso condizionale alle app, accesso condizionale con Azure AD, accesso sicuro alle risorse aziendali, criteri di accesso condizionale
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 3e524c116479c1af6eb6a601c9b57d27a697c5a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="01024-104">Procedure consigliate per l'accesso condizionale in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01024-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="01024-105">Questo argomento fornisce informazioni sugli aspetti da conoscere e su ciò che è consigliabile evitare quando si configurano i criteri di accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="01024-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="01024-106">Prima di procedere nella lettura, occorre acquisire familiarità con i concetti e la terminologia descritti in [Accesso condizionale in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="01024-106">Before reading this topic, you should familiarize yourself with the concepts and the terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="01024-107">Informazioni utili</span><span class="sxs-lookup"><span data-stu-id="01024-107">What you should know</span></span>

### <a name="whats-required-to-make-a-policy-work"></a><span data-ttu-id="01024-108">Elementi necessari per il funzionamento di un criterio</span><span class="sxs-lookup"><span data-stu-id="01024-108">What’s required to make a policy work?</span></span>

<span data-ttu-id="01024-109">Quando si crea un nuovo criterio, non sono selezionti utenti, gruppi, app o controlli di accesso.</span><span class="sxs-lookup"><span data-stu-id="01024-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![App cloud](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="01024-111">Per far funzionare il criterio, è necessario configurare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="01024-111">To make your policy work, you must configure the following:</span></span>


|<span data-ttu-id="01024-112">Cosa</span><span class="sxs-lookup"><span data-stu-id="01024-112">What</span></span>           | <span data-ttu-id="01024-113">Come</span><span class="sxs-lookup"><span data-stu-id="01024-113">How</span></span>                                  | <span data-ttu-id="01024-114">Motivo</span><span class="sxs-lookup"><span data-stu-id="01024-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="01024-115">**App cloud**</span><span class="sxs-lookup"><span data-stu-id="01024-115">**Cloud apps**</span></span> |<span data-ttu-id="01024-116">È necessario selezionare una o più app.</span><span class="sxs-lookup"><span data-stu-id="01024-116">You need to select one or more apps.</span></span>  | <span data-ttu-id="01024-117">L'obiettivo di un criterio di accesso condizionale è consentire di ottimizzare il modo in cui gli utenti autorizzati possono accedere alle app.</span><span class="sxs-lookup"><span data-stu-id="01024-117">The goal of a conditional access policy is to enable you to fine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="01024-118">**Utenti e gruppi**</span><span class="sxs-lookup"><span data-stu-id="01024-118">**Users and groups**</span></span> | <span data-ttu-id="01024-119">È necessario selezionare almeno un utente o gruppo che è autorizzato ad accedere alle app cloud selezionate.</span><span class="sxs-lookup"><span data-stu-id="01024-119">You need to select at least one user or group that is authorized to access the cloud apps you have selected.</span></span> | <span data-ttu-id="01024-120">Un criterio di accesso condizionale a cui non sono assegnati utenti e gruppi non viene mai attivato.</span><span class="sxs-lookup"><span data-stu-id="01024-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="01024-121">**Controlli di accesso**</span><span class="sxs-lookup"><span data-stu-id="01024-121">**Access controls**</span></span> | <span data-ttu-id="01024-122">È necessario selezionare almeno un controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="01024-122">You need to select at least one access control.</span></span> | <span data-ttu-id="01024-123">Il processore del criterio deve sapere cosa fare se vengono soddisfatte le condizioni.</span><span class="sxs-lookup"><span data-stu-id="01024-123">Your policy processor needs to know what to do if your conditions are satisfied.</span></span>|


<span data-ttu-id="01024-124">Oltre a questi requisiti di base, in molti casi è necessario anche configurare una condizione.</span><span class="sxs-lookup"><span data-stu-id="01024-124">In addition to these basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="01024-125">Mentre un criterio funzionerebbe anche senza una condizione configurata, le condizioni rappresentano il fattore determinante per ottimizzare l'accesso alle app.</span><span class="sxs-lookup"><span data-stu-id="01024-125">While a policy would also work without a configured condition, conditions are the driving factor for fine-tuning access to your apps.</span></span>


![App cloud](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="01024-127">Come vengono valutate le assegnazioni?</span><span class="sxs-lookup"><span data-stu-id="01024-127">How are assignments evaluated?</span></span>

<span data-ttu-id="01024-128">Tutte le assegnazioni vengono collegate logicamente con l'operatore **AND**.</span><span class="sxs-lookup"><span data-stu-id="01024-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="01024-129">Se è configurata più di un'assegnazione, per attivare un criterio, devono essere soddisfatte tutte le assegnazioni.</span><span class="sxs-lookup"><span data-stu-id="01024-129">If you have more than one assignment configured, to trigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="01024-130">Se è necessario configurare una condizione della località che si applica a tutte le connessioni stabilite dall'esterno della rete dell'organizzazione, è possibile:</span><span class="sxs-lookup"><span data-stu-id="01024-130">If you need to configure a location condition that applies to all connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="01024-131">Includere **Tutte le località**</span><span class="sxs-lookup"><span data-stu-id="01024-131">Including **All locations**</span></span>
- <span data-ttu-id="01024-132">Escludere **Tutti gli indirizzi IP attendibili**</span><span class="sxs-lookup"><span data-stu-id="01024-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-the-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="01024-133">Che cosa accade se sono configurati criteri nel portale di Azure classico e nel portale di Azure?</span><span class="sxs-lookup"><span data-stu-id="01024-133">What happens if you have policies in the Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="01024-134">Entrambi i criteri vengono applicati da Azure Active Directory e l'utente ottiene l'accesso solo quando tutti i requisiti vengono soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="01024-134">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-the-intune-silverlight-portal-and-the-azure-portal"></a><span data-ttu-id="01024-135">Che cosa accade se sono presenti criteri nel portale di Intune Silverlight e nel portale di Azure?</span><span class="sxs-lookup"><span data-stu-id="01024-135">What happens if you have policies in the Intune Silverlight portal and the Azure Portal?</span></span>
<span data-ttu-id="01024-136">Entrambi i criteri vengono applicati da Azure Active Directory e l'utente ottiene l'accesso solo quando tutti i requisiti vengono soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="01024-136">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-the-same-user-configured"></a><span data-ttu-id="01024-137">Che cosa accade se sono configurati più criteri per lo stesso utente?</span><span class="sxs-lookup"><span data-stu-id="01024-137">What happens if I have multiple policies for the same user configured?</span></span>  
<span data-ttu-id="01024-138">Per ogni accesso, Azure Active Directory valuta tutti i criteri e verifica che tutti i requisiti vengano soddisfatti prima di concedere l'accesso all'utente.</span><span class="sxs-lookup"><span data-stu-id="01024-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access to the user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="01024-139">L'accesso condizionale funziona con Exchange ActiveSync?</span><span class="sxs-lookup"><span data-stu-id="01024-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="01024-140">Sì, è possibile usare Exchange ActiveSync in criteri di accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="01024-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="01024-141">Azioni da evitare</span><span class="sxs-lookup"><span data-stu-id="01024-141">What you should avoid doing</span></span>

<span data-ttu-id="01024-142">Il framework di accesso condizionale offre ottima flessibilità di configurazione.</span><span class="sxs-lookup"><span data-stu-id="01024-142">The conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="01024-143">Tuttavia, questa flessibilità ideale comporta anche che è opportuno esaminare attentamente ogni criterio di configurazione prima che venga rilasciato, in modo da evitare risultati indesiderati.</span><span class="sxs-lookup"><span data-stu-id="01024-143">However, great flexibility  also means that you should carefully review each configuration policy prior to releasing it to avoid undesirable results.</span></span> <span data-ttu-id="01024-144">In questo contesto, è necessario prestare particolare attenzione alle assegnazioni che interessano set completi, ad esempio **tutti gli utenti/i gruppi/le applicazioni cloud**.</span><span class="sxs-lookup"><span data-stu-id="01024-144">In this context, you should pay special attention to assignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="01024-145">Nell'ambiente, è necessario evitare le seguenti configurazioni:</span><span class="sxs-lookup"><span data-stu-id="01024-145">In your environment, you should avoid the following configurations:</span></span>


<span data-ttu-id="01024-146">**Per tutti gli utenti e tutte le applicazioni cloud:**</span><span class="sxs-lookup"><span data-stu-id="01024-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="01024-147">**Blocca accesso**: questa configurazione consente di bloccare l'intera organizzazione. Un'idea chiaramente non buona.</span><span class="sxs-lookup"><span data-stu-id="01024-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="01024-148">**Richiedi un dispositivo conforme**: per gli utenti che non hanno ancora registrato i propri dispositivi, questo criterio blocca tutti gli accessi, tra cui l'accesso al portale di Intune.</span><span class="sxs-lookup"><span data-stu-id="01024-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access to the Intune portal.</span></span> <span data-ttu-id="01024-149">Se l'utente è amministratore senza un dispositivo registrato, questo criterio blocca l'accesso al portale di Azure per la modifica dei criteri.</span><span class="sxs-lookup"><span data-stu-id="01024-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into the Azure portal to change the policy.</span></span>

- <span data-ttu-id="01024-150">**Require domain join** (Richiedi aggiunta a dominio): se ancora non si dispone di un dispositivo aggiunto al dominio, questo criterio di blocco dell'accesso è anche in grado di bloccare l'accesso per tutti gli utenti nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="01024-150">**Require domain join** - This policy block access has also the potential to block access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="01024-151">**Per tutti gli utenti, tutte le applicazioni cloud e tutte le piattaforme per dispositivi:**</span><span class="sxs-lookup"><span data-stu-id="01024-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="01024-152">**Blocca accesso**: questa configurazione consente di bloccare l'intera organizzazione. Un'idea chiaramente non buona.</span><span class="sxs-lookup"><span data-stu-id="01024-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="01024-153">Scenari comuni</span><span class="sxs-lookup"><span data-stu-id="01024-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="01024-154">Richiesta dell'autenticazione a più fattori per le app</span><span class="sxs-lookup"><span data-stu-id="01024-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="01024-155">Diversi ambienti hanno app che richiedono un livello di protezione maggiore delle altre,</span><span class="sxs-lookup"><span data-stu-id="01024-155">Many environments have apps requiring a higher level of protection than the others.</span></span>
<span data-ttu-id="01024-156">ad esempio, app che hanno accesso a dati sensibili.</span><span class="sxs-lookup"><span data-stu-id="01024-156">This is, for example, the case for apps that have access to sensitive data.</span></span>
<span data-ttu-id="01024-157">Per aggiungere un altro livello di protezione a queste app, è possibile configurare un criterio di accesso condizionale che richiede l'autenticazione a più fattori quando gli utenti accedono a queste app.</span><span class="sxs-lookup"><span data-stu-id="01024-157">If you want to add another layer of protection to these apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="01024-158">Richiesta dell'autenticazione a più fattori per l'accesso da reti non considerate attendibili</span><span class="sxs-lookup"><span data-stu-id="01024-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="01024-159">Questo scenario è simile a quello precedente perché aggiunge un requisito per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="01024-159">This scenario is similar to the previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="01024-160">La differenza principale è tuttavia la condizione per questo requisito.</span><span class="sxs-lookup"><span data-stu-id="01024-160">However, the main difference is the condition for this requirement.</span></span>  
<span data-ttu-id="01024-161">Mentre l'elemento essenziale dello scenario precedente sono le app con accesso a dati sensibili, in questo scenario l'elemento essenziale sono le località attendibili.</span><span class="sxs-lookup"><span data-stu-id="01024-161">While the focus of the previous scenario was on apps with access to sensitve data, the focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="01024-162">In altre parole, è possibile avere un requisito per l'autenticazione a più fattori se un'app è accessibile a un utente da una rete non considerata attendibile.</span><span class="sxs-lookup"><span data-stu-id="01024-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="01024-163">Solo i dispositivi attendibili possono accedere ai servizi di Office 365</span><span class="sxs-lookup"><span data-stu-id="01024-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="01024-164">Se si usa Intune nell'ambiente, è possibile iniziare immediatamente a usare l'interfaccia del criterio di accesso condizionale nella console Azure.</span><span class="sxs-lookup"><span data-stu-id="01024-164">If you are using Intune in your environment, you can immediately start using the conditional access policy interface in the Azure console.</span></span>

<span data-ttu-id="01024-165">Molti clienti Intune usano l'accesso condizionale per assicurarsi che solo i dispositivi attendibili possano accedere a Office 365.</span><span class="sxs-lookup"><span data-stu-id="01024-165">Many Intune customers are using conditional access to ensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="01024-166">Di conseguenza i dispositivi mobili vengono registrati con Intune e soddisfano i requisiti dei criteri di conformità e i PC Windows vengono aggiunti e un dominio locale.</span><span class="sxs-lookup"><span data-stu-id="01024-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined to an on-premises domain.</span></span> <span data-ttu-id="01024-167">Un importante miglioramento consiste nel fatto che non è necessario impostare lo stesso criterio per ogni servizio di Office 365.</span><span class="sxs-lookup"><span data-stu-id="01024-167">A key improvement is that you do not have to set the same policy for each of the Office 365 services.</span></span>  <span data-ttu-id="01024-168">Quando si crea un nuovo criterio, configurare le app per cloud per includere ogni app di O365 che si vuole proteggere con l'accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="01024-168">When you create a new policy, configure the Cloud apps to include each of the O365 apps that you wish to protect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01024-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="01024-169">Next steps</span></span>

<span data-ttu-id="01024-170">Per informazioni su come configurare un criterio di accesso condizionale, vedere [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md) (Introduzione all'accesso condizionale in Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="01024-170">If you want to know how to configure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
