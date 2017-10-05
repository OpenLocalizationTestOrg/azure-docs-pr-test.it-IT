---
title: 'Azure Active Directory B2C: informazioni sui criteri personalizzati dello starter pack | Microsoft Docs'
description: Argomento sui criteri personalizzati di Azure Active Directory B2C
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
ms.openlocfilehash: 9847bcfcc139a769847678c1cca6a8b9c3a30e93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-the-custom-policies-of-the-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="94bd7-103">Informazioni sui criteri personalizzati dello starter pack di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="94bd7-103">Understanding the custom policies of the Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="94bd7-104">Questa sezione elenca tutti gli elementi principali del criterio B2C_1A_base disponibile nello **starter pack**, che può essere sfruttato per creare i propri criteri tramite l'ereditarietà del *criterio B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="94bd7-104">This section lists all the core elements of the B2C_1A_base policy that comes with the **Starter Pack** and that is leveraged for authoring your own policies through the inheritance of the *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="94bd7-105">Più in particolare vengono illustrati i tipi di attestazioni già definiti, le trasformazioni delle attestazioni, le definizioni del contenuto, i provider di attestazioni con i profili tecnici e i percorsi utente principali.</span><span class="sxs-lookup"><span data-stu-id="94bd7-105">As such, it more particularly focusses on the already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and the core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94bd7-106">Microsoft non rilascia alcuna garanzia, espressa o implicita, in merito alle informazioni fornite da questo punto in avanti.</span><span class="sxs-lookup"><span data-stu-id="94bd7-106">Microsoft makes no warranties, express or implied, with respect to the information provided hereafter.</span></span> <span data-ttu-id="94bd7-107">Potrebbero essere apportate modifiche in qualsiasi momento, prima della disponibilità a livello generale, al momento della disponibilità a livello generale o in seguito.</span><span class="sxs-lookup"><span data-stu-id="94bd7-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="94bd7-108">Sia i criteri personalizzati che il criterio B2C_1A_base_extensions possono eseguire l'override di queste definizioni ed estendere questo criterio padre fornendone altre, se necessario.</span><span class="sxs-lookup"><span data-stu-id="94bd7-108">Both your own policies and the B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="94bd7-109">Gli elementi principali del *criterio B2C_1A_base* sono tipi di attestazioni, trasformazioni di attestazioni e definizioni del contenuto.</span><span class="sxs-lookup"><span data-stu-id="94bd7-109">The core elements of the *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="94bd7-110">Questi elementi possono essere usati come riferimento nei criteri personalizzati e nel *criterio B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="94bd7-110">These elements can susceptible to be referenced in your own policies as well as in the *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="94bd7-111">Schema delle attestazioni</span><span class="sxs-lookup"><span data-stu-id="94bd7-111">Claims schemas</span></span>

