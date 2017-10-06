---
title: Accesso singolo sul protocollo SAML aaaAzure | Documenti Microsoft
description: Questo articolo descrive il protocollo di accesso singolo in SAML hello in Azure Active Directory
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: ad8437f5-b887-41ff-bd77-779ddafc33fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 435cfe0e7be3f2defd34e8b6f6b0f08596ee1f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Protocollo SAML per Single Sign-On
Questo articolo vengono illustrate le richieste di autenticazione SAML 2.0 hello e le risposte che supporta Azure Active Directory (Azure AD) per Single Sign-On.

diagramma di protocollo Hello riportato di seguito descrive una sequenza hello single sign-on. il servizio cloud (provider di servizi hello) Hello utilizza un toopass associazione reindirizzamento HTTP un `AuthnRequest` tooAzure elemento (richiesta di autenticazione) AD (provider di identità hello). Quindi AD Azure Usa un toopost di associazione HTTP post un `Response` servizio cloud toohello di elemento.

![Flusso di lavoro di Single Sign-On](media/active-directory-single-sign-on-protocol-reference/active-directory-saml-single-sign-on-workflow.png)

## AuthnRequest
servizi cloud di toorequest un'autenticazione utente, inviano un `AuthnRequest` tooAzure elemento Active Directory. Un esempio di SAML 2.0 `AuthnRequest` può essere simile al seguente:

```
<samlp:AuthnRequest
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="id6c1c178c166d486687be4aaf5e482730"
Version="2.0" IssueInstant="2013-03-18T03:28:54.1839884Z"
xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
</samlp:AuthnRequest>
```


| Parametro |  | Descrizione |
| --- | --- | --- |
| ID |Obbligatoria |Azure AD Usa questo hello toopopulate attributo `InResponseTo` attributo di hello ha restituito una risposta. ID non deve iniziare con un numero, in modo una strategia comune è tooprepend una stringa come "id" toohello di rappresentazione di stringa di un GUID. Ad esempio, `id6c1c178c166d486687be4aaf5e482730` è un ID valido. |
| Versione |Obbligatoria |Deve essere **2.0**. |
| IssueInstant |Obbligatoria |Stringa DateTime con un valore UTC e [formato round trip ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). Azure Active Directory prevede un valore DateTime di questo tipo, ma non valutare o utilizzare il valore di hello. |
| AssertionConsumerServiceUrl |Facoltativa |Se specificato, questo valore deve corrispondere hello `RedirectUri` del servizio cloud hello in Azure AD. |
| ForceAuthn |Facoltativa | Si tratta di un valore booleano. Se true, ciò significa che tale utente hello sarà forzato toore-autenticazione, anche se hanno una sessione valida con Azure AD. |
| IsPassive |Facoltativa |Si tratta di un valore booleano che specifica se Azure AD deve eseguire l'autenticazione utente hello in modalità invisibile, senza interazione dell'utente, utilizzando il cookie di sessione hello, se presente. In questo caso, Azure AD tenterà utente hello tooauthenticate l'utilizzo di cookie di sessione hello. |

Tutti gli altri attributi `AuthnRequest` , ad esempio Consent, Destination, AssertionConsumerServiceIndex, AttributeConsumerServiceIndex e ProviderName, vengono **ignorati**.

Azure Active Directory ignora inoltre hello `Conditions` elemento `AuthnRequest`.

### Issuer
Hello `Issuer` elemento in un `AuthnRequest` deve corrispondere esattamente a uno di hello **ServicePrincipalNames** nel servizio cloud hello in Azure AD. In genere, viene impostato toohello **URI ID App** specificato durante la registrazione dell'applicazione.

Un estratto di codice SAML di esempio contenente hello `Issuer` elemento è simile al seguente:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
```

### NameIDPolicy
Questo elemento richiede un formato ID nome specifico in risposta hello ed è facoltativo in `AuthnRequest` tooAzure elementi inviati AD.

Un elemento `NameIdPolicy` di esempio è simile al seguente:

```
<NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
```

Se viene specificato `NameIDPolicy` è possibile includere l'attributo facoltativo `Format`. Hello `Format` attributo può avere solo uno dei seguenti valori hello; qualsiasi altro valore comporta un errore.

* `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`: Azure Active Directory rilascia l'attestazione NameID hello come identificatore pairwise.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`: Azure Active Directory rilascia l'attestazione NameID hello in formato di indirizzo di posta elettronica.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`: Questo valore consente formato dell'attestazione tooselect hello Azure Active Directory. Azure Active Directory rilascia hello NameID come identificatore pairwise.
* `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`: Azure Active Directory rilascia l'attestazione NameID hello come un valore generato casualmente operazione SSO corrente toohello univoco. Ciò significa che il valore di hello è temporaneo e non può essere hello tooidentify utilizzata l'autenticazione utente.

