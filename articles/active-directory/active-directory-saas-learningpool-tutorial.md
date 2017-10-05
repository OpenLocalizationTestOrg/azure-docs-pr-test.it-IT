---
title: 'Esercitazione: Integrazione di Azure Active Directory con Learningpool Act | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Learningpool Act.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 932f5f12c75299e532d3fa2c31f1805a7df30158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="b09bf-103">Esercitazione: Integrazione di Azure Active Directory con Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="b09bf-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="b09bf-104">Questa esercitazione descrive come integrare Learningpool Act con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b09bf-104">In this tutorial, you learn how to integrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b09bf-105">L'integrazione di Learningpool Act con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b09bf-105">Integrating Learningpool Act with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b09bf-106">È possibile controllare in Azure AD chi può accedere a Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="b09bf-106">You can control in Azure AD who has access to Learningpool Act</span></span>
- <span data-ttu-id="b09bf-107">È possibile abilitare gli utenti per l'accesso automatico a Learningpool Act (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="b09bf-107">You can enable your users to automatically get signed-on to Learningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b09bf-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b09bf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b09bf-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b09bf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b09bf-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b09bf-110">Prerequisites</span></span>

<span data-ttu-id="b09bf-111">Per configurare l'integrazione di Azure AD con Learningpool Act sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b09bf-111">To configure Azure AD integration with Learningpool Act, you need the following items:</span></span>

- <span data-ttu-id="b09bf-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b09bf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b09bf-113">Sottoscrizione di Learningpool Act abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b09bf-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b09bf-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b09bf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b09bf-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b09bf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b09bf-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b09bf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b09bf-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b09bf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b09bf-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b09bf-118">Scenario description</span></span>
<span data-ttu-id="b09bf-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b09bf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b09bf-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b09bf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b09bf-121">Aggiunta di Learningpool Act dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b09bf-121">Adding Learningpool Act from the gallery</span></span>
2. <span data-ttu-id="b09bf-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b09bf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-the-gallery"></a><span data-ttu-id="b09bf-123">Aggiunta di Learningpool Act dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b09bf-123">Adding Learningpool Act from the gallery</span></span>
<span data-ttu-id="b09bf-124">Per configurare l'integrazione di Learningpool Act in Azure AD, è necessario aggiungere Learningpool Act dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b09bf-124">To configure the integration of Learningpool Act into Azure AD, you need to add Learningpool Act from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b09bf-125">**Per aggiungere Learningpool Act dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b09bf-125">**To add Learningpool Act from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b09bf-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b09bf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b09bf-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b09bf-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b09bf-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="b09bf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b09bf-133">Nella casella di ricerca digitare **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-133">In the search box, type **Learningpool Act**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_search.png)

5. <span data-ttu-id="b09bf-135">Nel pannello dei risultati selezionare **Learningpool Act** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b09bf-135">In the results panel, select **Learningpool Act**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b09bf-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b09bf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b09bf-138">In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con Learningpool Act in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b09bf-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b09bf-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Learningpool Act che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b09bf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learningpool Act is to a user in Azure AD.</span></span> <span data-ttu-id="b09bf-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="b09bf-140">In other words, a link relationship between an Azure AD user and the related user in Learningpool Act needs to be established.</span></span>

<span data-ttu-id="b09bf-141">Per stabilire la relazione di collegamento, in Learningpool Act assegnare il valore di **nome utente** in Azure AD come valore dell'attributo **Nome utente**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-141">In Learningpool Act, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b09bf-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Learningpool Act, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b09bf-142">To configure and test Azure AD single sign-on with Learningpool Act, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b09bf-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b09bf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b09bf-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b09bf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b09bf-145">**[Creazione di un utente test di Learningpool Act](#creating-a-learningpool-act-test-user)**: per avere una controparte di Britta Simon in Learningpool Act collegata alla relativa rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b09bf-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - to have a counterpart of Britta Simon in Learningpool Act that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b09bf-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b09bf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b09bf-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="b09bf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b09bf-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b09bf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b09bf-149">In questa sezione si abilita l'accesso Single Sign-On di Azure AD nel portale di Azure e si configura l'accesso Single Sign-On nell'applicazione Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="b09bf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="b09bf-150">**Per configurare Single Sign-On di Azure AD con Learningpool Act, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b09bf-150">**To configure Azure AD single sign-on with Learningpool Act, perform the following steps:**</span></span>

1. <span data-ttu-id="b09bf-151">Nella pagina di integrazione dell'applicazione **Learningpool Act** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-151">In the Azure portal, on the **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b09bf-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b09bf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

