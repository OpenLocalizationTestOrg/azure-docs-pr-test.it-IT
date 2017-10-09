---
title: aaaMigrate da Azure RemoteApp tooCitrix informazioni Essentials | Documenti Microsoft
description: Come toomigrate da Azure RemoteApp tooCitrix informazioni Essentials
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 695a8165-3454-4855-8e21-f2eb2c61201b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aa3ce28bc5a86d5b1dd3408196d51935395f55c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toocitrix-xenapp-essentials"></a>Eseguire la migrazione da Azure RemoteApp tooCitrix informazioni Essentials

Se si utilizza Azure RemoteApp e si desidera toomigrate tooCitrix informazioni Essentials, esistono alcuni prerequisiti tookeep presente. Innanzitutto leggere la [guida tecnica dettagliata alla distribuzione per Citrix XenApp Essentials](https://docs.citrix.com/content/dam/docs/en-us/citrix-cloud/downloads/xenapp-essentials-deployment-guide.pdf) e la relativa [libreria tecnica online](http://docs.citrix.com/en-us/citrix-cloud/xenapp-and-xendesktop-service/xenapp-essentials.html). 

## <a name="prerequisite-steps-for-migration"></a>Passaggi preliminari per la migrazione

1. Creare una nuova rete virtuale o determinare la rete virtuale di Azure in Azure Resource Manager in cui si distribuirà Citrix XenApp Essentials. Azure RemoteApp utilizza hello portale di Azure classico; Citrix informazioni Essentials supporta solo Gestione risorse di Azure.  
2. Verificare che tale rete virtuale hello selezionato dispone di controller di dominio di accesso tooyour, di rete poiché Citrix supporta solo le distribuzioni ibride. Se si utilizza una distribuzione cloud di Azure RemoteApp, verificare che la rete virtuale dispone di controller di dominio Active Directory tooan di accesso di rete. È anche possibile usare Azure Active Directory Domain Services, ovvero Azure AD DS. 
3. Assicurarsi che DNS sia configurato correttamente per la rete virtuale hello, in modo che uniscono in join dominio ha esito positivo del primo tentativo di hello. È possibile creare una macchina virtuale (VM) nella rete virtuale di hello selezionato ed eseguire un tooverify join manuale di dominio DNS che hello e aggiunta al dominio funziona come previsto. In questo modo vengono hello ha esito positivo prima volta che si distribuisce Essentials informazioni Citrix. 
4. Se necessario, creare un peering di rete virtuale tra rete virtuale classica di Azure in uso con Azure RemoteApp e la rete virtuale di Azure Resource Manager. Questo processo peering funziona se le reti hello due si trovano in hello stessa area. In caso contrario, è possibile usare site-to-site VPN tooconnect hello le reti virtuali per la rete. 
5. Se è necessario leggere [come toomigrate dati dentro e fuori da Azure RemoteApp](remoteapp-migrate.md). 
6. Aggiornare il hello componente Citrix VDA tooinclude immagine esistente di Azure RemoteApp (per istruzioni, vedere la documentazione di Citrix hello). 
7. Andare toohello Azure Marketplace e iniziare la distribuzione di Essentials informazioni Citrix.

## <a name="other-considerations"></a>Altre considerazioni

Tenere hello seguenti considerazioni aggiuntive quando esegue la migrazione:
- Citrix XenApp Essentials supporta solo distribuzioni ibride. In altre parole, è necessario controller di dominio tooa di accesso di rete in aggiunta al dominio tooperform ordine. Se si utilizza una distribuzione cloud di Azure RemoteApp, usare Azure Active Directory o verificare che la rete virtuale abbia accesso tooActive Directory per l'aggiunta al dominio. 
- toolearn toomove utente dati tooCitrix Essentials informazioni, vedere [come toomigrate dati dentro e fuori da Azure RemoteApp](remoteapp-migrate.md). 
- Citrix XenApp Essentials supporta solo account Active Directory. Non supporta gli account Microsoft, ad esempio outlook.com, msn.com o hotmail.com. 

## <a name="citrix-xenapp-essentials-billing"></a>Fatturazione di Citrix XenApp Essentials

Per informazioni dettagliate sui prezzi, vedere hello [domande frequenti su](https://www.citrix.com/global-partners/microsoft/resources/xenapp-essentials-faq.html#tab-30699) e [articolo introduttivo Citrix](https://www.citrix.com/global-partners/microsoft/remote-app.html). Sono presenti tre componenti fatturazione tooCitrix informazioni Essentials:

- addebito assistenza Citrix Hello, ovvero $12 per utente al mese. Come tutti gli acquisti di Azure Marketplace, questo è il metodo di pagamento toohello fatturati associato alla sottoscrizione di Azure. I clienti con contratto Enterprise non possono usare i crediti monetari di Azure. 
- Licenze di accesso al client Remote Data Services (RDS). Attualmente, è possibile acquistare hello tariffa di accesso remoto che viene fornito con hello pagamento Essentials informazioni Citrix per $6,25. Nel caso di un cliente EA, è possibile utilizzare toopay Azure crediti monetari per questo oggetto. Se si desidera toouse le licenze esistenti, contattare Microsoft all'indirizzo [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com), pertanto è possibile applicare questo effetto tooyour. 
- Calcolo e archiviazione di Azure. Si tratta di un costo di archiviazione Azure hello e utilizzo di calcolo per le macchine virtuali hello utilizzato. Tenere presenti i prezzi quando si selezionano le dimensioni della macchina virtuale e la densità di utenti. Nel caso di un cliente EA, è possibile utilizzare toopay Azure crediti monetari per questo oggetto.

In caso di altre domande, è possibile:
- Scrivere un'e-mail all'indirizzo [arainfo@microsoft.com](mailto:arainfo@microsoft.com).
- [Contattare il supporto tecnico di Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Per iniziare, [apertura di un case di supporto tecnico di Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toohelp con prerequisito necessario per i passaggi da 1 a 5. Per i passaggi 6 e 7, contattare Citrix aprendo un ticket di supporto nel portale di gestione di Citrix hello. 
