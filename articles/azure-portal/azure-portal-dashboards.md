---
title: aaaCreate e condividere i dashboard del portale di Azure | Documenti Microsoft
description: Questo articolo spiega come toocreate e modificare i dashboard in hello portale di Azure.
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a>Creare e condividere i dashboard di hello portale di Azure
È possibile creare più dashboard e condividerli con altri utenti che dispongono di accesso tooyour Azure sottoscrizioni.  In questo articolo è illustrati nozioni di base di hello di creazione, modifica, la pubblicazione e la gestione di accesso toodashboards.

## <a name="create-a-dashboard"></a>Creare un dashboard
toocreate un dashboard, seleziona hello **nuovo dashboard** pulsante il nome del dashboard Avanti toohello corrente.  

![Creare un dashboard](./media/azure-portal-dashboards/new-dashboard.png)

Questa azione crea un nuovo dashboard privato vuoto e attiva la modalità di personalizzazione, in cui è possibile assegnare un nome al dashboard e aggiungere o ridisporre i riquadri.  In questa modalità, hello comprimibile riquadro accetta raccolta tramite il menu di navigazione sinistro hello.  Hello riquadro raccolta consente di trovare i riquadri per le risorse di Azure in vari modi: è possibile esplorare facendo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups), dal tipo di risorsa, da [tag](../azure-resource-manager/resource-group-using-tags.md), o eseguendo una ricerca per la risorsa in base al nome.  

![Personalizzare il dashboard](./media/azure-portal-dashboards/customize-dashboard.png)

Aggiungere riquadri trascinandoli e rilasciandoli sulla superficie del dashboard hello ovunque si desideri.

