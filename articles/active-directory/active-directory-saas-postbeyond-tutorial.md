---
title: 'Esercitazione: Integrazione di Azure Active Directory con PostBeyond | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e PostBeyond.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 09992f08-ec50-4472-997f-ccbe719039e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 80b920dc99619795cbc86e8cb2e3ac2a78a71932
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-postbeyond"></a><span data-ttu-id="b71d5-103">Esercitazione: Integrazione di Azure Active Directory con PostBeyond</span><span class="sxs-lookup"><span data-stu-id="b71d5-103">Tutorial: Azure Active Directory integration with PostBeyond</span></span>

<span data-ttu-id="b71d5-104">Questa esercitazione descrive come integrare PostBeyond con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b71d5-104">In this tutorial, you learn how to integrate PostBeyond with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b71d5-105">L'integrazione di PostBeyond con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b71d5-105">Integrating PostBeyond with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b71d5-106">È possibile controllare in Azure AD chi può accedere a PostBeyond</span><span class="sxs-lookup"><span data-stu-id="b71d5-106">You can control in Azure AD who has access to PostBeyond</span></span>
- <span data-ttu-id="b71d5-107">È possibile abilitare gli utenti per l'accesso automatico a PostBeyond (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="b71d5-107">You can enable your users to automatically get signed-on to PostBeyond (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b71d5-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b71d5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b71d5-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b71d5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b71d5-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b71d5-110">Prerequisites</span></span>

<span data-ttu-id="b71d5-111">Per configurare l'integrazione di Azure AD con PostBeyond, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b71d5-111">To configure Azure AD integration with PostBeyond, you need the following items:</span></span>

- <span data-ttu-id="b71d5-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b71d5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b71d5-113">Sottoscrizione di PostBeyond abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b71d5-113">A PostBeyond single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b71d5-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b71d5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b71d5-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b71d5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b71d5-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b71d5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b71d5-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b71d5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b71d5-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b71d5-118">Scenario description</span></span>
<span data-ttu-id="b71d5-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b71d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b71d5-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b71d5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b71d5-121">Aggiunta di PostBeyond dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b71d5-121">Adding PostBeyond from the gallery</span></span>
2. <span data-ttu-id="b71d5-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b71d5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-postbeyond-from-the-gallery"></a><span data-ttu-id="b71d5-123">Aggiunta di PostBeyond dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b71d5-123">Adding PostBeyond from the gallery</span></span>
<span data-ttu-id="b71d5-124">Per configurare l'integrazione di PostBeyond in Azure AD, è necessario aggiungerla dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b71d5-124">To configure the integration of PostBeyond into Azure AD, you need to add PostBeyond from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b71d5-125">**Per aggiungere PostBeyond dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b71d5-125">**To add PostBeyond from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b71d5-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b71d5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b71d5-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b71d5-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b71d5-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="b71d5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b71d5-133">Nella casella di ricerca digitare **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-133">In the search box, type **PostBeyond**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_search.png)

5. <span data-ttu-id="b71d5-135">Nel pannello dei risultati selezionare **PostBeyond** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b71d5-135">In the results panel, select **PostBeyond**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b71d5-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b71d5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b71d5-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con PostBeyond con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b71d5-138">In this section, you configure and test Azure AD single sign-on with PostBeyond based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b71d5-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di PostBeyond che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b71d5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PostBeyond is to a user in Azure AD.</span></span> <span data-ttu-id="b71d5-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="b71d5-140">In other words, a link relationship between an Azure AD user and the related user in PostBeyond needs to be established.</span></span>

<span data-ttu-id="b71d5-141">Per stabilire la relazione di collegamento, in PostBeyond assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="b71d5-141">In PostBeyond, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b71d5-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con PostBeyond, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b71d5-142">To configure and test Azure AD single sign-on with PostBeyond, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b71d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b71d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b71d5-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b71d5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b71d5-145">**[Creazione di un utente test PostBeyond](#creating-a-postbeyond-test-user)**: per avere una controparte di Britta Simon in PostBeyond collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b71d5-145">**[Creating a PostBeyond test user](#creating-a-postbeyond-test-user)** - to have a counterpart of Britta Simon in PostBeyond that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b71d5-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b71d5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b71d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="b71d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b71d5-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b71d5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b71d5-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="b71d5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PostBeyond application.</span></span>

<span data-ttu-id="b71d5-150">**Per configurare l'accesso Single Sign-On di Azure AD con PostBeyond, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b71d5-150">**To configure Azure AD single sign-on with PostBeyond, perform the following steps:**</span></span>

1. <span data-ttu-id="b71d5-151">Nella pagina di integrazione dell'applicazione **PostBeyond** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-151">In the Azure portal, on the **PostBeyond** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b71d5-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b71d5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_samlbase.png)

3. <span data-ttu-id="b71d5-155">Nella sezione **URL e dominio PostBeyond** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b71d5-155">On the **PostBeyond Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_url.png)

    <span data-ttu-id="b71d5-157">a.</span><span class="sxs-lookup"><span data-stu-id="b71d5-157">a.</span></span> <span data-ttu-id="b71d5-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.postbeyond.com`.</span><span class="sxs-lookup"><span data-stu-id="b71d5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    <span data-ttu-id="b71d5-159">b.</span><span class="sxs-lookup"><span data-stu-id="b71d5-159">b.</span></span> <span data-ttu-id="b71d5-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="b71d5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b71d5-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="b71d5-161">These values are not real.</span></span> <span data-ttu-id="b71d5-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="b71d5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b71d5-163">Per ottenere questi valori, contattare il [team di supporto clienti di PostBeyond](mailto:sso@postbeyond.com).</span><span class="sxs-lookup"><span data-stu-id="b71d5-163">Contact [PostBeyond Client support team](mailto:sso@postbeyond.com) to get these values.</span></span> 
 
4. <span data-ttu-id="b71d5-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="b71d5-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_certificate.png) 

