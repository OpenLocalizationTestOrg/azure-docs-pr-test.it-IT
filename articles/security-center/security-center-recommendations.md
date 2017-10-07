---
title: consigli sulla sicurezza aaaManaging nel Centro protezione di Azure | Documenti Microsoft
description: "Questo documento dimostra come le raccomandazioni presenti nel Centro sicurezza di Azure facilitino la protezione delle risorse di Azure e garantiscano la conformità ai criteri di sicurezza."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 86c50c9f-eb6b-4d97-acb3-6d599c06133e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: f6bbe36a7a5636095b339b3e9765b87cc0ab669a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-security-recommendations-in-azure-security-center"></a>Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure
Questo documento illustra come indicazioni toouse toohelp Centro sicurezza di Azure proteggere le risorse di Azure.

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione.  Questo argomento non costituisce una guida dettagliata.
>
>

## <a name="what-are-security-recommendations"></a>Informazioni sulle raccomandazioni di sicurezza
Centro sicurezza PC analizza periodicamente lo stato di sicurezza hello delle risorse di Azure. Quando identifica potenziali vulnerabilità della sicurezza, crea raccomandazioni. indicazioni Hello semplificato il processo di hello di configurazione dei controlli di hello necessita.

## <a name="implementing-security-recommendations"></a>Implementare le raccomandazioni di sicurezza
### <a name="set-recommendations"></a>Impostare le raccomandazioni
In [Impostazione dei criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md)si apprende come:

* Configurare i criteri di sicurezza.
* Attivare la raccolta dei dati.
* Scegliere quali toosee indicazioni come parte dei criteri di protezione.

Le raccomandazioni relative ai criteri di sicurezza si basano attualmente su aggiornamenti di sistema, regole di base, programmi antimalware, [gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md) per subnet e interfacce di rete, controllo del database SQL, Transparent Data Encryption per il database SQL e web application firewall.  [Impostazione dei criteri di sicurezza](security-center-policies.md) fornisce una descrizione di ogni opzione relativa alle raccomandazioni.

### <a name="monitor-recommendations"></a>Monitorare le raccomandazioni
Dopo aver impostato un criterio di sicurezza, il Centro sicurezza PC analizza stato protezione hello i potenziali vulnerabilità tooidentify di risorse. Hello **indicazioni** riquadro hello **Centro sicurezza PC** pannello consente di conoscere il numero totale di hello delle raccomandazioni identificato dal Centro sicurezza PC.

![Riquadro Raccomandazioni][1]

toosee dettagli hello ogni raccomandazione:

Seleziona hello **indicazioni riquadro** su hello **Centro sicurezza PC** blade. Hello **indicazioni** apre blade.

indicazioni Hello vengono visualizzati in un formato di tabella in cui ogni riga rappresenta una raccomandazione particolare. Hello colonne della tabella sono:

* **Descrizione**: illustra indicazioni hello e delle operazioni eseguite tooaddress toobe è.
* **RISORSA**: Elenca toowhich risorse hello questa indicazione è valida.
* **STATO**: descrive lo stato corrente di hello della raccomandazione hello:
  * **Aprire**: non è stato indirizzato ancora raccomandazione hello.
  * **In corso**: indicazione hello è attualmente in fase di risorse applicata toohello e senza alcun intervento da parte dell'utente.
  * **Risolto**: indicazione hello è già stata completata (in questo caso, la riga hello è grigio).
* **GRAVITÀ**: descrive gravità hello di raccomandazione particolare:
  * **Alta**: una vulnerabilità associata a una risorsa significativa, ad esempio un'applicazione, una macchina virtuale o un gruppo di sicurezza di rete, richiede attenzione.
  * **Media**: esiste una vulnerabilità e non critici o altri passaggi sono necessari tooeliminate oppure toocomplete un processo.
  * **Bassa**: una vulnerabilità che è opportuno risolvere, non richiede attenzione immediata. (Per impostazione predefinita, non vengono presentati suggerimenti basse, ma è possibile filtrare indicazioni basse se si desidera toosee li.)

Tabella di hello utilizzare riportata di seguito come un riferimento di toohelp comprendere indicazioni disponibili hello e la funzione ognuno se lo si applica.

> [!NOTE]
> È consigliabile hello toounderstand [classica e modelli di distribuzione di gestione risorse](../azure-classic-rm.md) per le risorse di Azure.
>
>

