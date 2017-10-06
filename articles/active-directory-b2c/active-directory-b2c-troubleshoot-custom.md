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
# <a name="azure-active-directory-b2c-collecting-logs"></a>Azure Active Directory B2C: raccolta di log

Questo articolo illustra i passaggi per la raccolta di log da Azure AD B2C in modo che sia possibile diagnosticare con criteri personalizzati.

>[!NOTE]
>Attualmente, hello log dettagliato di attività qui descritte sono progettati **solo** tooaid nello sviluppo di criteri personalizzati. Non usare la modalità di sviluppo in fase di produzione.  Registri di raccolgono tutte le attestazioni inviate tooand dai provider di identità hello durante lo sviluppo.  Se utilizzata in produzione, sviluppatore hello assume la responsabilità di informazioni personali (privatamente informazioni personali) raccolta nel log di App Insights hello cui sono proprietari.  Questi log dettagliati vengono raccolti solo quando i criteri di hello viene inserito in **modalità di sviluppo**.


## <a name="use-application-insights"></a>Usare Application Insights

Azure Active Directory B2C supporta una funzionalità per l'invio di dati tooApplication Insights.  Application Insights fornisce un modo toodiagnose eccezioni e visualizzare i problemi di prestazioni dell'applicazione.

### <a name="setup-application-insights"></a>Configurazione di Application Insights

1. Passare toohello [portale di Azure](https://portal.azure.com). Verificare di essere nel tenant di hello con la sottoscrizione di Azure (non il tenant di Azure Active Directory B2C).
1. Fare clic su **+ nuovo** nel menu di navigazione a sinistra di hello.
1. Cercare e selezionare **Application Insights** e quindi fare clic su **Crea**.
1. Completare il modulo hello e fare clic su **crea**. Selezionare **generale** per hello **tipo di applicazione**.
1. Dopo aver creata la risorsa hello, aprire la risorsa di Application Insights hello.
1. Trovare **proprietà** in hello menu a sinistra e fare clic su di esso.
1. Hello copia **chiave di strumentazione** e salvarla per la sezione successiva di hello.

### <a name="set-up-hello-custom-policy"></a>Impostare i criteri personalizzati di hello

1. Aprire il file RP hello (ad esempio, SignUpOrSignin.xml).
1. Aggiungere i seguenti attributi toohello hello `<TrustFrameworkPolicy>` elemento:

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. Se non esiste già, aggiungere un nodo figlio `<UserJourneyBehaviors>` toohello `<RelyingParty>` nodo. Deve essere posizionato immediatamente dopo hello`<DefaultUserJourney ReferenceId="YourPolicyName" />`
2. Aggiungere hello successivo nodo come figlio di hello `<UserJourneyBehaviors>` elemento. Verificare che tooreplace `{Your Application Insights Key}` con hello **chiave di strumentazione** ottenuta da Application Insights nella sezione precedente hello.

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * `DeveloperMode="true"`indica i dati di telemetria di ApplicationInsights tooexpedite hello tramite pipeline di elaborazione hello, buono per lo sviluppo, ma vincolato in volumi elevati.
  * `ClientEnabled="true"`Invia uno script di hello ApplicationInsights lato client per la registrazione di errori di visualizzazione e sul lato client di pagina (non necessari).
  * `ServerEnabled="true"`Invia hello esistente UserJourneyRecorder JSON come tooApplication un evento personalizzato Insights.
Esempio:

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

3. Caricare i criteri di hello.

### <a name="see-hello-logs-in-application-insights"></a>Vedere hello registra in Application Insights

>[!NOTE]
> I log di Application Insights possono essere visualizzati dopo un breve ritardo (meno di cinque minuti).

1. Aprire una risorsa di Application Insights hello creati in hello [portale di Azure](https://portal.azure.com).
1. In hello **Panoramica** menu, fare clic su **Analitica**.
1. Aprire una nuova scheda in Application Insights.
1. Ecco un elenco di query che è possibile utilizzare i registri di hello toosee

| Query | Descrizione |
|---------------------|--------------------|
traces | Visualizzare tutti i log di hello generati da Azure Active Directory B2C |
traces \| where timestamp > ago(1d) | Vedere tutti i log di hello generati da Azure AD B2C per hello ultimo giorno

le voci di Hello potrebbero essere lunghi.  Esportare tooCSV per informazioni dettagliate.

Sono disponibili ulteriori informazioni sullo strumento Analitica hello [qui](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).

>[!NOTE]
>community di Hello ha sviluppato una sviluppatori di identità utente viaggio Visualizzatore toohelp.  Non è supportato da Microsoft ed reso disponibile esclusivamente così com'è.  Legge l'istanza di Application Insights e fornisce una visualizzazione well-struttura di eventi di viaggio hello utente.  Ottenere il codice sorgente hello e distribuirlo nella soluzione.

>[!NOTE]
>Attualmente, hello log dettagliato di attività qui descritte sono progettati **solo** tooaid nello sviluppo di criteri personalizzati. Non usare la modalità di sviluppo in fase di produzione.  Registri di raccolgono tutte le attestazioni inviate tooand dai provider di identità hello durante lo sviluppo.  Se utilizzata in produzione, sviluppatore hello assume la responsabilità di informazioni personali (privatamente informazioni personali) raccolta nel log di App Insights hello cui sono proprietari.  Questi log dettagliati vengono raccolti solo quando i criteri di hello viene inserito in **modalità di sviluppo**.

[Repository GitHub di esempi di criteri personalizzate non supportati e strumenti correlati](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a>Passaggi successivi

Esplorare i dati hello toohelp Application Insights è comprendere come hello identità esperienza Framework sottostante B2C funziona toodeliver si verifichi la propria identità.
