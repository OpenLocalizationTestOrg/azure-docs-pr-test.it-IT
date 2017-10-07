---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cisco Webex | Documentazione Microsoft'
description: Informazioni su come toouse Cisco Webex con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a>Esercitazione: Integrazione di Azure Active Directory con Cisco Webex
obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e Cisco Webex.  
scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

* Sottoscrizione di Azure valida
* Tenant di Cisco Webex

Dopo aver completato questa esercitazione, hello Azure AD utenti assegnati tooCisco Webex sarà in grado di toosingle sign in un'applicazione hello nel sito della società Cisco Webex (accesso avviato dal provider di servizi su) o tramite hello [toohello introduzione Accedere al pannello](active-directory-saas-access-panel-introduction.md).

scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:

* Abilitazione hello di integrazione dell'applicazione per Cisco Webex
* Configurazione dell'accesso Single Sign-On (SSO)
* Configurazione del provisioning utente
* Assegnazione degli utenti

![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")

## <a name="enable-hello-application-integration-for-cisco-webex"></a>Abilitare l'integrazione dell'applicazione hello per Cisco Webex
obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione hello tooenable per Cisco Webex.

**integrazione dell'applicazione hello tooenable per Cisco Webex, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
   ![Applicazioni](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applicazioni")
4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
   ![Aggiungere un'applicazione](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Aggiungere un'applicazione")
5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
   ![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")
6. In hello **casella di ricerca**, tipo **Cisco Webex**.
   
   ![Raccolta di applicazioni](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Raccolta di applicazioni")
7. Nel riquadro risultati hello selezionare **Cisco Webex**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
   ![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")
   
## <a name="configure-single-sign-on"></a>Configura accesso Single Sign-On

obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooCisco Webex con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.  

Come parte di questa procedura, sono toocreate richiesto un certificato con codifica base 64. Se non si ha familiarità con questa procedura, vedere [come tooconvert certificato di un file binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, in hello hello **Cisco Webex** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configurare l'accesso Single Sign-On")
2. In hello **come si sarebbe ad esempio utenti toosign su tooCisco Webex** selezionare **Microsoft Azure AD Single Sign-On**, quindi fare clic su **Avanti**.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configurare l'accesso Single Sign-On")
3. In hello **Configura URL App** pagina, eseguire hello alla procedura seguente e quindi fare clic su **Avanti**.
   
   ![Configurare l'URL dell'app](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configurare l'URL dell'app")   
   1. In hello **URL di accesso** casella di testo, digitare l'URL del tenant Cisco Webex (ad esempio: *http://contoso.webex.com*).
   2. In hello **URL di risposta Cisco Webex** digitare il **Cisco Webex AssertionConsumerService URL** (ad esempio: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).
4. In hello **Configura accesso single sign-on in Cisco Webex** pagina, toodownload il certificato, fare clic su **Scarica certificato**e quindi salvare il file di certificato hello nel computer in uso.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configurare l'accesso Single Sign-On")
5. In un'altra finestra del Web browser accedere al sito aziendale di Cisco Webex come amministratore.
6. Scegliere dal menu hello in primo piano hello **amministrazione sito**.
   
   ![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")
7. In hello **Manage Site** fare clic su **configurazione di SSO**.
   
   ![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")
8. Nella sezione di configurazione di SSO Web federata hello, eseguire hello alla procedura seguente:
   
   ![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")  
   1. Da hello **protocollo Federation** elenco, selezionare **SAML 2.0**.
   2. Creare un file **con codifica Base 64** dal certificato scaricato.  
    >[!TIP]
    >Per ulteriori informazioni, vedere [come tooconvert certificato di un file binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o)
    >  
   3. Aprire il certificato con codifica base 64 nel blocco note e quindi hello copia del contenuto di esso.
   4. Fare clic su **Import SAML Metadata**e quindi incollare il certificato con codifica Base 64.
   5. Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Cisco Webex** nella pagina, hello copia **URL autorità di certificazione** valore e quindi incollarlo hello **Issuer for SAML (IdP ID)** casella di testo.
   6. Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Cisco Webex** nella pagina, hello copia **URL accesso remoto** valore e quindi incollarlo hello **Customer SSO Service Login URL** casella di testo.
   7. Da hello **NameID Format** elenco, selezionare **indirizzo di posta elettronica**.
   8. In hello **AuthnContextClassRef** casella tipo **urn: oasis: nomi: tc: SAML:2.0:ac:classes:Password**.
   9. Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Cisco Webex** nella pagina, hello copia **URL disconnessione remota** valore e quindi incollarlo hello **Customer SSO Service Logout URL** casella di testo.
   10. Fare clic su **Update**.
9. Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Cisco Webex** nella pagina, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa**.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configurare l'accesso Single Sign-On")
   
## <a name="configure-user-provisioning"></a>Configura provisioning utenti

In ordine tooenable Azure AD utenti toolog a Cisco Webex, è necessario eseguirne il provisioning in Cisco Webex.  

* Nel caso di hello di Cisco Webex, il provisioning è un'attività manuale.

**eseguire un account utente, tooprovision hello i passaggi seguenti:**

1. Accedi tooyour **Cisco Webex** tenant.
2. Andare troppo**Gestisci utenti \> Aggiungi utente**.
   
   ![Aggiungere utenti](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Aggiungere utenti")
3. Nella sezione Aggiungi utente hello, eseguire hello alla procedura seguente:
   
   ![Aggiungere un utente](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Aggiungere un utente")   
   1. Per **Account Type** (Tipo di account), scegliere **Host**.
   2. Immettere informazioni hello di un utente di Azure AD esistente in hello seguenti caselle di testo: **nome, cognome**, **nome utente**, **posta elettronica**, **Password**, **Conferma Password**.
   3. Fare clic su **Aggiungi**.

>[!NOTE]
>È possibile usare qualsiasi altro Cisco Webex utente account strumento di creazione o qualsiasi API fornita da Cisco Webex tooprovision account utente di AAD. 
> 

## <a name="assign-users"></a>Assegna utenti
tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.

**gli utenti di tooassign tooCisco Webex, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico hello, creare un account di prova.
2. In hello **Cisco Webex** pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.
   
   ![Assegnare utenti](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assegnare utenti")
3. Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.
   
   ![Sì](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Sì")

Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello. Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

