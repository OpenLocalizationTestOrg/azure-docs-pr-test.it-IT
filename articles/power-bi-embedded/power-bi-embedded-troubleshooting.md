---
title: risoluzione dei problemi di Power BI Preview incorporato aaaMicrosoft
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
ms.openlocfilehash: a0a25cd73977c0ea0bd6b7c82e215412245771bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="75b90-103">Anteprima della risoluzione dei problemi di Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="75b90-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="75b90-104">In questo articolo vengono fornite le risposte per informazioni su come tootroubleshoot **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="75b90-104">This article provides answers for how  tootroubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="75b90-105">Impostare le stringhe di connessione di SQL Server</span><span class="sxs-lookup"><span data-stu-id="75b90-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="75b90-106">tooset una stringa di connessione di SQL Server, è necessario toofollow un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="75b90-106">tooset a SQL Server connecting string, you need toofollow a specific format.</span></span> <span data-ttu-id="75b90-107">Di seguito viene specificata una stringa di connessione di esempio per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="75b90-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="75b90-108">toolearn più sulle stringhe di connessione SQL Server, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="75b90-108">toolearn more about SQL Server connection strings, see hello following articles:</span></span>

* [<span data-ttu-id="75b90-109">Stringhe di connessione di SQL Server</span><span class="sxs-lookup"><span data-stu-id="75b90-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="75b90-110">Proprietà SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="75b90-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="75b90-111">Impostazione delle credenziali</span><span class="sxs-lookup"><span data-stu-id="75b90-111">Setting credentials</span></span>
<span data-ttu-id="75b90-112">In caso di hello in cui si dispone di credenziali per un ambiente di sviluppo o gestione temporanea, ad esempio nome utente e password, potrebbe essere necessario tooupdate credenziali che corrispondono a una soluzione di produzione.</span><span class="sxs-lookup"><span data-stu-id="75b90-112">In hello case where you have credentials for a development or staging environment, such as user name and password, you might need tooupdate credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="75b90-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="75b90-113">See Also</span></span>
* [<span data-ttu-id="75b90-114">Esempio introduttivo</span><span class="sxs-lookup"><span data-stu-id="75b90-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="75b90-115">Informazioni su Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="75b90-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

