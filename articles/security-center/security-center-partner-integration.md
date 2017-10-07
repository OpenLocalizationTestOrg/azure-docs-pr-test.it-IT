---
title: integrazione di aaaPartner in Centro sicurezza di Azure | Documenti Microsoft
description: Informazioni su come Centro sicurezza di Azure si integra con i partner tooenhance sicurezza complessiva delle risorse di Azure.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 6af354da-f27a-467a-8b7e-6cbcf70fdbcb
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: 3621335730a076721cb3c23788a47be50aa8fc73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="partner-integration-in-azure-security-center"></a>Integrazione dei partner nel Centro sicurezza di Azure

In questo articolo viene descritto come Centro sicurezza di Azure si integra con i partner toohelp è migliorare la sicurezza complessiva. Centro sicurezza offre un'esperienza integrata in Azure e sfrutta hello Azure Marketplace per partner certificazione e fatturazione.

> [!NOTE] 
> A partire da giugno 2017, centro di sicurezza Usa toocollect e l'archivio dati di Microsoft Monitoring Agent di hello. Per altre informazioni, vedere [Migrazione della piattaforma del Centro sicurezza di Azure](security-center-platform-migration.md). informazioni di Hello in questo articolo rappresentano funzionalità Centro sicurezza dopo la transizione toohello Microsoft Monitoring Agent.
>

## <a name="why-deploy-partner-solutions-from-security-center"></a>Perché distribuire soluzioni partner dal Centro sicurezza

Integrazione con partner tooleverage motivi principali quattro in Centro sicurezza PC sono:

- **Facilità di distribuzione**. La distribuzione di una soluzione di partner dal seguente hello raccomandazione Centro sicurezza PC è molto più semplice. il processo di distribuzione Hello è possibile automatizzare completamente con una topologia di rete e il programma di installazione predefinito. In alternativa, i clienti possono scegliere un'opzione semi-automatizzata per ottenere un livello superiore di flessibilità e personalizzazione.
- **Rilevamenti integrati**. Gli eventi di sicurezza delle soluzioni partner vengono raccolti, aggregati e visualizzati automaticamente nell'ambito degli avvisi e degli eventi imprevisti del Centro sicurezza. Questi eventi vengono inoltre fusibile con rilevamenti da altre origini di tooprovide avanzate funzionalità di rilevamento minacce.
- **Gestione e monitoraggio dell'integrità unificati**. I clienti possono utilizzare toomonitor gli eventi di integrità integrata tutte le soluzioni di partner a colpo d'occhio. Gestione di base è disponibile, con il programma di installazione di un accesso semplice tooadvanced utilizzando hello partner soluzione.
- **Esportare tooSIEM**. I clienti possono esportare tutti Centro sicurezza PC e partner genera avvisi in comune sistemi di informazioni di sicurezza e gestione di eventi (SIEM) tooon locali evento formato (CEF) tramite l'integrazione di log di Azure (anteprima).


## <a name="partners-that-integrate-with-security-center"></a>Partner integrati con il Centro sicurezza

Il Centro sicurezza offre attualmente l'integrazione con le soluzioni seguenti:

- Protezione endpoint ([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html), Symantec e [Microsoft Antimalware per Servizi cloud e Macchine virtuali di Azure](https://docs.microsoft.com/azure/security/azure-security-antimalware)) 
- Web application firewall ([Barracuda](https://www.barracuda.com/products/webapplicationfirewall), [F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html), [Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF), [Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets) e [gateway applicazione di Azure](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/)) 
- Firewall di nuova generazione ([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/), [Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/), [Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2) e [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html)) 
- Valutazione della vulnerabilità ([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))  

Nel corso del tempo, il Centro sicurezza PC espandere numero hello di partner all'interno di queste categorie e aggiungere nuove categorie. 

## <a name="deploy-a-partner-solution"></a>Distribuire una soluzione partner

Il programma di installazione di hello dell'ambiente Azure e i criteri di sicurezza hello che è definito, il Centro sicurezza PC potrebbe consigliare che si distribuisce una soluzione di partner. Hello raccomandazione Centro sicurezza PC in modo semplificato il processo di hello di selezione e l'installazione di una soluzione di partner. Hello generale dell'esperienza di distribuzione potrebbe variare, in base al tipo hello della soluzione e i partner che si utilizza. Per ulteriori informazioni, vedere hello seguenti articoli:

- [Installare Endpoint Protection](security-center-install-endpoint-protection.md)
- [Aggiungere un Web Application Firewall](security-center-add-web-application-firewall.md)
- [Aggiungere un firewall di nuova generazione](security-center-add-next-generation-firewall.md)
- [La valutazione della vulnerabilità non è installata](security-center-vulnerability-assessment-recommendations.md)

## <a name="manage-partner-solutions"></a>Gestire le soluzioni partner

Dopo la distribuzione, tooview informazioni sulle hello integrità della soluzione hello e attività di gestione di base, sull'hello **Centro sicurezza PC** blade, seleziona hello **soluzioni Partner** opzione. Per altre informazioni sulla gestione delle soluzioni partner nel Centro sicurezza, leggere [Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure](security-center-partner-solutions.md).

![Integrazione dei partner](./media/security-center-partner-integration/security-center-partner-integration-fig1-new2.png)

> [!NOTE]
> Il supporto di Symantec endpoint protection è toodiscovery limitato. Non sono disponibili avvisi sull'integrità.
>

## <a name="see-also"></a>Vedere anche

In questo articolo è stato descritto come toointegrate partner soluzioni in Centro sicurezza di Azure. toolearn ulteriori informazioni su Centro di sicurezza, vedere hello seguenti articoli:

* [Guida alla pianificazione e alla gestione del Centro sicurezza di Azure](security-center-planning-and-operations-guide.md)
* [Gestire e rispondere toosecurity avvisi del Centro sicurezza PC](security-center-managing-and-responding-alerts.md)
* [Avvisi di sicurezza per tipo nel Centro sicurezza di Azure](security-center-alerts-type.md)
* [Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md). Informazioni su come toomonitor hello integrità delle risorse di Azure.
* [Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure](security-center-partner-solutions.md). Informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md). Ottenere risposte toofrequently domande frequenti sull'utilizzo del servizio hello.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/). Post di blog sulla sicurezza e sulla conformità di Azure.
