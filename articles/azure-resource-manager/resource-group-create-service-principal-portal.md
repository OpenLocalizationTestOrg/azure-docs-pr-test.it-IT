---
title: "identità aaaCreate per app nel portale di Azure | Documenti Microsoft"
description: "Viene descritto come toocreate una nuova applicazione Azure Active Directory e il servizio dell'entità che può essere usato con il controllo di accesso basato sui ruoli hello in Gestione risorse di Azure toomanage accedere tooresources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="7f6c8-103">Utilizzare portale toocreate un'applicazione Azure Active Directory e dell'entità servizio che possono accedere alle risorse</span><span class="sxs-lookup"><span data-stu-id="7f6c8-103">Use portal toocreate an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="7f6c8-104">Quando si dispone di un'applicazione che richiede tooaccess o modifica le risorse, è necessario configurare un'applicazione Azure Active Directory (AD) e assegnare tooit autorizzazioni hello necessario.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-104">When you have an application that needs tooaccess or modify resources, you must set up an Azure Active Directory (AD) application and assign hello required permissions tooit.</span></span> <span data-ttu-id="7f6c8-105">Questo approccio è preferibile toorunning hello app con le proprie credenziali perché:</span><span class="sxs-lookup"><span data-stu-id="7f6c8-105">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="7f6c8-106">È possibile assegnare le autorizzazioni di identità app toohello che sono diverse dalle proprie autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-106">You can assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="7f6c8-107">In genere, queste autorizzazioni sono limitate tooexactly quali app hello deve toodo.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-107">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="7f6c8-108">Non si dispone delle credenziali dell'applicazione hello toochange se Modifica responsabilità dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-108">You do not have toochange hello app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="7f6c8-109">Quando si esegue uno script automatico, è possibile utilizzare l'autenticazione tooautomate un certificato.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-109">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>

