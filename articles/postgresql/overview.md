---
title: aaaOverview del Database di Azure per il servizio di database relazionale PostgreSQL | Documenti Microsoft
description: Offre una panoramica del servizio di database relazionale Database di Azure per PostgreSQL.
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: overview
ms.date: 08/01/2017
ms.openlocfilehash: fd6821b56e5295b8b341d87b14d113f7a4b247c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-postgresql"></a>Che cos'è Database di Azure per PostgreSQL

Il Database di Azure per PostgreSQL è un servizio di database relazionale in hello compilato per gli sviluppatori basati sulla versione community hello di open source di Microsoft cloud [PostgreSQL](https://www.postgresql.org/) motore di database. Questo servizio è disponibile in anteprima pubblica. Database di Azure per PostgreSQL offre:
- Prestazioni prevedibili a più livelli di servizio
- Scalabilità dinamica senza tempi di inattività dell'applicazione
- Disponibilità elevata predefinita
- Protezione dati

Tutte le funzionalità richiedono pochissima amministrazione e sono disponibili senza costi aggiuntivi. Queste funzionalità consentono di toofocus in sviluppo rapido di applicazioni e accelerare il tempo toomarket, invece di allocare il tempo e risorse toomanaging le macchine virtuali e l'infrastruttura. Inoltre, è possibile continuare toodevelop aprire Strumenti di origine e la piattaforma di propria scelta, l'applicazione hello e recapitare con velocità di hello e l'efficienza di esigenze aziendali senza dover toolearn nuove competenze. 

Questo articolo è tooAzure un'introduzione Database PostgreSQL i concetti e funzionalità correlate tooperformance, scalabilità e gestibilità. Vedere che le guide introduttive tooget che è stato avviato:

- [Creare un database di Azure per PostgreSQL usando il portale di Azure](quickstart-create-server-database-portal.md)
- [Creare un Database di Azure per PostgreSQL utilizzando hello CLI di Azure](quickstart-create-server-database-azure-cli.md)

Per un set di esempi dell'interfaccia della riga di comando di Azure e di PowerShell, vedere:

- [Azure CLI samples for Azure Database for PostgreSQL](./sample-scripts-azure-cli.md) (Esempi di interfaccia della riga di comando di Azure per Database di Azure per PostgreSQL)

## <a name="adjust-performance-and-scale-without-downtime"></a>Regolare le prestazioni e scalabilità senza tempi di inattività

Il servizio Database di Azure per PostgreSQL offre attualmente due livelli di servizio: Basic e Standard. Ogni livello di servizio offre [diversi livelli di prestazioni, le garanzie di IOPS e funzionalità](concepts-service-tiers.md) carichi di lavoro database toosupport tooheavyweight lightweight. È possibile compilare la prima app in un server di piccole dimensioni per soldi qualche mese, quindi [modificare il livello di prestazioni hello](scripts/sample-scale-server-up-or-down.md) all'interno del servizio livello manualmente o a livello di eventuali esigenze di hello toomeet ora della soluzione. È possibile farlo senza applicazione tooyour tempi di inattività o i clienti tooyour. Consente la scalabilità dinamica tootransparently il database rispondere toorapidly la modifica di requisiti di risorse e attiva tooonly si paga per risorse hello che è necessario quando necessario.

## <a name="monitoring-and-alerting"></a>Monitoraggio e avviso
Come è possibile stabilire quando toodial su e giù? Utilizzare il monitoraggio delle prestazioni predefinite hello e caratteristiche, combinati con le valutazioni delle prestazioni hello in base alle unità di calcolo di avviso. Utilizzando questi strumenti consentono di valutare rapidamente impatto hello dell'aumento delle unità di calcolo di o verso il basso in base alle proprie esigenze di prestazioni corrente o previsto. Per informazioni dettagliate, vedere [Azure Database for PostgreSQL options and performance: Understand what's available in each service tier](./concepts-service-tiers.md) (Opzioni e prestazioni disponibili in ogni livello di servizio di Database di Azure per PostgreSQL).

## <a name="keep-your-app-and-business-running"></a>Mantenere l'applicazione e l’esecuzione dell’azienda
Il Contratto di servizio per la disponibilità del 99,99% (non disponibile in anteprima) leader del settore di Azure, fornito da una rete globale di datacenter gestiti da Microsoft, consente di mantenere l'applicazione in esecuzione 24 ore su 24, 7 giorni su 7. Con ogni Database di Azure per server PostgreSQL, ora usufruire della protezione incorporata, la tolleranza di errore e la protezione dei dati che altrimenti sarebbe toobuy o struttura, creare e gestire. Con il Database di Azure per PostgreSQL, ogni livello di servizio offre un set completo di funzionalità di continuità aziendale e le opzioni che è possibile utilizzare tooget e in esecuzione e rimane in questo modo. È possibile utilizzare [in fase di punto di ripristino](howto-restore-server-portal.md) tooreturn tooan un database di stato in precedenza, fino alla versione di 35 giorni. Inoltre, se il Data Center hello che ospita i database di cui si verifichi un'interruzione, è possibile ripristinare i database dalle copie con ridondanza geografica dei recenti backup.

## <a name="secure-your-data"></a>Protezione dei dati
I servizi di database di Azure vantano una tradizione di sicurezza dei dati rispettata anche da Database di Azure per PostgreSQL con funzionalità che limitano l'accesso, proteggono i dati inattivi e in transito e consentono di monitorare l'attività. Visitare hello [Azure Trust Center](https://www.microsoft.com/TrustCenter/Security/default.aspx) per informazioni sulla sicurezza della piattaforma di Azure.

Hello Azure Database PostgreSQL servizio utilizza la crittografia di archiviazione per dati in altre. Compresi i backup di dati vengono crittografati su disco (con l'eccezione di hello di file temporanei creati dal motore hello durante l'esecuzione di query). servizio Hello Usa crittografia AES 256 bit in cui è incluso nella crittografia di archiviazione di Azure e le chiavi di hello sono gestito dal sistema. La crittografia di archiviazione è sempre attiva e non può essere disabilitata.

Per impostazione predefinita, hello Azure Database PostgreSQL servizio è configurato toorequire [sicurezza della connessione SSL](./concepts-ssl-connection-security.md) per dati in movimento attraverso la rete hello. Le connessioni SSL tra il server di database e applicazioni client di imposizione consente di proteggere da attacchi "man in intermedio hello" crittografando il flusso di dati hello tra server hello e l'applicazione.  Facoltativamente, è possibile disabilitare richiedere SSL per la connessione del servizio di database tooyour se l'applicazione client non supporta la connettività SSL.

## <a name="next-steps"></a>Passaggi successivi
- Vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/postgresql/) per confronti di costo e strumenti di calcolo.
- Per iniziare, [creare il primo database di Azure per PostgreSQL tramite](./quickstart-create-server-database-portal.md).
- Compilare la prima app in Python, PHP, Ruby, C\#, Java, Node.js: [raccolte di connessioni](./concepts-connection-libraries.md)
