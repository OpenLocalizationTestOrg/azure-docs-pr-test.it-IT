---
title: aaaCreate e ripristinare un backup nei servizi BizTalk | Documenti Microsoft
description: "I Servizi BizTalk includono funzionalità di backup e ripristino. Informazioni su come toocreate determinare quali backup e ripristinare un backup. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a>Servizi BizTalk: backup e ripristino

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

I Servizi BizTalk di Azure includono funzioni di backup e ripristino. In questo argomento viene descritto come toobackup e ripristino di servizi di BizTalk utilizzando hello portale di Azure classico.

È inoltre possibile eseguire i servizi di BizTalk utilizzando hello [API REST di servizi BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584). 

> [!NOTE]
> Le connessioni ibride non sottoposti a backup, indipendentemente dall'edizione hello. È necessario ricreare le connessioni ibride.


## <a name="before-you-begin"></a>Operazioni preliminari
* Le funzionalità di backup e ripristino potrebbero non essere disponibili per tutte le edizioni. Vedere [Servizi BizTalk: Grafico edizioni](biztalk-editions-feature-chart.md).
* Utilizza hello portale di Azure classico, è possibile creare un backup su richiesta o creare un backup pianificato. 
* Contenuto di backup può essere ripristinato toohello stesso BizTalk Service o tooa nuovo BizTalk Service. toorestore hello BizTalk Service utilizzando hello stesso nome, hello esistente BizTalk Service deve essere eliminato e il nome di hello deve essere disponibile. Dopo aver eliminato un BizTalk Service, può richiedere più tempo desiderato per hello stesso nome toobe disponibili. Se non è possibile attendere hello stesso nome toobe disponibili, quindi ripristinare tooa nuovo BizTalk Service.
* Servizi BizTalk può essere ripristinato toohello stessa versione o una versione successiva. Ripristino dei servizi BizTalk tooa edizione inferiore, da quando è stato eseguito il backup di hello, non è supportata.
  
    Ad esempio, un backup utilizzando hello che Edizione Basic può essere ripristinato toohello Premium Edition. Un backup utilizzando hello che edizione Premium non può essere ripristinato toohello Standard Edition.
* numeri di controllo EDI Hello sottoposti a backup continuità toomaintain hello dei numeri di controllo. Se i messaggi vengono elaborati dopo l'ultimo backup hello, ripristinare il contenuto di backup può provocare numeri di controllo duplicati.
* Se dispone di un batch di messaggi attivi, elabora il batch di hello **prima** in esecuzione un backup. Quando si crea un backup (secondo le esigenze o pianificato), i messaggi in batch non vengono mai archiviati. 
  
    **Se si crea un backup con la presenza di messaggi attivi in un batch, non verrà eseguito il backup di questi messaggi, che andranno pertanto perduti.**
* Facoltativo: Nel portale dei servizi BizTalk di hello, arrestare eventuali operazioni di gestione.

## <a name="create-a-backup"></a>Creare un backup
È possibile creare in qualsiasi momento un backup controllato interamente dall'utente. Questa sezione sono elencati i backup di toocreate passaggi hello utilizzando hello Azure classico portale, tra cui:

