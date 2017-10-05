---
title: 'Esercitazione: Integrazione di Azure Active Directory con MobileXpense | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e MobileXpense.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e649fc4e-3e15-4948-b977-00bfe9f7db13
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: jeedes
ms.openlocfilehash: 030a1fc9f36d6fcfa607552d85ce232e36eaa64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mobilexpense"></a><span data-ttu-id="88e30-103">Esercitazione: Integrazione di Azure Active Directory con MobileXpense</span><span class="sxs-lookup"><span data-stu-id="88e30-103">Tutorial: Azure Active Directory integration with MobileXpense</span></span>

<span data-ttu-id="88e30-104">Questa esercitazione descrive come integrare MobileXpense con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88e30-104">In this tutorial, you learn how to integrate MobileXpense with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88e30-105">L'integrazione di MobileXpense con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="88e30-105">Integrating MobileXpense with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="88e30-106">È possibile controllare in Azure AD chi può accedere a MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="88e30-106">You can control in Azure AD who has access to MobileXpense</span></span>
- <span data-ttu-id="88e30-107">È possibile abilitare gli utenti per l'accesso automatico a MobileXpense (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88e30-107">You can enable your users to automatically get signed-on to MobileXpense (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88e30-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="88e30-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="88e30-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88e30-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88e30-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="88e30-110">Prerequisites</span></span>

<span data-ttu-id="88e30-111">Per configurare l'integrazione di Azure AD con MobileXpense, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="88e30-111">To configure Azure AD integration with MobileXpense, you need the following items:</span></span>

- <span data-ttu-id="88e30-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88e30-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88e30-113">Sottoscrizione di MobileXpense abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="88e30-113">A MobileXpense single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88e30-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="88e30-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88e30-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="88e30-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88e30-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="88e30-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="88e30-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88e30-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88e30-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="88e30-118">Scenario description</span></span>
<span data-ttu-id="88e30-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="88e30-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88e30-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="88e30-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88e30-121">Aggiunta di MobileXpense dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="88e30-121">Adding MobileXpense from the gallery</span></span>
2. <span data-ttu-id="88e30-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e30-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mobilexpense-from-the-gallery"></a><span data-ttu-id="88e30-123">Aggiunta di MobileXpense dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="88e30-123">Adding MobileXpense from the gallery</span></span>
<span data-ttu-id="88e30-124">Per configurare l'integrazione di MobileXpense in Azure AD, è necessario aggiungere MobileXpense dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="88e30-124">To configure the integration of MobileXpense into Azure AD, you need to add MobileXpense from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="88e30-125">**Per aggiungere MobileXpense dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="88e30-125">**To add MobileXpense from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="88e30-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="88e30-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="88e30-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="88e30-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="88e30-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="88e30-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="88e30-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="88e30-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="88e30-133">Nella casella di ricerca digitare **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="88e30-133">In the search box, type **MobileXpense**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_search.png)

5. <span data-ttu-id="88e30-135">Nel pannello dei risultati selezionare **MobileXpense** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="88e30-135">In the results panel, select **MobileXpense**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88e30-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e30-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88e30-138">In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con MobileXpense in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="88e30-138">In this section, you configure and test Azure AD single sign-on with MobileXpense based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="88e30-139">Per il corretto funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di MobileXpense che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88e30-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MobileXpense is to a user in Azure AD.</span></span> <span data-ttu-id="88e30-140">Deve essere stabilita, in altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato in MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="88e30-140">In other words, a link relationship between an Azure AD user and the related user in MobileXpense needs to be established.</span></span>

<span data-ttu-id="88e30-141">Per stabilire la relazione di collegamento, in MobileXpense assegnare il valore di **nome utente** in Azure AD come valore dell'attributo **Username**.</span><span class="sxs-lookup"><span data-stu-id="88e30-141">In MobileXpense, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="88e30-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con MobileXpense, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="88e30-142">To configure and test Azure AD single sign-on with MobileXpense, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="88e30-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="88e30-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="88e30-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88e30-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88e30-145">**[Creazione di un utente test di MobileXpense](#creating-a-mobilexpense-test-user)**: per avere una controparte di Britta Simon in MobileXpense collegata alla rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="88e30-145">**[Creating a MobileXpense test user](#creating-a-mobilexpense-test-user)** - to have a counterpart of Britta Simon in MobileXpense that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="88e30-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88e30-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88e30-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="88e30-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88e30-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e30-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88e30-149">In questa sezione si abilita l'accesso Single Sign-On di Azure AD nel portale di Azure e si configura l'accesso Single Sign-On nell'applicazione MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="88e30-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MobileXpense application.</span></span>

<span data-ttu-id="88e30-150">**Per configurare l'accesso Single Sign-On di Azure AD con MobileXpense, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="88e30-150">**To configure Azure AD single sign-on with MobileXpense, perform the following steps:**</span></span>

1. <span data-ttu-id="88e30-151">Nella pagina di integrazione dell'applicazione **MobileXpense** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="88e30-151">In the Azure portal, on the **MobileXpense** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="88e30-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="88e30-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_samlbase.png)

