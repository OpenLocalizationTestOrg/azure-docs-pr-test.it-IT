---
title: 'Esercitazione: Integrazione di Azure Active Directory con LearnUpon | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e LearnUpon.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: b6ac8acc244e9029be01ede5e0865c280171217d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="2e24e-103">Esercitazione: Integrazione di Azure Active Directory con LearnUpon</span><span class="sxs-lookup"><span data-stu-id="2e24e-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="2e24e-104">Questa esercitazione descrive come integrare LearnUpon con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e24e-104">In this tutorial, you learn how to integrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e24e-105">L'integrazione di LearnUpon con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e24e-105">Integrating LearnUpon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2e24e-106">È possibile controllare in Azure AD chi può accedere a LearnUpon</span><span class="sxs-lookup"><span data-stu-id="2e24e-106">You can control in Azure AD who has access to LearnUpon</span></span>
- <span data-ttu-id="2e24e-107">È possibile abilitare gli utenti per l'accesso automatico a LearnUpon (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e24e-107">You can enable your users to automatically get signed-on to LearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2e24e-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e24e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2e24e-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e24e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e24e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2e24e-110">Prerequisites</span></span>

<span data-ttu-id="2e24e-111">Per configurare l'integrazione di Azure AD con LearnUpon, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e24e-111">To configure Azure AD integration with LearnUpon, you need the following items:</span></span>

- <span data-ttu-id="2e24e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e24e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e24e-113">Sottoscrizione di LearnUpon abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2e24e-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e24e-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2e24e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2e24e-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e24e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e24e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2e24e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2e24e-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e24e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e24e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2e24e-118">Scenario description</span></span>
<span data-ttu-id="2e24e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2e24e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e24e-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e24e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e24e-121">Aggiunta di LearnUpon dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2e24e-121">Adding LearnUpon from the gallery</span></span>
2. <span data-ttu-id="2e24e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e24e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-the-gallery"></a><span data-ttu-id="2e24e-123">Aggiunta di LearnUpon dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2e24e-123">Adding LearnUpon from the gallery</span></span>
<span data-ttu-id="2e24e-124">Per configurare l'integrazione di LearnUpon in Azure AD, è necessario aggiungere LearnUpon dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2e24e-124">To configure the integration of LearnUpon into Azure AD, you need to add LearnUpon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2e24e-125">**Per aggiungere LearnUpon dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2e24e-125">**To add LearnUpon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2e24e-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2e24e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2e24e-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2e24e-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="2e24e-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="2e24e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="2e24e-133">Nella casella di ricerca digitare **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-133">In the search box, type **LearnUpon**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="2e24e-135">Nel pannello dei risultati selezionare **LearnUpon** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2e24e-135">In the results panel, select **LearnUpon**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2e24e-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e24e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2e24e-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LearnUpon in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2e24e-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e24e-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di LearnUpon che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e24e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LearnUpon is to a user in Azure AD.</span></span> <span data-ttu-id="2e24e-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="2e24e-140">In other words, a link relationship between an Azure AD user and the related user in LearnUpon needs to be established.</span></span>

