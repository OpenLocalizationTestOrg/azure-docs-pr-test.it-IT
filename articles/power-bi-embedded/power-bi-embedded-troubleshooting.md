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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Anteprima della risoluzione dei problemi di Microsoft Power BI Embedded
In questo articolo vengono fornite le risposte per informazioni su come tootroubleshoot **Power BI Embedded**.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>Impostare le stringhe di connessione di SQL Server
tooset una stringa di connessione di SQL Server, è necessario toofollow un formato specifico. Di seguito viene specificata una stringa di connessione di esempio per SQL Server.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

toolearn più sulle stringhe di connessione SQL Server, vedere hello seguenti articoli:

* [Stringhe di connessione di SQL Server](https://msdn.microsoft.com/library/jj653752.aspx)
* [Proprietà SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>Impostazione delle credenziali
In caso di hello in cui si dispone di credenziali per un ambiente di sviluppo o gestione temporanea, ad esempio nome utente e password, potrebbe essere necessario tooupdate credenziali che corrispondono a una soluzione di produzione.

## <a name="see-also"></a>Vedere anche
* [Esempio introduttivo](power-bi-embedded-get-started-sample.md)
* [Informazioni su Power BI Embedded](power-bi-embedded-what-is-power-bi-embedded.md)

