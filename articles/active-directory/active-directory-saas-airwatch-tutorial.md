---
title: 'Esercitazione: Integrazione di Azure Active Directory con AirWatch | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory ed AirWatch.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1996ec97e7c0d94c5606ca43bb5956548f1f3712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="b43b1-103">Esercitazione: Integrazione di Azure Active Directory con AirWatch</span><span class="sxs-lookup"><span data-stu-id="b43b1-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="b43b1-104">Questa esercitazione descrive come integrare AirWatch con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b43b1-104">In this tutorial, you learn how to integrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b43b1-105">L'integrazione di AirWatch con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b43b1-105">Integrating AirWatch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b43b1-106">È possibile controllare in Azure AD chi può accedere a AirWatch</span><span class="sxs-lookup"><span data-stu-id="b43b1-106">You can control in Azure AD who has access to AirWatch</span></span>
- <span data-ttu-id="b43b1-107">È possibile abilitare gli utenti per l'accesso automatico a AirWatch (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="b43b1-107">You can enable your users to automatically get signed-on to AirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b43b1-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b43b1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b43b1-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b43b1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b43b1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b43b1-110">Prerequisites</span></span>

<span data-ttu-id="b43b1-111">Per configurare l'integrazione di Azure AD con AirWatch, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b43b1-111">To configure Azure AD integration with AirWatch, you need the following items:</span></span>

- <span data-ttu-id="b43b1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b43b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b43b1-113">Sottoscrizione di AirWatch abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b43b1-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b43b1-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b43b1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b43b1-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b43b1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b43b1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b43b1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b43b1-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b43b1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b43b1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b43b1-118">Scenario description</span></span>
<span data-ttu-id="b43b1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b43b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b43b1-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b43b1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b43b1-121">Aggiunta di AirWatch dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b43b1-121">Adding AirWatch from the gallery</span></span>
2. <span data-ttu-id="b43b1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b43b1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-the-gallery"></a><span data-ttu-id="b43b1-123">Aggiunta di AirWatch dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b43b1-123">Adding AirWatch from the gallery</span></span>
<span data-ttu-id="b43b1-124">Per configurare l'integrazione di AirWatch in Azure AD, è necessario aggiungere AirWatch dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b43b1-124">To configure the integration of AirWatch into Azure AD, you need to add AirWatch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b43b1-125">**Per aggiungere AirWatch dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b43b1-125">**To add AirWatch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b43b1-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b43b1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b43b1-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b43b1-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b43b1-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="b43b1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b43b1-133">Nella casella di ricerca digitare **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-133">In the search box, type **AirWatch**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="b43b1-135">Nel pannello dei risultati selezionare **AirWatch** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b43b1-135">In the results panel, select **AirWatch**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b43b1-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b43b1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b43b1-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con AirWatch con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b43b1-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b43b1-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di AirWatch che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b43b1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AirWatch is to a user in Azure AD.</span></span> <span data-ttu-id="b43b1-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in AirWatch.</span><span class="sxs-lookup"><span data-stu-id="b43b1-140">In other words, a link relationship between an Azure AD user and the related user in AirWatch needs to be established.</span></span>

<span data-ttu-id="b43b1-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in AirWatch.</span><span class="sxs-lookup"><span data-stu-id="b43b1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in AirWatch.</span></span>

<span data-ttu-id="b43b1-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con AirWatch, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b43b1-142">To configure and test Azure AD single sign-on with AirWatch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b43b1-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b43b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b43b1-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b43b1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b43b1-145">**[Creazione di un utente di test di AirWatch](#creating-a-airwatch-test-user)**: per avere una controparte di Britta Simon in AirWatch collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b43b1-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - to have a counterpart of Britta Simon in AirWatch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b43b1-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b43b1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b43b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="b43b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b43b1-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b43b1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b43b1-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione AirWatch.</span><span class="sxs-lookup"><span data-stu-id="b43b1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="b43b1-150">**Per configurare l'accesso Single Sign-On di Azure AD con AirWatch, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b43b1-150">**To configure Azure AD single sign-on with AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="b43b1-151">Nella pagina di integrazione dell'applicazione **AirWatch** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-151">In the Azure portal, on the **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b43b1-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b43b1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="b43b1-155">Nella sezione **URL e dominio AirWatch** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b43b1-155">On the **AirWatch Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="b43b1-157">a.</span><span class="sxs-lookup"><span data-stu-id="b43b1-157">a.</span></span> <span data-ttu-id="b43b1-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`.</span><span class="sxs-lookup"><span data-stu-id="b43b1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="b43b1-159">b.</span><span class="sxs-lookup"><span data-stu-id="b43b1-159">b.</span></span> <span data-ttu-id="b43b1-160">Nella casella di testo **Identificatore** digitare il valore `AirWatch`.</span><span class="sxs-lookup"><span data-stu-id="b43b1-160">In the **Identifier** textbox, type the value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b43b1-161">Poiché non è il valore reale,</span><span class="sxs-lookup"><span data-stu-id="b43b1-161">This value is not the real.</span></span> <span data-ttu-id="b43b1-162">aggiornarlo con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="b43b1-162">Update this value with the actual Sign-on URL.</span></span> <span data-ttu-id="b43b1-163">Per ottenere tale valore, contattare il [team di supporto clienti di AirWatch](http://www.air-watch.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="b43b1-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) to get this value.</span></span> 
 
