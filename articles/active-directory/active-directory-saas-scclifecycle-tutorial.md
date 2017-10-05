---
title: 'Esercitazione: Integrazione di Azure Active Directory con SCC LifeCycle | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SCC LifeCycle.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0f8f9d03e8c35109b74088350ef1d68f6b823e8b
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="ecc3a-103">Esercitazione: Integrazione di Azure Active Directory con SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="ecc3a-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>

<span data-ttu-id="ecc3a-104">Questa esercitazione descrive come integrare SCC LifeCycle con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ecc3a-104">In this tutorial, you learn how to integrate SCC LifeCycle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ecc3a-105">L'integrazione di SCC LifeCycle con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ecc3a-105">Integrating SCC LifeCycle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ecc3a-106">È possibile controllare in Azure AD chi può accedere a SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="ecc3a-106">You can control in Azure AD who has access to SCC LifeCycle</span></span>
- <span data-ttu-id="ecc3a-107">È possibile abilitare gli utenti per l'accesso automatico a SCC LifeCycle (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecc3a-107">You can enable your users to automatically get signed-on to SCC LifeCycle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ecc3a-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ecc3a-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ecc3a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ecc3a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ecc3a-110">Prerequisites</span></span>

<span data-ttu-id="ecc3a-111">Per configurare l'integrazione di Azure AD con SCC LifeCycle, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ecc3a-111">To configure Azure AD integration with SCC LifeCycle, you need the following items:</span></span>

- <span data-ttu-id="ecc3a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ecc3a-113">Sottoscrizione di SCC LifeCycle abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ecc3a-113">An SCC LifeCycle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ecc3a-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ecc3a-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ecc3a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ecc3a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ecc3a-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ecc3a-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ecc3a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ecc3a-118">Scenario description</span></span>
<span data-ttu-id="ecc3a-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ecc3a-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ecc3a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ecc3a-121">Aggiunta di SCC LifeCycle dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ecc3a-121">Adding SCC LifeCycle from the gallery</span></span>
2. <span data-ttu-id="ecc3a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecc3a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scc-lifecycle-from-the-gallery"></a><span data-ttu-id="ecc3a-123">Aggiunta di SCC LifeCycle dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ecc3a-123">Adding SCC LifeCycle from the gallery</span></span>
<span data-ttu-id="ecc3a-124">Per configurare l'integrazione di SCC LifeCycle in Azure AD, è necessario aggiungere SCC LifeCycle dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-124">To configure the integration of SCC LifeCycle into Azure AD, you need to add SCC LifeCycle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ecc3a-125">**Per aggiungere SCC LifeCycle dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ecc3a-125">**To add SCC LifeCycle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ecc3a-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ecc3a-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ecc3a-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="ecc3a-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="ecc3a-133">Nella casella di ricerca digitare **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-133">In the search box, type **SCC LifeCycle**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_search.png)

5. <span data-ttu-id="ecc3a-135">Nel pannello dei risultati selezionare **SCC LifeCycle** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-135">In the results panel, select **SCC LifeCycle**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ecc3a-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecc3a-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="ecc3a-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SCC LifeCycle in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ecc3a-138">In this section, you configure and test Azure AD single sign-on with SCC LifeCycle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ecc3a-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di SCC LifeCycle che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SCC LifeCycle is to a user in Azure AD.</span></span> <span data-ttu-id="ecc3a-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-140">In other words, a link relationship between an Azure AD user and the related user in SCC LifeCycle needs to be established.</span></span>

