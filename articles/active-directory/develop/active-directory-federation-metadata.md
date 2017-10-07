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
# <a name="federation-metadata"></a><span data-ttu-id="b4c1c-103">Metadati della federazione</span><span class="sxs-lookup"><span data-stu-id="b4c1c-103">Federation metadata</span></span>
<span data-ttu-id="b4c1c-104">Azure Active Directory (Azure AD) pubblica un documento metadati federazione per servizi che è configurato i token di sicurezza hello tooaccept rilasciati da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured tooaccept hello security tokens that Azure AD issues.</span></span> <span data-ttu-id="b4c1c-105">Hello formato del documento metadati federazione è descritto in hello [Web Services Federation Language (WS-Federation) versione 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), che estende [i metadati per hello OASIS Security Assertion Markup Language (SAML) v 2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="b4c1c-105">hello federation metadata document format is described in hello [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for hello OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="b4c1c-106">Endpoint dei metadati specifici del tenant e indipendenti dal tenant</span><span class="sxs-lookup"><span data-stu-id="b4c1c-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="b4c1c-107">Azure AD pubblica endpoint specifici del tenant e indipendenti dal tenant.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="b4c1c-108">Gli endpoint specifici del tenant sono progettati per un particolare tenant.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="b4c1c-109">i metadati di federazione specifici del tenant Hello includono informazioni sul tenant hello, nonché informazioni sull'endpoint emittente specifico del tenant.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-109">hello tenant-specific federation metadata includes information about hello tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="b4c1c-110">Le applicazioni che limitano l'accesso tooa single-tenant utilizzano endpoint specifici del tenant.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-110">Applications that restrict access tooa single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="b4c1c-111">Endpoint indipendenti dal tenant forniscono informazioni che sono comune tenant di Azure Active Directory tooall.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-111">Tenant-independent endpoints provide information that is common tooall Azure AD tenants.</span></span> <span data-ttu-id="b4c1c-112">Queste informazioni si applicano tootenants ospitati *login.microsoftonline.com* e viene condiviso da più tenant.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-112">This information applies tootenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="b4c1c-113">Per le applicazioni multi-tenant si consiglia di utilizzare endpoint indipendenti dal tenant, dal momento che non sono associate a un particolare tenant.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="b4c1c-114">Endpoint dei metadati della federazione</span><span class="sxs-lookup"><span data-stu-id="b4c1c-114">Federation metadata endpoints</span></span>
<span data-ttu-id="b4c1c-115">Azure AD pubblica i metadati della federazione all'indirizzo `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="b4c1c-116">Per **endpoint specifici del tenant**, hello `TenantDomainName` può essere uno dei seguenti tipi di hello:</span><span class="sxs-lookup"><span data-stu-id="b4c1c-116">For **tenant-specific endpoints**, hello `TenantDomainName` can be one of hello following types:</span></span>

* <span data-ttu-id="b4c1c-117">Un nome di dominio registrato di un tenant di Azure AD, ad esempio: `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="b4c1c-118">Hello non modificabile del tenant ID del dominio hello, ad esempio `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-118">hello immutable tenant ID of hello domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="b4c1c-119">Per **endpoint indipendenti dal tenant**, hello `TenantDomainName` è `common`.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-119">For **tenant-independent endpoints**, hello `TenantDomainName` is `common`.</span></span> <span data-ttu-id="b4c1c-120">Questo documento elenca solo gli elementi dei metadati di federazione hello che sono comuni tenant di Azure AD tooall vengono ospitati in login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-120">This document lists only hello Federation Metadata elements that are common tooall Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="b4c1c-121">Un endpoint specifico del tenant può essere ad esempio `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="b4c1c-122">endpoint indipendente dal tenant Hello è [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="b4c1c-122">hello tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="b4c1c-123">È possibile visualizzare il documento di metadati federazione hello digitando l'URL in un browser.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-123">You can view hello federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="b4c1c-124">Contenuto dei metadati della federazione</span><span class="sxs-lookup"><span data-stu-id="b4c1c-124">Contents of federation Metadata</span></span>
<span data-ttu-id="b4c1c-125">Hello seguente sezione vengono fornite informazioni necessarie per i servizi che utilizzano token hello rilasciati da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-125">hello following section provides information needed by services that consume hello tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="b4c1c-126">ID entità</span><span class="sxs-lookup"><span data-stu-id="b4c1c-126">Entity ID</span></span>
<span data-ttu-id="b4c1c-127">Hello `EntityDescriptor` elemento contiene un `EntityID` attributo.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-127">hello `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="b4c1c-128">valore di hello Hello `EntityID` attributo rappresenta l'autorità emittente hello, vale a dire hello token di sicurezza (STS) servizio token emesso hello.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-128">hello value of hello `EntityID` attribute represents hello issuer, that is, hello security token service (STS) that issued hello token.</span></span> <span data-ttu-id="b4c1c-129">È importante toovalidate dell'autorità di certificazione hello quando si riceve un token.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-129">It is important toovalidate hello issuer when you receive a token.</span></span>

<span data-ttu-id="b4c1c-130">Hello metadati seguenti viene illustrato un esempio specifico del tenant `EntityDescriptor` elemento con un `EntityID` elemento.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-130">hello following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="b4c1c-131">È possibile sostituire l'ID tenant hello in endpoint indipendente dal tenant hello toocreate di ID del tenant specifico del tenant `EntityID` valore.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-131">You can replace hello tenant ID in hello tenant-independent endpoint with your tenant ID toocreate a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="b4c1c-132">valore risultante di Hello verrà hello stesso hello emittente del token.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-132">hello resulting value will be hello same as hello token issuer.</span></span> <span data-ttu-id="b4c1c-133">strategia di Hello consente un'autorità emittente hello toovalidate di applicazione multi-tenant per un determinato tenant.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-133">hello strategy allows a multi-tenant application toovalidate hello issuer for a given tenant.</span></span>

<span data-ttu-id="b4c1c-134">Hello metadati seguenti viene illustrato un esempio indipendente dal tenant `EntityID` elemento.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-134">hello following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="b4c1c-135">Tenere presente che hello `{tenant}` è un valore letterale, non è un segnaposto.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-135">Please note, that hello `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="b4c1c-136">Certificati per la firma di token</span><span class="sxs-lookup"><span data-stu-id="b4c1c-136">Token signing certificates</span></span>
<span data-ttu-id="b4c1c-137">Quando un servizio riceve un token emesso da un tenant di Azure AD, hello firma di token hello deve essere convalidata con una chiave di firma pubblicata nel documento di metadati di federazione hello.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-137">When a service receives a token that is issued by a Azure AD tenant, hello signature of hello token must be validated with a signing key that is published in hello federation metadata document.</span></span> <span data-ttu-id="b4c1c-138">metadati di federazione Hello includono parte pubblica di hello dei certificati di hello che i tenant hello utilizzare per la firma di token.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-138">hello federation metadata includes hello public portion of hello certificates that hello tenants use for token signing.</span></span> <span data-ttu-id="b4c1c-139">byte non elaborati di Hello certificato vengono visualizzati in hello `KeyDescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-139">hello certificate raw bytes appear in hello `KeyDescriptor` element.</span></span> <span data-ttu-id="b4c1c-140">certificato di firma di token Hello è valido per la firma solo quando hello valore hello `use` attributo `signing`.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-140">hello token signing certificate is valid for signing only when hello value of hello `use` attribute is `signing`.</span></span>

<span data-ttu-id="b4c1c-141">Un documento di metadati di federazione pubblicato da Azure AD può avere più chiavi di firme, ad esempio quando Azure AD è preparazione hello tooupdate certificato di firma.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing tooupdate hello signing certificate.</span></span> <span data-ttu-id="b4c1c-142">Quando un documento metadati federazione include più di un certificato, un servizio che convalida i token hello deve supportare tutti i certificati nel documento hello.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-142">When a federation metadata document includes more than one certificate, a service that is validating hello tokens should support all certificates in hello document.</span></span>

<span data-ttu-id="b4c1c-143">Hello metadati seguenti viene illustrato un esempio `KeyDescriptor` elemento con una chiave di firma.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-143">hello following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="b4c1c-144">Hello `KeyDescriptor` elemento viene visualizzato in due posizioni nel documento di metadati di federazione hello; sezione hello specifici di WS-Federation e hello specifica SAML.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-144">hello `KeyDescriptor` element appears in two places in hello federation metadata document; in hello WS-Federation-specific section and hello SAML-specific section.</span></span> <span data-ttu-id="b4c1c-145">certificati Hello pubblicati in entrambe le sezioni verranno hello a stesso.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-145">hello certificates published in both sections will be hello same.</span></span>

<span data-ttu-id="b4c1c-146">Nella sezione hello specifici di WS-Federation un lettore di metadati WS-Federation leggerà i certificati di hello da un `RoleDescriptor` elemento con hello `SecurityTokenServiceType` tipo.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-146">In hello WS-Federation-specific section, a WS-Federation metadata reader would read hello certificates from a `RoleDescriptor` element with hello `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="b4c1c-147">Hello metadati seguenti viene illustrato un esempio `RoleDescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-147">hello following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="b4c1c-148">Nella sezione hello specifiche SAML un lettore di metadati WS-Federation leggerà i certificati di hello da un `IDPSSODescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-148">In hello SAML-specific section, a WS-Federation metadata reader would read hello certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="b4c1c-149">Hello metadati seguenti viene illustrato un esempio `IDPSSODescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-149">hello following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="b4c1c-150">Non esistono differenze nel formato hello di certificati specifici del tenant e indipendenti dal tenant.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-150">There are no differences in hello format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="b4c1c-151">URL dell'endpoint WS-Federation</span><span class="sxs-lookup"><span data-stu-id="b4c1c-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="b4c1c-152">metadati di federazione Hello includono hello viene utilizzato l'URL di Azure Active Directory per single sign-in e single Sign-Out nel protocollo WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-152">hello federation metadata includes hello URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="b4c1c-153">Questo endpoint viene visualizzato in hello `PassiveRequestorEndpoint` elemento.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-153">This endpoint appears in hello `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="b4c1c-154">Hello metadati seguenti viene illustrato un esempio `PassiveRequestorEndpoint` elemento per un endpoint specifico del tenant.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-154">hello following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="b4c1c-155">Per l'endpoint indipendente dal tenant hello, hello URL di WS-Federation viene visualizzato nell'endpoint hello WS-Federation, come illustrato nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-155">For hello tenant-independent endpoint, hello WS-Federation URL appears in hello WS-Federation endpoint, as shown in hello following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="b4c1c-156">URL dell'endpoint del protocollo SAML</span><span class="sxs-lookup"><span data-stu-id="b4c1c-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="b4c1c-157">metadati di federazione Hello includono hello URL usato da Azure AD per single sign-in e single Sign-Out nel protocollo SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-157">hello federation metadata includes hello URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="b4c1c-158">Questi endpoint vengono visualizzati in hello `IDPSSODescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-158">These endpoints appear in hello `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="b4c1c-159">Hello, accesso e disconnessione URL vengono visualizzati in hello `SingleSignOnService` e `SingleLogoutService` elementi.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-159">hello sign-in and sign-out URLs appear in hello `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="b4c1c-160">Hello metadati seguenti viene illustrato un esempio `PassiveResistorEndpoint` per un endpoint specifico del tenant.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-160">hello following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="b4c1c-161">Allo stesso modo degli endpoint hello per endpoint del protocollo SAML 2.0 comuni hello vengono pubblicati nei metadati di federazione indipendenti dal tenant hello, come illustrato nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="b4c1c-161">Similarly hello endpoints for hello common SAML 2.0 protocol endpoints are published in hello tenant-independent federation metadata, as shown in hello following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
