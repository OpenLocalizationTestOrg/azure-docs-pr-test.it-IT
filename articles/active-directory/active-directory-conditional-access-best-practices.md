---
title: aaaBest procedure consigliate per l'accesso condizionale in Azure Active Directory | Documenti Microsoft
description: "Informazioni sugli aspetti da conoscere e su ciò che è consigliabile evitare quando si configurano i criteri di accesso condizionale."
services: active-directory
keywords: accesso condizionale tooapps, l'accesso condizionale con Azure AD, proteggere l'accesso alle risorse toocompany, criteri di accesso condizionale
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
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="719b9-104">Procedure consigliate per l'accesso condizionale in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="719b9-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="719b9-105">Questo argomento fornisce informazioni sugli aspetti da conoscere e su ciò che è consigliabile evitare quando si configurano i criteri di accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="719b9-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="719b9-106">Prima di leggere questo argomento, è consigliabile acquisire familiarità con concetti hello e terminologia hello descritte nella [accesso condizionale in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="719b9-106">Before reading this topic, you should familiarize yourself with hello concepts and hello terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="719b9-107">Informazioni utili</span><span class="sxs-lookup"><span data-stu-id="719b9-107">What you should know</span></span>

### <a name="whats-required-toomake-a-policy-work"></a><span data-ttu-id="719b9-108">Le impostazioni necessarie toomake un lavoro criteri?</span><span class="sxs-lookup"><span data-stu-id="719b9-108">What’s required toomake a policy work?</span></span>

<span data-ttu-id="719b9-109">Quando si crea un nuovo criterio, non sono selezionti utenti, gruppi, app o controlli di accesso.</span><span class="sxs-lookup"><span data-stu-id="719b9-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![App cloud](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="719b9-111">i criteri di toomake lavoro, è necessario configurare l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="719b9-111">toomake your policy work, you must configure hello following:</span></span>


|<span data-ttu-id="719b9-112">Cosa</span><span class="sxs-lookup"><span data-stu-id="719b9-112">What</span></span>           | <span data-ttu-id="719b9-113">Come</span><span class="sxs-lookup"><span data-stu-id="719b9-113">How</span></span>                                  | <span data-ttu-id="719b9-114">Motivo</span><span class="sxs-lookup"><span data-stu-id="719b9-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="719b9-115">**App cloud**</span><span class="sxs-lookup"><span data-stu-id="719b9-115">**Cloud apps**</span></span> |<span data-ttu-id="719b9-116">È necessario tooselect una o più app.</span><span class="sxs-lookup"><span data-stu-id="719b9-116">You need tooselect one or more apps.</span></span>  | <span data-ttu-id="719b9-117">obiettivo di Hello di criteri di accesso condizionale è tooenable è ottimizzare toofine come gli utenti autorizzati possono accedere le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="719b9-117">hello goal of a conditional access policy is tooenable you toofine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="719b9-118">**Utenti e gruppi**</span><span class="sxs-lookup"><span data-stu-id="719b9-118">**Users and groups**</span></span> | <span data-ttu-id="719b9-119">È necessario tooselect almeno un utente o gruppo che è autorizzato tooaccess hello cloud App è stata selezionata.</span><span class="sxs-lookup"><span data-stu-id="719b9-119">You need tooselect at least one user or group that is authorized tooaccess hello cloud apps you have selected.</span></span> | <span data-ttu-id="719b9-120">Un criterio di accesso condizionale a cui non sono assegnati utenti e gruppi non viene mai attivato.</span><span class="sxs-lookup"><span data-stu-id="719b9-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="719b9-121">**Controlli di accesso**</span><span class="sxs-lookup"><span data-stu-id="719b9-121">**Access controls**</span></span> | <span data-ttu-id="719b9-122">È necessario tooselect almeno un controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="719b9-122">You need tooselect at least one access control.</span></span> | <span data-ttu-id="719b9-123">Il processore di criteri deve tooknow quali toodo se vengono soddisfatte le condizioni.</span><span class="sxs-lookup"><span data-stu-id="719b9-123">Your policy processor needs tooknow what toodo if your conditions are satisfied.</span></span>|


<span data-ttu-id="719b9-124">Aggiunta toothese base dei requisiti, in molti casi, è necessario configurare anche una condizione.</span><span class="sxs-lookup"><span data-stu-id="719b9-124">In addition toothese basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="719b9-125">Mentre un criterio funzionerebbe anche senza una condizione configurata, le condizioni sono un fattore determinante per l'ottimizzazione di accesso tooyour App hello.</span><span class="sxs-lookup"><span data-stu-id="719b9-125">While a policy would also work without a configured condition, conditions are hello driving factor for fine-tuning access tooyour apps.</span></span>


