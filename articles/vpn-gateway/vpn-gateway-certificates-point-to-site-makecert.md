---
title: 'Generare ed esportare certificati per connessioni da punto a sito: MakeCert: Azure | Microsoft Docs'
description: In questo articolo contiene passaggi toocreate un certificato radice autofirmato, esportare la chiave pubblica hello e generare i certificati client utilizzando MakeCert.
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
ms.openlocfilehash: 0b795ccf74f1f97fbd3de8a0dc339f9cb0b48183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a>Generare ed esportare certificati per connessioni da punto a sito usando MakeCert

Le connessioni Point-to-Site, utilizzano tooauthenticate certificati. In questo articolo viene illustrato come certificato radice toocreate a autofirmato e generare i certificati client utilizzando MakeCert. Se si sta cercando i passaggi di configurazione da punto a sito, ad esempio come elenco di certificati radice tooupload, selezionare uno degli articoli hello ' Configure Point-to-Site' di hello seguenti:

> [!div class="op_single_selector"]
> * [Create self-signed certificates - PowerShell](vpn-gateway-certificates-point-to-site.md) (Creare certificati autofirmati - PowerShell)
> * [Creare certificati autofirmati - MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Configure Point-to-Site - Resource Manager - Azure portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md) (Eseguire una configurazione da punto a sito - Resource Manager - Portale di Azure)
> * [Configurazione da punto a sito - Gestione risorse - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Configure Point-to-Site - Classic - Azure portal](vpn-gateway-howto-point-to-site-classic-azure-portal.md) (Eseguire una configurazione da punto a sito - Classica - Portale di Azure)
> 
> 

Mentre si consiglia di utilizzare hello [passaggi di PowerShell di Windows 10](vpn-gateway-certificates-point-to-site.md) toocreate ai certificati, è fornire queste istruzioni MakeCert come un metodo facoltativo. certificati Hello generate usando dei metodi possono essere installati su [qualsiasi sistema operativo client supportato](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq). Tuttavia, MakeCert presenta hello seguente limitazione:

* MakeCert è deprecato. Questo strumento potrebbe quindi essere rimosso in qualsiasi momento. I certificati già generati con MakeCert non saranno interessati quando MakeCert non sarà più disponibile. MakeCert solo i certificati hello toogenerate utilizzato, non è un meccanismo di convalida.

## <a name="rootcert"></a>Creare un certificato radice autofirmato

Hello alla procedura seguente viene illustrato come toocreate un autofirmato certificato utilizzando MakeCert. Questi passaggi non sono specifici di un modello di distribuzione. Sono validi sia per Gestione risorse che per il modello classico.

1. Scaricare e installare [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx).
2. Dopo l'installazione, è possibile trovare utilità makecert.exe hello in questo percorso: ' C:\Program Files (x86) \Windows Kits\10\bin\<arch >'. Tuttavia, è possibile che sia stato installato tooanother percorso. Aprire un prompt dei comandi come amministratore e passare percorso toohello di hello utilità MakeCert. È possibile utilizzare hello di esempio seguente, l'adattamento per la posizione corretta hello:

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. Creare e installare un certificato nell'archivio certificati personale hello nel computer in uso. Hello esempio seguente viene creato un corrispondente *con estensione cer* file caricato tooAzure quando si configura P2S. Sostituire 'P2SRootCert' e 'P2SRootCert.cer' con nome hello che si desidera toouse certificato hello. Hello certificato si trova in 'Certificati - corrente\Personale\Certificati'.

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <a name="cer"></a>Esportare la chiave pubblica hello (con estensione cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

file exported.cer Hello deve essere caricato tooAzure. Per istruzioni, vedere [Configurare una connessione da punto a sito](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile). tooadd un certificato radice attendibile, vedere [in questa sezione](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) dell'articolo hello.

### <a name="export-hello-self-signed-certificate-and-private-key-toostore-it-optional"></a>Esporta certificato autofirmato hello e toostore chiave privata è (facoltativo)

È opportuno tooexport hello certificato radice autofirmato e archiviarlo in modo sicuro. Se necessario, in seguito è possibile installarlo su un altro computer e generare altri certificati client oppure esportare un altro file.cer. hello tooexport autofirmato certificato radice come una con estensione pfx, un certificato radice hello selezionare e usare hello stessi passaggi, come descritto in [esportare un certificato client](#clientexport).

## <a name="create-and-install-client-certificates"></a>Creare e installare i certificati client

Non si installa certificato autofirmato hello direttamente in computer client hello. È necessario un certificato client dal certificato autofirmato hello toogenerate. Quindi esportare e installare il computer client toohello di hello client certificato. Hello alla procedura seguente non è specifiche di modello di distribuzione. Sono validi sia per Gestione risorse che per il modello classico.

### <a name="clientcert"></a>Generazione di un certificato client

Ogni computer client che si connette tooa virtuale usando Point-to-Site deve avere installato un certificato client. Genera un certificato client dal certificato radice autofirmato hello e quindi esportare e installare il certificato client hello. Se non è stato installato il certificato client hello, l'autenticazione ha esito negativo. 

Hello passaggi seguenti consentono di eseguire la generazione di un certificato client da un certificato radice autofirmato. È possibile generare più certificati client da hello stesso certificato radice. Quando si generano i certificati client con passaggi hello riportati di seguito, certificato hello del client viene installato automaticamente nel computer di hello utilizzato certificato hello toogenerate. Se si desidera tooinstall un certificato client in un altro computer client, è possibile esportare il certificato di hello.
 
1. In hello stesso computer utilizzato hello toocreate certificato autofirmato, aprire un prompt dei comandi come amministratore.
2. Modificare ed eseguire toogenerate esempio hello un certificato client.
  * Modifica *"P2SRootCert"* toohello nome radice autofirmato hello che si desidera generare il certificato client hello da. Assicurarsi che si sta utilizzando il nome di hello del certificato radice hello, ovvero qualsiasi hello ' CN =' valore è stato specificato al momento della creazione radice autofirmato hello.
  * Modifica *P2SChildCert* nome toohello da toogenerate un toobe certificato client.

  Se si esegue l'esempio seguente senza modificarla hello, il risultato di hello è un certificato client denominato P2SChildcert nell'archivio certificati personale che è stato generato dal certificato radice P2SRootCert.

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <a name="clientexport"></a>Esportare un certificato client

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <a name="install"></a>Installare un certificato client esportato

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Passaggi successivi

Continuare con la configurazione da punto a sito. 

* Per **Gestione risorse** passaggi di distribuzione del modello, vedere [configurare un tooa connessione Point-to-Site rete virtuale](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* Per **classico** passaggi di distribuzione del modello, vedere [configurare tooa di connessione tra reti virtuali (classico) un VPN Point-to-Site](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
