---
title: Creare e gestire Database di Azure per il server MySQL con il portale di Azure | Microsoft Docs
description: Questo articolo descrive come creare rapidamente una nuova istanza di Database di Azure per il server MySQL e gestire il server con il portale di Azure.
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4605518b6955d9943e76c25df2d4105a6a94433d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="a2475-103">Creare e gestire Database di Azure per il server MySQL con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a2475-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="a2475-104">Questo articolo descrive come creare rapidamente una nuova istanza di Database di Azure per il server MySQL e gestire il server con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2475-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage the server using the Azure Portal.</span></span> <span data-ttu-id="a2475-105">La gestione del server include la visualizzazione di database e dettagli del server, la reimpostazione delle password e l'eliminazione del server.</span><span class="sxs-lookup"><span data-stu-id="a2475-105">Server management includes viewing server details & databases, resetting password and deleting the server.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="a2475-106">Accedere al Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2475-106">Log in to the Azure portal</span></span>
<span data-ttu-id="a2475-107">Accedere al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a2475-107">Log in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="a2475-108">Creare un'istanza di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="a2475-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="a2475-109">Seguire questi passaggi per creare un'istanza di Database di Azure per il server MySQL denominata "mysqlserver4demo"</span><span class="sxs-lookup"><span data-stu-id="a2475-109">Follow these steps to create an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="a2475-110">1- Fare clic sul pulsante **Nuovo** nell'angolo superiore sinistro del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2475-110">1- Click **New** button found on the upper left-hand corner of the Azure portal.</span></span>

<span data-ttu-id="a2475-111">2- Selezionare **Database** nella pagina Nuovo e quindi **Database di Azure per MySQL** nella pagina Database.</span><span class="sxs-lookup"><span data-stu-id="a2475-111">2- Select **Databases** from the New page, and select **Azure Database for MySQL** from the Databases page.</span></span>

> <span data-ttu-id="a2475-112">Verrà creata un'istanza di Database di Azure per il server MySQL con un set definito di risorse di [calcolo e di archiviazione](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a2475-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="a2475-113">Il database viene creato in un gruppo di risorse di Azure e in un'istanza di Database di Azure per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="a2475-113">The database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="a2475-115">3- Compilare il modulo Database di Azure per MySQL con le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2475-115">3- Fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="a2475-116">**Campo modulo**</span><span class="sxs-lookup"><span data-stu-id="a2475-116">**Form Field**</span></span> | <span data-ttu-id="a2475-117">**Descrizione campo**</span><span class="sxs-lookup"><span data-stu-id="a2475-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="a2475-118">*Server name* (Nome server)</span><span class="sxs-lookup"><span data-stu-id="a2475-118">*Server name*</span></span> | <span data-ttu-id="a2475-119">azure-mysql. Il nome server è univoco a livello globale</span><span class="sxs-lookup"><span data-stu-id="a2475-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="a2475-120">*Sottoscrizione*</span><span class="sxs-lookup"><span data-stu-id="a2475-120">*Subscription*</span></span> | <span data-ttu-id="a2475-121">MySQLaaS. Selezionare dall'elenco a discesa</span><span class="sxs-lookup"><span data-stu-id="a2475-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="a2475-122">*Gruppo di risorse*</span><span class="sxs-lookup"><span data-stu-id="a2475-122">*Resource group*</span></span> | <span data-ttu-id="a2475-123">myresource. Creare un nuovo gruppo di risorse o usarne uno esistente</span><span class="sxs-lookup"><span data-stu-id="a2475-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="a2475-124">*Accesso amministratore server*</span><span class="sxs-lookup"><span data-stu-id="a2475-124">*Server admin login*</span></span> | <span data-ttu-id="a2475-125">myadmin (configurare il nome dell'account amministratore)</span><span class="sxs-lookup"><span data-stu-id="a2475-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="a2475-126">*Password*</span><span class="sxs-lookup"><span data-stu-id="a2475-126">*Password*</span></span> | <span data-ttu-id="a2475-127">Definire la password dell'account amministratore</span><span class="sxs-lookup"><span data-stu-id="a2475-127">setup admin account password</span></span> |
| <span data-ttu-id="a2475-128">*Conferma password*</span><span class="sxs-lookup"><span data-stu-id="a2475-128">*Confirm password*</span></span> | <span data-ttu-id="a2475-129">Confermare la password dell'account amministratore</span><span class="sxs-lookup"><span data-stu-id="a2475-129">confirm admin account password</span></span> |
| <span data-ttu-id="a2475-130">*Posizione*</span><span class="sxs-lookup"><span data-stu-id="a2475-130">*Location*</span></span> | <span data-ttu-id="a2475-131">Europa settentrionale. La scelta è tra Europa settentrionale e Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="a2475-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="a2475-132">*Versione*</span><span class="sxs-lookup"><span data-stu-id="a2475-132">*Version*</span></span> | <span data-ttu-id="a2475-133">5.6. Scegliere la versione di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="a2475-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="a2475-134">4- Fare clic su **Piano tariffario** per specificare il livello di servizio e il livello delle prestazioni per il nuovo server.</span><span class="sxs-lookup"><span data-stu-id="a2475-134">4- Click **Pricing tier** to specify the service tier and performance level for your new server.</span></span> <span data-ttu-id="a2475-135">Il numero delle unità di calcolo può essere configurato tra 50 e 100 nel piano Basic e tra 100 e 200 nel piano Standard. È possibile aggiungere spazio di archiviazione in base alla quantità inclusa.</span><span class="sxs-lookup"><span data-stu-id="a2475-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="a2475-136">Per questa guida si sceglieranno 50 unità di calcolo e 50 GB.</span><span class="sxs-lookup"><span data-stu-id="a2475-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="a2475-137">Fare clic su **OK** per salvare la selezione.</span><span class="sxs-lookup"><span data-stu-id="a2475-137">Click **OK** to save your selection.</span></span>
<span data-ttu-id="a2475-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="a2475-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="a2475-139">5- Fare clic su **Crea** per effettuare il provisioning del server.</span><span class="sxs-lookup"><span data-stu-id="a2475-139">5- Click **Create** to provision the server.</span></span> <span data-ttu-id="a2475-140">Il provisioning richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="a2475-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="a2475-141">Selezionare l'opzione **Aggiungi al dashboard** per tenere facilmente traccia delle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="a2475-141">Check the **Pin to dashboard** option to allow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="a2475-142">Anche se sono supportati fino a 1000 GB di spazio di archiviazione nel piano Basic e fino a 10000 GB nel piano Standard, per l'anteprima pubblica lo spazio di archiviazione massimo è ancora limitato temporaneamente a 1000 GB.</span><span class="sxs-lookup"><span data-stu-id="a2475-142">Although up to 1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, the maximum storage is still limited to 1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="a2475-143">Aggiornare un'istanza di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="a2475-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="a2475-144">Dopo il provisioning di un nuovo server, l'utente ha 2 opzioni per modificare un server esistente: reimpostare la password amministratore oppure aumentare/ridurre le prestazioni del server modificando le unità di calcolo.</span><span class="sxs-lookup"><span data-stu-id="a2475-144">After new server is provisioned, user has 2 options to edit an existing server: reset administrator password or scale up/down the server by changing the compute-units.</span></span>

