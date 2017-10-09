---
title: ricerche di gruppi aaaComputer Log Analitica log | Documenti Microsoft
description: "I gruppi di computer nel Log Analitica consentono tooscope log ricerche tooa particolare set di computer.  Questo articolo descrive i diversi metodi hello è possibile utilizzare gruppi di computer toocreate e come toouse in un log di ricerca."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a28b9e8a-6761-4ead-aa61-c8451ca90125
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 7dafea9829e541f5582a1d855fafb82aa4d94430
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="computer-groups-in-log-analytics-log-searches"></a>Gruppi di computer nelle ricerche nei log in Log Analytics

>[!NOTE]
> Questo articolo descrive utilizzare hello di gruppi di Computer usando il linguaggio di query hello corrente Anayltics Log.    Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi i gruppi di Computer di lavoro in modo diverso.  Note vengono fornite in questo articolo con una sintassi diversa hello e il comportamento per il nuovo linguaggio di query hello.  


Gruppi di computer in Analitica Log consentono di tooscope [log ricerche](log-analytics-log-searches.md) tooa particolare set di computer.  Ogni gruppo viene popolato con i computer usando una query definita dall'utente oppure importando gruppi da diverse origini.  Quando il gruppo di hello è inclusa in una ricerca log, i risultati di hello sono toorecords limitato che corrispondono a computer hello hello gruppo.

## <a name="creating-a-computer-group"></a>Creazione di un gruppo di computer
È possibile creare un gruppo di computer nel Log Analitica utilizzando uno dei metodi di hello in hello nella tabella seguente.  Nelle sezioni hello riportato di seguito vengono forniti dettagli su ogni metodo. 

| Metodo | Descrizione |
|:--- |:--- |
| Ricerca log |Creare una ricerca di log che restituisce un elenco di computer e salvare i risultati di hello di un gruppo di computer. |
| API di ricerca nei log |Utilizzare hello API di ricerca Log tooprogrammatically creare un gruppo di computer in base ai risultati di hello di una ricerca di log. |
| Active Directory |Analizza automaticamente l'appartenenza al gruppo hello dei computer agente che sono membri di un dominio Active Directory e creare un gruppo in Analitica di Log per ogni gruppo di sicurezza. |
| WSUS |Analizzare automaticamente i server o i client WSUS per rilevare i gruppi di destinazione e creare in Log Analytics un gruppo per ognuno. |

### <a name="log-search"></a>Ricerca log
Gruppi di computer creati da una ricerca di Log contengono tutti i computer hello restituiti da una query di ricerca definiti.  Questa query viene eseguita ogni volta che viene utilizzato il gruppo di computer hello in modo da rispecchiare le modifiche perché è stato creato il gruppo di hello.

Utilizzare hello seguendo procedure toocreate un gruppo di computer da una ricerca di log.

1. [Creare una ricerca nei log](log-analytics-log-searches.md) che restituisca un elenco di computer.  Hello ricerca deve restituire un set distinto di computer con un risultato simile **Computer distinti** o **measure Count () dal Computer** nella query hello.  
2. Fare clic su hello **salvare** pulsante in alto hello hello.
3. Selezionare **Sì** troppo**salvare la query come un gruppo di computer**.
4. Digitare un **nome** e **categoria** per il gruppo di hello.  Se una ricerca con hello stesso nome e la categoria già esiste, sono toooverwrite richiesto è.  È possibile avere più ricerche con hello stesso nome in categorie diverse. 

Di seguito sono riportate ricerche di esempio che è possibile salvare come gruppo di computer.

    Computer="Computer1" OR Computer="Computer2" | distinct Computer 
    Computer=*srv* | measure count() by Computer

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md) quindi hello sono modifiche seguenti apportate toohello procedura toocreate un nuovo gruppo di computer.
>  
> - Hello toocreate query deve includere un gruppo di computer `distinct Computer`.  Ecco un esempio di un toocreate query un gruppo di computer.<br>`Heartbeat | where Computer contains "srv" `
> - Quando si crea un nuovo gruppo di computer, è necessario specificare un alias nel nome toohello aggiunta.  Utilizzare alias di hello quando si utilizza il gruppo di computer hello in una query, come descritto di seguito.  

### <a name="log-search-api"></a>API di ricerca nei log
Gruppi di computer creati con l'API di ricerca Log vengono hello hello stesso come ricerche create con una ricerca di Log.

Per ulteriori informazioni sulla creazione di un gruppo di computer utilizzando l'API di ricerca Log hello vedere [API REST di ricerca di gruppi di Computer nel registro eventi di Log Analitica](log-analytics-log-search-api.md#computer-groups).

### <a name="active-directory"></a>Active Directory
Quando si configura l'appartenenza al gruppo Active Directory di Log Analitica tooimport, analizza l'appartenenza al gruppo hello di qualsiasi computer aggiunto a un dominio con l'agente OMS hello.  Viene creato un gruppo di computer in Analitica di Log per ogni gruppo di sicurezza in Active Directory, e ogni computer viene aggiunto toohello gruppi di computer sono membri di gruppi di sicurezza di toohello corrispondente.  L'appartenenza viene aggiornata continuamente ogni 4 ore.  

