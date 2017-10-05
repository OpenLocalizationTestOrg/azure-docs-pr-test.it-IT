---
title: "Creare un'identità per un'app Azure nel portale | Documentazione Microsoft"
description: "Descrive come creare una nuova applicazione ed entità servizio di Azure Active Directory da usare con il controllo degli accessi in base al ruolo in Gestione risorse di Azure per gestire l'accesso alle risorse."
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
ms.openlocfilehash: 5d24fb99e1095d53e5ea547e53b80178d9cb77c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-portal-to-create-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="8a040-103">Usare il portale per creare un'applicazione Azure Active Directory e un'entità servizio che possano accedere alle risorse</span><span class="sxs-lookup"><span data-stu-id="8a040-103">Use portal to create an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="8a040-104">Quando un'applicazione deve accedere alle risorse o modificarle, è necessario configurare un'applicazione Azure Active Directory (AD) a cui assegnare le autorizzazioni richieste.</span><span class="sxs-lookup"><span data-stu-id="8a040-104">When you have an application that needs to access or modify resources, you must set up an Azure Active Directory (AD) application and assign the required permissions to it.</span></span> <span data-ttu-id="8a040-105">Questo approccio è preferibile all'esecuzione dell'app con le credenziali dell'utente per i motivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a040-105">This approach is preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="8a040-106">È possibile assegnare all'identità dell'app autorizzazioni diverse rispetto a quelle dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8a040-106">You can assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="8a040-107">Tali autorizzazioni sono in genere limitate alle specifiche operazioni che devono essere eseguite dall'app.</span><span class="sxs-lookup"><span data-stu-id="8a040-107">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="8a040-108">Non è necessario modificare le credenziali dell'app in caso di cambiamento delle responsabilità dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8a040-108">You do not have to change the app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="8a040-109">È possibile usare un certificato per automatizzare l'autenticazione in caso di esecuzione di uno script automatico.</span><span class="sxs-lookup"><span data-stu-id="8a040-109">You can use a certificate to automate authentication when executing an unattended script.</span></span>

