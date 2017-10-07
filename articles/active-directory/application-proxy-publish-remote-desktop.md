---
title: aaaPublish Desktop remoto con il Proxy di App di Azure AD | Documenti Microsoft
description: Nozioni fondamentali di hello include informazioni sui connettori Proxy di applicazione di Azure AD.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: kgremban
ms.custom: it-pro
ms.reviewer: harshja
ms.openlocfilehash: 1174161d0b5ef1157c334970f00ef4f0702a9545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-remote-desktop-with-azure-ad-application-proxy"></a>Pubblicare Desktop remoto con il proxy applicazione di Azure AD

Questo articolo descrive come toodeploy servizi di Desktop remoto (RDS) con Proxy dell'applicazione in modo che gli utenti remoti possono comunque essere produttivi.

Hello destinati destinatari di questo articolo sono:
- Clienti Proxy dell'applicazione Azure Active Directory correnti che desidera che gli utenti finali di altre applicazioni tootheir toooffer tramite la pubblicazione di applicazioni locali tramite Servizi Desktop remoto.
- Clienti attuali Servizi Desktop remoto che desiderano superficie di attacco hello tooreduce della loro distribuzione usando il Proxy di applicazione AD Azure. Questo scenario fornisce un set limitato di verifica in due passaggi e tooRDS controlla l'accesso condizionale.

## <a name="how-application-proxy-fits-in-hello-standard-rds-deployment"></a>Adattamento Proxy dell'applicazione nella distribuzione di servizi desktop remoto standard hello

