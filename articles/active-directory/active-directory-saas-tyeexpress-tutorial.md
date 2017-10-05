---
title: 'Esercitazione: Integrazione di Azure Active Directory con T&E Express| Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e T&E Express.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 869e5284c71904fcc817ceee0f39d94fab1bc6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="7da5b-103">Esercitazione: Integrazione di Azure Active Directory con T&E Express</span><span class="sxs-lookup"><span data-stu-id="7da5b-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="7da5b-104">Questa esercitazione illustra come integrare T&E Express con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7da5b-104">In this tutorial, you learn how to integrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7da5b-105">L'integrazione di T&E Express con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7da5b-105">Integrating T&E Express with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7da5b-106">È possibile controllare in Azure AD chi può accedere a T&E Express</span><span class="sxs-lookup"><span data-stu-id="7da5b-106">You can control in Azure AD who has access to T&E Express</span></span>
- <span data-ttu-id="7da5b-107">È possibile abilitare gli utenti per l'accesso automatico a T&E Express (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="7da5b-107">You can enable your users to automatically get signed-on to T&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7da5b-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="7da5b-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="7da5b-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7da5b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7da5b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7da5b-110">Prerequisites</span></span>

<span data-ttu-id="7da5b-111">Per configurare l'integrazione di Azure AD con T&E Express, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7da5b-111">To configure Azure AD integration with T&E Express, you need the following items:</span></span>

- <span data-ttu-id="7da5b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7da5b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7da5b-113">Sottoscrizione di T&E Express abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7da5b-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7da5b-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7da5b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7da5b-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7da5b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7da5b-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="7da5b-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7da5b-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7da5b-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7da5b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="7da5b-118">Scenario description</span></span>
<span data-ttu-id="7da5b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="7da5b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7da5b-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7da5b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7da5b-121">Aggiunta di T&E Express dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7da5b-121">Adding T&E Express from the gallery</span></span>
2. <span data-ttu-id="7da5b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7da5b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-the-gallery"></a><span data-ttu-id="7da5b-123">Aggiungere T&E Express dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7da5b-123">Adding T&E Express from the gallery</span></span>
<span data-ttu-id="7da5b-124">Per configurare l'integrazione di T&E Express in Azure AD, è necessario aggiungere T&E Express dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="7da5b-124">To configure the integration of T&E Express into Azure AD, you need to add T&E Express from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7da5b-125">**Per aggiungere T&E Express dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7da5b-125">**To add T&E Express from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7da5b-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7da5b-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7da5b-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7da5b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7da5b-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7da5b-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="7da5b-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7da5b-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="7da5b-133">Digitare **T&E Express** nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="7da5b-133">In the search box, type **T&E Express**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="7da5b-135">Nel pannello dei risultati selezionare **T&E Express** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7da5b-135">In the results panel, select **T&E Express**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7da5b-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7da5b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7da5b-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con T&E Express usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7da5b-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7da5b-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente controparte di T&E Express che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7da5b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in T&E Express is to a user in Azure AD.</span></span> <span data-ttu-id="7da5b-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in T&E Express.</span><span class="sxs-lookup"><span data-stu-id="7da5b-140">In other words, a link relationship between an Azure AD user and the related user in T&E Express needs to be established.</span></span>

<span data-ttu-id="7da5b-141">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** di Azure AD come valore di **Username** (Nome utente) in T&E Express.</span><span class="sxs-lookup"><span data-stu-id="7da5b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in T&E Express.</span></span>

