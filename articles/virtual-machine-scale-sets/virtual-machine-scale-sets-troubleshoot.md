---
title: "scalabilità automatica aaaTroubleshoot con set di scalabilità di macchine virtuali | Documenti Microsoft"
description: "Informazioni sulla risoluzione dei problemi di scalabilità automatica con set di scalabilità di macchine virtuali. Comprendere i problemi tipici e come tooresolve li."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7d87b72-ee24-4e52-9377-a42f337f76fa
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: windows
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: guybo
ms.openlocfilehash: 4c9a70992348d87fb43646421a90a027bf400a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-autoscale-with-virtual-machine-scale-sets"></a>Risoluzione dei problemi di scalabilità automatica con set di scalabilità di macchine virtuali
**Problema** – creato un'infrastruttura per la scalabilità automatica di gestione di risorse di Azure utilizzando il set di scalabilità di macchine Virtuali, ad esempio per la distribuzione di un modello simile al seguente: https://github.com/Azure/azure-quickstart-templates/tree/master/201- autoscale-bottle vmss sono definite le regole di scalabilità e tutto funziona bene, ad eccezione del fatto che, indipendentemente da quanto carico inserire hello macchine virtuali, non scalabilità automatica.

## <a name="troubleshooting-steps"></a>Passaggi per la risoluzione dei problemi
Alcuni aspetti tooconsider includono:

