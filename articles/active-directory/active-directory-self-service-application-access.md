---
title: accesso all'applicazione di servizio di aaaSelf e la gestione delegata con Azure Active Directory | Documenti Microsoft
description: In questo articolo descrive come accedere alle applicazioni self-service tooenable e la gestione delegata con Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 448a7fe8-a162-475e-9ba2-2e3ab59302bc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: asmalser
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 90bec3bd71796f22a782929b028db0d18c3aa1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-application-access-and-delegated-management-with-azure-active-directory"></a>Accesso alle applicazioni self-service e gestione delegata con Azure Active Directory
L'abilitazione della funzionalità self-service per gli utenti finali è uno scenario comune nell'IT aziendale. Un numero elevato di utenti, un numero elevato di applicazioni e hello persona best-informed toomake accesso concede decisioni potrebbero non essere amministratore di directory hello. Spesso hello migliore persona toodecide che può accedere a un'applicazione è responsabile del team o un altro amministratore delegato. Tuttavia, è utente di hello che utilizza l'applicazione hello e hello utente sappia quali devono toodo in grado di toobe il proprio lavoro.

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo. 

L'accesso alle applicazioni self-service è una funzionalità delle licenze P1 e P2 di [Azure Active Directory Premium](https://azure.microsoft.com/trial/get-started-active-directory/) che permette agli amministratori di directory di:

* Abilitare l'accesso di utenti toorequest tooapplications utilizzando un "altre applicazioni Get" riquadro in hello [Pannello di accesso AD Azure](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)
* Impostare le applicazioni a cui gli utenti possono richiedere l'accesso.
* Impostare o meno un'approvazione è necessaria per gli utenti toobe in grado di tooself assegna accesso tooan applicazione
* Set che devono approvare le richieste di hello e gestire l'accesso per ogni applicazione

Attualmente questa funzionalità è supportata per tutte le app preintegrate e personalizzate che supportano federato o basato su password single sign-on in hello [raccolta di applicazioni per Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/), incluse le app come Salesforce, Dropbox, Google Apps e altro ancora.
Questo articolo illustra come:

* Configurare l'accesso alle applicazioni self-service per gli utenti finali e configurare un flusso di lavoro di approvazione facoltativo. 
* Delegare la gestione di accesso per applicazioni specifiche toohello più adatto agli utenti dell'organizzazione e consentire richieste di accesso al pannello tooapprove toouse hello Azure AD access, assegnare direttamente l'accesso agli utenti di tooselected o impostare (facoltativamente) credenziali per l'accesso all'applicazione quando basato su password single sign-on è configurato

## <a name="configuring-self-service-application-access"></a>Configurazione dell'accesso alle applicazioni self-service
accesso all'applicazione self-service tooenable e configurato le applicazioni che possono essere aggiunti o richiesto dagli utenti finali, seguono queste istruzioni.