4. <span data-ttu-id="b43b1-164">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="b43b1-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="b43b1-166">Nella sezione **Configurazione di AirWatch** fare clic su **Configura AirWatch** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-166">On the **AirWatch Configuration** section, click **Configure AirWatch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b43b1-167">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="b43b1-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="b43b1-169">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b43b1-169">Click **Save** button.</span></span>

    <span data-ttu-id="b43b1-170">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="b43b1-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="b43b1-171">In un'altra finestra del Web browser accedere al sito aziendale di AirWatch come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b43b1-171">In a different web browser window, log in to your AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="b43b1-172">Nel riquadro di spostamento sinistro fare clic su **Accounts** e quindi su **Administrators**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-172">In the left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="b43b1-173">![Amministratori](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Amministratori")</span><span class="sxs-lookup"><span data-stu-id="b43b1-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="b43b1-174">Espandere il menu **Settings** e quindi fare clic su **Directory Services**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-174">Expand the **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="b43b1-175">![Impostazioni](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="b43b1-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="b43b1-176">Fare clic sulla scheda **User** (Utente), digitare il proprio nome di dominio nella casella di testo **Base DN** (Nome distinto di base) e quindi fare clic su **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="b43b1-176">Click the **User** tab, in the **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="b43b1-177">![Utente](./media/active-directory-saas-airwatch-tutorial/ic791922.png "Utente")</span><span class="sxs-lookup"><span data-stu-id="b43b1-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="b43b1-178">Fare clic sulla scheda **Server** .</span><span class="sxs-lookup"><span data-stu-id="b43b1-178">Click the **Server** tab.</span></span>
   
   <span data-ttu-id="b43b1-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span><span class="sxs-lookup"><span data-stu-id="b43b1-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="b43b1-180">Eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b43b1-180">Perform the following steps:</span></span>
    
    <span data-ttu-id="b43b1-181">![Caricamento](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Caricamento")</span><span class="sxs-lookup"><span data-stu-id="b43b1-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="b43b1-182">a.</span><span class="sxs-lookup"><span data-stu-id="b43b1-182">a.</span></span> <span data-ttu-id="b43b1-183">Per **Directory Type** selezionare **None**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="b43b1-184">b.</span><span class="sxs-lookup"><span data-stu-id="b43b1-184">b.</span></span> <span data-ttu-id="b43b1-185">Selezionare **Use SAML For Authentication**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="b43b1-186">c.</span><span class="sxs-lookup"><span data-stu-id="b43b1-186">c.</span></span> <span data-ttu-id="b43b1-187">Per caricare il certificato scaricato, fare clic su **Upload**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-187">To upload the downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="b43b1-188">Nella sezione **Request** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b43b1-188">In the **Request** section, perform the following steps:</span></span>
    
    <span data-ttu-id="b43b1-189">![Richiesta](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Richiesta")</span><span class="sxs-lookup"><span data-stu-id="b43b1-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="b43b1-190">a.</span><span class="sxs-lookup"><span data-stu-id="b43b1-190">a.</span></span> <span data-ttu-id="b43b1-191">Per **Request Binding Type** selezionare **POST**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="b43b1-192">b.</span><span class="sxs-lookup"><span data-stu-id="b43b1-192">b.</span></span> <span data-ttu-id="b43b1-193">Nella finestra di dialogo **Configura accesso Single Sign-On in Airwatch** del portale di Azure copiare il valore di **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) e quindi incollarlo nella casella di testo **Identity Provider Single Sign On URL** (URL di accesso Single Sign-On del provider di identità).</span><span class="sxs-lookup"><span data-stu-id="b43b1-193">In the Azure portal, on the **Configure single sign-on at Airwatch** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="b43b1-194">c.</span><span class="sxs-lookup"><span data-stu-id="b43b1-194">c.</span></span> <span data-ttu-id="b43b1-195">Per **NameID format** selezionare **Email address**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="b43b1-196">d.</span><span class="sxs-lookup"><span data-stu-id="b43b1-196">d.</span></span> <span data-ttu-id="b43b1-197">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-197">Click **Save**.</span></span>

14. <span data-ttu-id="b43b1-198">Fare di nuovo clic sulla scheda **User** .</span><span class="sxs-lookup"><span data-stu-id="b43b1-198">Click the **User** tab again.</span></span>
    
    <span data-ttu-id="b43b1-199">![Utente](./media/active-directory-saas-airwatch-tutorial/ic791926.png "Utente")</span><span class="sxs-lookup"><span data-stu-id="b43b1-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="b43b1-200">Nella sezione **Attribute** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b43b1-200">In the **Attribute** section, perform the following steps:</span></span>
    
    <span data-ttu-id="b43b1-201">![Attributo](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attributo")</span><span class="sxs-lookup"><span data-stu-id="b43b1-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="b43b1-202">a.</span><span class="sxs-lookup"><span data-stu-id="b43b1-202">a.</span></span> <span data-ttu-id="b43b1-203">Nella casella di testo **Object Identifier** digitare **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-203">In the **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="b43b1-204">b.</span><span class="sxs-lookup"><span data-stu-id="b43b1-204">b.</span></span> <span data-ttu-id="b43b1-205">Nella casella di testo **Username** digitare **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-205">In the **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="b43b1-206">c.</span><span class="sxs-lookup"><span data-stu-id="b43b1-206">c.</span></span> <span data-ttu-id="b43b1-207">Nella casella di testo **Display Name** digitare **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-207">In the **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="b43b1-208">d.</span><span class="sxs-lookup"><span data-stu-id="b43b1-208">d.</span></span> <span data-ttu-id="b43b1-209">Nella casella di testo **First Name** digitare **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-209">In the **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="b43b1-210">e.</span><span class="sxs-lookup"><span data-stu-id="b43b1-210">e.</span></span> <span data-ttu-id="b43b1-211">Nella casella di testo **Last Name** digitare **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-211">In the **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="b43b1-212">f.</span><span class="sxs-lookup"><span data-stu-id="b43b1-212">f.</span></span> <span data-ttu-id="b43b1-213">Nella casella di testo **Email** digitare **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-213">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="b43b1-214">g.</span><span class="sxs-lookup"><span data-stu-id="b43b1-214">g.</span></span> <span data-ttu-id="b43b1-215">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b43b1-216">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b43b1-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="b43b1-217">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b43b1-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b43b1-219">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b43b1-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b43b1-220">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b43b1-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b43b1-222">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="b43b1-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b43b1-224">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b43b1-226">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b43b1-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b43b1-228">a.</span><span class="sxs-lookup"><span data-stu-id="b43b1-228">a.</span></span> <span data-ttu-id="b43b1-229">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b43b1-230">b.</span><span class="sxs-lookup"><span data-stu-id="b43b1-230">b.</span></span> <span data-ttu-id="b43b1-231">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b43b1-231">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="b43b1-232">c.</span><span class="sxs-lookup"><span data-stu-id="b43b1-232">c.</span></span> <span data-ttu-id="b43b1-233">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b43b1-234">d.</span><span class="sxs-lookup"><span data-stu-id="b43b1-234">d.</span></span> <span data-ttu-id="b43b1-235">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="b43b1-236">Creazione di un utente di test di AirWatch</span><span class="sxs-lookup"><span data-stu-id="b43b1-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="b43b1-237">Per consentire agli utenti di Azure AD di accedere a AirWatch, è necessario effettuarne il provisioning in AirWatch.</span><span class="sxs-lookup"><span data-stu-id="b43b1-237">To enable Azure AD users to log in to AirWatch, they must be provisioned in to AirWatch.</span></span>

* <span data-ttu-id="b43b1-238">Nel caso di AirWatch, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="b43b1-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="b43b1-239">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b43b1-239">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b43b1-240">Accedere al sito aziendale di **AirWatch** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b43b1-240">Log in to your **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="b43b1-241">Nel riquadro di spostamento a sinistra fare clic su **Accounts** e quindi su **Users**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-241">In the navigation pane on the left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="b43b1-242">![Utenti](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="b43b1-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="b43b1-243">Dal menu **Users** scegliere **List View** e quindi fare clic su **Add \> Add User**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-243">In the **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="b43b1-244">![Aggiungere un utente](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="b43b1-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="b43b1-245">Nella finestra di dialogo **Add / Edit User** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b43b1-245">On the **Add / Edit User** dialog, perform the following steps:</span></span>

   <span data-ttu-id="b43b1-246">![Aggiungere un utente](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="b43b1-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="b43b1-247">Nelle caselle di testo **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name** e **Email Address** digitare il nome utente, la password, la conferma password, il nome e il cognome di un account Azure Active Directory valido di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="b43b1-247">Type the **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="b43b1-248">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="b43b1-249">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da AirWatch per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b43b1-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b43b1-250">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b43b1-250">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b43b1-251">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a AirWatch.</span><span class="sxs-lookup"><span data-stu-id="b43b1-251">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AirWatch.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b43b1-253">**Per assegnare Britta Simon a AirWatch, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b43b1-253">**To assign Britta Simon to AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="b43b1-254">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-254">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b43b1-256">Nell'elenco delle applicazioni selezionare **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-256">In the applications list, select **AirWatch**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="b43b1-258">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b43b1-258">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b43b1-260">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-260">Click **Add** button.</span></span> <span data-ttu-id="b43b1-261">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b43b1-263">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="b43b1-263">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b43b1-264">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b43b1-265">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b43b1-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b43b1-266">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b43b1-266">Testing single sign-on</span></span>

<span data-ttu-id="b43b1-267">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b43b1-267">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b43b1-268">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b43b1-268">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="b43b1-269">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b43b1-269">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b43b1-270">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b43b1-270">Additional resources</span></span>

* [<span data-ttu-id="b43b1-271">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b43b1-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b43b1-272">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b43b1-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

