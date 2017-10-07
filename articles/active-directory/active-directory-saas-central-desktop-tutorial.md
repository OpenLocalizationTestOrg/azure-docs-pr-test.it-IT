---
title: 'Esercitazione: Integrazione di Azure Active Directory con Central Desktop | Documentazione Microsoft'
description: Informazioni su come toouse Central Desktop con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a>Esercitazione: Integrazione di Azure Active Directory con Central Desktop
obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e Central Desktop. scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

* Sottoscrizione di Azure valida
* Sottoscrizione di Central Desktop abilitata per l'accesso Single Sign-On e tenant di Central Desktop

scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:

* Abilitazione hello di integrazione dell'applicazione per Central Desktop
* Configurazione dell'accesso Single Sign-On (SSO)
* Configurazione del provisioning utente
* Assegnazione degli utenti

![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")

## <a name="enable-hello-application-integration-for-central-desktop"></a>Abilitare l'integrazione dell'applicazione hello per Central Desktop
obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione hello tooenable per Central Desktop.

**integrazione dell'applicazione hello tooenable per Central Desktop, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
   ![Applicazioni](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applicazioni")
4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
   ![Aggiungere un'applicazione](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Aggiungere un'applicazione")
5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
   ![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")
6. In hello **casella di ricerca**, tipo **Central Desktop**.
   
   ![Raccolta di applicazioni](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Raccolta di applicazioni")
7. Nel riquadro risultati hello selezionare **Central Desktop**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
   ![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")
   
## <a name="configure-single-sign-on"></a>Configura accesso Single Sign-On

obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooCentral Desktop con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.

Come parte di questa procedura, è necessario tooupload un tenant di Central Desktop tooyour certificato con codifica base 64.  
Se non si ha familiarità con questa procedura, vedere [come tooconvert certificato di un file binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o).

**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico, in hello hello **Central Desktop** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** hello tooopen * * configurare Single Sign-On * * finestra di dialogo.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configurare l'accesso Single Sign-On")
2. In hello **come si sarebbe ad esempio utenti toosign su tooCentral Desktop** selezionare **Microsoft Azure AD Single Sign-On**, quindi fare clic su **Avanti**.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configurare l'accesso Single Sign-On")
3. In hello **Configura URL App** pagina, eseguire hello alla procedura seguente e quindi fare clic su **Avanti**: 
   
   1. In hello **Central Desktop Sign In URL** casella di testo, hello digitare l'URL del tenant di Central Desktop (ad esempio: *http://contoso.centraldesktop.com*).
   2. Nella casella di testo URL di risposta Central Desktop hello, digitare l'URL AssertionConsumerService di Central Desktop (ad esempio: https://contoso.centraldesktop.com/saml2-assertion.php).
   
   >[!NOTE]
   >È possibile ottenere il valore di hello dai metadati desktop centrale hello (ad esempio: *http://contoso.centraldesktop.com*).
   >  
   
   ![Configurare l'URL dell'app](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configurare l'URL dell'app")
4. In hello **Configura accesso single sign-on in Central Desktop** pagina, toodownload il certificato, fare clic su **Scarica certificato**e quindi salvare il file di certificato hello nel computer in uso.
   
  ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configurare l'accesso Single Sign-On")
5. Accedi tooyour **Central Desktop** tenant.
6. Andare troppo**impostazioni**, fare clic su **avanzate**, quindi fare clic su **Single Sign-On**.
   
  ![Installazione - Avanzate](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Installazione - Avanzate")
7. In hello **Single Sign On Settings** eseguire hello alla procedura seguente:
   
  ![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")
   
  1. Selezionare **Enable SAML v2 Single Sign On**.
  2. Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Central Desktop** pagina, hello copia **URL autorità di certificazione** valore e quindi incollarlo hello **URL SSO** casella di testo.
  3. Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Central Desktop** pagina, hello copia **URL accesso remoto** valore e quindi incollarlo hello **SSO Login URL**casella di testo.
  4. Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Central Desktop** pagina, hello copia **URL del servizio Single Sign-Out** valore e quindi incollarlo hello **URL disconnessione SSO** casella di testo.
8. In hello **metodo verifica della firma del messaggio** seguire hello alla procedura seguente:
   
   ![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")
   
  1. Selezionare **Certificate**.
  2. Da hello **certificato SSO** elenco, selezionare **RSH SHA256**.
  3. Creare un file di testo dal certificato scaricato hello, hello copia del contenuto del file di testo hello e quindi incollarlo hello **certificato SSO** campo.  
     >[!TIP]
     >Per ulteriori informazioni, vedere [come tooconvert certificato di un file binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o)
      >  
   4. Selezionare **visualizzare una pagina di accesso di SAMLv2 tooyour collegamento**.
9. Fare clic su **Update**.
10. Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.
    
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configurare l'accesso Single Sign-On")
    
## <a name="configure-user-provisioning"></a>Configura provisioning utenti

Per AAD utenti toobe in grado di toosign in devono essere sottoposte a provisioning toohello applicazione Central Desktop. In questa sezione viene descritto come degli account utente AAD toocreate in Central Desktop.

**gli account utente tooprovision tooCentral Desktop:**
1. Accedi tooyour tenant di Central Desktop.
2. Andare troppo**persone \> membri interni**.
3. Fare clic su **Add Internal Members**.
   
  ![Persone](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Persone")
4. In hello **Email Address of New Members** casella di testo, digitare un account AAD, si desidera tooprovision e quindi fare clic su **Avanti**.
   
  ![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")
5. Fare clic su **Add Internal member(s)**.
   
  ![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")
   
   >[!NOTE]
   >gli utenti di Hello aggiunti riceveranno un messaggio di posta elettronica che include un collegamento di conferma account hello di tooclick tooactivate.
   > 

>[!NOTE]
>È possibile usare qualsiasi altro Central Desktop utente account strumento di creazione o le API fornite da Central Desktop tooprovision account utente di AAD
>  

## <a name="assign-users"></a>Assegna utenti
tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.

**gli utenti di tooassign tooCentral Desktop, eseguire hello alla procedura seguente:**

1. Nel portale di Azure classico hello, creare un account di prova.
2. In hello **Central Desktop** pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.
   
   ![Assegnare utenti](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assegnare utenti")
3. Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.
   
   ![Sì](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Sì")

Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello. Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

