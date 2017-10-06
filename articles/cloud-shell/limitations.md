---
title: limitazioni di aaaAzure Cloud Shell (anteprima) | Documenti Microsoft
description: Panoramica delle limitazioni di Azure Cloud Shell
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a>Limitazioni di Azure Cloud Shell
Azure Cloud Shell offre i seguenti di hello limitazioni note:

## <a name="system-state-and-persistence"></a>Persistenza e stato del sistema
macchina Hello che fornisce la sessione della Shell di Cloud è temporaneo e viene riciclato dopo che la sessione rimane inattiva per 20 minuti. Shell cloud richiede un toobe condivisione di file montati. Di conseguenza, la sottoscrizione deve essere in grado di tooset backup tooaccess risorse di archiviazione Cloud Shell. Altre considerazioni di cui tenere conto:
* Con l'archiviazione montata vengono conservate soltanto le modifiche apportate all'interno della directory `$Home` o `clouddrive`.
* Le condivisioni file possono essere implementate solo dall'interno dell'[area assegnata](persisting-shell-storage.md#mount-a-new-clouddrive).
* File di Azure supporta solo account di archiviazione con ridondanza locale e account di archiviazione con ridondanza geografica.

## <a name="user-permissions"></a>Autorizzazioni utente
Le autorizzazioni sono impostate come utenti normali senza accesso SUDO. Qualsiasi installazione esterna alla directory `$Home` non verrà conservata.
Anche se alcuni comandi all'interno di hello `clouddrive` directory, ad esempio `git clone`, non dispone delle autorizzazioni appropriate, il `$Home` directory dispone di autorizzazioni.

## <a name="browser-support"></a>Supporto browser
Shell cloud supporta le versioni più recenti di hello di Microsoft Internet Explorer, Microsoft Edge, Google Chrome, Mozilla Firefox e Apple Safari. Safari in modalità privata non è supportato.

## <a name="copy-and-paste"></a>Copiare e incollare
CTRL + C e Ctrl + V non funzionano come copiare e incollare collegamenti in Cloud Shell nei computer Windows, utilizzare Ctrl + ins e MAIUSC + INS toocopy e incollare rispettivamente.

Opzioni di copia e Incolla del menu sono anche disponibili, ma pulsante destro del mouse è un accesso agli Appunti toobrowser specifiche dell'oggetto.

## <a name="editing-bashrc"></a>Modifica di .bashrc
Fare attenzione quando si modifica il file con estensione bashrc, poiché questa operazione può provocare errori imprevisti in Cloud Shell.

## <a name="bashhistory"></a>.bash_history
È possibile che la cronologia dei comandi bash sia incoerente a causa dell'interruzione della sessione Cloud Shell o di sessioni simultanee.

## <a name="usage-limits"></a>Limiti di consumo
Cloud Shell è pensato per l'uso interattivo e qualsiasi sessione non interattiva in esecuzione prolungata viene quindi interrotta senza preavviso.

## <a name="network-connectivity"></a>Connettività di rete
Latenza nella Shell di Cloud è la connessione a internet toolocal soggetto, Cloud Shell continua toocarry tooattempt le eventuali istruzioni inviate.

## <a name="next-steps"></a>Passaggi successivi
[Avvio rapido di Cloud Shell](quickstart.md)
