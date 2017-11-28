---
title: 'Azure Active B2C di Directory: Informazioni sui criteri personalizzati di pacchetto hello | Documenti Microsoft'
description: Un argomento sui criteri personalizzati di Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="83fb9-103">Informazioni sui criteri personalizzati di hello del pacchetto hello Azure Active Directory B2C criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="83fb9-103">Understanding hello custom policies of hello Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="83fb9-104">Questa sezione sono elencati tutti gli elementi di base hello dei criteri di hello B2C_1A_base fornita con hello **principianti** e che viene utilizzata per la creazione di propri criteri tramite ereditarietà hello di hello *B2C_1A_base_ criteri di estensioni*.</span><span class="sxs-lookup"><span data-stu-id="83fb9-104">This section lists all hello core elements of hello B2C_1A_base policy that comes with hello **Starter Pack** and that is leveraged for authoring your own policies through hello inheritance of hello *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="83fb9-105">Di conseguenza, più in particolare mette in hello già definito tipi, le trasformazioni di attestazioni, le definizioni di contenuto, i provider di attestazioni con i relativi profili tecnici di attestazione e hello viaggi utente core.</span><span class="sxs-lookup"><span data-stu-id="83fb9-105">As such, it more particularly focusses on hello already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and hello core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="83fb9-106">Microsoft non rilascia alcuna garanzia, esplicita o implicita, riguardo toohello informazioni fornite di seguito.</span><span class="sxs-lookup"><span data-stu-id="83fb9-106">Microsoft makes no warranties, express or implied, with respect toohello information provided hereafter.</span></span> <span data-ttu-id="83fb9-107">Potrebbero essere apportate modifiche in qualsiasi momento, prima della disponibilità a livello generale, al momento della disponibilità a livello generale o in seguito.</span><span class="sxs-lookup"><span data-stu-id="83fb9-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="83fb9-108">Propri criteri e hello B2C_1A_base_extensions criteri è possibile eseguire l'override di queste definizioni ed estendere questi criteri padre fornendo aggiuntive in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="83fb9-108">Both your own policies and hello B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="83fb9-109">gli elementi principali di hello Hello *B2C_1A_base criteri* sono tipi di attestazione, le trasformazioni di attestazioni e le definizioni di contenuto.</span><span class="sxs-lookup"><span data-stu-id="83fb9-109">hello core elements of hello *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="83fb9-110">Questi elementi possono toobe soggetti a cui fa riferimento anche propri criteri come hello *B2C_1A_base_extensions criteri*.</span><span class="sxs-lookup"><span data-stu-id="83fb9-110">These elements can susceptible toobe referenced in your own policies as well as in hello *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="83fb9-111">Schema delle attestazioni</span><span class="sxs-lookup"><span data-stu-id="83fb9-111">Claims schemas</span></span>