<span data-ttu-id="94bd7-112">Questo schema delle attestazioni è diviso in tre sezioni:</span><span class="sxs-lookup"><span data-stu-id="94bd7-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="94bd7-113">Una prima sezione che elenca le attestazioni minime necessarie per il corretto funzionamento dei percorsi utente.</span><span class="sxs-lookup"><span data-stu-id="94bd7-113">A first section that lists the minimum claims that are required for the user journeys to work properly.</span></span>
2.  <span data-ttu-id="94bd7-114">Una seconda sezione che elenca le attestazioni necessarie per i parametri della stringa di query e altri speciali parametri da passare ad altri provider di attestazioni, in particolare login.microsoftonline.com per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="94bd7-114">A second section that lists the claims required for query string parameters and other special parameters to be passed to other claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="94bd7-115">**Non modificare queste attestazioni**.</span><span class="sxs-lookup"><span data-stu-id="94bd7-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="94bd7-116">Infine una terza sezione che elenca altre attestazioni facoltative che possono essere raccolte dall'utente, archiviate nella directory e inviate in token durante l'accesso.</span><span class="sxs-lookup"><span data-stu-id="94bd7-116">And eventually a third section that lists any additional, optional claims that can be collected from the user, stored in the directory and sent in tokens during sign in.</span></span> <span data-ttu-id="94bd7-117">In questa sezione possono essere aggiunti nuovi tipi di attestazioni che devono essere raccolte dall'utente e/o inviate nel token.</span><span class="sxs-lookup"><span data-stu-id="94bd7-117">New claims type to be collected from the user and/or sent in the token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94bd7-118">Lo schema delle attestazioni contiene le limitazioni relative a determinate attestazioni, ad esempio password e nomi utente.</span><span class="sxs-lookup"><span data-stu-id="94bd7-118">The claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="94bd7-119">Il criterio del framework attendibilità considera Azure AD come qualsiasi altro provider di attestazioni e tutte le limitazioni sono modellate nel criterio premium.</span><span class="sxs-lookup"><span data-stu-id="94bd7-119">The Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in the premium policy.</span></span> <span data-ttu-id="94bd7-120">Un criterio può essere modificato per aggiungere altre limitazioni o usare un altro provider di attestazioni per la risorsa di archiviazione delle credenziali che avrà le proprie limitazioni.</span><span class="sxs-lookup"><span data-stu-id="94bd7-120">A policy could be modified to add more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="94bd7-121">Di seguito sono elencati i tipi di attestazioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="94bd7-121">The available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-the-user-journeys"></a><span data-ttu-id="94bd7-122">Attestazioni necessarie per i percorsi utente</span><span class="sxs-lookup"><span data-stu-id="94bd7-122">Claims that are required for the user journeys</span></span>

<span data-ttu-id="94bd7-123">Le attestazioni seguenti sono necessarie per il corretto funzionamento dei percorsi utente:</span><span class="sxs-lookup"><span data-stu-id="94bd7-123">The following claims are required for user journeys to work properly:</span></span>

