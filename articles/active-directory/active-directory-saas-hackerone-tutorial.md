---
title: 'Esercitazione: Integrazione di Azure Active Directory con HackerOne | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e HackerOne.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 657d8d4c98b7b133698a5cda0aa675da7f68c464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="a8d23-103">Esercitazione: Integrazione di Azure Active Directory con HackerOne</span><span class="sxs-lookup"><span data-stu-id="a8d23-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="a8d23-104">Questa esercitazione descrive come integrare HackerOne con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8d23-104">In this tutorial, you learn how to integrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a8d23-105">L'integrazione di HackerOne con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8d23-105">Integrating HackerOne with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a8d23-106">È possibile controllare in Azure AD chi può accedere a HackerOne</span><span class="sxs-lookup"><span data-stu-id="a8d23-106">You can control in Azure AD who has access to HackerOne</span></span>
- <span data-ttu-id="a8d23-107">È possibile abilitare gli utenti per l'accesso automatico a HackerOne (Single Sign-On) con l'account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8d23-107">You can enable your users to automatically get signed-on to HackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a8d23-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8d23-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a8d23-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a8d23-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8d23-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a8d23-110">Prerequisites</span></span>

<span data-ttu-id="a8d23-111">Per configurare l'integrazione di Azure AD con HackerOne, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8d23-111">To configure Azure AD integration with HackerOne, you need the following items:</span></span>

- <span data-ttu-id="a8d23-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8d23-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a8d23-113">Sottoscrizione di HackerOne abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a8d23-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a8d23-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a8d23-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a8d23-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8d23-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a8d23-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a8d23-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a8d23-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8d23-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a8d23-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a8d23-118">Scenario description</span></span>
<span data-ttu-id="a8d23-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a8d23-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a8d23-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8d23-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a8d23-121">Aggiunta di HackerOne dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a8d23-121">Adding HackerOne from the gallery</span></span>
2. <span data-ttu-id="a8d23-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8d23-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-the-gallery"></a><span data-ttu-id="a8d23-123">Aggiunta di HackerOne dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a8d23-123">Adding HackerOne from the gallery</span></span>
<span data-ttu-id="a8d23-124">Per configurare l'integrazione di HackerOne in Azure AD, è necessario aggiungere HackerOne dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a8d23-124">To configure the integration of HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a8d23-125">**Per aggiungere HackerOne dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a8d23-125">**To add HackerOne from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a8d23-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a8d23-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a8d23-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a8d23-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a8d23-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="a8d23-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a8d23-133">Nella casella di ricerca digitare **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-133">In the search box, type **HackerOne**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="a8d23-135">Nel pannello dei risultati selezionare **HackerOne** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a8d23-135">In the results panel, select **HackerOne**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a8d23-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8d23-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="a8d23-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con HackerOne usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a8d23-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a8d23-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di HackerOne corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8d23-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne is to a user in Azure AD.</span></span> <span data-ttu-id="a8d23-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a8d23-140">In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.</span></span>

