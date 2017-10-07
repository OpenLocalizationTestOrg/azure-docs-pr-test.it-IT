---
title: Panoramica della delega DNS aaaAzure | Documenti Microsoft
description: Comprendere come usare DNS di Azure e delega di dominio toochange denominati server tooprovide dominio ospita.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: eaf2d2e345004b4d631e8d81d548b8ca23277d05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="delegation-of-dns-zones-with-azure-dns"></a>Delega di zone DNS con DNS di Azure

DNS di Azure consente una zona DNS toohost e gestire i record DNS hello per un dominio in Azure. Per le query DNS per tooreach un dominio DNS di Azure, il dominio hello deve toobe delegato tooAzure DNS del dominio padre hello. Tenere presente il DNS di Azure non è il registrar di dominio hello. Questo articolo viene illustrato come funziona la delega di dominio e come toodelegate domini tooAzure DNS.

## <a name="how-dns-delegation-works"></a>Funzionamento della delega DNS

### <a name="domains-and-zones"></a>Domini e zone

Hello Domain Name System è una gerarchia di domini. gerarchia di Hello inizia dal dominio 'root' hello, il cui nome è semplicemente '**.**'.  seguito dai domini di primo livello, come "com", "net", "org", "uk" o "jp",  e quindi dai domini di secondo livello, come "org.uk" o "co.jp"  e così via. i domini Hello hello gerarchia DNS sono ospitati tramite zone DNS separate. Queste aree vengono distribuite a livello globale, ospitati da server dei nomi DNS in tutto il mondo hello.

**Zona DNS** -un dominio è un nome univoco nel Domain Name System, ad esempio 'contoso.com' hello. Una zona DNS è utilizzato toohost hello DNS record per un particolare dominio. Ad esempio, il dominio di hello 'contoso.com' può contenere più record DNS, ad esempio 'mail.contoso.com' (per un server di posta elettronica) e 'www.contoso.com' (per un sito Web).

**Registrar**: un registrar è una società che può fornire nomi di dominio Internet. Verifica dominio Internet hello toouse è disponibile e consentono di toopurchase è. Una volta registrato, il nome di dominio di hello è legittimo proprietario di hello hello nome di dominio. Se si dispone già di un dominio Internet, si utilizzerà hello corrente dominio registrar toodelegate tooAzure DNS.

toofind ulteriori informazioni su chi possiede un nome di dominio specificato o per informazioni su come toobuy un dominio, vedere [gestione dei domini Internet in Azure AD](https://msdn.microsoft.com/library/azure/hh969248.aspx).

### <a name="resolution-and-delegation"></a>Risoluzione e delega

Esistono due tipi di server DNS:

* Un server DNS *autorevole* ospita le zone DNS e risponde alle query DNS solo per i record presenti in tali zone.
* Un server DNS *ricorsivo* non ospita zone DNS, Vengono fornite risposte alle tutte le query DNS chiamando le dati hello toogather server DNS autorevole che necessari.

Il servizio DNS di Azure fornisce un servizio DNS autorevole.  Non fornisce un servizio DNS ricorsivo. Servizi cloud e macchine virtuali in Azure vengono configurate automaticamente toouse un servizio DNS ricorsivo che viene fornito separatamente come parte dell'infrastruttura di Azure. Per informazioni su come toochange queste impostazioni DNS, vedere [la risoluzione dei nomi in Azure](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

I client DNS in PC o dispositivi mobili in genere chiamano una tooperform di server DNS ricorsivo tutte le query DNS le applicazioni client hello devono.

Quando un server DNS ricorsivo riceve una query per un record DNS, ad esempio 'www.contoso.com', deve prima toofind hello Nome hosting hello la zona del server per il dominio 'contoso.com' hello. server dei nomi toofind hello, inizia in corrispondenza di server dei nomi radice hello e da lì Trova server di nome hello ospita hello "com" zona. Viene quindi eseguita una query hello '' nome server toofind hello Nome server com ospita hello 'contoso.com' zona.  Infine, è in grado di tooquery questi server dei nomi per 'www.contoso.com'.

Questa procedura viene chiamata la risoluzione nome DNS hello. In teoria, la risoluzione DNS include passaggi aggiuntivi, ad esempio i seguenti record CNAME, ma che non è importante toounderstanding funzionamento della delega DNS.

Come una zona padre 'punto' toohello server dei nomi per una zona figlio? Usando un tipo speciale di record DNS, denominato record NS (Name Server, server dei nomi). Ad esempio, zona radice hello contiene i record NS per "com" e Mostra i server dei nomi per l'area 'com' hello hello. Zona "com" hello contiene a sua volta, i record NS per 'contoso.com', che mostra i server dei nomi per l'area 'contoso.com' hello hello. Impostazione record NS hello per una zona figlio in una zona padre viene denominata a dominio hello delega.

Hello seguente immagine mostra un esempio di query DNS. partners.contoso.NET e contoso.net hello sono zone DNS di Azure.

![Dns-nameserver](./media/dns-domain-delegation/image1.png)

1. le richieste client Hello `www.partners.contoso.net` dal relativo server DNS locale.
1. server DNS locale Hello non dispone di record hello, pertanto è un server dei nomi radice tootheir richiesta.
1. server dei nomi radice Hello non dispone di record di hello, ma conosce indirizzo hello di hello `.net` server dei nomi, fornisce il server DNS di indirizzo toohello
1. Hello DNS invia hello richiesta toohello `.net` server dei nomi, non è presente hello record ma non conosce l'indirizzo di hello hello contoso.net del server dei nomi. In questo caso si tratta di una zona DNS ospitata in DNS di Azure.
1. zona Hello `contoso.net` non dispone di record hello ma SA server dei nomi hello per `partners.contoso.net` e con quello di risposta. In questo caso si tratta di una zona DNS ospitata in DNS di Azure.
1. server DNS Hello richiede l'indirizzo IP hello del `partners.contoso.net` da hello `partners.contoso.net` zona. Contiene i record A hello e risponde con l'indirizzo IP hello.
1. server DNS Hello fornisce hello IP indirizzo toohello client
1. client di Hello si connette il sito toohello `www.partners.contoso.net`.

Ogni delega abbia effettivamente due copie di record NS hello. una zona padre hello verso toohello figlio e un altro in una zona figlio hello stesso. zona 'contoso.net' Hello contiene i record NS hello per 'contoso.net' (in aggiunta toohello i record NS 'netto'). Questi record vengono chiamati i record NS autorevoli e si trovano al vertice hello della zona figlio hello.

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come troppo[delegare il tooAzure di dominio DNS](dns-delegate-domain-azure-dns.md)

