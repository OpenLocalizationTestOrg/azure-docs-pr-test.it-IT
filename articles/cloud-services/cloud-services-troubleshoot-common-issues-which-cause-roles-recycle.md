---
title: aaaCommon causa del riciclo dei ruoli del servizio Cloud | Documenti Microsoft
description: "Un ruolo del servizio cloud che viene riciclato improvvisamente può causare tempi di inattività significativi. Ecco alcuni problemi comuni che causano toobe ruoli riciclato, che consentono di ridurre i tempi di inattività."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 533930d1-8035-4402-b16a-cf887b2c4f85
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 8fa152b33d2b22a8a02f834d4bc38519b4272f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="common-issues-that-cause-roles-toorecycle"></a>Problemi comuni che causano toorecycle ruoli
In questo articolo vengono descritte alcune delle cause più comuni di hello di problemi di distribuzione e risoluzione dei problemi di toohelp suggerimenti risolvere questi problemi. Un'indicazione che si verifica un problema con un'applicazione è quando l'istanza del ruolo hello ha esito negativo toostart o dal relativo passaggio tra gli stati inizializzazione, occupato e arresto di hello.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-runtime-dependencies"></a>Dipendenze di runtime mancanti
Se un ruolo nell'applicazione si basa su qualsiasi assembly che non fa parte di hello libreria gestita di .NET Framework o hello Azure, è necessario includere in modo esplicito tale assembly nel pacchetto di applicazione hello. Tenere presente che in Azure non sono disponibili per impostazione predefinita altri framework di Microsoft. Se il ruolo si basa su un framework di questo tipo, è necessario aggiungere pacchetto di applicazione toohello tali assembly.

Prima di compilare e assemblare l'applicazione, verificare i seguenti aspetti di hello:

* Se si utilizza Visual studio, verificare che hello **Copia localmente** impostata troppo**True** per ogni riferimento di assembly del progetto che non fa parte di hello Azure SDK oppure hello .NET Framework.
* Assicurarsi che i file Web. config hello non fa riferimento ad alcun assembly inutilizzato nell'elemento di compilazione hello.
* Hello **azione di compilazione** di ogni cshtml file è troppo**contenuto**. In questo modo che i file hello vengano visualizzati correttamente nel pacchetto hello e Abilita tooappear altri file a cui fa riferimento nel pacchetto hello.

## <a name="assembly-targets-wrong-platform"></a>Riferimento dell'assembly alla piattaforma errata
Azure è un ambiente a 64 bit, pertanto gli assembly .NET compilati per una destinazione a 32 bit non funzioneranno in Azure.

## <a name="role-throws-unhandled-exceptions-while-initializing-or-stopping"></a>Generazione di eccezioni non gestite da parte del ruolo durante l'inizializzazione o l'arresto
Eventuali eccezioni generate dai metodi hello di hello [RoleEntryPoint] (classe), che include hello [OnStart], [OnStop], e [eseguire]metodi, sono eccezioni non gestite. Se viene generata un'eccezione non gestita in uno di questi metodi, è possibile che hello ruolo verrà riciclato. Se il ruolo di hello il riciclo ripetuto potrebbe generare un'eccezione non gestita, ogni volta che viene effettuato il tentativo toostart.

## <a name="role-returns-from-run-method"></a>Restituzioni del ruolo dal metodo Run
Hello [eseguire] metodo è toorun previsto per un periodo illimitato. Se il codice esegue l'override di hello [eseguire] (metodo), deve essere sospeso per un periodo illimitato. Se hello [eseguire] metodo viene restituito, hello ruolo viene riciclato.

## <a name="incorrect-diagnosticsconnectionstring-setting"></a>Impostazione di DiagnosticsConnectionString errata
Se l'applicazione usa diagnostica Azure, file di configurazione del servizio è necessario specificare hello `DiagnosticsConnectionString` impostazione di configurazione. Questa impostazione è necessario specificare un account di archiviazione tooyour connessione HTTPS in Azure.

tooensure che il `DiagnosticsConnectionString` impostazioni siano corrette prima di distribuire il tooAzure pacchetto di applicazione, verificare hello segue:  

* Hello `DiagnosticsConnectionString` l'impostazione di account di archiviazione valido tooa punti in Azure.  
  Per impostazione predefinita, questa impostazione punta account di archiviazione emulato toohello, pertanto è necessario modificare questa impostazione in modo esplicito prima di distribuire il pacchetto dell'applicazione. Se non si modifica questa impostazione, viene generata un'eccezione quando tenta di istanza del ruolo hello toostart monitor di diagnostica hello. Ciò potrebbe causare hello ruolo istanza toorecycle per un periodo illimitato.
* Hello stringa di connessione è specificata nel seguente hello [formato](../storage/common/storage-configure-connection-string.md). (protocollo hello deve essere specificato come HTTPS). Sostituire *MyAccountName* con nome hello dell'account di archiviazione, e *MyAccountKey* con la chiave di accesso:    

        DefaultEndpointsProtocol=https;AccountName=MyAccountName;AccountKey=MyAccountKey

  Se si sviluppa l'applicazione tramite gli strumenti di Azure per Microsoft Visual Studio, è possibile utilizzare questo valore tooset pagine di proprietà hello.

## <a name="exported-certificate-does-not-include-private-key"></a>Chiave privata non inclusa nel certificato esportato
toorun un ruolo web in SSL, è necessario assicurarsi che il certificato di gestione esportato include la chiave privata di hello. Se si utilizza hello *gestione certificati di Windows* certificato hello tooexport, tooselect assicurarsi di essere **Sì** per hello **Esporta chiave privata di hello** opzione. Hello certificato deve essere esportato in formato PFX hello, ovvero unico formato di hello attualmente supportato.

## <a name="next-steps"></a>Passaggi successivi
Altri [articoli sulla risoluzione dei problemi](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) per i servizi cloud.

Per altri scenari di riciclo dei ruoli, vedere la [serie di blog di Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

[RoleEntryPoint]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx
[OnStart]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx
[OnStop]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx
[eseguire]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx
