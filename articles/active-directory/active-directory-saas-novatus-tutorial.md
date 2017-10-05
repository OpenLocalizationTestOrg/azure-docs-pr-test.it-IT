---
title: 'Esercitazione: Integrazione di Azure Active Directory con Novatus | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Novatus.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: jeedes
ms.openlocfilehash: ec67e96309a8877e6fb65b30da1501e4f34a9ee4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="254b4-103">Esercitazione: Integrazione di Azure Active Directory con Novatus</span><span class="sxs-lookup"><span data-stu-id="254b4-103">Tutorial: Azure Active Directory integration with Novatus</span></span>

<span data-ttu-id="254b4-104">Questa esercitazione descrive come integrare Novatus con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="254b4-104">In this tutorial, you learn how to integrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="254b4-105">L'integrazione di Novatus con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="254b4-105">Integrating Novatus with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="254b4-106">È possibile controllare in Azure AD chi può accedere a Novatus.</span><span class="sxs-lookup"><span data-stu-id="254b4-106">You can control in Azure AD who has access to Novatus</span></span>
- <span data-ttu-id="254b4-107">È possibile abilitare gli utenti per l'accesso automatico a Novatus (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="254b4-107">You can enable your users to automatically get signed-on to Novatus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="254b4-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="254b4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="254b4-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="254b4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="254b4-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="254b4-110">Prerequisites</span></span>

<span data-ttu-id="254b4-111">Per configurare l'integrazione di Azure AD con Novatus, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="254b4-111">To configure Azure AD integration with Novatus, you need the following items:</span></span>

- <span data-ttu-id="254b4-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="254b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="254b4-113">Sottoscrizione di Novatus abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="254b4-113">A Novatus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="254b4-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="254b4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="254b4-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="254b4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="254b4-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="254b4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="254b4-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="254b4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="254b4-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="254b4-118">Scenario description</span></span>
<span data-ttu-id="254b4-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="254b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="254b4-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="254b4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="254b4-121">Aggiunta di Novatus dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="254b4-121">Adding Novatus from the gallery</span></span>
2. <span data-ttu-id="254b4-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="254b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-novatus-from-the-gallery"></a><span data-ttu-id="254b4-123">Aggiunta di Novatus dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="254b4-123">Adding Novatus from the gallery</span></span>
<span data-ttu-id="254b4-124">Per configurare l'integrazione di Novatus in Azure AD, è necessario aggiungere Novatus dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="254b4-124">To configure the integration of Novatus into Azure AD, you need to add Novatus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="254b4-125">**Per aggiungere Novatus dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="254b4-125">**To add Novatus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="254b4-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="254b4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="254b4-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="254b4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="254b4-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="254b4-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="254b4-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="254b4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="254b4-133">Nella casella di ricerca digitare **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="254b4-133">In the search box, type **Novatus**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_search.png)

5. <span data-ttu-id="254b4-135">Nel pannello dei risultati selezionare **Novatus** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="254b4-135">In the results panel, select **Novatus**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="254b4-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="254b4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="254b4-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Novatus usando un utente di prova di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="254b4-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="254b4-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente controparte di Novatus che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="254b4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Novatus is to a user in Azure AD.</span></span> <span data-ttu-id="254b4-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Novatus.</span><span class="sxs-lookup"><span data-stu-id="254b4-140">In other words, a link relationship between an Azure AD user and the related user in Novatus needs to be established.</span></span>

<span data-ttu-id="254b4-141">Per stabilire la relazione di collegamento, in Novatus assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="254b4-141">In Novatus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="254b4-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Novatus, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="254b4-142">To configure and test Azure AD single sign-on with Novatus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="254b4-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="254b4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="254b4-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="254b4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="254b4-145">**[Creazione di un utente test per Novatus](#creating-a-novatus-test-user)** : per avere una controparte di Britta Simon in Novatus collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="254b4-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - to have a counterpart of Britta Simon in Novatus that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="254b4-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="254b4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="254b4-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="254b4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="254b4-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="254b4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="254b4-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On all’applicazione Novatus.</span><span class="sxs-lookup"><span data-stu-id="254b4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Novatus application.</span></span>

<span data-ttu-id="254b4-150">**Per configurare l'accesso Single Sign-On di Azure AD con Novatus, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="254b4-150">**To configure Azure AD single sign-on with Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="254b4-151">Nella pagina di integrazione dell'applicazione **Novatus** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="254b4-151">In the Azure portal, on the **Novatus** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="254b4-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="254b4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_samlbase.png)

