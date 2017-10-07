---
title: 'Esercitazione: Integrazione di Azure Active Directory con Lesson.ly | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Lesson.ly.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 23b339dcc26471b42aaa7e1baadcb42500d6b7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="4f12a-103">Esercitazione: Integrazione di Azure Active Directory con Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="4f12a-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>

<span data-ttu-id="4f12a-104">In questa esercitazione, è illustrato come toointegrate Lesson.ly con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4f12a-104">In this tutorial, you learn how toointegrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4f12a-105">Integrazione Lesson.ly con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4f12a-105">Integrating Lesson.ly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4f12a-106">È possibile controllare in Azure AD che ha accesso tooLesson.ly</span><span class="sxs-lookup"><span data-stu-id="4f12a-106">You can control in Azure AD who has access tooLesson.ly</span></span>
- <span data-ttu-id="4f12a-107">È possibile abilitare l'utenti tooautomatically get connesso tooLesson.ly (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f12a-107">You can enable your users tooautomatically get signed-on tooLesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4f12a-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4f12a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4f12a-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4f12a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f12a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4f12a-110">Prerequisites</span></span>

<span data-ttu-id="4f12a-111">integrazione di Azure AD con Lesson.ly tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4f12a-111">tooconfigure Azure AD integration with Lesson.ly, you need hello following items:</span></span>

- <span data-ttu-id="4f12a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f12a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4f12a-113">Sottoscrizione di Lesson.ly abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4f12a-113">A Lesson.ly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4f12a-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4f12a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4f12a-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4f12a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4f12a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4f12a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4f12a-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4f12a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4f12a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4f12a-118">Scenario description</span></span>
<span data-ttu-id="4f12a-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4f12a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4f12a-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4f12a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4f12a-121">Aggiunta di Lesson.ly dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4f12a-121">Adding Lesson.ly from hello gallery</span></span>
2. <span data-ttu-id="4f12a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f12a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-hello-gallery"></a><span data-ttu-id="4f12a-123">Aggiunta di Lesson.ly dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4f12a-123">Adding Lesson.ly from hello gallery</span></span>
<span data-ttu-id="4f12a-124">integrazione hello tooconfigure di Lesson.ly in Azure AD, è necessario tooadd Lesson.ly dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4f12a-124">tooconfigure hello integration of Lesson.ly into Azure AD, you need tooadd Lesson.ly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4f12a-125">**tooadd Lesson.ly dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4f12a-125">**tooadd Lesson.ly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f12a-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4f12a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4f12a-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4f12a-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4f12a-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4f12a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4f12a-133">Nella casella di ricerca hello, digitare **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-133">In hello search box, type **Lesson.ly**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_search.png)

5. <span data-ttu-id="4f12a-135">Nel riquadro dei risultati hello, selezionare **Lesson.ly**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4f12a-135">In hello results panel, select **Lesson.ly**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4f12a-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f12a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4f12a-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Lesson.ly in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4f12a-138">In this section, you configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4f12a-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Lesson.ly è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f12a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lesson.ly is tooa user in Azure AD.</span></span> <span data-ttu-id="4f12a-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Lesson.ly deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="4f12a-140">In other words, a link relationship between an Azure AD user and hello related user in Lesson.ly needs toobe established.</span></span>

