---
title: "Azure AD Connect: Usare un provider di identità SAML 2.0 per l'accesso Single Sign On | Microsoft Docs"
description: Questo argomento descrive l'uso di un IdP conforme a SAML 2.0 per l'accesso Single Sign-On.
services: active-directory
author: billmath
manager: femila
ms.custom: it-pro
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f9653dc44fb284a9b3c1988f623c33f27ae148cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#  <a name="use-a-saml-20-identity-provider-idp-for-single-sign-on"></a>Usare un provider di identità (IdP) SAML 2.0 per l'accesso Single Sign-On

Questo argomento contiene informazioni sull'utilizzo di un SAML 2.0 profilo SP-Lite basato su Provider di identità come hello preferito la servizio Token di sicurezza (STS) / provider di identità. Si tratta di un'opzione utile quando si hanno già una directory di utenti e un archivio di password locali a cui è possibile accedere con SAML 2.0. La directory utenti esistente è utilizzabile per sign-on tooOffice 365 e altre risorse protette AD Azure. Hello SP-Lite di SAML 2.0 profilo si basa sull'hello ampiamente utilizzato tooprovide standard di identità federato Security asserzione Markup Language (SAML) sign-on e il framework di scambio degli attributi.

>[!NOTE]
>Per un elenco di parti 3rd Idps che sono stati testati per l'utilizzo con Azure AD vedere hello [elenco di compatibilità di federazione di Azure AD](active-directory-aadconnect-federation-compatibility.md)

Microsoft supporta questa esperienza sign-on come integrazione hello di un servizio cloud Microsoft, ad esempio Office 365, con la correttamente configurato di SAML 2.0 profilo basato su provider di identità. Provider di identità SAML 2.0 sono prodotti di terze parti e pertanto Microsoft non fornisce alcun supporto per la distribuzione di hello, configurazione, essi relative procedure consigliate di risoluzione dei problemi. Una volta configurato correttamente, integrazione hello con hello SAML 2.0 i provider di identità è possibile verificare la corretta configurazione utilizzando hello strumento Analizzatore di connettività Microsoft descritto in dettaglio più avanti. Per ulteriori informazioni sui provider di identità basato sul profilo SP-Lite di SAML 2.0, rivolgersi organizzazione hello cui è stato fornito.

>[!IMPORTANT]
>In questo scenario di accesso con i provider di identità SAML 2.0 è disponibile solo un set limitato di client, tra cui:

>- Client basati sul Web, ad esempio Outlook Web Access e SharePoint Online
- Client di posta elettronica che utilizzano l'autenticazione di base e un metodo di accesso Exchange supportato come IMAP, POP, Active Sync, MAPI, e così via (Buongiorno protocollo Client avanzato punto finale è obbligatorio toobe distribuito), tra cui:
    - Microsoft Outlook 2010/Outlook 2013/Outlook 2016, Apple iPhone (diverse versioni di iOS)
    - Diversi dispositivi Google Android
    - Windows Phone 7, Windows Phone 7.8 e Windows Phone 8.0
    - Client di posta elettronica di Windows 8 e Windows 8.1
    - Client di posta elettronica di Windows 10

Tutti gli altri client non sono disponibili in questo scenario di accesso con il provider di identità SAML 2.0. Ad esempio, il client desktop Lync 2010 hello non è in grado di toologin in servizio hello con il Provider di identità SAML 2.0 configurato per single sign-on.

## <a name="azure-ad-saml-20-protocol-requirements"></a>Requisiti del protocollo SAML 2.0 in Azure AD
In questo argomento contiene informazioni dettagliate sui requisiti di protocollo hello e alla formattazione dei messaggi che il provider di identità SAML 2.0 deve implementare toofederate con Azure AD tooenable sign-on tooone o altri servizi cloud Microsoft (ad esempio Office 365). Hello SAML 2.0 relying party (SP-STS) per un servizio cloud Microsoft in questo scenario è Azure AD.

