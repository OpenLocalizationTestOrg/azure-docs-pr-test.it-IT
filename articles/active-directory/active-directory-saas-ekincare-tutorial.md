---
title: 'Esercitazione: Integrazione di Azure Active Directory con eKincare | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e eKincare.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 014eaff14974bb6cd551b6fe53409ede6a6dfea1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="8d714-103">Esercitazione: Integrazione di Azure Active Directory con eKincare</span><span class="sxs-lookup"><span data-stu-id="8d714-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="8d714-104">Questa esercitazione descrive come integrare eKincare con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d714-104">In this tutorial, you learn how to integrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d714-105">L'integrazione di eKincare con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d714-105">Integrating eKincare with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8d714-106">È possibile controllare in Azure AD chi può accedere a eKincare</span><span class="sxs-lookup"><span data-stu-id="8d714-106">You can control in Azure AD who has access to eKincare</span></span>
- <span data-ttu-id="8d714-107">È possibile abilitare gli utenti per l'accesso automatico a eKincare (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d714-107">You can enable your users to automatically get signed-on to eKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d714-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8d714-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8d714-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d714-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d714-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8d714-110">Prerequisites</span></span>

<span data-ttu-id="8d714-111">Per configurare l'integrazione di Azure AD con eKincare, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d714-111">To configure Azure AD integration with eKincare, you need the following items:</span></span>

- <span data-ttu-id="8d714-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d714-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d714-113">Sottoscrizione di eKincare abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8d714-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d714-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8d714-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d714-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d714-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d714-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8d714-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d714-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d714-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d714-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8d714-118">Scenario description</span></span>
<span data-ttu-id="8d714-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8d714-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d714-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d714-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d714-121">Aggiunta di eKincare dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8d714-121">Adding eKincare from the gallery</span></span>
2. <span data-ttu-id="8d714-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d714-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-the-gallery"></a><span data-ttu-id="8d714-123">Aggiunta di eKincare dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8d714-123">Adding eKincare from the gallery</span></span>
<span data-ttu-id="8d714-124">Per configurare l'integrazione di eKincare in Azure AD, è necessario aggiungere eKincare dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8d714-124">To configure the integration of eKincare into Azure AD, you need to add eKincare from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8d714-125">**Per aggiungere eKincare dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8d714-125">**To add eKincare from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8d714-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8d714-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8d714-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8d714-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8d714-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8d714-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8d714-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="8d714-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8d714-133">Nella casella di ricerca digitare **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="8d714-133">In the search box, type **eKincare**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="8d714-135">Nel pannello dei risultati selezionare **eKincare** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8d714-135">In the results panel, select **eKincare**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d714-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d714-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d714-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con eKincare con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8d714-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8d714-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di eKincare che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d714-139">For single sign-on to work, Azure AD needs to know what the counterpart user in eKincare is to a user in Azure AD.</span></span> <span data-ttu-id="8d714-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in eKincare.</span><span class="sxs-lookup"><span data-stu-id="8d714-140">In other words, a link relationship between an Azure AD user and the related user in eKincare needs to be established.</span></span>

