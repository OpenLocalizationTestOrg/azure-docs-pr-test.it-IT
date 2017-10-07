---
title: 'Azure Active Directory B2C: scambi di attestazioni API REST come passaggio di orchestrazione | Microsoft Docs'
description: Argomento relativo all'integrazione dei criteri personalizzati di Azure Active Directory B2C con un'API
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/24/2017
ms.author: joroja
ms.openlocfilehash: 90a495029f48d70232ef3f99de4ea4d351395aa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a>Procedura dettagliata: Integrare scambi di attestazioni API REST nei percorsi utente di Azure AD B2C come passaggio di orchestrazione

Hello identità esperienza Framework (IEF) sottostante di Azure Active Directory B2C (Azure AD B2C) consente di hello identità developer toointegrate un'interazione con un'API RESTful in viaggio un utente.  

Alla fine di hello di questa procedura dettagliata, si sarà in grado di toocreate un proprio processo utente Azure AD B2C che interagisce con servizi RESTful.

Hello IEF invia i dati delle attestazioni e riceve i dati nuovamente nelle attestazioni. Hello exchange attestazioni API REST:

- Può essere progettato come passaggio di orchestrazione.
- Può attivare un'azione esterna. Può registrare ad esempio un evento in un database esterno.
- Può essere utilizzato toofetch un valore e quindi archiviarla nel database utente hello.

È possibile utilizzare le attestazioni ricevuta hello successive toochange hello il flusso di esecuzione.

È inoltre possibile progettare l'interazione di hello come un profilo di convalida. Per altre informazioni, vedere [Procedura dettagliata: Integrare scambi di attestazioni API REST nei percorsi utente di Azure AD B2C come convalida dell'input utente](active-directory-b2c-rest-api-validation-custom.md).

scenario di Hello è che quando un utente esegue la modifica di un profilo, si desidera:

1. Cercare l'utente hello in un sistema esterno.
2. Ottenere città hello in cui tale utente è registrato.
3. Restituisce tale applicazione toohello attributo come attestazione.

## <a name="prerequisites"></a>Prerequisiti

- Un toocomplete di tenant configurato un account locale sign-configurazione/Accedi, come descritto in Azure Active Directory B2C [Introduzione](active-directory-b2c-get-started-custom.md).
- Toointeract un endpoint API REST con. Questa procedura dettagliata usa come esempio un webhook di app per le funzioni di Azure molto semplice.
- *Consigliato*: hello completo [procedura dettagliata di exchange come passaggio di convalida di attestazioni di API REST](active-directory-b2c-rest-api-validation-custom.md).

## <a name="step-1-prepare-hello-rest-api-function"></a>Passaggio 1: Preparare la funzione di API REST hello

> [!NOTE]
> Il programma di installazione di funzioni API REST è di fuori ambito hello di questo articolo. [Funzioni di Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) offre un'eccellente toolkit toocreate servizi RESTful nel cloud hello.

È stata configurata una funzione di Azure che riceve un'attestazione chiamata `email`, e quindi restituisce hello attestazione `city` con valore hello assegnato `Redmond`. esempio Hello Azure funzione è nel [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

Hello `userMessage` attestazione che hello restituiti da funzioni di Azure è facoltativa in questo contesto e hello IEF verrà ignorato. È potenzialmente possibile utilizzarlo come un messaggio passato applicazione toohello e presentati toohello utente in un secondo momento.

```csharp
if (requestContentAsJObject.email == null)
{
    return request.CreateResponse(HttpStatusCode.BadRequest);
}

var email = ((string) requestContentAsJObject.email).ToLower();

return request.CreateResponse<ResponseContent>(
    HttpStatusCode.OK,
    new ResponseContent
    {
        version = "1.0.0",
        status = (int) HttpStatusCode.OK,
        userMessage = "User Found",
        city = "Redmond"
    },
    new JsonMediaTypeFormatter(),
    "application/json");
```

Un'app di funzione Azure rende facile tooget hello funzione URL, che include l'identificatore hello della funzione specifica hello. In questo caso, hello URL è: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==. È possibile usarlo per il test.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a>Passaggio 2: Configurare hello API RESTful attestazioni exchange come profilo tecnico nel file TrustFrameworExtensions.xml

Un profilo tecnico è configurazione completa di hello di exchange hello desiderato con hello servizio RESTful. Aprire il file TrustFrameworkExtensions.xml hello e aggiungere hello seguente frammento di codice XML all'interno di hello `<ClaimsProvider>` elemento.

