---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP NetWeaver | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SAP NetWeaver.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: ad4140eb1183094a67822ad92eabcd35101360b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="07cd1-103">Esercitazione: Integrazione di Azure Active Directory con SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="07cd1-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>

<span data-ttu-id="07cd1-104">Questa esercitazione descrive come integrare SAP NetWeaver con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="07cd1-104">In this tutorial, you learn how to integrate SAP NetWeaver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07cd1-105">L'integrazione di SAP NetWeaver con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="07cd1-105">Integrating SAP NetWeaver with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="07cd1-106">È possibile controllare in Azure AD chi può accedere a SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="07cd1-106">You can control in Azure AD who has access to SAP NetWeaver</span></span>
- <span data-ttu-id="07cd1-107">È possibile abilitare gli utenti per l'accesso automatico a SAP NetWeaver (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="07cd1-107">You can enable your users to automatically get signed-on to SAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="07cd1-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="07cd1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="07cd1-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07cd1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="07cd1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="07cd1-110">Prerequisites</span></span>

<span data-ttu-id="07cd1-111">Per configurare l'integrazione di Azure AD con SAP NetWeaver, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="07cd1-111">To configure Azure AD integration with SAP NetWeaver, you need the following items:</span></span>

- <span data-ttu-id="07cd1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07cd1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="07cd1-113">Sottoscrizione di SAP NetWeaver abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="07cd1-113">An SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="07cd1-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="07cd1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="07cd1-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="07cd1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="07cd1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="07cd1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="07cd1-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07cd1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07cd1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="07cd1-118">Scenario description</span></span>
<span data-ttu-id="07cd1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="07cd1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07cd1-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="07cd1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07cd1-121">Aggiunta di SAP NetWeaver dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="07cd1-121">Adding SAP NetWeaver from the gallery</span></span>
2. <span data-ttu-id="07cd1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07cd1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-the-gallery"></a><span data-ttu-id="07cd1-123">Aggiunta di SAP NetWeaver dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="07cd1-123">Adding SAP NetWeaver from the gallery</span></span>
<span data-ttu-id="07cd1-124">Per configurare l'integrazione di SAP NetWeaver in Azure AD, è necessario aggiungere SAP NetWeaver dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="07cd1-124">To configure the integration of SAP NetWeaver into Azure AD, you need to add SAP NetWeaver from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="07cd1-125">**Per aggiungere SAP NetWeaver dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="07cd1-125">**To add SAP NetWeaver from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="07cd1-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="07cd1-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="07cd1-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="07cd1-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="07cd1-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="07cd1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="07cd1-133">Nella casella di ricerca digitare **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-133">In the search box, type **SAP NetWeaver**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_search.png)

5. <span data-ttu-id="07cd1-135">Nel pannello dei risultati selezionare **SAP NetWeaver** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07cd1-135">In the results panel, select **SAP NetWeaver**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="07cd1-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07cd1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="07cd1-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAP NetWeaver con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="07cd1-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="07cd1-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di SAP NetWeaver che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07cd1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP NetWeaver is to a user in Azure AD.</span></span> <span data-ttu-id="07cd1-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="07cd1-140">In other words, a link relationship between an Azure AD user and the related user in SAP NetWeaver needs to be established.</span></span>

<span data-ttu-id="07cd1-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="07cd1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="07cd1-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con SAP NetWeaver, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="07cd1-142">To configure and test Azure AD single sign-on with SAP NetWeaver, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="07cd1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="07cd1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="07cd1-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07cd1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07cd1-145">**[Creazione di un utente test di SAP NetWeaver](#creating-an-sap-netweaver-test-user)**: per avere una controparte di Britta Simon in SAP NetWeaver collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07cd1-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - to have a counterpart of Britta Simon in SAP NetWeaver that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="07cd1-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07cd1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07cd1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="07cd1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="07cd1-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07cd1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="07cd1-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale Azure e viene configurato l'accesso Single Sign-On nell'applicazione SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="07cd1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="07cd1-150">**Per configurare l'accesso Single Sign-On di Azure AD con SAP NetWeaver, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="07cd1-150">**To configure Azure AD single sign-on with SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="07cd1-151">Nella pagina di integrazione dell'applicazione **SAP NetWeaver** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-151">In the Azure portal, on the **SAP NetWeaver** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="07cd1-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="07cd1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_samlbase.png)

