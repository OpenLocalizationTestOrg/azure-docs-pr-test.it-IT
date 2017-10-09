---
title: 'Esercitazione: Integrazione di Azure Active Directory con HR2day by Merces | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e HR2day da Merces.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="b1273-103">Esercitazione: Integrazione di Azure Active Directory con HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="b1273-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="b1273-104">In questa esercitazione, è illustrato come toointegrate HR2day da Merces con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b1273-104">In this tutorial, you learn how toointegrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b1273-105">Integrazione HR2day da Merces con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="b1273-105">Integrating HR2day by Merces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b1273-106">È possibile controllare in Azure AD che ha accesso tooHR2day da Merces.</span><span class="sxs-lookup"><span data-stu-id="b1273-106">You can control in Azure AD who has access tooHR2day by Merces.</span></span>
- <span data-ttu-id="b1273-107">È possibile abilitare gli utenti tooautomatically ottenere l'accesso tooHR2day Merces con gli account di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1273-107">You can enable your users tooautomatically get signed in tooHR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="b1273-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1273-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="b1273-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b1273-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1273-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b1273-110">Prerequisites</span></span>

<span data-ttu-id="b1273-111">integrazione di Azure AD con HR2day da Merces tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="b1273-111">tooconfigure Azure AD integration with HR2day by Merces, you need hello following items:</span></span>

- <span data-ttu-id="b1273-112">Una sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1273-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="b1273-113">Sottoscrizione di HR2day by Merces abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b1273-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="b1273-114">Non è consigliabile utilizzare un hello tootest ambiente di produzione i passaggi in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b1273-114">We don't recommend using a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="b1273-115">passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:</span><span class="sxs-lookup"><span data-stu-id="b1273-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="b1273-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b1273-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="b1273-117">Ottenere una [versione di valutazione gratuita di un mese di Azure AD](https://azure.microsoft.com/pricing/free-trial/), se non la si ha già.</span><span class="sxs-lookup"><span data-stu-id="b1273-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="b1273-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b1273-118">Scenario description</span></span>
<span data-ttu-id="b1273-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b1273-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b1273-120">scenario di Hello descritta di seguito è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="b1273-120">hello scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="b1273-121">Aggiunta di HR2day da Merces dalla raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="b1273-121">Adding HR2day by Merces from hello gallery.</span></span>
2. <span data-ttu-id="b1273-122">Configurazione e test dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1273-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-hello-gallery"></a><span data-ttu-id="b1273-123">Aggiungere HR2day da Merces dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="b1273-123">Add HR2day by Merces from hello gallery</span></span>
<span data-ttu-id="b1273-124">integrazione di hello tooconfigure di HR2day da Merces in Azure AD, aggiungere HR2day da Merces hello raccolta tooyour elenco di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b1273-124">tooconfigure hello integration of HR2day by Merces into Azure AD, add HR2day by Merces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b1273-125">**tooadd HR2day da Merces dalla raccolta di hello, richiedere hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b1273-125">**tooadd HR2day by Merces from hello gallery, take hello following steps:**</span></span>

1. <span data-ttu-id="b1273-126">In hello [portale di Azure](https://portal.azure.com), nel riquadro di spostamento a sinistra di hello, selezionare hello **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b1273-126">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b1273-128">Andare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b1273-128">Go too**Enterprise applications**.</span></span> <span data-ttu-id="b1273-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b1273-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b1273-131">tooadd una nuova applicazione, seleziona hello **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="b1273-131">tooadd a new application, select hello **New application** button on hello top of hello dialog box.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b1273-133">Nella casella di ricerca hello, digitare **HR2day da Merces**.</span><span class="sxs-lookup"><span data-stu-id="b1273-133">In hello search box, type **HR2day by Merces**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="b1273-135">Nel riquadro dei risultati hello, selezionare **HR2day da Merces**, quindi selezionare hello **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b1273-135">In hello results panel, select **HR2day by Merces**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b1273-137">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1273-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b1273-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con HR2day by Merces usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b1273-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b1273-139">Per toowork di accesso singolo, Azure AD deve tooknow chi hello controparte utente in HR2day da Merces tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1273-139">For single sign-on toowork, Azure AD needs tooknow who hello counterpart user in HR2day by Merces is tooa user in Azure AD.</span></span> <span data-ttu-id="b1273-140">In altre parole, è necessario un collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in HR2day da Merces tooestablish.</span><span class="sxs-lookup"><span data-stu-id="b1273-140">In other words, you need tooestablish a link between an Azure AD user and hello related user in HR2day by Merces.</span></span>

<span data-ttu-id="b1273-141">In HR2day da Merces, assegnare hello **nome utente** in Azure AD troppo **Username** relazione hello tooestablish.</span><span class="sxs-lookup"><span data-stu-id="b1273-141">In HR2day by Merces, assign hello **user name** in Azure AD too **Username** tooestablish hello relationship.</span></span>

<span data-ttu-id="b1273-142">tooconfigure e prova AD Azure single sign-on con HR2day da Merces, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="b1273-142">tooconfigure and test Azure AD single sign-on with HR2day by Merces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b1273-143">[Configurare Azure AD single sign-on](#configuring-azure-ad-single-sign-on): abilitare il toouse agli utenti di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b1273-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users toouse this feature.</span></span>
2. <span data-ttu-id="b1273-144">[Creare un utente di test di Azure AD](#creating-an-azure-ad-test-user): per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b1273-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b1273-145">[Creare un HR2day utente test Merces](#creating-an-hr2day-by-merces-test-user): creare un equivalente di Britta Simon in HR2day da Merces che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b1273-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b1273-146">[Assegnare l'utente test hello Azure AD](#assigning-the-azure-ad-test-user): abilitare Britta Simon toouse AD Azure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b1273-146">[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b1273-147">[Testare single sign-on](#testing-single-sign-on): verificare se funziona configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="b1273-147">[Test single sign-on](#testing-single-sign-on): Verify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b1273-148">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1273-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b1273-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nel HR2day dall'applicazione Merces.</span><span class="sxs-lookup"><span data-stu-id="b1273-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="b1273-150">**Azure AD tooconfigure single sign-on con HR2day da Merces, richiedere hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b1273-150">**tooconfigure Azure AD single sign-on with HR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="b1273-151">Nel portale di Azure su hello hello **HR2day da Merces** pagina di integrazione dell'applicazione, seleziona **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b1273-151">In hello Azure portal, on hello **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b1273-153">tooenable accesso single sign-on, in hello **Single sign-on** nella finestra di dialogo **modalità** come **basato su SAML Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b1273-153">tooenable single sign-on, in hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="b1273-155">In hello **HR2day Merces dominio e gli URL** sezione, richiedere hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b1273-155">In hello **HR2day by Merces Domain and URLs** section, take hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="b1273-157">a.</span><span class="sxs-lookup"><span data-stu-id="b1273-157">a.</span></span> <span data-ttu-id="b1273-158">In hello **Sign-on URL** casella, digitare un URL utilizzando hello seguente motivo: `https://<tenantname>.force.com/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="b1273-158">In hello **Sign-on URL** box, type a URL by using hello following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="b1273-159">b.</span><span class="sxs-lookup"><span data-stu-id="b1273-159">b.</span></span> <span data-ttu-id="b1273-160">In hello **identificatore** casella, digitare un URL utilizzando hello seguente motivo: `https://hr2day.force.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="b1273-160">In hello **Identifier** box, type a URL by using hello following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b1273-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="b1273-161">These values are not real.</span></span> <span data-ttu-id="b1273-162">Aggiornare questi valori con URL hello effettivo sign-on e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="b1273-162">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="b1273-163">Contatto hello [HR2day dal team di supporto client Merces](mailto:servicedesk@merces.nl) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="b1273-163">Contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl) tooget these values.</span></span> 
 


4. <span data-ttu-id="b1273-164">In hello **certificato di firma SAML** selezionare **Certificate(Base64)**e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="b1273-164">On hello **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="b1273-166">Questa sezione viene descritto come tooenable utenti tooauthenticate tooHR2day da Merces con il proprio account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1273-166">This section describes how tooenable users tooauthenticate tooHR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="b1273-167">Tale scopo, usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="b1273-167">They do this by using federation that's based on hello SAML protocol.</span></span>

    <span data-ttu-id="b1273-168">Il HR2day dall'applicazione Merces prevede asserzioni SAML hello in un formato specifico, che richiede il token SAML tooyour di tooadd attributo personalizzato mapping.</span><span class="sxs-lookup"><span data-stu-id="b1273-168">Your HR2day by Merces application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token.</span></span> <span data-ttu-id="b1273-169">Hello seguente schermata mostra un esempio di questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="b1273-169">hello following screenshot shows an example of this.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="b1273-171">Prima di poter configurare l'asserzione SAML hello, è necessario contattare hello [HR2day dal team di supporto Merces Client](mailto:servicedesk@merces.nl) e valore hello dell'attributo dell'identificatore univoco hello per le richieste per il tenant.</span><span class="sxs-lookup"><span data-stu-id="b1273-171">Before you can configure hello SAML assertion, you must contact hello [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="b1273-172">È necessario passaggi di hello toocomplete questo valore nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="b1273-172">You need this value toocomplete hello steps in hello next section.</span></span> 

6. <span data-ttu-id="b1273-173">In hello **Single sign-on** della finestra di dialogo hello **gli attributi utente** sezione, configurare un attributo di token SAML hello, come illustrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="b1273-173">In hello **Single sign-on** dialog box, in hello **User Attributes** section, configure hello SAML token attribute as shown in hello following image.</span></span> <span data-ttu-id="b1273-174">Richiedere quindi hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="b1273-174">Then take hello following steps.</span></span>
    
      | <span data-ttu-id="b1273-175">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="b1273-175">Attribute name</span></span>    |   <span data-ttu-id="b1273-176">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="b1273-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="b1273-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="b1273-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="b1273-178">join([mail],"102938475Z","@"</span><span class="sxs-lookup"><span data-stu-id="b1273-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="b1273-179">a.</span><span class="sxs-lookup"><span data-stu-id="b1273-179">a.</span></span> <span data-ttu-id="b1273-180">hello tooopen **Aggiungi attributo** finestra di dialogo Seleziona **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="b1273-180">tooopen hello **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="b1273-183">b.</span><span class="sxs-lookup"><span data-stu-id="b1273-183">b.</span></span> <span data-ttu-id="b1273-184">In hello **nome** digitare **ATTR_LOGINCLAIM**.</span><span class="sxs-lookup"><span data-stu-id="b1273-184">In hello **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="b1273-185">c.</span><span class="sxs-lookup"><span data-stu-id="b1273-185">c.</span></span> <span data-ttu-id="b1273-186">Da hello **valore** elenco, selezionare **join**.</span><span class="sxs-lookup"><span data-stu-id="b1273-186">From hello **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="b1273-187">d.</span><span class="sxs-lookup"><span data-stu-id="b1273-187">d.</span></span> <span data-ttu-id="b1273-188">Da hello **String1** elenco, selezionare **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="b1273-188">From hello **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="b1273-189">e.</span><span class="sxs-lookup"><span data-stu-id="b1273-189">e.</span></span> <span data-ttu-id="b1273-190">Per **String2**, digitare l'identificatore univoco di hello che viene fornito dal team HR2day.</span><span class="sxs-lookup"><span data-stu-id="b1273-190">For **String2**, type hello unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="b1273-191">f.</span><span class="sxs-lookup"><span data-stu-id="b1273-191">f.</span></span> <span data-ttu-id="b1273-192">In hello **separatore** digitare  **@** .</span><span class="sxs-lookup"><span data-stu-id="b1273-192">In hello **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="b1273-193">g.</span><span class="sxs-lookup"><span data-stu-id="b1273-193">g.</span></span> <span data-ttu-id="b1273-194">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1273-194">Select **Ok**.</span></span>

7. <span data-ttu-id="b1273-195">Seleziona hello **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="b1273-195">Select hello **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b1273-197">In hello **HR2day dalla configurazione Merces** selezionare **configurare HR2day da Merces** tooopen hello **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="b1273-197">In hello **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="b1273-198">Hello copia **Sign-Out URL**, **ID entità SAML**, e **SAML Single Sign-On Service URL** da hello **riferimento rapido** sezione.</span><span class="sxs-lookup"><span data-stu-id="b1273-198">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="b1273-200">tooconfigure SSO per l'applicazione, contattare di hello [HR2day dal team di supporto client Merces](mailTo:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="b1273-200">tooconfigure SSO  for your application, contact hello [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="b1273-201">Collegare hello scaricato **Certificate(Base64)** file tooyour messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="b1273-201">Attach hello downloaded **Certificate(Base64)** file tooyour email.</span></span> <span data-ttu-id="b1273-202">Forniscono anche hello **Sign-Out URL**, **ID entità SAML**, e **SAML Single Sign-On Service URL** in modo che può essere configurati per l'integrazione di SSO.</span><span class="sxs-lookup"><span data-stu-id="b1273-202">Also provide hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="b1273-203">Ricordare toohello Merces team necessarie per l'integrazione hello toobe ID entità impostata con il modello di hello **https://hr2day.force.com/INSTANCENAME**.</span><span class="sxs-lookup"><span data-stu-id="b1273-203">Mention toohello Merces team that this integration needs hello Entity ID toobe set with hello pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="b1273-204">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="b1273-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b1273-205">Dopo aver aggiunto questa app da hello **Active Directory** > **applicazioni aziendali** sezione, seleziona hello **Single Sign-On** scheda. Quindi hello accesso incorporati documentazione tramite hello **configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b1273-205">After you add this app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab. Then access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b1273-206">Altre informazioni sulla funzionalità di documentazione embedded hello in hello [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="b1273-206">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b1273-207">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1273-207">Create an Azure AD test user</span></span>
<span data-ttu-id="b1273-208">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b1273-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b1273-210">**un utente di prova in Azure AD, toocreate richiedere hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b1273-210">**toocreate a test user in Azure AD, take hello following steps:**</span></span>

1. <span data-ttu-id="b1273-211">In hello **portale di Azure**, nel riquadro di spostamento a sinistra di hello, selezionare hello **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b1273-211">In hello **Azure portal**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b1273-213">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi selezionare **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="b1273-213">toodisplay hello list of users, go too**Users and groups**, and then select **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b1273-215">hello tooopen **utente** nella finestra di dialogo **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="b1273-215">tooopen hello **User** dialog box, select **Add** on hello top of hello dialog box.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b1273-217">In hello **utente** nella finestra di dialogo hello take alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b1273-217">In hello **User** dialog box, take hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b1273-219">a.</span><span class="sxs-lookup"><span data-stu-id="b1273-219">a.</span></span> <span data-ttu-id="b1273-220">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b1273-220">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b1273-221">b.</span><span class="sxs-lookup"><span data-stu-id="b1273-221">b.</span></span> <span data-ttu-id="b1273-222">In hello **nome utente** casella, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b1273-222">In hello **User name** box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b1273-223">c.</span><span class="sxs-lookup"><span data-stu-id="b1273-223">c.</span></span> <span data-ttu-id="b1273-224">Selezionare **Show Password**e quindi annotare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="b1273-224">Select **Show Password**, and then write down hello password.</span></span>

    <span data-ttu-id="b1273-225">d.</span><span class="sxs-lookup"><span data-stu-id="b1273-225">d.</span></span> <span data-ttu-id="b1273-226">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b1273-226">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="b1273-227">Creare un utente di test di HR2day Merces</span><span class="sxs-lookup"><span data-stu-id="b1273-227">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="b1273-228">obiettivo di Hello di questa sezione è un utente chiamato Britta Simon in HR2day da Merces toocreate.</span><span class="sxs-lookup"><span data-stu-id="b1273-228">hello objective of this section is toocreate a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="b1273-229">gli utenti di hello tooadd nell'account hello HR2day, lavorare con hello [HR2day dal team di supporto client Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="b1273-229">tooadd hello users in hello HR2day account, work with hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="b1273-230">Se è necessario un utente toocreate manualmente, contattare hello [HR2day dal team di supporto client Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="b1273-230">If you need toocreate a user manually, contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b1273-231">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1273-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b1273-232">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooHR2day proprio accesso da Merces.</span><span class="sxs-lookup"><span data-stu-id="b1273-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHR2day by Merces.</span></span>

![Assegnare utenti][200] 

<span data-ttu-id="b1273-234">**tooassign Britta Simon tooHR2day da Merces, richiedere hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b1273-234">**tooassign Britta Simon tooHR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="b1273-235">In hello Azure hello portale, aprire applicazioni consente di visualizzare, Vai a visualizzazione directory toohello e quindi andare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b1273-235">In hello Azure portal, open hello applications view, go toohello directory view, and then go too**Enterprise applications**.</span></span> <span data-ttu-id="b1273-236">Selezionare quindi **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b1273-236">Next, select **All applications**.</span></span>

    ![Assegnare utenti][201] 

2. <span data-ttu-id="b1273-238">Nell'elenco di applicazioni hello, selezionare **HR2day da Merces**.</span><span class="sxs-lookup"><span data-stu-id="b1273-238">In hello applications list, select **HR2day by Merces**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="b1273-240">Dal menu hello hello sinistra, selezionare **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b1273-240">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Assegnare utenti][202] 

4. <span data-ttu-id="b1273-242">Seleziona hello **Aggiungi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="b1273-242">Select hello **Add** button.</span></span> <span data-ttu-id="b1273-243">Quindi, nel hello **Aggiungi** nella finestra di dialogo **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b1273-243">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Assegnare utenti][203]

5. <span data-ttu-id="b1273-245">In hello **utenti e gruppi** della finestra di dialogo hello **utenti** elenco, selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b1273-245">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="b1273-246">Fare clic su hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="b1273-246">Click hello **Select** button.</span></span>

7. <span data-ttu-id="b1273-247">In hello **Aggiungi** nella finestra di dialogo **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="b1273-247">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b1273-248">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b1273-248">Test single sign-on</span></span>

<span data-ttu-id="b1273-249">obiettivo di questa sezione Hello è tootest hello di configurazione di Azure AD single sign-on tramite Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b1273-249">hello objective of this section is tootest your Azure AD single sign-on configuration by using hello Access Panel.</span></span>  

<span data-ttu-id="b1273-250">Quando si seleziona hello HR2day dal riquadro Merces in hello Pannello di accesso, l'utente automaticamente ottenere connesso tooyour HR2day dall'applicazione Merces.</span><span class="sxs-lookup"><span data-stu-id="b1273-250">When you select hello HR2day by Merces tile in hello Access Panel, you automatically get signed in  tooyour HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1273-251">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b1273-251">Additional resources</span></span>

* [<span data-ttu-id="b1273-252">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1273-252">List of tutorials about how tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1273-253">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1273-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

