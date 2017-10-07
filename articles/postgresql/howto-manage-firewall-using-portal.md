---
title: aaaCreate e gestire i Database di Azure per le regole firewall PostgreSQL utilizzando hello portale di Azure | Documenti Microsoft
description: Creare e gestire i Database di Azure per le regole firewall PostgreSQL utilizzando hello portale di Azure
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="57954-103">Creare e gestire i Database di Azure per le regole firewall PostgreSQL utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="57954-103">Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="57954-104">Le regole del firewall a livello di server abilitare tooaccess agli amministratori un Database di Azure per PostgreSQL Server da un indirizzo IP specifico o l'intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="57954-104">Server-level firewall rules enable administrators tooaccess an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="57954-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="57954-105">Prerequisites</span></span>
<span data-ttu-id="57954-106">toostep tramite questa procedura-tooguide, è necessario:</span><span class="sxs-lookup"><span data-stu-id="57954-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="57954-107">Un server [Creare un database di Azure per PostgreSQL](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="57954-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="57954-108">Creare una regola del firewall a livello di server nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="57954-108">Create a server-level firewall rule in hello Azure portal</span></span>
1. <span data-ttu-id="57954-109">Nel Pannello di server PostgreSQL hello, in impostazioni fare clic su **sicurezza della connessione** tooopen hello sicurezza della connessione pannello hello Azure Database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="57954-109">On hello PostgreSQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for PostgreSQL.</span></span>

  ![Portale di Azure: fare clic su Sicurezza connessione](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="57954-111">Fare clic su **Aggiungi IP My** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="57954-111">Click **Add My IP** on hello toolbar.</span></span> <span data-ttu-id="57954-112">Questa viene creata automaticamente una regola con indirizzo IP di hello del computer, come percepito da hello sistema Azure.</span><span class="sxs-lookup"><span data-stu-id="57954-112">This will create a rule automatically with hello IP address of your computer, as perceived by hello Azure system.</span></span>

  ![Portale di Azure: fare clic su Aggiungi indirizzo IP corrente](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="57954-114">Verificare l'indirizzo IP prima di salvare la configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="57954-114">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="57954-115">In alcune situazioni, l'indirizzo IP hello osservato dal portale di Azure è diverso dall'indirizzo IP hello utilizzato quando l'accesso a hello internet e i server Azure.</span><span class="sxs-lookup"><span data-stu-id="57954-115">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="57954-116">Di conseguenza, potrebbe essere necessario toochange IP iniziale e finale IP toomake hello regola funzione hello come previsto.</span><span class="sxs-lookup"><span data-stu-id="57954-116">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>
<span data-ttu-id="57954-117">Utilizzare un motore di ricerca o altri toocheck strumento online il proprio indirizzo IP (ad esempio, ricerca Bing "che cos'è l'IP").</span><span class="sxs-lookup"><span data-stu-id="57954-117">Use a search engine or other online tool toocheck your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Ricerca Bing di What is my IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="57954-119">Aggiungere altri intervalli di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="57954-119">Add additional address ranges.</span></span> <span data-ttu-id="57954-120">Nelle regole di hello per hello Azure Database PostgreSQL firewall, è possibile specificare un singolo indirizzo IP o un intervallo di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="57954-120">In hello rules for hello Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="57954-121">Se si desidera toolimit hello regola tooone singolo indirizzo IP, hello tipo stesso indirizzo nel campo hello per IP iniziale e IP finale.</span><span class="sxs-lookup"><span data-stu-id="57954-121">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="57954-122">Apertura firewall hello consente di utenti e amministratori di database di tooany toologin su hello PostgreSQL server toowhich disporre di credenziali valide.</span><span class="sxs-lookup"><span data-stu-id="57954-122">Opening hello firewall enables administrators and users toologin tooany database on hello PostgreSQL server toowhich they have valid credentials.</span></span>

  ![<span data-ttu-id="57954-123">Portale di Azure: regole del firewall</span><span class="sxs-lookup"><span data-stu-id="57954-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="57954-124">Fare clic su **salvare** su hello toosave barra degli strumenti la regola del firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="57954-124">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="57954-125">Attendere la conferma hello hello regole del firewall toohello aggiornamento ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="57954-125">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

  ![Portale di Azure: fare clic su Salva](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="57954-127">Gestire le regole firewall di livello server esistente tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="57954-127">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="57954-128">Ripetere le regole del firewall di hello passaggi toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="57954-128">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="57954-129">tooadd hello correnti del computer, fare clic su pulsante hello troppo + **Aggiungi IP My**.</span><span class="sxs-lookup"><span data-stu-id="57954-129">tooadd hello current computer, click hello button too+ **Add My IP**.</span></span> <span data-ttu-id="57954-130">Fare clic su **salvare** modifiche hello toosave.</span><span class="sxs-lookup"><span data-stu-id="57954-130">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="57954-131">indirizzi IP aggiuntivi tooadd, digitare hello regola nome, indirizzo IP iniziale e l'indirizzo IP finale.</span><span class="sxs-lookup"><span data-stu-id="57954-131">tooadd additional IP addresses, type in hello Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="57954-132">Fare clic su **salvare** modifiche hello toosave.</span><span class="sxs-lookup"><span data-stu-id="57954-132">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="57954-133">toomodify una regola esistente, fare clic su uno dei campi di hello nella regola hello e modificare.</span><span class="sxs-lookup"><span data-stu-id="57954-133">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span> <span data-ttu-id="57954-134">Fare clic su **salvare** modifiche hello toosave.</span><span class="sxs-lookup"><span data-stu-id="57954-134">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="57954-135">toodelete una regola esistente, fare clic sui puntini di sospensione hello […] e fare clic su Rimuovi Elimina regola di hello.</span><span class="sxs-lookup"><span data-stu-id="57954-135">toodelete an existing rule, click hello ellipsis […] and click Delete remove hello rule.</span></span> <span data-ttu-id="57954-136">Fare clic su **salvare** modifiche hello toosave.</span><span class="sxs-lookup"><span data-stu-id="57954-136">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57954-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="57954-137">Next steps</span></span>
- <span data-ttu-id="57954-138">Analogamente, è possibile generare script troppo[creare e gestire i Database di Azure per le regole firewall PostgreSQL mediante Azure CLI](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="57954-138">Similarly, you can script too[Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="57954-139">Per informazioni sulla connessione tooan Database di Azure per server PostgreSQL, vedere [raccolte di connessioni per il Database di Azure per PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="57954-139">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