3. <span data-ttu-id="b09bf-155">Nella sezione **URL e dominio Learningpool Act** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b09bf-155">On the **Learningpool Act Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="b09bf-157">a.</span><span class="sxs-lookup"><span data-stu-id="b09bf-157">a.</span></span> <span data-ttu-id="b09bf-158">Nella casella di testo **URL accesso** digitare l'URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span><span class="sxs-lookup"><span data-stu-id="b09bf-158">In the **Sign-on URL** textbox, type the URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="b09bf-159">b.</span><span class="sxs-lookup"><span data-stu-id="b09bf-159">b.</span></span> <span data-ttu-id="b09bf-160">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="b09bf-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="b09bf-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="b09bf-161">These values are not real.</span></span> <span data-ttu-id="b09bf-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="b09bf-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b09bf-163">Per ottenere questi valori, contattare il [team di supporto clienti di Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="b09bf-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="b09bf-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="b09bf-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

5. <span data-ttu-id="b09bf-166">L'applicazione Learningpool Act prevede che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="b09bf-166">Learningpool Act application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="b09bf-167">Configurare le attestazioni seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="b09bf-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="b09bf-168">È possibile gestire i valori di questi attributi dalla scheda **Attribute (Attributo)** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b09bf-168">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="b09bf-169">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="b09bf-169">The following screenshot shows an example for this.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

6. <span data-ttu-id="b09bf-171">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come illustrato nell'immagine e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b09bf-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="b09bf-172">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="b09bf-172">Attribute Name</span></span> | <span data-ttu-id="b09bf-173">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="b09bf-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="b09bf-174">urn:oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="b09bf-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="b09bf-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="b09bf-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="b09bf-176">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="b09bf-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="b09bf-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="b09bf-177">user.givenname</span></span> |
    | <span data-ttu-id="b09bf-178">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="b09bf-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="b09bf-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="b09bf-179">user.mail</span></span> |    
    | <span data-ttu-id="b09bf-180">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="b09bf-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="b09bf-181">user.surname</span><span class="sxs-lookup"><span data-stu-id="b09bf-181">user.surname</span></span> |
    
    <span data-ttu-id="b09bf-182">a.</span><span class="sxs-lookup"><span data-stu-id="b09bf-182">a.</span></span> <span data-ttu-id="b09bf-183">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="b09bf-186">b.</span><span class="sxs-lookup"><span data-stu-id="b09bf-186">b.</span></span> <span data-ttu-id="b09bf-187">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="b09bf-187">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="b09bf-188">c.</span><span class="sxs-lookup"><span data-stu-id="b09bf-188">c.</span></span> <span data-ttu-id="b09bf-189">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="b09bf-189">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="b09bf-190">d.</span><span class="sxs-lookup"><span data-stu-id="b09bf-190">d.</span></span> <span data-ttu-id="b09bf-191">Lasciare vuota la casella **Spazio dei nomi**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-191">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="b09bf-192">e.</span><span class="sxs-lookup"><span data-stu-id="b09bf-192">e.</span></span> <span data-ttu-id="b09bf-193">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-193">Click **Ok**.</span></span>

7. <span data-ttu-id="b09bf-194">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b09bf-194">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b09bf-196">Per configurare l'accesso Single Sign-On sul lato **Learningpool Act**, è necessario inviare il file di **XML metadati** scaricato al [team di supporto di Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="b09bf-196">To configure single sign-on on **Learningpool Act** side, you need to send the downloaded **Metadata XML** to [Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="b09bf-197">Questa impostazione viene configurata in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="b09bf-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b09bf-198">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b09bf-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b09bf-199">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="b09bf-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b09bf-200">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b09bf-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b09bf-201">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b09bf-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="b09bf-202">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b09bf-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b09bf-204">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b09bf-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b09bf-205">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b09bf-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b09bf-207">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="b09bf-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b09bf-209">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b09bf-211">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b09bf-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b09bf-213">a.</span><span class="sxs-lookup"><span data-stu-id="b09bf-213">a.</span></span> <span data-ttu-id="b09bf-214">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b09bf-215">b.</span><span class="sxs-lookup"><span data-stu-id="b09bf-215">b.</span></span> <span data-ttu-id="b09bf-216">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b09bf-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b09bf-217">c.</span><span class="sxs-lookup"><span data-stu-id="b09bf-217">c.</span></span> <span data-ttu-id="b09bf-218">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b09bf-219">d.</span><span class="sxs-lookup"><span data-stu-id="b09bf-219">d.</span></span> <span data-ttu-id="b09bf-220">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="b09bf-221">Creazione di un utente test di Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="b09bf-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="b09bf-222">Per consentire agli utenti di Azure AD di accedere a Learningpool Act, è necessario eseguirne il provisioning in Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="b09bf-222">To enable Azure AD users to log in to Learningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="b09bf-223">Non è richiesta alcuna operazione per configurare il provisioning degli utenti in Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="b09bf-223">There is no action item for you to configure user provisioning to Learningpool Act.</span></span>  
<span data-ttu-id="b09bf-224">Gli utenti dovranno essere creati dal [team di supporto di Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="b09bf-224">Users need to be created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="b09bf-225">È possibile usare qualsiasi altro strumento di creazione di account utente di Learningpool Act o le API fornite da Learningpool Act per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="b09bf-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b09bf-226">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b09bf-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b09bf-227">In questa sezione si abilita Britta Simon per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="b09bf-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learningpool Act.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b09bf-229">**Per assegnare Britta Simon a Learningpool Act, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b09bf-229">**To assign Britta Simon to Learningpool Act, perform the following steps:**</span></span>

1. <span data-ttu-id="b09bf-230">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b09bf-232">Nell'elenco di applicazioni selezionare **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-232">In the applications list, select **Learningpool Act**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_app.png) 

3. <span data-ttu-id="b09bf-234">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b09bf-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b09bf-236">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-236">Click **Add** button.</span></span> <span data-ttu-id="b09bf-237">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b09bf-239">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="b09bf-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b09bf-240">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b09bf-241">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b09bf-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b09bf-242">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b09bf-242">Testing single sign-on</span></span>

<span data-ttu-id="b09bf-243">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b09bf-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b09bf-244">Quando si fa clic sul riquadro Learningpool Act nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="b09bf-244">When you click the Learningpool Act tile in the Access Panel, you should get automatically signed-on to your Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b09bf-245">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b09bf-245">Additional resources</span></span>

* [<span data-ttu-id="b09bf-246">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b09bf-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b09bf-247">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b09bf-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_203.png