<span data-ttu-id="7f6c8-110">Questo argomento viene illustrato come tooperform quelli passaggi tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-110">This topic shows you how tooperform those steps through hello portal.</span></span> <span data-ttu-id="7f6c8-111">Si concentra in un'applicazione single-tenant in cui un'applicazione hello è previsto toorun all'interno del sola organizzazione.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-111">It focuses on a single-tenant application where hello application is intended toorun within only one organization.</span></span> <span data-ttu-id="7f6c8-112">Le applicazioni con un tenant singolo si usano in genere per applicazioni line-of-business eseguite all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="7f6c8-113">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="7f6c8-113">Required permissions</span></span>
<span data-ttu-id="7f6c8-114">toocomplete in questo argomento, è necessario disporre di un'applicazione tooregister di autorizzazioni sufficienti con tenant di Azure AD e assegnare ruoli di tooa applicazione hello nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-114">toocomplete this topic, you must have sufficient permissions tooregister an application with your Azure AD tenant, and assign hello application tooa role in your Azure subscription.</span></span> <span data-ttu-id="7f6c8-115">Verifichiamo che tu sia che è hello delle corrette autorizzazioni tooperform questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-115">Let's make sure you have hello right permissions tooperform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="7f6c8-116">Controllare le autorizzazioni di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f6c8-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="7f6c8-117">Accedi tooyour Account Azure tramite hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f6c8-117">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7f6c8-118">Selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-118">Select **Azure Active Directory**.</span></span>

     ![Selezionare Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="7f6c8-120">In Azure Active Directory selezionare **Impostazioni utente**.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-120">In Azure Active Directory, select **User settings**.</span></span>

     ![Selezionare Impostazioni utente](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="7f6c8-122">Controllare hello **registrazioni di App** impostazione.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-122">Check hello **App registrations** setting.</span></span> <span data-ttu-id="7f6c8-123">Se impostato troppo**Sì**, gli utenti non amministratori possono registrare le app di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-123">If set too**Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="7f6c8-124">Questa impostazione indica che qualsiasi utente nel tenant di Azure AD hello può registrare un'app.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-124">This setting means any user in hello Azure AD tenant can register an app.</span></span> <span data-ttu-id="7f6c8-125">È possibile procedere troppo[autorizzazioni della sottoscrizione Azure controllare](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="7f6c8-125">You can proceed too[Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![Visualizzare le registrazioni dell'app](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="7f6c8-127">Se le registrazioni di app hello impostazione è troppo**n**, solo gli utenti amministratori possono registrare le app.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-127">If hello app registrations setting is set too**No**, only admin users can register apps.</span></span> <span data-ttu-id="7f6c8-128">È necessario toocheck se l'account è un amministratore per il tenant di Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-128">You need toocheck whether your account is an admin for hello Azure AD tenant.</span></span> <span data-ttu-id="7f6c8-129">Selezionare **Panoramica** e **Trova un utente** da Attività rapide.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![Trova un utente](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="7f6c8-131">Cercare il proprio account e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-131">Search for your account, and select it when you find it.</span></span>

     ![Cercare un utente](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="7f6c8-133">Per il proprio account selezionare **Ruolo della directory**.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-133">For your account, select **Directory role**.</span></span> 

     ![Ruolo della directory](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="7f6c8-135">Visualizzare il proprio ruolo della directory assegnato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="7f6c8-136">Se l'account viene assegnato il ruolo di utente toohello, ma impostazioni di registrazione dell'app (da hello passaggi precedenti) hello sono limitato tooadmin utenti, chiedere tooeither l'amministratore assegna si tooan ruolo di amministratore o tooenable utenti tooregister app.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-136">If your account is assigned toohello User role, but hello app registration setting (from hello preceding steps) is limited tooadmin users, ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

     ![Visualizzare il ruolo](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="7f6c8-138">Controllare le autorizzazioni di sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="7f6c8-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="7f6c8-139">Nella sottoscrizione di Azure, è necessario che l'account `Microsoft.Authorization/*/Write` tooassign un ruolo di tooa AD app di accedere.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access tooassign an AD app tooa role.</span></span> <span data-ttu-id="7f6c8-140">Questa azione viene concesso tramite hello [proprietario](../active-directory/role-based-access-built-in-roles.md#owner) ruolo o [amministratore di accesso utente](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) ruolo.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-140">This action is granted through hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="7f6c8-141">Se l'account viene assegnata toohello **collaboratore** ruolo, non si dispone dell'autorizzazione appropriata.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-141">If your account is assigned toohello **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="7f6c8-142">Si riceverà un errore durante il tentativo di ruolo tooa principale del servizio tooassign hello.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-142">You will receive an error when attempting tooassign hello service principal tooa role.</span></span> 

<span data-ttu-id="7f6c8-143">toocheck le autorizzazioni della sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="7f6c8-143">toocheck your subscription permissions:</span></span>

1. <span data-ttu-id="7f6c8-144">Se non già desiderata al proprio account Azure AD da hello passaggi precedenti, selezionare **Azure Active Directory** hello nel riquadro di sinistra.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-144">If you are not already looking at your Azure AD account from hello preceding steps, select **Azure Active Directory** from hello left pane.</span></span>

2. <span data-ttu-id="7f6c8-145">Trovare il proprio account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-145">Find your Azure AD account.</span></span> <span data-ttu-id="7f6c8-146">Selezionare **Panoramica** e **Trova un utente** da Attività rapide.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![Trova un utente](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="7f6c8-148">Cercare il proprio account e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-148">Search for your account, and select it when you find it.</span></span>

     ![Cercare un utente](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="7f6c8-150">Selezionare **Risorse di Azure**.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-150">Select **Azure resources**.</span></span>

     ![Selezionare le risorse](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="7f6c8-152">Consente di visualizzare i ruoli assegnati e determinare se si dispone delle autorizzazioni appropriate tooassign un ruolo di tooa AD app.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-152">View your assigned roles, and determine if you have adequate permissions tooassign an AD app tooa role.</span></span> <span data-ttu-id="7f6c8-153">In caso contrario, chiedere il tooadd amministratore sottoscrizione si tooUser accesso ruolo di amministratore.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-153">If not, ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span> <span data-ttu-id="7f6c8-154">Hello seguente immagine, hello utente è assegnato toohello ruolo di proprietario per le sottoscrizioni di due, il che significa che l'utente disponga delle autorizzazioni adeguate.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-154">In hello following image, hello user is assigned toohello Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![Visualizzare le autorizzazioni](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="7f6c8-156">Creare un'applicazione Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f6c8-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="7f6c8-157">Accedi tooyour Account Azure tramite hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f6c8-157">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7f6c8-158">Selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-158">Select **Azure Active Directory**.</span></span>

     ![Selezionare Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="7f6c8-160">Selezionare **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-160">Select **App registrations**.</span></span>   

     ![Selezionare Registrazioni per l'app](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="7f6c8-162">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-162">Select **Add**.</span></span>

     ![Aggiungere l'app](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="7f6c8-164">Fornire un nome e l'URL per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-164">Provide a name and URL for hello application.</span></span> <span data-ttu-id="7f6c8-165">Selezionare l'opzione **app Web / API** o **nativo** per il tipo di hello dell'applicazione si desidera toocreate.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-165">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="7f6c8-166">Dopo aver impostato i valori hello, selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-166">After setting hello values, select **Create**.</span></span>

     ![assegnare un nome all'applicazione](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="7f6c8-168">L'applicazione è stata creata.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="7f6c8-169">Ottenere l'ID applicazione e la chiave di autenticazione</span><span class="sxs-lookup"><span data-stu-id="7f6c8-169">Get application ID and authentication key</span></span>
<span data-ttu-id="7f6c8-170">Durante l'accesso a livello di codice, è necessario hello ID per l'applicazione e una chiave di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-170">When programmatically logging in, you need hello ID for your application and an authentication key.</span></span> <span data-ttu-id="7f6c8-171">tooget tali valori, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7f6c8-171">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="7f6c8-172">Da **Registrazioni dell'app** in Azure Active Directory selezionare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![Selezionare l'applicazione](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="7f6c8-174">Hello copia **ID applicazione** e archiviarlo nel codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-174">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="7f6c8-175">le applicazioni in hello Hello [applicazioni di esempio](#sample-applications) sezione valore toothis hello client id di riferimento.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-175">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![ID CLIENT](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="7f6c8-177">Selezionare una chiave di autenticazione, toogenerate **chiavi**.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-177">toogenerate an authentication key, select **Keys**.</span></span>

     ![Selezionare Chiavi](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="7f6c8-179">Fornire una descrizione della chiave hello e una durata per la chiave di hello.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-179">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="7f6c8-180">Al termine scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-180">When done, select **Save**.</span></span>

     ![Salvare la chiave](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="7f6c8-182">Dopo aver salvato chiave hello, viene visualizzato il valore di hello della chiave di hello.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-182">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="7f6c8-183">Copiare questo valore perché non si è in grado di tooretrieve chiave di hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-183">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="7f6c8-184">Fornire valore chiave hello con toolog ID applicazione di hello in come un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-184">You provide hello key value with hello application ID toolog in as hello application.</span></span> <span data-ttu-id="7f6c8-185">Archiviare il valore di chiave hello in cui l'applicazione può recuperare.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-185">Store hello key value where your application can retrieve it.</span></span>

     ![chiave salvata](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="7f6c8-187">Ottenere l'ID tenant</span><span class="sxs-lookup"><span data-stu-id="7f6c8-187">Get tenant ID</span></span>
<span data-ttu-id="7f6c8-188">Durante l'accesso a livello di codice, è necessario l'ID tenant hello toopass con la richiesta di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-188">When programmatically logging in, you need toopass hello tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="7f6c8-189">ID tenant tooget hello selezionare **proprietà** per tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-189">tooget hello tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![selezionare le proprietà di Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="7f6c8-191">Hello copia **ID Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-191">Copy hello **Directory ID**.</span></span> <span data-ttu-id="7f6c8-192">Questo valore è l'ID tenant.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-192">This value is your tenant ID.</span></span>

     ![tenant id](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a><span data-ttu-id="7f6c8-194">Assegnare l'applicazione toorole</span><span class="sxs-lookup"><span data-stu-id="7f6c8-194">Assign application toorole</span></span>
<span data-ttu-id="7f6c8-195">tooaccess risorse nella sottoscrizione, è necessario assegnare ruoli di tooa applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-195">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="7f6c8-196">Decidere quale ruolo rappresenta hello delle autorizzazioni necessarie per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-196">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="7f6c8-197">toolearn sui ruoli disponibile hello, vedere [RBAC: compilato nei ruoli](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="7f6c8-197">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="7f6c8-198">È possibile impostare l'ambito hello a livello di hello di sottoscrizione hello, gruppo di risorse o la risorsa.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-198">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="7f6c8-199">Le autorizzazioni sono ereditate toolower livelli di ambito.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-199">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="7f6c8-200">Ad esempio, l'aggiunta di un ruolo di lettore toohello applicazione per un gruppo di risorse che significa che può leggere il gruppo di risorse hello e tutte le risorse che contiene.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-200">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="7f6c8-201">Passa al livello toohello dell'ambito desiderato per un'applicazione hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-201">Navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="7f6c8-202">Ad esempio, di selezionare un ruolo nell'ambito di sottoscrizione hello di tooassign **sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-202">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="7f6c8-203">In alternativa è possibile selezionare una risorsa o un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-203">You could instead select a resource group or resource.</span></span>

     ![selezionare la sottoscrizione](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="7f6c8-205">Selezionare la sottoscrizione specifica (gruppo di risorse o risorsa) tooassign hello applicazione hello per.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-205">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![selezionare la sottoscrizione per l'assegnazione](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="7f6c8-207">Selezionare **Controllo di accesso (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-207">Select **Access Control (IAM)**.</span></span>

     ![selezionare accesso](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="7f6c8-209">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-209">Select **Add**.</span></span>

     ![selezionare aggiungi](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="7f6c8-211">Selezionare il ruolo di hello desiderato tooassign toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-211">Select hello role you wish tooassign toohello application.</span></span> <span data-ttu-id="7f6c8-212">Hello immagine seguente viene illustrato hello **lettore** ruolo.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-212">hello following image shows hello **Reader** role.</span></span>

     ![selezionare il ruolo](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="7f6c8-214">Cercare l'applicazione e selezionarla.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-214">Search for your application, and select it.</span></span>

     ![Cercare l'app](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="7f6c8-216">Selezionare **OK** toofinish l'assegnazione di ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-216">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="7f6c8-217">Viene visualizzata l'applicazione nell'elenco di hello di utenti con ruolo tooa per tale ambito.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-217">You see your application in hello list of users assigned tooa role for that scope.</span></span>

## <a name="log-in-as-hello-application"></a><span data-ttu-id="7f6c8-218">Accedere come un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="7f6c8-218">Log in as hello application</span></span>

<span data-ttu-id="7f6c8-219">L'applicazione è ora configurata in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="7f6c8-220">È necessario un ID e toouse chiave per l'accesso come un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-220">You have an ID and key toouse for signing in as hello application.</span></span> <span data-ttu-id="7f6c8-221">un'applicazione Hello viene assegnata il ruolo tooa che fornisce alcune azioni che è possibile eseguire.</span><span class="sxs-lookup"><span data-stu-id="7f6c8-221">hello application is assigned tooa role that gives it certain actions it can perform.</span></span> <span data-ttu-id="7f6c8-222">Per informazioni su come un'applicazione hello tramite diverse piattaforme, vedere:</span><span class="sxs-lookup"><span data-stu-id="7f6c8-222">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="7f6c8-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f6c8-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="7f6c8-224">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="7f6c8-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="7f6c8-225">REST</span><span class="sxs-lookup"><span data-stu-id="7f6c8-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="7f6c8-226">.NET</span><span class="sxs-lookup"><span data-stu-id="7f6c8-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="7f6c8-227">Java</span><span class="sxs-lookup"><span data-stu-id="7f6c8-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="7f6c8-228">Node.js</span><span class="sxs-lookup"><span data-stu-id="7f6c8-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="7f6c8-229">Python</span><span class="sxs-lookup"><span data-stu-id="7f6c8-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="7f6c8-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="7f6c8-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="7f6c8-231">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f6c8-231">Next steps</span></span>
* <span data-ttu-id="7f6c8-232">tooset backup di un'applicazione multi-tenant, vedere [tooauthorization di Guida per gli sviluppatori con API di gestione risorse di Azure hello](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7f6c8-232">tooset up a multi-tenant application, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="7f6c8-233">toolearn sull'impostazione di criteri di sicurezza, vedere [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="7f6c8-233">toolearn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="7f6c8-234">Per un elenco di azioni disponibili che possono essere concesse o negate toousers, vedere [operazioni di Provider di risorse di Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="7f6c8-234">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