<span data-ttu-id="a8d23-141">Per stabilire la relazione di collegamento, in HackerOne assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="a8d23-141">In HackerOne, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a8d23-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con HackerOne, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8d23-142">To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a8d23-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a8d23-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a8d23-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8d23-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a8d23-145">**[Creazione di un utente di test di HackerOne](#creating-a-hackerone-test-user)**: per avere una controparte di Britta Simon in HackerOne collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8d23-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in HackerOne that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a8d23-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8d23-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a8d23-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="a8d23-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a8d23-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8d23-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a8d23-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a8d23-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="a8d23-150">**Per configurare l'accesso Single Sign-On di Azure AD con HackerOne, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a8d23-150">**To configure Azure AD single sign-on with HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="a8d23-151">Nella pagina di integrazione dell'applicazione **HackerOne** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-151">In the Azure portal, on the **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a8d23-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a8d23-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="a8d23-155">Nella sezione **HackerOne Single sign-on URL and Identifier** (Identificatore e URL Single Sign-On di HackerOne) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a8d23-155">On the **HackerOne Single sign-on URL and Identifier** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="a8d23-157">a.</span><span class="sxs-lookup"><span data-stu-id="a8d23-157">a.</span></span> <span data-ttu-id="a8d23-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://hackerone.com/<company name>/authentication`.</span><span class="sxs-lookup"><span data-stu-id="a8d23-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="a8d23-159">b.</span><span class="sxs-lookup"><span data-stu-id="a8d23-159">b.</span></span> <span data-ttu-id="a8d23-160">Nella casella di testo **Identificatore** digitare un URL come indicato di seguito: `https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="a8d23-160">In the **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="a8d23-161">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="a8d23-161">This value is not real.</span></span> <span data-ttu-id="a8d23-162">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="a8d23-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="a8d23-163">Per ottenere questo valore, contattare il [team di supporto di HackerOne](mailto:support@hackerone.com).</span><span class="sxs-lookup"><span data-stu-id="a8d23-163">Contact [HackerOne support team](mailto:support@hackerone.com) to get this value.</span></span> 
 
4. <span data-ttu-id="a8d23-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="a8d23-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="a8d23-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a8d23-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a8d23-168">Nella sezione **Configurazione di HackerOne** fare clic su **Configura HackerOne** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-168">On the **HackerOne Configuration** section, click **Configure HackerOne** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a8d23-169">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="a8d23-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="a8d23-171">Accedere al tenant di HackerOne come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a8d23-171">Sign On to your HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="a8d23-172">Nel menu in alto fare clic su **Settings** (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="a8d23-172">In the menu on the top, click the "**Settings**."</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="a8d23-174">Passare all'opzione **Authentication** (Autenticazione) e fare clic su **Add SAML settings** (Aggiungi impostazioni SAML).</span><span class="sxs-lookup"><span data-stu-id="a8d23-174">Navigate to "**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="a8d23-176">Nella finestra di dialogo **SAML Settings** (Impostazioni SAML) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a8d23-176">On the **SAML Settings** dialog, perform the following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="a8d23-178">a.</span><span class="sxs-lookup"><span data-stu-id="a8d23-178">a.</span></span> <span data-ttu-id="a8d23-179">Nella casella di testo **Email Domain** (Dominio di posta elettronica) digitare un dominio registrato.</span><span class="sxs-lookup"><span data-stu-id="a8d23-179">In the **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="a8d23-180">b.</span><span class="sxs-lookup"><span data-stu-id="a8d23-180">b.</span></span> <span data-ttu-id="a8d23-181">Nella casella di testo **Single Sign On URL** (URL Single Sign-On) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8d23-181">In  **Single Sign On URL** textboxes, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a8d23-182">c.</span><span class="sxs-lookup"><span data-stu-id="a8d23-182">c.</span></span> <span data-ttu-id="a8d23-183">Aprire nel Blocco note il **file del certificato** scaricato dal portale di Azure, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **X509 Certificate** (Certificato X.509).</span><span class="sxs-lookup"><span data-stu-id="a8d23-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="a8d23-184">d.</span><span class="sxs-lookup"><span data-stu-id="a8d23-184">d.</span></span> <span data-ttu-id="a8d23-185">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-185">Click **Save**.</span></span>

11. <span data-ttu-id="a8d23-186">Nella finestra di dialogo relativa alle impostazioni di autenticazione seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a8d23-186">On the Authentication Settings dialog, perform the following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="a8d23-188">a.</span><span class="sxs-lookup"><span data-stu-id="a8d23-188">a.</span></span> <span data-ttu-id="a8d23-189">Fare clic su **Run test**(Esegui test).</span><span class="sxs-lookup"><span data-stu-id="a8d23-189">Click **Run test**.</span></span>

    <span data-ttu-id="a8d23-190">b.</span><span class="sxs-lookup"><span data-stu-id="a8d23-190">b.</span></span> <span data-ttu-id="a8d23-191">Se il valore del campo **Status** (Stato) corrisponde a **Last test status: created** (Stato ultimo test: creato), contattare il [team di supporto di HackerOne](mailto:support@hackerone.com) per richiedere una verifica della configurazione.</span><span class="sxs-lookup"><span data-stu-id="a8d23-191">If the value of the **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) to request a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="a8d23-192">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a8d23-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a8d23-193">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="a8d23-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a8d23-194">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8d23-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a8d23-195">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8d23-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="a8d23-196">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8d23-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a8d23-198">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a8d23-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a8d23-199">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a8d23-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a8d23-201">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="a8d23-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a8d23-203">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a8d23-205">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a8d23-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a8d23-207">a.</span><span class="sxs-lookup"><span data-stu-id="a8d23-207">a.</span></span> <span data-ttu-id="a8d23-208">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a8d23-209">b.</span><span class="sxs-lookup"><span data-stu-id="a8d23-209">b.</span></span> <span data-ttu-id="a8d23-210">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a8d23-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a8d23-211">c.</span><span class="sxs-lookup"><span data-stu-id="a8d23-211">c.</span></span> <span data-ttu-id="a8d23-212">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a8d23-213">d.</span><span class="sxs-lookup"><span data-stu-id="a8d23-213">d.</span></span> <span data-ttu-id="a8d23-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="a8d23-215">Creazione di un utente test di HackerOne</span><span class="sxs-lookup"><span data-stu-id="a8d23-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="a8d23-216">Successivamente, viene creato un utente chiamato Britta Simon in HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a8d23-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="a8d23-217">HackerOne supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a8d23-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="a8d23-218">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="a8d23-218">There is no action item for you in this section.</span></span> <span data-ttu-id="a8d23-219">Quando si accede a HackerOne, viene creato un nuovo utente se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="a8d23-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="a8d23-220">Per creare un utente manualmente, è necessario contattare il team di supporto di HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a8d23-220">If you need to create a user manually, you need to contact the Certify support team.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a8d23-221">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8d23-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a8d23-222">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a8d23-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HackerOne.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a8d23-224">**Per assegnare Britta Simon a HackerOne, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a8d23-224">**To assign Britta Simon to HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="a8d23-225">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a8d23-227">Nell'elenco di applicazioni selezionare **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-227">In the applications list, select **HackerOne**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="a8d23-229">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="a8d23-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a8d23-231">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-231">Click **Add** button.</span></span> <span data-ttu-id="a8d23-232">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a8d23-234">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="a8d23-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a8d23-235">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a8d23-236">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a8d23-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a8d23-237">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a8d23-237">Testing single sign-on</span></span>

<span data-ttu-id="a8d23-238">Viene infine eseguito il test della configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a8d23-238">Finally, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="a8d23-239">Quando si fa clic sul riquadro HackerOne nel pannello di accesso, verrà eseguito automaticamente l'accesso all'applicazione HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a8d23-239">When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a8d23-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a8d23-240">Additional resources</span></span>

* [<span data-ttu-id="a8d23-241">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8d23-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a8d23-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8d23-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