| <span data-ttu-id="94bd7-124">Tipo di attestazione</span><span class="sxs-lookup"><span data-stu-id="94bd7-124">Claims type</span></span> | <span data-ttu-id="94bd7-125">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94bd7-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="94bd7-126">*UserId*</span><span class="sxs-lookup"><span data-stu-id="94bd7-126">*UserId*</span></span> | <span data-ttu-id="94bd7-127">Nome utente</span><span class="sxs-lookup"><span data-stu-id="94bd7-127">Username</span></span> |
| <span data-ttu-id="94bd7-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="94bd7-128">*signInName*</span></span> | <span data-ttu-id="94bd7-129">Nome di accesso</span><span class="sxs-lookup"><span data-stu-id="94bd7-129">Sign in name</span></span> |
| <span data-ttu-id="94bd7-130">*tenantId*</span><span class="sxs-lookup"><span data-stu-id="94bd7-130">*tenantId*</span></span> | <span data-ttu-id="94bd7-131">Identificatore (ID) tenant dell'oggetto utente in Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="94bd7-131">Tenant identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="94bd7-132">*objectId*</span><span class="sxs-lookup"><span data-stu-id="94bd7-132">*objectId*</span></span> | <span data-ttu-id="94bd7-133">Identificatore (ID) oggetto dell'oggetto utente in Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="94bd7-133">Object identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="94bd7-134">*password*</span><span class="sxs-lookup"><span data-stu-id="94bd7-134">*password*</span></span> | <span data-ttu-id="94bd7-135">Password</span><span class="sxs-lookup"><span data-stu-id="94bd7-135">Password</span></span> |
| <span data-ttu-id="94bd7-136">*newPassword*</span><span class="sxs-lookup"><span data-stu-id="94bd7-136">*newPassword*</span></span> | |
| <span data-ttu-id="94bd7-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="94bd7-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="94bd7-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="94bd7-138">*passwordPolicies*</span></span> | <span data-ttu-id="94bd7-139">Criteri password usati da Azure AD B2C Premium per determinare la complessità delle password, la scadenza e così via.</span><span class="sxs-lookup"><span data-stu-id="94bd7-139">Password policies used by Azure AD B2C Premium to determine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="94bd7-140">*sub*</span><span class="sxs-lookup"><span data-stu-id="94bd7-140">*sub*</span></span> | |
| <span data-ttu-id="94bd7-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="94bd7-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="94bd7-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="94bd7-142">*identityProvider*</span></span> | |
| <span data-ttu-id="94bd7-143">*displayName*</span><span class="sxs-lookup"><span data-stu-id="94bd7-143">*displayName*</span></span> | |
| <span data-ttu-id="94bd7-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="94bd7-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="94bd7-145">Numero di telefono dell'utente</span><span class="sxs-lookup"><span data-stu-id="94bd7-145">User's telephone number</span></span> |
| <span data-ttu-id="94bd7-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="94bd7-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="94bd7-147">*email*</span><span class="sxs-lookup"><span data-stu-id="94bd7-147">*email*</span></span> | <span data-ttu-id="94bd7-148">Indirizzo di posta elettronica che può essere usato per contattare l'utente</span><span class="sxs-lookup"><span data-stu-id="94bd7-148">Email address that can be used to contact the user</span></span> |
| <span data-ttu-id="94bd7-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="94bd7-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="94bd7-150">Indirizzo di posta elettronica che l'utente può usare per l'accesso</span><span class="sxs-lookup"><span data-stu-id="94bd7-150">Email address that the user can use to sign in</span></span> |
| <span data-ttu-id="94bd7-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="94bd7-151">*otherMails*</span></span> | <span data-ttu-id="94bd7-152">Indirizzi di posta elettronica che possono essere usati per contattare l'utente</span><span class="sxs-lookup"><span data-stu-id="94bd7-152">Email addresses that can be used to contact the user</span></span> |
| <span data-ttu-id="94bd7-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="94bd7-153">*userPrincipalName*</span></span> | <span data-ttu-id="94bd7-154">Nome utente archiviato in Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="94bd7-154">Username as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="94bd7-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="94bd7-155">*upnUserName*</span></span> | <span data-ttu-id="94bd7-156">Nome utente per la creazione di nome dell'entità utente</span><span class="sxs-lookup"><span data-stu-id="94bd7-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="94bd7-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="94bd7-157">*mailNickName*</span></span> | <span data-ttu-id="94bd7-158">Nome alternativo per la posta elettronica dell'utente archiviato in Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="94bd7-158">User's mail nick name as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="94bd7-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="94bd7-159">*newUser*</span></span> | |
| <span data-ttu-id="94bd7-160">*executed-SelfAsserted-Input*</span><span class="sxs-lookup"><span data-stu-id="94bd7-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="94bd7-161">Attestazione che specifica se gli attributi sono stati raccolti dall'utente</span><span class="sxs-lookup"><span data-stu-id="94bd7-161">Claim that specifies whether attributes were collected from the user</span></span> |
| <span data-ttu-id="94bd7-162">*executed-PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="94bd7-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="94bd7-163">Attestazione che specifica se un nuovo numero di telefono è stato raccolto dall'utente</span><span class="sxs-lookup"><span data-stu-id="94bd7-163">Claim that specifies whether a new phone number was collected from the user</span></span> |
| <span data-ttu-id="94bd7-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="94bd7-164">*authenticationSource*</span></span> | <span data-ttu-id="94bd7-165">Specifica se l'utente è stato autenticato con il provider di identità basato su social network, login.microsoftonline.com o l'account locale</span><span class="sxs-lookup"><span data-stu-id="94bd7-165">Specifies whether the user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="94bd7-166">Attestazioni necessarie per i parametri della stringa di query e altri parametri speciali</span><span class="sxs-lookup"><span data-stu-id="94bd7-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="94bd7-167">Le attestazioni seguenti sono necessarie per passare particolari parametri (inclusi alcuni parametri della stringa di query) ad altri provider di attestazioni:</span><span class="sxs-lookup"><span data-stu-id="94bd7-167">The following claims are required to pass on special parameters (including some query string parameters) to other claims providers:</span></span>

