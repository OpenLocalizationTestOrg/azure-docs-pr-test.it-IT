---
title: 'Esercitazione: Integrazione di Azure Active Directory con Teamwork | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Teamwork.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: edd2f9446515531f1147a8abf99295b618b89b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="df2ef-103">Esercitazione: Integrazione di Azure Active Directory con Teamwork</span><span class="sxs-lookup"><span data-stu-id="df2ef-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="df2ef-104">Questa esercitazione descrive come integrare Teamwork con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="df2ef-104">In this tutorial, you learn how to integrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df2ef-105">L'integrazione di Teamwork con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="df2ef-105">Integrating Teamwork with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="df2ef-106">È possibile controllare in Azure AD chi può accedere a Teamwork.</span><span class="sxs-lookup"><span data-stu-id="df2ef-106">You can control in Azure AD who has access to Teamwork</span></span>
- <span data-ttu-id="df2ef-107">È possibile abilitare gli utenti per l'accesso automatico a Teamwork (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df2ef-107">You can enable your users to automatically get signed-on to Teamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="df2ef-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="df2ef-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="df2ef-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df2ef-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df2ef-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="df2ef-110">Prerequisites</span></span>

<span data-ttu-id="df2ef-111">Per configurare l'integrazione di Azure AD con Teamwork, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="df2ef-111">To configure Azure AD integration with Teamwork, you need the following items:</span></span>

- <span data-ttu-id="df2ef-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df2ef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df2ef-113">Sottoscrizione di Teamwork abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="df2ef-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="df2ef-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="df2ef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="df2ef-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="df2ef-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="df2ef-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="df2ef-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="df2ef-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df2ef-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="df2ef-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="df2ef-118">Scenario description</span></span>
<span data-ttu-id="df2ef-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="df2ef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="df2ef-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="df2ef-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df2ef-121">Aggiunta di Teamwork dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="df2ef-121">Adding Teamwork from the gallery</span></span>
2. <span data-ttu-id="df2ef-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="df2ef-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-the-gallery"></a><span data-ttu-id="df2ef-123">Aggiunta di Teamwork dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="df2ef-123">Adding Teamwork from the gallery</span></span>
<span data-ttu-id="df2ef-124">Per configurare l'integrazione di Teamwork in Azure AD, è necessario aggiungere Teamwork dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="df2ef-124">To configure the integration of Teamwork into Azure AD, you need to add Teamwork from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="df2ef-125">**Per aggiungere Teamwork dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="df2ef-125">**To add Teamwork from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="df2ef-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="df2ef-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="df2ef-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="df2ef-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="df2ef-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="df2ef-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="df2ef-133">Nella casella di ricerca digitare **Teamwork**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-133">In the search box, type **Teamwork**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="df2ef-135">Nel pannello dei risultati selezionare **Teamwork** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="df2ef-135">In the results panel, select **Teamwork**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="df2ef-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="df2ef-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="df2ef-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Teamwork in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="df2ef-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="df2ef-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Teamwork che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df2ef-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamwork is to a user in Azure AD.</span></span> <span data-ttu-id="df2ef-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Teamwork.</span><span class="sxs-lookup"><span data-stu-id="df2ef-140">In other words, a link relationship between an Azure AD user and the related user in Teamwork needs to be established.</span></span>

<span data-ttu-id="df2ef-141">La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Username** in Teamwork.</span><span class="sxs-lookup"><span data-stu-id="df2ef-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamwork.</span></span>

