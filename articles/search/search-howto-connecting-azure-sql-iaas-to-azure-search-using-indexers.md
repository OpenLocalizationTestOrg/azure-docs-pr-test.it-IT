---
title: aaaSQL VM connessione tooAzure ricerca | Documenti Microsoft
description: Abilitare connessioni crittografate e configurare hello firewall tooallow connessioni tooSQL Server in una macchina virtuale Azure (VM) da un indicizzatore in ricerca di Azure.
services: search
documentationcenter: 
author: HeidiSteen
manager: pablocas
editor: 
ms.assetid: 46e42e0e-c8de-4fec-b11a-ed132db7e7bc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: heidist
ms.openlocfilehash: 1f0db8a2812b0a7d012e58bb873c4b2b29fa1338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-connection-from-an-azure-search-indexer-toosql-server-on-an-azure-vm"></a>Configurare una connessione da un tooSQL indicizzatore di ricerca di Azure Server in una macchina virtuale di Azure
Come indicato nella [tooAzure connessione Database SQL di Azure esegue una ricerca usando gli indicizzatori](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md#faq), creazione indicizzatori contro **SQL Server in macchine virtuali di Azure** (o **macchine virtuali di Azure SQL** breve) è supportata dalla ricerca di Azure, ma esistono alcuni prerequisiti correlati alla sicurezza tootake cure prima. 

**Durata dell'attività:** circa 30 minuti, presupponendo che sia già installato un certificato in hello macchina virtuale.

## <a name="enable-encrypted-connections"></a>Abilitare le connessioni crittografate
Ricerca di Azure richiede un canale crittografato per tutte le richieste di indicizzatori su una connessione Internet pubblica. Questa sezione elenca hello passaggi toomake questo lavoro.

1. Controllare le proprietà di hello hello tooverify hello soggetto il nome del certificato è il nome di dominio completo hello (FQDN) di hello macchina virtuale di Azure. È possibile utilizzare uno strumento come CertUtils o hello le proprietà di hello tooview snap-in certificati. È possibile ottenere hello FQDN dalla sezione Essentials del Pannello di hello macchina virtuale del servizio, in hello **etichetta nome indirizzo IP pubblico/DNS** campo, hello [portale di Azure](https://portal.azure.com/).
   
   * Per le macchine virtuali create utilizzando più recente di hello **Gestione risorse** modello hello FQDN è formattato come `<your-VM-name>.<region>.cloudapp.azure.com`. 
   * Per macchine virtuali meno recenti create come un **classico** macchina virtuale, in formato FQDN hello `<your-cloud-service-name.cloudapp.net>`. 
2. Configurare SQL Server toouse hello certificato utilizzando hello Editor del Registro di sistema (regedit). 
   
    Anche se Gestione configurazione SQL Server viene usato spesso per questa attività, non è possibile usarlo per questo scenario. Poiché non ne trova hello certificato importato perché hello FQDN di hello macchina virtuale in Azure non corrisponde a hello FQDN come determinato da hello VM (identifichi hello dominio come computer locale hello o hello toowhich di dominio di rete che viene unita in join). Quando i nomi non corrispondono, utilizzare certificati di hello toospecify regedit.
   
   * In regedit passare chiave del Registro di sistema toothis: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\[MSSQL13.MSSQLSERVER]\MSSQLServer\SuperSocketNetLib\Certificate`.
     
     Hello `[MSSQL13.MSSQLSERVER]` parte varia in base alla versione e nome di istanza. 
   * Impostare il valore di hello di hello **certificato** toohello chiave **identificazione personale** del certificato SSL hello toohello VM è stato importato.
     
     Esistono diversi modi tooget hello identificazione digitale alcune prestazioni migliori rispetto ad altri utenti. Se li si copia da hello **certificati** snap-in MMC, è probabilmente selezionerà un carattere iniziale invisibile [come descritto in questo articolo del supporto tecnico](https://support.microsoft.com/kb/2023869/), che genera un errore quando si tenta un connessione. Esistono diverse soluzioni alternative per risolvere il problema. Hello più semplice è toobackspace su e quindi digitare di nuovo primo carattere di hello di hello identificazione personale tooremove hello carattere iniziale nel campo valore di chiave hello regedit. In alternativa, è possibile utilizzare un'identificazione digitale hello toocopy di uno strumento diverso.
3. Concedere le autorizzazioni toohello account del servizio. 
   
    Verificare che hello account del servizio SQL Server viene concessa l'autorizzazione appropriata per la chiave privata di hello del certificato SSL hello. Se si ignora questo passaggio, SQL Server non verrà avviato. È possibile utilizzare hello **certificati** snap-in o **CertUtils** per questa attività.
4. Riavviare il servizio di SQL Server hello.

## <a name="configure-sql-server-connectivity-in-hello-vm"></a>Configurare la connettività di SQL Server in VM hello
Dopo aver impostato la connessione crittografato hello richiesta dalla ricerca di Azure, esistono tooSQL intrinseco di passaggi di configurazione aggiuntive Server in macchine virtuali di Azure. Se non è già fatto, passaggio successivo hello è toofinish configurazione utilizzando uno di questi articoli:

* Per un **Gestione risorse** macchina virtuale, vedere [connessione macchina virtuale di SQL Server in Azure tramite Gestione risorse di tooa](../virtual-machines/windows/sql/virtual-machines-windows-sql-connect.md). 
* Per un **classico** macchina virtuale, vedere [connessione macchina virtuale di SQL Server in Azure classico tooa](../virtual-machines/windows/classic/sql-connect.md).

In particolare, nella sezione hello in ogni articolo per "connessione su hello internet".

## <a name="configure-hello-network-security-group-nsg"></a>Configurare hello gruppo di sicurezza (rete)
Non è insolito tooconfigure hello gruppo e l'endpoint di Azure corrispondente o elenco di controllo di accesso (ACL) toomake le parti accessibili tooother macchina virtuale di Azure. Probabilità sono di che fatto questo prima tooallow tooyour di tooconnect la propria logica dell'applicazione macchina virtuale di SQL Azure. Non è diversa per tooyour di connessione SQL Azure VM una ricerca di Azure. 

Hello collegamenti riportati di seguito forniscono istruzioni sulla configurazione di gruppo per distribuzioni di macchine Virtuali. Usare queste istruzioni che tooacl un endpoint di ricerca di Azure in base al relativo indirizzo IP.

> [!NOTE]
> Per informazioni, vedere [Che cos'è un gruppo di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)
> 
> 

* Per un **Gestione risorse** macchina virtuale, vedere [come toocreate NSGs per le distribuzioni di ARM](../virtual-network/virtual-networks-create-nsg-arm-pportal.md). 
* Per un **classico** macchina virtuale, vedere [come toocreate NSGs per le distribuzioni classica](../virtual-network/virtual-networks-create-nsg-classic-ps.md).

Gli indirizzi IP può causare alcuni problemi che possono essere facilmente superate se si è consapevoli del problema hello e soluzioni alternative potenziali. nelle restanti sezioni Hello forniscono suggerimenti per la gestione di problemi correlati tooIP indirizzi hello ACL.

#### <a name="restrict-access-toohello-search-service-ip-address"></a>Limitare l'indirizzo IP del servizio di accesso toohello ricerca
È consigliabile limitare l'indirizzo IP di toohello hello accesso del servizio di ricerca in hello ACL anziché eseguire le macchine virtuali di SQL Azure livello aprire tooany le richieste di connessione. È possibile scoprire hello IP indirizzo eseguendo il ping hello nome di dominio completo (ad esempio, `<your-search-service-name>.search.windows.net`) del servizio di ricerca.

#### <a name="managing-ip-address-fluctuations"></a>Gestire le fluttuazioni degli indirizzi IP
Se il servizio di ricerca ha un solo numero di unità di ricerca (ovvero, una replica e una partizione), l'indirizzo IP hello verrà modificata durante l'avvio del servizio di routine, invalidare un ACL con indirizzo IP del servizio di ricerca esistente.

Errore di connettività successive hello tooavoid unidirezionale è toouse più di una replica e una partizione in ricerca di Azure. In questo modo aumenta il costo di hello, ma anche risolto hello IP indirizzo. In Ricerca di Azure gli indirizzi IP non vengono modificati quando si ha più di un'unità di ricerca.

Un secondo approccio è tooallow hello connessione toofail e quindi riconfigurare hello ACL di NSG hello. In Media, è possibile prevedere toochange gli indirizzi IP ogni due settimane. Per i clienti che hanno controllato l'indicizzazione raramente, questo potrebbe essere un approccio valido.

Un terzo approccio possibile (ma non particolarmente sicuro) è l'intervallo di indirizzi IP hello toospecify di hello area in cui viene eseguito il provisioning del servizio di ricerca di Azure. elenco Hello intervalli IP da cui gli indirizzi IP pubblici tooAzure le risorse vengono allocati sia pubblicata nel [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/details.aspx?id=41653). 

#### <a name="include-hello-azure-search-portal-ip-addresses"></a>Includere gli indirizzi IP del portale di hello ricerca di Azure
Se si utilizza hello toocreate portale Azure un indicizzatore, logica del portale di ricerca di Azure deve inoltre tooyour accesso SQL Azure VM durante la fase di creazione. Gli indirizzi IP del portale di Ricerca di Azure sono reperibili eseguendo il ping di `stamp2.search.ext.azure.com`.

## <a name="next-steps"></a>Passaggi successivi
Con configurazione fuori modo hello, è ora possibile specificare un Server SQL nella macchina virtuale di Azure come origine dati hello per un indicizzatore di ricerca di Azure. Vedere [tooAzure connessione Database SQL di Azure esegue una ricerca usando gli indicizzatori](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) per ulteriori informazioni.

