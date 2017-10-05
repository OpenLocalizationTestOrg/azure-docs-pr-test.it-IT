---
title: 'Esercitazione: Integrazione di Azure Active Directory con Jobscience | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Jobscience.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 66bec35a8f17482433dbf02827b90620d1cff378
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="b98ec-103">Esercitazione: Integrazione di Azure Active Directory con Jobscience</span><span class="sxs-lookup"><span data-stu-id="b98ec-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="b98ec-104">Questa esercitazione descrive come integrare Jobscience con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b98ec-104">In this tutorial, you learn how to integrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b98ec-105">L'integrazione di Jobscience con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b98ec-105">Integrating Jobscience with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b98ec-106">È possibile controllare in Azure AD chi può accedere a Jobscience</span><span class="sxs-lookup"><span data-stu-id="b98ec-106">You can control in Azure AD who has access to Jobscience</span></span>
- <span data-ttu-id="b98ec-107">È possibile abilitare gli utenti per l'accesso automatico a Jobscience (Single Sign-On) con gli account Azure AD</span><span class="sxs-lookup"><span data-stu-id="b98ec-107">You can enable your users to automatically get signed-on to Jobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b98ec-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b98ec-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b98ec-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b98ec-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b98ec-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b98ec-110">Prerequisites</span></span>

<span data-ttu-id="b98ec-111">Per configurare l'integrazione di Azure AD con Jobscience, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b98ec-111">To configure Azure AD integration with Jobscience, you need the following items:</span></span>

- <span data-ttu-id="b98ec-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b98ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b98ec-113">Sottoscrizione di Jobscience abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b98ec-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b98ec-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b98ec-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b98ec-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b98ec-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b98ec-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b98ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b98ec-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b98ec-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b98ec-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b98ec-118">Scenario description</span></span>
<span data-ttu-id="b98ec-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b98ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b98ec-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b98ec-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b98ec-121">Aggiunta di Jobscience dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b98ec-121">Adding Jobscience from the gallery</span></span>
2. <span data-ttu-id="b98ec-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b98ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-the-gallery"></a><span data-ttu-id="b98ec-123">Aggiunta di Jobscience dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b98ec-123">Adding Jobscience from the gallery</span></span>
<span data-ttu-id="b98ec-124">Per configurare l'integrazione di Jobscience in Azure AD, è necessario aggiungere Jobscience dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b98ec-124">To configure the integration of Jobscience into Azure AD, you need to add Jobscience from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b98ec-125">**Per aggiungere Jobscience dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b98ec-125">**To add Jobscience from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b98ec-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b98ec-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b98ec-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b98ec-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b98ec-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="b98ec-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b98ec-133">Nella casella di ricerca digitare **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-133">In the search box, type **Jobscience**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="b98ec-135">Nel pannello dei risultati selezionare **Jobscience** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b98ec-135">In the results panel, select **Jobscience**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b98ec-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b98ec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b98ec-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Jobscience in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b98ec-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b98ec-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve individuare l'utente di Jobscience corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b98ec-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobscience is to a user in Azure AD.</span></span> <span data-ttu-id="b98ec-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Jobscience.</span><span class="sxs-lookup"><span data-stu-id="b98ec-140">In other words, a link relationship between an Azure AD user and the related user in Jobscience needs to be established.</span></span>

