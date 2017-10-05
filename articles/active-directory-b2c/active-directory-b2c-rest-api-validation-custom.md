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
ms.openlocfilehash: eb44a0d2234c9ee3801d8b3a1655d877aa2f4fef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="95cb5-103">Procedura dettagliata: Integrare scambi di attestazioni API REST nel percorso utente di Azure AD B2C come convalida dell'input utente</span><span class="sxs-lookup"><span data-stu-id="95cb5-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="95cb5-104">Il framework dell'esperienza di gestione delle identità alla base di Azure Active Directory B2C (Azure AD B2C) consente allo sviluppatore delle identità di integrare un'interazione con un'API RESTful in un percorso utente.</span><span class="sxs-lookup"><span data-stu-id="95cb5-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="95cb5-105">Al termine di questa procedura dettagliata sarà possibile creare percorsi utente di Azure AD B2C che interagiscono con i servizi RESTful.</span><span class="sxs-lookup"><span data-stu-id="95cb5-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="95cb5-106">Il framework dell'esperienza di gestione delle identità invia i dati in attestazioni e riceve di nuovo i dati in attestazioni.</span><span class="sxs-lookup"><span data-stu-id="95cb5-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="95cb5-107">L'interazione con l'API:</span><span class="sxs-lookup"><span data-stu-id="95cb5-107">The interaction with the API:</span></span>

- <span data-ttu-id="95cb5-108">Può essere progettata come scambio di attestazioni API REST o come profilo di convalida all'interno di un passaggio di orchestrazione.</span><span class="sxs-lookup"><span data-stu-id="95cb5-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="95cb5-109">In genere viene convalidato l'input dell'utente.</span><span class="sxs-lookup"><span data-stu-id="95cb5-109">Typically validates input from the user.</span></span> <span data-ttu-id="95cb5-110">Se il valore fornito dall'utente viene rifiutato, l'utente può provare nuovamente a immettere un valore valido con la possibilità di restituire un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="95cb5-110">If the value from the user is rejected, the user can try again to enter a valid value with the opportunity to return an error message.</span></span>

<span data-ttu-id="95cb5-111">È possibile progettare l'interazione anche come passaggio di orchestrazione.</span><span class="sxs-lookup"><span data-stu-id="95cb5-111">You can also design the interaction as an orchestration step.</span></span> <span data-ttu-id="95cb5-112">Per altre informazioni, vedere [Procedura dettagliata: Integrare scambi di attestazioni API REST nei percorsi utente di Azure AD B2C come passaggio di orchestrazione](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="95cb5-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="95cb5-113">Per l'esempio del profilo di convalida si userà il percorso utente di modifica profilo disponibile nel file ProfileEdit.xml dello starter pack.</span><span class="sxs-lookup"><span data-stu-id="95cb5-113">For the validation profile example, we will use the profile edit user journey in the starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="95cb5-114">È possibile verificare che il nome fornito dall'utente nella modifica del profilo non faccia parte di un elenco di esclusione.</span><span class="sxs-lookup"><span data-stu-id="95cb5-114">We can verify that the name provided by the user in the profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95cb5-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="95cb5-115">Prerequisites</span></span>