[Backup su richiesta](#backupnow)

[Pianificare un backup](#backupschedule)

#### <a name="backupnow"></a>Backup su richiesta
1. Nel portale di Azure classico hello, selezionare **servizi BizTalk**, e quindi selezionare hello BizTalk Service desiderato toobackup.
2. In hello **Dashboard** , selezionare **backup** nella parte inferiore di hello della pagina hello.
3. Indicare un nome per il backup. Ad esempio, immettere *ServizioBizTalk*BU*Data*.
4. Scegliere un account di archiviazione blob di backup e selezionare hello segno di spunta toostart hello.

Al termine del backup hello, viene creato un contenitore con nome del backup hello che immesso nell'account di archiviazione hello. Questo contenitore include la configurazione del backup del proprio servizio BizTalk.

#### <a name="backupschedule"></a>Pianificare un backup
1. Nel portale di Azure classico hello, selezionare **servizi BizTalk**, selezionare hello Nome BizTalk Service backup hello tooschedule desiderato e quindi selezionare hello **configura** scheda.
2. Set hello **stato Backup** troppo**automatica**. 
3. Seleziona hello **Account di archiviazione** toostore hello backup, immettere hello **frequenza** toocreate hello backup e il tempo tookeep hello backup (**giorni di conservazione**):
   
    ![][AutomaticBU]
   
    **Note**     
   
   * In **giorni di conservazione**, il periodo di memorizzazione hello deve essere maggiore della frequenza di backup hello.
   * Selezionare **mantenere sempre almeno un backup**, anche se è stata superata hello periodo di memorizzazione.
4. Selezionare **Salva**.

Quando viene eseguito un processo di backup pianificato, viene creato un contenitore (dati di backup toostore) nell'account di archiviazione hello immesso. nome Hello del contenitore di hello è denominata *BizTalk Service Name-data-ora*. 

Se viene visualizzato il dashboard di BizTalk Service hello un **Failed** stato:

![Last scheduled backup status][BackupStatus] 

collegamento Hello apre hello registri operazioni di Gestione servizi toohelp risoluzione dei problemi. Vedere [Servizi BizTalk: Risoluzione dei problemi mediante i log operazioni](http://go.microsoft.com/fwlink/p/?LinkId=391211).

## <a name="restore"></a>Ripristino
È possibile ripristinare i backup dal portale di Azure classico hello o da hello [ripristinare API REST dei servizi BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325582). Questa sezione elenca hello passaggi toorestore utilizzando portale classico hello.

#### <a name="before-restoring-a-backup"></a>Prima di ripristinare un backup
* Durante il ripristino di un Servizio BizTalk è possibile immettere nuovi archivi di rilevamento, archiviazione e monitoraggio.
* Hello stessi dati di Runtime EDI viene ripristinati. backup di Runtime EDI Hello archivia numeri di controllo hello. numeri di controllo Hello ripristinato sono in sequenza dall'ora hello del backup hello. Se i messaggi vengono elaborati dopo l'ultimo backup hello, ripristinare il contenuto di backup può provocare numeri di controllo duplicati.

#### <a name="restore-a-backup"></a>Ripristino di un backup
1. Nel portale di Azure classico hello, selezionare **New** > **servizi App** > **BizTalk Service** > **ripristino** :
   
    ![Ripristino di un backup][Restore]
2. In **Backup URL**, selezionare l'icona della cartella hello ed espandere hello account di archiviazione Azure che archivi hello backup della configurazione di BizTalk Service. Espandere il contenitore di hello e nel riquadro di destra hello, selezionare hello corrispondente, eseguire il backup dei file con estensione txt. 
   <br/><br/>
   Scegliere **Open**(Apri).
3. In hello **servizio Ripristino configurazione di BizTalk** pagina, immettere un **nome del servizio BizTalk** e verificare hello **URL di dominio**, **Edition**e **Area** per hello ripristinato BizTalk Service. **Creare una nuova istanza di database SQL** per database di rilevamento hello:
   
    ![][RestoreBizTalkService]
   
    Selezionare sulla freccia avanti hello.
4. Verificare il nome di hello del database SQL di hello, immettere hello server fisici in cui verrà creato il database SQL hello e un nome utente e password per il server.

    Se si desidera l'edizione del database SQL tooconfigure hello, dimensioni e altre proprietà, selezionare **Configure Advanced Settings Database**. 

    Selezionare sulla freccia avanti hello.

1. Creare un nuovo account di archiviazione o immettere un account di archiviazione esistente per hello BizTalk Service.
2. Selezionare Ripristina hello toostart di hello segno di spunta.

Dopo il ripristino di hello è stata completata correttamente, è elencato un nuovo di BizTalk Service in uno stato sospeso, nella pagina servizi BizTalk hello hello portale di Azure classico.

### <a name="postrestore"></a>Dopo aver ripristinato un backup
Hello BizTalk Service viene sempre ripristinato un **Suspended** stato. In questo stato, può essere modifiche alla configurazione prima nuovo ambiente hello è funzionale, tra cui:

* Se le applicazioni di BizTalk Service utilizzando hello Azure BizTalk Services SDK è stato creato, potrebbe essere credenziali di controllo di accesso (ACS) tootooupdate hello in toowork tali applicazioni con ambiente hello ripristinato.
* Ripristinare un tooreplicate BizTalk Service un ambiente BizTalk Service esistente. In questo caso, se sono presenti contratti configurati nel portale di servizi BizTalk originale hello che utilizzano una cartella di origine FTP, potrebbe essere contratti hello tooupdate in toouse ambiente hello appena ripristinato una cartella FTP di origine diversa. In caso contrario, potrebbero essere presenti due contratti diversi durante il tentativo toopull hello stesso messaggio.
* Se è stato ripristinato toohave più ambienti BizTalk Service, assicurarsi che la destinazione è ambiente corretto di hello in applicazioni di Visual Studio hello, i cmdlet di PowerShell, API REST o API del modello a oggetti gestione dei Partner commerciali.
* Si tratta di un backup di tooconfigure automatizzata buona norma in ambiente del servizio BizTalk hello appena ripristinato.

Ciao toostart BizTalk Service hello portale di Azure classico, hello seleziona ripristinato BizTalk Service e selezionare **Resume** nella barra delle applicazioni hello. 

## <a name="what-gets-backed-up"></a>Elementi di cui viene eseguito il backup
Quando viene creato un backup, hello seguenti elementi vengono eseguito il backup:

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH>Elementi di backup</TH> 
</tr> 
<tr>
<td colspan="2">
 <strong>Portale Servizi BizTalk di Azure</strong></td>
</tr> 
<tr>
<td>Configurazione e runtime</td> 
<td>
<ul>
<li>Dettagli su partner e profilo</li>
<li>Contratti con il partner</li>
<li>Assembly personalizzati distribuiti</li>
<li>Bridge distribuiti</li>
<li>Certificati</li>
<li>Trasformazioni distribuite</li>
<li>Pipeline</li>
<li>I modelli creati e salvati in hello portale dei servizi BizTalk</li>
<li>Mapping X12 ST01 e GS01</li>
<li>Numeri di controllo (EDI)</li>
<li>Valori MIC del messaggio AS2</li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2">
 <strong>Servizio BizTalk di Azure</strong></td>
</tr> 
<tr>
<td>Certificato SSL</td> 
<td>
<ul>
<li>Dati certificato SSL</li>
<li>Password certificato SSL</li>
</ul>
</td>
</tr> 
<tr>
<td>Impostazioni del servizio BizTalk</td> 
<td>
<ul>
<li>Conteggio dell'unità di scala</li>
<li>Edizione</li>
<li>Versione prodotto</li>
<li>Area/data center</li>
<li>Spazio dei nomi e chiave del Servizio di controllo di accesso (ACS)</li>
<li>Rilevamento della stringa di connessione al database</li>
<li>Archiviazione della stringa di connessione all'account di archiviazione</li>
<li>Monitoraggio della stringa di connessione all'account di archiviazione</li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2">
 <strong>Elementi aggiuntivi</strong></td>
</tr> 
<tr>
<td>Database di rilevamento</td> 
<td>Quando viene creato hello BizTalk Service, vengono immessi i dettagli del Database di rilevamento hello inclusi hello Server di Database SQL di Azure e il nome di Database di rilevamento hello. Hello Database di rilevamento non viene automaticamente eseguito il backup.
<br/><br/>
<strong>Importante</strong><br/>
Se hello Database di rilevamento viene eliminata e hello esigenze database ripristinate, deve esistere un backup precedente. Se non esiste un backup, i Database di rilevamento hello e i relativi dati non sono recuperabili. In questo caso, creare un nuovo Database di rilevamento con hello stesso nome di database. È consigliata la replica geografica.</td>
</tr> 
</table>

## <a name="next"></a>Avanti
Servizi BizTalk di Azure toocreate in hello Azure classico, andare troppo[servizi BizTalk: portale classico di Provisioning tramite Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280). creazione di applicazioni, andare troppo toostart[servizi BizTalk di Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Vedere anche
* [Backup del servizio BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [Ripristino del servizio BizTalk da un backup](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [Servizi BizTalk: effettuare il provisioning di un servizio BizTalk mediante il portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [Servizi BizTalk: Tabella degli stati del servizio](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [Servizi BizTalk: Schede Dashboard, Monitoraggio, Scalabilità](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [Servizi BizTalk: limitazione](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [Servizi BizTalk: nome e chiave dell'autorità emittente](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Come è possibile utilizzare hello Azure BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

