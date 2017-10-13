---
title: 'Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox | Documentazione Microsoft'
description: Informazioni su come usare Salesforce Sandbox con Azure Active Directory per abilitare l'accesso Single Sign-On, il provisioning automatizzato e altro ancora.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 32835e79188806bb2ff319eea23b1b52ab585ab1
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox

In questa esercitazione viene illustrata l'integrazione di Azure e Salesforce Sandbox.  

>[!TIP]
>Per commenti, vedere la [pagina del supporto tecnico Azure](http://go.microsoft.com/fwlink/?LinkId=521878). 
> 

Sandbox offre la possibilità di creare più copie dell'organizzazione in ambienti distinti per diversi scopi, ad esempio sviluppo, test e formazione, senza compromettere i dati e le applicazioni dell’organizzazione di produzione Salesforce.  

Per ulteriori informazioni, vedere [Panoramica di Sandbox](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)

Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:

* Sottoscrizione di Azure valida
* Sandbox in Salesforce.com

Se non si dispone di un sandbox valido in Salesforce.com, è necessario contattare Salesforce.

Lo scenario descritto in questa esercitazione include i blocchi predefiniti seguenti:

1. Abilitazione dell'integrazione dell'applicazione per Salesforce Sandbox
2. Configurazione dell'accesso Single Sign-On (SSO)
3. Abilitazione del dominio
4. Configurazione del provisioning utente
5. Assegnazione degli utenti

![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")

## <a name="enable-the-application-integration-for-salesforce-sandbox"></a>Abilitare l'integrazione dell'applicazione per Salesforce Sandbox
In questa sezione viene descritto come abilitare l'integrazione dell'applicazione per Salesforce Sandbox.

**Per abilitare l'integrazione dell'applicazione per Salesforce Sandbox, eseguire la procedura seguente:**

1. Nel portale di Azure classico fare clic su **Active Directory**nel riquadro di spostamento sinistro.
   
   ![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")
2. Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.
3. Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.
   
   ![Applicazioni](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applicazioni")
4. Per aprire la **Raccolta di applicazioni**, fare clic su **Aggiungi app**, quindi fare clic su **Aggiungi un'applicazione che verrà utilizzata dall'organizzazione**.
   
   ![Come procedere](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Come procedere")
5. Nella **casella di ricerca** digitare **Salesforce Sandbox**.
   
   ![Raccolta di applicazioni](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Raccolta di applicazioni")
6. Nel riquadro dei risultati selezionare **Salesforce Sandbox**, quindi fare clic su **Completa** per aggiungere l'applicazione.
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")
   
## <a name="configur-single-sign-on-sso"></a>Configurare l'accesso Single Sign-On (SSO)

In questa sezione viene descritto come consentire agli utenti di eseguire l'autenticazione a Salesforce Sandbox tramite il proprio account di Azure AD usando la federazione basata sul protocollo SAML.

**Per configurare l'accesso Single Sign-On, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Salesforce Sandbox** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configurare l'accesso Single Sign-On")
2. Nella pagina **Stabilire come si desidera che gli utenti accedano a Salesforce Sandbox** selezionare **Single Sign-On di Microsoft Azure AD** e quindi fare clic su **Avanti**.
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")
3. Nella casella di testo **URL di accesso** della pagina **Configura URL app** digitare l'URL nel formato `http://company.my.salesforce.com` e quindi fare clic su **Avanti**.
   
   ![Configurare l'URL dell'app](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configurare l'URL dell'app")
4. Se l'accesso Single Sign-On è già stato configurato per un'altra istanza di Salesforce Sandbox nella directory, sarà necessario configurare anche l'**identificatore** in modo che abbia lo stesso valore di **URL di accesso**. 
 * Per trovare il campo **Identificatore**, selezionare la casella di controllo **Impostazioni avanzate** nella pagina **Configura URL app** della finestra di dialogo.
5. Nella pagina **Configura accesso Single Sign-On in Salesforce Sandbox** fare clic su **Scarica certificato** e quindi salvare il file di certificato nel computer.
   
   ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configurare l'accesso Single Sign-On")
6. In un'altra finestra del Web browser accedere al sito aziendale di Salesforce Sandbox come amministratore.
7. Nel menu in alto fare clic su **Impostazione**.
   
   ![Installazione](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Installazione")
8. Nel riquadro di spostamento a sinistra, fare clic su **Security Controls** (Controlli di sicurezza) e quindi fare clic su **Single Sign-On Settings** (Impostazioni Single Sign-On).
   
   ![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")
9. Nella sezione Impostazioni Single Sign-On, eseguire la procedura seguente:
   
   ![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")  
 1.  Selezionare **Abilitato SAML**. 
 2.  Fare clic su **New**.
10. Nella sezione Impostazioni SAML Single Sign-On, eseguire la procedura seguente:
    
    ![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")  
 1. Nella casella di testo Nome digitare il nome della configurazione, ad esempio *SPSSOWAAD\_Test*. 
 2. Nella finestra di dialogo **Configura accesso Single Sign-On in Salesforce Sandbox** del portale di Azure classico copiare il valore di **URL autorità di certificazione** e incollarlo nella casella di testo **Issuer** (Autorità di certificazione).
 3. Nella casella di testo **ID entità** digitare **https://test.salesforce.com** se è la prima istanza di Salesforce Sandbox aggiunta alla directory. Se esiste già un'istanza di Salesforce Sandbox, in **ID entità** digitare l'**URL di accesso**, che deve avere questo formato: `http://company.my.salesforce.com`   
 4. Per caricare il certificato scaricato, fare clic su **Sfoglia** .  
 5. In **SAML Identity Type** (Tipo di identità SAML) selezionare **Assertion contains the Federation ID from the User object** (L'asserzione contiene l'ID federazione dell'oggetto utente). 
 6. In **SAML Identity Location**(Percorso identità SAML) selezionare **Identity is in the NameIdentifier element of the Subject statement** (L'identità è nell'elemento NameIdentifier dell'istruzione Subject).
 7. Nella pagina della finestra di dialogo **Configura accesso Single Sign-On in Salesforce Sandbox** del portale di Azure classico copiare il valore di **URL accesso remoto** e incollarlo nella casella di testo **Identity Provider Login URL** (URL di accesso provider di identità). 
 8. SFDC non supporta la disconnessione SAML.  Come soluzione alternativa, incollare "https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0" nella casella di testo **Identity Provider Logout URL** (URL di disconnessione provider di identità).
 9. In **Service Provider Initiated Request Binding** (Binding richiesta avviato dal provider di servizi) selezionare **HTTP POST**. 
 10. Fare clic su **Save**.
11. Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Complete** per chiudere la finestra di dialogo **Configura accesso Single Sign-On**.
    
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configurare l'accesso Single Sign-On")

## <a name="enable-your-domain"></a>Abilitare il dominio
In questa sezione si presuppone che sia già stato creato un dominio.  Per informazioni dettagliate, vedere [Definizione del nome di dominio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**Per abilitare il dominio, eseguire la procedura seguente:**

1. Nel riquadro di spostamento a sinistra fare clic su **Domain Management** (Gestione dominio) e quindi su **My Domain** (Dominio personale).
   
   ![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")
   
   >[!NOTE]
   >Assicurarsi che il dominio sia stato configurato correttamente. 
   > 
2. Nella sezione **Login Page Settings** (Impostazioni pagina di accesso) fare clic su **Edit** (Modifica), quindi per **Authentication Service** (Servizio di autenticazione) selezionare il nome dell'impostazione Single Sign-On SAML definita nella sezione precedente e fare clic su **Save** (Salva).
   
   ![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")

Non appena si dispone di un dominio configurato, gli utenti devono utilizzare l'URL del dominio per l'accesso a Salesforce Sandbox.  

Per ottenere il valore dell'URL, fare clic sul profilo SSO creato nella sezione precedente.

## <a name="configure-user-provisioning"></a>Configura provisioning utenti
In questa sezione viene descritto come abilitare il provisioning utente degli account utente di Active Directory in Salesforce Sandbox.

**Per configurare il provisioning utenti, seguire questa procedura:**

1. Nella barra di spostamento in alto del portale di Salesforce, selezionare il nome per espandere il menu utente:
   
   ![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")
2. Nel menu utente selezionare **My Settings** (Impostazioni personali) per aprire la pagina **My Settings** (Impostazioni personali).
3. Nel riquadro a sinistra fare clic su **Personal** (Personale) per espandere la sezione corrispondente e fare clic su **Reset My Security Token** (Reimposta token di sicurezza personale):
   
   ![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")
4. Nella pagina **Reset My Security Token** (Reimposta token di sicurezza personale) fare clic su **Reset Security Token** (Reimposta token di sicurezza) per richiedere un messaggio di posta elettronica con il token di sicurezza di Salesforce.com.
   
   ![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")
5. Verificare nella cartella Posta in arrivo la presenza di un messaggio da Salesforce.com con oggetto analogo a "**conferma di sicurezza di salesforce.com.com**".
6. Aprire il messaggio di posta elettronica e copiare il valore del token di sicurezza.
7. Nella pagina di integrazione dell'applicazione **Salesforce Sandbox** del portale di Azure classico fare clic su **Configura provisioning utenti** per aprire la finestra di dialogo **Configura provisioning utenti**.
   
   ![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")
8. Nella pagina **Immettere le credenziali di Salesforce Sandbox per abilitare il provisioning automatico degli utenti** specificare le impostazioni di configurazione seguenti:
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")   
 1. Nella casella di testo **Nome utente amministratore Salesforce Sandbox** digitare un nome account di Salesforce Sandbox con il profilo **Amministratore di sistema** assegnato in Salesforce.com.
 2. Nella casella di testo **Password amministratore Salesforce Sandbox** digitare la password per questo account.
 3. Nella casella di testo **Token di sicurezza utente** incollare il valore del token di sicurezza.
 4. Fare clic su **Convalida** per verificare la configurazione.
 5. Fare clic sul pulsante **Avanti** per aprire la pagina **Conferma**.
9. Nella pagina **Conferma** fare clic su **Completa** per salvare la configurazione.
   
## <a name="assigning-users"></a>Assegnazione degli utenti

Per testare la configurazione, è necessario concedere l'accesso all'applicazione agli utenti di Azure AD a cui si vuole consentirne l'uso, assegnando tali utenti all'applicazione.

**Per assegnare gli utenti a Salesforce Sandbox, eseguire la procedura seguente:**

1. Nel portale di Azure classico creare un account di test.
2. Nella pagina di integrazione dell'applicazione **Salesforce Sandbox** fare clic su **Assegna utenti**.
   
   ![Assegnare utenti](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assegnare utenti")
3. Selezionare l'utente di test, fare clic su **Assegna** e quindi su **Sì** per confermare l'assegnazione.
   
   ![Sì](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Sì")

È ora necessario attendere 10 minuti e verificare che l'account sia stato sincronizzato con Salesforce Sandbox.

Per testare le impostazioni di SSO, aprire il pannello di accesso. Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).

