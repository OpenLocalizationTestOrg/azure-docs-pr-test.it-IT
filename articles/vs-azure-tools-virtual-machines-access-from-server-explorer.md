---
title: Macchine virtuali di Azure da Esplora Server aaaAccessing | Documenti Microsoft
description: Panoramica di come tooview creare e gestire macchine virtuali di Azure (VM) in Esplora Server in Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: f8326aed105a64ca558f766d712cc68701f82c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>Accesso alle macchine virtuali di Azure da Esplora server
Con Esplora server in Visual Studio è possibile visualizzare informazioni sulle macchine virtuali ospitate da Azure.

## <a name="accessing-virtual-machines-in-server-explorer"></a>Accesso alle macchine virtuali in Esplora server
Se ci sono macchine virtuali ospitate da Azure, è possibile accedervi in Esplora server. È necessario innanzitutto accedere tooyour sottoscrizione di Azure tooview i servizi mobili. toosign, aprire il menu di scelta rapida hello per hello nodo di Azure in Esplora Server e scegliere **connettersi tooMicrosoft Azure**.

### <a name="tooget-information-about-your-virtual-machines"></a>tooget informazioni sulle macchine virtuali
1. In Esplora Server, scegliere una macchina virtuale, quindi tooshow chiave hello F4 la finestra delle proprietà.
   
    Hello nella tabella seguente vengono illustrate le proprietà disponibili, ma sono di sola lettura. toochange, utilizzare hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).
   
   | Proprietà | Descrizione |
   | --- | --- |
   | Nome DNS |URL di Hello con hello indirizzo Internet della macchina virtuale hello. |
   | Environment |Per una macchina virtuale, il valore di hello di questa proprietà è sempre produzione. |
   | Nome |nome Hello della macchina virtuale hello. |
   | Dimensione |dimensione Hello della macchina virtuale di hello, che riflette hello quantità di memoria e spazio su disco disponibile. Per altre informazioni, vedere Come configurare le dimensioni della macchina virtuale. |
   | Stato |I valori includono Avvio in corso, Avviato, Arresto, Arrestato e Recupero dello stato. Se viene visualizzato recupero dello stato, lo stato corrente di hello è sconosciuto. i valori Hello per questa proprietà sono diversi dai valori hello che vengono utilizzati in hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885). |
   | SubscriptionID |ID sottoscrizione Hello per l'account di Azure. È possibile visualizzare queste informazioni in hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885) visualizzando le proprietà di hello per una sottoscrizione. |
2. Scegliere un nodo dell'endpoint e quindi visualizzare hello **proprietà** finestra.
3. Hello tabella seguente vengono descritte le proprietà disponibili hello degli endpoint, ma sono di sola lettura. gli endpoint di hello tooadd o di modifica per una macchina virtuale, utilizzare hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885). 
   
   | Proprietà | Descrizione |
   | --- | --- |
   | Nome |Un identificatore per l'endpoint di hello. |
   | Private Port |porta Hello per applicazione interna tooyour accesso di rete. |
   | Protocol |protocollo di Hello hello layer di trasporto per l'endpoint utilizza TCP o UDP. |
   | Public Port |porta Hello che viene utilizzata per l'accesso pubblico tooyour applicazione. |

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni sull'utilizzo di ruoli di Azure in Visual Studio, vedere [tramite Desktop remoto con i ruoli Azure](vs-azure-tools-remote-desktop-roles.md).

