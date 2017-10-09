---
title: le impostazioni DNS in un file di configurazione del servizio aaaSpecifying | Documenti Microsoft
description: Specificare le impostazioni DNS personalizzate utilizzando il file di configurazione del servizio per la rete virtuale
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: f192e33566dd8e669da04e6378a0c8e4b0b35ecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a>Specifica le impostazioni DNS in un File di configurazione del servizio
## <a name="dns-elements"></a>Elemento DNS
Un file di configurazione del servizio può contenere un elemento DnsServers con un elenco di indirizzi IPv4 per i server di sistema DNS (Domain Name) hello che verrà utilizzato dal servizio hello. Le impostazioni nel file di configurazione del servizio hello hanno la precedenza rispetto alle impostazioni nel file di configurazione di rete hello. Per altre informazioni, vedere [Schema di configurazione dei servizi di Azure (con estensione .cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx).

**Elemento NetworkConfiguration**

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> Hello **nome** attributo hello **DnsServer** elemento viene usato solo come un nome di riferimento. Che rappresenta il nome host hello per il server DNS hello. Ogni **DnsServer** intera sottoscrizione di Microsoft Azure hello valore dell'attributo deve essere univoco.
> 
> 

## <a name="see-also"></a>Vedere anche
[Schema di configurazione dei servizi di Azure (file .cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710)

[Attività di configurazione di Rete virtuale di Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Configurare una rete virtuale usando un file di configurazione di rete](http://go.microsoft.com/fwlink/?LinkId=248094)

[Informazioni sulle impostazioni di rete virtuale nel portale di gestione di hello](http://go.microsoft.com/fwlink/?LinkId=248092)

