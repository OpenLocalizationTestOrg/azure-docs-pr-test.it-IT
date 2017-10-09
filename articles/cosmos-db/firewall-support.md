---
title: controllo di accesso IP e il supporto di firewall Cosmos DB aaaAzure | Documenti Microsoft
description: Informazioni su come criteri di controllo di accesso toouse IP per firewall il supporto per gli account di database di Azure Cosmos DB.
keywords: controllo di accesso IP, supporto del firewall
services: cosmos-db
author: shahankur11
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: c1b9ede0-ed93-411a-ac9a-62c113a8e887
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ankshah
ms.openlocfilehash: b5cdbdb28e9d7ee0fd0ea54aad277167b699929f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-firewall-support"></a>Supporto del firewall di Azure Cosmos DB
toosecure dati archiviati in un account di database di Azure Cosmos DB, Cosmos Azure DB ha fornito il supporto per una chiave privata in base [modello di autorizzazione](https://msdn.microsoft.com/library/azure/dn783368.aspx) che usa un codice di autenticazione di messaggi basato su Hash complessa (HMAC). A questo punto, inoltre segreto toohello basato sul modello di autorizzazione, Azure Cosmos DB supporta criteri basati sui controlli di accesso basato su IP per il supporto firewall in ingresso. Questo modello è molto simile toohello regole del firewall di un sistema di database tradizionale e fornisce un ulteriore livello di sicurezza toohello Azure Cosmos DB account del database. Con questo modello, è possibile ora configurare un toobe account database Azure Cosmos DB accessibile solo da un set di computer approvati e/o i servizi cloud. Accedere alle risorse di DB Cosmos tooAzure da questi set di servizi e macchine approvati richiede comunque hello chiamante toopresent un token di autorizzazione valido.

## <a name="ip-access-control-overview"></a>Panoramica del controllo di accesso IP
Per impostazione predefinita, un account di database DB Cosmos Azure è accessibile da internet pubblico, purché hello richiesta è accompagnata da un token di autorizzazione valido. controllo di accesso basata su criteri IP tooconfigure, utente hello deve specificare il set di hello di indirizzi IP o intervalli di indirizzi IP in toobe formato CIDR inclusa come hello consentito l'elenco di IP client per un account di database specificato. Una volta applicata questa configurazione, tutte le richieste provenienti da computer di fuori di questo elenco consentito verranno bloccate dal server hello.  connessione Hello l'elaborazione del flusso di controllo di accesso basato su IP hello è descritto nel seguente diagramma hello.

![Diagramma che illustra il processo di connessione hello per il controllo di accesso basato su IP](./media/firewall-support/firewall-support-flow.png)

## <a name="connections-from-cloud-services"></a>Connessioni da servizi cloud
In Azure, i servizi cloud sono uno strumento molto comune per ospitare la logica del servizio di livello intermedio con Azure Cosmos DB. tooenable accesso tooan Azure Cosmos DB account del database da un servizio cloud, indirizzo IP pubblico hello del servizio cloud hello deve essere aggiunto toohello consentito l'elenco di indirizzi IP associati all'account di database di Azure Cosmos DB da [configurazione criteri di controllo di accesso IP Hello](#configure-ip-policy).  In questo modo si garantisce che tutte le istanze del ruolo di servizi cloud hanno accesso tooyour Azure Cosmos DB account del database. È possibile recuperare gli indirizzi IP per i servizi cloud nel portale di Azure hello, come illustrato nella seguente schermata hello.

![Schermata di indirizzo IP pubblico hello per un servizio cloud nel portale di Azure hello](./media/firewall-support/public-ip-addresses.png)

Quando scala in orizzontale il servizio cloud aggiungendo istanze del ruolo aggiuntivi, tali nuove istanze avranno automaticamente accesso account del database Azure Cosmos DB toohello poiché sono parte di hello stesso servizio cloud.

## <a name="connections-from-virtual-machines"></a>Connessioni da macchine virtuali
[Macchine virtuali](https://azure.microsoft.com/services/virtual-machines/) o [set di scalabilità di macchine virtuali](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) può anche essere toohost utilizzati servizi di livello intermedio tramite Azure Cosmos DB.  tooconfigure hello Azure Cosmos DB accesso tooallow account al database da macchine virtuali, gli indirizzi IP pubblici di macchina virtuale e/o set di scalabilità della macchina virtuale deve essere configurato come uno degli indirizzi IP per l'account di database di Azure Cosmos DB da consentiti hello [configurazione dei criteri di controllo di accesso IP hello](#configure-ip-policy). È possibile recuperare gli indirizzi IP per le macchine virtuali in hello portale di Azure, come illustrato nella seguente schermata hello.

![Screenshot che illustra un indirizzo IP pubblico per una macchina virtuale visualizzata nel portale di Azure hello](./media/firewall-support/public-ip-addresses-dns.png)

Quando si aggiunge il gruppo di toohello istanze di macchina virtuale aggiuntiva, vengono fornite automaticamente account di accesso tooyour Azure Cosmos DB del database.

## <a name="connections-from-hello-internet"></a>Le connessioni da hello internet
Quando l'accesso di un database di Azure Cosmos account da un computer del database su hello internet, hello indirizzo IP del client o l'intervallo di indirizzi IP della macchina hello deve essere aggiunto toohello elenco degli indirizzi IP per l'account del database Azure Cosmos DB hello consentito. 

## <a id="configure-ip-policy"></a>Configurazione dei criteri di controllo di accesso IP hello
criteri di controllo di accesso IP Hello possono essere impostati nel portale di Azure hello o a livello di programmazione tramite [CLI di Azure](cli-samples.md), [Azure Powershell](powershell-samples.md), o hello [API REST](/rest/api/documentdb/) aggiornando hello `ipRangeFilter` proprietà. Gli intervalli di indirizzi IP o i singoli indirizzi IP devono essere delimitati da virgole e non devono contenere spazi. Esempio: "13.91.6.132,13.91.6.1/24". Quando si aggiorna l'account del database tramite questi metodi, toopopulate assicurarsi di essere tutti di hello proprietà tooprevent toodefault reimpostazione.

> [!NOTE]
> Abilita un criterio di controllo di accesso IP per l'account di database di Azure Cosmos DB, tutti accesso tooyour account database DB Cosmos Azure dal computer esterni hello configurato consentito elenco di intervalli di indirizzi IP sono bloccati. In virtù di questo modello, esplorazione l'operazione di hello dati piano dal portale hello anche sarà bloccato tooensure hello integrità del controllo di accesso.

sviluppo toosimplify, hello portale di Azure consente di identificare e aggiungere IP hello del toohello macchina client consentito elenco, in modo che le applicazioni in esecuzione nel computer possono accedere hello account Azure Cosmos DB. Si noti che viene rilevato hello indirizzo IP del client qui indicato dal portale di hello. È possibile indirizzo IP del client hello del computer, ma è anche possibile indirizzo IP di hello del gateway di rete. Non dimenticare tooremove prima tooproduction continua.

tooset criteri di controllo di accesso IP a hello in hello portale di Azure, passare a pannello di account Azure Cosmos DB toohello, fare clic su **Firewall** nel menu di navigazione hello, quindi fare clic su **ON** 

![Screenshot che illustra come tooopen hello pannello Firewall in hello portale di Azure](./media/firewall-support/azure-portal-firewall.png)

Nel riquadro nuova hello, specificare se hello portale di Azure può accedere l'account di hello, aggiungere altri indirizzi e intervalli come appropriato, quindi fare clic su **salvare**.  

> [!NOTE]
> Quando si abilita un criterio di controllo di accesso IP, è necessario l'indirizzo IP hello tooadd per hello accesso toomaintain portale Azure. gli indirizzi IP portali Hello sono:
> |Region|Indirizzo IP|
> |------|----------|
> |Tutte le aree a eccezione di quelle specificate di seguito| 104.42.195.92|
> |Germania|51.4.229.218|
> |Cina|139.217.8.252|
> |Governo degli Stati Uniti - Arizona|52.244.48.71|
>

![Screenshot che illustra come impostazioni del firewall tooconfigure in hello portale di Azure](./media/firewall-support/azure-portal-firewall-configure.png)

## <a name="troubleshooting-hello-ip-access-control-policy"></a>Risoluzione dei problemi di criteri di controllo di accesso IP hello
### <a name="portal-operations"></a>Operazioni nel portale
Abilita un criterio di controllo di accesso IP per l'account di database di Azure Cosmos DB, tutti accesso tooyour account database DB Cosmos Azure dal computer esterni hello configurato consentito elenco di intervalli di indirizzi IP sono bloccati. Pertanto, se si desidera operazioni piano dei dati portale tooenable quali raccolte e query nei documenti di esplorazione, è necessario tooexplicitly consentire l'accesso al portale Azure utilizzando hello **Firewall** pannello nel portale di hello. 

![Screenshot che illustra come tooenable accesso toohello portale di Azure](./media/firewall-support/azure-portal-access-firewall.png)

### <a name="sdk--rest-api"></a>SDK e API REST
Per motivi di sicurezza, l'accesso tramite SDK o l'API REST da computer non in elenco consentiti hello restituirà un generico 404 non trovato risposta con nessun ulteriore dettaglio. Verificare che Hello IP consentito elenco configurato per la configurazione dei criteri corretti di Azure Cosmos DB database account tooensure hello è applicato tooyour Azure Cosmos DB account del database.

## <a name="next-steps"></a>Passaggi successivi
Per suggerimenti relativi alle prestazioni di rete, vedere [Suggerimenti sulle prestazioni per DocumentDB](performance-tips.md).