| <span data-ttu-id="94bd7-168">Tipo di attestazione</span><span class="sxs-lookup"><span data-stu-id="94bd7-168">Claims type</span></span> | <span data-ttu-id="94bd7-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94bd7-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="94bd7-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="94bd7-170">*nux*</span></span> | <span data-ttu-id="94bd7-171">Parametro speciale passato per autenticazione dell'account locale in login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="94bd7-171">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="94bd7-172">*nca*</span><span class="sxs-lookup"><span data-stu-id="94bd7-172">*nca*</span></span> | <span data-ttu-id="94bd7-173">Parametro speciale passato per autenticazione dell'account locale in login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="94bd7-173">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="94bd7-174">*prompt*</span><span class="sxs-lookup"><span data-stu-id="94bd7-174">*prompt*</span></span> | <span data-ttu-id="94bd7-175">Parametro speciale passato per autenticazione dell'account locale in login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="94bd7-175">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="94bd7-176">*mkt*</span><span class="sxs-lookup"><span data-stu-id="94bd7-176">*mkt*</span></span> | <span data-ttu-id="94bd7-177">Parametro speciale passato per autenticazione dell'account locale in login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="94bd7-177">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="94bd7-178">*lc*</span><span class="sxs-lookup"><span data-stu-id="94bd7-178">*lc*</span></span> | <span data-ttu-id="94bd7-179">Parametro speciale passato per autenticazione dell'account locale in login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="94bd7-179">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="94bd7-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="94bd7-180">*grant_type*</span></span> | <span data-ttu-id="94bd7-181">Parametro speciale passato per autenticazione dell'account locale in login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="94bd7-181">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="94bd7-182">*scope*</span><span class="sxs-lookup"><span data-stu-id="94bd7-182">*scope*</span></span> | <span data-ttu-id="94bd7-183">Parametro speciale passato per autenticazione dell'account locale in login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="94bd7-183">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="94bd7-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="94bd7-184">*client_id*</span></span> | <span data-ttu-id="94bd7-185">Parametro speciale passato per autenticazione dell'account locale in login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="94bd7-185">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="94bd7-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="94bd7-186">*objectIdFromSession*</span></span> | <span data-ttu-id="94bd7-187">Parametro fornito dal provider di gestione delle sessioni predefinite per indicare che l'oggetto è stato recuperato da una sessione SSO</span><span class="sxs-lookup"><span data-stu-id="94bd7-187">Parameter provided by the default session management provider to indicate that the object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="94bd7-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="94bd7-188">*isActiveMFASession*</span></span> | <span data-ttu-id="94bd7-189">Parametro fornito dal provider di gestione delle sessioni MFA per indicare che l'utente ha una sessione MFA attiva</span><span class="sxs-lookup"><span data-stu-id="94bd7-189">Parameter provided by the MFA session management to indicate that the user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="94bd7-190">Attestazioni aggiuntive (facoltative) che possono essere raccolte</span><span class="sxs-lookup"><span data-stu-id="94bd7-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="94bd7-191">Le seguenti sono attestazioni aggiuntive che possono essere raccolte dagli utenti, archiviate nella directory e inviate nel token.</span><span class="sxs-lookup"><span data-stu-id="94bd7-191">The following claims are additional claims that can be collected from the users, stored in the directory, and sent in the token.</span></span> <span data-ttu-id="94bd7-192">Come indicato prima, si possono aggiungere altre attestazioni a questo elenco.</span><span class="sxs-lookup"><span data-stu-id="94bd7-192">As outlined before, additional claims can be added to this list.</span></span>

