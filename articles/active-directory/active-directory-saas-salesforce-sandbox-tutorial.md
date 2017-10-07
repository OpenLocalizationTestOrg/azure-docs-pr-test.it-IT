---
title: 'Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox | Microsoft Docs'
description: Informazioni su come toouse Salesforce Sandbox con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox

obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e Salesforce Sandbox.  

>[!TIP]
>Per commenti e suggerimenti, vedere hello [pagina di supporto tecnico di Azure](http://go.microsoft.com/fwlink/?LinkId=521878). 
> 

Concedere sandbox hello possibilità toocreate più copie della propria organizzazione in ambienti separati per diversi scopi, ad esempio sviluppo, testing e training, senza compromettere i dati hello e nelle applicazioni di produzione Salesforce organizzazione.  

Per ulteriori informazioni, vedere [Panoramica di Sandbox](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

* Sottoscrizione di Azure valida
* Sandbox in Salesforce.com

Se non si dispone di un ambiente sandbox valido in Salesforce.com, è necessario toocontact Salesforce.

scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:

1. Abilitazione hello di integrazione dell'applicazione per Salesforce Sandbox
2. Configurazione dell'accesso Single Sign-On (SSO)
3. Abilitazione del dominio
4. Configurazione del provisioning utente
5. Assegnazione degli utenti

![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a>Abilitare l'integrazione dell'applicazione hello per Salesforce Sandbox
obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione hello tooenable per Salesforce sandbox.

**integrazione dell'applicazione hello tooenable per Salesforce sandbox, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
   ![Applicazioni](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applicazioni")
4. hello tooopen **raccolta di applicazioni**, fare clic su **Aggiungi un'App**, quindi fare clic su **aggiungere un'applicazione per my toouse organizzazione**.
   
   ![Cosa si desidera toodo? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Cosa si desidera toodo?")
5. In hello **casella di ricerca**, tipo **Salesforce Sandbox**.
   
   ![Raccolta di applicazioni](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Raccolta di applicazioni")
6. Nel riquadro risultati hello selezionare **Salesforce Sandbox**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")
   
## <a name="configur-single-sign-on-sso"></a>Configurare l'accesso Single Sign-On (SSO)

obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooSalesforce con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.

**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, in hello hello **Salesforce Sandbox** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configurare l'accesso Single Sign-On")
2. In hello **come si sarebbe ad esempio utenti toosign su tooSalesforce Sandbox** selezionare **Microsoft Azure AD Single Sign-On**, quindi fare clic su **Avanti**.
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")
3. In hello **Configura URL App** pagina hello **URL di accesso** casella di testo, digitare l'URL usando hello modello `http://company.my.salesforce.com`e quindi fare clic su **Avanti**.
   
   ![Configurare l'URL dell'app](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configurare l'URL dell'app")
4. Se già stato configurato single sign-on per un'altra istanza di Salesforce Sandbox nella directory, quindi è necessario configurare anche hello **identificatore** toohave hello stesso valore di hello **URL di accesso**. 
 * Hello **identificatore** trovato controllando hello **Mostra impostazioni avanzate** casella di controllo hello **Configura URL App** pagina della finestra di dialogo hello.
5. In hello **Configura accesso single sign-on in Salesforce Sandbox** pagina, fare clic su **Scarica certificato**e quindi salvare il file di certificato hello nel computer in uso.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configurare l'accesso Single Sign-On")
6. In un'altra finestra del Web browser accedere al sito aziendale di Salesforce Sandbox come amministratore.
7. Scegliere dal menu hello in primo piano hello **installazione**.
   
   ![Installazione](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Installazione")
8. Nel riquadro di spostamento hello hello sinistra, fare clic su **controlli di sicurezza**, quindi fare clic su **Single Sign-On Settings**.
   
   ![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")
9. Nella sezione Impostazioni di Single Sign-On hello, eseguire hello alla procedura seguente:
   
   ![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")  
 1.  Selezionare **Abilitato SAML**. 
 2.  Fare clic su **New**.
10. Nella sezione SAML Single Sign-On Settings hello, eseguire hello alla procedura seguente:
    
    ![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")  
 1. Nella casella di testo Nome hello, digitare il nome di hello della configurazione di hello (ad esempio: *SPSSOWAAD\_Test*). 
 2. Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Salesforce Sandbox** pagina finestra di dialogo, hello copia **URL autorità di certificazione** valore e quindi incollarlo hello **dell'autorità di certificazione**casella di testo.
 3. In hello **Id entità** casella tipo **https://test.salesforce.com** se si tratta di hello prima Salesforce Sandbox istanza che si sta aggiungendo tooyour directory. Se esiste già un'istanza di Salesforce Sandbox, quindi per hello **ID entità** tipo di hello **URL di accesso**, che deve essere nel formato seguente:`http://company.my.salesforce.com`   
 4. Fare clic su **Sfoglia** hello tooupload scaricato certificato.  
 5. Come **tipo di identità SAML**selezionare **l'asserzione contiene l'ID di federazione di hello dall'oggetto utente hello**. 
 6. Come **SAML Identity Location**selezionare **identità si trova nell'elemento NameIdentifier hello di hello Subject statement**.
 7. Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Salesforce Sandbox** pagina finestra di dialogo, hello copia **URL accesso remoto** valore e quindi incollarlo hello **Provider di identità URL di accesso** casella di testo. 
 8. SFDC non supporta la disconnessione SAML.  In alternativa, incollare 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' in hello **Identity Provider Logout URL** casella di testo.
 9. In **Service Provider Initiated Request Binding** (Binding richiesta avviato dal provider di servizi) selezionare **HTTP POST**. 
 10. Fare clic su **Salva**.
11. Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.
    
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configurare l'accesso Single Sign-On")

## <a name="enable-your-domain"></a>Abilitare il dominio
In questa sezione si presuppone che sia già stato creato un dominio.  Per informazioni dettagliate, vedere [Definizione del nome di dominio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable il dominio, eseguire hello alla procedura seguente:**

1. Nel riquadro di spostamento a sinistra di hello, fare clic su **Gestione dominio**, quindi fare clic su **risorse del dominio.**
   
   ![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")
   
   >[!NOTE]
   >Assicurarsi che il dominio sia stato configurato correttamente. 
   > 
2. In hello **Login Page Settings** fare clic su **modifica**, quindi, come **servizio di autenticazione**, selezionare il nome di hello di hello impostazione SAML Single Sign-On da hello precedente sezione e infine fare clic su **salvare**.
   
   ![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")

Non appena si dispone di un dominio configurato, gli utenti devono usare Salesforce sandbox di hello dominio URL toologin toohello.  

valore di hello tooget dell'URL di hello, selezionare il profilo SSO hello creato nella sezione precedente hello.

## <a name="configure-user-provisioning"></a>Configura provisioning utenti
obiettivo di Hello di questa sezione è toooutline tooenable provisioning utente dell'utente di Active Directory come account di tooSalesforce Sandbox.

**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**

1. Nel portale Salesforce hello, nella barra di spostamento superiore hello, selezionare il nome tooexpand nel menu utente:
   
   ![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")
2. Nel menu utente selezionare **impostazioni personali** tooopen il **impostazioni personali** pagina.
3. Nel riquadro di sinistra hello, fare clic su **personale** tooexpand hello sezione personale e quindi fare clic su **Reimposta Token di sicurezza personale**:
   
   ![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")
4. In hello **Reimposta Token di sicurezza personale** pagina, fare clic su **Reimposta Token di sicurezza** toorequest un messaggio di posta elettronica che contiene il token di sicurezza di Salesforce.com.
   
   ![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")
5. Verificare nella cartella Posta in arrivo la presenza di un messaggio da Salesforce.com con oggetto analogo a "**conferma di sicurezza di salesforce.com.com**".
6. Esaminare il messaggio di posta elettronica e copia hello sicurezza valore del token.
7. Nel portale di Azure classico, in hello hello **salesforce Sandbox** pagina di integrazione dell'applicazione, fare clic su **Configura provisioning utente** tooopen hello **Configura Provisioning utente**finestra di dialogo.
   
   ![Configurare il provisioning degli utenti](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configurare il provisioning degli utenti")
8. In hello **immettere il Salesforce Sandbox credenziali tooenable il provisioning utente automatico** fornire hello le impostazioni di configurazione seguente:
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")   
 1. In hello **nome utente di amministratore Sandbox Salesforce** casella di testo, tipo di un ambiente sandbox Salesforce nome account a cui è hello **amministratore di sistema** profilo in Salesforce.com assegnato.
 2. In hello **Password amministratore Salesforce Sandbox** casella di testo, digitare la password hello per questo account.
 3. In hello **Token di sicurezza utente** casella valore del token di sicurezza hello Incolla.
 4. Fare clic su **convalida** tooverify la configurazione.
 5. Fare clic su hello **Avanti** hello tooopen pulsante **conferma** pagina.
9. In hello **conferma** pagina, fare clic su **completa** toosave la configurazione.
   
## <a name="assigning-users"></a>Assegnazione degli utenti

tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.

**gli utenti di tooassign tooSalesforce Sandbox, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico hello, creare un account di prova.
2. In hello * * Salesforce Sandbox * * pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.
   
   ![Assegnare utenti](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assegnare utenti")
3. Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.
   
   ![Sì](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Sì")

È ora necessario attendere 10 minuti e verificare che l'account di hello sia stato sincronizzato tooSalesforce Sandbox.

Se si desiderano tootest le impostazioni SSO, aprire Pannello di accesso hello. Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](https://msdn.microsoft.com/library/dn308586).

