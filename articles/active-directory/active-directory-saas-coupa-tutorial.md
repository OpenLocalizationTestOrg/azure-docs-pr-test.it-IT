---
title: 'Esercitazione: Integrazione di Azure Active Directory con Coupa | Documentazione Microsoft'
description: Informazioni su come toouse Coupa con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>Esercitazione: Integrazione di Azure Active Directory con Coupa
obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e Coupa.  
scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

* Sottoscrizione di Azure valida
* Sottoscrizione di Coupa abilitata per l'accesso Single Sign-On (SSO)

Dopo aver completato questa esercitazione, gli utenti di hello Azure AD assegnati tooCoupa saranno in grado di toosingle sign in un'applicazione hello utilizzando hello [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:

* Abilitazione di hello integrazione dell'applicazione Coupa
* Configurazione dell'accesso Single Sign-On
* Configurazione del provisioning utente
* Assegnazione degli utenti

![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")

## <a name="enable-hello-application-integration-for-coupa"></a>Abilitare l'integrazione dell'applicazione hello per Coupa
obiettivo di Hello di questa sezione è toooutline come tooenable hello integrazione dell'applicazione Coupa.

**tooenable hello integrazione dell'applicazione Coupa, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
   ![Applicazioni](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applicazioni")
4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
   ![Aggiungere un'applicazione](./media/active-directory-saas-coupa-tutorial/IC749321.png "Aggiungere un'applicazione")
5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
   ![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-coupa-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")
6. In hello **casella di ricerca**, tipo **Coupa**.
   
   ![Raccolta di applicazioni](./media/active-directory-saas-coupa-tutorial/IC791898.png "Raccolta di applicazioni")
7. Nel riquadro risultati hello selezionare **Coupa**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
   ![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")
   
## <a name="configure-single-sign-on"></a>Configura accesso Single Sign-On

obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooCoupa con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.  

La configurazione di single sign-on per Coupa richiede tooretrieve un valore di identificazione personale da un certificato. Se non si ha familiarità con questa procedura, vedere [come tooretrieve il valore di identificazione personale del certificato](http://youtu.be/YKQF266SAxI).

**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**

1. Accesso tooyour sito della società Coupa come amministratore.
2. Andare troppo**installazione \> controllo di sicurezza**.
   
   ![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")
3. Fare clic su toodownload hello Coupa metadati file tooyour computer **scaricare e importare metadati SP**.
   
   ![Metadati Coupa SP](./media/active-directory-saas-coupa-tutorial/IC791901.png "Metadati Coupa SP")
4. In un'altra finestra del browser, accedere toohello portale di Azure classico.
5. In hello **Coupa** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configurare l'accesso Single Sign-On")
6. In hello **come si sarebbe ad esempio utenti toosign su tooCoupa** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configurare l'accesso Single Sign-On")
7. In hello **Configura URL App** eseguire hello alla procedura seguente:
   
   ![Configurare l'URL dell'app](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configurare l'URL dell'app")   
   1. In hello **URL di accesso** casella di testo, digitare l'URL usato per il toosign gli utenti in tooyour applicazione Coupa (ad esempio: "*http://company.Coupa.com*").
   2. Aprire il file di metadati Coupa scaricato e quindi copiare hello **AssertionConsumerService index/URL**.
   3. In hello **URL di risposta Coupa** casella di testo, incollare hello **AssertionConsumerService index/URL** valore.
   4. Fare clic su **Avanti**.
8. In hello **Configura accesso single sign-on in Coupa** pagina, toodownload il file di metadati, fare clic su **Scarica metadati**e quindi salvare il file hello in locale nel computer.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configurare l'accesso Single Sign-On")
9. Nel sito della società Coupa hello passare troppo**installazione \> controllo di sicurezza**.
   
   ![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")
10. In hello **accedere con credenziali Coupa** seguire hello alla procedura seguente:  

   ![Accesso mediante le credenziali di Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Accesso mediante le credenziali di Coupa") 
   1. Selezionare **Accedere mediante SAML**.
   2. Fare clic su **Sfoglia** tooupload il file di metadati scaricato Azure attivo.
   3. Fare clic su **Salva**.
11. Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.
    
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configurare l'accesso Single Sign-On")
    
## <a name="configure-user-provisioning"></a>Configura provisioning utenti

In ordine tooenable Azure AD utenti toolog a Coupa, è necessario eseguirne il provisioning in Coupa.  

* Nel caso di hello di Coupa, il provisioning è un'attività manuale.

**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**

1. Accedi tooyour **Coupa** sito aziendale come amministratore.
2. Scegliere dal menu hello in primo piano hello **installazione**e quindi fare clic su **utenti**.
   
   ![Utenti](./media/active-directory-saas-coupa-tutorial/IC791908.png "Utenti")
3. Fare clic su **Crea**.
   
   ![Creare utenti](./media/active-directory-saas-coupa-tutorial/IC791909.png "Creare utenti")
4. In hello **utente creare** seguire hello alla procedura seguente:
   
   ![Dettagli utente](./media/active-directory-saas-coupa-tutorial/IC791910.png "Dettagli utente")
   
   1. Hello tipo **accesso**, **nome**, **Last Name**, **Single Sign-On ID**, **posta elettronica** gli attributi di un account di Azure Active Directory valido desiderate tooprovision hello relative caselle di testo.
   2. Fare clic su **Crea**.   
   >[!NOTE]
   >titolare dell'account di Azure Active Directory Hello verrà visualizzato un messaggio di posta elettronica con un account di hello tooconfirm collegamento prima che diventi attivo. 
   > 

>[!NOTE]
>È possibile usare qualsiasi altro Coupa utente account strumento di creazione o le API fornite da Coupa tooprovision account utente di AAD. 
> 

## <a name="assign-users"></a>Assegna utenti
tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.

**tooassign tooCoupa di utenti, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico hello, creare un account di prova.
2. In hello * * Coupa * * pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.
   
   ![Assegnare utenti](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assegnare utenti")
3. Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.
   
   ![Sì](./media/active-directory-saas-coupa-tutorial/IC767830.png "Sì")

Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello. Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

