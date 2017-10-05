---
title: Controllo degli accessi in base al ruolo per controllare i diritti di accesso e gestire le richieste di supporto | Documentazione Microsoft
description: Controllo degli accessi in base al ruolo di Azure per controllare i diritti di accesso e gestire le richieste di supporto
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: 20ebd324cbf379980b43d255d468673de2b6d950
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-based-access-control-rbac-to-control-access-rights-to-create-and-manage-support-requests"></a><span data-ttu-id="8ead5-103">Controllo degli accessi in base al ruolo di Azure per controllare i diritti di accesso e gestire le richieste di supporto</span><span class="sxs-lookup"><span data-stu-id="8ead5-103">Azure Role-Based Access Control (RBAC) to control access rights to create and manage support requests</span></span>

<span data-ttu-id="8ead5-104">Il [Controllo degli accessi in base al ruolo di Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) consente una gestione specifica degli accessi per Azure.</span><span class="sxs-lookup"><span data-stu-id="8ead5-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="8ead5-105">La creazione di richieste di supporto nel portale di Azure, [portal.azure.com](https://portal.azure.com), usa il modello di Controllo degli accessi in base al ruolo per definire chi può creare e gestire le richieste di supporto.</span><span class="sxs-lookup"><span data-stu-id="8ead5-105">Support request creation in the Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model to define who can create and manage support requests.</span></span>
<span data-ttu-id="8ead5-106">L'accesso viene concesso assegnando ruoli di Controllo degli accessi in base al ruolo appropriati a utenti, gruppi e applicazioni in un ambito specifico: una sottoscrizione, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="8ead5-106">Access is granted by assigning the appropriate RBAC role to users, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="8ead5-107">Esaminiamo l'esempio di un proprietario di un gruppo di risorse con autorizzazioni di lettura nell'ambito della sottoscrizione che può gestire tutte le risorse nel gruppo di risorse, come siti Web, macchine virtuali e subnet.</span><span class="sxs-lookup"><span data-stu-id="8ead5-107">Let’s take an example: As a resource group owner with read permissions at the subscription scope, you can manage all the resources under the resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="8ead5-108">Quando tuttavia tenta di creare una richiesta di supporto per la risorsa macchina virtuale, si verifica l'errore seguente</span><span class="sxs-lookup"><span data-stu-id="8ead5-108">However, when you try to create a support request against the virtual machine resource, you encounter the following error</span></span>

