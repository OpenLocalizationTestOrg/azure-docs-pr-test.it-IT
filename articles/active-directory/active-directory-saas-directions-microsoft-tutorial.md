---
title: 'Esercitazione: Integrazione di Azure Active Directory con Directions on Microsoft | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Directions on Microsoft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f9c068c71eb00a4c779c91c8ee0f0dc9d6ba85ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="013c7-103">Esercitazione: Integrazione di Azure Active Directory con Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="013c7-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>

<span data-ttu-id="013c7-104">Questa esercitazione descrive come integrare Directions on Microsoft con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="013c7-104">In this tutorial, you learn how to integrate Directions on Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="013c7-105">L'integrazione di Directions on Microsoft con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="013c7-105">Integrating Directions on Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="013c7-106">È possibile controllare in Azure AD chi può accedere a Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="013c7-106">You can control in Azure AD who has access to Directions on Microsoft</span></span>
- <span data-ttu-id="013c7-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a Directions on Microsoft con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="013c7-107">You can enable your users to automatically get signed-on to Directions on Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="013c7-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="013c7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="013c7-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="013c7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="013c7-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="013c7-110">Prerequisites</span></span>

<span data-ttu-id="013c7-111">Per configurare l'integrazione di Azure AD con Directions on Microsoft sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="013c7-111">To configure Azure AD integration with Directions on Microsoft, you need the following items:</span></span>

- <span data-ttu-id="013c7-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="013c7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="013c7-113">Sottoscrizione di Directions on Microsoft abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="013c7-113">A Directions on Microsoft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="013c7-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="013c7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="013c7-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="013c7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="013c7-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="013c7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="013c7-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="013c7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="013c7-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="013c7-118">Scenario description</span></span>
<span data-ttu-id="013c7-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="013c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="013c7-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="013c7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="013c7-121">Aggiunta di Directions on Microsoft dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="013c7-121">Adding Directions on Microsoft from the gallery</span></span>
2. <span data-ttu-id="013c7-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="013c7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-directions-on-microsoft-from-the-gallery"></a><span data-ttu-id="013c7-123">Aggiunta di Directions on Microsoft dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="013c7-123">Adding Directions on Microsoft from the gallery</span></span>
<span data-ttu-id="013c7-124">Per configurare l'integrazione di Directions on Microsoft in Azure AD è necessario aggiungere Directions on Microsoft dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="013c7-124">To configure the integration of Directions on Microsoft into Azure AD, you need to add Directions on Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="013c7-125">**Per aggiungere Directions on Microsoft dalla raccolta seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="013c7-125">**To add Directions on Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="013c7-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="013c7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="013c7-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="013c7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="013c7-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="013c7-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="013c7-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="013c7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="013c7-133">Nella casella di ricerca digitare **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="013c7-133">In the search box, type **Directions on Microsoft**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_search.png)

5. <span data-ttu-id="013c7-135">Nel riquadro dei risultati selezionare **Directions on Microsoft** e quindi fare clic su **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="013c7-135">In the results panel, select **Directions on Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="013c7-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="013c7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="013c7-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Directions on Microsoft mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="013c7-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="013c7-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Directions on Microsoft corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="013c7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Directions on Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="013c7-140">In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="013c7-140">In other words, a link relationship between an Azure AD user and the related user in Directions on Microsoft needs to be established.</span></span>

<span data-ttu-id="013c7-141">Per stabilire la relazione di collegamento, in Directions on Microsoft assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="013c7-141">In Directions on Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="013c7-142">Per configurare e testare l'accesso Single Sign-On di Microsoft Azure AD con Directions on Microsoft è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="013c7-142">To configure and test Azure AD single sign-on with Directions on Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="013c7-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="013c7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="013c7-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="013c7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="013c7-145">**[Creazione di un utente test di Directions on Microsoft](#creating-a-directions-on-microsoft-test-user)**: per avere una controparte di Britta Simon in Directions on Microsoft collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="013c7-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - to have a counterpart of Britta Simon in Directions on Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="013c7-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="013c7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="013c7-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="013c7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="013c7-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="013c7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="013c7-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="013c7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Directions on Microsoft application.</span></span>

<span data-ttu-id="013c7-150">**Per configurare l'accesso Single Sign-On di Azure AD con Directions on Microsoft, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="013c7-150">**To configure Azure AD single sign-on with Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="013c7-151">Nella pagina di integrazione dell'applicazione **Directions on Microsoft** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="013c7-151">In the Azure portal, on the **Directions on Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="013c7-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="013c7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_samlbase.png)

3. <span data-ttu-id="013c7-155">Nella sezione **URL e dominio Directions on Microsoft** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="013c7-155">On the **Directions on Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_url.png)

    <span data-ttu-id="013c7-157">a.</span><span class="sxs-lookup"><span data-stu-id="013c7-157">a.</span></span> <span data-ttu-id="013c7-158">Nella casella di testo **URL di accesso** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="013c7-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://www.directionsonmicrosoft.com/user/login` |
    | `https://<subdomain>.devcloud.acquia-sites.com/<companyname>` |

    <span data-ttu-id="013c7-159">b.</span><span class="sxs-lookup"><span data-stu-id="013c7-159">b.</span></span> <span data-ttu-id="013c7-160">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="013c7-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://rhelmdirectionsonmicrosoftcomtest.devcloud.acquia-sites.com/simplesaml/<companyname>` |
    | `https://www.directionsonmicrosoft.com/simplesaml/<companyname>` |

    > [!NOTE] 
    > <span data-ttu-id="013c7-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="013c7-161">These values are not real.</span></span> <span data-ttu-id="013c7-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="013c7-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="013c7-163">Per ottenere questi valori contattare il [team di supporto clienti di Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="013c7-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) to get these values.</span></span> 
 