<span data-ttu-id="8a040-110">Questo argomento illustra come eseguire questa procedura tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="8a040-110">This topic shows you how to perform those steps through the portal.</span></span> <span data-ttu-id="8a040-111">È incentrato su un'applicazione con un tenant singolo dove si prevede che l'applicazione venga eseguita all'interno di una sola organizzazione.</span><span class="sxs-lookup"><span data-stu-id="8a040-111">It focuses on a single-tenant application where the application is intended to run within only one organization.</span></span> <span data-ttu-id="8a040-112">Le applicazioni con un tenant singolo si usano in genere per applicazioni line-of-business eseguite all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="8a040-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="8a040-113">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="8a040-113">Required permissions</span></span>
<span data-ttu-id="8a040-114">Per completare questo argomento è necessario disporre di autorizzazioni sufficienti per registrare un'applicazione con il tenant di Azure AD e assegnare l'applicazione a un ruolo nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a040-114">To complete this topic, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.</span></span> <span data-ttu-id="8a040-115">Assicurarsi di avere le autorizzazioni appropriate per eseguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="8a040-115">Let's make sure you have the right permissions to perform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="8a040-116">Controllare le autorizzazioni di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a040-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="8a040-117">Accedere all'account di Azure tramite il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8a040-117">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8a040-118">Selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a040-118">Select **Azure Active Directory**.</span></span>

     ![Selezionare Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="8a040-120">In Azure Active Directory selezionare **Impostazioni utente**.</span><span class="sxs-lookup"><span data-stu-id="8a040-120">In Azure Active Directory, select **User settings**.</span></span>

     ![Selezionare Impostazioni utente](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="8a040-122">Controllare l'impostazione **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="8a040-122">Check the **App registrations** setting.</span></span> <span data-ttu-id="8a040-123">Se il valore è **Sì**, gli utenti non amministratori possono registrare app di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8a040-123">If set to **Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="8a040-124">Questa impostazione indica che qualsiasi utente in Azure AD può registrare un'app.</span><span class="sxs-lookup"><span data-stu-id="8a040-124">This setting means any user in the Azure AD tenant can register an app.</span></span> <span data-ttu-id="8a040-125">È possibile passare a [Controllare le autorizzazioni di sottoscrizione di Azure](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="8a040-125">You can proceed to [Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![Visualizzare le registrazioni dell'app](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="8a040-127">Se Registrazioni per l'app è impostata su **No**, solo gli utenti amministratori possono registrare app.</span><span class="sxs-lookup"><span data-stu-id="8a040-127">If the app registrations setting is set to **No**, only admin users can register apps.</span></span> <span data-ttu-id="8a040-128">È necessario controllare se l'account è un amministratore per il tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a040-128">You need to check whether your account is an admin for the Azure AD tenant.</span></span> <span data-ttu-id="8a040-129">Selezionare **Panoramica** e **Trova un utente** da Attività rapide.</span><span class="sxs-lookup"><span data-stu-id="8a040-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![Trova un utente](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="8a040-131">Cercare il proprio account e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="8a040-131">Search for your account, and select it when you find it.</span></span>

     ![Cercare un utente](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="8a040-133">Per il proprio account selezionare **Ruolo della directory**.</span><span class="sxs-lookup"><span data-stu-id="8a040-133">For your account, select **Directory role**.</span></span> 

     ![Ruolo della directory](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="8a040-135">Visualizzare il proprio ruolo della directory assegnato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a040-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="8a040-136">Se l'account è assegnato al ruolo Utente, ma l'impostazione Registrazioni per l'app (dei passaggi precedenti) è limitata agli utenti amministratori, chiedere all'amministratore di essere assegnati a un ruolo amministrativo o di consentire agli utenti di registrare le app.</span><span class="sxs-lookup"><span data-stu-id="8a040-136">If your account is assigned to the User role, but the app registration setting (from the preceding steps) is limited to admin users, ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

     ![Visualizzare il ruolo](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="8a040-138">Controllare le autorizzazioni di sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="8a040-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="8a040-139">Nella sottoscrizione di Azure è necessario che l'account disponga dell'accesso `Microsoft.Authorization/*/Write` per assegnare un'app di Active Directory a un ruolo.</span><span class="sxs-lookup"><span data-stu-id="8a040-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access to assign an AD app to a role.</span></span> <span data-ttu-id="8a040-140">Questa azione è concessa tramite il ruolo [Proprietario](../active-directory/role-based-access-built-in-roles.md#owner) o [Amministratore accessi utente](../active-directory/role-based-access-built-in-roles.md#user-access-administrator).</span><span class="sxs-lookup"><span data-stu-id="8a040-140">This action is granted through the [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="8a040-141">Se il proprio account è assegnato al ruolo **Collaboratore**, non si dispone dell'autorizzazione appropriata.</span><span class="sxs-lookup"><span data-stu-id="8a040-141">If your account is assigned to the **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="8a040-142">Se si tenterà di assegnare l'entità servizio a un ruolo si riceverà un errore.</span><span class="sxs-lookup"><span data-stu-id="8a040-142">You will receive an error when attempting to assign the service principal to a role.</span></span> 

<span data-ttu-id="8a040-143">Per controllare le proprie autorizzazioni di sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="8a040-143">To check your subscription permissions:</span></span>

1. <span data-ttu-id="8a040-144">Se non è già visualizzato il proprio account Azure AD in seguito ai passaggi precedenti, selezionare **Azure Active Directory** nel pannello a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8a040-144">If you are not already looking at your Azure AD account from the preceding steps, select **Azure Active Directory** from the left pane.</span></span>

2. <span data-ttu-id="8a040-145">Trovare il proprio account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a040-145">Find your Azure AD account.</span></span> <span data-ttu-id="8a040-146">Selezionare **Panoramica** e **Trova un utente** da Attività rapide.</span><span class="sxs-lookup"><span data-stu-id="8a040-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![Trova un utente](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="8a040-148">Cercare il proprio account e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="8a040-148">Search for your account, and select it when you find it.</span></span>

     ![Cercare un utente](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="8a040-150">Selezionare **Risorse di Azure**.</span><span class="sxs-lookup"><span data-stu-id="8a040-150">Select **Azure resources**.</span></span>

     ![Selezionare le risorse](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="8a040-152">Visualizzare i propri ruoli assegnati e determinare se si dispone delle autorizzazioni adeguate per assegnare un'app di Active Directory a un ruolo.</span><span class="sxs-lookup"><span data-stu-id="8a040-152">View your assigned roles, and determine if you have adequate permissions to assign an AD app to a role.</span></span> <span data-ttu-id="8a040-153">In caso contrario chiedere all'amministratore della sottoscrizione di essere aggiunti al ruolo Amministratore accessi utente.</span><span class="sxs-lookup"><span data-stu-id="8a040-153">If not, ask your subscription administrator to add you to User Access Administrator role.</span></span> <span data-ttu-id="8a040-154">Nella figura seguente l'utente è assegnato al ruolo Proprietario per due sottoscrizioni, perciò dispone delle autorizzazioni adeguate.</span><span class="sxs-lookup"><span data-stu-id="8a040-154">In the following image, the user is assigned to the Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![Visualizzare le autorizzazioni](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="8a040-156">Creare un'applicazione Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a040-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="8a040-157">Accedere all'account di Azure tramite il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8a040-157">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8a040-158">Selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a040-158">Select **Azure Active Directory**.</span></span>

     ![Selezionare Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="8a040-160">Selezionare **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="8a040-160">Select **App registrations**.</span></span>   

     ![Selezionare Registrazioni per l'app](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="8a040-162">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8a040-162">Select **Add**.</span></span>

     ![Aggiungere l'app](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="8a040-164">Specificare un nome e un URL per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8a040-164">Provide a name and URL for the application.</span></span> <span data-ttu-id="8a040-165">Selezionare **App Web/API** o **Nativa** come tipo di applicazione da creare.</span><span class="sxs-lookup"><span data-stu-id="8a040-165">Select either **Web app / API** or **Native** for the type of application you want to create.</span></span> <span data-ttu-id="8a040-166">Dopo aver impostato i valori selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8a040-166">After setting the values, select **Create**.</span></span>

     ![assegnare un nome all'applicazione](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="8a040-168">L'applicazione è stata creata.</span><span class="sxs-lookup"><span data-stu-id="8a040-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="8a040-169">Ottenere l'ID applicazione e la chiave di autenticazione</span><span class="sxs-lookup"><span data-stu-id="8a040-169">Get application ID and authentication key</span></span>
<span data-ttu-id="8a040-170">Quando si esegue l'accesso a livello di codice sono necessari l'ID dell'applicazione e una chiave di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="8a040-170">When programmatically logging in, you need the ID for your application and an authentication key.</span></span> <span data-ttu-id="8a040-171">Per ottenere questi valori eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8a040-171">To get those values, use the following steps:</span></span>

1. <span data-ttu-id="8a040-172">Da **Registrazioni dell'app** in Azure Active Directory selezionare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8a040-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![Selezionare l'applicazione](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="8a040-174">Copiare l'**ID applicazione** e archiviarlo nel codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8a040-174">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="8a040-175">Le applicazioni nella sezione delle [applicazioni di esempio](#sample-applications) indicano questo valore come ID client.</span><span class="sxs-lookup"><span data-stu-id="8a040-175">The applications in the [sample applications](#sample-applications) section refer to this value as the client id.</span></span>

     ![ID CLIENT](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="8a040-177">Per generare una chiave di autenticazione selezionare **Chiavi**.</span><span class="sxs-lookup"><span data-stu-id="8a040-177">To generate an authentication key, select **Keys**.</span></span>

     ![Selezionare Chiavi](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="8a040-179">Specificare una descrizione e una durata per la chiave.</span><span class="sxs-lookup"><span data-stu-id="8a040-179">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="8a040-180">Al termine scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8a040-180">When done, select **Save**.</span></span>

     ![Salvare la chiave](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="8a040-182">Dopo aver salvato la chiave viene visualizzato il valore della chiave.</span><span class="sxs-lookup"><span data-stu-id="8a040-182">After saving the key, the value of the key is displayed.</span></span> <span data-ttu-id="8a040-183">Copiare il valore in quanto non sarà possibile recuperare la chiave in seguito.</span><span class="sxs-lookup"><span data-stu-id="8a040-183">Copy this value because you are not able to retrieve the key later.</span></span> <span data-ttu-id="8a040-184">Il valore della chiave sarà fornito insieme all'ID applicazione per eseguire l'accesso come applicazione.</span><span class="sxs-lookup"><span data-stu-id="8a040-184">You provide the key value with the application ID to log in as the application.</span></span> <span data-ttu-id="8a040-185">Salvare il valore della chiave in una posizione in cui l'applicazione possa recuperarlo.</span><span class="sxs-lookup"><span data-stu-id="8a040-185">Store the key value where your application can retrieve it.</span></span>

     ![chiave salvata](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="8a040-187">Ottenere l'ID tenant</span><span class="sxs-lookup"><span data-stu-id="8a040-187">Get tenant ID</span></span>
<span data-ttu-id="8a040-188">Quando si esegue l'accesso a livello di codice è necessario specificare l'ID tenant con la richiesta di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="8a040-188">When programmatically logging in, you need to pass the tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="8a040-189">Per ottenere l'ID tenant selezionare **Proprietà** per il tenanto di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a040-189">To get the tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![selezionare le proprietà di Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="8a040-191">Copiare l'**ID directory**.</span><span class="sxs-lookup"><span data-stu-id="8a040-191">Copy the **Directory ID**.</span></span> <span data-ttu-id="8a040-192">Questo valore è l'ID tenant.</span><span class="sxs-lookup"><span data-stu-id="8a040-192">This value is your tenant ID.</span></span>

     ![tenant id](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-to-role"></a><span data-ttu-id="8a040-194">Assegnare l'applicazione al ruolo</span><span class="sxs-lookup"><span data-stu-id="8a040-194">Assign application to role</span></span>
<span data-ttu-id="8a040-195">Per accedere alle risorse della propria sottoscrizione è necessario assegnare l'applicazione a un ruolo.</span><span class="sxs-lookup"><span data-stu-id="8a040-195">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="8a040-196">Decidere quale ruolo rappresenti le autorizzazioni appropriate per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8a040-196">Decide which role represents the right permissions for the application.</span></span> <span data-ttu-id="8a040-197">Per informazioni sui ruoli disponibili, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="8a040-197">To learn about the available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="8a040-198">È possibile impostare l'ambito al livello della sottoscrizione, del gruppo di risorse o della risorsa.</span><span class="sxs-lookup"><span data-stu-id="8a040-198">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="8a040-199">Le autorizzazioni vengono ereditate a livelli inferiori dell'ambito.</span><span class="sxs-lookup"><span data-stu-id="8a040-199">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="8a040-200">Se ad esempio si aggiunge un'applicazione al ruolo Lettore per un gruppo di risorse, l'applicazione può leggere il gruppo di risorse e le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="8a040-200">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span></span>

1. <span data-ttu-id="8a040-201">Passare al livello dell'ambito al quale si vuole assegnare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8a040-201">Navigate to the level of scope you wish to assign the application to.</span></span> <span data-ttu-id="8a040-202">Ad esempio, per assegnare un ruolo a un ambito della sottoscrizione, selezionare **Sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="8a040-202">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="8a040-203">In alternativa è possibile selezionare una risorsa o un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8a040-203">You could instead select a resource group or resource.</span></span>

     ![selezionare la sottoscrizione](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="8a040-205">Selezionare la sottoscrizione specifica (risorsa o un gruppo di risorse) a cui assegnare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8a040-205">Select the particular subscription (resource group or resource) to assign the application to.</span></span>

     ![selezionare la sottoscrizione per l'assegnazione](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="8a040-207">Selezionare **Controllo di accesso (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="8a040-207">Select **Access Control (IAM)**.</span></span>

     ![selezionare accesso](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="8a040-209">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8a040-209">Select **Add**.</span></span>

     ![selezionare aggiungi](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="8a040-211">Selezionare il ruolo che si desidera assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8a040-211">Select the role you wish to assign to the application.</span></span> <span data-ttu-id="8a040-212">L'immagine seguente mostra il ruolo **Lettore**.</span><span class="sxs-lookup"><span data-stu-id="8a040-212">The following image shows the **Reader** role.</span></span>

     ![selezionare il ruolo](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="8a040-214">Cercare l'applicazione e selezionarla.</span><span class="sxs-lookup"><span data-stu-id="8a040-214">Search for your application, and select it.</span></span>

     ![Cercare l'app](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="8a040-216">Selezionare **OK** per completare l'assegnazione del ruolo.</span><span class="sxs-lookup"><span data-stu-id="8a040-216">Select **OK** to finish assigning the role.</span></span> <span data-ttu-id="8a040-217">L'applicazione ora compare nell'elenco degli utenti assegnati a un ruolo per quell'ambito.</span><span class="sxs-lookup"><span data-stu-id="8a040-217">You see your application in the list of users assigned to a role for that scope.</span></span>

## <a name="log-in-as-the-application"></a><span data-ttu-id="8a040-218">Eseguire l'accesso come applicazione</span><span class="sxs-lookup"><span data-stu-id="8a040-218">Log in as the application</span></span>

<span data-ttu-id="8a040-219">L'applicazione è ora configurata in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8a040-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="8a040-220">Si dispone di un ID e una chiave da usare per eseguire l'accesso come applicazione.</span><span class="sxs-lookup"><span data-stu-id="8a040-220">You have an ID and key to use for signing in as the application.</span></span> <span data-ttu-id="8a040-221">L'applicazione viene assegnata a un ruolo che le consente di eseguire alcune azioni.</span><span class="sxs-lookup"><span data-stu-id="8a040-221">The application is assigned to a role that gives it certain actions it can perform.</span></span> <span data-ttu-id="8a040-222">Per informazioni su come effettuare l'accesso all'applicazione su diverse piattaforme, vedere:</span><span class="sxs-lookup"><span data-stu-id="8a040-222">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="8a040-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a040-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="8a040-224">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="8a040-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="8a040-225">REST</span><span class="sxs-lookup"><span data-stu-id="8a040-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="8a040-226">.NET</span><span class="sxs-lookup"><span data-stu-id="8a040-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="8a040-227">Java</span><span class="sxs-lookup"><span data-stu-id="8a040-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="8a040-228">Node.js</span><span class="sxs-lookup"><span data-stu-id="8a040-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="8a040-229">Python</span><span class="sxs-lookup"><span data-stu-id="8a040-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="8a040-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="8a040-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="8a040-231">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a040-231">Next steps</span></span>
* <span data-ttu-id="8a040-232">Per configurare un'applicazione multi-tenant, vedere [Guida per gli sviluppatori all'autorizzazione con l'API di Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8a040-232">To set up a multi-tenant application, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="8a040-233">Per informazioni su come specificare i criteri di sicurezza, vedere [Controllo degli accessi in base al ruolo nel portale di Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8a040-233">To learn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="8a040-234">Per un elenco di azioni disponibili che è possibile concedere o negare agli utenti, vedere [Operazioni di provider di risorse con Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="8a040-234">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
