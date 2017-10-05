---
title: 'Esercitazione: Integrazione di Azure Active Directory con OpsGenie | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e OpsGenie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: ce63726d2406d2f1415d29786f0ef92ca95b9b90
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="6f2b1-103">Esercitazione: Integrazione di Azure Active Directory con OpsGenie</span><span class="sxs-lookup"><span data-stu-id="6f2b1-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="6f2b1-104">Questa esercitazione descrive come integrare OpsGenie con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f2b1-104">In this tutorial, you learn how to integrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f2b1-105">L'integrazione di OpsGenie con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f2b1-105">Integrating OpsGenie with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6f2b1-106">È possibile controllare in Azure AD chi può accedere a OpsGenie</span><span class="sxs-lookup"><span data-stu-id="6f2b1-106">You can control in Azure AD who has access to OpsGenie</span></span>
- <span data-ttu-id="6f2b1-107">È possibile abilitare gli utenti per l'accesso automatico a OpsGenie (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f2b1-107">You can enable your users to automatically get signed-on to OpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6f2b1-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6f2b1-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f2b1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f2b1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6f2b1-110">Prerequisites</span></span>

<span data-ttu-id="6f2b1-111">Per configurare l'integrazione di Azure AD con OpsGenie, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f2b1-111">To configure Azure AD integration with OpsGenie, you need the following items:</span></span>

- <span data-ttu-id="6f2b1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6f2b1-113">Sottoscrizione di OpsGenie abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6f2b1-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f2b1-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6f2b1-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f2b1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6f2b1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f2b1-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f2b1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f2b1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6f2b1-118">Scenario description</span></span>
<span data-ttu-id="6f2b1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6f2b1-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f2b1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f2b1-121">Aggiunta di OpsGenie dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="6f2b1-121">Adding OpsGenie from the gallery</span></span>
2. <span data-ttu-id="6f2b1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f2b1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-the-gallery"></a><span data-ttu-id="6f2b1-123">Aggiunta di OpsGenie dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="6f2b1-123">Adding OpsGenie from the gallery</span></span>
<span data-ttu-id="6f2b1-124">Per configurare l'integrazione di OpsGenie in Azure AD, è necessario aggiungere OpsGenie dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-124">To configure the integration of OpsGenie into Azure AD, you need to add OpsGenie from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6f2b1-125">**Per aggiungere OpsGenie dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6f2b1-125">**To add OpsGenie from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6f2b1-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6f2b1-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6f2b1-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="6f2b1-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="6f2b1-133">Nella casella di ricerca digitare **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-133">In the search box, type **OpsGenie**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. <span data-ttu-id="6f2b1-135">Nel pannello dei risultati selezionare **OpsGenie** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-135">In the results panel, select **OpsGenie**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6f2b1-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f2b1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6f2b1-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con OpsGenie in base a un utente di prova di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6f2b1-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6f2b1-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di OpsGenie che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in OpsGenie is to a user in Azure AD.</span></span> <span data-ttu-id="6f2b1-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-140">In other words, a link relationship between an Azure AD user and the related user in OpsGenie needs to be established.</span></span>

