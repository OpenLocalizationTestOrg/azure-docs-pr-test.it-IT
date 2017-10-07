---
title: aaaHow tooadminister Cache Redis di Azure | Documenti Microsoft
description: "Informazioni su come attività di amministrazione tooperform come riavviare il computer e Pianifica aggiornamenti per Cache Redis di Azure"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 8c915ae6-5322-4046-9938-8f7832403000
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: eb24668a3f6264444e7d4daf1ac43b41b12dfe66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadminister-azure-redis-cache"></a>La modalità di Cache Redis di Azure di tooadminister
Questo argomento viene descritto come attività di amministrazione tooperform come [riavvio](#reboot) e [pianificazione degli aggiornamenti di](#schedule-updates) per le istanze di Cache Redis di Azure.

## <a name="reboot"></a>Reboot
Hello **riavviare** pannello consente tooreboot uno o più nodi della cache. Questa funzionalità di riavvio consente si tootest all'applicazione per garantire la resilienza, se si verifica un errore di un nodo della cache.

![Reboot](./media/cache-administration/redis-cache-administration-reboot.png)

Selezionare tooreboot nodi hello e fare clic su **riavviare**.

![Reboot](./media/cache-administration/redis-cache-reboot.png)

Se si dispone di una cache premium con clustering abilitato, è possibile selezionare le partizioni di tooreboot cache di hello.

![Reboot](./media/cache-administration/redis-cache-reboot-cluster.png)

tooreboot uno o più nodi della cache, selezionare i nodi di hello desiderato e fare clic su **riavviare**. Se si dispone di una cache premium con clustering abilitato, selezionare tooreboot partizioni hello desiderato e quindi fare clic su **riavviare**. Dopo alcuni minuti, hello riavvio nodi selezionati e sono in linea alcuni minuti in un secondo momento.

impatto di Hello sulle applicazioni client varia a seconda di quali sono i nodi che si riavvia.

* **Master** - quando viene riavviato, Azure ha esito negativo di Cache Redis nel nodo di replica toohello e innalza di livello toomaster di nodo principale hello. Durante il failover, potrebbe esserci un breve periodo di tempo in cui le connessioni potrebbero non riuscire toohello cache.
* **Slave** : quando il nodo di slave hello viene riavviato, non è in genere i client toocache alcun impatto.
* **Il master e slave** : quando entrambi i nodi della cache vengono riavviati, tutti i dati vengono persi nel hello cache e le connessioni toohello cache avranno esito negativo fino a quando non nodo primario hello torna online. Se è stato configurato [persistenza dei dati](cache-how-to-premium-persistence.md), ripristino del backup più recente di hello quando la cache di hello torna online, ma eventuali operazioni di scrittura cache che si sono verificati dopo il backup più recente di hello vanno perdute.
* **I nodi di un premio memorizzare nella cache con il clustering abilitato** : quando si riavvia uno o più nodi di una cache premium con clustering abilitata, hello comportamento per hello selezionata è hello stessi nodi come quando si riavvia hello corrispondente o nodi di non cluster cache.

> [!IMPORTANT]
> Il riavvio ora è disponibile per tutti i piani tariffari.
> 
> 

## <a name="reboot-faq"></a>Domande frequenti sulla funzionalità di riavvio
* [Il nodo è necessario il riavvio tootest la mia applicazione?](#which-node-should-i-reboot-to-test-my-application)
* [È possibile riavviare il computer connessioni client tooclear della cache di hello?](#can-i-reboot-the-cache-to-clear-client-connections)
* [Con il riavvio i dati nella cache andranno persi?](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [È possibile riavviare la cache usando PowerShell, l'interfaccia della riga di comando o altri strumenti di gestione?](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [I prezzi livelli, è possibile utilizzare la funzionalità di riavvio hello?](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-tootest-my-application"></a>Il nodo è necessario il riavvio tootest la mia applicazione?
resilienza hello tootest dell'applicazione in caso di errore del nodo primario di hello della cache, il riavvio hello **Master** nodo. resilienza hello tootest dell'applicazione in caso di errore del nodo secondario di hello, riavvio hello **Slave** nodo. resilienza hello tootest dell'applicazione in caso di errore totale della cache di hello, riavviare il computer **entrambi** nodi.

### <a name="can-i-reboot-hello-cache-tooclear-client-connections"></a>È possibile riavviare il computer connessioni client tooclear della cache di hello?
Sì, se si riavvia una cache di hello vengono cancellate tutte le connessioni client. Il riavvio può essere utile in caso di hello in tutte le connessioni client vengono utilizzate a causa di errori di logica tooa o un bug nell'applicazione client hello. Ogni piano tariffario presenta diversi [limiti di connessione client](cache-configure.md#default-redis-server-configuration) per diverse dimensioni di hello e una volta raggiungono i limiti, non più connessioni client vengono accettate. Il riavvio della cache di hello fornisce un modo tooclear tutte le connessioni client.

> [!IMPORTANT]
> Se si riavvia le connessioni client di cache tooclear, stackexchange. Redis si riconnette automaticamente dopo il nodo di Redis hello è tornata in linea. Se non è stato risolto il problema sottostante hello, le connessioni client hello possono continuare toobe utilizzato.
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a>Con il riavvio i dati nella cache andranno persi?
Se si riavvia entrambi hello **Master** e **Slave** nodi, tutti i dati nella cache di hello (o in tale partizione, se si utilizza una cache premium con clustering abilitata) viene perso. Se è stato configurato [persistenza dei dati](cache-how-to-premium-persistence.md), verrà ripristinato backup più recente di hello quando la cache di hello torna online, ma eventuali operazioni di scrittura cache che si sono verificati dopo che è stato eseguito il backup di hello vanno perdute.

Se si riavvia solo uno dei nodi di hello, dati non sono in genere persi, ma è comunque possibile. Ad esempio, se il nodo principale hello viene riavviato e la scrittura della cache è in corso, dati hello dalla scrittura cache di hello è persa. Un altro scenario per la perdita di dati sarebbe se si riavvia un nodo e hello altro nodo avviene toogo verso il basso a causa di errore tooa hello contemporaneamente. Per ulteriori informazioni sulle possibili cause di perdita dei dati, vedere [quali dati toomy verificato anomalo in Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a>È possibile riavviare la cache usando PowerShell, l'interfaccia della riga di comando o altri strumenti di gestione?
Sì, per PowerShell istruzioni, vedere [tooreboot una cache Redis](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache).

### <a name="what-pricing-tiers-can-use-hello-reboot-functionality"></a>I prezzi livelli, è possibile utilizzare la funzionalità di riavvio hello?
Il riavvio è disponibile per tutti i piani tariffari.

## <a name="schedule-updates"></a>Pianificare gli aggiornamenti
Hello **pianificare aggiornamenti** pannello consente toodesignate una finestra di manutenzione per la cache di livello Premium. Quando la finestra di manutenzione hello è specificata, vengono eseguiti tutti gli aggiornamenti server Redis durante questa finestra. 

> [!NOTE] 
> finestra di manutenzione Hello si applica solo aggiornamenti di server tooRedis e tooany Azure aggiorna o aggiorna il sistema operativo toohello delle macchine virtuali di hello che ospitano una cache di hello.
> 
> 

![Pianificare gli aggiornamenti](./media/cache-administration/redis-schedule-updates.png)

toospecify una finestra di manutenzione, controllare i giorni hello desiderato e specificare l'ora di inizio finestra di manutenzione di hello per ogni giorno e fare clic su **OK**. Si noti che ora finestra di manutenzione hello è in formato UTC. 

> [!NOTE]
> finestra di manutenzione Hello predefinito per gli aggiornamenti sono cinque ore. Questo valore non è configurabile dal portale di Azure hello, ma è possibile configurarlo in PowerShell usando hello `MaintenanceWindow` parametro di hello [New AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) cmdlet. Per altre informazioni, vedere [È possibile gestire gli aggiornamenti pianificati usando PowerShell, l'interfaccia della riga di comando o altri strumenti di gestione?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)
> 
> 

## <a name="schedule-updates-faq"></a>Domande frequenti sulla pianificazione degli aggiornamenti
* [Quando gli aggiornamenti si verificano se non si utilizza funzionalità di aggiornamento pianificazione hello?](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [Il tipo di aggiornamenti apportate durante hello pianificare una finestra di manutenzione?](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [È possibile gestire gli aggiornamenti pianificati usando PowerShell, l'interfaccia della riga di comando o altri strumenti di gestione?](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [I prezzi livelli, è possibile utilizzare funzionalità di aggiornamenti di pianificazione hello?](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-hello-schedule-updates-feature"></a>Quando gli aggiornamenti si verificano se non si utilizza funzionalità di aggiornamento pianificazione hello?
Se non si specifica un intervallo di manutenzione, è possibile eseguire aggiornamenti in qualsiasi momento.

### <a name="what-type-of-updates-are-made-during-hello-scheduled-maintenance-window"></a>Il tipo di aggiornamenti apportate durante hello pianificare una finestra di manutenzione?
Redis solo gli aggiornamenti vengono eseguiti durante la finestra di manutenzione pianificata hello server. finestra di manutenzione Hello non applicare gli aggiornamenti di tooAzure o aggiorna toohello macchina virtuale del sistema operativo.

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a>È possibile gestire gli aggiornamenti pianificati usando PowerShell, l'interfaccia della riga di comando o altri strumenti di gestione?
Sì, è possibile gestire gli aggiornamenti pianificati utilizzando hello i cmdlet di PowerShell seguente:

* [Get-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/get-azurermrediscachepatchschedule)
* [New-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/new-azurermrediscachepatchschedule)
* [New-AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry)
* [Remove-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-hello-schedule-updates-functionality"></a>I prezzi livelli, è possibile utilizzare funzionalità di aggiornamenti di pianificazione hello?
Hello **pianificare aggiornamenti** funzionalità è disponibile solo in tariffario premium hello.

## <a name="next-steps"></a>Passaggi successivi
* Esplorare altre funzionalità del [piano Premium di Cache Redis di Azure](cache-premium-tier-intro.md) .

