---
title: Creare e gestire regole del firewall per Database di Azure per PostgreSQL usando il portale di Azure | Microsoft Docs
description: Creare e gestire regole del firewall per Database di Azure per PostgreSQL usando il portale di Azure
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 20ac1392949a6f604e68d984cb50273b61051037
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="77f0b-103">Creare e gestire regole del firewall per Database di Azure per PostgreSQL usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="77f0b-103">Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="77f0b-104">Le regole del firewall a livello di server consentono agli amministratori di accedere a un server di Database di Azure per PostgreSQL da un indirizzo IP specificato o da un intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="77f0b-104">Server-level firewall rules enable administrators to access an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="77f0b-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="77f0b-105">Prerequisites</span></span>
<span data-ttu-id="77f0b-106">Per proseguire con questa guida, si richiedono:</span><span class="sxs-lookup"><span data-stu-id="77f0b-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="77f0b-107">Un server [Creare un database di Azure per PostgreSQL](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="77f0b-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="77f0b-108">Creare una regola del firewall a livello di server nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="77f0b-108">Create a server-level firewall rule in the Azure portal</span></span>
1. <span data-ttu-id="77f0b-109">Nell'intestazione Impostazioni del pannello del server PostgreSQL fare clic su **Sicurezza connessione** per aprire il pannello Sicurezza connessione per il database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="77f0b-109">On the PostgreSQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for PostgreSQL.</span></span>

  ![Portale di Azure: fare clic su Sicurezza connessione](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="77f0b-111">Fare clic su **Aggiungi indirizzo IP corrente** sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="77f0b-111">Click **Add My IP** on the toolbar.</span></span> <span data-ttu-id="77f0b-112">Verrà creata automaticamente una regola con l'indirizzo IP del computer rilevato dal sistema Azure.</span><span class="sxs-lookup"><span data-stu-id="77f0b-112">This will create a rule automatically with the IP address of your computer, as perceived by the Azure system.</span></span>

  ![Portale di Azure: fare clic su Aggiungi indirizzo IP corrente](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="77f0b-114">Verificare l'indirizzo IP prima di salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="77f0b-114">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="77f0b-115">In alcuni casi, l'indirizzo IP individuato dal portale di Azure è diverso da quello usato per l'accesso a Internet e ai server Azure,</span><span class="sxs-lookup"><span data-stu-id="77f0b-115">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="77f0b-116">quindi potrebbe essere necessario modificare l'indirizzo IP iniziale e l'indirizzo IP finale per fare in modo che la regola funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="77f0b-116">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>
<span data-ttu-id="77f0b-117">Usare un motore di ricerca o un altro strumento online per controllare l'indirizzo IP (ad esempio, la ricerca Bing di "what is my IP").</span><span class="sxs-lookup"><span data-stu-id="77f0b-117">Use a search engine or other online tool to check your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Ricerca Bing di What is my IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="77f0b-119">Aggiungere altri intervalli di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="77f0b-119">Add additional address ranges.</span></span> <span data-ttu-id="77f0b-120">Nelle regole per il firewall di Database di Azure per PostgreSQL è possibile specificare un solo indirizzo IP o un intervallo di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="77f0b-120">In the rules for the Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="77f0b-121">Per limitare la regola a un solo indirizzo IP, digitare lo stesso indirizzo nei campi Indirizzo IP iniziale e Indirizzo IP finale.</span><span class="sxs-lookup"><span data-stu-id="77f0b-121">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="77f0b-122">L'apertura del firewall consente agli amministratori e agli utenti di accedere a qualsiasi database nel server PostgreSQL per cui hanno credenziali valide.</span><span class="sxs-lookup"><span data-stu-id="77f0b-122">Opening the firewall enables administrators and users to login to any database on the PostgreSQL server to which they have valid credentials.</span></span>

  ![<span data-ttu-id="77f0b-123">Portale di Azure: regole del firewall</span><span class="sxs-lookup"><span data-stu-id="77f0b-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="77f0b-124">Fare clic su **Salva** sulla barra degli strumenti per salvare questa regola del firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="77f0b-124">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="77f0b-125">Attendere la conferma che l'aggiornamento delle regole del firewall abbia avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="77f0b-125">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

  ![Portale di Azure: fare clic su Salva](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="77f0b-127">Gestione delle regole del firewall a livello di server esistenti tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="77f0b-127">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="77f0b-128">Ripetere i passaggi per gestire le regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="77f0b-128">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="77f0b-129">Per aggiungere il computer corrente, fare clic sul pulsante + **Aggiungi indirizzo IP corrente**.</span><span class="sxs-lookup"><span data-stu-id="77f0b-129">To add the current computer, click the button to + **Add My IP**.</span></span> <span data-ttu-id="77f0b-130">È consigliabile fare clic su **Salva** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="77f0b-130">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="77f0b-131">Per aggiungere ulteriori indirizzi IP, digitare nome della regola, indirizzo IP iniziale e indirizzo IP finale.</span><span class="sxs-lookup"><span data-stu-id="77f0b-131">To add additional IP addresses, type in the Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="77f0b-132">È consigliabile fare clic su **Salva** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="77f0b-132">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="77f0b-133">Per modificare una regola esistente, fare clic su uno dei campi nella regola e modificare.</span><span class="sxs-lookup"><span data-stu-id="77f0b-133">To modify an existing rule, click any of the fields in the rule and modify.</span></span> <span data-ttu-id="77f0b-134">È consigliabile fare clic su **Salva** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="77f0b-134">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="77f0b-135">Per eliminare una regola esistente, fare clic sui puntini di sospensione […] e fare clic su Elimina per rimuovere la regola.</span><span class="sxs-lookup"><span data-stu-id="77f0b-135">To delete an existing rule, click the ellipsis […] and click Delete remove the rule.</span></span> <span data-ttu-id="77f0b-136">È consigliabile fare clic su **Salva** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="77f0b-136">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77f0b-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77f0b-137">Next steps</span></span>
- <span data-ttu-id="77f0b-138">Analogamente, è possibile generare uno script per [creare e gestire le regole del firewall per Database di Azure per PostgreSQL usando l'interfaccia della riga di comando di Azure](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="77f0b-138">Similarly, you can script to [Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="77f0b-139">Per informazioni sulla connessione a un'istanza di Database di Azure per il server PostgreSQL, vedere [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md) (Raccolte di connessioni per Database di Azure per PostgreSQL)</span><span class="sxs-lookup"><span data-stu-id="77f0b-139">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
