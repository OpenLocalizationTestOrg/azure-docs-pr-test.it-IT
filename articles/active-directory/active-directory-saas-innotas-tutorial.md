---
title: 'Esercitazione: Integrazione di Azure Active Directory con Innotas | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Innotas.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: eb9e9c2c-4b09-4177-bbab-423fd657448e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 674d01b2c0818dc10fdab5844a23c5ebf29bb2d2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-innotas"></a><span data-ttu-id="3421c-103">Esercitazione: Integrazione di Azure Active Directory con Innotas</span><span class="sxs-lookup"><span data-stu-id="3421c-103">Tutorial: Azure Active Directory integration with Innotas</span></span>

<span data-ttu-id="3421c-104">Questa esercitazione descrive come integrare Innotas con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3421c-104">In this tutorial, you learn how to integrate Innotas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3421c-105">L'integrazione di Innotas con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3421c-105">Integrating Innotas with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3421c-106">È possibile controllare in Azure AD chi può accedere a Innotas</span><span class="sxs-lookup"><span data-stu-id="3421c-106">You can control in Azure AD who has access to Innotas</span></span>
- <span data-ttu-id="3421c-107">È possibile abilitare gli utenti per l'accesso automatico a Innotas (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="3421c-107">You can enable your users to automatically get signed-on to Innotas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3421c-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3421c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3421c-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3421c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3421c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3421c-110">Prerequisites</span></span>

<span data-ttu-id="3421c-111">Per configurare l'integrazione di Azure AD con Innotas sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3421c-111">To configure Azure AD integration with Innotas, you need the following items:</span></span>

- <span data-ttu-id="3421c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3421c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3421c-113">Sottoscrizione Innotas abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3421c-113">An Innotas single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3421c-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3421c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3421c-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3421c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3421c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="3421c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3421c-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3421c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3421c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="3421c-118">Scenario description</span></span>

<span data-ttu-id="3421c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="3421c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3421c-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3421c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3421c-121">Aggiunta di Innotas dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="3421c-121">Adding Innotas from the gallery</span></span>
2. <span data-ttu-id="3421c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3421c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-innotas-from-the-gallery"></a><span data-ttu-id="3421c-123">Aggiunta di Innotas dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="3421c-123">Adding Innotas from the gallery</span></span>
<span data-ttu-id="3421c-124">Per configurare l'integrazione di Innotas in Azure AD, è necessario aggiungere Innotas dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="3421c-124">To configure the integration of Innotas into Azure AD, you need to add Innotas from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3421c-125">**Per aggiungere Innotas dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3421c-125">**To add Innotas from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3421c-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="3421c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3421c-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="3421c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3421c-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3421c-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="3421c-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="3421c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="3421c-133">Nella casella di ricerca digitare **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="3421c-133">In the search box, type **Innotas**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_search.png)

5. <span data-ttu-id="3421c-135">Nel pannello dei risultati selezionare **Innotas** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3421c-135">In the results panel, select **Innotas**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3421c-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3421c-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="3421c-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Innotas usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3421c-138">In this section, you configure and test Azure AD single sign-on with Innotas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3421c-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Innotas corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3421c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Innotas is to a user in Azure AD.</span></span> <span data-ttu-id="3421c-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Innotas.</span><span class="sxs-lookup"><span data-stu-id="3421c-140">In other words, a link relationship between an Azure AD user and the related user in Innotas needs to be established.</span></span>

