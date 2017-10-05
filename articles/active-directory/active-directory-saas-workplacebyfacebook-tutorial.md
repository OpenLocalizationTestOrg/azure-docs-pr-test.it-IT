---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Workplace by Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1590a66f215f0c093d24ff602c0ad951ba1e1eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="39738-103">Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="39738-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="39738-104">Questa esercitazione descrive come integrare Workplace by Facebook con Azure Active Directory, ovvero Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39738-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="39738-105">L'integrazione di Workplace by Facebook con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="39738-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="39738-106">È possibile controllare in Azure AD chi può accedere a Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="39738-106">You can control in Azure AD who has access to Workplace by Facebook</span></span>
- <span data-ttu-id="39738-107">È possibile abilitare gli utenti per l'accesso automatico a Workplace by Facebook (Single Sign-On) con i propri account di Azure AD</span><span class="sxs-lookup"><span data-stu-id="39738-107">You can enable your users to automatically get signed-on to Workplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="39738-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="39738-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="39738-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="39738-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39738-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="39738-110">Prerequisites</span></span>

<span data-ttu-id="39738-111">Per configurare l'integrazione di Azure AD con Workplace by Facebook, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="39738-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="39738-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39738-112">An Azure AD subscription</span></span>
- <span data-ttu-id="39738-113">Una sottoscrizione di Workplace by Facebook abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="39738-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="39738-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="39738-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="39738-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="39738-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="39738-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="39738-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="39738-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="39738-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="39738-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="39738-118">Scenario description</span></span>
<span data-ttu-id="39738-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="39738-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="39738-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="39738-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39738-121">Aggiunta di Workplace by Facebook dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="39738-121">Adding Workplace by Facebook from the gallery</span></span>
2. <span data-ttu-id="39738-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="39738-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="39738-123">Aggiunta di Workplace by Facebook dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="39738-123">Adding Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="39738-124">Per configurare l'integrazione di Workplace by Facebook in Azure AD, è necessario aggiungere Workplace by Facebook dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="39738-124">To configure the integration of Workplace by Facebook into Azure AD, you need to add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="39738-125">**Per aggiungere Workplace by Facebook dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="39738-125">**To add Workplace by Facebook from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="39738-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="39738-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="39738-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="39738-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="39738-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="39738-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="39738-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="39738-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="39738-133">Nella casella di ricerca digitare **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="39738-133">In the search box, type **Workplace by Facebook**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="39738-135">Nel pannello dei risultati selezionare **Workplace by Facebook** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="39738-135">In the results panel, select **Workplace by Facebook**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="39738-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="39738-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="39738-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Workplace by Facebook usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="39738-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="39738-139">Affinché l'accesso Single Sign-On funzioni correttamente, Azure AD deve conoscere l'utente controparte di Workplace by Facebook corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39738-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="39738-140">In altre parole, si deve stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="39738-140">In other words, a link relationship between an Azure AD user and the related user in Workplace by Facebook needs to be established.</span></span>