1. Sign in hello [portale di Azure classico](https://manage.windowsazure.com/).

2.   In hello **Active Directory** sezione, selezionare la directory, quindi selezionare hello **applicazioni** scheda. 

3. Seleziona hello **Aggiungi** pulsante e utilizzare hello raccolta opzione tooselect e aggiungere un'applicazione.

4. Dopo aver aggiunto l'app, si otterrà pagina avvio rapido di hello app. Fare clic su **configurare Single Sign-On**selezionare hello desiderato modalità single sign-on e salvare la configurazione di hello. 

5. Selezionare quindi hello **configura** scheda tooenable utenti toorequest accesso toothis app dal Pannello di accesso hello Azure AD, impostare **consentire l'accesso all'applicazione self-service** troppo**Sì**.
  
  ![][1]

6. toooptionally configurare un flusso di lavoro di approvazione per le richieste di accesso, impostare **richiedono l'approvazione prima di concedere l'accesso** troppo**Sì**. Quindi è possibile selezionare uno o più revisori utilizzando hello **responsabili approvazione** pulsante.

  Un responsabile approvazione può essere qualsiasi utente nell'organizzazione hello con un account di Azure AD e potrebbe essere responsabile dell'account di provisioning, licenze, o qualsiasi altro processo di business dell'organizzazione richiede prima di concedere l'accesso tooan app. responsabile approvazione Hello potrebbe anche essere proprietario del gruppo di hello di uno o più gruppi di account condiviso ed è possibile assegnare hello tooone di utenti di questi gruppi di toogive loro l'accesso tramite un account condiviso. 

  Se nessuna approvazione è necessaria, quindi gli utenti ricevono immediatamente Pannello di accesso di hello applicazione tootheir aggiunto AD Azure. Se un'applicazione hello è stata impostata per [il provisioning utente automatico](active-directory-saas-app-provisioning.md), o è stato impostato [modalità SSO "gestite dall'utente" password](active-directory-appssoaccess-whatis.md#password-based-single-sign-on), utente hello dovrebbe già disporre di un utente dell'account e conoscere la password hello.

7. Se un'applicazione hello è stato configurato toouse basato su password single sign-on quindi un'opzione per consentire di responsabile approvazione hello credenziali SSO di hello tooset per conto di ogni utente è anche disponibile. Per ulteriori informazioni, vedere la sezione hello in [accesso gestione delegata](#delegated-application-access-management).

8. Infine, hello **gruppo per gli utenti Self-Assigned** Mostra hello nome del gruppo di hello che gli utenti di hello toostore utilizzati che sono state concessi o accesso toohello applicazione assegnati. responsabile approvazione accesso Hello diventa il proprietario di hello di questo gruppo. Se il nome di gruppo hello mostrato non esiste, viene creato automaticamente. Facoltativamente è possibile impostare il nome di gruppo hello toohello nome di un gruppo esistente.

9. configurazione di hello toosave, fare clic su **salvare** in basso hello hello. Gli utenti possono ora toorequest accesso toothis app dal Pannello di accesso hello.

10. esperienza dell'utente finale hello tootry, accedere al pannello di accesso di Azure AD dell'organizzazione in https://myapps.microsoft.com, preferibilmente in un altro account che non è un responsabile approvazione di app. 

11. In hello **applicazioni** scheda, fare clic su hello **altre applicazioni** riquadro. Questo riquadro Visualizza una raccolta di tutte le applicazioni che sono state abilitate per l'accesso all'applicazione self-service nella directory di hello, con toosearch possibilità hello e Filtra per categoria di app a sinistra di hello hello. 

12. Facendo clic su un'app verrà avviato il processo di richiesta di hello. Se non è richiesto alcun processo di approvazione, l'applicazione hello verrà aggiunto immediatamente sotto hello **applicazioni** scheda dopo un breve messaggio di conferma. Se è necessaria l'approvazione, verranno visualizzate una finestra di dialogo per indicare questa condizione e un messaggio di posta elettronica viene inviato ai responsabili approvazione toohello. È necessario essere connessi in hello Pannello di accesso come un toosee non approvatore questo processo di richiesta.

13. messaggio di posta elettronica Hello indirizza hello approvatore toosign nel Pannello di accesso di Azure AD hello e approva la richiesta di hello. Una volta hello richiesta viene approvata e i processi speciali definire siano stati eseguiti dal responsabile approvazione hello, hello visualizzato dall'utente dell'applicazione hello vengono visualizzati nella loro **applicazioni** scheda in cui possono accedere al suo interno.

## <a name="delegated-application-access-management"></a>Gestione delegata degli accessi alle applicazioni
Un responsabile approvazione l'accesso dell'applicazione può essere qualsiasi utente nell'organizzazione è tooapprove persona più appropriato hello o negare l'accesso toohello applicazione in questione. L'utente potrebbe essere responsabile dell'account di provisioning, licenze, o qualsiasi altro processo di business dell'organizzazione richiede prima di concedere l'accesso tooan app.

Quando si configura l'accesso all'applicazione self-service descritto in precedenza, qualsiasi applicazione assegnata ai responsabili approvazione vedere un'ulteriore **Gestisci applicazioni di** riquadro nel Pannello di accesso hello Azure AD, che li visualizza le applicazioni che sono Hello accesso amministratore. Facendo clic su un'app viene visualizzata una schermata con diverse opzioni.

![][2]

### <a name="approve-requests"></a>Approva richieste
Hello **approvare richieste** riquadro consente ai responsabili approvazione toosee qualsiasi app specifiche toothat approvazioni in sospeso e scheda approvazioni di reindirizzamenti toohello in cui le richieste hello può essere confermato o negato. responsabile approvazione Hello riceve messaggi di posta elettronica automatizzati anche ogni volta che viene creata una richiesta che indica a tali quali toodo.

### <a name="add-users"></a>Aggiungi utenti
Hello **Aggiungi utenti** riquadro consente ai responsabili approvazione toodirectly grant selezionato agli utenti accesso toohello applicazione. Al momento facendo clic su questo riquadro, responsabile approvazione hello visualizzerà che una finestra di dialogo consente tooview e ricerca per gli utenti nella propria directory. Aggiunta dei risultati di un utente in un'applicazione hello attualmente visualizzata in pannelli di accesso dell'utente, tali Azure AD o Office 365. Se tutti gli utenti manuali il processo di provisioning sono necessario all'applicazione hello prima che l'utente hello è in grado di toosign in, quindi approvatore hello è consigliabile eseguire la procedura prima di assegnare l'accesso.  

### <a name="manage-users"></a>Gestire gli utenti
Hello **Gestisci utenti** riquadro consente ai responsabili approvazione toodirectly aggiornamento o rimuovere gli utenti che hanno accesso toohello applicazione. 

### <a name="configure-password-sso-credentials-if-applicable"></a>Configurare le credenziali SSO con password (se applicabile)
Hello **configura** riquadro viene visualizzato solo se è stata configurata un'applicazione hello da hello IT amministratore toouse basato su password single sign-on e amministratore hello concesso approvatore hello credenziali SSO di hello possibilità tooset password come descritto in precedenza. Quando è selezionata, hello responsabile approvazione viene presentato con diverse opzioni per come credenziali di hello vengono propagati tooassigned utenti:

![][3]

* **Gli utenti di accedere con le proprie password** : In questa modalità, gli utenti assegnato hello conoscano i relativi nomi utente e password per l'applicazione hello e sono tooenter richiesta loro dopo la prima domanda di toohello Accedi. Hello scenario corrisponde case SSO di password toohello dove hello [agli utenti di gestire le credenziali](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Gli utenti sono automaticamente l'accesso con account distinti che è possibile gestire** : In questa modalità, hello assegnato o degli utenti non tooenter necessario conoscere le proprie credenziali specifico dell'applicazione quando si accede a un'applicazione hello. Al contrario, responsabile approvazione hello imposta le credenziali di hello per ogni utente dopo l'assegnazione dell'accesso tramite hello **Aggiungi utente** riquadro. Quando l'utente hello fa clic su un'applicazione hello Pannello di accesso o Office 365, accede automaticamente con le credenziali di hello impostate dal responsabile approvazione hello. Hello scenario corrisponde case SSO di password toohello dove hello [gli amministratori di gestiscono le credenziali](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Gli utenti sono automaticamente l'accesso utilizzando un account singolo che è possibile gestire** -un caso speciale, in questo caso è toouse appropriata quando tutti gli utenti assegnati necessitano toobe concesso l'accesso utilizzando un singolo account condiviso. Hello più comuni per questa funzionalità viene usata con le applicazioni di social media, in cui un'organizzazione ha un account singolo "company" e più utenti devono toomake aggiornamenti toothat account. Hello scenario corrisponde inoltre case SSO di password toohello dove hello [gli amministratori di gestiscono le credenziali](active-directory-appssoaccess-whatis.md#password-based-single-sign-on). Tuttavia, dopo aver selezionato questa opzione, responsabile approvazione hello sarà richiesta tooenter hello username e password per account condiviso singolo hello. Una volta completato, tutti gli utenti assegnati sono firmati con questo account quando si fa clic sull'applicazione hello pannelli di accesso di Azure AD o Office 365.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)

<!--Image references-->
[1]: ./media/active-directory-self-service-application-access/ssaa_admin.PNG
[2]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app.PNG
[3]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app_config.PNG
