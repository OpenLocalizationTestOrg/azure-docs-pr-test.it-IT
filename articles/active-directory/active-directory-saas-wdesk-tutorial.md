---
title: 'Esercitazione: Integrazione di Azure Active Directory con Wdesk | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Wdesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="47e50-103">Esercitazione: Integrazione di Azure Active Directory con Wdesk</span><span class="sxs-lookup"><span data-stu-id="47e50-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="47e50-104">In questa esercitazione, è illustrato come toointegrate Wdesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="47e50-104">In this tutorial, you learn how toointegrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="47e50-105">Integrazione Wdesk con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="47e50-105">Integrating Wdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="47e50-106">È possibile controllare in Azure AD che ha accesso tooWdesk</span><span class="sxs-lookup"><span data-stu-id="47e50-106">You can control in Azure AD who has access tooWdesk</span></span>
- <span data-ttu-id="47e50-107">È possibile abilitare l'utenti tooautomatically get connesso tooWdesk (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="47e50-107">You can enable your users tooautomatically get signed-on tooWdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="47e50-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="47e50-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="47e50-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere.</span><span class="sxs-lookup"><span data-stu-id="47e50-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="47e50-110">[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="47e50-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47e50-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="47e50-111">Prerequisites</span></span>

<span data-ttu-id="47e50-112">integrazione di Azure AD con Wdesk tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="47e50-112">tooconfigure Azure AD integration with Wdesk, you need hello following items:</span></span>

- <span data-ttu-id="47e50-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47e50-113">An Azure AD subscription</span></span>
- <span data-ttu-id="47e50-114">Sottoscrizione di Wdesk abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="47e50-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="47e50-115">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="47e50-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="47e50-116">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="47e50-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="47e50-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="47e50-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="47e50-118">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47e50-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="47e50-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="47e50-119">Scenario description</span></span>
<span data-ttu-id="47e50-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="47e50-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="47e50-121">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="47e50-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="47e50-122">Aggiunta di Wdesk dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="47e50-122">Adding Wdesk from hello gallery</span></span>
2. <span data-ttu-id="47e50-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47e50-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-hello-gallery"></a><span data-ttu-id="47e50-124">Aggiunta di Wdesk dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="47e50-124">Adding Wdesk from hello gallery</span></span>
<span data-ttu-id="47e50-125">integrazione hello tooconfigure di Wdesk in Azure AD, è necessario tooadd Wdesk dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="47e50-125">tooconfigure hello integration of Wdesk into Azure AD, you need tooadd Wdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="47e50-126">**tooadd Wdesk dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47e50-126">**tooadd Wdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="47e50-127">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="47e50-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="47e50-129">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="47e50-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="47e50-130">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="47e50-130">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="47e50-132">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="47e50-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="47e50-134">Nella casella di ricerca hello, digitare **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="47e50-134">In hello search box, type **Wdesk**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="47e50-136">Nel riquadro dei risultati hello, selezionare **Wdesk**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="47e50-136">In hello results panel, select **Wdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="47e50-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47e50-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="47e50-139">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Wdesk con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="47e50-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="47e50-140">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Wdesk è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47e50-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="47e50-141">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Wdesk deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="47e50-141">In other words, a link relationship between an Azure AD user and hello related user in Wdesk needs toobe established.</span></span>

<span data-ttu-id="47e50-142">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Wdesk.</span><span class="sxs-lookup"><span data-stu-id="47e50-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wdesk.</span></span>

