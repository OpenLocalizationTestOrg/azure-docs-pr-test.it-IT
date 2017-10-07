---
title: "Novità di gestione delle applicazioni dell'organizzazione in Azure Active Directory aaa | Documenti Microsoft"
description: "Informazioni sulle novità della gestione delle applicazioni aziendali in Azure Active Directory."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: asteen
ms.reviewer: asteen
ms.openlocfilehash: 7f4b7b11b256f1e910e557f45f3709d762416f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="whats-new-in-enterprise-application-management-in-azure-active-directory"></a>Novità della gestione delle applicazioni aziendali in Azure Active Directory 

Azure Active Directory (Azure AD) è migliorata strumenti di gestione di applicazioni aziendali, con il nuovo toomake di caratteristiche e funzionalità di gestione delle app più semplice ed efficiente.

Ecco alcuni dei miglioramenti hello per Azure AD in hello [portale di Azure](https://portal.azure.com).

- Una raccolta di applicazioni esperienza, con un modello di creazione di applicazioni semplificata e supporto per tutti i tipi di applicazione hello utilizzata per. 
- Esperienza di avvio rapido completamente nuova che consente di creare rapidamente un progetto pilota dell'applicazione. 
- Possibilità di configurare i criteri self-service con pochi clic. 
- Proxy tooapplication miglioramenti, single sign-on, configurazione e portare la propria esperienza di applicazione, consentendo tooget più eseguita rispetto a prima.

## <a name="improvements-toohello-azure-active-directory-application-gallery"></a>Miglioramenti toohello raccolta applicazioni di Azure Active Directory

Aggiungere applicazioni preferite, siano essi da hello [raccolta di applicazioni](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), applicazioni personalizzate si estensione cloud toohello o nuove applicazioni che si sta sviluppando.  È possibile iniziare a usare questa nuova esperienza facendo **Aggiungi** su hello **applicazioni aziendali** panoramica o **tutte le applicazioni** pannelli.
 
  ![Aggiunta di un'applicazione](./media/active-directory-enterprise-apps-whats-new-azure-portal/01.png)

Una volta nella raccolta di hello, verrà visualizzato tutte le applicazioni in primo piano che supportano il provisioning utente anteriore e centrale.  È possibile esplorare tutti i tipi di categorie diverse toodrill in applicazioni hello che è rilevante, o è possibile utilizzare hello ricerca esperienza toorapidly trova hello applicazioni da toointegrate.

  ![raccolta di applicazioni Hello](./media/active-directory-enterprise-apps-whats-new-azure-portal/02.png)

## <a name="add-custom-applications-from-one-place"></a>Aggiungere applicazioni personalizzate da un'unica posizione

Inoltre tooadding pre-integrata applicazioni dalla raccolta di hello, tutte le esperienze di configurazione dell'applicazione personalizzata hello che è stato utilizzato tooin portale di gestione classico hello ora sono possibili nel nuovo portale di hello. Se si estende un'applicazione locale mediante il proxy di applicazione hello, integrare la propria password o l'applicazione SSO federato o creazione di un'applicazione completamente nuova, utilizzo del Registro di sistema dell'applicazione hello, è possibile ottenere tooit da questo un unico sul posto.

  ![Aggiunta di una propria applicazione](./media/active-directory-enterprise-apps-whats-new-azure-portal/03.png)

 
**tooget avviata l'aggiunta di un'applicazione**:

1. Fare clic su hello **aggiungere il propria collegamento** nella parte superiore di hello della raccolta di applicazioni hello. 
2. Verranno visualizzate due opzioni: **Distribuzione di un'applicazione esistente** o **Sviluppo di una nuova applicazione**. Leggere differenza hello toolearn tra le opzioni di hello due e in che modo toouse li.

### <a name="deploying-existing-applications"></a>Distribuzione di applicazioni esistenti

1. Se si dispone di un'applicazione già in esecuzione e si desidera semplicemente toointegrate in Azure AD per single-sign-on o il provisioning, scegliere hello **distribuire un'applicazione esistente** opzione. Scegliere un nome per l'applicazione, quindi fare clic su **Aggiungi**.
2. L'operazione è terminata. Invece che necessitano di tooknow tutti i dettagli sull'applicazione di hello, è possibile ora impostare come nuova applicazione funziona passando tramite i menu a sinistra di hello e configurazione desiderato di tooyour applicazione hello in qualsiasi momento.

  ![Aggiunta di un'applicazione esistente con un clic](./media/active-directory-enterprise-apps-whats-new-azure-portal/04.png)
 
### <a name="developing-new-applications"></a>Sviluppo di nuove applicazioni

1. Se si sviluppa una nuova applicazione, è un modo semplice per è tooget toohello del Registro di sistema dell'applicazione direttamente dalla raccolta hello:
2. Fare clic su hello **aggiungere la propria** opzione dalla raccolta di applicazioni, seleziona hello hello **sviluppare un'applicazione esistente** scelta e verrà visualizzato un collegamento rapido destro toohello applicazione aggiungere esperienza.

  ![Aggiunta di un'applicazione appena sviluppata in pochi clic](./media/active-directory-enterprise-apps-whats-new-azure-portal/05.png)


>[!NOTE]
>Dopo aver aggiunto un'applicazione utilizzando hello del Registro di sistema dell'applicazione, si noterà Mostra fino nell'elenco di hello di applicazioni aziendali in cui sarà in grado di tooconfigure single sign-on e gestire i criteri di accesso per la nuova applicazione.

  ![La gestione di accesso tooyour nuova applicazione con le applicazioni aziendali](./media/active-directory-enterprise-apps-whats-new-azure-portal/06.png)


## <a name="quick-start-get-going-with-your-new-application-right-away"></a>Avvio rapido: iniziare a usare subito la nuova applicazione 

Dopo aver aggiunto un'applicazione, se essere pre-integrata o un'app, abbiamo creato tooget un'esperienza di avvio rapido personalizzata che senza nella nuova esperienza di applicazioni hello rapidamente. Se si segue sistematicamente ogni opzione, verrà illustrata hello dell'interfaccia utente e spiegano come tooget accade al più presto un progetto pilota della nuova applicazione. 
 
  ![le nuove applicazioni Hello quick start esperienza](./media/active-directory-enterprise-apps-whats-new-azure-portal/07.png)

 È possibile visitare questa nuova esperienza di avvio rapido in qualsiasi momento e per qualsiasi applicazione, facendo clic su **introduttiva** dal menu di navigazione a sinistra dell'applicazione hello.


## <a name="updated-application-proxy-configuration"></a>Aggiornamento della configurazione del proxy dell'applicazione
A questo punto, si pronuncia di nuove applicazioni hello è stato aggiunto è in esecuzione nell'ambiente locale e si desidera toointegrate con Azure AD.  Uno dei hello nuove operazioni più interessanti sulla nuova esperienza di configurazione dell'applicazione hello nel portale di nuovo AD Azure hello è che la suddivisione modalità sign-on dell'applicazione hello rispetto alla configurazione del proxy dell'applicazione, è ora possibile facilmente esporre password SSO o federata applicazioni in esecuzione nel cloud toohello destra alla rete aziendale, senza la necessità di più istanze di un'applicazione hello toocreate.

Inoltre toothis, è ora possibile anche configurare le nuove applicazioni hello che aggiunti per l'utilizzo con Proxy dell'applicazione AD Azure hello direttamente dal nuovo portale di hello, incluse le applicazioni che supportano l'autenticazione di Windows nativo cui si verifichi.

  ![Configurazione di un hello toouse applicazione opzione sign-on di autenticazione integrata di Windows](./media/active-directory-enterprise-apps-whats-new-azure-portal/08.png)
 

tooget avviata la configurazione di un'applicazione di autenticazione di Windows native con Proxy dell'applicazione hello:
1. Fare clic sull'elemento di navigazione del servizio Single sign-on hello e scegliere **autenticazione integrata di Windows** dal pannello impostazioni sign-on hello e configurare desiderato di tooyour impostazioni hello.
2. Nella parte superiore di supporto di queste nuove modalità di autenticazione, è ora possibile inoltre caricare certificati dalle applicazioni di toosupport domini personalizzati in esecuzione su un endpoint protetto all'interno dell'organizzazione.  
 
   ![Caricamento di un certificato toobe utilizzato con Proxy dell'applicazione hello](./media/active-directory-enterprise-apps-whats-new-azure-portal/09.png)

3. tooupload un nuovo certificato per l'applicazione locale Preferiti, fare clic su hello **proxy dell'applicazione** opzione dal menu di navigazione a sinistra di hello, fare clic su hello **certificato** selettore e caricare un file di certificato, è possibile utilizzare tooencrypt richieste dall'applicazione tooyour endpoint cloud.

## <a name="advanced-federated-single-sign-on-configuration"></a>Configurazione dell'accesso Single Sign-On federato avanzato

Per utenti che utilizzano applicazioni federate oggi stesso, esistono numerose nuove funzionalità nel Pannello di configurazione basato su SAML sign-on hello. toostart, ora sono completamente personalizzabili, aggiungere, rimuovere e il mapping di attributi utente esistenti hello rilasciati come attestazioni nei token SAML.
 
  ![Personalizzazione degli attributi del token utente SAML hello passato applicazione tooa federata](./media/active-directory-enterprise-apps-whats-new-azure-portal/10.png)


toocheck che out hello federata nuova configurazione di SSO:
1. Aprire un'applicazione federata **accesso single sign-on** pannello da prova spostamento a sinistra menu e assicurarsi che prova '*basato su SAML Sign-on** è selezionata la modalità. 
2. Una volta, abilitare hello casella hello **gli attributi utente** toomodify intestazione tutti gli attributi di hello incluse nel token SAML di hello passato toothat applicazione.

È possibile inoltre creare, rollover e gestire i certificati utilizzati per single sign-on federato, nonché modificare che riceve la notifica quando il certificato su tooexpire. Si noterà che queste opzioni di nuovo in hello **certificati** titolo su hello stesso pannello servizio Single sign-on.
 
  ![Creazione di un nuovo certificato, personalizzazione della notifica e-mail di scadenza e delle opzioni di firma del certificato](./media/active-directory-enterprise-apps-whats-new-azure-portal/11.png)

### <a name="relay-state-paramenter"></a>Parametro Stato dell'inoltro
Infine, abbiamo inoltre esteso set hello dei parametri URL SAML sostegno hello tooinclude **parametro di stato di inoltro**, ovvero pagina hello agli utenti verranno visualizzata all'interno di un'applicazione federata una volta che accedi hello sono stata completata. Ciò si rivela utile impostando tooconfigure se si desidera toosend specifici utenti tooa inserirli all'interno di tooget applicazione hello accade rapidamente.

  ![Se si imposta il parametro di stato di inoltro SAML hello](./media/active-directory-enterprise-apps-whats-new-azure-portal/12.png)
 
**parametro di stato di inoltro hello tooset**:

1. Abilitare hello **Mostra URL impostazioni avanzate** la casella di controllo in hello **dominio e gli URL** titolo su hello single-sign-on Pannello di configurazione. 
2. Una volta fatto questo, verrà visualizzato che un set di nuovo URL di input verranno visualizzate finestre che consentirà tooset questa e altre impostazioni dell'URL di SAML.

## <a name="bring-your-own-password-sso-applications"></a>Applicazioni con Single Sign-On basato su password con funzionalità "Bring Your Own Applications"

Sappiamo che non tutte le applicazioni supporta la federazione subito casella hello. Ad esempio, potrebbe essere una delle nuove applicazioni hello che è stato aggiunto ha una schermata di accesso personalizzata che gli utenti usano un nome utente e password toosign in a. È comunque possibile integrare questi tipi di applicazioni con Azure AD usando la **portare le proprie applicazioni** funzionalità, è ora disponibile per si tooconfigure nel nuovo portale di hello.
 
  ![Integrazione con Azure AD di applicazioni personalizzate con insieme di credenziali delle password](./media/active-directory-enterprise-apps-whats-new-azure-portal/13.png)

**toocheck funzione 'Portare le proprie applicazioni' hello**:

1. Dopo aver impostato hello modalità single sign-on per una nuova applicazione personalizzata aggiunti troppo**basato su Password Sign-on**immettere hello URL in cui un'applicazione hello viene visualizzata la schermata di accesso, quindi scegliere **salvare**.  
2. Una volta tale scopo, si verrà automaticamente cercare come URL per un nome utente e password casella di input e consentono di toouse AD Azure toosecurely trasmettere applicazione toothat le password utilizzando l'estensione browser del Pannello di accesso hello.

## <a name="configure-self-service-application-access"></a>Configurare l'accesso alle applicazioni self-service

Dopo aver aggiunto un numero elevato di nuove applicazioni, potrebbe essere tooallow il toobrowse gli utenti che desideri aggiungere pannelli di accesso personalizzati tootheir tali applicazioni, senza la necessità di toobother è un amministratore. A questo punto, con questa versione più recente, è possibile configurare e gestire l'accesso all'applicazione self-service direttamente dal nuovo portale di hello.

  ![Configurazione dell'accesso alle applicazioni self-service per un'applicazione con Single Sign-On basato su password](./media/active-directory-enterprise-apps-whats-new-azure-portal/14.png)
 
**tooconfigure e gestire l'accesso all'applicazione self-service**:

1. tooget avviato, è possibile selezionare hello **self-service** opzione da un'applicazione hello del menu di navigazione a sinistra e impostare hello **consentire agli utenti dell'applicazione di toothis accesso toorequest?** opzione troppo ' **Sì**'. 
2. Ciò consentirà tooconfigure chi è autorizzato l'applicazione di toothis tooapprove accesso e gli utenti self-service che gruppo verranno aggiunto. Inoltre, se un'applicazione hello è configurata per la password single-sign-on, verrà anche visualizzato un'altra opzione che consente facoltativamente Consenti tali responsabili approvazione toomanage hello password assegnati toohello applicazione.

##<a name="feedback"></a>Commenti e suggerimenti

Ci auguriamo che è simile all'utilizzo di hello migliorata l'esperienza di Azure AD. Tenere feedback hello in arrivo. Inviare commenti e suggerimenti e idee per analisi utilizzo software hello **portale di amministrazione** sezione del nostro [forum sul feedback su](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Si sta entusiasti compilazione curiosi di nuovo ogni giorno e tooshape le linee guida e definire cosa creiamo successivamente.

## <a name="next-steps"></a>Passaggi successivi

Per altri dettagli, vedere [Gestione di applicazioni con Azure Active Directory](active-directory-enable-sso-scenario.md).