<span data-ttu-id="6f2b1-141">Per stabilire la relazione di collegamento, in OpsGenie assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="6f2b1-141">In OpsGenie, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6f2b1-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con OpsGenie, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f2b1-142">To configure and test Azure AD single sign-on with OpsGenie, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6f2b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6f2b1-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f2b1-145">**[Creazione di un utente di test di OpsGenie](#creating-a-opsgenie-test-user)** : per avere una controparte di Britta Simon in OpsGenie collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - to have a counterpart of Britta Simon in OpsGenie that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6f2b1-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f2b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6f2b1-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f2b1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6f2b1-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="6f2b1-150">**Per configurare Single Sign-On di Azure AD con OpsGenie, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6f2b1-150">**To configure Azure AD single sign-on with OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="6f2b1-151">Nella pagina di integrazione dell'applicazione **OpsGenie** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-151">In the Azure portal, on the **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6f2b1-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. <span data-ttu-id="6f2b1-155">Nella sezione **URL e dominio OpsGenie** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6f2b1-155">On the **OpsGenie Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="6f2b1-157">Nella casella di testo **URL accesso** digitare l'URL: `https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="6f2b1-157">In the **Sign-on URL** textbox, type the URL: `https://app.opsgenie.com/auth/login`</span></span>

4. <span data-ttu-id="6f2b1-158">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. <span data-ttu-id="6f2b1-160">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6f2b1-160">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6f2b1-162">Nella sezione **Configurazione di OpsGenie** fare clic su **Configura OpsGenie** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-162">On the **OpsGenie Configuration** section, click **Configure OpsGenie** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6f2b1-163">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="6f2b1-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. <span data-ttu-id="6f2b1-165">Aprire un'altra istanza del browser e quindi accedere a OpsGenie come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-165">Open another browser instance, and then log-in to OpsGenie as an administrator.</span></span>

8. <span data-ttu-id="6f2b1-166">Fare clic su **Settings** e quindi selezionare la scheda **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-166">Click **Settings**, and then click the **Single Sign On** tab.</span></span>
   
    ![Accesso Single Sign-On di OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. <span data-ttu-id="6f2b1-168">Per abilitare l'accesso Single Sign-On, selezionare **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-168">To enable SSO, select **Enabled**.</span></span>
   
    ![Impostazioni di OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. <span data-ttu-id="6f2b1-170">Nella sezione **Provider** fare clic sulla scheda **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-170">In the **Provider** section, click the **Azure Active Directory** tab.</span></span>
   
    ![Impostazioni di OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. <span data-ttu-id="6f2b1-172">Nella pagina Azure Active Directory, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6f2b1-172">On the Azure Active Directory dialog page, perform the following steps:</span></span>
   
    ![Impostazioni di OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="6f2b1-174">a.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-174">a.</span></span> <span data-ttu-id="6f2b1-175">Incollare l'**URL del servizio Single Sign-On** copiato dal portale di Azure nella casella di testo **SAML 2.0 Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-175">Paste **Single Sign On Service URL**, which you have copied from the Azure portal into the **SAML 2.0 Endpoint** textbox.</span></span>
    
    <span data-ttu-id="6f2b1-176">b.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-176">b.</span></span> <span data-ttu-id="6f2b1-177">Aprire il certificato con codifica Base 64 scaricato nel Blocco note, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **X.500 Certificate** .</span><span class="sxs-lookup"><span data-stu-id="6f2b1-177">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **X.500 Certificate** textbox.</span></span>
    
    <span data-ttu-id="6f2b1-178">c.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-178">c.</span></span> <span data-ttu-id="6f2b1-179">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-179">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="6f2b1-180">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6f2b1-181">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6f2b1-182">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f2b1-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6f2b1-183">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f2b1-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="6f2b1-184">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="6f2b1-186">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f2b1-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6f2b1-187">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6f2b1-189">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6f2b1-191">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6f2b1-193">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6f2b1-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6f2b1-195">a.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-195">a.</span></span> <span data-ttu-id="6f2b1-196">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6f2b1-197">b.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-197">b.</span></span> <span data-ttu-id="6f2b1-198">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6f2b1-199">c.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-199">c.</span></span> <span data-ttu-id="6f2b1-200">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6f2b1-201">d.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-201">d.</span></span> <span data-ttu-id="6f2b1-202">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-202">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="6f2b1-203">Creazione di un utente di test di OpsGenie</span><span class="sxs-lookup"><span data-stu-id="6f2b1-203">Creating a OpsGenie test user</span></span>

<span data-ttu-id="6f2b1-204">Questa sezione descrive come creare un utente chiamato Britta Simon in OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-204">The objective of this section is to create a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="6f2b1-205">In una finestra del Web browser accedere al tenant di OpsGenie come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-205">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

2. <span data-ttu-id="6f2b1-206">Passare all'elenco di utenti facendo clic su **User** nel pannello a sinistra.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-206">Navigate to Users list by clicking **User** in left panel.</span></span>
   
   ![Impostazioni di OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. <span data-ttu-id="6f2b1-208">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-208">Click **Add User**.</span></span>

4. <span data-ttu-id="6f2b1-209">Nella finestra di dialogo **Aggiungi utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6f2b1-209">On the **Add User** dialog, perform the following steps:</span></span>
   
   ![Impostazioni di OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="6f2b1-211">a.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-211">a.</span></span> <span data-ttu-id="6f2b1-212">Nella casella di testo **Email** , digitare l'indirizzo di posta elettronica di Britta in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-212">In the **Email** textbox, type the email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="6f2b1-213">b.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-213">b.</span></span> <span data-ttu-id="6f2b1-214">Nella casella di testo **Nome completo** digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-214">In the **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="6f2b1-215">c.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-215">c.</span></span> <span data-ttu-id="6f2b1-216">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-216">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="6f2b1-217">Britta riceve un messaggio di posta elettronica con istruzioni per la configurazione del profilo.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-217">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6f2b1-218">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f2b1-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6f2b1-219">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OpsGenie.</span></span>

![Assegna utente][200] 

<span data-ttu-id="6f2b1-221">**Per assegnare Britta Simon a OpsGenie, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6f2b1-221">**To assign Britta Simon to OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="6f2b1-222">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6f2b1-224">Nell'elenco di applicazioni selezionare **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-224">In the applications list, select **OpsGenie**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. <span data-ttu-id="6f2b1-226">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="6f2b1-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-228">Click **Add** button.</span></span> <span data-ttu-id="6f2b1-229">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="6f2b1-231">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6f2b1-232">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6f2b1-233">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6f2b1-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6f2b1-234">Testing single sign-on</span></span>

<span data-ttu-id="6f2b1-235">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-235">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="6f2b1-236">Quando si fa clic sul riquadro OpsGenie nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="6f2b1-236">When you click the OpsGenie tile in the Access Panel, you should get automatically signed-on to your OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6f2b1-237">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6f2b1-237">Additional resources</span></span>

* [<span data-ttu-id="6f2b1-238">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f2b1-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f2b1-239">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f2b1-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

