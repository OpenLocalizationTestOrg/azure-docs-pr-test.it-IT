---
title: Anteprima della risoluzione dei problemi di Microsoft Power BI Embedded
description: Anteprima della risoluzione dei problemi di Microsoft Power BI Embedded
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: c8aee652-ed8b-4c66-9c63-f798b7a655b4
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: f406d23e578acc825514aa5bd9eabcbf160bf9ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="5218e-103">Anteprima della risoluzione dei problemi di Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="5218e-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="5218e-104">Questo articolo fornisce alcune risposte per la risoluzione dei problemi di **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="5218e-104">This article provides answers for how  to troubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="5218e-105">Impostare le stringhe di connessione di SQL Server</span><span class="sxs-lookup"><span data-stu-id="5218e-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="5218e-106">Per impostare una stringa di connessione di SQL Server, è necessario seguire un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="5218e-106">To set a SQL Server connecting string, you need to follow a specific format.</span></span> <span data-ttu-id="5218e-107">Di seguito viene specificata una stringa di connessione di esempio per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5218e-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="5218e-108">Per altre informazioni sulle stringhe di connessione di SQL Server, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="5218e-108">To learn more about SQL Server connection strings, see the following articles:</span></span>

* [<span data-ttu-id="5218e-109">Stringhe di connessione di SQL Server</span><span class="sxs-lookup"><span data-stu-id="5218e-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="5218e-110">Proprietà SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="5218e-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="5218e-111">Impostazione delle credenziali</span><span class="sxs-lookup"><span data-stu-id="5218e-111">Setting credentials</span></span>
<span data-ttu-id="5218e-112">Nel caso in cui si abbiano credenziali per un ambiente di sviluppo o di gestione temporanea, ad esempio nome utente e password, potrebbe essere necessario aggiornare le credenziali che corrispondono a una soluzione di produzione.</span><span class="sxs-lookup"><span data-stu-id="5218e-112">In the case where you have credentials for a development or staging environment, such as user name and password, you might need to update credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="5218e-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5218e-113">See Also</span></span>
* [<span data-ttu-id="5218e-114">Esempio introduttivo</span><span class="sxs-lookup"><span data-stu-id="5218e-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="5218e-115">Informazioni su Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="5218e-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

