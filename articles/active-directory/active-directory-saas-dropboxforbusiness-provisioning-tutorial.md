---
title: 'Esercitazione: Integrazione di Azure Active Directory con Dropbox for Business | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Dropbox for Business.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a>Esercitazione: Configurazione di Dropbox for Business per il provisioning utenti automatico

obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in Dropbox per Business e Azure AD tooautomatically effettuare il provisioning e il de-provisioning degli account utente da Azure AD tooDropbox for Business.

## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory.
*   Sottoscrizione di Dropbox for Business abilitata per l'accesso Single Sign-On.
*   Account utente in Dropbox for Business con autorizzazioni di amministratore di team.

## <a name="assigning-users-toodropbox-for-business"></a>L'assegnazione di utenti tooDropbox for Business

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.

Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano utenti hello bisogno di accesso tooyour Dropbox per app di Business. Una volta deciso, è possibile assegnare questi tooyour utenti Dropbox App Business seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a>Suggerimenti importanti per l'assegnazione di utenti tooDropbox for Business

*   È consigliabile che un singolo utente AD Azure viene assegnato tooDropbox per hello tootest Business configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

*   Quando si assegna un tooDropbox utente per le aziende, è necessario selezionare un ruolo utente valido. ruolo di "accesso predefinita" Hello non funziona per il provisioning...

## <a name="enable-automated-user-provisioning"></a>Abilitare il provisioning utenti automatizzato

In questa sezione viene illustrata la connessione del tooDropbox di Azure AD per l'API di provisioning dell'account utente di Business e hello provisioning toocreate servizio di configurazione, aggiornare e disabilitare gli account utente assegnato in Dropbox for Business in base a utenti e gruppi assegnazione di Azure AD.

>[!Tip]
>È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Dropbox for Business, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure account il provisioning utente automatico:

1. In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

2. Se è già stato configurato Dropbox for Business per single sign-on, eseguire la ricerca per l'istanza di Dropbox for Business utilizzando il campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **Dropbox for Business** nella raccolta di applicazione hello. Selezionare Dropbox for Business dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

3. Selezionare l'istanza di Dropbox for Business, quindi selezionare hello **Provisioning** scheda.

4. Set hello **modalità di Provisioning** troppo**automatica**. 

    ![provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. In hello **credenziali di amministratore** fare clic su **Authorize**. Viene aperta una finestra di dialogo di accesso di Dropbox for Business in una nuova finestra del browser.

6. In hello **Accedi tooDropbox toolink con Azure AD** finestra di dialogo di accesso tooyour Dropbox per il tenant di Business.

     ![Provisioning degli utenti](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Provisioning degli utenti")

7. Confermare che si desidera toogive Azure Active Directory autorizzazione toomake modifiche tooyour Dropbox per il tenant di Business. Fare clic su **Consenti**.
    
      ![Provisioning degli utenti](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Provisioning degli utenti")

8. Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour Dropbox per app di Business. Se hello connessione non riesce, assicurarsi di Dropbox per conto di Business con autorizzazioni di amministratore di Team e provare a hello **"Autorizza"** esegue nuovamente l'istruzione.

9. Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello.

10. Fare clic su **Salva**.

11. Nella sezione mapping hello, selezionare **tooDropbox sincronizzare Active Directory gli utenti di Azure per le aziende.**

12. In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da Azure AD tooDropbox for Business. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello account utente in Dropbox for Business per le operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

13. tooenable hello servizio provisioning di Azure AD per Dropbox for Business, hello modifica **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello

14. Fare clic su **Salva**.

Avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooDropbox for Business in hello gli utenti e gruppi. la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio in Dropbox per app di Business.

È ora possibile creare un account di test. Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooDropbox for Business.

Un ciclo di provisioning utenti completato correttamente è indicato da uno stato correlato.

![Assegnare utenti](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assegnare utenti")


## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configurare l'accesso Single Sign-On](active-directory-saas-dropboxforbusiness-tutorial.md)