Una distribuzione standard di Servizi Desktop remoto include vari servizi ruolo Desktop remoto in esecuzione su Windows Server. Esaminando hello [architettura di Servizi Desktop remoto](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture), sono disponibili più opzioni di distribuzione. la differenza più evidente tra hello Hello [distribuzione di servizi desktop remoto con Proxy dell'applicazione AD Azure](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) (mostrato nel seguente diagramma hello) e hello altre opzioni di distribuzione è lo scenario Proxy dell'applicazione hello è permanente in uscita connessione dal server hello in esecuzione il servizio connettore hello. Altre distribuzioni lasciano le connessioni in ingresso aperte tramite un servizio di bilanciamento del carico.

![Applicazione risiede Proxy tra hello VM RDS e hello rete internet pubblica](./media/application-proxy-publish-remote-desktop/rds-with-app-proxy.png)

In una distribuzione di servizi desktop remoto, ruolo Web desktop remoto hello e ruolo Gateway Desktop remoto hello eseguiti su computer con connessione Internet. Questi endpoint vengono esposte per hello seguenti motivi:
- Web desktop remoto offre utente hello toosign un endpoint pubblico in e visualizzazione hello varie applicazioni locali e i desktop possono accedere. Dopo aver selezionato una risorsa, una connessione RDP viene creata utilizzando l'app nativa hello in hello del sistema operativo.
- Gateway Desktop remoto viene immagine hello dopo che un utente avvia connessione RDP hello. gestisce il traffico RDP crittografato hello transita tramite Internet hello Hello Gateway Desktop remoto e lo converte toohello server locale che hello utente si connette a. In questo scenario, hello traffico hello che Gateway Desktop remoto sta ricevendo proviene da hello Proxy dell'applicazione AD Azure.

>[!TIP]
>Se si non sono stati distribuiti servizi desktop remoto prima di, o altre informazioni prima di iniziare, informazioni su come troppo[distribuire facilmente i servizi desktop remoto con Gestione risorse di Azure e Azure Marketplace](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure).

## <a name="requirements"></a>Requisiti

- Entrambi hello Web desktop remoto e Gateway Desktop remoto gli endpoint devono trovarsi sul hello stesso computer e con una radice comune. Web desktop remoto e Gateway Desktop remoto verrà pubblicato come una singola applicazione in modo da poter un'esperienza single sign-on tra applicazioni hello due.

- Si dovrebbe avere già [distribuito Servizi Desktop remoto](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure) e avere già [abilitato il proxy applicazione](active-directory-application-proxy-enable.md).

- Questo scenario si presuppone che gli utenti finali possono passare tramite Internet Explorer sul desktop di Windows 7 o Windows 10 che si connettono tramite una pagina Web desktop remoto hello. Se è necessario toosupport altri sistemi operativi, vedere [il supporto per le altre configurazioni client](#support-for-other-client-configurations).

  >[!NOTE]
  >Windows 10 Creators Update non è attualmente supportato.

- In Internet Explorer, abilitare il componente aggiuntivo di hello ActiveX di servizi desktop remoto.

## <a name="deploy-hello-joint-rds-and-application-proxy-scenario"></a>Distribuire hello scenario di servizi desktop remoto e Proxy di applicazione comune

Dopo aver configurato i servizi desktop remoto e Proxy di applicazione AD Azure per l'ambiente, seguire hello passaggi toocombine hello due soluzioni. Questa procedura tramite hello due basata sul web di servizi desktop remoto gli endpoint di pubblicazione (Web desktop remoto e Gateway Desktop remoto) come applicazioni e quindi indirizzare il traffico su toogo i servizi desktop remoto tramite il Proxy di applicazione.

### <a name="publish-hello-rd-host-endpoint"></a>Pubblicare l'endpoint dell'host di hello desktop remoto

1. [Pubblicare una nuova applicazione Proxy di applicazione](application-proxy-publish-azure-portal.md) con hello seguenti valori:
   - URL interno: https://\<rdhost\>. com /, dove \<rdhost\> è radice comune hello che condividono Web desktop remoto e Gateway Desktop remoto.
   - URL esterno: Questo campo viene popolato automaticamente in base al nome dell'applicazione hello hello, ma è possibile modificarlo. Entra toothis URL agli utenti quando accedono a RDS.
   - Metodo di autenticazione preliminare: Azure Active Directory
   - Tradurre le intestazioni degli URL: No
2. Assegnare gli utenti toohello pubblicata l'applicazione di desktop remoto. Assicurarsi che tutti abbiano accesso tooRDS, troppo.
3. Lasciare hello metodo single sign-on per un'applicazione hello come **Azure single sign-on AD disabilitato**. Gli utenti vengono richiesto tooauthenticate una volta tooAzure AD e una volta tooRD Web, ma tooRD single sign-on Gateway.
4. Andare troppo**Azure Active Directory** > **registrazioni di App** > *applicazione* > **impostazioni**.
5. Selezionare **proprietà** e aggiornamento hello **URL della Home page** endpoint Web desktop remoto di campo toopoint tooyour (ad esempio https://\<rdhost\>. com/RDWeb).

### <a name="direct-rds-traffic-tooapplication-proxy"></a>Indirizzare il traffico di servizi desktop remoto tooApplication Proxy

Connettere toohello distribuzione di servizi desktop remoto come amministratore e modificare nome hello del server Gateway Desktop remoto per la distribuzione di hello. In questo modo si garantisce che le connessioni attraversano hello Proxy dell'applicazione AD Azure.

1. Connettere il server di servizi desktop remoto toohello esegue il ruolo di Gestore connessione desktop remoto hello.
2. Avviare **Server Manager**.
3. Selezionare **Servizi Desktop remoto** riquadro hello hello sinistra.
4. Selezionare **Panoramica**.
5. Nella sezione Panoramica della distribuzione hello, selezionare il menu di scelta rapida hello e scegliere **modificare le proprietà di distribuzione**.
6. Nella scheda Gateway Desktop remoto hello modificare hello **nome Server** toohello campo URL esterno impostato per l'endpoint dell'host hello desktop remoto nel Proxy dell'applicazione.
7. Hello modifica **accesso metodo** campo troppo**l'autenticazione di Password**.

  ![Schermata Proprietà di distribuzione in Servizi Desktop remoto](./media/application-proxy-publish-remote-desktop/rds-deployment-properties.png)

8. Per ogni raccolta, eseguire hello comando seguente. Sostituire *\<yourcollectionname\>* e *\<proxyfrontendurl\>* con le proprie informazioni. Questo comando abilita l'accesso Single Sign-On tra Web Desktop remoto e Gateway Desktop remoto e ottimizza le prestazioni:

   ```
   Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s:<proxyfrontendurl>`nrequire pre-authentication:i:1"
   ```

   **Ad esempio:**
   ```
   Set-RDSessionCollectionConfiguration -CollectionName "QuickSessionCollection" -CustomRdpProperty "pre-authentication server address:s:https://gateway.contoso.msappproxy.net/`nrequire pre-authentication:i:1"
   ```

9. modifica di hello tooverify di proprietà RDP personalizzate hello, nonché visualizzare hello RDP contenuto del file che verrà scaricati da RDWeb per questa raccolta, eseguire hello comando seguente:
    ```
    (get-wmiobject -Namespace root\cimv2\terminalservices -Class Win32_RDCentralPublishedRemoteDesktop).RDPFileContents
    ```

Dopo aver configurato Desktop remoto, i Proxy dell'applicazione Azure AD ha assunto come componente di hello con connessione internet di RDS. È possibile rimuovere hello altri endpoint con connessione internet pubblici in computer Web desktop remoto e Gateway Desktop remoto.

## <a name="test-hello-scenario"></a>Scenario di test di hello

Scenario di hello con Internet Explorer in un Windows 7 o 10 computer di test.

1. Visitare toohello URL esterno è impostare oppure individuare l'applicazione in hello [MyApps pannello](https://myapps.microsoft.com).
2. Verrà chiesto tooauthenticate tooAzure Active Directory. Utilizzare un account assegnato toohello applicazione.
3. Verrà chiesto tooauthenticate tooRD Web.
4. Una volta completato l'autenticazione di servizi desktop remoto, è possibile selezionare desktop hello o l'applicazione desiderata e iniziare a lavorare.

## <a name="support-for-other-client-configurations"></a>Supportare altre configurazione client

configurazione di Hello descritta in questo articolo è per gli utenti in Windows 7 o 10, con Internet Explorer e componente aggiuntivo di hello ActiveX di servizi desktop remoto. Se necessario è possibile comunque supportare altri sistemi operativi o browser. Hello differenza sta nel metodo di autenticazione hello in uso.

| Metodo di autenticazione | Configurazione client supportata |
| --------------------- | ------------------------------ |
| Pre-autenticazione    | Windows 7/10 con Internet Explorer + componente aggiuntivo ActiveX di Servizi Desktop remoto |
| Pass-through | Qualsiasi altro sistema operativo che supporta un'applicazione hello Desktop remoto Microsoft |

flusso di preautenticazione Hello offre ulteriori vantaggi di sicurezza di flusso di hello pass-through. Con la pre-autenticazione è possibile sfruttare le funzionalità di autenticazione di Azure AD, ad esempio Single Sign-On, accesso condizionale e verifica in due passaggi per le risorse locali. È anche possibile garantire che solo il traffico autenticato raggiunga la rete.

autenticazione pass-through toouse, vi sono solo due modifiche toohello passaggi elencati in questo articolo:
1. In [pubblicare endpoint dell'host di desktop remoto hello](#publish-the-rd-host-endpoint) passaggio 1, Imposta metodo di preautenticazione hello troppo**pass-through**.
2. In [tooApplication Proxy il traffico diretto RDS](#direct-rds-traffic-to-application-proxy), ignorare il passaggio 8 completamente.

## <a name="next-steps"></a>Passaggi successivi

[Abilitare accesso remoto tooSharePoint con Proxy dell'applicazione Azure AD](application-proxy-enable-remote-access-sharepoint.md)  
[Considerazioni relative alla sicurezza quando si accede alle app in remoto usando il proxy applicazione di Azure AD](application-proxy-security-considerations.md)
