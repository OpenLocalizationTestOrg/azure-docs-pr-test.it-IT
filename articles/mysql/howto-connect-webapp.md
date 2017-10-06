---
title: aaaConnect tooAzure di servizio App di Azure esistente del Database per MySQL | Documenti Microsoft
description: "Istruzioni per la modalità di connessione un tooAzure di servizio App di Azure esistente Database tooproperly per MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a><span data-ttu-id="efa57-103">Connettersi a un servizio App di Azure tooAzure Database esistente per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="efa57-103">Connect an existing Azure App Service tooAzure Database for MySQL server</span></span>
<span data-ttu-id="efa57-104">Questo documento viene illustrato come Database di Azure tooconnect un tooyour di servizio App di Azure esistente per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="efa57-104">This document explains how tooconnect an existing Azure App Service tooyour Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="efa57-105">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="efa57-105">Before you begin</span></span>
<span data-ttu-id="efa57-106">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="efa57-106">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="efa57-107">Creare un database di Azure per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="efa57-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="efa57-108">Per informazioni dettagliate, vedere troppo[come toocreate del Database per il server MySQL dal portale di Azure](quickstart-create-mysql-server-database-using-azure-portal.md) o [come toocreate Azure Database per il server di MySQL con CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="efa57-108">For details, refer too[How toocreate Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How toocreate Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="efa57-109">Attualmente sono disponibili due soluzioni tooenable di accesso da un Database di Azure di tooan di servizio App di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="efa57-109">Currently there are two solutions tooenable access from an Azure App Service tooan Azure Database for MySQL.</span></span> <span data-ttu-id="efa57-110">Entrambe le soluzioni implicano la configurazione di regole firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="efa57-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a><span data-ttu-id="efa57-111">Soluzione 1 - creare un tooallow regola firewall di tutti gli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="efa57-111">Solution 1 - Create a firewall rule tooallow all IPs</span></span>
<span data-ttu-id="efa57-112">Il Database di Azure per MySQL offre la sicurezza di accesso usando un tooprotect firewall i dati.</span><span class="sxs-lookup"><span data-stu-id="efa57-112">Azure Database for MySQL provides access security using a firewall tooprotect your data.</span></span> <span data-ttu-id="efa57-113">Quando la connessione da un Database di tooAzure servizio App di Azure per il server MySQL, tenere presente che hello in uscita, gli indirizzi IP di servizio App sono dinamico in natura.</span><span class="sxs-lookup"><span data-stu-id="efa57-113">When connecting from an Azure App Service tooAzure Database for MySQL server, keep in mind that hello outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="efa57-114">disponibilità di hello tooensure del servizio App di Azure, è consigliabile utilizzare questo tooallow soluzione tutti gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="efa57-114">tooensure hello availability of your Azure App Service, we recommend using this solution tooallow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="efa57-115">Microsoft sta lavorando per un tooavoid soluzione a lungo termine consentendo tutti gli indirizzi IP per servizi di Azure tooconnect tooAzure Database MySQL.</span><span class="sxs-lookup"><span data-stu-id="efa57-115">Microsoft is working for a long-term solution tooavoid allowing all IPs for Azure services tooconnect tooAzure Database for MySQL.</span></span>