Azure Active Directory ignora hello `AllowCreate` attributo.

### RequestAuthnContext
Hello `RequestedAuthnContext` elemento specifica i metodi di autenticazione hello desiderato. È facoltativo negli `AuthnRequest` tooAzure elementi inviati AD. Azure AD supporta un solo valore `AuthnContextClassRef`: `urn:oasis:names:tc:SAML:2.0:ac:classes:Password`.

### Scoping
Hello `Scoping` elemento, che include un elenco di provider di identità, è facoltativo in `AuthnRequest` tooAzure elementi inviati AD.

Se fornito, non includere hello `ProxyCount` attributo `IDPListOption` o `RequesterID` elemento, poiché non è supportati.

### Firma
Non includere un elemento `Signature` negli elementi `AuthnRequest` perché Azure AD non supporta le richieste di autenticazione firmate.

### Oggetto
Azure Active Directory ignora hello `Subject` elemento `AuthnRequest` elementi.

## Response
Quando un richiesto sign-on viene completato, Azure AD invia un servizio cloud toohello di risposta. Un esempio risposta tooa sign-on tentativo riuscito è simile al seguente:

```
<samlp:Response ID="_a4958bfd-e107-4e67-b06d-0d85ade2e76a" Version="2.0" IssueInstant="2013-03-18T07:38:15.144Z" Destination="https://contoso.com/identity/inboundsso.aspx" InResponseTo="id758d0ef385634593a77bdf7e632984b6" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
    ...
  </ds:Signature>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
  <Assertion ID="_bf9c623d-cc20-407a-9a59-c2d0aee84d12" IssueInstant="2013-03-18T07:38:15.144Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      ...
    </ds:Signature>
    <Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
  </Assertion>
</samlp:Response>
```

### Response
Hello `Response` elemento include il risultato di hello della richiesta di autorizzazione hello. Azure Active Directory imposta hello `ID`, `Version` e `IssueInstant` valori hello `Response` elemento. Imposta inoltre hello gli attributi seguenti:

* `Destination`: Quando l'accesso viene completato, viene impostato toohello `RedirectUri` hello provider di servizi (servizio cloud).
* `InResponseTo`: Questa proprietà è impostata toohello `ID` attributo di hello `AuthnRequest` elemento che ha avviato la risposta hello.

### Issuer
Azure Active Directory imposta hello `Issuer` elemento troppo`https://login.microsoftonline.com/<TenantIDGUID>/` dove <TenantIDGUID> è l'ID tenant hello del tenant hello Azure AD.

Una risposta di esempio con elemento Issuer può avere un aspetto simile al seguente:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

### Stato
Hello `Status` elemento fornisce hello esiti di sign-on. Include hello `StatusCode` elemento che contiene un codice o un set di codici annidati che rappresentano lo stato di hello della richiesta di hello. Include inoltre hello `StatusMessage` elemento che contiene messaggi di errore personalizzati generati durante il processo di accesso hello.

<!-- TODO: Add a authentication protocol error reference -->

di seguito Hello è un SAML risposta tooan tentativo non riuscito sign-on.

```
<samlp:Response ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Requester">
      <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:RequestUnsupported" />
    </samlp:StatusCode>
    <samlp:StatusMessage>AADSTS75006: An error occurred while processing a SAML2 Authentication request. AADSTS90011: hello SAML authentication request property 'NameIdentifierPolicy/SPNameQualifier' is not supported.
Trace ID: 66febed4-e737-49ff-ac23-464ba090d57c
Timestamp: 2013-03-18 08:49:24Z</samlp:StatusMessage>
  </samlp:Status>
```

### Assertion
In aggiunta toohello `ID`, `IssueInstant` e `Version`, Azure Active Directory imposta hello segue gli elementi in hello `Assertion` elemento della risposta hello.