3. <span data-ttu-id="88e30-155">Nella sezione **URL e dominio MobileXpense**, se si vuole configurare l'applicazione in modalità avviata da **IDP**:</span><span class="sxs-lookup"><span data-stu-id="88e30-155">On the **MobileXpense Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url11.png)

    <span data-ttu-id="88e30-157">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="88e30-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span></span>

4. <span data-ttu-id="88e30-158">Selezionare **Mostra impostazioni URL avanzate**, se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="88e30-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url22.png)

<span data-ttu-id="88e30-160">Nella casella di testo **URL di accesso** digitare l'URL adottando il modello seguente: `https://<sub domain>.mobilexpense.com/<customername>`</span><span class="sxs-lookup"><span data-stu-id="88e30-160">In the **Sign-on URL** textbox, type a URL using the following pattern:: `https://<sub domain>.mobilexpense.com/<customername>`</span></span>

> [!NOTE] 
> <span data-ttu-id="88e30-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="88e30-161">These values are not real.</span></span> <span data-ttu-id="88e30-162">è necessario aggiornarli con l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="88e30-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="88e30-163">Per ottenere questi valori, contattare il [team di supporto clienti di MobileXpense](http://www.mobilexpense.net/contact).</span><span class="sxs-lookup"><span data-stu-id="88e30-163">Contact [MobileXpense Client support team](http://www.mobilexpense.net/contact) to get these values.</span></span> 

5. <span data-ttu-id="88e30-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="88e30-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_certificate.png) 

6. <span data-ttu-id="88e30-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="88e30-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="88e30-168">Per configurare l’accesso Single Sign-On sul lato **MobileXpense**, è necessario inviare il file **XML metadati** scaricato al [team di supporto di MobileXpense](http://www.mobilexpense.net/contact).</span><span class="sxs-lookup"><span data-stu-id="88e30-168">To configure single sign-on on **MobileXpense** side, you need to send the downloaded **Metadata XML** to [MobileXpense support team](http://www.mobilexpense.net/contact).</span></span>

> [!TIP]
> <span data-ttu-id="88e30-169">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="88e30-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="88e30-170">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="88e30-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="88e30-171">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88e30-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88e30-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e30-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="88e30-173">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="88e30-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="88e30-175">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="88e30-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="88e30-176">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="88e30-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88e30-178">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="88e30-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88e30-180">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="88e30-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88e30-182">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="88e30-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88e30-184">a.</span><span class="sxs-lookup"><span data-stu-id="88e30-184">a.</span></span> <span data-ttu-id="88e30-185">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88e30-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88e30-186">b.</span><span class="sxs-lookup"><span data-stu-id="88e30-186">b.</span></span> <span data-ttu-id="88e30-187">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="88e30-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="88e30-188">c.</span><span class="sxs-lookup"><span data-stu-id="88e30-188">c.</span></span> <span data-ttu-id="88e30-189">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="88e30-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="88e30-190">d.</span><span class="sxs-lookup"><span data-stu-id="88e30-190">d.</span></span> <span data-ttu-id="88e30-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="88e30-191">Click **Create**.</span></span>
 
### <a name="creating-a-mobilexpense-test-user"></a><span data-ttu-id="88e30-192">Creazione di un utente test di MobileXpense</span><span class="sxs-lookup"><span data-stu-id="88e30-192">Creating a MobileXpense test user</span></span>

<span data-ttu-id="88e30-193">In questa sezione si crea un utente di nome Britta Simon in MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="88e30-193">In this section, you create a user called Britta Simon in MobileXpense.</span></span> <span data-ttu-id="88e30-194">Collaborare con il [team di supporto di MobileXpense](http://www.mobilexpense.net/contact) per aggiungere gli utenti alla piattaforma MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="88e30-194">work with [MobileXpense support team](http://www.mobilexpense.net/contact) to add the users in the MobileXpense platform.</span></span> <span data-ttu-id="88e30-195">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="88e30-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="88e30-196">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e30-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="88e30-197">In questa sezione si abilita Britta Simon per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="88e30-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MobileXpense.</span></span>

![Assegna utente][200] 

<span data-ttu-id="88e30-199">**Per assegnare Britta Simon a MobileXpense, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="88e30-199">**To assign Britta Simon to MobileXpense, perform the following steps:**</span></span>

1. <span data-ttu-id="88e30-200">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="88e30-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="88e30-202">Nell'elenco di applicazioni selezionare **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="88e30-202">In the applications list, select **MobileXpense**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_app.png) 

3. <span data-ttu-id="88e30-204">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="88e30-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="88e30-206">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="88e30-206">Click **Add** button.</span></span> <span data-ttu-id="88e30-207">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="88e30-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="88e30-209">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="88e30-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="88e30-210">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="88e30-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88e30-211">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="88e30-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="88e30-212">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="88e30-212">Testing single sign-on</span></span>

<span data-ttu-id="88e30-213">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="88e30-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="88e30-214">Quando si fa clic sul riquadro MobileXpense nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="88e30-214">When you click the MobileXpense tile in the Access Panel, you should get automatically signed-on to your MobileXpense application.</span></span>
<span data-ttu-id="88e30-215">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="88e30-215">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="88e30-216">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="88e30-216">Additional resources</span></span>

* [<span data-ttu-id="88e30-217">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88e30-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88e30-218">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88e30-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_203.png

