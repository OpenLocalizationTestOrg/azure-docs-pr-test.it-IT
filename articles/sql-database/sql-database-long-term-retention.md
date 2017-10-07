---
title: aaaStore i backup di Database SQL di Azure per backup anni too10 | Documenti Microsoft
description: Informazioni su come Database SQL di Azure supporta l'archiviazione di backup per backup too10 anni.
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a>Archiviare i backup del Database SQL di Azure per backup too10 anni
Molte applicazioni hanno normativi, conformità o altre attività che richiedono i backup di database tooretain oltre hello 7-35 giorni forniti dal Database SQL di Azure a scopo [backup automatici](sql-database-automated-backups.md). Tramite funzionalità di conservazione dei backup a lungo termine hello, è possibile archiviare i backup dei database SQL in un insieme di credenziali di servizi di ripristino di Azure per backup too10 anni. È possibile archiviare backup too1, 000 database per ogni insieme di credenziali. È quindi possibile selezionare qualsiasi backup hello insieme di credenziali toorestore come un nuovo database.

> [!IMPORTANT]
> Conservazione dei backup a lungo termine è attualmente in anteprima e disponibile in hello seguenti aree: Australia orientale, Australia sudorientale, Brasile meridionale, Stati Uniti centrali, Asia orientale, Stati Uniti orientali, Stati Uniti orientali 2, India centrale, India meridionale, Giappone orientale, Giappone occidentale, North Central US, settentrionale Europa, Stati Uniti centro-meridionali, Asia sudorientale, Europa occidentale e Stati Uniti occidentali.
>

> [!NOTE]
> È possibile abilitare dei database too200 per ogni insieme di credenziali durante un periodo di 24 ore. È consigliabile utilizzare un archivio separato per ogni impatto hello toominimize di server di questo limite. 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a>Funzionamento della conservazione a lungo termine dei backup del database SQL

La conservazione a lungo termine dei backup consente di associare un server del database SQL a un insieme di credenziali di Servizi di ripristino di Azure. 

* È necessario creare l'insieme di credenziali hello in hello stessa sottoscrizione Azure creata hello SQL server e in hello stesso gruppo risorse e area geografico. 
* È quindi possibile configurare un criterio di conservazione per qualsiasi database. Hello criteri cause hello settimanale completo del database backup toobe copiati insieme di credenziali di servizi di ripristino toohello e conservati per il periodo di memorizzazione specificato hello (backup too10 anni). 
* È quindi possibile ripristinare il database di hello da uno qualsiasi di questi backup tooa nuovo database in qualsiasi server nella sottoscrizione hello. Archiviazione di Azure crea una copia di backup esistenti e copia hello non ha alcun impatto sulle prestazioni per il database esistente di hello.

> [!TIP]
> Per una procedura-tooguide, vedere [Configura e il ripristino da conservazione dei backup di Database SQL di Azure a lungo termine](sql-database-long-term-backup-retention-configure.md).

## <a name="enable-long-term-backup-retention"></a>Abilitare la conservazione del backup a lungo termine

tooconfigure a lungo termine conservazione dei backup per un database:

1. Creare un insieme di credenziali di servizi di ripristino di Azure in hello stesso gruppo di area, sottoscrizione e delle risorse del server di database SQL. 
2. Registrare l'insieme di credenziali di hello server toohello.
3. Creare un criterio di protezione per i servizi di ripristino di Azure.
4. Applicare i database toohello criteri di protezione hello che richiedono di conservazione dei backup a lungo termine.

tooconfigure, gestire e ripristinare un database da conservazione dei backup a lungo termine dei backup automatizzati in un insieme di credenziali di servizi di ripristino di Azure, effettuare una delle seguenti hello:

