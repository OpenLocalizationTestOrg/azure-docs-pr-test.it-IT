---
title: toocontrol di controllo di accesso basato sui ruoli (RBAC) aaaAzure toocreate diritti di accesso e gestire le richieste di assistenza | Documenti Microsoft
description: Azure toocontrol di controllo di accesso basato sui ruoli (RBAC) toocreate diritti di accesso e gestire le richieste di assistenza
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a><span data-ttu-id="eca1d-103">Azure toocontrol di controllo di accesso basato sui ruoli (RBAC) toocreate diritti di accesso e gestire le richieste di assistenza</span><span class="sxs-lookup"><span data-stu-id="eca1d-103">Azure Role-Based Access Control (RBAC) toocontrol access rights toocreate and manage support requests</span></span>

<span data-ttu-id="eca1d-104">Il [Controllo degli accessi in base al ruolo di Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) consente una gestione specifica degli accessi per Azure.</span><span class="sxs-lookup"><span data-stu-id="eca1d-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="eca1d-105">Supporta la creazione della richiesta nel portale di Azure hello [portal.azure.com](https://portal.azure.com), utilizza toodefine di modello RBAC di Azure, che è possibile creare e gestire le richieste di assistenza.</span><span class="sxs-lookup"><span data-stu-id="eca1d-105">Support request creation in hello Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model toodefine who can create and manage support requests.</span></span>
<span data-ttu-id="eca1d-106">Assegnando hello appropriato RBAC ruolo toousers, gruppi e applicazioni in un determinato ambito, può essere una sottoscrizione, gruppo di risorse o una risorsa è concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="eca1d-106">Access is granted by assigning hello appropriate RBAC role toousers, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="eca1d-107">Esaminiamo un esempio: come un proprietario del gruppo di risorse con le autorizzazioni di lettura nell'ambito di hello sottoscrizione, è possibile gestire tutte le risorse di hello nel gruppo di risorse hello, ad esempio siti Web, macchine virtuali e subnet.</span><span class="sxs-lookup"><span data-stu-id="eca1d-107">Let’s take an example: As a resource group owner with read permissions at hello subscription scope, you can manage all hello resources under hello resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="eca1d-108">Tuttavia, quando si tenta una richiesta di supporto per la risorsa di macchina virtuale hello toocreate, si verifica il seguente errore hello</span><span class="sxs-lookup"><span data-stu-id="eca1d-108">However, when you try toocreate a support request against hello virtual machine resource, you encounter hello following error</span></span>

