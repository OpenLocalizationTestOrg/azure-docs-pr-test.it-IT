---
title: 'Azure Active B2C di Directory: scambi di attestazioni API REST come convalida | Microsoft Docs'
description: Un argomento sui criteri personalizzati di Azure Active Directory B2C
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
ms.openlocfilehash: cec6c6e110514a8bbe0e0780f36738ff21ae2f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a>Procedura dettagliata: Integrare scambi di attestazioni API REST nel percorso utente di Azure AD B2C come convalida dell'input utente

Hello identità esperienza Framework (IEF) sottostante di Azure Active Directory B2C (Azure AD B2C) consente di hello identità developer toointegrate un'interazione con un'API RESTful in viaggio un utente.  

Alla fine di hello di questa procedura dettagliata, si sarà in grado di toocreate un proprio processo utente Azure AD B2C che interagisce con servizi RESTful.

Hello IEF invia i dati delle attestazioni e riceve i dati nuovamente nelle attestazioni. interazione di Hello con hello API:

- Può essere progettata come scambio di attestazioni API REST o come profilo di convalida all'interno di un passaggio di orchestrazione.
- In genere convalida l'input utente hello. Se il valore di hello utente hello viene rifiutato, utente hello riprovare tooenter un valore valido con hello opportunità tooreturn un messaggio di errore.

È inoltre possibile progettare l'interazione di hello come un passaggio di orchestrazione. Per altre informazioni, vedere [Procedura dettagliata: Integrare scambi di attestazioni API REST nei percorsi utente di Azure AD B2C come passaggio di orchestrazione](active-directory-b2c-rest-api-step-custom.md).

Ad esempio di profilo di convalida hello, verrà utilizzato nel file di pacchetto starter hello ProfileEdit.xml viaggio di hello profilo Modifica utente.

Possiamo verificare il nome di hello fornito dall'utente hello nel profilo hello modifica non fa parte di un elenco di esclusione.

## <a name="prerequisites"></a>Prerequisiti

- Un toocomplete di tenant configurato un account locale sign-configurazione/Accedi, come descritto in Azure Active Directory B2C [Introduzione](active-directory-b2c-get-started-custom.md).
- Toointeract un endpoint API REST con. Per questa procedura dettagliata è stato configurato un sito demo denominato [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) con un servizio API REST.

## <a name="step-1-prepare-hello-rest-api-function"></a>Passaggio 1: Preparare la funzione di API REST hello

> [!NOTE]
> Il programma di installazione di funzioni API REST è di fuori ambito hello di questo articolo. [Funzioni di Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) offre un'eccellente toolkit toocreate servizi RESTful nel cloud hello.

È stata creata una funzione di Azure che riceve un'attestazione prevista come `playerTag`. funzione Hello convalida l'esistenza di questa attestazione. È possibile accedere a codice della funzione di Azure completo hello in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

```csharp
if (requestContentAsJObject.playerTag == null)
{
  return request.CreateResponse(HttpStatusCode.BadRequest);
}

var playerTag = ((string) requestContentAsJObject.playerTag).ToLower();

if (playerTag == "mcvinny" || playerTag == "msgates123" || playerTag == "revcottonmarcus")
{
  return request.CreateResponse<ResponseContent>(
    HttpStatusCode.Conflict,
    new ResponseContent
    {
      version = "1.0.0",
      status = (int) HttpStatusCode.Conflict,
      userMessage = $"hello player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

Hello IEF prevede hello `userMessage` attestazione restituisce tale funzione Azure hello. Questa attestazione verrà presentata come un utente toohello stringa se hello convalida ha esito negativo, ad esempio quando lo stato di 409 conflitto viene restituito in hello sopra riportato.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a>Passaggio 2: Configurare hello API RESTful attestazioni exchange come profilo tecnico nel file TrustFrameworkExtensions.xml

Un profilo tecnico è configurazione completa di hello di exchange hello desiderato con hello servizio RESTful. Aprire il file TrustFrameworkExtensions.xml hello e aggiungere hello seguente frammento di codice XML all'interno di hello `<ClaimsProviders>` elemento.

> [!NOTE]
> Nel seguente codice XML, provider RESTful hello `Version=1.0.0.0` viene descritto come protocollo di hello. Viene considerata come funzione hello che interagirà con il servizio esterno hello. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```xml
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-CheckPlayerTagWebHook">
            <DisplayName>Check Player Tag Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/CheckPlayerTagWebHook?code=L/05YRSpojU0nECzM4Tp3LjBiA2ZGh3kTwwp1OVV7m0SelnvlRVLCg==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="playerTag" />
            </InputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
        <TechnicalProfile Id="SelfAsserted-ProfileUpdate">
            <ValidationTechnicalProfiles>
                <ValidationTechnicalProfile ReferenceId="AzureFunctions-CheckPlayerTagWebHook" />
            </ValidationTechnicalProfiles>
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Hello `InputClaims` elemento definisce le attestazioni hello che verranno inviate dal servizio REST di toohello IEF hello. In questo esempio, i contenuti dell'attestazione hello hello `givenName` verrà inviato il servizio REST toohello come `playerTag`. In questo esempio hello che IEF non prevede le attestazioni di nuovo. In alternativa, è in attesa di una risposta dal servizio REST hello e agisce in base ai codici di stato hello che riceve.

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a>Passaggio 3: Includere hello servizio RESTful attestazioni exchange nel profilo di tecnico asserzione autonomo in cui si desidera toovalidate hello l'input dell'utente

utilizzo più comune di Hello di passaggio di convalida hello è interazione hello con un utente. Tutte le interazioni dove utente hello è previsto tooprovide di input sono *automatica dichiarata profili tecnici*. Per questo esempio, si aggiungerà profilo tecniche di hello convalida toohello Self Asserted-ProfileUpdate. Si tratta di profilo tecniche hello che hello file dei criteri relying party (RP) `Profile Edit` utilizza.

tooadd hello attestazioni exchange toohello automatica dichiarata tecnico profilo:

1. Aprire il file di TrustFrameworkBase.xml hello e cercare `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.
2. Verificare la configurazione hello del profilo corrente tecnico. Osservare come exchange hello con utente hello è definito attestazioni che verranno richiesto di utente hello (attestazioni di input) e che sarà necessario tornare dal provider di self-asserzione hello (attestazioni di output).
3. Cercare `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`. Tenere presente che questo profilo viene richiamato come passaggio di orchestrazione 6 di `<UserJourney Id="ProfileEdit">`.

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a>Passaggio 4: Caricare e verificare i file dei criteri RP Modifica profilo hello

1. Caricare hello nuova versione del file TrustFrameworkExtensions.xml hello.
2. Utilizzare **Esegui ora** profilo hello tootest modificare il file di criteri di relying Party.
3. Il test di convalida hello fornendo uno dei nomi esistente hello (ad esempio, mcvinny) in hello **nome** campo. Se tutto è configurato correttamente, verrà visualizzato un messaggio che avvisa gli utenti di hello tag player hello viene già utilizzato.

## <a name="next-steps"></a>Passaggi successivi

[Modificare hello profilo utente e Modifica registrazione toogather informazioni aggiuntive agli utenti](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[Procedura dettagliata: Integrare scambi di attestazioni API REST nei percorsi utente di Azure AD B2C come passaggio di orchestrazione](active-directory-b2c-rest-api-step-custom.md)
