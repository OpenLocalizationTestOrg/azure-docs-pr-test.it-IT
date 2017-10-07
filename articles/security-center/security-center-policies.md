---
title: criteri di sicurezza aaaSet Centro sicurezza di Azure | Documenti Microsoft
description: Questo documento consente di criteri di sicurezza tooconfigure Centro sicurezza di Azure.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3b9e1c15-3cdb-4820-b678-157e455ceeba
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: yurid
ms.openlocfilehash: 59226dd84a1c66a2d8367417060ab10a1ff73848
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-security-policies-in-azure-security-center"></a>Impostare i criteri di sicurezza nel Centro sicurezza di Azure
Questo documento consente di criteri di sicurezza tooconfigure in Centro sicurezza PC mostrando hello necessarie tooperform questa attività.

>[!NOTE] 
>A partire da anticipata giugno 2017, il Centro sicurezza PC utilizza toocollect e l'archivio dati di Microsoft Monitoring Agent di hello. Vedere [migrazione della piattaforma Azure sicurezza Center](security-center-platform-migration.md) toolearn altre. informazioni di Hello in questo articolo rappresentano funzionalità Centro sicurezza dopo la transizione toohello Microsoft Monitoring Agent.
>

## <a name="what-are-security-policies"></a>Informazioni sui criteri di sicurezza
Un criterio di sicurezza definisce il set di hello dei controlli, sono consigliate per le risorse all'interno di hello specificato sottoscrizione. Centro sicurezza PC, definire i criteri per le sottoscrizioni di Azure in base alle esigenze di sicurezza aziendale tooyour e tipo hello delle applicazioni o riservatezza dei dati di hello in ogni sottoscrizione.

Ad esempio, le risorse usate per lo sviluppo o il test possono avere requisiti di sicurezza diversi da quelli delle risorse usate per le applicazioni di produzione. In modo analogo, le applicazioni che usano dati regolamentati come le informazioni personali possono richiedere un maggiore livello di sicurezza. Criteri di sicurezza che sono abilitati nel monitoraggio toohelp è identificare potenziali vulnerabilità e ridurre i rischi e consigli sulla protezione di unità di Centro sicurezza di Azure. Lettura [Guida alle operazioni e la pianificazione del Centro protezione Azure](security-center-planning-and-operations-guide.md) per ulteriori informazioni su come opzione toodetermine hello sono appropriate.

## <a name="set-security-policies"></a>Impostare i criteri di sicurezza
È possibile configurare criteri di sicurezza per ogni sottoscrizione. toomodify un criterio di sicurezza, è necessario essere un proprietario o collaboratore della sottoscrizione. Accedi al portale di Azure toohello e seguire hello successivi passaggi dei criteri di protezione tooconfigure in Centro sicurezza:

1. Fare clic su hello **criteri** riquadro nel dashboard di hello Centro sicurezza PC.
2. Nel pannello dei criteri di sicurezza hello visualizzata, selezionare sottoscrizione hello in cui si desidera che Criteri di sicurezza tooenable hello.

    ![Definizione dei criteri](./media/security-center-policies/security-center-policies-fig1-ga.png)
3. Hello **criteri di sicurezza** pannello per sottoscrizione hello selezionata verrà visualizzata con un set di opzioni. Hello opzioni disponibili in questo pannello sono:

   * **Criteri di prevenzione**: usare i criteri di tooconfigure questa opzione per ogni sottoscrizione.  
   * **Notifica tramite posta elettronica**: utilizzare questo tooconfigure opzione una notifica di posta elettronica viene inviata su hello prima giornaliero occorrenza di un avviso e per gli avvisi di livello di gravità elevato. Le preferenze di posta elettronica possono essere configurate solo per i criteri della sottoscrizione. Lettura [fornire dettagli di contatto di sicurezza nel Centro protezione Azure](security-center-provide-security-contact-details.md) per ulteriori informazioni su come tooconfigure notifiche di posta elettronica.
   * **Livello di prezzo**: utilizzare questo hello tooupgrade opzione dei prezzi di selezione. Vedere [Centro sicurezza PC prezzi](security-center-pricing.md) toolearn più sui prezzi di opzioni.
4. Verificare che l'opzione **Raccogli dati dalle macchine virtuali** sia **Sì**. Questa opzione Abilita la raccolta automatica dei registri per le risorse nuove ed esistenti utilizzando Microsoft Monitoring Agent hello: si tratta dello stesso agente usato dal servizio di Operations Management Suite e Log Analitica hello hello. Dati raccolti dall'agente sono archiviati in un workspace Analitica Log esistenti associati alla sottoscrizione di Azure o in un nuovo aree di lavoro, tenendo geography hello account di hello macchina virtuale.

5. In hello **criteri di sicurezza** pannello, fare clic su **criteri di prevenzione** toosee hello opzioni disponibili. Fare clic su **su** tooenable hello consigli relativi alla sicurezza sono rilevanti per questa sottoscrizione.

    ![Selezionare i criteri di sicurezza hello](./media/security-center-policies/security-center-policies-fig7.png)

Ogni opzione hello come toounderstand un riferimento nella tabella seguente:

