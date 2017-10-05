---
title: 'Esercitazione: Integrazione di Azure Active Directory con Printix | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Printix.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 97dbb3fa0531f2f679badb6bb9752f2e42fc9cb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="dc93c-103">Esercitazione: Integrazione di Azure Active Directory con Printix</span><span class="sxs-lookup"><span data-stu-id="dc93c-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="dc93c-104">Questa esercitazione descrive come integrare Printix con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc93c-104">In this tutorial, you learn how to integrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc93c-105">L'integrazione di Printix con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dc93c-105">Integrating Printix with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dc93c-106">È possibile controllare in Azure AD chi può accedere a Printix</span><span class="sxs-lookup"><span data-stu-id="dc93c-106">You can control in Azure AD who has access to Printix</span></span>
- <span data-ttu-id="dc93c-107">È possibile abilitare gli utenti per l'accesso automatico a Printix (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc93c-107">You can enable your users to automatically get signed-on to Printix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dc93c-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc93c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dc93c-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dc93c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc93c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dc93c-110">Prerequisites</span></span>

<span data-ttu-id="dc93c-111">Per configurare l'integrazione di Azure AD con Printix sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dc93c-111">To configure Azure AD integration with Printix, you need the following items:</span></span>

- <span data-ttu-id="dc93c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc93c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc93c-113">Sottoscrizione di Printix abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dc93c-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc93c-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="dc93c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc93c-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="dc93c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc93c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="dc93c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dc93c-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc93c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc93c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="dc93c-118">Scenario description</span></span>
<span data-ttu-id="dc93c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="dc93c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc93c-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="dc93c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc93c-121">Aggiunta di Printix dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="dc93c-121">Adding Printix from the gallery</span></span>
2. <span data-ttu-id="dc93c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc93c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-the-gallery"></a><span data-ttu-id="dc93c-123">Aggiunta di Printix dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="dc93c-123">Adding Printix from the gallery</span></span>
<span data-ttu-id="dc93c-124">Per configurare l'integrazione di Printix in Azure AD è necessario aggiungere Printix dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="dc93c-124">To configure the integration of Printix into Azure AD, you need to add Printix from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dc93c-125">**Per aggiungere Printix dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dc93c-125">**To add Printix from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dc93c-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="dc93c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dc93c-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dc93c-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="dc93c-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="dc93c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="dc93c-133">Nella casella di ricerca digitare **Printix**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-133">In the search box, type **Printix**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="dc93c-135">Nel pannello dei risultati selezionare **Printix** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dc93c-135">In the results panel, select **Printix**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dc93c-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc93c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dc93c-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Printix con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dc93c-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dc93c-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Printix che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc93c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Printix is to a user in Azure AD.</span></span> <span data-ttu-id="dc93c-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Printix.</span><span class="sxs-lookup"><span data-stu-id="dc93c-140">In other words, a link relationship between an Azure AD user and the related user in Printix needs to be established.</span></span>