- <span data-ttu-id="95cb5-116">Un tenant di Azure AD B2C configurato per completare una procedura di iscrizione/accesso di un account locale, come descritto in [Introduzione](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="95cb5-116">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="95cb5-117">Un endpoint API REST con il quale interagire.</span><span class="sxs-lookup"><span data-stu-id="95cb5-117">A REST API endpoint to interact with.</span></span> <span data-ttu-id="95cb5-118">Per questa procedura dettagliata è stato configurato un sito demo denominato [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) con un servizio API REST.</span><span class="sxs-lookup"><span data-stu-id="95cb5-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="95cb5-119">Passaggio 1: Preparare la funzione API REST</span><span class="sxs-lookup"><span data-stu-id="95cb5-119">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="95cb5-120">La configurazione delle funzioni API REST non rientra nell'ambito di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="95cb5-120">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="95cb5-121">[Funzioni di Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) offre un eccellente toolkit per creare servizi RESTful nel cloud.</span><span class="sxs-lookup"><span data-stu-id="95cb5-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="95cb5-122">È stata creata una funzione di Azure che riceve un'attestazione prevista come `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="95cb5-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="95cb5-123">La funzione verifica che l'attestazione esista.</span><span class="sxs-lookup"><span data-stu-id="95cb5-123">The function validates whether this claim exists.</span></span> <span data-ttu-id="95cb5-124">È possibile accedere al codice completo della funzione di Azure in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="95cb5-124">You can access the complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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
      userMessage = $"The player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="95cb5-125">L'attestazione `userMessage` restituita dalla funzione di Azure è prevista dal framework dell'esperienza di gestione delle identità</span><span class="sxs-lookup"><span data-stu-id="95cb5-125">The IEF expects the `userMessage` claim that the Azure function returns.</span></span> <span data-ttu-id="95cb5-126">e verrà visualizzata all'utente sotto forma di stringa se la convalida non riesce, ad esempio quando viene restituito lo stato di conflitto 409 nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="95cb5-126">This claim will be presented as a string to the user if the validation fails, such as when a 409 conflict status is returned in the preceding example.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="95cb5-127">Passaggio 2: Configurare lo scambio di attestazioni API RESTful come profilo tecnico nel file TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="95cb5-127">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="95cb5-128">Un profilo tecnico è la configurazione completa dello scambio desiderato con il servizio RESTful.</span><span class="sxs-lookup"><span data-stu-id="95cb5-128">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="95cb5-129">Aprire il file TrustFrameworkExtensions.xml e aggiungere il frammento XML seguente all'interno dell'elemento `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="95cb5-129">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="95cb5-130">Nell'XML seguente il provider RESTful `Version=1.0.0.0` viene descritto come il protocollo.</span><span class="sxs-lookup"><span data-stu-id="95cb5-130">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="95cb5-131">Considerarlo come la funzione che interagirà con il servizio esterno.</span><span class="sxs-lookup"><span data-stu-id="95cb5-131">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="95cb5-132">L'elemento `InputClaims` definisce le attestazioni che verranno inviate dal framework dell'esperienza di gestione delle identità al servizio REST.</span><span class="sxs-lookup"><span data-stu-id="95cb5-132">The `InputClaims` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="95cb5-133">In questo esempio il contenuto dell'attestazione `givenName` verrà inviato al servizio REST come `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="95cb5-133">In this example, the contents of the claim `givenName` will be sent to the REST service as `playerTag`.</span></span> <span data-ttu-id="95cb5-134">In questo esempio, il framework dell'esperienza di gestione non prevede di ricevere attestazioni,</span><span class="sxs-lookup"><span data-stu-id="95cb5-134">In this example, the IEF does not expect claims back.</span></span> <span data-ttu-id="95cb5-135">ma attende una risposta dal servizio REST e agisce in base ai codici di stato ricevuti.</span><span class="sxs-lookup"><span data-stu-id="95cb5-135">Instead, it waits for a response from the REST service and acts based on the status codes that it receives.</span></span>

## <a name="step-3-include-the-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-to-validate-the-user-input"></a><span data-ttu-id="95cb5-136">Passaggio 3: Includere lo scambio di attestazioni del servizio RESTful nel profilo tecnico autocertificato in cui si vuole convalidare l'input dell'utente</span><span class="sxs-lookup"><span data-stu-id="95cb5-136">Step 3: Include the RESTful service claims exchange in self-asserted technical profile where you want to validate the user input</span></span>

<span data-ttu-id="95cb5-137">L'uso più comune del passaggio di convalida è nell'interazione con un utente.</span><span class="sxs-lookup"><span data-stu-id="95cb5-137">The most common use of the validation step is in the interaction with a user.</span></span> <span data-ttu-id="95cb5-138">Tutte le interazioni in cui è previsto che l'utente fornisca un input sono *profili tecnici autocertificati*.</span><span class="sxs-lookup"><span data-stu-id="95cb5-138">All interactions where the user is expected to provide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="95cb5-139">Per questo esempio si aggiungerà la convalida al profilo tecnico Self-Asserted-ProfileUpdate.</span><span class="sxs-lookup"><span data-stu-id="95cb5-139">For this example, we will add the validation to the Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="95cb5-140">Questo è il profilo tecnico usato dal file dei criteri relying party `Profile Edit`.</span><span class="sxs-lookup"><span data-stu-id="95cb5-140">This is the technical profile that the relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="95cb5-141">Per aggiungere lo scambio di attestazioni al profilo tecnico autocertificato:</span><span class="sxs-lookup"><span data-stu-id="95cb5-141">To add the claims exchange to the self-asserted technical profile:</span></span>

1. <span data-ttu-id="95cb5-142">Aprire il file TrustFrameworkBase.xml e cercare `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="95cb5-142">Open the TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="95cb5-143">Esaminare la configurazione di questo profilo tecnico.</span><span class="sxs-lookup"><span data-stu-id="95cb5-143">Review the configuration of this technical profile.</span></span> <span data-ttu-id="95cb5-144">Si noti che lo scambio con l'utente è definito come attestazioni che verranno chieste all'utente (attestazioni di input) e attestazioni che dovranno essere inviate dal provider autocertificato (attestazioni di output).</span><span class="sxs-lookup"><span data-stu-id="95cb5-144">Observe how the exchange with the user is defined as claims that will be asked of the user (input claims) and claims that will be expected back from the self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="95cb5-145">Cercare `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`. Tenere presente che questo profilo viene richiamato come passaggio di orchestrazione 6 di `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="95cb5-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-the-profile-edit-rp-policy-file"></a><span data-ttu-id="95cb5-146">Passaggio 4: Caricare e testare il file dei criteri relying party di modifica del profilo</span><span class="sxs-lookup"><span data-stu-id="95cb5-146">Step 4: Upload and test the profile edit RP policy file</span></span>

1. <span data-ttu-id="95cb5-147">Caricare la nuova versione del file TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="95cb5-147">Upload the new version of the TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="95cb5-148">Usare **Esegui adesso** per testare il file dei criteri relying party di modifica del profilo.</span><span class="sxs-lookup"><span data-stu-id="95cb5-148">Use **Run now** to test the profile edit RP policy file.</span></span>
3. <span data-ttu-id="95cb5-149">Testare la convalida specificando uno dei nomi esistenti, ad esempio mcvinny, nel campo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="95cb5-149">Test the validation by providing one of the existing names (for example, mcvinny) in the **Given Name** field.</span></span> <span data-ttu-id="95cb5-150">Se la configurazione è stata eseguita correttamente, verrà visualizzato un messaggio per avvisare l'utente che il tag del player è già in uso.</span><span class="sxs-lookup"><span data-stu-id="95cb5-150">If everything is set up correctly, you should receive a message that notifies the user that the player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95cb5-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="95cb5-151">Next steps</span></span>

[<span data-ttu-id="95cb5-152">Cambiare la modifica del profilo e la registrazione degli utenti per raccogliere informazioni dagli utenti</span><span class="sxs-lookup"><span data-stu-id="95cb5-152">Modify the profile edit and user registration to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="95cb5-153">Procedura dettagliata: Integrare scambi di attestazioni API REST nei percorsi utente di Azure AD B2C come passaggio di orchestrazione</span><span class="sxs-lookup"><span data-stu-id="95cb5-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
