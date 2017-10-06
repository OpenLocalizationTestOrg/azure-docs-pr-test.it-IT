---
title: 'Esercitazione: Integrazione di Azure Active Directory con Citrix GoToMeeting | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Citrix GoToMeeting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a>Esercitazione: Configurazione di Citrix GoToMeeting per il provisioning utenti automatico

obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in Citrix GoToMeeting e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooCitrix GoToMeeting.

## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory.
*   Una sottoscrizione di Citrix GoToMeeting abilitata per l'accesso Single Sign-On.
*   Un account utente in Citrix GoToMeeting con autorizzazioni di amministratore di team.

## <a name="assigning-users-toocitrix-gotomeeting"></a>L'assegnazione di utenti tooCitrix GoToMeeting

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.

Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano utenti hello bisogno di accesso tooyour app Citrix GoToMeeting. Una volta deciso, è possibile assegnare questi tooyour utenti Citrix GoToMeeting app seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a>Suggerimenti importanti per l'assegnazione di utenti tooCitrix GoToMeeting

*   È consigliabile che un singolo utente AD Azure viene assegnato tooCitrix GoToMeeting tootest hello configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

*   Quando si assegna un tooCitrix utente GoToMeeting, è necessario selezionare un ruolo utente valido. ruolo di "accesso predefinita" Hello non funziona per il provisioning.

## <a name="enable-automated-user-provisioning"></a>Abilitare il provisioning utenti automatizzato

In questa sezione viene illustrata la connessione API di provisioning dell'account utente del GoToMeeting tooCitrix il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare l'utente assegnato conti in Citrix GoToMeeting basati su utenti e gruppi assegnazione di Azure AD.

> [!TIP]
> È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Citrix GoToMeeting, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure account il provisioning utente automatico:

1. In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

2. Se è già stato configurato Citrix GoToMeeting per single sign-on, eseguire la ricerca per l'istanza di Citrix GoToMeeting con il campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **Citrix GoToMeeting** nella raccolta di applicazione hello. Selezionare Citrix GoToMeeting dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

3. Selezionare l'istanza di Citrix GoToMeeting e quindi hello **Provisioning** scheda.

4. Set hello **Provisioning** modalità troppo**automatica**. 

    ![provisioning](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. In hello sezione credenziali di amministratore, eseguire hello alla procedura seguente:
   
    a. In hello **nome di utente amministratore Citrix GoToMeeting** casella di testo, digitare il nome utente hello di un amministratore.

    b. In hello **Password amministratore Citrix GoToMeeting** casella di testo, la password dell'amministratore di hello.

6. Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour app Citrix GoToMeeting. Se hello connessione non riesce, verificare che l'account Citrix GoToMeeting con autorizzazioni di amministratore di Team e provare a hello **"Credenziali di amministratore"** esegue nuovamente l'istruzione.

7. Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello.

8. Fare clic su **Salva**.

9. Nella sezione mapping hello, selezionare **tooCitrix sincronizzare Active Directory gli utenti di Azure GoToMeeting.**

10. In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da Azure AD tooCitrix GoToMeeting. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in Citrix GoToMeeting per operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

11. tooenable hello servizio provisioning di Azure AD per Citrix GoToMeeting, hello modifica **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello

12. Fare clic su **Salva**.

Avviare la sincronizzazione iniziale di hello di tutti gli utenti e/o gruppi assegnati tooCitrix GoToMeeting nella sezione utenti e gruppi di hello. la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio nella tua app di Citrix GoToMeeting.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configurare l'accesso Single Sign-On](active-directory-saas-citrix-gotomeeting-tutorial.md)