* Il numero di core ogni macchina virtuale presenta e si sta caricando a ogni core? modello di avvio rapido di Azure esempio Hello precedente dispone di uno script do_work.php, che consente di caricare un singolo core. Se si usa una macchina virtuale di maggiore di un singolo core dimensioni della macchina virtuale come Standard_A1 o D1, sarà necessario toorun il carico corrente più volte. Per verificare il numero di core delle macchine virtuali, vedere [Dimensioni delle macchine virtuali in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Quanti macchine virtuali nel Set di scalabilità di macchine Virtuali, hello si eseguono operazioni su ciascuna di esse?
  
    Scalabilità evento avrà luogo solo quando hello medio della CPU tra **tutti** hello macchine virtuali in un set di scalabilità supera hello valore soglia, nel corso del tempo di hello interno definiti nelle regole di scalabilità automatica hello.
* Sono stati persi eventi di scalabilità?
  
    Controllare i log di controllo di hello in hello portale di Azure per gli eventi di scala. Potrebbero essersi verificati un aumento e poi una riduzione delle prestazioni non rilevati. È possibile filtrare per "Scalabilità".
  
    ![Log di controllo][audit]
* Le soglie di aumento e riduzione del numero di istanze sono sufficientemente diverse?
  
    Si supponga di che impostare una regola tooscale quando utilizzo medio della CPU è superiore al 50% più di 5 minuti e tooscale in quando utilizzo medio della CPU è inferiore al 50%. Si verificherebbe un problema "Ali" quando l'utilizzo della CPU è toothis Chiudi soglia, le azioni di scalabilità hello costantemente aumentare e ridurre le dimensioni del set di hello. Per questo motivo, il servizio di scalabilità automatica hello tenta tooprevent "instabile", che possono verificarsi come non sulla scalabilità. Verificare pertanto che la scalabilità orizzontale e le soglie di scala sono sufficientemente diversi tooallow liberare spazio tra il ridimensionamento.
* È stato scritto un modello JSON personalizzato?
  
    È facile toomake errori, quindi iniziare con un modello di hello uno oltre la quale viene dimostrato toowork e apportare piccole modifiche incrementali. 
* È possibile eseguire manualmente l'aumento o la riduzione del numero di istanze?
  
    Provare hello ridistribuzione risorsa Set di scalabilità della macchina virtuale con un diverso "capacità" impostazione toochange hello del numero di macchine virtuali manualmente. Un toodo modello di esempio si tratta di seguito: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing: potrebbe essere necessario tooedit hello modello toomake che disponga di hello stesso computer di dimensioni, il Set di scalabilità utilizza. Se è stato possibile modificare manualmente numero hello di macchine virtuali, si saprà problema hello è isolato tooautoscale.
* Controllare il Microsoft.Compute/virtualMachineScaleSet e le risorse Insights hello [Esplora inventario risorse di Azure](https://resources.azure.com/)
  
    Si tratta di un indispensabile risoluzione dei problemi dello strumento che illustra hello lo stato delle risorse di gestione risorse di Azure. Fare clic sulla sottoscrizione e osservare hello si debbano risolvere problemi di gruppo di risorse. Nel provider di risorse di calcolo hello cercare hello Set di scalabilità macchina virtuale è stato creato e verificare hello Vista istanza, che mostra lo stato di una distribuzione di hello. Controllare inoltre visualizzazione dell'istanza hello di macchine virtuali in hello Set di scalabilità della macchina virtuale. Quindi andare nel provider di risorse Insights hello e verificare le regole di scalabilità automatica hello visualizzate correttamente.
* Hello estensione diagnostica utilizzo e la creazione di dati sulle prestazioni?
  
    **Aggiornamento:** Azure scalabilità automatica sono stata avanzata toouse pipeline le metriche che non richiede più un toobe estensione di diagnostica installata basato su un host. Ciò significa hello prossime paragrafi non sono più valide se si crea un'applicazione per la scalabilità automatica tramite la nuova pipeline di hello. È un esempio di modelli di Azure che sono stati della pipeline di host hello toouse convertito: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale. 
  
    Utilizzo di metriche basata su host per la scalabilità automatica è preferibile per hello seguenti motivi:
  
  * Meno parti mobili come estensioni di diagnostica non è necessario toobe installato.
  * Modelli più semplici. Aggiungere modello di set di scalabilità tooan di regole di scalabilità automatica insights esistente.
  * Creazione di report più affidabile e avvio più veloce delle nuove macchine virtuali.
    
    Hello solo motivi per cui che è opportuno tookeep utilizza un'estensione di diagnostica sarebbe se è necessario memoria diagnostica reporting/scalabilità. Le metriche basate su host non creano report della memoria.
    
    Tenendo in considerazione, se si siano ancora utilizzando le estensioni di diagnostica per il ridimensionamento automatico solo seguire rest hello di questo articolo.
    
    Scalabilità automatica in Azure Resource Manager può funzionare (ma non dispone più di) tramite un'estensione di macchina virtuale denominata hello estensione di diagnostica. Account di archiviazione delle tooa di prestazioni dati definite nel modello hello emette. Questi dati vengono quindi aggregati dal servizio di monitoraggio di Azure hello.
    
    Se hello servizio Insights non è possibile leggere i dati da hello macchine virtuali, si suppone che toosend un messaggio di posta elettronica, ad esempio, se le macchine virtuali hello verso il basso, controlla la posta elettronica (Buongiorno quello specificato durante la creazione di account Azure hello).
    
    È anche possibile passare ed esamina i dati di hello. Esaminare hello account di archiviazione Azure tramite una finestra di esplorazione cloud. Ad esempio usando hello [Visual Studio Cloud Explorer](https://visualstudiogallery.msdn.microsoft.com/aaef6e67-4d99-40bc-aacf-662237db85a2), accedi e selezionare hello sottoscrizione di Azure in uso e hello account di archiviazione di diagnostica nome a cui fa riferimento in hello definizione di estensione di diagnostica della distribuzione modello...
    
    ![Cloud Explorer][explorer]
    
    In questo caso, si noterà una serie di tabelle in cui l'archiviazione dei dati di hello da ogni macchina virtuale. Accettando Linux e hello metrica CPU ad esempio, esaminare le righe più recenti di hello. Hello Visual Studio cloud explorer supporta un linguaggio di query, pertanto è possibile eseguire una query come "Timestamp gt datetime'2016-02-02T21:20:00Z'" toomake certi di disporre di eventi più recenti di hello (Presupponi che ora è in UTC). Hello i dati visualizzati in vi corrispondono toohello scalabilità configuri le regole? Nel seguente esempio hello hello della CPU per macchina 20 avviato aumenta too100% nel hello ultimi 5 minuti...
    
    ![Tabelle di archiviazione][tables]
    
    Se dati hello non sono presente, è presente il problema di hello è con estensione di diagnostica hello in esecuzione in macchine virtuali hello. Se i dati di hello sono presente, significa che si verifica un problema con le regole di scalabilità o con il servizio di Insights hello. Verificare lo [Stato di Azure](https://azure.microsoft.com/status/).
    
    Una volta superata questi passaggi, se si verificano ancora problemi di scalabilità automatica è possibile provare forum hello [MSDN](https://social.msdn.microsoft.com/forums/azure/home?category=windowsazureplatform%2Cazuremarketplace%2Cwindowsazureplatformctp), o [overflow dello Stack](http://stackoverflow.com/questions/tagged/azure), o una chiamata al supporto di log. Essere preparata tooshare hello modello e una visualizzazione dei dati delle prestazioni hello.

[audit]: ./media/virtual-machine-scale-sets-troubleshoot/image3.png
[explorer]: ./media/virtual-machine-scale-sets-troubleshoot/image1.png
[tables]: ./media/virtual-machine-scale-sets-troubleshoot/image4.png
