---
title: 'Autenticazione dell''utente finale: Data Lake Store con Azure Active Directory | Documentazione Microsoft'
description: Informazioni su come l'autenticazione degli utenti finali tooachieve con archivio Data Lake tramite Azure Active Directory
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="78077-103">Autenticazione dell'utente finale con Data Lake Store tramite Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78077-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="78077-104">Autenticazione da servizio a servizio</span><span class="sxs-lookup"><span data-stu-id="78077-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="78077-105">Autenticazione dell'utente finale</span><span class="sxs-lookup"><span data-stu-id="78077-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="78077-106">Azure Data Lake Store usa Azure Active Directory per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="78077-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="78077-107">Prima di creazione di un'applicazione che funziona con archivio Azure Data Lake o Azure Data Lake Analitica, è necessario innanzitutto decidere come tooauthenticate l'applicazione con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78077-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like tooauthenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="78077-108">Hello due opzioni disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="78077-108">hello two main options available are:</span></span>

* <span data-ttu-id="78077-109">Autenticazione dell'utente finale (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="78077-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="78077-110">Autenticazione da servizio a servizio</span><span class="sxs-lookup"><span data-stu-id="78077-110">Service-to-service authentication</span></span>

<span data-ttu-id="78077-111">Entrambe queste opzioni comportare l'applicazione viene fornita con un token OAuth 2.0, che ottiene tooeach collegato richiesta effettuata tooAzure archivio Data Lake o Azure Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="78077-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached tooeach request made tooAzure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="78077-112">Questo articolo illustra come creare un'**applicazione nativa di Azure AD per l'autenticazione dell'utente finale**.</span><span class="sxs-lookup"><span data-stu-id="78077-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="78077-113">Per istruzioni sulla configurazione dell'applicazione Azure AD per l'autenticazione da servizio a servizio, vedere [Autenticazione da servizio a servizio con Data Lake Store tramite Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="78077-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78077-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="78077-114">Prerequisites</span></span>
* <span data-ttu-id="78077-115">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="78077-115">An Azure subscription.</span></span> <span data-ttu-id="78077-116">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78077-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="78077-117">ID sottoscrizione personale.</span><span class="sxs-lookup"><span data-stu-id="78077-117">Your subscription ID.</span></span> <span data-ttu-id="78077-118">È possibile recuperarlo dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="78077-118">You can retrieve it from hello Azure Portal.</span></span> <span data-ttu-id="78077-119">Ad esempio, è disponibile dal Pannello di account archivio Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="78077-119">For example, it is available from hello Data Lake Store account blade.</span></span>
  
    ![Ottenere l'ID sottoscrizione](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="78077-121">Il nome di dominio di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78077-121">Your Azure AD domain name.</span></span> <span data-ttu-id="78077-122">È possibile recuperarlo dal passaggio del mouse hello nell'angolo superiore destro di hello di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="78077-122">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure Portal.</span></span> <span data-ttu-id="78077-123">Dalla schermata hello riportata di seguito, il nome di dominio hello è **contoso.onmicrosoft.com**, e hello GUID racchiuso tra parentesi quadre è hello ID del tenant.</span><span class="sxs-lookup"><span data-stu-id="78077-123">From hello screenshot below, hello domain name is **contoso.onmicrosoft.com**, and hello GUID within brackets is hello tenant ID.</span></span> 
  
    ![Ottenere il dominio AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="78077-125">Autenticazione dell'utente finale</span><span class="sxs-lookup"><span data-stu-id="78077-125">End-user authentication</span></span>
<span data-ttu-id="78077-126">Si tratta di hello approccio consigliato se si desidera un toolog gestito dall'utente nell'applicazione tooyour tramite Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78077-126">This is hello recommended approach if you want an end-user toolog in tooyour application via Azure AD.</span></span> <span data-ttu-id="78077-127">L'applicazione sarà in grado di tooaccess risorse di Azure con hello stesso livello di accesso dell'utente finale di hello connesso.</span><span class="sxs-lookup"><span data-stu-id="78077-127">Your application will be able tooaccess Azure resources with hello same level of access as hello end-user that logged in.</span></span> <span data-ttu-id="78077-128">L'utente finale sarà necessario tooprovide le proprie credenziali periodicamente in modo che l'accesso toomaintain dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="78077-128">Your end-user will need tooprovide their credentials periodically in order for your application toomaintain access.</span></span>

<span data-ttu-id="78077-129">il risultato di Hello dell'utente finale di hello Accedi è che l'applicazione viene fornito un token di accesso e un token di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="78077-129">hello result of having hello end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="78077-130">token di accesso Hello Ottiene richiesta tooeach collegato archivio Lake tooData o Data Lake Analitica, e è valido per un'ora per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="78077-130">hello access token gets attached tooeach request made tooData Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="78077-131">token di aggiornamento Hello può essere utilizzato tooobtain un nuovo token di accesso e è valido per le settimane tootwo per impostazione predefinita, se utilizzate regolarmente.</span><span class="sxs-lookup"><span data-stu-id="78077-131">hello refresh token can be used tooobtain a new access token, and it is valid for up tootwo weeks by default, if used regularly.</span></span> <span data-ttu-id="78077-132">È possibile usare due diversi approcci per l'accesso degli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="78077-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-hello-oauth-20-pop-up"></a><span data-ttu-id="78077-133">Utilizzando i menu a comparsa hello OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="78077-133">Using hello OAuth 2.0 pop-up</span></span>
<span data-ttu-id="78077-134">L'applicazione può attivare un popup di autorizzazione OAuth 2.0, in cui hello degli utenti finali possono immettere le credenziali.</span><span class="sxs-lookup"><span data-stu-id="78077-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which hello end-user can enter their credentials.</span></span> <span data-ttu-id="78077-135">Questa opzione funziona anche con il processo di autenticazione di Azure AD a due fattori (2FA) hello, se necessario.</span><span class="sxs-lookup"><span data-stu-id="78077-135">This pop-up also works with hello Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="78077-136">Questo metodo non ancora supportato in hello Azure AD Authentication Library (ADAL) per Python o Java.</span><span class="sxs-lookup"><span data-stu-id="78077-136">This method is not yet supported in hello Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="78077-137">Accesso diretto tramite le credenziali dell'utente</span><span class="sxs-lookup"><span data-stu-id="78077-137">Directly passing in user credentials</span></span>
<span data-ttu-id="78077-138">L'applicazione può fornire direttamente tooAzure le credenziali utente Active Directory.</span><span class="sxs-lookup"><span data-stu-id="78077-138">Your application can directly provide user credentials tooAzure AD.</span></span> <span data-ttu-id="78077-139">Questo metodo funziona solo con gli account utente con ID organizzazione. Non è compatibile con gli account utente personali/con "ID dinamico", inclusi quelli che terminano con @outlook.com o @live.com. Inoltre, questo metodo non è compatibile con gli account utente che richiedono l'autenticazione a due fattori (2FA) di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78077-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com. Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-toouse-this-approach"></a><span data-ttu-id="78077-140">Che cosa è necessario toouse questo approccio?</span><span class="sxs-lookup"><span data-stu-id="78077-140">What do I need toouse this approach?</span></span>
* <span data-ttu-id="78077-141">Il nome di dominio di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78077-141">Azure AD domain name.</span></span> <span data-ttu-id="78077-142">È già elencata nel prerequisito hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="78077-142">This is already listed in hello prerequisite of this article.</span></span>
* <span data-ttu-id="78077-143">**L'applicazione nativa** di Azure AD</span><span class="sxs-lookup"><span data-stu-id="78077-143">Azure AD **native application**</span></span>
* <span data-ttu-id="78077-144">ID dell'applicazione nativa hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="78077-144">Application ID for hello Azure AD native application</span></span>
* <span data-ttu-id="78077-145">URI di reindirizzamento per hello applicazione nativa AD Azure</span><span class="sxs-lookup"><span data-stu-id="78077-145">Redirect URI for hello Azure AD native application</span></span>
* <span data-ttu-id="78077-146">Impostare autorizzazioni delegate</span><span class="sxs-lookup"><span data-stu-id="78077-146">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="78077-147">Passaggio 1: creare un'applicazione nativa di Active Directory</span><span class="sxs-lookup"><span data-stu-id="78077-147">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="78077-148">Creare e configurare un'applicazione nativa di Azure AD per l'autenticazione dell'utente finale con Azure Data Lake Store tramite Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="78077-148">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="78077-149">Per istruzioni, vedere [Creare un'applicazione Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78077-149">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="78077-150">Seguendo le istruzioni di hello in hello di sopra di collegamento, assicurarsi di selezionare **nativo** per il tipo di applicazione, come illustrato nella schermata di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="78077-150">While following hello instructions at hello above link, make sure you select **Native** for application type, as shown in hello screenshot below.</span></span>

<span data-ttu-id="78077-151">![Creare un'app Web](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Creare un'app nativa")</span><span class="sxs-lookup"><span data-stu-id="78077-151">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="78077-152">Passaggio 2: ottenere l'ID dell'applicazione e l'URI di reindirizzamento</span><span class="sxs-lookup"><span data-stu-id="78077-152">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="78077-153">Vedere [Ottieni ID applicazione hello](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello id applicazione (detto anche l'ID client hello nel portale di Azure classico hello) di un'applicazione nativa hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78077-153">See [Get hello application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello application id (also called hello client ID in hello Azure classic portal) of hello Azure AD native application.</span></span>

<span data-ttu-id="78077-154">hello tooretrieve URI di reindirizzamento, attenersi alla procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="78077-154">tooretrieve hello redirect URI, follow hello steps below.</span></span>

1. <span data-ttu-id="78077-155">Hello portale di Azure, selezionare **Azure Active Directory**, fare clic su **registrazioni di App**, quindi individuare e fare clic su un'applicazione nativa hello Azure AD appena creato.</span><span class="sxs-lookup"><span data-stu-id="78077-155">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="78077-156">Da hello **impostazioni** pannello per un'applicazione hello, fare clic su **Redirect URIs**.</span><span class="sxs-lookup"><span data-stu-id="78077-156">From hello **Settings** blade for hello application, click **Redirect URIs**.</span></span>

    ![Ottenere l'URI di reindirizzamento](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="78077-158">Copiare il valore di hello visualizzato.</span><span class="sxs-lookup"><span data-stu-id="78077-158">Copy hello value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="78077-159">Passaggio 3: Impostare le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="78077-159">Step 3: Set permissions</span></span>

1. <span data-ttu-id="78077-160">Hello portale di Azure, selezionare **Azure Active Directory**, fare clic su **registrazioni di App**, quindi individuare e fare clic su un'applicazione nativa hello Azure AD appena creato.</span><span class="sxs-lookup"><span data-stu-id="78077-160">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="78077-161">Da hello **impostazioni** pannello per un'applicazione hello, fare clic su **delle autorizzazioni necessarie**, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="78077-161">From hello **Settings** blade for hello application, click **Required permissions**, and then click **Add**.</span></span>

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="78077-163">In hello **aggiungere l'accesso all'API** pannello, fare clic su **selezionare un'API**, fare clic su **Azure Data Lake**, quindi fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="78077-163">In hello **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="78077-165">In hello **aggiungere l'accesso all'API** pannello, fare clic su **selezionare le autorizzazioni**, selezionare hello toogive casella di controllo **accesso completo archivio Lake tooData**, quindi fare clic su **selezionare** .</span><span class="sxs-lookup"><span data-stu-id="78077-165">In hello **Add API Access** blade, click **Select permissions**, select hello check box toogive **Full access tooData Lake Store**, and then click **Select**.</span></span>

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="78077-167">Fare clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="78077-167">Click **Done**.</span></span>

5. <span data-ttu-id="78077-168">Ripetizione hello ultimi due passaggi toogrant le autorizzazioni per **API di gestione del servizio di Windows Azure** anche.</span><span class="sxs-lookup"><span data-stu-id="78077-168">Repeat hello last two steps toogrant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="78077-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="78077-169">Next steps</span></span>
<span data-ttu-id="78077-170">In questo articolo è stata creata un'applicazione nativa AD Azure e raccolte informazioni hello che è necessario nelle applicazioni client che si creano utilizzando il SDK di .NET SDK per Java, API REST, e così via. È ora possibile procedere toohello seguenti articoli in cui descrivere come toofirst di applicazione web di toouse hello Azure AD eseguire l'autenticazione con l'archivio Data Lake ed eseguono altre operazioni sull'archivio hello.</span><span class="sxs-lookup"><span data-stu-id="78077-170">In this article you created an Azure AD native application and gathered hello information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed toohello following articles that talk about how toouse hello Azure AD web application toofirst authenticate with Data Lake Store and then perform other operations on hello store.</span></span>

* [<span data-ttu-id="78077-171">Introduzione a Azure Data Lake Store utilizzando .NET SDK</span><span class="sxs-lookup"><span data-stu-id="78077-171">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="78077-172">Introduzione ad Azure Data Lake Store con Java SDK</span><span class="sxs-lookup"><span data-stu-id="78077-172">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="78077-173">Introduzione ad Azure Data Lake Store con API REST</span><span class="sxs-lookup"><span data-stu-id="78077-173">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

