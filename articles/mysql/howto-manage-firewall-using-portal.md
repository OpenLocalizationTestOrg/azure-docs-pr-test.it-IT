---
title: Creare e gestire le regole del firewall di Database di Azure per MySQL con il portale di Azure | Microsoft Docs
description: Creare e gestire le regole del firewall di Database di Azure per MySQL con il portale di Azure
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 33198e5a6e11df2db3a17fc96a0b3cd4b1a284e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="d6640-103">Creare e gestire le regole del firewall di Database di Azure per MySQL con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d6640-103">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="d6640-104">Le regole del firewall a livello di server consentono agli amministratori di accedere a un server di Database di Azure per MySQL da un indirizzo IP specificato o da un intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="d6640-104">Server-level firewall rules enable administrators to access an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="d6640-105">Creare una regola del firewall a livello di server nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d6640-105">Create a server-level firewall rule in the Azure portal</span></span>

1. <span data-ttu-id="d6640-106">Nel pannello del server MySQL fare clic su **Sicurezza connessione** sotto l'intestazione Impostazioni per aprire il pannello Sicurezza connessione per Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="d6640-106">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Portale di Azure: fare clic su Sicurezza connessione](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="d6640-108">Fare clic su **Aggiungi indirizzo IP corrente** sulla barra degli strumenti per creare una regola con l'indirizzo IP del computer rilevato dal sistema Azure.</span><span class="sxs-lookup"><span data-stu-id="d6640-108">Click **Add My IP** on the toolbar to create a rule with the IP address of your computer, as perceived by the Azure system.</span></span>

   ![Portale di Azure: fare clic su Aggiungi indirizzo IP corrente](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="d6640-110">Verificare l'indirizzo IP prima di salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="d6640-110">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="d6640-111">In alcuni casi, l'indirizzo IP individuato dal portale di Azure è diverso da quello usato per l'accesso a Internet e ai server Azure,</span><span class="sxs-lookup"><span data-stu-id="d6640-111">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="d6640-112">quindi potrebbe essere necessario modificare l'indirizzo IP iniziale e l'indirizzo IP finale per fare in modo che la regola funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="d6640-112">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>

   <span data-ttu-id="d6640-113">Usare un motore di ricerca o un altro strumento online per controllare il proprio indirizzo IP (ad esempio, cercare "what is my IP").</span><span class="sxs-lookup"><span data-stu-id="d6640-113">Use a search engine or other online tool to check your own IP address (for example, search "what is my IP address").</span></span>

   ![Ricerca del proprio indirizzo IP in Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="d6640-115">Aggiungere altri intervalli di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="d6640-115">Add additional address ranges.</span></span> <span data-ttu-id="d6640-116">Nelle regole per il firewall di Database di Azure per MySQL è possibile specificare un singolo indirizzo IP o un intervallo di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="d6640-116">In the rules for the Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="d6640-117">Per limitare la regola a un solo indirizzo IP, digitare lo stesso indirizzo nei campi Indirizzo IP iniziale e Indirizzo IP finale.</span><span class="sxs-lookup"><span data-stu-id="d6640-117">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="d6640-118">L'apertura del firewall consente agli amministratori e agli utenti di accedere a qualsiasi database del server MySQL per cui hanno credenziali valide.</span><span class="sxs-lookup"><span data-stu-id="d6640-118">Opening the firewall enables administrators and users to access any database on the MySQL server to which they have valid credentials.</span></span>

   ![<span data-ttu-id="d6640-119">Portale di Azure: regole del firewall</span><span class="sxs-lookup"><span data-stu-id="d6640-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="d6640-120">Fare clic su **Salva** sulla barra degli strumenti per salvare questa regola del firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="d6640-120">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="d6640-121">Attendere la conferma che l'aggiornamento delle regole del firewall abbia avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="d6640-121">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

   ![Portale di Azure: fare clic su Salva](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="d6640-123">Gestione delle regole del firewall a livello di server esistenti tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d6640-123">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="d6640-124">Ripetere i passaggi per gestire le regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="d6640-124">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="d6640-125">Per aggiungere il computer corrente, fare clic su **+ Aggiungi indirizzo IP corrente**.</span><span class="sxs-lookup"><span data-stu-id="d6640-125">To add the current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="d6640-126">Per aggiungere altri indirizzi IP, digitare **NOME REGOLA**, **INDIRIZZO IP INIZIALE** e **INDIRIZZO IP FINALE**.</span><span class="sxs-lookup"><span data-stu-id="d6640-126">To add additional IP addresses, type in the **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="d6640-127">Per modificare una regola esistente, fare clic su uno dei campi nella regola e modificare.</span><span class="sxs-lookup"><span data-stu-id="d6640-127">To modify an existing rule, click any of the fields in the rule and modify.</span></span>
* <span data-ttu-id="d6640-128">Per eliminare una regola esistente, fare clic sui puntini di sospensione (…) e quindi su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="d6640-128">To delete an existing rule, click the ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="d6640-129">È consigliabile fare clic su **Salva** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d6640-129">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6640-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d6640-130">Next steps</span></span>
- <span data-ttu-id="d6640-131">Per informazioni sulla connessione a un server di Database di Azure per MySQL, vedere [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md) (Raccolte di connessioni per Database di Azure per MySQL)</span><span class="sxs-lookup"><span data-stu-id="d6640-131">For help in connecting to an Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
