---
title: 'Esercitazione: Integrazione di Azure Active Directory con Amazon Web Service (AWS) | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Amazon Web Services (AWS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a>Esercitazione: Integrazione di Azure Active Directory con Amazon Web Service (AWS)

In questa esercitazione, è illustrato come toointegrate Amazon Web Services (AWS) con Azure Active Directory (Azure AD).

Integrazione di Amazon Web Services (AWS) con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooAmazon Web Services (AWS)
- È possibile abilitare l'utenti tooautomatically get connesso tooAmazon Web Services (AWS) (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Amazon Web Services (AWS) tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione Amazon Web Service (AWS) abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Amazon Web Services (AWS) dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a>Aggiunta di Amazon Web Services (AWS) dalla raccolta hello
integrazione di hello di tooconfigure di Amazon Web Services (AWS) in Azure AD, è necessario tooadd Amazon Web Services (AWS) dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Amazon Web Services (AWS) dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Amazon Web Services (AWS)**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. Nel riquadro dei risultati hello, selezionare **Amazon Web Services (AWS)**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Amazon Web Services (AWS) usando un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello Amazon Web Services (AWS) è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello Amazon Web Services (AWS) richiede toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** Amazon Web Services (AWS).

tooconfigure e test di Azure AD single sign-on con Amazon Web Services (AWS), è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente di test di Amazon Web Services](#creating-an-amazon-web-services-test-user)**  -toohave un equivalente di Britta Simon Amazon Web Services (AWS) che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Amazon Web Services (AWS).

**tooconfigure AD Azure single sign-on con Amazon Web Services (AWS), eseguire hello alla procedura seguente:**

1. Nel portale di Azure, di hello in hello **Amazon Web Services (AWS)** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. In hello **Amazon Web Services (AWS) dominio e gli URL** sezione, hello utente non dispone di tooperform tutte le operazioni come l'applicazione hello è già pre-integrata con Azure.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. applicazione Software Amazon Web Services (AWS) Hello prevede asserzioni SAML hello in un formato specifico. Configurare hello seguendo le attestazioni per questa applicazione. È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione. Hello seguente schermata mostra un esempio per questo oggetto.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine di hello precedente ed eseguire hello alla procedura seguente:
    
    | Nome attributo  | Valore attributo | Spazio dei nomi |
    | --------------- | --------------- | --------------- |
    | RoleSessionName | user.userprincipalname | https://AWS.Amazon.com/SAML/Attributes |
    | Ruolo            | user.assignedroles |  https://AWS.Amazon.com/SAML/Attributes |
    
    >[!TIP]
    >È necessario il provisioning in Azure AD toofetch tutti i ruoli di hello dalla Console di AWS degli utenti tooconfigure hello. Consultare hello provisioning passaggi riportati di seguito.

    a. Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    b. In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    c. Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga. Aggiungere il valore di Namespace hello come indicato in precedenza.
    
    d. Fare clic su **OK**.

7. Fare clic su **salvare** pulsante Impostazioni hello toosave in Azure.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. In un'altra finestra del browser del sito della società di Amazon Web Services (AWS) tooyour sign-on come amministratore.

9. Fare clic su **Console Home**.
   
    ![Configura accesso Single Sign-On][11]

10. Fare clic su **IAM** dal servizio **Sicurezza, identità e conformità**.
   
    ![Configura accesso Single Sign-On][12]

11. Fare clic su **Provider di identità** e quindi fare clic su **Create Provider** (Crea provider).
   
    ![Configura accesso Single Sign-On][13]

12. In hello **configurare Provider** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Configura accesso Single Sign-On][14]
 
    a. In **Tipo provider** selezionare **SAML**.

    b. In hello **nome Provider** casella di testo, digitare un nome di provider (ad esempio: *WAAD*).

    c. tooupload file di metadati scaricato, fare clic su **Scegli File**.

    d. Fare clic su **Next Step**.

13. In hello **verificare le informazioni sul Provider** nella pagina, fare clic su **crea**. 
    
    ![Configura accesso Single Sign-On][15]

14. Fare clic su **Ruoli** e quindi fare clic su **Crea nuovo ruolo**. 
    
    ![Configura accesso Single Sign-On][16]

15. In hello **imposta il nome del ruolo** finestra di dialogo, eseguire hello alla procedura seguente: 
    
    ![Configura accesso Single Sign-On][17] 

    a. In hello **nome ruolo** casella di testo, digitare un nome di ruolo (ad esempio: *TestUser*). 

    b. Fare clic su **Next Step**.

16. In hello **Seleziona tipo di ruolo** finestra di dialogo, eseguire hello alla procedura seguente: 
    
    ![Configura accesso Single Sign-On][18] 

    a. Selezionare **Role For Identity Provider Access**. 

    b. In hello **Grant Web Single Sign-On (WebSSO) provider tooSAML accesso** fare clic su **selezionare**.