* Tramite il portale di Azure di hello: fare clic su **conservazione dei backup a lungo termine**, selezionare un database e quindi fare clic su **configura**. 

   ![Selezionare un database per la conservazione backup a lungo termine](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* Utilizzo di PowerShell: Andare troppo[Configura e il ripristino da conservazione dei backup di Database SQL di Azure a lungo termine](sql-database-long-term-backup-retention-configure.md).

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a>Ripristinare un database che viene archiviato con funzionalità di conservazione dei backup a lungo termine hello

toorecover da un backup di conservazione dei backup a lungo termine:

1. Elenco hello insieme di credenziali in cui è memorizzato il backup di hello.
2. Elenco hello contenitore server logico tooyour mappato.
3. Origine dati dell'elenco hello all'interno dell'insieme di credenziali hello che è mappata tooyour database.
4. Elenco hello dei punti di ripristino sono disponibili toorestore.
5. Ripristinare il database di hello dal server di destinazione toohello punto di ripristino hello nella sottoscrizione.

tooconfigure, gestire e ripristinare un database da conservazione dei backup a lungo termine dei backup automatizzati in un insieme di credenziali di servizi di ripristino di Azure, effettuare una delle seguenti hello:

* Utilizzando hello portale di Azure: passare troppo[con conservazione dei backup a lungo termine Gestisci hello Azure portal](sql-database-long-term-backup-retention-configure.md). 

* Utilizzo di PowerShell: Andare troppo[gestire la conservazione di backup a lungo termine tramite PowerShell](sql-database-long-term-backup-retention-configure.md).

## <a name="get-pricing-for-long-term-backup-retention"></a>Trovare i prezzi per la conservazione del backup a lungo termine

Conservazione dei backup a lungo termine di un database SQL viene addebitato in base toohello [servizi di Azure backup prezzi tariffe](https://azure.microsoft.com/pricing/details/backup/).

Dopo aver registrato toohello insieme di credenziali server di database SQL di hello, vengono addebitati i hello spazio di archiviazione totale utilizzato da backup settimanale di hello archiviati nell'insieme di credenziali hello.

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a>Visualizzare i backup disponibili archiviati nella conservazione dei backup a lungo termine

tooconfigure, gestire e ripristinare un database da conservazione dei backup a lungo termine dei backup automatizzati in un insieme di credenziali di servizi di ripristino di Azure tramite hello portale di Azure, effettuare una delle seguenti hello:

* Utilizzando hello portale di Azure: passare troppo[con conservazione dei backup a lungo termine Gestisci hello Azure portal](sql-database-long-term-backup-retention-configure.md). 

* Utilizzo di PowerShell: Andare troppo[gestire la conservazione di backup a lungo termine tramite PowerShell](sql-database-long-term-backup-retention-configure.md).

## <a name="disable-long-term-retention"></a>Disabilitare la conservazione a lungo termine

il servizio di ripristino Hello gestisce automaticamente la pulizia di hello di backup in base a hello fornito criteri di conservazione. 

backup hello l'invio di toostop per un insieme di credenziali toohello database specifico, rimuovere i criteri di conservazione hello per il database.
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> i backup di Hello che sono già nell'insieme di credenziali hello non sono interessati. Vengono automaticamente eliminati dal servizio di ripristino hello quando scade il periodo di memorizzazione.

## <a name="long-term-backup-retention-faq"></a>Domande frequenti sulla conservazione del backup a lungo termine

**È possibile manualmente eliminare backup specifici nell'insieme di credenziali hello?**

No, per il momento. insieme di credenziali Hello pulisce automaticamente i backup quando è scaduto il periodo di memorizzazione hello.

**È possibile registrare il toomore di backup server toostore rispetto a un insieme di credenziali?**

No, è attualmente possibile archiviare backup tooonly due insiemi di credenziali alla volta.

**È possibile disporre di un insieme di credenziali e un server in sottoscrizioni diverse?**

No, attualmente insieme di credenziali hello e server devono trovarsi in hello stesso gruppo di risorse e di sottoscrizione.

**È possibile usare un insieme di credenziali creato in un'area diversa rispetto all'area del mio server?**

No, deve essere l'insieme di credenziali hello e server hello toominimize area stessa ora di copiare ed evitare addebiti per il traffico.

**Quanti database è possibile archiviare in un insieme di credenziali?**

Attualmente supporta backup too1, 000 database per ogni insieme di credenziali. 

**Quanti insiemi di credenziali è possibile creare per ogni sottoscrizione?**

È possibile creare backup too25 gli insiemi di credenziali per ogni sottoscrizione.

**Quanti database è possibile configurare al giorno per ogni insieme di credenziali?**

È possibile configurare 200 database al giorno per ogni insieme di credenziali.

**La conservazione dei backup a lungo termine funziona con i pool elastici?**

Sì. Qualsiasi database nel pool di hello può essere configurato con criteri di conservazione hello.

**È possibile scegliere l'ora di hello in corrispondenza del quale viene creato il backup di hello?**

No, il Database SQL controlla hello pianificazione del backup toominimize hello impatto sulle prestazioni dei database.

**Per il database è attiva Transparent Data Encryption . È possibile usarli insieme di credenziali hello.** 

Sì, Transparent Data Encryption è supportata. È possibile ripristinare il database di hello dall'insieme di credenziali hello anche se il database originale di hello non esiste più.

**Cosa accade con backup hello nell'insieme di credenziali hello se la sottoscrizione è sospesa.** 

Se la sottoscrizione è sospesa, è conservare i backup e i database esistenti di hello. I nuovi backup non sono toohello copiati insieme di credenziali. Dopo aver riattivato sottoscrizione hello, servizio hello riprende la copia di backup toohello insieme di credenziali. L'insieme di credenziali diventa accessibile toohello operazioni di ripristino tramite backup di hello che sono stati copiati in tale posizione prima sottoscrizione hello è stata sospesa. 

**È possibile ottenere accesso toohello file di backup del database SQL in modo è possibile scaricare o ripristinarli toohello SQL server?**

No, non attualmente.

**È possibile toohave più pianificazioni (giornaliera, settimanale, mensile, annuale) all'interno di un criterio di conservazione SQL.**

No, le pianificazioni multiple sono attualmente disponibili solo per i backup della macchina virtuale.

**Cosa accade se si configura la conservazione dei backup a lungo termine in un database che è una replica geografica attiva secondaria?**

Attualmente non vengono eseguiti backup sulle repliche e pertanto non è possibile la conservazione dei backup a lungo termine nei database secondari. Tuttavia, è importante per gli utenti tooset di conservazione dei backup a lungo termine in un database secondario di replica geografica attiva per i motivi seguenti:
* Quando si verifica un failover e database hello diventa un database primario, si esegue il backup completo, ovvero toovault caricato.
* Non vi è alcun extra costi toohello cliente per l'impostazione di conservazione dei backup a lungo termine in un database secondario.

## <a name="next-steps"></a>Passaggi successivi
Poiché i backup dei database proteggono i dati da danneggiamenti o eliminazioni accidentali, sono una parte essenziale di qualsiasi strategia di continuità aziendale e ripristino di emergenza. toolearn circa hello altre soluzioni di continuità aziendale del Database SQL, vedere [Panoramica di continuità aziendale](sql-database-business-continuity.md).
