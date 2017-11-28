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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="3a179-103">Procedura dettagliata: Integrare scambi di attestazioni API REST nel percorso utente di Azure AD B2C come convalida dell'input utente</span><span class="sxs-lookup"><span data-stu-id="3a179-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="3a179-104">Hello identità esperienza Framework (IEF) sottostante di Azure Active Directory B2C (Azure AD B2C) consente di hello identità developer toointegrate un'interazione con un'API RESTful in viaggio un utente.</span><span class="sxs-lookup"><span data-stu-id="3a179-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="3a179-105">Alla fine di hello di questa procedura dettagliata, si sarà in grado di toocreate un proprio processo utente Azure AD B2C che interagisce con servizi RESTful.</span><span class="sxs-lookup"><span data-stu-id="3a179-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="3a179-106">Hello IEF invia i dati delle attestazioni e riceve i dati nuovamente nelle attestazioni.</span><span class="sxs-lookup"><span data-stu-id="3a179-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="3a179-107">interazione di Hello con hello API:</span><span class="sxs-lookup"><span data-stu-id="3a179-107">hello interaction with hello API:</span></span>

- <span data-ttu-id="3a179-108">Può essere progettata come scambio di attestazioni API REST o come profilo di convalida all'interno di un passaggio di orchestrazione.</span><span class="sxs-lookup"><span data-stu-id="3a179-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="3a179-109">In genere convalida l'input utente hello.</span><span class="sxs-lookup"><span data-stu-id="3a179-109">Typically validates input from hello user.</span></span> <span data-ttu-id="3a179-110">Se il valore di hello utente hello viene rifiutato, utente hello riprovare tooenter un valore valido con hello opportunità tooreturn un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="3a179-110">If hello value from hello user is rejected, hello user can try again tooenter a valid value with hello opportunity tooreturn an error message.</span></span>

<span data-ttu-id="3a179-111">È inoltre possibile progettare l'interazione di hello come un passaggio di orchestrazione.</span><span class="sxs-lookup"><span data-stu-id="3a179-111">You can also design hello interaction as an orchestration step.</span></span> <span data-ttu-id="3a179-112">Per altre informazioni, vedere [Procedura dettagliata: Integrare scambi di attestazioni API REST nei percorsi utente di Azure AD B2C come passaggio di orchestrazione](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="3a179-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="3a179-113">Ad esempio di profilo di convalida hello, verrà utilizzato nel file di pacchetto starter hello ProfileEdit.xml viaggio di hello profilo Modifica utente.</span><span class="sxs-lookup"><span data-stu-id="3a179-113">For hello validation profile example, we will use hello profile edit user journey in hello starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="3a179-114">Possiamo verificare il nome di hello fornito dall'utente hello nel profilo hello modifica non fa parte di un elenco di esclusione.</span><span class="sxs-lookup"><span data-stu-id="3a179-114">We can verify that hello name provided by hello user in hello profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a179-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3a179-115">Prerequisites</span></span>