<span data-ttu-id="dc93c-141">Per stabilire la relazione di collegamento, in Printix assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="dc93c-141">In Printix, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dc93c-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Printix è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="dc93c-142">To configure and test Azure AD single sign-on with Printix, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dc93c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="dc93c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dc93c-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc93c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dc93c-145">**[Creazione di un utente test di Printix](#creating-a-printix-test-user)**: per avere una controparte di Britta Simon in Printix collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc93c-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - to have a counterpart of Britta Simon in Printix that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dc93c-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc93c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dc93c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="dc93c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dc93c-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc93c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dc93c-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Printix.</span><span class="sxs-lookup"><span data-stu-id="dc93c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="dc93c-150">**Per configurare l'accesso Single Sign-On di Azure AD con Printix, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dc93c-150">**To configure Azure AD single sign-on with Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="dc93c-151">Nella pagina di integrazione dell'applicazione **Printix** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-151">In the Azure portal, on the **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="dc93c-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="dc93c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="dc93c-155">Nella sezione **URL e dominio Printix** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dc93c-155">On the **Printix Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="dc93c-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="dc93c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dc93c-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="dc93c-158">The value is not real.</span></span> <span data-ttu-id="dc93c-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="dc93c-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="dc93c-160">Per ottenere tale valore, contattare il [team di supporto clienti di Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="dc93c-160">Contact [Printix Client support team](mailto:support@printix.net) to get the value.</span></span> 
 
4. <span data-ttu-id="dc93c-161">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="dc93c-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="dc93c-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="dc93c-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dc93c-165">Accedere al tenant di Printix come amministratore.</span><span class="sxs-lookup"><span data-stu-id="dc93c-165">Sign-on to your Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="dc93c-166">Nel menu in alto, fare clic sull'icona nell'angolo superiore destro e selezionare "**Authentication**" (Autenticazione).</span><span class="sxs-lookup"><span data-stu-id="dc93c-166">In the menu on the top, click the icon at the upper right corner and select "**Authentication**".</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="dc93c-168">Nella scheda **Setup** (Configurazione) selezionare **Enable Azure/Office 365 authentication** (Abilita autenticazione Azure/Office 365)</span><span class="sxs-lookup"><span data-stu-id="dc93c-168">On the **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="dc93c-170">Nella scheda **Azure**, immettere l'URL dei metadati della federazione nella casella di testo "**Federation metadata document**" (Documento metadati federazione).</span><span class="sxs-lookup"><span data-stu-id="dc93c-170">On the **Azure** tab, input federation metadata URL to the textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="dc93c-171">Allegare il file dei metadati con estensione xml scaricato da Azure AD e inviarlo al [team di supporto Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="dc93c-171">Attach the metadata xml file which you downloaded from Azure AD to [Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="dc93c-172">Il team carica il file con estensione xml e metterà a disposizione un URL di metadati di federazione.</span><span class="sxs-lookup"><span data-stu-id="dc93c-172">Then they upload the xml file and provide a federation metadata URL.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="dc93c-174">Fare clic sul pulsante "**Test**" e quindi su "**OK**", se il test ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="dc93c-174">Click the "**Test**" button and click "**OK**" button if the test was successful.</span></span>
   
     <span data-ttu-id="dc93c-175">Dopo aver fatto clic sul pulsante **test** verrà visualizzata la pagina di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dc93c-175">Azure active directory page will show after clicking the **test** button.</span></span> <span data-ttu-id="dc93c-176">In questo caso, "esito positivo" significa che dopo aver immesso le credenziali dell'account di test di Azure verrà visualizzato un messaggio "Settings tested OK" (Il test delle impostazioni è riuscito). Fare clic sul pulsante **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-176">"The test was successful" here means after entering the credentials of your Azure test account it will pop up a message "Settings tested OK".Then click the **OK** button.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="dc93c-178">Fare clic sul pulsante **Save** (Salva) nella pagina "**Authentication**" (Autenticazione).</span><span class="sxs-lookup"><span data-stu-id="dc93c-178">Click the **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="dc93c-179">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="dc93c-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dc93c-180">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="dc93c-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dc93c-181">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc93c-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dc93c-182">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc93c-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="dc93c-183">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc93c-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="dc93c-185">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="dc93c-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dc93c-186">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="dc93c-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dc93c-188">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="dc93c-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dc93c-190">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dc93c-192">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dc93c-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dc93c-194">a.</span><span class="sxs-lookup"><span data-stu-id="dc93c-194">a.</span></span> <span data-ttu-id="dc93c-195">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc93c-196">b.</span><span class="sxs-lookup"><span data-stu-id="dc93c-196">b.</span></span> <span data-ttu-id="dc93c-197">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dc93c-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dc93c-198">c.</span><span class="sxs-lookup"><span data-stu-id="dc93c-198">c.</span></span> <span data-ttu-id="dc93c-199">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dc93c-200">d.</span><span class="sxs-lookup"><span data-stu-id="dc93c-200">d.</span></span> <span data-ttu-id="dc93c-201">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="dc93c-202">Creazione di un utente test di Printix</span><span class="sxs-lookup"><span data-stu-id="dc93c-202">Creating a Printix test user</span></span>

<span data-ttu-id="dc93c-203">Questa sezione descrive come creare un utente chiamato Britta Simon in Printix.</span><span class="sxs-lookup"><span data-stu-id="dc93c-203">The objective of this section is to create a user called Britta Simon in Printix.</span></span> <span data-ttu-id="dc93c-204">Printix supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="dc93c-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="dc93c-205">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="dc93c-205">There is no action item for you in this section.</span></span> <span data-ttu-id="dc93c-206">Durante un tentativo di accesso a Printix viene creato un nuovo utente, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="dc93c-206">A new user is created during an attempt to access Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="dc93c-207">Per creare un utente manualmente è necessario contattare il [team di supporto di Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="dc93c-207">If you need to create a user manually, you need to contact the [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dc93c-208">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc93c-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dc93c-209">In questa sezione, Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Printix.</span><span class="sxs-lookup"><span data-stu-id="dc93c-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Printix.</span></span>

![Assegna utente][200] 

<span data-ttu-id="dc93c-211">**Per assegnare Britta Simon a Printix, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dc93c-211">**To assign Britta Simon to Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="dc93c-212">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="dc93c-214">Nell'elenco di applicazioni selezionare **Printix**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-214">In the applications list, select **Printix**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="dc93c-216">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="dc93c-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="dc93c-218">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-218">Click **Add** button.</span></span> <span data-ttu-id="dc93c-219">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="dc93c-221">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="dc93c-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dc93c-222">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dc93c-223">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="dc93c-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dc93c-224">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dc93c-224">Testing single sign-on</span></span>

<span data-ttu-id="dc93c-225">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="dc93c-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dc93c-226">Quando si fa clic sul riquadro Printix nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Printix.</span><span class="sxs-lookup"><span data-stu-id="dc93c-226">When you click the Printix tile in the Access Panel, you should get automatically signed-on to your Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dc93c-227">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="dc93c-227">Additional resources</span></span>

* [<span data-ttu-id="dc93c-228">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc93c-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dc93c-229">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc93c-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

