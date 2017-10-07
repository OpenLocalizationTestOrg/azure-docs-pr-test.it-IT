---
title: aaaAzure AD i metadati della federazione | Documenti Microsoft
description: Questo articolo descrive documento di metadati di federazione hello pubblica di Azure Active Directory per i servizi che accettano i token di Azure Active Directory.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c2d5f80b-aa74-452c-955b-d8eb3ed62652
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 23535bcd5eeb3e9b2e17d89a9b0420fc98bd3895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="federation-metadata"></a>Metadati della federazione
Azure Active Directory (Azure AD) pubblica un documento metadati federazione per servizi che è configurato i token di sicurezza hello tooaccept rilasciati da Azure AD. Hello formato del documento metadati federazione è descritto in hello [Web Services Federation Language (WS-Federation) versione 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), che estende [i metadati per hello OASIS Security Assertion Markup Language (SAML) v 2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a>Endpoint dei metadati specifici del tenant e indipendenti dal tenant
Azure AD pubblica endpoint specifici del tenant e indipendenti dal tenant.

Gli endpoint specifici del tenant sono progettati per un particolare tenant. i metadati di federazione specifici del tenant Hello includono informazioni sul tenant hello, nonché informazioni sull'endpoint emittente specifico del tenant. Le applicazioni che limitano l'accesso tooa single-tenant utilizzano endpoint specifici del tenant.

Endpoint indipendenti dal tenant forniscono informazioni che sono comune tenant di Azure Active Directory tooall. Queste informazioni si applicano tootenants ospitati *login.microsoftonline.com* e viene condiviso da più tenant. Per le applicazioni multi-tenant si consiglia di utilizzare endpoint indipendenti dal tenant, dal momento che non sono associate a un particolare tenant.

## <a name="federation-metadata-endpoints"></a>Endpoint dei metadati della federazione
Azure AD pubblica i metadati della federazione all'indirizzo `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.

Per **endpoint specifici del tenant**, hello `TenantDomainName` può essere uno dei seguenti tipi di hello:

* Un nome di dominio registrato di un tenant di Azure AD, ad esempio: `contoso.onmicrosoft.com`.
* Hello non modificabile del tenant ID del dominio hello, ad esempio `72f988bf-86f1-41af-91ab-2d7cd011db45`.

Per **endpoint indipendenti dal tenant**, hello `TenantDomainName` è `common`. Questo documento elenca solo gli elementi dei metadati di federazione hello che sono comuni tenant di Azure AD tooall vengono ospitati in login.microsoftonline.com.

Un endpoint specifico del tenant può essere ad esempio `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`. endpoint indipendente dal tenant Hello è [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml). È possibile visualizzare il documento di metadati federazione hello digitando l'URL in un browser.

## <a name="contents-of-federation-metadata"></a>Contenuto dei metadati della federazione
Hello seguente sezione vengono fornite informazioni necessarie per i servizi che utilizzano token hello rilasciati da Azure AD.

### <a name="entity-id"></a>ID entità
Hello `EntityDescriptor` elemento contiene un `EntityID` attributo. valore di hello Hello `EntityID` attributo rappresenta l'autorità emittente hello, vale a dire hello token di sicurezza (STS) servizio token emesso hello. È importante toovalidate dell'autorità di certificazione hello quando si riceve un token.

Hello metadati seguenti viene illustrato un esempio specifico del tenant `EntityDescriptor` elemento con un `EntityID` elemento.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
È possibile sostituire l'ID tenant hello in endpoint indipendente dal tenant hello toocreate di ID del tenant specifico del tenant `EntityID` valore. valore risultante di Hello verrà hello stesso hello emittente del token. strategia di Hello consente un'autorità emittente hello toovalidate di applicazione multi-tenant per un determinato tenant.

Hello metadati seguenti viene illustrato un esempio indipendente dal tenant `EntityID` elemento. Tenere presente che hello `{tenant}` è un valore letterale, non è un segnaposto.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a>Certificati per la firma di token
Quando un servizio riceve un token emesso da un tenant di Azure AD, hello firma di token hello deve essere convalidata con una chiave di firma pubblicata nel documento di metadati di federazione hello. metadati di federazione Hello includono parte pubblica di hello dei certificati di hello che i tenant hello utilizzare per la firma di token. byte non elaborati di Hello certificato vengono visualizzati in hello `KeyDescriptor` elemento. certificato di firma di token Hello è valido per la firma solo quando hello valore hello `use` attributo `signing`.

Un documento di metadati di federazione pubblicato da Azure AD può avere più chiavi di firme, ad esempio quando Azure AD è preparazione hello tooupdate certificato di firma. Quando un documento metadati federazione include più di un certificato, un servizio che convalida i token hello deve supportare tutti i certificati nel documento hello.

Hello metadati seguenti viene illustrato un esempio `KeyDescriptor` elemento con una chiave di firma.

```
<KeyDescriptor use="signing">
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
<X509Data>
<X509Certificate>
MIIDPjCCAiqgAwIBAgIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTIwNjA3MDcwMDAwWhcNMTQwNjA3MDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEArCz8Sn3GGXmikH2MdTeGY1D711EORX/lVXpr+ecGgqfUWF8MPB07XkYuJ54DAuYT318+2XrzMjOtqkT94VkXmxv6dFGhG8YZ8vNMPd4tdj9c0lpvWQdqXtL1TlFRpD/P6UMEigfN0c9oWDg9U7Ilymgei0UXtf1gtcQbc5sSQU0S4vr9YJp2gLFIGK11Iqg4XSGdcI0QWLLkkC6cBukhVnd6BCYbLjTYy3fNs4DzNdemJlxGl8sLexFytBF6YApvSdus3nFXaMCtBGx16HzkK9ne3lobAwL2o79bP4imEGqg+ibvyNmbrwFGnQrBc1jTF9LyQX9q+louxVfHs6ZiVwIDAQABo2IwYDBeBgNVHQEEVzBVgBCxDDsLd8xkfOLKm4Q/SzjtoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAA4IBAQAkJtxxm/ErgySlNk69+1odTMP8Oy6L0H17z7XGG3w4TqvTUSWaxD4hSFJ0e7mHLQLQD7oV/erACXwSZn2pMoZ89MBDjOMQA+e6QzGB7jmSzPTNmQgMLA8fWCfqPrz6zgH+1F1gNp8hJY57kfeVPBiyjuBmlTEBsBlzolY9dd/55qqfQk6cgSeCbHCy/RU/iep0+UsRMlSgPNNmqhj5gmN2AFVCN96zF694LwuPae5CeR2ZcVknexOWHYjFM0MgUSw0ubnGl0h9AJgGyhvNGcjQqu9vd1xkupFgaN+f7P3p3EVN5csBg5H94jEcQZT7EKeTiZ6bTrpDAnrr8tDCy8ng
</X509Certificate>
</X509Data>
</KeyInfo>
</KeyDescriptor>
  ```

Hello `KeyDescriptor` elemento viene visualizzato in due posizioni nel documento di metadati di federazione hello; sezione hello specifici di WS-Federation e hello specifica SAML. certificati Hello pubblicati in entrambe le sezioni verranno hello a stesso.

Nella sezione hello specifici di WS-Federation un lettore di metadati WS-Federation leggerà i certificati di hello da un `RoleDescriptor` elemento con hello `SecurityTokenServiceType` tipo.

Hello metadati seguenti viene illustrato un esempio `RoleDescriptor` elemento.

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

Nella sezione hello specifiche SAML un lettore di metadati WS-Federation leggerà i certificati di hello da un `IDPSSODescriptor` elemento.

Hello metadati seguenti viene illustrato un esempio `IDPSSODescriptor` elemento.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
Non esistono differenze nel formato hello di certificati specifici del tenant e indipendenti dal tenant.

### <a name="ws-federation-endpoint-url"></a>URL dell'endpoint WS-Federation
metadati di federazione Hello includono hello viene utilizzato l'URL di Azure Active Directory per single sign-in e single Sign-Out nel protocollo WS-Federation. Questo endpoint viene visualizzato in hello `PassiveRequestorEndpoint` elemento.

Hello metadati seguenti viene illustrato un esempio `PassiveRequestorEndpoint` elemento per un endpoint specifico del tenant.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
Per l'endpoint indipendente dal tenant hello, hello URL di WS-Federation viene visualizzato nell'endpoint hello WS-Federation, come illustrato nel seguente esempio hello.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a>URL dell'endpoint del protocollo SAML
metadati di federazione Hello includono hello URL usato da Azure AD per single sign-in e single Sign-Out nel protocollo SAML 2.0. Questi endpoint vengono visualizzati in hello `IDPSSODescriptor` elemento.

Hello, accesso e disconnessione URL vengono visualizzati in hello `SingleSignOnService` e `SingleLogoutService` elementi.

Hello metadati seguenti viene illustrato un esempio `PassiveResistorEndpoint` per un endpoint specifico del tenant.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

Allo stesso modo degli endpoint hello per endpoint del protocollo SAML 2.0 comuni hello vengono pubblicati nei metadati di federazione indipendenti dal tenant hello, come illustrato nel seguente esempio hello.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
