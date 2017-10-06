---
title: 'Esercitazione: Integrazione di Azure Active Directory con NetSuite | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Netsuite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a>Esercitazione: Configurazione di Netsuite per il provisioning utenti automatico

obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in Netsuite e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooNetsuite.

## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory.
*   Sottoscrizione di Netsuite abilitata per l'accesso Single Sign-On.
*   Account utente in Netsuite con autorizzazioni di amministratore di team.

## <a name="assigning-users-toonetsuite"></a>L'assegnazione di utenti tooNetsuite

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, vengono sincronizzati solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD.

Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour Netsuite app. Una volta deciso, è possibile assegnare queste app di Netsuite tooyour utenti seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a>Suggerimenti importanti per l'assegnazione di utenti tooNetsuite

*   È consigliabile che un singolo utente AD Azure viene assegnato hello tootest tooNetsuite configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

*   Quando si assegna un tooNetsuite utente, è necessario selezionare un ruolo utente valido. ruolo di "accesso predefinita" Hello non funziona per il provisioning.

## <a name="enable-user-provisioning"></a>Abilitare il provisioning utenti

Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooNetsuite il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in Netsuite in base all'assegnazione di utenti e gruppi in Azure AD.

> [!TIP] 
> È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Netsuite, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure provisioning dell'account utente:

obiettivo di Hello di questa sezione è toooutline tooenable provisioning utente dell'utente di Active Directory come account di tooNetsuite.

1. In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

2. Se è già stato configurato Netsuite per single sign-on, eseguire la ricerca per l'istanza di tramite il campo di ricerca hello Netsuite. In caso contrario, selezionare **Aggiungi** e cercare **Netsuite** nella raccolta di applicazione hello. Selezionare Netsuite dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

3. Selezionare l'istanza di Netsuite, quindi selezionare hello **Provisioning** scheda.

4. Set hello **modalità di Provisioning** troppo**automatica**. 

    ![provisioning](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. In hello **credenziali di amministratore** sezione, fornire hello le impostazioni di configurazione seguente:
   
    a. In hello **nome utente amministratore** casella di testo, digitare un Netsuite nome account cui ha hello **amministratore di sistema** profilo in Netsuite.com assegnato.
   
    b. In hello **Password amministratore** casella di testo, digitare la password hello per questo account.
      
6. Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour Netsuite app.

7. In hello **notifica tramite posta elettronica** immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning e casella di controllo hello.

8. Fare clic su **Salva**.

9. Nella sezione mapping hello, selezionare **tooNetsuite sincronizzare Active Directory gli utenti di Azure.**

10. In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooNetsuite di Azure AD. Si noti che gli attributi selezionati come hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in Netsuite per operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

11. tooenable hello servizio provisioning di Azure AD per Netsuite, hello modifica **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello

12. Fare clic su **Salva**.

Avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooNetsuite in hello gli utenti e gruppi. Si noti che la sincronizzazione iniziale hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite dal servizio nella tua app Netsuite hello.

È ora possibile creare un account di test. Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooNetsuite.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configurare l'accesso Single Sign-On](active-directory-saas-netsuite-tutorial.md)