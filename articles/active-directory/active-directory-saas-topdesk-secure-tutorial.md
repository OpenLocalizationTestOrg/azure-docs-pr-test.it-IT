---
title: 'Esercitazione: Integrazione di Azure Active Directory con TOPdesk - Secure | Documentazione Microsoft'
description: Informazioni su come toouse TOPdesk - Secure con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e altro ancora!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a>Esercitazione: Integrazione di Azure Active Directory con TOPdesk - Secure
obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e TOPdesk - Secure.  
scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

* Sottoscrizione di Azure valida
* Sottoscrizione di TOPdesk - Secure abilitata per l'accesso Single Sign-On

Dopo aver completato questa esercitazione, gli utenti di hello Azure AD assegnati tooTOPdesk - verrà protetto è in grado di toosingle sign in un'applicazione hello in TOPdesk - sito aziendale protetta (accesso avviato dal provider di servizi su) oppure utilizza hello [introduzione Pannello di accesso toohello](active-directory-saas-access-panel-introduction.md).

scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:

1. Abilitare l'integrazione dell'applicazione hello per TOPdesk - Secure
2. Configurazione dell'accesso Single Sign-On
3. Configurazione del provisioning utente
4. Assegnazione degli utenti

![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a>Abilitare l'integrazione dell'applicazione hello per TOPdesk - Secure
obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione hello tooenable per TOPdesk - Secure.

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a>integrazione dell'applicazione hello tooenable per TOPdesk - Secure, eseguire hello alla procedura seguente:
1. Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")

2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.

3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Applicazioni](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applicazioni")

4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
    ![Aggiungere un'applicazione](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Aggiungere un'applicazione")

5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
    ![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")

6. In hello **casella di ricerca**, tipo **TOPdesk - Secure**.
   
    ![Raccolta di applicazioni](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Raccolta di applicazioni")

7. Nel riquadro risultati hello selezionare **TOPdesk - Secure**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
    ![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")

## <a name="configuring-single-sign-on"></a>Configurazione dell'accesso Single Sign-On
obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooTOPdesk - Secure con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.  
Configurazione single sign-on per TOPdesk - Secure richiede tooupload un file icona del logo. file dell'icona hello tooget, team di supporto di TOPdesk hello contatto.

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a>tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:
1. Accesso tooyour **TOPdesk - Secure** sito aziendale come amministratore.
2. In hello **TOPdesk** menu, fare clic su **impostazioni**.
   
    ![Impostazioni](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Impostazioni")

3. Fare clic su **Login Settings**.
   
    ![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")

4. Espandere hello **impostazioni di accesso** menu e quindi fare clic su **generale**.
   
    ![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")

5. In hello **sicura** sezione di hello **SAML login** configurazione seguire hello alla procedura seguente:
   
    ![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")
   
    a. Fare clic su **scaricare** toodownload hello file di metadati pubblici e quindi salvarlo in locale nel computer in uso.
   
    b. Aprire il file di metadati hello e individuare hello **AssertionConsumerService** nodo.
    
    ![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")
   
    c. Hello copia **AssertionConsumerService** valore.  
      
    > [!NOTE]
    > Si sarà necessario hello valore hello **Configura URL App** sezione più avanti in questa esercitazione.
    > 
    > 

6. In un'altra finestra del Web browser accedere al portale di **portale di Azure classico** come amministratore.

7. In hello **TOPdesk - Secure** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** hello tooopen * * configurare Single Sign-On * * finestra di dialogo.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configurare l'accesso Single Sign-On")

8. In hello **come verrebbe come utenti toosign su tooTOPdesk - Secure** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configurare l'accesso Single Sign-On")

9. In hello **Configura URL App** eseguire hello alla procedura seguente:
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configurare l'URL dell'app")
   
    a. In hello **TOPdesk - Secure URL di accesso** casella di testo, digitare l'URL hello usato dal toosign gli utenti nell'applicazione TOPdesk - Secure (ad esempio: "*https://qssolutions.topdesk.net*").
   
    b. In hello **TOPdesk-URL di risposta pubblica** casella di testo, incollare hello **TOPdesk - Secure AssertionConsumerService URL** (ad esempio: "*https://qssolutions.topdesk.net/tas/public/login/saml*")
   
    c. Fare clic su **Avanti**.

10. In hello **Configura accesso single sign-on in TOPdesk - Secure** pagina, toodownload il file di metadati, fare clic su **Scarica metadati**e quindi salvare il file hello in locale nel computer.
    
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configurare l'accesso Single Sign-On")

11. toocreate un file di certificato, eseguire hello alla procedura seguente:
    
    ![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")
    
    a. File di metadati scaricato hello aperto.
    b. Espandere hello **RoleDescriptor** nodo che dispone di un **xsi: Type** di **fed: ApplicationServiceType**.
    c. Copiare il valore di hello di hello **X509Certificate** nodo.
    d. Salva hello copiato **X509Certificate** valore in locale nel computer in un file.

12. In TOPdesk - Secure hello del sito della società **TOPdesk** menu, fare clic su **impostazioni**.
    
    ![Impostazioni](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Impostazioni")

13. Fare clic su **Login Settings**.
    
    ![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")

14. Espandere hello **impostazioni di accesso** menu e quindi fare clic su **generale**.
    
    ![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")

15. In hello **pubblica** fare clic su **Aggiungi**.
    
    ![Aggiungi](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Aggiungi")

16. In hello **Assistente configurazione SAML** finestra di dialogo eseguire hello alla procedura seguente:
    
    ![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")
    
    a. tooupload file i metadati scaricati, in **i metadati della federazione**, fare clic su **Sfoglia**.

    b. file del certificato, in tooupload **Certificate (RSA)**, fare clic su **Sfoglia**.

    c. file del logo hello tooupload ottenuto dal team di supporto di TOPdesk hello, in **icona del Logo**, fare clic su **Sfoglia**.

    d. In hello **attributo nome utente** casella tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    e. In hello **nome visualizzato** casella di testo, digitare un nome per la configurazione.

    f. Fare clic su **Salva**.

17. Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.
    
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configurare l'accesso Single Sign-On")

## <a name="configuring-user-provisioning"></a>Configurazione del provisioning utente
In ordine tooenable Azure AD utenti toolog TopDesk - Secure, è necessario eseguirne il provisioning in TOPdesk - Secure.  
Nel caso di hello di TOPdesk - Secure, il provisioning è un'attività manuale.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:
1. Accesso tooyour **TOPdesk - Secure** sito aziendale come amministratore.
2. Scegliere dal menu hello in primo piano hello **TOPdesk \> New \> i file di supporto \> operatore**.
   
    ![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")

3. In hello **nuovo operatore** finestra di dialogo, eseguire hello alla procedura seguente:
   
    ![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")
   
    a. Fare clic sulla scheda Generale hello.
   
    b. In hello **Surname** casella di testo di hello **generale** sezione, digitare hello cognome di un account Azure Active Directory valido, si desidera tooprovision.
   
    c. Selezionare un **sito** per conto di hello in hello **percorso** sezione.
   
    d. In hello **nome account di accesso** casella di testo di hello **TOPdesk Login** , immettere un nome di account di accesso per l'utente.
   
    e. Fare clic su **Salva**.

> [!NOTE]
> È possibile usare qualsiasi altro - account utente sicura di creazione o le API fornite da TOPdesk - Secure tooprovision account utente di AAD.
> 
> 

## <a name="assigning-users"></a>Assegnazione degli utenti
tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a>tooassign utenti tooTOPdesk - Secure, eseguire hello alla procedura seguente:
1. Nel portale di Azure classico hello, creare un account di prova.
2. In hello * * TOPdesk - Secure * * pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.
   
    ![Assegnare utenti](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assegnare utenti")

3. Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.
   
    ![Sì](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Sì")

Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello. Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

