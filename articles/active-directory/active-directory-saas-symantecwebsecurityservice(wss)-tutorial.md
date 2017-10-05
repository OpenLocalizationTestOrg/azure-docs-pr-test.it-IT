---
title: 'Esercitazione: Integrazione di Azure Active Directory con Symantec Web Security Service (WSS) | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Symantec Web Security Service (WSS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: d0738bb750a82863b2f77540e8e7b94cca4b64e3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="1272f-103">Esercitazione: integrazione di Azure Active Directory con Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="1272f-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="1272f-104">Questa esercitazione descrive come integrare Symantec Web Security Service (WSS) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1272f-104">In this tutorial, you learn how to integrate Symantec Web Security Service (WSS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1272f-105">L'integrazione di Symantec Web Security Service (WSS) con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1272f-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1272f-106">È possibile controllare in Azure AD chi può accedere ad Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="1272f-106">You can control in Azure AD who has access to Symantec Web Security Service (WSS)</span></span>
- <span data-ttu-id="1272f-107">È possibile abilitare gli utenti per l'accesso automatico a Symantec Web Security Service (WSS), ovvero il Single Sign-On con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1272f-107">You can enable your users to automatically get signed-on to Symantec Web Security Service (WSS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1272f-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1272f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1272f-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1272f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1272f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1272f-110">Prerequisites</span></span>

<span data-ttu-id="1272f-111">Per configurare l'integrazione di Azure AD con Symantec Web Security Service (WSS), sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1272f-111">To configure Azure AD integration with Symantec Web Security Service (WSS), you need the following items:</span></span>

- <span data-ttu-id="1272f-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1272f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1272f-113">Una sottoscrizione abilitata per il Single Sign-On di Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="1272f-113">A Symantec Web Security Service (WSS) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1272f-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1272f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1272f-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1272f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1272f-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1272f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1272f-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1272f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1272f-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1272f-118">Scenario description</span></span>
<span data-ttu-id="1272f-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1272f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1272f-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1272f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1272f-121">Aggiunta di Symantec Web Security Service (WSS) dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="1272f-121">Adding Symantec Web Security Service (WSS) from the gallery</span></span>
2. <span data-ttu-id="1272f-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1272f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-the-gallery"></a><span data-ttu-id="1272f-123">Aggiunta di Symantec Web Security Service (WSS) dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="1272f-123">Adding Symantec Web Security Service (WSS) from the gallery</span></span>
<span data-ttu-id="1272f-124">Per configurare l'integrazione di Symantec Web Security Service (WSS) in Azure AD, è necessario aggiungere Symantec Web Security Service (WSS) dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1272f-124">To configure the integration of Symantec Web Security Service (WSS) into Azure AD, you need to add Symantec Web Security Service (WSS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1272f-125">**Per aggiungere Symantec Web Security Service (WSS) dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1272f-125">**To add Symantec Web Security Service (WSS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1272f-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="1272f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1272f-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1272f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1272f-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1272f-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1272f-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="1272f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1272f-133">Nella casella di ricerca, digitare **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="1272f-133">In the search box, type **Symantec Web Security Service (WSS)**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_search.png)

5. <span data-ttu-id="1272f-135">Nel pannello dei risultati selezionare **Symantec Web Security Service (WSS)** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1272f-135">In the results panel, select **Symantec Web Security Service (WSS)**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1272f-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1272f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1272f-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Symantec Web Security Service (WSS) usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1272f-138">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1272f-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Symantec Web Security Service (WSS) corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1272f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Symantec Web Security Service (WSS) is to a user in Azure AD.</span></span> <span data-ttu-id="1272f-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="1272f-140">In other words, a link relationship between an Azure AD user and the related user in Symantec Web Security Service (WSS) needs to be established.</span></span>

