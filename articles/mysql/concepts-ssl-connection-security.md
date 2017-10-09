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
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="146be-103">Connettività SSL nel Database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="146be-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="146be-104">Il Database di Azure per MySQL supporta la connessione di database tooclient applicazioni server usando Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="146be-104">Azure Database for MySQL supports connecting your database server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="146be-105">Le connessioni SSL tra il server di database e applicazioni client di imposizione consente di proteggere da attacchi "man in intermedio hello" crittografando il flusso di dati hello tra server hello e l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="146be-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="146be-106">Impostazioni predefinite</span><span class="sxs-lookup"><span data-stu-id="146be-106">Default settings</span></span>
<span data-ttu-id="146be-107">Per impostazione predefinita, il servizio di database hello deve essere connessioni SSL configurato toorequire quando ci si connette tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="146be-107">By default, hello database service should be configured toorequire SSL connections when connecting tooMySQL.</span></span>  <span data-ttu-id="146be-108">È consigliabile evitare di disattivare l'opzione SSL di hello quando possibile.</span><span class="sxs-lookup"><span data-stu-id="146be-108">It is recommended avoid disabling hello SSL option whenever possible.</span></span> 

<span data-ttu-id="146be-109">Durante il provisioning di un nuovo Database di Azure per il server MySQL tramite hello portale di Azure e CLI, l'applicazione di connessioni SSL è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="146be-109">When provisioning a new Azure Database for MySQL server through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="146be-110">Allo stesso modo, le stringhe di connessione predefinite nelle impostazioni di "Stringhe di connessione" hello del server di hello portale di Azure includono parametri hello necessario per il server database tooyour tooconnect linguaggi comuni mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="146be-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="146be-111">Hello parametro SSL varia in base al connettore hello, ad esempio "ssl = true" o "sslmode = richiedono" o "sslmode = obbligatorio" e altre varianti.</span><span class="sxs-lookup"><span data-stu-id="146be-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="146be-112">toolearn come tooenable o disabilitare connessione SSL durante lo sviluppo di applicazioni, consultare troppo[come tooconfigure SSL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="146be-112">toolearn how tooenable or disable SSL connection when developing application, please refer too[How tooconfigure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="146be-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="146be-113">Next steps</span></span>
[<span data-ttu-id="146be-114">Raccolte connessioni per il Database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="146be-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
