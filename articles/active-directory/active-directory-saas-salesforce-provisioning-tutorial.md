---
title: 'Esercitazione: Integrazione di Azure Active Directory con Salesforce | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Salesforce.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a916be8dbf0b4c6173cda873936a53cd1f3ff12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a>Esercitazione: Configurazione di Salesforce per il provisioning utenti automatico

obiettivo di Hello di questa esercitazione è tooshow tooperform necessari passaggi hello in Salesforce e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooSalesforce.

## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory.
*   È necessario disporre di un tenant valido per Salesforce for Work o Salesforce for Education. È possibile usare un account della versione di valutazione gratuita per entrambi i servizi.
*   Account utente in Salesforce con autorizzazioni di amministratore di team.

## <a name="assigning-users-toosalesforce"></a>L'assegnazione di utenti tooSalesforce

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.

Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour Salesforce app. Una volta deciso, è possibile assegnare queste app di Salesforce tooyour utenti seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce"></a>Suggerimenti importanti per l'assegnazione di utenti tooSalesforce

*   È consigliabile che un singolo utente AD Azure viene assegnato hello tootest tooSalesforce configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

*  Quando si assegna un tooSalesforce utente, è necessario selezionare un ruolo utente valido. ruolo di "accesso predefinita" Hello non funziona per il provisioning

    > [!NOTE]
    > Questa app Importa ruoli personalizzati da Salesforce come parte del processo, il cliente che hello opportuno tooselect assegnare gli utenti di provisioning hello

## <a name="enable-automated-user-provisioning"></a>Abilitare il provisioning utenti automatizzato

Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooSalesforce il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in Salesforce in base all'assegnazione di utenti e gruppi in Azure AD .

>[!Tip]
>È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Salesforce, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure account il provisioning utente automatico:

obiettivo di Hello di questa sezione è toooutline tooenable provisioning utente dell'utente di Active Directory come account di tooSalesforce.

1. In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

2. Se è già stato configurato Salesforce per single sign-on, eseguire la ricerca per l'istanza di Salesforce utilizzando il campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **Salesforce** nella raccolta di applicazione hello. Selezionare Salesforce dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

3. Selezionare l'istanza di Salesforce, quindi selezionare hello **Provisioning** scheda.

4. Set hello **modalità di Provisioning** troppo**automatica**. 
![provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)

5. In hello **credenziali di amministratore** sezione, fornire hello le impostazioni di configurazione seguente:
   
    a. In hello **nome utente amministratore** digitare un nome che è hello account Salesforce **amministratore di sistema** profilo in Salesforce.com assegnato.
   
    b. In hello **Password amministratore** casella di testo, digitare la password hello per questo account.

6. tooget il token di sicurezza di Salesforce, aprire una nuova scheda e accedere a hello stesso account di amministratore di Salesforce. Fare clic sul nome, hello angolo superiore destro della pagina hello e quindi fare clic su **impostazioni personali**.

     ![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")
7. Nel riquadro di spostamento a sinistra di hello, fare clic su **personale** tooexpand hello sezione correlata e quindi fare clic su **Reimposta Token di sicurezza personale**.
  
    ![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")
8. In hello **Reimposta Token di sicurezza personale** pagina, fare clic su **Reimposta Token di sicurezza** pulsante.

    ![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")
9. Controllare hello posta in arrivo associata all'account di amministratore. Cercare un messaggio di posta elettronica da Salesforce.com che contiene il nuovo token di sicurezza hello.
10. Hello tooyour di token, vedere la finestra di Azure AD copiare e incollare il codice in hello **Socket Token** campo.

11. Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour Salesforce app.

12. In hello **notifica tramite posta elettronica** immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning e casella di controllo hello riportato di seguito.

13. Fare clic su **Salva**.  
    
14.  Nella sezione mapping hello, selezionare **tooSalesforce sincronizzare Active Directory gli utenti di Azure.**

15. In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooSalesforce di Azure AD. Si noti che gli attributi selezionati come hello **corrispondenza** proprietà sono utilizzate toomatch hello account utente in Salesforce per operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

16. tooenable hello servizio provisioning di Azure AD per Salesforce, hello modifica **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello

17. Fare clic su **Salva**.

Verrà avviata la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooSalesforce in hello gli utenti e gruppi. Si noti che la sincronizzazione iniziale hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio nella tua app di Salesforce.

È ora possibile creare un account di test. Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooSalesforce.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configurare l'accesso Single Sign-On](active-directory-saas-salesforce-tutorial.md)