---
title: 'Generare ed esportare certificati per connessioni da punto a sito: MakeCert: Azure | Microsoft Docs'
description: Questo articolo contiene i passaggi per creare un certificato radice autofirmato, esportare la chiave pubblica e generare certificati client con MakeCert.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 2beacc461370f268e54e1eedcb32939f7c606b14
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a>Generare ed esportare certificati per connessioni da punto a sito usando MakeCert

Le connessioni da punto a sito usano certificati per l'autenticazione. Questo articolo illustra come creare un certificato radice autofirmato e generare i certificati client usando MakeCert. Per le procedure di configurazione da punto a sito, ad esempio come caricare i certificati radice, selezionare uno degli articoli dell'elenco seguente:

> [!div class="op_single_selector"]
> * [Create self-signed certificates - PowerShell](vpn-gateway-certificates-point-to-site.md) (Creare certificati autofirmati - PowerShell)
> * [Creare certificati autofirmati - MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Configure Point-to-Site - Resource Manager - Azure portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md) (Eseguire una configurazione da punto a sito - Resource Manager - Portale di Azure)
> * [Configurazione da punto a sito - Gestione risorse - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Configure Point-to-Site - Classic - Azure portal](vpn-gateway-howto-point-to-site-classic-azure-portal.md) (Eseguire una configurazione da punto a sito - Classica - Portale di Azure)
> 
> 

Anche se è consigliabile usare la [procedura con PowerShell per Windows 10](vpn-gateway-certificates-point-to-site.md) per creare i certificati, queste istruzioni relative a MakeCert vengono fornite come metodo facoltativo. I certificati generati con uno dei due metodi possono essere installati in [qualsiasi sistema operativo client supportato](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq). MakeCert presenta tuttavia la limitazione seguente:

* MakeCert è deprecato. Questo strumento potrebbe quindi essere rimosso in qualsiasi momento. I certificati già generati con MakeCert non saranno interessati quando MakeCert non sarà più disponibile. MakeCert viene usato solo per generare i certificati, non come meccanismo di convalida.

## <a name="rootcert"></a>Creare un certificato radice autofirmato

La procedura seguente illustra come creare un certificato autofirmato usando MakeCert. Questi passaggi non sono specifici di un modello di distribuzione. Sono validi sia per Gestione risorse che per il modello classico.

1. Scaricare e installare [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx).
2. Dopo l'installazione, in genere è possibile trovare l'utilità makecert.exe nel percorso seguente: "C:\Programmi (x86)\Windows Kits\10\bin\<arch>". È tuttavia possibile che sia stato installato in un altro percorso. Aprire un prompt dei comandi come amministratore e passare al percorso dell'utilità MakeCert. È possibile usare l'esempio seguente, apportando le modifiche necessarie per il percorso corretto:

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. Creare e installare quindi un certificato nell'archivio Certificati personali nel computer in uso. Nell'esempio seguente viene creato un file *.cer* corrispondente da caricare in Azure quando si configura una connessione da punto a sito. Sostituire 'P2SRootCert' e 'P2SRootCert.cer' con il nome da assegnare al certificato. Il certificato si trova in 'Certificati -Utente corrente\Personale\Certificati'.

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <a name="cer"></a>Esportare la chiave pubblica (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

Il file exported.cer deve essere caricato in Azure. Per istruzioni, vedere [Configurare una connessione da punto a sito](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile). Per aggiungere un certificato radice attendibile aggiuntivo, vedere [questa sezione](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) dell'articolo.

### <a name="export-the-self-signed-certificate-and-private-key-to-store-it-optional"></a>Esportare il certificato autofirmato e la chiave privata per archiviarli (facoltativo)

Si consiglia di esportare il certificato radice autofirmato e archiviarlo in un percorso sicuro. Se necessario, in seguito è possibile installarlo su un altro computer e generare altri certificati client oppure esportare un altro file.cer. Per esportare il certificato radice autofirmato come file .pfx, selezionare il certificato radice ed eseguire la stessa procedura descritta in [Esportazione di un certificato client](#clientexport).

## <a name="create-and-install-client-certificates"></a>Creare e installare i certificati client

Il certificato autofirmato non deve essere installato direttamente nel computer client. È necessario generare un certificato client da un certificato autofirmato. Quindi, esportare e installare il certificato client nel computer client. I seguenti passaggi non si applicano specificatamente a un modello di distribuzione. Sono validi sia per Gestione risorse che per il modello classico.

### <a name="clientcert"></a>Generazione di un certificato client

Ogni computer client che si connette a una rete virtuale usando la soluzione Da punto a sito deve avere un certificato client installato. È possibile generare un certificato client da un certificato radice autofirmato, quindi esportare e installare il certificato client. Se il certificato client non è installato, l'autenticazione ha esito negativo. 

I passaggi seguenti illustrano come generare un certificato client da un certificato radice autofirmato. È possibile generare più certificati client dallo stesso certificato radice. Quando si generano certificati client con la procedura seguente, il certificato client viene installato automaticamente nel computer che è stato usato per generare il certificato. Se si vuole installare un certificato client in un altro computer client, è possibile esportare il certificato.
 
1. Nello stesso computer usato per creare il certificato autofirmato aprire un prompt dei comandi come amministratore.
2. Modificare ed eseguire l'esempio per generare un certificato client.
  * Modificare *"P2SRootCert"* nel nome della radice autofirmata dalla quale si intende generare il certificato client. Assicurarsi di usare il nome del certificato radice, ovvero il valore "CN =" che è stato specificato al momento della creazione della radice autofirmata.
  * Modificare *P2SChildCert* nel nome che si desidera assegnare al certificato client generato.

  Se si esegue l'esempio riportato di seguito senza modificarlo, si otterrà un certificato client denominato P2SChildcert nell'archivio dei certificati personale generato dal certificato radice P2SRootCert.

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <a name="clientexport"></a>Esportare un certificato client

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <a name="install"></a>Installare un certificato client esportato

Per installare un certificato client, vedere [Installare un certificato client](point-to-site-how-to-vpn-client-install-azure-cert.md).

## <a name="next-steps"></a>Passaggi successivi

Continuare con la configurazione da punto a sito. 

* Per i passaggi del modello di distribuzione di **Resource Manager**, vedere [Configurare una connessione da punto a sito con l'autenticazione del certificato nativa di Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* Per i passaggi del modello di distribuzione **classico**, vedere [Configurare una connessione VPN da punto a sito a una rete virtuale (classico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
