---
title: Application Insights per risolvere i problemi relativi ai criteri personalizzati - Azure AD B2C | Microsoft Docs
description: Informazioni su come configurare Application Insights per tenere traccia dell'esecuzione di criteri personalizzati
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: saeda
ms.openlocfilehash: 8c79df33cd5f04f490e2cc6372f7e8ac1c4d9bbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="a21c4-103">Azure Active Directory B2C: raccolta di log</span><span class="sxs-lookup"><span data-stu-id="a21c4-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="a21c4-104">Questo articolo illustra i passaggi per la raccolta di log da Azure AD B2C in modo che sia possibile diagnosticare con criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a21c4-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="a21c4-105">I log attività dettagliati descritti qui attualmente sono progettati **SOLO** per facilitare lo sviluppo di criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a21c4-105">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="a21c4-106">Non usare la modalità di sviluppo in fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="a21c4-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="a21c4-107">I log raccolgono tutte le attestazioni inviate verso e dai provider di identità durante lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="a21c4-107">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="a21c4-108">Se usato in fase di produzione, lo sviluppatore si assume la responsabilità delle informazioni personali raccolte nel log di App Insights di cui è proprietario.</span><span class="sxs-lookup"><span data-stu-id="a21c4-108">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="a21c4-109">Questi log dettagliati vengono raccolti solo quando il criterio è in **MODALITÀ DI SVILUPPO**.</span><span class="sxs-lookup"><span data-stu-id="a21c4-109">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="a21c4-110">Usare Application Insights</span><span class="sxs-lookup"><span data-stu-id="a21c4-110">Use Application Insights</span></span>

<span data-ttu-id="a21c4-111">Azure Active Directory B2C supporta una funzionalità per l'invio di dati ad Application Insights,</span><span class="sxs-lookup"><span data-stu-id="a21c4-111">Azure AD B2C supports a feature for sending data to Application Insights.</span></span>  <span data-ttu-id="a21c4-112">servizio che consente di diagnosticare le eccezioni e di visualizzare i problemi di prestazioni delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a21c4-112">Application Insights provides a way to diagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="a21c4-113">Configurazione di Application Insights</span><span class="sxs-lookup"><span data-stu-id="a21c4-113">Setup Application Insights</span></span>

1. <span data-ttu-id="a21c4-114">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a21c4-114">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a21c4-115">Verificarsi di trovarsi nel tenant con la propria sottoscrizione di Azure (non il tenant di Azure AD B2C in uso).</span><span class="sxs-lookup"><span data-stu-id="a21c4-115">Ensure you are in the tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="a21c4-116">Fare clic su **+ Nuovo** nel menu di navigazione a sinistra.</span><span class="sxs-lookup"><span data-stu-id="a21c4-116">Click **+ New** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="a21c4-117">Cercare e selezionare **Application Insights** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a21c4-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="a21c4-118">Completare il modulo e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a21c4-118">Complete the form and click **Create**.</span></span> <span data-ttu-id="a21c4-119">Selezionare **Generale** come valore per **Tipo di applicazione**.</span><span class="sxs-lookup"><span data-stu-id="a21c4-119">Select **General** for the **Application Type**.</span></span>
1. <span data-ttu-id="a21c4-120">Dopo aver creato la risorsa, aprire la risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a21c4-120">Once the resource has been created, open the Application Insights resource.</span></span>
1. <span data-ttu-id="a21c4-121">Fare clic su **Proprietà** nel menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="a21c4-121">Find **Properties** in the left-menu, and click on it.</span></span>
1. <span data-ttu-id="a21c4-122">Copiare il valore di **Chiave di strumentazione** e salvarlo per la sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="a21c4-122">Copy the **Instrumentation Key** and save it for the next section.</span></span>

### <a name="set-up-the-custom-policy"></a><span data-ttu-id="a21c4-123">Configurare i criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="a21c4-123">Set up the custom policy</span></span>

