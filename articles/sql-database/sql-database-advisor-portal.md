---
title: consigli relativi alle prestazioni aaaApply - Database SQL di Azure | Documenti Microsoft
description: "È possibile utilizzare hello toofind portale Azure suggerimenti relativi alle prestazioni che è possibile ottimizzare le prestazioni del Database SQL di Azure o toocorrect un problema identificato nel carico di lavoro."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a>Trovare e applicare raccomandazioni per le prestazioni

È possibile utilizzare hello toofind portale Azure suggerimenti relativi alle prestazioni che è possibile ottimizzare le prestazioni del Database SQL di Azure o toocorrect un problema identificato nel carico di lavoro. **Indicazione delle prestazioni** pagina nel portale di Azure consente principale indicazioni in base a impatto potenziale hello toofind. 

## <a name="viewing-recommendations"></a>Visualizzazione delle raccomandazioni

tooview e applicare i consigli relativi alle prestazioni, è necessario hello corretto [controllo di accesso basato sui ruoli](../active-directory/role-based-access-control-what-is.md) autorizzazioni in Azure. **Lettore**, **collaboratore DB SQL** le autorizzazioni sono necessarie tooview indicazioni, e **proprietario**, **collaboratore DB SQL** sono necessarie le autorizzazioni tooexecute eventuali azioni; creare o eliminare gli indici e annullare la creazione dell'indice.

Consigli relativi alle prestazioni toofind i passaggi da utilizzare hello seguenti nel portale di Azure:

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Andare troppo**più servizi** > **database SQL**e selezionare il database.
3. Passare troppo**raccomandazione prestazioni** tooview le indicazioni disponibili per il database selezionato hello.

Consigli relativi alle prestazioni sono shonw in hello tabella simile toohello illustrato nella seguente illustrazione hello:

![Raccomandazioni](./media/sql-database-advisor-portal/recommendations.png)

Indicazioni vengono ordinate in base il potenziale impatto sulle prestazioni in hello seguenti categorie:

| Impatto | Descrizione |
|:--- |:--- |
| Alto |Indicazioni di alto impatto devono fornire l'impatto più significativo sulle prestazioni di hello. |
| Media |Le raccomandazioni a impatto medio devono migliorare le prestazioni, ma non sostanzialmente. |
| Basso |Le raccomandazioni a basso impatto devono offrire prestazioni migliori, ma i miglioramenti potrebbero non essere significativi. |


> [!NOTE]
> Database SQL di Azure richiede attività toomonitor almeno per un giorno in ordine tooidentify alcune raccomandazioni. Hello Database SQL di Azure può ottimizzare più facilmente modelli di query coerente anziché casuale irregolare picchi di attività. Se indicazioni non sono disponibili corrently, hello **raccomandazione prestazioni** pagina fornisce un messaggio che spiega il motivo.
> 

Inoltre, è possibile visualizzare lo stato di hello di operazioni storiche hello. Selezionare un suggerimento o lo stato di toosee ulteriori dettagli.

Di seguito è riportato un esempio di "Creazione dell'indice di" azione consigliata nell'hello portale di Azure.