5. <span data-ttu-id="b71d5-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b71d5-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-postbeyond-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b71d5-168">Nella sezione **Configurazione di PostBeyond** fare clic su **Configura PostBeyond** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-168">On the **PostBeyond Configuration** section, click **Configure PostBeyond** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b71d5-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="b71d5-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_configure.png) 

7. <span data-ttu-id="b71d5-171">Per configurare l'accesso Single Sign-On sul lato **PostBeyond**, è necessario inviare il file di **Certificato (Base64) scaricato**, **l'ID entità SAML**, **l'URL di disconnessione e l'URL del servizio Single Sign-On SAML** e  **l’URL di disconnessione** al [team di supporto di PostBeyond](mailto:sso@postbeyond.com).</span><span class="sxs-lookup"><span data-stu-id="b71d5-171">To configure single sign-on on **PostBeyond** side, you need to send the downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** to [PostBeyond support team](mailto:sso@postbeyond.com).</span></span> <span data-ttu-id="b71d5-172">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="b71d5-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b71d5-173">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b71d5-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b71d5-174">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="b71d5-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b71d5-175">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b71d5-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b71d5-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b71d5-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="b71d5-177">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b71d5-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b71d5-179">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b71d5-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b71d5-180">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b71d5-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b71d5-182">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="b71d5-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b71d5-184">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b71d5-186">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b71d5-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b71d5-188">a.</span><span class="sxs-lookup"><span data-stu-id="b71d5-188">a.</span></span> <span data-ttu-id="b71d5-189">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b71d5-190">b.</span><span class="sxs-lookup"><span data-stu-id="b71d5-190">b.</span></span> <span data-ttu-id="b71d5-191">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b71d5-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b71d5-192">c.</span><span class="sxs-lookup"><span data-stu-id="b71d5-192">c.</span></span> <span data-ttu-id="b71d5-193">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b71d5-194">d.</span><span class="sxs-lookup"><span data-stu-id="b71d5-194">d.</span></span> <span data-ttu-id="b71d5-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-195">Click **Create**.</span></span>
 
### <a name="creating-a-postbeyond-test-user"></a><span data-ttu-id="b71d5-196">Creazione di un utente test PostBeyond</span><span class="sxs-lookup"><span data-stu-id="b71d5-196">Creating a PostBeyond test user</span></span>

<span data-ttu-id="b71d5-197">In questa sezione viene creato un utente chiamato Britta Simon in PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="b71d5-197">In this section, you create a user called Britta Simon in PostBeyond.</span></span> <span data-ttu-id="b71d5-198">Se non si sa come aggiungere Britta Simon in PostBeyond, rivolgersi al [team di supporto di PostBeyond](mailto:sso@postbeyond.com) per aggiungere l'utente test e abilitare SSO.</span><span class="sxs-lookup"><span data-stu-id="b71d5-198">If you don't know how to add Britta Simon in PostBeyond, please work with [PostBeyond support team](mailto:sso@postbeyond.com) to add the test user and enable SSO.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b71d5-199">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b71d5-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b71d5-200">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="b71d5-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PostBeyond.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b71d5-202">**Per assegnare Britta Simon a PostBeyond, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b71d5-202">**To assign Britta Simon to PostBeyond, perform the following steps:**</span></span>

1. <span data-ttu-id="b71d5-203">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b71d5-205">Nell'elenco di applicazioni selezionare **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-205">In the applications list, select **PostBeyond**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_app.png) 

3. <span data-ttu-id="b71d5-207">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b71d5-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b71d5-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-209">Click **Add** button.</span></span> <span data-ttu-id="b71d5-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b71d5-212">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="b71d5-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b71d5-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b71d5-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b71d5-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b71d5-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b71d5-215">Testing single sign-on</span></span>

<span data-ttu-id="b71d5-216">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b71d5-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="b71d5-217">Quando si fa clic sul riquadro PostBeyond nel pannello di accesso, verrà visualizzata la pagina di accesso di PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="b71d5-217">When you click the PostBeyond tile in the Access Panel, you should get to the PostBeyond sign in page.</span></span> <span data-ttu-id="b71d5-218">Fare clic su **Sign in with Office 365**(Accedi con Office 365) e immettere le credenziali di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b71d5-218">Click on **Sign in with Office 365**, enter your Azure AD credentials.</span></span> <span data-ttu-id="b71d5-219">Verrà eseguito l'accesso a PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="b71d5-219">Then, you should be logged in into PostBeyond.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b71d5-220">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b71d5-220">Additional resources</span></span>

* [<span data-ttu-id="b71d5-221">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b71d5-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b71d5-222">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b71d5-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_203.png

