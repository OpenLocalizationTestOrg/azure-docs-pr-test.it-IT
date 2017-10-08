---
title: "aaaCreate un listener del gruppo di disponibilità di SQL Server in macchine virtuali di Azure | Documenti Microsoft"
description: "Istruzioni dettagliate per creare un listener per un gruppo di disponibilità Always On per SQL Server nelle macchine virtuali di Azure"
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/01/2017
ms.author: mikeray
ms.openlocfilehash: c6a44dc5c7c18b572c2bf5772b4651b7210aacbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a>Configurare un servizio di bilanciamento del carico interno per un gruppo di disponibilità Always On in Azure
Questo articolo viene illustrato come un bilanciamento del carico per un gruppo di disponibilità SQL Server Always On in Azure virtuale toocreate computer che eseguono con Gestione risorse di Azure. Un gruppo di disponibilità richiede un bilanciamento del carico quando si trovano le istanze di SQL Server hello in macchine virtuali di Azure. servizio di bilanciamento del carico Hello archivia l'indirizzo IP hello per listener del gruppo di disponibilità hello. Se un gruppo di disponibilità si estende su più aree, è necessario un servizio di bilanciamento del carico per ogni area.

toocomplete questa attività, è necessario un gruppo di disponibilità di SQL Server è distribuito in macchine virtuali di Azure che eseguono con Gestione risorse di toohave. Entrambe le macchine virtuali di SQL Server deve appartenere toohello stesso set di disponibilità. È possibile utilizzare hello [modello Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically creare il gruppo di disponibilità di hello in Gestione risorse. Questo modello crea automaticamente un servizio di bilanciamento del carico interno. 

Se si preferisce, è possibile [configurare manualmente un gruppo di disponibilità](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Per questo articolo è necessario che i gruppi di disponibilità siano già configurati.  

Gli argomenti correlati includono:

* [Configurare i gruppi di disponibilità Always On in una macchina virtuale di Azure, GUI](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Configurare una connessione da VNet a VNet tramite Azure Resource Manager e PowerShell](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

Esaminando questo articolo, creare e configurare un bilanciamento del carico in hello portale di Azure. Una volta completato il processo di hello, configurare hello toouse hello indirizzo IP del cluster di bilanciamento del carico hello per listener del gruppo di disponibilità hello.

## <a name="create-and-configure-hello-load-balancer-in-hello-azure-portal"></a>Creare e configurare Bilanciamento carico di hello in hello portale di Azure
In questa parte dell'attività hello hello seguenti:

1. Nel portale di Azure hello, bilanciamento del carico hello creare e configurare l'indirizzo IP di hello.
2. Configurare il pool di back-end hello.
3. Creare il probe hello. 
4. Impostare regole di bilanciamento del carico di hello.

> [!NOTE]
> Se le istanze di SQL Server hello in più gruppi di risorse e le aree, eseguire ogni passaggio due volte, una volta in ogni gruppo di risorse.
> 
> 

### <a name="step-1-create-hello-load-balancer-and-configure-hello-ip-address"></a>Passaggio 1: Creare bilanciamento del carico hello e configurare l'indirizzo IP hello
Innanzitutto, creare bilanciamento del carico hello. 

1. Nel portale di Azure hello, aprire gruppo di risorse hello contenente hello macchine virtuali di SQL Server. 

2. Nel gruppo di risorse hello, fare clic su **Aggiungi**.

3. Cercare **bilanciamento del carico** nei risultati della ricerca hello, quindi selezionare **bilanciamento del carico**, che viene pubblicato da **Microsoft**.

4. In hello **bilanciamento del carico** pannello, fare clic su **crea**.

5. In hello **Crea servizio di bilanciamento del carico** finestra di dialogo casella, configurare il bilanciamento del carico di hello come indicato di seguito:

   | Impostazione | Valore |
   | --- | --- |
   | **Nome** |Un nome di testo che rappresenta di bilanciamento del carico hello. Ad esempio **sqlLB**. |
   | **Tipo** |**Interno**: la maggior parte delle implementazioni usano un servizio di bilanciamento del carico interno, che consente alle applicazioni all'interno di hello stesso gruppo di disponibilità toohello di tooconnect rete virtuale.  </br> **Esterno**: consente di gruppo di disponibilità di applicazioni tooconnect toohello tramite una connessione Internet pubblica. |
   | **Rete virtuale** |Selezionare hello la rete virtuale che si trovano in istanze di SQL Server hello. |
   | **Subnet** |Selezionare subnet hello presenti istanze di SQL Server hello. |
   | **Assegnazione indirizzi IP** |**Statico** |
   | **Indirizzo IP privato** |Specificare un indirizzo IP disponibile dalla subnet hello. Utilizzare questo indirizzo IP quando si crea un listener in cluster hello. In uno script di PowerShell, più avanti in questo articolo, utilizzare questo indirizzo per hello `$ILBIP` variabile. |
   | **Sottoscrizione** |Se si hanno più sottoscrizioni, può essere visualizzato questo campo. Selezionare una sottoscrizione di hello che si desidera tooassociate con questa risorsa. Come tutte le risorse di hello per il gruppo di disponibilità hello in genere è hello stessa sottoscrizione. |
   | **Gruppo di risorse** |Selezionare gruppo di risorse hello presenti istanze di SQL Server hello. |
   | **Posizione** |Selezionare una località di Azure che sono istanze di SQL Server hello in hello. |

6. Fare clic su **Crea**. 

Azure Crea servizio di bilanciamento del carico hello. servizio di bilanciamento del carico Hello appartiene tooa di rete specifica, subnet, gruppo di risorse e percorso. Al termine dell'attività hello Azure, verificare le impostazioni del servizio di bilanciamento carico di hello in Azure. 

### <a name="step-2-configure-hello-back-end-pool"></a>Passaggio 2: Configurare i pool di back-end hello
Le chiamate Azure hello pool di indirizzi back-end *pool back-end*. In questo caso, il pool di back-end hello è indirizzi hello hello due istanze di SQL Server nel gruppo di disponibilità. 

1. Nel gruppo di risorse, fare clic su servizio di bilanciamento del carico hello creato. 

2. In **Impostazioni** fare clic su **Pool back-end**.

3. In **pool back-end**, fare clic su **Aggiungi** toocreate un pool di indirizzi back-end. 

4. In **aggiungere pool back-end**in **nome**, digitare un nome per il pool back-end hello.

5. In **Macchine virtuali** fare clic su **Aggiungi una macchina virtuale**. 

6. In **scegliere macchine virtuali**, fare clic su **scegliere un set di disponibilità**, quindi specificare set di disponibilità di hello che hello macchine virtuali di SQL Server deve appartenere a.

7. Dopo aver scelto il set di disponibilità di hello, fare clic su **scegliere macchine virtuali hello**, selezionare hello due macchine virtuali che ospitano istanze di SQL Server hello nel gruppo di disponibilità hello e quindi fare clic su **selezionare**. 

8. Fare clic su **OK** pannelli hello tooclose per **scegliere macchine virtuali**, e **aggiungere pool back-end**. 

Azure Aggiorna le impostazioni di hello per il pool di indirizzi back-end di hello. Il set di disponibilità ora include un pool di due istanze di SQL Server.

### <a name="step-3-create-a-probe"></a>Passaggio 3: Creare un probe
probe Hello definisce come Azure verifica hello istanze di SQL Server attualmente proprietario del listener del gruppo di disponibilità hello. Azure le ricerche basato sull'indirizzo IP hello su una porta definiti durante la creazione di probe hello del servizio di hello.

1. In hello bilanciamento del carico **impostazioni** pannello, fare clic su **probe di integrità**. 

2. In hello **probe di integrità** pannello, fare clic su **Aggiungi**.

3. Configurare il probe hello in hello **Aggiungi probe** blade. Hello utilizzare valori tooconfigure hello probe seguenti:

   | Impostazione | Valore |
   | --- | --- |
   | **Nome** |Un nome di testo che rappresenta il probe hello. Ad esempio **SQLAlwaysOnEndPointProbe**. |
   | **Protocollo** |**TCP** |
   | **Porta** |È possibile usare qualsiasi porta disponibile. Ad esempio *59999*. |
   | **Interval** |*5* |
   | **Soglia non integra** |*2* |

4.  Fare clic su **OK**. 

> [!NOTE]
> Assicurarsi che porta hello specificata sia aperta nel firewall hello di entrambe le istanze di SQL Server. Entrambe le istanze richiedono una regola in ingresso per hello la porta TCP in uso. Per altre informazioni, vedere [Aggiungere o modificare una regola del firewall](http://technet.microsoft.com/library/cc753558.aspx). 
> 
> 

Azure crea probe hello e viene utilizzata l'istanza di SQL Server ha listener hello per il gruppo di disponibilità hello tootest.

### <a name="step-4-set-hello-load-balancing-rules"></a>Passaggio 4: Impostare le regole di bilanciamento del carico di hello
regole di bilanciamento del carico Hello configurare come servizio di bilanciamento del carico hello instrada le istanze di SQL Server toohello di traffico. Per il bilanciamento del carico, abilitare direct server return perché solo uno di due istanze di SQL Server hello proprietario risorsa listener del gruppo di disponibilità hello alla volta.

1. In hello bilanciamento del carico **impostazioni** pannello, fare clic su **regole di bilanciamento del carico**. 

2. In hello **regole di bilanciamento del carico** pannello, fare clic su **Aggiungi**.

3. In hello **regole di bilanciamento del carico di Aggiungi** pannello, configurare una regola di bilanciamento del carico di hello. Utilizzare hello seguenti impostazioni: 

   | Impostazione | Valore |
   | --- | --- |
   | **Nome** |Un nome di testo che rappresenta le regole di bilanciamento del carico di hello. Ad esempio **SQLAlwaysOnEndPointListener**. |
   | **Protocollo** |**TCP** |
   | **Porta** |*1433* |
   | **Porta back-end** |*1433*. Questo valore verrà ignorato perché questa regola usa **IP mobile (Direct Server Return)**. |
   | **Probe** |Utilizzare il nome di hello del probe hello creato per il bilanciamento del carico. |
   | **Persistenza della sessione** |**Nessuno** |
   | **Timeout di inattività (minuti)** |*4* |
   | **IP mobile (Direct Server Return)** |**Enabled** |

   > [!NOTE]
   > Potrebbe essere tooscroll verso il basso hello pannello tooview tutte le impostazioni di hello.
   > 

4. Fare clic su **OK**. 
5. Azure Configura regola di bilanciamento del carico di hello. Bilanciamento del carico hello è ora configurato tooroute traffico toohello istanza di SQL Server ospita hello listener per gruppo di disponibilità hello. 

A questo punto, il gruppo di risorse hello dispone di un bilanciamento del carico che si connette tooboth macchine di SQL Server. servizio di bilanciamento del carico Hello contiene anche un indirizzo IP per hello SQL Server Always On listener gruppo di disponibilità, in modo che entrambi i computer possano rispondere toorequests per gruppi di disponibilità hello.

> [!NOTE]
> Se le istanze di SQL Server sono in due aree distinte, ripetere i passaggi di hello in hello altre aree. Ogni area richiede un servizio di bilanciamento del carico. 
> 
> 

## <a name="configure-hello-cluster-toouse-hello-load-balancer-ip-address"></a>Configurare hello toouse hello carico bilanciamento del carico indirizzo IP del cluster
passaggio successivo Hello tooconfigure hello listener in cluster hello e portare hello listener online. Hello seguenti: 

1. Creare listener del gruppo di disponibilità hello nel cluster di failover hello. 

2. Portare hello listener online.

### <a name="step-5-create-hello-availability-group-listener-on-hello-failover-cluster"></a>Passaggio 5: Creare listener del gruppo di disponibilità hello nel cluster di failover hello
In questo passaggio, creare manualmente listener del gruppo di disponibilità di hello in Gestione Cluster di Failover e SQL Server Management Studio.

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-hello-configuration-of-hello-listener"></a>Verificare la configurazione del listener hello hello

Se le dipendenze e le risorse cluster hello siano configurate correttamente, dovrebbe essere in grado di tooview listener di hello in SQL Server Management Studio. tooset hello porta del listener, hello seguenti:

1. Avviare SQL Server Management Studio e connettiti toohello replica primaria.

2. Andare troppo**disponibilità elevata AlwaysOn** > **gruppi di disponibilità** > **listener del gruppo di disponibilità**.  
    Viene visualizzato il nome del listener hello creati in Gestione Cluster di Failover. 

3. Il nome del listener hello destro e quindi fare clic su **proprietà**.

4. In hello **porta** , specificare il numero di porta hello del listener del gruppo di disponibilità hello utilizzando hello $EndpointPort utilizzato in precedenza (1433 è predefinito hello), quindi fare clic su **OK**.

Ora si ha un gruppo di disponibilità nelle macchine virtuali di Azure in esecuzione in modalità Resource Manager. 

## <a name="test-hello-connection-toohello-listener"></a>Listener toohello connessione hello di test
Test connessione hello eseguendo hello seguenti:

1. Istanza di SQL Server tooa RDP in hello stesso virtuale di rete, ma non non replica hello personalizzati. Questo server può essere hello altra istanza SQL Server in cluster hello.

2. Utilizzare **sqlcmd** connessione hello tootest di utilità. Ad esempio, lo script seguente hello stabilisce un **sqlcmd** replica primaria toohello di connessione tramite il listener hello con l'autenticazione di Windows:
   
        sqlcmd -S <listenerName> -E

connessione SQLCMD Hello si connette automaticamente toohello istanza di SQL Server che ospita la replica primaria hello. 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a>Creare un indirizzo IP per un gruppo di disponibilità aggiuntivo

Ogni gruppo di disponibilità usa un listener diverso. Ogni listener ha un proprio indirizzo IP. Utilizzare hello stesso carica l'indirizzo IP di bilanciamento del carico toohold hello per listener aggiuntivi. Dopo aver creato un gruppo di disponibilità, aggiungere toohello hello IP indirizzo il bilanciamento del carico e quindi configurare il listener hello.

tooadd un bilanciamento del carico IP indirizzo tooa con il portale di Azure, hello hello seguenti:

1. Nel portale di Azure hello, aprire gruppo di risorse hello contenente bilanciamento del carico hello e quindi fare clic su servizio di bilanciamento del carico hello. 

2. In **IMPOSTAZIONI** fare clic su **Pool di indirizzi IP front-end** e quindi su **Aggiungi**. 

3. In **Aggiungi indirizzo IP di front-end**, assegnare un nome front-end hello. 

4. Verificare che hello **rete virtuale** hello e **Subnet** sono hello stesso hello istanze di SQL Server.

5. Impostare l'indirizzo IP hello per listener hello. 
   
   >[!TIP]
   >È possibile impostare toostatic indirizzo IP di hello e digitare un indirizzo che non è attualmente usato nella subnet hello. In alternativa, è possibile impostare toodynamic indirizzo IP di hello e salvare il pool IP di hello nuovo front-end. Quando si esegue questa operazione, hello portale di Azure assegna automaticamente un pool di toohello di indirizzi IP disponibile. È quindi possibile riaprire il pool IP front-end di hello e modificare toostatic assegnazione hello. 

6. Salva l'indirizzo IP hello per listener hello. 

7. Aggiungere un probe di integrità tramite hello seguenti impostazioni:

   |Impostazione |Valore
   |:-----|:----
   |**Nome** |Probe di hello tooidentify un nome.
   |**Protocollo** |TCP
   |**Porta** |Una porta TCP non usata che deve essere disponibile in tutte le macchine virtuali. Non può essere usata per altri scopi. Nessun due listener può utilizzare hello stessa porta probe. 
   |**Interval** |tenta di Hello periodo di tempo tra probe. Usare hello predefinito (5).
   |**Soglia non integra** |numero di Hello delle soglie consecutive che devono verificarsi prima di una macchina virtuale viene considerata non integra.

8. Fare clic su **OK** probe hello toosave. 

9. Creare una regola di bilanciamento del carico. Fare clic su **Regole di bilanciamento del carico** e quindi fare clic su **Aggiungi**.

10. Configurare hello nuovo bilanciamento del carico regola utilizzando hello seguenti impostazioni:

   |Impostazione |Valore
   |:-----|:----
   |**Nome** |Un hello tooidentify nome caricare la regola di bilanciamento del carico. 
   |**Indirizzo IP front-end IP** |Selezionare l'indirizzo IP hello che è stato creato. 
   |**Protocollo** |TCP
   |**Porta** |Utilizzare hello porta che utilizzano le istanze di SQL Server hello. Un'istanza predefinita utilizza la porta 1433, a meno che non venga modificata. 
   |**Porta back-end** |Hello utilizzare lo stesso valore **porta**.
   |**Pool back-end** |pool di Hello contenente macchine virtuali hello con istanze di SQL Server hello. 
   |**Probe di integrità** |Scegliere probe hello che è stato creato.
   |**Persistenza della sessione** |Nessuno
   |**Timeout di inattività (minuti)** |Valore predefinito (4)
   |**IP mobile (Direct Server Return)** | Enabled

### <a name="configure-hello-availability-group-toouse-hello-new-ip-address"></a>Configurare hello disponibilità gruppo toouse hello nuovo indirizzo IP

toofinish configurazione cluster hello, passaggi ripetizione hello eseguiti dopo il primo gruppo di disponibilità hello effettuato. Vale a dire, configurare hello [toouse hello nuovo indirizzo IP del cluster](#configure-the-cluster-to-use-the-load-balancer-ip-address). 

Dopo aver aggiunto un indirizzo IP del listener hello, configurare il gruppo di disponibilità aggiuntiva hello eseguendo hello seguenti: 

1. Verificare che la porta probe hello nuovo indirizzo IP di hello è aperta in entrambe le macchine virtuali di SQL Server. 

2. [In Gestione Cluster di aggiungere il punto di accesso client hello](#addcap).

3. [Configurare la risorsa IP hello per il gruppo di disponibilità hello](#congroup).

   >[!IMPORTANT]
   >Quando si crea l'indirizzo IP di hello, utilizzare l'indirizzo IP hello aggiunto toohello servizio di bilanciamento del carico.  

4. [Rendere dipendente nel punto di accesso client hello risorsa gruppo di disponibilità SQL Server hello](#dependencyGroup).

5. [Rendere l'accesso ai client di hello punto risorsa dipendente dalla risorsa indirizzo IP hello](#listname).
 
6. [Impostare i parametri del cluster hello in PowerShell](#setparam).

Dopo aver configurato hello disponibilità gruppo toouse hello nuovo indirizzo IP, configurare toohello listener della connessione hello. 

## <a name="next-steps"></a>Passaggi successivi

- [Configurare un gruppo di disponibilità SQL Server AlwaysOn nelle macchine virtuali di Azure](virtual-machines-windows-portal-sql-availability-group-dr.md)