<span data-ttu-id="39738-141">La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Username** (Nome utente) in Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="39738-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="39738-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Workplace by Facebook, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="39738-142">To configure and test Azure AD single sign-on with Workplace by Facebook, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="39738-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="39738-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="39738-144">**[Configurazione della frequenza di riautenticazione](#configuring-reauthentication-frequency)**: per configurare Workplace per la richiesta di una verifica SAML.</span><span class="sxs-lookup"><span data-stu-id="39738-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - to configure Workplace to prompt for a SAML check.</span></span>
3. <span data-ttu-id="39738-145">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39738-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="39738-146">**[Creazione di un utente di test di Workplace by Facebook](#creating-a-workplace-by-facebook-test-user)**: per avere una controparte di Britta Simon in Workplace by Facebook collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39738-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - to have a counterpart of Britta Simon in Workplace by Facebook that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="39738-147">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39738-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="39738-148">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="39738-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="39738-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="39738-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="39738-150">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="39738-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="39738-151">**Per configurare l'accesso Single Sign-On di Azure AD con Workplace by Facebook, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="39738-151">**To configure Azure AD single sign-on with Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="39738-152">Nella pagina di integrazione dell'applicazione **Workplace by Facebook** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="39738-152">In the Azure portal, on the **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="39738-154">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="39738-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="39738-156">Nella sezione **Workplace by Facebook Domain and URLs** (URL e dominio Workplace by Facebook) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="39738-156">On the **Workplace by Facebook Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="39738-158">a.</span><span class="sxs-lookup"><span data-stu-id="39738-158">a.</span></span> <span data-ttu-id="39738-159">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<instancename>.facebook.com`.</span><span class="sxs-lookup"><span data-stu-id="39738-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="39738-160">b.</span><span class="sxs-lookup"><span data-stu-id="39738-160">b.</span></span> <span data-ttu-id="39738-161">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="39738-161">In the **Identifier** textbox, type a URL using the following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="39738-162">Questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="39738-162">These values are not the real.</span></span> <span data-ttu-id="39738-163">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="39738-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="39738-164">Per ottenere questi valori, contattare il [team di supporto clienti di Workplace by Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="39738-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="39738-165">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="39738-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="39738-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="39738-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="39738-169">Nella sezione **Workplace by Facebook Configuration** (Configurazione di Workplace by Facebook) fare clic su **Configure Workplace by Facebook** (Configurare Workplace by Facebook) per aprire la finestra **Configurare accesso**.</span><span class="sxs-lookup"><span data-stu-id="39738-169">On the **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** to open **Configure sign-on** window.</span></span> <span data-ttu-id="39738-170">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="39738-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="39738-172">In un'altra finestra del Web browser accedere al sito aziendale di Workplace by Facebook come amministratore.</span><span class="sxs-lookup"><span data-stu-id="39738-172">In a different web browser window, login to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="39738-173">Come parte del processo di autenticazione SAML, Workplace può usare stringhe di query di dimensioni massime di 2,5 kilobyte per passare i parametri ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39738-173">As part of the SAML authentication process, Workplace may utilize query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="39738-174">In **Company Dashboard** (Company Dashboard) passare alla scheda **Authentication** (Autenticazione).</span><span class="sxs-lookup"><span data-stu-id="39738-174">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="39738-175">In **SAML Authentication** (Autenticazione SAML) selezionare **SSO Only** (Solo SSO) dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="39738-175">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="39738-176">Immettere i valori copiati dalla sezione **Workplace by Facebook Configuration** (Configurazione di Workplace by Facebook) del portale di Azure nei campi corrispondenti:</span><span class="sxs-lookup"><span data-stu-id="39738-176">Input the values copied from **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="39738-177">Nella casella di testo **SAML URL** (URL SAML) incollare il valore di **URL servizio Single Sign-On** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="39738-177">In **SAML URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="39738-178">Nella **casella di testo SAML Issuer URL** (URL dell'autorità di certificazione SAML) incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="39738-178">In **SAML Issuer URL textbox**, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="39738-179">In **SAML Logout Redirect (Optional)** (Reindirizzamento disconnessione SAML (facoltativo)) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="39738-179">In **SAML Logout Redirect** (Optional), paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="39738-180">Aprire nel Blocco note il **certificato con codifica Base 64** scaricato dal portale di Azure, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **SAML Certificate** (Certificato SAML).</span><span class="sxs-lookup"><span data-stu-id="39738-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="39738-181">Potrebbe essere necessario inserire l'URL del pubblico, l'URL del destinatario e l'URL ACS (servizio consumer di asserzione) elencati nella sezione **SAML Configuration** (Configurazione SAML).</span><span class="sxs-lookup"><span data-stu-id="39738-181">You may need to enter the Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="39738-182">Scorrere fino alla fine della sezione e fare clic sul pulsante **Test SSO** (Testa SSO).</span><span class="sxs-lookup"><span data-stu-id="39738-182">Scroll to the bottom of the section and click the **Test SSO** button.</span></span> <span data-ttu-id="39738-183">Si ottiene una finestra popup visualizzata con la pagina di accesso di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39738-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="39738-184">Immettere le credenziali come di consueto per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="39738-184">Enter your credentials in as normal to authenticate.</span></span> 

    <span data-ttu-id="39738-185">**Risoluzione dei problemi:** assicurarsi che l'indirizzo e-mail restituito da Azure AD sia lo stesso dell'account aziendale con cui si è connessi.</span><span class="sxs-lookup"><span data-stu-id="39738-185">**Troubleshooting:** Ensure the email address being returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="39738-186">Dopo il completamento del test, scorrere fino alla fine della pagina e fare clic sul pulsante **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="39738-186">Once the test has been completed successfully, scroll to the bottom of the page and click the **Save** button.</span></span>

14. <span data-ttu-id="39738-187">Tutti gli utenti che usano Workplace visualizzeranno ora una pagina di accesso di Azure AD per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="39738-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="39738-188">**Reindirizzamento disconnessione SAML (facoltativo)** -</span><span class="sxs-lookup"><span data-stu-id="39738-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="39738-189">È possibile scegliere di configurare facoltativamente un URL di disconnessione SAML, che può essere usato per puntare alla pagina di disconnessione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39738-189">You can choose to optionally configure a SAML Logout Url, which can be used to point at Azure AD's logout page.</span></span> <span data-ttu-id="39738-190">Quando questa impostazione è abilitata e configurata, l'utente non sarà più indirizzato alla pagina di disconnessione di Workplace.</span><span class="sxs-lookup"><span data-stu-id="39738-190">When this setting is enabled and configured, the user will no longer be directed to the Workplace logout page.</span></span> <span data-ttu-id="39738-191">Al contrario, l'utente verrà reindirizzato all'URL aggiunto nelle impostazioni di reindirizzamento di disconnessione SAML.</span><span class="sxs-lookup"><span data-stu-id="39738-191">Instead, the user will be redirected to the url that was added in the SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="39738-192">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="39738-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="39738-193">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="39738-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="39738-194">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="39738-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="39738-195">Configurazione della frequenza di riautenticazione</span><span class="sxs-lookup"><span data-stu-id="39738-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="39738-196">È possibile configurare Workplace per la richiesta di una verifica SAML ogni giorno, ogni 3 giorni, ogni settimana, ogni 2 settimane, ogni mese o mai.</span><span class="sxs-lookup"><span data-stu-id="39738-196">You can configure Workplace to prompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="39738-197">Il valore minimo per la verifica SAML nelle applicazioni per dispositivi mobili è impostato su una settimana.</span><span class="sxs-lookup"><span data-stu-id="39738-197">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="39738-198">È anche possibile forzare una reimpostazione SAML per tutti gli utenti che usano il pulsante: Require SAML authentication for all users now (Richiedi ora l'autenticazione SAML a tutti gli utenti).</span><span class="sxs-lookup"><span data-stu-id="39738-198">You can also force a SAML reset for all users using the button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="39738-199">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="39738-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="39738-200">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="39738-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="39738-202">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="39738-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="39738-203">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="39738-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="39738-205">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="39738-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="39738-207">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="39738-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="39738-209">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="39738-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="39738-211">a.</span><span class="sxs-lookup"><span data-stu-id="39738-211">a.</span></span> <span data-ttu-id="39738-212">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="39738-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="39738-213">b.</span><span class="sxs-lookup"><span data-stu-id="39738-213">b.</span></span> <span data-ttu-id="39738-214">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="39738-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="39738-215">c.</span><span class="sxs-lookup"><span data-stu-id="39738-215">c.</span></span> <span data-ttu-id="39738-216">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="39738-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="39738-217">d.</span><span class="sxs-lookup"><span data-stu-id="39738-217">d.</span></span> <span data-ttu-id="39738-218">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="39738-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="39738-219">Creazione di un utente test di Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="39738-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="39738-220">In questa sezione si crea un utente di nome Britta Simon in Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="39738-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="39738-221">Workplace by Facebook supporta il provisioning JIT, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="39738-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="39738-222">Non è necessaria alcuna azione dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="39738-222">There is no action for you in this section.</span></span> <span data-ttu-id="39738-223">Se un utente non esiste in Workplace by Facebook, si crea una nuova istanza quando si tenta di accedere a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="39738-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="39738-224">Se è necessario creare un utente manualmente, contattare il [team di supporto al cliente di Workplace by Facebook](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="39738-224">If you need to create a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="39738-225">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="39738-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="39738-226">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="39738-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workplace by Facebook.</span></span>

![Assegna utente][200] 

<span data-ttu-id="39738-228">**Per assegnare Britta Simon a Workplace by Facebook, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="39738-228">**To assign Britta Simon to Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="39738-229">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="39738-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="39738-231">Nell'elenco di applicazioni selezionare **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="39738-231">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="39738-233">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="39738-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="39738-235">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="39738-235">Click **Add** button.</span></span> <span data-ttu-id="39738-236">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="39738-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="39738-238">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="39738-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="39738-239">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="39738-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="39738-240">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="39738-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="39738-241">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="39738-241">Testing single sign-on</span></span>

<span data-ttu-id="39738-242">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="39738-242">If you want to test your single sign-on settings, open the Access Panel.</span></span>
<span data-ttu-id="39738-243">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="39738-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="39738-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="39738-244">Additional resources</span></span>

* [<span data-ttu-id="39738-245">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39738-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="39738-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39738-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="39738-247">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="39738-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

