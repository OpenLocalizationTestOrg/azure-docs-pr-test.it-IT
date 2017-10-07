---
title: ruoli di servizi Cloud aaaAzure domande frequenti | Documenti Microsoft
description: Domande frequenti su Servizi cloud di Azure. L'articolo contiene risposte ad alcune domande frequenti su certificati, ruoli Web e ruoli di lavoro.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a>Domande frequenti sui servizi cloud
Questo articolo risponde ad alcune domande frequenti sui servizi cloud di Microsoft Azure. È inoltre possibile visitare hello [domande frequenti su Azure supporta](http://go.microsoft.com/fwlink/?LinkID=185083) per informazioni generali su Azure prezzi e supporto. È anche possibile consultare hello [pagina dimensione di macchina virtuale di servizi Cloud](cloud-services-sizes-specs.md) per informazioni sulle dimensioni.

## <a name="certificates"></a>Certificati
### <a name="where-should-i-install-my-certificate"></a>Dove deve essere installato il certificato?
* **My**  
  Certificato dell'applicazione con chiave privata (con estensione \*pfx, \*p12).
* **CA**  
  Tutti i certificati intermedi, come CA secondari e criteri, vanno in questo archivio.
* **ROOT**  
  autorità di certificazione radice Hello store, il certificato della CA radice deve fare clic qui.

### <a name="i-cant-remove-expired-certificate"></a>Non è possibile rimuovere un certificato scaduto
Azure impedisce la rimozione di un certificato mentre viene usato. È necessario tooeither delete hello che utilizza il certificato di hello oppure aggiornamento hello distribuzione con un certificato diverso o rinnovato.

### <a name="delete-an-expired-certificate"></a>Eliminare un certificato scaduto
Come certificato hello non è in uso, è possibile utilizzare hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) tooremove cmdlet PowerShell un certificato.

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a>Sono presenti certificati scaduti denominati Gestione dei servizi Microsoft Azure per le estensioni
Questi certificati vengono creati ogni volta che si aggiunge il servizio cloud toohello, ad esempio hello estensione Desktop remoto di un'estensione. Questi certificati vengono utilizzati solo per la crittografia e decrittografia configurazione privata di hello dell'estensione hello. Non è un problema se questi certificati scadono, Data di scadenza Hello non è selezionata.

### <a name="certificates-i-have-deleted-keep-reappearing"></a>I certificati eliminati continuano a riapparire
Molto probabilmente questi certificati continuano a ricomparire a causa di uno strumento che si sta usando, ad esempio Visual Studio. Ogni volta che si riconnette con uno strumento che utilizza un certificato, verrà nuovamente tooAzure caricato.

### <a name="my-certificates-keep-disappearing"></a>I certificati continuano a scomparire
Quando l'istanza di macchina virtuale hello viene riciclato, tutte le modifiche locali vengono perse. Utilizzare un [attività di avvio](cloud-services-startup-tasks.md) macchina virtuale di tooinstall certificati toohello ogni ora hello avviato.

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a>Non è possibile trovare i certificati di gestione nel portale di hello
[I certificati di gestione](../azure-api-management-certs.md) sono disponibili solo in hello portale classico di Azure. portale di Azure corrente Hello non utilizza i certificati di gestione. 

### <a name="how-can-i-disable-a-management-certificate"></a>Come è possibile disabilitare un certificato di gestione?
[certificati di gestione](../azure-api-management-certs.md) non possono essere disabilitati. È eliminarli tramite hello portale di Azure classico quando non si desidera toobe più utilizzato.

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a>Come è possibile creare un certificato SSL per un indirizzo IP specifico?
Seguire le direzioni di hello in hello [creare un'esercitazione certificato](cloud-services-certs-create.md). Utilizzare l'indirizzo IP hello come hello nome DNS.

## <a name="security"></a>Sicurezza
### <a name="disable-ssl-30"></a>Disabilitare SSL 3.0
toodisable SSL 3.0 e TLS utilizzo, protezione, creare un'attività di avvio è documentata in questo post di blog: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/

### <a name="add-nosniff-tooyour-website"></a>Aggiungere **nosniff** sito Web tooyour
i client tooprevent dall'analisi dei tipi MIME hello, aggiungere un'impostazione nel *Web. config* file.

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

È possibile aggiungerla anche come impostazione in IIS. Comando che segue hello di utilizzo con hello [comuni attività di avvio](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) articolo.

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a>Personalizzare IIS per un ruolo Web
Utilizzare lo script di avvio IIS hello da hello [comuni attività di avvio](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) articolo.

## <a name="scaling"></a>Ridimensionamento
### <a name="i-cannot-scale-beyond-x-instances"></a>Impossibile eseguire la scalabilità per un numero di istanze superiore a X
La sottoscrizione di Azure ha un limite sul numero di hello di core, che è possibile utilizzare. Il ridimensionamento non funzionerà se sono stati utilizzati tutti i core hello è disponibili. Ad esempio, se si dispone di un limite di 100 memorie centrali, vuol dire che è possibile avere 100 istanze di macchina virtuale con dimensioni A1 per il servizio cloud o 50 istanze di macchine virtuali con dimensioni A2.

## <a name="networking"></a>Rete
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Non è possibile riservare un indirizzo IP in un servizio cloud con più indirizzi VIP
Innanzitutto, assicurarsi che tale istanza di macchina virtuale hello che si sta tentando di IP hello tooreserve per sia attivata. In secondo luogo, verificare che si usi IP riservati per le distribuzioni di gestione temporanea e produzione hello integra. **Non** modificare le impostazioni di hello durante l'aggiornamento di distribuzione hello.

## <a name="remote-desktop"></a>Desktop remoto
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Come si usa Desktop remoto quando si ha un gruppo di sicurezza di rete?
Aggiungere regole toohello NSG che consentano il traffico sulle porte **3389** e **20000**.  Desktop remoto usa la porta **3389**.  Le istanze del servizio cloud sono con carico bilanciato, pertanto non è possibile controllare direttamente quale tooconnect istanza di.  Hello *RemoteForwarder* e *RemoteAccess* gli agenti di gestire il traffico RDP e consentire hello client toosend un cookie RDP e specificare tooconnect una singola istanza di.  Hello *RemoteForwarder* e *RemoteAccess* agenti richiedono tale porta **20000*** aperto, che può essere bloccato se si dispone di un gruppo.
