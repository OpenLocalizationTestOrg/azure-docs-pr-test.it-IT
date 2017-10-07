---
title: elenco di controllo protezione dell'infrastruttura del servizio aaaAzure | Documenti Microsoft
description: Questo articolo include un set di elenchi di controllo per la sicurezza di Azure Service Fabric.
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: 10ffaea9e7e4de6d758b0a57a79e269c87bfd14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-checklist"></a>Elenco di controllo per la sicurezza di Azure Service Fabric
Questo articolo include un elenco di controllo di facile utilizzo che aiuta a proteggere l'ambiente Azure Service Fabric.

## <a name="introduction"></a>Introduzione
Azure Service Fabric è una piattaforma di sistemi distribuiti che rende facile toopackage, distribuire e gestire microservizi scalabili e affidabili. Service Fabric risolve inoltre le sfide significativo hello nello sviluppo e la gestione delle applicazioni cloud. Gli sviluppatori e gli amministratori non devono più occuparsi di risolvere complessi problemi di infrastruttura e possono concentrarsi sull'implementazione di carichi di lavoro cruciali e impegnativi, con la certezza di assicurare scalabilità, affidabilità e gestibilità.

## <a name="checklist"></a>Elenco di controllo
Utilizzare hello seguente toohelp elenco di controllo per assicurarsi che ancora stato trascurato eventuali problemi importanti di gestione e configurazione di una soluzione di Azure Service Fabric protetta.


|Categoria dell'elenco di controllo| Descrizione |
| ------------ | -------- |
|[Controllo degli accessi in base al ruolo (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles) | <ul><li>Controllo degli accessi consente hello cluster amministratore toolimit accesso toocertain le operazioni del cluster per diversi gruppi di utenti, di rendere più sicuro cluster hello.</li><li>Gli amministratori hanno capacità di toomanagement accesso completo (incluse le funzionalità di lettura/scrittura). </li><li>   Gli utenti, per impostazione predefinita, dispongono solo dell'accesso in lettura toomanagement funzionalità (ad esempio, funzionalità di query), hello possibilità tooresolve applicazioni e servizi e.</li></ul>|
|[Certificati X.509 e Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>È consigliabile creare i [certificati](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/working-with-certificates) usati nei cluster che eseguono carichi di lavoro di produzione con un servizio certificati di Windows Server configurato correttamente oppure ottenerli da un'[autorità di certificazione (CA)](https://en.wikipedia.org/wiki/Certificate_authority) approvata.</li><li>Non usare mai in fase di produzione [certificati temporanei o di test](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development) creati con strumenti come [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968.aspx). </li><li>È possibile usare un [certificato autofirmato](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security), ma lo si deve fare solo per i cluster di test e non nell'ambiente di produzione.</li></ul>|
|[Sicurezza del cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>scenari di sicurezza cluster Hello includono nodi di sicurezza, al nodo Client, [il controllo di accesso basato sui ruoli (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles).</li></ul>|
|[Autenticazione del cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Autentica la [comunicazione da nodo a nodo](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/service-fabric/service-fabric-cluster-security.md) per la federazione di cluster. </li></ul>|
|[Autenticazione del server](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Autentica hello [endpoint di gestione del cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-portal) tooa client di gestione.</li></ul>|
|[Sicurezza delle applicazioni](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm)| <ul><li>Crittografia e decrittografia dei valori di configurazione dell'applicazione.</li><li> Crittografia dei dati tra i nodi durante la replica.</li></ul>|
|[Certificato del cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security) | <ul><li>Questo certificato è obbligatorio toosecure hello comunicazione tra i nodi di hello in un cluster.</li><li>  Impostare identificazione personale hello del certificato primario hello hello sezione identificazione personale e quello di hello secondaria nelle variabili ThumbprintSecondary hello.</li></ul>|
|[ServerCertificate](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security)| <ul><li>Questo certificato viene presentato toohello client durante il tentativo di tooconnect toothis cluster. È possibile usare due diversi certificati del server, uno primario e uno secondario per l'aggiornamento.</li></ul>|
|ClientCertificateThumbprints| <ul><li>Si tratta di un set di certificati che si desidera tooinstall nei client hello autenticato. </li></ul>|
|ClientCertificateCommonNames| <ul><li>Impostare hello nome comune del certificato client prima di hello hello CertificateCommonName. Hello CertificateIssuerThumbprint è l'identificazione personale hello per emittente hello del certificato. </li></ul>|
|ReverseProxyCertificate| <ul><li>Si tratta di un certificato facoltativo che può essere specificato se si desidera toosecure il [Proxy inverso](https://docs.microsoft.com/en-in/azure/service-fabric/service-fabric-reverseproxy). </li></ul>|
|Insieme di credenziali delle chiavi| <ul><li>Utilizzato toomanage certificati per i cluster di Service Fabric in Azure.  </li></ul>|


## <a name="next-steps"></a>Passaggi successivi
- [Processo di aggiornamento del cluster di infrastruttura di servizi e operazioni eseguibile dall'utente](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-upgrade)
- [Gestione delle applicazioni di Infrastruttura di servizi in Visual Studio](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-manage-application-in-visual-studio).
- [Introduzione al monitoraggio dell'integrità di Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-health-introduction).
