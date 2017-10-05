---
title: 'Esercitazione: Integrazione di Azure Active Directory con Mixpanel | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Mixpanel.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3dd11b3477de1329c1c8e45a6dbf212b1635fd95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="30b3c-103">Esercitazione: Integrazione di Azure Active Directory con Mixpanel</span><span class="sxs-lookup"><span data-stu-id="30b3c-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="30b3c-104">Questa esercitazione descrive come integrare Mixpanel con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="30b3c-104">In this tutorial, you learn how to integrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="30b3c-105">L'integrazione di Mixpanel con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="30b3c-105">Integrating Mixpanel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="30b3c-106">È possibile controllare in Azure AD chi può accedere a Mixpanel</span><span class="sxs-lookup"><span data-stu-id="30b3c-106">You can control in Azure AD who has access to Mixpanel</span></span>
- <span data-ttu-id="30b3c-107">È possibile abilitare gli utenti per l'accesso automatico a Mixpanel (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="30b3c-107">You can enable your users to automatically get signed-on to Mixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="30b3c-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="30b3c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="30b3c-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="30b3c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30b3c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="30b3c-110">Prerequisites</span></span>

<span data-ttu-id="30b3c-111">Per configurare l'integrazione di Azure AD con Mixpanel, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="30b3c-111">To configure Azure AD integration with Mixpanel, you need the following items:</span></span>

- <span data-ttu-id="30b3c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30b3c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="30b3c-113">Sottoscrizione di Mixpanel abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="30b3c-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="30b3c-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="30b3c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="30b3c-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="30b3c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="30b3c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="30b3c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="30b3c-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="30b3c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="30b3c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="30b3c-118">Scenario description</span></span>
<span data-ttu-id="30b3c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="30b3c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="30b3c-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="30b3c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="30b3c-121">Aggiunta di Mixpanel dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="30b3c-121">Adding Mixpanel from the gallery</span></span>
2. <span data-ttu-id="30b3c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="30b3c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-the-gallery"></a><span data-ttu-id="30b3c-123">Aggiunta di Mixpanel dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="30b3c-123">Adding Mixpanel from the gallery</span></span>
<span data-ttu-id="30b3c-124">Per configurare l'integrazione di Mixpanel in Azure AD, è necessario aggiungere Mixpanel dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="30b3c-124">To configure the integration of Mixpanel into Azure AD, you need to add Mixpanel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="30b3c-125">**Per aggiungere Mixpanel dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="30b3c-125">**To add Mixpanel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="30b3c-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="30b3c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="30b3c-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="30b3c-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="30b3c-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="30b3c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="30b3c-133">Nella casella di ricerca digitare **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-133">In the search box, type **Mixpanel**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. <span data-ttu-id="30b3c-135">Nel pannello dei risultati selezionare **Mixpanel** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="30b3c-135">In the results panel, select **Mixpanel**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="30b3c-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="30b3c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="30b3c-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Mixpanel con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="30b3c-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="30b3c-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Mixpanel che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30b3c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mixpanel is to a user in Azure AD.</span></span> <span data-ttu-id="30b3c-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="30b3c-140">In other words, a link relationship between an Azure AD user and the related user in Mixpanel needs to be established.</span></span>

<span data-ttu-id="30b3c-141">Per stabilire la relazione di collegamento, in Mixpanel assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="30b3c-141">In Mixpanel, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="30b3c-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Mixpanel, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="30b3c-142">To configure and test Azure AD single sign-on with Mixpanel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="30b3c-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="30b3c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="30b3c-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="30b3c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="30b3c-145">**[Creare un utente di test Mixpanel](#creating-a-mixpanel-test-user)** : per avere una controparte di Britta Simon in Mixpanel collegata alla rispettiva rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30b3c-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - to have a counterpart of Britta Simon in Mixpanel that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="30b3c-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30b3c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="30b3c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="30b3c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="30b3c-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="30b3c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="30b3c-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="30b3c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="30b3c-150">**Per configurare l'accesso Single Sign-On di Azure AD con Mixpanel, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="30b3c-150">**To configure Azure AD single sign-on with Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="30b3c-151">Nella pagina di integrazione dell'applicazione **Mixpanel** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-151">In the Azure portal, on the **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="30b3c-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="30b3c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. <span data-ttu-id="30b3c-155">Nella sezione **URL e dominio Mixpanel** eseguire i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="30b3c-155">On the **Mixpanel Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="30b3c-157">Nella casella di testo **URL di accesso** digitare l'URL come: `https://mixpanel.com/login/`</span><span class="sxs-lookup"><span data-stu-id="30b3c-157">In the **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="30b3c-158">Eseguire la registrazione nella pagina [https://mixpanel.com/register/](https://mixpanel.com/register/) per configurare le credenziali di accesso e contattare il [team di supporto di Mixpanel](mailto:support@mixpanel.com) per abilitare le impostazioni SSO per il tenant.</span><span class="sxs-lookup"><span data-stu-id="30b3c-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) to set up your login credentials and  contact the [Mixpanel support team](mailto:support@mixpanel.com) to enable SSO settings for your tenant.</span></span> <span data-ttu-id="30b3c-159">Se necessario, è possibile ottenere anche il valore per l'URL di accesso dal team di supporto di Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="30b3c-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
4. <span data-ttu-id="30b3c-160">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="30b3c-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. <span data-ttu-id="30b3c-162">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="30b3c-162">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="30b3c-164">Nella sezione **Configurazione di Mixpanel** fare clic su **Configura Mixpanel** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-164">On the **Mixpanel Configuration** section, click **Configure Mixpanel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="30b3c-165">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="30b3c-165">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. <span data-ttu-id="30b3c-167">In una finestra del browser diversa accedere all'applicazione Mixpanel come amministratore.</span><span class="sxs-lookup"><span data-stu-id="30b3c-167">In a different browser window, sign-on to your Mixpanel application as an administrator.</span></span>

