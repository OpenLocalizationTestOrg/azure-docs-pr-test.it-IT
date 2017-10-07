---
title: Introduzione a Azure Service Fabric XPlat CLI aaaGetting
description: Introduzione all'interfaccia della riga di comando XPlat per Azure Service Fabric
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a>Utilizzo di hello XPlat CLI toointeract con un cluster di Service Fabric

È possibile interagire con i cluster di Service Fabric dai computer Linux usando hello XPlat CLI su Linux.

innanzitutto Hello è ottenere la versione più recente di hello di hello CLI da rep git hello e set, configurarlo nel percorso utilizzando hello seguenti comandi:

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

Per ogni comando, supporta, è possibile digitare nome hello della Guida in linea hello tooobtain comando hello per quel comando.
Completamento automatico è supportato per i comandi di hello. Ad esempio, hello seguente consente di comando che la Guida per tutti i comandi di applicazione hello. 

```sh
 azure servicefabric application 
```

È possibile filtrare ulteriormente i comandi specifici tooa Guida hello, come hello esempio illustrato di seguito:

```sh
 azure servicefabric application  create
```

tooenable il completamento automatico in hello CLI, eseguire hello seguenti comandi:

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

Hello seguenti comandi connettersi toohello cluster e si hello nodi cluster hello Mostra:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

toouse parametri denominati e individuare che cosa sono, è possibile digitare - Guida in linea dopo un comando. ad esempio:

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

Quando ci si connette tooa cluster con più computer da una macchina **che non fanno parte del cluster hello**, utilizzare hello comando seguente:

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

Sostituire il tag di PublicIPorFQDN hello con hello reale IP o FQDN come appropriato. Quando ci si connette tooa cluster con più computer da una macchina **che fa parte del cluster hello**, utilizzare hello comando seguente:

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

È possibile utilizzare PowerShell o toointeract CLI con il Cluster di Service Fabric Linux creato tramite hello portale di Azure.

> [!WARNING]
> Questi cluster non sono protetti, pertanto, potrebbe essere aprendo l'unica finestra aggiungendo l'indirizzo IP pubblico hello nel manifesto del cluster hello.

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a>Utilizzo di cluster di Service Fabric tooa tooconnect XPlat CLI hello

Hello seguendo i comandi CLI di Azure viene descritto come tooconnect tooa proteggere i cluster. dettagli del certificato Hello devono corrispondere al certificato sui nodi del cluster hello.

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

Se il certificato dispone di autorità di certificazione (CA), è necessario tooadd hello - ca-cert-parametro come hello di esempio seguente: 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

Se si dispone di più autorità di certificazione, è possibile utilizzare la virgola come delimitatore di hello.

Se il nome comune nel certificato hello non corrisponde a endpoint della connessione hello, è possibile utilizzare il parametro hello `--strict-ssl-false` toobypass hello verifica, come illustrato nel comando seguente hello:

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

Se si desidera verifica hello CA tooskip, è possibile aggiungere hello - parametro false non autorizzato rifiuta, come illustrato nel comando seguente hello: 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

Dopo la connessione, dovrebbe essere in grado di toorun altri toointeract comandi CLI con cluster hello.

## <a name="deploying-your-service-fabric-application"></a>Distribuzione dell'applicazione di Service Fabric

Eseguire i seguenti comandi toocopy, registrare e avviare l'applicazione di service fabric hello hello:

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a>Aggiornamento dell'applicazione

il processo di Hello è simile toohello [processo Windows](service-fabric-application-upgrade-tutorial-powershell.md)).

Compilare, copiare, registrare e creare l'applicazione dalla directory radice del progetto. Se l'istanza dell'applicazione è denominato `fabric:/MySFApp`e il tipo di hello è MySFApp, comandi hello sarebbe come indicato di seguito:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

Apportare hello Modifica applicazione tooyour e ricompilare il servizio hello modificato.  Hello aggiornamento modificate file manifesto del servizio (ServiceManifest.xml) con le versioni aggiornata di hello per hello servizio (e codice o configurazione o dati come appropriato). Inoltre modificare il manifesto dell'applicazione hello (ApplicationManifest.xml) con numero di versione di hello aggiornato per un'applicazione hello e hello servizio modificato.  A questo punto, copiare e registrare l'applicazione aggiornata utilizzando hello seguenti comandi:

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

A questo punto, è possibile avviare l'aggiornamento dell'applicazione hello con hello comando seguente:

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

Ora è possibile monitorare l'aggiornamento di applicazione hello utilizzando SFX. In pochi minuti, un'applicazione hello sarebbe sono stata aggiornata. È anche possibile provare una versione aggiornata dell'app con un errore e verificare la funzionalità di rollback automatico hello nell'infrastruttura del servizio.

## <a name="converting-from-pfx-toopem-and-vice-versa"></a>La conversione dal file PFX tooPEM e viceversa

Potrebbe essere necessario tooinstall un certificato nel computer locale (con Windows o Linux) tooaccess sicura cluster che potrebbero essere in un ambiente diverso. Ad esempio, durante l'accesso a un cluster Linux protetto da un computer Windows e viceversa potrebbe essere tooconvert il certificato dal file PFX tooPEM e viceversa. 

tooconvert da un file PFX tooa di file PEM, utilizzare hello comando seguente:

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

tooconvert da un file PEM tooa di file PFX, utilizzare hello comando seguente:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Fare riferimento troppo[OpenSSL documentazione](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) per informazioni dettagliate.

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a>Risoluzione dei problemi


### <a name="copying-of-hello-application-package-does-not-succeed"></a>Copia del pacchetto di applicazione hello non riesce

Controllare se `openssh` è installato. Per impostazione predefinita, in Ubuntu Desktop non è installato. L'installazione utilizzando hello comando seguente:

```sh
sudo apt-get install openssh-server openssh-client**
```

Se hello problema persiste, provare a disabilitare PAM per ssh modificando hello `sshd_config` file utilizzando hello seguenti comandi:

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

Se hello problema persiste, provare a numero crescente di hello di ssh sessioni eseguendo hello seguenti comandi:

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

Utilizzo di chiavi per ssh autenticazione (come anziché toopasswords) non è ancora supportata (poiché hello piattaforma Usa ssh toocopy pacchetti), quindi utilizzare l'autenticazione di password.

## <a name="next-steps"></a>Passaggi successivi

[Configurare un ambiente di sviluppo hello e distribuire un cluster di Service Fabric applicazione tooa Linux.](service-fabric-get-started-linux.md)

## <a name="related-articles"></a>Articoli correlati

* [Introduzione a Service Fabric e all'interfaccia della riga di comando di Azure 2.0](service-fabric-azure-cli-2-0.md)
