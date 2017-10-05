---
title: Azure IoT Suite e Azure Active Directory | Documentazione Microsoft
description: Descrive in che modo Azure IoT Suite usa Azure Active Directory per gestire le autorizzazioni.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 518e6a481ab6385b03dd3ddc2e155fb724e677fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-on-the-azureiotsuitecom-site"></a><span data-ttu-id="f273b-103">Autorizzazioni per il sito azureiotsuite.com</span><span class="sxs-lookup"><span data-stu-id="f273b-103">Permissions on the azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="f273b-104">Cosa accade quando si accede</span><span class="sxs-lookup"><span data-stu-id="f273b-104">What happens when you sign in</span></span>

<span data-ttu-id="f273b-105">Quando si accede per la prima volta ad [azureiotsuite.com][lnk-azureiotsuite], il sito determina i livelli di autorizzazione in base al tenant di Azure Active Directory (AAD) attualmente selezionato e alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f273b-105">The first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], the site determines the permission levels you have based on the currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="f273b-106">Per prima cosa, il sito cerca prima in Azure a quale tenant di AAD appartiene l'utente per popolare l'elenco di tenant visualizzato accanto al nome utente connesso.</span><span class="sxs-lookup"><span data-stu-id="f273b-106">First, to populate the list of tenants seen next to your username, the site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="f273b-107">In questo momento, il sito può ricevere solo i token utente per un tenant alla volta.</span><span class="sxs-lookup"><span data-stu-id="f273b-107">Currently, the site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="f273b-108">Di conseguenza, quando si passa a un tenant diverso usando l'elenco a discesa nell'angolo superiore destro, il sito registra di nuovo l'utente nel tenant per ottenere il token di tale tenant.</span><span class="sxs-lookup"><span data-stu-id="f273b-108">Therefore, when you switch tenants using the dropdown in the top right corner, the site logs you in to that tenant to obtain the tokens for that tenant.</span></span>

2. <span data-ttu-id="f273b-109">Successivamente, il sito cerca in Azure quali sottoscrizioni sono state associate dall'utente al tenant selezionato.</span><span class="sxs-lookup"><span data-stu-id="f273b-109">Next, the site finds out from Azure which subscriptions you have associated with the selected tenant.</span></span> <span data-ttu-id="f273b-110">Le sottoscrizioni disponibili vengono visualizzate quando si crea una nuova soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="f273b-110">You see the available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="f273b-111">Infine, il sito recupera tutte le risorse nelle sottoscrizioni e nei gruppi di risorse contrassegnati come soluzioni preconfigurate e popola i riquadri nella home page.</span><span class="sxs-lookup"><span data-stu-id="f273b-111">Finally, the site retrieves all the resources in the subscriptions and resource groups tagged as preconfigured solutions and populates the tiles on the home page.</span></span>

<span data-ttu-id="f273b-112">Le sezioni seguenti descrivono i ruoli che controllano l'accesso alle soluzioni preconfigurate.</span><span class="sxs-lookup"><span data-stu-id="f273b-112">The following sections describe the roles that control access to the preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="f273b-113">Ruoli AAD</span><span class="sxs-lookup"><span data-stu-id="f273b-113">AAD roles</span></span>

<span data-ttu-id="f273b-114">I ruoli AAD controllano la capacità di provisioning delle soluzioni preconfigurate e gestiscono gli utenti in una soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="f273b-114">The AAD roles control the ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="f273b-115">Per altre informazioni sui ruoli di amministratore in AAD, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="f273b-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="f273b-116">L'articolo corrente è incentrato sui ruoli della directory di **Amministratore globale** e **Utente** usati dalle soluzioni preconfigurate.</span><span class="sxs-lookup"><span data-stu-id="f273b-116">The current article focuses on the **Global Administrator** and the **User** directory roles as used by the preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="f273b-117">Amministratore globale</span><span class="sxs-lookup"><span data-stu-id="f273b-117">Global administrator</span></span>

