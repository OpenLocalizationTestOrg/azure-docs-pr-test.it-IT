---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP HANA | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SAP HANA.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a>Esercitazione: Integrazione di Azure Active Directory con SAP HANA

In questa esercitazione, è illustrato come toointegrate SAP HANA con Azure Active Directory (Azure AD).

Integrazione di SAP HANA con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooSAP HANA
- È possibile abilitare l'utenti tooautomatically get connesso tooSAP HANA (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con SAP HANA tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di SAP HANA abilitata per l'accesso Single Sign-On
- Istanza di HANA in esecuzione in qualsiasi VM IaaS pubblica, locale o di Azure oppure in istanze di grandi dimensioni di SAP in Azure
- Interfaccia Web di amministrazione XSA Hello nonché HANA Studio installato nell'istanza HANA hello.

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione di SAP HANA. Prima di tutto testare integrazione hello nello sviluppo e gestione temporanea di ambiente dell'applicazione hello e quindi utilizzare hello ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di SAP HANA dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-sap-hana-from-hello-gallery"></a>Aggiunta di SAP HANA dalla raccolta hello
integrazione hello tooconfigure di SAP HANA in Azure AD, è necessario tooadd SAP HANA dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd SAP HANA dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **SAP HANA**selezionare **SAP HANA** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd. 

    ![Nuova applicazione Hello](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAP HANA usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in SAP HANA è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in SAP HANA deve toobe stabilita.

In SAP HANA, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con SAP HANA, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test SAP HANA](#creating-a-sap-hana-test-user)**  -toohave un equivalente di Britta Simon in SAP HANA che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione SAP HANA.

**Azure AD tooconfigure single sign-on con SAP HANA, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **SAP HANA** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. In hello **URL e SAP HANA dominio** seguire hello alla procedura seguente:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    a. In hello **identificatore** casella di testo, tipo:`HA100` 

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con URL di risposta e identificatore effettivo hello. Contatto [team di supporto di SAP HANA Client](https://cloudplatform.sap.com/contact.html) tooget questi valori. 

4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    >Se il certificato non è attivo renderlo attivo facendo hello "creare nuovo certificato active" casella di controllo in hello Azure AD. 

5. Applicazione SAP HANA prevede asserzioni SAML hello in un formato specifico. Hello seguente schermata mostra un esempio per questo oggetto. Di seguito è stato eseguito il mapping hello **identificatore utente** con **ExtractMailPrefix()** funzione **user.mail**. In questo modo il valore di prefisso hello messaggi di posta elettronica dell'utente hello che è hello ID utente univoco. Viene inviato toohello applicazione SAP HANA in ogni risposta con esito positivo.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo:

    a. In hello **identificatore utente** elenco a discesa, seleziona **ExtractMailPrefix**.
    
    b. In hello **posta** elenco a discesa, seleziona **user.mail**.

7. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. tooconfigure single sign-on sul **SAP HANA** lato, account di accesso tooyour **HANA XSA Web Console** esplorando toohello rispettivi endpoint HTTPS.

    > [!Note]
    > Nella configurazione predefinita di hello, hello URL reindirizza hello richiesta tooa schermata di accesso, che richiede credenziali hello di un processo accesso autenticato di SAP HANA database utente toocomplete hello. utente di Hello che effettua l'accesso deve disporre di attività di amministrazione di hello privilegi necessari tooperform SAML.

9. Nell'interfaccia Web XSA hello, passare troppo**Provider di identità SAML** e da lì, fare clic su hello **"+"** -pulsante nella parte inferiore di hello del riquadro di aggiungere informazioni sul Provider di identità di hello schermata toodisplay hello ed eseguire Hello alla procedura seguente:

    ![Aggiungi provider di identità](./media/active-directory-saas-saphana-tutorial/sap1.png)

    a. In hello **aggiungere informazioni sul Provider di identità** riquadro contenuto di hello Incolla di hello Metadata XML, che è stato scaricato dal portale di Azure in hello **metadati** casella di testo.

    ![Impostazioni di aggiunta del provider di identità](./media/active-directory-saas-saphana-tutorial/sap2.png)

    b. Se il contenuto di hello del documento XML hello è valido, hello analisi del processo estrae tooinsert informazioni necessarie hello in hello **oggetto, ID entità e dell'autorità di certificazione** campi di dati generale hello area dello schermo e hello campi URL hello Schermata area di destinazione, ad esempio,  **URL di Base e l'URL di ADFS (*)**.

    ![Impostazioni di aggiunta del provider di identità](./media/active-directory-saas-saphana-tutorial/sap3.png)

    c. Nella casella Nome hello di hello dati generale area dello schermo, immettere un nome per il nuovo provider di identità SAML SSO di hello.

    > [!Note]
    > nome Hello del provider di identità SAML hello è obbligatoria e deve essere univoco. viene visualizzato nell'elenco hello di IDPs SAML disponibili che è visibile, se si seleziona SAML come metodo di autenticazione hello per toouse applicazioni SAP HANA XS, ad esempio, nell'area dello schermo di autenticazione hello hello XS artefatto dello strumento di amministrazione.

10. Salvare i dettagli di hello del nuovo provider di identità SAML hello. Scegliere **salvare** toosave hello dettagli del provider di identità SAML hello e hello nuovo provider di identità SAML toohello elenco di noti IDPs SAML.

    ![Pulsante per il salvataggio](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. In Studio HANA all'interno delle proprietà di sistema hello di hello **configurazione** scheda, filtrare solo le impostazioni da **saml** e regolare hello **assertion_timeout** da **10 sec** troppo**120 secondi**.

    ![Impostazione assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-sap-hana-test-user"></a>Creazione di un utente di test di SAP HANA

toolog agli utenti di Azure AD tooenable in tooSAP HANA, è necessario eseguirne il provisioning in SAP HANA.
SAP HANA supporta il provisioning JIT, abilitato per impostazione predefinita.

Se è necessario un utente toocreate manualmente, eseguire hello alla procedura seguente:

>[!Note]
>È possibile modificare l'autenticazione di hello esterno utilizzato dall'utente hello.
Gli utenti esterni vengono autenticati mediante un sistema esterno, ad esempio un sistema Kerberos. Per informazioni dettagliate sulle identità esterne, contattare l'[amministratore di dominio](https://cloudplatform.sap.com/contact.html).

1. Aprire hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) come amministratore e abilitare hello database utente per SSO SAML.

    ![crea utente](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. Segni di graduazione hello casella di controllo invisibile toohello a sinistra della **SAML** e seguire il collegamento di configurazione hello.

3. Fare clic su **Aggiungi** tooadd hello provider di identità SAML e fare clic su **OK** selezionando hello provider di identità SAML appropriato.

4. Aggiungere hello **identità esterna** (es. BrittaSimon) oppure scegliere **"Any"** (Qualsiasi) e fare clic su **OK**.

    >[!Note]
    >Se "ANY" casella di controllo è deselezionata, il nome utente hello in HANA deve tooexactly corrispondenza hello nome utente hello in hello UPN prima il suffisso di dominio hello (vale a dire BrittaSimon@contoso.com diventerebbe BrittaSimon in HANA).

5. A scopo di test, assegnare tutte **"XS"** utente toohello ruoli.

    ![assegnazione di ruoli](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > È consigliabile assegnare solo le autorizzazioni appropriate per il caso d'uso.

6. Salvare utente hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSAP HANA.

![Assegnazione del ruolo utente hello][200] 

**tooassign Britta Simon tooSAP HANA, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **SAP HANA**.

    ![Assegna utente](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro SAP HANA hello in hello Pannello di accesso, è necessario ottenere l'applicazione SAP HANA tooyour automaticamente firmato-on.
Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

