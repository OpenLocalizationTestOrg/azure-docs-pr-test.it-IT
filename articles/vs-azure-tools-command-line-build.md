---
title: compilazione da riga di aaaCommand per Azure | Documenti Microsoft
description: Compilazione da riga di comando per Azure
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: kraigb
ms.openlocfilehash: 295b61ba162dd4373ee3f56cc1462decb3e16762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="building-azure-projects-from-hello-command-line"></a>Compilazione di progetti di Azure dalla riga di comando hello
Utilizza hello Microsoft Build Engine (MSBuild), è possibile compilare prodotti in ambienti lab di compilazione in cui non è installato Visual Studio. MSBuild usa per i file di progetto il formato XML, che è estendibile e completamente supportato da Microsoft. Utilizzando il formato di file MSBuild hello, è possibile descrivere quali elementi devono essere compilati per uno o più piattaforme e configurazioni.

È anche possibile eseguire MSBuild dalla riga di comando hello e questo approccio è descritto in questo argomento. Impostando le proprietà nella riga di comando hello, è possibile compilare configurazioni specifiche di un progetto. È inoltre possibile definire in modo analogo, MSBuild compila le destinazioni hello. Per altre informazioni sui parametri della riga di comando e su MSBuild, vedere [Riferimenti alla riga di comando di MSBuild](https://msdn.microsoft.com/library/ms164311.aspx).

## <a name="msbuild-parameters"></a>Parametri MSBuild
toocreate modo più semplice di Hello un pacchetto è toorun MSBuild con hello `/t:Publish` opzione. Per impostazione predefinita, questo comando crea una directory nella cartella radice toohello di relazione per il progetto di hello, ad esempio `<ProjectDirectory>\bin\Configuration\app.publish\`. Quando si compila un progetto Azure, vengono generati due file: hello file del pacchetto e il relativo file di configurazione hello:

* File del pacchetto (`project.cspkg`)
* File di configurazione(`ServiceConfiguration.TargetProfile.cscfg`)

Per impostazione predefinita, ogni progetto Azure include un file di configurazione del servizio per le compilazioni locali (debug) e un altro per le compilazioni cloud (gestione temporanea o produzione), ma è possibile aggiungere o rimuovere i file di configurazione del servizio in base alle proprie esigenze. Quando si compila un pacchetto all'interno di Visual Studio, verrà chiesto tooinclude quali file di configurazione del servizio insieme ai pacchetti hello. Quando si compila un pacchetto utilizzando MSBuild, i file di configurazione del servizio locale hello è incluso per impostazione predefinita. file tooinclude una configurazione del servizio diversi, hello set `TargetProfile` proprietà di hello comando MSBuild (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).

Se si desidera toouse una directory alternativa per hello memorizzati file di pacchetto e la configurazione, set hello percorso utilizzando hello `/p:PublishDir=Directory\` opzione, tra cui hello separatore barra rovesciata finale.

## <a name="next-steps"></a>Passaggi successivi
Una volta creato il pacchetto di hello, è possibile distribuire tooAzure. Per un'esercitazione che illustra come tooautomate che elaborano, vedere [il recapito continuo per servizi Cloud in Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).