<span data-ttu-id="4f12a-141">In Lesson.ly, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="4f12a-141">In Lesson.ly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4f12a-142">tooconfigure e prova AD Azure single sign-on con Lesson.ly, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4f12a-142">tooconfigure and test Azure AD single sign-on with Lesson.ly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4f12a-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4f12a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4f12a-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f12a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4f12a-145">**[Creazione di un utente test Lesson.ly](#creating-a-lessonly-test-user)**  -toohave un equivalente di Britta Simon in Lesson.ly che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4f12a-145">**[Creating a Lesson.ly test user](#creating-a-lessonly-test-user)** - toohave a counterpart of Britta Simon in Lesson.ly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4f12a-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4f12a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4f12a-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4f12a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4f12a-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f12a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4f12a-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="4f12a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lesson.ly application.</span></span>

<span data-ttu-id="4f12a-150">**Azure AD tooconfigure single sign-on con Lesson.ly, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4f12a-150">**tooconfigure Azure AD single sign-on with Lesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f12a-151">Nel portale di Azure su hello hello **Lesson.ly** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-151">In hello Azure portal, on hello **Lesson.ly** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4f12a-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4f12a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_samlbase.png)

3. <span data-ttu-id="4f12a-155">In hello **Lesson.ly dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4f12a-155">On hello **Lesson.ly Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_url.png)

    <span data-ttu-id="4f12a-157">a.</span><span class="sxs-lookup"><span data-stu-id="4f12a-157">a.</span></span> <span data-ttu-id="4f12a-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="4f12a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/signin`|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="4f12a-159">Quando assegna un nome che fanno riferimento a un oggetto generico che **companyname** deve toobe sostituito dal nome effettivo.</span><span class="sxs-lookup"><span data-stu-id="4f12a-159">When referencing a generic name that **companyname** needs toobe replaced by an actual name.</span></span>
    
    <span data-ttu-id="4f12a-160">b.</span><span class="sxs-lookup"><span data-stu-id="4f12a-160">b.</span></span> <span data-ttu-id="4f12a-161">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="4f12a-161">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/auth/saml/metadata`|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="4f12a-162">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="4f12a-162">These values are not real.</span></span> <span data-ttu-id="4f12a-163">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="4f12a-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4f12a-164">Contatto [team di supporto Lesson.ly Client](mailto:dev@lessonly.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="4f12a-164">Contact [Lesson.ly Client support team](mailto:dev@lessonly.com) tooget these values.</span></span> 

4. <span data-ttu-id="4f12a-165">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4f12a-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_certificate.png)

5. <span data-ttu-id="4f12a-167">Hello Lesson.ly applicazione prevede di asserzioni SAML hello in un formato specifico, che richiede il tooyour mapping di attributi personalizzati tooadd **attributi Token SAML** configuration.hello seguente schermata illustra un esempio di Questo metodo.</span><span class="sxs-lookup"><span data-stu-id="4f12a-167">hello Lesson.ly application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.hello following screenshot shows an example for this.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png)
           
6. <span data-ttu-id="4f12a-169">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine precedente hello ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4f12a-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="4f12a-170">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="4f12a-170">Attribute Name</span></span>   | <span data-ttu-id="4f12a-171">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="4f12a-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="4f12a-172">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="4f12a-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="4f12a-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="4f12a-173">user.givenname</span></span> |
    | <span data-ttu-id="4f12a-174">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="4f12a-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="4f12a-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="4f12a-175">user.surname</span></span> |
    | <span data-ttu-id="4f12a-176">urn: oid:0.9.2342.19200300.1001.3</span><span class="sxs-lookup"><span data-stu-id="4f12a-176">urn:oid:0.9.2342.19200300.1001.3</span></span> |<span data-ttu-id="4f12a-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="4f12a-177">user.mail</span></span> |

    <span data-ttu-id="4f12a-178">a.</span><span class="sxs-lookup"><span data-stu-id="4f12a-178">a.</span></span> <span data-ttu-id="4f12a-179">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4f12a-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="4f12a-182">b.</span><span class="sxs-lookup"><span data-stu-id="4f12a-182">b.</span></span> <span data-ttu-id="4f12a-183">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="4f12a-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="4f12a-184">c.</span><span class="sxs-lookup"><span data-stu-id="4f12a-184">c.</span></span> <span data-ttu-id="4f12a-185">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="4f12a-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4f12a-186">d.</span><span class="sxs-lookup"><span data-stu-id="4f12a-186">d.</span></span> <span data-ttu-id="4f12a-187">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-187">Click **Ok**.</span></span>     

7. <span data-ttu-id="4f12a-188">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4f12a-188">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lessonly-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4f12a-190">In hello **Lesson.ly configurazione** fare clic su **configurare Lesson.ly** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="4f12a-190">On hello **Lesson.ly Configuration** section, click **Configure Lesson.ly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4f12a-191">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="4f12a-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_configure.png)

9. <span data-ttu-id="4f12a-193">tooconfigure single sign-on sul **Lesson.ly** lato, è necessario hello toosend scaricato **Certificate(Base64)** e **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** troppo[team di supporto Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="4f12a-193">tooconfigure single sign-on on **Lesson.ly** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="4f12a-194">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="4f12a-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4f12a-195">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="4f12a-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4f12a-196">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4f12a-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4f12a-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f12a-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="4f12a-198">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4f12a-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4f12a-200">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4f12a-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f12a-201">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4f12a-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4f12a-203">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4f12a-205">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="4f12a-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4f12a-207">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4f12a-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4f12a-209">a.</span><span class="sxs-lookup"><span data-stu-id="4f12a-209">a.</span></span> <span data-ttu-id="4f12a-210">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4f12a-211">b.</span><span class="sxs-lookup"><span data-stu-id="4f12a-211">b.</span></span> <span data-ttu-id="4f12a-212">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4f12a-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4f12a-213">c.</span><span class="sxs-lookup"><span data-stu-id="4f12a-213">c.</span></span> <span data-ttu-id="4f12a-214">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4f12a-215">d.</span><span class="sxs-lookup"><span data-stu-id="4f12a-215">d.</span></span> <span data-ttu-id="4f12a-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-216">Click **Create**.</span></span>
 
### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="4f12a-217">Creazione di un utente test Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="4f12a-217">Creating a Lesson.ly test user</span></span>

<span data-ttu-id="4f12a-218">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Lesson.ly toocreate.</span><span class="sxs-lookup"><span data-stu-id="4f12a-218">hello objective of this section is toocreate a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="4f12a-219">Lesson.ly supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4f12a-219">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="4f12a-220">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="4f12a-220">There is no action item for you in this section.</span></span> <span data-ttu-id="4f12a-221">Verrà creato un nuovo utente durante una tooaccess tentativo Lesson.ly se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="4f12a-221">A new user will be created during an attempt tooaccess Lesson.ly if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="4f12a-222">Se è necessario un utente toocreate manualmente, è necessario hello toocontact [team di supporto Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="4f12a-222">If you need toocreate an user manually, you need toocontact hello [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4f12a-223">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f12a-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4f12a-224">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLesson.ly.</span><span class="sxs-lookup"><span data-stu-id="4f12a-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLesson.ly.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4f12a-226">**tooassign Britta Simon tooLesson.ly, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4f12a-226">**tooassign Britta Simon tooLesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f12a-227">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4f12a-229">Nell'elenco di applicazioni hello, selezionare **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-229">In hello applications list, select **Lesson.ly**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_app.png) 

3. <span data-ttu-id="4f12a-231">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4f12a-233">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-233">Click **Add** button.</span></span> <span data-ttu-id="4f12a-234">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4f12a-236">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="4f12a-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4f12a-237">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4f12a-238">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4f12a-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4f12a-239">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4f12a-239">Testing single sign-on</span></span>

<span data-ttu-id="4f12a-240">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4f12a-240">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4f12a-241">Quando si fa clic su riquadro Lesson.ly hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Lesson.ly applicazione.</span><span class="sxs-lookup"><span data-stu-id="4f12a-241">When you click hello Lesson.ly tile in hello Access Panel, you should get automatically signed-on tooyour Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4f12a-242">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4f12a-242">Additional resources</span></span>

* [<span data-ttu-id="4f12a-243">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f12a-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4f12a-244">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f12a-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_203.png

