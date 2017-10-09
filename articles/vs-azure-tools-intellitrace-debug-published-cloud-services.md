---
title: servizio con Visual Studio e IntelliTrace cloud di un report pubblicato un Azure aaaDebugging | Documenti Microsoft
description: Informazioni su come toodebug un cloud service con Visual Studio e IntelliTrace
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a>Debug di un servizio cloud di Azure pubblicato con Visual Studio e IntelliTrace
Con IntelliTrace è possibile registrare informazioni di debug approfondite per un'istanza del ruolo quando è in esecuzione in Azure. Se è necessario a causa di hello toofind di un problema, è possibile utilizzare hello IntelliTrace registri toostep tramite il codice da Visual Studio come se fosse in esecuzione in Azure. In effetti, i record codice chiave ambiente e sull'esecuzione dati IntelliTrace quando l'applicazione Azure è in esecuzione come servizio cloud in Azure e consente di riprodurre i dati di hello registrato da Visual Studio. 

È possibile usare IntelliTrace se Visual Studio Enterprise è installato e l'applicazione Azure è destinata a .NET Framework 4 o versione successiva. IntelliTrace raccoglie informazioni per i ruoli Azure. macchine virtuali di Hello per questi ruoli sempre sistemi operativi a 64 bit.

In alternativa, è possibile utilizzare [il debug remoto](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach direttamente tooa servizio cloud in cui è in esecuzione in Azure.

> [!IMPORTANT]
> IntelliTrace è destinato esclusivamente a scenari di debug e non deve essere usato per una distribuzione di produzione.
> 

## <a name="configure-an-azure-application-for-intellitrace"></a>Configurare un'applicazione Azure per IntelliTrace
tooenable IntelliTrace per un'applicazione Azure, è necessario creare e pubblicare un'applicazione hello da un progetto Azure di Visual Studio. È necessario configurare IntelliTrace per l'applicazione Azure prima di pubblicarla tooAzure. Se si pubblica l'applicazione senza configurare IntelliTrace, è necessario progetto hello toorepublish. Per altre informazioni, vedere [Pubblicazione di progetti di servizi cloud di Azure con Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).

1. Quando si è pronti a toodeploy l'applicazione Azure, verificare che le destinazioni di compilazione progetto siano impostate troppo**Debug**.

1. In **Esplora**, fare clic sul progetto e selezionare il menu di scelta rapida hello **pubblica**.
   
1. In hello **pubblica l'applicazione Azure** finestra di dialogo, seleziona hello sottoscrizione di Azure e scegliere **Avanti**.

1. In hello **impostazioni** pagina, seleziona hello **impostazioni avanzate** scheda.

1. Attivare hello **Abilita IntelliTrace** opzione toocollect i log di IntelliTrace per l'applicazione quando viene pubblicata nel cloud hello.
   
1. toocustomize hello IntelliTrace configurazione di base, selezionare **impostazioni** Avanti troppo**Abilita IntelliTrace**.

    ![Collegamento alle impostazioni di IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. In hello **impostazioni IntelliTrace** finestra di dialogo, è possibile specificare quali toolog eventi, se toocollect chiamare informazioni, quali toocollect moduli e i processi di log per e quanta registrazione toohello tooallocate di spazio. Per ulteriori informazioni su IntelliTrace, vedere [Debug con IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).
   
    ![Impostazioni di IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

log di IntelliTrace Hello è un file di log circolare delle dimensioni massime consentite di hello specificato nelle impostazioni di IntelliTrace hello (dimensione predefinita hello è 250 MB). I log IntelliTrace vengono raccolti tooa file hello file System della macchina virtuale hello. Quando si richiedono i log di hello, uno snapshot viene portato a questo punto nel tempo e scaricati tooyour computer locale.

Dopo è stato pubblicato tooAzure hello servizio cloud di Azure, è possibile determinare se è stato abilitato IntelliTrace da hello Azure nodo **Esplora Server**, come illustrato nella seguente immagine hello:

![Esplora server - IntelliTrace abilitato](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a>Scaricare i log di IntelliTrace per un'istanza del ruolo
Tramite Visual Studio, è possibile scaricare i log di IntelliTrace per un'istanza del ruolo attenendosi alla procedura seguente:

1. In **Esplora Server**, espandere hello **servizi Cloud** nodo, quindi individuare l'istanza del ruolo i cui log si desidera toodownload. 

1. Istanza del ruolo hello e dal menu di scelta rapida hello s, scegliere **Visualizza log IntelliTrace**. 

    ![Opzione del menu Visualizza log IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. i log di IntelliTrace Hello sono tooa scaricato i file in una directory sul computer locale. Ogni volta che si richiede il log di IntelliTrace hello, viene creato un nuovo snapshot. Mentre vengono scaricati i registri di hello, Visual Studio consente di visualizzare lo stato di avanzamento hello dell'operazione di hello in hello **Log attività Azure** finestra. Come illustrato nella seguente illustrazione hello, è possibile espandere voce di riga hello hello operazione toosee maggiori dettagli.

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

È possibile continuare toowork in Visual Studio durante il download dei log di IntelliTrace hello. Quando il log di hello ha completato il download, viene aperto in Visual Studio.

> [!NOTE]
> Hello log IntelliTrace possono contenere eccezioni tale framework hello genera e gestisce in un secondo momento. Codice interno del framework genera queste eccezioni come parte normale di avvio di un ruolo, pertanto può essere ignorato.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
- [Opzioni per il debug dei servizi cloud di Azure](vs-azure-tools-debugging-cloud-services-overview.md)
- [Pubblicazione di un servizio cloud di Azure con Visual Studio](vs-azure-tools-publishing-a-cloud-service.md)