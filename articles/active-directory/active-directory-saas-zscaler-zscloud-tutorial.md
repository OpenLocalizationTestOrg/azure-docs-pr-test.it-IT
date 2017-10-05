---
title: 'Esercitazione: Integrazione di Azure Active Directory con Zscaler ZSCloud | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Zscaler ZSCloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 2b6eb113e5725260bc04f50e9218939bf28b1ff0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="4d1d4-103">Esercitazione: Integrazione di Azure Active Directory con Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="4d1d4-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="4d1d4-104">Questa esercitazione descrive come integrare Zscaler ZSCloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4d1d4-104">In this tutorial, you learn how to integrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d1d4-105">L'integrazione di Zscaler ZSCloud con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-105">Integrating Zscaler ZSCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4d1d4-106">È possibile controllare in Azure AD chi può accedere a Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="4d1d4-106">You can control in Azure AD who has access to Zscaler ZSCloud</span></span>
- <span data-ttu-id="4d1d4-107">È possibile abilitare gli utenti per l'accesso automatico a Zscaler ZSCloud (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="4d1d4-107">You can enable your users to automatically get signed-on to Zscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4d1d4-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4d1d4-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d1d4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d1d4-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4d1d4-110">Prerequisites</span></span>

<span data-ttu-id="4d1d4-111">Per configurare l'integrazione di Azure AD con Zscaler ZSCloud, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-111">To configure Azure AD integration with Zscaler ZSCloud, you need the following items:</span></span>

- <span data-ttu-id="4d1d4-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4d1d4-113">Sottoscrizione di Zscaler ZSCloud abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4d1d4-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d1d4-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d1d4-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d1d4-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4d1d4-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d1d4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d1d4-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4d1d4-118">Scenario description</span></span>
<span data-ttu-id="4d1d4-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d1d4-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d1d4-121">Aggiunta di Zscaler ZSCloud dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="4d1d4-121">Adding Zscaler ZSCloud from the gallery</span></span>
2. <span data-ttu-id="4d1d4-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d1d4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-the-gallery"></a><span data-ttu-id="4d1d4-123">Aggiunta di Zscaler ZSCloud dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="4d1d4-123">Adding Zscaler ZSCloud from the gallery</span></span>
<span data-ttu-id="4d1d4-124">Per configurare l'integrazione di Zscaler ZSCloud in Azure AD, è necessario aggiungere Zscaler ZSCloud dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-124">To configure the integration of Zscaler ZSCloud into Azure AD, you need to add Zscaler ZSCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4d1d4-125">**Per aggiungere Zscaler ZSCloud dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4d1d4-125">**To add Zscaler ZSCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4d1d4-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4d1d4-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4d1d4-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4d1d4-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4d1d4-133">Nella casella di ricerca digitare **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-133">In the search box, type **Zscaler ZSCloud**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="4d1d4-135">Nel pannello dei risultati selezionare **Zscaler ZSCloud** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-135">In the results panel, select **Zscaler ZSCloud**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4d1d4-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d1d4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4d1d4-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Zscaler ZSCloud usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4d1d4-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4d1d4-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Zscaler ZSCloud corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler ZSCloud is to a user in Azure AD.</span></span> <span data-ttu-id="4d1d4-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler ZSCloud needs to be established.</span></span>

<span data-ttu-id="4d1d4-141">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente) in Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="4d1d4-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Zscaler ZSCloud, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-142">To configure and test Azure AD single sign-on with Zscaler ZSCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4d1d4-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4d1d4-144">**[Configurazione delle impostazioni proxy](#configuring-proxy-settings)**: per configurare le impostazioni proxy in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="4d1d4-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="4d1d4-145">**[Creazione di un utente di test di Azure AD](#creating-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d1d4-146">**[Creazione di un utente di test di Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**: per avere una controparte di Britta Simon in Zscaler ZSCloud collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - to have a counterpart of Britta Simon in Zscaler ZSCloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4d1d4-147">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d1d4-148">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4d1d4-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d1d4-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4d1d4-150">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="4d1d4-151">**Per configurare l'accesso Single Sign-On di Azure AD con Zscaler ZSCloud, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4d1d4-151">**To configure Azure AD single sign-on with Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="4d1d4-152">Nella pagina di integrazione dell'applicazione **Zscaler ZSCloud** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-152">In the Azure portal, on the **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4d1d4-154">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="4d1d4-156">Nella sezione **URL e dominio Zscaler ZSCloud** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-156">On the **Zscaler ZSCloud Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="4d1d4-158">Nella casella di testo **URL di accesso** digitare l'URL usato dagli utenti per accedere all'applicazione Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-158">In the **Sign-on URL** textbox, type the URL used by your users to sign-on to your ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="4d1d4-159">È necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="4d1d4-160">Per ottenere questo valore, contattare il [team di supporto clienti di Zscaler ZSCloud](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint).</span><span class="sxs-lookup"><span data-stu-id="4d1d4-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) to get this value.</span></span> 
 
4. <span data-ttu-id="4d1d4-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="4d1d4-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4d1d4-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4d1d4-165">Nella sezione **Configurazione di Zscaler ZSCloud** fare clic su **Configura Zscaler ZSCloud** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-165">On the **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4d1d4-166">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="4d1d4-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="4d1d4-168">In un'altra finestra del Web browser accedere al sito aziendale di Zscaler ZSCloud come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-168">In a different web browser window, log in to your ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="4d1d4-169">Scegliere **Amministrazione**dal menu disponibile nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="4d1d4-170">![Amministrazione](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="4d1d4-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="4d1d4-171">In **Manage Administrators & Roles** (Gestisci amministratori e ruoli) fare clic su **Manage Users & Authentication** (Gestisci utenti e autenticazione).</span><span class="sxs-lookup"><span data-stu-id="4d1d4-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="4d1d4-172">![Gestire utenti e autenticazione](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Gestire utenti e autenticazione")</span><span class="sxs-lookup"><span data-stu-id="4d1d4-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="4d1d4-173">Nella sezione **Choose Authentication Options for your Organization** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="4d1d4-174">![Autenticazione](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Autenticazione")</span><span class="sxs-lookup"><span data-stu-id="4d1d4-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="4d1d4-175">a.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-175">a.</span></span> <span data-ttu-id="4d1d4-176">Selezionare **Authenticate using SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="4d1d4-177">b.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-177">b.</span></span> <span data-ttu-id="4d1d4-178">Fare clic su **Configure SAML Single Sign-On Parameters**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="4d1d4-179">Nella pagina della finestra di dialogo **Configure SAML Single Sign-On Parameters** (Configura parametri accesso Single Sign-On SAML) procedere come descritto di seguito e quindi fare clic su **Done** (Fine)</span><span class="sxs-lookup"><span data-stu-id="4d1d4-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="4d1d4-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4d1d4-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="4d1d4-181">a.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-181">a.</span></span> <span data-ttu-id="4d1d4-182">Incollare il valore dell'**URL del servizio Single Sign-On SAML** nella casella di testo **URL of the SAML Portal to which users are sent for authentication** (URL del portale di SAML a cui vengono indirizzati gli utenti per l'autenticazione).</span><span class="sxs-lookup"><span data-stu-id="4d1d4-182">Paste the **SAML Single Sign-On Service URL** value into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="4d1d4-183">b.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-183">b.</span></span> <span data-ttu-id="4d1d4-184">Nella casella di testo **Attribute containing Login Name** digitare **NameID**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="4d1d4-185">c.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-185">c.</span></span> <span data-ttu-id="4d1d4-186">Per caricare il certificato scaricato fare clic su **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="4d1d4-187">d.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-187">d.</span></span> <span data-ttu-id="4d1d4-188">Selezionare **Enable SAML Auto-Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="4d1d4-189">Nella pagina della finestra di dialogo **Configure User Authentication** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="4d1d4-190">![Amministrazione](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="4d1d4-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="4d1d4-191">a.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-191">a.</span></span> <span data-ttu-id="4d1d4-192">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-192">Click **Save**.</span></span>

    <span data-ttu-id="4d1d4-193">b.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-193">b.</span></span> <span data-ttu-id="4d1d4-194">Fare clic su **Attiva subito**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="4d1d4-195">Configurazione delle impostazioni proxy</span><span class="sxs-lookup"><span data-stu-id="4d1d4-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="4d1d4-196">Per configurare le impostazioni proxy in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="4d1d4-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="4d1d4-197">Avviare **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="4d1d4-198">Selezionare **Opzioni Internet** dal menu **Strumenti** per aprire la finestra di dialogo **Opzioni Internet**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="4d1d4-199">![Opzioni Internet](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Opzioni Internet")</span><span class="sxs-lookup"><span data-stu-id="4d1d4-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="4d1d4-200">Fare clic sulla scheda **Connessioni** .</span><span class="sxs-lookup"><span data-stu-id="4d1d4-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="4d1d4-201">![Connessioni](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connessioni")</span><span class="sxs-lookup"><span data-stu-id="4d1d4-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="4d1d4-202">Fare clic su **Impostazioni LAN** per aprire la finestra di dialogo **Impostazioni LAN**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="4d1d4-203">Nella sezione del server proxy seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="4d1d4-204">![Server proxy](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Server proxy")</span><span class="sxs-lookup"><span data-stu-id="4d1d4-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="4d1d4-205">a.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-205">a.</span></span> <span data-ttu-id="4d1d4-206">Selezionare **Usa un server proxy per la LAN**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="4d1d4-207">b.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-207">b.</span></span> <span data-ttu-id="4d1d4-208">Nella casella di testo Indirizzo digitare **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-208">In the Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="4d1d4-209">c.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-209">c.</span></span> <span data-ttu-id="4d1d4-210">Nella casella di testo Porta digitare **80**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="4d1d4-211">d.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-211">d.</span></span> <span data-ttu-id="4d1d4-212">Selezionare **Ignora server proxy per indirizzi locali**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="4d1d4-213">e.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-213">e.</span></span> <span data-ttu-id="4d1d4-214">Fare clic su **OK** per chiudere la finestra di dialogo **Impostazioni rete locale (LAN)**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="4d1d4-215">Fare clic su **OK** per chiudere la finestra di dialogo **Opzioni Internet**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-215">Click **OK** to close the **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4d1d4-216">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d1d4-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="4d1d4-217">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4d1d4-219">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4d1d4-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4d1d4-220">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4d1d4-222">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4d1d4-224">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4d1d4-226">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4d1d4-228">a.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-228">a.</span></span> <span data-ttu-id="4d1d4-229">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d1d4-230">b.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-230">b.</span></span> <span data-ttu-id="4d1d4-231">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4d1d4-232">c.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-232">c.</span></span> <span data-ttu-id="4d1d4-233">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4d1d4-234">d.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-234">d.</span></span> <span data-ttu-id="4d1d4-235">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="4d1d4-236">Creazione di un utente di test di Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="4d1d4-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="4d1d4-237">Per consentire agli utenti di Azure AD di accedere a Zscaler ZSCloud, è necessario effettuarne il provisioning in Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-237">To enable Azure AD users to log in to ZScaler ZSCloud, they must be provisioned to ZScaler ZSCloud.</span></span>  
<span data-ttu-id="4d1d4-238">Nel caso di Zscaler ZSCloud, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-238">In the case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="4d1d4-239">Per configurare il provisioning utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-239">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="4d1d4-240">Accedere al tenant **Zscaler** .</span><span class="sxs-lookup"><span data-stu-id="4d1d4-240">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="4d1d4-241">Fare clic su **Administration**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="4d1d4-242">![Amministrazione](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="4d1d4-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="4d1d4-243">Fare clic su **User Management**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="4d1d4-244">![Aggiungi](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Aggiungi")</span><span class="sxs-lookup"><span data-stu-id="4d1d4-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="4d1d4-245">Nella scheda **Utenti** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-245">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="4d1d4-246">![Aggiungi](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Aggiungi")</span><span class="sxs-lookup"><span data-stu-id="4d1d4-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="4d1d4-247">Nella sezione Add User seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-247">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="4d1d4-248">![Aggiungere un utente](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="4d1d4-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="4d1d4-249">a.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-249">a.</span></span> <span data-ttu-id="4d1d4-250">Digitare **ID utente**, **nome visualizzato per l'utente**, **password**, **conferma della password** e quindi selezionare **gruppi** e **reparto** per un account AAD valido di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-250">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="4d1d4-251">b.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-251">b.</span></span> <span data-ttu-id="4d1d4-252">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="4d1d4-253">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Zscaler ZSCloud per eseguire il provisioning degli account utente Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4d1d4-254">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d1d4-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4d1d4-255">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler ZSCloud.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4d1d4-257">**Per assegnare Britta Simon a Zscaler ZSCloud, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4d1d4-257">**To assign Britta Simon to Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="4d1d4-258">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4d1d4-260">Nell'elenco delle applicazioni selezionare **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-260">In the applications list, select **Zscaler ZSCloud**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="4d1d4-262">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-262">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4d1d4-264">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-264">Click **Add** button.</span></span> <span data-ttu-id="4d1d4-265">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4d1d4-267">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4d1d4-268">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d1d4-269">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4d1d4-270">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4d1d4-270">Testing single sign-on</span></span>

<span data-ttu-id="4d1d4-271">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-271">If you want to test your single sign-on settings, open the Access Panel.</span></span>

<span data-ttu-id="4d1d4-272">Quando si fa clic sul riquadro Zscaler ZSCloud nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-272">When you click the Zscaler ZSCloud tile in the Access Panel, you should get automatically signed-on to your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="4d1d4-273">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4d1d4-273">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4d1d4-274">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4d1d4-274">Additional resources</span></span>

* [<span data-ttu-id="4d1d4-275">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d1d4-275">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d1d4-276">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d1d4-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