<span data-ttu-id="f273b-118">Per ogni tenant di AAD possono essere presenti più amministratori globali:</span><span class="sxs-lookup"><span data-stu-id="f273b-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="f273b-119">Quando si crea un tenant di AAD, si è per impostazione predefinita l'amministratore globale del tenant.</span><span class="sxs-lookup"><span data-stu-id="f273b-119">When you create an AAD tenant, you are by default the global administrator of that tenant.</span></span>
* <span data-ttu-id="f273b-120">L'amministratore globale può eseguire il provisioning di una soluzione preconfigurata e gli viene assegnato un ruolo **Admin** per l'applicazione all'interno di tenant di AAD.</span><span class="sxs-lookup"><span data-stu-id="f273b-120">The global administrator can provision a preconfigured solution and is assigned an **Admin** role for the application inside their AAD tenant.</span></span>
* <span data-ttu-id="f273b-121">Se un altro utente nello stesso tenant di AAD crea un'applicazione, il ruolo predefinito concesso all'amministratore globale è **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="f273b-121">If another user in the same AAD tenant creates an application, the default role granted to the global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="f273b-122">Gli amministratori globali possono assegnare agli utenti dei ruoli per le applicazioni tramite il [portale di Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="f273b-122">A global administrator can assign users to roles for applications using the [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="f273b-123">Utente di dominio</span><span class="sxs-lookup"><span data-stu-id="f273b-123">Domain user</span></span>

<span data-ttu-id="f273b-124">Per ogni tenant di AAD possono essere presenti molti utenti del dominio:</span><span class="sxs-lookup"><span data-stu-id="f273b-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="f273b-125">Un utente di dominio può effettuare il provisioning di una soluzione preconfigurata tramite il sito [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="f273b-125">A domain user can provision a preconfigured solution through the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="f273b-126">Per impostazione predefinita, all'utente di dominio viene concesso il ruolo di **Amministratore** nell'applicazione in cui è stato eseguito il provisioning.</span><span class="sxs-lookup"><span data-stu-id="f273b-126">By default, the domain user is granted the **Admin** role in the provisioned application.</span></span>
* <span data-ttu-id="f273b-127">Un utente di dominio può creare un'applicazione usando lo script build.cmd nel repository [azure-iot-remote-monitoring][lnk-rm-github-repo], [azure-iot-predictive-maintenance][lnk-pm-github-repo] oppure [azure-iot-connected-factory][lnk-cf-github-repo].</span><span class="sxs-lookup"><span data-stu-id="f273b-127">A domain user can create an application using the build.cmd script in the [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="f273b-128">Tuttavia, il ruolo predefinito concesso all'utente di dominio è **ReadOnly**, perché un utente di dominio non dispone dell'autorizzazione per assegnare i ruoli.</span><span class="sxs-lookup"><span data-stu-id="f273b-128">However, the default role granted to the domain user is **ReadOnly**, because a domain user does not have permission to assign roles.</span></span>
* <span data-ttu-id="f273b-129">Se un altro utente nel tenant di AAD crea un'applicazione, all'utente di dominio viene assegnato il ruolo **ReadOnly** per impostazione predefinita per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f273b-129">If another user in the AAD tenant creates an application, the domain user is assigned the **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="f273b-130">Un utente di dominio non può assegnare ruoli per le applicazioni, quindi non può aggiungere utenti o ruoli per gli utenti di un'applicazione anche se ne è stato effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="f273b-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="f273b-131">Utente guest</span><span class="sxs-lookup"><span data-stu-id="f273b-131">Guest User</span></span>

<span data-ttu-id="f273b-132">Per ogni tenant AAD possono essere presenti molti utenti guest.</span><span class="sxs-lookup"><span data-stu-id="f273b-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="f273b-133">Gli utenti guest hanno un set di diritti limitato nel tenant di AAD.</span><span class="sxs-lookup"><span data-stu-id="f273b-133">Guest users have a limited set of rights in the AAD tenant.</span></span> <span data-ttu-id="f273b-134">Di conseguenza, gli utenti guest non possono effettuare il provisioning di una soluzione preconfigurata nel tenant di AAD.</span><span class="sxs-lookup"><span data-stu-id="f273b-134">As a result, guest users cannot provision a preconfigured solution in the AAD tenant.</span></span>

<span data-ttu-id="f273b-135">Per altre informazioni sugli utenti e i ruoli in AAD, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="f273b-135">For more information about users and roles in AAD, see the following resources:</span></span>

* <span data-ttu-id="f273b-136">[Creare utenti in Azure AD][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="f273b-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="f273b-137">[Assegnare utenti alle app][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="f273b-137">[Assign users to apps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="f273b-138">Ruoli di amministratore della sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="f273b-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="f273b-139">I ruoli di amministrazione di Azure controllano la possibilità di eseguire il mapping di una sottoscrizione di Azure a un tenant di AD.</span><span class="sxs-lookup"><span data-stu-id="f273b-139">The Azure admin roles control the ability to map an Azure subscription to an AD tenant.</span></span>

<span data-ttu-id="f273b-140">È possibile trovare altre informazioni sui ruoli di amministratore nell'articolo [Come aggiungere o modificare i ruoli Co-amministratore, Amministratore del servizio e Amministratore account di Azure][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="f273b-140">Find out more about the Azure admin roles in the article [How to add or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="f273b-141">Ruoli applicazione</span><span class="sxs-lookup"><span data-stu-id="f273b-141">Application roles</span></span>

<span data-ttu-id="f273b-142">I ruoli applicazione controllano l'accesso ai dispositivi nella soluzione preconfigurato.</span><span class="sxs-lookup"><span data-stu-id="f273b-142">The application roles control access to devices in your preconfigured solution.</span></span>

<span data-ttu-id="f273b-143">In un'applicazione su cui è stato eseguito il provisioning sono stati definiti due ruoli e uno implicito:</span><span class="sxs-lookup"><span data-stu-id="f273b-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="f273b-144">**Admin:** dispone di autorizzazioni complete per aggiungere, gestire, rimuovere i dispositivi e modificare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="f273b-144">**Admin:** Has full control to add, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="f273b-145">**ReadOnly:** è possibile visualizzare i dispositivi, le regole, le azioni, i processi e i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="f273b-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="f273b-146">È possibile trovare le autorizzazioni assegnate a ogni ruolo nel file di origine [RolePermissions.cs][lnk-resource-cs].</span><span class="sxs-lookup"><span data-stu-id="f273b-146">You can find the permissions assigned to each role in the [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="f273b-147">Modifica dei ruoli applicazione di un utente</span><span class="sxs-lookup"><span data-stu-id="f273b-147">Changing application roles for a user</span></span>

<span data-ttu-id="f273b-148">È possibile usare la procedura seguente per configurare un utente di Active Directory come amministratore della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="f273b-148">You can use the following procedure to make a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="f273b-149">Per modificare i ruoli per un utente, è necessario essere un amministratore globale di AAD:</span><span class="sxs-lookup"><span data-stu-id="f273b-149">You must be an AAD global administrator to change roles for a user:</span></span>

1. <span data-ttu-id="f273b-150">Accedere al [portale di Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="f273b-150">Go to the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="f273b-151">Selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f273b-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="f273b-152">Verificare che si sta usando la directory selezionata in azureiotsuite.com durante il provisioning della soluzione.</span><span class="sxs-lookup"><span data-stu-id="f273b-152">Make sure you are using the directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="f273b-153">Se si dispone di più directory associate alla sottoscrizione, è possibile passare da una all'altra facendo clic sul nome dell'account in alto a destra del portale.</span><span class="sxs-lookup"><span data-stu-id="f273b-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at the top-right of the portal.</span></span>
4. <span data-ttu-id="f273b-154">Fare clic su **Applicazioni aziendali**, quindi su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f273b-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="f273b-155">Vengono visualizzate **Tutte le applicazioni** con stato **Qualsiasi**.</span><span class="sxs-lookup"><span data-stu-id="f273b-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="f273b-156">Eseguire quindi una ricerca per un'applicazione con il nome della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="f273b-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="f273b-157">Fare clic sul nome dell'applicazione che coincide con il nome della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="f273b-157">Click the name of the application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="f273b-158">Fare clic su **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f273b-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="f273b-159">Selezionare l'utente per cui si vogliono scambiare i ruoli.</span><span class="sxs-lookup"><span data-stu-id="f273b-159">Select the user you want to switch roles.</span></span>
8. <span data-ttu-id="f273b-160">Fare clic su **Assegna** e selezionare il ruolo, ad esempio **Amministratore**, da assegnare all'utente, fare clic sul segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="f273b-160">Click **Assign** and select the role (such as **Admin**) you'd like to assign to the user, click the check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="f273b-161">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="f273b-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-to-change-the-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="f273b-162">Un amministratore del servizio vuole modificare il mapping della directory tra la sottoscrizione e un tenant di AAD specifico.</span><span class="sxs-lookup"><span data-stu-id="f273b-162">I'm a service administrator and I'd like to change the directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="f273b-163">Come completare questa attività</span><span class="sxs-lookup"><span data-stu-id="f273b-163">How do I complete this task?</span></span>

1. <span data-ttu-id="f273b-164">Accedere al [portale di Azure classico][lnk-classic-portal] e fare clic su **Impostazioni** nell'elenco dei servizi sul lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="f273b-164">Go to the [Azure classic portal][lnk-classic-portal], click **Settings** in the list of services on the left-hand side.</span></span>
2. <span data-ttu-id="f273b-165">Selezionare la sottoscrizione per cui si vuole modificare il mapping della directory.</span><span class="sxs-lookup"><span data-stu-id="f273b-165">Select the subscription you'd like to change the directory mapping to.</span></span>
3. <span data-ttu-id="f273b-166">Fare clic su **Modifica directory**.</span><span class="sxs-lookup"><span data-stu-id="f273b-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="f273b-167">Nell'elenco a discesa selezionare la **Directory** si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="f273b-167">Select the **Directory** you would like to use in the dropdown.</span></span> <span data-ttu-id="f273b-168">Fare clic sulla freccia Avanti.</span><span class="sxs-lookup"><span data-stu-id="f273b-168">Click the forward arrow.</span></span>
5. <span data-ttu-id="f273b-169">Verificare il mapping della directory e i coamministratori interessati.</span><span class="sxs-lookup"><span data-stu-id="f273b-169">Confirm the directory mapping and affected co-administrators.</span></span> <span data-ttu-id="f273b-170">Se ci si sposta da un'altra directory, tutti i coamministratori dalla directory originale verranno rimossi.</span><span class="sxs-lookup"><span data-stu-id="f273b-170">If you are moving from another directory, all the co-administrators from the original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-the-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="f273b-171">Un utente o membro di dominio del tenant di AAD ha creato una soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="f273b-171">I'm a domain user/member on the AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="f273b-172">Come gli viene assegnato un ruolo per l'applicazione?</span><span class="sxs-lookup"><span data-stu-id="f273b-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="f273b-173">Contattare l'amministratore globale per diventare amministratore globale del tenant di AAD e assegnare ruoli agli utenti.</span><span class="sxs-lookup"><span data-stu-id="f273b-173">Ask a global administrator to make you a global administrator on the AAD tenant and then assign roles to users yourself.</span></span> <span data-ttu-id="f273b-174">In alternativa, contattare l'amministratore globale per assegnare direttamente un ruolo.</span><span class="sxs-lookup"><span data-stu-id="f273b-174">Alternatively, ask a global administrator to assign you a role directly.</span></span> <span data-ttu-id="f273b-175">Se si vuole modificare il tenant di AAD in cui è stata distribuita la soluzione preconfigurata, vedere la domanda successiva.</span><span class="sxs-lookup"><span data-stu-id="f273b-175">If you'd like to change the AAD tenant your preconfigured solution has been deployed to, see the next question.</span></span>

### <a name="how-do-i-switch-the-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="f273b-176">Come si cambia il tenant AAD a cui sono assegnate l'applicazione e soluzione preconfigurata di monitoraggio remoto?</span><span class="sxs-lookup"><span data-stu-id="f273b-176">How do I switch the AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="f273b-177">È possibile eseguire una distribuzione cloud da <https://github.com/Azure/azure-iot-remote-monitoring> ed eseguire una ridistribuizione con un tenant AAD appena creato.</span><span class="sxs-lookup"><span data-stu-id="f273b-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="f273b-178">Poiché per impostazione predefinita quando si crea un nuovo tenant di AAD si diventa un amministratore globale, si dispone anche dell'autorizzazione per aggiungere utenti e assegnare loro dei ruoli.</span><span class="sxs-lookup"><span data-stu-id="f273b-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions to add users and assign roles to those users.</span></span>

1. <span data-ttu-id="f273b-179">Creare una directory di AAD nel [Portale di Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="f273b-179">Create an AAD directory in the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="f273b-180">Passare a <https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="f273b-180">Go to <https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="f273b-181">Eseguire `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}`. Ad esempio `build.cmd cloud debug myRMSolution`.</span><span class="sxs-lookup"><span data-stu-id="f273b-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="f273b-182">Quando richiesto, impostare il **tenantid** come tenant appena creato al posto del tenant precedente.</span><span class="sxs-lookup"><span data-stu-id="f273b-182">When prompted, set the **tenantid** to be your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-to-change-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="f273b-183">Si vuole modificare un amministratore del servizio o coamministratore quando si accede con un account dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="f273b-183">I want to change a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="f273b-184">Vedere l'articolo di supporto [Modifica dell'amministratore del servizio e del coamministratore quando si effettua l'accesso con un account dell'organizzazione][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="f273b-184">See the support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-the-proper-permissions-to-create-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="f273b-185">Perché viene visualizzato un errore simile al seguente?</span><span class="sxs-lookup"><span data-stu-id="f273b-185">Why am I seeing this error?</span></span> <span data-ttu-id="f273b-186">"L'account non ha le autorizzazioni appropriate per creare una soluzione.</span><span class="sxs-lookup"><span data-stu-id="f273b-186">"Your account does not have the proper permissions to create a solution.</span></span> <span data-ttu-id="f273b-187">Rivolgersi all'amministratore account o provare con un account diverso".</span><span class="sxs-lookup"><span data-stu-id="f273b-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="f273b-188">Per indicazioni vedere il diagramma seguente:</span><span class="sxs-lookup"><span data-stu-id="f273b-188">Look at the following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="f273b-189">Se si continua a visualizzare l'errore dopo aver confermato di essere un amministratore globale del tenant AAD e un coamministratore della sottoscrizione, l'amministratore dell'account dovrà rimuovere l'utente e assegnare nuovamente le autorizzazioni necessarie in questo ordine.</span><span class="sxs-lookup"><span data-stu-id="f273b-189">If you continue to see the error after validating you are a global administrator on the AAD tenant and a co-administrator on the subscription, have your account administrator remove the user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="f273b-190">Innanzitutto, dovrà aggiungere l'utente come amministratore globale e quindi aggiungere l'utente come coamministratore della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f273b-190">First, add the user as a global administrator and then add user as a co-administrator on the Azure subscription.</span></span> <span data-ttu-id="f273b-191">Se i problemi persistono, contattare il tema [Guida e supporto][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="f273b-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-to-create-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="f273b-192">Perché viene visualizzato questo errore quando si dispone di una sottoscrizione di Azure?</span><span class="sxs-lookup"><span data-stu-id="f273b-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="f273b-193">"Per creare soluzioni preconfigurate è necessaria una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f273b-193">"An Azure subscription is required to create pre-configured solutions.</span></span> <span data-ttu-id="f273b-194">È possibile creare un account di valutazione gratuito in pochi minuti."</span><span class="sxs-lookup"><span data-stu-id="f273b-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="f273b-195">Se si è certi di avere una sottoscrizione di Azure, convalidare il mapping del tenant per la sottoscrizione e verificare che sia selezionato il tenant corretto nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="f273b-195">If you're certain you have an Azure subscription, validate the tenant mapping for your subscription and ensure the correct tenant is selected in the dropdown.</span></span> <span data-ttu-id="f273b-196">Se si è verificato che il tenant desiderato è corretto, seguire il diagramma precedente e verificare il mapping della sottoscrizione e il tenant di AAD.</span><span class="sxs-lookup"><span data-stu-id="f273b-196">If you’ve validated the desired tenant is correct, follow the preceding diagram and validate the mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f273b-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f273b-197">Next steps</span></span>
<span data-ttu-id="f273b-198">Per altre informazioni su IoT Suite, vedere come [personalizzare una soluzione preconfigurata][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="f273b-198">To continue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