### <a name="change-the-administrator-user-password"></a><span data-ttu-id="a2475-145">Modificare la password amministratore</span><span class="sxs-lookup"><span data-stu-id="a2475-145">Change the administrator user password</span></span>
<span data-ttu-id="a2475-146">1- Nel pannello **Panoramica** del server fare clic su **Reimposta password** per popolare una finestra di input e conferma della password.</span><span class="sxs-lookup"><span data-stu-id="a2475-146">1- On the server **Overview** blade, click **Reset password** to populate a password input and confirmation window.</span></span>

<span data-ttu-id="a2475-147">2- Immettere la nuova password e confermarla nella finestra come illustrato di seguito: ![reimposta password](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="a2475-147">2- Enter new password and confirm the password in the window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="a2475-148">3- Fare clic su **OK** per salvare la nuova password.</span><span class="sxs-lookup"><span data-stu-id="a2475-148">3- Click **OK** to save the new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="a2475-149">Aumentare/ridurre le prestazioni modificando le unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="a2475-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="a2475-150">1- Nel pannello del server fare clic su **Piano tariffario** in **Impostazioni** per aprire il pannello Piano tariffario relativo all'istanza di Database di Azure per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="a2475-150">1- On the server blade, under **Settings**, click **Pricing tier** to open the Pricing tier blade for the Azure Database for MySQL server.</span></span>

<span data-ttu-id="a2475-151">2- Seguire il passaggio 4 in **Creare Database di Azure per il server MySQL** per modificare le unità di calcolo nello stesso piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="a2475-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** to change Compute Units in the same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="a2475-152">Eliminare un'istanza di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="a2475-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="a2475-153">1- Nel pannello **Panoramica** del server fare clic sul pulsante **Elimina** per aprire il pannello di conferma dell'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="a2475-153">1- On the server **Overview** blade, click **Delete** command button to open the Deleting confirmation blade.</span></span>

<span data-ttu-id="a2475-154">2- Digitare il nome server corretto nella casella di input del pannello per una doppia conferma.</span><span class="sxs-lookup"><span data-stu-id="a2475-154">2- Type the correct server name in input box of the blade for double confirmation.</span></span>

<span data-ttu-id="a2475-155">3- Fare di nuovo clic su **Elimina** per confermare l'eliminazione e attendere che nella barra di notifica venga visualizzato un messaggio popup che indica che l'eliminazione è stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="a2475-155">3- Click **Delete** button again to confirm deleting action and wait for “Deleting success” popup on the notification bar.</span></span>

## <a name="list-the-azure-database-for-mysql-databases"></a><span data-ttu-id="a2475-156">Elencare i database di Database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="a2475-156">List the Azure Database for MySQL databases</span></span>
<span data-ttu-id="a2475-157">Nel pannello **Panoramica** del server scorrere verso il basso fino al riquadro dei database nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="a2475-157">On the server **Overview** blade, scroll down until you see the database tile on the bottom.</span></span> <span data-ttu-id="a2475-158">Tutti i database verranno elencati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="a2475-158">All the databases will be listed in the table.</span></span> <span data-ttu-id="a2475-159">Fare clic sul pulsante **Elimina** per aprire il pannello di conferma dell'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="a2475-159">click **Delete** command button to open the Deleting confirmation blade.</span></span>

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="a2475-161">Visualizzare i dettagli di un'istanza di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="a2475-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="a2475-162">Nel pannello del server fare clic su **Proprietà** in **Impostazioni** per aprire il pannello **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="a2475-162">Click **Properties** under **Settings** on the server blade will open the **Properties** blade.</span></span> <span data-ttu-id="a2475-163">Verranno visualizzate tutte le informazioni dettagliate sul server.</span><span class="sxs-lookup"><span data-stu-id="a2475-163">Then you can view all detailed information about the server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2475-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2475-164">Next steps</span></span>

[<span data-ttu-id="a2475-165">Guida introduttiva: Creare Database di Azure per il server MySQL con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a2475-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
