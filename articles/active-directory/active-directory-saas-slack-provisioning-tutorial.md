---
title: 'Esercitazione: Configurazione di Slack per il provisioning utenti automatico con Azure Active Directory | Documentazione Microsoft'
description: Informazioni su come tooconfigure Azure Active Directory tooautomatically il provisioning e il de-provisioning account utente di tooSlack.
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a>Esercitazione: Configurazione di Slack per il provisioning utenti automatico


obiettivo di questa esercitazione Hello è tooshow hello passaggi che è necessario tooperform in Slack e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooSlack. 

## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory
*   Il margine di flessibilità tenant hello [Plus piano](https://aadsyncfabric.slack.com/pricing) o meglio abilitato 
*   Account utente in Slack con autorizzazioni di amministratore di team 

Nota: hello provisioning integrazione di Azure AD si basa su hello [Slack SCIM API](https://api.slack.com/scim) ovvero team tooSlack disponibile sulla hello più piano o migliori.

## <a name="assigning-users-tooslack"></a>L'assegnazione di utenti tooSlack

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatica, verranno sincronizzati solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD. 

Prima di configurare e abilitare hello provisioning del servizio, sarà necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour Slack app. Una volta deciso, è possibile assegnare queste app di Slack tooyour utenti seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a>Suggerimenti importanti per l'assegnazione di utenti tooSlack

*   È consigliabile che un singolo utente di Azure AD assegnare tooSlack tootest hello configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

*   Quando si assegna un tooSlack utente, è necessario selezionare hello **utente** o il ruolo di "Gruppo" nella finestra di dialogo assegnazione hello. ruolo di "accesso predefinita" Hello non funziona per il provisioning.


## <a name="configuring-user-provisioning-tooslack"></a>Configurazione tooSlack di provisioning dell'utente 

Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooSlack il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in Slack in base all'assegnazione di utenti e gruppi in Azure AD.

**Suggerimento:** tooenabled basato su SAML Single Sign-On per Slack, attenendosi alle istruzioni hello cui (portale di Azure) è possibile scegliere [https://portal.azure.com]. L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a>account utente automatico tooconfigure tooSlack il provisioning in Azure AD:


1)  In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

2) Se è già stato configurato il margine di flessibilità per single sign-on, eseguire la ricerca per l'istanza di Slack usando il campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **Slack** nella raccolta di applicazione hello. Selezionare il margine di flessibilità dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

3)  Selezionare l'istanza di un margine di flessibilità, quindi selezionare hello **Provisioning** scheda.

4)  Set hello **modalità di Provisioning** troppo**automatica**.

![Provisioning in Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  In hello **credenziali di amministratore** fare clic su **Authorize**. Verrà aperta una finestra di dialogo di autorizzazione di Slack in una nuova finestra del browser. 

6) Nella nuova finestra hello, accedere a Slack utilizzando l'account amministratore di Team. Nella finestra di dialogo autorizzazione hello risultante selezionare hello Slack team che si desidera tooenable provisioning per e quindi selezionare **Authorize**. Hello toocomplete portale Azure toohello restituito, una volta completato il provisioning di configurazione.

![Finestra di dialogo di autorizzazione](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour Slack app. Se hello connessione non riesce, verificare che l'account Slack disponga delle autorizzazioni di amministratore di Team e provare hello che esegue nuovamente l'istruzione "Autorizza".

8) Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello riportato di seguito.

9) Fare clic su **Salva**. 

10) Nella sezione mapping hello, selezionare **tooSlack sincronizzare Active Directory gli utenti di Azure**.

11) In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che verranno sincronizzati da tooSlack di Azure AD. Si noti che gli attributi selezionati come hello **corrispondenza** proprietà saranno gli account utente hello toomatch utilizzata nel margine di flessibilità per operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

12) tooenable hello servizio provisioning di Azure AD per Slack, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione

13) Fare clic su **Salva**. 

Verrà avviata la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooSlack in hello gli utenti e gruppi. Si noti che la sincronizzazione iniziale hello tooperform più lungo di sincronizzazioni successive, che si verificano ogni 10 minuti circa, purché hello servizio è in esecuzione. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite dal servizio nella tua app Slack hello.

## <a name="optional-configuring-group-object-provisioning-tooslack"></a>[Facoltativo] Configurazione oggetto gruppo provisioning tooSlack 

Facoltativamente, è possibile abilitare il provisioning degli oggetti di gruppo da Azure AD tooSlack hello. Questo comportamento è diverso da "assegnazione dei gruppi di utenti", in tale oggetto gruppo effettivo di hello inoltre tooits membri verranno replicati dai tooSlack di Azure AD. Se si ha un gruppo denominato "Gruppo personale" in Azure AD, ad esempio, in Slack verrà creato un identico gruppo denominato "Gruppo personale".

### <a name="tooenable-provisioning-of-group-objects"></a>tooenable provisioning degli oggetti di gruppo:

1) Nella sezione mapping hello, selezionare **tooSlack sincronizzare Azure gruppi di Active Directory**.

2) Nel Pannello di mappatura attributi hello, impostare tooYes abilitato.

3) In hello **mapping degli attributi** sezione, verificare hello gruppo attributi che verranno sincronizzati da tooSlack di Azure AD. Si noti che gli attributi selezionati come hello **corrispondenza** proprietà saranno i gruppi di hello toomatch utilizzata nel margine di flessibilità per operazioni di aggiornamento. 

4) Fare clic su **Salva**.

Questo risultato in qualsiasi tooSlack di oggetti assegnati gruppo in hello **utenti e gruppi** sezione completamente sincronizzati da tooSlack di Azure AD. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite dal servizio nella tua app Slack hello.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-enterprise-apps-manage-provisioning.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