- <span data-ttu-id="3a179-116">Un toocomplete di tenant configurato un account locale sign-configurazione/Accedi, come descritto in Azure Active Directory B2C [Introduzione](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="3a179-116">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="3a179-117">Toointeract un endpoint API REST con.</span><span class="sxs-lookup"><span data-stu-id="3a179-117">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="3a179-118">Per questa procedura dettagliata è stato configurato un sito demo denominato [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) con un servizio API REST.</span><span class="sxs-lookup"><span data-stu-id="3a179-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="3a179-119">Passaggio 1: Preparare la funzione di API REST hello</span><span class="sxs-lookup"><span data-stu-id="3a179-119">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="3a179-120">Il programma di installazione di funzioni API REST è di fuori ambito hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3a179-120">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="3a179-121">[Funzioni di Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) offre un'eccellente toolkit toocreate servizi RESTful nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="3a179-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="3a179-122">È stata creata una funzione di Azure che riceve un'attestazione prevista come `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="3a179-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="3a179-123">funzione Hello convalida l'esistenza di questa attestazione.</span><span class="sxs-lookup"><span data-stu-id="3a179-123">hello function validates whether this claim exists.</span></span> <span data-ttu-id="3a179-124">È possibile accedere a codice della funzione di Azure completo hello in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="3a179-124">You can access hello complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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

<span data-ttu-id="3a179-125">Hello IEF prevede hello `userMessage` attestazione restituisce tale funzione Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3a179-125">hello IEF expects hello `userMessage` claim that hello Azure function returns.</span></span> <span data-ttu-id="3a179-126">Questa attestazione verrà presentata come un utente toohello stringa se hello convalida ha esito negativo, ad esempio quando lo stato di 409 conflitto viene restituito in hello sopra riportato.</span><span class="sxs-lookup"><span data-stu-id="3a179-126">This claim will be presented as a string toohello user if hello validation fails, such as when a 409 conflict status is returned in hello preceding example.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="3a179-127">Passaggio 2: Configurare hello API RESTful attestazioni exchange come profilo tecnico nel file TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="3a179-127">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="3a179-128">Un profilo tecnico è configurazione completa di hello di exchange hello desiderato con hello servizio RESTful.</span><span class="sxs-lookup"><span data-stu-id="3a179-128">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="3a179-129">Aprire il file TrustFrameworkExtensions.xml hello e aggiungere hello seguente frammento di codice XML all'interno di hello `<ClaimsProviders>` elemento.</span><span class="sxs-lookup"><span data-stu-id="3a179-129">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="3a179-130">Nel seguente codice XML, provider RESTful hello `Version=1.0.0.0` viene descritto come protocollo di hello.</span><span class="sxs-lookup"><span data-stu-id="3a179-130">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="3a179-131">Viene considerata come funzione hello che interagirà con il servizio esterno hello.</span><span class="sxs-lookup"><span data-stu-id="3a179-131">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="3a179-132">Hello `InputClaims` elemento definisce le attestazioni hello che verranno inviate dal servizio REST di toohello IEF hello.</span><span class="sxs-lookup"><span data-stu-id="3a179-132">hello `InputClaims` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="3a179-133">In questo esempio, i contenuti dell'attestazione hello hello `givenName` verrà inviato il servizio REST toohello come `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="3a179-133">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as `playerTag`.</span></span> <span data-ttu-id="3a179-134">In questo esempio hello che IEF non prevede le attestazioni di nuovo.</span><span class="sxs-lookup"><span data-stu-id="3a179-134">In this example, hello IEF does not expect claims back.</span></span> <span data-ttu-id="3a179-135">In alternativa, è in attesa di una risposta dal servizio REST hello e agisce in base ai codici di stato hello che riceve.</span><span class="sxs-lookup"><span data-stu-id="3a179-135">Instead, it waits for a response from hello REST service and acts based on hello status codes that it receives.</span></span>

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a><span data-ttu-id="3a179-136">Passaggio 3: Includere hello servizio RESTful attestazioni exchange nel profilo di tecnico asserzione autonomo in cui si desidera toovalidate hello l'input dell'utente</span><span class="sxs-lookup"><span data-stu-id="3a179-136">Step 3: Include hello RESTful service claims exchange in self-asserted technical profile where you want toovalidate hello user input</span></span>

<span data-ttu-id="3a179-137">utilizzo più comune di Hello di passaggio di convalida hello è interazione hello con un utente.</span><span class="sxs-lookup"><span data-stu-id="3a179-137">hello most common use of hello validation step is in hello interaction with a user.</span></span> <span data-ttu-id="3a179-138">Tutte le interazioni dove utente hello è previsto tooprovide di input sono *automatica dichiarata profili tecnici*.</span><span class="sxs-lookup"><span data-stu-id="3a179-138">All interactions where hello user is expected tooprovide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="3a179-139">Per questo esempio, si aggiungerà profilo tecniche di hello convalida toohello Self Asserted-ProfileUpdate.</span><span class="sxs-lookup"><span data-stu-id="3a179-139">For this example, we will add hello validation toohello Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="3a179-140">Si tratta di profilo tecniche hello che hello file dei criteri relying party (RP) `Profile Edit` utilizza.</span><span class="sxs-lookup"><span data-stu-id="3a179-140">This is hello technical profile that hello relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="3a179-141">tooadd hello attestazioni exchange toohello automatica dichiarata tecnico profilo:</span><span class="sxs-lookup"><span data-stu-id="3a179-141">tooadd hello claims exchange toohello self-asserted technical profile:</span></span>

1. <span data-ttu-id="3a179-142">Aprire il file di TrustFrameworkBase.xml hello e cercare `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="3a179-142">Open hello TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="3a179-143">Verificare la configurazione hello del profilo corrente tecnico.</span><span class="sxs-lookup"><span data-stu-id="3a179-143">Review hello configuration of this technical profile.</span></span> <span data-ttu-id="3a179-144">Osservare come exchange hello con utente hello è definito attestazioni che verranno richiesto di utente hello (attestazioni di input) e che sarà necessario tornare dal provider di self-asserzione hello (attestazioni di output).</span><span class="sxs-lookup"><span data-stu-id="3a179-144">Observe how hello exchange with hello user is defined as claims that will be asked of hello user (input claims) and claims that will be expected back from hello self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="3a179-145">Cercare `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`. Tenere presente che questo profilo viene richiamato come passaggio di orchestrazione 6 di `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="3a179-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a><span data-ttu-id="3a179-146">Passaggio 4: Caricare e verificare i file dei criteri RP Modifica profilo hello</span><span class="sxs-lookup"><span data-stu-id="3a179-146">Step 4: Upload and test hello profile edit RP policy file</span></span>

1. <span data-ttu-id="3a179-147">Caricare hello nuova versione del file TrustFrameworkExtensions.xml hello.</span><span class="sxs-lookup"><span data-stu-id="3a179-147">Upload hello new version of hello TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="3a179-148">Utilizzare **Esegui ora** profilo hello tootest modificare il file di criteri di relying Party.</span><span class="sxs-lookup"><span data-stu-id="3a179-148">Use **Run now** tootest hello profile edit RP policy file.</span></span>
3. <span data-ttu-id="3a179-149">Il test di convalida hello fornendo uno dei nomi esistente hello (ad esempio, mcvinny) in hello **nome** campo.</span><span class="sxs-lookup"><span data-stu-id="3a179-149">Test hello validation by providing one of hello existing names (for example, mcvinny) in hello **Given Name** field.</span></span> <span data-ttu-id="3a179-150">Se tutto è configurato correttamente, verrà visualizzato un messaggio che avvisa gli utenti di hello tag player hello viene già utilizzato.</span><span class="sxs-lookup"><span data-stu-id="3a179-150">If everything is set up correctly, you should receive a message that notifies hello user that hello player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a179-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3a179-151">Next steps</span></span>

[<span data-ttu-id="3a179-152">Modificare hello profilo utente e Modifica registrazione toogather informazioni aggiuntive agli utenti</span><span class="sxs-lookup"><span data-stu-id="3a179-152">Modify hello profile edit and user registration toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="3a179-153">Procedura dettagliata: Integrare scambi di attestazioni API REST nei percorsi utente di Azure AD B2C come passaggio di orchestrazione</span><span class="sxs-lookup"><span data-stu-id="3a179-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