<span data-ttu-id="7da5b-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con T&E Express, è necessario completare i seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="7da5b-142">To configure and test Azure AD single sign-on with T&E Express, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7da5b-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7da5b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7da5b-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7da5b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7da5b-145">**[Creazione di un utente test di T&E Express](#creating-a-te-express-test-user)** : per avere una controparte di Britta Simon in T&E Express collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7da5b-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - to have a counterpart of Britta Simon in T&E Express that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7da5b-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7da5b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7da5b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="7da5b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7da5b-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7da5b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7da5b-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione T&E Express.</span><span class="sxs-lookup"><span data-stu-id="7da5b-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="7da5b-150">**Per configurare Single Sign-On di Azure AD con T&E Express, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7da5b-150">**To configure Azure AD single sign-on with T&E Express, perform the following steps:**</span></span>

1. <span data-ttu-id="7da5b-151">Nella pagina di integrazione dell'applicazione **T&E Express** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="7da5b-151">In the Azure Management portal, on the **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="7da5b-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="7da5b-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="7da5b-155">Nella sezione **URL e dominio T&E Express** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7da5b-155">On the **T&E Express Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="7da5b-157">a.</span><span class="sxs-lookup"><span data-stu-id="7da5b-157">a.</span></span> <span data-ttu-id="7da5b-158">Nella casella di testo **Identificatore** digitare il valore `https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="7da5b-158">In the **Identifier** textbox, type the value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="7da5b-159">b.</span><span class="sxs-lookup"><span data-stu-id="7da5b-159">b.</span></span> <span data-ttu-id="7da5b-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="7da5b-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7da5b-161">Si noti che questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="7da5b-161">Please note that these are not the real values.</span></span> <span data-ttu-id="7da5b-162">È necessario aggiornare questi valori con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="7da5b-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="7da5b-163">In questo caso è consigliabile usare in Identificatore il valore univoco della stringa.</span><span class="sxs-lookup"><span data-stu-id="7da5b-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="7da5b-164">Per ottenere questi valori, contattare il [team di supporto di T&E Express](http://www.tyeexpress.com/contacto.aspx).</span><span class="sxs-lookup"><span data-stu-id="7da5b-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) to get these values.</span></span>

5. <span data-ttu-id="7da5b-165">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="7da5b-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="7da5b-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="7da5b-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7da5b-169">Per configurare l'accesso Single Sign-On sul lato **T&E Express**, accedere all'applicazione T&E Express senza SAML Single Sign-On usando le credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="7da5b-169">To configure single sign-on on **T&E Express** side, login to the T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="7da5b-170">Nella scheda **Admin** fare clic su **SAML domain** (Dominio SAML) per aprire la pagina delle impostazioni di SAML.</span><span class="sxs-lookup"><span data-stu-id="7da5b-170">Under the **Admin** Tab, Click on **SAML domain** to Open the SAML settings page.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="7da5b-172">Spostare il selettore dell'opzione **Activar** (Attivare) da **NO** a **SI**.</span><span class="sxs-lookup"><span data-stu-id="7da5b-172">Select the **Activar(Activate)** option from **No** to **SI(Yes)**.</span></span> <span data-ttu-id="7da5b-173">Nella casella di testo **Identity Provider Metadata** (Metadati provider di identità) incollare il file XML dei metadati scaricato in precedenza dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7da5b-173">In the **Identity Provider Metadata** textbox, paste the metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="7da5b-175">Fare clic sul pulsante **Guardar** (Salva) per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="7da5b-175">Click on the **Guardar(Save)** button to save the settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7da5b-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7da5b-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="7da5b-177">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7da5b-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="7da5b-179">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7da5b-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7da5b-180">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7da5b-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7da5b-182">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="7da5b-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7da5b-184">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="7da5b-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7da5b-186">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7da5b-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7da5b-188">a.</span><span class="sxs-lookup"><span data-stu-id="7da5b-188">a.</span></span> <span data-ttu-id="7da5b-189">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7da5b-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7da5b-190">b.</span><span class="sxs-lookup"><span data-stu-id="7da5b-190">b.</span></span> <span data-ttu-id="7da5b-191">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7da5b-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7da5b-192">c.</span><span class="sxs-lookup"><span data-stu-id="7da5b-192">c.</span></span> <span data-ttu-id="7da5b-193">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="7da5b-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7da5b-194">d.</span><span class="sxs-lookup"><span data-stu-id="7da5b-194">d.</span></span> <span data-ttu-id="7da5b-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7da5b-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="7da5b-196">Creare un utente test di T&E Express</span><span class="sxs-lookup"><span data-stu-id="7da5b-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="7da5b-197">Per consentire agli utenti di Azure AD di accedere a T&E Express, è necessario eseguirne il provisioning in T&E Express.</span><span class="sxs-lookup"><span data-stu-id="7da5b-197">In order to enable Azure AD users to log into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="7da5b-198">Nel caso di T&E Express, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="7da5b-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="7da5b-199">**Per effettuare il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7da5b-199">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="7da5b-200">Accedere al sito aziendale di T&E Express come amministratore.</span><span class="sxs-lookup"><span data-stu-id="7da5b-200">Log in to your T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="7da5b-201">Sotto il tag Admin fare clic su Users (Utenti) per aprire la pagina master degli utenti.</span><span class="sxs-lookup"><span data-stu-id="7da5b-201">Under Admin tag, click on Users to open the Users master page.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="7da5b-203">Nella home page fare clic su **+** per aggiungere gli utenti.</span><span class="sxs-lookup"><span data-stu-id="7da5b-203">On the home page, click on **+** to add the users.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="7da5b-205">Immettere tutti i dettagli obbligatori richiesti nel modulo e fare clic sul pulsante di salvataggio per salvare i dettagli.</span><span class="sxs-lookup"><span data-stu-id="7da5b-205">Enter all the mandatory details as asked in the form and click the save button to save the details.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Aggiungere un dipendente](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7da5b-208">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7da5b-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7da5b-209">In questa sezione viene concesso a Britta Simon l'accesso a T&E Express per consentirle di usare l'accesso Single Sign-On di Azure.</span><span class="sxs-lookup"><span data-stu-id="7da5b-209">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to T&E Express.</span></span>

![Assegna utente][200] 

<span data-ttu-id="7da5b-211">**Per assegnare Britta Simon a T&E Express, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7da5b-211">**To assign Britta Simon to T&E Express, perform the following steps:**</span></span>

1. <span data-ttu-id="7da5b-212">Nel portale di gestione di Azure aprire la visualizzazione con le applicazioni e quindi passare alla visualizzazione con le directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7da5b-212">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="7da5b-214">Selezionare **T&E Express** dall'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7da5b-214">In the applications list, select **T&E Express**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="7da5b-216">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7da5b-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="7da5b-218">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7da5b-218">Click **Add** button.</span></span> <span data-ttu-id="7da5b-219">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7da5b-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="7da5b-221">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="7da5b-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7da5b-222">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7da5b-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7da5b-223">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7da5b-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7da5b-224">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7da5b-224">Testing single sign-on</span></span>

<span data-ttu-id="7da5b-225">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7da5b-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7da5b-226">Quando si fa clic sul riquadro T&E Express nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione T&E Express.</span><span class="sxs-lookup"><span data-stu-id="7da5b-226">When you click the T&E Express tile in the Access Panel, you should get automatically signed-on to your T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7da5b-227">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7da5b-227">Additional resources</span></span>

* [<span data-ttu-id="7da5b-228">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7da5b-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7da5b-229">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7da5b-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

