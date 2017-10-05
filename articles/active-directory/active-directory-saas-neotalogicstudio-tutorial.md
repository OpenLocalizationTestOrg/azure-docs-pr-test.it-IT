---
title: 'Esercitazione: Integrazione di Azure Active Directory con Neota Logic Studio | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Neota Logic Studio.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: 99018277392cab44a6b579ad45b4611739a803d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="94f65-103">Esercitazione: Integrazione di Azure Active Directory con Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="94f65-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="94f65-104">Questa esercitazione descrive come integrare Neota Logic Studio con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94f65-104">In this tutorial, you learn how to integrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94f65-105">L'integrazione di Neota Logic Studio con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="94f65-105">Integrating Neota Logic Studio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="94f65-106">È possibile controllare in Azure AD chi può accedere a Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="94f65-106">You can control in Azure AD who has access to Neota Logic Studio</span></span>
- <span data-ttu-id="94f65-107">È possibile abilitare gli utenti per l'accesso automatico a Neota Logic Studio (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94f65-107">You can enable your users to automatically get signed-on to Neota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="94f65-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="94f65-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="94f65-109">Per altre informazioni sull'integrazione di app SaaS con Azure Active Directory, vedere:</span><span class="sxs-lookup"><span data-stu-id="94f65-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="94f65-110">[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="94f65-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94f65-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="94f65-111">Prerequisites</span></span>

<span data-ttu-id="94f65-112">Per configurare l'integrazione di Azure AD con Neota Logic Studio, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="94f65-112">To configure Azure AD integration with Neota Logic Studio, you need the following items:</span></span>

- <span data-ttu-id="94f65-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94f65-113">An Azure AD subscription</span></span>
- <span data-ttu-id="94f65-114">Sottoscrizione di Neota Logic Studio abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="94f65-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94f65-115">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="94f65-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94f65-116">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="94f65-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94f65-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="94f65-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94f65-118">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94f65-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94f65-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="94f65-119">Scenario description</span></span>

<span data-ttu-id="94f65-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="94f65-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94f65-121">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="94f65-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94f65-122">Aggiunta di Neota Logic Studio dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="94f65-122">Adding Neota Logic Studio from the gallery</span></span>
2. <span data-ttu-id="94f65-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94f65-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-the-gallery"></a><span data-ttu-id="94f65-124">Aggiunta di Neota Logic Studio dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="94f65-124">Adding Neota Logic Studio from the gallery</span></span>

<span data-ttu-id="94f65-125">Per configurare l'integrazione di Neota Logic Studio in Azure AD, è necessario aggiungere Neota Logic Studio dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="94f65-125">To configure the integration of Neota Logic Studio into Azure AD, you need to add Neota Logic Studio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="94f65-126">**Per aggiungere Neota Logic Studio dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="94f65-126">**To add Neota Logic Studio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="94f65-127">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="94f65-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="94f65-129">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="94f65-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="94f65-130">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="94f65-130">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="94f65-132">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="94f65-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="94f65-134">Nella casella di ricerca digitare **Neota Logic Studio**.</span><span class="sxs-lookup"><span data-stu-id="94f65-134">In the search box, type **Neota Logic Studio**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="94f65-136">Nel pannello dei risultati selezionare **Neota Logic Studio** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94f65-136">In the results panel, select **Neota Logic Studio**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="94f65-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94f65-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="94f65-139">In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con Neota Logic Studio con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="94f65-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="94f65-140">Per il corretto funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Neota Logic Studio che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94f65-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Neota Logic Studio is to a user in Azure AD.</span></span> <span data-ttu-id="94f65-141">Deve essere stabilita, in altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="94f65-141">In other words, a link relationship between an Azure AD user and the related user in Neota Logic Studio needs to be established.</span></span>

