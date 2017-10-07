---
title: 'Esercitazione: Integrazione di Azure Active Directory con Box | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Box.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e92baabb174642c22c99e2a30bc9c71845b3b75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a>Esercitazione: Configurazione di Box per il provisioning utenti automatico

obiettivo di Hello di questa esercitazione è tooshow hello passaggi tooperform nella casella e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooBox.

## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory.
*   Sottoscrizione di Box abilitata per l'accesso Single Sign-On.
*   Account utente in Box con autorizzazioni di amministratore di team.

## <a name="assigning-users-toobox"></a>L'assegnazione di utenti tooBox 

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.

Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour casella app. Una volta deciso, è possibile assegnare queste app di Box tooyour utenti seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a>Assegnare utenti e gruppi
Hello **casella > utenti e gruppi** scheda nel portale di Azure hello consente toospecify quali utenti e gruppi deve essere concesso accesso tooBox. Assegnazione di un utente o gruppo determina hello toooccur delle operazioni seguenti:

* Azure AD consente tooBox tooauthenticate di hello assegnato utente (tramite un'assegnazione diretta o l'appartenenza al gruppo). Se un utente non è assegnato, Azure AD non consente loro toosign in tooBox e restituisce un errore nella pagina di accesso AD Azure hello.
* Un riquadro dell'app per la casella viene aggiunta dell'utente toohello [avvio applicazione](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).
* Se il provisioning automatico è abilitato, gli utenti assegnato hello e/o i gruppi vengono aggiunti toohello toobe coda automaticamente il provisioning di provisioning.
  
  * Se solo oggetti utente sono stati configurati toobe il provisioning, quindi tutti gli utenti assegnati direttamente nella coda di provisioning hello e tutti gli utenti che sono membri di tutti i gruppi assegnati vengono inseriti nella coda provisioning hello. 
  * Se gli oggetti di gruppo sono stati configurati toobe il provisioning, tutti gli oggetti di gruppo assegnato sono tooBox provisioning e tutti gli utenti che sono membri di tali gruppi. appartenenza al gruppo e utente Hello viene mantenuti durante la scrittura di tooBox.

È possibile utilizzare hello **attributi > Single Sign-On** scheda tooconfigure quali attributi utente (o attestazioni) è presentati tooBox durante l'autenticazione basata su SAML e hello **attributi > Provisioning** scheda tooconfigure come flusso di attributi di utenti e gruppi da Azure AD tooBox durante le operazioni di provisioning.

### <a name="important-tips-for-assigning-users-toobox"></a>Suggerimenti importanti per l'assegnazione di utenti tooBox 

*   È consigliabile che un singolo Azure AD assegnati all'utente tooBox tootest hello configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

*   Quando si assegna un toobox utente, è necessario selezionare un ruolo utente valido. ruolo di "accesso predefinita" Hello non funziona per il provisioning.

## <a name="enable-automated-user-provisioning"></a>Abilitare il provisioning utenti automatizzato

Questa sezione contiene informazioni tramite la connessione API di provisioning dell'account utente del tooBox il Azure AD e configura provisioning servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato nella casella in base all'assegnazione di utenti e gruppi in Azure AD.

Se il provisioning automatico è abilitato, gli utenti assegnato hello e/o i gruppi vengono aggiunti toohello toobe coda automaticamente il provisioning di provisioning.
    
 * Se solo oggetti utente vengono configurati toobe provisioning, quindi, gli utenti assegnati direttamente vengono inseriti nella coda di provisioning hello e tutti gli utenti che sono membri di tutti i gruppi assegnati vengono inseriti nella coda provisioning hello. 
    
 * Se gli oggetti di gruppo sono stati configurati toobe il provisioning, tutti gli oggetti di gruppo assegnato sono tooBox provisioning e tutti gli utenti che sono membri di tali gruppi. appartenenza al gruppo e utente Hello viene mantenuti durante la scrittura di tooBox.

> [!TIP] 
> È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per una casella, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure account il provisioning utente automatico:

obiettivo di Hello di questa sezione è toooutline tooenable provisioning dell'utente di Active Directory come account di tooBox.

1. In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

2. Se Box è già stato configurato per single sign-on, la ricerca per l'istanza di casella utilizzando il campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **casella** nella raccolta di applicazione hello. Selezionare casella dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

3. Selezionare l'istanza di una casella, quindi selezionare hello **Provisioning** scheda.

4. Set hello **modalità di Provisioning** troppo**automatica**. 

    ![provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. In hello **credenziali di amministratore** fare clic su **Authorize** tooopen una finestra di dialogo accesso in una nuova finestra del browser.

6. In hello **tooBox di accesso di account di accesso toogrant** pagina, fornire le credenziali necessarie hello e quindi fare clic su **Authorize**. 
   
    ![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Enable automatic user provisioning")

7. Fare clic su **concedere accesso tooBox** tooauthorize questo toohello operazione e tooreturn portale di Azure. 
   
    ![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Enable automatic user provisioning")

8. Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour casella app. Se hello connessione non riesce, verificare che all'account Box disponga delle autorizzazioni di amministratore di Team e provare hello **"Autorizza"** esegue nuovamente l'istruzione.

9. Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello.

10. Fare clic su **Salva**.

11. Nella sezione mapping hello, selezionare **tooBox sincronizzare Active Directory gli utenti di Azure.**

12. In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooBox di Azure AD. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello account utente nella casella per le operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

13. tooenable hello servizio provisioning di Azure AD per casella di modifica hello **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello

14. Fare clic su **Salva**.

Che avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooBox in hello gli utenti e gruppi. la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite dal servizio nella tua app casella hello.

È ora possibile creare un account di test. Attendere che i minuti too20 tooverify che hello account è stato sincronizzato toobox.

Nel tenant di Box gli utenti sincronizzati sono elencati in **utenti gestiti** in hello **Console di amministrazione**.

![Stato integrazione](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Stato integrazione")


## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configurare l'accesso Single Sign-On](active-directory-saas-box-tutorial.md)