<span data-ttu-id="1272f-141">Per stabilire la relazione di collegamento, in Symantec Web Security Service (WSS) assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="1272f-141">In Symantec Web Security Service (WSS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1272f-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Symantec Web Security Service (WSS), è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1272f-142">To configure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1272f-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1272f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1272f-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1272f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1272f-145">**[Creazione di un utente test di Symantec Web Security Service (WSS)](#creating-a-symantec-web-security-service-wss-test-user)**: per avere una controparte di Britta Simon in Symantec Web Security Service (WSS) collegata alla relativa rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1272f-145">**[Creating a Symantec Web Security Service (WSS) test user](#creating-a-symantec-web-security-service-wss-test-user)** - to have a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1272f-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1272f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1272f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="1272f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1272f-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1272f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1272f-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="1272f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="1272f-150">**Per configurare l'accesso Single Sign-On di Azure AD con Symantec Web Security Service (WSS), seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1272f-150">**To configure Azure AD single sign-on with Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="1272f-151">Nella pagina di integrazione dell'applicazione **Symantec Web Security Service (WSS)** del Portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="1272f-151">In the Azure portal, on the **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1272f-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1272f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="1272f-155">Nella sezione **Symantec Web Security Service (WSS) Domain and URLs** (URL e dominio Symantec Web Security Service (WSS)) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1272f-155">On the **Symantec Web Security Service (WSS) Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="1272f-157">a.</span><span class="sxs-lookup"><span data-stu-id="1272f-157">a.</span></span> <span data-ttu-id="1272f-158">Nella casella di testo **URL accesso** specificare l'URL che si desidera bloccare in base al criterio di blocco di Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="1272f-158">In the **Sign-on URL** textbox, mention the url, which you want to block according to the blocking policy of the Symantec Web Security Service (WSS).</span></span>  
    
    <span data-ttu-id="1272f-159">b.</span><span class="sxs-lookup"><span data-stu-id="1272f-159">b.</span></span> <span data-ttu-id="1272f-160">Nella casella di testo **Identificatore** digitare l'URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="1272f-160">In the **Identifier** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1272f-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="1272f-161">These values are not real.</span></span> <span data-ttu-id="1272f-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="1272f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1272f-163">Per ottenere questi valori contattare il [team di supporto clienti di Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="1272f-163">Contact [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) to get these values.</span></span> 

4. <span data-ttu-id="1272f-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="1272f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="1272f-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1272f-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1272f-168">Per configurare l'accesso Single Sign-On sul lato **Symantec Web Security Service (WSS)**, è necessario inviare il file **Metadata XML** scaricato al [team di supporto Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="1272f-168">To configure single sign-on on **Symantec Web Security Service (WSS)** side, you need to send the downloaded **Metadata XML** to [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="1272f-169">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="1272f-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1272f-170">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="1272f-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1272f-171">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1272f-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1272f-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1272f-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="1272f-173">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1272f-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1272f-175">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1272f-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1272f-176">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="1272f-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1272f-178">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="1272f-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1272f-180">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="1272f-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1272f-182">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1272f-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1272f-184">a.</span><span class="sxs-lookup"><span data-stu-id="1272f-184">a.</span></span> <span data-ttu-id="1272f-185">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1272f-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1272f-186">b.</span><span class="sxs-lookup"><span data-stu-id="1272f-186">b.</span></span> <span data-ttu-id="1272f-187">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1272f-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1272f-188">c.</span><span class="sxs-lookup"><span data-stu-id="1272f-188">c.</span></span> <span data-ttu-id="1272f-189">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="1272f-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1272f-190">d.</span><span class="sxs-lookup"><span data-stu-id="1272f-190">d.</span></span> <span data-ttu-id="1272f-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1272f-191">Click **Create**.</span></span>
 
### <a name="creating-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="1272f-192">Creazione di un utente test di Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="1272f-192">Creating a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="1272f-193">In questa sezione viene creato un utente chiamato Britta Simon in Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="1272f-193">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="1272f-194">Contattare il [team di supporto di Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us) per aggiungere gli utenti nella piattaforma Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="1272f-194">Work with [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) to add the users in the Symantec Web Security Service (WSS) platform.</span></span> <span data-ttu-id="1272f-195">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1272f-195">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="1272f-196">Insieme alle informazioni dell'utente è necessario inviare l'indirizzo IP pubblico del computer da cui si tenta di accedere all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1272f-196">Also along with the user details you need to send the public IPaddress of the machine from which you are trying to access the application.</span></span>

> [!NOTE]
> <span data-ttu-id="1272f-197">[Fare clic qui](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) per ottenere l'indirizzo IP pubblico del computer.</span><span class="sxs-lookup"><span data-stu-id="1272f-197">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) to get your machine's public IPaddress.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1272f-198">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1272f-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1272f-199">In questa sezione, Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="1272f-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Symantec Web Security Service (WSS).</span></span>

![Assegna utente][200] 

<span data-ttu-id="1272f-201">**Per aggiungere Britta Simon a Symantec Web Security Service (WSS), seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1272f-201">**To assign Britta Simon to Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="1272f-202">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1272f-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1272f-204">Nell'elenco delle applicazioni, selezionare **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="1272f-204">In the applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_app.png) 

3. <span data-ttu-id="1272f-206">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1272f-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1272f-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1272f-208">Click **Add** button.</span></span> <span data-ttu-id="1272f-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1272f-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1272f-211">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="1272f-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1272f-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1272f-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1272f-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1272f-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1272f-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1272f-214">Testing single sign-on</span></span>

<span data-ttu-id="1272f-215">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1272f-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1272f-216">Quando si fa clic sul riquadro di Symantec Web Security Service (WSS) nel Pannello di accesso, l'utente viene reindirizzato alla pagina di blocco per la quale è stato configurato il criterio di blocco.</span><span class="sxs-lookup"><span data-stu-id="1272f-216">When you click the Symantec Web Security Service (WSS) tile in the Access Panel, you get redirected to the blocking page for which the blocking policy has been configured.</span></span>
<span data-ttu-id="1272f-217">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1272f-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1272f-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1272f-218">Additional resources</span></span>

* [<span data-ttu-id="1272f-219">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1272f-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1272f-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1272f-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_203.png

