---
title: 'Esercitazione: Integrazione di Azure Active Directory con IdeaScale | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e IdeaScale.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 88099e942319f16dd721da83e4e69b8fcb836c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="0fa56-103">Esercitazione: Integrazione di Azure Active Directory con IdeaScale</span><span class="sxs-lookup"><span data-stu-id="0fa56-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="0fa56-104">Questa esercitazione descrive come integrare IdeaScale con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0fa56-104">In this tutorial, you learn how to integrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0fa56-105">L'integrazione di IdeaScale con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0fa56-105">Integrating IdeaScale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0fa56-106">È possibile controllare in Azure AD chi può accedere a IdeaScale</span><span class="sxs-lookup"><span data-stu-id="0fa56-106">You can control in Azure AD who has access to IdeaScale</span></span>
- <span data-ttu-id="0fa56-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a IdeaScale con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa56-107">You can enable your users to automatically get signed-on to IdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0fa56-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fa56-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0fa56-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0fa56-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fa56-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0fa56-110">Prerequisites</span></span>

<span data-ttu-id="0fa56-111">Per configurare l'integrazione di Azure AD con IdeaScale sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0fa56-111">To configure Azure AD integration with IdeaScale, you need the following items:</span></span>

- <span data-ttu-id="0fa56-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fa56-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0fa56-113">Sottoscrizione di IdeaScale abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0fa56-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0fa56-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0fa56-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0fa56-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0fa56-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0fa56-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0fa56-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0fa56-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0fa56-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0fa56-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0fa56-118">Scenario description</span></span>
<span data-ttu-id="0fa56-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0fa56-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0fa56-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0fa56-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0fa56-121">Aggiunta di IdeaScale dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0fa56-121">Adding IdeaScale from the gallery</span></span>
2. <span data-ttu-id="0fa56-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa56-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-the-gallery"></a><span data-ttu-id="0fa56-123">Aggiunta di IdeaScale dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0fa56-123">Adding IdeaScale from the gallery</span></span>
<span data-ttu-id="0fa56-124">Per configurare l'integrazione di IdeaScale in Azure AD è necessario aggiungere IdeaScale dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0fa56-124">To configure the integration of IdeaScale into Azure AD, you need to add IdeaScale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0fa56-125">**Per aggiungere IdeaScale dalla raccolta seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0fa56-125">**To add IdeaScale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0fa56-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0fa56-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0fa56-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0fa56-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="0fa56-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="0fa56-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="0fa56-133">Nella casella di ricerca digitare **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-133">In the search box, type **IdeaScale**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="0fa56-135">Nel pannello dei risultati selezionare **IdeaScale** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0fa56-135">In the results panel, select **IdeaScale**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0fa56-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa56-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0fa56-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con IdeaScale mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0fa56-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0fa56-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di IdeaScale corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fa56-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IdeaScale is to a user in Azure AD.</span></span> <span data-ttu-id="0fa56-140">In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="0fa56-140">In other words, a link relationship between an Azure AD user and the related user in IdeaScale needs to be established.</span></span>