<span data-ttu-id="8d714-141">Per stabilire la relazione di collegamento, in eKincare assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="8d714-141">In eKincare, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8d714-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con eKincare, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d714-142">To configure and test Azure AD single sign-on with eKincare, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8d714-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8d714-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8d714-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d714-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d714-145">**[Creazione di un utente di test di eKincare](#creating-a-ekincare-test-user)**: per avere una controparte di Britta Simon in eKincare collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d714-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - to have a counterpart of Britta Simon in eKincare that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d714-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d714-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d714-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="8d714-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d714-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d714-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d714-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione eKincare.</span><span class="sxs-lookup"><span data-stu-id="8d714-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="8d714-150">**Per configurare l'accesso Single Sign-On di Azure AD con eKincare, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8d714-150">**To configure Azure AD single sign-on with eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="8d714-151">Nella pagina di integrazione dell'applicazione **eKincare** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="8d714-151">In the Azure portal, on the **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8d714-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8d714-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="8d714-155">Nella sezione **URL e dominio eKincare** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8d714-155">On the **eKincare Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="8d714-157">a.</span><span class="sxs-lookup"><span data-stu-id="8d714-157">a.</span></span> <span data-ttu-id="8d714-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="8d714-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="8d714-159">b.</span><span class="sxs-lookup"><span data-stu-id="8d714-159">b.</span></span> <span data-ttu-id="8d714-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="8d714-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d714-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="8d714-161">These values are not real.</span></span> <span data-ttu-id="8d714-162">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="8d714-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="8d714-163">Per ottenere tali valori, contattare il [team di supporto di eKincare](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="8d714-163">Contact [eKincare support team](mailto:tech@ekincare.com) to get these values.</span></span>
 
4. <span data-ttu-id="8d714-164">L'applicazione eKincare prevede un formato specifico per le asserzioni SAML.</span><span class="sxs-lookup"><span data-stu-id="8d714-164">eKincare application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="8d714-165">Configurare le attestazioni seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="8d714-165">Configure the following claims for this application.</span></span> <span data-ttu-id="8d714-166">È possibile gestire i valori di questi attributi dalla sezione "**Attributi utente**" nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8d714-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="8d714-167">Lo screenshot seguente illustra un esempio di questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="8d714-167">The following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="8d714-168">Il nome dell'attestazione sarà sempre **"employeeid"**, con mapping del valore a user.extensionattribute1, che contiene il valore employeeid dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8d714-168">The claim name will always be **"employeeid"** and the value of which we have mapped to user.extensionattribute1, that contains the employeeid of the user.</span></span> <span data-ttu-id="8d714-169">Il nome delle altre due attestazioni,</span><span class="sxs-lookup"><span data-stu-id="8d714-169">The other two claims' name i.e</span></span> <span data-ttu-id="8d714-170">**"organizationid"** e **"organizationname"**, sarà sempre lo stesso e i relativi valori contengono, rispettivamente, i dettagli dell'organizzazione e dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8d714-170">**"organizationid"** and **"organizationname"** will always be same and their values contain the details of the organization of the user respectively.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="8d714-172">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come indicato nell'immagine precedente e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8d714-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="8d714-173">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="8d714-173">Attribute Name</span></span> | <span data-ttu-id="8d714-174">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="8d714-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="8d714-175">employeeid</span><span class="sxs-lookup"><span data-stu-id="8d714-175">employeeid</span></span> | <span data-ttu-id="8d714-176">*user.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="8d714-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="8d714-177">organizationid</span><span class="sxs-lookup"><span data-stu-id="8d714-177">organizationid</span></span> | <span data-ttu-id="8d714-178">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="8d714-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="8d714-179">organizationname</span><span class="sxs-lookup"><span data-stu-id="8d714-179">organizationname</span></span> | <span data-ttu-id="8d714-180">*user.companyname*</span><span class="sxs-lookup"><span data-stu-id="8d714-180">*user.companyname*</span></span> |

    <span data-ttu-id="8d714-181">a.</span><span class="sxs-lookup"><span data-stu-id="8d714-181">a.</span></span> <span data-ttu-id="8d714-182">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="8d714-182">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="8d714-185">b.</span><span class="sxs-lookup"><span data-stu-id="8d714-185">b.</span></span> <span data-ttu-id="8d714-186">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="8d714-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8d714-187">c.</span><span class="sxs-lookup"><span data-stu-id="8d714-187">c.</span></span> <span data-ttu-id="8d714-188">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="8d714-188">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8d714-189">d.</span><span class="sxs-lookup"><span data-stu-id="8d714-189">d.</span></span> <span data-ttu-id="8d714-190">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="8d714-190">Click **Ok**</span></span>

6. <span data-ttu-id="8d714-191">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="8d714-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="8d714-193">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8d714-193">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8d714-195">Per configurare l'accesso Single Sign-On sul lato **eKincare**, è necessario inviare il file di **XML metadati** scaricato al [team di supporto di eKincare](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="8d714-195">To configure single sign-on on **eKincare** side, you need to send the downloaded **Metadata XML** to [eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="8d714-196">Questa impostazione viene configurata in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="8d714-196">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8d714-197">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="8d714-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8d714-198">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="8d714-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8d714-199">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d714-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d714-200">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d714-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d714-201">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8d714-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8d714-203">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8d714-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8d714-204">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8d714-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d714-206">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="8d714-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d714-208">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="8d714-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d714-210">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8d714-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d714-212">a.</span><span class="sxs-lookup"><span data-stu-id="8d714-212">a.</span></span> <span data-ttu-id="8d714-213">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d714-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d714-214">b.</span><span class="sxs-lookup"><span data-stu-id="8d714-214">b.</span></span> <span data-ttu-id="8d714-215">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8d714-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d714-216">c.</span><span class="sxs-lookup"><span data-stu-id="8d714-216">c.</span></span> <span data-ttu-id="8d714-217">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="8d714-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8d714-218">d.</span><span class="sxs-lookup"><span data-stu-id="8d714-218">d.</span></span> <span data-ttu-id="8d714-219">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8d714-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="8d714-220">Creazione di un utente di test di eKincare</span><span class="sxs-lookup"><span data-stu-id="8d714-220">Creating a eKincare test user</span></span>

<span data-ttu-id="8d714-221">L'applicazione supporta il provisioning dell'utente just-in-time e dopo l'autenticazione gli utenti vengono automaticamente creati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8d714-221">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8d714-222">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d714-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8d714-223">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a eKincare.</span><span class="sxs-lookup"><span data-stu-id="8d714-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eKincare.</span></span>

![Assegna utente][200] 

<span data-ttu-id="8d714-225">**Per assegnare Britta Simon a eKincare, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8d714-225">**To assign Britta Simon to eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="8d714-226">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8d714-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8d714-228">Nell'elenco delle applicazioni selezionare **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="8d714-228">In the applications list, select **eKincare**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="8d714-230">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8d714-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8d714-232">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8d714-232">Click **Add** button.</span></span> <span data-ttu-id="8d714-233">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8d714-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8d714-235">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="8d714-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8d714-236">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8d714-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d714-237">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8d714-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d714-238">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8d714-238">Testing single sign-on</span></span>

<span data-ttu-id="8d714-239">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8d714-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8d714-240">Quando si fa clic sul riquadro eKincare nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione eKincare.</span><span class="sxs-lookup"><span data-stu-id="8d714-240">When you click the eKincare tile in the Access Panel, you should get automatically signed-on to your eKincare application.</span></span>
<span data-ttu-id="8d714-241">Per altre informazioni in proposito, vedere l'[introduzione al pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8d714-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d714-242">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8d714-242">Additional resources</span></span>

* [<span data-ttu-id="8d714-243">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d714-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d714-244">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d714-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

