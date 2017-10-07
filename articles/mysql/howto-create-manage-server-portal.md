---
title: aaaCreate e gestire i Database di Azure per il server MySQL tramite il portale di Azure | Documenti Microsoft
description: "Questo articolo descrive come è possibile creare un nuovo Database di Azure per il server MySQL e gestire rapidamente server hello utilizzando hello portale di Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="c6804-103">Creare e gestire Database di Azure per il server MySQL con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c6804-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="c6804-104">Questo articolo descrive come è possibile creare un nuovo Database di Azure per il server MySQL e gestire rapidamente server hello utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6804-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage hello server using hello Azure Portal.</span></span> <span data-ttu-id="c6804-105">Gestione del server include la visualizzazione di database e i dettagli del server, la reimpostazione delle password e l'eliminazione di server hello.</span><span class="sxs-lookup"><span data-stu-id="c6804-105">Server management includes viewing server details & databases, resetting password and deleting hello server.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="c6804-106">Accedi toohello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c6804-106">Log in toohello Azure portal</span></span>
<span data-ttu-id="c6804-107">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c6804-107">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="c6804-108">Creare un database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="c6804-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="c6804-109">Seguire questi toocreate passaggi un Database di Azure per il server MySQL denominato "mysqlserver4demo"</span><span class="sxs-lookup"><span data-stu-id="c6804-109">Follow these steps toocreate an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="c6804-110">1-click **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c6804-110">1- Click **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

<span data-ttu-id="c6804-111">2-selezionare **database** nuova pagina hello e selezionare **Database di Azure per MySQL** dalla pagina di database hello.</span><span class="sxs-lookup"><span data-stu-id="c6804-111">2- Select **Databases** from hello New page, and select **Azure Database for MySQL** from hello Databases page.</span></span>

> <span data-ttu-id="c6804-112">Verrà creata un'istanza di Database di Azure per il server MySQL con un set definito di risorse di [calcolo e di archiviazione](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="c6804-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="c6804-113">Hello database viene creato all'interno di un gruppo di risorse di Azure e in un Database di Azure per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="c6804-113">hello database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="c6804-115">3 - compilare hello Azure Database MySQL form con hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="c6804-115">3- Fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="c6804-116">**Campo modulo**</span><span class="sxs-lookup"><span data-stu-id="c6804-116">**Form Field**</span></span> | <span data-ttu-id="c6804-117">**Descrizione campo**</span><span class="sxs-lookup"><span data-stu-id="c6804-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="c6804-118">*Server name* (Nome server)</span><span class="sxs-lookup"><span data-stu-id="c6804-118">*Server name*</span></span> | <span data-ttu-id="c6804-119">azure-mysql. Il nome server è univoco a livello globale</span><span class="sxs-lookup"><span data-stu-id="c6804-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="c6804-120">*Sottoscrizione*</span><span class="sxs-lookup"><span data-stu-id="c6804-120">*Subscription*</span></span> | <span data-ttu-id="c6804-121">MySQLaaS. Selezionare dall'elenco a discesa</span><span class="sxs-lookup"><span data-stu-id="c6804-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="c6804-122">*Gruppo di risorse*</span><span class="sxs-lookup"><span data-stu-id="c6804-122">*Resource group*</span></span> | <span data-ttu-id="c6804-123">myresource. Creare un nuovo gruppo di risorse o usarne uno esistente</span><span class="sxs-lookup"><span data-stu-id="c6804-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="c6804-124">*Accesso amministratore server*</span><span class="sxs-lookup"><span data-stu-id="c6804-124">*Server admin login*</span></span> | <span data-ttu-id="c6804-125">myadmin (configurare il nome dell'account amministratore)</span><span class="sxs-lookup"><span data-stu-id="c6804-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="c6804-126">*Password*</span><span class="sxs-lookup"><span data-stu-id="c6804-126">*Password*</span></span> | <span data-ttu-id="c6804-127">Definire la password dell'account amministratore</span><span class="sxs-lookup"><span data-stu-id="c6804-127">setup admin account password</span></span> |
| <span data-ttu-id="c6804-128">*Conferma password*</span><span class="sxs-lookup"><span data-stu-id="c6804-128">*Confirm password*</span></span> | <span data-ttu-id="c6804-129">Confermare la password dell'account amministratore</span><span class="sxs-lookup"><span data-stu-id="c6804-129">confirm admin account password</span></span> |
| <span data-ttu-id="c6804-130">*Posizione*</span><span class="sxs-lookup"><span data-stu-id="c6804-130">*Location*</span></span> | <span data-ttu-id="c6804-131">Europa settentrionale. La scelta è tra Europa settentrionale e Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="c6804-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="c6804-132">*Versione*</span><span class="sxs-lookup"><span data-stu-id="c6804-132">*Version*</span></span> | <span data-ttu-id="c6804-133">5.6. Scegliere la versione di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="c6804-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="c6804-134">Fare clic su 4 **tariffario** toospecify hello servizio livello di prestazioni e per il nuovo server.</span><span class="sxs-lookup"><span data-stu-id="c6804-134">4- Click **Pricing tier** toospecify hello service tier and performance level for your new server.</span></span> <span data-ttu-id="c6804-135">Il numero delle unità di calcolo può essere configurato tra 50 e 100 nel piano Basic e tra 100 e 200 nel piano Standard. È possibile aggiungere spazio di archiviazione in base alla quantità inclusa.</span><span class="sxs-lookup"><span data-stu-id="c6804-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="c6804-136">Per questa guida si sceglieranno 50 unità di calcolo e 50 GB.</span><span class="sxs-lookup"><span data-stu-id="c6804-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="c6804-137">Fare clic su **OK** toosave la selezione.</span><span class="sxs-lookup"><span data-stu-id="c6804-137">Click **OK** toosave your selection.</span></span>
<span data-ttu-id="c6804-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="c6804-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="c6804-139">Fare clic su 5 **crea** server hello tooprovision.</span><span class="sxs-lookup"><span data-stu-id="c6804-139">5- Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="c6804-140">Il provisioning richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="c6804-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="c6804-141">Controllare hello **toodashboard Pin** rilevamento semplice di opzione tooallow delle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="c6804-141">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="c6804-142">Sebbene too1000GB nel livello di base e 10000GB nello Standard sarà supportato livello per l'archiviazione, per l'anteprima pubblica, archiviazione massima hello è comunque limitata too1000GB temporaneamente.</span><span class="sxs-lookup"><span data-stu-id="c6804-142">Although up too1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, hello maximum storage is still limited too1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="c6804-143">Aggiornare un'istanza di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="c6804-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="c6804-144">Dopo il provisioning di nuovi server, l'utente ha 2 Opzioni tooedit un server esistente: reimpostare la password dell'amministratore o la scala su/giù server hello modificando l'unità di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="c6804-144">After new server is provisioned, user has 2 options tooedit an existing server: reset administrator password or scale up/down hello server by changing hello compute-units.</span></span>

