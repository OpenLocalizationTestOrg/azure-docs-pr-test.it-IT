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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="a5884-103">Procedura dettagliata: Integrare scambi di attestazioni API REST nei percorsi utente di Azure AD B2C come passaggio di orchestrazione</span><span class="sxs-lookup"><span data-stu-id="a5884-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="a5884-104">Hello identità esperienza Framework (IEF) sottostante di Azure Active Directory B2C (Azure AD B2C) consente di hello identità developer toointegrate un'interazione con un'API RESTful in viaggio un utente.</span><span class="sxs-lookup"><span data-stu-id="a5884-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="a5884-105">Alla fine di hello di questa procedura dettagliata, si sarà in grado di toocreate un proprio processo utente Azure AD B2C che interagisce con servizi RESTful.</span><span class="sxs-lookup"><span data-stu-id="a5884-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="a5884-106">Hello IEF invia i dati delle attestazioni e riceve i dati nuovamente nelle attestazioni.</span><span class="sxs-lookup"><span data-stu-id="a5884-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="a5884-107">Hello exchange attestazioni API REST:</span><span class="sxs-lookup"><span data-stu-id="a5884-107">hello REST API claims exchange:</span></span>

- <span data-ttu-id="a5884-108">Può essere progettato come passaggio di orchestrazione.</span><span class="sxs-lookup"><span data-stu-id="a5884-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="a5884-109">Può attivare un'azione esterna.</span><span class="sxs-lookup"><span data-stu-id="a5884-109">Can trigger an external action.</span></span> <span data-ttu-id="a5884-110">Può registrare ad esempio un evento in un database esterno.</span><span class="sxs-lookup"><span data-stu-id="a5884-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="a5884-111">Può essere utilizzato toofetch un valore e quindi archiviarla nel database utente hello.</span><span class="sxs-lookup"><span data-stu-id="a5884-111">Can be used toofetch a value and then store it in hello user database.</span></span>

<span data-ttu-id="a5884-112">È possibile utilizzare le attestazioni ricevuta hello successive toochange hello il flusso di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a5884-112">You can use hello received claims later toochange hello flow of execution.</span></span>

