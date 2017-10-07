---
title: 'Esercitazione: Integrazione di Azure Active Directory con Mimecast Admin Console | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Mimecast Admin Console.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a>Esercitazione: Integrazione di Azure Active Directory con Mimecast Admin Console

In questa esercitazione, è illustrato come toointegrate Mimecast Admin Console con Azure Active Directory (Azure AD).

Integrazione di Mimecast Admin Console con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooMimecast Console di amministrazione.
- È possibile abilitare l'utenti tooautomatically get connesso tooMimecast Console di amministrazione (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Mimecast Admin Console tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Mimecast Admin Console abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Mimecast Admin Console dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a>Aggiunta di Mimecast Admin Console dalla raccolta hello
integrazione hello tooconfigure di Mimecast Admin Console in Azure AD, è necessario tooadd Mimecast Admin Console dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Mimecast Admin Console dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **Mimecast Admin Console**selezionare **Mimecast Admin Console** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Mimecast Admin Console nell'elenco risultati hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Mimecast Admin Console con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Mimecast Admin Console è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Mimecast Admin Console richiede toobe stabilita.

Nella Console di amministrazione di Mimecast, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Mimecast Admin Console, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test Mimecast Admin Console](#create-a-mimecast-admin-console-test-user)**  -toohave un equivalente di Britta Simon in Mimecast Admin Console che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Mimecast Admin Console.

**tooconfigure Azure single sign-on AD Mimecast Admin console, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Mimecast Admin Console** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. In hello **Mimecast Admin Console dominio e gli URL** seguire hello alla procedura seguente:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    In hello **Sign-on URL** casella di testo, digitare l'URL hello:
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > URL di accesso Hello è specifico dell'area.

4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. In hello **Mimecast Admin Console configurazione** fare clic su **configurare Mimecast Admin Console** tooopen **Configura sign-on** finestra. Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configurazione di Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. In un'altra finestra del Web browser accedere a Mimecast Admin Console come amministratore.

8. Andare troppo**servizi \> applicazione**.

    ![Servizi](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Servizi")

9. Fare clic su **Authentication Profiles**.

    ![Profili di autenticazione](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Profili di autenticazione")
    
10. Fare clic su **New Authentication Profile**.

    ![Nuovi profili di autenticazione](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "Nuovi profili di autenticazione")

11. In hello **Authentication Profile** seguire hello alla procedura seguente:

    ![Profilo di autenticazione](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Profilo di autenticazione")
    
    a. In hello **descrizione** casella di testo, digitare un nome per la configurazione.
    
    b. Selezionare **Enforce SAML Authentication for Mimecast Admin Console**.
    
    c. Come **Provider** selezionare **Azure Active Directory**.
    
    d. Incolla **ID entità SAML**, che è stato copiato dal portale di Azure hello in hello **URL autorità di certificazione** casella di testo.
    
    e. Incolla **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure hello in hello **URL di accesso** casella di testo.

    f. Incolla **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure hello in hello **Logout URL** casella di testo.
    
    >[!NOTE]
    >Hello URL di accesso e valore hello Logout URL sono per hello Mimecast Admin Console hello stesso.
    
    g. Aprire il certificato in base 64 scaricato dal portale di Azure nel blocco note, rimuovere prima riga hello ("*--*") e l'ultima riga hello ("*--*"), hello copia rimanente contenuto di esso negli Appunti e quindi incollarlo toohello **Identity Provider Certificate (Metadata)** casella di testo.
    
    h. Selezionare **Allow Single Sign On**.
    
    i. Fare clic su **Salva**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985) 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

   ![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.

    ![pulsante Aggiungi Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![finestra di dialogo utente Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    d. Fare clic su **Crea**.
 
### <a name="create-a-mimecast-admin-console-test-user"></a>Creare un utente test di Mimecast Admin Console

In ordine tooenable Azure AD utenti toolog in Mimecast Admin Console, è necessario eseguirne il provisioning in Mimecast Admin Console. Nel caso di hello di Mimecast Admin Console, il provisioning è un'attività manuale.

* Prima di poter creare utenti, è necessario tooregister un dominio.

**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**

1. Accesso tooyour **Mimecast Admin Console** come amministratore.
2. Andare troppo**directory \> interno**.
   
   ![Directory](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directory")
3. Fare clic su **Register New Domain**.
   
   ![Registra nuovo dominio](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Registra nuovo dominio")
4. Dopo aver creato il nuovo dominio, fare clic su **New Address**.
   
   ![Nuovo indirizzo](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "Nuovo indirizzo")
5. In hello indirizzo finestra di dialogo Nuovo, eseguire hello alla procedura seguente:
   
   ![Salvare](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Salvare")
   
   a. Hello tipo **indirizzo di posta elettronica**, **nome globale**, **Password**, e **Conferma Password** gli attributi di un annuncio di Azure valido account si vuole tooprovision in hello relative caselle di testo.

   b. Fare clic su **Salva**.

>[!NOTE]
>È possibile utilizzare qualsiasi altro strumento di creazione di account utente Mimecast Admin Console o le API fornite da account utente di Azure AD tooprovision Mimecast Admin Console. 

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooMimecast Console di amministrazione.

![Assegnazione del ruolo utente hello][200] 

**tooassign Britta Simon tooMimecast Console di amministrazione, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Mimecast Admin Console**.

    ![collegamento di Mimecast Admin Console Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Mimecast Admin Console hello in hello Pannello di accesso, è necessario ottenere applicazione Mimecast Admin Console tooyour automaticamente firmato-on.
Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

