---
title: Credenziali del certificato in Azure AD | Microsoft Docs
description: Questo articolo illustra la registrazione e l'uso delle credenziali del certificato per l'autenticazione dell'applicazione
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 88f0c64a-25f7-4974-aca2-2acadc9acbd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 08bb5140bb35bbd120aaa506afeab8ad247f81e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="43b21-103">Credenziali del certificato per l'autenticazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="43b21-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="43b21-104">Azure Active Directory consente a un'applicazione di usare le proprie credenziali per l'autenticazione, ad esempio, nel flusso di concessione delle credenziali client di OAuth 2.0 e nel flusso on-behalf-of.</span><span class="sxs-lookup"><span data-stu-id="43b21-104">Azure Active Directory allows an application to use its own credentials for authentication, for example, in the OAuth 2.0 Client Credentials Grant flow and the On-Behalf-Of flow.</span></span>
<span data-ttu-id="43b21-105">Un tipo di credenziale che può essere usato è un'asserzione di token JSON Web (JWT) firmata con un certificato di proprietà dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="43b21-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that the application owns.</span></span>

## <a name="format-of-the-assertion"></a><span data-ttu-id="43b21-106">Formato dell'asserzione</span><span class="sxs-lookup"><span data-stu-id="43b21-106">Format of the assertion</span></span>
<span data-ttu-id="43b21-107">Per calcolare l'asserzione, è preferibile usare una delle numerose librerie di [token JSON Web](https://jwt.io/) nel linguaggio scelto.</span><span class="sxs-lookup"><span data-stu-id="43b21-107">To compute the assertion, you probably want to use one of the many [JSON Web Token](https://jwt.io/) libraries in the language of your choice.</span></span> <span data-ttu-id="43b21-108">Le informazioni incluse nel token sono:</span><span class="sxs-lookup"><span data-stu-id="43b21-108">The information carried by the token is:</span></span>

#### <a name="header"></a><span data-ttu-id="43b21-109">Intestazione</span><span class="sxs-lookup"><span data-stu-id="43b21-109">Header</span></span>

| <span data-ttu-id="43b21-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="43b21-110">Parameter</span></span> |  <span data-ttu-id="43b21-111">Commento</span><span class="sxs-lookup"><span data-stu-id="43b21-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="43b21-112">Deve essere **RS256**</span><span class="sxs-lookup"><span data-stu-id="43b21-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="43b21-113">Deve essere **JWT**</span><span class="sxs-lookup"><span data-stu-id="43b21-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="43b21-114">Deve essere l'identificazione personale SHA-1 del certificato X.509</span><span class="sxs-lookup"><span data-stu-id="43b21-114">Should be the X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="43b21-115">Attestazioni (payload)</span><span class="sxs-lookup"><span data-stu-id="43b21-115">Claims (Payload)</span></span>