3. <span data-ttu-id="254b4-155">Nella sezione **URL e dominio Novatus** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="254b4-155">On the **Novatus Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_url.png)

     <span data-ttu-id="254b4-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://sso.novatuscontracts.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="254b4-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.novatuscontracts.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="254b4-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="254b4-158">This value is not real.</span></span> <span data-ttu-id="254b4-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="254b4-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="254b4-160">Per ottenere questo valore, contattare il [team di supporto clienti di Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="254b4-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) to get this value.</span></span> 
 


4. <span data-ttu-id="254b4-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="254b4-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_certificate.png) 

5. <span data-ttu-id="254b4-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="254b4-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-novatus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="254b4-165">Nella sezione **Configurazione di Novatus** fare clic su **Configura Novatus** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="254b4-165">On the **Novatus Configuration** section, click **Configure Novatus** to open **Configure sign-on** window.</span></span> <span data-ttu-id="254b4-166">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="254b4-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_configure.png) 

7. <span data-ttu-id="254b4-168">Per ottenere la configurazione dell'accesso SSO per l'applicazione, contattare il [team di supporto di Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="254b4-168">To get SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> <span data-ttu-id="254b4-169">Allegare il file del **certificato scaricato** al messaggio di posta elettronica e condividere gli **URL dei metadati** (**URL di disconnessione, ID entità SAML, URL di accesso Single Sign-On di servizio SAML**) con il team Novatus per configurare SSO.</span><span class="sxs-lookup"><span data-stu-id="254b4-169">Attach the **downloaded certificate** file to your mail and share the **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team to set up SSO on their side.</span></span>

> [!TIP]
> <span data-ttu-id="254b4-170">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="254b4-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="254b4-171">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="254b4-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="254b4-172">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="254b4-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="254b4-173">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="254b4-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="254b4-174">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="254b4-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="254b4-176">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="254b4-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="254b4-177">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="254b4-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="254b4-179">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="254b4-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="254b4-181">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="254b4-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="254b4-183">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="254b4-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="254b4-185">a.</span><span class="sxs-lookup"><span data-stu-id="254b4-185">a.</span></span> <span data-ttu-id="254b4-186">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="254b4-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="254b4-187">b.</span><span class="sxs-lookup"><span data-stu-id="254b4-187">b.</span></span> <span data-ttu-id="254b4-188">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="254b4-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="254b4-189">c.</span><span class="sxs-lookup"><span data-stu-id="254b4-189">c.</span></span> <span data-ttu-id="254b4-190">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="254b4-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="254b4-191">d.</span><span class="sxs-lookup"><span data-stu-id="254b4-191">d.</span></span> <span data-ttu-id="254b4-192">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="254b4-192">Click **Create**.</span></span>
 
### <a name="creating-a-novatus-test-user"></a><span data-ttu-id="254b4-193">Creazione di un utente test per Novatus</span><span class="sxs-lookup"><span data-stu-id="254b4-193">Creating a Novatus test user</span></span>

<span data-ttu-id="254b4-194">Questa sezione descrive come creare un utente chiamato Britta Simon in Novatus.</span><span class="sxs-lookup"><span data-stu-id="254b4-194">The objective of this section is to create a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="254b4-195">Novatus supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="254b4-195">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="254b4-196">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="254b4-196">There is no action item for you in this section.</span></span> <span data-ttu-id="254b4-197">Durante il tentativo di accesso a Novatus verrà creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="254b4-197">A new user will be created during an attempt to access Novatus if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="254b4-198">Per creare un utente manualmente, è necessario contattare il [team di supporto di Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="254b4-198">If you need to create an user manually, you need to contact the [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="254b4-199">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="254b4-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="254b4-200">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Novatus.</span><span class="sxs-lookup"><span data-stu-id="254b4-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Novatus.</span></span>

![Assegna utente][200] 

<span data-ttu-id="254b4-202">**Per assegnare Britta Simon a Novatus, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="254b4-202">**To assign Britta Simon to Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="254b4-203">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="254b4-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="254b4-205">Nell'elenco di applicazioni selezionare **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="254b4-205">In the applications list, select **Novatus**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_app.png) 

3. <span data-ttu-id="254b4-207">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="254b4-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="254b4-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="254b4-209">Click **Add** button.</span></span> <span data-ttu-id="254b4-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="254b4-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="254b4-212">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="254b4-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="254b4-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="254b4-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="254b4-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="254b4-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="254b4-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="254b4-215">Testing single sign-on</span></span>

<span data-ttu-id="254b4-216">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="254b4-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="254b4-217">Quando si fa clic sul riquadro Novatus nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Novatus.</span><span class="sxs-lookup"><span data-stu-id="254b4-217">When you click the Novatus tile in the Access Panel, you should get automatically signed-on to your Novatus application.</span></span> <span data-ttu-id="254b4-218">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="254b4-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="254b4-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="254b4-219">Additional resources</span></span>

* [<span data-ttu-id="254b4-220">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="254b4-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="254b4-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="254b4-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_203.png

