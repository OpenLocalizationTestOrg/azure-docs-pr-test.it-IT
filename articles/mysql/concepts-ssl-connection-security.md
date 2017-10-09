---
title: "connettività aaaSSL per il Database di Azure per MySQL | Documenti Microsoft"
description: Informazioni per la configurazione di Database di Azure per MySQL e le applicazioni associate tooproperly utilizzare connessioni SSL
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6fca7c88fc0f1fd6058d68fcff90fd409abd97a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a>Connettività SSL nel Database di Azure per MySQL
Il Database di Azure per MySQL supporta la connessione di database tooclient applicazioni server usando Secure Sockets Layer (SSL). Le connessioni SSL tra il server di database e applicazioni client di imposizione consente di proteggere da attacchi "man in intermedio hello" crittografando il flusso di dati hello tra server hello e l'applicazione.

## <a name="default-settings"></a>Impostazioni predefinite
Per impostazione predefinita, il servizio di database hello deve essere connessioni SSL configurato toorequire quando ci si connette tooMySQL.  È consigliabile evitare di disattivare l'opzione SSL di hello quando possibile. 

Durante il provisioning di un nuovo Database di Azure per il server MySQL tramite hello portale di Azure e CLI, l'applicazione di connessioni SSL è abilitato per impostazione predefinita. 

Allo stesso modo, le stringhe di connessione predefinite nelle impostazioni di "Stringhe di connessione" hello del server di hello portale di Azure includono parametri hello necessario per il server database tooyour tooconnect linguaggi comuni mediante SSL. Hello parametro SSL varia in base al connettore hello, ad esempio "ssl = true" o "sslmode = richiedono" o "sslmode = obbligatorio" e altre varianti.

toolearn come tooenable o disabilitare connessione SSL durante lo sviluppo di applicazioni, consultare troppo[come tooconfigure SSL](howto-configure-ssl.md).

## <a name="next-steps"></a>Passaggi successivi
[Raccolte connessioni per il Database di Azure per MySQL](concepts-connection-libraries.md)
