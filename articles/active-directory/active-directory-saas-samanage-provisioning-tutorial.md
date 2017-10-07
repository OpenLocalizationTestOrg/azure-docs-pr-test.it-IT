---
title: 'Esercitazione: Configurazione di Samanage per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come tooconfigure Azure Active Directory tooautomatically il provisioning e il de-provisioning account utente di tooSamanage.
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
ms.openlocfilehash: 6cb36d2cc6ce33da4f8ebba65d138bfd4f2aca9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a>Esercitazione: Configurazione di Samanage per il provisioning utenti automatico


obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in Samanage e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooSamanage. 

## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory
*   Un tenant di Samanage con hello [piano Professional](https://www.samanage.com/pricing/) o meglio abilitato 
*   Account utente in Samanage con autorizzazioni di amministratore 

> [!NOTE]
> Hello provisioning integrazione di Azure AD si basa su hello [API REST di Samanage](https://www.samanage.com/api/), ovvero team tooSamanage disponibile sulla hello Professional pianificare o, meglio.

## <a name="assigning-users-toosamanage"></a>L'assegnazione di utenti tooSamanage

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato. 

Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour Samanage app. Una volta deciso, è possibile assegnare queste app di Samanage tooyour utenti seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toosamanage"></a>Suggerimenti importanti per l'assegnazione di utenti tooSamanage

*   È consigliabile che un singolo utente AD Azure viene assegnato hello tootest tooSamanage configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

*   Quando si assegna un tooSamanage utente, è necessario selezionare entrambi hello **utente** ruolo, o un altro valido specifici dell'applicazione, se disponibile, nella finestra di dialogo assegnazione hello. Hello **accesso predefinito** ruolo non funziona per il provisioning e gli utenti vengono ignorati.

> [!NOTE]
> Come funzionalità di aggiunta, hello provisioning servizio legge eventuali ruoli personalizzati definiti in Samanage e le Importa in Azure Active Directory in cui può essere selezionati nella finestra di dialogo selezionare il ruolo hello. Questi ruoli saranno visibili nel portale di Azure hello dopo hello provisioning del servizio è abilitata e un ciclo di sincronizzazione è stata completata.

## <a name="configuring-user-provisioning-toosamanage"></a>Configurazione tooSamanage di provisioning dell'utente 

Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooSamanage il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in Samanage in base all'assegnazione di utenti e gruppi in Azure AD.

> [!TIP]
> È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Samanage, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.


### <a name="configure-automatic-user-account-provisioning-toosamanage-in-azure-ad"></a>Configurare l'account utente automatico provisioning tooSamanage in Azure AD:


1. In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

2. Se è già stato configurato Samanage per single sign-on, eseguire la ricerca per l'istanza di Samanage usando il campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **Samanage** nella raccolta di applicazione hello. Selezionare Samanage dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

3. Selezionare l'istanza di Samanage, quindi selezionare hello **Provisioning** scheda.

4. Set hello **modalità di Provisioning** troppo**automatica**.

    ![Provisioning di Samanage](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. In hello **credenziali di amministratore** sezione, hello input **Admin Username e Password amministratore** dell'account di Samanage. 

6. Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour Samanage app. Se hello connessione non riesce, verificare che l'account di Samanage disponga delle autorizzazioni di amministratore e riprovare a eseguire il passaggio 5.

7. Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e controllo hello casella di controllo "Invia una notifica di posta elettronica quando si verifica un errore".

8. Fare clic su **Salva**. 

9. Nella sezione mapping hello, selezionare **tooSamanage sincronizzare Active Directory gli utenti di Azure**.

10. In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooSamanage di Azure AD. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in Samanage per operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

11. tooenable hello servizio provisioning di Azure AD per Samanage, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione

12. Fare clic su **Salva**. 

Questa operazione avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooSamanage in hello gli utenti e gruppi. la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio.

Per ulteriori informazioni sulla modalità di registrazione tooread provisioning di hello Azure AD, vedere [creazione di report per il provisioning utente automatico account](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-enterprise-apps-manage-provisioning.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Passaggi successivi

* [Informazioni su modalità di registrazione tooreview e ottengono report sull'attività di provisioning](active-directory-saas-provisioning-reporting.md)