<span data-ttu-id="83fb9-112">Questo schema delle attestazioni è diviso in tre sezioni:</span><span class="sxs-lookup"><span data-stu-id="83fb9-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="83fb9-113">Prima sezione in cui sono elencati hello minimo attestazioni richieste per hello utente viaggi toowork correttamente.</span><span class="sxs-lookup"><span data-stu-id="83fb9-113">A first section that lists hello minimum claims that are required for hello user journeys toowork properly.</span></span>
2.  <span data-ttu-id="83fb9-114">Una seconda sezione che elenchi hello attestazioni richieste per i parametri di stringa di query e altri parametri speciali di toobe passato tooother dai provider di attestazioni, in particolare login.microsoftonline.com per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="83fb9-114">A second section that lists hello claims required for query string parameters and other special parameters toobe passed tooother claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="83fb9-115">**Non modificare queste attestazioni**.</span><span class="sxs-lookup"><span data-stu-id="83fb9-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="83fb9-116">E infine una terza sezione che elenca tutte le attestazioni aggiuntive e facoltative che possono essere raccolti da utente hello, archiviati nella directory hello inviati nei token di accesso.</span><span class="sxs-lookup"><span data-stu-id="83fb9-116">And eventually a third section that lists any additional, optional claims that can be collected from hello user, stored in hello directory and sent in tokens during sign in.</span></span> <span data-ttu-id="83fb9-117">È possibile aggiungere nuove attestazioni toobe tipo raccolti dall'utente hello e/o inviati nel token hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="83fb9-117">New claims type toobe collected from hello user and/or sent in hello token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="83fb9-118">schema di attestazioni Hello contiene restrizioni su determinate attestazioni, ad esempio nomi utente e password.</span><span class="sxs-lookup"><span data-stu-id="83fb9-118">hello claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="83fb9-119">criteri di attendibilità Framework (TF) Hello considera AD Azure come qualsiasi altro provider di attestazioni e tutte le relative restrizioni sono modellate in Criteri di hello premium.</span><span class="sxs-lookup"><span data-stu-id="83fb9-119">hello Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in hello premium policy.</span></span> <span data-ttu-id="83fb9-120">Un criterio potrebbe essere modificato tooadd più restrizioni o utilizzare un altro provider di attestazioni per l'archiviazione di credenziali che conterrà i proprio restrizioni.</span><span class="sxs-lookup"><span data-stu-id="83fb9-120">A policy could be modified tooadd more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="83fb9-121">tipi di attestazione disponibili Hello sono elencati di seguito.</span><span class="sxs-lookup"><span data-stu-id="83fb9-121">hello available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-hello-user-journeys"></a><span data-ttu-id="83fb9-122">Attestazioni necessarie per i percorsi utente hello</span><span class="sxs-lookup"><span data-stu-id="83fb9-122">Claims that are required for hello user journeys</span></span>

<span data-ttu-id="83fb9-123">Hello seguendo le attestazioni è necessario per utente viaggi toowork correttamente:</span><span class="sxs-lookup"><span data-stu-id="83fb9-123">hello following claims are required for user journeys toowork properly:</span></span>

