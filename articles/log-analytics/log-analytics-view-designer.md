---
title: aaaCreate viste tooanalyze dati di OMS Log Analitica | Documenti Microsoft
description: "Visualizza finestra di progettazione nel Log Analitica consente personalizzato toocreate viste che vengono visualizzate nel portale OMS e Azure hello e contengono diverse visualizzazioni dei dati nel repository OMS hello. In questo articolo è presentata una panoramica su Progettazione viste e sulle procedure per creare e modificare viste personalizzate."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: ce41dc30-e568-43c1-97fa-81e5997c946a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 40b4bfef50d70e4479b6cae16abfa8ec33d1a2f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-view-designer-toocreate-custom-views-in-log-analytics"></a>Utilizzare le visualizzazioni personalizzate di toocreate Visualizza finestra di progettazione in Log Analitica
Hello Visualizza finestra di progettazione in [Log Analitica](log-analytics-overview.md) consente toocreate le visualizzazioni personalizzate nella console OMS hello contenenti visualizzazioni diverse dei dati nel repository OMS hello. In questo articolo è presentata una panoramica su Progettazione viste e sulle procedure per creare e modificare viste personalizzate.

Altri articoli disponibili su Progettazione viste sono:

* [Riquadro riferimento](log-analytics-view-designer-tiles.md) -riferimento delle impostazioni di hello per ognuna delle hello riquadri toouse disponibili nelle visualizzazioni personalizzate.
* [Riferimento alla parte visualizzazione](log-analytics-view-designer-parts.md) -riferimento delle impostazioni di hello per ognuna delle hello riquadri toouse disponibili nelle visualizzazioni personalizzate.

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), le query in tutte le visualizzazioni devono essere scritti in hello [nuovo linguaggio di query](https://go.microsoft.com/fwlink/?linkid=856078).  Le viste che sono state create prima dell'area di lavoro di hello è stato aggiornato sarà venga convertito.

## <a name="concepts"></a>Concetti
Viste create con progettazione vista hello contengono elementi hello hello nella tabella seguente.

| Parte: | Descrizione |
|:--- |:--- |
| Riquadro |Visualizzato nel dashboard Panoramica Analitica Log principale hello.  Include un riepilogo visual informazioni hello contenute in hello visualizzazione personalizzata.  Diversi tipi di sezioni forniscono visualizzazioni diverse di record nel repository OMS hello.  Fare clic su hello hello tooopen riquadro Vista personalizzata. |
| Vista personalizzata |Quando hello utente fa clic sul riquadro hello.  Contiene una o più parti della visualizzazione. |
| Parti della visualizzazione |Visualizzazione dei dati nel repository OMS hello in base a uno o più [log ricerche](log-analytics-log-searches.md).  La maggior parte delle parti includerà un'intestazione che fornisce una visualizzazione di alto livello e un elenco di risultati superiore hello.  Tipi di parte diversa forniscono visualizzazioni diverse di record nel repository OMS hello.  Fare clic sugli elementi hello parte tooperform una ricerca di log che fornisce i record dettagliati. |

![Panoramica di Progettazione viste](media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-tooyour-workspace"></a>Aggiungere l'area di lavoro di progettazione tooyour
Mentre Progettazione viste è disponibile in anteprima, è necessario aggiungerla tooyour dell'area di lavoro selezionando **le funzionalità di anteprima** in hello **impostazioni** sezione del portale OMS hello.

![Abilitazione dell'anteprima](media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a>Creazione e modifica di viste
### <a name="create-a-new-view"></a>Creazione di una nuova vista
Aprire una nuova vista in hello **Visualizza finestra di progettazione** facendo clic su Visualizza finestra di progettazione hello riquadro nel dashboard OMS principale hello.

![Riquadro Progettazione viste](media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a>Modifica di una vista esistente
una vista esistente in visualizzazione progettazione, hello aprire visualizzazione facendo clic su un riquadro nel dashboard OMS principale hello hello tooedit.  Quindi fare clic su hello **modifica** pulsante visualizzazione hello tooopen hello Visualizza finestra di progettazione.

![Modifica di una vista](media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a>Clonazione di una vista esistente
Quando si clona una vista, crea una nuova vista e verrà aperto in visualizzazione Progettazione hello.  nuova vista Hello avrà hello stesso nome come hello originale con fine toohello aggiunto "Copia".  una vista, aprire tooclone hello vista esistente facendo clic su un riquadro nel dashboard OMS principale hello.  Quindi fare clic su hello **Clone** pulsante visualizzazione hello tooopen hello Visualizza finestra di progettazione.

![Clonazione di una vista](media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a>Eliminazione di una vista esistente
toodelete una vista esistente, aprire hello visualizzazione facendo clic su un riquadro nel dashboard OMS principale hello.  Quindi fare clic su hello **modifica** pulsante visualizzazione hello tooopen hello Visualizza finestra di progettazione e fare clic su **Elimina visualizzazione**.

![Eliminazione di una vista](media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a>Esportazione di una vista esistente
È possibile esportare un file JSON tooa di visualizzazione che è possibile importare in un'altra area di lavoro o utilizzare un [modello di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).  tooexport una vista esistente, aprire hello visualizzazione facendo clic su un riquadro nel dashboard OMS principale hello.  Quindi fare clic su hello **esportare** pulsante toocreate un file nella cartella di download del browser hello.  nome di Hello del file hello sarà hello nome della vista hello con estensione hello *omsview*.

![Esportazione di una vista](media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a>Importazione di una vista esistente
È possibile importare un file *omsview* precedentemente esportato da un altro gruppo di gestione.  tooimport una vista esistente, creare innanzitutto una nuova vista.  Quindi fare clic su hello **importazione** pulsante e seleziona hello *omsview* file.  configurazione di Hello nel file hello verrà copiati in una vista esistente hello.

![Esportazione di una vista](media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a>Uso di Progettazione viste
Hello Visualizza finestra di progettazione dispone di tre riquadri.  Hello **progettazione** riquadro rappresenta la visualizzazione personalizzata hello.  Quando si aggiungono riquadri e le parti da hello **controllo** riquadro toohello **progettazione** riquadro sono aggiunti toohello visualizzazione.  Hello **proprietà** riquadro verranno visualizzati le proprietà di hello per riquadro hello o parte selezionata.

![Progettazione viste](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a>Configurazione del riquadro di vista
Una vista personalizzata può avere solo un singolo riquadro.  Seleziona hello **riquadro** scheda hello **controllo** riquadro tooview hello corrente riquadro o selezionarne uno alternativo.  Hello **proprietà** riquadro verranno visualizzati proprietà hello per tile corrente hello.  Configurare le proprietà del riquadro hello in base toohello informazioni dettagliate in hello [riquadro riferimento](log-analytics-view-designer-tiles.md) e fare clic su **applica** toosave modifiche.

### <a name="configure-visualization-parts"></a>Configurazione delle parti della visualizzazione
Una vista può includere qualsiasi numero di parti della visualizzazione.  Seleziona hello **vista** scheda e quindi una visualizzazione parte tooadd toohello visualizzazione.  Hello **proprietà** riquadro verranno visualizzati proprietà hello part hello selezionato.  Configurare la visualizzazione di hello proprietà in base toohello informazioni dettagliate in hello [riferimento parte visualizzazione](log-analytics-view-designer-parts.md) e fare clic su **applica** toosave modifiche.

### <a name="delete-a-visualization-part"></a>Eliminazione di una parte della visualizzazione
È possibile rimuovere una parte di visualizzazione dalla visualizzazione hello facendo hello **X** pulsante hello angolo superiore destro della parte hello.

### <a name="rearrange-visualization-parts"></a>Ridisposizione delle parti della visualizzazione
Le viste hanno solo di una riga di parti della visualizzazione.  Ridisporre parti esistenti in una visualizzazione facendo clic e trascinamento tooa nuova posizione.

## <a name="next-steps"></a>Passaggi successivi
* Aggiungere [riquadri](log-analytics-view-designer-tiles.md) tooyour di visualizzazione personalizzata.
* Aggiungere [visualizzazione parti](log-analytics-view-designer-parts.md) tooyour di visualizzazione personalizzata.
