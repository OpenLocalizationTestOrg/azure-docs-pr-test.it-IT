---
title: Application Insights tootroubleshoot criteri personalizzati - Azure AD B2C | Documenti Microsoft
description: come toosetup Application Insights tootrace hello esecuzione di criteri personalizzati
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
ms.openlocfilehash: c02d7178512c7f9e022385371c3effd4f8cb7726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="23ae0-103">Azure Active Directory B2C: raccolta di log</span><span class="sxs-lookup"><span data-stu-id="23ae0-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="23ae0-104">Questo articolo illustra i passaggi per la raccolta di log da Azure AD B2C in modo che sia possibile diagnosticare con criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="23ae0-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="23ae0-105">Attualmente, hello log dettagliato di attività qui descritte sono progettati **solo** tooaid nello sviluppo di criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="23ae0-105">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="23ae0-106">Non usare la modalità di sviluppo in fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="23ae0-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="23ae0-107">Registri di raccolgono tutte le attestazioni inviate tooand dai provider di identità hello durante lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="23ae0-107">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="23ae0-108">Se utilizzata in produzione, sviluppatore hello assume la responsabilità di informazioni personali (privatamente informazioni personali) raccolta nel log di App Insights hello cui sono proprietari.</span><span class="sxs-lookup"><span data-stu-id="23ae0-108">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="23ae0-109">Questi log dettagliati vengono raccolti solo quando i criteri di hello viene inserito in **modalità di sviluppo**.</span><span class="sxs-lookup"><span data-stu-id="23ae0-109">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="23ae0-110">Usare Application Insights</span><span class="sxs-lookup"><span data-stu-id="23ae0-110">Use Application Insights</span></span>

<span data-ttu-id="23ae0-111">Azure Active Directory B2C supporta una funzionalità per l'invio di dati tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="23ae0-111">Azure AD B2C supports a feature for sending data tooApplication Insights.</span></span>  <span data-ttu-id="23ae0-112">Application Insights fornisce un modo toodiagnose eccezioni e visualizzare i problemi di prestazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="23ae0-112">Application Insights provides a way toodiagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="23ae0-113">Configurazione di Application Insights</span><span class="sxs-lookup"><span data-stu-id="23ae0-113">Setup Application Insights</span></span>

1. <span data-ttu-id="23ae0-114">Passare toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="23ae0-114">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="23ae0-115">Verificare di essere nel tenant di hello con la sottoscrizione di Azure (non il tenant di Azure Active Directory B2C).</span><span class="sxs-lookup"><span data-stu-id="23ae0-115">Ensure you are in hello tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="23ae0-116">Fare clic su **+ nuovo** nel menu di navigazione a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-116">Click **+ New** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="23ae0-117">Cercare e selezionare **Application Insights** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="23ae0-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="23ae0-118">Completare il modulo hello e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="23ae0-118">Complete hello form and click **Create**.</span></span> <span data-ttu-id="23ae0-119">Selezionare **generale** per hello **tipo di applicazione**.</span><span class="sxs-lookup"><span data-stu-id="23ae0-119">Select **General** for hello **Application Type**.</span></span>
1. <span data-ttu-id="23ae0-120">Dopo aver creata la risorsa hello, aprire la risorsa di Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-120">Once hello resource has been created, open hello Application Insights resource.</span></span>
1. <span data-ttu-id="23ae0-121">Trovare **proprietà** in hello menu a sinistra e fare clic su di esso.</span><span class="sxs-lookup"><span data-stu-id="23ae0-121">Find **Properties** in hello left-menu, and click on it.</span></span>
1. <span data-ttu-id="23ae0-122">Hello copia **chiave di strumentazione** e salvarla per la sezione successiva di hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-122">Copy hello **Instrumentation Key** and save it for hello next section.</span></span>