| <span data-ttu-id="83fb9-124">Tipo di attestazione</span><span class="sxs-lookup"><span data-stu-id="83fb9-124">Claims type</span></span> | <span data-ttu-id="83fb9-125">Descrizione</span><span class="sxs-lookup"><span data-stu-id="83fb9-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="83fb9-126">*UserId*</span><span class="sxs-lookup"><span data-stu-id="83fb9-126">*UserId*</span></span> | <span data-ttu-id="83fb9-127">Nome utente</span><span class="sxs-lookup"><span data-stu-id="83fb9-127">Username</span></span> |
| <span data-ttu-id="83fb9-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="83fb9-128">*signInName*</span></span> | <span data-ttu-id="83fb9-129">Nome di accesso</span><span class="sxs-lookup"><span data-stu-id="83fb9-129">Sign in name</span></span> |
| <span data-ttu-id="83fb9-130">*tenantId*</span><span class="sxs-lookup"><span data-stu-id="83fb9-130">*tenantId*</span></span> | <span data-ttu-id="83fb9-131">Identificatore del tenant (ID) dell'oggetto utente hello in Azure Active Directory B2C Premium</span><span class="sxs-lookup"><span data-stu-id="83fb9-131">Tenant identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="83fb9-132">*objectId*</span><span class="sxs-lookup"><span data-stu-id="83fb9-132">*objectId*</span></span> | <span data-ttu-id="83fb9-133">Identificatore di oggetto (ID) dell'oggetto utente hello in Azure Active Directory B2C Premium</span><span class="sxs-lookup"><span data-stu-id="83fb9-133">Object identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="83fb9-134">*password*</span><span class="sxs-lookup"><span data-stu-id="83fb9-134">*password*</span></span> | <span data-ttu-id="83fb9-135">Password</span><span class="sxs-lookup"><span data-stu-id="83fb9-135">Password</span></span> |
| <span data-ttu-id="83fb9-136">*newPassword*</span><span class="sxs-lookup"><span data-stu-id="83fb9-136">*newPassword*</span></span> | |
| <span data-ttu-id="83fb9-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="83fb9-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="83fb9-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="83fb9-138">*passwordPolicies*</span></span> | <span data-ttu-id="83fb9-139">Criteri password utilizzati dalla complessità della password di Azure Active Directory B2C Premium toodetermine scadenza, e così via.</span><span class="sxs-lookup"><span data-stu-id="83fb9-139">Password policies used by Azure AD B2C Premium toodetermine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="83fb9-140">*sub*</span><span class="sxs-lookup"><span data-stu-id="83fb9-140">*sub*</span></span> | |
| <span data-ttu-id="83fb9-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="83fb9-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="83fb9-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="83fb9-142">*identityProvider*</span></span> | |
| <span data-ttu-id="83fb9-143">*displayName*</span><span class="sxs-lookup"><span data-stu-id="83fb9-143">*displayName*</span></span> | |
| <span data-ttu-id="83fb9-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="83fb9-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="83fb9-145">Numero di telefono dell'utente</span><span class="sxs-lookup"><span data-stu-id="83fb9-145">User's telephone number</span></span> |
| <span data-ttu-id="83fb9-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="83fb9-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="83fb9-147">*email*</span><span class="sxs-lookup"><span data-stu-id="83fb9-147">*email*</span></span> | <span data-ttu-id="83fb9-148">Indirizzo di posta elettronica che può essere utilizzato toocontact hello utente</span><span class="sxs-lookup"><span data-stu-id="83fb9-148">Email address that can be used toocontact hello user</span></span> |
| <span data-ttu-id="83fb9-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="83fb9-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="83fb9-150">Indirizzo di posta elettronica hello utente può utilizzare toosign in</span><span class="sxs-lookup"><span data-stu-id="83fb9-150">Email address that hello user can use toosign in</span></span> |
| <span data-ttu-id="83fb9-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="83fb9-151">*otherMails*</span></span> | <span data-ttu-id="83fb9-152">Indirizzi di posta elettronica che possono essere utilizzato toocontact hello utente</span><span class="sxs-lookup"><span data-stu-id="83fb9-152">Email addresses that can be used toocontact hello user</span></span> |
| <span data-ttu-id="83fb9-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="83fb9-153">*userPrincipalName*</span></span> | <span data-ttu-id="83fb9-154">Nome utente archiviato nella hello Premium di Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="83fb9-154">Username as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="83fb9-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="83fb9-155">*upnUserName*</span></span> | <span data-ttu-id="83fb9-156">Nome utente per la creazione di nome dell'entità utente</span><span class="sxs-lookup"><span data-stu-id="83fb9-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="83fb9-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="83fb9-157">*mailNickName*</span></span> | <span data-ttu-id="83fb9-158">Nome alternativo posta elettronica dell'utente archiviato nella hello Premium di Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="83fb9-158">User's mail nick name as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="83fb9-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="83fb9-159">*newUser*</span></span> | |
| <span data-ttu-id="83fb9-160">*executed-SelfAsserted-Input*</span><span class="sxs-lookup"><span data-stu-id="83fb9-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="83fb9-161">Attestazione che specifica se gli attributi sono stati raccolti dall'utente hello</span><span class="sxs-lookup"><span data-stu-id="83fb9-161">Claim that specifies whether attributes were collected from hello user</span></span> |
| <span data-ttu-id="83fb9-162">*executed-PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="83fb9-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="83fb9-163">Attestazione che specifica se è stato raccolto un numero di telefono da utente hello</span><span class="sxs-lookup"><span data-stu-id="83fb9-163">Claim that specifies whether a new phone number was collected from hello user</span></span> |
| <span data-ttu-id="83fb9-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="83fb9-164">*authenticationSource*</span></span> | <span data-ttu-id="83fb9-165">Specifica se l'utente hello è stato autenticato al Provider di identità di social networking, login.microsoftonline.com o un account locale</span><span class="sxs-lookup"><span data-stu-id="83fb9-165">Specifies whether hello user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="83fb9-166">Attestazioni necessarie per i parametri della stringa di query e altri parametri speciali</span><span class="sxs-lookup"><span data-stu-id="83fb9-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="83fb9-167">Hello attestazioni seguenti sono necessari toopass nel provider di attestazioni tooother parametri speciali (inclusi alcuni parametri di stringa di query).</span><span class="sxs-lookup"><span data-stu-id="83fb9-167">hello following claims are required toopass on special parameters (including some query string parameters) tooother claims providers:</span></span>