![Creare un indice](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a>Applicazione delle raccomandazioni
Database SQL di Azure offre controllo completo su come indicazioni vengono abilitati usando una qualsiasi delle tre opzioni seguenti hello: 

* Applicare le singole indicazioni una alla volta.
* Abilita hello tooautomatically ottimizzazione automatica applica indicazioni.
* tooimplement un'indicazione di eseguire manualmente, hello consigliato script T-SQL nel database.

Selezionare qualsiasi tooview raccomandazione i dettagli e quindi fare clic su **visualizzare script** tooreview hello dettagli esatti di modalità di creazione di raccomandazione hello.

database Hello rimane online durante raccomandazione hello viene applicato, l'utilizzo di suggerimento di prestazioni o l'ottimizzazione automatica mai richiede un database offline.

### <a name="apply-an-individual-recommendation"></a>Applicare una singola indicazione
È possibile leggere e accettare le indicazioni una alla volta.

1. In hello **indicazioni** pannello, selezionare una raccomandazione.
2. In hello **dettagli** fare clic su pannello **applica** pulsante.
   
    ![Applica suggerimento](./media/sql-database-advisor-portal/apply.png)

Indicazione selezionata verrà applicata nel database di hello.

### <a name="removing-recommendations-from-hello-list"></a>Rimozione di indicazioni dall'elenco di hello
Se l'elenco di suggerimenti contiene elementi che si desidera tooremove dall'elenco di hello, è possibile ignorare l'indicazione di hello:

1. Selezionare una raccomandazione nell'elenco di hello di **indicazioni** dettagli hello tooopen.
2. Fare clic su **ignorare** su hello **dettagli** blade.

Se si desidera, è possibile aggiungere elementi eliminati, eseguire il backup toohello **indicazioni** elenco:

1. In hello **indicazioni** fare clic su pannello **visualizzazione scartati**.
2. Selezionare un elemento rimosso dall'hello elenco tooview i dettagli.
3. Facoltativamente, fare clic su **Annulla Elimina** tooadd hello indice toohello indietro elenco principale di **indicazioni**.


### <a name="enable-automatic-tuning"></a>Abilitare l'ottimizzazione automatica
È possibile impostare automaticamente indicazioni tooimplement di hello Database SQL di Azure. Man mano che le indicazioni vengono rese disponibili, verranno applicate automaticamente. Come con tutte le indicazioni gestite da hello servizio se l'impatto sulle prestazioni di hello è raccomandazione hello negativo verrà annullata.

1. In hello **indicazioni** pannello, fare clic su **automatizzare**:
   
    ![Impostazioni di Advisor](./media/sql-database-advisor-portal/settings.png)
2. Selezionare le azioni tooautomate:
   
    ![Indici consigliati](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a>Eseguire manualmente hello consigliato script T-SQL
Selezionare qualsiasi raccomandazione e quindi fare clic su **Visualizza script**. Eseguire questo script per il database toomanually applicare l'indicazione di hello.

*Gli indici che vengono eseguiti manualmente non monitorati e convalidati per verificarne l'impatto sulle prestazioni dal servizio hello* pertanto è consigliabile monitorare tali indici dopo la creazione tooverify forniscono i miglioramenti delle prestazioni e regolare o eliminarli se necessario. Per informazioni dettagliate sulla creazione di indici, vedere [CREAZIONE INDICE (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).

### <a name="canceling-recommendations"></a>Annullamento delle raccomandazioni
Le raccomandazioni con stato **In sospeso**, **Verifica** o **Operazione completata** possono essere annullate. Le raccomandazioni con stato **In esecuzione** non possono essere annullate.

1. Selezionare un'indicazione in hello **cronologia ottimizzazione** hello tooopen area **dettagli indicazioni** blade.
2. Fare clic su **Annulla** processo hello tooabort dell'applicazione hello dell'indicazione.

## <a name="monitoring-operations"></a>Monitoraggio delle operazioni
L'applicazione di un'indicazione potrebbe non avvenire in tempo reale. portale Hello fornisce informazioni dettagliate relative allo stato di hello della raccomandazione. di seguito Hello sono stati possibili di un indice di:

| Stato | Descrizione |
|:--- |:--- |
| In sospeso |Il comando di applicazione della raccomandazione è stato ricevuto ed è pianificato per l'esecuzione. |
| In esecuzione |indicazione di Hello viene applicata. |
| Verifica |Indicazione è stata applicata e servizio hello misurati vantaggi hello. |
| Success |La raccomandazione è stata applicata e i vantaggi sono stati misurati. |
| Errore |Si è verificato un errore durante il processo di hello dell'applicazione hello dell'indicazione. Può trattarsi di un problema temporaneo o eventualmente una tabella toohello delle modifiche dello schema e script hello non è più valido. |
| Ripristino |indicazione di Hello è stato applicato, ma è stato considerato non ad alte prestazioni e viene viene ripristinato automaticamente. |
| Ripristinato |indicazione di Hello è stata annullata. |

Fare clic su una raccomandazione in-process hello elenco toosee ulteriori dettagli:

![Indici consigliati](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a>Ripristino di una raccomandazione
Se è stata utilizzata la raccomandazione hello hello prestazioni indicazioni tooapply (ovvero che non è stato eseguito manualmente script hello T-SQL) verrà automaticamente ripristinata, se trova toobe impatto sulle prestazioni di hello negativo. Se per qualsiasi motivo si desidera semplicemente toorevert una raccomandazione non è seguito hello:

1. Selezionare una raccomandazione applicata in hello **ottimizzazione cronologia** area.
2. Fare clic su **Revert** su hello **dettagli sulle raccomandazioni** blade.

![Indici consigliati](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a>Monitoraggio dell'impatto sulle prestazioni delle indicazioni relative agli indici
Dopo aver indicazioni sono correttamente implementate (attualmente, operazioni sugli indici e parametrizzare solo i suggerimenti di query) è possibile fare clic su **informazioni dettagliate Query** su hello raccomandazione dettagli pannello tooopen [Query Informazioni dettagliate prestazioni](sql-database-query-performance.md) per verificarne l'impatto sulle prestazioni hello per le prime query.

![Monitorare l'impatto sulle prestazioni](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a>Riepilogo
Il database SQL di Azure fornisce raccomandazioni per migliorare le prestazioni del database SQL. Questa funzionalità offre script T-SQL, nonché opzioni singole e completamente automatizzate, e risulta molto utile per ottimizzare il database e quindi per migliorare le prestazioni delle query.

## <a name="next-steps"></a>Passaggi successivi
Monitorare le raccomandazioni e continuare tooapply li toorefine prestazioni. I carichi di lavoro dei database sono dinamici e cambiano in modo continuo. Database SQL di Azure continuerà toomonitor e fornire indicazioni che possono potenzialmente migliorare le prestazioni del database. 

* Vedere [ottimizzazione automatica](sql-database-automatic-tuning.md) toolearn ulteriori informazioni sugli hello ottimizzazione automatica nel Database SQL di Azure.
* Vedere le [Raccomandazioni per le prestazioni](sql-database-advisor.md) per una panoramica delle raccomandazioni per le prestazioni per il database SQL di Azure.
* Vedere [informazioni dettagliate prestazioni Query](sql-database-query-performance.md) toolearn sulla visualizzazione impatto sulle prestazioni hello per le prime query.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Archivio query](https://msdn.microsoft.com/library/dn817826.aspx)
* [CREATE INDEX](https://msdn.microsoft.com/library/ms188783.aspx)
* [Controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-what-is.md)

