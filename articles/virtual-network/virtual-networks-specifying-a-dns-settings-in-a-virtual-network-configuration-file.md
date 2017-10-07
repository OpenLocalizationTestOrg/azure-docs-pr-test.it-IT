---
title: aaaSpecifying impostazioni DNS in un file di configurazione di rete virtuale | Documenti Microsoft
description: Come file di impostazioni del server DNS toochange in una rete virtuale usando una configurazione di rete virtuale nel modello di distribuzione classica hello
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a>Indicazione delle impostazioni DNS in un file di configurazione di rete virtuale
Un file di configurazione di rete dispone di due elementi che è possibile utilizzare le impostazioni di sistema DNS (Domain Name) toospecify: **DnsServers** e **DnsServerRef**. È possibile aggiungere un elenco dei server DNS specificando i relativi indirizzi IP e fare riferimento a nomi toohello **DnsServers** elemento. È quindi possibile utilizzare un **DnsServerRef** toospecify elemento quali voci dei server DNS dall'elemento DnsServers hello vengono utilizzate per vari siti di rete all'interno della rete virtuale.

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione classica hello.

file di configurazione di rete Hello può contenere hello seguenti elementi. titolo Hello di ogni elemento è collegato tooa pagina che fornisce informazioni aggiuntive sull'elemento hello impostazioni dei valori.

> [!IMPORTANT]
> Per informazioni su come tooconfigure hello file di configurazione di rete, vedere [configurare una rete virtuale usando un File di configurazione di rete](virtual-networks-using-network-configuration-file.md). Per informazioni su ogni elemento contenuto nel file di configurazione di rete hello, vedere [Schema di configurazione di rete virtuale Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
> 
> 

[Elemento DNS](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> Hello **nome** attributo hello **DnsServer** elemento viene usato solo come riferimento per hello **DnsServerRef** elemento. Che rappresenta il nome host hello per il server DNS hello. Ogni **DnsServer** intera sottoscrizione di Microsoft Azure hello valore dell'attributo deve essere univoco
> 
> 

[Elemento siti di rete virtuale](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> In ordine toospecify questa impostazione per l'elemento relativo ai siti di rete virtuale hello, deve essere definito in precedenza nell'elemento DNS hello. Hello DnsServerRef *nome* in siti di rete virtuale hello l'elemento deve fare riferimento tooa nome valore specificato nell'elemento DNS hello per DnsServer *nome*.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Comprendere hello [Schema di configurazione di rete virtuale Azure](http://go.microsoft.com/fwlink/?LinkId=248093).
* Comprendere hello [dello Schema di configurazione del servizio di Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).
* [Configurare una rete virtuale usando un file di configurazione di rete](virtual-networks-using-network-configuration-file.md).

