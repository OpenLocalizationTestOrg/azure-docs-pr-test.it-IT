---
title: 'Esercitazione: Configurazione di Cerner Central per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come il provisioning di roster tooa gli utenti nel centro Cerner tooconfigure tooautomatically di Azure Active Directory.
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a>Esercitazione: Configurazione di Cerner Central per il provisioning utenti automatico

obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform Cerner centrale e Azure AD tooautomatically il provisioning e il de-provisioning account utente dall'elenco di utenti di Azure AD tooa nella Cerner centrale. 


## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory
*   Tenant di Cerner Central 

> [!NOTE]
> Azure Active Directory si integra con Cerner centrale utilizzando hello [SCIM](http://www.simplecloud.info/) protocollo.

## <a name="assigning-users-toocerner-central"></a>L'assegnazione di utenti tooCerner centrale

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, vengono sincronizzati solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD. 

Prima di configurare e abilitare hello provisioning del servizio, è necessario decidere quali utenti e/o i gruppi in Azure AD rappresentano utenti hello bisogno di accesso centrale tooCerner. Una volta deciso, è possibile assegnare questi tooCerner utenti centrale seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a>Suggerimenti importanti per l'assegnazione di utenti tooCerner centrale

*   È consigliabile che un singolo utente di Azure AD assegnare tooCerner tootest centrale hello configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

* Al termine del test iniziale per un singolo utente, Cerner centrale consiglia di assegnare hello intero elenco utenti destinati tooaccess roster utente del tooCerner toobe provisioning qualsiasi Cerner soluzione (non solo Cerner centrale).  Altre soluzioni Cerner sfruttano questo elenco di utenti nell'elenco di utenti hello.

*   Quando si assegna un tooCerner utente centrale, è necessario selezionare hello **utente** ruolo nella finestra di dialogo assegnazione hello. Gli utenti con ruolo di "accesso predefinita" hello vengono esclusi dal provisioning.


## <a name="configuring-user-provisioning-toocerner-central"></a>Configurazione tooCerner centrale di provisioning dell'utente

In questa sezione in modo semplificato Roster utente del centro del tooCerner Azure AD tramite API di provisioning dell'account utente SCIM della Cerner connessione e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare l'utente assegnato account Cerner centrale in base assegnazione di utenti e gruppi in Azure AD.

> [!TIP]
> È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per sedi centrali Cerner, attenendosi alle istruzioni hello fornite in [portale di Azure (https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari. Per ulteriori informazioni, vedere hello [esercitazione centrale Cerner single sign-on](active-directory-saas-cernercentral-tutorial.md).


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a>account utente automatico tooconfigure provisioning tooCerner centrale in Azure AD:


In ordine tooprovision utente account tooCerner centrale, sarà necessario un account di sistema centrale Cerner da Cerner toorequest e generare un token di connessione OAuth che Azure AD è possibile utilizzare endpoint SCIM del tooCerner tooconnect. È inoltre consigliabile eseguire integrazione hello in un ambiente sandbox Cerner prima di distribuire tooproduction.

1.  primo passaggio Hello è persone hello tooensure gestione hello Cerner e integrazione di Azure AD avere un account CernerCare, che è necessario tooaccess hello documentazione necessari toocomplete hello istruzioni. Se necessario, utilizzare l'URL di hello sotto toocreate CernerCare account in ogni ambiente applicabile.

   * Sandbox: https://sandboxcernercare.com/accounts/create

   * Produzione: https://cernercare.com/accounts/create  

2.  È quindi necessario creare un account di sistema per Azure AD. Usare le istruzioni di hello sotto toorequest un Account di sistema per gli ambienti sandbox e di produzione.

   * Istruzioni: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account

   * Sandbox: https://sandboxcernercentral.com/system-accounts/

   * Produzione: https://cernercentral.com/system-accounts/

3.  Generare quindi un token di connessione OAuth per ogni account di sistema. toodo, seguire hello istruzioni seguenti.

   * Istruzioni: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token

   * Sandbox: https://sandboxcernercentral.com/system-accounts/

   * Produzione: https://cernercentral.com/system-accounts/

4. Infine, è necessario tooacquire utente Roster dell'area di autenticazione per entrambi gli ambienti sandbox e di produzione di hello nella configurazione di hello toocomplete Cerner. Per informazioni su come tooacquire questa operazione, vedere: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM. 

5. È ora possibile configurare tooCerner gli account utente di Azure AD tooprovision. Accedi toohello [portale di Azure](https://portal.azure.com)e passare toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

6. Se Cerner centrale già stato configurato per single sign-on, la ricerca per l'istanza del sito centrale Cerner usando il campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **Cerner centrale** nella raccolta di applicazione hello. Selezionare Cerner centrale dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

7.  Selezionare l'istanza di Cerner centrale, quindi selezionare hello **Provisioning** scheda.

8.  Set hello **modalità di Provisioning** troppo**automatica**.

   ![Provisioning in Cerner Central](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  Compilare hello seguenti campi in **credenziali di amministratore**:

   * In hello **URL Tenant** immettere un URL nel formato hello seguito, sostituendo "Roster-area di autenticazione-ID utente" con ID area di autenticazione hello acquisite nel passaggio &#4;.

> Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

> Produzione: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

   * In hello **segreto Token** campo immettere i token di connessione OAuth hello generato nel passaggio &#3;, quindi scegliere **Test connessione**.

   * Vedrai una notifica di esito positivo sul lato upperright hello del portale.

10. Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello riportato di seguito.

11. Fare clic su **Salva**. 

12. In hello **mapping degli attributi** sezione, esaminare utente hello e gruppo attributi toobe sincronizzati da Azure AD tooCerner centrale. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello utente account e gruppi nel centro Cerner per operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

13. tooenable hello servizio provisioning di Azure AD per sedi centrali Cerner, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione

14. Fare clic su **Salva**. 

Verrà avviata la sincronizzazione iniziale di hello di tutti gli utenti e/o gruppi assegnati tooCerner Central nella sezione utenti e gruppi di hello. la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio provisioning di Azure AD è in esecuzione. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio nella tua app Cerner centrale.

Per ulteriori informazioni sulla modalità di registrazione tooread provisioning di hello Azure AD, vedere [creazione di report per il provisioning utente automatico account](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Cerner Central: Publishing identity data using Azure AD (Cerner Central: Pubblicazione dei dati sull'identità con Azure AD)](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [Esercitazione sulla configurazione di Cerner Central per l'accesso Single Sign-On con Azure Active Directory](active-directory-saas-cernercentral-tutorial.md)
* [Gestione del provisioning degli account utente per app aziendali](active-directory-enterprise-apps-manage-provisioning.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Passaggi successivi
* [Informazioni su modalità di registrazione tooreview e ottenere report sull'attività di provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).
