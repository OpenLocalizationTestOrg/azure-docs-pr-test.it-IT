---
title: 'Esercitazione: Integrazione di Azure Active Directory con Atomic Learning | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Atomic Learning.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 495f54a6-e6c4-41b0-aafa-a6283d33efc8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 6cce8fc839e60eb6498ab48bf68e9906c98889a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atomic-learning"></a><span data-ttu-id="eb842-103">Esercitazione: Integrazione di Azure Active Directory con Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="eb842-103">Tutorial: Azure Active Directory integration with Atomic Learning</span></span>

<span data-ttu-id="eb842-104">Questa esercitazione descrive come integrare Atomic Learning con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb842-104">In this tutorial, you learn how to integrate Atomic Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb842-105">L'integrazione di Atomic Learning con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="eb842-105">Integrating Atomic Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="eb842-106">È possibile controllare in Azure AD chi può accedere ad Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="eb842-106">You can control in Azure AD who has access to Atomic Learning</span></span>
- <span data-ttu-id="eb842-107">È possibile abilitare gli utenti per l'accesso automatico ad Atomic Learning (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb842-107">You can enable your users to automatically get signed-on to Atomic Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eb842-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb842-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="eb842-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb842-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb842-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eb842-110">Prerequisites</span></span>

<span data-ttu-id="eb842-111">Per configurare l'integrazione di Azure AD con Atomic Learning sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="eb842-111">To configure Azure AD integration with Atomic Learning, you need the following items:</span></span>

- <span data-ttu-id="eb842-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb842-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb842-113">Sottoscrizione di Atomic Learning abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="eb842-113">An Atomic Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eb842-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="eb842-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eb842-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="eb842-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb842-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="eb842-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eb842-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb842-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb842-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="eb842-118">Scenario description</span></span>
<span data-ttu-id="eb842-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="eb842-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eb842-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="eb842-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb842-121">Aggiunta di Atomic Learning dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="eb842-121">Adding Atomic Learning from the gallery</span></span>
2. <span data-ttu-id="eb842-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb842-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atomic-learning-from-the-gallery"></a><span data-ttu-id="eb842-123">Aggiunta di Atomic Learning dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="eb842-123">Adding Atomic Learning from the gallery</span></span>
<span data-ttu-id="eb842-124">Per configurare l'integrazione di Atomic Learning in Azure AD è necessario aggiungere Atomic Learning dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="eb842-124">To configure the integration of Atomic Learning into Azure AD, you need to add Atomic Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="eb842-125">**Per aggiungere Atomic Learning dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="eb842-125">**To add Atomic Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="eb842-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="eb842-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eb842-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="eb842-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="eb842-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="eb842-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="eb842-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="eb842-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="eb842-133">Nella casella di ricerca digitare **Atomic Learning**.</span><span class="sxs-lookup"><span data-stu-id="eb842-133">In the search box, type **Atomic Learning**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_search.png)

5. <span data-ttu-id="eb842-135">Nel pannello dei risultati selezionare **Atomic Learning** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eb842-135">In the results panel, select **Atomic Learning**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eb842-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb842-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eb842-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Atomic Learning in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="eb842-138">In this section, you configure and test Azure AD single sign-on with Atomic Learning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eb842-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di Atomic Learning che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb842-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Atomic Learning is to a user in Azure AD.</span></span> <span data-ttu-id="eb842-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="eb842-140">In other words, a link relationship between an Azure AD user and the related user in Atomic Learning needs to be established.</span></span>

<span data-ttu-id="eb842-141">Per stabilire la relazione di collegamento, in Atomic Learning assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="eb842-141">In Atomic Learning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="eb842-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Atomic Learning è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="eb842-142">To configure and test Azure AD single sign-on with Atomic Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="eb842-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="eb842-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="eb842-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb842-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb842-145">**[Creazione di un utente di test di Atomic Learning](#creating-an-atomic-learning-test-user)**: per avere una controparte di Britta Simon in Atomic Learning collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb842-145">**[Creating an Atomic Learning test user](#creating-an-atomic-learning-test-user)** - to have a counterpart of Britta Simon in Atomic Learning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="eb842-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb842-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb842-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="eb842-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eb842-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb842-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eb842-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="eb842-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atomic Learning application.</span></span>

<span data-ttu-id="eb842-150">**Per configurare l'accesso Single Sign-On di Azure AD con Atomic Learning seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="eb842-150">**To configure Azure AD single sign-on with Atomic Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="eb842-151">Nella pagina di integrazione dell'applicazione **Atomic Learning** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="eb842-151">In the Azure portal, on the **Atomic Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="eb842-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="eb842-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_samlbase.png)