| Criteri | Quando lo stato è Sì |
| --- | --- |
| Aggiornamenti del sistema |Recupera un elenco giornaliero degli aggiornamenti della sicurezza e critici da Windows Update o da Windows Server Update Services. elenco recuperato Hello dipende dal servizio di hello è configurato per tale macchina virtuale e si consiglia di applicare gli aggiornamenti mancanti hello. Per i sistemi Linux, il criterio di hello utilizza hello pacchetti forniti distro gestione sistema toodetermine pacchetti con aggiornamenti disponibili. Controlla anche la presenza di aggiornamenti critici e della sicurezza dalle macchine virtuali di [Servizi cloud di Azure](../cloud-services/cloud-services-how-to-configure.md). |
| Vulnerabilità del sistema operativo |Analizza le configurazioni giornaliero toodetermine problemi del sistema operativo che potrebbe rendere vulnerabile tooattack di hello macchina virtuale. criteri Hello consiglia anche tooaddress modifiche di configurazione di queste vulnerabilità. Vedere hello [elenco delle linee di base consigliati](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335) per ulteriori informazioni sulle configurazioni specifiche hello che vengono monitorati. (Al momento, Windows Server 2016 non è completamente supportato.) |
| Endpoint Protection |Si consiglia di endpoint protection toobe effettuato il provisioning per tutte le macchine virtuali Windows toohelp identificare e rimuovere i virus, spyware e altro software dannoso. |
| Crittografia del disco |Si consiglia l'abilitazione della crittografia del disco in tutte le macchine virtuali tooenhance la protezione dei dati inattivi. |
| Gruppi di sicurezza di rete |Consiglia [gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md) essere toocontrol configurata in ingresso e in uscita traffico tooVMs con gli endpoint pubblici. I gruppi di sicurezza di rete configurati per una subnet vengono ereditati da tutte le interfacce di rete della macchina virtuale se non diversamente specificato. Inoltre toochecking che sia stato configurato un gruppo di sicurezza di rete, questo criterio consente di valutare la sicurezza in ingresso tooidentify regole che consentano il traffico in ingresso. |
| Web application firewall |Si consiglia che un firewall applicazione web eseguirne il provisioning nelle macchine virtuali quando viene soddisfatta una delle seguenti hello: </br></br>[Indirizzo IP pubblico a livello di istanza](../virtual-network/virtual-networks-instance-level-public-ip.md) (ILPIP) viene usato e le regole di sicurezza in ingresso per gruppo di sicurezza di rete associato hello hello sono configurati tooallow accesso tooport 80/443.</br></br>IP con bilanciamento del carico viene utilizzato e hello associata a bilanciamento del carico e regole di rete in ingresso address translation (NAT) sono configurati tooallow accesso tooport 80/443. Per altre informazioni, vedere [Supporto di Azure Resource Manager per il servizio di bilanciamento del carico](../load-balancer/load-balancer-arm.md). |
| Firewall di nuova generazione |Estende le protezioni di rete oltre i gruppi di sicurezza di rete predefiniti di Azure. Centro sicurezza PC consente di individuare le distribuzioni per il quale un firewall generazione successivo, è consigliabile e abilitare si tooprovision appliance virtuale. |
| Servizio di controllo SQL e rilevamento delle minacce |Si consiglia che il controllo di accesso tooAzure Database abilitato per la conformità e anche avanzato di rilevamento minacce, per motivi di indagine. |
| Crittografia SQL |Consiglia l'abilitazione della crittografia dati inattivi per il database SQL di Azure, i backup associati e file di log delle transazioni. Anche se i dati vengono violati, non saranno leggibili. |
| Valutazione della vulnerabilità |Consiglia di installare una soluzione di valutazione della vulnerabilità nella VM. |
| Crittografia di archiviazione |Questa funzionalità è attualmente disponibile per BLOB di Azure e File di Azure. Dopo l'abilitazione della Crittografia del servizio di archiviazione verranno crittografati solo i nuovi dati, mentre i file già esistenti nell'account di archiviazione rimarranno non crittografati. |
| Accesso alla rete JIT |Quando è abilitata in-time, il Centro sicurezza PC protegge il traffico in entrata tooyour macchine virtuali di Azure tramite la creazione di una regola di gruppo. Selezionare le porte hello su hello VM toowhich deve essere bloccato il traffico in ingresso verso il basso. Per altre informazioni, vedere [Gestire l'accesso alle macchine virtuali con la funzionalità JIT (Just-in-Time)](https://docs.microsoft.com/azure/security-center/security-center-just-in-time). |

Dopo aver configurato tutte le opzioni, fare clic su **OK** in hello **criteri di sicurezza** pannello in cui sono presenti indicazioni hello e quindi fare clic su **salvare** in hello **sicurezza Criteri** pannello contenente le impostazioni iniziali hello.

> [!NOTE]
> livello di prezzo Hello è ancora applicabile per livello di gruppo di risorse hello. Per ulteriori informazioni, visitare hello [prezzi](https://azure.microsoft.com/pricing/details/security-center/) pagina.
>
>

## <a name="see-also"></a>Vedere anche
In questo documento, si è appreso come criteri di sicurezza tooconfigure Centro sicurezza di Azure. toolearn ulteriori informazioni su Centro sicurezza di Azure, vedere l'esempio hello:

* [Guida alla pianificazione e alla gestione del Centro sicurezza di Azure](security-center-planning-and-operations-guide.md). Informazioni su come tooplan e comprendere considerazioni sulla progettazione hello tooadopt Centro sicurezza di Azure.
* [Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md). Informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md). Informazioni su come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure](security-center-partner-solutions.md). Informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md). Trovare le domande frequenti sull'utilizzo del servizio hello.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/). Post di blog sulla sicurezza e sulla conformità di Azure.
