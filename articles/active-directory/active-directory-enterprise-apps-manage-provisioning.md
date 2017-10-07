---
title: provisioning di gestione per applicazioni aziendali in Azure Active Directory hello aaaUser | Documenti Microsoft
description: Informazioni su come utente toomanage provisioning account per le app aziendali usando hello Azure Active Directory
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.openlocfilehash: a613f844c8f51e04b92e62b488313a78ab85f7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-user-account-provisioning-for-enterprise-apps-in-hello-azure-portal"></a>La gestione per applicazioni aziendali nel portale di Azure hello di provisioning dell'account utente
Questo articolo viene descritto come hello toouse [portale di Azure](https://portal.azure.com) toomanage automatica account di provisioning e deprovisioning per le applicazioni che lo supportano, in particolare quelle che sono stati aggiunti da hello "in primo piano" categoria di Hello [raccolta di applicazioni per Azure Active Directory](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). toolearn ulteriori informazioni su provisioning account automatico degli utenti e il relativo funzionamento, vedere [tooSaaS automatizzare Provisioning e Deprovisioning applicazioni con Azure Active Directory](active-directory-saas-app-provisioning.md).

## <a name="finding-your-apps-in-hello-portal"></a>Ricerca di App nel portale di hello
Tutte le applicazioni che sono configurate per single sign-on in una directory, da un amministratore di directory tramite hello [raccolta di applicazioni per Azure Active Directory](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), possono essere visualizzati e gestiti in hello [il portale di Azure](https://portal.azure.com). applicazioni Hello sono reperibile in hello **più servizi** &gt; **applicazioni aziendali** sezione del portale hello. Le app aziendali sono app distribuite e usate all'interno dell'organizzazione.

![Pannello Applicazioni aziendali][0]

Se si seleziona hello **tutte le applicazioni** collegamento a sinistra di hello Mostra un elenco di tutte le app che sono stati configurati, incluse applicazioni che sono stati aggiunti dalla raccolta hello. Selezione di un'app carica pannello della risorsa hello per l'app, in cui per l'app, è possibile visualizzare i report e una serie di impostazioni può essere gestita.

Le impostazioni di provisioning dell'account utente possono essere gestiti selezionando **Provisioning** a sinistra di hello.

![Pannello Risorsa applicazione][1]

## <a name="provisioning-modes"></a>Modalità di provisioning
Hello **Provisioning** pannello inizia con un **modalità** menu, che indica le modalità di provisioning sono supportate per un'applicazione aziendale e consente loro toobe configurato. Hello le opzioni disponibili includono:

* **Automatico** -questa opzione viene visualizzata se Azure AD supporta provisioning automatico basato su API e/o deprovisioning dell'applicazione di toothis gli account utente. Selezione di questa modalità consente di visualizzare un'interfaccia che consente agli amministratori tramite la configurazione di gestione di utenti dell'applicazione di Azure AD tooconnect toohello API, creare i mapping degli account e i flussi di lavoro che definiscono la modalità del flusso di dati di account utente tra Azure AD e app Hello e servizio di provisioning di gestione hello Azure AD.
* **Manuale** -questa opzione viene visualizzata se Azure AD non supporta il provisioning automatico dell'applicazione di toothis gli account utente. Questa opzione indica che i record di account utente archiviati in un'applicazione hello devono essere gestiti mediante un processo esterno, in base alle hello utente gestione e provisioning funzionalità fornite da tale applicazione (che può includere provisioning JIT SAML).

## <a name="configuring-automatic-user-account-provisioning"></a>Configurazione del provisioning automatico degli account utente
Se si seleziona hello **automatica** opzione consente di visualizzare una schermata in cui è suddivisa nelle quattro sezioni:

### <a name="admin-credentials"></a>Credenziali di amministratore
Si tratta in cui vengono immesse credenziali hello necessarie per l'API di gestione utente dell'applicazione di Azure AD tooconnect toohello. input Hello richiesto varia a seconda dell'applicazione hello. toolearn sui tipi di credenziale hello e i requisiti per applicazioni specifiche, vedere hello [esercitazione di configurazione per l'applicazione specifica](active-directory-saas-app-provisioning.md#list-of-apps-that-support-automated-user-provisioning).

Se si seleziona hello **Test connessione** pulsante consente di credenziali di hello tootest con Azure AD app toohello tooconnect tenta provisioning dell'app usando le credenziali di hello fornito.

### <a name="mappings"></a>Mapping
Si tratta in cui gli amministratori possono visualizzare e modificare il flusso di attributi utente tra Azure AD e l'applicazione di destinazione hello, quando gli account utente sono provisioning o l'aggiornamento.

Esiste un set preconfigurato di mapping tra gli oggetti utente di Azure AD e gli oggetti utente di ogni app SaaS. Alcune app gestiscono altri tipi di oggetti, quali Gruppi o Contatti. Se si seleziona uno di questi mapping nella tabella hello Mostra editor mapping hello toohello destra, in cui possono essere visualizzate e personalizzate.

![Pannello Risorsa applicazione][2]

Le personalizzazioni supportate includono:

* Abilitazione e disabilitazione di mapping per oggetti specifici, ad esempio di oggetto dell'hello utente oggetto toohello SaaS app di Azure AD utente.
* Modifica gli attributi che vengono passati dall'oggetto utente dell'app di Azure AD hello utente oggetto toohello. Per altre informazioni sul mapping degli attributi, vedere [Informazioni sui tipi di mapping degli attributi](active-directory-saas-customizing-attribute-mappings.md#understanding-attribute-mapping-types).
* Applicazione di destinazione hello filtro provisioning azioni eseguite su hello Azure AD. Anziché Azure AD-sincronizzare completamente gli oggetti, è possibile limitare le azioni eseguite hello. Se si seleziona solo **Aggiorna**, ad esempio, Azure AD aggiorna solo gli account utente esistenti in un'applicazione e non crea nuovi account utente. Se si seleziona solo **Crea**, Azure crea solo nuovi account utente, ma non aggiorna gli account utente esistenti. Questa funzionalità consente admins toocreate diversi mapping per account di flussi di lavoro creazione e aggiornamento.

### <a name="settings"></a>Impostazioni
In questa sezione consente toostart admins e hello arresto servizio di provisioning di Azure AD per un'applicazione hello selezionato, nonché provisioning facoltativamente crittografato hello memorizzare nella cache e riavviare il servizio di hello.

Se il provisioning è abilitato per hello prima volta per un'applicazione, attivare il servizio di hello modificando hello **lo stato di Provisioning** troppo**su**. In questo modo tooperform servizio provisioning hello Azure AD una sincronizzazione iniziale, da cui legge utenti hello assegnati hello **utenti e gruppi** sezione applicazione di destinazione hello per le query e quindi esegue il provisioning di hello le azioni definite in Azure AD hello **mapping** sezione. Durante questo processo, hello provisioning del servizio vengono archiviati i dati memorizzati nella cache su quali account utente che gestisce gli account non gestiti all'interno delle applicazioni di destinazione hello che sono stati mai nell'ambito per l'assegnazione non sono interessati da operazioni del deprovisioning. Dopo hello la sincronizzazione iniziale, hello automaticamente il provisioning del servizio si sincronizza gli oggetti utente e gruppo in un intervallo di dieci minuti.

Modifica hello **lo stato di Provisioning** troppo**Off** semplicemente pause hello provisioning del servizio. In questo stato, Azure non creare, aggiornare o rimuovere eventuali oggetti utente o gruppo nell'app hello. Se si modifica hello stato nascosto tooon, hello servizio toopick da dove era stata interrotta.

Se si seleziona hello **cancellare lo stato corrente e riavviare la sincronizzazione** casella di controllo e il salvataggio viene arrestata salve provisioning del servizio, dump dei dati memorizzati nella cache di hello sui quali account Azure AD è la gestione, riavvia i servizi di hello ed esegue hello sincronizzazione iniziale nuovamente. Questa opzione consente di hello toostart admins provisioning processo di distribuzione tramite nuovamente.

### <a name="synchronization-details"></a>Dettagli sincronizzazione
In questa sezione fornisce inoltre dettagli sull'operazione di hello di hello provisioning del servizio, tra cui hello tempi primo e ultimo hello provisioning servizio è stato eseguito da un'applicazione hello e il numero di utenti e gruppi di oggetti gestito.

Vengono forniti i collegamenti toohello **report attività di Provisioning**, che fornisce un log di tutti gli utenti e gruppi creati, aggiornati ed rimosso tra Azure AD e applicazione di destinazione hello e toohello **errore di Provisioning report** che fornisce ulteriori messaggi di errore per l'utente e gruppo di oggetti che toobe non riuscito di lettura, creato, aggiornato o rimosso. 

##<a name="feedback"></a>Commenti e suggerimenti

Speriamo che gli utenti apprezzino Azure AD Tenere feedback hello in arrivo. Inviare commenti e suggerimenti e idee per analisi utilizzo software hello **portale di amministrazione** sezione del nostro [forum sul feedback su](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Si sta entusiasti compilazione curiosi di nuovo ogni giorno e utilizzare tooshape le linee guida e definire cosa creiamo successivamente.


[0]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-blade.PNG
[1]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning.PNG
[2]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning-mapping.PNG