| <span data-ttu-id="94bd7-193">Tipo di attestazione</span><span class="sxs-lookup"><span data-stu-id="94bd7-193">Claims type</span></span> | <span data-ttu-id="94bd7-194">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94bd7-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="94bd7-195">*givenName*</span><span class="sxs-lookup"><span data-stu-id="94bd7-195">*givenName*</span></span> | <span data-ttu-id="94bd7-196">Nome di battesimo dell'utente (noto anche come nome)</span><span class="sxs-lookup"><span data-stu-id="94bd7-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="94bd7-197">*surname*</span><span class="sxs-lookup"><span data-stu-id="94bd7-197">*surname*</span></span> | <span data-ttu-id="94bd7-198">Cognome dell'utente</span><span class="sxs-lookup"><span data-stu-id="94bd7-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="94bd7-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="94bd7-199">*Extension_picture*</span></span> | <span data-ttu-id="94bd7-200">Immagine dell'utente da social network</span><span class="sxs-lookup"><span data-stu-id="94bd7-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="94bd7-201">Trasformazioni delle attestazioni</span><span class="sxs-lookup"><span data-stu-id="94bd7-201">Claim transformations</span></span>

<span data-ttu-id="94bd7-202">Di seguito sono elencate le trasformazioni di attestazioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="94bd7-202">The available claim transformations are listed below.</span></span>

| <span data-ttu-id="94bd7-203">Trasformazione attestazione</span><span class="sxs-lookup"><span data-stu-id="94bd7-203">Claim transformation</span></span> | <span data-ttu-id="94bd7-204">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94bd7-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="94bd7-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="94bd7-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="94bd7-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="94bd7-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="94bd7-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="94bd7-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="94bd7-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="94bd7-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="94bd7-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="94bd7-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="94bd7-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="94bd7-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="94bd7-211">Definizioni del contenuto</span><span class="sxs-lookup"><span data-stu-id="94bd7-211">Content definitions</span></span>

<span data-ttu-id="94bd7-212">Questa sezione descrive le definizioni del contenuto già dichiarate nel criterio *B2C_1A_base*.</span><span class="sxs-lookup"><span data-stu-id="94bd7-212">This section describes the content definitions already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="94bd7-213">È possibile fare riferimento a queste definizioni del contenuto, eseguirne l'override e/o estenderle, se necessario, nei propri criteri oltre che nel criterio *B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="94bd7-213">These content definitions are susceptible to be referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="94bd7-214">Provider di attestazioni</span><span class="sxs-lookup"><span data-stu-id="94bd7-214">Claims provider</span></span> | <span data-ttu-id="94bd7-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94bd7-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="94bd7-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="94bd7-216">*Facebook*</span></span> | |
| <span data-ttu-id="94bd7-217">*Accesso all'account locale*</span><span class="sxs-lookup"><span data-stu-id="94bd7-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="94bd7-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="94bd7-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="94bd7-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="94bd7-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="94bd7-220">*Autocertificazione*</span><span class="sxs-lookup"><span data-stu-id="94bd7-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="94bd7-221">*Account locale*</span><span class="sxs-lookup"><span data-stu-id="94bd7-221">*Local Account*</span></span> | |
| <span data-ttu-id="94bd7-222">*Gestione delle sessioni*</span><span class="sxs-lookup"><span data-stu-id="94bd7-222">*Session Management*</span></span> | |
| <span data-ttu-id="94bd7-223">*Motore di criteri Trustframework*</span><span class="sxs-lookup"><span data-stu-id="94bd7-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="94bd7-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="94bd7-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="94bd7-225">*Autorità emittente di token*</span><span class="sxs-lookup"><span data-stu-id="94bd7-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="94bd7-226">Profili tecnici</span><span class="sxs-lookup"><span data-stu-id="94bd7-226">Technical profiles</span></span>

