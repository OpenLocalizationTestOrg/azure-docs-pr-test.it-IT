---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP HANA Cloud Platform | Microsoft Docs'
description: Informazioni su come toouse SAP HANA Cloud Platform con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a>Esercitazione: Integrazione di Azure Active Directory con SAP HANA Cloud Platform
obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e SAP HANA Cloud Platform.

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

* Sottoscrizione di Azure valida
* Account di SAP HANA Cloud Platform

Dopo aver completato questa esercitazione, hello Azure AD utenti assegnati tooSAP HANA Cloud Platform sarà toosingle in grado di accesso in un'applicazione hello utilizzando hello [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

>[!IMPORTANT]
>È necessario toodeploy la propria applicazione o la sottoscrizione tooan applicazione sulla piattaforma SAP HANA Cloud singolo tootest di account di accesso. In questa esercitazione, un'applicazione viene distribuita nell'account hello.
> 
> 

scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:

1. Abilitare l'integrazione dell'applicazione hello per SAP HANA Cloud Platform
2. Configurazione dell'accesso Single Sign-On (SSO)
3. Assegnazione di un utente tooa ruolo
4. Assegnazione degli utenti

![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a>Abilitare l'integrazione dell'applicazione hello per SAP HANA Cloud Platform
obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione hello tooenable per SAP HANA Cloud Platform.

**integrazione dell'applicazione hello tooenable per SAP HANA Cloud Platform, eseguire hello alla procedura seguente:**

1. In hello portale di gestione di Azure, nel riquadro di spostamento a sinistra di hello, fare clic su **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Applicazioni](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applicazioni")
4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
    ![Aggiungere un'applicazione](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Aggiungere un'applicazione")
5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
    ![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")
6. In hello **casella di ricerca**, tipo **SAP HANA Cloud Platform**.
   
    ![Raccolta di applicazioni](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Raccolta di applicazioni")
7. Nel riquadro risultati hello selezionare **SAP HANA Cloud Platform**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
    ![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")
   
## <a name="configure-single-sign-on"></a>Configura accesso Single Sign-On

obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooSAP HANA Cloud Platform con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.

Come parte di questa procedura, è necessario tooupload un tenant di SAP HANA Cloud Platform tooyour certificato con codifica base 64.  

Se non si ha familiarità con questa procedura, vedere [come tooconvert certificato di un file binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, in hello hello **SAP HANA Cloud Platform** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On**finestra di dialogo.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configurare l'accesso Single Sign-On")
2. In hello **come si sarebbe ad esempio utenti toosign su tooSAP HANA Cloud Platform** selezionare **Microsoft Azure AD Single Sign-On**, quindi fare clic su **Avanti**.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configurare l'accesso Single Sign-On")
3. In una finestra del web browser, accedere toohello SAP HANA Cloud Platform Cockpit all'https://account. \<host orizzontale\>.ondemand.com/cockpit (ad esempio: *https://account.hanatrial.ondemand.com/cockpit*).
4. Fare clic su hello **Trust** scheda.
   
    ![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")
5. Nella sezione Gestione trust eseguire hello alla procedura seguente:
   
    ![Ottenere i metadati](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Ottenere i metadati")
   
   1. Fare clic su hello **Local Service Provider** scheda.
   2. Fare clic su hello toodownload file di metadati di SAP HANA Cloud Platform, **Get Metadata**.
6. In hello Azure attiva portale classico, in hello **Configura URL App** pagina, eseguire hello alla procedura seguente e quindi fare clic su **Avanti**.
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configurare l'URL dell'app")
   
   1. In hello **URL di accesso** hello digitare l'URL usato dal toosign gli utenti nella casella del **SAP HANA Cloud Platform** dell'applicazione. Si tratta hello URL specifico per l'account di una risorsa protetta nell'applicazione SAP HANA Cloud Platform. Hello URL si basa sul modello di hello: *https://\<applicationName\>\<accountName\>.\< host orizzontale\>.ondemand.com/\<percorso\_a\_protetti\_risorse\>*  (ad esempio: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)
      
     >[!NOTE]
     >Si tratta hello URL dell'applicazione SAP HANA Cloud Platform che richiede tooauthenticate utente hello.
     > 

   2. Aprire file di metadati di SAP HANA Cloud Platform scaricato hello e individuare hello **NS3: assertionconsumerservice** tag.
   3. Copiare il valore di hello di hello **percorso** attributo e quindi incollarlo hello **SAP HANA Cloud Platform Reply URL** casella di testo.

7. In hello **Configura accesso single sign-on in SAP HANA Cloud Platform** pagina, toodownload i metadati, fare clic su **Scarica metadati**e quindi salvare il file hello nel computer in uso.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configurare l'accesso Single Sign-On")
8. In SAP HANA Cloud Platform Cockpit Ciao hello **Local Service Provider** seguire hello alla procedura seguente:
   
    ![Gestione dell'attendibilità](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Gestione dell'attendibilità")
   
  1. Fare clic su **Modifica**.
  2. In **Configuration Type** selezionare **Custom**.
  3. Come **Local Provider Name**, lasciare il valore di predefinito hello.
  4. toogenerate un **chiave per la firma** e **certificato di firma** coppia di chiavi, fare clic su **Generate Key Pair**.
  5. In **Propagazione entità** selezionare **Disabilitato**.
  6. In **Force Authentication** selezionare **Disabled**.
  7. Fare clic su **Salva**.

9. Fare clic su hello **Trusted Identity Provider** scheda e quindi fare clic su **Add Trusted Identity Provider**.
   
    ![Gestione dell'attendibilità](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Gestione dell'attendibilità")
   
    >[!NOTE]
    >elenco di hello toomanage dei provider di identità attendibile, è necessario toohave scelto per il tipo di configurazione personalizzata hello hello sezione Local Service Provider. Per il tipo di configurazione predefinito, è necessario toohello una relazione di trust implicita e non modificabile SAP ID Service. Per Nessuno, non sono disponibili impostazioni di trust.
    > 
    > 

10. Fare clic su hello **generale** scheda e quindi fare clic su **Sfoglia** hello tooupload scaricato i file di metadati.
    
    ![Gestione dell'attendibilità](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Gestione dell'attendibilità")
    
    >[!NOTE]
    >Dopo aver caricato il file di metadati hello, hello i valori del parametro **URL servizio Single Sign-on**, **Single Logout URL** e **certificato di firma** vengono popolati automaticamente.
    > 
    > 

11. Fare clic su hello **attributi** scheda.
12. In hello **attributi** effettuare hello seguente passaggio:
    
    ![Attributi](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributi") 
  * Fare clic su **Assertion attributo**, quindi aggiungere hello gli attributi basati su asserzione seguenti:
       
    | Attributo di asserzione | Attributo di entità |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname |firstname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname |Lastname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress |email 
   
     >[!NOTE]
     >configurazione di Hello di hello attributi dipende dalla modalità hello applicazioni in HCP vengono sviluppati, ad esempio quali sono gli attributi previsti nella risposta SAML hello e con quale nome (attributo entità) accedono all'attributo nel codice hello.
     > 
     >  

    1.  Hello **l'attributo predefinito** in hello schermata è solo a scopo illustrativo. Non è richiesto di lavoro di uno scenario toomake hello.   
    2.  Hello nomi e valori per **Principal Attribute** nell'hello schermata dipendono dalla modalità di sviluppo di un'applicazione hello. È possibile che l'applicazione richieda mapping diversi.
     
13. Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in SAP HANA Cloud Platform** finestra di dialogo pagina, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa**.
    
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configurare l'accesso Single Sign-On")

###<a name="assertion-based-groups"></a>Gruppi basati su asserzione
Come passaggio facoltativo, è possibile configurare gruppi basati su asserzione per il provider di identità Azure Active Directory.

L'utilizzo di gruppi in SAP HANA Cloud Platform consente di assegnare toodynamically uno o più utenti tooone o più ruoli nelle applicazioni SAP HANA Cloud Platform, determinato dai valori di attributi in hello SAML 2.0 asserzione. 

Ad esempio, se hello l'asserzione contiene attributi hello "*contratto = temporanea*", si consiglia di tutti gli utenti interessati toobe toohello aggiunto gruppo"*TEMPORANEO*". gruppo Hello "*TEMPORANEO*" può contenere uno o più ruoli da uno o più applicazioni distribuite nell'account di SAP HANA Cloud Platform.
 
Utilizzare i gruppi basati su asserzione quando si desidera assegnare toosimultaneously molti utenti tooone o più ruoli di applicazioni nell'account di SAP HANA Cloud Platform. Se si desidera tooassign solo un singolo o piccolo numero di utenti toospecific ruoli, si consiglia di assegnarli direttamente in hello "**autorizzazioni**" scheda di SAP HANA Cloud Platform cockpit di hello.

## <a name="assign-a-role-tooa-user"></a>Assegnare un utente tooa ruolo
In ordine tooenable Azure AD utenti toolog a SAP HANA Cloud Platform, è necessario assegnare i ruoli in hello toothem di SAP HANA Cloud Platform.

**tooassign utente tooa un ruolo, eseguire hello alla procedura seguente:**

1. Accedi tooyour **SAP HANA Cloud Platform** Pannello di controllo.
2. Eseguire l'esempio hello:
   
   ![Autorizzazioni](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Autorizzazioni")
   
  1. Fare clic su **Authorization**.
  2. Fare clic su hello **utenti** scheda.
  3. In hello **utente** casella Indirizzo di posta elettronica dell'utente di tipo hello.
  4. Fare clic su **assegnare** ruolo tooa di tooassign hello utente.
  5. Fare clic su **Salva**.

## <a name="assign-users"></a>Assegna utenti
tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.

**gli utenti di tooassign tooSAP HANA Cloud Platform, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico hello, creare un account di prova.
2. In hello **SAP HANA Cloud Platform** pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.
   
   ![Assegnare utenti](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assegnare utenti")
3. Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.
   
   ![Sì](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Sì")

Se si desiderano tootest le impostazioni SSO, aprire Pannello di accesso hello. Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

