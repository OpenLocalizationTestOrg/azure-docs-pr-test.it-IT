---
title: 'Esercitazione: Integrazione di Azure Active Directory con UltiPro | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e UltiPro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: afc0f2b9-2eac-47ec-af04-65ed0fb0ca5a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: ab60bda1be7101d5bd0c51f5499a820db40375bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ultipro"></a><span data-ttu-id="dfff2-103">Esercitazione: Integrazione di Azure Active Directory con UltiPro</span><span class="sxs-lookup"><span data-stu-id="dfff2-103">Tutorial: Azure Active Directory integration with UltiPro</span></span>

<span data-ttu-id="dfff2-104">Questa esercitazione descrive come integrare UltiPro con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dfff2-104">In this tutorial, you learn how to integrate UltiPro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dfff2-105">L'integrazione di UltiPro con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dfff2-105">Integrating UltiPro with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dfff2-106">È possibile controllare in Azure AD chi può accedere a UltiPro</span><span class="sxs-lookup"><span data-stu-id="dfff2-106">You can control in Azure AD who has access to UltiPro</span></span>
- <span data-ttu-id="dfff2-107">È possibile abilitare gli utenti per l'accesso automatico a UltiPro (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfff2-107">You can enable your users to automatically get signed-on to UltiPro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dfff2-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dfff2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dfff2-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dfff2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfff2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dfff2-110">Prerequisites</span></span>

<span data-ttu-id="dfff2-111">Per configurare l'integrazione di Azure AD con UltiPro, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dfff2-111">To configure Azure AD integration with UltiPro, you need the following items:</span></span>

- <span data-ttu-id="dfff2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dfff2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dfff2-113">Sottoscrizione di UltiPro abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dfff2-113">A UltiPro single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dfff2-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="dfff2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dfff2-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="dfff2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dfff2-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="dfff2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dfff2-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dfff2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dfff2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="dfff2-118">Scenario description</span></span>
<span data-ttu-id="dfff2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="dfff2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dfff2-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="dfff2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dfff2-121">Aggiunta di UltiPro dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="dfff2-121">Adding UltiPro from the gallery</span></span>
2. <span data-ttu-id="dfff2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfff2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ultipro-from-the-gallery"></a><span data-ttu-id="dfff2-123">Aggiunta di UltiPro dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="dfff2-123">Adding UltiPro from the gallery</span></span>
<span data-ttu-id="dfff2-124">Per configurare l'integrazione di UltiPro in Azure AD, è necessario aggiungere UltiPro dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="dfff2-124">To configure the integration of UltiPro into Azure AD, you need to add UltiPro from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dfff2-125">**Per aggiungere UltiPro dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dfff2-125">**To add UltiPro from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dfff2-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="dfff2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dfff2-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dfff2-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="dfff2-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="dfff2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="dfff2-133">Nella casella di ricerca digitare **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-133">In the search box, type **UltiPro**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_search.png)

5. <span data-ttu-id="dfff2-135">Nel pannello dei risultati selezionare **UltiPro** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dfff2-135">In the results panel, select **UltiPro**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dfff2-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfff2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dfff2-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con UltiPro con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dfff2-138">In this section, you configure and test Azure AD single sign-on with UltiPro based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dfff2-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di UltiPro che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dfff2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UltiPro is to a user in Azure AD.</span></span> <span data-ttu-id="dfff2-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in UltiPro.</span><span class="sxs-lookup"><span data-stu-id="dfff2-140">In other words, a link relationship between an Azure AD user and the related user in UltiPro needs to be established.</span></span>

