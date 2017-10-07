---
title: 'Esercitazione: Integrazione di Azure Active Directory con Qlik Sense Enterprise | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Qlik senso Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a>Esercitazione: Integrazione di Azure Active Directory con Qlik Sense Enterprise

In questa esercitazione, è illustrato come toointegrate Qlik senso Enterprise con Azure Active Directory (Azure AD).

Integrazione di Enterprise senso Qlik con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooQlik senso Enterprise.
- È possibile abilitare l'utenti tooautomatically get connesso tooQlik senso Enterprise (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Enterprise senso Qlik tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Qlik Sense Enterprise abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Qlik senso Enterprise dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a>Aggiunta di Qlik senso Enterprise dalla raccolta hello
integrazione hello tooconfigure di Qlik senso Enterprise in Azure AD, è necessario tooadd Qlik senso Enterprise dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Qlik senso Enterprise dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **Qlik senso Enterprise**selezionare **Qlik senso Enterprise** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Enterprise senso Qlik nell'elenco risultati hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Qlik Sense Enterprise con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Qlik senso Enterprise è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Qlik senso Enterprise richiede toobe stabilita.

In Enterprise senso Qlik, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Qlik senso Enterprise, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test Qlik senso Enterprise](#create-a-qlik-sense-enterprise-test-user)**  -toohave un equivalente di Britta Simon Qlik senso organizzazione che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Qlik senso Enterprise.

**tooconfigure AD Azure single sign-on con Qlik senso Enterprise, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Qlik senso Enterprise** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. In hello **Qlik senso Enterprise dominio e gli URL** seguire hello alla procedura seguente:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`
    
    > [!NOTE]
    > Si noti hello barra alla fine di hello dell'URI finale. È obbligatoria.
    
    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornamento di questi valori con hello effettivo URL Sign-On e l'identificatore, che vengono descritte più avanti in questa esercitazione o contatto [team di supporto Client di Enterprise senso Qlik](https://www.qlik.com/us/services/support) tooget questi valori. 

4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. Preparare il file di codice XML dei metadati di federazione hello in modo che è possibile caricare tale server senso tooQlik.
   
    > [!NOTE]
    > Prima di caricare hello IdP metadati toohello server Qlik senso, il file hello deve toobe modificato tooremove informazioni tooensure il corretto funzionamento tra Azure AD e ha senso Qlik server.
    
    ![Qlik Sense][qs24]
   
    a. Aprire il file FederationMetadata hello, che è stato scaricato dal portale di Azure in un editor di testo.
   
    b. Cercare il valore di hello **RoleDescriptor**.  Ci sono quattro voci (due coppie di tag di elementi di apertura e di chiusura).
   
    c. Eliminare tra i tag di elemento RoleDescriptor hello e tutte le informazioni dal file hello.
   
    d. Salvare il file hello e mantenerlo nelle vicinanze per usare più avanti in questo documento.

7. Passare toohello Qlik senso Qlik Management Console (QMC) come un utente può creare configurazioni virtuale proxy.

8. In hello QMC, fare clic su hello **virtuale proxy** voce di menu.
   
    ![Qlik Sense][qs6] 

9. In basso hello hello, fare clic su hello **Crea nuovo** pulsante.
   
    ![Qlik Sense][qs7]

10. verrà visualizzata la schermata di modifica di Hello virtuale proxy.  In hello lato destro dello schermo hello è un menu di rendere visibili le opzioni di configurazione.
   
    ![Qlik Sense][qs9]

11. Con l'opzione di menu identificazione hello selezionata, immettere informazioni di identificazione per la configurazione del proxy virtuale Azure hello hello.
    
    ![Qlik Sense][qs8]  
    
    a. Hello **descrizione** campo è un nome descrittivo per la configurazione del proxy virtuale hello.  Immettere un valore per la descrizione.
    
    b. Hello **prefisso** campo identifica l'endpoint proxy virtuale hello per la connessione tooQlik senso con Azure AD Single Sign-On.  Immettere un nome di prefisso univoco per il proxy virtuale.
    
    c. **Timeout di inattività della sessione (minuti)** timeout hello per le connessioni tramite proxy virtuale.
    
    d. Hello **nome intestazione cookie della sessione** è l'archiviazione di hello cookie nome hello identificatore di sessione per hello sessione senso Qlik un utente riceve dopo l'autenticazione.  Il nome deve essere univoco.

12. Fare clic su hello autenticazione menu opzione toomake è visibile.  verrà visualizzata la schermata di autenticazione Hello.
    
    ![Qlik Sense][qs10]
    
    a. Hello **modalità di accesso anonimo** elenco a discesa determina se gli utenti anonimi possono accedere senso Qlik tramite proxy virtuale hello.  opzione predefinita di Hello non è l'utente anonimo.
    
    b. Hello **metodo di autenticazione** elenco a discesa determina l'utilizzo di proxy virtuale hello hello autenticazione schema.  Selezionare SAML dall'elenco a discesa hello.  Verranno di conseguenza visualizzate altre opzioni.
    
    c. In hello **il campo URI host SAML**, gli utenti di nome host di input hello immettere tooaccess Qlik senso attraverso questo proxy virtuale SAML.  il nome host Hello è uri hello del server ha senso Qlik hello.
    
    d. In hello **ID entità SAML**, immettere hello stesso valore immesso per il campo hello SAML host URI.
    
    e. Hello **SAML IdP metadata** file hello modificato in precedenza in hello **modificare i metadati di federazione dalla configurazione di Azure AD** sezione.  **Prima di caricare hello IdP metadata, file hello deve modificare toobe** tooremove informazioni tooensure il corretto funzionamento tra Azure AD e ha senso Qlik server.  **Se il file hello è ancora toobe modificato, fare riferimento toohello istruzioni sopra riportate.**  Se file hello è stato modificato fare clic su pulsante hello e tooupload file di metadati modificati hello selezionare la configurazione del proxy virtuale toohello.
    
    f. Immettere hello di attributo nome o lo schema di riferimento per attributo SAML hello che rappresenta hello **UserID** Azure AD invia toohello server Qlik senso.  Informazioni di riferimento dello schema sono disponibile in hello Azure app schermate post-configurazione.  attributo del nome hello toouse immettere `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    g. Immettere il valore di hello per hello **directory utente** che verranno collegati toousers durante l'autenticazione server senso tooQlik tramite Azure AD.  I valori hardcoded devono essere racchiusi tra **parentesi quadre []**.  un attributo inviato nell'asserzione SAML per Azure AD, hello toouse immettere il nome di hello dell'attributo hello in questa casella di testo **senza** le parentesi quadre.
    
    h. Hello **algoritmo di firma SAML** hello di set di configurazione del proxy virtuale hello di firma del certificato del servizio provider (in questo server ha senso Qlik case).  Se il server ha senso Qlik utilizza un certificato attendibile generato utilizzando Microsoft Enhanced RSA e AES Cryptographic Provider, modificare algoritmo di firma SAML hello troppo**SHA-256**.
    
    i. sezione di mapping di attributi SAML Hello consente di attributi aggiuntivi quali gruppi toobe inviati tooQlik senso per l'utilizzo nelle regole di sicurezza.

13. Fare clic su hello **il bilanciamento del carico** toomake opzione di menu è visibile.  verrà visualizzata la schermata di bilanciamento del carico Hello.
    
    ![Qlik Sense][qs11]

14. Fare clic su hello **Aggiungi nuovo nodo server** pulsante, selezionare motore o nodi Qlik senso verranno inviato a scopo di bilanciamento del carico di toofor di sessioni e fare clic su hello **Aggiungi** pulsante.
    
    ![Qlik Sense][qs12]

15. Fare clic su toomake opzione di menu Avanzate hello è visibile. verrà visualizzata la schermata di Hello avanzate.
    
    ![Qlik Sense][qs13]
    
    elenco vuoto di Hello Host identifica i nomi host che vengono accettati quando ci si connette il server ha senso Qlik toohello.  **Immettere il nome host hello gli utenti specificheranno durante la connessione server senso tooQlik.** nome host Hello è hello stesso valore di hello SAML host uri senza hello https://.

16. Fare clic su hello **applica** pulsante.
    
    ![Qlik Sense][qs14]

17. Fare clic su OK tooaccept messaggio di avviso hello indicante proxy proxy virtuale toohello collegato verrà riavviato.
    
    ![Qlik Sense][qs15]

18. Sul lato destro di hello della schermata ciao, viene visualizzato dal menu di elementi associati hello.  Fare clic su hello **proxy** opzione di menu.
    
    ![Qlik Sense][qs16]

19. verrà visualizzata la schermata di Hello proxy.  Fare clic su hello **collegamento** pulsante hello inferiore toolink proxy virtuale toohello proxy.
    
    ![Qlik Sense][qs17]

20. Nodo proxy selezionare hello che supporterà questa connessione proxy virtuale e fare clic su hello **collegamento** pulsante.  Dopo aver collegato, proxy hello sarà elencata sotto proxy associati.
    
    ![Qlik Sense][qs18]
  
    ![Qlik Sense][qs19]

21. Dopo circa cinque secondi tooten, hello messaggio QMC aggiornamento verranno visualizzati.  Fare clic su hello **QMC aggiornamento** pulsante.
    
    ![Qlik Sense][qs20]

22. Quando viene aggiornato hello QMC, fare clic su hello **virtuale proxy** voce di menu. nuova voce di proxy virtuale SAML Hello è elencato nella tabella hello nella schermata di hello.  Singolo clic sulla voce proxy virtuale hello.
    
    ![Qlik Sense][qs51]

23. In basso hello hello, pulsante di hello SP scaricare i metadati verrà attivati.  Fare clic su hello **scaricare SP metadata** file tooa di pulsante toosave hello metadati.
    
    ![Qlik Sense][qs52]

24. File di metadati sp hello aperto.  Osservare hello **entityID** voce e hello **AssertionConsumerService** voce.  Questi valori sono equivalente toohello **identificatore** hello e **URL di accesso** nella configurazione dell'applicazione hello Azure AD. Incollare questi valori in hello **Qlik senso Enterprise dominio e gli URL** sezione di configurazione dell'applicazione hello Azure AD se essi non corrispondono, quindi è necessario sostituirli nella configurazione guidata di Azure AD App hello.
    
    ![Qlik Sense][qs53]

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

   ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.

   ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.

   ![pulsante Aggiungi Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

   ![finestra di dialogo utente Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   a. In hello **nome** digitare **BrittaSimon**.

   b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

   c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

   d. Fare clic su **Crea**.
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a>Creare un utente di test di Qlik Sense Enterprise

In questa sezione viene creato un utente chiamato Britta Simon in Qlik Sense Enterprise. Lavorare con [team di supporto Client di Enterprise senso Qlik](https://www.qlik.com/us/services/support) per aggiungere gli utenti di hello nella piattaforma Qlik senso Enterprise hello. Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On. 

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooQlik senso Enterprise.

![Assegnazione del ruolo utente hello][200] 

**tooassign Britta Simon tooQlik senso Enterprise, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Qlik senso Enterprise**.

    ![collegamento Qlik senso Enterprise Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Qlik senso Enterprise hello in hello Pannello di accesso, è necessario ottenere applicazione Enterprise senso Qlik tooyour automaticamente firmato-on. 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