3. <span data-ttu-id="eb842-155">Nella sezione **URL e dominio Atomic Learning** eseguire i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="eb842-155">On the **Atomic Learning Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_url.png)

     <span data-ttu-id="eb842-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="eb842-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="eb842-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="eb842-158">This value is not real.</span></span> <span data-ttu-id="eb842-159">è necessario aggiornare questo valore con l'URL di accesso Sign-On effettivo.</span><span class="sxs-lookup"><span data-stu-id="eb842-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="eb842-160">Per ottenere tale valore, contattare il [team di supporto clienti di Atomic Learning](mailto:cs@atomiclearning.com).</span><span class="sxs-lookup"><span data-stu-id="eb842-160">Contact [Atomic Learning Client support team](mailto:cs@atomiclearning.com) to get this value.</span></span> 
 
4. <span data-ttu-id="eb842-161">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="eb842-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_certificate.png) 

5. <span data-ttu-id="eb842-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="eb842-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eb842-165">Per configurare l'accesso Single Sign-On sul lato **Atomic Learning** è necessario inviare il file **XML metadati** scaricato al [team di supporto di Atomic Learning](mailto:cs@atomiclearning.com).</span><span class="sxs-lookup"><span data-stu-id="eb842-165">To configure single sign-on on **Atomic Learning** side, you need to send the downloaded **Metadata XML** to [Atomic Learning support team](mailto:cs@atomiclearning.com).</span></span> <span data-ttu-id="eb842-166">L’impostazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="eb842-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="eb842-167">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="eb842-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="eb842-168">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="eb842-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="eb842-169">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb842-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eb842-170">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb842-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="eb842-171">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb842-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="eb842-173">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="eb842-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="eb842-174">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="eb842-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eb842-176">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="eb842-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eb842-178">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="eb842-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eb842-180">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="eb842-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eb842-182">a.</span><span class="sxs-lookup"><span data-stu-id="eb842-182">a.</span></span> <span data-ttu-id="eb842-183">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb842-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb842-184">b.</span><span class="sxs-lookup"><span data-stu-id="eb842-184">b.</span></span> <span data-ttu-id="eb842-185">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eb842-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eb842-186">c.</span><span class="sxs-lookup"><span data-stu-id="eb842-186">c.</span></span> <span data-ttu-id="eb842-187">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="eb842-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="eb842-188">d.</span><span class="sxs-lookup"><span data-stu-id="eb842-188">d.</span></span> <span data-ttu-id="eb842-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="eb842-189">Click **Create**.</span></span>
 
### <a name="creating-an-atomic-learning-test-user"></a><span data-ttu-id="eb842-190">Creazione di un utente test di Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="eb842-190">Creating an Atomic Learning test user</span></span>

<span data-ttu-id="eb842-191">In questa sezione viene creato un utente di nome Britta Simon in Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="eb842-191">In this section, you create a user called Britta Simon in Atomic Learning.</span></span> <span data-ttu-id="eb842-192">Atomic Learning supporta il provisioning just-in-time, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="eb842-192">Atomic Learning supports just-in-time provisioning, which is by default enabled.</span></span> 

<span data-ttu-id="eb842-193">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="eb842-193">There is no action item for you in this section.</span></span> <span data-ttu-id="eb842-194">Un utente, se non esiste già, viene creato durante un tentativo di accesso ad Atomic Learning con l'indirizzo e-mail dell'utente stesso.</span><span class="sxs-lookup"><span data-stu-id="eb842-194">A new user is created during an attempt to access Atomic Learning if it doesn't exist yet using the email address for the user.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="eb842-195">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb842-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="eb842-196">In questa sezione, Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="eb842-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Atomic Learning.</span></span>

![Assegna utente][200] 

<span data-ttu-id="eb842-198">**Per assegnare Britta Simon ad Atomic Learning seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="eb842-198">**To assign Britta Simon to Atomic Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="eb842-199">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="eb842-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="eb842-201">Nell'elenco delle applicazioni selezionare **Atomic Learning**.</span><span class="sxs-lookup"><span data-stu-id="eb842-201">In the applications list, select **Atomic Learning**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_app.png) 

3. <span data-ttu-id="eb842-203">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="eb842-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="eb842-205">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="eb842-205">Click **Add** button.</span></span> <span data-ttu-id="eb842-206">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="eb842-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="eb842-208">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="eb842-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="eb842-209">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="eb842-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb842-210">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="eb842-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eb842-211">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="eb842-211">Testing single sign-on</span></span>

<span data-ttu-id="eb842-212">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="eb842-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="eb842-213">Quando si fa clic sul riquadro Atomic Learning nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="eb842-213">When you click the Atomic Learning tile in the Access Panel, you should get automatically signed-on to your Atomic Learning application.</span></span>
<span data-ttu-id="eb842-214">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eb842-214">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="eb842-215">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="eb842-215">Additional resources</span></span>

* [<span data-ttu-id="eb842-216">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb842-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb842-217">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb842-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_203.png

