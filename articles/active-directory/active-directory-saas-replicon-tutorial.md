---
title: 'Esercitazione: Integrazione di Azure Active Directory con Replicon | Documentazione Microsoft'
description: Informazioni su come toouse Replicon con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a>Esercitazione: Integrazione di Azure Active Directory con Replicon
obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e Replicon. scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

* Sottoscrizione di Azure valida
* Tenant Replicon

Dopo aver completato questa esercitazione, gli utenti di hello Azure AD assegnati tooReplicon saranno in grado di toosingle sign applicazione hello nel sito aziendale Replicon (accesso avviato dal provider di servizi su) o tramite hello [introduzione toohello accesso Pannello](active-directory-saas-access-panel-introduction.md).

scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:

1. Abilitazione hello di integrazione dell'applicazione per Replicon
2. Configurazione dell'accesso Single Sign-On (SSO)
3. Configurazione del provisioning utente
4. Assegnazione degli utenti

![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")

## <a name="enable-hello-application-integration-for-replicon"></a>Abilitare l'integrazione dell'applicazione per Replicon hello
obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione per Replicon tooenable hello.

**integrazione dell'applicazione hello tooenable per Replicon, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Applicazioni](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applicazioni")
4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
    ![Aggiungere un'applicazione](./media/active-directory-saas-replicon-tutorial/IC749321.png "Aggiungere un'applicazione")
5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
    ![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-replicon-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")
6. In hello **casella di ricerca**, tipo **Replicon**.
   
    ![Raccolta di applicazioni](./media/active-directory-saas-replicon-tutorial/IC777799.png "Raccolta di applicazioni")
7. Nel riquadro risultati hello selezionare **Replicon**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
    ![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")
   
## <a name="configure-single-sign-on"></a>Configura accesso Single Sign-On

obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooReplicon con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.

**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, in hello hello **Replicon** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configurare l'accesso Single Sign-On")
2. In hello **come si sarebbe ad esempio utenti toosign su tooReplicon** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configurare l'accesso Single Sign-On")
3. In hello **Configura URL App** eseguire hello alla procedura seguente:
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configurare l'URL dell'app")
  1. In hello **URL di accesso Replicon** casella di testo, digitare l'URL del tenant Replicon (ad esempio: *https://na2.replicon.com/company/saml2/sp-sso/post*).
  2. In hello **URL di risposta Replicon** casella di testo, digitare l'URL **AssertionConsumerService** URL (ad esempio: *https://global.replicon.com/!saml2/aziendale/sso/post/*).  
      
     >[!NOTE]
     >È possibile ottenere l'URL di hello dai metadati di Replicon hello in: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.
     > 
     > 
 
  3. Fare clic su **Avanti**.

4. In hello **Configura accesso single sign-on in Replicon** pagina, toodownload i metadati, fare clic su **Scarica metadati**e quindi salvare hello metadati nel computer in uso.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configurare l'accesso Single Sign-On")
5. In un'altra finestra del Web browser accedere al sito aziendale di Replicon come amministratore.

6. tooconfigure SAML 2.0, eseguire hello alla procedura seguente:
   
    ![Abilita autenticazione SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "autenticazione SAML abilitare")
  
  1. hello toodisplay **EnableSAML Authentication2** finestra di dialogo, aggiungere hello seguente URL di tooyour, dopo la chiave dell'azienda: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**  
    * Hello il seguente schema hello dell'URL completo di hello:  
   **https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**
   2. Fare clic su hello  **+**  tooexpand hello **v20Configuration** sezione.
   3. Fare clic su hello  **+**  tooexpand hello **metaDataConfiguration** sezione.
   4. Fare clic su **Scegli File**, tooselect del file XML dei metadati del provider di identità e scegliere **Invia**.

7. Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configurare l'accesso Single Sign-On")
   
## <a name="configure-user-provisioning"></a>Configura provisioning utenti

In ordine tooenable Azure AD utenti toolog a Replicon, è necessario eseguirne il provisioning in Replicon.  

Nel caso di hello di Replicon, il provisioning è un'attività manuale.

**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**

1. In una finestra del Web browser accedere al sito aziendale di Replicon come amministratore.
2. Andare troppo**amministrazione \> utenti**.
   
    ![Utenti](./media/active-directory-saas-replicon-tutorial/IC777806.png "Utenti")
3. Fare clic su **+Aggiungi utente**.
   
    ![Aggiungere un utente](./media/active-directory-saas-replicon-tutorial/IC777807.png "Aggiungere un utente")
4. In hello **profilo utente** seguire hello alla procedura seguente:
   
    ![Profilo utente](./media/active-directory-saas-replicon-tutorial/IC777808.png "Profilo utente")
   
  1. In hello **nome account di accesso** casella di testo, hello tipo AD Azure indirizzo di posta elettronica dell'utente hello Azure AD si vuole tooprovision.
  2. In **Tipo di autenticazione** selezionare **SSO**.
  3. In hello **reparto** casella di testo, digitare il reparto dell'utente hello.
  4. In **Tipo di dipendente** selezionare **Amministratore**.
  5. Fare clic su **Salva profilo utente**.

>[!NOTE]
>È possibile usare qualsiasi altro Replicon utente account strumento di creazione o le API fornite da Replicon tooprovision account utente di AAD.
> 
> 

## <a name="assign-users"></a>Assegna utenti
tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.

**tooassign tooReplicon di utenti, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico hello, creare un account di prova.

2. In hello **Replicon** pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.
   
    ![Assegnare utenti](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assegnare utenti")

3. Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.
   
    ![Sì](./media/active-directory-saas-replicon-tutorial/IC767830.png "Sì")

Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello. Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

