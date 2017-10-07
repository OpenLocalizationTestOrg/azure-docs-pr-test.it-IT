---
title: problemi di distribuzione del servizio cloud aaaTroubleshoot | Documenti Microsoft
description: Esistono alcuni problemi comuni che potrebbero verificarsi quando si distribuisce un tooAzure servizio cloud. Questo articolo fornisce soluzioni toosome di essi.
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 15aea4f2b2913d95f3378b2e9762b232531f3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a>Risolvere eventuali problemi di distribuzione dei servizi cloud
Quando si distribuisce un tooAzure di pacchetto dell'applicazione di servizio cloud, è possibile ottenere informazioni sulla distribuzione di hello da hello **proprietà** riquadro hello portale di Azure. È possibile utilizzare dettagli hello in toohelp questo riquadro per i problemi con il servizio cloud hello ed è possibile fornire il supporto di tooAzure informazioni quando si apre una nuova richiesta di supporto.

È possibile trovare hello **proprietà** riquadro come indicato di seguito:

* In hello portale di Azure, fare clic su distribuzione hello del servizio cloud, fare clic su **tutte le impostazioni**, quindi fare clic su **proprietà**.
* In hello portale di Azure classico, fare clic su distribuzione hello del servizio cloud, fare clic su **DASHBOARD**, che si trova nell'angolo inferiore destro di hello della pagina di hello (in **riepilogo rapido**). Tenere presente che l'etichetta "Proprietà" è mancante in questo riquadro.

> [!NOTE]
> È possibile copiare il contenuto di hello di hello **proprietà** Appunti toohello riquadro facendo clic sull'icona di hello nell'angolo superiore destro di hello del riquadro hello.
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a>Problema: non è possibile accedere al sito Web, ma la distribuzione è stata avviata e tutte le istanze del ruolo sono pronte.
collegamento URL del sito Web di Hello visualizzato nel portale di hello non includa la porta hello. porta predefinita Hello per i siti Web è 80. Se l'applicazione è configurata toorun in una porta diversa, è necessario aggiungere URL toohello numero di porta corretto hello durante l'accesso del sito Web hello.

1. Nel portale di Azure hello, fare clic su distribuzione hello del servizio cloud.
2. In hello **proprietà** riquadro di hello portale di Azure, controllare le porte hello per le istanze del ruolo hello (in **endpoint di Input**).
3. Se non porta hello è 80, aggiungere hello porta corretta valore toohello URL quando si accede a un'applicazione hello. toospecify una porta non predefinito, digitare l'URL di hello, seguito da due punti (:), seguito dal numero di porta hello, senza spazi.

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a>Problema: istanze del ruolo personalizzate riciclate senza intervento dell'utente.
Correzione del servizio si verifica automaticamente quando Azure rileva i nodi di problema e quindi sposta i nodi toonew di istanze di ruolo. In tal caso, è possibile che le istanze del ruolo vengano riciclate automaticamente. durante la correzione del servizio toofind se:

1. Nel portale di Azure hello, fare clic su distribuzione hello del servizio cloud.
2. In hello **proprietà** riquadro di hello portale di Azure, esaminare le informazioni di hello e determinare se correzione del servizio si è verificato durante la fase di hello che si è notato ruoli hello riciclo.

I ruoli vengono riciclati approssimativamente una volta al mese durante gli aggiornamenti del sistema operativo host e del sistema operativo guest.  
Per ulteriori informazioni, vedere hello post di blog [istanza del ruolo viene riavviato dovuti tooOS aggiornamenti](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a>Problema: Non è possibile eseguire uno scambio VIP e si riceve un errore
Non è possibile eseguire uno scambio VIP se è in corso l'aggiornamento di una distribuzione. Gli aggiornamenti di distribuzione si possono verificare automaticamente quando:

* È disponibile un nuovo sistema operativo guest e sono stati configurati gli aggiornamenti automatici.
* Si verifica la correzione del servizio.

toofind out Se Aggiorna automatica è impedito da uno scambio VIP:

1. Nel portale di Azure hello, fare clic su distribuzione hello del servizio cloud.
2. In hello **proprietà** riquadro di hello portale di Azure, esaminare il valore di hello di **stato**. Se è **pronto**, quindi controllare **ultima operazione** toosee se uno di recente si è verificato che potrebbe impedire lo scambio di VIP hello.
3. Ripetere i passaggi 1 e 2 per la distribuzione di produzione hello.
4. Se un aggiornamento automatico è in corso, attendere toofinish prima di scambio di VIP hello toodo durante il tentativo.

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a>Problema: Viene eseguito il ciclo di un'istanza del ruolo tra Avviato, Inizializzazione in corso, Occupato e Arrestato.
Questa condizione potrebbe indicare un problema relativo al codice, al pacchetto o al file di configurazione dell'applicazione. In tal caso, è necessario che lo stato di hello in grado di toosee cambia ogni pochi minuti e hello portale di Azure può essere simile al seguente **riciclo**, **occupato**, o **Initializing**. Ciò indica che si sono verificati problemi con un'applicazione hello che impedisce esecuzione istanza del ruolo hello.

Per ulteriori informazioni su come tootroubleshoot per questo problema, vedere post di blog hello [dati di diagnostica di calcolo di Azure PaaS](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) e [toorecycle di ruoli che causa problemi comuni](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

## <a name="problem-my-application-stopped-working"></a>Problema: Arresto del funzionamento dell'applicazione
1. Nel portale di Azure hello, fare clic su istanza del ruolo hello.
2. In hello **proprietà** riquadro di hello portale di Azure, è consigliabile il problema hello tooresolve le condizioni seguenti:
   * Se l'istanza del ruolo hello recentemente è stato arrestato (è possibile controllare il valore di hello di **conteggio interruzioni**), potrebbe essere aggiornamento distribuzione hello. Attendere toosee se l'istanza del ruolo hello riprende a funzionare in modo autonomo.
   * Se l'istanza del ruolo hello è **occupato**, controllare il toosee codice dell'applicazione se hello [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) viene gestito l'evento. Si potrebbe essere necessario tooadd o correggere il codice che gestisce l'evento.
   * Scorrere i dati di diagnostica hello e problemi relativi agli scenari in post di blog hello [dati di diagnostica di calcolo di Azure PaaS](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

> [!WARNING]
> Se si ricicla il servizio cloud, si reimpostano le proprietà di hello per la distribuzione di hello, cancellando effettivamente informazioni hello hello originale problema.
>
>

## <a name="next-steps"></a>Passaggi successivi
Altri [articoli sulla risoluzione dei problemi](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) per i servizi cloud.

toolearn come ruolo del servizio cloud tootroubleshoot problemi utilizzando i dati di diagnostica di Azure PaaS computer, vedere [serie di blog di Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
