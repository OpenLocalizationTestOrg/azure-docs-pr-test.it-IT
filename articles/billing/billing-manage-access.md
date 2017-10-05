---
title: Gestire l'accesso alla fatturazione di Azure tramite i ruoli | Microsoft Docs
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: c70904097f139bc2178feed83f1cf1274f3c738d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-access-to-billing-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="719be-102">Gestire l'accesso alle informazioni di fatturazione per Azure tramite il controllo di accesso basato sui ruoli</span><span class="sxs-lookup"><span data-stu-id="719be-102">Manage access to billing information for Azure using role-based access control</span></span>

<span data-ttu-id="719be-103">È possibile concedere l'accesso alle informazioni di fatturazione di Azure ai membri del team assegnando uno dei ruoli utente seguenti alla sottoscrizione: amministratore dell'account, amministratore del servizio, coamministratore, proprietario, collaboratore, lettore e lettore della fatturazione.</span><span class="sxs-lookup"><span data-stu-id="719be-103">You can grant access for Azure billing information to members of your team by assigning one of the following user roles to your subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="719be-104">Questi hanno accesso alle informazioni di fatturazione nel [portale di Azure](https://portal.azure.com/) e possono usare le [API di fatturazione](billing-usage-rate-card-overview.md) per ottenere le fatture a livello di programmazione, dopo aver scelto questa modalità, e i dettagli di uso.</span><span class="sxs-lookup"><span data-stu-id="719be-104">They would have access to billing information in the [Azure portal](https://portal.azure.com/), and they can use the [Billing APIs](billing-usage-rate-card-overview.md) to programmatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="719be-105">Per altre informazioni su chi può concedere ruoli e i compiti per ogni ruolo, vedere [Ruoli in Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="719be-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="719be-106"><a name="opt-in"></a> Consentire ad altri utenti di accedere alle fatture</span><span class="sxs-lookup"><span data-stu-id="719be-106"><a name="opt-in"></a> Allowing additional users to access invoices</span></span>

<span data-ttu-id="719be-107">L'amministratore dell'account deve concedere il consenso esplicito tramite il [portale di Azure](https://portal.azure.com/) che concede ad altri utenti di accedere alle fatture e tramite le API.</span><span class="sxs-lookup"><span data-stu-id="719be-107">The Account Administrator must opt in using the [Azure portal](https://portal.azure.com/) allow access to invoices for other users and via API.</span></span>

1. <span data-ttu-id="719be-108">In qualità di amministratore dell'account, selezionare la sottoscrizione dal [pannello Sottoscrizioni](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="719be-108">As the Account Administrator, select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="719be-109">Selezionare **Fatture** e quindi **Access to invoices** (Accesso alle fatture).</span><span class="sxs-lookup"><span data-stu-id="719be-109">Select **Invoices** and then **Access to invoices**.</span></span>

    ![Lo screenshot mostra come delegare l'accesso alle fatture](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="719be-111">Impostare su **On** l'accesso, quindi salvare le modifiche per consentire agli utenti nei ruoli con ambito della sottoscrizione di scaricare la fattura.</span><span class="sxs-lookup"><span data-stu-id="719be-111">Turn **On** the access followed by saving the changes, to allow users in subscription scoped roles to download invoice.</span></span>

    ![Lo screenshot mostra le impostazioni on-off per delegare l'accesso alla fattura](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="719be-113">Il consenso esplicito permette all'amministratore del servizio, al coamministratore, al proprietario, al collaboratore, al lettore e al lettore della fatturazione nella sottoscrizione di scaricare le fatture PDF nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="719be-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on the subscription to download PDF invoices in the Azure portal.</span></span> <span data-ttu-id="719be-114">Tuttavia, le fatture redatte prima di dicembre 2016 sono disponibili solo per l'amministratore dell'account attualmente.</span><span class="sxs-lookup"><span data-stu-id="719be-114">However, invoices older than December 2016 are available only to the Account Administrator for now.</span></span>

<span data-ttu-id="719be-115">L'amministratore dell'account può anche impostare una configurazione in modo da ricevere le fatture tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="719be-115">The Account Administrator can also configure to have invoices sent via email.</span></span> <span data-ttu-id="719be-116">Per altre informazioni, vedere [Ottenere la fatturazione tramite posta elettronica](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="719be-116">To learn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-to-the-billing-reader-role"></a><span data-ttu-id="719be-117">Aggiunta di utenti al ruolo di lettore della fatturazione</span><span class="sxs-lookup"><span data-stu-id="719be-117">Adding users to the Billing Reader role</span></span>

<span data-ttu-id="719be-118">Il ruolo di lettore della fatturazione dispone di accesso in sola lettura alle informazioni di fatturazione della sottoscrizione nel portale di Azure e nessun accesso ai servizi, ad esempio macchine virtuali e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="719be-118">The Billing Reader role has read-only access to subscription billing information in Azure portal, and no access to services such as VMs and storage accounts.</span></span> <span data-ttu-id="719be-119">Assegnare il ruolo di lettore della fatturazione a un utente che richiede l'accesso alle informazioni di fatturazione della sottoscrizione, ma non la possibilità di gestire i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="719be-119">Assign the Billing Reader role to someone that needs access to the subscription billing information but not the ability to manage Azure services.</span></span> <span data-ttu-id="719be-120">Questo ruolo è appropriato per gli utenti che in un'organizzazione eseguono solo la gestione finanziaria e dei costi per le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="719be-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="719be-121">Selezionare la sottoscrizione dal [pannello delle Sottoscrizioni](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="719be-121">Select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="719be-122">Selezionare **Controllo di accesso (IAM)** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="719be-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![Schermate che mostrano l'IAM nel pannello della sottoscrizione](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="719be-124">Scegliere **Billing Reader** (Lettore della fatturazione) nella pagina **Selezionare un ruolo**.</span><span class="sxs-lookup"><span data-stu-id="719be-124">Choose **Billing Reader** in the **Select a role** page.</span></span>

    ![Schermate che mostrano il lettore della fatturazione nella visualizzazione del popup](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="719be-126">Digitare il messaggio di posta elettronica per l'utente che si desidera invitare, quindi fare clic su **OK** per inviare l'invito.</span><span class="sxs-lookup"><span data-stu-id="719be-126">Type the email for the user you want to invite, then click **OK** to send the invitation.</span></span>

    ![Schermata che mostra come immettere il messaggio di posta elettronica per invitare un utente](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="719be-128">Seguire le istruzioni nel messaggio di posta elettronica di invito per accedere come un lettore della fatturazione.</span><span class="sxs-lookup"><span data-stu-id="719be-128">Follow instructions in the invite email to log in as a Billing Reader.</span></span>

    ![Schermata che mostra ciò che vede il lettore della fatturazione nel portale di Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="719be-130">La funzionalità Fatturazione per lettore è disponibile in anteprima e non supporta ancora le sottoscrizioni enterprise (EA) o i cloud non globali.</span><span class="sxs-lookup"><span data-stu-id="719be-130">The Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-to-other-roles"></a><span data-ttu-id="719be-131">Aggiunta di utenti ad altri ruoli</span><span class="sxs-lookup"><span data-stu-id="719be-131">Adding users to other roles</span></span>

<span data-ttu-id="719be-132">Gli utenti in altri ruoli, ad esempio proprietario o collaboratore, possono accedere non solo alle informazioni di fatturazione, ma anche ai servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="719be-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="719be-133">Per gestire questi ruoli, vedere [Aggiungere o modificare i ruoli di amministratore di Azure che gestiscono la sottoscrizione o i servizi](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="719be-133">To manage these roles, see [Add or change Azure administrator roles that manage the subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-the-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="719be-134">Chi può accedere al [Centro account](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="719be-134">Who can access the [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="719be-135">Solo l'amministratore dell'account può accedere al Centro account.</span><span class="sxs-lookup"><span data-stu-id="719be-135">Only the Account Administrator can log in to the Account center.</span></span> <span data-ttu-id="719be-136">L'amministratore dell'account è il proprietario legale della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="719be-136">The Account Administrator is the legal owner of the subscription.</span></span> <span data-ttu-id="719be-137">Per impostazione predefinita, la persona che ha effettuato l'accesso o ha acquistato la sottoscrizione di Azure è l'amministratore dell'account, a meno che non la [proprietà della sottoscrizione non venga trasferita](billing-subscription-transfer.md) a un altro utente.</span><span class="sxs-lookup"><span data-stu-id="719be-137">By default, the person who signed up for or bought the Azure subscription is the Account Administrator, unless the [subscription ownership was transferred](billing-subscription-transfer.md) to somebody else.</span></span> <span data-ttu-id="719be-138">L'amministratore dell'account può creare e annullare le sottoscrizioni, modificare l'indirizzo di fatturazione per una sottoscrizione e gestire i criteri di accesso alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="719be-138">The Account Administrator can create subscriptions, cancel subscriptions, change the billing address for a subscription, and manage access policies for the subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="719be-139">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="719be-139">Need help?</span></span> <span data-ttu-id="719be-140">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="719be-140">Contact support.</span></span>

<span data-ttu-id="719be-141">Per altre domande, è possibile [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) per ottenere una rapida risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="719be-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