### <a name="set-up-hello-custom-policy"></a><span data-ttu-id="23ae0-123">Impostare i criteri personalizzati di hello</span><span class="sxs-lookup"><span data-stu-id="23ae0-123">Set up hello custom policy</span></span>

1. <span data-ttu-id="23ae0-124">Aprire il file RP hello (ad esempio, SignUpOrSignin.xml).</span><span class="sxs-lookup"><span data-stu-id="23ae0-124">Open hello RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="23ae0-125">Aggiungere i seguenti attributi toohello hello `<TrustFrameworkPolicy>` elemento:</span><span class="sxs-lookup"><span data-stu-id="23ae0-125">Add hello following attributes toohello `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="23ae0-126">Se non esiste già, aggiungere un nodo figlio `<UserJourneyBehaviors>` toohello `<RelyingParty>` nodo.</span><span class="sxs-lookup"><span data-stu-id="23ae0-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` toohello `<RelyingParty>` node.</span></span> <span data-ttu-id="23ae0-127">Deve essere posizionato immediatamente dopo hello`<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="23ae0-127">It must be located immediately after hello `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="23ae0-128">Aggiungere hello successivo nodo come figlio di hello `<UserJourneyBehaviors>` elemento.</span><span class="sxs-lookup"><span data-stu-id="23ae0-128">Add hello following node as a child of hello `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="23ae0-129">Verificare che tooreplace `{Your Application Insights Key}` con hello **chiave di strumentazione** ottenuta da Application Insights nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-129">Make sure tooreplace `{Your Application Insights Key}` with hello **Instrumentation Key** that you obtained from Application Insights in hello previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="23ae0-130">`DeveloperMode="true"`indica i dati di telemetria di ApplicationInsights tooexpedite hello tramite pipeline di elaborazione hello, buono per lo sviluppo, ma vincolato in volumi elevati.</span><span class="sxs-lookup"><span data-stu-id="23ae0-130">`DeveloperMode="true"` tells ApplicationInsights tooexpedite hello telemetry through hello processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="23ae0-131">`ClientEnabled="true"`Invia uno script di hello ApplicationInsights lato client per la registrazione di errori di visualizzazione e sul lato client di pagina (non necessari).</span><span class="sxs-lookup"><span data-stu-id="23ae0-131">`ClientEnabled="true"` sends hello ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="23ae0-132">`ServerEnabled="true"`Invia hello esistente UserJourneyRecorder JSON come tooApplication un evento personalizzato Insights.</span><span class="sxs-lookup"><span data-stu-id="23ae0-132">`ServerEnabled="true"` sends hello existing UserJourneyRecorder JSON as a custom event tooApplication Insights.</span></span>
<span data-ttu-id="23ae0-133">Esempio:</span><span class="sxs-lookup"><span data-stu-id="23ae0-133">Sample:</span></span>

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

3. <span data-ttu-id="23ae0-134">Caricare i criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="23ae0-134">Upload hello policy.</span></span>

### <a name="see-hello-logs-in-application-insights"></a><span data-ttu-id="23ae0-135">Vedere hello registra in Application Insights</span><span class="sxs-lookup"><span data-stu-id="23ae0-135">See hello logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="23ae0-136">I log di Application Insights possono essere visualizzati dopo un breve ritardo (meno di cinque minuti).</span><span class="sxs-lookup"><span data-stu-id="23ae0-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="23ae0-137">Aprire una risorsa di Application Insights hello creati in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="23ae0-137">Open hello Application Insights resource that you created in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="23ae0-138">In hello **Panoramica** menu, fare clic su **Analitica**.</span><span class="sxs-lookup"><span data-stu-id="23ae0-138">In hello **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="23ae0-139">Aprire una nuova scheda in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="23ae0-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="23ae0-140">Ecco un elenco di query che è possibile utilizzare i registri di hello toosee</span><span class="sxs-lookup"><span data-stu-id="23ae0-140">Here is a list of queries you can use toosee hello logs</span></span>

| <span data-ttu-id="23ae0-141">Query</span><span class="sxs-lookup"><span data-stu-id="23ae0-141">Query</span></span> | <span data-ttu-id="23ae0-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="23ae0-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="23ae0-143">traces</span><span class="sxs-lookup"><span data-stu-id="23ae0-143">traces</span></span> | <span data-ttu-id="23ae0-144">Visualizzare tutti i log di hello generati da Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="23ae0-144">See all of hello logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="23ae0-145">traces \\</span><span class="sxs-lookup"><span data-stu-id="23ae0-145">traces \\</span></span>| <span data-ttu-id="23ae0-146">where timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="23ae0-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="23ae0-147">Vedere tutti i log di hello generati da Azure AD B2C per hello ultimo giorno</span><span class="sxs-lookup"><span data-stu-id="23ae0-147">See all of hello logs generated by Azure AD B2C for hello last day</span></span>

<span data-ttu-id="23ae0-148">le voci di Hello potrebbero essere lunghi.</span><span class="sxs-lookup"><span data-stu-id="23ae0-148">hello entries may be long.</span></span>  <span data-ttu-id="23ae0-149">Esportare tooCSV per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="23ae0-149">Export tooCSV for a closer look.</span></span>

<span data-ttu-id="23ae0-150">Sono disponibili ulteriori informazioni sullo strumento Analitica hello [qui](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="23ae0-150">You can learn more about hello Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="23ae0-151">community di Hello ha sviluppato una sviluppatori di identità utente viaggio Visualizzatore toohelp.</span><span class="sxs-lookup"><span data-stu-id="23ae0-151">hello community has developed a user journey viewer toohelp identity developers.</span></span>  <span data-ttu-id="23ae0-152">Non è supportato da Microsoft ed reso disponibile esclusivamente così com'è.</span><span class="sxs-lookup"><span data-stu-id="23ae0-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="23ae0-153">Legge l'istanza di Application Insights e fornisce una visualizzazione well-struttura di eventi di viaggio hello utente.</span><span class="sxs-lookup"><span data-stu-id="23ae0-153">It reads from your Application Insights instance and provides a well-structure view of hello user journey events.</span></span>  <span data-ttu-id="23ae0-154">Ottenere il codice sorgente hello e distribuirlo nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="23ae0-154">You obtain hello source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="23ae0-155">Attualmente, hello log dettagliato di attività qui descritte sono progettati **solo** tooaid nello sviluppo di criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="23ae0-155">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="23ae0-156">Non usare la modalità di sviluppo in fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="23ae0-156">Do not use development mode in production.</span></span>  <span data-ttu-id="23ae0-157">Registri di raccolgono tutte le attestazioni inviate tooand dai provider di identità hello durante lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="23ae0-157">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="23ae0-158">Se utilizzata in produzione, sviluppatore hello assume la responsabilità di informazioni personali (privatamente informazioni personali) raccolta nel log di App Insights hello cui sono proprietari.</span><span class="sxs-lookup"><span data-stu-id="23ae0-158">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="23ae0-159">Questi log dettagliati vengono raccolti solo quando i criteri di hello viene inserito in **modalità di sviluppo**.</span><span class="sxs-lookup"><span data-stu-id="23ae0-159">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="23ae0-160">Repository GitHub di esempi di criteri personalizzate non supportati e strumenti correlati</span><span class="sxs-lookup"><span data-stu-id="23ae0-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="23ae0-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="23ae0-161">Next Steps</span></span>

<span data-ttu-id="23ae0-162">Esplorare i dati hello toohelp Application Insights è comprendere come hello identità esperienza Framework sottostante B2C funziona toodeliver si verifichi la propria identità.</span><span class="sxs-lookup"><span data-stu-id="23ae0-162">Explore hello data in Application Insights toohelp you understand how hello Identity Experience Framework underlying B2C works toodeliver your own identity experiences.</span></span>