<span data-ttu-id="b98ec-141">Per stabilire la relazione di collegamento, in Jobscience assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="b98ec-141">In Jobscience, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b98ec-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Jobscience, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b98ec-142">To configure and test Azure AD single sign-on with Jobscience, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b98ec-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b98ec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b98ec-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b98ec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b98ec-145">**[Creazione di un utente test di Jobscience](#creating-a-jobscience-test-user)**: per avere una controparte di Britta Simon in Jobscience collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b98ec-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - to have a counterpart of Britta Simon in Jobscience that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b98ec-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b98ec-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b98ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="b98ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b98ec-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b98ec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b98ec-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Jobscience.</span><span class="sxs-lookup"><span data-stu-id="b98ec-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="b98ec-150">**Per configurare l'accesso Single Sign-On di Azure AD con Jobscience, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b98ec-150">**To configure Azure AD single sign-on with Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="b98ec-151">Nella pagina di integrazione dell'applicazione **Jobscience** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-151">In the Azure portal, on the **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b98ec-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b98ec-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="b98ec-155">Nella sezione **URL e dominio Jobscience** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b98ec-155">On the **Jobscience Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="b98ec-157">Nella casella di testo **URL di accesso** digitare l'URL usando il criterio seguente: `http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="b98ec-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="b98ec-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="b98ec-158">This value is not real.</span></span> <span data-ttu-id="b98ec-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="b98ec-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b98ec-160">Ottenere questo valore dal [team di supporto clienti di Jobscience](https://www.jobscience.com/support) o dal profilo SSO che verrà creato come descritto più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b98ec-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from the SSO profile you will create which is explained later in the tutorial.</span></span> 
 
4. <span data-ttu-id="b98ec-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="b98ec-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="b98ec-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b98ec-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b98ec-165">Nella sezione **Configurazione di Jobscience** fare clic su **Configura Jobscience** per visualizzare la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-165">On the **Jobscience Configuration** section, click **Configure Jobscience** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b98ec-166">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="b98ec-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="b98ec-168">Accedere al sito aziendale di Jobscience come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b98ec-168">Log in to your Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="b98ec-169">Passare a **Setup**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-169">Go to **Setup**.</span></span>
   
   <span data-ttu-id="b98ec-170">![Installazione](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="b98ec-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="b98ec-171">Nella sezione **Administer** (Amministra) del riquadro di spostamento sinistro fare clic su **Domain Management** (Gestione dominio) per espandere la sezione correlata e quindi fare clic su **My Domain** (Dominio personale) per aprire la pagina **My Domain** (Dominio personale).</span><span class="sxs-lookup"><span data-stu-id="b98ec-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
   <span data-ttu-id="b98ec-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="b98ec-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="b98ec-173">Per verificare che il dominio sia stato configurato correttamente, verificare che sia presente in "**Step 4 Deployed to Users**" (Passaggio 4 Distribuzione agli utenti) e quindi verificare le selezioni in "**My Domain Settings**" (Impostazioni dominio personale).</span><span class="sxs-lookup"><span data-stu-id="b98ec-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="b98ec-174">![Domain Deployed to User](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed to User")</span><span class="sxs-lookup"><span data-stu-id="b98ec-174">![Domain Deployed to User](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="b98ec-175">Nel sito aziendale Jobscience fare clic su **Security Controls** (Controlli di sicurezza) e quindi fare clic su **Single Sign-On Settings** (Impostazioni Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="b98ec-175">On the Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="b98ec-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="b98ec-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="b98ec-177">Nella sezione **Single Sign-On Settings** , eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b98ec-177">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="b98ec-178">![Impostazioni di Single Sign-On](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Impostazioni di Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="b98ec-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="b98ec-179">a.</span><span class="sxs-lookup"><span data-stu-id="b98ec-179">a.</span></span> <span data-ttu-id="b98ec-180">Selezionare **Abilitato SAML**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="b98ec-181">b.</span><span class="sxs-lookup"><span data-stu-id="b98ec-181">b.</span></span> <span data-ttu-id="b98ec-182">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-182">Click **New**.</span></span>

13. <span data-ttu-id="b98ec-183">Nella finestra di dialogo **SAML Single Sign-On Setting Edit** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b98ec-183">On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="b98ec-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span><span class="sxs-lookup"><span data-stu-id="b98ec-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="b98ec-185">a.</span><span class="sxs-lookup"><span data-stu-id="b98ec-185">a.</span></span> <span data-ttu-id="b98ec-186">Nella casella di testo **Name** digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="b98ec-186">In the **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="b98ec-187">b.</span><span class="sxs-lookup"><span data-stu-id="b98ec-187">b.</span></span> <span data-ttu-id="b98ec-188">Nella casella di testo **Issuer** (Autorità emittente) incollare il valore dell'**ID entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b98ec-188">In **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b98ec-189">c.</span><span class="sxs-lookup"><span data-stu-id="b98ec-189">c.</span></span> <span data-ttu-id="b98ec-190">Nella casella di testo **Entity Id** (ID entità) digitare `https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="b98ec-190">In the **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="b98ec-191">d.</span><span class="sxs-lookup"><span data-stu-id="b98ec-191">d.</span></span> <span data-ttu-id="b98ec-192">Fare clic su **Browse** per caricare il certificato di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b98ec-192">Click **Browse** to upload your Azure AD certificate.</span></span>

    <span data-ttu-id="b98ec-193">e.</span><span class="sxs-lookup"><span data-stu-id="b98ec-193">e.</span></span> <span data-ttu-id="b98ec-194">In **SAML Identity Type** (Tipo di identità SAML) selezionare **Assertion contains the Federation ID from the User object** (L'asserzione contiene l'ID federazione dell'oggetto utente).</span><span class="sxs-lookup"><span data-stu-id="b98ec-194">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>

    <span data-ttu-id="b98ec-195">f.</span><span class="sxs-lookup"><span data-stu-id="b98ec-195">f.</span></span> <span data-ttu-id="b98ec-196">In **SAML Identity Location** (Percorso identità SAML) selezionare **Identity is in the NameIdentfier element of the Subject statement** (L'identità è nell'elemento NameIdentfier dell'istruzione Subject).</span><span class="sxs-lookup"><span data-stu-id="b98ec-196">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>

    <span data-ttu-id="b98ec-197">g.</span><span class="sxs-lookup"><span data-stu-id="b98ec-197">g.</span></span> <span data-ttu-id="b98ec-198">Nella casella di testo **Identity Provider Login URL** (URL accesso provider di identità) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b98ec-198">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b98ec-199">h.</span><span class="sxs-lookup"><span data-stu-id="b98ec-199">h.</span></span> <span data-ttu-id="b98ec-200">Nella casella di testo **Identity Provider Logout URL** (URL disconnessione provider di identità) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b98ec-200">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b98ec-201">i.</span><span class="sxs-lookup"><span data-stu-id="b98ec-201">i.</span></span> <span data-ttu-id="b98ec-202">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-202">Click **Save**.</span></span>

14. <span data-ttu-id="b98ec-203">Nella sezione **Administer** (Amministra) del riquadro di spostamento sinistro fare clic su **Domain Management** (Gestione dominio) per espandere la sezione correlata e quindi fare clic su **My Domain** (Dominio personale) per aprire la pagina **My Domain** (Dominio personale).</span><span class="sxs-lookup"><span data-stu-id="b98ec-203">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="b98ec-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="b98ec-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="b98ec-205">Nella sezione **Login Page Branding** (Personalizzazione pagina di accesso) della pagina **My Domain** (Dominio personale) fare clic su **Edit** (Modifica).</span><span class="sxs-lookup"><span data-stu-id="b98ec-205">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="b98ec-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="b98ec-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="b98ec-207">Nella sezione**Authentication Service** (Servizio autenticazione) della pagina **Login Page Branding** (Personalizzazione pagina di accesso) viene visualizzato il nome delle **impostazioni SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-207">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="b98ec-208">Selezionarlo e quindi fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="b98ec-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="b98ec-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="b98ec-210">Per ottenere l'URL di accesso Single Sign-On avviato dal provider di servizi, fare clic su **Single Sign-On Settings** (Impostazioni Single Sign-On) nella sezione di menu **Security Controls** (Controlli di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="b98ec-210">To get the SP initiated Single Sign on Login URL click on the **Single Sign On settings** in the **Security Controls** menu section.</span></span>

    <span data-ttu-id="b98ec-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="b98ec-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="b98ec-212">Fare clic sul profilo SSO creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="b98ec-212">Click the SSO profile you have created in the step above.</span></span> <span data-ttu-id="b98ec-213">Questa pagina mostra l'URL di accesso Single Sign-On della società, ad esempio [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span><span class="sxs-lookup"><span data-stu-id="b98ec-213">This page shows the Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="b98ec-214">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b98ec-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b98ec-215">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="b98ec-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b98ec-216">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b98ec-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b98ec-217">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b98ec-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="b98ec-218">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b98ec-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b98ec-220">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b98ec-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b98ec-221">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b98ec-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b98ec-223">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="b98ec-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b98ec-225">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b98ec-227">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b98ec-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b98ec-229">a.</span><span class="sxs-lookup"><span data-stu-id="b98ec-229">a.</span></span> <span data-ttu-id="b98ec-230">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b98ec-231">b.</span><span class="sxs-lookup"><span data-stu-id="b98ec-231">b.</span></span> <span data-ttu-id="b98ec-232">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b98ec-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b98ec-233">c.</span><span class="sxs-lookup"><span data-stu-id="b98ec-233">c.</span></span> <span data-ttu-id="b98ec-234">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b98ec-235">d.</span><span class="sxs-lookup"><span data-stu-id="b98ec-235">d.</span></span> <span data-ttu-id="b98ec-236">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="b98ec-237">Creazione di un utente test di Jobscience</span><span class="sxs-lookup"><span data-stu-id="b98ec-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="b98ec-238">Per consentire agli utenti di Azure AD di accedere a Jobscience, è necessario eseguirne il provisioning in Jobscience.</span><span class="sxs-lookup"><span data-stu-id="b98ec-238">In order to enable Azure AD users to log in to Jobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="b98ec-239">Nel caso di Jobscience, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="b98ec-239">In the case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="b98ec-240">È possibile usare qualsiasi altro strumento o API di creazione di account utente offerta da Jobscience per eseguire il provisioning degli account utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b98ec-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="b98ec-241">**Per configurare il provisioning utenti, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b98ec-241">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="b98ec-242">Accedere al sito aziendale di **Jobscience** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b98ec-242">Log in to your **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="b98ec-243">Passare a Setup (Installazione).</span><span class="sxs-lookup"><span data-stu-id="b98ec-243">Go to Setup.</span></span>
   
   <span data-ttu-id="b98ec-244">![Installazione](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="b98ec-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="b98ec-245">Passare a **Manage Users (Gestisci utenti) \> Users (Utenti)**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-245">Go to **Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="b98ec-246">![Utenti](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="b98ec-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="b98ec-247">Fare clic su **Nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-247">Click **New User**.</span></span>
   
   <span data-ttu-id="b98ec-248">![Tutti gli utenti](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Tutti gli utenti")</span><span class="sxs-lookup"><span data-stu-id="b98ec-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="b98ec-249">Nella finestra di dialogo **Edit User** seguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b98ec-249">On the **Edit User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="b98ec-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span><span class="sxs-lookup"><span data-stu-id="b98ec-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="b98ec-251">a.</span><span class="sxs-lookup"><span data-stu-id="b98ec-251">a.</span></span> <span data-ttu-id="b98ec-252">Nella casella di testo **First Name** (Nome) digitare il nome dell'utente, ad esempio Britta.</span><span class="sxs-lookup"><span data-stu-id="b98ec-252">In the **First Name** textbox, type a first name of the user like Britta.</span></span>
   
   <span data-ttu-id="b98ec-253">b.</span><span class="sxs-lookup"><span data-stu-id="b98ec-253">b.</span></span> <span data-ttu-id="b98ec-254">Nella casella **Last Name** (Cognome) digitare il cognome dell'utente, ad esempio Simon.</span><span class="sxs-lookup"><span data-stu-id="b98ec-254">In the **Last Name** textbox, type a last name of the user like Simon.</span></span>
   
   <span data-ttu-id="b98ec-255">c.</span><span class="sxs-lookup"><span data-stu-id="b98ec-255">c.</span></span> <span data-ttu-id="b98ec-256">Nella casella di testo **Alias** digitare un nome alias dell'utente, ad esempio brittas.</span><span class="sxs-lookup"><span data-stu-id="b98ec-256">In the **Alias** textbox, type an alias name of the user like brittas.</span></span>

   <span data-ttu-id="b98ec-257">d.</span><span class="sxs-lookup"><span data-stu-id="b98ec-257">d.</span></span> <span data-ttu-id="b98ec-258">Nella casella di testo **Email** digitare l'indirizzo di posta elettronica dell'utente, ad esempio Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="b98ec-258">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="b98ec-259">e.</span><span class="sxs-lookup"><span data-stu-id="b98ec-259">e.</span></span> <span data-ttu-id="b98ec-260">Nella casella di testo **User Name** (Nome utente) digitare il nome utente dell'utente, ad esempio Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="b98ec-260">In the **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="b98ec-261">f.</span><span class="sxs-lookup"><span data-stu-id="b98ec-261">f.</span></span> <span data-ttu-id="b98ec-262">Nella casella di testo **Nick Name** (Nome alternativo) digitare un nome alternativo dell'utente, ad esempio Simon.</span><span class="sxs-lookup"><span data-stu-id="b98ec-262">In the **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="b98ec-263">g.</span><span class="sxs-lookup"><span data-stu-id="b98ec-263">g.</span></span> <span data-ttu-id="b98ec-264">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="b98ec-265">Il titolare dell'account Azure Active Directory riceve un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="b98ec-265">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b98ec-266">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b98ec-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b98ec-267">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Jobscience.</span><span class="sxs-lookup"><span data-stu-id="b98ec-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobscience.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b98ec-269">**Per assegnare Britta Simon a Jobscience, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b98ec-269">**To assign Britta Simon to Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="b98ec-270">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b98ec-272">Nell'elenco di applicazioni selezionare **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-272">In the applications list, select **Jobscience**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="b98ec-274">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b98ec-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b98ec-276">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-276">Click **Add** button.</span></span> <span data-ttu-id="b98ec-277">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b98ec-279">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="b98ec-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b98ec-280">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b98ec-281">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b98ec-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b98ec-282">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b98ec-282">Testing single sign-on</span></span>

<span data-ttu-id="b98ec-283">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b98ec-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b98ec-284">Quando si fa clic sul riquadro Jobscience nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Jobscience.</span><span class="sxs-lookup"><span data-stu-id="b98ec-284">When you click the Jobscience tile in the Access Panel, you should get automatically signed-on to your Jobscience application.</span></span>
<span data-ttu-id="b98ec-285">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b98ec-285">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b98ec-286">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b98ec-286">Additional resources</span></span>

* [<span data-ttu-id="b98ec-287">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b98ec-287">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b98ec-288">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b98ec-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