| <span data-ttu-id="83fb9-168">Tipo di attestazione</span><span class="sxs-lookup"><span data-stu-id="83fb9-168">Claims type</span></span> | <span data-ttu-id="83fb9-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="83fb9-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="83fb9-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="83fb9-170">*nux*</span></span> | <span data-ttu-id="83fb9-171">Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale</span><span class="sxs-lookup"><span data-stu-id="83fb9-171">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="83fb9-172">*nca*</span><span class="sxs-lookup"><span data-stu-id="83fb9-172">*nca*</span></span> | <span data-ttu-id="83fb9-173">Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale</span><span class="sxs-lookup"><span data-stu-id="83fb9-173">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="83fb9-174">*prompt*</span><span class="sxs-lookup"><span data-stu-id="83fb9-174">*prompt*</span></span> | <span data-ttu-id="83fb9-175">Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale</span><span class="sxs-lookup"><span data-stu-id="83fb9-175">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="83fb9-176">*mkt*</span><span class="sxs-lookup"><span data-stu-id="83fb9-176">*mkt*</span></span> | <span data-ttu-id="83fb9-177">Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale</span><span class="sxs-lookup"><span data-stu-id="83fb9-177">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="83fb9-178">*lc*</span><span class="sxs-lookup"><span data-stu-id="83fb9-178">*lc*</span></span> | <span data-ttu-id="83fb9-179">Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale</span><span class="sxs-lookup"><span data-stu-id="83fb9-179">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="83fb9-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="83fb9-180">*grant_type*</span></span> | <span data-ttu-id="83fb9-181">Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale</span><span class="sxs-lookup"><span data-stu-id="83fb9-181">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="83fb9-182">*scope*</span><span class="sxs-lookup"><span data-stu-id="83fb9-182">*scope*</span></span> | <span data-ttu-id="83fb9-183">Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale</span><span class="sxs-lookup"><span data-stu-id="83fb9-183">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="83fb9-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="83fb9-184">*client_id*</span></span> | <span data-ttu-id="83fb9-185">Per account locale autenticazione toologin.microsoftonline.com passato il parametro speciale</span><span class="sxs-lookup"><span data-stu-id="83fb9-185">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="83fb9-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="83fb9-186">*objectIdFromSession*</span></span> | <span data-ttu-id="83fb9-187">Parametro fornito dal hello predefinito sessione Gestione provider tooindicate che hello id di oggetto è stato recuperato da una sessione SSO</span><span class="sxs-lookup"><span data-stu-id="83fb9-187">Parameter provided by hello default session management provider tooindicate that hello object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="83fb9-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="83fb9-188">*isActiveMFASession*</span></span> | <span data-ttu-id="83fb9-189">Parametro fornito da hello MFA sessione gestione tooindicate che utente hello dispone di una sessione attiva di autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="83fb9-189">Parameter provided by hello MFA session management tooindicate that hello user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="83fb9-190">Attestazioni aggiuntive (facoltative) che possono essere raccolte</span><span class="sxs-lookup"><span data-stu-id="83fb9-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="83fb9-191">esempio Hello attestazioni sono attestazioni aggiuntive che possono essere raccolti da utenti hello, archiviati nella directory di hello e inviati nel token hello.</span><span class="sxs-lookup"><span data-stu-id="83fb9-191">hello following claims are additional claims that can be collected from hello users, stored in hello directory, and sent in hello token.</span></span> <span data-ttu-id="83fb9-192">Come descritto prima, possono essere aggiunte ulteriori attestazioni toothis elenco.</span><span class="sxs-lookup"><span data-stu-id="83fb9-192">As outlined before, additional claims can be added toothis list.</span></span>

