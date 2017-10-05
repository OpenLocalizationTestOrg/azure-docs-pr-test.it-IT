---
title: 'Esercitazione: Integrazione di Azure Active Directory con Deputy | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Deputy.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 51aed908208b7a40ea2ab710dffe84370b573991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="ae649-103">Esercitazione: Integrazione di Azure Active Directory con Deputy</span><span class="sxs-lookup"><span data-stu-id="ae649-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="ae649-104">Questa esercitazione descrive come integrare Deputy con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae649-104">In this tutorial, you learn how to integrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae649-105">L'integrazione di Deputy con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ae649-105">Integrating Deputy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae649-106">È possibile controllare in Azure AD chi può accedere a Deputy</span><span class="sxs-lookup"><span data-stu-id="ae649-106">You can control in Azure AD who has access to Deputy</span></span>
- <span data-ttu-id="ae649-107">È possibile abilitare gli utenti per l'accesso automatico a Deputy (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae649-107">You can enable your users to automatically get signed-on to Deputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae649-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae649-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ae649-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae649-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae649-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ae649-110">Prerequisites</span></span>

<span data-ttu-id="ae649-111">Per configurare l'integrazione di Azure AD con Deputy, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ae649-111">To configure Azure AD integration with Deputy, you need the following items:</span></span>

- <span data-ttu-id="ae649-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae649-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae649-113">Sottoscrizione di Deputy abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ae649-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae649-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ae649-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae649-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ae649-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae649-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ae649-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae649-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae649-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae649-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ae649-118">Scenario description</span></span>
<span data-ttu-id="ae649-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ae649-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae649-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ae649-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae649-121">Aggiunta di Deputy dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ae649-121">Adding Deputy from the gallery</span></span>
2. <span data-ttu-id="ae649-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae649-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-the-gallery"></a><span data-ttu-id="ae649-123">Aggiunta di Deputy dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ae649-123">Adding Deputy from the gallery</span></span>
<span data-ttu-id="ae649-124">Per configurare l'integrazione di Deputy in Azure AD, è necessario aggiungere Deputy dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ae649-124">To configure the integration of Deputy into Azure AD, you need to add Deputy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae649-125">**Per aggiungere Deputy dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ae649-125">**To add Deputy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae649-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="ae649-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae649-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ae649-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ae649-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ae649-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="ae649-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="ae649-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="ae649-133">Nella casella di ricerca digitare **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="ae649-133">In the search box, type **Deputy**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="ae649-135">Nel pannello dei risultati selezionare **Deputy** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ae649-135">In the results panel, select **Deputy**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae649-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae649-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae649-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Deputy mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ae649-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ae649-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Deputy corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae649-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Deputy is to a user in Azure AD.</span></span> <span data-ttu-id="ae649-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Deputy.</span><span class="sxs-lookup"><span data-stu-id="ae649-140">In other words, a link relationship between an Azure AD user and the related user in Deputy needs to be established.</span></span>

