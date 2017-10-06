---
title: aaaAzure Centro sicurezza PC e Linux virtuali in Azure | Documenti Microsoft
description: Informazioni sulla sicurezza per macchine virtuali Linux in Azure con il Centro sicurezza di Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/07/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7aa0de35fb311457e769f152c8575ec43e41c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a>Monitorare la sicurezza delle macchine virtuali con il Centro sicurezza di Azure

Il Centro sicurezza di Azure consente di ottenere visibilità nelle procedure per la sicurezza delle risorse di Azure. Il Centro sicurezza offre il monitoraggio della sicurezza integrato. Consente di rilevare minacce che altrimenti non verrebbero rilevate. Questa esercitazione illustra il Centro sicurezza di Azure e come:
 
> [!div class="checklist"]
> * configurare la raccolta dei dati
> * configurare i criteri di sicurezza
> * visualizzare e risolvere i problemi di integrità della configurazione
> * esaminare le minacce rilevate  

## <a name="security-center-overview"></a>Panoramica del Centro sicurezza di Azure

Il Centro sicurezza aiuta a identificare i potenziali problemi di configurazione e le minacce specifiche alla sicurezza delle macchina virtuale. Questi possono includere macchine virtuali mancanti dei gruppi di sicurezza di rete, dischi non crittografati e attacchi di forza bruta Remote Desktop Protocol (RDP). Hello informazioni vengono visualizzate nel dashboard di Centro sicurezza PC hello nei grafici di facile lettura.

tooaccess hello dashboard Centro sicurezza PC, nel portale di Azure, dal menu di hello, seleziona hello **Centro sicurezza PC**. Nel dashboard di hello, può visualizzare hello integrità di protezione dell'ambiente Azure, trovare un conteggio dei consigli correnti e hello lo stato corrente degli avvisi di minaccia di visualizzazione. È possibile espandere ogni toosee grafico di alto livello dettaglio.

![Dashboard del Centro sicurezza](./media/tutorial-azure-security/asc-dash.png)

Centro sicurezza PC va oltre indicazioni tooprovide di individuazione dati per i problemi rilevati. Ad esempio, se una macchina virtuale è stata distribuita senza un gruppo di sicurezza di rete collegato, il Centro sicurezza consente di visualizzare una raccomandazione, con una procedura di correzione da eseguire. Monitoraggio e aggiornamento automatizzato viene visualizzato senza uscire da contesto hello del Centro sicurezza PC.  

