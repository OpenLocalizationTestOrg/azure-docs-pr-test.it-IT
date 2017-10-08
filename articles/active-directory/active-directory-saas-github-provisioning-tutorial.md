---
title: 'Esercitazione: Configurazione di GitHub per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come tooconfigure Azure Active Directory tooautomatically il provisioning e il de-provisioning account utente di tooGitHub.
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a>Esercitazione: Configurazione di GitHub per il provisioning utenti automatico


obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in GitHub e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooGitHub. 

## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory
*   Un tenant di Github con hello [piano aziendale](https://help.github.com/articles/organization-billing-plans/#business-plan) o meglio abilitato 
*   Account utente in GitHub con autorizzazioni di amministratore 

> [!NOTE]
> Hello provisioning integrazione di Azure AD si basa su hello [GitHub SCIM API](https://developer.github.com/v3/scim/), ovvero i team tooGithub disponibili nel piano aziendale hello o migliori.

## <a name="assigning-users-toogithub"></a>L'assegnazione di utenti tooGitHub

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato. 

Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour GitHub app. Una volta deciso, è possibile assegnare queste app di GitHub tooyour utenti seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a>Suggerimenti importanti per l'assegnazione di utenti tooGitHub

*   È consigliabile che un singolo utente AD Azure viene assegnato hello tootest tooGitHub configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

*   Quando si assegna un tooGitHub utente, è necessario selezionare entrambi hello **utente** ruolo, o un altro valido specifici dell'applicazione, se disponibile, nella finestra di dialogo assegnazione hello. Hello **accesso predefinito** ruolo non funziona per il provisioning e gli utenti vengono ignorati.


## <a name="configuring-user-provisioning-toogithub"></a>Configurazione tooGitHub di provisioning dell'utente 

Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooGitHub il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in GitHub in base all'assegnazione di utenti e gruppi in Azure AD.

> [!TIP]
> È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per GitHub, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a>Configurare l'account utente automatico provisioning tooGitHub in Azure AD


1. In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

2. Se è già stato configurato GitHub per single sign-on, eseguire la ricerca per l'istanza di GitHub usando il campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **GitHub** nella raccolta di applicazione hello. Selezionare GitHub dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

3. Selezionare l'istanza di GitHub, quindi selezionare hello **Provisioning** scheda.

4. Set hello **modalità di Provisioning** troppo**automatica**.

    ![Provisioning di GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. In hello **credenziali di amministratore** fare clic su **Authorize**. Viene aperta una finestra di dialogo di autorizzazione di GitHub in una nuova finestra del browser. 

6. In nuova finestra hello, accedere a GitHub utilizzando l'account amministratore. Nella finestra di dialogo autorizzazione hello risultante selezionare team di GitHub hello che si desidera tooenable provisioning per e quindi selezionare **Authorize**. Hello toocomplete portale Azure toohello restituito, una volta completato il provisioning di configurazione.

    ![Finestra di dialogo di autorizzazione](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. Nel portale di Azure hello, input **URL Tenant** e fare clic su **Test connessione** tooensure Azure AD può connettersi app GitHub tooyour. Se hello connessione non riesce, verificare che l'account GitHub abbia autorizzazioni di amministratore e **URl Tenant** immesso è corretto, quindi provare a hello "Autorizza" esegue nuovamente l'istruzione (è possibile costituiscono **URL Tenant** dalla regola: "https : //api.github.com/scim/v2/organizations/ + < Organizations_name > ", è possibile trovare le organizzazioni con l'account GitHub: **impostazioni** > **organizzazioni**).

    ![Finestra di dialogo di autorizzazione](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e controllo hello casella di controllo "Invia una notifica di posta elettronica quando si verifica un errore".

9. Fare clic su **Salva**. 

10. Nella sezione mapping hello, selezionare **tooGitHub sincronizzare Active Directory gli utenti di Azure**.

11. In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooGitHub di Azure AD. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello account utente in GitHub per operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

12. tooenable hello servizio provisioning di Azure AD per GitHub, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione

13. Fare clic su **Salva**. 

Questa operazione avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooGitHub in hello gli utenti e gruppi. la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio.

Per ulteriori informazioni sulla modalità di registrazione tooread provisioning di hello Azure AD, vedere [creazione di report per il provisioning utente automatico account](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-enterprise-apps-manage-provisioning.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Passaggi successivi

* [Informazioni su modalità di registrazione tooreview e ottengono report sull'attività di provisioning](active-directory-saas-provisioning-reporting.md)