<span data-ttu-id="a5884-113">È inoltre possibile progettare l'interazione di hello come un profilo di convalida.</span><span class="sxs-lookup"><span data-stu-id="a5884-113">You can also design hello interaction as a validation profile.</span></span> <span data-ttu-id="a5884-114">Per altre informazioni, vedere [Procedura dettagliata: Integrare scambi di attestazioni API REST nei percorsi utente di Azure AD B2C come convalida dell'input utente](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="a5884-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="a5884-115">scenario di Hello è che quando un utente esegue la modifica di un profilo, si desidera:</span><span class="sxs-lookup"><span data-stu-id="a5884-115">hello scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="a5884-116">Cercare l'utente hello in un sistema esterno.</span><span class="sxs-lookup"><span data-stu-id="a5884-116">Look up hello user in an external system.</span></span>
2. <span data-ttu-id="a5884-117">Ottenere città hello in cui tale utente è registrato.</span><span class="sxs-lookup"><span data-stu-id="a5884-117">Get hello city where that user is registered.</span></span>
3. <span data-ttu-id="a5884-118">Restituisce tale applicazione toohello attributo come attestazione.</span><span class="sxs-lookup"><span data-stu-id="a5884-118">Return that attribute toohello application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5884-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a5884-119">Prerequisites</span></span>

- <span data-ttu-id="a5884-120">Un toocomplete di tenant configurato un account locale sign-configurazione/Accedi, come descritto in Azure Active Directory B2C [Introduzione](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="a5884-120">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="a5884-121">Toointeract un endpoint API REST con.</span><span class="sxs-lookup"><span data-stu-id="a5884-121">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="a5884-122">Questa procedura dettagliata usa come esempio un webhook di app per le funzioni di Azure molto semplice.</span><span class="sxs-lookup"><span data-stu-id="a5884-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="a5884-123">*Consigliato*: hello completo [procedura dettagliata di exchange come passaggio di convalida di attestazioni di API REST](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="a5884-123">*Recommended*: Complete hello [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="a5884-124">Passaggio 1: Preparare la funzione di API REST hello</span><span class="sxs-lookup"><span data-stu-id="a5884-124">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="a5884-125">Il programma di installazione di funzioni API REST è di fuori ambito hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a5884-125">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="a5884-126">[Funzioni di Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) offre un'eccellente toolkit toocreate servizi RESTful nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="a5884-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="a5884-127">È stata configurata una funzione di Azure che riceve un'attestazione chiamata `email`, e quindi restituisce hello attestazione `city` con valore hello assegnato `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="a5884-127">We have set up an Azure function that receives a claim called `email`, and then returns hello claim `city` with hello assigned value of `Redmond`.</span></span> <span data-ttu-id="a5884-128">esempio Hello Azure funzione è nel [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="a5884-128">hello sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="a5884-129">Hello `userMessage` attestazione che hello restituiti da funzioni di Azure è facoltativa in questo contesto e hello IEF verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="a5884-129">hello `userMessage` claim that hello Azure function returns is optional in this context, and hello IEF will ignore it.</span></span> <span data-ttu-id="a5884-130">È potenzialmente possibile utilizzarlo come un messaggio passato applicazione toohello e presentati toohello utente in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="a5884-130">You can potentially use it as a message passed toohello application and presented toohello user later.</span></span>

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

<span data-ttu-id="a5884-131">Un'app di funzione Azure rende facile tooget hello funzione URL, che include l'identificatore hello della funzione specifica hello.</span><span class="sxs-lookup"><span data-stu-id="a5884-131">An Azure function app makes it easy tooget hello function URL, which includes hello identifier of hello specific function.</span></span> <span data-ttu-id="a5884-132">In questo caso, hello URL è: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="a5884-132">In this case, hello URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="a5884-133">È possibile usarlo per il test.</span><span class="sxs-lookup"><span data-stu-id="a5884-133">You can use it for testing.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="a5884-134">Passaggio 2: Configurare hello API RESTful attestazioni exchange come profilo tecnico nel file TrustFrameworExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="a5884-134">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="a5884-135">Un profilo tecnico è configurazione completa di hello di exchange hello desiderato con hello servizio RESTful.</span><span class="sxs-lookup"><span data-stu-id="a5884-135">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="a5884-136">Aprire il file TrustFrameworkExtensions.xml hello e aggiungere hello seguente frammento di codice XML all'interno di hello `<ClaimsProvider>` elemento.</span><span class="sxs-lookup"><span data-stu-id="a5884-136">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="a5884-137">Nel seguente codice XML, provider RESTful hello `Version=1.0.0.0` viene descritto come protocollo di hello.</span><span class="sxs-lookup"><span data-stu-id="a5884-137">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="a5884-138">Viene considerata come funzione hello che interagirà con il servizio esterno hello.</span><span class="sxs-lookup"><span data-stu-id="a5884-138">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="a5884-139">Hello `<InputClaims>` elemento definisce le attestazioni hello che verranno inviate dal servizio REST di toohello IEF hello.</span><span class="sxs-lookup"><span data-stu-id="a5884-139">hello `<InputClaims>` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="a5884-140">In questo esempio, i contenuti dell'attestazione hello hello `givenName` verranno inviati servizio REST toohello come attestazione hello `email`.</span><span class="sxs-lookup"><span data-stu-id="a5884-140">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as hello claim `email`.</span></span>  

<span data-ttu-id="a5884-141">Hello `<OutputClaims>` elemento definisce le attestazioni hello che hello IEF previsti dal servizio REST hello.</span><span class="sxs-lookup"><span data-stu-id="a5884-141">hello `<OutputClaims>` element defines hello claims that hello IEF will expect from hello REST service.</span></span> <span data-ttu-id="a5884-142">Indipendentemente dal numero di hello di attestazioni che vengono ricevuti, hello IEF utilizzerà solo quelli individuati qui.</span><span class="sxs-lookup"><span data-stu-id="a5884-142">Regardless of hello number of claims that are received, hello IEF will use only those identified here.</span></span> <span data-ttu-id="a5884-143">In questo esempio, un'attestazione ricevuta come `city` verrà chiamato tooan mappato IEF attestazione `city`.</span><span class="sxs-lookup"><span data-stu-id="a5884-143">In this example, a claim received as `city` will be mapped tooan IEF claim called `city`.</span></span>

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="a5884-144">Passaggio 3: Aggiungere una nuova attestazione hello `city` toohello schema del file TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="a5884-144">Step 3: Add hello new claim `city` toohello schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="a5884-145">attestazione Hello `city` non è ancora definito in questo schema.</span><span class="sxs-lookup"><span data-stu-id="a5884-145">hello claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="a5884-146">In tal caso, aggiungere una definizione di elemento di hello `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="a5884-146">So, add a definition inside hello element `<BuildingBlocks>`.</span></span> <span data-ttu-id="a5884-147">È possibile trovare questo elemento all'inizio di hello del file TrustFrameworkExtensions.xml hello.</span><span class="sxs-lookup"><span data-stu-id="a5884-147">You can find this element at hello beginning of hello TrustFrameworkExtensions.xml file.</span></span>

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

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="a5884-148">Passaggio 4: Includere scambio attestazioni del servizio REST hello come un passaggio di orchestrazione in percorso profilo utente modifica in TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="a5884-148">Step 4: Include hello REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="a5884-149">Aggiungere un passaggio toohello profilo Modifica utente viaggio, dopo che l'utente hello è stato autenticato (orchestrazione i passaggi 1-4 in hello seguente XML) e l'utente hello ha fornito informazioni sul profilo hello aggiornato (passaggio 5).</span><span class="sxs-lookup"><span data-stu-id="a5884-149">Add a step toohello profile edit user journey, after hello user has been authenticated (orchestration steps 1-4 in hello following XML) and hello user has provided hello updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="a5884-150">Esistono numerosi casi d'uso in hello chiamata all'API REST può essere utilizzato come un passaggio di orchestrazione.</span><span class="sxs-lookup"><span data-stu-id="a5884-150">There are many use cases where hello REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="a5884-151">Come un passaggio di orchestrazione, può essere utilizzato come un sistema esterno tooan di aggiornamento, dopo che un utente ha completato un'attività come prima registrazione, oppure come un profilo di aggiornare informazioni tookeep sincronizzate.</span><span class="sxs-lookup"><span data-stu-id="a5884-151">As an orchestration step, it can be used as an update tooan external system after a user has successfully completed a task like first-time registration, or as a profile update tookeep information synchronized.</span></span> <span data-ttu-id="a5884-152">In questo caso, è utilizzato tooaugment hello indicazioni toohello applicazione dopo la modifica profilo hello.</span><span class="sxs-lookup"><span data-stu-id="a5884-152">In this case, it's used tooaugment hello information provided toohello application after hello profile edit.</span></span>

<span data-ttu-id="a5884-153">Copia hello profilo Modifica codice XML di viaggio utente dal hello TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml file all'interno di hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="a5884-153">Copy hello profile edit user journey XML code from hello TrustFrameworkBase.xml file tooyour TrustFrameworkExtensions.xml file inside hello `<UserJourneys>` element.</span></span> <span data-ttu-id="a5884-154">Apportare la modifica di hello nel passaggio 6.</span><span class="sxs-lookup"><span data-stu-id="a5884-154">Then make hello modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="a5884-155">Se l'ordine di hello non corrisponde alla versione, assicurarsi che sia inserito codice hello come passaggio hello prima hello `ClaimsExchange` tipo `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="a5884-155">If hello order does not match your version, make sure that you insert hello code as hello step before hello `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="a5884-156">XML finale per proprio processo utente hello Hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a5884-156">hello final XML for hello user journey should look like this:</span></span>

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

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a><span data-ttu-id="a5884-157">Passaggio 5: Aggiungere hello attestazione `city` file di criteri di tooyour relying party attestazione hello viene inviato tooyour applicazione</span><span class="sxs-lookup"><span data-stu-id="a5884-157">Step 5: Add hello claim `city` tooyour relying party policy file so hello claim is sent tooyour application</span></span>

<span data-ttu-id="a5884-158">Modificare il file di ProfileEdit.xml relying party (RP) e modificare hello `<TechnicalProfile Id="PolicyProfile">` seguente di hello elemento tooadd: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="a5884-158">Edit your ProfileEdit.xml relying party (RP) file and modify hello `<TechnicalProfile Id="PolicyProfile">` element tooadd hello following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="a5884-159">Dopo aver aggiunto una nuova attestazione hello, profilo tecniche hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a5884-159">After you add hello new claim, hello technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="a5884-160">Passaggio 6: Caricare le modifiche ed eseguire un test</span><span class="sxs-lookup"><span data-stu-id="a5884-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="a5884-161">Sovrascrivi le versioni esistenti di hello del criterio hello.</span><span class="sxs-lookup"><span data-stu-id="a5884-161">Overwrite hello existing versions of hello policy.</span></span>

1.  <span data-ttu-id="a5884-162">(Facoltativo:) Salvare la versione esistente di hello (scaricando) del file con estensioni prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="a5884-162">(Optional:) Save hello existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="a5884-163">tookeep hello iniziale complessità bassa, si consiglia di non caricare più versioni di hello estensioni file.</span><span class="sxs-lookup"><span data-stu-id="a5884-163">tookeep hello initial complexity low, we recommend that you do not upload multiple versions of hello extensions file.</span></span>
2.  <span data-ttu-id="a5884-164">(Facoltativo:) Rinominare una nuova versione di hello di ID criteri hello per file di modifica dei criteri di hello modificando `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="a5884-164">(Optional:) Rename hello new version of hello policy ID for hello policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="a5884-165">Caricare file estensioni hello.</span><span class="sxs-lookup"><span data-stu-id="a5884-165">Upload hello extensions file.</span></span>
4.  <span data-ttu-id="a5884-166">Caricare file RP Modifica criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="a5884-166">Upload hello policy edit RP file.</span></span>
5.  <span data-ttu-id="a5884-167">Utilizzare **Esegui** criteri hello tootest.</span><span class="sxs-lookup"><span data-stu-id="a5884-167">Use **Run Now** tootest hello policy.</span></span> <span data-ttu-id="a5884-168">Token di hello revisione hello IEF restituisce toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="a5884-168">Review hello token that hello IEF returns toohello application.</span></span>

<span data-ttu-id="a5884-169">Se tutto è configurato correttamente, il token hello includerà nuova attestazione hello `city`, con valore hello `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="a5884-169">If everything is set up correctly, hello token will include hello new claim `city`, with hello value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a5884-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a5884-170">Next steps</span></span>

[<span data-ttu-id="a5884-171">Usare un'API REST come passaggio di convalida</span><span class="sxs-lookup"><span data-stu-id="a5884-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="a5884-172">Modificare hello profilo Modifica toogather informazioni aggiuntive agli utenti</span><span class="sxs-lookup"><span data-stu-id="a5884-172">Modify hello profile edit toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
