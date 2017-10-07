---
title: aaaAzure tooService servizio AD autenticazione tramite OAuth 2.0 | Documenti Microsoft
description: In questo articolo viene descritto come tooimplement messaggi toouse HTTP del servizio di autenticazione tooservice tramite flusso di concessione di credenziali client OAuth 2.0 hello.
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: a7f939d9-532d-4b6d-b6d3-95520207965d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f4bfd4ea8a7de1929c7dcf7ad65a156edff74f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Chiamate al servizio tooservice utilizzando le credenziali del client (segreto condiviso o certificato)
Flusso di OAuth 2.0 Client credenziali Grant Hello permette a un servizio web (*client riservato*) toouse le proprie credenziali invece di rappresentare un utente, tooauthenticate quando si chiama un altro servizio web. In questo scenario, hello client è in genere di un servizio web di livello intermedio, un servizio daemon o un sito web. Per un maggiore livello di garanzia, Azure AD consente inoltre la chiamata di un certificato (anziché un segreto condiviso) come credenziale del servizio toouse hello.

## Diagramma del flusso di concessione delle credenziali client
Hello diagramma seguente viene illustrato come le credenziali del client hello concedono il funzionamento del flusso di Azure Active Directory (Azure AD).

![Flusso di concessione delle credenziali client di OAuth 2.0](media/active-directory-protocols-oauth-service-to-service/active-directory-protocols-oauth-client-credentials-grant-flow.jpg)

1. un'applicazione client Hello autentica toohello endpoint di rilascio dei token di Azure AD e richiede un token di accesso.
2. problemi di endpoint di rilascio dei token Hello Azure AD hello token di accesso.
3. token di accesso Hello è toohello tooauthenticate utilizzate risorse protetta.
4. Applicazione web toohello vengono restituiti dati dalla risorsa protetta hello.

## Registrare i servizi di hello in Azure AD
Registrare hello la chiamata di servizio e hello servizio che riceve in Azure Active Directory (Azure AD). Per altre informazioni, vedere [Integrazione di applicazioni con Azure Active Directory](active-directory-integrating-applications.md).

## Richiedere un token di accesso
toorequest un token di accesso, utilizzare un endpoint specifico del tenant di Azure AD toohello HTTP POST.

```
https://login.microsoftonline.com/<tenant id>/oauth2/token
```

## Richiesta del token di accesso da servizio a servizio
Esistono due casi, a seconda se un'applicazione hello client sceglie toobe protetto da un segreto condiviso o un certificato.

### Primo caso: richiesta del token di accesso con un segreto condiviso
Quando si utilizza un segreto condiviso, una richiesta di token di accesso da servizio a servizio contiene hello seguenti parametri:

