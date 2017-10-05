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
ms.openlocfilehash: dc319c97e64e55861b84cc3943667418077a05d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="c305d-103">Procedura dettagliata: Integrare scambi di attestazioni API REST nei percorsi utente di Azure AD B2C come passaggio di orchestrazione</span><span class="sxs-lookup"><span data-stu-id="c305d-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="c305d-104">Il framework dell'esperienza di gestione delle identità alla base di Azure Active Directory B2C (Azure AD B2C) consente allo sviluppatore delle identità di integrare un'interazione con un'API RESTful in un percorso utente.</span><span class="sxs-lookup"><span data-stu-id="c305d-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="c305d-105">Al termine di questa procedura dettagliata sarà possibile creare percorsi utente di Azure AD B2C che interagiscono con i servizi RESTful.</span><span class="sxs-lookup"><span data-stu-id="c305d-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="c305d-106">Il framework dell'esperienza di gestione delle identità invia i dati in attestazioni e riceve di nuovo i dati in attestazioni.</span><span class="sxs-lookup"><span data-stu-id="c305d-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="c305d-107">Lo scambio di attestazioni di API REST:</span><span class="sxs-lookup"><span data-stu-id="c305d-107">The REST API claims exchange:</span></span>

- <span data-ttu-id="c305d-108">Può essere progettato come passaggio di orchestrazione.</span><span class="sxs-lookup"><span data-stu-id="c305d-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="c305d-109">Può attivare un'azione esterna.</span><span class="sxs-lookup"><span data-stu-id="c305d-109">Can trigger an external action.</span></span> <span data-ttu-id="c305d-110">Può registrare ad esempio un evento in un database esterno.</span><span class="sxs-lookup"><span data-stu-id="c305d-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="c305d-111">Consente di recuperare un valore e quindi archiviarlo nel database utente.</span><span class="sxs-lookup"><span data-stu-id="c305d-111">Can be used to fetch a value and then store it in the user database.</span></span>

<span data-ttu-id="c305d-112">È possibile usare le attestazioni ricevute in un secondo momento per modificare il flusso di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c305d-112">You can use the received claims later to change the flow of execution.</span></span>