| <span data-ttu-id="83fb9-193">Tipo di attestazione</span><span class="sxs-lookup"><span data-stu-id="83fb9-193">Claims type</span></span> | <span data-ttu-id="83fb9-194">Descrizione</span><span class="sxs-lookup"><span data-stu-id="83fb9-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="83fb9-195">*givenName*</span><span class="sxs-lookup"><span data-stu-id="83fb9-195">*givenName*</span></span> | <span data-ttu-id="83fb9-196">Nome di battesimo dell'utente (noto anche come nome)</span><span class="sxs-lookup"><span data-stu-id="83fb9-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="83fb9-197">*surname*</span><span class="sxs-lookup"><span data-stu-id="83fb9-197">*surname*</span></span> | <span data-ttu-id="83fb9-198">Cognome dell'utente</span><span class="sxs-lookup"><span data-stu-id="83fb9-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="83fb9-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="83fb9-199">*Extension_picture*</span></span> | <span data-ttu-id="83fb9-200">Immagine dell'utente da social network</span><span class="sxs-lookup"><span data-stu-id="83fb9-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="83fb9-201">Trasformazioni delle attestazioni</span><span class="sxs-lookup"><span data-stu-id="83fb9-201">Claim transformations</span></span>

<span data-ttu-id="83fb9-202">le trasformazioni delle attestazioni disponibili di Hello sono elencate di seguito.</span><span class="sxs-lookup"><span data-stu-id="83fb9-202">hello available claim transformations are listed below.</span></span>

| <span data-ttu-id="83fb9-203">Trasformazione attestazione</span><span class="sxs-lookup"><span data-stu-id="83fb9-203">Claim transformation</span></span> | <span data-ttu-id="83fb9-204">Descrizione</span><span class="sxs-lookup"><span data-stu-id="83fb9-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="83fb9-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="83fb9-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="83fb9-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="83fb9-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="83fb9-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="83fb9-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="83fb9-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="83fb9-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="83fb9-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="83fb9-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="83fb9-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="83fb9-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="83fb9-211">Definizioni del contenuto</span><span class="sxs-lookup"><span data-stu-id="83fb9-211">Content definitions</span></span>

<span data-ttu-id="83fb9-212">Questa sezione vengono descritte le definizioni di hello contenuto già dichiarate in hello *B2C_1A_base* criteri.</span><span class="sxs-lookup"><span data-stu-id="83fb9-212">This section describes hello content definitions already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="83fb9-213">Queste definizioni di contenuto sono sensibili toobe a cui fa riferimento, viene sottoposto a override e/o estesi in base alle esigenze di propri criteri anche come hello *B2C_1A_base_extensions* criteri.</span><span class="sxs-lookup"><span data-stu-id="83fb9-213">These content definitions are susceptible toobe referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="83fb9-214">Provider di attestazioni</span><span class="sxs-lookup"><span data-stu-id="83fb9-214">Claims provider</span></span> | <span data-ttu-id="83fb9-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="83fb9-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="83fb9-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="83fb9-216">*Facebook*</span></span> | |
| <span data-ttu-id="83fb9-217">*Accesso all'account locale*</span><span class="sxs-lookup"><span data-stu-id="83fb9-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="83fb9-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="83fb9-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="83fb9-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="83fb9-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="83fb9-220">*Autocertificazione*</span><span class="sxs-lookup"><span data-stu-id="83fb9-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="83fb9-221">*Account locale*</span><span class="sxs-lookup"><span data-stu-id="83fb9-221">*Local Account*</span></span> | |
| <span data-ttu-id="83fb9-222">*Gestione delle sessioni*</span><span class="sxs-lookup"><span data-stu-id="83fb9-222">*Session Management*</span></span> | |
| <span data-ttu-id="83fb9-223">*Motore di criteri Trustframework*</span><span class="sxs-lookup"><span data-stu-id="83fb9-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="83fb9-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="83fb9-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="83fb9-225">*Autorità emittente di token*</span><span class="sxs-lookup"><span data-stu-id="83fb9-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="83fb9-226">Profili tecnici</span><span class="sxs-lookup"><span data-stu-id="83fb9-226">Technical profiles</span></span>