<span data-ttu-id="2e24e-141">Per stabilire la relazione di collegamento, in LearnUpon assegnare il valore del **nome utente** di Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-141">In LearnUpon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2e24e-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con LearnUpon, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e24e-142">To configure and test Azure AD single sign-on with LearnUpon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2e24e-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2e24e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2e24e-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e24e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e24e-145">**[Creazione di un utente test LearnUpon](#creating-a-learnupon-test-user)** : per avere una controparte di Britta Simon in LearnUpon collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e24e-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - to have a counterpart of Britta Simon in LearnUpon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2e24e-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e24e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e24e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="2e24e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2e24e-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e24e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2e24e-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="2e24e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="2e24e-150">**Per configurare Single Sign-On di Azure AD con LearnUpon, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2e24e-150">**To configure Azure AD single sign-on with LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="2e24e-151">Nella pagina di integrazione dell'applicazione **LearnUpon** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-151">In the Azure portal, on the **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="2e24e-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="2e24e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="2e24e-155">Nella sezione **URL e dominio LearnUpon** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2e24e-155">On the **LearnUpon Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="2e24e-157">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="2e24e-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2e24e-158">Si noti che questo non è il valore reale.</span><span class="sxs-lookup"><span data-stu-id="2e24e-158">Please note that this is not the real value.</span></span> <span data-ttu-id="2e24e-159">È necessario aggiornare questo valore con l'URL di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="2e24e-159">you have to update this value with the actual Reply URL.</span></span> <span data-ttu-id="2e24e-160">Per ottenere il valore, contattare il [team di supporto di LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="2e24e-160">To get this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="2e24e-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificate (Raw)** (Certificato (base)) e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="2e24e-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="2e24e-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="2e24e-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2e24e-165">Nella sezione **Configurazione di LearnUpon** fare clic su **Configura LearnUpon** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-165">On the **LearnUpon Configuration** section, click **Configure LearnUpon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2e24e-166">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="2e24e-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="2e24e-168">Aprire un'altra istanza del browser e accedere a LearnUpon con un account amministratore.</span><span class="sxs-lookup"><span data-stu-id="2e24e-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="2e24e-169">Fare clic sulla scheda **Impostazioni** .</span><span class="sxs-lookup"><span data-stu-id="2e24e-169">Click the **settings** tab.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="2e24e-171">Fare clic su **Single Sign On - SAML** e quindi fare clic su **General Settings** (Impostazioni generali) per configurare le impostazioni SAML.</span><span class="sxs-lookup"><span data-stu-id="2e24e-171">Click **Single Sign On - SAML**, and then click **General Settings** to configure SAML settings.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="2e24e-173">Nella sezione **General Settings** (Impostazioni generali), seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2e24e-173">In the **General Settings** section, perform the following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="2e24e-175">a.</span><span class="sxs-lookup"><span data-stu-id="2e24e-175">a.</span></span> <span data-ttu-id="2e24e-176">Selezionare **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-176">Select **Enabled**.</span></span>

    <span data-ttu-id="2e24e-177">b.</span><span class="sxs-lookup"><span data-stu-id="2e24e-177">b.</span></span> <span data-ttu-id="2e24e-178">Per **Version** selezionare **2.0**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="2e24e-179">c.</span><span class="sxs-lookup"><span data-stu-id="2e24e-179">c.</span></span> <span data-ttu-id="2e24e-180">Per **Skip conditions** (Ignorare le condizioni) selezionare **No**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="2e24e-181">d.</span><span class="sxs-lookup"><span data-stu-id="2e24e-181">d.</span></span> <span data-ttu-id="2e24e-182">Nella casella di testo **SAML Token Post param name** (Nome parametro POST di richiesta token SAML) digitare il nome del parametro POST di richiesta all'URL del consumer SAML indicato in precedenza che contiene l'asserzione SAML da verificare e autenticare, ad esempio **SAMLResponse**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-182">In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="2e24e-183">e.</span><span class="sxs-lookup"><span data-stu-id="2e24e-183">e.</span></span> <span data-ttu-id="2e24e-184">Nella casella di testo **Name Identifier Format** (Formato identificatore nome) digitare il valore che indica la posizione dell'identificatore degli utenti (indirizzo di posta elettronica) nell'asserzione SAML, ad esempio **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-184">In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="2e24e-185">f.</span><span class="sxs-lookup"><span data-stu-id="2e24e-185">f.</span></span> <span data-ttu-id="2e24e-186">Nella casella di testo **Identify Provider Location** (Identificare il percorso del provider) digitare il valore che indica il percorso a cui verranno indirizzati gli utenti quando fanno clic sull'icona caricata dalla schermata di accesso del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e24e-186">In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="2e24e-187">g.</span><span class="sxs-lookup"><span data-stu-id="2e24e-187">g.</span></span> <span data-ttu-id="2e24e-188">Nella casella di testo **Sign out URL** (URL di disconnessione) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e24e-188">In the **Sign out URL** textbox, paste the **Sign-Out URL** which you have copied from the Azure portal.</span></span>
    
    <span data-ttu-id="2e24e-189">h.</span><span class="sxs-lookup"><span data-stu-id="2e24e-189">h.</span></span> <span data-ttu-id="2e24e-190">Fare clic su **Manage finger prints**(Gestione impronte digitali) e quindi caricare l'impronta digitale del certificato scaricato.</span><span class="sxs-lookup"><span data-stu-id="2e24e-190">Click **Manage finger prints**, and then upload the finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="2e24e-191">Fare clic su **User Settings**(Impostazioni utente), e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2e24e-191">Click **User Settings**, and then perform the following steps:</span></span>
   
     ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="2e24e-193">a.</span><span class="sxs-lookup"><span data-stu-id="2e24e-193">a.</span></span> <span data-ttu-id="2e24e-194">Nella casella di testo **First Name Identifier Format** (Formato identificatore nome) digitare il valore che indica la posizione del nome degli utenti dell'asserzione SAML, ad esempio **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-194">In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="2e24e-195">b.</span><span class="sxs-lookup"><span data-stu-id="2e24e-195">b.</span></span> <span data-ttu-id="2e24e-196">Nella casella di testo **Last Name Identifier Format** (Formato identificatore cognome) digitare il valore che indica la posizione del cognome degli utenti dell'asserzione SAML, ad esempio **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-196">In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="2e24e-197">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="2e24e-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2e24e-198">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="2e24e-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2e24e-199">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e24e-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2e24e-200">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e24e-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="2e24e-201">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e24e-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="2e24e-203">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2e24e-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2e24e-204">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2e24e-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2e24e-206">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="2e24e-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2e24e-208">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2e24e-210">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2e24e-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2e24e-212">a.</span><span class="sxs-lookup"><span data-stu-id="2e24e-212">a.</span></span> <span data-ttu-id="2e24e-213">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e24e-214">b.</span><span class="sxs-lookup"><span data-stu-id="2e24e-214">b.</span></span> <span data-ttu-id="2e24e-215">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2e24e-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2e24e-216">c.</span><span class="sxs-lookup"><span data-stu-id="2e24e-216">c.</span></span> <span data-ttu-id="2e24e-217">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2e24e-218">d.</span><span class="sxs-lookup"><span data-stu-id="2e24e-218">d.</span></span> <span data-ttu-id="2e24e-219">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="2e24e-220">Creazione di un utente test LearnUpon</span><span class="sxs-lookup"><span data-stu-id="2e24e-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="2e24e-221">Questa sezione descrive come creare un utente chiamato Britta Simon in LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="2e24e-221">The objective of this section is to create a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="2e24e-222">LearnUpon supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2e24e-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="2e24e-223">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="2e24e-223">There is no action item for you in this section.</span></span> <span data-ttu-id="2e24e-224">Durante un tentativo di accesso a LearnUpon verrà creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="2e24e-224">A new user will be created during an attempt to access LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="2e24e-225">[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="2e24e-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="2e24e-226">Per creare un utente manualmente, è necessario contattare il [team di supporto di LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="2e24e-226">If you need to create an user manually, you need to contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2e24e-227">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e24e-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2e24e-228">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="2e24e-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LearnUpon.</span></span>

![Assegna utente][200] 

<span data-ttu-id="2e24e-230">**Per assegnare Britta Simon a LearnUpon, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2e24e-230">**To assign Britta Simon to LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="2e24e-231">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2e24e-233">Nell'elenco di applicazioni selezionare **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-233">In the applications list, select **LearnUpon**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="2e24e-235">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="2e24e-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="2e24e-237">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-237">Click **Add** button.</span></span> <span data-ttu-id="2e24e-238">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="2e24e-240">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="2e24e-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2e24e-241">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2e24e-242">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2e24e-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2e24e-243">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2e24e-243">Testing single sign-on</span></span>

<span data-ttu-id="2e24e-244">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2e24e-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2e24e-245">Quando si fa clic sul riquadro LearnUpon nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="2e24e-245">When you click the LearnUpon tile in the Access Panel, you should get automatically signed-on to your LearnUpon application.</span></span>
<span data-ttu-id="2e24e-246">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2e24e-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2e24e-247">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2e24e-247">Additional resources</span></span>

* [<span data-ttu-id="2e24e-248">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e24e-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e24e-249">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e24e-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

