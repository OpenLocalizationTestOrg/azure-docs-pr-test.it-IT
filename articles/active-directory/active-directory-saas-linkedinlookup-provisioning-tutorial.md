---
title: 'Esercitazione: Configurazione di LinkedIn Lookup per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come tooconfigure Azure Active Directory tooautomatically il provisioning e il de-provisioning account utente di tooLinkedIn ricerca.
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 3e41abb8af00715f70e5a14d9d26ff600c10f492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a>Esercitazione: Configurazione di LinkedIn Lookup per il provisioning utenti automatico


obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in ricerca di LinkedIn e Azure AD tooautomatically effettuare il provisioning e il de-provisioning degli account utente da Azure AD tooLinkedIn ricerca. 

## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory
*   Tenant di LinkedIn Lookup 
*   Un account di amministratore per la ricerca di LinkedIn con accesso toohello centro Account LinkedIn

> [!NOTE]
> Azure Active Directory si integra con ricerca di LinkedIn con hello [SCIM](http://www.simplecloud.info/) protocollo.

## <a name="assigning-users-toolinkedin-lookup"></a>L'assegnazione di utenti tooLinkedIn ricerca

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatica, verranno sincronizzati solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD. 

Prima di configurare e abilitare hello provisioning del servizio, sarà necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano utenti hello bisogno di accesso tooLinkedIn ricerca. Una volta deciso, è possibile assegnare questi tooLinkedIn utenti ricerca seguendo le istruzioni di hello qui:

[Assegnare un'applicazione aziendale tooan utente o gruppo](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-lookup"></a>Suggerimenti importanti per l'assegnazione di utenti tooLinkedIn ricerca

*   È consigliabile che un singolo utente di Azure AD assegnare hello tootest di ricerca tooLinkedIn configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.

*   Quando si assegna un tooLinkedIn utente ricerca, è necessario selezionare hello **utente** ruolo nella finestra di dialogo assegnazione hello. ruolo di "accesso predefinita" Hello non funziona per il provisioning.


## <a name="configuring-user-provisioning-toolinkedin-lookup"></a>Configurazione di ricerca tooLinkedIn di provisioning dell'utente

In questa sezione viene illustrata la connessione API di provisioning dell'account utente SCIM della ricerca tooLinkedIn Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare l'utente assegnato conti nella ricerca di LinkedIn basati su utenti e gruppi assegnazione di Azure AD.

> [!TIP]
> È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per la ricerca di LinkedIn, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-lookup-in-azure-ad"></a>account utente automatico tooconfigure provisioning tooLinkedIn ricerca di Azure AD:


primo passaggio Hello è tooretrieve il token di accesso di LinkedIn. Un amministratore dell'organizzazione può eseguire il provisioning automatico di un token di accesso. Nel centro account, Vai troppo**impostazioni &gt; impostazioni globali** e aprire hello **SCIM installazione** pannello.

> [!NOTE]
> Se si accede centro account hello direttamente anziché tramite un collegamento, è possibile raggiungerli tramite hello alla procedura seguente.

1)  Accedi tooAccount Center.

2)  Selezionare **Admin (Amministratore) &gt; Admin Settings** (Opzioni amministratore).

3)  Fare clic su **avanzate integrazioni** intestazione laterale sinistra hello. Si è centro account toohello diretto.

4)  Fare clic su **+ Aggiungi nuova configurazione di SCIM** e seguire la procedura hello compilando ogni campo.

> Se l'opzione di assegnazione automatica delle licenze non è abilitata, vengono sincronizzati solo i dati degli utenti.

![Provisioning di LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> Quando l'assegnazione autolicense è abilitato, è necessario toonote l'istanza dell'applicazione e tipo di licenza. Assegnazione delle licenze in un primo arrivato, prima di servire base fino a quando non vengono eseguite tutte le licenze hello.

![Provisioning di LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  Fare clic su **Generate token** (Genera token). Verrà visualizzata la visualizzazione del token di accesso in hello **token di accesso** campo.

6)  Salva negli Appunti tooyour token di accesso o nel computer prima di uscire dalla pagina hello.

7) Successivamente, accedi toohello [portale di Azure](https://portal.azure.com)e passare toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

8) Se è già stato configurato LinkedIn ricerca per single sign-on, eseguire la ricerca per l'istanza di ricerca di LinkedIn con campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **LinkedIn ricerca** nella raccolta di applicazione hello. Selezionare ricerca LinkedIn dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

9)  Selezionare l'istanza di LinkedIn ricerca, quindi selezionare hello **Provisioning** scheda.

10) Set hello **modalità di Provisioning** troppo**automatica**.

![Provisioning di LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  Compilare hello seguenti campi in **credenziali di amministratore** :

* In hello **URL Tenant** immettere https://api.linkedin.com.

* In hello **segreto Token** campo, immettere il token di accesso hello generato nel passaggio 1 e fare clic su **Test connessione** .

* Vedrai una notifica di esito positivo sul lato upperright hello del portale.

12) Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello riportato di seguito.

13) Fare clic su **Salva**. 

14) In hello **mapping degli attributi** sezione, esaminare gli attributi utente e gruppo hello che verranno sincronizzati da Azure AD tooLinkedIn ricerca. Si noti che gli attributi selezionati come hello **corrispondenza** proprietà saranno utilizzati toomatch hello account e gruppi utente nella ricerca di LinkedIn per operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

![Provisioning di LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) tooenable hello servizio provisioning di Azure AD per la ricerca di LinkedIn, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione

16) Fare clic su **Salva**. 

Verrà avviata la sincronizzazione iniziale di hello di tutti gli utenti e/o gruppi assegnati tooLinkedIn ricerca nella sezione utenti e gruppi di hello. Si noti che la sincronizzazione iniziale hello tooperform più lungo di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio nella tua app di ricerca di LinkedIn.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-enterprise-apps-manage-provisioning.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
