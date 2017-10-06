---
title: 'Esercitazione: Integrazione di Azure Active Directory con Jive | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Jive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a>Esercitazione: Configurazione di Jive per il provisioning utenti

obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in Jive e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooJive.

## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory.
*   Una sottoscrizione di Jive abilitata per l'accesso Single Sign-On.
*   Un account utente in Jive con autorizzazioni di amministratore di team.

## <a name="assigning-users-toojive"></a>L'assegnazione di utenti tooJive

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.

Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano utenti hello bisogno di accesso dell'applicazione Jive tooyour. Una volta deciso, è possibile assegnare queste app di Jive tooyour utenti seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a>Suggerimenti importanti per l'assegnazione di utenti tooJive

*   È consigliabile che un singolo utente di Azure AD assegnare tooJive tootest hello configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

*   Quando si assegna un tooJive utente, è necessario selezionare un ruolo utente valido. ruolo di "accesso predefinita" Hello non funziona per il provisioning.

## <a name="enable-user-provisioning"></a>Abilitare il provisioning utenti

Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooJive il Azure AD e configura provisioning servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in Jive in base all'assegnazione di utenti e gruppi in Azure AD.

> [!TIP]
> È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Jive, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure provisioning dell'account utente:

obiettivo di Hello di questa sezione è toooutline tooenable provisioning utente dell'utente di Active Directory come account di tooJive.
Come parte di questa procedura, è necessario tooprovide un token di sicurezza utente è necessario toorequest a Jive.com.

1. In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

2. Se è già stato configurato Jive per single sign-on, eseguire la ricerca per l'istanza di tramite il campo di ricerca hello Jive. In caso contrario, selezionare **Aggiungi** e cercare **Jive** nella raccolta di applicazione hello. Selezionare Jive dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

3. Selezionare l'istanza di Jive, quindi selezionare hello **Provisioning** scheda.

4. Set hello **modalità di Provisioning** troppo**automatica**. 

    ![provisioning](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. In hello **credenziali di amministratore** sezione, fornire hello le impostazioni di configurazione seguente:
   
    a. In hello **nome utente amministratore Jive** casella di testo, digitare un Jive nome account cui ha hello **amministratore di sistema** profilo assegnato in Jive.com.
   
    b. In hello **Password amministratore Jive** casella di testo, digitare la password hello per questo account.
   
    c. In hello **URL Tenant Jive** casella di testo, digitare l'URL tenant Jive hello.
      
      > [!NOTE]
      > URL tenant Jive di Hello è utilizzato da toolog l'organizzazione in tooJive.  
      > URL di hello include in genere hello seguente formato: **www.\< organizzazione\>. jive.com**.          

6. Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour Jive app.

7. Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello riportato di seguito.

8. Fare clic su **Salva**.

9. Nella sezione mapping hello, selezionare **tooJive sincronizzare Active Directory gli utenti di Azure.**

10. In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooJive di Azure AD. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in Jive per operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

11. tooenable hello servizio provisioning di Azure AD per Jive, hello modifica **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello

12. Fare clic su **Salva**.

Avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooJive in hello gli utenti e gruppi. la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio nella tua app Jive.

È ora possibile creare un account di test. Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooJive.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configurare l'accesso Single Sign-On](active-directory-saas-jive-tutorial.md)