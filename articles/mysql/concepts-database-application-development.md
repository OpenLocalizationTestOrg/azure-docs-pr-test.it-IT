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
# <a name="application-development-overview-for-azure-database-for-mysql"></a>Panoramica dello sviluppo di applicazioni per il database di Azure per MySQL 
In questo articolo verranno illustrate alcune considerazioni di progettazione che uno sviluppatore deve seguire quando si scrivono applicazioni codice tooconnect tooAzure Database MySQL 

> [!TIP]
> Per visualizzare un'esercitazione si come toocreate un server, creare un firewall basato su server, consente di visualizzare le proprietà del server, creare database, connettersi ed eseguire query utilizzando l'area di lavoro e mysql.exe, vedere [progetta il primo database di MySQL di Azure](tutorial-design-database-using-portal.md)

## <a name="language-and-platform"></a>Linguaggio e piattaforma
Sono disponibili esempi di codice per svariati linguaggi di programmazione e piattaforme. È possibile trovare esempi di codice toohello in collegamenti: [tooconnect tooAzure Database di utilizzare le librerie di connettività per MySQL](concepts-connection-libraries.md)

## <a name="tools"></a>Strumenti
Il Database di Azure per MySQL Usa hello MySQL community versione, compatibile con strumenti di gestione comuni di MySQL come area di lavoro o MySQL utilità, ad esempio mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)e altri. È inoltre possibile utilizzare hello portale di Azure, Azure CLI e toointeract API REST con il servizio di database hello.

## <a name="resource-limitations"></a>Limiti delle risorse
MySQL Database Azure gestisce hello risorse disponibili tooa server tramite due meccanismi diversi: 
- Governance delle risorse 
- Imposizione di limiti.

## <a name="security"></a>Sicurezza
Il database MySQL di Azure fornisce risorse per limitare l'accesso, proteggere i dati, configurare gli utenti e i ruoli e monitorare le attività in un database MySQL.

## <a name="authentication"></a>Autenticazione
Il database MySQL di Azure supporta l'autenticazione server degli utenti e degli accessi.

## <a name="resiliency"></a>Resilienza
Quando un errore temporaneo si verifica durante la connessione tooMySQL Database, il codice deve ripetere chiamata hello. È consigliabile utilizzare logica di ripetizione hello Backoff logica, in modo che non sovraccarica hello Database SQL con più client contemporaneamente con nuovo tentativo in corso.

- Esempi di codice: per gli esempi di codice che illustrano la logica di riesecuzione, vedere gli esempi per la lingua di hello di propria scelta nel: [tooconnect tooAzure Database di utilizzare le librerie di connettività per MySQL](concepts-connection-libraries.md)

## <a name="managing-connections"></a>Gestione delle connessioni
Le connessioni di database sono una risorsa limitata, pertanto si consiglia di utilizzare ragionevoli di connessioni durante l'accesso del MySQL Database tooachieve ottenere prestazioni migliori.
- Database di Access hello utilizzando il pool di connessioni o connessioni permanenti.
- Database di Access hello tramite una connessione di breve durata. 
- Utilizzare logica di ripetizione tentativi nell'applicazione in un momento hello del tentativo di connessione hello, toocatch errori a causa di connessioni tooconcurrent stato raggiunto il massimo di hello consentito. La logica di riesecuzione in hello, impostare un breve ritardo e quindi attendere un tempo casuale prima di tentativi di connessione aggiuntive hello.