8. <span data-ttu-id="30b3c-168">Nella parte inferiore della pagina fare clic sull'icona a forma di piccolo **ingranaggio** nell'angolo sinistro.</span><span class="sxs-lookup"><span data-stu-id="30b3c-168">On bottom of the page, click the little **gear** icon in the left corner.</span></span> 
   
    ![Accesso Single Sign-On di Mixpanel ](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. <span data-ttu-id="30b3c-170">Fare clic sulla scheda **Access security** (Sicurezza accesso) e quindi su **Change settings** (Modifica impostazioni).</span><span class="sxs-lookup"><span data-stu-id="30b3c-170">Click the **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Impostazioni di Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. <span data-ttu-id="30b3c-172">Nella finestra di dialogo **Change your certificate** (Modifica certificato) fare clic su **Choose file** (Scegli file) per caricare il certificato scaricato e quindi su **NEXT** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="30b3c-172">On the **Change your certificate** dialog page, click **Choose file** to upload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Impostazioni di Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  <span data-ttu-id="30b3c-174">Nella casella di testo per l'URL di autenticazione della finestra di dialogo **Modifica l'URL di autenticazione**, incollare il valore dell'**URL di SAML Single Sign-On Service** copiato dal portale di Azure e quindi fare clic su **NEXT** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="30b3c-174">In the authentication URL textbox on the **Change your authentication  URL** dialog page, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Impostazioni di Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. <span data-ttu-id="30b3c-176">Fare clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="30b3c-177">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="30b3c-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="30b3c-178">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="30b3c-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="30b3c-179">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="30b3c-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="30b3c-180">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="30b3c-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="30b3c-181">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="30b3c-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="30b3c-183">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="30b3c-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="30b3c-184">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="30b3c-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="30b3c-186">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="30b3c-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="30b3c-188">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="30b3c-190">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="30b3c-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="30b3c-192">a.</span><span class="sxs-lookup"><span data-stu-id="30b3c-192">a.</span></span> <span data-ttu-id="30b3c-193">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="30b3c-194">b.</span><span class="sxs-lookup"><span data-stu-id="30b3c-194">b.</span></span> <span data-ttu-id="30b3c-195">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="30b3c-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="30b3c-196">c.</span><span class="sxs-lookup"><span data-stu-id="30b3c-196">c.</span></span> <span data-ttu-id="30b3c-197">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="30b3c-198">d.</span><span class="sxs-lookup"><span data-stu-id="30b3c-198">d.</span></span> <span data-ttu-id="30b3c-199">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="30b3c-200">Creare un utente di test Mixpanel</span><span class="sxs-lookup"><span data-stu-id="30b3c-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="30b3c-201">Questa sezione descrive come creare un utente chiamato Britta Simon in Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="30b3c-201">The objective of this section is to create a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="30b3c-202">Accedere al sito aziendale di Mixpanel come amministratore.</span><span class="sxs-lookup"><span data-stu-id="30b3c-202">Sign on to your Mixpanel company site as an administrator.</span></span>

2. <span data-ttu-id="30b3c-203">Nella parte inferiore della pagina fare clic sul pulsante a forma di piccolo ingranaggio nell'angolo sinistro per aprire la finestra **Settings** .</span><span class="sxs-lookup"><span data-stu-id="30b3c-203">On the bottom of the page, click the little gear button on the left corner to open the **Settings** window.</span></span>

3. <span data-ttu-id="30b3c-204">Fare clic sulla scheda **Team** .</span><span class="sxs-lookup"><span data-stu-id="30b3c-204">Click the **Team** tab.</span></span>

4. <span data-ttu-id="30b3c-205">Nella casella di testo **team member** digitare l'indirizzo di posta elettronica di Britta disponibile in Azure.</span><span class="sxs-lookup"><span data-stu-id="30b3c-205">In the **team member** textbox, type Britta's email address in the Azure.</span></span>
   
    ![Impostazioni di Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. <span data-ttu-id="30b3c-207">Fare clic su **Invita**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="30b3c-208">L'utente riceverà un messaggio di posta elettronica per la configurazione del profilo.</span><span class="sxs-lookup"><span data-stu-id="30b3c-208">The user will get an email to set up the profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="30b3c-209">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="30b3c-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="30b3c-210">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="30b3c-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mixpanel.</span></span>

![Assegna utente][200] 

<span data-ttu-id="30b3c-212">**Per assegnare Britta Simon a Mixpanel, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="30b3c-212">**To assign Britta Simon to Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="30b3c-213">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="30b3c-215">Nell'elenco di applicazioni selezionare **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-215">In the applications list, select **Mixpanel**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. <span data-ttu-id="30b3c-217">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="30b3c-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="30b3c-219">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-219">Click **Add** button.</span></span> <span data-ttu-id="30b3c-220">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="30b3c-222">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="30b3c-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="30b3c-223">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="30b3c-224">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="30b3c-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="30b3c-225">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="30b3c-225">Testing single sign-on</span></span>

<span data-ttu-id="30b3c-226">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="30b3c-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="30b3c-227">Quando si fa clic sul riquadro Mixpanel nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="30b3c-227">When you click the Mixpanel tile in the Access Panel, you should get automatically signed-on to your Mixpanel application.</span></span>
<span data-ttu-id="30b3c-228">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="30b3c-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="30b3c-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="30b3c-229">Additional resources</span></span>

* [<span data-ttu-id="30b3c-230">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30b3c-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="30b3c-231">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30b3c-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

