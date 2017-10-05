---
title: 'Esercitazione: Integrazione di Azure Active Directory con Inkling | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Inkling.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 7b0639c6515298731f88346c2e4ca82664653a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="2b355-103">Esercitazione: Integrazione di Azure Active Directory con Inkling</span><span class="sxs-lookup"><span data-stu-id="2b355-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="2b355-104">Questa esercitazione descrive come integrare Inkling con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b355-104">In this tutorial, you learn how to integrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2b355-105">L'integrazione di Inkling con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b355-105">Integrating Inkling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2b355-106">È possibile controllare in Azure AD chi può accedere a Inkling</span><span class="sxs-lookup"><span data-stu-id="2b355-106">You can control in Azure AD who has access to Inkling</span></span>
- <span data-ttu-id="2b355-107">È possibile abilitare gli utenti per l'accesso automatico a Inkling (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b355-107">You can enable your users to automatically get signed-on to Inkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2b355-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="2b355-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="2b355-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2b355-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b355-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2b355-110">Prerequisites</span></span>

<span data-ttu-id="2b355-111">Per configurare l'integrazione di Azure AD con Inkling sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b355-111">To configure Azure AD integration with Inkling, you need the following items:</span></span>

- <span data-ttu-id="2b355-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b355-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2b355-113">Sottoscrizione di Inkling abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2b355-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="2b355-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2b355-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="2b355-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b355-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b355-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2b355-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2b355-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b355-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="2b355-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2b355-118">Scenario description</span></span>
<span data-ttu-id="2b355-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2b355-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2b355-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b355-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b355-121">Aggiunta di Inkling dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2b355-121">Adding Inkling from the gallery</span></span>
2. <span data-ttu-id="2b355-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b355-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-the-gallery"></a><span data-ttu-id="2b355-123">Aggiunta di Inkling dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2b355-123">Adding Inkling from the gallery</span></span>
<span data-ttu-id="2b355-124">Per configurare l'integrazione di Inkling in Azure AD è necessario aggiungere Inkling dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2b355-124">To configure the integration of Inkling into Azure AD, you need to add Inkling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2b355-125">**Per aggiungere Inkling dalla raccolta seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2b355-125">**To add Inkling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2b355-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2b355-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2b355-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="2b355-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2b355-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2b355-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="2b355-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2b355-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="2b355-133">Nella casella di ricerca digitare **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="2b355-133">In the search box, type **Inkling**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="2b355-135">Nel pannello dei risultati selezionare **Inkling** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2b355-135">In the results panel, select **Inkling**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2b355-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b355-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2b355-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Inkling in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2b355-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2b355-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di Inkling che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b355-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Inkling is to a user in Azure AD.</span></span> <span data-ttu-id="2b355-140">In altre parole deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Inkling.</span><span class="sxs-lookup"><span data-stu-id="2b355-140">In other words, a link relationship between an Azure AD user and the related user in Inkling needs to be established.</span></span>

<span data-ttu-id="2b355-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in Inkling.</span><span class="sxs-lookup"><span data-stu-id="2b355-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Inkling.</span></span>

<span data-ttu-id="2b355-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Inkling è necessario completare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b355-142">To configure and test Azure AD single sign-on with Inkling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2b355-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2b355-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2b355-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2b355-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b355-145">**[Creazione di un utente di test di Inkling](#creating-an-inkling-test-user)**: per avere una controparte di Britta Simon in Inkling collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b355-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - to have a counterpart of Britta Simon in Inkling that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2b355-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b355-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b355-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="2b355-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2b355-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b355-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2b355-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Inkling.</span><span class="sxs-lookup"><span data-stu-id="2b355-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="2b355-150">**Per configurare l'accesso Single Sign-On di Azure AD con Inkling, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2b355-150">**To configure Azure AD single sign-on with Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="2b355-151">Nella pagina di integrazione dell'applicazione **Inkling** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2b355-151">In the Azure Management portal, on the **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="2b355-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="2b355-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="2b355-155">Nella sezione **URL e dominio Inkling** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2b355-155">On the **Inkling Domain and URLs** section, perform the following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="2b355-157">a.</span><span class="sxs-lookup"><span data-stu-id="2b355-157">a.</span></span> <span data-ttu-id="2b355-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="2b355-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="2b355-159">b.</span><span class="sxs-lookup"><span data-stu-id="2b355-159">b.</span></span> <span data-ttu-id="2b355-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="2b355-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2b355-161">Si noti che questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="2b355-161">Please note that these are not the real values.</span></span> <span data-ttu-id="2b355-162">È necessario aggiornare questi valori con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="2b355-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="2b355-163">Per ottenere questi valori contattare il [team di supporto di Inkling](mailto:press@inkling.com).</span><span class="sxs-lookup"><span data-stu-id="2b355-163">Contact [Inkling support team](mailto:press@inkling.com) to get these values.</span></span>

