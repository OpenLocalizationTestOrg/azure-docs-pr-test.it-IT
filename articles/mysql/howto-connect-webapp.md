---
title: Connessione del servizio app di Azure esistente al Database di Azure per MySQL | Microsoft Docs
description: Istruzioni su come connettere correttamente un servizio app di Azure esistente al Database di Azure per MySQL
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 735e21e8135d67405ec6b88d75be1711a2f071f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-an-existing-azure-app-service-to-azure-database-for-mysql-server"></a><span data-ttu-id="8b35d-103">Connessione di un servizio app di Azure esistente al Database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="8b35d-103">Connect an existing Azure App Service to Azure Database for MySQL server</span></span>
<span data-ttu-id="8b35d-104">Questo documento descrive come connettere un servizio app di Azure esistente al Database di Azure per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="8b35d-104">This document explains how to connect an existing Azure App Service to your Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8b35d-105">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="8b35d-105">Before you begin</span></span>
<span data-ttu-id="8b35d-106">Accedere al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8b35d-106">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8b35d-107">Creare un database di Azure per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="8b35d-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="8b35d-108">Per informazioni dettagliate, vedere [Come creare il database di Azure per il server MySQL dal portale](quickstart-create-mysql-server-database-using-azure-portal.md) o [Come creare il database di Azure per il server MySQL con l'interfaccia della riga di comando](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8b35d-108">For details, refer to [How to create Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How to create Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="8b35d-109">Attualmente sono disponibili due soluzioni per abilitare l'accesso dal servizio app di Azure a un database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="8b35d-109">Currently there are two solutions to enable access from an Azure App Service to an Azure Database for MySQL.</span></span> <span data-ttu-id="8b35d-110">Entrambe le soluzioni implicano la configurazione di regole firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="8b35d-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-to-allow-all-ips"></a><span data-ttu-id="8b35d-111">Soluzione 1: creare una regola del firewall per consentire tutti gli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="8b35d-111">Solution 1 - Create a firewall rule to allow all IPs</span></span>
<span data-ttu-id="8b35d-112">Il database di Azure per MySQL offre accesso alla sicurezza tramite un firewall per proteggere i dati.</span><span class="sxs-lookup"><span data-stu-id="8b35d-112">Azure Database for MySQL provides access security using a firewall to protect your data.</span></span> <span data-ttu-id="8b35d-113">Durante la connessione da un servizio app di Azure al database di Azure per il server MySQL, tenere presente che gli indirizzi IP in uscita del servizio app hanno una natura dinamica.</span><span class="sxs-lookup"><span data-stu-id="8b35d-113">When connecting from an Azure App Service to Azure Database for MySQL server, keep in mind that the outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="8b35d-114">Per garantire la disponibilità del servizio app di Azure, è consigliabile usare questa soluzione per consentire tutti gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="8b35d-114">To ensure the availability of your Azure App Service, we recommend using this solution to allow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="8b35d-115">Microsoft sta lavorando a una soluzione a lungo termine per evitare che tutti gli indirizzi IP consentano ai servizi di Azure di connettersi al database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="8b35d-115">Microsoft is working for a long-term solution to avoid allowing all IPs for Azure services to connect to Azure Database for MySQL.</span></span>

1. <span data-ttu-id="8b35d-116">Nel pannello del server MySQL fare clic su **Sicurezza connessione** sotto l'intestazione Impostazioni per aprire il pannello Sicurezza connessione per Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="8b35d-116">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Portale di Azure: fare clic su Sicurezza connessione](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="8b35d-118">Compilare i campi **NOME REGOLA**, **INDIRIZZO IP INIZIALE** e **INDIRIZZO IP FINALE**.</span><span class="sxs-lookup"><span data-stu-id="8b35d-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="8b35d-119">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8b35d-119">Then click **Save**.</span></span>
   - <span data-ttu-id="8b35d-120">Nome regola: Allow-All-IPs</span><span class="sxs-lookup"><span data-stu-id="8b35d-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="8b35d-121">Indirizzo IP iniziale: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="8b35d-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="8b35d-122">Indirizzo IP finale: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="8b35d-122">End IP: 255.255.255.255</span></span>

   ![Portale di Azure - Aggiungere tutti gli indirizzi IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-to-explicitly-allow-outbound-ips"></a><span data-ttu-id="8b35d-124">Soluzione 2: creare una regola del firewall per consentire in modo esplicito gli indirizzi IP in uscita</span><span class="sxs-lookup"><span data-stu-id="8b35d-124">Solution 2 - Create a firewall rule to explicitly allow outbound IPs</span></span>
<span data-ttu-id="8b35d-125">È possibile aggiungere in modo esplicito tutti gli IP in uscita del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b35d-125">You can explicitly add all the outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="8b35d-126">Nel pannello Proprietà del servizio app, visualizzare l'**INDIRIZZO IP IN USCITA**.</span><span class="sxs-lookup"><span data-stu-id="8b35d-126">On the App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Portale di Azure - Visualizzare gli indirizzi IP in uscita](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="8b35d-128">Nel pannello Sicurezza connessione di MySQL, aggiungere gli indirizzi IP in uscita uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="8b35d-128">On the MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Portale di Azure - Aggiungere indirizzi IP in modo esplicito](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="8b35d-130">Ricordarsi di **salvare** le regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="8b35d-130">Remember to **Save** your firewall rules.</span></span>

<span data-ttu-id="8b35d-131">Sebbene il servizio app di Azure tenti di mantenere gli indirizzi IP costanti nel tempo, vi sono casi in cui gli indirizzi IP possono cambiare.</span><span class="sxs-lookup"><span data-stu-id="8b35d-131">Though the Azure App service attempts to keep IP addresses constant over time, there are cases where the IP addresses may change.</span></span> <span data-ttu-id="8b35d-132">Ad esempio, quando l'app ricicla o si effettua un'operazione di ridimensionamento, oppure quando vengono aggiunti nuovi data center nell'area di Azure per aumentare la capacità.</span><span class="sxs-lookup"><span data-stu-id="8b35d-132">For example, when the app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers to increase the capacity.</span></span> <span data-ttu-id="8b35d-133">Quando gli indirizzi IP cambiano, l'app potrebbe subire tempi di inattività nel caso in cui non riesca a connettersi al server MySQL.</span><span class="sxs-lookup"><span data-stu-id="8b35d-133">When the IP addresses change, the app could experience downtime in the event it can no longer connect to the MySQL server.</span></span> <span data-ttu-id="8b35d-134">Considerare questa possibilità quando si sceglie una delle soluzioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="8b35d-134">Consider this potential when choosing one of the preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="8b35d-135">Configurazione SSL</span><span class="sxs-lookup"><span data-stu-id="8b35d-135">SSL configuration</span></span>
<span data-ttu-id="8b35d-136">Il database di Azure per MySQL ha abilitato SSL per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8b35d-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="8b35d-137">Se l'applicazione non usa SSL per la connessione al database, è necessario disabilitarlo sul server MySQL.</span><span class="sxs-lookup"><span data-stu-id="8b35d-137">If your application is not using SSL to connect to the database, then you need to disable SSL on MySQL server.</span></span> <span data-ttu-id="8b35d-138">Per informazioni dettagliate su come configurare SSL, vedere [Uso di SSL con il database di Azure per MySQL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="8b35d-138">For details on how to configure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b35d-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8b35d-139">Next steps</span></span>
<span data-ttu-id="8b35d-140">Per altre informazioni sulle stringhe di connessione, vedere l'argomento relativo alle [stringhe di connessione](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="8b35d-140">For more information about connection strings, refer to [Connection Strings](howto-connection-string.md).</span></span>