<span data-ttu-id="47e50-143">tooconfigure e prova AD Azure single sign-on con Wdesk, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="47e50-143">tooconfigure and test Azure AD single sign-on with Wdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="47e50-144">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="47e50-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="47e50-145">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47e50-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="47e50-146">**[Creazione di un utente test Wdesk](#creating-a-wdesk-test-user)**  -toohave un equivalente di Britta Simon in Wdesk che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="47e50-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - toohave a counterpart of Britta Simon in Wdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="47e50-147">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="47e50-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="47e50-148">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="47e50-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="47e50-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47e50-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="47e50-150">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Wdesk.</span><span class="sxs-lookup"><span data-stu-id="47e50-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="47e50-151">**Azure AD tooconfigure single sign-on con Wdesk, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47e50-151">**tooconfigure Azure AD single sign-on with Wdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="47e50-152">Nel portale di Azure su hello hello **Wdesk** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="47e50-152">In hello Azure portal, on hello **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="47e50-154">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="47e50-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="47e50-156">In hello **Wdesk dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità avviato da eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47e50-156">On hello **Wdesk Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="47e50-158">a.</span><span class="sxs-lookup"><span data-stu-id="47e50-158">a.</span></span> <span data-ttu-id="47e50-159">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="47e50-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="47e50-160">b.</span><span class="sxs-lookup"><span data-stu-id="47e50-160">b.</span></span> <span data-ttu-id="47e50-161">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="47e50-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="47e50-162">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="47e50-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="47e50-163">Se si desidera un'applicazione hello tooconfigure in **SP** , modalità iniziata da eseguire hello seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="47e50-163">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="47e50-165">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="47e50-165">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="47e50-166">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="47e50-166">These values are not real.</span></span> <span data-ttu-id="47e50-167">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="47e50-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="47e50-168">Ottenere questi valori dal portale WDesk quando si configura SSO hello.</span><span class="sxs-lookup"><span data-stu-id="47e50-168">You get these values from WDesk portal when you configure hello SSO.</span></span> 
  
5. <span data-ttu-id="47e50-169">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="47e50-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="47e50-171">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="47e50-171">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="47e50-173">In una finestra del web browser, account di accesso tooWdesk come un amministratore della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="47e50-173">In a different web browser window, login tooWdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="47e50-174">In hello in basso a sinistra, fare clic su **Admin** e scegliere **amministratore dell'Account**:</span><span class="sxs-lookup"><span data-stu-id="47e50-174">In hello bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="47e50-176">In Wdesk Admin, passare troppo**sicurezza**, quindi **SAML** > **impostazioni SAML**:</span><span class="sxs-lookup"><span data-stu-id="47e50-176">In Wdesk Admin, navigate too**Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="47e50-178">In **impostazioni generali**, controllare hello **Abilita SAML Single Sign On**:</span><span class="sxs-lookup"><span data-stu-id="47e50-178">Under **General Settings**, check hello **Enable SAML Single Sign On**:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="47e50-180">In **i dettagli del Provider servizio**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47e50-180">Under **Service Provider Details**, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="47e50-182">a.</span><span class="sxs-lookup"><span data-stu-id="47e50-182">a.</span></span> <span data-ttu-id="47e50-183">Hello copia **URL di accesso** e incollarlo in **Sign-on Url** casella di testo nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="47e50-183">Copy hello **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="47e50-184">b.</span><span class="sxs-lookup"><span data-stu-id="47e50-184">b.</span></span> <span data-ttu-id="47e50-185">Hello copia **Url dei metadati** e incollarlo in **identificatore** casella di testo nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="47e50-185">Copy hello **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="47e50-186">c.</span><span class="sxs-lookup"><span data-stu-id="47e50-186">c.</span></span> <span data-ttu-id="47e50-187">Hello copia **url Consumer** e incollarlo in **Url di risposta** casella di testo nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="47e50-187">Copy hello **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="47e50-188">d.</span><span class="sxs-lookup"><span data-stu-id="47e50-188">d.</span></span> <span data-ttu-id="47e50-189">Fare clic su **salvare** alle modifiche apportate hello toosave portale Azure.</span><span class="sxs-lookup"><span data-stu-id="47e50-189">Click **Save** on Azure portal toosave hello changes.</span></span>      