<span data-ttu-id="94bd7-227">Questa sezione illustra i profili tecnici già dichiarati per ogni provider di attestazioni nel criterio *B2C_1A_base*.</span><span class="sxs-lookup"><span data-stu-id="94bd7-227">This section depicts the technical profiles already declared per claim provider in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="94bd7-228">È possibile fare ulteriore riferimento a questi profili tecnici, eseguirne l'override e/o estenderli, se necessario, nei propri criteri oltre che nel criterio *B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="94bd7-228">These technical profiles are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="94bd7-229">Profili tecnici per Facebook</span><span class="sxs-lookup"><span data-stu-id="94bd7-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="94bd7-230">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="94bd7-230">Technical profile</span></span> | <span data-ttu-id="94bd7-231">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94bd7-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="94bd7-232">*Facebook-OAUTH*</span><span class="sxs-lookup"><span data-stu-id="94bd7-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="94bd7-233">Profili tecnici per l'accesso all'account locale</span><span class="sxs-lookup"><span data-stu-id="94bd7-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="94bd7-234">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="94bd7-234">Technical profile</span></span> | <span data-ttu-id="94bd7-235">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94bd7-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="94bd7-236">*Login-NonInteractive*</span><span class="sxs-lookup"><span data-stu-id="94bd7-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="94bd7-237">Profili tecnici per PhoneFactor</span><span class="sxs-lookup"><span data-stu-id="94bd7-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="94bd7-238">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="94bd7-238">Technical profile</span></span> | <span data-ttu-id="94bd7-239">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94bd7-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="94bd7-240">*PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="94bd7-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="94bd7-241">*PhoneFactor-InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="94bd7-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="94bd7-242">*PhoneFactor-Verify*</span><span class="sxs-lookup"><span data-stu-id="94bd7-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="94bd7-243">Profili tecnici per Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94bd7-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="94bd7-244">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="94bd7-244">Technical profile</span></span> | <span data-ttu-id="94bd7-245">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94bd7-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="94bd7-246">*AAD-Common*</span><span class="sxs-lookup"><span data-stu-id="94bd7-246">*AAD-Common*</span></span> | <span data-ttu-id="94bd7-247">Profilo tecnico incluso dagli altri profili tecnici AAD-xxx</span><span class="sxs-lookup"><span data-stu-id="94bd7-247">Technical profile included by the other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="94bd7-248">*AAD-UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="94bd7-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="94bd7-249">Profilo tecnico per gli accessi basati su social network</span><span class="sxs-lookup"><span data-stu-id="94bd7-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="94bd7-250">*AAD-UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="94bd7-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="94bd7-251">Profilo tecnico per gli accessi basati su social network</span><span class="sxs-lookup"><span data-stu-id="94bd7-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="94bd7-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span><span class="sxs-lookup"><span data-stu-id="94bd7-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="94bd7-253">Profilo tecnico per gli accessi basati su social network</span><span class="sxs-lookup"><span data-stu-id="94bd7-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="94bd7-254">*AAD-UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="94bd7-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="94bd7-255">Profili tecnici per gli account locali</span><span class="sxs-lookup"><span data-stu-id="94bd7-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="94bd7-256">*AAD-UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="94bd7-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="94bd7-257">Profili tecnici per gli account locali</span><span class="sxs-lookup"><span data-stu-id="94bd7-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="94bd7-258">*AAD-UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="94bd7-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="94bd7-259">Profilo tecnico per aggiornare il record utente usando objectId</span><span class="sxs-lookup"><span data-stu-id="94bd7-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="94bd7-260">*AAD-UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="94bd7-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="94bd7-261">Profilo tecnico per aggiornare il record utente usando objectId</span><span class="sxs-lookup"><span data-stu-id="94bd7-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="94bd7-262">*AAD-UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="94bd7-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="94bd7-263">Profilo tecnico per aggiornare il record utente usando objectId</span><span class="sxs-lookup"><span data-stu-id="94bd7-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="94bd7-264">*AAD-UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="94bd7-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="94bd7-265">Il profilo tecnico viene usato per leggere i dati dopo l'autenticazione dell'utente</span><span class="sxs-lookup"><span data-stu-id="94bd7-265">Technical profile is used to read data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="94bd7-266">Profili tecnici per l'autocertificazione</span><span class="sxs-lookup"><span data-stu-id="94bd7-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="94bd7-267">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="94bd7-267">Technical profile</span></span> | <span data-ttu-id="94bd7-268">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94bd7-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="94bd7-269">*SelfAsserted-Social*</span><span class="sxs-lookup"><span data-stu-id="94bd7-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="94bd7-270">*SelfAsserted-ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="94bd7-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="94bd7-271">Profili tecnici per l'account locale</span><span class="sxs-lookup"><span data-stu-id="94bd7-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="94bd7-272">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="94bd7-272">Technical profile</span></span> | <span data-ttu-id="94bd7-273">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94bd7-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="94bd7-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="94bd7-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="94bd7-275">Profili tecnici per la gestione delle sessioni</span><span class="sxs-lookup"><span data-stu-id="94bd7-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="94bd7-276">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="94bd7-276">Technical profile</span></span> | <span data-ttu-id="94bd7-277">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94bd7-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="94bd7-278">*SM-Noop*</span><span class="sxs-lookup"><span data-stu-id="94bd7-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="94bd7-279">*SM-AAD*</span><span class="sxs-lookup"><span data-stu-id="94bd7-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="94bd7-280">*SM-SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="94bd7-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="94bd7-281">Il nome del profilo viene usato per evitare ambiguità nella sessione AAD tra iscrizione e accesso</span><span class="sxs-lookup"><span data-stu-id="94bd7-281">Profile name is being used to disambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="94bd7-282">*SM-SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="94bd7-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="94bd7-283">*SM-MFA*</span><span class="sxs-lookup"><span data-stu-id="94bd7-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="94bd7-284">Profili tecnici per TechnicalProfiles del motore di criteri Trustframework</span><span class="sxs-lookup"><span data-stu-id="94bd7-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="94bd7-285">Non sono attualmente definiti profili tecnici per il provider di attestazioni **TechnicalProfiles del motore di criteri Trustframework**.</span><span class="sxs-lookup"><span data-stu-id="94bd7-285">Currently, no technical profiles are defined for the **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="94bd7-286">Profili tecnici per l'autorità emittente di token</span><span class="sxs-lookup"><span data-stu-id="94bd7-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="94bd7-287">Profilo tecnico</span><span class="sxs-lookup"><span data-stu-id="94bd7-287">Technical profile</span></span> | <span data-ttu-id="94bd7-288">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94bd7-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="94bd7-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="94bd7-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="94bd7-290">Percorsi utente</span><span class="sxs-lookup"><span data-stu-id="94bd7-290">User journeys</span></span>

<span data-ttu-id="94bd7-291">Questa sezione illustra i percorsi utente già dichiarati nel criterio *B2C_1A_base*.</span><span class="sxs-lookup"><span data-stu-id="94bd7-291">This section depicts the user journeys already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="94bd7-292">È possibile fare ulteriore riferimento a questi percorsi utente, eseguirne l'override e/o estenderli, se necessario, nei propri criteri oltre che nel criterio *B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="94bd7-292">These user journeys are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="94bd7-293">Percorso utente</span><span class="sxs-lookup"><span data-stu-id="94bd7-293">User journey</span></span> | <span data-ttu-id="94bd7-294">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94bd7-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="94bd7-295">*SignUp*</span><span class="sxs-lookup"><span data-stu-id="94bd7-295">*SignUp*</span></span> | |
| <span data-ttu-id="94bd7-296">*SignIn*</span><span class="sxs-lookup"><span data-stu-id="94bd7-296">*SignIn*</span></span> | |
| <span data-ttu-id="94bd7-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="94bd7-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="94bd7-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="94bd7-298">*EditProfile*</span></span> | |
| <span data-ttu-id="94bd7-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="94bd7-299">*PasswordReset*</span></span> | |