Per i riquadri non associati a una particolare risorsa è disponibile una nuova categoria denominata **Generale**.  In questo esempio, si aggiunge riquadro Markdown hello.  Utilizzare il dashboard di riquadro tooadd tooyour contenuto personalizzato.  riquadro Hello supporta testo normale, [sintassi Markdown](https://daringfireball.net/projects/markdown/syntax)e un set limitato di HTML.  (Per motivi di sicurezza, non è possibile eseguire operazioni come inserire `<script>` tag o utilizzare un determinato elemento lo stile di stile CSS che potrebbero interferire con il portale di hello.) 

![Aggiungere Markdown](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a>Modificare un dashboard
Dopo aver creato il dashboard, è possibile aggiungere riquadri dalla raccolta di riquadro hello o rappresentazione in forma di riquadro hello dei pannelli. Consente di aggiungere rappresentazione hello il gruppo di risorse. È possibile aggiungere quando si esplorano hello elemento oppure dal pannello della risorsa gruppo hello. Entrambi gli approcci si ottiene il blocco di rappresentazione in forma di riquadro hello hello del gruppo di risorse.

![PIN toodashboard](./media/azure-portal-dashboards/pin-to-dashboard.png)

Dopo aver aggiunto l'elemento hello, viene visualizzato nel dashboard.

![visualizzare il dashboard](./media/azure-portal-dashboards/view-dashboard.png)

Ora che è disponibile un riquadro del Markdown e un dashboard toohello aggiunto gruppo di risorse, è possibile ridimensionare e ridisporre riquadri hello in un layout appropriato.

Passaggio del mouse e selezionando "…" o facendo clic su un riquadro è possibile visualizzare tutti i comandi contestuali hello per tale riquadro. Per impostazione predefinita, sono disponibili due voci:

1. **Rimuovi dal dashboard** -riquadro hello rimuove dal dashboard hello
2. **Personalizza** consente di passare alla modalità di personalizzazione

![Personalizzare un riquadro](./media/azure-portal-dashboards/customize-tile.png)

Selezionando Personalizza è possibile ridimensionare e riordinare i riquadri. un riquadro, seleziona tooresize hello nuova dimensione dal menu di scelta rapida hello, come illustrato nella seguente immagine hello.

![Ridimensionare il riquadro](./media/azure-portal-dashboards/resize-tile.png)

In alternativa, se il riquadro hello supporta qualsiasi dimensione, è possibile trascinare dimensioni di toohello desiderato hello in basso a destra.

![Ridimensionare il riquadro](./media/azure-portal-dashboards/resize-corner.png)

Dopo il ridimensionamento di riquadri, visualizzare il dashboard di hello.

![Visualizzare il riquadro](./media/azure-portal-dashboards/view-tile.png)

Dopo avere completato la personalizzazione di un dashboard, selezionare semplicemente hello **eseguite di personalizzazione** tooexit la modalità di personalizzazione o destro del mouse e selezionare **eseguite di personalizzazione** dal menu di scelta rapida hello.

## <a name="publish-a-dashboard-and-manage-access-control"></a>Pubblicare un dashboard e gestire il controllo di accesso
Quando si crea un dashboard, è privato per impostazione predefinita, ovvero che sono hello unica persona che può essere visualizzato.  toomake è visibile tooothers, utilizzare hello **condivisione** pulsante che viene visualizzato hello altri comandi del dashboard.

![Condividere il dashboard](./media/azure-portal-dashboards/share-dashboard.png)

Verrà chiesto toochoose che un gruppo di risorse e di sottoscrizione per toobe i dashboard pubblicato. dashboard tooseamlessly integrare ecosistema hello, sono stati implementati i dashboard condivisi come risorse di Azure (in modo non è possibile condividere digitando un indirizzo di posta elettronica).  Accedere a informazioni toohello visualizzati dalla maggior parte dei riquadri hello nel portale di hello dipendono dal [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md). Dal punto di vista del controllo di accesso, i dashboard condivisi non sono diversi da una macchina virtuale o da un account di archiviazione.  

Si supponga di avere una sottoscrizione di Azure e i membri del team assegnati ruoli hello di **proprietario**, **collaboratore**, o **lettore** della sottoscrizione hello.  Gli utenti che sono proprietari o i collaboratori sono in grado di toolist, visualizzare, creare, modificare o eliminare i dashboard all'interno di tale sottoscrizione.  Gli utenti che sono i visualizzatori sono in grado di toolist e visualizzare i dashboard, ma non è possibile modificarli o eliminarli.  Gli utenti con accesso in lettura sono dashboard condiviso tooa le modifiche locali di toomake in grado di, ma non è possibile toopublish tali server back-toohello modifiche.  Tuttavia, rendono possibile una copia privata di dashboard hello per uso personale.  Come sempre, i singoli riquadri nei dashboard hello applicano le proprie regole di controllo di accesso in base alle risorse di hello che corrispondano a.  

Per praticità, portale hello di pubblicazione del Guide esperienza è verso un modello in cui inserire i dashboard in un gruppo di risorse denominato **dashboard**.  

![Pubblicare il dashboard](./media/azure-portal-dashboards/publish-dashboard.png)

È anche possibile scegliere toopublish un dashboard tooa determinato gruppo di risorse.  controllo di accesso Hello per tale dashboard consente di ricercare il controllo di accesso per il gruppo di risorse hello hello.  Gli utenti che possono gestire le risorse di hello in tale gruppo di risorse hanno inoltre accesso toohello dashboard.

![pubblicare dashboard tooresource gruppo](./media/azure-portal-dashboards/publish-to-resource-group.png)

Dopo la pubblicazione di dashboard, hello **condivisione + accesso** Pannello di controllo verrà aggiornare e Mostra le informazioni sui dashboard pubblicati hello, tra cui dashboard toohello collegamento toomanage utente l'accesso.  Questo collegamento consente di avviare hello Role Based Access Control blade utilizzata toomanage accesso standard per qualsiasi risorsa di Azure.  È sempre possibile ottenere nuovamente toothis visualizzazione selezionando **condivisione**.

![Gestire il controllo di accesso](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a>Passaggi successivi
* vedere le risorse toomanage, [le risorse di gestione di Azure tramite il portale](../azure-resource-manager/resource-group-portal.md).
* vedere le risorse toodeploy, [distribuire le risorse con modelli di gestione risorse e il portale di Azure](../azure-resource-manager/resource-group-template-deploy-portal.md).

