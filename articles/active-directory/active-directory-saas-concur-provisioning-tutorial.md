---
title: 'Esercitazione: Integrazione di Azure Active Directory con Concur | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Concur.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a>Esercitazione: Configurazione di Concur per il provisioning utenti

obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in Concur e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooConcur.

## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory.
*   Sottoscrizione di Concur abilitata per l'accesso Single Sign-On.
*   Account utente in Concur con autorizzazioni di amministratore di team.

## <a name="assigning-users-tooconcur"></a>L'assegnazione di utenti tooConcur

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.

Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour Concur app. Una volta deciso, è possibile assegnare queste app di Concur tooyour utenti seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a>Suggerimenti importanti per l'assegnazione di utenti tooConcur

*   È consigliabile che un singolo utente di Azure AD assegnare tooConcur tootest hello configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

*   Quando si assegna un tooConcur utente, è necessario selezionare un ruolo utente valido. ruolo di "accesso predefinita" Hello non funziona per il provisioning.

## <a name="enable-user-provisioning"></a>Abilitare il provisioning utenti

Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooConcur il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in Concur in base all'assegnazione di utenti e gruppi in Azure AD.

> [!Tip] 
> È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Concur, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure provisioning dell'account utente:

obiettivo di Hello di questa sezione è toooutline tooenable provisioning dell'utente di Active Directory come account di tooConcur.

App tooenable in hello servizio Expense, è toobe corretta configurazione e l'utilizzo di un profilo di amministratore del servizio Web. Non aggiungere hello amministratore ruolo tooyour profilo amministratore esistente utilizzato per le funzioni amministrative di T & E.

I consulenti concur o amministratore client hello è necessario creare un profilo di amministratore del servizio Web distinti e messaggio per l'amministratore Client debba usare questo profilo per le funzioni hello amministratore dei servizi Web (ad esempio, l'abilitazione di App). Questi profili devono essere mantenuti separati dal profilo amministratore T & E giornaliero dell'amministratore di hello client (hello T & profilo di amministratore E non deve hello assegnato il ruolo).

Quando si crea hello profilo toobe utilizzato per l'abilitazione di app hello, immettere il nome dell'amministratore di hello client nei campi di profilo utente hello. Ciò consente di assegnare il profilo toohello proprietà. Dopo aver creato uno o più profili, i client di hello dovrà accedere con questo hello tooclick profilo "*abilitare*" pulsante per un'App Partner nel menu Web Services hello.

Per i seguenti motivi di hello, questa azione non deve essere eseguita con il profilo di hello usato per la normale amministrazione T & E.

* Hello client ha toobe hello che fa clic su "*Sì*" nella finestra di dialogo hello visualizzata dopo l'abilitazione di un'app. Fare clic su Invia un acknowledgement client hello viene disposto per hello Partner applicazione tooaccess i propri dati, pertanto si o hello Partner non è possibile fare clic su che pulsante Sì.

* Se un amministratore client che ha abilitato un'app usando hello T & profilo di amministratore E lascia la società hello (risultante nel profilo hello viene disattivato), tutte le app abilitate tramite tale profilo non funzionare fino a quando l'applicazione hello è abilitata con un altro amministratore active profilo. È per questo motivo che si suppone toocreate distinct amministratore profili.

* Se un amministratore lascia la società hello, profilo di amministratore può essere amministratore di sostituzione toohello modificato se si desidera senza conseguenze hello abilitato app perché tale profilo non è necessario disattivata toohello hello associata.

**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**

1. Accesso tooyour **Concur** tenant.

2. Da hello **amministrazione** dal menu **servizi Web**.
   
    ![Tenant Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Tenant Concur")

3. Sul lato sinistro, da hello hello **servizi Web** riquadro, selezionare **Abilita applicazione Partner**.
   
    ![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")

4. Da hello **Abilita applicazione** elenco, selezionare **Azure Active Directory**, quindi fare clic su **abilitare**.
   
    ![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")

5. Fare clic su **Sì** tooclose hello **conferma azione** finestra di dialogo.
   
    ![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")

6. In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

7. Se è già stato configurato Concur per single sign-on, eseguire la ricerca per l'istanza di Concur utilizzando il campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **Concur** nella raccolta di applicazione hello. Selezionare Concur dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

8. Selezionare l'istanza di Concur, quindi selezionare hello **Provisioning** scheda.

9. Set hello **modalità di Provisioning** troppo**automatica**. 
 
    ![provisioning](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. In hello **credenziali di amministratore** immettere hello **nome utente** hello e **password** dell'amministratore di Concur.

11. Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour Concur app. Se hello connessione non riesce, verificare che l'account di Concur disponga delle autorizzazioni di amministratore di Team.

12. Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello.

13. Fare clic su **Salva**.

14. Nella sezione mapping hello, selezionare **tooConcur sincronizzare Active Directory gli utenti di Azure.**

15. In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooConcur di Azure AD. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello account utente in Concur per operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

16. tooenable hello servizio provisioning di Azure AD per Concur, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione

17. Fare clic su **Salva**.

È ora possibile creare un account di test. Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooConcur.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configurare l'accesso Single Sign-On](active-directory-saas-concur-tutorial.md)