<span data-ttu-id="df2ef-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Teamwork, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="df2ef-142">To configure and test Azure AD single sign-on with Teamwork, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="df2ef-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="df2ef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="df2ef-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df2ef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df2ef-145">**[Creazione di un utente test di Teamwork](#creating-a-teamwork-test-user)**: per avere una controparte di Britta Simon in Tidemark collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df2ef-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - to have a counterpart of Britta Simon in Teamwork that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="df2ef-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df2ef-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df2ef-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="df2ef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="df2ef-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="df2ef-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="df2ef-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Teamwork.</span><span class="sxs-lookup"><span data-stu-id="df2ef-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="df2ef-150">**Per configurare Single Sign-On di Azure AD con Teamwork, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="df2ef-150">**To configure Azure AD single sign-on with Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="df2ef-151">Nella pagina di integrazione dell'applicazione **Teamwork** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-151">In the Azure Management portal, on the **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="df2ef-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="df2ef-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="df2ef-155">Nella casella di testo **URL di accesso** della sezione **URL e dominio di Teamwork** digitare un URL usando il modello seguente: `https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="df2ef-155">On the **Teamwork Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="df2ef-157">Si noti che questo non è il valore reale.</span><span class="sxs-lookup"><span data-stu-id="df2ef-157">Please note that this is not the real value.</span></span> <span data-ttu-id="df2ef-158">È necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="df2ef-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="df2ef-159">Per ottenere tale valore, contattare il [team di supporto di Teamwork](mailto:support@teamwork.com).</span><span class="sxs-lookup"><span data-stu-id="df2ef-159">Contact [Teamwork support team](mailto:support@teamwork.com) to get this value.</span></span> 

4. <span data-ttu-id="df2ef-160">Nella sezione **Certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="df2ef-162">Nella finestra di dialogo **Crea nuovo certificato** fare clic sull'icona del calendario e selezionare una **data di scadenza**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="df2ef-163">Fare quindi clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-163">Then click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="df2ef-165">Nella sezione **Certificato di firma SAML** selezionare **Make new certificate active** (Rendi attivo il nuovo certificato) e fare clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="df2ef-167">Nella finestra popup **Rollover certificate** (Certificato di rollover) fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="df2ef-169">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="df2ef-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="df2ef-171">Per ottenere la configurazione dell'accesso Single Sign-On per l'applicazione, contattare il [team di supporto di Teamwork](mailto:support@teamwork.com) e fornire i **metadati** scaricati.</span><span class="sxs-lookup"><span data-stu-id="df2ef-171">To get SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with the downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="df2ef-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="df2ef-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="df2ef-173">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="df2ef-173">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="df2ef-175">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="df2ef-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="df2ef-176">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="df2ef-176">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="df2ef-178">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="df2ef-178">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="df2ef-180">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-180">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="df2ef-182">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="df2ef-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="df2ef-184">a.</span><span class="sxs-lookup"><span data-stu-id="df2ef-184">a.</span></span> <span data-ttu-id="df2ef-185">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="df2ef-186">b.</span><span class="sxs-lookup"><span data-stu-id="df2ef-186">b.</span></span> <span data-ttu-id="df2ef-187">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="df2ef-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="df2ef-188">c.</span><span class="sxs-lookup"><span data-stu-id="df2ef-188">c.</span></span> <span data-ttu-id="df2ef-189">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="df2ef-190">d.</span><span class="sxs-lookup"><span data-stu-id="df2ef-190">d.</span></span> <span data-ttu-id="df2ef-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="df2ef-192">Creazione di un utente test Teamwork</span><span class="sxs-lookup"><span data-stu-id="df2ef-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="df2ef-193">In questa sezione viene creato un utente chiamato Britta Simon in Teamwork.</span><span class="sxs-lookup"><span data-stu-id="df2ef-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="df2ef-194">Collaborare con il [team di supporto di Teamwork](mailto:support@teamwork.com) per aggiungere gli utenti alla piattaforma Teamwork.</span><span class="sxs-lookup"><span data-stu-id="df2ef-194">Please work with [Teamwork support team](mailto:support@teamwork.com) to add the users in the Teamwork platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="df2ef-195">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="df2ef-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="df2ef-196">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Teamwork.</span><span class="sxs-lookup"><span data-stu-id="df2ef-196">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamwork.</span></span>

![Assegna utente][200] 

<span data-ttu-id="df2ef-198">**Per assegnare Britta Simon a Teamwork, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="df2ef-198">**To assign Britta Simon to Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="df2ef-199">Nel portale di gestione di Azure aprire la visualizzazione applicazioni, passare alla visualizzazione directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-199">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="df2ef-201">Nell'elenco delle applicazioni selezionare **Teamwork**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-201">In the applications list, select **Teamwork**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="df2ef-203">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="df2ef-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="df2ef-205">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-205">Click **Add** button.</span></span> <span data-ttu-id="df2ef-206">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="df2ef-208">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="df2ef-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="df2ef-209">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="df2ef-210">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="df2ef-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="df2ef-211">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="df2ef-211">Testing single sign-on</span></span>

<span data-ttu-id="df2ef-212">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="df2ef-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="df2ef-213">Quando si fa clic sul riquadro Teamwork nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Teamwork.</span><span class="sxs-lookup"><span data-stu-id="df2ef-213">When you click the Teamwork tile in the Access Panel, you should get automatically signed-on to your Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="df2ef-214">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="df2ef-214">Additional resources</span></span>

* [<span data-ttu-id="df2ef-215">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df2ef-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df2ef-216">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df2ef-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png