#### Issuer
Questa proprietà è impostata troppo`https://sts.windows.net/<TenantIDGUID>/`dove <TenantIDGUID> è hello ID Tenant del tenant hello Azure AD.

```
<Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

#### Firma
Azure Active Directory firma l'asserzione hello in risposta tooa riuscita sign-on. Hello `Signature` elemento contiene una firma digitale usato servizio cloud hello tooauthenticate hello tooverify hello integrità per origine dell'asserzione hello.

la firma digitale, Azure AD Usa toogenerate hello chiave di firma in hello `IDPSSODescriptor` elemento del documento dei metadati.

```
<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      digital_signature_here
    </ds:Signature>
```

#### Oggetto
Specifica l'entità hello soggetto hello di istruzioni hello asserzione hello. Contiene un `NameID` elemento che rappresenta l'utente autenticato hello. Hello `NameID` valore è un identificatore di destinazione è diretto toohello solo i provider di servizi che è destinataria hello hello token. È persistente: può essere revocato, ma mai riassegnato. È anche opaco, in quanto non rivela alcun dettaglio relativo utente hello e non può essere utilizzata come identificatore per le query di attributi.

Hello `Method` attributo di hello `SubjectConfirmation` elemento è sempre impostato troppo`urn:oasis:names:tc:SAML:2.0:cm:bearer`.

```
<Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
</Subject>
```

#### Condizioni
Questo elemento specifica le condizioni che definiscono hello accettabile usare di asserzioni SAML.

```
<Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
</Conditions>
```

Hello `NotBefore` e `NotOnOrAfter` attributi specificano l'intervallo hello durante cui hello l'asserzione è valida.

* valore di hello Hello `NotBefore` attributo è uguale tooor leggermente (meno di un secondo) successiva al valore di hello di `IssueInstant` attributo di hello `Assertion` elemento. Azure AD non tiene conto dell'eventuale differenza di tempo tra l'elemento e hello (provider di servizi) di servizio cloud e non aggiunge alcun tempo di toothis buffer.
* valore di hello Hello `NotOnOrAfter` attributo è di 70 minuti successivi valore hello hello `NotBefore` attributo.

#### Audience
Contiene un URI che identifica un gruppo di destinatari. Azure Active Directory imposta il valore di hello di questo elemento toohello valore `Issuer` elemento di hello `AuthnRequest` che ha avviato hello sign-on. hello tooevaluate `Audience` valore, utilizzare il valore di hello di hello `App ID URI` che è stato specificato durante la registrazione dell'applicazione.

```
<AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
</AudienceRestriction>
```

Ad esempio hello `Issuer` valore hello `Audience` valore deve corrispondere esattamente a uno hello nomi dell'entità servizio che rappresenta il servizio di cloud hello in Azure AD. Tuttavia, se hello del valore di hello `Issuer` elemento non è un valore URI, hello `Audience` valore nella risposta hello è hello `Issuer` valore preceduto da `spn:`.

#### AttributeStatement
Contiene le attestazioni sull'oggetto hello o all'utente. Hello estratto di codice seguente è incluso un esempio `AttributeStatement` elemento. i puntini di sospensione Hello indica che tale elemento hello può includere più attributi e valori di attributo.

```
<AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
</AttributeStatement>
```        

* **Nome attestazione** : hello valore hello `Name` attributo (`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`) è hello UPN dell'utente autenticato hello, ad esempio `testuser@managedtenant.com`.
* **Attestazione ObjectIdentifier** : hello valore hello `ObjectIdentifier` attributo (`http://schemas.microsoft.com/identity/claims/objectidentifier`) è hello `ObjectId` dell'oggetto directory hello che rappresenta hello utente autenticato in Azure AD. `ObjectId`riutilizzo di identificatore sicuro di hello autenticato l'utente è non modificabile, univoco globale.

#### AuthnStatement
Questo elemento dichiara che tale oggetto asserzione hello è stato autenticato in un determinato modo a una determinata ora.

* Hello `AuthnInstant` attributo specifica il tempo di hello utente hello autenticato con Azure AD.
* Hello `AuthnContext` elemento specifica il contesto di autenticazione hello utilizzato tooauthenticate hello.

```
<AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
</AuthnStatement>
```