1. <span data-ttu-id="a21c4-124">Aprire il file RP, ad esempio SignUpOrSignin.xml.</span><span class="sxs-lookup"><span data-stu-id="a21c4-124">Open the RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="a21c4-125">Aggiungere gli attributi seguenti all'elemento `<TrustFrameworkPolicy>`:</span><span class="sxs-lookup"><span data-stu-id="a21c4-125">Add the following attributes to the `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="a21c4-126">Se non esiste già, aggiungere un nodo figlio `<UserJourneyBehaviors>` al nodo `<RelyingParty>`.</span><span class="sxs-lookup"><span data-stu-id="a21c4-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` to the `<RelyingParty>` node.</span></span> <span data-ttu-id="a21c4-127">Deve trovarsi immediatamente dopo `<DefaultUserJourney ReferenceId="YourPolicyName" />`.</span><span class="sxs-lookup"><span data-stu-id="a21c4-127">It must be located immediately after the `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="a21c4-128">Aggiungere il nodo seguente come figlio dell'elemento `<UserJourneyBehaviors>`.</span><span class="sxs-lookup"><span data-stu-id="a21c4-128">Add the following node as a child of the `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="a21c4-129">Assicurarsi di sostituire `{Your Application Insights Key}` con la **chiave di strumentazione** ottenuta da Application Insights nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="a21c4-129">Make sure to replace `{Your Application Insights Key}` with the **Instrumentation Key** that you obtained from Application Insights in the previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="a21c4-130">`DeveloperMode="true"` indica ad Application Insights di accelerare la telemetria nella pipeline di elaborazione, valida per lo sviluppo, ma vincolata a volumi elevati.</span><span class="sxs-lookup"><span data-stu-id="a21c4-130">`DeveloperMode="true"` tells ApplicationInsights to expedite the telemetry through the processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="a21c4-131">`ClientEnabled="true"` invia lo script di Application Insights lato client per tenere traccia della visualizzazione della pagina e degli errori del client (non necessari).</span><span class="sxs-lookup"><span data-stu-id="a21c4-131">`ClientEnabled="true"` sends the ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="a21c4-132">`ServerEnabled="true"` invia l'elemento JSON UserJourneyRecorder esistente come evento personalizzato ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a21c4-132">`ServerEnabled="true"` sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.</span></span>
<span data-ttu-id="a21c4-133">Esempio:</span><span class="sxs-lookup"><span data-stu-id="a21c4-133">Sample:</span></span>

  ```XML
  <TrustFrameworkPolicy
    ...
    TenantId="fabrikamb2c.onmicrosoft.com"
    PolicyId="SignUpOrSignInWithAAD"
    DeploymentMode="Development"
    UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="YourPolicyName" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
  </TrustFrameworkPolicy>
  ```

3. <span data-ttu-id="a21c4-134">Caricare i criteri.</span><span class="sxs-lookup"><span data-stu-id="a21c4-134">Upload the policy.</span></span>

### <a name="see-the-logs-in-application-insights"></a><span data-ttu-id="a21c4-135">Visualizza i log in Application Insights</span><span class="sxs-lookup"><span data-stu-id="a21c4-135">See the logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="a21c4-136">I log di Application Insights possono essere visualizzati dopo un breve ritardo (meno di cinque minuti).</span><span class="sxs-lookup"><span data-stu-id="a21c4-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="a21c4-137">Aprire la risorsa di Application Insights creata nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a21c4-137">Open the Application Insights resource that you created in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="a21c4-138">Nel menu **Panoramica** fare clic su **Analytics**.</span><span class="sxs-lookup"><span data-stu-id="a21c4-138">In the **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="a21c4-139">Aprire una nuova scheda in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a21c4-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="a21c4-140">Di seguito viene indicato un elenco di query che è possibile usare per visualizzare i log</span><span class="sxs-lookup"><span data-stu-id="a21c4-140">Here is a list of queries you can use to see the logs</span></span>

| <span data-ttu-id="a21c4-141">Query</span><span class="sxs-lookup"><span data-stu-id="a21c4-141">Query</span></span> | <span data-ttu-id="a21c4-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a21c4-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="a21c4-143">traces</span><span class="sxs-lookup"><span data-stu-id="a21c4-143">traces</span></span> | <span data-ttu-id="a21c4-144">Consente di visualizzare tutti i log generati da Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="a21c4-144">See all of the logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="a21c4-145">traces \\</span><span class="sxs-lookup"><span data-stu-id="a21c4-145">traces \\</span></span>| <span data-ttu-id="a21c4-146">where timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="a21c4-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="a21c4-147">Consente di visualizzare tutti i log generati da Azure AD B2C nell'ultimo giorno</span><span class="sxs-lookup"><span data-stu-id="a21c4-147">See all of the logs generated by Azure AD B2C for the last day</span></span>

<span data-ttu-id="a21c4-148">Le voci possono essere lunghe.</span><span class="sxs-lookup"><span data-stu-id="a21c4-148">The entries may be long.</span></span>  <span data-ttu-id="a21c4-149">Per visualizzarle meglio è possibile esportarle in formato CSV.</span><span class="sxs-lookup"><span data-stu-id="a21c4-149">Export to CSV for a closer look.</span></span>

<span data-ttu-id="a21c4-150">Per altre informazioni sullo strumento Analytics, vedere [qui](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="a21c4-150">You can learn more about the Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="a21c4-151">La community ha sviluppato un visualizzatore di percorsi utente per supportare gli sviluppatori di identità.</span><span class="sxs-lookup"><span data-stu-id="a21c4-151">The community has developed a user journey viewer to help identity developers.</span></span>  <span data-ttu-id="a21c4-152">Non è supportato da Microsoft ed reso disponibile esclusivamente così com'è.</span><span class="sxs-lookup"><span data-stu-id="a21c4-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="a21c4-153">Legge l'istanza di Application Insights e restituisce una visualizzazione strutturata degli eventi di percorso utente.</span><span class="sxs-lookup"><span data-stu-id="a21c4-153">It reads from your Application Insights instance and provides a well-structure view of the user journey events.</span></span>  <span data-ttu-id="a21c4-154">Ottenere il codice sorgente e distribuirlo nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="a21c4-154">You obtain the source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="a21c4-155">I log attività dettagliati descritti qui attualmente sono progettati **SOLO** per facilitare lo sviluppo di criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a21c4-155">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="a21c4-156">Non usare la modalità di sviluppo in fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="a21c4-156">Do not use development mode in production.</span></span>  <span data-ttu-id="a21c4-157">I log raccolgono tutte le attestazioni inviate verso e dai provider di identità durante lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="a21c4-157">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="a21c4-158">Se usato in fase di produzione, lo sviluppatore si assume la responsabilità delle informazioni personali raccolte nel log di App Insights di cui è proprietario.</span><span class="sxs-lookup"><span data-stu-id="a21c4-158">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="a21c4-159">Questi log dettagliati vengono raccolti solo quando il criterio è in **MODALITÀ DI SVILUPPO**.</span><span class="sxs-lookup"><span data-stu-id="a21c4-159">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="a21c4-160">Repository GitHub di esempi di criteri personalizzate non supportati e strumenti correlati</span><span class="sxs-lookup"><span data-stu-id="a21c4-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="a21c4-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a21c4-161">Next Steps</span></span>

<span data-ttu-id="a21c4-162">Esplorare i dati in Application Insights per capire il funzionamento di B2C sottostante del framework dell'esperienza di gestione delle identità per distribuire le proprie esperienze di gestione delle identità.</span><span class="sxs-lookup"><span data-stu-id="a21c4-162">Explore the data in Application Insights to help you understand how the Identity Experience Framework underlying B2C works to deliver your own identity experiences.</span></span>
