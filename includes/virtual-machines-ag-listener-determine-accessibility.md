È importante toorealize che non esistono due modi tooconfigure un listener del gruppo di disponibilità in Azure. Hello modi diversi in tipo di hello di bilanciamento del carico di Azure che è usare quando si crea il listener hello. Hello nella tabella seguente vengono descritte le differenze di hello:

| Tipo di servizio di bilanciamento del carico | Implementazione | Usare questo tipo nei seguenti casi: |
| --- | --- | --- |
| **Esterno** |Usa hello *indirizzo IP virtuale pubblico* del servizio cloud hello che ospita macchine virtuali hello (VM). |È necessario listener hello tooaccess dalla rete virtuale esterna hello, compreso Internet hello. |
| **Interno** |Usa un *bilanciamento del carico interno* con un indirizzo privato per listener hello. |È possibile accedere hello listener solo all'interno di hello stessa rete virtuale. Questa modalità di accesso include la VPN da sito a sito in scenari ibridi. |

> [!IMPORTANT]
> Per un listener che utilizza hello VIP del servizio cloud pubblico (servizio di bilanciamento del carico esterno), purché hello client, il listener e i database si trovano in hello stessa area di Azure, non spese in uscita. In caso contrario, i dati restituiti tramite hello listener viene considerato in uscita e viene addebitato in base alle tariffe normali trasferimento dei dati. 
> 
> 

Un servizio di bilanciamento del carico interno può essere configurato solo nelle reti virtuali con ambito a livello di area. Le reti virtuali esistenti che sono state configurate per un gruppo di affinità non possono usare un servizio di bilanciamento del carico interno. Per altre informazioni, vedere [Panoramica del bilanciamento del carico interno](../articles/load-balancer/load-balancer-internal-overview.md).

