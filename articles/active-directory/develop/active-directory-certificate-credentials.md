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
# <a name="certificate-credentials-for-application-authentication"></a>Credenziali del certificato per l'autenticazione dell'applicazione

Azure Active Directory consente un'applicazione toouse le proprie credenziali per l'autenticazione, ad esempio, nel flusso di concessione di credenziali Client OAuth 2.0 hello e flusso di On-Behalf-Of hello.
Un tipo di credenziale che può essere usato è un'asserzione di Token(JWT) Web JSON firmata con un certificato che possiede un'applicazione hello.

## <a name="format-of-hello-assertion"></a>Formato dell'asserzione hello
asserzione hello toocompute, si vorrà toouse uno di hello molti [Token Web JSON](https://jwt.io/) librerie in linguaggio hello di propria scelta. informazioni Hello trasportate dal token hello sono:

#### <a name="header"></a>Intestazione

| Parametro |  Commento |
| --- | --- | --- |
| `alg` | Deve essere **RS256** |
| `typ` | Deve essere **JWT** |
| `x5t` | Deve essere l'identificazione personale del certificato x. 509. SHA-1 hello |

#### <a name="claims-payload"></a>Attestazioni (payload)

| Parametro |  Commento |
| --- | --- | --- |
| `aud` | Gruppo di destinatari: deve essere **https://login.microsoftonline.com/*tenant_Id*/oauth2/token** |
| `exp` | Data di scadenza: data hello scadenza token hello. tempo Hello è rappresentato come numero di secondi di hello dal 1 gennaio 1970 (1970-01-01T0:0:0Z) UTC fino alla scadenza hello hello token validità.|
| `iss` | Autorità di certificazione: deve essere client_id hello (Id applicazione del servizio client hello) |
| `jti` | GUID: hello ID JWT |
| `nbf` | Non prima: data hello prima quali hello token non può essere utilizzato. tempo Hello è rappresentato come numero di secondi di hello dal 1 gennaio 1970 (1970-01-01T0:0:0Z) UTC fino a quando non è stato rilasciato hello ora hello token. |
| `sub` | Oggetto: del `iss`, deve essere client_id hello (Id applicazione del servizio client hello) |

#### <a name="signature"></a>Firma
firma Hello viene calcolata l'applicazione certificato hello come descritto in hello [JSON Web Token RFC7519 specifica](https://tools.ietf.org/html/rfc7519)

### <a name="example-of-a-decoded-jwt-assertion"></a>Esempio di asserzione del token JWT decodificata
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

### <a name="example-of-an-encoded-jwt-assertion"></a>Esempio di asserzione del token JWT codificata
Hello stringa seguente è riportato un esempio di asserzione codificato. Se si osserva con attenzione, è possibile notare tre sezioni separate da punti (.).
prima sezione Hello codifica hello intestazione, hello secondo hello payload, e per ultimo è hello firma hello calcolata con certificati hello dal contenuto hello delle prime due sezioni di hello.
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a>Registrare il certificato con Azure AD
credenziali di certificato tooassociate hello con un'applicazione client hello in Azure AD, è necessario tooedit manifesto dell'applicazione di hello.
Con l'attesa di un certificato, è necessario toocompute:
- `$base64Thumbprint`, che è hello codifica base64 del certificato hello Hash
- `$base64Value`, che è hello codifica base64 di dati non elaborati certificato hello

è inoltre necessario disporre di una chiave di hello tooidentify GUID nel manifesto dell'applicazione hello tooprovide (`$keyId`)

Nella registrazione dell'app Azure per un'applicazione client hello hello, aprire il manifesto dell'applicazione hello e sostituire hello *keyCredentials* proprietà con le informazioni del nuovo certificato utilizzando hello seguente schema:
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

Salvare il manifesto di applicazione hello modifiche toohello e caricare tooAzure Active Directory. proprietà keyCredentials Hello è multivalore, pertanto è possibile caricare più certificati per la gestione delle chiavi più dettagliato.
