---
title: 'Esercitazione: configurazione di Google Apps per il provisioning utenti automatico in Azure | Microsoft Docs'
description: Informazioni su come degli account utente di effettuare il provisioning e la prestazione tooautomatically da Azure AD tooGoogle app.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a>Esercitazione: configurazione di Google Apps per il provisioning utenti automatico

obiettivo di Hello di questa esercitazione è tooshow che Hello passaggi è necessario tooperform riserva tooautomatically Google Apps e Azure AD e il deprovisioning degli account utente da Azure AD tooGoogle app.

## <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

*   Tenant di Azure Active Directory.
*   È necessario disporre di un tenant valido per Google Apps for Work o Google Apps for Education. È possibile usare un account della versione di valutazione gratuita per entrambi i servizi.
*   Account utente in Google Apps con autorizzazioni di amministratore di team.

## <a name="assigning-users-toogoogle-apps"></a>Assegnazione di utenti tooGoogle App

Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso. Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.

Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano utenti hello necessitano accedere alle app di Google Apps tooyour. Una volta deciso, è possibile assegnare queste app di Google Apps tooyour utenti seguendo le istruzioni di hello qui: [assegnare un'applicazione aziendale tooan utente o gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

> [!IMPORTANT]
>*   È consigliabile che un singolo utente di Azure AD assegnare hello tootest di App tooGoogle configurazione provisioning. È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.
>*   Quando si assegna un tooGoogle utente App, è necessario selezionare hello utente o ruolo di "Gruppo" nella finestra di dialogo assegnazione hello. ruolo di "accesso predefinita" Hello non funziona per il provisioning.

## <a name="enable-automated-user-provisioning"></a>Abilitare il provisioning utenti automatico

Questa sezione viene illustrato come tramite la connessione di account utente dell'Azure AD tooGoogle App API di provisioning e configurazione hello toocreate servizio di provisioning, aggiornare e disabilitare gli account utente assegnato in Google Apps in base all'assegnazione di utenti e gruppi in Azure AD .

>[!Tip]
>È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Google Apps, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com). L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.

### <a name="configure-automatic-user-account-provisioning"></a>Configurare il provisioning automatico degli account utente

> [!NOTE]
> Un'altra opzione valida per l'automazione delle applicazioni tooGoogle il provisioning degli utenti è toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) che esegue il provisioning del tooGoogle di identità di Active Directory locale app. Al contrario, la soluzione hello in questa esercitazione viene eseguito il provisioning gli utenti di Azure Active Directory (cloud) e i gruppi abilitati alla posta elettronica tooGoogle app. 

