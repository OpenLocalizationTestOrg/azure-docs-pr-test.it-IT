---
title: 'Esercitazione: Integrazione di Azure Active Directory con SilkRoad Life Suite | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SilkRoad vita Suite.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a>Esercitazione: Integrazione di Azure Active Directory con SilkRoad Life Suite
obiettivo di Hello di questa esercitazione è tooshow è come toointegrate SilkRoad vita Suite con Azure Active Directory (Azure AD). 

Integrazione SilkRoad vita Suite con Azure AD fornisce hello seguenti vantaggi: 

* È possibile controllare in Azure AD che ha accesso tooSilkRoad vita Suite 
* È possibile abilitare l'utenti tooautomatically get connesso tooSilkRoad vita Suite single sign-on (SSO) con i propri account Azure AD

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti
integrazione di Azure AD con SilkRoad vita Suite tooconfigure, è necessario hello seguenti elementi:

* Sottoscrizione di Azure AD.
* Sottoscrizione di SilkRoad Life Suite abilitata per l'accesso SSO

>[!NOTE]
>hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione. 
> 

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

* Non usare l'ambiente di produzione, a meno che non sia necessario.
* Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descrizione dello scenario
obiettivo di Hello di questa esercitazione è tooenable si tootest SSO AD Azure in un ambiente di test.

scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta gruppo vita SilkRoad dalla raccolta hello 
2. Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD

## <a name="add-silkroad-life-suite-from-hello-gallery"></a>Aggiungere il gruppo di vita SilkRoad dalla raccolta hello
integrazione hello tooconfigure di SilkRoad vita Suite in Azure AD, è necessario tooadd SilkRoad vita gruppo dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd SilkRoad vita Suite dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**. 
   
    ![Active Directory][1]

2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.

3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Applicazioni][2]

4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
    ![Applicazioni][3]

5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
    ![Applicazioni][4]

6. Nella casella di ricerca hello, digitare **SilkRoad vita Suite**.
   
    ![Applicazioni][5]

7. Nel riquadro risultati hello selezionare **SilkRoad vita Suite**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
    ![Applicazioni][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
obiettivo di Hello di questa sezione è tooshow come tooconfigure e SSO AD Azure con SilkRoad vita Suite di test basato su un utente di test denominato "Britta Simon".

Per toowork SSO, Azure AD deve tooknow è quale utente controparte hello utente tooan SilkRoad vita Suite in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello SilkRoad vita Suite deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** SilkRoad vita Suite.

tooconfigure e prova AD Azure single sign-on con SilkRoad vita Suite, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure single sign-on AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test SilkRoad vita Suite](#creating-a-silkroad-life-suite-test-user)**  -toohave un equivalente di Britta Simon SilkRoad vita Suite rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di accesso single sign-on](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD
obiettivo di Hello di questa sezione è tooenable SSO AD Azure nel portale di Azure classico hello e tooconfigure SSO nell'applicazione SilkRoad vita Suite.

**tooconfigure AD Azure single sign-on con SilkRoad vita Suite eseguire hello alla procedura seguente:**

1. Sito dell'azienda SilkRoad tooyour accesso come amministratore. 

  >[!NOTE] 
  > tooobtain accesso toohello applicazione SilkRoad vita Suite autenticazione per configurare la federazione con Microsoft Azure AD, contattare il supporto SilkRoad o il rappresentante SilkRoad servizi.
  > 

2. Andare troppo**Provider di servizi**, quindi fare clic su **federazione dettagli**. 
   
    ![Single Sign-On di Microsoft Azure AD][10] 

3. Fare clic su **scaricare i metadati della federazione**e quindi salvare il file di metadati hello nel computer in uso.
   
    ![Single Sign-On di Microsoft Azure AD][11] 

4. Nel portale di Azure classico, in hello hello **SilkRoad vita Suite** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On**  finestra di dialogo.
   
    ![Configura accesso Single Sign-On][6] 

5. In hello **come si sarebbe ad esempio utenti toosign su tooSilkRoad vita Suite** selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**.
   
    ![Single Sign-On di Microsoft Azure AD][7] 

6. In hello **Configura impostazioni App** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Single Sign-On di Microsoft Azure AD][8]   
 1. In hello **URL di accesso** casella di testo, digitare l'URL hello utilizzato dal sito SilkRoad vita Suite tooyour toosign-on agli utenti (ad esempio: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).  
 2. Aprire hello scaricato **Silkroad** file di metadati. 
 3. Individuare hello **AssertionConsumerService** tag e quindi hello copia **percorso** attributo.         
   
    ![Single Sign-On di Microsoft Azure AD][21] 
 4. Incollare il valore di hello hello **URL di risposta** casella di testo.  
 5. Fare clic su **Avanti**.

