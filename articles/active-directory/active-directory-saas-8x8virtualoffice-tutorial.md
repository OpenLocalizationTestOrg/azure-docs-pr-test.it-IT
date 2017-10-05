---
title: 'Esercitazione: Integrazione di Azure Active Directory con 8x8 Virtual Office | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e 8x8 Virtual Office.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d8dcf0171b93fec15347e810a1b525bd815dbf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="a0596-103">Esercitazione: Integrazione di Azure Active Directory con 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="a0596-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="a0596-104">Questa esercitazione descrive come integrare 8x8 Virtual Office con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0596-104">In this tutorial, you learn how to integrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0596-105">L'integrazione di 8x8 Virtual Office con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0596-105">Integrating 8x8 Virtual Office with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a0596-106">È possibile controllare in Azure AD chi può accedere a 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="a0596-106">You can control in Azure AD who has access to 8x8 Virtual Office</span></span>
- <span data-ttu-id="a0596-107">È possibile abilitare gli utenti per l'accesso automatico a 8x8 Virtual Office (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0596-107">You can enable your users to automatically get signed-on to 8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a0596-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0596-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a0596-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a0596-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0596-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a0596-110">Prerequisites</span></span>

<span data-ttu-id="a0596-111">Per configurare l'integrazione di Azure AD con 8x8 Virtual Office, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0596-111">To configure Azure AD integration with 8x8 Virtual Office, you need the following items:</span></span>

- <span data-ttu-id="a0596-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0596-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a0596-113">Sottoscrizione di 8x8 Virtual Office abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a0596-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a0596-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a0596-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a0596-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0596-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a0596-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a0596-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a0596-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a0596-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a0596-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a0596-118">Scenario description</span></span>
<span data-ttu-id="a0596-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a0596-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a0596-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0596-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a0596-121">Aggiunta di 8x8 Virtual Office dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a0596-121">Adding 8x8 Virtual Office from the gallery</span></span>
2. <span data-ttu-id="a0596-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0596-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-the-gallery"></a><span data-ttu-id="a0596-123">Aggiunta di 8x8 Virtual Office dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a0596-123">Adding 8x8 Virtual Office from the gallery</span></span>
<span data-ttu-id="a0596-124">Per configurare l'integrazione di 8x8 Virtual Office in Azure AD, è necessario aggiungere 8x8 Virtual Office dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a0596-124">To configure the integration of 8x8 Virtual Office into Azure AD, you need to add 8x8 Virtual Office from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a0596-125">**Per aggiungere 8x8 Virtual Office dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a0596-125">**To add 8x8 Virtual Office from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a0596-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a0596-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a0596-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a0596-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a0596-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a0596-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a0596-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="a0596-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a0596-133">Nella casella di ricerca digitare **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="a0596-133">In the search box, type **8x8 Virtual Office**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="a0596-135">Nel pannello dei risultati selezionare **8x8 Virtual Office** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a0596-135">In the results panel, select **8x8 Virtual Office**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a0596-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0596-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a0596-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con 8x8 Virtual Office mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a0596-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a0596-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di 8x8 Virtual Office corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0596-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 8x8 Virtual Office is to a user in Azure AD.</span></span> <span data-ttu-id="a0596-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="a0596-140">In other words, a link relationship between an Azure AD user and the related user in 8x8 Virtual Office needs to be established.</span></span>

<span data-ttu-id="a0596-141">Per stabilire la relazione di collegamento, in 8x8 Virtual Office assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="a0596-141">In 8x8 Virtual Office, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a0596-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con 8x8 Virtual Office è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0596-142">To configure and test Azure AD single sign-on with 8x8 Virtual Office, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a0596-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a0596-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a0596-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a0596-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a0596-145">**[Creazione di un utente test di 8x8 Virtual Office](#creating-a-8x8-virtual-office-test-user)**: per avere una controparte di Britta Simon in 8x8 Virtual Office collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0596-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - to have a counterpart of Britta Simon in 8x8 Virtual Office that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a0596-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0596-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a0596-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="a0596-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a0596-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0596-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a0596-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="a0596-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="a0596-150">**Per configurare l'accesso Single Sign-On di Azure AD con 8x8 Virtual Office, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a0596-150">**To configure Azure AD single sign-on with 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="a0596-151">Nella pagina di integrazione dell'applicazione **8x8 Virtual Office** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a0596-151">In the Azure portal, on the **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a0596-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a0596-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="a0596-155">Nella sezione **URL e dominio 8x8 Virtual Office** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a0596-155">On the **8x8 Virtual Office Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="a0596-157">a.</span><span class="sxs-lookup"><span data-stu-id="a0596-157">a.</span></span> <span data-ttu-id="a0596-158">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="a0596-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="a0596-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="a0596-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="a0596-160">b.</span><span class="sxs-lookup"><span data-stu-id="a0596-160">b.</span></span> <span data-ttu-id="a0596-161">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="a0596-161">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="a0596-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="a0596-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a0596-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="a0596-163">These values are not real.</span></span> <span data-ttu-id="a0596-164">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="a0596-164">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="a0596-165">Per ottenere questi valori contattare il [team di supporto di 8x8 Virtual Office](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="a0596-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) to get these values.</span></span>
 


4. <span data-ttu-id="a0596-166">Nella sezione **Certificato di firma SAML** fare clic su **Certificate (Raw)** (Certificato (base)) e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="a0596-166">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="a0596-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a0596-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a0596-170">Nella sezione **Configurazione di 8x8 Virtual Office** fare clic su **Configura 8x8 Virtual Office** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="a0596-170">On the **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a0596-171">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="a0596-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="a0596-173">Accedere al tenant di 8x8 Virtual Office come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a0596-173">Sign-on to your 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="a0596-174">Selezionare **Virtual Office Account Mgr** (Account manager di Virtual Office) nel pannello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a0596-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Configurazione sul lato app](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="a0596-176">Selezionare l'account **Business** (Aziendale) da gestire e fare clic sul pulsante **Sign In** (Accedi).</span><span class="sxs-lookup"><span data-stu-id="a0596-176">Select **Business** account to manage and click **Sign In** button.</span></span>
   
    ![Configurazione sul lato app](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="a0596-178">Fare clic sulla scheda **Accounts** (Account) nell'elenco di menu.</span><span class="sxs-lookup"><span data-stu-id="a0596-178">Click **Accounts** tab in the menu list.</span></span>
   
    ![Configurazione sul lato app](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="a0596-180">Fare clic su **Single Sign On** nell'elenco di account.</span><span class="sxs-lookup"><span data-stu-id="a0596-180">Click **Single Sign On** in the list of Accounts.</span></span>
   
    ![Configurazione sul lato app](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="a0596-182">Selezionare **Single Sign-On** nel metodo di autenticazione e fare clic su **SAML**.</span><span class="sxs-lookup"><span data-stu-id="a0596-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Configurazione sul lato app](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="a0596-184">Copiare i valori di **URL SSO SAML**, **URL servizio Single Sign-Out** e **URL autorità di certificazione** da Azure AD nei campi **Sign In URL** (URL di accesso), **Sign Out URL** (URL di disconnessione) e **Issuer URL** (URL autorità di certificazione) in 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="a0596-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD to **Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Configurazione sul lato app](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="a0596-186">Fare clic sul pulsante **Browser** per caricare il certificato scaricato da Azure AD e sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a0596-186">Click **Browser** button to upload the certificate which you downloaded from Azure AD, and click the **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="a0596-187">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a0596-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a0596-188">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="a0596-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a0596-189">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0596-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a0596-190">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0596-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="a0596-191">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0596-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a0596-193">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a0596-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a0596-194">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a0596-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a0596-196">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="a0596-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a0596-198">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="a0596-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a0596-200">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a0596-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a0596-202">a.</span><span class="sxs-lookup"><span data-stu-id="a0596-202">a.</span></span> <span data-ttu-id="a0596-203">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a0596-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a0596-204">b.</span><span class="sxs-lookup"><span data-stu-id="a0596-204">b.</span></span> <span data-ttu-id="a0596-205">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a0596-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0596-206">c.</span><span class="sxs-lookup"><span data-stu-id="a0596-206">c.</span></span> <span data-ttu-id="a0596-207">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="a0596-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a0596-208">d.</span><span class="sxs-lookup"><span data-stu-id="a0596-208">d.</span></span> <span data-ttu-id="a0596-209">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a0596-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="a0596-210">Creazione di un utente test di 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="a0596-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="a0596-211">Questa sezione descrive come creare un utente chiamato Britta Simon in 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="a0596-211">The objective of this section is to create a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="a0596-212">8x8 Virtual Office supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a0596-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a0596-213">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="a0596-213">There is no action item for you in this section.</span></span> <span data-ttu-id="a0596-214">Durante un tentativo di accesso a 8x8 Virtual Office viene creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="a0596-214">A new user is created during an attempt to access 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="a0596-215">Per creare un utente manualmente è necessario contattare il [team di supporto di 8x8 Virtual Office](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="a0596-215">If you need to create a user manually, you need to contact the [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a0596-216">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0596-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a0596-217">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="a0596-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 8x8 Virtual Office.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a0596-219">**Per assegnare Britta Simon a 8x8 Virtual Office, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a0596-219">**To assign Britta Simon to 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="a0596-220">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a0596-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a0596-222">Nell'elenco di applicazioni, selezionare **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="a0596-222">In the applications list, select **8x8 Virtual Office**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="a0596-224">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="a0596-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a0596-226">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a0596-226">Click **Add** button.</span></span> <span data-ttu-id="a0596-227">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a0596-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a0596-229">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="a0596-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a0596-230">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a0596-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a0596-231">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a0596-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a0596-232">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a0596-232">Testing single sign-on</span></span>

<span data-ttu-id="a0596-233">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a0596-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a0596-234">Quando si fa clic sul riquadro 8x8 Virtual Office nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="a0596-234">When you click the 8x8 Virtual Office tile in the Access Panel, you should get automatically signed-on to your 8x8 Virtual Office application.</span></span>
<span data-ttu-id="a0596-235">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a0596-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0596-236">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a0596-236">Additional resources</span></span>

* [<span data-ttu-id="a0596-237">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0596-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a0596-238">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0596-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

