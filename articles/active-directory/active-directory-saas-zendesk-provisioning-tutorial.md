---
title: 'Esercitazione: Configurazione di ZenDesk per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come tooconfigure Azure Active Directory tooautomatically il provisioning e il de-provisioning account utente di tooZenDesk.
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
ms.openlocfilehash: 200e8790ec1755f5cf927274ceb38527dd993f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a>Esercitazione: Configurazione di ZenDesk per il provisioning utenti automatico


obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in ZenDesk e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooZenDesk. 

## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory
*   Un tenant di ZenDesk con hello [piano Enterprise](https://www.zendesk.com/product/pricing/) o meglio abilitato 
*   Account utente in ZenDesk con autorizzazioni di amministratore 

> [!NOTE]
> Hello provisioning integrazione di Azure AD si basa su hello [API REST di ZenDesk](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), ovvero i team tooZenDesk disponibili nel piano essenziali hello o migliori.

## <a name="assigning-users-toozendesk"></a>L'assegnazione di utenti tooZenDesk

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, vengono sincronizzati solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD. 

Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere app ZenDesk tooyour. Una volta deciso, è possibile assegnare queste app di ZenDesk tooyour utenti seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toozendesk"></a>Suggerimenti importanti per l'assegnazione di utenti tooZenDesk

*   È consigliabile che un singolo utente AD Azure viene assegnato hello tootest tooZenDesk configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

*   Quando si assegna un tooZenDesk utente, è necessario selezionare entrambi hello **utente** ruolo, o un altro valido specifici dell'applicazione, se disponibile, nella finestra di dialogo assegnazione hello. Hello **accesso predefinito** ruolo non funziona per il provisioning e gli utenti vengono ignorati.

> [!NOTE]
> Come funzionalità di aggiunta, hello provisioning servizio legge eventuali ruoli personalizzati definiti in Zendesk e le Importa in Azure Active Directory in cui può essere selezionati nella finestra di dialogo selezionare il ruolo hello. Questi ruoli saranno visibili nel portale di Azure hello dopo hello provisioning del servizio è abilitata e un ciclo di sincronizzazione è stata completata.

## <a name="configuring-user-provisioning-toozendesk"></a>Configurazione tooZenDesk di provisioning dell'utente 

Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooZenDesk il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in ZenDesk in base all'assegnazione di utenti e gruppi in Azure AD.

> [!TIP] 
> È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per ZenDesk, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.


### <a name="configure-automatic-user-account-provisioning-toozendesk-in-azure-ad"></a>Configurare l'account utente automatico provisioning tooZenDesk in Azure AD


1. In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

2. Se è già stato configurato ZenDesk per single sign-on, eseguire la ricerca per l'istanza di ZenDesk con il campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **ZenDesk** nella raccolta di applicazione hello. Selezionare ZenDesk dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

3. Selezionare l'istanza di ZenDesk, quindi selezionare hello **Provisioning** scheda.

4. Set hello **modalità di Provisioning** troppo**automatica**.

    ![Provisioning di ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. In hello **credenziali di amministratore** sezione, hello input **Admin Username & tokenkey & dominio** generato dall'account di ZenDesk (è possibile trovare il token hello con l'account: **Admin**   >  **API** > **impostazioni**). 

    ![Provisioning di ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi app ZenDesk tooyour. Se hello connessione non riesce, verificare che l'account ZenDesk disponga delle autorizzazioni di amministratore e riprovare a eseguire il passaggio 5.

7. Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e controllo hello casella di controllo "Invia una notifica di posta elettronica quando si verifica un errore".

8. Fare clic su **Salva**. 

9. Nella sezione mapping hello, selezionare **tooZenDesk sincronizzare Active Directory gli utenti di Azure**.

10. In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooZenDesk di Azure AD. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in ZenDesk per operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

11. tooenable hello servizio provisioning di Azure AD per ZenDesk, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione

12. Fare clic su **Salva**. 

Questa operazione avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooZenDesk in hello gli utenti e gruppi. la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio.

Per ulteriori informazioni sulla modalità di registrazione tooread provisioning di hello Azure AD, vedere [creazione di report per il provisioning utente automatico account](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-enterprise-apps-manage-provisioning.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Passaggi successivi

* [Informazioni su modalità di registrazione tooreview e ottengono report sull'attività di provisioning](active-directory-saas-provisioning-reporting.md)