6. In hello **Configura accesso single sign-on SilkRoad vita Suite** eseguire hello alla procedura seguente:
   
    ![Single Sign-On di Microsoft Azure AD][9]  
 1. Fare clic su Download certificate e quindi salvare il file hello nel computer in uso.  
 2. Fare clic su **Avanti**.

7. Nell'applicazione **SilkRoad**, fare clic su **Authentication Sources** (Origini autenticazione).
   
    ![Single Sign-On di Microsoft Azure AD][12] 

8. Fare clic su **Add Authentication Source**(Aggiungi origine autenticazione). 
   
    ![Single Sign-On di Microsoft Azure AD][13] 

9. In hello **Aggiungi origine autenticazione** seguire hello alla procedura seguente: 
   
    ![Single Sign-On di Microsoft Azure AD][14]  
 1. In **opzione 2 - File di metadati**, fare clic su **Sfoglia** hello tooupload scaricato i file di metadati.  
 2. Fare clic su **Create Identity Provider using File Data**.

10. In hello **origini di autenticazione** fare clic su **modifica**. 
    
     ![Single Sign-On di Microsoft Azure AD][15] 

11. In hello **Modifica autenticazione origine** finestra di dialogo, eseguire hello alla procedura seguente: 
    
     ![Single Sign-On di Microsoft Azure AD][16] 
 1. In **Enabled** (Attivo) selezionare **Yes** (Sì).   
 2. In hello **descrizione IdP** casella di testo, digitare una descrizione per la configurazione (ad esempio: *SSO AD Azure*).  
 3. In hello **nome IdP** casella di testo, digitare un nome di configurazione tooyour specifico (ad esempio: *Azure SP*).  
 4. Fare clic su **Salva**.

12. Disabilitare tutte le altre origini di autenticazione. 
    
     ![Single Sign-On di Microsoft Azure AD][17]

13. Nel portale di Azure classico, in hello hello **Single sign-on conferma** pagina, fare clic su **Avanti**.  
    
     ![Single Sign-On di Microsoft Azure AD][18]

14. In hello **Single sign-on conferma** pagina, fare clic su **completa**.
    
     ![Single Sign-On di Microsoft Azure AD][19]

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure classico chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][20]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.

3. Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**. 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente: 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. In Tipo di utente selezionare Nuovo utente nell'organizzazione.  
 2. In nome utente hello **textbox**, tipo **BrittaSimon**. 
 3. Fare clic su **Avanti**.

6. In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente: 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. In hello **nome** casella tipo **Laura**.    
 2. In hello **cognome** casella di testo, tipo, **Simon**. 
 3. In hello **nome visualizzato** casella tipo **Britta Simon**. 
 4. In hello **ruolo** elenco, selezionare **utente**.
 5. Fare clic su **Avanti**.

7. In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. Annotare il valore di hello di hello **nuova Password**. 
 2. Fare clic su **Complete**.   

### <a name="create-a-silkroad-life-suite-test-user"></a>Creare un utente test di SilkRoad Life Suite
obiettivo di Hello di questa sezione è un utente denominato Britta Simon SilkRoad vita Suite toocreate. Laura deve avere un ID di SSO (talvolta tooas un *AuthParam*) corrispondente di Laura **emailaddress** in Azure AD.

**un utente denominato Britta Simon SilkRoad vita Suite, toocreate eseguire hello alla procedura seguente:**

- Chiedere a un utente che ha il toocreate team di supporto SilkRoad vita Suite **ID SSO** hello attributo lo stesso valore hello **emailaddress** di Britta Simon in Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD
obiettivo Hello di questa sezione è tooenable Britta Simon toouse SSO Azure concedendo proprio tooSilkRoad accesso vita Suite.

![Assegna utente][200] 

**tooassign Britta Simon tooSilkRoad vita Suite, eseguire hello alla procedura seguente:**

1. In hello Azure portale classico, visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **SilkRoad vita Suite**.
   
    ![Assegna utente][202] 

3. Scegliere dal menu hello in primo piano hello **utenti**.
   
    ![Assegna utente][203] 

4. Nell'elenco di utenti hello, selezionare **Britta Simon**.

5. Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.
   
    ![Assegna utente][205]

### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On
obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.  

Quando si fa clic su riquadro SilkRoad vita Suite hello in hello Pannello di accesso, è necessario ottenere un'applicazione SilkRoad vita Suite tooyour firmato in automaticamente.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





