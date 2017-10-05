---
title: 'Esercitazione: Integrazione di Azure Active Directory con Work.com | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Work.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 7cfec8e9ac12d43095483696a15c0580776d3114
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="b9bf5-103">Esercitazione: Integrazione di Azure Active Directory con Work.com</span><span class="sxs-lookup"><span data-stu-id="b9bf5-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="b9bf5-104">Questa esercitazione descrive come integrare Work.com con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-104">In this tutorial, you learn how to integrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9bf5-105">L'integrazione di Work.com con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9bf5-105">Integrating Work.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b9bf5-106">È possibile controllare in Azure AD chi può accedere a Work.com</span><span class="sxs-lookup"><span data-stu-id="b9bf5-106">You can control in Azure AD who has access to Work.com</span></span>
- <span data-ttu-id="b9bf5-107">È possibile abilitare gli utenti per l'accesso automatico a Work.com (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="b9bf5-107">You can enable your users to automatically get signed-on to Work.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9bf5-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b9bf5-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9bf5-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b9bf5-110">Prerequisites</span></span>

<span data-ttu-id="b9bf5-111">Per configurare l'integrazione di Azure AD con Work.com, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9bf5-111">To configure Azure AD integration with Work.com, you need the following items:</span></span>

- <span data-ttu-id="b9bf5-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9bf5-113">Sottoscrizione di Work.com abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b9bf5-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9bf5-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9bf5-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9bf5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9bf5-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9bf5-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9bf5-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b9bf5-118">Scenario description</span></span>
<span data-ttu-id="b9bf5-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9bf5-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9bf5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9bf5-121">Aggiungere Work.com dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b9bf5-121">Add Work.com from the gallery</span></span>
2. <span data-ttu-id="b9bf5-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9bf5-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-the-gallery"></a><span data-ttu-id="b9bf5-123">Aggiungere Work.com dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b9bf5-123">Add Work.com from the gallery</span></span>
<span data-ttu-id="b9bf5-124">Per configurare l'integrazione di Work.com in Azure AD, è necessario aggiungere Work.com dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-124">To configure the integration of Work.com into Azure AD, you need to add Work.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b9bf5-125">**Per aggiungere Work.com dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b9bf5-125">**To add Work.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b9bf5-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b9bf5-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b9bf5-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b9bf5-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b9bf5-133">Nella casella di ricerca digitare **Work.com**, selezionare **Work.com** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-133">In the search box, type **Work.com**, select **Work.com** from results panel then click **Add** button to add the application.</span></span>

    ![Aggiungere dalla raccolta](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b9bf5-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9bf5-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b9bf5-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Work.com usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b9bf5-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9bf5-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Work.com corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Work.com is to a user in Azure AD.</span></span> <span data-ttu-id="b9bf5-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Work.com.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-138">In other words, a link relationship between an Azure AD user and the related user in Work.com needs to be established.</span></span>

<span data-ttu-id="b9bf5-139">Per stabilire la relazione di collegamento, in Work.com assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-139">In Work.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b9bf5-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Work.com, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9bf5-140">To configure and test Azure AD single sign-on with Work.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b9bf5-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b9bf5-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9bf5-143">**[Creare un utente di test di Work.com](#create-a-workcom-test-user)**: per avere una controparte di Britta Simon in Work.com collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - to have a counterpart of Britta Simon in Work.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9bf5-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9bf5-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b9bf5-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9bf5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b9bf5-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Work.com.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="b9bf5-148">Per configurare l'accesso Single Sign-On, è necessario configurare un nome di dominio personalizzato Work.com.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-148">To configure single sign-on, you need to setup a custom Work.com domain name yet.</span></span> <span data-ttu-id="b9bf5-149">È necessario definire almeno un nome di dominio, testare il nome di dominio e distribuirlo in tutta l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-149">You need to define at least a domain name, test your domain name, and deploy it to your entire organization.</span></span>

<span data-ttu-id="b9bf5-150">**Per configurare l'accesso Single Sign-On di Azure AD con Work.com, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b9bf5-150">**To configure Azure AD single sign-on with Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="b9bf5-151">Nella pagina di integrazione dell'applicazione **Work.com** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-151">In the Azure portal, on the **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b9bf5-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Accesso basato su SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="b9bf5-155">Nella sezione **URL e dominio Work.com** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b9bf5-155">On the **Work.com Domain and URLs** section, perform the following:</span></span>

    ![Sezione URL e dominio Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="b9bf5-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `http://<companyname>.my.salesforce.com`.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9bf5-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="b9bf5-158">This value is not real.</span></span> <span data-ttu-id="b9bf5-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b9bf5-160">Per ottenere questo valore, contattare il [team di supporto clienti di Work.com](https://help.salesforce.com/articleView?id=000159855&type=3).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) to get this value.</span></span> 

4. <span data-ttu-id="b9bf5-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Sezione Certificato di firma SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="b9bf5-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b9bf5-163">Click **Save** button.</span></span>

    ![Pulsante per il salvataggio](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9bf5-165">Nella sezione **Configurazione di Work.com** fare clic su **Configura Work.com** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-165">On the **Work.com Configuration** section, click **Configure Work.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b9bf5-166">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="b9bf5-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Sezione Configurazione di Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="b9bf5-168">Accedere al tenant di Work.com come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-168">Log in to your Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="b9bf5-169">Passare a **Setup**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-169">Go to **Setup**.</span></span>
   
    <span data-ttu-id="b9bf5-170">![Installazione](./media/active-directory-saas-work-com-tutorial/ic794108.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="b9bf5-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="b9bf5-171">Nella sezione **Administer** (Amministra) del riquadro di spostamento sinistro fare clic su **Domain Management** (Gestione dominio) per espandere la sezione correlata e quindi fare clic su **My Domain** (Dominio personale) per aprire la pagina **My Domain** (Dominio personale).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
    <span data-ttu-id="b9bf5-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="b9bf5-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="b9bf5-173">Per verificare che il dominio sia stato configurato correttamente, verificare che sia presente in "**Step 4 Deployed to Users**" (Passaggio 4 Distribuzione agli utenti) e quindi verificare le selezioni in "**My Domain Settings**" (Impostazioni dominio personale).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="b9bf5-174">![Dominio distribuito all'utente](./media/active-directory-saas-work-com-tutorial/ic784377.png "Dominio distribuito all'utente")</span><span class="sxs-lookup"><span data-stu-id="b9bf5-174">![Domain Deployed to User](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="b9bf5-175">Accedere al tenant di Work.com.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-175">Log in to your Work.com tenant.</span></span>

12. <span data-ttu-id="b9bf5-176">Passare a **Setup**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-176">Go to **Setup**.</span></span>
    
    <span data-ttu-id="b9bf5-177">![Installazione](./media/active-directory-saas-work-com-tutorial/ic794108.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="b9bf5-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="b9bf5-178">Espandere il menu **Security Controls** (Controlli di sicurezza) e quindi fare clic su **Single Sign-On Settings** (Impostazioni Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-178">Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="b9bf5-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="b9bf5-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="b9bf5-180">Nella finestra di dialogo **Single Sign-On Settings** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b9bf5-180">On the **Single Sign-On Settings** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="b9bf5-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span><span class="sxs-lookup"><span data-stu-id="b9bf5-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="b9bf5-182">a.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-182">a.</span></span> <span data-ttu-id="b9bf5-183">Selezionare **Abilitato SAML**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="b9bf5-184">b.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-184">b.</span></span> <span data-ttu-id="b9bf5-185">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-185">Click **New**.</span></span>

15. <span data-ttu-id="b9bf5-186">Nella sezione **SAML Single Sign-On Setting** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b9bf5-186">In the **SAML Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="b9bf5-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span><span class="sxs-lookup"><span data-stu-id="b9bf5-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="b9bf5-188">a.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-188">a.</span></span> <span data-ttu-id="b9bf5-189">Nella casella di testo **Name** digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-189">In the **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="b9bf5-190">Se si specifica un valore per **Name** (Nome) verrà popolata automaticamente la casella di testo **API Name** (Nome API).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-190">Providing a value for **Name** does automatically populate the **API Name** textbox.</span></span>
    
    <span data-ttu-id="b9bf5-191">b.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-191">b.</span></span> <span data-ttu-id="b9bf5-192">Nella casella di testo **Issuer** (Autorità emittente) incollare il valore dell'**ID entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-192">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="b9bf5-193">c.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-193">c.</span></span> <span data-ttu-id="b9bf5-194">Per caricare il certificato scaricato dal portale di Azure, fare clic su **Browse** (Sfoglia).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-194">To upload the downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="b9bf5-195">d.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-195">d.</span></span> <span data-ttu-id="b9bf5-196">Nella casella di testo **Entity Id** (ID entità) digitare `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-196">In the **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="b9bf5-197">e.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-197">e.</span></span> <span data-ttu-id="b9bf5-198">In **SAML Identity Type** (Tipo di identità SAML) selezionare **Assertion contains the Federation ID from the User object** (L'asserzione contiene l'ID federazione dell'oggetto utente).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-198">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
    
    <span data-ttu-id="b9bf5-199">f.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-199">f.</span></span> <span data-ttu-id="b9bf5-200">In **SAML Identity Location** (Percorso identità SAML) selezionare **Identity is in the NameIdentfier element of the Subject statement** (L'identità è nell'elemento NameIdentfier dell'istruzione Subject).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-200">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>
    
    <span data-ttu-id="b9bf5-201">g.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-201">g.</span></span> <span data-ttu-id="b9bf5-202">Nella casella di testo **Identity Provider Login URL** (URL di accesso provider di identità) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-202">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b9bf5-203">h.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-203">h.</span></span> <span data-ttu-id="b9bf5-204">Nella casella di testo **Identity Provider Logout URL** (URL di disconnessione provider di identità) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-204">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="b9bf5-205">i.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-205">i.</span></span> <span data-ttu-id="b9bf5-206">In **Service Provider Initiated Request Binding** (Binding richiesta avviato dal provider di servizi) selezionare **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="b9bf5-207">j.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-207">j.</span></span> <span data-ttu-id="b9bf5-208">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-208">Click **Save**.</span></span>

16. <span data-ttu-id="b9bf5-209">Nel pannello di navigazione a sinistra del portale di Work.com classico fare clic su **Domain Management** (Gestione dominio) per espandere la sezione correlata e quindi fare clic su **My Domain** (Dominio personale) per aprire la pagina **My Domain** (Dominio personale).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-209">In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="b9bf5-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="b9bf5-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="b9bf5-211">Nella sezione **Login Page Branding** (Personalizzazione pagina di accesso) della pagina **My Domain** (Dominio personale) fare clic su **Edit** (Modifica).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-211">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="b9bf5-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="b9bf5-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="b9bf5-213">Nella sezione**Authentication Service** (Servizio autenticazione) della pagina **Login Page Branding** (Personalizzazione pagina di accesso) viene visualizzato il nome delle **impostazioni SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-213">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="b9bf5-214">Selezionarlo e quindi fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="b9bf5-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="b9bf5-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="b9bf5-216">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b9bf5-217">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b9bf5-218">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b9bf5-219">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9bf5-219">Create an Azure AD test user</span></span>
<span data-ttu-id="b9bf5-220">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b9bf5-222">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b9bf5-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b9bf5-223">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b9bf5-225">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Utenti e gruppi -> Tutti gli utenti](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b9bf5-227">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Add](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9bf5-229">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b9bf5-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b9bf5-231">a.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-231">a.</span></span> <span data-ttu-id="b9bf5-232">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9bf5-233">b.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-233">b.</span></span> <span data-ttu-id="b9bf5-234">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9bf5-235">c.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-235">c.</span></span> <span data-ttu-id="b9bf5-236">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b9bf5-237">d.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-237">d.</span></span> <span data-ttu-id="b9bf5-238">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="b9bf5-239">Creare un utente di test di Work.com</span><span class="sxs-lookup"><span data-stu-id="b9bf5-239">Create a Work.com test user</span></span>
<span data-ttu-id="b9bf5-240">Per consentire l'accesso agli utenti di Azure Active Directory, è necessario che eseguano il provisioning a Work.com.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-240">For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.</span></span> <span data-ttu-id="b9bf5-241">Nel caso di Work.com, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-241">In the case of Work.com, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="b9bf5-242">Per configurare il provisioning utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b9bf5-242">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="b9bf5-243">Accedere al sito aziendale di Work.com come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-243">Sign on to your Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="b9bf5-244">Passare a **Setup**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-244">Go to **Setup**.</span></span>
   
    <span data-ttu-id="b9bf5-245">![Installazione](./media/active-directory-saas-work-com-tutorial/IC794108.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="b9bf5-245">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="b9bf5-246">Passare a **Manage Users (Gestisci utenti) \> Users (Utenti)**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-246">Go to **Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="b9bf5-247">![Gestione utenti](./media/active-directory-saas-work-com-tutorial/IC784369.png "Gestione utenti")</span><span class="sxs-lookup"><span data-stu-id="b9bf5-247">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="b9bf5-248">Fare clic su **Nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-248">Click **New User**.</span></span>
   
    <span data-ttu-id="b9bf5-249">![Tutti gli utenti](./media/active-directory-saas-work-com-tutorial/IC794117.png "Tutti gli utenti")</span><span class="sxs-lookup"><span data-stu-id="b9bf5-249">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="b9bf5-250">Nella sezione relativa alle modifiche utente eseguire i passaggi seguenti inserendo nelle caselle di testo correlate gli attributi di un account Azure AD valido di cui si vuole effettuare il provisioning:</span><span class="sxs-lookup"><span data-stu-id="b9bf5-250">In the User Edit section, perform the following steps, in attributes of a valid Azure AD account you want to provision into the related textboxes:</span></span>
   
    <span data-ttu-id="b9bf5-251">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span><span class="sxs-lookup"><span data-stu-id="b9bf5-251">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="b9bf5-252">a.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-252">a.</span></span> <span data-ttu-id="b9bf5-253">Nella casella di testo **First Name** (Nome) digitare il **nome** dell'utente **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-253">In the **First Name** textbox, type the **first name** of the user **Britta**.</span></span>
    
    <span data-ttu-id="b9bf5-254">b.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-254">b.</span></span> <span data-ttu-id="b9bf5-255">Nella casella di testo **Last Name** (Cognome) digitare il **cognome** dell'utente **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-255">In the **Last Name** textbox, type the **last name** of the user **Simon**.</span></span>
    
    <span data-ttu-id="b9bf5-256">c.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-256">c.</span></span> <span data-ttu-id="b9bf5-257">Nella casella di testo **Alias** digitare il **nome** dell'utente **BrittaS**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-257">In the **Alias** textbox, type the **name** of the user **BrittaS**.</span></span>
    
    <span data-ttu-id="b9bf5-258">d.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-258">d.</span></span> <span data-ttu-id="b9bf5-259">Nella casella di testo **Email** (Posta elettronica) digitare l'**indirizzo e-mail** dell'utente **Brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-259">In the **Email** textbox, type the **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="b9bf5-260">e.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-260">e.</span></span> <span data-ttu-id="b9bf5-261">Nella casella di testo **User Name** (Nome utente) digitare un nome utente, ad esempio **Brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-261">In the **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="b9bf5-262">f.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-262">f.</span></span> <span data-ttu-id="b9bf5-263">Nella casella di testo **Nick Name** (Nome alternativo) digitare un **nome alternativo** dell'utente **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-263">In the **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="b9bf5-264">g.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-264">g.</span></span> <span data-ttu-id="b9bf5-265">Selezionare **Role** (Ruolo), **User License**(Licenza utente) e **Profile** (Profilo).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-265">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="b9bf5-266">h.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-266">h.</span></span> <span data-ttu-id="b9bf5-267">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-267">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="b9bf5-268">Il titolare dell'account Azure AD riceverà un messaggio di posta elettronica con un collegamento per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-268">The Azure AD account holder will get an email including a link to confirm the account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b9bf5-269">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9bf5-269">Assign the Azure AD test user</span></span>

<span data-ttu-id="b9bf5-270">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Work.com.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-270">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Work.com.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b9bf5-272">**Per assegnare Britta Simon a Work.com, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b9bf5-272">**To assign Britta Simon to Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="b9bf5-273">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-273">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b9bf5-275">Nell'elenco delle applicazioni selezionare **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-275">In the applications list, select **Work.com**.</span></span>

    ![Work.com nell'elenco delle app](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="b9bf5-277">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-277">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b9bf5-279">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-279">Click **Add** button.</span></span> <span data-ttu-id="b9bf5-280">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-280">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b9bf5-282">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-282">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b9bf5-283">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-283">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9bf5-284">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-284">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b9bf5-285">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b9bf5-285">Test single sign-on</span></span>

<span data-ttu-id="b9bf5-286">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-286">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b9bf5-287">Quando si fa clic sul riquadro Work.com nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Work.com.</span><span class="sxs-lookup"><span data-stu-id="b9bf5-287">When you click the Work.com tile in the Access Panel, you should get automatically signed-on to your Work.com application.</span></span>
<span data-ttu-id="b9bf5-288">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9bf5-288">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9bf5-289">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b9bf5-289">Additional resources</span></span>

* [<span data-ttu-id="b9bf5-290">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9bf5-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9bf5-291">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9bf5-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