<span data-ttu-id="0fa56-141">Per stabilire la relazione di collegamento, in IdeaScale assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="0fa56-141">In IdeaScale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0fa56-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con IdeaScale è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0fa56-142">To configure and test Azure AD single sign-on with IdeaScale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0fa56-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0fa56-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0fa56-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0fa56-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0fa56-145">**[Creazione di un utente test di IdeaScale](#creating-an-ideascale-test-user)**: per avere una controparte di Britta Simon in IdeaScale collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fa56-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - to have a counterpart of Britta Simon in IdeaScale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0fa56-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fa56-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0fa56-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="0fa56-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0fa56-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa56-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0fa56-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="0fa56-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="0fa56-150">**Per configurare l'accesso Single Sign-On di Azure AD con IdeaScale, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0fa56-150">**To configure Azure AD single sign-on with IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="0fa56-151">Nella pagina di integrazione dell'applicazione **IdeaScale** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-151">In the Azure portal, on the **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0fa56-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0fa56-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="0fa56-155">Nella sezione **URL e dominio IdeaScale** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0fa56-155">On the **IdeaScale Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="0fa56-157">a.</span><span class="sxs-lookup"><span data-stu-id="0fa56-157">a.</span></span> <span data-ttu-id="0fa56-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.ideascale.com`.</span><span class="sxs-lookup"><span data-stu-id="0fa56-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="0fa56-159">b.</span><span class="sxs-lookup"><span data-stu-id="0fa56-159">b.</span></span> <span data-ttu-id="0fa56-160">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="0fa56-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="0fa56-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="0fa56-161">These values are not real.</span></span> <span data-ttu-id="0fa56-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="0fa56-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0fa56-163">Per ottenere questi valori contattare il [team di supporto clienti di IdeaScale](http://support.ideascale.com/).</span><span class="sxs-lookup"><span data-stu-id="0fa56-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="0fa56-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="0fa56-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="0fa56-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0fa56-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0fa56-168">Nella sezione **Configurazione di IdeaScale** fare clic su **Configura IdeaScale** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-168">On the **IdeaScale Configuration** section, click **Configure IdeaScale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0fa56-169">Copiare i valori **Sign-Out URL (URL di disconnessione) e SAML Entity ID (ID entità SAML)** dalla **sezione Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="0fa56-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="0fa56-171">In un'altra finestra del Web browser accedere al sito aziendale di IdeaScale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0fa56-171">In a different web browser window, log in to your IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="0fa56-172">Passare a **Impostazioni Community**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-172">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="0fa56-173">![Impostazioni Community](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Impostazioni Community")</span><span class="sxs-lookup"><span data-stu-id="0fa56-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="0fa56-174">Passare a **Security (Sicurezza) \> Single Signon Settings (Impostazioni di Single Sign-O)**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-174">Go to **Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="0fa56-175">![Impostazioni di Single Sign-On](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Impostazioni di Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="0fa56-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="0fa56-176">In **Single-Signon Type** (Tipo di accesso Single Sign-On) selezionare **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="0fa56-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span><span class="sxs-lookup"><span data-stu-id="0fa56-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="0fa56-178">Nella finestra di dialogo **Impostazioni di Single Sign-O** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0fa56-178">On the **Single Signon Settings** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="0fa56-179">![Impostazioni di Single Sign-On](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Impostazioni di Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="0fa56-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="0fa56-180">a.</span><span class="sxs-lookup"><span data-stu-id="0fa56-180">a.</span></span> <span data-ttu-id="0fa56-181">Nella casella di testo **SAML IdP Entity ID** (ID entità IdP SAML) incollare il valore **SAML Entity ID** (ID entità SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fa56-181">In **SAML IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0fa56-182">b.</span><span class="sxs-lookup"><span data-stu-id="0fa56-182">b.</span></span> <span data-ttu-id="0fa56-183">Copiare il contenuto del file dei metadati scaricato dal portale di Azure e incollarlo nella casella di testo **SAML IdP Metadata** (Metadati IdP SAML).</span><span class="sxs-lookup"><span data-stu-id="0fa56-183">Copy the content of your downloaded metadata file from Azure portal, and paste it into the **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="0fa56-184">c.</span><span class="sxs-lookup"><span data-stu-id="0fa56-184">c.</span></span> <span data-ttu-id="0fa56-185">Nella casella di testo **Logout Success URL** (URL disconnessione riuscita) incollare il valore di **Sign-Out URL** (URL di disconnessione) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fa56-185">In **Logout Success URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0fa56-186">d.</span><span class="sxs-lookup"><span data-stu-id="0fa56-186">d.</span></span> <span data-ttu-id="0fa56-187">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0fa56-188">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="0fa56-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0fa56-189">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="0fa56-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0fa56-190">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0fa56-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0fa56-191">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa56-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="0fa56-192">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fa56-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="0fa56-194">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0fa56-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0fa56-195">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0fa56-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0fa56-197">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="0fa56-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0fa56-199">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0fa56-201">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0fa56-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0fa56-203">a.</span><span class="sxs-lookup"><span data-stu-id="0fa56-203">a.</span></span> <span data-ttu-id="0fa56-204">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0fa56-205">b.</span><span class="sxs-lookup"><span data-stu-id="0fa56-205">b.</span></span> <span data-ttu-id="0fa56-206">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0fa56-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0fa56-207">c.</span><span class="sxs-lookup"><span data-stu-id="0fa56-207">c.</span></span> <span data-ttu-id="0fa56-208">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0fa56-209">d.</span><span class="sxs-lookup"><span data-stu-id="0fa56-209">d.</span></span> <span data-ttu-id="0fa56-210">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="0fa56-211">Creazione di un utente test di IdeaScale</span><span class="sxs-lookup"><span data-stu-id="0fa56-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="0fa56-212">Per consentire agli utenti di Azure AD di accedere a IdeaScale, è necessario eseguire il provisioning degli utenti in IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="0fa56-212">To enable Azure AD users to log into IdeaScale, they must be provisioned in to IdeaScale.</span></span> <span data-ttu-id="0fa56-213">Nel caso di IdeaScale, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="0fa56-213">In the case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="0fa56-214">**Per configurare il provisioning utenti, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0fa56-214">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="0fa56-215">Accedere al sito aziendale di **IdeaScale** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0fa56-215">Log in to your **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="0fa56-216">Passare a **Impostazioni Community**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-216">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="0fa56-217">![Impostazioni Community](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Impostazioni Community")</span><span class="sxs-lookup"><span data-stu-id="0fa56-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="0fa56-218">Passare a **Basic Settings (Impostazioni di base) \> Member Management (Gestione membri)**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-218">Go to **Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="0fa56-219">Fare clic su **Aggiungi membro**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="0fa56-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span><span class="sxs-lookup"><span data-stu-id="0fa56-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="0fa56-221">Nella sezione Add New Member seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0fa56-221">In the Add New Member section, perform the following steps:</span></span>
   
    <span data-ttu-id="0fa56-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span><span class="sxs-lookup"><span data-stu-id="0fa56-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="0fa56-223">a.</span><span class="sxs-lookup"><span data-stu-id="0fa56-223">a.</span></span> <span data-ttu-id="0fa56-224">Nella casella di testo **Indirizzi email** digitare l'indirizzo di posta elettronica di un account di AAD valido di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="0fa56-224">In the **Email Addresses** textbox, type the email address of a valid AAD account you want to provision.</span></span>
   
    <span data-ttu-id="0fa56-225">b.</span><span class="sxs-lookup"><span data-stu-id="0fa56-225">b.</span></span> <span data-ttu-id="0fa56-226">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="0fa56-227">Il titolare dell'account Azure Active Directory riceve un messaggio di posta elettronica con un collegamento per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="0fa56-227">The Azure Active Directory account holder gets an email with a link to confirm the account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="0fa56-228">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da IdeaScale per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="0fa56-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0fa56-229">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa56-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0fa56-230">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="0fa56-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IdeaScale.</span></span>

![Assegna utente][200] 

<span data-ttu-id="0fa56-232">**Per assegnare Britta Simon a IdeaScale, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0fa56-232">**To assign Britta Simon to IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="0fa56-233">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0fa56-235">Nell'elenco delle applicazioni selezionare **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-235">In the applications list, select **IdeaScale**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="0fa56-237">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0fa56-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="0fa56-239">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-239">Click **Add** button.</span></span> <span data-ttu-id="0fa56-240">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="0fa56-242">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="0fa56-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0fa56-243">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0fa56-244">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0fa56-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0fa56-245">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0fa56-245">Testing single sign-on</span></span>


<span data-ttu-id="0fa56-246">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0fa56-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0fa56-247">Quando si fa clic sul riquadro IdeaScale nel pannello di accesso si accede automaticamente all'applicazione IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="0fa56-247">When you click the IdeaScale tile in the Access Panel, you should get automatically signed-on to your IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0fa56-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0fa56-248">Additional resources</span></span>

* [<span data-ttu-id="0fa56-249">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0fa56-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0fa56-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0fa56-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