![Raccomandazioni](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a>configurare la raccolta dei dati

Prima di poter ottenere visibilità in configurazioni di protezione VM, è necessario tooset Centro sicurezza PC la raccolta dei dati. Ciò comporta l'abilitazione della raccolta di dati e la creazione di un account di archiviazione di Azure toohold raccolti dati. 

1. Nel dashboard del Centro sicurezza PC hello, fare clic su **criteri di sicurezza**, quindi selezionare la sottoscrizione. 
2. Per **Raccolta di dati** selezionare **On** (Abilitata).
3. Selezionare un account di archiviazione, toocreate **scegliere un account di archiviazione**. Quindi selezionare **OK**.
4. In hello **criteri di sicurezza** pannello seleziona **salvare**. 

agente di raccolta dati di Hello Centro sicurezza PC viene installato in tutte le macchine virtuali e inizi la raccolta dei dati. 

## <a name="set-up-a-security-policy"></a>Configurare un criterio di sicurezza

Criteri di sicurezza sono elementi di hello toodefine utilizzato per il quale il Centro sicurezza PC raccoglie i dati e fornisce consigli. È possibile applicare set toodifferent criteri di sicurezza diversi di risorse di Azure. Sebbene per impostazione predefinita le risorse di Azure vengono valutate per tutti gli elementi dei criteri, è possibile disattivare gli elementi di criteri individuali per tutte le risorse di Azure o per un gruppo di risorse. Per informazioni approfondite sui criteri di sicurezza del Centro sicurezza, vedere [Impostare i criteri di sicurezza nel Centro sicurezza di Azure](../../security-center/security-center-policies.md). 

tooset i criteri di sicurezza per tutte le risorse di Azure:

1. Nel dashboard del Centro sicurezza PC hello, selezionare **criteri di sicurezza**, quindi selezionare la sottoscrizione.
2. Selezionare **Prevention policy** (Criteri di protezione).
3. Attivare o disattivare gli elementi dei criteri che si desidera tooapply tooall risorse di Azure.
4. Al termine della selezione delle impostazioni, selezionare **OK**.
5. In hello **criteri di sicurezza** pannello seleziona **salvare**. 

tooset i criteri per un determinato gruppo di risorse:

1. Nel dashboard del Centro sicurezza PC hello, selezionare **criteri di sicurezza**, quindi selezionare un gruppo di risorse.
2. Selezionare **Prevention policy** (Criteri di protezione).
3. Attivare o disattivare gli elementi dei criteri che si desidera tooapply toohello gruppo di risorse.
4. In **EREDITARIETÀ** selezionare **Univoco**.
5. Al termine della selezione delle impostazioni, selezionare **OK**.
6. In hello **criteri di sicurezza** pannello seleziona **salvare**.  

È anche possibile disattivare la raccolta dei dati per un gruppo di risorse specifico in questa pagina.

Nell'esempio seguente di hello, un criterio univoco è stato creato per un gruppo di risorse denominato *myResoureGroup*. In questi criteri sono state disabilitate le raccomandazioni relative alla crittografia del disco e al firewall dell'applicazione Web.

![Criteri univoci](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a>Visualizzare lo stato della configurazione delle VM

Dopo aver attivato la raccolta dei dati e impostare un criterio di sicurezza, il Centro sicurezza PC inizia indicazioni e tooprovide avvisi. Come vengono distribuite le macchine virtuali, è installato l'agente di raccolta dati hello. Centro sicurezza PC viene quindi popolato con i dati per hello nuove macchine virtuali. Per informazioni dettagliate sullo stato di configurazione delle macchine virtuali, vedere [Protezione delle macchine virtuali nel Centro sicurezza di Azure](../../security-center/security-center-virtual-machine-recommendations.md). 

Come vengono raccolti i dati vengono aggregati integrità delle risorse hello per ogni macchina virtuale e le risorse di Azure correlate. Hello informazioni vengono visualizzate in un grafico di facile lettura. 

integrità delle risorse tooview:

1.  Nel dashboard del Centro sicurezza PC hello, in **integrità delle risorse di sicurezza**selezionare **calcolo**. 
2.  In hello **calcolo** pannello seleziona **macchine virtuali**. Questa visualizzazione fornisce un riepilogo dello stato di configurazione hello per tutte le macchine virtuali.

![Stato del calcolo](./media/tutorial-azure-security/compute-health.png)

toosee tutte le indicazioni per una macchina virtuale, selezionare hello macchina virtuale. Risoluzione di problemi e suggerimenti sono descritte più dettagliatamente nella sezione successiva di hello di questa esercitazione.

## <a name="remediate-configuration-issues"></a>Risolvere i problemi di configurazione

Dopo l'avvio di Centro sicurezza PC toopopulate con dati di configurazione, raccomandazioni in base ai criteri di sicurezza hello impostati. Se una macchina virtuale è stata configurata senza un gruppo di sicurezza di rete associati, ad esempio, un'indicazione è toocreate uno. 

toosee un elenco di tutte le indicazioni: 

1. Nel dashboard del Centro sicurezza PC hello, selezionare **indicazioni**.
2. Selezionare una raccomandazione specifica. Viene visualizzato un elenco di tutte le risorse per cui si applica l'indicazione di hello.
3. tooapply una raccomandazione, selezionare una risorsa specifica. 
4. Seguire le istruzioni di hello per la procedura di correzione. 

In molti casi, il Centro sicurezza PC viene descritta la procedura che è possibile eseguire una raccomandazione tooaddress senza uscire da Centro sicurezza PC. Nell'esempio seguente di hello, Centro sicurezza PC rileva un gruppo di sicurezza di rete con una regola in entrata senza restrizioni. Nella pagina di raccomandazione hello, è possibile selezionare hello **modificare le regole in entrata** pulsante. verrà visualizzata la finestra di Hello dell'interfaccia utente che è necessario toomodify hello regola. 

![Raccomandazioni](./media/tutorial-azure-security/remediation.png)

Le raccomandazioni risolte vengono contrassegnate come tali. 

## <a name="view-detected-threats"></a>Visualizzare le minacce rilevate

Inoltre consigli sulla configurazione di tooresource, centro di sicurezza consente di visualizzare gli avvisi di rilevamento minacce. funzionalità degli avvisi di sicurezza Hello aggrega i dati raccolti da ogni macchina virtuale, i log di rete di Azure e partner connesso soluzioni toodetect minacce per la sicurezza contro le risorse di Azure. Per informazioni dettagliate sulle funzionalità di rilevamento delle minacce nel Centro sicurezza, vedere [Funzionalità di rilevamento del Centro sicurezza di Azure](../../security-center/security-center-detection-capabilities.md).

funzionalità degli avvisi di sicurezza Hello richiede il Centro sicurezza PC hello prezzi toobe livello aumentato da *libero* troppo*Standard*. 30 giorni **versione di valutazione gratuita** è disponibile quando si sposta toothis maggiore livello di prezzo. 

livello di prezzo hello toochange:  

1. Nel dashboard del Centro sicurezza PC hello, fare clic su **criteri di sicurezza**, quindi selezionare la sottoscrizione.
2. Selezionare **Piano tariffario**.
3. Selezionare il nuovo livello di hello, quindi **selezionare**.
4. In hello **criteri di sicurezza** pannello seleziona **salvare**. 

Dopo aver modificato hello a livello di prezzo, grafico gli avvisi di sicurezza hello inizia toopopulate quando vengono rilevati minacce alla sicurezza.

![Avvisi di sicurezza](./media/tutorial-azure-security/security-alerts.png)

Selezionare un avviso tooview informazioni. Ad esempio, è possibile visualizzare una descrizione del rischio di hello, ora del rilevamento hello, tutti i tentativi di minaccia e hello correzione consigliata. Nell'esempio seguente di hello, è stato rilevato un attacco di forza bruta RDP, con 294 tentativi non riusciti RDP. Viene indicata una risoluzione consigliata.

![Attacco RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione viene configurato il Centro sicurezza di Azure e vengono quindi esaminate le macchine virtuali nel Centro sicurezza. Si è appreso come:

> [!div class="checklist"]
> * configurare la raccolta dei dati
> * configurare i criteri di sicurezza
> * visualizzare e risolvere i problemi di integrità della configurazione
> * esaminare le minacce rilevate

Avanzamento toohello successivo dell'esercitazione toolearn ulteriori informazioni sulla creazione di un elemento di configurazione/CD pipeline con Jenkins, GitHub e Docker.

> [!div class="nextstepaction"]
> [Creare un'infrastruttura di integrazione continua e di distribuzione continua con Jenkins, GitHub e Docker](tutorial-jenkins-github-docker-cicd.md)

