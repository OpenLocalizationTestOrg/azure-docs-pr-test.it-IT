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
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a>Azure Active Directory B2C: gestire la personalizzazione dei token e SSO con i criteri personalizzati
Utilizzo di criteri personalizzati fornisce che si hello stesso controllo su token, sessione e single sign-on (SSO) le configurazioni di esempio tramite criteri predefiniti.  toolearn quali di ciascuna impostazione, vedere la documentazione di hello [qui](#active-directory-b2c-token-session-sso).

## <a name="token-lifetimes-and-claims-configuration"></a>Configurazione delle attestazioni e delle durate dei token
toochange impostazioni hello la durata dei token, è necessario tooadd un `<ClaimsProviders>` elemento hello relying party file criteri hello desiderate tooimpact.  Hello `<ClaimsProviders>` è un elemento figlio di hello `<TrustFrameworkPolicy>`.  All'interno, è necessario informazioni hello tooput che interessa la durata dei token.  Hello XML è simile al seguente:

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

**Durata dei token di accesso** hello accesso durata del token può essere cambiata modificando valore hello all'interno di hello `<Item>` con hello Key = "token_lifetime_secs" in secondi.  valore predefinito di Hello predefinito è 3600 secondi (60 minuti).

**Durata del token ID** durata del token ID hello può essere cambiata modificando valore hello all'interno di hello `<Item>` con hello Key = "id_token_lifetime_secs" in secondi.  valore predefinito di Hello predefinito è 3600 secondi (60 minuti).

**Durata del token di aggiornamento** durata del token hello aggiornamento può essere modificata modificando il valore di hello all'interno di hello `<Item>` con hello Key = "refresh_token_lifetime_secs" in secondi.  valore predefinito di Hello incorporato è 1209600 secondi (14 giorni).

**Aggiorna durata token di una finestra temporale scorrevole** se si desidera tooset un token di aggiornamento tooyour di durata finestra temporale scorrevole, modificare il valore di hello all'interno di `<Item>` con hello Key = "rolling_refresh_token_lifetime_secs" in secondi.  valore predefinito di Hello incorporato è 7776000 (90 giorni).  Se non si desidera tooenfore una variabile di durata di una finestra, sostituire questa riga con:
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

**Attestazione autorità di certificazione (iss)** se si desidera toochange hello dell'autorità di certificazione (iss di) attestazione, modificare il valore di hello all'interno di hello `<Item>` con hello Key = "IssuanceClaimPattern".  i valori applicabili Hello sono `AuthorityAndTenantGuid` e `AuthorityWithTfp`.

**Impostazione di attestazioni che rappresentano ID criterio** le opzioni di hello per l'impostazione di questo valore sono TFP (criteri di attendibilità framework) e ACR (riferimenti di contesto di autenticazione).  
È consigliabile impostare il valore questo tooTFP, toodo, assicurarsi di hello `<Item>` con hello Key = "AuthenticationContextReferenceClaimPattern" esiste e il valore di hello è `None`.
Nell'elemento `<OutputClaims>`, aggiungere questo elemento:
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
Per record, rimuovere hello `<Item>` con hello Key = "AuthenticationContextReferenceClaimPattern".

**Attestazione soggetto (sub)** questa opzione è per impostazione predefinita tooObjectID, se si desidera tooswitch questo troppo`Not Supported`, hello seguenti:

Sostituire questa riga 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
con la riga seguente:
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a>Comportamento della sessione e SSO
toochange il comportamento di sessione e le configurazioni di SSO, è necessario tooadd un `<UserJourneyBehaviors>` elemento all'interno di hello `<RelyingParty>` elemento.  Hello `<UserJourneyBehaviors>` elemento deve seguire immediatamente hello `<DefaultUserJourney>`.  Hello all'interno del `<UserJourneyBehavors>` elemento dovrebbe essere simile al seguente:

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
**Configurazione Single sign-on (SSO)** toochange hello configurazione single sign-on, è necessario toomodify hello valore `<SingleSignOn>`.  i valori applicabili Hello sono `Tenant`, `Application`, `Policy` e `Disabled`. 

**App Web durata della sessione (minuti)** toochange hello hello web app durata della sessione, è necessario toomodify valore hello `<SessionExpiryInSeconds>` elemento.  il valore predefinito Hello nei criteri predefiniti è 86.400 secondi (1440 minuti).

**Timeout della sessione Web app** toochange timeout di sessione di hello web app, è necessario toomodify hello valore `<SessionExpiryType>`.  i valori applicabili Hello sono `Absolute` e `Rolling`.
