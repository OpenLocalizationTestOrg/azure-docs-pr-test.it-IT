---
title: 'Esercitazione: Integrazione di Azure Active Directory con Huddle | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Huddle.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 59d4019545d39ec76bf401696338140f430630c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="b7a05-103">Esercitazione: Integrazione di Azure Active Directory con Huddle</span><span class="sxs-lookup"><span data-stu-id="b7a05-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="b7a05-104">Questa esercitazione descrive come integrare Huddle con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b7a05-104">In this tutorial, you learn how to integrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b7a05-105">L'integrazione di Huddle con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7a05-105">Integrating Huddle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b7a05-106">È possibile controllare in Azure AD chi può accedere a Huddle</span><span class="sxs-lookup"><span data-stu-id="b7a05-106">You can control in Azure AD who has access to Huddle</span></span>
- <span data-ttu-id="b7a05-107">È possibile abilitare gli utenti per l'accesso automatico a Huddle (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="b7a05-107">You can enable your users to automatically get signed-on to Huddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b7a05-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7a05-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b7a05-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b7a05-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7a05-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b7a05-110">Prerequisites</span></span>

<span data-ttu-id="b7a05-111">Per configurare l'integrazione di Azure AD con Huddle, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7a05-111">To configure Azure AD integration with Huddle, you need the following items:</span></span>

- <span data-ttu-id="b7a05-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7a05-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b7a05-113">Sottoscrizione di Huddle abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b7a05-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b7a05-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b7a05-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b7a05-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7a05-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b7a05-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b7a05-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b7a05-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7a05-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b7a05-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b7a05-118">Scenario description</span></span>

<span data-ttu-id="b7a05-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b7a05-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b7a05-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7a05-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b7a05-121">Aggiunta di Huddle dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b7a05-121">Adding Huddle from the gallery</span></span>
2. <span data-ttu-id="b7a05-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7a05-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-the-gallery"></a><span data-ttu-id="b7a05-123">Aggiunta di Huddle dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b7a05-123">Adding Huddle from the gallery</span></span>
<span data-ttu-id="b7a05-124">Per configurare l'integrazione di Huddle in Azure AD, è necessario aggiungere Huddle dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b7a05-124">To configure the integration of Huddle into Azure AD, you need to add Huddle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b7a05-125">**Per aggiungere Huddle dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b7a05-125">**To add Huddle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b7a05-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b7a05-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b7a05-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b7a05-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b7a05-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="b7a05-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b7a05-133">Nella casella di ricerca digitare **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-133">In the search box, type **Huddle**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="b7a05-135">Nel pannello dei risultati selezionare **Huddle** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b7a05-135">In the results panel, select **Huddle**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b7a05-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7a05-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="b7a05-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Huddle usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b7a05-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b7a05-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Huddle corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7a05-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Huddle is to a user in Azure AD.</span></span> <span data-ttu-id="b7a05-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Huddle.</span><span class="sxs-lookup"><span data-stu-id="b7a05-140">In other words, a link relationship between an Azure AD user and the related user in Huddle needs to be established.</span></span>

<span data-ttu-id="b7a05-141">Per stabilire la relazione di collegamento, in Huddle assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="b7a05-141">In Huddle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b7a05-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Huddle, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7a05-142">To configure and test Azure AD single sign-on with Huddle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b7a05-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b7a05-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>

2. <span data-ttu-id="b7a05-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7a05-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="b7a05-145">**[Creazione di un utente di test di Huddle](#creating-a-huddle-test-user)**: per avere una controparte di Britta Simon in Huddle collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7a05-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - to have a counterpart of Britta Simon in Huddle that is linked to the Azure AD representation of user.</span></span>

4. <span data-ttu-id="b7a05-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7a05-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>

5. <span data-ttu-id="b7a05-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="b7a05-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b7a05-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7a05-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b7a05-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Huddle.</span><span class="sxs-lookup"><span data-stu-id="b7a05-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="b7a05-150">**Per configurare l'accesso Single Sign-On di Azure AD con Huddle, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b7a05-150">**To configure Azure AD single sign-on with Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="b7a05-151">Nella pagina di integrazione dell'applicazione **Huddle** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-151">In the Azure portal, on the **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b7a05-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b7a05-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="b7a05-155">Nella sezione **URL e dominio Huddle** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b7a05-155">On the **Huddle Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="b7a05-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="b7a05-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b7a05-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="b7a05-158">This value is not real.</span></span> <span data-ttu-id="b7a05-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="b7a05-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b7a05-160">Per ottenere questo valore, contattare il [team di supporto clienti di Huddle](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="b7a05-160">Contact [Huddle Client support team](https://huddle.zendesk.com) to get this value.</span></span> 

