---
title: problemi di gestione e aaaConfiguration per domande frequenti sui servizi Cloud di Microsoft Azure | Documenti Microsoft
description: Questo articolo vengono elencati hello domande frequenti sulla configurazione e gestione per i servizi Cloud di Microsoft Azure.
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 62ece142ac0ef5d45081cab333375b1a0a8f0ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemi di configurazione e gestione per Servizi cloud di Azure: domande frequenti

Questo articolo include le domande frequenti relative ai problemi di configurazione e gestione per [Servizi cloud di Microsoft Azure](https://azure.microsoft.com/services/cloud-services). È anche possibile consultare hello [pagina dimensione di macchina virtuale di servizi Cloud](cloud-services-sizes-specs.md) per informazioni sulle dimensioni.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-add-nosniff-toomy-website"></a>Aggiunta di sito Web toomy "nosniff"?
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

## <a name="how-do-i-customize-iis-for-a-web-role"></a>Come si personalizza IIS per un ruolo Web?
Utilizzare lo script di avvio IIS hello da hello [comuni attività di avvio](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) articolo.

## <a name="i-cannot-scale-beyond-x-instances"></a>Impossibile eseguire la scalabilità per un numero di istanze superiore a X
La sottoscrizione di Azure ha un limite sul numero di hello di core, che è possibile utilizzare. Il ridimensionamento non funzionerà se sono stati utilizzati tutti i core hello è disponibili. Ad esempio, se si dispone di un limite di 100 memorie centrali, vuol dire che è possibile avere 100 istanze di macchina virtuale con dimensioni A1 per il servizio cloud o 50 istanze di macchine virtuali con dimensioni A2.

## <a name="how-can-i-implement-role-based-access-for-cloud-services"></a>Come si implementa l'accesso in base al ruolo per Servizi cloud?
Servizi cloud non supporta il modello di controllo di accesso basato sui ruoli (RBAC) di hello, perché non è un servizio basato su Azure Resource Manager.

Vedere [Controllo degli accessi in base al ruolo di Azure e Amministratore sottoscrizione classico](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators).

## <a name="how-do-i-set-hello-idle-timeout-for-azure-load-balancer"></a>Impostazione di timeout di inattività hello servizio di bilanciamento del carico di Azure
È possibile specificare il timeout di hello nel file di definizione (csdef) del servizio analogo al seguente:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="mgVS2015Worker" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10100"   idleTimeoutInMinutes="30" />
    </Endpoints>
  </WorkerRole>
```
Per altre informazioni, vedere [New: Configurable Idle Timeout for Azure Load Balancer](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/) (Novità: Timeout di inattività configurabile per Azure Load Balancer).

## <a name="can-microsoft-internal-engineers-rdp-toocloud-service-instances-without-permission"></a>È possibile tecnici interni Microsoft le istanze del servizio toocloud RDP senza autorizzazione.
Segue Microsoft tooRDP di decodificare un processo strict che non consentirà l'interno nel servizio cloud senza autorizzazione (posta elettronica o altre comunicazioni scritte) è scritta da proprietario hello o da loro designata.

## <a name="why-is-hello-certificate-chain-of-my-cloud-service-ssl-certificate-incomplete"></a>Perché è incompleto catena di certificati hello del certificato SSL del servizio cloud?
È consigliabile installare hello intera catena di certificati (cert foglia, i certificati intermedi e del certificato radice) anziché solo il certificato di foglia hello. Quando si installa solo i certificati di foglia hello, basarsi sulla catena di certificati di Windows toobuild hello scorrendo hello CTL. In caso di problemi intermittenti della rete o problemi DNS in Azure o Windows Update quando si tenta certificato hello toovalidate, certificato hello può essere considerato non valido. Installando hello intera catena di certificati, è possibile evitare questo problema. Hello blog all'indirizzo [come tooinstall un certificato SSL concatenato](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/) viene illustrato come toodo questo.

## <a name="how-do-i-associate-a-static-ip-address-toomy-cloud-service"></a>Modalità di associazione di un servizio cloud toomy di indirizzo IP statico
tooset di un indirizzo IP statico, è necessario toocreate un indirizzo IP riservato. Questo indirizzo IP riservato può essere associato tooa nuovo servizio o tooan esistente distribuzione cloud. Vedere hello documenti per i dettagli seguenti:
* [Come toocreate un indirizzo IP riservato](../virtual-network/virtual-networks-reserved-public-ip.md#manage-reserved-vips)
* [Riservare hello di indirizzo IP di un servizio cloud esistente](../virtual-network/virtual-networks-reserved-public-ip.md#reserve-the-ip-address-of-an-existing-cloud-service)
* [Associare un riservato IP tooa nuovo servizio cloud](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-new-cloud-service)
* [Associare un tooa IP riservato in esecuzione la distribuzione](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-running-deployment)
* [Associare un servizio cloud di tooa IP riservato con un file di configurazione del servizio](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file)

## <a name="what-is-hello-quota-limit-for-my-cloud-service"></a>Che cos'è il limite di quota hello per il servizio cloud?
Vedere [Limiti specifici del servizio](../azure-subscription-service-limits.md#subscription-limits).

## <a name="why-does-hello-drive-on-my-cloud-service-vm-show-very-little-free-disk-space"></a>Perché il servizio cloud VM unità hello visualizzato poco spazio libero su disco?
Tale comportamento è previsto, e non dovrebbe causare qualsiasi applicazione tooyour problema. Inserimento nel journal è attivata per hello % uproot % unità nelle macchine virtuali di Azure PaaS, che essenzialmente utilizza double hello quantità di spazio file occupano normalmente. Esistono tuttavia alcune operazioni toobe tenere presente, essenzialmente diventare un problema.

Hello approot % % della dimensione unità viene calcolata come < dimensioni del file con estensione cspkg + dimensione massima del diario > + un margine di spazio disponibile, 1,5 GB, o qualunque sia il maggiore. dimensioni Hello della macchina virtuale non sono rilevante per questo calcolo. (hello dimensioni della VM influisce solo su dimensioni hello dell'unità c: temporaneo hello.) 

È supportato toowrite toohello % approot % unità. Se si sta scrivendo toohello macchina virtuale di Azure, è necessario farlo in una risorsa LocalStorage temporanea (o un'altra opzione, ad esempio l'archiviazione Blob, file di Azure, ecc.). Hello spazio libero nella cartella hello % approot % non è pertanto significativo. Se non si certi se unità toohello % approot % scrittura dell'applicazione, è sempre possibile consentire al servizio Esegui per alcuni giorni e quindi Confronta hello "before" e "after" dimensioni. 

Azure non scrivono alcun elemento toohello % approot % unità. Una volta hello disco rigido virtuale viene creato dal file cspkg e montato in hello macchina virtuale di Azure, hello unico elemento che può scrivere toothis unità è l'applicazione. 

le impostazioni di registrazione di Hello sono non configurabile in modo non è possibile disattivare.

## <a name="what-are-hello-features-and-capabilities-that-azure-basic-ipsids-and-ddos-provides"></a>Quali sono hello e le funzionalità che fornisce gli indirizzi IP di base Azure o gli ID e DDOS?
Azure offre gli ID e gli indirizzi IP in Data Center server fisici toodefend minacce. I clienti possono anche distribuire soluzioni di sicurezza di terze parti, ad esempio web application firewall, firewall di rete, antimalware, sistemi di rilevamento delle intrusioni, sistemi di prevenzione e altro ancora. Per altre informazioni, vedere [Protect your data and assets and comply with global security standards](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity) (Proteggere dati e asset e rispettare gli standard di sicurezza globali).

Microsoft monitora costantemente minacce toodetect server, reti e applicazioni. L'approccio ramificazioni minaccia-gestione di Azure Usa il rilevamento delle intrusioni, attacchi di prevenzione, test di penetrazione, comportamento analitica, il rilevamento di anomalie distributed denial of service (DDoS) e machine learning tooconstantly rafforzare la difesa e ridurre i rischi. Microsoft Antimalware per Azure protegge i servizi cloud e le macchine virtuali di Azure. Hai soluzioni per la sicurezza di terze parti toodeploy hello opzione, inoltre, ad esempio tramite firewall di applicazione web, i firewall di rete, antimalware, rilevare e prevenire i sistemi delle intrusioni (ID/IP) e altro ancora.

## <a name="why-does-iis-stop-writing-toohello-log-directory"></a>Perché IIS interrompere la scrittura di directory di log toohello?
Quota di archiviazione locale di hello per la scrittura di directory di log toohello aver esaurito. Per risolvere il problema, è possibile eseguire una delle tre operazioni seguenti:
* Abilitare la diagnostica per IIS e capacità di archiviazione tooblob diagnostica periodicamente spostata hello.
* Rimuovere manualmente i file di log da directory di registrazione hello.
* Aumentare il limite di quota per le risorse locali.

Per ulteriori informazioni, vedere hello seguenti documenti:
* [Archiviare e visualizzare i dati di diagnostica in Archiviazione di Azure](cloud-services-dotnet-diagnostics-storage.md)
* [IIS Logs stops writing in cloud service](https://blogs.msdn.microsoft.com/cie/2013/12/21/iis-logs-stops-writing-in-cloud-service/) (I log di IIS non vengono più scritti nel servizio cloud)

## <a name="what-is-hello-purpose-of-hello-windows-azure-tools-encryption-certificate-for-extensions"></a>Qual è la funzione hello di "Windows Azure estensioni degli strumenti di crittografia certificato per" hello?
Questi certificati vengono creati automaticamente ogni volta che si aggiunge il servizio di cloud toohello un'estensione. In genere, questo è hello estensione WAD o hello estensione RDP, ma può trattarsi di altri utenti, ad esempio hello estensione Antimalware o Log Collector. Questi certificati vengono utilizzati solo per la crittografia e decrittografia configurazione privata di hello per estensione hello. Data di scadenza Hello mai è selezionata, pertanto non è rilevante se hello certificato è scaduto. 

È possibile ignorare questi certificati. Se si desidera pulire certificati hello, è possibile eliminarli tutti. Azure genererà un errore se si tenta di toodelete un certificato che è in uso.

## <a name="how-can-i-generate-a-certificate-signing-request-csr-without-rdp-ing-in-toohello-instance"></a>Come è possibile generare una firma richiesta certificato (CSR) senza "RDP ing" nell'istanza toohello?
Vedere hello fornite nel documento seguente:

>[Obtaining a certificate for use with Windows Azure Web Sites (WAWS)](https://azure.microsoft.com/blog/obtaining-a-certificate-for-use-with-windows-azure-web-sites-waws/) (Ottenere un certificato per l'uso con Siti Web di Azure)

Si noti che una richiesta di firma del certificato è semplicemente un file di testo. NON dispone di toobe creato dal computer hello in cui il certificato di hello verrà utilizzato. Sebbene in questo documento per un servizio App, hello creazione CSR è generico e si applica anche per i servizi Cloud.
