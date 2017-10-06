---
title: aaaCreate e gestire i Database di Azure per le regole firewall di MySQL mediante hello portale di Azure | Documenti Microsoft
description: Creare e gestire i Database di Azure per le regole firewall di MySQL mediante hello portale di Azure
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="63cf5-103">Creare e gestire i Database di Azure per le regole firewall di MySQL mediante hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="63cf5-103">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="63cf5-104">Le regole del firewall a livello di server abilitare tooaccess agli amministratori un Database di Azure per il MySQL Server da un indirizzo IP specifico o l'intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="63cf5-104">Server-level firewall rules enable administrators tooaccess an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="63cf5-105">Creare una regola del firewall a livello di server nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="63cf5-105">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="63cf5-106">Nel Pannello di server MySQL hello, in impostazioni fare clic su **sicurezza della connessione** tooopen hello sicurezza della connessione pannello hello Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="63cf5-106">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Portale di Azure: fare clic su Sicurezza connessione](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="63cf5-108">Fare clic su **Aggiungi IP My** nella barra degli strumenti di hello toocreate una regola con indirizzo IP di hello del computer, in base alla percezione hello sistema Azure.</span><span class="sxs-lookup"><span data-stu-id="63cf5-108">Click **Add My IP** on hello toolbar toocreate a rule with hello IP address of your computer, as perceived by hello Azure system.</span></span>

   ![Portale di Azure: fare clic su Aggiungi indirizzo IP corrente](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="63cf5-110">Verificare l'indirizzo IP prima di salvare la configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="63cf5-110">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="63cf5-111">In alcune situazioni, l'indirizzo IP hello osservato dal portale di Azure è diverso dall'indirizzo IP hello utilizzato quando l'accesso a hello internet e i server Azure.</span><span class="sxs-lookup"><span data-stu-id="63cf5-111">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="63cf5-112">Di conseguenza, potrebbe essere necessario toochange IP iniziale e finale IP toomake hello regola funzione hello come previsto.</span><span class="sxs-lookup"><span data-stu-id="63cf5-112">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>

   <span data-ttu-id="63cf5-113">Utilizzare un motore di ricerca o altri toocheck strumento online il proprio indirizzo IP (ad esempio, cercare "Qual è l'indirizzo IP").</span><span class="sxs-lookup"><span data-stu-id="63cf5-113">Use a search engine or other online tool toocheck your own IP address (for example, search "what is my IP address").</span></span>

   ![Ricerca del proprio indirizzo IP in Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="63cf5-115">Aggiungere altri intervalli di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="63cf5-115">Add additional address ranges.</span></span> <span data-ttu-id="63cf5-116">Nelle regole di hello per hello Azure Database MySQL firewall, è possibile specificare un singolo indirizzo IP o un intervallo di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="63cf5-116">In hello rules for hello Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="63cf5-117">Se si desidera toolimit hello regola tooone singolo indirizzo IP, hello tipo stesso indirizzo nel campo hello per IP iniziale e IP finale.</span><span class="sxs-lookup"><span data-stu-id="63cf5-117">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="63cf5-118">Apertura firewall hello consente tooaccess amministratori e utenti di qualsiasi database hello toowhich di server MySQL disporre di credenziali valide.</span><span class="sxs-lookup"><span data-stu-id="63cf5-118">Opening hello firewall enables administrators and users tooaccess any database on hello MySQL server toowhich they have valid credentials.</span></span>

   ![<span data-ttu-id="63cf5-119">Portale di Azure: regole del firewall</span><span class="sxs-lookup"><span data-stu-id="63cf5-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="63cf5-120">Fare clic su **salvare** su hello toosave barra degli strumenti la regola del firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="63cf5-120">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="63cf5-121">Attendere la conferma hello hello regole del firewall toohello aggiornamento ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="63cf5-121">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

   ![Portale di Azure: fare clic su Salva](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="63cf5-123">Gestire le regole firewall di livello server esistente tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="63cf5-123">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="63cf5-124">Ripetere le regole del firewall di hello passaggi toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="63cf5-124">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="63cf5-125">tooadd hello correnti del computer, fare clic su **+ Aggiungi IP My**.</span><span class="sxs-lookup"><span data-stu-id="63cf5-125">tooadd hello current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="63cf5-126">indirizzi IP aggiuntivi tooadd, digitare hello **nome regola**, **IP iniziale**, e **IP finale**.</span><span class="sxs-lookup"><span data-stu-id="63cf5-126">tooadd additional IP addresses, type in hello **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="63cf5-127">toomodify una regola esistente, fare clic su uno dei campi di hello nella regola hello e modificare.</span><span class="sxs-lookup"><span data-stu-id="63cf5-127">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span>
* <span data-ttu-id="63cf5-128">regola toodelete esistente, fare clic sui puntini di sospensione hello […] e scegliere **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="63cf5-128">toodelete an existing rule, click hello ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="63cf5-129">Fare clic su **salvare** modifiche hello toosave.</span><span class="sxs-lookup"><span data-stu-id="63cf5-129">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63cf5-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="63cf5-130">Next steps</span></span>
- <span data-ttu-id="63cf5-131">Per informazioni sulla connessione tooan Database di Azure per il server MySQL, vedere [raccolte di connessioni per il Database di Azure per MySQL](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="63cf5-131">For help in connecting tooan Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
