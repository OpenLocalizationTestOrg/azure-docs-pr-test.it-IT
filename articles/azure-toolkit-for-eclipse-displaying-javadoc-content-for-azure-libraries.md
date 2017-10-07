---
title: aaaDisplaying contenuto Javadoc in Eclipse per hello pacchetto di librerie di Azure per Java
description: Come toodisplay hello contenuto Javadoc per hello le librerie di Azure in Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a>Visualizzazione di contenuto Javadoc in Eclipse per hello pacchetto di librerie di Azure per Java
Hello contenuto Javadoc per Azure Libraries for Java hello può essere visualizzato all'interno dell'ambiente Eclipse associando toohello contenuto Javadoc di hello Azure Libraries for Java. Hello passaggi seguenti viene illustrato come toouse questa funzionalità in Eclipse.

Questa procedura presuppone che Hello Azure Library per il percorso di compilazione Java tooyour è già stato aggiunto.

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a>toodisplay contenuto Javadoc in Eclipse per hello Azure Libraries for Java
* In Project Explorer di Eclipse, in hello **Referenced Libraries** sezione del progetto, hello Apri menu di scelta rapida della libreria di Azure per Java JAR hello. Ad esempio, **0.1.0.jar-microsoft-Azure-api** (numero di versione di hello potrebbe essere diverse, a seconda della versione installata).

* Fare clic su **Proprietà**.

* All'interno di hello **proprietà** finestra di dialogo, nel riquadro di sinistra hello, fare clic su **Javadoc Location**. Hello **Javadoc Location** viene visualizzata una finestra di dialogo.

* È possibile specificare un **URL Javadoc** o un **Javadoc nell'archivio**.

   * Se si sceglie toospecify un **Javadoc URL**, utilizzare ad esempio hello URL **http://dl.windowsazure.com/javadoc** o **http://dl.windowsazure.com/storage/javadoc**.

   * Se si sceglie toouse **Javadoc in archive**, è possibile specificare un file esterno o un file di area di lavoro.

   Effettuare la selezione e sfogliare/convalidare in base alle esigenze. Hello esempio associa hello Azure Libraries for Java hello corrispondente file JAR di Javadoc è stato scaricato localmente tooa cartella denominata **c:\MyAzureJARs**.

   ![][ic553487]

* *Passaggio facoltativo*: fare clic su **Convalida**. Potenziali problemi con i file JAR di Javadoc hello potrebbero essere visualizzati.

* Fare clic su **OK**.

Una volta associato libreria hello, hello contenuto Javadoc deve essere visualizzato nell'IDE di Eclipse. Ad esempio, se `blob` è definito come tipo `CloudBlockBlob` all'interno del codice, hello seguito è riportato un esempio del contenuto Javadoc che viene visualizzata quando si digita `blob.acquireLease` nel codice:

![][ic553488]

## <a name="see-also"></a>Vedere anche
[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]

[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[L'installazione di hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse] 

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
