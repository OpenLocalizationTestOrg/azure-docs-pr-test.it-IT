---
title: Panoramica dello sviluppo di applicazioni di database per il database di Azure per MySQL | Documentazione Microsoft
description: Introduce aspetti di progettazione che lo sviluppatore deve considerare quando scrive il codice dell'applicazione per la connessione al database di Azure per MySQL
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 350dd775e172120d806d1193877a34d94f4d3f6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="0f653-103">Panoramica dello sviluppo di applicazioni per il database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="0f653-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="0f653-104">Questo articolo tratta alcuni aspetti di progettazione che lo sviluppatore deve considerare quando scrive il codice dell'applicazione per la connessione al database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="0f653-104">This article discusses design considerations that a developer should follow when writing application code to connect to Azure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="0f653-105">Per un'esercitazione che mostra come creare un server, creare un firewall basato su server, visualizzare le proprietà del server, creare il database, connettersi ed eseguire query usando Workbench e mysql.exe, vedere [Design your first Azure MySQL database](tutorial-design-database-using-portal.md) (Progettare il primo database MySQL di Azure)</span><span class="sxs-lookup"><span data-stu-id="0f653-105">For a tutorial showing you how to create a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="0f653-106">Linguaggio e piattaforma</span><span class="sxs-lookup"><span data-stu-id="0f653-106">Language and platform</span></span>
<span data-ttu-id="0f653-107">Sono disponibili esempi di codice per svariati linguaggi di programmazione e piattaforme.</span><span class="sxs-lookup"><span data-stu-id="0f653-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="0f653-108">È possibile trovare collegamenti a esempi di codice in: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md) (Raccolte connessioni utilizzate per connettersi al database di Azure per MySQL)</span><span class="sxs-lookup"><span data-stu-id="0f653-108">You can find links to the code samples at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="0f653-109">Strumenti</span><span class="sxs-lookup"><span data-stu-id="0f653-109">Tools</span></span>
<span data-ttu-id="0f653-110">Il database di Azure per MySQL usa la versione community di MySQL, compatibile con comuni strumenti di gestione di MySQL quali Workbench o utilità di MySQL come mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql) e altre.</span><span class="sxs-lookup"><span data-stu-id="0f653-110">Azure Database for MySQL uses the MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="0f653-111">È possibile anche usare il portale di Azure, l'interfaccia della riga di comando di Azure e le API REST per interagire con il servizio di database.</span><span class="sxs-lookup"><span data-stu-id="0f653-111">You can also use the Azure portal, Azure CLI, and REST APIs to interact with the database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="0f653-112">Limiti delle risorse</span><span class="sxs-lookup"><span data-stu-id="0f653-112">Resource limitations</span></span>
<span data-ttu-id="0f653-113">Il database MySQL di Azure gestisce le risorse disponibili per un server usando due diversi meccanismi:</span><span class="sxs-lookup"><span data-stu-id="0f653-113">Azure MySQL Database manages the resources available to a server using two different mechanisms:</span></span> 
- <span data-ttu-id="0f653-114">Governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="0f653-114">Resources Governance</span></span> 
- <span data-ttu-id="0f653-115">Imposizione di limiti.</span><span class="sxs-lookup"><span data-stu-id="0f653-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="0f653-116">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="0f653-116">Security</span></span>
<span data-ttu-id="0f653-117">Il database MySQL di Azure fornisce risorse per limitare l'accesso, proteggere i dati, configurare gli utenti e i ruoli e monitorare le attività in un database MySQL.</span><span class="sxs-lookup"><span data-stu-id="0f653-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="0f653-118">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="0f653-118">Authentication</span></span>
<span data-ttu-id="0f653-119">Il database MySQL di Azure supporta l'autenticazione server degli utenti e degli accessi.</span><span class="sxs-lookup"><span data-stu-id="0f653-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="0f653-120">Resilienza</span><span class="sxs-lookup"><span data-stu-id="0f653-120">Resiliency</span></span>
<span data-ttu-id="0f653-121">Quando si verifica un errore temporaneo durante la connessione al database MySQL, il codice deve ripetere la chiamata.</span><span class="sxs-lookup"><span data-stu-id="0f653-121">When a transient error occurs while connecting to MySQL Database, your code should retry the call.</span></span> <span data-ttu-id="0f653-122">Per la ripetizione dei tentativi si consiglia di usare una logica backoff, in modo da non sovraccaricare il database SQL con più client che ripetono i tentativi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="0f653-122">We recommend the retry logic use back off logic, so that it does not overwhelm the SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="0f653-123">Esempi di codice: per alcuni esempi di codice che illustrano la logica di ripetizione dei tentativi, vedere gli esempi del linguaggio in uso in [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md) (Raccolte connessioni utilizzate per connettersi al database di Azure per MySQL)</span><span class="sxs-lookup"><span data-stu-id="0f653-123">Code samples: For code samples that illustrate retry logic, see samples for the language of your choice at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="0f653-124">Gestione delle connessioni</span><span class="sxs-lookup"><span data-stu-id="0f653-124">Managing Connections</span></span>
<span data-ttu-id="0f653-125">Le connessioni di database sono una risorsa limitata, pertanto si consiglia di usare in modo ragionevole le connessioni quando si accede al database MySQL per ottenere prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="0f653-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database to achieve better performance.</span></span>
- <span data-ttu-id="0f653-126">Accedere al database usando il pool di connessioni o connessioni permanenti.</span><span class="sxs-lookup"><span data-stu-id="0f653-126">Access the database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="0f653-127">Accedere al database tramite una connessione di breve durata.</span><span class="sxs-lookup"><span data-stu-id="0f653-127">Access the database by using short connection life span.</span></span> 
- <span data-ttu-id="0f653-128">Usare la logica di ripetizione tentativi nell'applicazione al momento del tentativo di connessione, per rilevare gli errori causati dal raggiungimento del massimo livello di connessioni simultanee consentito.</span><span class="sxs-lookup"><span data-stu-id="0f653-128">Use retry logic in your application at the point of the connection attempt, to catch failures due to concurrent connections have reached the maximum allowed.</span></span> <span data-ttu-id="0f653-129">Nella logica di ripetizione impostare un breve ritardo e quindi attendere un tempo casuale prima di eseguire altri tentativi di connessione.</span><span class="sxs-lookup"><span data-stu-id="0f653-129">In the retry logic, set a short delay, and then wait for a random time before the additional connection attempts.</span></span>