![Errore relativo alla sottoscrizione](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="eca1d-110">Nella gestione delle richieste di supporto, è necessario scrivere autorizzazione o un ruolo che dispone di hello azione Microsoft.Support/* toocreate toobe di ambito sottoscrizione hello in grado di supportare e gestire le richieste di assistenza.</span><span class="sxs-lookup"><span data-stu-id="eca1d-110">In support request management, you need write permission or a role that has hello Support action Microsoft.Support/* at hello Subscription scope toobe able toocreate and manage support requests.</span></span>

<span data-ttu-id="eca1d-111">Hello articolo seguente viene illustrato come utilizzare toocreate di controllo di accesso basato sui ruoli (RBAC) personalizzato di Azure e gestire le richieste di supporto di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eca1d-111">hello following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) toocreate and manage support requests in hello Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="eca1d-112">Introduzione</span><span class="sxs-lookup"><span data-stu-id="eca1d-112">Getting Started</span></span>

<span data-ttu-id="eca1d-113">Utilizzando l'esempio hello precedente, sarà in grado di toocreate una richiesta di supporto per la risorsa se sono stati è stato assegnato un ruolo personalizzato RBAC sottoscrizione hello dal proprietario della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="eca1d-113">Using hello example above, you would be able toocreate a support request for your resource if you were assigned a custom RBAC role on hello subscription by hello subscription owner.</span></span>
<span data-ttu-id="eca1d-114">[Ruoli RBAC personalizzati](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) può essere creata usando Azure PowerShell, l'interfaccia della riga di comando (CLI) di Azure e hello API REST.</span><span class="sxs-lookup"><span data-stu-id="eca1d-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and hello REST API.</span></span>

<span data-ttu-id="eca1d-115">proprietà di azioni Hello di un ruolo personalizzato specifica hello Azure operazioni toowhich hello ruolo concede l'accesso.</span><span class="sxs-lookup"><span data-stu-id="eca1d-115">hello actions property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span>
<span data-ttu-id="eca1d-116">toocreate un ruolo personalizzato per la gestione delle richieste di supporto, hello al ruolo deve essere azione hello Microsoft.Support/*</span><span class="sxs-lookup"><span data-stu-id="eca1d-116">toocreate a custom role for support request management, hello role must have hello action Microsoft.Support/*</span></span>

<span data-ttu-id="eca1d-117">Di seguito è riportato un esempio di un ruolo personalizzato, è possibile utilizzare toocreate e gestire le richieste di supporto.</span><span class="sxs-lookup"><span data-stu-id="eca1d-117">Here’s an example of a custom role you can use toocreate and manage support requests.</span></span>
<span data-ttu-id="eca1d-118">È stato denominato in questo ruolo "Collaboratore di richiesta di supporto" e si riferisce toohello ruolo personalizzato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="eca1d-118">We’ve named this role “Support Request Contributor” and that’s how we refer toohello custom role in this article.</span></span>

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

<span data-ttu-id="eca1d-119">Seguire i passaggi di hello illustrati in [questo video](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn come toocreate un ruolo personalizzato per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="eca1d-119">Follow hello steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn how toocreate a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a><span data-ttu-id="eca1d-120">Creare e gestire le richieste di assistenza in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="eca1d-120">Create and manage support requests in hello Azure portal</span></span>

<span data-ttu-id="eca1d-121">Esaminiamo un esempio: si è proprietari di hello di sottoscrizione "Visual Studio MSDN sottoscrizione."</span><span class="sxs-lookup"><span data-stu-id="eca1d-121">Let’s take an example – you are hello owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="eca1d-122">Joe è il peer che è un toosome proprietario risorsa hello di gruppi di risorse nella sottoscrizione e che disponga di sottoscrizione toohello autorizzazione di lettura.</span><span class="sxs-lookup"><span data-stu-id="eca1d-122">Joe is your peer who is a resource owner toosome of hello resource groups in this subscription and has read permission toohello subscription.</span></span>
<span data-ttu-id="eca1d-123">Si desidera toogive accesso tooyour peer, Gianni, hello possibilità toocreate e gestire i ticket di supporto per le risorse di hello in questa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="eca1d-123">You wish toogive access tooyour peer, Joe, hello ability toocreate and manage support tickets for hello resources under this subscription.</span></span>

1. <span data-ttu-id="eca1d-124">primo passaggio Hello è toogo toohello sottoscrizione e in "Impostazioni" viene visualizzato un elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="eca1d-124">hello first step is toogo toohello subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="eca1d-125">Fare clic su utente hello Joe che dispone dell'accesso in lettura per hello sottoscrizione e si assegna un nuovo toohim di ruolo personalizzata.</span><span class="sxs-lookup"><span data-stu-id="eca1d-125">Click hello user Joe who has reader access on hello Subscription and let’s assign a new custom role toohim.</span></span>

    ![Aggiungi ruolo](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="eca1d-127">Nel Pannello di "Utenti" hello, fare clic su "Aggiungi".</span><span class="sxs-lookup"><span data-stu-id="eca1d-127">Click "Add" under hello "Users" blade.</span></span> <span data-ttu-id="eca1d-128">Selezionare il ruolo personalizzato hello "Collaboratore di richiesta di supporto" hello elenco dei ruoli</span><span class="sxs-lookup"><span data-stu-id="eca1d-128">Select hello custom role "Support Request Contributor" from hello list of roles</span></span>

    ![Aggiungere il ruolo di collaboratore di supporto](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="eca1d-130">Dopo aver selezionato il nome del ruolo hello, fare clic su "Aggiungi utenti" e immettere le credenziali di posta elettronica hello Joe.</span><span class="sxs-lookup"><span data-stu-id="eca1d-130">After selecting hello role name, click "Add users" and enter hello Joe's email credentials.</span></span> <span data-ttu-id="eca1d-131">Fare clic su "Seleziona"</span><span class="sxs-lookup"><span data-stu-id="eca1d-131">Click "Select"</span></span>

    ![Aggiungi utenti](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="eca1d-133">Fare clic su "Ok" tooproceed</span><span class="sxs-lookup"><span data-stu-id="eca1d-133">Click "Ok" tooproceed</span></span>

    ![Aggiungere un accesso](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="eca1d-135">È ora possibile visualizzare utente hello con il ruolo personalizzato appena aggiunto "Supporto richiesta Collaboratore" nella sottoscrizione hello per cui si è proprietari di hello hello</span><span class="sxs-lookup"><span data-stu-id="eca1d-135">Now you see hello user with hello newly added custom role "Support Request Contributor" under hello Subscription for which you are hello owner</span></span>

    ![Utente aggiunto](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="eca1d-137">Quando si connette Joe portale hello, vede hello toowhich di sottoscrizione che è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="eca1d-137">When Joe logs in hello portal, he sees hello subscription toowhich he was added.</span></span>

7. <span data-ttu-id="eca1d-138">Joe fa clic su "Nuova richiesta di supporto" pannello "Guida in linea e supporto di" hello e può creare richieste di supporto per "Visual Studio Ultimate con MSDN"</span><span class="sxs-lookup"><span data-stu-id="eca1d-138">Joe clicks "New Support request" from hello "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![Nuova richiesta di supporto](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="eca1d-140">Fare clic su "Tutte le richieste di supporto" Joe possibile visualizzare l'elenco di hello delle richieste di supporto creato per questa sottoscrizione ![Case visualizzazione dettagli](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="eca1d-140">Clicking "All support requests" Joe can see hello list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-hello-azure-portal"></a><span data-ttu-id="eca1d-141">Rimuovere il supporto richiedere l'accesso in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="eca1d-141">Remove support request access in hello Azure portal</span></span>

<span data-ttu-id="eca1d-142">Come è possibile toogrant accesso tooa utente toocreate e gestire le richieste di supporto, è possibili tooremove accesso utente hello.</span><span class="sxs-lookup"><span data-stu-id="eca1d-142">Just as it is possible toogrant access tooa user toocreate and manage support requests, it's possible tooremove access for hello user as well.</span></span>
<span data-ttu-id="eca1d-143">tooremove hello toocreate possibilità gestire le richieste di supporto, toohello sottoscrizione, fare clic su "Impostazioni" e fare clic utente hello (in questo caso, Joe).</span><span class="sxs-lookup"><span data-stu-id="eca1d-143">tooremove hello ability toocreate and manage support requests, go toohello Subscription, click "Settings" and click hello user (in this case, Joe).</span></span>
<span data-ttu-id="eca1d-144">Fare doppio clic su nome ruolo hello, "Collaboratore di richiesta di supporto" e fare clic su "Rimuovi"</span><span class="sxs-lookup"><span data-stu-id="eca1d-144">Right-click hello role name, "Support Request Contributor" and click "Remove"</span></span>

![Rimuovere l'accesso alle richiesta di supporto](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="eca1d-146">Quando Joe registra nel portale toohello e tenta di toocreate una richiesta di supporto, egli rileva il seguente errore hello</span><span class="sxs-lookup"><span data-stu-id="eca1d-146">When Joe logs in toohello portal and tries toocreate a support request, he encounters hello following error</span></span>

![Errore di sottoscrizione 2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="eca1d-148">Quando Joe fa clic su "Tutte le richieste di supporto", non sarà visibile nessuna richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="eca1d-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![Visualizzazione dettagli del caso 2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