![App cloud](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="719b9-127">Come vengono valutate le assegnazioni?</span><span class="sxs-lookup"><span data-stu-id="719b9-127">How are assignments evaluated?</span></span>

<span data-ttu-id="719b9-128">Tutte le assegnazioni vengono collegate logicamente con l'operatore **AND**.</span><span class="sxs-lookup"><span data-stu-id="719b9-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="719b9-129">Se si dispone di più di un'assegnazione configurata, tootrigger un criterio, tutte le assegnazioni devono essere soddisfatta.</span><span class="sxs-lookup"><span data-stu-id="719b9-129">If you have more than one assignment configured, tootrigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="719b9-130">Se è necessario tooconfigure una condizione di percorso che applica le connessioni tooall effettuate all'esterno della rete aziendale, è possibile farlo da:</span><span class="sxs-lookup"><span data-stu-id="719b9-130">If you need tooconfigure a location condition that applies tooall connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="719b9-131">Includere **Tutte le località**</span><span class="sxs-lookup"><span data-stu-id="719b9-131">Including **All locations**</span></span>
- <span data-ttu-id="719b9-132">Escludere **Tutti gli indirizzi IP attendibili**</span><span class="sxs-lookup"><span data-stu-id="719b9-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="719b9-133">Cosa accade se si dispone di criteri nel portale di Azure classico hello e portale di Azure configurato.</span><span class="sxs-lookup"><span data-stu-id="719b9-133">What happens if you have policies in hello Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="719b9-134">Entrambi i criteri vengono applicati da Azure Active Directory e hello utente ottiene l'accesso solo quando tutti i requisiti.</span><span class="sxs-lookup"><span data-stu-id="719b9-134">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a><span data-ttu-id="719b9-135">Cosa accade se si dispone di criteri nel portale Silverlight di Intune hello e hello portale di Azure?</span><span class="sxs-lookup"><span data-stu-id="719b9-135">What happens if you have policies in hello Intune Silverlight portal and hello Azure Portal?</span></span>
<span data-ttu-id="719b9-136">Entrambi i criteri vengono applicati da Azure Active Directory e hello utente ottiene l'accesso solo quando tutti i requisiti.</span><span class="sxs-lookup"><span data-stu-id="719b9-136">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a><span data-ttu-id="719b9-137">Cosa accade se si dispone di più criteri per hello configurato dall'utente stesso.</span><span class="sxs-lookup"><span data-stu-id="719b9-137">What happens if I have multiple policies for hello same user configured?</span></span>  
<span data-ttu-id="719b9-138">Per ogni accesso, Azure Active Directory restituisce tutti i criteri e assicura che tutti i requisiti siano soddisfatti prima che l'utente di toohello concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="719b9-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access toohello user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="719b9-139">L'accesso condizionale funziona con Exchange ActiveSync?</span><span class="sxs-lookup"><span data-stu-id="719b9-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="719b9-140">Sì, è possibile usare Exchange ActiveSync in criteri di accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="719b9-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="719b9-141">Azioni da evitare</span><span class="sxs-lookup"><span data-stu-id="719b9-141">What you should avoid doing</span></span>

<span data-ttu-id="719b9-142">il framework di accesso condizionale Hello offre la flessibilità di una configurazione ottimale.</span><span class="sxs-lookup"><span data-stu-id="719b9-142">hello conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="719b9-143">Tuttavia, una grande flessibilità significa anche che è opportuno esaminare attentamente ogni criterio di configurazione precedente tooreleasing è tooavoid di risultati non desiderabili.</span><span class="sxs-lookup"><span data-stu-id="719b9-143">However, great flexibility  also means that you should carefully review each configuration policy prior tooreleasing it tooavoid undesirable results.</span></span> <span data-ttu-id="719b9-144">In questo contesto, è necessario prestare particolare attenzione tooassignments che interessano un set completo, ad esempio **tutti gli utenti / gruppi / App cloud**.</span><span class="sxs-lookup"><span data-stu-id="719b9-144">In this context, you should pay special attention tooassignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="719b9-145">Nell'ambiente in uso, è necessario evitare hello seguenti configurazioni:</span><span class="sxs-lookup"><span data-stu-id="719b9-145">In your environment, you should avoid hello following configurations:</span></span>


<span data-ttu-id="719b9-146">**Per tutti gli utenti e tutte le applicazioni cloud:**</span><span class="sxs-lookup"><span data-stu-id="719b9-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="719b9-147">**Blocca accesso**: questa configurazione consente di bloccare l'intera organizzazione. Un'idea chiaramente non buona.</span><span class="sxs-lookup"><span data-stu-id="719b9-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="719b9-148">**Richiede un dispositivo conforme** - per gli utenti che non hanno registrato i dispositivi ancora, questo criterio blocca tutti gli accessi inclusi accesso toohello Intune portale.</span><span class="sxs-lookup"><span data-stu-id="719b9-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access toohello Intune portal.</span></span> <span data-ttu-id="719b9-149">Se si è un amministratore senza un dispositivo registrato, questo criterio verrà bloccata dal rimettersi in Criteri di hello hello toochange portale Azure.</span><span class="sxs-lookup"><span data-stu-id="719b9-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into hello Azure portal toochange hello policy.</span></span>

- <span data-ttu-id="719b9-150">**Richiedere l'aggiunta a dominio** : questo blocco criteri accesso ha inoltre hello potenziali tooblock accesso per tutti gli utenti nell'organizzazione se non si dispone ancora di un dispositivo aggiunto al dominio.</span><span class="sxs-lookup"><span data-stu-id="719b9-150">**Require domain join** - This policy block access has also hello potential tooblock access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="719b9-151">**Per tutti gli utenti, tutte le applicazioni cloud e tutte le piattaforme per dispositivi:**</span><span class="sxs-lookup"><span data-stu-id="719b9-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="719b9-152">**Blocca accesso**: questa configurazione consente di bloccare l'intera organizzazione. Un'idea chiaramente non buona.</span><span class="sxs-lookup"><span data-stu-id="719b9-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="719b9-153">Scenari comuni</span><span class="sxs-lookup"><span data-stu-id="719b9-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="719b9-154">Richiesta dell'autenticazione a più fattori per le app</span><span class="sxs-lookup"><span data-stu-id="719b9-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="719b9-155">Molti ambienti dispongono di applicazioni che richiedono un livello di protezione maggiore rispetto a hello ad altri utenti.</span><span class="sxs-lookup"><span data-stu-id="719b9-155">Many environments have apps requiring a higher level of protection than hello others.</span></span>
<span data-ttu-id="719b9-156">Questo accade, ad esempio, hello per le applicazioni che dispongono di accesso toosensitive dati.</span><span class="sxs-lookup"><span data-stu-id="719b9-156">This is, for example, hello case for apps that have access toosensitive data.</span></span>
<span data-ttu-id="719b9-157">Se si desidera tooadd un ulteriore livello di protezione toothese App, è possibile configurare un criterio di accesso condizionale che richiede l'autenticazione a più fattori quando gli utenti accedono a tali app.</span><span class="sxs-lookup"><span data-stu-id="719b9-157">If you want tooadd another layer of protection toothese apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="719b9-158">Richiesta dell'autenticazione a più fattori per l'accesso da reti non considerate attendibili</span><span class="sxs-lookup"><span data-stu-id="719b9-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="719b9-159">Questo scenario consente simile toohello precedente perché aggiunge un requisito per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="719b9-159">This scenario is similar toohello previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="719b9-160">Tuttavia, la differenza principale hello è condizione hello per questo requisito.</span><span class="sxs-lookup"><span data-stu-id="719b9-160">However, hello main difference is hello condition for this requirement.</span></span>  
<span data-ttu-id="719b9-161">Durante lo stato attivo hello dello scenario precedente hello per le app con accesso ai dati toosensitve, hello di questo scenario è attiva percorsi attendibili.</span><span class="sxs-lookup"><span data-stu-id="719b9-161">While hello focus of hello previous scenario was on apps with access toosensitve data, hello focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="719b9-162">In altre parole, è possibile avere un requisito per l'autenticazione a più fattori se un'app è accessibile a un utente da una rete non considerata attendibile.</span><span class="sxs-lookup"><span data-stu-id="719b9-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="719b9-163">Solo i dispositivi attendibili possono accedere ai servizi di Office 365</span><span class="sxs-lookup"><span data-stu-id="719b9-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="719b9-164">Se si usa Intune nel proprio ambiente, è possibile avviare immediatamente usando l'interfaccia di criteri di accesso condizionale hello nella console di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="719b9-164">If you are using Intune in your environment, you can immediately start using hello conditional access policy interface in hello Azure console.</span></span>

<span data-ttu-id="719b9-165">Molti clienti di Intune usano tooensure di accesso condizionale che solo i dispositivi attendibili possono accedere ai servizi di Office 365.</span><span class="sxs-lookup"><span data-stu-id="719b9-165">Many Intune customers are using conditional access tooensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="719b9-166">Ciò significa che i dispositivi mobili registrati con Intune e che soddisfano i requisiti di conformità e che i PC Windows sono dominio locale tooan unita in join.</span><span class="sxs-lookup"><span data-stu-id="719b9-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined tooan on-premises domain.</span></span> <span data-ttu-id="719b9-167">Dei miglioramenti principali è che non sia tooset hello stesso criterio per ognuno dei servizi di Office 365 hello.</span><span class="sxs-lookup"><span data-stu-id="719b9-167">A key improvement is that you do not have tooset hello same policy for each of hello Office 365 services.</span></span>  <span data-ttu-id="719b9-168">Quando si crea un nuovo criterio, è possibile configurare hello Cloud App tooinclude ogni delle app di Office 365 hello che si desidera tooprotect con accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="719b9-168">When you create a new policy, configure hello Cloud apps tooinclude each of hello O365 apps that you wish tooprotect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="719b9-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="719b9-169">Next steps</span></span>

<span data-ttu-id="719b9-170">Se si desidera tooknow tooconfigure criteri di accesso condizionale, vedere [iniziare con l'accesso condizionale in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="719b9-170">If you want tooknow how tooconfigure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