4. <span data-ttu-id="2b355-164">Nella sezione **Certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="2b355-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="2b355-166">Nella finestra di dialogo **Crea nuovo certificato** fare clic sull'icona del calendario e selezionare una **data di scadenza**.</span><span class="sxs-lookup"><span data-stu-id="2b355-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="2b355-167">Fare quindi clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="2b355-167">Then click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="2b355-169">Nella sezione **Certificato di firma SAML** selezionare **Make new certificate active** (Rendi attivo il nuovo certificato) e fare clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="2b355-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="2b355-171">Nella finestra popup **Rollover certificate** (Certificato di rollover) fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b355-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="2b355-173">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="2b355-173">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="2b355-175">Per ottenere la configurazione dell'accesso Single Sign-On per l'applicazione contattare il [team di supporto di Inkling](mailto:press@inkling.com) e fornire i **metadati** scaricati.</span><span class="sxs-lookup"><span data-stu-id="2b355-175">To get SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2b355-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b355-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="2b355-177">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2b355-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="2b355-179">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2b355-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2b355-180">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2b355-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2b355-182">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="2b355-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2b355-184">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="2b355-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2b355-186">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2b355-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2b355-188">a.</span><span class="sxs-lookup"><span data-stu-id="2b355-188">a.</span></span> <span data-ttu-id="2b355-189">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2b355-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2b355-190">b.</span><span class="sxs-lookup"><span data-stu-id="2b355-190">b.</span></span> <span data-ttu-id="2b355-191">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2b355-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2b355-192">c.</span><span class="sxs-lookup"><span data-stu-id="2b355-192">c.</span></span> <span data-ttu-id="2b355-193">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="2b355-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2b355-194">d.</span><span class="sxs-lookup"><span data-stu-id="2b355-194">d.</span></span> <span data-ttu-id="2b355-195">Fare clic su **Create**(Crea).</span><span class="sxs-lookup"><span data-stu-id="2b355-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="2b355-196">Creazione di un utente di test di Inkling</span><span class="sxs-lookup"><span data-stu-id="2b355-196">Creating an Inkling test user</span></span>

<span data-ttu-id="2b355-197">In questa sezione viene creato un utente chiamato Britta Simon in Inkling.</span><span class="sxs-lookup"><span data-stu-id="2b355-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="2b355-198">Collaborare con il [team di supporto di Inkling](mailto:press@inkling.com) per aggiungere gli utenti alla piattaforma Inkling.</span><span class="sxs-lookup"><span data-stu-id="2b355-198">Please work with [Inkling support team](mailto:press@inkling.com) to add the users in the Inkling platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2b355-199">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b355-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2b355-200">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Inkling.</span><span class="sxs-lookup"><span data-stu-id="2b355-200">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Inkling.</span></span>

![Assegna utente][200] 

<span data-ttu-id="2b355-202">**Per assegnare Britta Simon a Inkling seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2b355-202">**To assign Britta Simon to Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="2b355-203">Nel portale di gestione di Azure aprire la visualizzazione applicazioni, passare alla visualizzazione directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2b355-203">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2b355-205">Nell'elenco di applicazioni selezionare **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="2b355-205">In the applications list, select **Inkling**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="2b355-207">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="2b355-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="2b355-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2b355-209">Click **Add** button.</span></span> <span data-ttu-id="2b355-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2b355-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="2b355-212">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="2b355-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2b355-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2b355-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2b355-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2b355-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="2b355-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2b355-215">Testing single sign-on</span></span>

<span data-ttu-id="2b355-216">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2b355-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2b355-217">Quando si fa clic sul riquadro Inkling nel pannello di accesso, si accederà automaticamente all'applicazione Inkling.</span><span class="sxs-lookup"><span data-stu-id="2b355-217">When you click the Inkling tile in the Access Panel, you should get automatically signed-on to your Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2b355-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2b355-218">Additional resources</span></span>

* [<span data-ttu-id="2b355-219">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b355-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b355-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b355-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png