17. In hello **stabilire Trust** finestra di dialogo, eseguire hello alla procedura seguente:  
    
    ![Configura accesso Single Sign-On][19] 

    a. Come provider SAML, selezionare provider SAML hello creato in precedenza (ad esempio: *WAAD*)
  
    b. Fare clic su **Next Step**.

18. In hello **verificare Trust ruolo** finestra di dialogo, fare clic su **passaggio successivo**.
    
    ![Configura accesso Single Sign-On][32]

19. In hello **collegare criteri** finestra di dialogo, fare clic su **passaggio successivo**.
    
    ![Configura accesso Single Sign-On][33]

20. In hello **revisione** finestra di dialogo, eseguire hello alla procedura seguente:
    
    ![Configura accesso Single Sign-On][34]
 
    a. Fare clic su **Crea ruolo**.

    b. Creare tutti i ruoli in base alle esigenze ed eseguirne il mapping toohello Provider di identità.

21. Configurare tutti i ruoli di hello di AWS toofetch il provisioning degli utenti hello

    a. In accesso alla Console di AWS hello con l'account radice

    b. In hello angolo superiore destro, fare clic sul nome e quindi fare clic su hello **le credenziali di sicurezza personale** opzione. Verrà aperta una schermata come messaggio di avviso. Fare clic sul pulsante hello **le credenziali di sicurezza** toopass pulsante hello dello schermo.
        
       ![Configura accesso Single Sign-On][36]

       ![Configura accesso Single Sign-On][37]

    c. In hello chiavi di accesso fare clic su hello **Crea nuova chiave di accesso** pulsante. Questo genera hello ID chiave di accesso e un valore di token.
    
       ![Configura accesso Single Sign-On][38]

    d. Copiare entrambi questi valori e scaricarli, in modo da non perderli.

    e. In hello portale di Azure, nella pagina di integrazione dell'applicazione hello Amazon Web Services (AWS), fare clic su **Provisioning**.
        
       ![Configura accesso Single Sign-On][35]

    f. Impostare la modalità di Provisioning hello troppo**automatico**
        
       ![Configura accesso Single Sign-On][39]

    g. Ora in hello **clientsecret** e **segreto Token** incollare hello corrispondenti valori che è stato copiato dalla Console di AWS.
    
    h. È possibile fare clic su hello **Test connessione** pulsante connettività hello tootest. Una volta che ha esito positivo è possibile avviare hello provisioning connettore.
       
       ![Configura accesso Single Sign-On][40]

    i. Ora abilitare lo stato di Provisioning hello troppo**su**. Verrà avviato il recupero dei ruoli hello da un'applicazione hello.

       ![Configura accesso Single Sign-On][41]

    > [!NOTE]
    > Viene eseguito il servizio Azure Provisioning AD ogni dopo alcuni ruoli di hello ora toosync da AWS. Dovrebbe essere hello tutti i Provider di identità associati ruoli AWS in Azure AD e di utilizzarli durante l'assegnazione toousers applicazione hello o gruppi.

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-an-amazon-web-services-test-user"></a>Creazione di un utente test in Amazon Web Service

In ordine tooenable Azure AD utenti toolog in tooAmazon Web Services (AWS), è necessario che eseguirne il provisioning in Amazon Web Services (AWS). In caso di hello di Amazon Web Services (AWS), il provisioning è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour **Amazon Web Services (AWS)** sito aziendale come amministratore.

2. Fare clic su hello **Home Console** icona. 
   
    ![Configura accesso Single Sign-On][11]

3. Fare clic su Identity and Access Management. 
   
    ![Configura accesso Single Sign-On][28]

4. In hello Dashboard, fare clic su **utenti**, quindi fare clic su **creare nuovi utenti**. 
   
    ![Configura accesso Single Sign-On][29]

5. Nella finestra di dialogo Crea utente hello eseguire hello alla procedura seguente: 
   
    ![Configura accesso Single Sign-On][30]   
    
    a. In hello **immettere i nomi utente** nelle caselle di testo, digitare il nome utente Brita Simon (userprincipalname) in Azure AD.

    b. Fare clic su **Crea**.
        
### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo proprio tooAmazon accesso Web Services (AWS).

![Assegna utente][200] 

**tooassign Britta Simon tooAmazon Web Services (AWS), eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Amazon Web Services (AWS)**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. In **selezionare il ruolo** scheda, ruolo appropriato di hello selezionare per utente hello. Tutti i ruoli vengono visualizzati con il nome di ruolo hello e il nome del provider di identità. In questo modo è possibile identificare facilmente i ruoli di hello da AWS.

8. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello Amazon Web Services (AWS) riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Amazon Web Services (AWS). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
