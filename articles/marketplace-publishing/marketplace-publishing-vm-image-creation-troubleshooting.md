---
title: aaaHow tootroubleshoot i problemi comuni durante la creazione del disco rigido virtuale | Documenti Microsoft
description: Risoluzione dei problemi di risposte toocommon domande e problemi durante la creazione del disco rigido virtuale.
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: e4ff09a979bdf575badff2d33f2299abb17c947d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-common-issues-encountered-during-vhd-creation"></a>Come tootroubleshoot problemi rilevati durante la creazione del disco rigido virtuale
In questo articolo viene fornita toohelp un server di pubblicazione di Azure Marketplace e/o un coamministratore che potrebbe verificarsi un problema o domande comuni durante la pubblicazione o gestire le soluzioni di macchina virtuale.

1. Come è possibile modificare il nome di hello dell'host di hello?
   
    Una volta creata la VM, gli utenti non è possibile aggiornare il nome di hello dell'host di hello.
2. Come tooreset hello servizio Desktop remoto o la password di account di accesso?
   
   * [Riferimento per macchine virtuali Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [Riferimento per macchine virtuali Linux](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. Utilizzo toogenerate nuovo ssh dei certificati?
   
   Consultare il collegamento toohello: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
4. Come tooconfigure un certificato della rete VPN aprire?
   
   Consultare il collegamento toohello: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)
5. Quali sono hello criteri di supporto per l'esecuzione di software server Microsoft nell'ambiente di macchina virtuale di Microsoft Azure hello (infrastructure-as-a-service)?
   
   Consultare il collegamento toohello: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)
6. Le macchine virtuali hanno un identificatore univoco?
   
   Azure codifica un ID univoco in ogni macchina virtuale di Azure. Per maggiori informazioni, visitare il blog e la documentazione appropriati.
7. In una macchina virtuale come è possibile gestire estensione script personalizzata hello nell'attività di avvio hello?
   
   Consultare il collegamento toohello: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)
8. Toocreate una macchina virtuale dal portale Azure usando hello hello VHD caricato come archiviazione toopremium?
   
   Questa funzionalità non è ancora supportata.
9. Un'applicazione a 32 bit è supportata in Azure Marketplace hello?
   
   Per dettagli sui criteri di supporto hello, vedere collegamento toohello: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)
10. Ogni volta che si sta tentando di toocreate un'immagine da my dischi rigidi virtuali, viene visualizzato l'errore hello ". Disco rigido virtuale è già registrato con l'archivio immagini come risorsa hello"in PowerShell. Ma non ho creato alcun tipo di risorsa in precedenza, né ho trovato un'immagine con questo nome in Azure. Come posso risolvere il problema?
    
    Ciò in genere verificarsi se una macchina virtuale da questo disco rigido virtuale di provisioning utente hello ed è presente un blocco su tale disco rigido virtuale. Verificare che non sia stata allocata nessuna macchina virtuale da questo disco rigido virtuale. Se vengono comunque mantenute errore hello, per genera un ticket di supporto utilizzando questo collegamento o da hello portale sulla pubblicazione (sono indicati i dettagli risposte hello della domanda 11).