![Errore relativo alla sottoscrizione](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="8ead5-110">Per la gestione delle richieste di supporto è necessaria l'autorizzazione di scrittura o un ruolo con l'azione Microsoft.Support/* nell'ambito della sottoscrizione in grado di creare e gestire le richieste di supporto.</span><span class="sxs-lookup"><span data-stu-id="8ead5-110">In support request management, you need write permission or a role that has the Support action Microsoft.Support/* at the Subscription scope to be able to create and manage support requests.</span></span>

<span data-ttu-id="8ead5-111">L'articolo seguente illustra come è possibile usare il Controllo degli accessi in base al ruolo di Azure per creare e gestire le richieste di supporto nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ead5-111">The following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) to create and manage support requests in the Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8ead5-112">Introduzione</span><span class="sxs-lookup"><span data-stu-id="8ead5-112">Getting Started</span></span>

<span data-ttu-id="8ead5-113">Nell'esempio precedente è possibile creare una richiesta di supporto per la risorsa se il proprietario della sottoscrizione ha assegnato un ruolo personalizzato di Controllo degli accessi in base al ruolo nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8ead5-113">Using the example above, you would be able to create a support request for your resource if you were assigned a custom RBAC role on the subscription by the subscription owner.</span></span>
<span data-ttu-id="8ead5-114">I [ruoli personalizzati di Controllo degli accessi in base al ruolo](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) possono essere creati usando Azure PowerShell, l'interfaccia della riga di comando di Azure e l'API REST.</span><span class="sxs-lookup"><span data-stu-id="8ead5-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and the REST API.</span></span>

<span data-ttu-id="8ead5-115">La proprietà Actions di un ruolo personalizzato specifica le operazioni di Azure a cui il ruolo concede l'accesso.</span><span class="sxs-lookup"><span data-stu-id="8ead5-115">The actions property of a custom role specifies the Azure operations to which the role grants access.</span></span>
<span data-ttu-id="8ead5-116">Per creare un ruolo personalizzato per la gestione delle richieste di supporto, il ruolo deve includere l'azione Microsoft.Support/*</span><span class="sxs-lookup"><span data-stu-id="8ead5-116">To create a custom role for support request management, the role must have the action Microsoft.Support/*</span></span>

<span data-ttu-id="8ead5-117">Di seguito è riportato un esempio di un ruolo personalizzato che consente di creare e gestire le richieste di supporto.</span><span class="sxs-lookup"><span data-stu-id="8ead5-117">Here’s an example of a custom role you can use to create and manage support requests.</span></span>
<span data-ttu-id="8ead5-118">Questo ruolo è stato denominato "Support Request Contributor" ed ecco come si fa riferimento al ruolo personalizzato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="8ead5-118">We’ve named this role “Support Request Contributor” and that’s how we refer to the custom role in this article.</span></span>

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

<span data-ttu-id="8ead5-119">Seguire i passaggi descritti in [questo video](https://www.youtube.com/watch?v=-PaBaDmfwKI) per imparare a creare un ruolo personalizzato per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8ead5-119">Follow the steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) to learn how to create a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-the-azure-portal"></a><span data-ttu-id="8ead5-120">Creare e gestire le richieste di supporto nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8ead5-120">Create and manage support requests in the Azure portal</span></span>

<span data-ttu-id="8ead5-121">Esaminiamo un esempio in cui si è proprietari della sottoscrizione "Visual Studio MSDN Subscription".</span><span class="sxs-lookup"><span data-stu-id="8ead5-121">Let’s take an example – you are the owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="8ead5-122">Joe è il collega proprietario delle risorse in alcuni gruppi di risorse nella sottoscrizione e autorizzazione di lettura per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8ead5-122">Joe is your peer who is a resource owner to some of the resource groups in this subscription and has read permission to the subscription.</span></span>
<span data-ttu-id="8ead5-123">Si vuole concedere al collega Joe l'accesso per poter creare e gestire i ticket di supporto per le risorse in questa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8ead5-123">You wish to give access to your peer, Joe, the ability to create and manage support tickets for the resources under this subscription.</span></span>

1. <span data-ttu-id="8ead5-124">Il primo passaggio consiste nel passare alla sottoscrizione e in "Impostazioni" viene visualizzato un elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="8ead5-124">The first step is to go to the subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="8ead5-125">Fare clic sull'utente Joe che ha accesso in lettura per la sottoscrizione e assegnargli un nuovo ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="8ead5-125">Click the user Joe who has reader access on the Subscription and let’s assign a new custom role to him.</span></span>

    ![Aggiungi ruolo](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="8ead5-127">Fare clic su "Aggiungi" nel pannello "Utenti".</span><span class="sxs-lookup"><span data-stu-id="8ead5-127">Click "Add" under the "Users" blade.</span></span> <span data-ttu-id="8ead5-128">Selezionare il ruolo personalizzato di "Support Request Contributor" nell'elenco di ruoli</span><span class="sxs-lookup"><span data-stu-id="8ead5-128">Select the custom role "Support Request Contributor" from the list of roles</span></span>

    ![Aggiungere il ruolo di collaboratore di supporto](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="8ead5-130">Dopo avere selezionato il nome del ruolo, fare clic su "Aggiungi utenti" e immettere le credenziali di posta elettronica di Joe.</span><span class="sxs-lookup"><span data-stu-id="8ead5-130">After selecting the role name, click "Add users" and enter the Joe's email credentials.</span></span> <span data-ttu-id="8ead5-131">Fare clic su "Seleziona"</span><span class="sxs-lookup"><span data-stu-id="8ead5-131">Click "Select"</span></span>

    ![Aggiungi utenti](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="8ead5-133">Fare clic su "OK" per procedere</span><span class="sxs-lookup"><span data-stu-id="8ead5-133">Click "Ok" to proceed</span></span>

    ![Aggiungere un accesso](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="8ead5-135">Si noti ora che l'utente con il ruolo personalizzato appena aggiunto "Support Request Contributor" diventa visibile nella sottoscrizione di cui si è proprietari</span><span class="sxs-lookup"><span data-stu-id="8ead5-135">Now you see the user with the newly added custom role "Support Request Contributor" under the Subscription for which you are the owner</span></span>

    ![Utente aggiunto](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="8ead5-137">Quando Joe accederà al portale, la sottoscrizione a cui è stato aggiunto risulterà visibile.</span><span class="sxs-lookup"><span data-stu-id="8ead5-137">When Joe logs in the portal, he sees the subscription to which he was added.</span></span>

7. <span data-ttu-id="8ead5-138">Joe fa clic su "Nuova richiesta di supporto" nel pannello "Guida e supporto tecnico" ed è in grado di creare richieste di supporto per "Visual Studio Ultimate con MSDN"</span><span class="sxs-lookup"><span data-stu-id="8ead5-138">Joe clicks "New Support request" from the "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![Nuova richiesta di supporto](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="8ead5-140">Fare clic su "Tutte le richieste di supporto" Joe possibile visualizzare l'elenco delle richieste di supporto creato per questa sottoscrizione ![Case visualizzazione dettagli](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="8ead5-140">Clicking "All support requests" Joe can see the list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-the-azure-portal"></a><span data-ttu-id="8ead5-141">Rimuovere l'accesso alle richieste di supporto nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8ead5-141">Remove support request access in the Azure portal</span></span>

<span data-ttu-id="8ead5-142">Esattamente come è possibile concedere l'accesso a un utente per creare e gestire le richieste di supporto, è possibile anche rimuovere l'accesso per l'utente.</span><span class="sxs-lookup"><span data-stu-id="8ead5-142">Just as it is possible to grant access to a user to create and manage support requests, it's possible to remove access for the user as well.</span></span>
<span data-ttu-id="8ead5-143">Per rimuovere la possibilità di creare e gestire le richieste di supporto, passare alla sottoscrizione, fare clic su "Impostazioni", quindi sull'utente, in questo caso, Joe.</span><span class="sxs-lookup"><span data-stu-id="8ead5-143">To remove the ability to create and manage support requests, go to the Subscription, click "Settings" and click the user (in this case, Joe).</span></span>
<span data-ttu-id="8ead5-144">Fare clic con il pulsante destro del mouse sul nome del ruolo "Support Request Contributor" e fare clic su "Rimuovi"</span><span class="sxs-lookup"><span data-stu-id="8ead5-144">Right-click the role name, "Support Request Contributor" and click "Remove"</span></span>

![Rimuovere l'accesso alle richiesta di supporto](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="8ead5-146">Quando Joe eseguirà l'accesso al portale e tenterà di creare una richiesta di supporto, verrà visualizzato l'errore seguente</span><span class="sxs-lookup"><span data-stu-id="8ead5-146">When Joe logs in to the portal and tries to create a support request, he encounters the following error</span></span>

![Errore di sottoscrizione 2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="8ead5-148">Quando Joe fa clic su "Tutte le richieste di supporto", non sarà visibile nessuna richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="8ead5-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![Visualizzazione dettagli del caso 2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
