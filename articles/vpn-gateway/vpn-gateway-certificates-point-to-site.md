---
title: 'Generare ed esportare certificati autofirmati per connessioni da punto a sito: PowerShell: Azure | Microsoft Docs'
description: In questo articolo contiene passaggi toocreate un certificato radice autofirmato, esportare la chiave pubblica hello e generare i certificati client tramite PowerShell in Windows 10.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a>Generare ed esportare i certificati per le connessioni da punto a sito usando PowerShell su Windows 10

Le connessioni Point-to-Site, utilizzano tooauthenticate certificati. In questo articolo viene illustrato come certificato radice toocreate a autofirmato e generare i certificati client tramite PowerShell in Windows 10. Se si sta cercando i passaggi di configurazione da punto a sito, ad esempio come elenco di certificati radice tooupload, selezionare uno degli articoli hello ' Configure Point-to-Site' di hello seguenti:

> [!div class="op_single_selector"]
> * [Create self-signed certificates - PowerShell](vpn-gateway-certificates-point-to-site.md) (Creare certificati autofirmati - PowerShell)
> * [Creare certificati autofirmati - MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Configure Point-to-Site - Resource Manager - Azure portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md) (Eseguire una configurazione da punto a sito - Resource Manager - Portale di Azure)
> * [Configurazione da punto a sito - Gestione risorse - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Configure Point-to-Site - Classic - Azure portal](vpn-gateway-howto-point-to-site-classic-azure-portal.md) (Eseguire una configurazione da punto a sito - Classica - Portale di Azure)
> 
> 


In questo articolo in un computer che eseguono Windows 10, è necessario eseguire passaggi di hello. i cmdlet di PowerShell Hello utilizzare certificati toogenerate fanno parte del sistema operativo Windows 10 hello e non funzionano nelle altre versioni di Windows. computer Windows 10 Hello è solo necessario toogenerate hello certificati. Una volta generati certificati hello, è possibile caricarli o installarli in qualsiasi sistema operativo client supportato. 

