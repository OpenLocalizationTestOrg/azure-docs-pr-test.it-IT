---
title: aaaManage tooAzure di accesso tramite ruoli di fatturazione | Documenti Microsoft
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
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="e673d-102">Gestire le informazioni di accesso toobilling per Azure tramite il controllo di accesso basato sui ruoli</span><span class="sxs-lookup"><span data-stu-id="e673d-102">Manage access toobilling information for Azure using role-based access control</span></span>

<span data-ttu-id="e673d-103">È possibile concedere l'accesso per Azure toomembers informazioni fatturazione del team tramite l'assegnazione di uno di hello sottoscrizione tooyour di ruoli utente di seguenti: Account amministratore, amministratore del servizio, coamministratore, proprietario, collaboratore, lettore e lettore fatturazione.</span><span class="sxs-lookup"><span data-stu-id="e673d-103">You can grant access for Azure billing information toomembers of your team by assigning one of hello following user roles tooyour subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="e673d-104">Hanno accesso toobilling informazioni in hello [portale di Azure](https://portal.azure.com/), e possono usare hello [fatturazione API](billing-usage-rate-card-overview.md) tooprogrammatically Visualizza fatture (una volta scelto-in) e informazioni di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="e673d-104">They would have access toobilling information in hello [Azure portal](https://portal.azure.com/), and they can use hello [Billing APIs](billing-usage-rate-card-overview.md) tooprogrammatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="e673d-105">Per altre informazioni su chi può concedere ruoli e i compiti per ogni ruolo, vedere [Ruoli in Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="e673d-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="e673d-106"><a name="opt-in"></a>Consentendo a utenti aggiuntivi tooaccess fatture</span><span class="sxs-lookup"><span data-stu-id="e673d-106"><a name="opt-in"></a> Allowing additional users tooaccess invoices</span></span>

<span data-ttu-id="e673d-107">Hello amministratore dell'Account deve acconsentire esplicitamente all'invio tramite hello [portale di Azure](https://portal.azure.com/) Consenti tooinvoices accesso ad altri utenti e tramite l'API.</span><span class="sxs-lookup"><span data-stu-id="e673d-107">hello Account Administrator must opt in using hello [Azure portal](https://portal.azure.com/) allow access tooinvoices for other users and via API.</span></span>

1. <span data-ttu-id="e673d-108">Come amministratore dell'Account di hello, selezionare la sottoscrizione da hello [pannello sottoscrizioni](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e673d-108">As hello Account Administrator, select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="e673d-109">Selezionare **fatture** e quindi **accedere tooinvoices**.</span><span class="sxs-lookup"><span data-stu-id="e673d-109">Select **Invoices** and then **Access tooinvoices**.</span></span>

    ![Schermata illustrata toodelegate accesso tooinvoices](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="e673d-111">Attivare **su** accesso hello seguita da salvare le modifiche di hello, gli utenti tooallow nella fattura toodownload ruoli con ambito di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="e673d-111">Turn **On** hello access followed by saving hello changes, tooallow users in subscription scoped roles toodownload invoice.</span></span>

    ![Schermata mostra tooinvoice accesso toodelegate-off](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="e673d-113">Acconsentito esplicitamente tradizionale di amministratore del servizio, coamministratore, proprietario, collaboratore, lettore e fatturazione lettore hello sottoscrizione toodownload PDF fatture hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e673d-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on hello subscription toodownload PDF invoices in hello Azure portal.</span></span> <span data-ttu-id="e673d-114">Tuttavia, più vecchi di dicembre 2016 sono disponibile toohello solo amministratore dell'Account per il momento.</span><span class="sxs-lookup"><span data-stu-id="e673d-114">However, invoices older than December 2016 are available only toohello Account Administrator for now.</span></span>

<span data-ttu-id="e673d-115">Hello amministratore dell'Account è anche possibile configurare le fatture toohave inviate tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="e673d-115">hello Account Administrator can also configure toohave invoices sent via email.</span></span> <span data-ttu-id="e673d-116">vedere, più toolearn [ottenere la fattura nel messaggio di posta elettronica](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="e673d-116">toolearn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-toohello-billing-reader-role"></a><span data-ttu-id="e673d-117">Aggiunta del ruolo di lettore fatturazione toohello utenti</span><span class="sxs-lookup"><span data-stu-id="e673d-117">Adding users toohello Billing Reader role</span></span>

<span data-ttu-id="e673d-118">ruolo di lettore fatturazione Hello dispone di accesso in sola lettura toosubscription le informazioni di fatturazione nel portale di Azure e non tooservices di accesso, ad esempio le macchine virtuali e gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e673d-118">hello Billing Reader role has read-only access toosubscription billing information in Azure portal, and no access tooservices such as VMs and storage accounts.</span></span> <span data-ttu-id="e673d-119">Assegnare hello fatturazione lettore ruolo toosomeone che deve accedere alle informazioni di fatturazione sottoscrizione toohello ma non hello possibilità toomanage Azure servizi.</span><span class="sxs-lookup"><span data-stu-id="e673d-119">Assign hello Billing Reader role toosomeone that needs access toohello subscription billing information but not hello ability toomanage Azure services.</span></span> <span data-ttu-id="e673d-120">Questo ruolo è appropriato per gli utenti che in un'organizzazione eseguono solo la gestione finanziaria e dei costi per le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="e673d-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="e673d-121">Selezionare la sottoscrizione da hello [pannello sottoscrizioni](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e673d-121">Select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="e673d-122">Selezionare **Controllo di accesso (IAM)** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e673d-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![Schermata mostra IAM nel Pannello di sottoscrizione hello](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="e673d-124">Scegliere **lettore fatturazione** in hello **selezionare un ruolo** pagina.</span><span class="sxs-lookup"><span data-stu-id="e673d-124">Choose **Billing Reader** in hello **Select a role** page.</span></span>

    ![Schermata mostra fatturazione lettore nella visualizzazione popup hello](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="e673d-126">Tipo di messaggio di posta elettronica hello per utente hello tooinvite desiderato, quindi fare clic su **OK** invito hello toosend.</span><span class="sxs-lookup"><span data-stu-id="e673d-126">Type hello email for hello user you want tooinvite, then click **OK** toosend hello invitation.</span></span>

    ![Schermata che mostra tooenter tooinvite di posta elettronica a un utente](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="e673d-128">Seguire le istruzioni toolog di posta elettronica di invito hello in come un lettore di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="e673d-128">Follow instructions in hello invite email toolog in as a Billing Reader.</span></span>

    ![Schermata che mostra cosa hello fatturazione lettura possa vedere nel portale di Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="e673d-130">funzionalità di fatturazione lettore Hello è disponibile in anteprima e non supporta ancora le sottoscrizioni enterprise (EA) o il cloud non globali.</span><span class="sxs-lookup"><span data-stu-id="e673d-130">hello Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-tooother-roles"></a><span data-ttu-id="e673d-131">Aggiunta di utenti tooother ruoli</span><span class="sxs-lookup"><span data-stu-id="e673d-131">Adding users tooother roles</span></span>

<span data-ttu-id="e673d-132">Gli utenti in altri ruoli, ad esempio proprietario o collaboratore, possono accedere non solo alle informazioni di fatturazione, ma anche ai servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e673d-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="e673d-133">toomanage questi ruoli, vedere [aggiungere o modificare ruoli di amministratore di Azure che gestiscono la sottoscrizione hello o servizi](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="e673d-133">toomanage these roles, see [Add or change Azure administrator roles that manage hello subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="e673d-134">Chi può accedere hello [centro Account](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="e673d-134">Who can access hello [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="e673d-135">Centro Account toohello può accedere solo hello amministratore dell'Account.</span><span class="sxs-lookup"><span data-stu-id="e673d-135">Only hello Account Administrator can log in toohello Account center.</span></span> <span data-ttu-id="e673d-136">Hello amministratore dell'Account è hello legittimo proprietario sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="e673d-136">hello Account Administrator is hello legal owner of hello subscription.</span></span> <span data-ttu-id="e673d-137">Per impostazione predefinita, hello persona iscritti a o acquistati hello sottoscrizione di Azure è hello amministratore dell'Account, a meno che non hello [la proprietà di sottoscrizione è stata trasferita](billing-subscription-transfer.md) toosomebody else.</span><span class="sxs-lookup"><span data-stu-id="e673d-137">By default, hello person who signed up for or bought hello Azure subscription is hello Account Administrator, unless hello [subscription ownership was transferred](billing-subscription-transfer.md) toosomebody else.</span></span> <span data-ttu-id="e673d-138">Hello amministratore dell'Account può creare sottoscrizioni, annullare sottoscrizioni, modificare l'indirizzo di fatturazione hello per una sottoscrizione e gestire i criteri di accesso per la sottoscrizione di hello.</span><span class="sxs-lookup"><span data-stu-id="e673d-138">hello Account Administrator can create subscriptions, cancel subscriptions, change hello billing address for a subscription, and manage access policies for hello subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="e673d-139">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="e673d-139">Need help?</span></span> <span data-ttu-id="e673d-140">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="e673d-140">Contact support.</span></span>

<span data-ttu-id="e673d-141">Se è ancora più domande, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.</span><span class="sxs-lookup"><span data-stu-id="e673d-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