1. Sign in hello [Console di amministrazione di Google Apps](http://admin.google.com/) con l'account amministratore e fare clic su **sicurezza**. Se non viene visualizzato il collegamento hello, possono essere nascosti in hello **più controlli** menu in basso hello hello.
   
    ![Fare clic su sicurezza.][10]

2. In hello **sicurezza** pagina, fare clic su **riferimento all'API**.
   
    ![Fare clic su Informazioni di riferimento sulle API.][15]

3. Selezionare **Enable API access**.
   
    ![Fare clic su Informazioni di riferimento sulle API.][16]

    > [!IMPORTANT]
    > Per ogni utente che si desidera tooprovision tooGoogle App, il suo nome utente in Azure Active Directory *deve* essere abbinato tooa dominio personalizzato. Ad esempio, nomi utente simili a bob@contoso.onmicrosoft.com non verranno accettati da Google Apps, mentre bob@contoso.com verranno accettati. È possibile modificare il dominio di un utente esistente modificandone le proprietà in Azure AD. Istruzioni per come inclusi in un dominio personalizzato per Azure Active Directory e Google Apps tooset i passaggi seguenti.
      
4. Se non sono stati aggiunti ancora un tooyour di nome di dominio personalizzato Azure Active Directory, quindi seguire hello alla procedura seguente:
  
    a. In hello [portale di Azure](https://portal.azure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**. Nell'elenco di directory hello, selezionare la directory. 

    b. Fare clic su **nome domini** hello riquadro di spostamento a sinistra e quindi fare clic su **Aggiungi**.
     
     ![dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![aggiunta del dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    c. Digitare il nome di dominio in hello **nome di dominio** campo. Il nome di dominio deve essere hello stesso nome di dominio che si desidera toouse per Google Apps. Quando si è pronti, fare clic su hello **Aggiungi dominio** pulsante.
     
     ![nome di dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    d. Fare clic su **Avanti** toogo toohello pagina di verifica. tooverify che si è proprietari di questo dominio, è necessario modificare i record DNS del dominio hello in base a valori toohello forniti in questa pagina. È possibile scegliere tooverify utilizzando **record MX** o **record TXT**, a seconda della selezione per hello **tipo di Record** opzione. Per istruzioni più complete su come nome di dominio tooverify con Azure AD, vedere [aggiungere la propria tooAzure nome di dominio Active Directory](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).
     
     ![dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    e. Ripetere i passaggi per tutti i domini di hello che si desidera tooadd tooyour directory precedenti hello.

5. Ora che tutti i domini sono stati verificati con Azure AD, è necessario verificarli nuovamente con Google Apps. Per ogni dominio che non è già registrata con Google Apps, eseguire hello alla procedura seguente:
   
    a. In hello [Console di amministrazione di Google Apps](http://admin.google.com/), fare clic su **domini**.
     
     ![Fare clic su Domini][20]

    b. Fare clic su **Add a domain or a domain alias**.
     
     ![Aggiungere un nuovo dominio][21]

    c. Selezionare **aggiungere un altro dominio**e digitare il nome di hello del dominio hello che si desidera tooadd.
     
     ![Digitare il nome di dominio][22]

    d. Fare clic su **Continue and verify domain ownership** (Continua e verifica la proprietà del dominio). Seguire quindi hello passaggi tooverify che si è proprietari di nome di dominio hello. Per istruzioni dettagliate su come tooverify del dominio con Google Apps, vedere. [Verificare la proprietà del sito con Google Apps](https://support.google.com/webmasters/answer/35179).

    e. Ripetere i passaggi per tutti i domini aggiuntivi che si desidera tooadd tooGoogle App precedenti hello.
     
     > [!WARNING]
     > Se si modifica il dominio primario hello del tenant di Google Apps, e se è già configurato single sign-on con Azure AD e aver toorepeat passaggio #3 nella sezione [passaggio 2: abilitare Single Sign-On](#step-two-enable-single-sign-on).
       
6. In hello [Console di amministrazione di Google Apps](http://admin.google.com/), fare clic su **ruoli di amministratore**.
   
     ![Fare clic su Google Apps][26]

7. Determinare quale amministratore account desideri toouse toomanage provisioning degli utenti. Per hello **ruolo admin** di tale account, modificare hello **privilegi** per tale ruolo. Assicurarsi che tutti hello **privilegi di amministratore API** abilitato in modo che questo account può essere usato per il provisioning.
   
     ![Fare clic su Google Apps][27]
   
    > [!NOTE]
    > Se si sta configurando un ambiente di produzione, hello consiglia toocreate un account di amministratore in Google Apps in modo specifico per questo passaggio. Questi account devono avere un ruolo di amministratore associato che disponga dei privilegi di API necessari hello.
     
8. In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.

9. Se è già stato configurato Google Apps per single sign-on, eseguire la ricerca per l'istanza di Google Apps utilizzando il campo di ricerca hello. In caso contrario, selezionare **Aggiungi** e cercare **Google Apps** nella raccolta di applicazione hello. Selezionare Google Apps dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.

10. Selezionare l'istanza di Google Apps, quindi selezionare hello **Provisioning** scheda.

11. Set hello **modalità di Provisioning** troppo**automatica**. 

     ![provisioning](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. In hello **credenziali di amministratore** fare clic su **Authorize**. Verrà aperta una finestra di dialogo di autorizzazione di Google Apps in una nuova finestra del browser.

13. Confermare che si desidera toogive Azure Active Directory toomake le modifiche alle autorizzazioni che tenant tooyour Google Apps. Fare clic **Accept**.
    
     ![Verificare le autorizzazioni.][28]

14. Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour app di Google Apps. Se hello connessione non riesce, verificare che l'account Google Apps ha autorizzazioni di amministratore di Team e provare a hello **"Autorizza"** esegue nuovamente l'istruzione.

15. Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello.

16. Fare clic su **Salva**.

17. Nella sezione mapping hello, selezionare **tooGoogle sincronizzare Active Directory gli utenti di Azure app.**

18. In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da Azure AD tooGoogle app. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in Google Apps per operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

19. tooenable hello servizio provisioning di Azure AD per Google Apps, hello modifica **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello

20. Fare clic su **Salva**.

Avviare la sincronizzazione iniziale di hello di tutti gli utenti e/o gruppi assegnati App tooGoogle nella sezione utenti e gruppi di hello. la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione. È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio nella tua app di Google Apps.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configurare l'accesso Single Sign-On](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png