<span data-ttu-id="ecc3a-141">Per stabilire la relazione di collegamento, in SCC LifeCycle assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="ecc3a-141">In SCC LifeCycle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ecc3a-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con SCC LifeCycle, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="ecc3a-142">To configure and test Azure AD single sign-on with SCC LifeCycle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ecc3a-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ecc3a-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ecc3a-145">**[Creazione di un utente di test di SCC LifeCycle](#creating-an-scc-lifecycle-test-user)**: per avere una controparte di Britta Simon in SCC LifeCycle collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-145">**[Creating an SCC LifeCycle test user](#creating-an-scc-lifecycle-test-user)** - to have a counterpart of Britta Simon in SCC LifeCycle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ecc3a-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ecc3a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ecc3a-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecc3a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ecc3a-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SCC LifeCycle application.</span></span>

<span data-ttu-id="ecc3a-150">**Per configurare Single Sign-On di Azure AD con SCC LifeCycle, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ecc3a-150">**To configure Azure AD single sign-on with SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="ecc3a-151">Nella pagina di integrazione dell'applicazione **SCC LifeCycle** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-151">In the Azure portal, on the **SCC LifeCycle** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="ecc3a-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_samlbase.png)

3. <span data-ttu-id="ecc3a-155">Nella sezione **URL e dominio SCC LifeCycle** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ecc3a-155">On the **SCC LifeCycle Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_url.png)

    <span data-ttu-id="ecc3a-157">a.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-157">a.</span></span> <span data-ttu-id="ecc3a-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span></span>

    <span data-ttu-id="ecc3a-159">b.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-159">b.</span></span> <span data-ttu-id="ecc3a-160">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="ecc3a-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|--|
    | `https://bs1.scc.com/<entity>`|
    | `https://lifecycle.scc.com/<entity>`|
    
    > [!NOTE] 
    > <span data-ttu-id="ecc3a-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="ecc3a-161">These values are not real.</span></span> <span data-ttu-id="ecc3a-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ecc3a-163">Per ottenere questi valori contattare il [team di supporto clienti di SCC LifeCycle](mailto:lifecycle.support@scc.com).</span><span class="sxs-lookup"><span data-stu-id="ecc3a-163">Contact [SCC LifeCycle Client support team](mailto:lifecycle.support@scc.com) to get these values.</span></span> 
 
4. <span data-ttu-id="ecc3a-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_certificate.png) 

5. <span data-ttu-id="ecc3a-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ecc3a-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ecc3a-168">Per configurare l'accesso Single Sign-On sul lato **SCC LifeCycle** è necessario inviare il file **XML dei metadati** scaricato al [team di supporto di SCC LifeCycle](mailto:lifecycle.support@scc.com).</span><span class="sxs-lookup"><span data-stu-id="ecc3a-168">To configure single sign-on on **SCC LifeCycle** side, you need to send the downloaded **Metadata XML** to [SCC LifeCycle support team](mailto:lifecycle.support@scc.com).</span></span> <span data-ttu-id="ecc3a-169">Questa impostazione viene configurata in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

     >[!NOTE]
   ><span data-ttu-id="ecc3a-170">L'accesso Single Sign-On deve essere abilitato dal team di supporto di SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-170">Single sign-on has to be enabled by the SCC LifeCycle support team.</span></span>
   > 
   > 

> [!TIP]
> <span data-ttu-id="ecc3a-171">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ecc3a-172">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ecc3a-173">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ecc3a-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ecc3a-174">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecc3a-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="ecc3a-175">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="ecc3a-177">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ecc3a-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ecc3a-178">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ecc3a-180">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ecc3a-182">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ecc3a-184">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ecc3a-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ecc3a-186">a.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-186">a.</span></span> <span data-ttu-id="ecc3a-187">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ecc3a-188">b.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-188">b.</span></span> <span data-ttu-id="ecc3a-189">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ecc3a-190">c.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-190">c.</span></span> <span data-ttu-id="ecc3a-191">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ecc3a-192">d.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-192">d.</span></span> <span data-ttu-id="ecc3a-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-193">Click **Create**.</span></span>
 
### <a name="creating-an-scc-lifecycle-test-user"></a><span data-ttu-id="ecc3a-194">Creazione di un utente di test di SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="ecc3a-194">Creating an SCC LifeCycle test user</span></span>

<span data-ttu-id="ecc3a-195">Per consentire agli utenti di Azure AD di accedere a SCC LifeCycle, è necessario eseguirne il provisioning in SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-195">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="ecc3a-196">Non è richiesto alcun intervento dell'utente per configurare il provisioning degli utenti in SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-196">There is no action item for you to configure user provisioning to SCC LifeCycle.</span></span>

<span data-ttu-id="ecc3a-197">Quando un utente assegnato tenta di accedere a SCC LifeCycle, se necessario viene creato automaticamente un account di SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-197">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

> [!NOTE]
    > <span data-ttu-id="ecc3a-198">Il titolare dell'account Azure Active Directory riceve un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-198">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ecc3a-199">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecc3a-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ecc3a-200">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SCC LifeCycle.</span></span>

![Assegna utente][200] 

<span data-ttu-id="ecc3a-202">**Per assegnare Britta Simon a SCC LifeCycle, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ecc3a-202">**To assign Britta Simon to SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="ecc3a-203">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications.**</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ecc3a-205">Nell'elenco di applicazioni selezionare **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-205">In the applications list, select **SCC LifeCycle**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_app.png) 

3. <span data-ttu-id="ecc3a-207">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="ecc3a-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-209">Click **Add** button.</span></span> <span data-ttu-id="ecc3a-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="ecc3a-212">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ecc3a-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ecc3a-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ecc3a-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ecc3a-215">Testing single sign-on</span></span>

<span data-ttu-id="ecc3a-216">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ecc3a-217">Quando si fa clic sul riquadro SCC LifeCycle nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="ecc3a-217">When you click the SCC LifeCycle tile in the Access Panel, you should get automatically signed-on to SCC LifeCycle application.</span></span>
<span data-ttu-id="ecc3a-218">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ecc3a-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ecc3a-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ecc3a-219">Additional resources</span></span>

* [<span data-ttu-id="ecc3a-220">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ecc3a-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ecc3a-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ecc3a-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_203.png

