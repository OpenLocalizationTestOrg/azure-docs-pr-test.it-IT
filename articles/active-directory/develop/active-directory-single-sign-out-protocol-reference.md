---
title: Single Sign Out SAML protocollo aaaAzure | Documenti Microsoft
description: Questo articolo descrive hello protocollo di SAML Single Sign-Out in Azure Active Directory
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 0e4aa75d-d1ad-4bde-a94c-d8a41fb0abe6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 889c9b3397a601c16ba6971d2b15bfee305576de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Protocollo SAML per Single Sign-Out
Hello di supporta Active Directory (Azure AD) Azure SAML 2.0 single Sign-Out profilo del web browser. Per singolo toowork disconnessione correttamente, hello **LogoutURL** per un'applicazione hello deve essere registrata con Azure AD durante la registrazione dell'applicazione in modo esplicito. Azure AD Usa gli utenti di hello LogoutURL tooredirect dopo che si sono disconnessi.

Questo diagramma mostra flusso di lavoro di hello del processo di disconnessione singola di hello Azure AD.

![Flusso di lavoro di Single Sign-Out](media/active-directory-single-sign-out-protocol-reference/active-directory-saml-single-sign-out-workflow.png)

## LogoutRequest
Hello servizio cloud invia un `LogoutRequest` tooindicate tooAzure AD messaggio che è stata terminata una sessione. Hello estratto di codice seguente viene illustrato un esempio `LogoutRequest` elemento.

```
<samlp:LogoutRequest xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="idaa6ebe6839094fe4abc4ebd5281ec780" Version="2.0" IssueInstant="2013-03-28T07:10:49.6004822Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.workaad.com</Issuer>
  <NameID xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
</samlp:LogoutRequest>
```

### LogoutRequest
Hello `LogoutRequest` tooAzure elemento inviati AD richiede hello gli attributi seguenti:

* `ID`: Identifica richiesta di disconnessione hello. valore di Hello `ID` non deve iniziare con un numero. Hello tipico consiste tooappend **id** toohello rappresentazione di stringa di un GUID.
* `Version`: Impostare il valore di hello di questo elemento troppo**2.0**. Questo valore è obbligatorio.
* `IssueInstant` : è una stringa `DateTime` con un valore di UTC (Coordinate Universal Time) e il [formato round trip ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). Azure AD prevede un valore di questo tipo, ma non lo impone.

### Issuer
Hello `Issuer` elemento in un `LogoutRequest` deve corrispondere esattamente a uno di hello **ServicePrincipalNames** nel servizio cloud hello in Azure AD. In genere, viene impostato toohello **URI ID App** specificato durante la registrazione dell'applicazione.

### NameID
valore di hello Hello `NameID` elemento deve corrispondere esattamente hello `NameID` dell'utente hello che viene disconnesso.

## LogoutResponse
Azure AD invia una `LogoutResponse` nella risposta tooa `LogoutRequest` elemento. Hello estratto di codice seguente viene illustrato un esempio `LogoutResponse`.

```
<samlp:LogoutResponse ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
</samlp:LogoutResponse>
```

### LogoutResponse
Azure Active Directory imposta hello `ID`, `Version` e `IssueInstant` valori hello `LogoutResponse` elemento. Imposta inoltre hello `InResponseTo` toohello elemento valore hello `ID` attributo di hello `LogoutRequest` che ha provocato la risposta hello.

### Issuer
Azure AD questo valore viene impostato troppo`https://login.microsoftonline.com/<TenantIdGUID>/` dove <TenantIdGUID> è l'ID tenant hello del tenant hello Azure AD.

valore di hello tooevaluate di hello `Issuer` elemento, Usa il valore di hello hello **URI ID App** fornito durante la registrazione dell'applicazione.

### Stato
Azure AD Usa hello `StatusCode` elemento hello `Status` elemento tooindicate hello esiti di disconnessione. Quando hello disconnessione tentativo non riesce, hello `StatusCode` elemento può anche contenere messaggi di errore personalizzati.
