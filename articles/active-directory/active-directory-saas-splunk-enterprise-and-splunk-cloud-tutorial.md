---
title: 'Esercitazione: Integrazione di Azure Active Directory con Splunk Enterprise e Splunk Cloud | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed Splunk Enterprise e Splunk Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a>Esercitazione: Integrazione di Azure Active Directory con Splunk Enterprise e Splunk Cloud

In questa esercitazione, è illustrato come toointegrate Splunk Enterprise e Splunk Cloud con Azure Active Directory (Azure AD).

Integrazione di Splunk Enterprise e Splunk Cloud con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso Enterprise tooSplunk e Splunk Cloud
- È possibile abilitare l'utenti tooautomatically get connesso tooSplunk Splunk Cloud e Enterprise single sign-on (SSO) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Splunk Enterprise e Splunk Cloud tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Splunk Enterprise o Splunk Cloud abilitata per l'accesso SSO


>[!NOTE]
>hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.
>

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.

scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Splunk Enterprise e Splunk Cloud dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a>Aggiungere Splunk Enterprise e Splunk Cloud dalla raccolta di hello
integrazione hello tooconfigure di Splunk Enterprise e Splunk Cloud in Azure AD, è necessario tooadd Splunk Enterprise Splunk Cloud dall'elenco di tooyour hello raccolta di App e gestite SaaS.

**tooadd Splunk Enterprise e Splunk Cloud dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.

    ![Active Directory][1]

2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.

3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.

    ![Applicazioni][2]

4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.

    ![Applicazioni][3]

5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.

    ![Applicazioni][4]

6. Nella casella di ricerca hello, digitare **Splunk Enterprise o Splunk Cloud**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. Nel riquadro dei risultati di hello, selezionare **Splunk Enterprise e Splunk Cloud**, quindi fare clic su **completa** tooadd un'applicazione hello.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Splunk Enterprise e Splunk Cloud con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Splunk Enterprise e Splunk Cloud è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Splunk Enterprise e Splunk Cloud deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** Splunk Enterprise e Splunk Cloud.

tooconfigure e prova AD Azure single sign-on con Splunk Enterprise e Splunk Cloud, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure single sign-on AD](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Splunk Enterprise e Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave un equivalente di Britta Simon Splunk azienda e Splunk Cloud toohello collegato AD Azure rappresentazione dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di accesso single sign-on](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione abilitare SSO AD Azure nel portale classico hello e configurare SSO nell'applicazione Splunk Enterprise e Splunk Cloud.


**tooconfigure AD Azure single sign-on con Splunk Enterprise e Splunk Cloud, eseguire hello alla procedura seguente:**

1. Nel portale classico hello in hello **Splunk Enterprise e Splunk Cloud** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.
     
    ![Configura accesso Single Sign-On][6] 

2. In hello **come si desidera che gli utenti toosign su tooSplunk Enterprise e Splunk Cloud** selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. In hello **Configura impostazioni App** finestra di dialogo eseguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. In hello **URL di accesso** casella di testo, digitare l'URL hello usato dall'applicazione Splunk Cloud hello modello di utilizzo e gli utenti toosign-on tooyour Splunk Enterprise:`https://<splunkserverUrl>/en-US/app/launcher/home`
  2. In hello **identificatore** casella di testo, digitare l'URL del Splunk Server hello.
  3. In hello **URL di risposta** casella di testo, digitare l'URL hello con hello seguente motivo:`https://<splunkserver>/saml/acs`
  4. Fare clic su **Avanti**.
 
4. In hello **configurare single sign-on in Splunk Enterprise e Splunk Cloud** eseguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. Fare clic su **Scarica metadati**e quindi salvare il file hello nel computer in uso.
  2. Fare clic su **Avanti**.

5. tooget SSO configurato per l'applicazione, contattare Splunk Enterprise e il team di supporto Splunk Cloud e fornire loro seguente hello:

    * Hello scaricato **federaton metadati**
6. Nel portale classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**.
    
    ![Single Sign-On di Microsoft Azure AD][10]

7. In hello **Single sign-on conferma** pagina, fare clic su **completa**.  
 
    ![Single Sign-On di Microsoft Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
In questa sezione creare un utente test nel portale classico di hello chiamato Britta Simon.

![Creare un utente di Azure AD][20]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.

3. Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. In Tipo di utente selezionare Nuovo utente nell'organizzazione.
  2. In nome utente hello **textbox**, tipo **BrittaSimon**.
  3. Fare clic su **Avanti**.

6.  In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:
  
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. In hello **nome** casella tipo **Laura**.  
  2. In hello **cognome** casella di testo, tipo, **Simon**.
  3. In hello **nome visualizzato** casella tipo **Britta Simon**.
  4. In hello **ruolo** elenco, selezionare **utente**.
  5. Fare clic su **Avanti**.

7. In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. Annotare il valore di hello di hello **nuova Password**.
  2. Fare clic su **Complete**.   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a>Creare un utente test di Splunk Enterprise e Splunk Cloud

In questa sezione viene creato un utente chiamato Britta Simon in Splunk Enterprise e Splunk Cloud. Rivolgersi Splunk Enterprise e Splunk Cloud supporto team tooadd hello utenti hello Splunk Enterprise e Splunk Cloud platform.


### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse SSOy Azure conceda proprio accesso tooSplunk Enterprise e Splunk Cloud.

![Assegna utente][200] 

**tooassign Britta Simon tooSplunk Enterprise e Splunk Cloud, eseguire hello alla procedura seguente:**

1. Nel portale classico hello, fare clic su visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello **applicazioni** nel menu superiore hello.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Splunk Enterprise e Splunk Cloud**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. Scegliere dal menu hello in primo piano hello **utenti**.

    ![Assegna utente][203]

4. Nell'elenco di utenti hello, selezionare **Britta Simon**.

5. Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.

    ![Assegna utente][205]

### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione è verificare il AD SSOonfiguration Azure tramite hello Pannello di accesso.

Quando si fa clic hello Splunk Enterprise e riquadro Splunk Cloud in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Splunk Enterprise e Splunk Cloud.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