1. <span data-ttu-id="efa57-116">Nel Pannello di server MySQL hello, in impostazioni fare clic su **sicurezza della connessione** tooopen hello sicurezza della connessione pannello hello Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="efa57-116">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Portale di Azure: fare clic su Sicurezza connessione](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="efa57-118">Compilare i campi **NOME REGOLA**, **INDIRIZZO IP INIZIALE** e **INDIRIZZO IP FINALE**.</span><span class="sxs-lookup"><span data-stu-id="efa57-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="efa57-119">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="efa57-119">Then click **Save**.</span></span>
   - <span data-ttu-id="efa57-120">Nome regola: Allow-All-IPs</span><span class="sxs-lookup"><span data-stu-id="efa57-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="efa57-121">Indirizzo IP iniziale: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="efa57-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="efa57-122">Indirizzo IP finale: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="efa57-122">End IP: 255.255.255.255</span></span>

   ![Portale di Azure - Aggiungere tutti gli indirizzi IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a><span data-ttu-id="efa57-124">Soluzione 2: creare un firewall tooexplicitly regola consentire gli indirizzi IP in uscita</span><span class="sxs-lookup"><span data-stu-id="efa57-124">Solution 2 - Create a firewall rule tooexplicitly allow outbound IPs</span></span>
<span data-ttu-id="efa57-125">È possibile aggiungere in modo esplicito che tutti hello gli indirizzi IP in uscita del servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="efa57-125">You can explicitly add all hello outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="efa57-126">Nel Pannello proprietà del servizio App hello, visualizzare il **indirizzo IP in uscita**.</span><span class="sxs-lookup"><span data-stu-id="efa57-126">On hello App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Portale di Azure - Visualizzare gli indirizzi IP in uscita](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="efa57-128">Nel Pannello di sicurezza di connessione MySQL hello, aggiungere indirizzi IP in uscita, uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="efa57-128">On hello MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Portale di Azure - Aggiungere indirizzi IP in modo esplicito](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="efa57-130">Ricordare troppo**salvare** regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="efa57-130">Remember too**Save** your firewall rules.</span></span>

<span data-ttu-id="efa57-131">Anche se hello servizio App di Azure tenta costante di indirizzi IP tookeep nel tempo, vi sono casi in cui è possano modificare gli indirizzi IP hello.</span><span class="sxs-lookup"><span data-stu-id="efa57-131">Though hello Azure App service attempts tookeep IP addresses constant over time, there are cases where hello IP addresses may change.</span></span> <span data-ttu-id="efa57-132">Ad esempio, quando hello ricicli app si verifica un'operazione di scala o quando vengono aggiunti nuovi computer in Azure dati internazionali centri capacità hello tooincrease.</span><span class="sxs-lookup"><span data-stu-id="efa57-132">For example, when hello app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers tooincrease hello capacity.</span></span> <span data-ttu-id="efa57-133">Quando si modifica indirizzi IP hello app hello potrebbe subire tempi di inattività in caso di hello non può più connettersi toohello MySQL server.</span><span class="sxs-lookup"><span data-stu-id="efa57-133">When hello IP addresses change, hello app could experience downtime in hello event it can no longer connect toohello MySQL server.</span></span> <span data-ttu-id="efa57-134">Quando si sceglie una delle soluzioni precedenti hello, prendere in considerazione questo potenziale.</span><span class="sxs-lookup"><span data-stu-id="efa57-134">Consider this potential when choosing one of hello preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="efa57-135">Configurazione SSL</span><span class="sxs-lookup"><span data-stu-id="efa57-135">SSL configuration</span></span>
<span data-ttu-id="efa57-136">Il database di Azure per MySQL ha abilitato SSL per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="efa57-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="efa57-137">Se l'applicazione non utilizza SSL tooconnect toohello database, è necessario toodisable SSL sul server MySQL.</span><span class="sxs-lookup"><span data-stu-id="efa57-137">If your application is not using SSL tooconnect toohello database, then you need toodisable SSL on MySQL server.</span></span> <span data-ttu-id="efa57-138">Per informazioni dettagliate su come tooconfigure SSL, vedere [utilizzando SSL con il Database di Azure per MySQL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="efa57-138">For details on how tooconfigure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="efa57-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="efa57-139">Next steps</span></span>
<span data-ttu-id="efa57-140">Per ulteriori informazioni sulle stringhe di connessione, fare riferimento troppo[le stringhe di connessione](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="efa57-140">For more information about connection strings, refer too[Connection Strings](howto-connection-string.md).</span></span>