> [!NOTE]
> Nel seguente codice XML, provider RESTful hello `Version=1.0.0.0` viene descritto come protocollo di hello. Viene considerata come funzione hello che interagirà con il servizio esterno hello. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```XML
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-LookUpLoyaltyWebHook">
            <DisplayName>Check LookUpLoyalty Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="email" />
            </InputClaims>
            <OutputClaims>
                <OutputClaim ClaimTypeReferenceId="city" PartnerClaimType="city" />
            </OutputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Hello `<InputClaims>` elemento definisce le attestazioni hello che verranno inviate dal servizio REST di toohello IEF hello. In questo esempio, i contenuti dell'attestazione hello hello `givenName` verranno inviati servizio REST toohello come attestazione hello `email`.  

Hello `<OutputClaims>` elemento definisce le attestazioni hello che hello IEF previsti dal servizio REST hello. Indipendentemente dal numero di hello di attestazioni che vengono ricevuti, hello IEF utilizzerà solo quelli individuati qui. In questo esempio, un'attestazione ricevuta come `city` verrà chiamato tooan mappato IEF attestazione `city`.

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a>Passaggio 3: Aggiungere una nuova attestazione hello `city` toohello schema del file TrustFrameworkExtensions.xml

attestazione Hello `city` non è ancora definito in questo schema. In tal caso, aggiungere una definizione di elemento di hello `<BuildingBlocks>`. È possibile trovare questo elemento all'inizio di hello del file TrustFrameworkExtensions.xml hello.

```XML
<BuildingBlocks>
    <!--hello claimtype city must be added toohello TrustFrameworkPolicy-->
    <!-- You can add new claims in hello BASE file Section III, or in hello extensions file-->
    <ClaimsSchema>
        <ClaimType Id="city">
            <DisplayName>City</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your city</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a>Passaggio 4: Includere scambio attestazioni del servizio REST hello come un passaggio di orchestrazione in percorso profilo utente modifica in TrustFrameworkExtensions.xml

Aggiungere un passaggio toohello profilo Modifica utente viaggio, dopo che l'utente hello è stato autenticato (orchestrazione i passaggi 1-4 in hello seguente XML) e l'utente hello ha fornito informazioni sul profilo hello aggiornato (passaggio 5).

> [!NOTE]
> Esistono numerosi casi d'uso in hello chiamata all'API REST può essere utilizzato come un passaggio di orchestrazione. Come un passaggio di orchestrazione, può essere utilizzato come un sistema esterno tooan di aggiornamento, dopo che un utente ha completato un'attività come prima registrazione, oppure come un profilo di aggiornare informazioni tookeep sincronizzate. In questo caso, è utilizzato tooaugment hello indicazioni toohello applicazione dopo la modifica profilo hello.

Copia hello profilo Modifica codice XML di viaggio utente dal hello TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml file all'interno di hello `<UserJourneys>` elemento. Apportare la modifica di hello nel passaggio 6.

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> Se l'ordine di hello non corrisponde alla versione, assicurarsi che sia inserito codice hello come passaggio hello prima hello `ClaimsExchange` tipo `SendClaims`.

XML finale per proprio processo utente hello Hello dovrebbe essere simile al seguente:

```XML
<UserJourney Id="ProfileEdit">
    <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
            <ClaimsProviderSelections>
                <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
                <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
            </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
                <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>localAccountAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserRead" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>socialIdpAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserReadWithObjectId" TechnicalProfileReferenceId="AAD-UserReadUsingObjectId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="5" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="B2CUserProfileUpdateExchange" TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <!-- Add a step 6 toohello user journey before hello JWT token is created-->
        <OrchestrationStep Order="6" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="7" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
    </OrchestrationSteps>
    <ClientDefinition ReferenceId="DefaultWeb" />
</UserJourney>
```

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a>Passaggio 5: Aggiungere hello attestazione `city` file di criteri di tooyour relying party attestazione hello viene inviato tooyour applicazione

Modificare il file di ProfileEdit.xml relying party (RP) e modificare hello `<TechnicalProfile Id="PolicyProfile">` seguente di hello elemento tooadd: `<OutputClaim ClaimTypeReferenceId="city" />`.

Dopo aver aggiunto una nuova attestazione hello, profilo tecniche hello è simile al seguente:

```XML
<DisplayName>PolicyProfile</DisplayName>
    <Protocol Name="OpenIdConnect" />
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
</TechnicalProfile>
```

## <a name="step-6-upload-your-changes-and-test"></a>Passaggio 6: Caricare le modifiche ed eseguire un test

Sovrascrivi le versioni esistenti di hello del criterio hello.

1.  (Facoltativo:) Salvare la versione esistente di hello (scaricando) del file con estensioni prima di procedere. tookeep hello iniziale complessità bassa, si consiglia di non caricare più versioni di hello estensioni file.
2.  (Facoltativo:) Rinominare una nuova versione di hello di ID criteri hello per file di modifica dei criteri di hello modificando `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.
3.  Caricare file estensioni hello.
4.  Caricare file RP Modifica criteri di hello.
5.  Utilizzare **Esegui** criteri hello tootest. Token di hello revisione hello IEF restituisce toohello applicazione.

Se tutto è configurato correttamente, il token hello includerà nuova attestazione hello `city`, con valore hello `Redmond`.

```JSON
{
  "exp": 1493053292,
  "nbf": 1493049692,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493049692,
  "auth_time": 1493049692,
  "city": "Redmond"
}
```

## <a name="next-steps"></a>Passaggi successivi

[Usare un'API REST come passaggio di convalida](active-directory-b2c-rest-api-validation-custom.md)

[Modificare hello profilo Modifica toogather informazioni aggiuntive agli utenti](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