### <a name="change-hello-administrator-user-password"></a><span data-ttu-id="c6804-145">Password dell'utente amministratore hello modifica</span><span class="sxs-lookup"><span data-stu-id="c6804-145">Change hello administrator user password</span></span>
<span data-ttu-id="c6804-146">1 - server hello **Panoramica** pannello, fare clic su **reimpostazione password** toopopulate una finestra di input e Conferma password.</span><span class="sxs-lookup"><span data-stu-id="c6804-146">1- On hello server **Overview** blade, click **Reset password** toopopulate a password input and confirmation window.</span></span>

<span data-ttu-id="c6804-147">2 - Immettere la nuova password e Conferma password hello nella finestra di hello come indicato di seguito: ![reimpostazione della password](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="c6804-147">2- Enter new password and confirm hello password in hello window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="c6804-148">3-fare clic su **OK** nuova password di toosave hello.</span><span class="sxs-lookup"><span data-stu-id="c6804-148">3- Click **OK** toosave hello new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="c6804-149">Aumentare/ridurre le prestazioni modificando le unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="c6804-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="c6804-150">1 - nel pannello server hello in **impostazioni**, fare clic su **tariffario** tooopen hello prezzi livello pannello hello Azure Database per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="c6804-150">1- On hello server blade, under **Settings**, click **Pricing tier** tooopen hello Pricing tier blade for hello Azure Database for MySQL server.</span></span>

<span data-ttu-id="c6804-151">2-seguire il passaggio 4 **creare un Database di Azure per il server MySQL** toochange unità di calcolo in hello stesso livello di prezzo.</span><span class="sxs-lookup"><span data-stu-id="c6804-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** toochange Compute Units in hello same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="c6804-152">Eliminare un'istanza di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="c6804-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="c6804-153">1 - server hello **Panoramica** pannello, fare clic su **eliminare** del Pannello di conferma eliminazione comando pulsante tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="c6804-153">1- On hello server **Overview** blade, click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

<span data-ttu-id="c6804-154">Nome corretto del server di tipo 2 hello nella casella di input del pannello hello conferma double.</span><span class="sxs-lookup"><span data-stu-id="c6804-154">2- Type hello correct server name in input box of hello blade for double confirmation.</span></span>

<span data-ttu-id="c6804-155">3-fare clic su **eliminare** tooconfirm l'eliminazione di azione di nuovo il pulsante e attendere che "L'eliminazione di successo" popup nella barra di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="c6804-155">3- Click **Delete** button again tooconfirm deleting action and wait for “Deleting success” popup on hello notification bar.</span></span>

## <a name="list-hello-azure-database-for-mysql-databases"></a><span data-ttu-id="c6804-156">Elenco hello Database di Azure per i database MySQL</span><span class="sxs-lookup"><span data-stu-id="c6804-156">List hello Azure Database for MySQL databases</span></span>
<span data-ttu-id="c6804-157">Nel server di hello **Panoramica** pannello, scorrere verso il basso fino a visualizzare database hello riquadro nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="c6804-157">On hello server **Overview** blade, scroll down until you see hello database tile on hello bottom.</span></span> <span data-ttu-id="c6804-158">Tutti i database hello verranno elencati nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="c6804-158">All hello databases will be listed in hello table.</span></span> <span data-ttu-id="c6804-159">Fare clic su **eliminare** del Pannello di conferma eliminazione comando pulsante tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="c6804-159">click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="c6804-161">Visualizzare i dettagli di un'istanza di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="c6804-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="c6804-162">Fare clic su **proprietà** in **impostazioni** sul server hello pannello aprirà hello **proprietà** blade.</span><span class="sxs-lookup"><span data-stu-id="c6804-162">Click **Properties** under **Settings** on hello server blade will open hello **Properties** blade.</span></span> <span data-ttu-id="c6804-163">È quindi possibile visualizzare tutte le informazioni dettagliate sui server hello.</span><span class="sxs-lookup"><span data-stu-id="c6804-163">Then you can view all detailed information about hello server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6804-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c6804-164">Next steps</span></span>

[<span data-ttu-id="c6804-165">Guida introduttiva: Creare Database di Azure per il server MySQL con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c6804-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
