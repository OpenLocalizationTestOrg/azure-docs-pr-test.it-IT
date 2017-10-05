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
ms.openlocfilehash: 8f5703d15766f221517cd89352d41685652d32d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="e8648-102">Azure Active Directory B2C: gestire la personalizzazione dei token e SSO con i criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="e8648-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="e8648-103">L'uso dei criteri personalizzati offre lo stesso controllo sulle configurazioni di token, sessioni e Single Sign-On (SSO) dei criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="e8648-103">Using custom policies provides you the same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="e8648-104">Per informazioni sulle singole impostazioni, vedere la documentazione [qui](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="e8648-104">To learn what each setting does, please see the documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="e8648-105">Configurazione delle attestazioni e delle durate dei token</span><span class="sxs-lookup"><span data-stu-id="e8648-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="e8648-106">Per modificare le impostazioni delle durate dei token, è necessario aggiungere un elemento `<ClaimsProviders>` nel file di relying party del criterio su cui si vuole intervenire.</span><span class="sxs-lookup"><span data-stu-id="e8648-106">To change the settings on your token lifetimes, you need to add a `<ClaimsProviders>` element in the relying party file of the policy you want to impact.</span></span>  <span data-ttu-id="e8648-107">`<ClaimsProviders>` è un elemento figlio di `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="e8648-107">The `<ClaimsProviders>` element is a child of the `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="e8648-108">Sarà necessario inserirvi le informazioni che interessano le durate dei token.</span><span class="sxs-lookup"><span data-stu-id="e8648-108">Inside you'll need to put the information that affects your token lifetimes.</span></span>  <span data-ttu-id="e8648-109">Il codice XML è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e8648-109">The XML looks like this:</span></span>

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

<span data-ttu-id="e8648-110">**Durate dei token di accesso** La durata dei token di accesso può essere cambiata modificando il valore nell'elemento `<Item>` con Key="token_lifetime_secs" espresso in secondi.</span><span class="sxs-lookup"><span data-stu-id="e8648-110">**Access token lifetimes** The access token lifetime can be changed by modifying the value inside the `<Item>` with the Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="e8648-111">Il valore predefinito è pari a 3600 secondi (60 minuti).</span><span class="sxs-lookup"><span data-stu-id="e8648-111">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="e8648-112">**Durata dei token di ID** La durata dei token di ID può essere cambiata modificando il valore nell'elemento `<Item>` con Key="id_token_lifetime_secs" espresso in secondi.</span><span class="sxs-lookup"><span data-stu-id="e8648-112">**ID token lifetime** The ID token lifetime can be changed by modifying the value inside the `<Item>` with the Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="e8648-113">Il valore predefinito è pari a 3600 secondi (60 minuti).</span><span class="sxs-lookup"><span data-stu-id="e8648-113">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="e8648-114">**Durata del token di aggiornamento** La durata del token di aggiornamento può essere cambiata modificando il valore nell'elemento `<Item>` con Key="refresh_token_lifetime_secs" espresso in secondi.</span><span class="sxs-lookup"><span data-stu-id="e8648-114">**Refresh token lifetime** The refresh token lifetime can be changed by modifying the value inside the `<Item>` with the Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="e8648-115">Il valore predefinito è pari a 1209600 secondi (14 giorni).</span><span class="sxs-lookup"><span data-stu-id="e8648-115">The default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="e8648-116">**Durata della finestra temporale scorrevole del token di aggiornamento** Per impostare una durata della finestra temporale scorrevole per il token di aggiornamento, modificare il valore nell'elemento `<Item>` con Key="rolling_refresh_token_lifetime_secs" espresso in secondi.</span><span class="sxs-lookup"><span data-stu-id="e8648-116">**Refresh token sliding window lifetime** If you would like to set a sliding window lifetime to your refresh token, modify the value inside `<Item>` with the Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="e8648-117">Il valore predefinito è pari a 7776000 secondi (90 giorni).</span><span class="sxs-lookup"><span data-stu-id="e8648-117">The default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="e8648-118">Se non si vuole applicare una durata della finestra temporale scorrevole, sostituire questa riga con:</span><span class="sxs-lookup"><span data-stu-id="e8648-118">If you don't want to enfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="e8648-119">**Attestazione autorità di certificazione (iss)** Per cambiare l'attestazione autorità di certificazione (iss), modificare il valore nell'elemento `<Item>` con Key="IssuanceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="e8648-119">**Issuer (iss) claim** If you want to change the Issuer (iss) claim, modify the value inside the `<Item>` with the Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="e8648-120">I valori applicabili sono `AuthorityAndTenantGuid` e `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="e8648-120">The applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="e8648-121">**Impostazione dell'attestazione che rappresenta l'ID criteri** Le opzioni per impostare questo valore sono TFP (Trust Framework Policy) e ACR (Authentication Context Reference).</span><span class="sxs-lookup"><span data-stu-id="e8648-121">**Setting claim representing policy ID** The options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="e8648-122">È consigliabile impostarlo su TFP. A questo scopo, assicurarsi che l'elemento `<Item>` con Key="AuthenticationContextReferenceClaimPattern" esista e il valore sia `None`.</span><span class="sxs-lookup"><span data-stu-id="e8648-122">We recommend setting this to TFP, to do this, ensure the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern" exists and the value is `None`.</span></span>
<span data-ttu-id="e8648-123">Nell'elemento `<OutputClaims>`, aggiungere questo elemento:</span><span class="sxs-lookup"><span data-stu-id="e8648-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="e8648-124">Per ACR, rimuovere l'elemento `<Item>` con Key="AuthenticationContextReferenceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="e8648-124">For ACR, remove the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="e8648-125">**Attestazione soggetto (sub)** L'impostazione predefinita di questa opzione è ObjectID. Per impostarla su `Not Supported`, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e8648-125">**Subject (sub) claim** This option is defaulted to ObjectID, if you would like to switch this to `Not Supported`, do the following:</span></span>