<span data-ttu-id="94f65-142">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** in Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="94f65-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="94f65-143">Per configurare e testare l'accesso Single Sign-On di Azure AD con Neota Logic Studio, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="94f65-143">To configure and test Azure AD single sign-on with Neota Logic Studio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="94f65-144">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="94f65-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="94f65-145">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94f65-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="94f65-146">**[Creazione di un utente test di Neota Logic Studio](#creating-a-neota-logic-studio-test-user)**: per avere una controparte di Britta Simon in Neota Logic Studio collegata alla rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="94f65-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - to have a counterpart of Britta Simon in Neota Logic Studio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="94f65-147">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94f65-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="94f65-148">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="94f65-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="94f65-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94f65-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="94f65-150">In questa sezione si abilita l'accesso Single Sign-On di Azure AD nel portale di Azure e si configura l'accesso Single Sign-On nell'applicazione Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="94f65-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="94f65-151">**Per configurare l'accesso Single Sign-On di Azure AD con Neota Logic Studio, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="94f65-151">**To configure Azure AD single sign-on with Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="94f65-152">Nella pagina di integrazione dell'applicazione **Neota Logic Studio** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="94f65-152">In the Azure portal, on the **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="94f65-154">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="94f65-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="94f65-156">Nella sezione **URL e dominio Neota Logic Studio** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="94f65-156">On the **Neota Logic Studio Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="94f65-158">a.</span><span class="sxs-lookup"><span data-stu-id="94f65-158">a.</span></span> <span data-ttu-id="94f65-159">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<sub domain>.neotalogic.com/a/<sub application>`.</span><span class="sxs-lookup"><span data-stu-id="94f65-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="94f65-160">b.</span><span class="sxs-lookup"><span data-stu-id="94f65-160">b.</span></span> <span data-ttu-id="94f65-161">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="94f65-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="94f65-162">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="94f65-162">These values are not the real.</span></span> <span data-ttu-id="94f65-163">è necessario aggiornarli con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="94f65-163">Update these values with the actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="94f65-164">In questo caso è consigliabile usare in Identificatore il valore univoco della stringa.</span><span class="sxs-lookup"><span data-stu-id="94f65-164">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="94f65-165">Per ottenere questi valori, contattare il [team di supporto clienti di Neota Logic Studio](https://www.neotalogic.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="94f65-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="94f65-166">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="94f65-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="94f65-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="94f65-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="94f65-170">Per ottenere la configurazione dell'accesso Single Sign-On per l'applicazione, contattare il [team di supporto di Neota Logic Studio](https://www.neotalogic.com/contact-us/) e fornire il file **XML metadati** scaricato.</span><span class="sxs-lookup"><span data-stu-id="94f65-170">To get SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="94f65-171">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="94f65-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="94f65-172">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="94f65-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="94f65-173">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94f65-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="94f65-174">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94f65-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="94f65-175">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="94f65-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="94f65-177">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="94f65-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="94f65-178">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="94f65-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="94f65-180">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="94f65-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="94f65-182">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="94f65-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="94f65-184">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="94f65-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="94f65-186">a.</span><span class="sxs-lookup"><span data-stu-id="94f65-186">a.</span></span> <span data-ttu-id="94f65-187">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="94f65-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94f65-188">b.</span><span class="sxs-lookup"><span data-stu-id="94f65-188">b.</span></span> <span data-ttu-id="94f65-189">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="94f65-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="94f65-190">c.</span><span class="sxs-lookup"><span data-stu-id="94f65-190">c.</span></span> <span data-ttu-id="94f65-191">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="94f65-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="94f65-192">d.</span><span class="sxs-lookup"><span data-stu-id="94f65-192">d.</span></span> <span data-ttu-id="94f65-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="94f65-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="94f65-194">Creazione di un utente test di Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="94f65-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="94f65-195">In questa sezione si crea un utente di nome Britta Simon in Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="94f65-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="94f65-196">Collaborare con il [team di supporto clienti di Neota Logic Studio](https://www.neotalogic.com/contact-us/) per aggiungere gli utenti nella piattaforma Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="94f65-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add the users in the Neota Logic Studio platform.</span></span> <span data-ttu-id="94f65-197">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="94f65-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="94f65-198">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94f65-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="94f65-199">In questa sezione si abilita Britta Simon per l'uso dell'accesso Single Sign-On di Azure, concedendole l'accesso a Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="94f65-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Neota Logic Studio.</span></span>

![Assegna utente][200] 

<span data-ttu-id="94f65-201">**Per assegnare Britta Simon a Neota Logic Studio, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="94f65-201">**To assign Britta Simon to Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="94f65-202">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="94f65-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="94f65-204">Nell'elenco di applicazioni selezionare **Neota Logic Studio**.</span><span class="sxs-lookup"><span data-stu-id="94f65-204">In the applications list, select **Neota Logic Studio**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="94f65-206">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="94f65-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="94f65-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="94f65-208">Click **Add** button.</span></span> <span data-ttu-id="94f65-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="94f65-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="94f65-211">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="94f65-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="94f65-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="94f65-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="94f65-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="94f65-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="94f65-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="94f65-214">Testing single sign-on</span></span>

<span data-ttu-id="94f65-215">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="94f65-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="94f65-216">Fare clic sul riquadro Neota Logic Studio nel pannello di accesso e si verrà reindirizzati alla pagina di accesso dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="94f65-216">Click the Neota Logic Studio tile in the Access Panel, you will be redirected to Organization sign-on page.</span></span> <span data-ttu-id="94f65-217">Dopo aver eseguito l'accesso, si verrà registrati nell'applicazione Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="94f65-217">After successful login, you will be signed-on to your Neota Logic Studio application.</span></span> <span data-ttu-id="94f65-218">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="94f65-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="94f65-219">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="94f65-219">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="94f65-220">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="94f65-220">Additional resources</span></span>

* [<span data-ttu-id="94f65-221">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94f65-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="94f65-222">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94f65-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png