| <span data-ttu-id="43b21-116">Parametro</span><span class="sxs-lookup"><span data-stu-id="43b21-116">Parameter</span></span> |  <span data-ttu-id="43b21-117">Commento</span><span class="sxs-lookup"><span data-stu-id="43b21-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="43b21-118">Gruppo di destinatari: deve essere **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span><span class="sxs-lookup"><span data-stu-id="43b21-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="43b21-119">Data di scadenza: la data di scadenza del token.</span><span class="sxs-lookup"><span data-stu-id="43b21-119">Expiration date: the date when the token expires.</span></span> <span data-ttu-id="43b21-120">L'ora è rappresentata come numero di secondi dal 1° gennaio 1970 (1970-01-01T0:0:0Z) UTC fino all'ora in cui scade la validità del token.</span><span class="sxs-lookup"><span data-stu-id="43b21-120">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token validity expires.</span></span>|
| `iss` | <span data-ttu-id="43b21-121">Autorità di certificazione: deve essere il parametro client_id (ID applicazione del servizio client)</span><span class="sxs-lookup"><span data-stu-id="43b21-121">Issuer: should be the client_id (Application Id of the client service)</span></span> |
| `jti` | <span data-ttu-id="43b21-122">GUID: l'ID token JWT</span><span class="sxs-lookup"><span data-stu-id="43b21-122">GUID: the JWT ID</span></span> |
| `nbf` | <span data-ttu-id="43b21-123">Non prima: la data prima della quale il token non può essere usato.</span><span class="sxs-lookup"><span data-stu-id="43b21-123">Not Before: the date before which the token cannot be used.</span></span> <span data-ttu-id="43b21-124">La data e l'ora sono rappresentate come numero di secondi dal 1 gennaio 1970 (1970-01-01T0:0:0Z) UTC fino alla data e all'ora in cui il token è stato rilasciato.</span><span class="sxs-lookup"><span data-stu-id="43b21-124">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token was issued.</span></span> |
| `sub` | <span data-ttu-id="43b21-125">Oggetto: per quanto riguarda `iss`, deve essere il parametro client_id (ID applicazione del servizio client)</span><span class="sxs-lookup"><span data-stu-id="43b21-125">Subject: As for `iss`, should be the client_id (Application Id of the client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="43b21-126">Firma</span><span class="sxs-lookup"><span data-stu-id="43b21-126">Signature</span></span>
<span data-ttu-id="43b21-127">La firma viene calcolata applicando il certificato come descritto nella [specifica RFC7519 sul token JSON Web](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="43b21-127">The signature is computed applying the certificate as described in the [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="43b21-128">Esempio di asserzione del token JWT decodificata</span><span class="sxs-lookup"><span data-stu-id="43b21-128">Example of a decoded JWT assertion</span></span>
```
{
  "alg": "RS256",
  "typ": "JWT",
  "x5t": "gx8tGysyjcRqKjFPnd7RFwvwZI0"
}
.
{
  "aud": "https: //login.microsoftonline.com/contoso.onmicrosoft.com/oauth2/token",
  "exp": 1484593341,
  "iss": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05",
  "jti": "22b3bb26-e046-42df-9c96-65dbd72c1c81",
  "nbf": 1484592741,  
  "sub": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05"
}
.
"Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"

```

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="43b21-129">Esempio di asserzione del token JWT codificata</span><span class="sxs-lookup"><span data-stu-id="43b21-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="43b21-130">La stringa seguente è un esempio di asserzione codificata.</span><span class="sxs-lookup"><span data-stu-id="43b21-130">The following string is an example of encoded assertion.</span></span> <span data-ttu-id="43b21-131">Se si osserva con attenzione, è possibile notare tre sezioni separate da punti (.).</span><span class="sxs-lookup"><span data-stu-id="43b21-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="43b21-132">La prima sezione codifica l'intestazione, la seconda il payload e l'ultima è la firma calcolata con i certificati a partire dal contenuto delle prime due sezioni.</span><span class="sxs-lookup"><span data-stu-id="43b21-132">The first section encodes the header, the second the payload, and the last is the signature computed with the certificates from the content of the first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="43b21-133">Registrare il certificato con Azure AD</span><span class="sxs-lookup"><span data-stu-id="43b21-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="43b21-134">Per associare la credenziale del certificato all'applicazione client in Azure AD, è necessario modificare il manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="43b21-134">To associate the certificate credential with the client application in Azure AD, you need to edit the application manifest.</span></span>
<span data-ttu-id="43b21-135">Con un certificato disponibile, è necessario calcolare:</span><span class="sxs-lookup"><span data-stu-id="43b21-135">Having hold of a certificate, you need to compute:</span></span>
- <span data-ttu-id="43b21-136">`$base64Thumbprint`, che è la codifica Base 64 dell'hash del certificato</span><span class="sxs-lookup"><span data-stu-id="43b21-136">`$base64Thumbprint`, which is the base64 encoding of the certificate Hash</span></span>
- <span data-ttu-id="43b21-137">`$base64Value`, che è la codifica Base 64 dei dati non elaborati dell'hash del certificato</span><span class="sxs-lookup"><span data-stu-id="43b21-137">`$base64Value`, which is the base64 encoding of the certificate raw data</span></span>

<span data-ttu-id="43b21-138">È anche necessario specificare un GUID per identificare la chiave nel manifesto dell'applicazione (`$keyId`).</span><span class="sxs-lookup"><span data-stu-id="43b21-138">you also need to provide a GUID to identify the key in the application manifest (`$keyId`)</span></span>

<span data-ttu-id="43b21-139">Nella registrazione dell'app di Azure per l'applicazione client aprire il manifesto dell'applicazione e sostituire la proprietà *keyCredentials* con le informazioni del nuovo certificato usando lo schema seguente:</span><span class="sxs-lookup"><span data-stu-id="43b21-139">In the Azure app registration for the client application, open the application manifest, and replace the *keyCredentials* property with your new certificate information using the following schema:</span></span>
```
"keyCredentials": [
    {
        "customKeyIdentifier": "$base64Thumbprint",
        "keyId": "$keyid",
        "type": "AsymmetricX509Cert",
        "usage": "Verify",
        "value":  "$base64Value"
    }
]
```

<span data-ttu-id="43b21-140">Salvare le modifiche apportate al manifesto dell'applicazione e caricare in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43b21-140">Save the edits to the application manifest, and upload to Azure AD.</span></span> <span data-ttu-id="43b21-141">La proprietà keyCredentials è multivalore, quindi è possibile caricare più certificati per una gestione delle chiavi più completa.</span><span class="sxs-lookup"><span data-stu-id="43b21-141">The keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