<span data-ttu-id="e8648-126">Sostituire questa riga</span><span class="sxs-lookup"><span data-stu-id="e8648-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="e8648-127">con la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="e8648-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="e8648-128">Comportamento della sessione e SSO</span><span class="sxs-lookup"><span data-stu-id="e8648-128">Session behavior and SSO</span></span>
<span data-ttu-id="e8648-129">Per modificare il comportamento della sessione e le configurazioni SSO, è necessario aggiungere un elemento `<UserJourneyBehaviors>` nell'elemento `<RelyingParty>`.</span><span class="sxs-lookup"><span data-stu-id="e8648-129">To change your session behavior and SSO configurations, you need to add a `<UserJourneyBehaviors>` element inside of the `<RelyingParty>` element.</span></span>  <span data-ttu-id="e8648-130">L'elemento `<UserJourneyBehaviors>` deve seguire immediatamente `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="e8648-130">The `<UserJourneyBehaviors>` element must immediately follow the `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="e8648-131">Il contenuto dell'elemento `<UserJourneyBehavors>` sarà il seguente:</span><span class="sxs-lookup"><span data-stu-id="e8648-131">The inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="e8648-132">**Configurazione dell'accesso Single Sign-On** Per cambiare la configurazione dell'accesso Single Sign-On, è necessario modificare il valore di `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="e8648-132">**Single sign-on (SSO) configuration** To change the single sign-on configuration, you need to modify the value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="e8648-133">I valori applicabili sono `Tenant`, `Application` `Policy` e `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="e8648-133">The applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="e8648-134">**Durata della sessione dell'app Web (minuti)** Per cambiare la durata della sessione dell'app Web, è necessario modificare il valore dell'elemento `<SessionExpiryInSeconds>`.</span><span class="sxs-lookup"><span data-stu-id="e8648-134">**Web app session lifetime (minutes)** To change the the web app session lifetime, you need to modify value of the `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="e8648-135">Il valore predefinito nei criteri predefiniti è pari a 86400 secondi (1440 minuti).</span><span class="sxs-lookup"><span data-stu-id="e8648-135">The default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="e8648-136">**Timeout della sessione dell'app Web** Per cambiare il timeout della sessione dell'app Web, è necessario modificare il valore di `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="e8648-136">**Web app session timeout** To change the web app session timeout, you need to modify the value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="e8648-137">I valori applicabili sono `Absolute` e `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="e8648-137">The applicable values are `Absolute` and `Rolling`.</span></span>
