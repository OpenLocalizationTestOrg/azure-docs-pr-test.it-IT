---
title: 'Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Salesforce Sandbox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 06ff50050845383a602b0edd6fca953ddd37cebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a>Esercitazione: Configurazione di Salesforce Sandbox per il provisioning utenti automatico

obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in Salesforce Sandbox e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooSalesforce Sandbox.

## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory.
*   È necessario disporre di un tenant valido per Salesforce Sandbox for Work o Salesforce Sandbox for Education. È possibile usare un account della versione di valutazione gratuita per entrambi i servizi.
*   Account utente in Salesforce Sandbox con autorizzazioni di amministratore di team.

## <a name="assigning-users-toosalesforce-sandbox"></a>L'assegnazione di utenti tooSalesforce Sandbox

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, vengono sincronizzati solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD.

Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano utenti hello bisogno di accesso tooyour app Salesforce Sandbox. Una volta deciso, è possibile assegnare questi tooyour utenti Salesforce Sandbox app seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce-sandbox"></a>Suggerimenti importanti per l'assegnazione di utenti tooSalesforce Sandbox

* È consigliabile che un singolo utente AD Azure viene assegnato hello tootest Sandbox di tooSalesforce configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

* Quando si assegna un tooSalesforce utente Sandbox, è necessario selezionare un ruolo utente valido. ruolo di "accesso predefinita" Hello non funziona per il provisioning.

> [!NOTE]
> Questa app Importa ruoli personalizzati da Salesforce Sandbox come parte del processo, il cliente che hello opportuno tooselect assegnare gli utenti di provisioning hello.

## <a name="enable-automated-user-provisioning"></a>Abilitare il provisioning utenti automatizzato

In questa sezione viene illustrata la connessione API di provisioning dell'account utente del Sandbox tooSalesforce il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare l'utente assegnato account in Salesforce Sandbox in base a utenti e gruppi assegnazione di Azure AD.

>[!Tip]
>È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Salesforce Sandbox, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure account il provisioning utente automatico:

obiettivo di Hello di questa sezione è toooutline tooenable provisioning utente dell'utente di Active Directory come account di tooSalesforce Sandbox.

1. In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

2. Se è già stato configurato Salesforce Sandbox per single sign-on, eseguire la ricerca per l'istanza di Salesforce Sandbox utilizzando il campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **Salesforce Sandbox** nella raccolta di applicazione hello. Selezionare Salesforce Sandbox dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

3. Selezionare l'istanza di Salesforce Sandbox, quindi selezionare hello **Provisioning** scheda.

4. Set hello **modalità di Provisioning** troppo**automatica**. 
    ![provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)

5. In hello **credenziali di amministratore** sezione, fornire hello le impostazioni di configurazione seguente:
   
    a. In hello **nome utente amministratore** casella di testo, tipo di un ambiente Salesforce Sandbox nome account a cui è hello **amministratore di sistema** profilo in Salesforce.com assegnato.
   
    b. In hello **Password amministratore** casella di testo, digitare la password hello per questo account.

6. tooget il token di sicurezza di Salesforce Sandbox, aprire una nuova scheda e accedere a hello stesso account di amministratore Salesforce Sandbox. Fare clic sul nome, hello angolo superiore destro della pagina hello e quindi fare clic su **impostazioni personali**.

     ![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")
7. Nel riquadro di spostamento a sinistra di hello, fare clic su **personale** tooexpand hello sezione correlata e quindi fare clic su **Reimposta Token di sicurezza personale**.
  
    ![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")
8. In hello **Reimposta Token di sicurezza personale** pagina, fare clic su hello **Reimposta Token di sicurezza** pulsante.

    ![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")
9. Controllare hello posta in arrivo associata all'account di amministratore. Cercare un messaggio di posta elettronica da Salesforce Sandbox.com che contiene il nuovo token di sicurezza hello.
10. Hello tooyour di token, vedere la finestra di Azure AD copiare e incollare il codice in hello **Socket Token** campo.

11. Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour app Salesforce Sandbox.

12. In hello **notifica tramite posta elettronica** immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning e casella di controllo hello.

13. Fare clic su **Salva**.  
    
14.  Nella sezione mapping hello, selezionare **tooSalesforce sincronizzare Active Directory gli utenti di Azure Sandbox.**

15. In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da Azure AD tooSalesforce Sandbox. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in Salesforce Sandbox per le operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

16. tooenable hello servizio provisioning di Azure AD per Salesforce Sandbox, hello modifica **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello

17. Fare clic su **Salva**.


Avviare la sincronizzazione iniziale di hello di tutti gli utenti e/o gruppi assegnati tooSalesforce Sandbox nella sezione utenti e gruppi di hello. la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio App Salesforce Sandbox.

È ora possibile creare un account di test. Attendere che i minuti too20 tooverify che hello account è stato sincronizzato toosalesforce.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configurare l'accesso Single Sign-On](active-directory-saas-salesforcesandbox-tutorial.md)