<span data-ttu-id="c305d-113">È anche possibile progettare l'interazione come un profilo di convalida.</span><span class="sxs-lookup"><span data-stu-id="c305d-113">You can also design the interaction as a validation profile.</span></span> <span data-ttu-id="c305d-114">Per altre informazioni, vedere [Procedura dettagliata: Integrare scambi di attestazioni API REST nei percorsi utente di Azure AD B2C come convalida dell'input utente](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="c305d-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="c305d-115">Lo scenario è che quando un utente esegue la modifica di un profilo, si desidera:</span><span class="sxs-lookup"><span data-stu-id="c305d-115">The scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="c305d-116">Cercare l'utente in un sistema esterno.</span><span class="sxs-lookup"><span data-stu-id="c305d-116">Look up the user in an external system.</span></span>
2. <span data-ttu-id="c305d-117">Ottenere la città in cui tale utente è registrato.</span><span class="sxs-lookup"><span data-stu-id="c305d-117">Get the city where that user is registered.</span></span>
3. <span data-ttu-id="c305d-118">Restituire tale attributo all'applicazione come un'attestazione.</span><span class="sxs-lookup"><span data-stu-id="c305d-118">Return that attribute to the application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c305d-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c305d-119">Prerequisites</span></span>

- <span data-ttu-id="c305d-120">Un tenant di Azure AD B2C configurato per completare una procedura di iscrizione/accesso di un account locale, come descritto in [Introduzione](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="c305d-120">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="c305d-121">Un endpoint API REST con il quale interagire.</span><span class="sxs-lookup"><span data-stu-id="c305d-121">A REST API endpoint to interact with.</span></span> <span data-ttu-id="c305d-122">Questa procedura dettagliata usa come esempio un webhook di app per le funzioni di Azure molto semplice.</span><span class="sxs-lookup"><span data-stu-id="c305d-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="c305d-123">*Scelta consigliata*: completare la [Procedura dettagliata: Integrare scambi di attestazioni API REST nei percorsi utente di Azure AD B2C come convalida dell'input utente](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="c305d-123">*Recommended*: Complete the [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="c305d-124">Passaggio 1: Preparare la funzione API REST</span><span class="sxs-lookup"><span data-stu-id="c305d-124">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="c305d-125">La configurazione delle funzioni API REST non rientra nell'ambito di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c305d-125">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="c305d-126">[Funzioni di Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) offre un eccellente toolkit per creare servizi RESTful nel cloud.</span><span class="sxs-lookup"><span data-stu-id="c305d-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="c305d-127">È stata configurata una funzione di Azure che riceve un'attestazione denominata `email` e quindi restituisce l'attestazione `city` con il valore assegnato di `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="c305d-127">We have set up an Azure function that receives a claim called `email`, and then returns the claim `city` with the assigned value of `Redmond`.</span></span> <span data-ttu-id="c305d-128">La funzione di Azure di esempio è disponibile in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="c305d-128">The sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="c305d-129">L'attestazione `userMessage` restituita dalla funzione di Azure è facoltativa in questo contesto e verrà ignorata dal framework dell'esperienza di gestione delle identità.</span><span class="sxs-lookup"><span data-stu-id="c305d-129">The `userMessage` claim that the Azure function returns is optional in this context, and the IEF will ignore it.</span></span> <span data-ttu-id="c305d-130">Può essere usata come messaggio passato all'applicazione e presentata all'utente in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="c305d-130">You can potentially use it as a message passed to the application and presented to the user later.</span></span>

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

<span data-ttu-id="c305d-131">Un'app per le funzioni di Azure semplifica il recupero dell'URL della funzione, che include l'identificatore della funzione specifica.</span><span class="sxs-lookup"><span data-stu-id="c305d-131">An Azure function app makes it easy to get the function URL, which includes the identifier of the specific function.</span></span> <span data-ttu-id="c305d-132">In questo caso l'URL è: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="c305d-132">In this case, the URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="c305d-133">È possibile usarlo per il test.</span><span class="sxs-lookup"><span data-stu-id="c305d-133">You can use it for testing.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="c305d-134">Passaggio 2: Configurare lo scambio di attestazioni API RESTful come profilo tecnico nel file TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="c305d-134">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="c305d-135">Un profilo tecnico è la configurazione completa dello scambio desiderato con il servizio RESTful.</span><span class="sxs-lookup"><span data-stu-id="c305d-135">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="c305d-136">Aprire il file TrustFrameworkExtensions.xml e aggiungere il frammento XML seguente all'interno dell'elemento `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="c305d-136">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="c305d-137">Nell'XML seguente il provider RESTful `Version=1.0.0.0` viene descritto come il protocollo.</span><span class="sxs-lookup"><span data-stu-id="c305d-137">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="c305d-138">Considerarlo come la funzione che interagirà con il servizio esterno.</span><span class="sxs-lookup"><span data-stu-id="c305d-138">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="c305d-139">L'elemento `<InputClaims>` definisce le attestazioni che verranno inviate dal framework dell'esperienza di gestione delle identità al servizio REST.</span><span class="sxs-lookup"><span data-stu-id="c305d-139">The `<InputClaims>` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="c305d-140">In questo esempio il contenuto dell'attestazione `givenName` verrà inviato al servizio REST come attestazione `email`.</span><span class="sxs-lookup"><span data-stu-id="c305d-140">In this example, the contents of the claim `givenName` will be sent to the REST service as the claim `email`.</span></span>  

<span data-ttu-id="c305d-141">L'elemento `<OutputClaims>` definisce le attestazioni che il framework dell'esperienza di gestione delle identità deve ricevere dal servizio REST.</span><span class="sxs-lookup"><span data-stu-id="c305d-141">The `<OutputClaims>` element defines the claims that the IEF will expect from the REST service.</span></span> <span data-ttu-id="c305d-142">Indipendentemente dal numero di attestazioni ricevute, il framework dell'esperienza di gestione delle identità usa soltanto le attestazioni qui indicate.</span><span class="sxs-lookup"><span data-stu-id="c305d-142">Regardless of the number of claims that are received, the IEF will use only those identified here.</span></span> <span data-ttu-id="c305d-143">In questo esempio viene eseguito il mapping dell'attestazione ricevuta come `city` a un'attestazione del framework dell'esperienza di gestione delle identità denominata `city`.</span><span class="sxs-lookup"><span data-stu-id="c305d-143">In this example, a claim received as `city` will be mapped to an IEF claim called `city`.</span></span>

## <a name="step-3-add-the-new-claim-city-to-the-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="c305d-144">Passaggio 3: Aggiungere la nuova attestazione `city` allo schema del file TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="c305d-144">Step 3: Add the new claim `city` to the schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="c305d-145">L'attestazione `city` non è ancora definita nello schema.</span><span class="sxs-lookup"><span data-stu-id="c305d-145">The claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="c305d-146">In tal caso, aggiungere una definizione all'interno dell'elemento `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="c305d-146">So, add a definition inside the element `<BuildingBlocks>`.</span></span> <span data-ttu-id="c305d-147">È possibile trovare questo elemento all'inizio del file TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="c305d-147">You can find this element at the beginning of the TrustFrameworkExtensions.xml file.</span></span>

```XML
<BuildingBlocks>
    <!--The claimtype city must be added to the TrustFrameworkPolicy-->
    <!-- You can add new claims in the BASE file Section III, or in the extensions file-->
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

## <a name="step-4-include-the-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="c305d-148">Passaggio 4: Includere lo scambio di attestazioni del servizio REST come passaggio di orchestrazione nel percorso utente di modifica del profilo nel file TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="c305d-148">Step 4: Include the REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="c305d-149">Aggiungere un passaggio al percorso utente di modifica del profilo, dopo che l'utente è stato autenticato (passaggi di orchestrazione da 1 a 4 riportati nel seguente XML) e che ha specificato le informazioni sul profilo aggiornato (passaggio 5).</span><span class="sxs-lookup"><span data-stu-id="c305d-149">Add a step to the profile edit user journey, after the user has been authenticated (orchestration steps 1-4 in the following XML) and the user has provided the updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="c305d-150">In molti casi d'uso la chiamata all'API REST può essere usata come passaggio di orchestrazione.</span><span class="sxs-lookup"><span data-stu-id="c305d-150">There are many use cases where the REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="c305d-151">Come passaggio di orchestrazione, può essere usata come aggiornamento a un sistema esterno dopo che un utente ha completato un'attività, come una prima registrazione o un aggiornamento del profilo per sincronizzare le informazioni.</span><span class="sxs-lookup"><span data-stu-id="c305d-151">As an orchestration step, it can be used as an update to an external system after a user has successfully completed a task like first-time registration, or as a profile update to keep information synchronized.</span></span> <span data-ttu-id="c305d-152">In questo caso viene usata per incrementare le informazioni fornite all'applicazione dopo la modifica del profilo.</span><span class="sxs-lookup"><span data-stu-id="c305d-152">In this case, it's used to augment the information provided to the application after the profile edit.</span></span>

<span data-ttu-id="c305d-153">Copiare il codice XML del percorso utente di modifica del profilo dal file TrustFrameworkBase.xml al file TrustFrameworkExtensions.xml all'interno dell'elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="c305d-153">Copy the profile edit user journey XML code from the TrustFrameworkBase.xml file to your TrustFrameworkExtensions.xml file inside the `<UserJourneys>` element.</span></span> <span data-ttu-id="c305d-154">Eseguire quindi la modifica indicata nel passaggio 6.</span><span class="sxs-lookup"><span data-stu-id="c305d-154">Then make the modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="c305d-155">Se l'ordine non corrisponde alla versione usata, assicurarsi di inserire il codice come passaggio prima del `ClaimsExchange`tipo`SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="c305d-155">If the order does not match your version, make sure that you insert the code as the step before the `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="c305d-156">Il codice XML finale per il percorso utente dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c305d-156">The final XML for the user journey should look like this:</span></span>

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
        <!-- Add a step 6 to the user journey before the JWT token is created-->
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

## <a name="step-5-add-the-claim-city-to-your-relying-party-policy-file-so-the-claim-is-sent-to-your-application"></a><span data-ttu-id="c305d-157">Passaggio 5: Aggiungere l'attestazione `city` al file dei criteri relying party in modo che l'attestazione venga inviata all'applicazione</span><span class="sxs-lookup"><span data-stu-id="c305d-157">Step 5: Add the claim `city` to your relying party policy file so the claim is sent to your application</span></span>

<span data-ttu-id="c305d-158">Modificare il file relying party (RP) ProfileEdit.xml e l'elemento `<TechnicalProfile Id="PolicyProfile">` per aggiungere quanto segue: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="c305d-158">Edit your ProfileEdit.xml relying party (RP) file and modify the `<TechnicalProfile Id="PolicyProfile">` element to add the following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="c305d-159">Dopo aver aggiunto la nuova attestazione, il profilo tecnico avrà un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c305d-159">After you add the new claim, the technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="c305d-160">Passaggio 6: Caricare le modifiche ed eseguire un test</span><span class="sxs-lookup"><span data-stu-id="c305d-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="c305d-161">Sovrascrivere le versioni esistenti dei criteri.</span><span class="sxs-lookup"><span data-stu-id="c305d-161">Overwrite the existing versions of the policy.</span></span>

1.  <span data-ttu-id="c305d-162">(Facoltativo) Salvare, scaricandola, la versione esistente del file delle estensioni prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="c305d-162">(Optional:) Save the existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="c305d-163">Per tenere bassa la complessità iniziale, evitare di caricare più versioni del file delle estensioni.</span><span class="sxs-lookup"><span data-stu-id="c305d-163">To keep the initial complexity low, we recommend that you do not upload multiple versions of the extensions file.</span></span>
2.  <span data-ttu-id="c305d-164">(Facoltativo) Rinominare la nuova versione dell'ID dei criteri del file di modifica dei criteri modificando...`PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="c305d-164">(Optional:) Rename the new version of the policy ID for the policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="c305d-165">Caricare il file delle estensioni.</span><span class="sxs-lookup"><span data-stu-id="c305d-165">Upload the extensions file.</span></span>
4.  <span data-ttu-id="c305d-166">Caricare il file RP di modifica dei criteri.</span><span class="sxs-lookup"><span data-stu-id="c305d-166">Upload the policy edit RP file.</span></span>
5.  <span data-ttu-id="c305d-167">Usare **Esegui adesso** per testare i criteri.</span><span class="sxs-lookup"><span data-stu-id="c305d-167">Use **Run Now** to test the policy.</span></span> <span data-ttu-id="c305d-168">Esaminare il token restituito dal framework dell'esperienza di gestione delle identità all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c305d-168">Review the token that the IEF returns to the application.</span></span>

<span data-ttu-id="c305d-169">Se tutte le impostazioni sono corrette, il token include la nuova attestazione `city`, con il valore `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="c305d-169">If everything is set up correctly, the token will include the new claim `city`, with the value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c305d-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c305d-170">Next steps</span></span>

[<span data-ttu-id="c305d-171">Usare un'API REST come passaggio di convalida</span><span class="sxs-lookup"><span data-stu-id="c305d-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="c305d-172">Cambiare la modifica del profilo per raccogliere altre informazioni dagli utenti</span><span class="sxs-lookup"><span data-stu-id="c305d-172">Modify the profile edit to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