12. <span data-ttu-id="47e50-190">Fare clic su **Configura impostazioni IdP** tooopen **Modifica impostazioni IdP** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="47e50-190">Click **Configure IdP Settings** tooopen **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="47e50-191">Fare clic su **Scegli File** toolocate hello **Metadata.xml** file salvato dal portale di Azure, quindi caricare il file.</span><span class="sxs-lookup"><span data-stu-id="47e50-191">Click **Choose File** toolocate hello **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="47e50-193">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="47e50-193">Click **Save changes**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="47e50-195">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="47e50-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="47e50-196">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="47e50-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="47e50-197">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="47e50-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="47e50-198">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47e50-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="47e50-199">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="47e50-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="47e50-201">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47e50-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="47e50-202">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="47e50-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="47e50-204">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="47e50-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="47e50-206">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="47e50-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="47e50-208">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47e50-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="47e50-210">a.</span><span class="sxs-lookup"><span data-stu-id="47e50-210">a.</span></span> <span data-ttu-id="47e50-211">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="47e50-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="47e50-212">b.</span><span class="sxs-lookup"><span data-stu-id="47e50-212">b.</span></span> <span data-ttu-id="47e50-213">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="47e50-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="47e50-214">c.</span><span class="sxs-lookup"><span data-stu-id="47e50-214">c.</span></span> <span data-ttu-id="47e50-215">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="47e50-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="47e50-216">d.</span><span class="sxs-lookup"><span data-stu-id="47e50-216">d.</span></span> <span data-ttu-id="47e50-217">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="47e50-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="47e50-218">Creazione di un utente test di Wdesk</span><span class="sxs-lookup"><span data-stu-id="47e50-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="47e50-219">toolog agli utenti di Azure AD tooenable in tooWdesk, è necessario eseguirne il provisioning in Wdesk.</span><span class="sxs-lookup"><span data-stu-id="47e50-219">tooenable Azure AD users toolog in tooWdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="47e50-220">Nel caso di Wdesk il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="47e50-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="47e50-221">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47e50-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="47e50-222">Accedi tooWdesk come un amministratore della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="47e50-222">Log in tooWdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="47e50-223">Passare troppo**Admin** > **amministratore dell'Account**.</span><span class="sxs-lookup"><span data-stu-id="47e50-223">Navigate too**Admin** > **Account Admin**.</span></span>

     ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="47e50-225">Fare clic su **Members** (Membri) in **People** (Persone).</span><span class="sxs-lookup"><span data-stu-id="47e50-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="47e50-226">Fare clic su **Add Member** tooopen **Add Member** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="47e50-226">Now click **Add Member** tooopen **Add Member** dialog box.</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="47e50-228">In **utente** testo casella, immettere un nome utente dell'utente come hello  **brittasimon@contoso.com**  e fare clic su **continua** pulsante.</span><span class="sxs-lookup"><span data-stu-id="47e50-228">In **User** text box, enter hello username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="47e50-230">Immettere i dettagli di hello, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="47e50-230">Enter hello details as shown below:</span></span>
  
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="47e50-232">a.</span><span class="sxs-lookup"><span data-stu-id="47e50-232">a.</span></span> <span data-ttu-id="47e50-233">In **posta elettronica** testo messaggio di posta elettronica hello dell'utente come immettere  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="47e50-233">In **E-mail** text box, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="47e50-234">b.</span><span class="sxs-lookup"><span data-stu-id="47e50-234">b.</span></span> <span data-ttu-id="47e50-235">In **nome** testo hello nome dell'utente come immettere **Laura**.</span><span class="sxs-lookup"><span data-stu-id="47e50-235">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="47e50-236">c.</span><span class="sxs-lookup"><span data-stu-id="47e50-236">c.</span></span> <span data-ttu-id="47e50-237">In **cognome** testo immettere il cognome di hello dell'utente come **Simon**.</span><span class="sxs-lookup"><span data-stu-id="47e50-237">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

7. <span data-ttu-id="47e50-238">Fare clic sul pulsante **Save Member** (Salva membro).</span><span class="sxs-lookup"><span data-stu-id="47e50-238">Click **Save Member** button.</span></span>  

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="47e50-240">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="47e50-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="47e50-241">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWdesk.</span><span class="sxs-lookup"><span data-stu-id="47e50-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWdesk.</span></span>

![Assegna utente][200] 

<span data-ttu-id="47e50-243">**tooassign Britta Simon tooWdesk, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47e50-243">**tooassign Britta Simon tooWdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="47e50-244">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="47e50-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="47e50-246">Nell'elenco di applicazioni hello, selezionare **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="47e50-246">In hello applications list, select **Wdesk**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="47e50-248">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="47e50-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="47e50-250">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="47e50-250">Click **Add** button.</span></span> <span data-ttu-id="47e50-251">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="47e50-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="47e50-253">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="47e50-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="47e50-254">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="47e50-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="47e50-255">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="47e50-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="47e50-256">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="47e50-256">Testing single sign-on</span></span>

<span data-ttu-id="47e50-257">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="47e50-257">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="47e50-258">Quando si fa clic su riquadro Wdesk hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Wdesk applicazione.</span><span class="sxs-lookup"><span data-stu-id="47e50-258">When you click hello Wdesk tile in hello Access Panel, you should get automatically signed-on tooyour Wdesk application.</span></span>
<span data-ttu-id="47e50-259">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="47e50-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="47e50-260">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="47e50-260">Additional resources</span></span>

* [<span data-ttu-id="47e50-261">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47e50-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="47e50-262">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47e50-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

