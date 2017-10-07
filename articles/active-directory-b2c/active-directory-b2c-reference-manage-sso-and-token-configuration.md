---
title: 'Azure Active Directory B2C: gestire la personalizzazione dei token e SSO con i criteri personalizzati| Microsoft Docs'
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/02/2017
ms.author: sama
ms.openlocfilehash: b65271a22c77ea41eeec2126e4a3ad24364edd17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="9c032-102">Azure Active Directory B2C: gestire la personalizzazione dei token e SSO con i criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="9c032-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="9c032-103">Utilizzo di criteri personalizzati fornisce che si hello stesso controllo su token, sessione e single sign-on (SSO) le configurazioni di esempio tramite criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="9c032-103">Using custom policies provides you hello same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="9c032-104">toolearn quali di ciascuna impostazione, vedere la documentazione di hello [qui](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="9c032-104">toolearn what each setting does, please see hello documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="9c032-105">Configurazione delle attestazioni e delle durate dei token</span><span class="sxs-lookup"><span data-stu-id="9c032-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="9c032-106">toochange impostazioni hello la durata dei token, è necessario tooadd un `<ClaimsProviders>` elemento hello relying party file criteri hello desiderate tooimpact.</span><span class="sxs-lookup"><span data-stu-id="9c032-106">toochange hello settings on your token lifetimes, you need tooadd a `<ClaimsProviders>` element in hello relying party file of hello policy you want tooimpact.</span></span>  <span data-ttu-id="9c032-107">Hello `<ClaimsProviders>` è un elemento figlio di hello `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="9c032-107">hello `<ClaimsProviders>` element is a child of hello `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="9c032-108">All'interno, è necessario informazioni hello tooput che interessa la durata dei token.</span><span class="sxs-lookup"><span data-stu-id="9c032-108">Inside you'll need tooput hello information that affects your token lifetimes.</span></span>  <span data-ttu-id="9c032-109">Hello XML è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="9c032-109">hello XML looks like this:</span></span>

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

<span data-ttu-id="9c032-110">**Durata dei token di accesso** hello accesso durata del token può essere cambiata modificando valore hello all'interno di hello `<Item>` con hello Key = "token_lifetime_secs" in secondi.</span><span class="sxs-lookup"><span data-stu-id="9c032-110">**Access token lifetimes** hello access token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="9c032-111">valore predefinito di Hello predefinito è 3600 secondi (60 minuti).</span><span class="sxs-lookup"><span data-stu-id="9c032-111">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="9c032-112">**Durata del token ID** durata del token ID hello può essere cambiata modificando valore hello all'interno di hello `<Item>` con hello Key = "id_token_lifetime_secs" in secondi.</span><span class="sxs-lookup"><span data-stu-id="9c032-112">**ID token lifetime** hello ID token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="9c032-113">valore predefinito di Hello predefinito è 3600 secondi (60 minuti).</span><span class="sxs-lookup"><span data-stu-id="9c032-113">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="9c032-114">**Durata del token di aggiornamento** durata del token hello aggiornamento può essere modificata modificando il valore di hello all'interno di hello `<Item>` con hello Key = "refresh_token_lifetime_secs" in secondi.</span><span class="sxs-lookup"><span data-stu-id="9c032-114">**Refresh token lifetime** hello refresh token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="9c032-115">valore predefinito di Hello incorporato è 1209600 secondi (14 giorni).</span><span class="sxs-lookup"><span data-stu-id="9c032-115">hello default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="9c032-116">**Aggiorna durata token di una finestra temporale scorrevole** se si desidera tooset un token di aggiornamento tooyour di durata finestra temporale scorrevole, modificare il valore di hello all'interno di `<Item>` con hello Key = "rolling_refresh_token_lifetime_secs" in secondi.</span><span class="sxs-lookup"><span data-stu-id="9c032-116">**Refresh token sliding window lifetime** If you would like tooset a sliding window lifetime tooyour refresh token, modify hello value inside `<Item>` with hello Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="9c032-117">valore predefinito di Hello incorporato è 7776000 (90 giorni).</span><span class="sxs-lookup"><span data-stu-id="9c032-117">hello default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="9c032-118">Se non si desidera tooenfore una variabile di durata di una finestra, sostituire questa riga con:</span><span class="sxs-lookup"><span data-stu-id="9c032-118">If you don't want tooenfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="9c032-119">**Attestazione autorità di certificazione (iss)** se si desidera toochange hello dell'autorità di certificazione (iss di) attestazione, modificare il valore di hello all'interno di hello `<Item>` con hello Key = "IssuanceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="9c032-119">**Issuer (iss) claim** If you want toochange hello Issuer (iss) claim, modify hello value inside hello `<Item>` with hello Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="9c032-120">i valori applicabili Hello sono `AuthorityAndTenantGuid` e `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="9c032-120">hello applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="9c032-121">**Impostazione di attestazioni che rappresentano ID criterio** le opzioni di hello per l'impostazione di questo valore sono TFP (criteri di attendibilità framework) e ACR (riferimenti di contesto di autenticazione).</span><span class="sxs-lookup"><span data-stu-id="9c032-121">**Setting claim representing policy ID** hello options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="9c032-122">È consigliabile impostare il valore questo tooTFP, toodo, assicurarsi di hello `<Item>` con hello Key = "AuthenticationContextReferenceClaimPattern" esiste e il valore di hello è `None`.</span><span class="sxs-lookup"><span data-stu-id="9c032-122">We recommend setting this tooTFP, toodo this, ensure hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern" exists and hello value is `None`.</span></span>
<span data-ttu-id="9c032-123">Nell'elemento `<OutputClaims>`, aggiungere questo elemento:</span><span class="sxs-lookup"><span data-stu-id="9c032-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="9c032-124">Per record, rimuovere hello `<Item>` con hello Key = "AuthenticationContextReferenceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="9c032-124">For ACR, remove hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="9c032-125">**Attestazione soggetto (sub)** questa opzione è per impostazione predefinita tooObjectID, se si desidera tooswitch questo troppo`Not Supported`, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="9c032-125">**Subject (sub) claim** This option is defaulted tooObjectID, if you would like tooswitch this too`Not Supported`, do hello following:</span></span>