4. <span data-ttu-id="b7a05-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="b7a05-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="b7a05-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b7a05-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b7a05-165">Nella sezione **Configurazione di Huddle** fare clic su **Configura Huddle** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-165">On the **Huddle Configuration** section, click **Configure Huddle** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b7a05-166">Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="b7a05-168">Per configurare l'accesso Single Sign-On sul lato Huddle, è necessario inviare il file **Certificato** scaricato, l'**URL del servizio Single Sign-On SAM** e l'**ID di entità SAML** al [team di supporto clienti di Huddle](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="b7a05-168">To configure single sign-on on Huddle side, you need to send the downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="b7a05-169">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="b7a05-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="b7a05-170">L'accesso Single Sign-On deve essere abilitato dal team di supporto di Huddle.</span><span class="sxs-lookup"><span data-stu-id="b7a05-170">Single sign-on needs to be enabled by the Huddle support team.</span></span> <span data-ttu-id="b7a05-171">Al termine della configurazione verrà visualizzata una notifica.</span><span class="sxs-lookup"><span data-stu-id="b7a05-171">You get a notification when the configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="b7a05-172">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b7a05-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b7a05-173">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="b7a05-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b7a05-174">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b7a05-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b7a05-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7a05-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="b7a05-176">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7a05-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b7a05-178">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b7a05-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b7a05-179">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b7a05-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b7a05-181">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="b7a05-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b7a05-183">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b7a05-185">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b7a05-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b7a05-187">a.</span><span class="sxs-lookup"><span data-stu-id="b7a05-187">a.</span></span> <span data-ttu-id="b7a05-188">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b7a05-189">b.</span><span class="sxs-lookup"><span data-stu-id="b7a05-189">b.</span></span> <span data-ttu-id="b7a05-190">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b7a05-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b7a05-191">c.</span><span class="sxs-lookup"><span data-stu-id="b7a05-191">c.</span></span> <span data-ttu-id="b7a05-192">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b7a05-193">d.</span><span class="sxs-lookup"><span data-stu-id="b7a05-193">d.</span></span> <span data-ttu-id="b7a05-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="b7a05-195">Creazione di un utente di test di Huddle</span><span class="sxs-lookup"><span data-stu-id="b7a05-195">Creating a Huddle test user</span></span>

<span data-ttu-id="b7a05-196">Per consentire agli utenti di Azure AD di accedere a Huddle, è necessario effettuarne il provisioning in Huddle.</span><span class="sxs-lookup"><span data-stu-id="b7a05-196">To enable Azure AD users to log in to Huddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="b7a05-197">Nel caso di Huddle, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="b7a05-197">In the case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="b7a05-198">**Per configurare il provisioning utenti, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b7a05-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="b7a05-199">Accedere al sito aziendale di **Huddle** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b7a05-199">Log in to your **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="b7a05-200">Fare clic su **Area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="b7a05-201">Fare clic su **Persone \> Invite People (Invita persone)**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="b7a05-202">![Persone](./media/active-directory-saas-huddle-tutorial/IC787838.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="b7a05-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="b7a05-203">Nella sezione **Create a new invitation** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b7a05-203">In the **Create a new invitation** section, perform the following steps:</span></span>
   
   <span data-ttu-id="b7a05-204">![Nuovo invito](./media/active-directory-saas-huddle-tutorial/IC787839.png "Nuovo invito")</span><span class="sxs-lookup"><span data-stu-id="b7a05-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="b7a05-205">a.</span><span class="sxs-lookup"><span data-stu-id="b7a05-205">a.</span></span> <span data-ttu-id="b7a05-206">Nell'elenco **Scegli un team per invitare persone a partecipare** selezionare **team**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-206">In the **Choose a team to invite people to join** list, select **team**.</span></span>

   <span data-ttu-id="b7a05-207">b.</span><span class="sxs-lookup"><span data-stu-id="b7a05-207">b.</span></span> <span data-ttu-id="b7a05-208">Nella casella di testo **Enter email address for people you'd like to invite** (Immetti indirizzo di posta elettronica degli utenti da invitare) digitare l'**indirizzo di posta elettronica** di un account Azure AD valido di cui si vuole effettuare il provisioning.</span><span class="sxs-lookup"><span data-stu-id="b7a05-208">Type the **Email Address** of a valid Azure AD account you want to provision in to **Enter email address for people you'd like to invite** textbox.</span></span>

   <span data-ttu-id="b7a05-209">c.</span><span class="sxs-lookup"><span data-stu-id="b7a05-209">c.</span></span> <span data-ttu-id="b7a05-210">Fare clic su **Invita**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="b7a05-211">Il titolare dell'account Azure AD riceverà un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="b7a05-211">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="b7a05-212">È possibile usare qualsiasi altro strumento o API di creazione di account utente offerti da Huddle per effettuare il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7a05-212">You can use any other Huddle user account creation tools or APIs provided by Huddle to provision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b7a05-213">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7a05-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b7a05-214">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Huddle.</span><span class="sxs-lookup"><span data-stu-id="b7a05-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Huddle.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b7a05-216">**Per assegnare Britta Simon a Huddle, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b7a05-216">**To assign Britta Simon to Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="b7a05-217">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b7a05-219">Nell'elenco di applicazioni selezionare **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-219">In the applications list, select **Huddle**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="b7a05-221">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b7a05-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b7a05-223">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-223">Click **Add** button.</span></span> <span data-ttu-id="b7a05-224">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b7a05-226">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="b7a05-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b7a05-227">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b7a05-228">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b7a05-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b7a05-229">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b7a05-229">Testing single sign-on</span></span>

<span data-ttu-id="b7a05-230">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b7a05-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b7a05-231">Quando si fa clic sul riquadro Huddle nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Huddle.</span><span class="sxs-lookup"><span data-stu-id="b7a05-231">When you click the Huddle tile in the Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="b7a05-232">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b7a05-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b7a05-233">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b7a05-233">Additional resources</span></span>

* [<span data-ttu-id="b7a05-234">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7a05-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b7a05-235">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7a05-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