<span data-ttu-id="3421c-141">Per stabilire la relazione di collegamento, in Innotas assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="3421c-141">In Innotas, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3421c-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Innotas, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="3421c-142">To configure and test Azure AD single sign-on with Innotas, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3421c-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3421c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3421c-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3421c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3421c-145">**[Creazione di un utente di test di Innotas](#creating-an-innotas-test-user)**: per avere una controparte di Britta Simon in Innotas collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3421c-145">**[Creating an Innotas test user](#creating-an-innotas-test-user)** - to have a counterpart of Britta Simon in Innotas that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3421c-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3421c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3421c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="3421c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3421c-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3421c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3421c-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Innotas.</span><span class="sxs-lookup"><span data-stu-id="3421c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Innotas application.</span></span>

<span data-ttu-id="3421c-150">**Per configurare l'accesso Single Sign-On di Azure AD con Innotas, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3421c-150">**To configure Azure AD single sign-on with Innotas, perform the following steps:**</span></span>

1. <span data-ttu-id="3421c-151">Nella pagina di integrazione dell'applicazione **Innotas** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="3421c-151">In the Azure portal, on the **Innotas** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="3421c-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="3421c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_samlbase.png)

3. <span data-ttu-id="3421c-155">Nella sezione **URL e dominio Innotas** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3421c-155">On the **Innotas Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_url.png)

    <span data-ttu-id="3421c-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenant-name>.Innotas.com`</span><span class="sxs-lookup"><span data-stu-id="3421c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Innotas.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3421c-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="3421c-158">This value is not real.</span></span> <span data-ttu-id="3421c-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="3421c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="3421c-160">Per ottenere questo valore, contattare il [team di supporto clienti di Innotas](https://www.innotas.com/contact).</span><span class="sxs-lookup"><span data-stu-id="3421c-160">Contact [Innotas Client support team](https://www.innotas.com/contact) to get this value.</span></span> 
 
4. <span data-ttu-id="3421c-161">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="3421c-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_certificate.png) 

5. <span data-ttu-id="3421c-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="3421c-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-innotas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3421c-165">Per configurare l'accesso Single Sign-On sul lato **Innotas**, è necessario inviare il file **XML metadati** scaricato al [team di supporto di Innotas](https://www.innotas.com/contact).</span><span class="sxs-lookup"><span data-stu-id="3421c-165">To configure single sign-on on **Innotas** side, you need to send the downloaded **Metadata XML** to [Innotas support team](https://www.innotas.com/contact).</span></span> <span data-ttu-id="3421c-166">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="3421c-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3421c-167">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="3421c-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3421c-168">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="3421c-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3421c-169">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3421c-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3421c-170">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3421c-170">Creating an Azure AD test user</span></span>

<span data-ttu-id="3421c-171">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3421c-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="3421c-173">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3421c-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3421c-174">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="3421c-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3421c-176">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="3421c-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3421c-178">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="3421c-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3421c-180">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3421c-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3421c-182">a.</span><span class="sxs-lookup"><span data-stu-id="3421c-182">a.</span></span> <span data-ttu-id="3421c-183">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3421c-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3421c-184">b.</span><span class="sxs-lookup"><span data-stu-id="3421c-184">b.</span></span> <span data-ttu-id="3421c-185">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3421c-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3421c-186">c.</span><span class="sxs-lookup"><span data-stu-id="3421c-186">c.</span></span> <span data-ttu-id="3421c-187">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="3421c-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3421c-188">d.</span><span class="sxs-lookup"><span data-stu-id="3421c-188">d.</span></span> <span data-ttu-id="3421c-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3421c-189">Click **Create**.</span></span>
 
### <a name="creating-an-innotas-test-user"></a><span data-ttu-id="3421c-190">Creazione di un utente di test di Innotas</span><span class="sxs-lookup"><span data-stu-id="3421c-190">Creating an Innotas test user</span></span>

<span data-ttu-id="3421c-191">Non è necessaria alcuna attività di configurazione per il provisioning degli utenti in Innotas.</span><span class="sxs-lookup"><span data-stu-id="3421c-191">There is no action item for you to configure user provisioning to Innotas.</span></span>  
<span data-ttu-id="3421c-192">Quando un utente assegnato prova ad accedere a Innotas usando il pannello di accesso, Innotas verifica se l'utente esiste.</span><span class="sxs-lookup"><span data-stu-id="3421c-192">When an assigned user tries to log in to Innotas using the access panel, Innotas checks whether the user exists.</span></span>  

>[!NOTE]
><span data-ttu-id="3421c-193">Se l'account utente non è presente, Innotas lo crea automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3421c-193">If there is no user account available yet, it is automatically created by Innotas.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3421c-194">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3421c-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3421c-195">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Innotas.</span><span class="sxs-lookup"><span data-stu-id="3421c-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Innotas.</span></span>

![Assegna utente][200] 

<span data-ttu-id="3421c-197">**Per assegnare Britta Simon a Innotas, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3421c-197">**To assign Britta Simon to Innotas, perform the following steps:**</span></span>

1. <span data-ttu-id="3421c-198">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3421c-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="3421c-200">Nell'elenco di applicazioni selezionare **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="3421c-200">In the applications list, select **Innotas**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_app.png) 

3. <span data-ttu-id="3421c-202">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="3421c-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="3421c-204">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3421c-204">Click **Add** button.</span></span> <span data-ttu-id="3421c-205">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3421c-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="3421c-207">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="3421c-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3421c-208">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3421c-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3421c-209">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3421c-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3421c-210">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3421c-210">Testing single sign-on</span></span>

<span data-ttu-id="3421c-211">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3421c-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3421c-212">Quando si fa clic sul riquadro Innotas nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Innotas.</span><span class="sxs-lookup"><span data-stu-id="3421c-212">When you click the Innotas tile in the Access Panel, you should get automatically signed-on to your Innotas application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3421c-213">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="3421c-213">Additional resources</span></span>

* [<span data-ttu-id="3421c-214">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3421c-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3421c-215">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3421c-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_203.png

