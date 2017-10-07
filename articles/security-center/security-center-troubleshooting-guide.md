---
title: Guida alla risoluzione dei problemi di sicurezza Center aaaAzure | Documenti Microsoft
description: Questo documento consente tootroubleshoot problemi nel Centro protezione di Azure.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 44462de6-2cc5-4672-b1d3-dbb4749a28cd
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 78b3c49eb66fe3a4f80efbba3a47a87b039c07ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-troubleshooting-guide"></a>Guida alla risoluzione dei problemi del Centro sicurezza di Azure
Questa guida è per professionisti information technology (IT), gli analisti della sicurezza di informazioni e gli amministratori cloud cui le organizzazioni usano Centro sicurezza di Azure ed è necessario che il centro di sicurezza tootroubleshoot problemi correlati.

>[!NOTE] 
>A partire da anticipata giugno 2017, il Centro sicurezza PC utilizza toocollect e l'archivio dati di Microsoft Monitoring Agent di hello. Vedere [migrazione della piattaforma Azure sicurezza Center](security-center-platform-migration.md) toolearn altre. informazioni di Hello in questo articolo rappresentano funzionalità Centro sicurezza dopo la transizione toohello Microsoft Monitoring Agent.
>

## <a name="troubleshooting-guide"></a>Guida per la risoluzione dei problemi
Questa guida illustra come centro di sicurezza tootroubleshoot problemi correlati. La maggior parte di risoluzione dei problemi di hello eseguita nel Centro sicurezza PC viene eseguita da un primo sguardo hello [Log di controllo](https://azure.microsoft.com/updates/audit-logs-in-azure-preview-portal/) record per hello Impossibile componente. Tramite i log di controllo, è possibile determinare:

* Quali operazioni sono state eseguite.
* Che ha avviato l'operazione di hello
* Quando si è verificato il funzionamento di hello
* stato Hello dell'operazione di hello
* i valori Hello altre proprietà che potrebbero facilitare la ricerca operazione hello

Registro di controllo di Hello contiene tutte le operazioni di scrittura (PUT, POST, DELETE) eseguite su risorse, ma non include le operazioni di lettura (GET).

## <a name="microsoft-monitoring-agent"></a>Microsoft Monitoring Agent
Centro sicurezza PC utilizza Microsoft Monitoring Agent hello: si tratta di hello stesso agente usato da hello Operations Management Suite e il servizio Registro Analitica – toocollect i dati di protezione da macchine virtuali di Azure. Dopo la raccolta dati è abilitata e agente hello sia installato correttamente nel computer di destinazione hello, procedura hello seguente deve essere in esecuzione:

* HealthService.exe

Se si apre una console di gestione di hello servizi (services.msc), si verifica anche servizio in esecuzione Microsoft Monitoring Agent hello come illustrato di seguito:

![Services](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig5.png)

Aprire la versione dell'agente di hello si dispone, toosee **Task Manager**, in hello **processi** scheda individuare hello **servizio Microsoft Monitoring Agent**, fare doppio clic su di esso e Fare clic su **proprietà**. In hello **dettagli** scheda, cercare la versione del file hello, come illustrato di seguito:

![File](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig6.png)
   

## <a name="microsoft-monitoring-agent-installation-scenarios"></a>Scenari di installazione di Microsoft Monitoring Agent
Esistono due scenari di installazione che possono produrre risultati diversi quando si installa Microsoft Monitoring Agent hello nel computer in uso. gli scenari di Hello supportato sono:

* **Agente installato automaticamente tramite il Centro sicurezza PC**: in questo scenario sarà tooview in grado di avvisi di hello sia percorsi, Centro sicurezza PC e ricerca nei Log. Viene visualizzato l'indirizzo di posta elettronica con i toohello le notifiche tramite posta elettronica configurati nei criteri di sicurezza hello per hello sottoscrizione hello risorsa appartiene a.
.
* **Agente installato manualmente su una macchina virtuale si trova in Azure**: in questo scenario, se si usano agenti scaricato e installato manualmente precedente tooFebruary 2017, sarà avvisi hello in grado di tooview nel portale di Centro sicurezza PC hello solo se si filtra su hello area di lavoro hello sottoscrizione a cui appartiene. In caso di filtro sulla risorsa di hello sottoscrizione hello appartiene, si sarà toosee in grado di tutti gli avvisi. Viene visualizzato l'indirizzo di posta elettronica con i toohello le notifiche tramite posta elettronica configurati nei criteri di sicurezza hello per l'area di lavoro hello hello sottoscrizione appartiene.

>[!NOTE]
> il comportamento di hello tooavoid illustrato in hello in secondo luogo, verificare di scaricare più recente dell'agente di hello hello.
> 

## <a name="troubleshooting-monitoring-agent-network-requirements"></a>Risoluzione dei problemi di rete di Microsoft Monitoring Agent
È necessario che gli agenti tooconnect tooand register con Centro sicurezza PC, accedere alle risorse di toonetwork, inclusi i numeri di porta hello e gli URL di dominio.

- Per i server proxy, è necessario tooensure che hello server proxy corretto le risorse vengono configurate nelle impostazioni dell'agente. Leggere questo articolo per ulteriori informazioni su [come toochange hello le impostazioni del proxy](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-windows-agents#configure-proxy-settings).
- Per i firewall che limitano l'accesso toohello Internet, è necessario tooconfigure tooOMS di accesso toopermit il firewall. Non è necessaria alcuna azione sulle impostazioni dell'agente.

Hello nella tabella seguente mostra le risorse necessarie per la comunicazione.

| Risorsa agente | Porte | Ignorare l'analisi HTTPS |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Sì |
| *.oms.opinsights.azure.com | 443 | Sì |
| *.blob.core.windows.net | 443 | Sì |
| *.azure-automation.net | 443 | Sì |

Se si verificano problemi di caricamento con agente hello, assicurarsi che articolo di hello tooread [come problemi di integrazione di Operations Management Suite tootroubleshoot](https://support.microsoft.com/en-us/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues).


## <a name="troubleshooting-endpoint-protection-not-working-properly"></a>Risoluzione dei problemi relativi al mancato funzionamento della protezione degli endpoint

l'agente guest Hello è il processo padre hello di qualsiasi elemento hello [Microsoft Antimalware](../security/azure-security-antimalware.md) estensione. Quando si verifica un errore di processo dell'agente guest hello, hello Microsoft Antimalware che viene eseguito come processo dell'agente guest hello figlio potrebbe non riuscire anche.  In scenari come quello è consigliato tooverify hello le opzioni seguenti:

- Se la destinazione hello VM è un'immagine personalizzata e creatore hello di hello VM è mai stato installato l'agente guest.
- Se una VM Linux invece di una macchina virtuale Windows, quindi installare la versione di Windows hello dell'estensione antimalware hello in una VM Linux di destinazione hello avrà esito negativo. l'agente guest Linux Hello presenta requisiti specifici in termini di versione del sistema operativo e i pacchetti necessari, e se tali requisiti non vengono soddisfatte agente VM hello non funzionerà vi sia. 
- Se hello VM è stato creato con una versione precedente dell'agente guest. Se è stato, è necessario tenere presente che alcuni agenti precedente potrebbero non l'aggiornamento automatico stessa versione più recente toohello e questo potrebbe causare il problema toothis. Utilizzare sempre il più recente dell'agente guest hello se la creazione di immagini personalizzate.
- Alcuni software di terze parti amministrazione può disabilitare l'agente guest hello o bloccare l'accesso toocertain percorsi dei file. Se si dispone di terze parti installata nella macchina virtuale, assicurarsi che l'agente di hello è nell'elenco di esclusione hello.
- Alcune impostazioni del firewall o un gruppo di sicurezza (rete) può bloccare tooand il traffico di rete da agente guest.
- Determinati elenchi di controllo di accesso (ACL) potrebbero impedire l'accesso al disco.
- Mancanza di spazio su disco può bloccare l'agente guest hello funzionerà correttamente. 

Per hello predefinita dell'interfaccia utente Microsoft Antimalware è disabilitato, lettura [l'abilitazione di interfaccia utente di Microsoft Antimalware in macchine virtuali di post-distribuzione di Azure Resource Manager](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/09/enabling-microsoft-antimalware-user-interface-post-deployment/) per ulteriori informazioni su come tooenable se è necessario.

## <a name="troubleshooting-problems-loading-hello-dashboard"></a>Risoluzione dei problemi durante il caricamento del dashboard hello

Se si verificano problemi durante il caricamento del dashboard di hello Centro sicurezza PC, assicurarsi che l'utente hello registra hello sottoscrizione tooSecurity Center (vale a dire hello prima utente un utente che ha aperto il Centro sicurezza PC con sottoscrizione hello) e gli utenti hello desiderano tooturn in raccolta di dati deve essere *proprietario* o *collaboratore* sottoscrizione hello. Da quel momento anche gli utenti con *lettore* su hello sottoscrizione è possibile visualizzare dashboard hello/avvisi/raccomandazione/criteri.

## <a name="contacting-microsoft-support"></a>Contattare il supporto tecnico Microsoft
Alcuni problemi possono essere identificati utilizzando linee guida hello fornite in questo articolo, altri sono disponibili anche documentato all'hello Centro sicurezza PC pubblico [Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureSecurityCenter). Tuttavia, se è necessario un altro tipo di risoluzione dei problemi, è possibile aprire una nuova richiesta di supporto tramite il **portale di Azure**, come illustrato di seguito: 

![Supporto tecnico Microsoft](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig2.png)


## <a name="see-also"></a>Vedere anche
In questo documento, si è appreso come criteri di sicurezza tooconfigure Centro sicurezza di Azure. toolearn ulteriori informazioni su Centro sicurezza di Azure, vedere l'esempio hello:

* [Centro sicurezza di Azure Guida alla pianificazione e le operazioni](security-center-planning-and-operations-guide.md) , informazioni come tooplan e comprendere considerazioni sulla progettazione hello tooadopt Centro sicurezza di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) : informazioni su come toomonitor hello integrità delle risorse di Azure
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) , informazioni come avvisi toosecurity toomanage e rispondere
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure

