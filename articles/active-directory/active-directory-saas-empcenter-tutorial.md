---
title: 'Esercitazione: Integrazione di Azure Active Directory con EmpCenter | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory ed EmpCenter.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a00ecf6e-917a-4284-b998-41506931585e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: aa27175165f4b15477bef4e70ad1c25016db31a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-empcenter"></a><span data-ttu-id="8b113-103">Esercitazione: Integrazione di Azure Active Directory con EmpCenter</span><span class="sxs-lookup"><span data-stu-id="8b113-103">Tutorial: Azure Active Directory integration with EmpCenter</span></span>

<span data-ttu-id="8b113-104">Questa esercitazione descrive come integrare EmpCenter con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b113-104">In this tutorial, you learn how to integrate EmpCenter with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b113-105">L'integrazione di EmpCenter con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b113-105">Integrating EmpCenter with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8b113-106">È possibile controllare in Azure AD chi può accedere a EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="8b113-106">You can control in Azure AD who has access to EmpCenter</span></span>
- <span data-ttu-id="8b113-107">È possibile abilitare gli utenti per l'accesso automatico a EmpCenter (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b113-107">You can enable your users to automatically get signed-on to EmpCenter (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8b113-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b113-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8b113-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8b113-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b113-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8b113-110">Prerequisites</span></span>

<span data-ttu-id="8b113-111">Per configurare l'integrazione di Azure AD con EmpCenter, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b113-111">To configure Azure AD integration with EmpCenter, you need the following items:</span></span>

- <span data-ttu-id="8b113-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b113-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8b113-113">Sottoscrizione di EmpCenter abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8b113-113">An EmpCenter single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b113-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8b113-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8b113-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b113-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8b113-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8b113-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8b113-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b113-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b113-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8b113-118">Scenario description</span></span>
<span data-ttu-id="8b113-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8b113-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8b113-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b113-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b113-121">Aggiunta di EmpCenter dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8b113-121">Adding EmpCenter from the gallery</span></span>
2. <span data-ttu-id="8b113-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b113-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-empcenter-from-the-gallery"></a><span data-ttu-id="8b113-123">Aggiunta di EmpCenter dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8b113-123">Adding EmpCenter from the gallery</span></span>
<span data-ttu-id="8b113-124">Per configurare l'integrazione di EmpCenter in Azure AD, è necessario aggiungere EmpCenter dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8b113-124">To configure the integration of EmpCenter into Azure AD, you need to add EmpCenter from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8b113-125">**Per aggiungere EmpCenter dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8b113-125">**To add EmpCenter from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8b113-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8b113-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8b113-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8b113-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8b113-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8b113-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8b113-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="8b113-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8b113-133">Nella casella di ricerca digitare **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="8b113-133">In the search box, type **EmpCenter**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_search.png)

5. <span data-ttu-id="8b113-135">Nel pannello dei risultati selezionare **EmpCenter** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8b113-135">In the results panel, select **EmpCenter**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8b113-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b113-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8b113-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con EmpCenter in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8b113-138">In this section, you configure and test Azure AD single sign-on with EmpCenter based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8b113-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente controparte di EmpCenter che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b113-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EmpCenter is to a user in Azure AD.</span></span> <span data-ttu-id="8b113-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="8b113-140">In other words, a link relationship between an Azure AD user and the related user in EmpCenter needs to be established.</span></span>

<span data-ttu-id="8b113-141">Per stabilire la relazione di collegamento, in EmpCenter assegnare il valore di **nome utente** in Azure AD come valore dell'attributo **Username**.</span><span class="sxs-lookup"><span data-stu-id="8b113-141">In EmpCenter, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8b113-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con EmpCenter, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b113-142">To configure and test Azure AD single sign-on with EmpCenter, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8b113-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8b113-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8b113-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8b113-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b113-145">**[Creazione di un utente di test di EmpCenter](#creating-an-empcenter-test-user)**: per avere una controparte di Britta Simon in EmpCenter collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b113-145">**[Creating an EmpCenter test user](#creating-an-empcenter-test-user)** - to have a counterpart of Britta Simon in EmpCenter that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8b113-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b113-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b113-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="8b113-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8b113-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b113-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8b113-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="8b113-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EmpCenter application.</span></span>

<span data-ttu-id="8b113-150">**Per configurare Single Sign-On di Azure AD con EmpCenter, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8b113-150">**To configure Azure AD single sign-on with EmpCenter, perform the following steps:**</span></span>

1. <span data-ttu-id="8b113-151">Nella pagina di integrazione dell'applicazione **EmpCenter** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="8b113-151">In the Azure portal, on the **EmpCenter** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8b113-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8b113-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_samlbase.png)