<span data-ttu-id="ae649-141">Per stabilire la relazione di collegamento, in Deputy assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="ae649-141">In Deputy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ae649-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Deputy, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ae649-142">To configure and test Azure AD single sign-on with Deputy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae649-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ae649-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ae649-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae649-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae649-145">**[Creazione di un utente test di Deputy](#creating-a-deputy-test-user)**: per avere una controparte di Britta Simon in Deputy collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae649-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - to have a counterpart of Britta Simon in Deputy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae649-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae649-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae649-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="ae649-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae649-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae649-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae649-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Deputy.</span><span class="sxs-lookup"><span data-stu-id="ae649-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="ae649-150">**Per configurare Single Sign-On di Azure AD con Deputy, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ae649-150">**To configure Azure AD single sign-on with Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="ae649-151">Nella pagina di integrazione dell'applicazione **Deputy** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="ae649-151">In the Azure portal, on the **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="ae649-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="ae649-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="ae649-155">Nella sezione **URL e dominio Deputy** per configurare l'applicazione in modalità avviata da **IDP**:</span><span class="sxs-lookup"><span data-stu-id="ae649-155">On the **Deputy Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="ae649-157">a.</span><span class="sxs-lookup"><span data-stu-id="ae649-157">a.</span></span> <span data-ttu-id="ae649-158">Nella casella di testo **Identificatore** digitare l'URL adottando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="ae649-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="ae649-159">b.</span><span class="sxs-lookup"><span data-stu-id="ae649-159">b.</span></span> <span data-ttu-id="ae649-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="ae649-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="ae649-161">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="ae649-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="ae649-162">se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="ae649-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="ae649-164">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="ae649-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="ae649-165">Il suffisso di area di Deputy è facoltativo. Se usato deve essere uno dei seguenti: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span><span class="sxs-lookup"><span data-stu-id="ae649-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae649-166">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="ae649-166">These values are not real.</span></span> <span data-ttu-id="ae649-167">aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="ae649-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="ae649-168">Per ottenere questi valori contattare il [team di supporto di Deputy](https://www.deputy.com/call-centers-customer-support-scheduling-software).</span><span class="sxs-lookup"><span data-stu-id="ae649-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) to get these values.</span></span> 

5. <span data-ttu-id="ae649-169">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="ae649-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="ae649-171">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ae649-171">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="ae649-173">Nella sezione **Configurazione di Deputy** fare clic su **Configura Deputy** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="ae649-173">On the **Deputy Configuration** section, click **Configure Deputy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ae649-174">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="ae649-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="ae649-176">Accedere all'URL seguente: [https://(sottodominio-utente).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="ae649-176">Navigate to the following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="ae649-177">Passare a **Security Settings**(Impostazioni di sicurezza) e fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="ae649-177">Go to **Security Settings** and click **Edit**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="ae649-179">In questa pagina **Security Settings** (Impostazioni di sicurezza) attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="ae649-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="ae649-181">a.</span><span class="sxs-lookup"><span data-stu-id="ae649-181">a.</span></span> <span data-ttu-id="ae649-182">Abilitare **Social Login**(Accesso social).</span><span class="sxs-lookup"><span data-stu-id="ae649-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="ae649-183">b.</span><span class="sxs-lookup"><span data-stu-id="ae649-183">b.</span></span> <span data-ttu-id="ae649-184">Aprire il certificato con codifica Base 64 scaricato dal portale di Azure nel Blocco note, copiarne il contenuto negli Appunti e quindi incollarlo nella casella di testo **OpenSSL Certificate** (Certificato OpenSSL).</span><span class="sxs-lookup"><span data-stu-id="ae649-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="ae649-185">c.</span><span class="sxs-lookup"><span data-stu-id="ae649-185">c.</span></span> <span data-ttu-id="ae649-186">Nella casella di testo URL SSO SAML digitare `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="ae649-186">In the SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="ae649-187">d.</span><span class="sxs-lookup"><span data-stu-id="ae649-187">d.</span></span> <span data-ttu-id="ae649-188">Nella casella di testo URL SSO SAML sostituire `<your subdomain>` con il sottodominio.</span><span class="sxs-lookup"><span data-stu-id="ae649-188">In the SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="ae649-189">e.</span><span class="sxs-lookup"><span data-stu-id="ae649-189">e.</span></span> <span data-ttu-id="ae649-190">Nella casella di testo URL SSO SAML sostituire `<saml sso url>` con il valore **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae649-190">In the SAML SSO URL textbox, replace `<saml sso url>` with the **SAML Single Sign-On Service URL** you have copied from the Azure portal.</span></span>
   
    <span data-ttu-id="ae649-191">f.</span><span class="sxs-lookup"><span data-stu-id="ae649-191">f.</span></span> <span data-ttu-id="ae649-192">Fare clic su **Salva impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="ae649-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="ae649-193">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="ae649-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ae649-194">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="ae649-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ae649-195">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae649-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae649-196">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae649-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae649-197">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae649-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="ae649-199">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ae649-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae649-200">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="ae649-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae649-202">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="ae649-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae649-204">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="ae649-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae649-206">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ae649-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae649-208">a.</span><span class="sxs-lookup"><span data-stu-id="ae649-208">a.</span></span> <span data-ttu-id="ae649-209">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae649-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae649-210">b.</span><span class="sxs-lookup"><span data-stu-id="ae649-210">b.</span></span> <span data-ttu-id="ae649-211">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae649-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae649-212">c.</span><span class="sxs-lookup"><span data-stu-id="ae649-212">c.</span></span> <span data-ttu-id="ae649-213">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="ae649-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ae649-214">d.</span><span class="sxs-lookup"><span data-stu-id="ae649-214">d.</span></span> <span data-ttu-id="ae649-215">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ae649-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="ae649-216">Creazione di un utente test di Deputy</span><span class="sxs-lookup"><span data-stu-id="ae649-216">Creating a Deputy test user</span></span>

<span data-ttu-id="ae649-217">Per consentire agli utenti di Azure AD di accedere a Deputy è necessario eseguire il provisioning degli utenti in Deputy.</span><span class="sxs-lookup"><span data-stu-id="ae649-217">To enable Azure AD users to log in to Deputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="ae649-218">Nel caso di Deputy il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="ae649-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="ae649-219">Per eseguire il provisioning di un account utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ae649-219">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="ae649-220">Accedere al sito aziendale di Deputy come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ae649-220">Log in to your Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="ae649-221">Nel pannello di navigazione in alto fare clic su **People**(Persone).</span><span class="sxs-lookup"><span data-stu-id="ae649-221">On the top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="ae649-222">![Persone](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="ae649-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="ae649-223">Fare clic su **Add People** (Aggiungi persone) e quindi su **Add a single person** (Aggiungi una singola persona).</span><span class="sxs-lookup"><span data-stu-id="ae649-223">Click the **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="ae649-224">![Aggiungere persone](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Aggiungere persone")</span><span class="sxs-lookup"><span data-stu-id="ae649-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="ae649-225">Eseguire i passaggi seguenti e fare clic su **Save & Invite** (Salva e invita).</span><span class="sxs-lookup"><span data-stu-id="ae649-225">Perform the following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="ae649-226">![Nuovo utente](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="ae649-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="ae649-227">a.</span><span class="sxs-lookup"><span data-stu-id="ae649-227">a.</span></span> <span data-ttu-id="ae649-228">Nella casella di testo **Name** (Nome) digitare il nome dell'utente, ad esempio **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae649-228">In the **Name** textbox, type name of the user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="ae649-229">b.</span><span class="sxs-lookup"><span data-stu-id="ae649-229">b.</span></span> <span data-ttu-id="ae649-230">Nella casella di testo **Email** (Indirizzo di posta elettronica) digitare l'indirizzo di posta elettronica dell'account Azure AD di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="ae649-230">In the **Email** textbox, type the email address of an Azure AD account you want to provision.</span></span>
   
   <span data-ttu-id="ae649-231">c.</span><span class="sxs-lookup"><span data-stu-id="ae649-231">c.</span></span> <span data-ttu-id="ae649-232">Nella casella di testo **Work at** (Lavora presso) digitare il nome dell'azienda.</span><span class="sxs-lookup"><span data-stu-id="ae649-232">In the **Work at** textbox, type the business name.</span></span>
   
   <span data-ttu-id="ae649-233">d.</span><span class="sxs-lookup"><span data-stu-id="ae649-233">d.</span></span> <span data-ttu-id="ae649-234">Fare clic sul pulsante **Save & Invite** (Salva e invita).</span><span class="sxs-lookup"><span data-stu-id="ae649-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="ae649-235">Il titolare dell'account Azure Active Directory riceve un messaggio di posta elettronica e fa clic su un collegamento per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="ae649-235">The AAD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="ae649-236">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Deputy per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="ae649-236">You can use any other Deputy user account creation tools or APIs provided by Deputy to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ae649-237">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae649-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ae649-238">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Deputy.</span><span class="sxs-lookup"><span data-stu-id="ae649-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Deputy.</span></span>

![Assegna utente][200] 

<span data-ttu-id="ae649-240">**Per assegnare Britta Simon a Deputy, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ae649-240">**To assign Britta Simon to Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="ae649-241">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ae649-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ae649-243">Nell'elenco di applicazioni selezionare **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="ae649-243">In the applications list, select **Deputy**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="ae649-245">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="ae649-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="ae649-247">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ae649-247">Click **Add** button.</span></span> <span data-ttu-id="ae649-248">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ae649-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="ae649-250">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="ae649-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ae649-251">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ae649-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae649-252">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ae649-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae649-253">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ae649-253">Testing single sign-on</span></span>

<span data-ttu-id="ae649-254">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ae649-254">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="ae649-255">Quando si fa clic sul riquadro Deputy nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Deputy.</span><span class="sxs-lookup"><span data-stu-id="ae649-255">When you click the Deputy tile in the Access Panel, you should get automatically signed-on to your Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae649-256">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ae649-256">Additional resources</span></span>

* [<span data-ttu-id="ae649-257">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae649-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae649-258">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae649-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

