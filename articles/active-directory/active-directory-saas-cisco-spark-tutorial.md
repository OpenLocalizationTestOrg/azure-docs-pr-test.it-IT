---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cisco Spark | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Spark Cisco.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a>Esercitazione: Integrazione di Azure Active Directory con Cisco Spark

In questa esercitazione, è illustrato come toointegrate Cisco nascita con Azure Active Directory (Azure AD).

L'integrazione di Cisco Spark in Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooCisco Spark
- È possibile abilitare l'utenti tooautomatically get connesso tooCisco Spark (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Cisco Spark tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Cisco Spark abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Cisco Spark dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-cisco-spark-from-hello-gallery"></a>Aggiunta di Cisco Spark dalla raccolta hello
integrazione hello tooconfigure di Cisco Spark in Azure AD, è necessario tooadd Cisco Spark dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Spark Cisco dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Spark Cisco**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. Nel riquadro dei risultati hello, selezionare **Spark Cisco**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Cisco Spark mediante un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Spark Cisco è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Spark Cisco deve toobe stabilita.

In Spark Cisco, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e test Azure single sign-on AD con Cisco Spark, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Spark Cisco](#creating-a-cisco-spark-test-user)**  -toohave un equivalente di Britta Simon in Spark Cisco che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Spark Cisco.

**Azure AD tooconfigure single sign-on con Cisco Spark, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Spark Cisco** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. In hello **Cisco Spark dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL come:`https://web.ciscospark.com/#/signin`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://idbroker.webex.com/<companyname>`

    > [!NOTE] 
    > Poiché non è reale, Aggiorna il valore con hello identificatore effettivo. Contatto [team di supporto Client di Spark Cisco](https://support.ciscospark.com/) tooget questo valore. 
 
4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. Applicazione di Spark Cisco prevede attributi specifici toocontain di hello asserzioni SAML. Configurare gli attributi per questa applicazione seguenti hello. È possibile gestire i valori hello di questi attributi da hello **gli attributi utente** sezione nella pagina di integrazione dell'applicazione. Hello seguente schermata mostra un esempio per questo oggetto.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine di hello precedente ed eseguire hello alla procedura seguente:
    
    | Nome attributo  | Valore attributo |
    | --------------- | -------------------- |    
    |   uid    | user.userprincipalname |   

    a. Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    b. In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.
    
    c. Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.
    
    d. Fare clic su **OK**.

7. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. Accedi troppo[Cisco Cloud collaborazione gestione](https://admin.ciscospark.com/) con le credenziali di amministratore completo.

9. Selezionare **impostazioni** in hello **autenticazione** fare clic su **modifica**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. Selezionare **Integrate a 3rd-party identity provider. (Avanzate)**  e toohello andare nella schermata successiva.

11. In hello **Import Idp Metadata** pagina entrambi trascinare e rilasciare file di metadati hello Azure AD nella pagina hello o utilizzare hello file browser opzione toolocate e caricare il file di metadati hello Azure AD. Selezionare quindi **Require certificate signed by a certificate authority in Metadata (more secure)** (Richiedi certificato firmato da un'autorità di certificazione in metadati - più sicura) e fare clic su **Next** (Avanti). 
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. Selezionare **Test SSO Connection** (Test connessione SSO) e, quando viene aperta una nuova scheda del browser, eseguire l'autenticazione con Azure AD effettuando l'accesso.

13. Restituire toohello **Cisco Cloud collaborazione gestione** scheda del browser. Se hello è stata stabilita, selezionare **questa è stata stabilita. Enable Single Sign-On**  (Test riuscito. Abilita Single Sign-On), quindi fare clic su **Next** (Avanti).

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-cisco-spark-test-user"></a>Creazione di un utente test di Cisco Spark

In questa sezione viene creato un utente di nome Britta Simon in Cisco Spark. In questa sezione viene creato un utente di nome Britta Simon in Cisco Spark.

1. Passare toohello [Cisco Cloud collaborazione gestione](https://admin.ciscospark.com/) con le credenziali di amministratore completo.

2. Fare clic su **Users** (Utenti) e quindi su **Manage Users** (Gestisci utenti).
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. In hello **Manage User** selezionare **agli utenti di modificare o aggiungere manualmente** e fare clic su **Avanti**.

4. Selezionare **Names and Email address** (Nomi e indirizzi di posta elettronica). Quindi, compilare hello casella di testo come indicato di seguito:
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    a. In hello **nome** casella tipo **Laura**. 
    
    b. In hello **cognome** casella tipo **Simon**.
    
    c. In hello **indirizzo di posta elettronica** casella tipo  **britta.simon@contoso.com** .

5. Fare clic su hello segno tooadd Britta Simon. Quindi fare clic su **Next**.

6. In hello **Aggiungi servizi per gli utenti** finestra, fare clic su **salvare** e quindi **fine**.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCisco Spark.

![Assegna utente][200] 

**tooassign Britta Simon tooCisco Spark, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Spark Cisco**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Cisco Spark hello in hello Pannello di accesso, è necessario ottenere applicazione Spark Cisco tooyour automaticamente firmato-on.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