Se non si dispone di computer Windows 10 tooa di accesso, è possibile utilizzare [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificati. Hello certificati generati usando dei metodi possono essere installati su qualsiasi [supportati](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) sistema operativo client.

## <a name="rootcert"></a>Creare un certificato radice autofirmato

Utilizzare toocreate di cmdlet New-SelfSignedCertificate hello un certificato radice autofirmato. Per altre informazioni sui parametri, vedere [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

1. Da un computer che esegue Windows 10 aprire una console di Windows PowerShell con privilegi elevati.
2. Utilizzare hello certificato radice autofirmato hello toocreate di esempio seguente. Hello seguente viene creato un certificato radice autofirmato denominato 'P2SRootCert' che viene installato automaticamente in 'Corrente\Personale\Certificati certificati'. È possibile visualizzare il certificato di hello aprendo *certmgr.msc*, o *gestire i certificati utente*.

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <a name="cer"></a>Esportare la chiave pubblica hello (con estensione cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

file exported.cer Hello deve essere caricato tooAzure. Per istruzioni, vedere [Configurare una connessione da punto a sito](vpn-gateway-howto-point-to-site-rm-ps.md#upload). un certificato radice attendibile, tooadd [in questa sezione](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) dell'articolo hello.

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a>Esporta certificato radice autofirmato hello e toostore chiave pubblica è (facoltativo)

È opportuno tooexport hello certificato radice autofirmato e archiviarlo in modo sicuro. Se necessario, in seguito è possibile installarlo su un altro computer e generare altri certificati client oppure esportare un altro file.cer. hello tooexport autofirmato certificato radice come una con estensione pfx, un certificato radice hello selezionare e usare hello stessi passaggi, come descritto in [esportare un certificato client](#clientexport).

## <a name="clientcert"></a>Generazione di un certificato client

Ogni computer client che si connette tooa virtuale usando Point-to-Site deve avere installato un certificato client. Genera un certificato client dal certificato radice autofirmato hello e quindi esportare e installare il certificato client hello. Se non è stato installato il certificato client hello, l'autenticazione ha esito negativo. 

Hello passaggi seguenti consentono di eseguire la generazione di un certificato client da un certificato radice autofirmato. È possibile generare più certificati client da hello stesso certificato radice. Quando si generano i certificati client con passaggi hello riportati di seguito, certificato hello del client viene installato automaticamente nel computer di hello utilizzato certificato hello toogenerate. Se si desidera tooinstall un certificato client in un altro computer client, è possibile esportare il certificato di hello.

esempi di Hello utilizzano toogenerate di cmdlet New-SelfSignedCertificate hello un certificato client che scade dopo un anno. Per informazioni aggiuntive sui parametri, ad esempio l'impostazione di un valore di scadenza diversa per il certificato client hello, vedere [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

### <a name="example-1"></a>Esempio 1

Questo esempio Usa hello dichiarata la variabile '$cert' dalla sezione precedente hello. Se si chiude la console di PowerShell hello dopo la creazione di hello certificato radice autofirmato o sta creando i certificati client aggiuntive in una nuova sessione di console di PowerShell, utilizzare i passaggi di hello in [esempio 2](#ex2).

Modificare ed eseguire toogenerate esempio hello un certificato client. Se si esegue l'esempio seguente senza modificarla hello, il risultato di hello è un certificato client denominato 'P2SChildCert'.  Se si desidera certificato figlio hello tooname con un altro, modificare il valore CN hello. Non modificare hello TextExtension quando si esegue questo esempio. certificato client Hello generato viene installato automaticamente in 'Certificati - corrente\Personale\Certificati' nel computer in uso.

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <a name="ex2"></a>Esempio 2

Se si sta creando i certificati client aggiuntive o sono non utilizza hello stessa sessione di PowerShell utilizzato toocreate il certificato radice autofirmato, utilizzare hello alla procedura seguente:

1. Identificare certificato radice autofirmato hello installata nel computer di hello. Questo cmdlet restituisce un elenco dei certificati installati nel computer in uso.

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. Individuare il nome soggetto hello da hello restituito l'elenco, quindi l'identificazione personale hello copia che si trova il testo successivo tooa tooit file. Nell'esempio seguente di hello, esistono due certificati. nome CN Hello è hello del certificato radice autofirmato hello da cui si desidera toogenerate un certificato figlio. In questo caso "P2SRootCert".

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. Dichiarare una variabile per il certificato radice hello con identificazione personale hello dal passaggio precedente hello. Sostituire l'identificazione personale con identificazione personale hello del certificato radice hello da cui si desidera toogenerate un certificato figlio.

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  Ad esempio, con identificazione personale hello per P2SRootCert nel passaggio precedente hello, variabile hello simile al seguente:

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  Modificare ed eseguire toogenerate esempio hello un certificato client. Se si esegue l'esempio seguente senza modificarla hello, il risultato di hello è un certificato client denominato 'P2SChildCert'. Se si desidera certificato figlio hello tooname con un altro, modificare il valore CN hello. Non modificare hello TextExtension quando si esegue questo esempio. certificato client Hello generato viene installato automaticamente in 'Certificati - corrente\Personale\Certificati' nel computer in uso.

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <a name="clientexport"></a>Esportare un certificato client   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <a name="install"></a>Installare un certificato client esportato

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Passaggi successivi

Continuare con la configurazione da punto a sito. 

* Per **Gestione risorse** passaggi di distribuzione del modello, vedere [configurare un tooa connessione Point-to-Site rete virtuale](vpn-gateway-howto-point-to-site-resource-manager-portal.md). 
* Per **classico** passaggi di distribuzione del modello, vedere [configurare tooa di connessione tra reti virtuali (classico) un VPN Point-to-Site](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