È consigliabile verificare i messaggi di output del provider di identità essere simile toohello fornito tracce di esempio come possibili di SAML 2.0. Dove possibile, inoltre, utilizzare i valori di attributo specifici dai metadati di Azure AD hello fornito. Quando si è soddisfatti dei messaggi di output, è possibile testare hello analizzatore connettività Microsoft come descritto di seguito.

metadati Hello Azure AD possono essere scaricati dal seguente URL: [https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml](http://https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml).
Per i clienti in Cina utilizzando hello istanza Cina specifici di Office 365, hello seguenti endpoint di federazione deve essere utilizzato: [https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml](https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml).

## <a name="saml-protocol-requirements"></a>Requisiti del protocollo SAML
Dettagli questa sezione come coppie di messaggi di richiesta e risposta hello vengono raggruppati nel toohelp ordine si tooformat i messaggi correttamente.

Azure AD può essere configurato toowork con provider di identità che utilizzano il profilo SP-Lite di SAML 2.0 di hello con alcuni requisiti specifici, come indicato di seguito. Utilizza hello messaggi SAML di esempio di richiesta e risposta con test automatizzati e manuali, è possibile utilizzare tooachieve interoperabilità con Azure AD.

## <a name="signature-block-requirements"></a>Requisiti del blocco di firma
All'interno di hello risposta SAML nodo di messaggio hello firma contiene informazioni sulla firma digitale di hello per il messaggio hello stesso. blocco della firma Hello sono hello seguenti requisiti:

1. Hello nodo di asserzione deve essere firmato.
2.  algoritmo Hello RSA-sha1 deve essere utilizzato come DigestMethod hello. Altri algoritmi di firma digitale non sono accettati.
   `<ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>`
3.  È anche possibile firmare il documento XML hello. 
4.  Algoritmo di trasformazione Hello deve corrispondere ai valori hello nel seguente esempio hello:`<ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
       <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>`
9.  Algoritmo SignatureMethod Hello deve corrispondere hello seguente esempio:`<ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>`

## <a name="supported-bindings"></a>Binding supportati
Le associazioni sono trasporto hello correlati che sono necessari i parametri di comunicazione. Hello seguenti requisiti si applica le associazioni toohello

1. HTTPS è richiesto hello trasporto.
2.  Azure AD richiede HTTP POST per l'invio dei token durante l'accesso
3.  Azure AD userà HTTP POST per hello autenticazione richiesta toohello provider identità e REDIRECT per provider di identità toohello messaggio hello disconnessione.

## <a name="required-attributes"></a>Attributi richiesti
Questa tabella sono riportati i requisiti per gli attributi specifici nel messaggio hello SAML 2.0.
 
|Attributo|Descrizione|
| ----- | ----- |
|NameID|il valore di Hello di questa asserzione deve essere hello stesso immutableid hello Azure AD dell'utente. Può trattarsi di too64 caratteri alfanumerici. Qualsiasi carattere non compatibile con HTML deve essere codificato. Ad esempio, il carattere "+" viene visualizzato come ".2B".|
|IDPEmail|Hello del nome dell'entità utente (UPN) è elencato in hello SAML risposta come un elemento con hello Nome IDPEmail questo è hello UserPrincipalName (UPN) dell'utente in Azure AD/Office 365. Hello UPN è nel formato di indirizzo di posta elettronica. Valore UPN in Office 365 (Azure Active Directory).|
|Issuer|Questo è necessario toobe un URI del provider di identità hello. Non è consigliabile riusare hello dell'autorità di certificazione da messaggi di esempio hello. Se si hanno più domini di primo livello nel hello tenant di Azure AD che dell'autorità di certificazione deve corrispondere hello specificato impostazione URI configurata per ogni dominio.|

>[!IMPORTANT]
>Azure AD attualmente supporta hello seguente URI NameID-Format per SAML 2.0:urn:oasis:names:tc:SAML:2.0:nameid-formato: persistente.

## <a name="sample-saml-request-and-response-messages"></a>Messaggi di richiesta e di risposta SAML di esempio
Una coppia di messaggi di richiesta e risposta viene visualizzata per lo scambio di messaggi di accesso hello.
Si tratta di un messaggio di richiesta di esempio che viene inviato dal provider di identità SAML 2.0 di Azure AD tooa esempio. provider di identità SAML 2.0 di esempio Hello è che Active Directory Federation Services (ADFS) configurato protocollo SAML-P toouse. È stato anche completato un test di interoperabilità con altri provider di identità SAML 2.0.

    `<samlp:AuthnRequest xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="_7171b0b2-19f2-4ba2-8f94-24b5e56b7f1e" IssueInstant="2014-01-30T16:18:35Z" Version="2.0" AssertionConsumerServiceIndex="0" >
    <saml:Issuer>urn:federation:MicrosoftOnline</saml:Issuer>
    <samlp:NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
    </samlp:AuthnRequest>`

Si tratta di un messaggio di risposta di esempio che viene inviato da hello esempio SAML 2.0 identità provider tooAzure AD / Office 365.

    `<samlp:Response ID="_592c022f-e85e-4d23-b55b-9141c95cd2a5" Version="2.0" IssueInstant="2014-01-31T15:36:31.357Z" Destination="https://login.microsoftonline.com/login.srf" Consent="urn:oasis:names:tc:SAML:2.0:consent:unspecified" InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
    </samlp:Status>
    <Assertion ID="_7e3c1bcd-f180-4f78-83e1-7680920793aa" IssueInstant="2014-01-31T15:36:31.279Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
        <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
        <ds:Reference URI="#_7e3c1bcd-f180-4f78-83e1-7680920793aa">
          <ds:Transforms>
            <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
            <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
          </ds:Transforms>
          <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
          <ds:DigestValue>CBn/5YqbheaJP425c0pHva9PhNY=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
      <ds:SignatureValue>TciWMyHW2ZODrh/2xrvp5ggmcHBFEd9vrp6DYXp+hZWJzmXMmzwmwS8KNRJKy8H7XqBsdELA1Msqi8I3TmWdnoIRfM/ZAyUppo8suMu6Zw+boE32hoQRnX9EWN/f0vH6zA/YKTzrjca6JQ8gAV1ErwvRWDpyMcwdYCiWALv9ScbkAcebOE1s1JctZ5RBXggdZWrYi72X+I4i6WgyZcIGai/rZ4v2otoWAEHS0y1yh1qT7NDPpl/McDaTGkNU6C+8VfjD78DrUXEcAfKvPgKlKrOMZnD1lCGsViimGY+LSuIdY45MLmyaa5UT4KWph6dA==</ds:SignatureValue>
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
        <ds:X509Data>
          <ds:X509Certificate>MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyhBREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDTE1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9ybWVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/+3ZWxd9T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEMb2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcCAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvyJOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBySx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==</ds:X509Certificate>
        </ds:X509Data>
      </KeyInfo>
    </ds:Signature>
    <Subject>
      <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">ABCDEG1234567890</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" NotOnOrAfter="2014-01-31T15:41:31.357Z" Recipient="https://login.microsoftonline.com/login.srf" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2014-01-31T15:36:31.263Z" NotOnOrAfter="2014-01-31T16:36:31.263Z">
      <AudienceRestriction>
        <Audience>urn:federation:MicrosoftOnline</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="IDPEmail">
        <AttributeValue>administrator@contoso.com</AttributeValue>
      </Attribute>
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2014-01-31T15:36:30.200Z" SessionIndex="_7e3c1bcd-f180-4f78-83e1-7680920793aa">
      <AuthnContext>
        <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
    </Assertion>
    </samlp:Response>`

## <a name="configure-your-saml-20-compliant-identity-provider"></a>Configurare il provider di identità conforme a SAML 2.0
In questo argomento fornisce linee guida su come tooconfigure il toofederate di provider di identità SAML 2.0 con Azure AD tooenable accesso single sign-on tooone o più cloud di Microsoft services (ad esempio Office 365) mediante il protocollo hello SAML 2.0. Hello SAML 2.0 relying party per un servizio cloud Microsoft in questo scenario è Azure AD.

## <a name="add-azure-ad-metadata"></a>Aggiungere i metadati di Azure AD
Il provider di identità SAML 2.0 deve tooinformation tooadhere sulla relying party di hello Azure AD. Azure AD pubblica i metadati in https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml.

È consigliabile importare sempre i metadati di hello Azure AD più recenti quando si configura il provider di identità SAML 2.0. Si noti che Azure AD non legge i metadati dal provider di identità hello.

## <a name="add-azure-ad-as-a-relying-party"></a>Aggiungere Azure AD come relying party
È necessario tooenable comunicazione tra il provider di identità SAML 2.0 e Azure AD. Questa configurazione sono dipende dal provider di identità specifico, è consigliabile consultare toodocumentation per tale. In genere è necessario impostare hello relying party ID toohello uguale al valore entityID hello dai metadati hello Azure AD.

>[!NOTE]
>Verificare che hello orologio del server di provider di identità SAML 2.0 origine ora precisa tooan sincronizzato. Ora non è corretta può causare toofail gli accessi federati.

## <a name="install-windows-powershell-for-sign-on-with-saml-20-identity-provider"></a>Installare Windows PowerShell per l'accesso con il provider di identità SAML 2.0
Dopo aver configurato il provider di identità SAML 2.0 per l'utilizzo con sign-on AD Azure, passaggio successivo hello è toodownload e hello Installa modulo di Azure Active Directory per Windows PowerShell. Una volta installato, si utilizzerà tooconfigure questi cmdlet i domini di Azure AD come domini federati.

Hello modulo di Azure Active Directory per Windows PowerShell è un download per la gestione dei dati dell'organizzazione in Azure AD. Questo modulo installa un set di cmdlet tooWindows PowerShell; si esegue tali tooset i cmdlet di accesso single sign-on tooAzure Active Directory e a sua volta i servizi sottoscritti cloud tooall di hello. Per istruzioni su come toodownload e installare hello cmdlet, vedere [http://technet.microsoft.com/library/jj151815.aspx](http://technet.microsoft.com/library/jj151815.aspx)

## <a name="set-up-a-trust-between-your-saml-identity-provider-and-azure-ad"></a>Impostare una relazione di trust tra il provider di identità SAML e Azure AD
Prima di configurare la federazione in un dominio di Azure AD, è necessario che sia configurato un dominio personalizzato. È possibile attuare la federazione dominio predefinito hello fornito da Microsoft. dominio predefinito Hello Microsoft termina con "onmicrosoft.com".
È eseguire una serie di cmdlet in tooadd interfaccia della riga di comando di PowerShell di Windows hello o convertire domini per single sign-on.

Ogni dominio di Azure Active Directory che si desidera toofederate utilizzando il provider di identità SAML 2.0 deve essere aggiunto come dominio single sign-on o convertito toobe un dominio single sign-on da dominio standard. Aggiungendo o convertendo un dominio si imposta una relazione di trust tra il provider di identità SAML 2.0 e Azure AD.

Hello procedura riportata di seguito viene illustrata la conversione di un dominio standard tooa dominio federato esistente utilizzando SP-Lite di SAML 2.0. Si noti che il dominio può verificarsi un'interruzione che influisce sugli utenti too2 ore dopo l'esecuzione di questo passaggio.

## <a name="configuring-a-domain-in-your-azure-ad-directory-for-federation"></a>Configurazione di un dominio nella directory di Azure AD per la federazione


1. La connessione di Azure Active Directory come amministratore tenant tooyour: Connect-MsolService.
2.  Configurare la federazione toouse desiderata del dominio Office 365 con SAML 2.0:`$dom = "contoso.com" $BrandName - "Sample SAML 2.0 IDP" $LogOnUrl = "https://WS2012R2-0.contoso.com/passiveLogon" $LogOffUrl = "https://WS2012R2-0.contoso.com/passiveLogOff" $ecpUrl = "https://WS2012R2-0.contoso.com/PAOS" $MyURI = "urn:uri:MySamlp2IDP" $MySigningCert = @" MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyh BREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDT E1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9yb WVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/kupQ VcjKuKLitVDbssFyqbDTjP7WRjlVMWAHBI3kgNT7oE362Gf2WMJFf1b0HcrsgLin7daRXpq4Qi6OA57 sW1YFMj3sqyuTP0eZV3S4+ZbDVob6amsZIdIwxaLP9Zfywg2bLsGnVldB0+XKedZwDbCLCVg+3ZWxd9 T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEM b2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcC AwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9 eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+ CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvy JOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBy Sx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==" "@ $uri = "http://WS2012R2-0.contoso.com/adfs/services/trust" $Protocol = "SAMLP" Set-MsolDomainAuthentication -DomainName $dom -FederationBrandName $dom -Authentication Federated -PassiveLogOnUri $MyURI -ActiveLogOnUri $ecpUrl -SigningCertificate $MySigningCert -IssuerUri $uri -LogOffUri $url -PreferredAuthenticationProtocol $Protocol` 

3.  È possibile ottenere hello stringa con codificata base64 del certificato dal file di metadati di provider di identità di firma. Di seguito è illustrato un esempio di questo percorso, che tuttavia potrebbe essere leggermente diverso, in base all'implementazione.

    `<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol"> <KeyDescriptor use="signing"> <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#"> <X509Data> <X509Certificate>MIIC5jCCAc6gAwIBAgIQLnaxUPzay6ZJsC8HVv/QfTANBgkqhkiG9w0BAQsFADAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwHhcNMTMxMTA0MTgxMzMyWhcNMTQxMTA0MTgxMzMyWjAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCwMdVLTr5YTSRp+ccbSpuuFeXMfABD9mVCi2wtkRwC30TIyPdORz642MkurdxdPCWjwgJ0HW6TvXwcO9afH3OC5V//wEGDoNcI8PV4enCzTYFe/h//w51uqyv48Fbb3lEXs+aVl8155OAj2sO9IX64OJWKey82GQWK3g7LfhWWpp17j5bKpSd9DBH5pvrV+Q1ESU3mx71TEOvikHGCZYitEPywNeVMLRKrevdWI3FAhFjcCSO6nWDiMqCqiTDYOURXIcHVYTSof1YotkJ4tG6mP5Kpjzd4VQvnR7Pjb47nhIYG6iZ3mR1F85Ns9+hBWukQWNN2hcD/uGdPXhpdMVpBAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAK7h7jF7wPzhZ1dPl4e+XMAr8I7TNbhgEU3+oxKyW/IioQbvZVw1mYVCbGq9Rsw4KE06eSMybqHln3w5EeBbLS0MEkApqHY+p68iRpguqa+W7UHKXXQVgPMCpqxMFKonX6VlSQOR64FgpBme2uG+LJ8reTgypEKspQIN0WvtPWmiq4zAwBp08hAacgv868c0MM4WbOYU0rzMIR6Q+ceGVRImlCwZ5b7XKp4mJZ9hlaRjeuyVrDuzBkzROSurX1OXoci08yJvhbtiBJLf3uPOJHrhjKRwIt2TnzS9ElgFZlJiDIA26Athe73n43CT0af2IG6yC7e6sK4L3NEXJrwwUZk=</X509Certificate> </X509Data> </KeyInfo> </KeyDescriptor>` 

Per altre informazioni su "Set-MsolDomainAuthentication", vedere: [http://technet.microsoft.com/library/dn194112.aspx](http://technet.microsoft.com/library/dn194112.aspx).

>[!NOTE]
>È necessario eseguire "$ecpUrl = “https://WS2012R2-0.contoso.com/PAOS" solo se si configura un'estensione ECP per il provider di identità. I client di Exchange Online, ad eccezione di Outlook Web Application (OWA), usano un endpoint attivo basato su POST. Se il servizio token di sicurezza di SAML 2.0 implementa corrispondente implementazione ECP di tooShibboleth simile un punto finale attivo un punto finale attivo è possibile per questi toointeract rich client con hello servizio Exchange Online.

Dopo aver configurato la federazione è possibile passare indietro troppo "non federata" o "gestito", tuttavia questa modifica richiede tootwo ore toocomplete e richiede l'assegnazione di nuove password casuali per cloud basato su utente tooeach Accedi. Passare troppo "gestito" potrebbe essere necessaria in alcuni scenari tooreset un errore nelle impostazioni. Per altre informazioni sulla conversione del dominio, vedere: [http://msdn.microsoft.com/library/windowsazure/dn194122.aspx](http://msdn.microsoft.com/library/windowsazure/dn194122.aspx).

## <a name="provision-user-principals-tooazure-ad--office-365"></a>Eseguire il provisioning utente entità tooAzure AD / Office 365
Prima di poter autenticare il tooOffice utenti 365 è necessario eseguire il provisioning di Azure AD con entità corrispondenti asserzione toohello in hello SAML 2.0 attestazione utente. Se queste entità utente non sono note in anticipo tooAzure AD quindi non possono essere utilizzati per l'accesso federato. Azure AD Connect o Windows PowerShell può essere utilizzato tooprovision utente entità.

Azure AD Connect può essere utilizzato tooprovision entità tooyour domini in Azure Active Directory da hello Active Directory locale. Per informazioni più dettagliate, vedere [Integrare le directory locali con Azure Active Directory](active-directory-aadconnect.md).

Windows PowerShell può essere anche usato tooautomate aggiunta di nuovi utenti tooAzure AD e toosynchronize le modifiche dalla directory locale hello. hello toouse cmdlet di Windows PowerShell, è necessario scaricare hello [moduli di Azure Active Directory](https://docs.microsoft.com/powershell/azure/install-adv2?view=azureadps-2.0).

Questa procedura viene illustrato come tooadd tooAzure un singolo utente AD.


1. La connessione di Azure Active Directory come amministratore tenant tooyour: Connect-MsolService.
2.  Creare una nuova entità utente: ` New-MsolUser
        -UserPrincipalName elwoodf1@contoso.com
        -ImmutableId ABCDEFG1234567890
        -DisplayName "Elwood Folk"
        -FirstName Elwood 
        -LastName Folk 
        -AlternateEmailAddresses "Elwood.Folk@contoso.com" 
        -LicenseAssignment "samlp2test:ENTERPRISEPACK" 
        -UsageLocation "US" ` 

Per altre informazioni su "New-MsolUser", vedere [http://technet.microsoft.com/library/dn194096.aspx](http://technet.microsoft.com/library/dn194096.aspx)

>[!NOTE]
>Hello "UserPrinciplName" valore deve corrispondere il valore hello che verrà inviato per "IDPEmail" nell'attestazione SAML 2.0 e hello "ImmutableID" valore deve corrispondere il valore di hello inviato l'asserzione "NameID".

## <a name="verify-single-sign-on-with-your-saml-20-idp"></a>Verificare l'accesso Single Sign-On con l'IdP SAML 2.0
Come amministratore di hello, prima di verificare e gestire single sign-on (anche noto federazione delle identità), esaminare le informazioni di hello ed eseguire i passaggi di hello in hello tooset gli articoli di single sign-on con il provider di identità basato sul SP-Lite di SAML 2.0 seguenti:


1.  Si è rivisti hello requisiti del protocollo SAML 2.0 per Azure AD
2.  Il provider di identità SAML 2.0 è stato configurato
3.  Installare Windows PowerShell per l'accesso Single Sign-On con il provider di identità SAML 2.0
4.  Impostare una relazione di trust tra il provider di identità SAML 2.0 e Azure AD
5.  Effettuare il provisioning di un test nota utente principale tooAzure Active Directory (Office 365) mediante Windows PowerShell o Azure AD Connect.
6.  Configurare la sincronizzazione della directory usando [Azure AD Connect](active-directory-aadconnect.md).

Dopo avere configurato l'accesso Single Sign-On con il provider di identità basato su SP-Lite SAML 2.0, è necessario verificare che funzioni correttamente.

>[!NOTE]
>Se la conversione di un dominio, invece di aggiunta di uno, potrebbe richiedere fino a too24 ore tooset di single sign-on.
Prima di verificare l'accesso Single Sign-On, completare la configurazione della sincronizzazione di Active Directory, sincronizzare le directory e attivare gli utenti sincronizzati.

### <a name="use-hello-tool-tooverify-that-single-sign-on-has-been-set-up-correctly"></a>Utilizzare hello strumento tooverify che l'accesso single sign-on è stato configurato correttamente
tooverify che single sign-on sia stato configurato correttamente, è possibile eseguire hello seguendo procedure tooconfirm che si è in grado di toosign nel servizio cloud toohello con le credenziali aziendali.

Microsoft ha fornito uno strumento che è possibile utilizzare tootest il SAML 2.0 basato su provider di identità. Prima di eseguire hello testare lo strumento è necessario aver configurato un toofederate tenant di Azure AD con il provider di identità.

>[!NOTE]
>Hello analizzatore connettività richiede Internet Explorer 10 o versioni successive.



1. Download hello analizzatore di connettività, [https://testconnectivity.microsoft.com/?tabid=Client](https://testconnectivity.microsoft.com/?tabid=Client).
2.  Fare clic su Installa toobegin download e installazione dello strumento hello.
3.  Selezionare "I can't set up federation with Office 365, Azure, or other services that use Azure Active Directory" (Impossibile configurare la federazione con Office 365, Azure o altri servizi che usano Azure Active Directory).
4.  Una volta hello strumento viene scaricato e in esecuzione, si noterà finestra diagnostica della connettività hello. strumento Hello passerà attraverso la connessione della federazione di test.
5.  Hello analizzatore connettività verrà aperto il provider di identità SAML 2.0 per è toologon, immettere le credenziali di hello per testare dell'entità utente di hello: ![SAML](media/active-directory-aadconnect-federation-saml-idp/saml1.png)
6.  Hello federazione prova nella finestra di accesso che è necessario immettere un nome account e password per tenant di Azure AD hello toobe configurato federata con il provider di identità SAML 2.0. strumento Hello tenterà toosign aggiuntivo utilizzando queste credenziali e i risultati dettagliati dei test eseguiti durante il tentativo di accesso hello verranno forniti come output.
![SAML](media/active-directory-aadconnect-federation-saml-idp/saml2.png)
7. Questa finestra mostra il risultato di un test non riuscito. Facendo clic su Controlla i risultati dettagliati verranno visualizzate informazioni sui risultati di hello per ogni test eseguito. È inoltre possibile salvare toodisk risultati hello in ordine tooshare li.
 
>[!NOTE]
>Hello analizzatore connettività inoltre verifica la federazione attiva con hello WS *-i protocolli di base ed ECP/PAOS. Se non si usano questi è possibile ignorare hello il seguente errore: test hello flusso di accesso Active utilizzando l'endpoint di federazione attivo del provider di identità.

### <a name="manually-verify-that-single-sign-on-has-been-set-up-correctly"></a>Verificare manualmente la corretta configurazione di Single Sign-On
Verifica manuale comporta i passaggi aggiuntivi che è possibile eseguire tooensure che il Provider di identità SAML 2.0 funzioni correttamente in molti scenari.
tooverify che l'accesso single sign-on è stato configurato correttamente, completare hello seguenti passaggi:


1. In un computer aggiunto al dominio, accedere nel servizio cloud tooyour utilizzando hello stesso nome utilizzato per le credenziali aziendali di accesso.
2.  Fare clic nella casella password hello. Se l'accesso single sign-on è impostato, hello password casella sarà ombreggiata e verrà visualizzato hello seguente messaggio: "sono ora necessari toosign in a <your company>."
3.  Fare clic su hello Accedi a <your company> collegamento. Se si è in grado di toosign in, quindi accesso single sign-on è stato impostato.

## <a name="next-steps"></a>Passaggi successivi


- [Gestione e personalizzazione di Active Directory Federation Services con Azure AD Connect](active-directory-aadconnect-federation-management.md)
- [Elenco di compatibilità di federazione di Azure AD](active-directory-aadconnect-federation-compatibility.md)
- [Installazione personalizzata di Azure AD Connect](active-directory-aadconnect-get-started-custom.md)
