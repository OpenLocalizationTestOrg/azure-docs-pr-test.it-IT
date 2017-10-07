---
title: Cenni preliminari sullo sviluppo di applicazioni aaaDatabase per il Database di Azure per MySQL | Documenti Microsoft
description: Introduce le considerazioni di progettazione uno sviluppatore deve seguire quando si scrivono applicazioni codice tooconnect tooAzure Database MySQL
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="7b43d-103">Panoramica dello sviluppo di applicazioni per il database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="7b43d-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="7b43d-104">In questo articolo verranno illustrate alcune considerazioni di progettazione che uno sviluppatore deve seguire quando si scrivono applicazioni codice tooconnect tooAzure Database MySQL</span><span class="sxs-lookup"><span data-stu-id="7b43d-104">This article discusses design considerations that a developer should follow when writing application code tooconnect tooAzure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="7b43d-105">Per visualizzare un'esercitazione si come toocreate un server, creare un firewall basato su server, consente di visualizzare le proprietà del server, creare database, connettersi ed eseguire query utilizzando l'area di lavoro e mysql.exe, vedere [progetta il primo database di MySQL di Azure](tutorial-design-database-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7b43d-105">For a tutorial showing you how toocreate a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="7b43d-106">Linguaggio e piattaforma</span><span class="sxs-lookup"><span data-stu-id="7b43d-106">Language and platform</span></span>
<span data-ttu-id="7b43d-107">Sono disponibili esempi di codice per svariati linguaggi di programmazione e piattaforme.</span><span class="sxs-lookup"><span data-stu-id="7b43d-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="7b43d-108">È possibile trovare esempi di codice toohello in collegamenti: [tooconnect tooAzure Database di utilizzare le librerie di connettività per MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="7b43d-108">You can find links toohello code samples at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="7b43d-109">Strumenti</span><span class="sxs-lookup"><span data-stu-id="7b43d-109">Tools</span></span>
<span data-ttu-id="7b43d-110">Il Database di Azure per MySQL Usa hello MySQL community versione, compatibile con strumenti di gestione comuni di MySQL come area di lavoro o MySQL utilità, ad esempio mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)e altri.</span><span class="sxs-lookup"><span data-stu-id="7b43d-110">Azure Database for MySQL uses hello MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="7b43d-111">È inoltre possibile utilizzare hello portale di Azure, Azure CLI e toointeract API REST con il servizio di database hello.</span><span class="sxs-lookup"><span data-stu-id="7b43d-111">You can also use hello Azure portal, Azure CLI, and REST APIs toointeract with hello database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="7b43d-112">Limiti delle risorse</span><span class="sxs-lookup"><span data-stu-id="7b43d-112">Resource limitations</span></span>
<span data-ttu-id="7b43d-113">MySQL Database Azure gestisce hello risorse disponibili tooa server tramite due meccanismi diversi:</span><span class="sxs-lookup"><span data-stu-id="7b43d-113">Azure MySQL Database manages hello resources available tooa server using two different mechanisms:</span></span> 
- <span data-ttu-id="7b43d-114">Governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="7b43d-114">Resources Governance</span></span> 
- <span data-ttu-id="7b43d-115">Imposizione di limiti.</span><span class="sxs-lookup"><span data-stu-id="7b43d-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="7b43d-116">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="7b43d-116">Security</span></span>
<span data-ttu-id="7b43d-117">Il database MySQL di Azure fornisce risorse per limitare l'accesso, proteggere i dati, configurare gli utenti e i ruoli e monitorare le attività in un database MySQL.</span><span class="sxs-lookup"><span data-stu-id="7b43d-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="7b43d-118">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="7b43d-118">Authentication</span></span>
<span data-ttu-id="7b43d-119">Il database MySQL di Azure supporta l'autenticazione server degli utenti e degli accessi.</span><span class="sxs-lookup"><span data-stu-id="7b43d-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="7b43d-120">Resilienza</span><span class="sxs-lookup"><span data-stu-id="7b43d-120">Resiliency</span></span>
<span data-ttu-id="7b43d-121">Quando un errore temporaneo si verifica durante la connessione tooMySQL Database, il codice deve ripetere chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="7b43d-121">When a transient error occurs while connecting tooMySQL Database, your code should retry hello call.</span></span> <span data-ttu-id="7b43d-122">È consigliabile utilizzare logica di ripetizione hello Backoff logica, in modo che non sovraccarica hello Database SQL con più client contemporaneamente con nuovo tentativo in corso.</span><span class="sxs-lookup"><span data-stu-id="7b43d-122">We recommend hello retry logic use back off logic, so that it does not overwhelm hello SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="7b43d-123">Esempi di codice: per gli esempi di codice che illustrano la logica di riesecuzione, vedere gli esempi per la lingua di hello di propria scelta nel: [tooconnect tooAzure Database di utilizzare le librerie di connettività per MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="7b43d-123">Code samples: For code samples that illustrate retry logic, see samples for hello language of your choice at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="7b43d-124">Gestione delle connessioni</span><span class="sxs-lookup"><span data-stu-id="7b43d-124">Managing Connections</span></span>
<span data-ttu-id="7b43d-125">Le connessioni di database sono una risorsa limitata, pertanto si consiglia di utilizzare ragionevoli di connessioni durante l'accesso del MySQL Database tooachieve ottenere prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="7b43d-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database tooachieve better performance.</span></span>
- <span data-ttu-id="7b43d-126">Database di Access hello utilizzando il pool di connessioni o connessioni permanenti.</span><span class="sxs-lookup"><span data-stu-id="7b43d-126">Access hello database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="7b43d-127">Database di Access hello tramite una connessione di breve durata.</span><span class="sxs-lookup"><span data-stu-id="7b43d-127">Access hello database by using short connection life span.</span></span> 
- <span data-ttu-id="7b43d-128">Utilizzare logica di ripetizione tentativi nell'applicazione in un momento hello del tentativo di connessione hello, toocatch errori a causa di connessioni tooconcurrent stato raggiunto il massimo di hello consentito.</span><span class="sxs-lookup"><span data-stu-id="7b43d-128">Use retry logic in your application at hello point of hello connection attempt, toocatch failures due tooconcurrent connections have reached hello maximum allowed.</span></span> <span data-ttu-id="7b43d-129">La logica di riesecuzione in hello, impostare un breve ritardo e quindi attendere un tempo casuale prima di tentativi di connessione aggiuntive hello.</span><span class="sxs-lookup"><span data-stu-id="7b43d-129">In hello retry logic, set a short delay, and then wait for a random time before hello additional connection attempts.</span></span>
