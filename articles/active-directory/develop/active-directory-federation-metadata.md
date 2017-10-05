---
title: Metadati della federazione di Azure AD | Documentazione Microsoft
description: Questo articolo descrive il documento di metadati della federazione pubblicato da Azure Active Directory per i servizi che accettano i token di Azure Active Directory.
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
ms.openlocfilehash: ecafb02a6ac13d1c3cd1fe77ef710cd8525e32b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="ed1b5-103">Metadati della federazione</span><span class="sxs-lookup"><span data-stu-id="ed1b5-103">Federation metadata</span></span>
<span data-ttu-id="ed1b5-104">Azure Active Directory (Azure AD) pubblica un documento di metadati della federazione per i servizi configurati per accettare i token di sicurezza rilasciati da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured to accept the security tokens that Azure AD issues.</span></span> <span data-ttu-id="ed1b5-105">Il formato del documento di metadati della federazione è descritto in [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) (Linguaggio Web Services Federation (WS-Federation) versione 1.2), che estende la pubblicazione [Metadata for the OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf) (Metadati per il linguaggio SAML (Security Assertion Markup Language) OASIS v 2.0).</span><span class="sxs-lookup"><span data-stu-id="ed1b5-105">The federation metadata document format is described in the [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for the OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="ed1b5-106">Endpoint dei metadati specifici del tenant e indipendenti dal tenant</span><span class="sxs-lookup"><span data-stu-id="ed1b5-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="ed1b5-107">Azure AD pubblica endpoint specifici del tenant e indipendenti dal tenant.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="ed1b5-108">Gli endpoint specifici del tenant sono progettati per un particolare tenant.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="ed1b5-109">I metadati di federazione specifici del tenant includono informazioni sul tenant, incluse le informazioni specifiche del tenant relative all'autorità emittente e all’endpoint.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-109">The tenant-specific federation metadata includes information about the tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="ed1b5-110">Le applicazioni che limitano l'accesso a un singolo tenant utilizzano endpoint specifici del tenant.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-110">Applications that restrict access to a single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="ed1b5-111">Gli endpoint indipendenti dal tenant forniscono informazioni comuni a tutti i tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-111">Tenant-independent endpoints provide information that is common to all Azure AD tenants.</span></span> <span data-ttu-id="ed1b5-112">Queste informazioni si applicano ai tenant ospitati in *login.microsoftonline.com* e vengono condivise tra i tenant.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-112">This information applies to tenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="ed1b5-113">Per le applicazioni multi-tenant si consiglia di utilizzare endpoint indipendenti dal tenant, dal momento che non sono associate a un particolare tenant.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="ed1b5-114">Endpoint dei metadati della federazione</span><span class="sxs-lookup"><span data-stu-id="ed1b5-114">Federation metadata endpoints</span></span>
<span data-ttu-id="ed1b5-115">Azure AD pubblica i metadati della federazione all'indirizzo `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="ed1b5-116">Per gli **endpoint specifici del tenant**, `TenantDomainName` può essere uno dei seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="ed1b5-116">For **tenant-specific endpoints**, the `TenantDomainName` can be one of the following types:</span></span>

* <span data-ttu-id="ed1b5-117">Un nome di dominio registrato di un tenant di Azure AD, ad esempio: `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="ed1b5-118">L'ID tenant non modificabile del dominio, ad esempio `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-118">The immutable tenant ID of the domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="ed1b5-119">Per gli **endpoint indipendenti dal tenant**, `TenantDomainName` è `common`.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-119">For **tenant-independent endpoints**, the `TenantDomainName` is `common`.</span></span> <span data-ttu-id="ed1b5-120">Questo documento elenca solo gli elementi dei metadati della federazione che sono comuni a tutti i tenant di Azure AD ospitati in login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-120">This document lists only the Federation Metadata elements that are common to all Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="ed1b5-121">Un endpoint specifico del tenant può essere ad esempio `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="ed1b5-122">L'endpoint indipendente dal tenant è [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="ed1b5-122">The tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="ed1b5-123">È possibile visualizzare il documento di metadati della federazione digitando questo URL in un browser.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-123">You can view the federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="ed1b5-124">Contenuto dei metadati della federazione</span><span class="sxs-lookup"><span data-stu-id="ed1b5-124">Contents of federation Metadata</span></span>
<span data-ttu-id="ed1b5-125">Nella sezione seguente vengono fornite le informazioni necessarie per i servizi che utilizzano token emessi da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-125">The following section provides information needed by services that consume the tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="ed1b5-126">ID entità</span><span class="sxs-lookup"><span data-stu-id="ed1b5-126">Entity ID</span></span>
<span data-ttu-id="ed1b5-127">L'elemento `EntityDescriptor` contiene un attributo `EntityID`.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-127">The `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="ed1b5-128">Il valore dell'attributo `EntityID` rappresenta l'autorità di certificazione, vale a dire il servizio token di sicurezza che ha rilasciato il token.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-128">The value of the `EntityID` attribute represents the issuer, that is, the security token service (STS) that issued the token.</span></span> <span data-ttu-id="ed1b5-129">È importante convalidare l'autorità di certificazione, quando si riceve un token.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-129">It is important to validate the issuer when you receive a token.</span></span>

<span data-ttu-id="ed1b5-130">I metadati seguenti indicano un elemento `EntityDescriptor` di esempio specifico del tenant con un elemento `EntityID`.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-130">The following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="ed1b5-131">È possibile sostituire l'ID tenant nell'endpoint indipendente dal tenant con il proprio ID tenant per creare un valore `EntityID` specifico del tenant.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-131">You can replace the tenant ID in the tenant-independent endpoint with your tenant ID to create a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="ed1b5-132">Il valore risultante sarà lo stesso dell’autorità emittente del token.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-132">The resulting value will be the same as the token issuer.</span></span> <span data-ttu-id="ed1b5-133">La strategia consente a un'applicazione multi-tenant di convalidare l'autorità di certificazione per un tenant specificato.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-133">The strategy allows a multi-tenant application to validate the issuer for a given tenant.</span></span>

<span data-ttu-id="ed1b5-134">I metadati seguenti indicano un esempio di elemento `EntityID` indipendente dal tenant.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-134">The following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="ed1b5-135">Si noti che `{tenant}` è un valore letterale e non un segnaposto.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-135">Please note, that the `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="ed1b5-136">Certificati per la firma di token</span><span class="sxs-lookup"><span data-stu-id="ed1b5-136">Token signing certificates</span></span>
<span data-ttu-id="ed1b5-137">Quando un servizio riceve un token emesso da un tenant di Azure AD, è necessario convalidare la firma del token con una chiave per la firma che viene pubblicata nel documento dei metadati di federazione.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-137">When a service receives a token that is issued by a Azure AD tenant, the signature of the token must be validated with a signing key that is published in the federation metadata document.</span></span> <span data-ttu-id="ed1b5-138">I metadati di federazione includono la parte pubblica dei certificati utilizzati dai tenant per la firma dei token.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-138">The federation metadata includes the public portion of the certificates that the tenants use for token signing.</span></span> <span data-ttu-id="ed1b5-139">I byte non elaborati del certificato vengono visualizzati nell'elemento `KeyDescriptor` .</span><span class="sxs-lookup"><span data-stu-id="ed1b5-139">The certificate raw bytes appear in the `KeyDescriptor` element.</span></span> <span data-ttu-id="ed1b5-140">Il certificato per la firma di token è valido per la firma solo quando il valore dell'attributo `use` è `signing`.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-140">The token signing certificate is valid for signing only when the value of the `use` attribute is `signing`.</span></span>

<span data-ttu-id="ed1b5-141">Un documento di metadati della federazione pubblicato da Azure AD può avere più chiavi per la firma, ad esempio quando Azure AD sta per aggiornare il certificato di firma.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing to update the signing certificate.</span></span> <span data-ttu-id="ed1b5-142">Quando un documento di metadati di federazione include certificati, un servizio che convalida i token deve supportare tutti i certificati nel documento.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-142">When a federation metadata document includes more than one certificate, a service that is validating the tokens should support all certificates in the document.</span></span>

<span data-ttu-id="ed1b5-143">I metadati seguenti indicano un esempio di elemento `KeyDescriptor` con una chiave di firma.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-143">The following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="ed1b5-144">L'elemento `KeyDescriptor` appare in due punti del documento di metadati della federazione: nella sezione specifica di WS-Federation e in quella specifica di SAML.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-144">The `KeyDescriptor` element appears in two places in the federation metadata document; in the WS-Federation-specific section and the SAML-specific section.</span></span> <span data-ttu-id="ed1b5-145">I certificati pubblicati in entrambe le sezioni saranno uguali.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-145">The certificates published in both sections will be the same.</span></span>

<span data-ttu-id="ed1b5-146">Nella sezione specifica di WS-Federation un lettore di metadati di WS-Federation legge i certificati da un elemento `RoleDescriptor` con il tipo `SecurityTokenServiceType`.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-146">In the WS-Federation-specific section, a WS-Federation metadata reader would read the certificates from a `RoleDescriptor` element with the `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="ed1b5-147">I metadati seguenti indicano un esempio di elemento `RoleDescriptor` .</span><span class="sxs-lookup"><span data-stu-id="ed1b5-147">The following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="ed1b5-148">Nella sezione specifica di SAML, un lettore di metadati di WS-Federation legge i certificati da un elemento `IDPSSODescriptor` .</span><span class="sxs-lookup"><span data-stu-id="ed1b5-148">In the SAML-specific section, a WS-Federation metadata reader would read the certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="ed1b5-149">I metadati seguenti indicano un esempio di elemento `IDPSSODescriptor` .</span><span class="sxs-lookup"><span data-stu-id="ed1b5-149">The following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="ed1b5-150">Non esistono differenze nel formato di certificati specifici del tenant e indipendenti dal tenant.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-150">There are no differences in the format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="ed1b5-151">URL dell'endpoint WS-Federation</span><span class="sxs-lookup"><span data-stu-id="ed1b5-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="ed1b5-152">I metadati di federazione includono l'URL utilizzato da Azure AD per il Single Sign-In e il Single Sign-Out nel protocollo WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-152">The federation metadata includes the URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="ed1b5-153">Questo endpoint viene visualizzato nell'elemento `PassiveRequestorEndpoint` .</span><span class="sxs-lookup"><span data-stu-id="ed1b5-153">This endpoint appears in the `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="ed1b5-154">I metadati seguenti indicano un elemento `PassiveRequestorEndpoint` di esempio per un endpoint specifico del tenant.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-154">The following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="ed1b5-155">Per l'endpoint indipendente dal tenant, l'URL di WS-Federation viene visualizzato nell'endpoint WS-Federation, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-155">For the tenant-independent endpoint, the WS-Federation URL appears in the WS-Federation endpoint, as shown in the following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="ed1b5-156">URL dell'endpoint del protocollo SAML</span><span class="sxs-lookup"><span data-stu-id="ed1b5-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="ed1b5-157">I metadati di federazione includono l'URL utilizzato da Azure AD per il Single Sign-In e il Single Sign-Out nel protocollo SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-157">The federation metadata includes the URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="ed1b5-158">Questi endpoint vengono visualizzati nell'elemento `IDPSSODescriptor` .</span><span class="sxs-lookup"><span data-stu-id="ed1b5-158">These endpoints appear in the `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="ed1b5-159">Gli URL di accesso e di disconnessione vengono visualizzati negli elementi `SingleSignOnService` e `SingleLogoutService`.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-159">The sign-in and sign-out URLs appear in the `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="ed1b5-160">I metadati seguenti indicano un `PassiveResistorEndpoint` di esempio per un endpoint specifico del tenant.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-160">The following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="ed1b5-161">Allo stesso modo, gli endpoint per gli endpoint del protocollo SAML 2.0 comune vengono pubblicati nei metadati di federazione indipendenti dal tenant, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="ed1b5-161">Similarly the endpoints for the common SAML 2.0 protocol endpoints are published in the tenant-independent federation metadata, as shown in the following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