3. <span data-ttu-id="8b113-155">Nella sezione **URL e dominio EmpCenter** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8b113-155">On the **EmpCenter Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_url.png)

    <span data-ttu-id="8b113-157">Nella casella di testo **URL di accesso** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="8b113-157">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.EmpCenter.com/<instancename>` |
    | `https://<subdomain>.workforcehosting.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="8b113-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="8b113-158">The value is not real.</span></span> <span data-ttu-id="8b113-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="8b113-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="8b113-160">Per ottenere il valore, contattare il [team di supporto clienti di EmpCenter](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="8b113-160">Contact [EmpCenter Client support team](http://www.workforcesoftware.com/services/customer-support/) to get the value.</span></span> 
 
4. <span data-ttu-id="8b113-161">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="8b113-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_certificate.png) 

5. <span data-ttu-id="8b113-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8b113-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8b113-165">Per configurare l'accesso Single Sign-On sul lato **EmpCenter**, è necessario inviare il file **XML di metadati** scaricato al [team di supporto di EmpCenter](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="8b113-165">To configure single sign-on on **EmpCenter** side, you need to send the downloaded **Metadata XML** to [EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span> <span data-ttu-id="8b113-166">Questa impostazione viene configurata in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="8b113-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8b113-167">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="8b113-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8b113-168">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="8b113-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8b113-169">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b113-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8b113-170">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b113-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="8b113-171">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b113-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8b113-173">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8b113-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8b113-174">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8b113-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8b113-176">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="8b113-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8b113-178">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="8b113-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8b113-180">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8b113-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8b113-182">a.</span><span class="sxs-lookup"><span data-stu-id="8b113-182">a.</span></span> <span data-ttu-id="8b113-183">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8b113-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b113-184">b.</span><span class="sxs-lookup"><span data-stu-id="8b113-184">b.</span></span> <span data-ttu-id="8b113-185">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8b113-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8b113-186">c.</span><span class="sxs-lookup"><span data-stu-id="8b113-186">c.</span></span> <span data-ttu-id="8b113-187">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="8b113-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8b113-188">d.</span><span class="sxs-lookup"><span data-stu-id="8b113-188">d.</span></span> <span data-ttu-id="8b113-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8b113-189">Click **Create**.</span></span>
 
### <a name="creating-an-empcenter-test-user"></a><span data-ttu-id="8b113-190">Creazione di un utente di test di EmpCenter</span><span class="sxs-lookup"><span data-stu-id="8b113-190">Creating an EmpCenter test user</span></span>

<span data-ttu-id="8b113-191">Per consentire agli utenti di Azure AD di accedere a EmpCenter, è necessario eseguirne il provisioning in EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="8b113-191">In order to enable Azure AD users to log in to EmpCenter, they must be provisioned into EmpCenter.</span></span> <span data-ttu-id="8b113-192">Nel caso di EmpCenter, gli account utente devono essere creati dal [team di supporto di EmpCenter](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="8b113-192">In the case of EmpCenter, the user accounts need to be created by your [EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span>

> [!NOTE]
> <span data-ttu-id="8b113-193">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da EmpCenter per eseguire il provisioning degli account utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8b113-193">You can use any other EmpCenter user account creation tools or APIs provided by EmpCenter to provision Azure Active Directory user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8b113-194">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b113-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8b113-195">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="8b113-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EmpCenter.</span></span>

![Assegna utente][200] 

<span data-ttu-id="8b113-197">**Per assegnare Britta Simon a EmpCenter, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8b113-197">**To assign Britta Simon to EmpCenter, perform the following steps:**</span></span>

1. <span data-ttu-id="8b113-198">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8b113-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8b113-200">Nell'elenco delle applicazioni selezionare **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="8b113-200">In the applications list, select **EmpCenter**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_app.png) 

3. <span data-ttu-id="8b113-202">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8b113-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8b113-204">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8b113-204">Click **Add** button.</span></span> <span data-ttu-id="8b113-205">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8b113-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8b113-207">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="8b113-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8b113-208">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8b113-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8b113-209">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8b113-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8b113-210">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8b113-210">Testing single sign-on</span></span>


<span data-ttu-id="8b113-211">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8b113-211">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8b113-212">Quando si fa clic sul riquadro EmpCenter nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="8b113-212">When you click the EmpCenter tile in the Access Panel, you should get automatically signed-on to your EmpCenter application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b113-213">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8b113-213">Additional resources</span></span>

* [<span data-ttu-id="8b113-214">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b113-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b113-215">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b113-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_203.png

