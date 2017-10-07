---
title: aaaUse Azure Backup tooreplace infrastruttura nastro | Documenti Microsoft
description: Informazioni su come Backup di Azure fornisce semantica simile a nastro che consente di toobackup e ripristinare i dati in Azure
services: backup
documentationcenter: 
author: trinadhk
manager: vijayts
editor: 
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4c5b095d95d39267c54b1eed9427bda09658bb94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a>Spostare lo spazio di archiviazione a lungo termine da nastro toohello cloud di Azure
I clienti di Backup di Azure e System Center Data Protection Manager possono eseguire le attività seguenti:

* Eseguire il backup dei dati nelle pianificazioni che più adatto alle proprie esigenze organizzative hello.
* Dati di backup hello vengono conservati per periodi più lunghi
* Includere Azure nelle strategie di conservazione dei dati a lungo termine, in alternativa al backup su nastro.

Questo articolo illustra come abilitare i criteri di backup e di conservazione. I clienti che utilizzano i nastri tooaddress lungo-termine-conservarli deve ora disponibile un'alternativa potente e affidabile con disponibilità hello di questa funzionalità. Hello è attivata nella versione più recente di hello di hello Azure Backup (disponibile [qui](http://aka.ms/azurebackup_agent)). I clienti di System Center Data Protection Manager è necessario aggiornare, almeno DPM 2012 R2 UR5 prima di utilizzare DPM con hello servizio Backup di Azure.

## <a name="what-is-hello-backup-schedule"></a>Che cos'è hello pianificazione Backup?
pianificazione del backup Hello indica la frequenza di hello hello operazione di backup. Ad esempio, le impostazioni di hello nella seguente schermata hello indicano che i backup vengono eseguiti ogni giorno alle 6 pm e a mezzanotte.

![Pianificazione giornaliera](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

I clienti possono anche pianificare un backup settimanale. Ad esempio, hello impostazioni nella seguente schermata hello indicano che i backup vengono eseguiti ogni alternativo domenica & mercoledì 9.30 e 1:00 AM.

![Pianificazione settimanale](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a>Che cos'è hello criteri di conservazione?
criteri di conservazione Hello specificano durata hello per cui devono essere archiviati i backup hello. Anziché specificare solo un criterio"semplice" per tutti i punti di backup, i clienti possono specificare criteri di conservazione diversi in base a quando viene eseguito il backup di hello. Hello punto di backup eseguito ogni giorno, che funge da un punto di ripristino operativo, ad esempio, viene mantenuto per 90 giorni. punto di backup Hello eseguita alla fine hello ogni trimestre per scopi di controllo viene mantenuto per una durata.

![Criteri di conservazione](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

Hello numero totale di "punti di conservazione" specificato in questo criterio è 90 (giornalieri punti) + 40 (uno ogni trimestre per 10 anni) = 130.

## <a name="example--putting-both-together"></a>Esempio: Uso di entrambi i metodi
![Schermata di esempio](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. **Criteri di mantenimento giornaliero**: i backup eseguiti quotidianamente vengono archiviati per sette giorni.
2. **Criteri di conservazione settimanale**: i backup eseguiti ogni giorno a mezzanotte e ogni sabato alle 18.00 verranno conservati per quattro settimane
3. **Criteri di conservazione mensile**: vengono conservati i backup eseguiti a mezzanotte e 6 pm hello ultima domenica di ogni mese per 12 mesi
4. **Criteri di conservazione annuale**: i backup eseguiti alla mezzanotte hello ultima domenica di ogni marzo vengono conservati per 10 anni

numero totale di "punti di conservazione" Hello (punti da cui un cliente può ripristinare i dati) in hello diagramma precedente viene calcolata come segue:

* due punti al giorno per sette giorni = 14 punti di ripristino
* due punti a settimana per quattro settimane = 8 punti di ripristino
* due punti al mese per 12 mesi = 24 punti di ripristino
* un punto all'anno per 10 anni = 10 punti di ripristino

numero totale di Hello dei punti di ripristino è 56.

> [!NOTE]
> Il backup di Azure non dispone di una restrizione sul numero di punti di ripristino.
>
>

## <a name="advanced-configuration"></a>Configurazione avanzata
Fare clic su **modifica** nella precedente schermata di hello, sono dotate di ulteriore flessibilità nello specificare pianificazioni di conservazione.

![Modifica](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sul Backup di Azure vedere:

* [Introduzione tooAzure Backup](backup-introduction-to-azure-backup.md)
* [Valutazione di Backup di Azure](backup-try-azure-backup-in-10-mins.md)
