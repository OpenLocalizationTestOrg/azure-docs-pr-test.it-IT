---
title: i certificati di servizi e la gestione aaaCloud | Documenti Microsoft
description: Informazioni su come toocreate e utilizzare i certificati con Microsoft Azure
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: fc70d00d-899b-4771-855f-44574dc4bfc6
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 69cb5467ece58a91dae06b4120954aeb2826bde1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="certificates-overview-for-azure-cloud-services"></a>Panoramica sui certificati per i servizi cloud di Azure
I certificati vengono usati in Azure per i servizi cloud ([certificati di servizio](#what-are-service-certificates)) e per l'autenticazione con l'API di gestione di hello ([i certificati di gestione](#what-are-management-certificates) quando utilizzando hello portale di Azure classico e non Hello non classico portale di Azure). In questo argomento fornisce una panoramica generale dei due tipi di certificato, come troppo[creare](#create) e [distribuire](#deploy) li tooAzure.

Quelli usati in Azure sono certificati x.509 v3 e possono essere firmati da un altro certificato attendibile o essere autofirmati. Un certificato autofirmato viene firmato dall'autore e pertanto non è attendibile per impostazione predefinita. La maggior parte dei browser può ignorare questo problema. È consigliabile utilizzare i certificati autofirmati solo quando si sviluppano e si testano servizi cloud. 

I certificati usati da Azure possono contenere una chiave privata o una pubblica. I certificati hanno un'identificazione digitale che fornisce un mezzo tooidentify loro in modo non ambiguo. Questa identificazione personale viene usata in hello Azure [file di configurazione](cloud-services-configure-ssl-certificate.md) tooidentify che un servizio cloud del certificato deve utilizzare. 

## <a name="what-are-service-certificates"></a>Cosa sono i certificati di servizio?
I certificati di servizio sono servizi collegati toocloud e abilitare tooand comunicazione protetta dal servizio hello. Ad esempio, se è stato distribuito un ruolo web, desideri toosupply un certificato che è possibile eseguire l'autenticazione di un endpoint HTTPS esposto. I certificati di servizio, definiti nella definizione del servizio, sono macchina virtuale toohello distribuito automaticamente in cui è in esecuzione un'istanza del ruolo. 

È possibile caricare classica tooAzure certificati di servizio portale tramite hello Azure classica portale o tramite il modello di distribuzione classica hello. I certificati di servizio sono associati a uno specifico servizio cloud. Vengono assegnati tooa distribuzione nel file di definizione del servizio hello.

I certificati di servizio possono essere gestiti separatamente dai servizi e da persone diverse. Ad esempio, uno sviluppatore potrebbe caricare un pacchetto del servizio che fa riferimento il certificato tooa che un responsabile IT è stato caricato precedentemente tooAzure. Un responsabile IT può gestire e rinnovare il certificato (Modifica configurazione hello del servizio di hello) senza la necessità di tooupload un nuovo pacchetto del servizio. L'aggiornamento senza un nuovo pacchetto del servizio è possibile perché nel file di definizione del servizio hello nome logico di hello, nome dell'archivio e percorso del certificato hello e durante l'identificazione personale del certificato hello è specificato nel file di configurazione del servizio hello. certificato di hello tooupdate, è solo necessario tooupload un nuovo certificato e l'identificazione personale hello Modifica valore nel file di configurazione del servizio hello.

>[!Note]
>Hello [domande frequenti su servizi Cloud](cloud-services-faq.md) articolo contiene alcune informazioni utili sui certificati.

## <a name="what-are-management-certificates"></a>Cosa sono i certificati di gestione?
I certificati di gestione consentono di tooauthenticate con modello di distribuzione classica hello. Molti programmi e strumenti (ad esempio Visual Studio o hello Azure SDK) di utilizzare questi configurazione tooautomate dei certificati e la distribuzione dei vari servizi di Azure. Non sono servizi toocloud effettivamente correlati. 

> [!WARNING]
> Fare attenzione. Questi tipi di certificati consentono di qualsiasi utente che esegue l'autenticazione con le sottoscrizioni di hello toomanage sono associate. 
> 
> 

### <a name="limitations"></a>Limitazioni
È previsto un limite di 100 certificati di gestione per ogni sottoscrizione. È anche previsto un limite di 100 certificati di gestione per tutte le sottoscrizioni che fanno riferimento all'ID utente di un amministratore del servizio specifico. Se è necessario per i certificati più hello ID utente per amministratore dell'account hello è già stato utilizzato tooadd 100 certificati di gestione, è possibile aggiungere un certificati aggiuntivi di CO-amministratore tooadd hello. 

Prima di aggiungere più di 100 certificati, verificare se è possibile riutilizzarne uno esistente. L'utilizzo di coamministratori aggiunge un processo di gestione dei certificati tooyour potrebbe rendere più complesso.

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a>Creare un nuovo certificato autofirmato
È possibile utilizzare qualsiasi toocreate disponibile lo strumento un certificato autofirmato, purché siano conformi alle impostazioni toothese:

* Un certificato X.509.
* Contiene una chiave privata.
* Viene creato per lo scambio di chiave (file PFX).
* Nome del soggetto deve corrispondere il servizio cloud hello di hello dominio utilizzato tooaccess.

    > Non è possibile acquistare un certificato SSL per cloudapp.net hello (o per qualsiasi correlate ad Azure) dominio. nome del soggetto del certificato Hello deve corrispondere tooaccess nome di dominio personalizzato hello l'applicazione. Ad esempio **contoso.net**, non **contoso.cloudapp.net**.

* Crittografia minima a 2048 bit.
* **Solo certificati di servizio**: certificato client deve risiedere in hello *personale* archivio certificati.

Sono disponibili due semplici modi toocreate un certificato in Windows, con hello `makecert.exe` utilità o IIS.

### <a name="makecertexe"></a>Makecert.exe
Questa utilità è stata deprecata e di seguito non è più disponibile la relativa documentazione. Per altre informazioni, vedere [questo articolo di MSDN](https://msdn.microsoft.com/library/windows/desktop/aa386968).

### <a name="powershell"></a>PowerShell
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> Se si desidera certificato hello toouse con un indirizzo IP anziché un dominio, è possibile utilizzare l'indirizzo IP hello nel parametro - DnsName hello.


Se si desidera toouse [certificato con il portale di gestione di hello](../azure-api-management-certs.md), esportarlo tooa **con estensione cer** file:

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)
Non sono presenti numerose pagine in hello internet che illustrano come toodo con IIS. [Qui](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) ce n’è uno ottimo che ho trovato che ritengo che spieghi bene. 

### <a name="java"></a>Java
È possibile utilizzare anche Java[creare un certificato](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).

### <a name="linux"></a>Linux
[Questo](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articolo viene descritto l'utilizzo toocreate dei certificati con SSH.

## <a name="next-steps"></a>Passaggi successivi
[Caricare il toohello certificato servizio portale di Azure classico](cloud-services-configure-ssl-certificate.md) (o hello [portale di Azure](cloud-services-configure-ssl-certificate-portal.md)).

Caricare un [certificato di gestione API](../azure-api-management-certs.md) toohello portale di Azure classico. portale di Azure Hello non utilizza i certificati di gestione per l'autenticazione.