<span data-ttu-id="83fb9-227">In questa sezione illustra i profili di tecniche hello già dichiarati per ogni provider di attestazioni di hello *B2C_1A_base* criteri.</span><span class="sxs-lookup"><span data-stu-id="83fb9-227">This section depicts hello technical profiles already declared per claim provider in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="83fb9-228">Questi profili tecnici sono sensibili toobe ulteriormente a cui fa riferimento, viene sottoposto a override e/o estesi in base alle esigenze di propri criteri anche come hello *B2C_1A_base_extensions* criteri.</span><span class="sxs-lookup"><span data-stu-id="83fb9-228">These technical profiles are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="83fb9-229">Profili tecnici per Facebook</span><span class="sxs-lookup"><span data-stu-id="83fb9-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="83fb9-230">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="83fb9-230">Technical profile</span></span> | <span data-ttu-id="83fb9-231">Descrizione</span><span class="sxs-lookup"><span data-stu-id="83fb9-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="83fb9-232">*Facebook-OAUTH*</span><span class="sxs-lookup"><span data-stu-id="83fb9-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="83fb9-233">Profili tecnici per l'accesso all'account locale</span><span class="sxs-lookup"><span data-stu-id="83fb9-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="83fb9-234">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="83fb9-234">Technical profile</span></span> | <span data-ttu-id="83fb9-235">Descrizione</span><span class="sxs-lookup"><span data-stu-id="83fb9-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="83fb9-236">*Login-NonInteractive*</span><span class="sxs-lookup"><span data-stu-id="83fb9-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="83fb9-237">Profili tecnici per PhoneFactor</span><span class="sxs-lookup"><span data-stu-id="83fb9-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="83fb9-238">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="83fb9-238">Technical profile</span></span> | <span data-ttu-id="83fb9-239">Descrizione</span><span class="sxs-lookup"><span data-stu-id="83fb9-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="83fb9-240">*PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="83fb9-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="83fb9-241">*PhoneFactor-InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="83fb9-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="83fb9-242">*PhoneFactor-Verify*</span><span class="sxs-lookup"><span data-stu-id="83fb9-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="83fb9-243">Profili tecnici per Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83fb9-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="83fb9-244">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="83fb9-244">Technical profile</span></span> | <span data-ttu-id="83fb9-245">Descrizione</span><span class="sxs-lookup"><span data-stu-id="83fb9-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="83fb9-246">*AAD-Common*</span><span class="sxs-lookup"><span data-stu-id="83fb9-246">*AAD-Common*</span></span> | <span data-ttu-id="83fb9-247">Profilo tecnico incluso da hello altri profili tecnici AAD-xxx</span><span class="sxs-lookup"><span data-stu-id="83fb9-247">Technical profile included by hello other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="83fb9-248">*AAD-UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="83fb9-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="83fb9-249">Profilo tecnico per gli accessi basati su social network</span><span class="sxs-lookup"><span data-stu-id="83fb9-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="83fb9-250">*AAD-UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="83fb9-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="83fb9-251">Profilo tecnico per gli accessi basati su social network</span><span class="sxs-lookup"><span data-stu-id="83fb9-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="83fb9-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span><span class="sxs-lookup"><span data-stu-id="83fb9-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="83fb9-253">Profilo tecnico per gli accessi basati su social network</span><span class="sxs-lookup"><span data-stu-id="83fb9-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="83fb9-254">*AAD-UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="83fb9-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="83fb9-255">Profili tecnici per gli account locali</span><span class="sxs-lookup"><span data-stu-id="83fb9-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="83fb9-256">*AAD-UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="83fb9-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="83fb9-257">Profili tecnici per gli account locali</span><span class="sxs-lookup"><span data-stu-id="83fb9-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="83fb9-258">*AAD-UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="83fb9-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="83fb9-259">Profilo tecnico per aggiornare il record utente usando objectId</span><span class="sxs-lookup"><span data-stu-id="83fb9-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="83fb9-260">*AAD-UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="83fb9-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="83fb9-261">Profilo tecnico per aggiornare il record utente usando objectId</span><span class="sxs-lookup"><span data-stu-id="83fb9-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="83fb9-262">*AAD-UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="83fb9-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="83fb9-263">Profilo tecnico per aggiornare il record utente usando objectId</span><span class="sxs-lookup"><span data-stu-id="83fb9-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="83fb9-264">*AAD-UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="83fb9-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="83fb9-265">Tecnica profilo è usato tooread dati dopo l'autenticazione dell'utente</span><span class="sxs-lookup"><span data-stu-id="83fb9-265">Technical profile is used tooread data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="83fb9-266">Profili tecnici per l'autocertificazione</span><span class="sxs-lookup"><span data-stu-id="83fb9-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="83fb9-267">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="83fb9-267">Technical profile</span></span> | <span data-ttu-id="83fb9-268">Descrizione</span><span class="sxs-lookup"><span data-stu-id="83fb9-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="83fb9-269">*SelfAsserted-Social*</span><span class="sxs-lookup"><span data-stu-id="83fb9-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="83fb9-270">*SelfAsserted-ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="83fb9-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="83fb9-271">Profili tecnici per l'account locale</span><span class="sxs-lookup"><span data-stu-id="83fb9-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="83fb9-272">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="83fb9-272">Technical profile</span></span> | <span data-ttu-id="83fb9-273">Descrizione</span><span class="sxs-lookup"><span data-stu-id="83fb9-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="83fb9-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="83fb9-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="83fb9-275">Profili tecnici per la gestione delle sessioni</span><span class="sxs-lookup"><span data-stu-id="83fb9-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="83fb9-276">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="83fb9-276">Technical profile</span></span> | <span data-ttu-id="83fb9-277">Descrizione</span><span class="sxs-lookup"><span data-stu-id="83fb9-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="83fb9-278">*SM-Noop*</span><span class="sxs-lookup"><span data-stu-id="83fb9-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="83fb9-279">*SM-AAD*</span><span class="sxs-lookup"><span data-stu-id="83fb9-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="83fb9-280">*SM-SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="83fb9-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="83fb9-281">Nome del profilo è sta toodisambiguate utilizzati AAD sessione tra accesso ed eseguire l'accesso</span><span class="sxs-lookup"><span data-stu-id="83fb9-281">Profile name is being used toodisambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="83fb9-282">*SM-SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="83fb9-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="83fb9-283">*SM-MFA*</span><span class="sxs-lookup"><span data-stu-id="83fb9-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="83fb9-284">Profili tecnici per TechnicalProfiles del motore di criteri Trustframework</span><span class="sxs-lookup"><span data-stu-id="83fb9-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="83fb9-285">Attualmente, non tecnici profili definiti per hello **Trustframework criteri motore TechnicalProfiles** provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="83fb9-285">Currently, no technical profiles are defined for hello **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="83fb9-286">Profili tecnici per l'autorità emittente di token</span><span class="sxs-lookup"><span data-stu-id="83fb9-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="83fb9-287">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="83fb9-287">Technical profile</span></span> | <span data-ttu-id="83fb9-288">Descrizione</span><span class="sxs-lookup"><span data-stu-id="83fb9-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="83fb9-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="83fb9-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="83fb9-290">Percorsi utente</span><span class="sxs-lookup"><span data-stu-id="83fb9-290">User journeys</span></span>