3. <span data-ttu-id="07cd1-155">Nella sezione **URL e dominio SAP NetWeaver** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="07cd1-155">On the **SAP NetWeaver Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_url.png)

    <span data-ttu-id="07cd1-157">a.</span><span class="sxs-lookup"><span data-stu-id="07cd1-157">a.</span></span> <span data-ttu-id="07cd1-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<your company instance of SAP NetWeaver>`.</span><span class="sxs-lookup"><span data-stu-id="07cd1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="07cd1-159">b.</span><span class="sxs-lookup"><span data-stu-id="07cd1-159">b.</span></span> <span data-ttu-id="07cd1-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="07cd1-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="07cd1-161">c.</span><span class="sxs-lookup"><span data-stu-id="07cd1-161">c.</span></span> <span data-ttu-id="07cd1-162">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span><span class="sxs-lookup"><span data-stu-id="07cd1-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="07cd1-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="07cd1-163">These values are not the real.</span></span> <span data-ttu-id="07cd1-164">è necessario aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="07cd1-164">Update these values with the actual Identifier and Reply URL and Sign-On URL.</span></span> <span data-ttu-id="07cd1-165">In questo caso è consigliabile usare in Identificatore il valore univoco della stringa.</span><span class="sxs-lookup"><span data-stu-id="07cd1-165">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="07cd1-166">Per ottenere questi valori, contattare il [team di supporto clienti di SAP NetWeaver](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="07cd1-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) to get these values.</span></span> 

4. <span data-ttu-id="07cd1-167">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="07cd1-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_certificate.png) 

5. <span data-ttu-id="07cd1-169">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="07cd1-169">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="07cd1-171">Nella sezione **Configurazione di SAP NetWeaver** fare clic su **Configura SAP NetWeaver** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-171">On the **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** to open **Configure sign-on** window.</span></span> <span data-ttu-id="07cd1-172">Copiare l'**ID di entità SAML** dalla **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="07cd1-172">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_configure.png) 

7. <span data-ttu-id="07cd1-174">Per configurare l'accesso Single Sign-On sul lato **SAP NetWeaver**, è necessario inviare il file **XML metadati** e l'**ID di entità SAML** al [team di supporto di SAP NetWeaver](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="07cd1-174">To configure single sign-on on **SAP NetWeaver** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [SAP NetWeaver support](https://www.sap.com/support.html).</span></span> 

> [!TIP]
> <span data-ttu-id="07cd1-175">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="07cd1-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="07cd1-176">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="07cd1-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="07cd1-177">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="07cd1-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="07cd1-178">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07cd1-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="07cd1-179">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="07cd1-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="07cd1-181">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="07cd1-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="07cd1-182">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="07cd1-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="07cd1-184">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="07cd1-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="07cd1-186">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="07cd1-188">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="07cd1-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="07cd1-190">a.</span><span class="sxs-lookup"><span data-stu-id="07cd1-190">a.</span></span> <span data-ttu-id="07cd1-191">Nella casella di testo **Name** (Nome) digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-191">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="07cd1-192">b.</span><span class="sxs-lookup"><span data-stu-id="07cd1-192">b.</span></span> <span data-ttu-id="07cd1-193">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07cd1-193">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="07cd1-194">c.</span><span class="sxs-lookup"><span data-stu-id="07cd1-194">c.</span></span> <span data-ttu-id="07cd1-195">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="07cd1-196">d.</span><span class="sxs-lookup"><span data-stu-id="07cd1-196">d.</span></span> <span data-ttu-id="07cd1-197">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-197">Click **Create**.</span></span>
 
### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="07cd1-198">Creazione di un utente test di SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="07cd1-198">Creating an SAP NetWeaver test user</span></span>

<span data-ttu-id="07cd1-199">In questa sezione viene creato un utente chiamato Britta Simon in SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="07cd1-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="07cd1-200">Collaborare con il [supporto di SAP NetWeaver](https://www.sap.com/support.html) per aggiungere gli utenti nella piattaforma SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="07cd1-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) to add the users in the SAP NetWeaver platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="07cd1-201">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07cd1-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="07cd1-202">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="07cd1-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP NetWeaver.</span></span>

![Assegna utente][200] 

<span data-ttu-id="07cd1-204">**Per assegnare Britta Simon a SAP NetWeaver, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="07cd1-204">**To assign Britta Simon to SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="07cd1-205">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="07cd1-207">Nell'elenco delle applicazioni selezionare **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-207">In the applications list, select **SAP NetWeaver**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_app.png) 

3. <span data-ttu-id="07cd1-209">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="07cd1-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="07cd1-211">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-211">Click **Add** button.</span></span> <span data-ttu-id="07cd1-212">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="07cd1-214">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="07cd1-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="07cd1-215">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07cd1-216">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="07cd1-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="07cd1-217">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="07cd1-217">Testing single sign-on</span></span>

<span data-ttu-id="07cd1-218">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="07cd1-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="07cd1-219">Quando si fa clic sul riquadro SAP NetWeaver nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="07cd1-219">When you click the SAP NetWeaver tile in the Access Panel, you should get automatically signed-on to your SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07cd1-220">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="07cd1-220">Additional resources</span></span>

* [<span data-ttu-id="07cd1-221">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07cd1-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07cd1-222">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07cd1-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_203.png