4. <span data-ttu-id="013c7-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="013c7-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_certificate.png) 

5. <span data-ttu-id="013c7-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="013c7-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="013c7-168">Per configurare l'accesso Single Sign-On sul lato **Directions on Microsoft** è necessario inviare il file **XML metadati** scaricato al [team di supporto di Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="013c7-168">To configure single sign-on on **Directions on Microsoft** side, you need to send the downloaded **Metadata XML** to [Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="013c7-169">Per consentire al team di supporto di Directions on Microsoft di trovare l'appartenenza al sito federato, includere nel messaggio di posta elettronica le informazioni relative alla società.</span><span class="sxs-lookup"><span data-stu-id="013c7-169">To enable the Directions on Microsoft support team to locate your federated site membership, include your company information in your email.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="013c7-170">L'accesso Single Sign-On per Directions on Microsoft deve essere abilitato dal [team di supporto clienti di Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="013c7-170">Single sign-on for Directions on Microsoft needs to be enabled by the [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="013c7-171">Quando l'accesso Single Sign-On verrà abilitato, si riceverà una notifica.</span><span class="sxs-lookup"><span data-stu-id="013c7-171">You will receive a notification when single sign-on has been enabled.</span></span>

> [!TIP]
> <span data-ttu-id="013c7-172">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="013c7-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="013c7-173">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="013c7-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="013c7-174">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="013c7-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="013c7-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="013c7-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="013c7-176">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="013c7-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="013c7-178">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="013c7-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="013c7-179">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="013c7-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="013c7-181">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="013c7-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="013c7-183">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="013c7-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="013c7-185">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="013c7-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="013c7-187">a.</span><span class="sxs-lookup"><span data-stu-id="013c7-187">a.</span></span> <span data-ttu-id="013c7-188">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="013c7-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="013c7-189">b.</span><span class="sxs-lookup"><span data-stu-id="013c7-189">b.</span></span> <span data-ttu-id="013c7-190">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="013c7-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="013c7-191">c.</span><span class="sxs-lookup"><span data-stu-id="013c7-191">c.</span></span> <span data-ttu-id="013c7-192">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="013c7-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="013c7-193">d.</span><span class="sxs-lookup"><span data-stu-id="013c7-193">d.</span></span> <span data-ttu-id="013c7-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="013c7-194">Click **Create**.</span></span>
 
### <a name="creating-a-directions-on-microsoft-test-user"></a><span data-ttu-id="013c7-195">Creazione di un utente test di Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="013c7-195">Creating a Directions on Microsoft test user</span></span>

<span data-ttu-id="013c7-196">Non è richiesto alcun intervento dell'utente per configurare il provisioning degli utenti in Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="013c7-196">There is no action item for you to configure user provisioning to Directions on Microsoft.</span></span>  

<span data-ttu-id="013c7-197">Quando un utente assegnato prova ad accedere a Directions on Microsoft usando il pannello di accesso, Directions on Microsoft verifica se l'utente esiste.</span><span class="sxs-lookup"><span data-stu-id="013c7-197">When an assigned user tries to log in to Directions on Microsoft using the access panel, Directions on Microsoft checks whether the user exists.</span></span> <span data-ttu-id="013c7-198">Se l'account utente non è presente, Directions on Microsoft lo crea automaticamente.</span><span class="sxs-lookup"><span data-stu-id="013c7-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="013c7-199">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="013c7-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="013c7-200">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Directions in Microsoft.</span><span class="sxs-lookup"><span data-stu-id="013c7-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Directions on Microsoft.</span></span>

![Assegna utente][200] 

<span data-ttu-id="013c7-202">**Per assegnare Britta Simon a Directions on Microsoft, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="013c7-202">**To assign Britta Simon to Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="013c7-203">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="013c7-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="013c7-205">Nell'elenco delle applicazioni selezionare **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="013c7-205">In the applications list, select **Directions on Microsoft**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_app.png) 

3. <span data-ttu-id="013c7-207">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="013c7-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="013c7-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="013c7-209">Click **Add** button.</span></span> <span data-ttu-id="013c7-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="013c7-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="013c7-212">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="013c7-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="013c7-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="013c7-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="013c7-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="013c7-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="013c7-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="013c7-215">Testing single sign-on</span></span>

<span data-ttu-id="013c7-216">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="013c7-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="013c7-217">Quando si fa clic sul riquadro Directions on Microsoft nel pannello di accesso si accede automaticamente all'applicazione Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="013c7-217">When you click the Directions on Microsoft tile in the Access Panel, you should get automatically signed-on to your Directions on Microsoft application.</span></span>

<span data-ttu-id="013c7-218">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="013c7-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="013c7-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="013c7-219">Additional resources</span></span>

* [<span data-ttu-id="013c7-220">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="013c7-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="013c7-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="013c7-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_203.png