| . |  | Descrizione |
| --- | --- | --- |
| grant_type |Obbligatoria |Specifica hello richiesto tipo di concessione. In un flusso di concessione di credenziali Client, deve essere il valore di hello **client_credentials**. |
| client_id |Obbligatoria |Specifica l'id client di Azure AD hello di hello chiamata servizio web. hello toofind chiamata ID client dell'applicazione, in hello [portale di Azure](https://portal.azure.com), fare clic su **Active Directory**, cambiare la directory, fare clic su un'applicazione hello. Hello client_id è hello *ID applicazione* |
| client_secret |Obbligatoria |Immettere una chiave registrata per hello chiamata applicazione daemon o di servizio web, in Azure AD. Fare clic su una chiave, nel portale di Azure hello toocreate **Active Directory**, cambiare la directory, fare clic su un'applicazione hello, fare clic su **impostazioni**, fare clic su **chiavi**, e aggiungere una chiave.|
| resource |Obbligatoria |Immettere l'URI ID App del servizio web che riceve hello hello. Fare clic su toofind hello URI ID App nel portale di Azure hello **Active Directory**, cambiare directory, fare clic su un'applicazione hello servizio e quindi fare clic su **impostazioni** e **proprietà** |

#### Esempio
Hello POST HTTP seguente richiede un token di accesso per il servizio web https://service.contoso.com/ di hello. Hello `client_id` individua hello del servizio web che richiede un token di accesso hello.

```
POST /contoso.com/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=625bc9f6-3bf6-4b6d-94ba-e97cf07a22de&client_secret=qkDwDJlDfig2IpeuUZYKH1Wb8q1V0ju6sILxQQqhJ+s=&resource=https%3A%2F%2Fservice.contoso.com%2F
```

### Secondo caso: richiesta del token di accesso con un certificato
Una richiesta di token di accesso da servizio a servizio con un certificato contiene hello seguenti parametri:

| . |  | Descrizione |
| --- | --- | --- |
| grant_type |Obbligatoria |Specifica hello richiesto il tipo di risposta. In un flusso di concessione di credenziali Client, deve essere il valore di hello **client_credentials**. |
| client_id |Obbligatoria |Specifica l'id client di Azure AD hello di hello chiamata servizio web. hello toofind chiamata ID client dell'applicazione, in hello [portale di Azure](https://portal.azure.com), fare clic su **Active Directory**, cambiare la directory, fare clic su un'applicazione hello. Hello client_id è hello *ID applicazione* |
| client_assertion_type |Obbligatoria |il valore di Hello deve essere`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |Obbligatoria | Un'asserzione (JSON Web Token) che è necessario toocreate e certificato di firma con hello è registrato come credenziali per l'applicazione. Conoscenza [credenziali del certificato](active-directory-certificate-credentials.md) toolearn come tooregister il formato di certificato e hello di asserzione hello.|
| resource | Obbligatoria |Immettere l'URI ID App del servizio web che riceve hello hello. Fare clic su toofind hello URI ID App nel portale di Azure hello **Active Directory**, fare clic su directory hello, fare clic su un'applicazione hello e quindi fare clic su **configura**. |

Si noti che i parametri di hello sono quasi uguale a quello nel caso di hello della richiesta di hello hello dal segreto condiviso a ad eccezione del fatto che il parametro client_secret hello viene sostituito da due parametri: un client_assertion_type e client_assertion.

#### Esempio
Hello POST HTTP seguente richiede un token di accesso per il servizio web https://service.contoso.com/ di hello con un certificato. Hello `client_id` individua hello del servizio web che richiede un token di accesso hello.

```
POST /<tenant_id>/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

resource=https%3A%2F%contoso.onmicrosoft.com%2Ffc7664b4-cdd6-43e1-9365-c2e1c4e1b3bf&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

### Risposta del token di accesso da servizio a servizio

Una risposta con esito positivo contiene una risposta JSON OAuth 2.0 con hello seguenti parametri:

| . | Descrizione |
| --- | --- |
| access_token |token di accesso richiesto Hello. Hello chiamata servizio web è possibile utilizzare questo toohello tooauthenticate token servizio web che riceve. |
| token_type |Indica il valore di tipo di token hello. Hello solo tipo di Azure AD supporta **connessione**. Per ulteriori informazioni sui token di connessione, vedere hello [Framework di autorizzazione OAuth 2.0: utilizzo dei Token di connessione (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| expires_in |Quanto tempo il token di accesso di hello è valido (in secondi). |
| expires_on |ora di Hello scadenza token di accesso hello. Data di Hello è rappresentata dal numero di hello di secondi da 1970-01-01T0:0:0Z UTC fino a ora di scadenza hello. Questo valore è durata hello toodetermine utilizzati del token memorizzati nella cache. |
| not_before |ora di Hello dalla quale hello token di accesso diventa utilizzabile. Data di Hello è rappresentata dal numero di hello di secondi da 1970-01-01T0:0:0Z UTC fino al tempo di validità per il token di hello.|
| resource |URI ID App del servizio web che riceve hello Hello. |

#### Esempio di risposta
Hello esempio seguente mostra una richiesta di tooa risposta di esito positivo per un servizio web tooa token di accesso.

```
{
"access_token":"eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0ODI2NywibmJmIjoxMzg4NDQ4MjY3LCJleHAiOjEzODg0NTIxNjcsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsInN1YiI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZS8iLCJhcHBpZCI6ImQxN2QxNWJjLWM1NzYtNDFlNS05MjdmLWRiNWYzMGRkNThmMSIsImFwcGlkYWNyIjoiMSJ9.aqtfJ7G37CpKV901Vm9sGiQhde0WMg6luYJR4wuNR2ffaQsVPPpKirM5rbc6o5CmW1OtmaAIdwDcL6i9ZT9ooIIicSRrjCYMYWHX08ip-tj-uWUihGztI02xKdWiycItpWiHxapQm0a8Ti1CWRjJghORC1B1-fah_yWx6Cjuf4QE8xJcu-ZHX0pVZNPX22PHYV5Km-vPTq2HtIqdboKyZy3Y4y3geOrRIFElZYoqjqSv5q9Jgtj5ERsNQIjefpyxW3EwPtFqMcDm4ebiAEpoEWRN4QYOMxnC9OUBeG9oLA0lTfmhgHLAtvJogJcYFzwngTsVo6HznsvPWy7UP3MINA",
"token_type":"Bearer",
"expires_in":"3599",
"expires_on":"1388452167",
"resource":"https://service.contoso.com/"
}
```

## Vedere anche
* [OAuth 2.0 in Azure AD](active-directory-protocols-oauth-code.md)
* [Esempio in c# di hello servizio tooservice chiamata con un segreto condiviso](https://github.com/Azure-Samples/active-directory-dotnet-daemon) e [esempio in c# di hello servizio tooservice chiamata con un certificato](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential)
