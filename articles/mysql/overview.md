---
title: aaaOverview del Database di Azure per il servizio di database relazionale di MySQL | Documenti Microsoft
description: Panoramica di hello Azure Database per il servizio di database relazionale di MySQL.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 08/02/2017
ms.custom: mvc
ms.openlocfilehash: f02493e2c3c38ccab408a718f98861600481812d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-mysql-service-introduction"></a>Database di Azure per MySQL: introduzione al servizio
Il Database di Azure per MySQL è un servizio di database relazionale in hello cloud Microsoft in base a [MySQL Community Edition](https://www.mysql.com/products/community/) motore di database.  Database di Azure per MySQL offre:

- Prestazioni prevedibili a più livelli di servizio
- Scalabilità dinamica senza tempi di inattività dell'applicazione
- Disponibilità elevata predefinita
- Protezione dati

Queste funzionalità richiedono pochissima amministrazione e sono disponibili senza costi aggiuntivi. Esse consentono toofocus sullo sviluppo rapido di app e accelerare il tempo toomarket, invece di allocare il tempo e risorse toomanaging le macchine virtuali e l'infrastruttura. Inoltre, è possibile continuare toodevelop aprire Strumenti di origine e la piattaforma di propria scelta, l'applicazione hello e recapitare con velocità di hello e l'efficienza di esigenze aziendali senza dover toolearn nuove competenze.

![Diagramma concettuale di Azure Database for MySQL](media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

Questo articolo è tooAzure un'introduzione Database MySQL i concetti e funzionalità correlate tooperformance, scalabilità e gestibilità, con dettagli tooexplore collegamenti. Vedere che le guide introduttive tooget che è stato avviato:
- [Create an Azure Database for MySQL server using Azure portal](quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)
- [Create an Azure Database for MySQL server using Azure CLI](quickstart-create-mysql-server-database-using-azure-cli.md) (Creare un database di Azure per il server MySQL usando l'interfaccia della riga di comando di Azure)

Per un set di esempi dell'interfaccia della riga di comando di Azure, vedere:
- [Azure CLI samples for Azure Database for MySQL](sample-scripts-azure-cli.md) (Esempi di interfaccia della riga di comando di Azure per Database di Azure per MySQL)

## <a name="adjust-performance-and-scale-without-downtime"></a>Regolare le prestazioni e scalabilità senza tempi di inattività
Il servizio Database di Azure per MySQL offre due livelli di servizio: Basic e Standard. Ogni livello offre prestazioni differenti e i carichi di lavoro di funzionalità toosupport tooheavyweight lightweight database. È possibile compilare la prima app in un database di piccole dimensioni per alcuni dollari un mese, quindi modifica la tooscale del livello di servizio con necessita della soluzione senza tempi di inattività. La scalabilità dinamica consente la toorapidly di rispondere tootransparently database variazioni dei requisiti di risorse. Si paga solo per le risorse di hello che è necessario, quando necessario.

## <a name="monitoring-and-alerting"></a>Monitoraggio e avviso
Come è possibile sapere a destra fare clic su Arresta hello quando ci si connette su e giù? Utilizzare il monitoraggio delle prestazioni predefinite hello e caratteristiche, combinati con le valutazioni delle prestazioni hello in base a unità di calcolo di avviso. Utilizzo di queste funzionalità consentono di valutare rapidamente impatto hello di ridimensionamento verso l'alto o verso il basso in base a corrente o progetto esigenze di prestazioni. Per informazioni dettagliate, vedere [Concepts: Service tiers](concepts-service-tiers.md) (Concetti: livelli di servizio).

## <a name="keep-your-app-and-business-running"></a>Mantenere l'applicazione e l’esecuzione dell’azienda
Il Contratto di servizio per la disponibilità del 99,99% leader del settore di Azure, fornito da una rete globale di datacenter gestiti da Microsoft, consente di mantenere l'applicazione in esecuzione 24 ore su 24, 7 giorni su 7. Con ogni Database di Azure per il server MySQL, ora usufruire della protezione incorporata, la tolleranza di errore e la protezione dei dati che altrimenti sarebbe toobuy o struttura, creare e gestire. Con il Database di Azure per MySQL, è possibile utilizzare in fase di punto di ripristino toorecover tooan un server di stato in precedenza, fino alla versione di 35 giorni.

## <a name="secure-your-data"></a>Protezione dei dati
I servizi di database di Azure vantano una tradizione di sicurezza dei dati rispettata anche da Database di Azure per MySQL con funzionalità che limitano l'accesso, proteggono i dati inattivi e in transito e consentono di monitorare l'attività. Visitare hello [Azure Trust Center](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) per informazioni sulla sicurezza della piattaforma di Azure.

Hello Azure Database per il servizio MySQL utilizza la crittografia di archiviazione per dati in altre. Dati, incluso il backup, vengono crittografati su disco (con l'eccezione di hello di file temporanei creati dal motore hello durante l'esecuzione di query). servizio Hello Usa crittografia AES 256 bit in cui è incluso nella crittografia di archiviazione di Azure e le chiavi di hello sono gestito dal sistema. La crittografia di archiviazione è sempre attiva e non può essere disabilitata.

Per impostazione predefinita, hello Azure Database per il servizio MySQL è configurato toorequire [sicurezza della connessione SSL](./concepts-ssl-connection-security.md) per dati in movimento attraverso la rete hello. Le connessioni SSL tra il server di database e applicazioni client di imposizione consente di proteggere da attacchi "man in intermedio hello" crittografando il flusso di dati hello tra server hello e l'applicazione.  Facoltativamente, è possibile disabilitare richiedere SSL per la connessione del servizio di database tooyour se l'applicazione client non supporta la connettività SSL.

## <a name="next-steps"></a>Passaggi successivi
Lettura di un Database di tooAzure introduzione per MySQL e ha risposto hello domanda "Qual è il Database di Azure per MySQL?", si è pronti per:
- Vedere hello pagina per i confronti di costo e calcolatori dei prezzi. [Prezzi](https://azure.microsoft.com/pricing/details/mysql/)
- Per iniziare, creare il primo server. [Create an Azure Database for MySQL server using Azure portal](quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)
- Creazione della prima applicazione Python, PHP, Ruby, C\#, Java, Node.js: [tooconnect tooAzure Database di utilizzare le librerie di connettività per MySQL](concepts-connection-libraries.md)