<span data-ttu-id="9c032-126">Sostituire questa riga</span><span class="sxs-lookup"><span data-stu-id="9c032-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="9c032-127">con la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="9c032-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="9c032-128">Comportamento della sessione e SSO</span><span class="sxs-lookup"><span data-stu-id="9c032-128">Session behavior and SSO</span></span>
<span data-ttu-id="9c032-129">toochange il comportamento di sessione e le configurazioni di SSO, è necessario tooadd un `<UserJourneyBehaviors>` elemento all'interno di hello `<RelyingParty>` elemento.</span><span class="sxs-lookup"><span data-stu-id="9c032-129">toochange your session behavior and SSO configurations, you need tooadd a `<UserJourneyBehaviors>` element inside of hello `<RelyingParty>` element.</span></span>  <span data-ttu-id="9c032-130">Hello `<UserJourneyBehaviors>` elemento deve seguire immediatamente hello `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="9c032-130">hello `<UserJourneyBehaviors>` element must immediately follow hello `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="9c032-131">Hello all'interno del `<UserJourneyBehavors>` elemento dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="9c032-131">hello inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="9c032-132">**Configurazione Single sign-on (SSO)** toochange hello configurazione single sign-on, è necessario toomodify hello valore `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="9c032-132">**Single sign-on (SSO) configuration** toochange hello single sign-on configuration, you need toomodify hello value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="9c032-133">i valori applicabili Hello sono `Tenant`, `Application`, `Policy` e `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="9c032-133">hello applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="9c032-134">**App Web durata della sessione (minuti)** toochange hello hello web app durata della sessione, è necessario toomodify valore hello `<SessionExpiryInSeconds>` elemento.</span><span class="sxs-lookup"><span data-stu-id="9c032-134">**Web app session lifetime (minutes)** toochange hello hello web app session lifetime, you need toomodify value of hello `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="9c032-135">il valore predefinito Hello nei criteri predefiniti è 86.400 secondi (1440 minuti).</span><span class="sxs-lookup"><span data-stu-id="9c032-135">hello default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="9c032-136">**Timeout della sessione Web app** toochange timeout di sessione di hello web app, è necessario toomodify hello valore `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="9c032-136">**Web app session timeout** toochange hello web app session timeout, you need toomodify hello value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="9c032-137">i valori applicabili Hello sono `Absolute` e `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="9c032-137">hello applicable values are `Absolute` and `Rolling`.</span></span>