| Raccomandazione | Descrizione |
| --- | --- |
| [Abilita la raccolta di dati per le sottoscrizioni](security-center-enable-data-collection.md) |Si consiglia di attivare la raccolta dei dati nei criteri di sicurezza hello per ognuna delle sottoscrizioni e tutte le macchine virtuali (VM) le sottoscrizioni. |
| [Remediate OS vulnerabilities (Risolvi vulnerabilità del sistema operativo)](security-center-remediate-os-vulnerabilities.md) |Si consiglia di allineare le configurazioni del sistema operativo con hello consiglia le regole di configurazione, ad esempio, non consentire password toobe salvato. |
| [Applicare gli aggiornamenti di sistema](security-center-apply-system-updates.md) |Consiglia di distribuire la protezione del sistema mancanti e gli aggiornamenti critici tooVMs. |
| [Applicare un controllo di accesso alla rete JIT](security-center-just-in-time.md) | Consiglia di applicare l'accesso Just-In-Time alla macchina virtuale. Hello solo nella funzione di tempo è in anteprima e disponibile nel livello Standard del Centro sicurezza PC hello. Vedere [prezzi](security-center-pricing.md) toolearn ulteriori informazioni su Centro sicurezza di livelli di prezzo. |
| [Riavvia dopo gli aggiornamenti del sistema](security-center-apply-system-updates.md#reboot-after-system-updates) |Si consiglia di riavviare un processo di hello VM toocomplete di applicazione degli aggiornamenti di sistema. |
| [Aggiungere un Web Application Firewall](security-center-add-web-application-firewall.md) |Suggerisce di distribuire un Web application firewall (WAF) per gli endpoint Web. Viene visualizzata una raccomandazione WAF per qualsiasi IP pubblico (IP a livello di istanza o IP con carico bilanciato) cui è associato un gruppo di sicurezza di rete con porte Web in ingresso aperte (80, 443). </br>Centro sicurezza PC consiglia che si provisioning un toohelp WAF difendersi da attacchi di applicazioni web nelle macchine virtuali e sull'ambiente di servizio App di destinazione. Un Ambiente del servizio app è un'opzione del piano di servizio [Premium](https://azure.microsoft.com/pricing/details/app-service/) del Servizio app di Azure che offre un ambiente completamente isolato e dedicato per eseguire in modo sicuro tutte le app del servizio. toolearn ulteriori informazioni su ASE, vedere hello [documentazione dell'ambiente del servizio App](../app-service/app-service-app-service-environments-readme.md).</br>È possibile proteggere nel Centro protezione di più applicazioni web tramite l'aggiunta di queste applicazioni tooyour WAF le distribuzioni esistenti. |
| [Finalizza la protezione dell'applicazione](security-center-add-web-application-firewall.md#finalize-application-protection) |configurazione di hello toocomplete di un WAF, il traffico deve essere reindirizzato toohello WAF accessorio. Seguendo queste indicazioni completa delle modifiche di installazione necessari hello. |
| [Aggiungi un firewall di nuova generazione](security-center-add-next-generation-firewall.md) |Consiglia di aggiungere un Firewall di generazione successiva (NGFW) da un tooincrease partner Microsoft i meccanismi di protezione. |
| [Indirizza il traffico solo tramite il firewall di nuova generazione](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Consiglia di configurare regole di gruppo () sicurezza di rete che impongono il traffico in entrata tooyour VM tramite il NGFW. |
| [Installa Endpoint Protection](security-center-install-endpoint-protection.md) |Si consiglia di eseguire il provisioning tooVMs programmi antimalware (solo per macchine virtuali Windows). |
| [Risolvi gli avvisi sull'integrità di Endpoint Protection](security-center-resolve-endpoint-protection-health-alerts.md) |Si consiglia di correggere gli errori relativi alla protezione degli endpoint. |
| [Abilita i gruppi di sicurezza di rete sulle subnet o sulle macchine virtuali](security-center-enable-network-security-groups.md) |Consiglia di attivare i gruppo di sicurezza di rete sulle subnet o sulle macchine virtuali. |
| [Limita l'accesso tramite un endpoint con connessione Internet](security-center-restrict-access-through-internet-facing-endpoints.md) |Consiglia di configurare le regole del traffico in ingresso per i gruppi di sicurezza di rete. |
| [Abilitare il controllo e il rilevamento delle minacce nei server SQL](security-center-enable-auditing-on-sql-servers.md) |Consiglia di attivare il controllo e il rilevamento delle minacce per i server di Azure SQL. (Solo servizio Azure SQL. Non include istanze di SQL in esecuzione nelle macchine virtuali.) |
| [Abilitare il controllo e il rilevamento delle minacce nei database SQL](security-center-enable-auditing-on-sql-databases.md) |Consiglia di attivare il controllo e il rilevamento delle minacce per i database SQL di Azure. (Solo servizio Azure SQL. Non include istanze di SQL in esecuzione nelle macchine virtuali.) |
| [Abilitare Transparent Data Encryption sui database SQL](security-center-enable-transparent-data-encryption.md) |Raccomanda di abilitare la crittografia per i database SQL (Solo servizio Azure SQL.) |
| [Abilita l'agente di macchine virtuali](security-center-enable-vm-agent.md) |Abilita agente VM di hello è toosee che richiedono che le macchine virtuali. Hello agente della macchina virtuale deve essere installato in macchine virtuali tooprovision patch l'analisi, l'analisi della linea di base e i programmi antimalware. Hello agente VM viene installato per impostazione predefinita per le macchine virtuali distribuite da hello Azure Marketplace. articolo Hello [agente VM ed estensioni-parte 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) vengono fornite informazioni su come tooinstall hello agente della macchina virtuale. |
| [Applicare Crittografia dischi](security-center-apply-disk-encryption.md) |Suggerisce di crittografare i dischi delle macchine virtuali con Crittografia dischi di Azure (VM Windows e Linux). La crittografia è consigliabile per hello del sistema operativo e i volumi di dati di una macchina virtuale. |
| [Specificare dettagli del contatto per la sicurezza](security-center-provide-security-contact-details.md) |Suggerisce di specificare le informazioni di contatto per la sicurezza per ogni sottoscrizione. Le informazioni di contatto sono un indirizzo di posta elettronica e un numero di telefono. informazioni Hello sono toocontact usato se il team di sicurezza rileva che le risorse vengano compromesse. |
| [Aggiornare la versione sistema operativo](security-center-update-os-version.md) |Consiglia di aggiornare versione di hello del sistema operativo (sistema operativo) per il servizio Cloud toohello più recente disponibile per la famiglia di sistemi operativi.  toolearn ulteriori informazioni sui servizi Cloud, vedere hello [Cenni preliminari sui servizi Cloud](../cloud-services/cloud-services-choose-me.md). |
| [La valutazione della vulnerabilità non è installata](security-center-vulnerability-assessment-recommendations.md) |Consiglia di installare una soluzione di valutazione della vulnerabilità nella VM. |
| [Correggi le vulnerabilità](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Consente le vulnerabilità di sistema e dell'applicazione toosee rilevate dalla soluzione di valutazione delle vulnerabilità hello installato nella macchina virtuale. |
| [Abilitare la crittografia per l'account di archiviazione di Azure](security-center-enable-encryption-for-storage-account.md) | Consiglia di abilitare la crittografia del servizio Archiviazione di Azure per i dati inattivi Crittografia del servizio di archiviazione (SSE) funziona mediante la crittografia dei dati di hello quando ne viene scritto archiviazione tooAzure e li decrittografa prima di recupero. SSE è attualmente disponibile solo per hello servizio Blob di Azure e può essere utilizzato per i BLOB in blocchi, BLOB di pagine e BLOB di aggiunta. vedere, più toolearn [la crittografia del servizio di archiviazione per i dati inattivi](../storage/common/storage-service-encryption.md).</br>La crittografia del servizio Archiviazione di Azure è supportata solo negli account di archiviazione di Resource Manager. |

È possibile filtrare ed eventualmente ignorare le raccomandazioni.

1. Selezionare **filtro** su hello **indicazioni** blade. Hello **filtro** pannello apre e si selezionano i valori di gravità e lo stato hello desiderato toosee.

    ![Filtrare le raccomandazioni][2]
2. Se si determina che una raccomandazione non è applicabile, è possibile ignorare una raccomandazione hello e filtrare la visualizzazione. Esistono due modi toodismiss una raccomandazione. Unidirezionale è tooright fare clic su un elemento e quindi selezionare **Dismiss**. Hello altri toohover su un elemento, fare clic su punti hello tre che appaiono toohello destra e quindi selezionano **Dismiss**. È possibile visualizzare le raccomandazioni ignorate facendo clic su **Filtro** e scegliendo **Ignorato**.

    ![Ignorare una raccomandazione][3]

### <a name="apply-recommendations"></a>Applicare le raccomandazioni
Dopo aver esaminato tutte le raccomandazioni, decidere quale applicare per prima. È consigliabile utilizzare gravità hello come hello parametro principale tooevaluate le indicazioni devono essere applicati per primo.

Nella tabella hello delle raccomandazioni descritte in precedenza, selezionare un'indicazione e seguirlo come un esempio di come tooapply una raccomandazione.

## <a name="next-steps"></a>Passaggi successivi
In questo documento è stato toosecurity introdotte indicazioni del Centro sicurezza PC. toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) , informazioni come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) : informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) , informazioni come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.

<!--Image references-->
[1]: ./media/security-center-recommendations/recommendations-tile.png
[2]: ./media/security-center-recommendations/filter-recommendations.png
[3]: ./media/security-center-recommendations/dismiss-recommendations.png
