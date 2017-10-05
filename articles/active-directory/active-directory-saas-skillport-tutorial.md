---
title: 'Esercitazione: Integrazione di Azure Active Directory con Skillport | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Skillport.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 668fc5ae4f964bd776904c3a9dbc2b203689d50c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="738a3-103">Esercitazione: Integrazione di Azure Active Directory con Skillport</span><span class="sxs-lookup"><span data-stu-id="738a3-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="738a3-104">Questa esercitazione descrive come integrare Skillport con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="738a3-104">In this tutorial, you learn how to integrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="738a3-105">L'integrazione di Skillport con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="738a3-105">Integrating Skillport with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="738a3-106">È possibile controllare in Azure AD chi può accedere a Skillport</span><span class="sxs-lookup"><span data-stu-id="738a3-106">You can control in Azure AD who has access to Skillport</span></span>
- <span data-ttu-id="738a3-107">È possibile abilitare gli utenti per l'accesso automatico a Skillport (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="738a3-107">You can enable your users to automatically get signed-on to Skillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="738a3-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="738a3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="738a3-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="738a3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="738a3-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="738a3-110">Prerequisites</span></span>

<span data-ttu-id="738a3-111">Per configurare l'integrazione di Azure AD con Skillport, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="738a3-111">To configure Azure AD integration with Skillport, you need the following items:</span></span>

- <span data-ttu-id="738a3-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="738a3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="738a3-113">Sottoscrizione di Skillport abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="738a3-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="738a3-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="738a3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="738a3-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="738a3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="738a3-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="738a3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="738a3-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="738a3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="738a3-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="738a3-118">Scenario description</span></span>
<span data-ttu-id="738a3-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="738a3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="738a3-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="738a3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="738a3-121">Aggiunta di Skillport dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="738a3-121">Adding Skillport from the gallery</span></span>
2. <span data-ttu-id="738a3-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="738a3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-the-gallery"></a><span data-ttu-id="738a3-123">Aggiunta di Skillport dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="738a3-123">Adding Skillport from the gallery</span></span>
<span data-ttu-id="738a3-124">Per configurare l'integrazione di Skillport in Azure AD, è necessario aggiungere Skillport dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="738a3-124">To configure the integration of Skillport into Azure AD, you need to add Skillport from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="738a3-125">**Per aggiungere Skillport dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="738a3-125">**To add Skillport from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="738a3-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="738a3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="738a3-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="738a3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="738a3-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="738a3-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="738a3-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="738a3-131">Click **New Application** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="738a3-133">Nella casella di ricerca digitare **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="738a3-133">In the search box, type **Skillport**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="738a3-135">Nel pannello dei risultati selezionare **Skillport** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="738a3-135">In the results panel, select **Skillport**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="738a3-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="738a3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="738a3-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Skillport usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="738a3-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="738a3-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Skillport corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="738a3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Skillport is to a user in Azure AD.</span></span> <span data-ttu-id="738a3-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Skillport.</span><span class="sxs-lookup"><span data-stu-id="738a3-140">In other words, a link relationship between an Azure AD user and the related user in Skillport needs to be established.</span></span>

<span data-ttu-id="738a3-141">Per stabilire la relazione di collegamento, assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente) in Skillport.</span><span class="sxs-lookup"><span data-stu-id="738a3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Skillport.</span></span>

<span data-ttu-id="738a3-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Skillport, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="738a3-142">To configure and test Azure AD single sign-on with Skillport, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="738a3-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="738a3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="738a3-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="738a3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="738a3-145">**[Creazione di un utente di test di Skillport](#creating-a-skillport-test-user)**: per avere una controparte di Britta Simon in Skillport collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="738a3-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - to have a counterpart of Britta Simon in Skillport that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="738a3-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="738a3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="738a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="738a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="738a3-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="738a3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="738a3-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Skillport.</span><span class="sxs-lookup"><span data-stu-id="738a3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="738a3-150">**Per configurare l'accesso Single Sign-On di Azure AD con Skillport, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="738a3-150">**To configure Azure AD single sign-on with Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="738a3-151">Nella pagina di integrazione dell'applicazione **Skillport** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="738a3-151">In the Azure  portal, on the **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="738a3-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="738a3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="738a3-155">Nella sezione **URL e dominio Skillport** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="738a3-155">On the **Skillport Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="738a3-157">a.</span><span class="sxs-lookup"><span data-stu-id="738a3-157">a.</span></span> <span data-ttu-id="738a3-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="738a3-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span>
      
      <span data-ttu-id="738a3-159">Data center UE: `https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="738a3-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="738a3-160">Data center USA: `https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="738a3-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="738a3-161">b.</span><span class="sxs-lookup"><span data-stu-id="738a3-161">b.</span></span> <span data-ttu-id="738a3-162">Nella casella di testo **URL di risposta** digitare l'URL usando i modelli seguenti:</span><span class="sxs-lookup"><span data-stu-id="738a3-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span>
    
      <span data-ttu-id="738a3-163">Data center UE: `https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="738a3-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="738a3-164">Data center USA: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="738a3-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="738a3-165">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="738a3-165">These values are not the real.</span></span> <span data-ttu-id="738a3-166">è necessario aggiornarli con l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="738a3-166">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="738a3-167">Per ottenere questi valori, contattare il [team di supporto clienti di Skillport](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="738a3-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) to get these values.</span></span>
 
4. <span data-ttu-id="738a3-168">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="738a3-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="738a3-170">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="738a3-170">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="738a3-172">Per configurare l'accesso Single Sign-On sul lato **Skillport**, è necessario inviare il file **XML metadati** scaricato al [team di supporto di Skillport](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="738a3-172">To configure single sign-on on **Skillport** side, you need to send the downloaded **Metadata XML** to [Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="738a3-173">La configurazione verrà eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="738a3-173">They will set it up to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="738a3-174">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="738a3-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="738a3-175">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="738a3-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="738a3-177">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="738a3-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="738a3-178">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="738a3-178">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="738a3-180">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="738a3-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="738a3-182">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="738a3-182">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="738a3-184">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="738a3-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="738a3-186">a.</span><span class="sxs-lookup"><span data-stu-id="738a3-186">a.</span></span> <span data-ttu-id="738a3-187">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="738a3-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="738a3-188">b.</span><span class="sxs-lookup"><span data-stu-id="738a3-188">b.</span></span> <span data-ttu-id="738a3-189">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="738a3-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="738a3-190">c.</span><span class="sxs-lookup"><span data-stu-id="738a3-190">c.</span></span> <span data-ttu-id="738a3-191">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="738a3-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="738a3-192">d.</span><span class="sxs-lookup"><span data-stu-id="738a3-192">d.</span></span> <span data-ttu-id="738a3-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="738a3-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="738a3-194">Creazione di un utente di test di Skillport</span><span class="sxs-lookup"><span data-stu-id="738a3-194">Creating a Skillport test user</span></span>

<span data-ttu-id="738a3-195">Per creare l'utente di test di Skillport, è necessario contattare il [team di supporto di Skillport](https://www.skillsoft.com/contact.asp) perché sono previsti diversi scenari aziendali in base ai requisiti dell'utente finale.</span><span class="sxs-lookup"><span data-stu-id="738a3-195">In order to create Skillport test user, you need to contact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according to the requirement of end user.</span></span> <span data-ttu-id="738a3-196">La configurazione verrà eseguita dopo averne discusso con gli utenti.</span><span class="sxs-lookup"><span data-stu-id="738a3-196">They will configure it after discussion with the users.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="738a3-197">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="738a3-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="738a3-198">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Skillport.</span><span class="sxs-lookup"><span data-stu-id="738a3-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skillport.</span></span>

![Assegna utente][200] 

<span data-ttu-id="738a3-200">**Per assegnare Britta Simon a Skillport, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="738a3-200">**To assign Britta Simon to Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="738a3-201">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="738a3-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="738a3-203">Nell'elenco delle applicazioni selezionare **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="738a3-203">In the applications list, select **Skillport**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="738a3-205">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="738a3-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="738a3-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="738a3-207">Click **Add** button.</span></span> <span data-ttu-id="738a3-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="738a3-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="738a3-210">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="738a3-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="738a3-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="738a3-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="738a3-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="738a3-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="738a3-213">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="738a3-213">Testing single sign-on</span></span>

<span data-ttu-id="738a3-214">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="738a3-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="738a3-215">Quando si fa clic sul riquadro Skillport nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Skillport.</span><span class="sxs-lookup"><span data-stu-id="738a3-215">When you click the Skillport tile in the Access Panel, you should get automatically signed-on to your Skillport application.</span></span>
<span data-ttu-id="738a3-216">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="738a3-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="738a3-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="738a3-217">Additional resources</span></span>

* [<span data-ttu-id="738a3-218">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="738a3-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="738a3-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="738a3-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