<span data-ttu-id="83fb9-291">In questa sezione illustra i percorsi utente hello già dichiarati in hello *B2C_1A_base* criteri.</span><span class="sxs-lookup"><span data-stu-id="83fb9-291">This section depicts hello user journeys already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="83fb9-292">Questi percorsi utente sono sensibili toobe ulteriormente a cui fa riferimento, viene sottoposto a override e/o estesi in base alle esigenze di propri criteri anche come hello *B2C_1A_base_extensions* criteri.</span><span class="sxs-lookup"><span data-stu-id="83fb9-292">These user journeys are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="83fb9-293">Percorso utente</span><span class="sxs-lookup"><span data-stu-id="83fb9-293">User journey</span></span> | <span data-ttu-id="83fb9-294">Descrizione</span><span class="sxs-lookup"><span data-stu-id="83fb9-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="83fb9-295">*SignUp*</span><span class="sxs-lookup"><span data-stu-id="83fb9-295">*SignUp*</span></span> | |
| <span data-ttu-id="83fb9-296">*SignIn*</span><span class="sxs-lookup"><span data-stu-id="83fb9-296">*SignIn*</span></span> | |
| <span data-ttu-id="83fb9-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="83fb9-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="83fb9-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="83fb9-298">*EditProfile*</span></span> | |
| <span data-ttu-id="83fb9-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="83fb9-299">*PasswordReset*</span></span> | |