Configurare gruppi di sicurezza di Active Directory Log Analitica tooimport da hello **gruppi di Computer** dal menu Registro Analitica **impostazioni**.  Selezionare **Automazione** e quindi **Importa le appartenenze a gruppi di Active Directory dai computer**.  Non è richiesta alcuna ulteriore configurazione.

![Gruppi di computer da Active Directory](media/log-analytics-computer-groups/configure-activedirectory.png)

Quando i gruppi siano stati importati, hello menu elenchi hello numero di computer con l'appartenenza al gruppo rilevato e numero di gruppi importati hello.  È possibile fare clic su uno di questi hello tooreturn collegamenti **ComputerGroup** i record con queste informazioni.

### <a name="windows-server-update-service"></a>Windows Server Update Service
Quando si configura Log Analitica tooimport WSUS appartenenza ai gruppi, che analizza hello come destinazione l'appartenenza al gruppo di qualsiasi computer con l'agente OMS hello.  Se si utilizza sul lato client come destinazione, qualsiasi computer connesso tooOMS e fa parte di qualsiasi WSUS gruppi di destinazione è l'appartenenza al gruppo importato tooLog Analitica. Se si utilizza sul lato server come destinazione, hello OMS deve essere installato l'agente hello WSUS server affinché toobe informazioni l'appartenenza al gruppo di hello importati tooOMS.  L'appartenenza viene aggiornata continuamente ogni 4 ore. 

Configurare gruppi di sicurezza di Active Directory Log Analitica tooimport da hello **gruppi di Computer** dal menu Registro Analitica **impostazioni**.  Selezionare **Active Directory** e quindi **Importa le appartenenze a gruppi di Active Directory dai computer**.  Non è richiesta alcuna ulteriore configurazione.

![Gruppi di computer da Active Directory](media/log-analytics-computer-groups/configure-wsus.png)

Quando i gruppi siano stati importati, hello menu elenchi hello numero di computer con l'appartenenza al gruppo rilevato e numero di gruppi importati hello.  È possibile fare clic su uno di questi hello tooreturn collegamenti **ComputerGroup** i record con queste informazioni.

## <a name="managing-computer-groups"></a>Gestione dei gruppi di computer
È possibile visualizzare i gruppi di computer creati da una ricerca di log o hello API di ricerca Log da hello **gruppi di Computer** dal menu Registro Analitica **impostazioni**.  Fare clic su hello **x** in hello **rimuovere** gruppo di computer hello toodelete di colonna.  Fare clic su hello **visualizzare membri** icona per la ricerca di log del gruppo di hello toorun gruppo che restituisce i relativi membri. 

![Gruppi di computer salvati](media/log-analytics-computer-groups/configure-saved.png)

hello toomodify gruppo, creare un nuovo gruppo con hello stesso **categoria** e **nome** toooverwrite gruppo originale di hello.

## <a name="using-a-computer-group-in-a-log-search"></a>Uso di un gruppo di computer in una ricerca nei log
Utilizzare hello seguente gruppo di computer tooa toorefer sintassi in una ricerca di log.  Se si specifica hello **categoria** è facoltativo e solo obbligatorio se si dispone di gruppi di computer con hello stesso nome in categorie diverse. 

    $ComputerGroups[Category: Name]

Quando viene eseguita una ricerca, vengono risolte innanzitutto i membri di gruppi di computer inclusi nella ricerca hello hello.  Se il gruppo di hello è basato su una ricerca log, la ricerca viene eseguita membri hello tooreturn del gruppo di hello prima di eseguire una ricerca nei log di primo livello hello.

Gruppi di computer sono in genere utilizzati con hello **IN** clausola nella ricerca nei log hello come hello di esempio seguente:

    Type=UpdateSummary Computer IN $ComputerGroups[My Computer Group]

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), utilizzare un gruppo di Computer in una query per trattare il relativo alias come una funzione come hello di esempio seguente:
> 
>  `UpdateSummary | where Computer IN (MyComputerGroup)`

## <a name="computer-group-records"></a>Record dei gruppi di computer
Viene creato un record nel repository OMS hello ogni appartenenza al gruppo di computer creato da Active Directory o Windows Server Update Services.  Questi record dispongono di un tipo di **ComputerGroup** e dispone di proprietà hello in hello nella tabella seguente.  Per i gruppi di computer basati su ricerche nei log non vengono creati record.

| Proprietà | Descrizione |
|:--- |:--- |
| Tipo |*ComputerGroup* |
| SourceSystem |*SourceSystem* |
| Computer |Nome del computer membro di hello. |
| Gruppo |Nome del gruppo di hello. |
| GroupFullName |Gruppo toohello percorso completo incluso origine hello e il nome di origine. |
| GroupSource |Origine da cui il gruppo è stato raccolto. <br><br>ActiveDirectory<br>WSUS<br>WSUSClientTargeting |
| GroupSourceName |Nome dell'origine hello che hello gruppo sono stati raccolti da.  Per Active Directory, questo è il nome di dominio di hello. |
| ManagementGroupName |Nome del gruppo di gestione di hello per gli agenti SCOM.  Per gli altri agenti, corrisponde ad AOI-\<ID area di lavoro\> |
| TimeGenerated |Gruppo di computer hello data e ora è stato creato o aggiornato. |

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni.  