<span data-ttu-id="dfff2-141">Per stabilire la relazione di collegamento, in UltiPro assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="dfff2-141">In UltiPro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dfff2-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con UltiPro, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="dfff2-142">To configure and test Azure AD single sign-on with UltiPro, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dfff2-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="dfff2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dfff2-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dfff2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dfff2-145">**[Creazione di un utente test UltiPro](#creating-a-ultipro-test-user)**: per avere una controparte di Britta Simon in UltiPro collegata alla relativa rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="dfff2-145">**[Creating a UltiPro test user](#creating-a-ultipro-test-user)** - to have a counterpart of Britta Simon in UltiPro that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dfff2-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dfff2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dfff2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="dfff2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dfff2-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfff2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dfff2-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione UltiPro.</span><span class="sxs-lookup"><span data-stu-id="dfff2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UltiPro application.</span></span>

<span data-ttu-id="dfff2-150">**Per configurare l'accesso Single Sign-On di Azure AD con UltiPro, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dfff2-150">**To configure Azure AD single sign-on with UltiPro, perform the following steps:**</span></span>

1. <span data-ttu-id="dfff2-151">Nella pagina di integrazione dell'applicazione **UltiPro** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-151">In the Azure portal, on the **UltiPro** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="dfff2-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="dfff2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_samlbase.png)

3. <span data-ttu-id="dfff2-155">Nella sezione **URL e dominio UltiPro** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dfff2-155">On the **UltiPro Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_url.png)

    <span data-ttu-id="dfff2-157">a.</span><span class="sxs-lookup"><span data-stu-id="dfff2-157">a.</span></span> <span data-ttu-id="dfff2-158">Nella casella di testo **URL di accesso** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="dfff2-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/`|
    | `https://<companyname>.ultiproworkplace.com?cpi=AZUREADISSSUERURL`|
    | ` https://<companyname>.ultipro.ca`|
    
    <span data-ttu-id="dfff2-159">b.</span><span class="sxs-lookup"><span data-stu-id="dfff2-159">b.</span></span> <span data-ttu-id="dfff2-160">Nella casella di testo **Identificatore** digitare l'URL adottando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="dfff2-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/adfs/services/trust`|
    | `https://<companyname>.ultiproworkplace.com/adfs/services/trust`|
    | `https://<companyname>.ultipro.ca/adfs/services/trust`|
    
    <span data-ttu-id="dfff2-161">c.</span><span class="sxs-lookup"><span data-stu-id="dfff2-161">c.</span></span> <span data-ttu-id="dfff2-162">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="dfff2-162">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/<instancename>`|
    | `https://<companyname>.ultiproworkplace.com/<instancename>`|
    | `https://<companyname>.ultipro.ca/<instancename>`|
    
    > [!NOTE] 
    > <span data-ttu-id="dfff2-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="dfff2-163">These values are not real.</span></span> <span data-ttu-id="dfff2-164">aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="dfff2-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="dfff2-165">Per ottenere questi valori, contattare il [team di supporto clienti di UltiPro](https://www.ultimatesoftware.com/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="dfff2-165">Contact [UltiPro Client support team](https://www.ultimatesoftware.com/ContactUs) to get these values.</span></span> 

5. <span data-ttu-id="dfff2-166">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="dfff2-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_certificate.png) 

6. <span data-ttu-id="dfff2-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="dfff2-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ultipro-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="dfff2-170">Nella sezione **Configurazione di UltiPro** fare clic su **Configura UltiPro** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-170">On the **UltiPro Configuration** section, click **Configure UltiPro** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dfff2-171">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="dfff2-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_configure.png) 

8. <span data-ttu-id="dfff2-173">Per configurare l'accesso Single Sign-On sul lato **UltiPro**, è necessario inviare il file di **Certificato (Base64) scaricato, l'URL di disconnessione, l'ID entità SAML e l'URL del servizio Single Sign-On SAML** al [team di supporto di UltiPro](https://www.ultimatesoftware.com/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="dfff2-173">To configure single sign-on on **UltiPro** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [UltiPro support team](https://www.ultimatesoftware.com/ContactUs).</span></span>

> [!TIP]
> <span data-ttu-id="dfff2-174">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="dfff2-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dfff2-175">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="dfff2-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dfff2-176">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dfff2-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dfff2-177">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfff2-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="dfff2-178">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dfff2-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="dfff2-180">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="dfff2-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dfff2-181">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="dfff2-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dfff2-183">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="dfff2-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dfff2-185">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dfff2-187">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dfff2-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dfff2-189">a.</span><span class="sxs-lookup"><span data-stu-id="dfff2-189">a.</span></span> <span data-ttu-id="dfff2-190">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dfff2-191">b.</span><span class="sxs-lookup"><span data-stu-id="dfff2-191">b.</span></span> <span data-ttu-id="dfff2-192">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dfff2-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dfff2-193">c.</span><span class="sxs-lookup"><span data-stu-id="dfff2-193">c.</span></span> <span data-ttu-id="dfff2-194">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dfff2-195">d.</span><span class="sxs-lookup"><span data-stu-id="dfff2-195">d.</span></span> <span data-ttu-id="dfff2-196">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-196">Click **Create**.</span></span>
 
### <a name="creating-a-ultipro-test-user"></a><span data-ttu-id="dfff2-197">Creazione di un utente test di UltiPro</span><span class="sxs-lookup"><span data-stu-id="dfff2-197">Creating a UltiPro test user</span></span>

<span data-ttu-id="dfff2-198">In questa sezione viene creato un utente di nome Britta Simon in UltiPro.</span><span class="sxs-lookup"><span data-stu-id="dfff2-198">In this section, you create a user called Britta Simon in UltiPro.</span></span> <span data-ttu-id="dfff2-199">Collaborare con il [team di supporto di Ultipro](https://www.ultimatesoftware.com/ContactUs) per aggiungere gli utenti nella piattaforma Ultipro.</span><span class="sxs-lookup"><span data-stu-id="dfff2-199">Work with [UltiPro support team](https://www.ultimatesoftware.com/ContactUs) to add the users in the UltiPro platform.</span></span> <span data-ttu-id="dfff2-200">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="dfff2-200">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dfff2-201">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfff2-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dfff2-202">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a UltiPro.</span><span class="sxs-lookup"><span data-stu-id="dfff2-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UltiPro.</span></span>

![Assegna utente][200] 

<span data-ttu-id="dfff2-204">**Per assegnare Britta Simon a UltiPro, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dfff2-204">**To assign Britta Simon to UltiPro, perform the following steps:**</span></span>

1. <span data-ttu-id="dfff2-205">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="dfff2-207">Nell'elenco di applicazioni selezionare **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-207">In the applications list, select **UltiPro**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_app.png) 

3. <span data-ttu-id="dfff2-209">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="dfff2-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="dfff2-211">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-211">Click **Add** button.</span></span> <span data-ttu-id="dfff2-212">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="dfff2-214">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="dfff2-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dfff2-215">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dfff2-216">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="dfff2-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dfff2-217">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dfff2-217">Testing single sign-on</span></span>

<span data-ttu-id="dfff2-218">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="dfff2-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="dfff2-219">Quando si fa clic sul riquadro UltiPro nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione UltiPro.</span><span class="sxs-lookup"><span data-stu-id="dfff2-219">When you click the UltiPro tile in the Access Panel, you should get automatically signed-on to your UltiPro application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dfff2-220">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="dfff2-220">Additional resources</span></span>

* [<span data-ttu-id="dfff2-221">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dfff2-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dfff2-222">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dfff2-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_203.png

