---
title: credenziali aaaCertificate in Azure AD | Documenti Microsoft
description: Questo articolo illustra la registrazione di hello e uso delle credenziali dei certificati per l'autenticazione dell'applicazione
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
ms.openlocfilehash: 3508803112ac06268d553db86ab74812aa53e455
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="a11b9-103">Credenziali del certificato per l'autenticazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a11b9-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="a11b9-104">Azure Active Directory consente un'applicazione toouse le proprie credenziali per l'autenticazione, ad esempio, nel flusso di concessione di credenziali Client OAuth 2.0 hello e flusso di On-Behalf-Of hello.</span><span class="sxs-lookup"><span data-stu-id="a11b9-104">Azure Active Directory allows an application toouse its own credentials for authentication, for example, in hello OAuth 2.0 Client Credentials Grant flow and hello On-Behalf-Of flow.</span></span>
<span data-ttu-id="a11b9-105">Un tipo di credenziale che può essere usato è un'asserzione di Token(JWT) Web JSON firmata con un certificato che possiede un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a11b9-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that hello application owns.</span></span>

## <a name="format-of-hello-assertion"></a><span data-ttu-id="a11b9-106">Formato dell'asserzione hello</span><span class="sxs-lookup"><span data-stu-id="a11b9-106">Format of hello assertion</span></span>
<span data-ttu-id="a11b9-107">asserzione hello toocompute, si vorrà toouse uno di hello molti [Token Web JSON](https://jwt.io/) librerie in linguaggio hello di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="a11b9-107">toocompute hello assertion, you probably want toouse one of hello many [JSON Web Token](https://jwt.io/) libraries in hello language of your choice.</span></span> <span data-ttu-id="a11b9-108">informazioni Hello trasportate dal token hello sono:</span><span class="sxs-lookup"><span data-stu-id="a11b9-108">hello information carried by hello token is:</span></span>

#### <a name="header"></a><span data-ttu-id="a11b9-109">Intestazione</span><span class="sxs-lookup"><span data-stu-id="a11b9-109">Header</span></span>

| <span data-ttu-id="a11b9-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="a11b9-110">Parameter</span></span> |  <span data-ttu-id="a11b9-111">Commento</span><span class="sxs-lookup"><span data-stu-id="a11b9-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="a11b9-112">Deve essere **RS256**</span><span class="sxs-lookup"><span data-stu-id="a11b9-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="a11b9-113">Deve essere **JWT**</span><span class="sxs-lookup"><span data-stu-id="a11b9-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="a11b9-114">Deve essere l'identificazione personale del certificato x. 509. SHA-1 hello</span><span class="sxs-lookup"><span data-stu-id="a11b9-114">Should be hello X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="a11b9-115">Attestazioni (payload)</span><span class="sxs-lookup"><span data-stu-id="a11b9-115">Claims (Payload)</span></span>

| <span data-ttu-id="a11b9-116">Parametro</span><span class="sxs-lookup"><span data-stu-id="a11b9-116">Parameter</span></span> |  <span data-ttu-id="a11b9-117">Commento</span><span class="sxs-lookup"><span data-stu-id="a11b9-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="a11b9-118">Gruppo di destinatari: deve essere **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span><span class="sxs-lookup"><span data-stu-id="a11b9-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="a11b9-119">Data di scadenza: data hello scadenza token hello.</span><span class="sxs-lookup"><span data-stu-id="a11b9-119">Expiration date: hello date when hello token expires.</span></span> <span data-ttu-id="a11b9-120">tempo Hello è rappresentato come numero di secondi di hello dal 1 gennaio 1970 (1970-01-01T0:0:0Z) UTC fino alla scadenza hello hello token validità.</span><span class="sxs-lookup"><span data-stu-id="a11b9-120">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token validity expires.</span></span>|
| `iss` | <span data-ttu-id="a11b9-121">Autorità di certificazione: deve essere client_id hello (Id applicazione del servizio client hello)</span><span class="sxs-lookup"><span data-stu-id="a11b9-121">Issuer: should be hello client_id (Application Id of hello client service)</span></span> |
| `jti` | <span data-ttu-id="a11b9-122">GUID: hello ID JWT</span><span class="sxs-lookup"><span data-stu-id="a11b9-122">GUID: hello JWT ID</span></span> |
| `nbf` | <span data-ttu-id="a11b9-123">Non prima: data hello prima quali hello token non può essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="a11b9-123">Not Before: hello date before which hello token cannot be used.</span></span> <span data-ttu-id="a11b9-124">tempo Hello è rappresentato come numero di secondi di hello dal 1 gennaio 1970 (1970-01-01T0:0:0Z) UTC fino a quando non è stato rilasciato hello ora hello token.</span><span class="sxs-lookup"><span data-stu-id="a11b9-124">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token was issued.</span></span> |
| `sub` | <span data-ttu-id="a11b9-125">Oggetto: del `iss`, deve essere client_id hello (Id applicazione del servizio client hello)</span><span class="sxs-lookup"><span data-stu-id="a11b9-125">Subject: As for `iss`, should be hello client_id (Application Id of hello client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="a11b9-126">Firma</span><span class="sxs-lookup"><span data-stu-id="a11b9-126">Signature</span></span>
<span data-ttu-id="a11b9-127">firma Hello viene calcolata l'applicazione certificato hello come descritto in hello [JSON Web Token RFC7519 specifica](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="a11b9-127">hello signature is computed applying hello certificate as described in hello [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="a11b9-128">Esempio di asserzione del token JWT decodificata</span><span class="sxs-lookup"><span data-stu-id="a11b9-128">Example of a decoded JWT assertion</span></span>
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

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="a11b9-129">Esempio di asserzione del token JWT codificata</span><span class="sxs-lookup"><span data-stu-id="a11b9-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="a11b9-130">Hello stringa seguente è riportato un esempio di asserzione codificato.</span><span class="sxs-lookup"><span data-stu-id="a11b9-130">hello following string is an example of encoded assertion.</span></span> <span data-ttu-id="a11b9-131">Se si osserva con attenzione, è possibile notare tre sezioni separate da punti (.).</span><span class="sxs-lookup"><span data-stu-id="a11b9-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="a11b9-132">prima sezione Hello codifica hello intestazione, hello secondo hello payload, e per ultimo è hello firma hello calcolata con certificati hello dal contenuto hello delle prime due sezioni di hello.</span><span class="sxs-lookup"><span data-stu-id="a11b9-132">hello first section encodes hello header, hello second hello payload, and hello last is hello signature computed with hello certificates from hello content of hello first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="a11b9-133">Registrare il certificato con Azure AD</span><span class="sxs-lookup"><span data-stu-id="a11b9-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="a11b9-134">credenziali di certificato tooassociate hello con un'applicazione client hello in Azure AD, è necessario tooedit manifesto dell'applicazione di hello.</span><span class="sxs-lookup"><span data-stu-id="a11b9-134">tooassociate hello certificate credential with hello client application in Azure AD, you need tooedit hello application manifest.</span></span>
<span data-ttu-id="a11b9-135">Con l'attesa di un certificato, è necessario toocompute:</span><span class="sxs-lookup"><span data-stu-id="a11b9-135">Having hold of a certificate, you need toocompute:</span></span>
- <span data-ttu-id="a11b9-136">`$base64Thumbprint`, che è hello codifica base64 del certificato hello Hash</span><span class="sxs-lookup"><span data-stu-id="a11b9-136">`$base64Thumbprint`, which is hello base64 encoding of hello certificate Hash</span></span>
- <span data-ttu-id="a11b9-137">`$base64Value`, che è hello codifica base64 di dati non elaborati certificato hello</span><span class="sxs-lookup"><span data-stu-id="a11b9-137">`$base64Value`, which is hello base64 encoding of hello certificate raw data</span></span>

<span data-ttu-id="a11b9-138">è inoltre necessario disporre di una chiave di hello tooidentify GUID nel manifesto dell'applicazione hello tooprovide (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="a11b9-138">you also need tooprovide a GUID tooidentify hello key in hello application manifest (`$keyId`)</span></span>

<span data-ttu-id="a11b9-139">Nella registrazione dell'app Azure per un'applicazione client hello hello, aprire il manifesto dell'applicazione hello e sostituire hello *keyCredentials* proprietà con le informazioni del nuovo certificato utilizzando hello seguente schema:</span><span class="sxs-lookup"><span data-stu-id="a11b9-139">In hello Azure app registration for hello client application, open hello application manifest, and replace hello *keyCredentials* property with your new certificate information using hello following schema:</span></span>
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

<span data-ttu-id="a11b9-140">Salvare il manifesto di applicazione hello modifiche toohello e caricare tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a11b9-140">Save hello edits toohello application manifest, and upload tooAzure AD.</span></span> <span data-ttu-id="a11b9-141">proprietà keyCredentials Hello è multivalore, pertanto è possibile caricare più certificati per la gestione delle chiavi più dettagliato.</span><span class="sxs-lookup"><span data-stu-id="a11b9-141">hello keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
