## <a name="overview"></a>Panoramica

In questa esercitazione è completare hello alla procedura seguente:

- Distribuire un'istanza di hello remoto monitoraggio soluzione preconfigurata tooyour sottoscrizione di Azure. Questo passaggio distribuisce e configura automaticamente più servizi di Azure.
- Consente di impostare toocommunicate il dispositivo con il computer e una soluzione di monitoraggio remoto hello.
- Aggiornare hello esempio dispositivo codice tooconnect toohello soluzione di monitoraggio remoto e inviare dati di telemetria simulati che è possibile visualizzare nel dashboard di soluzione hello.

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione, è necessaria una sottoscrizione di Azure attiva.

> [!NOTE]
> Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk-free-trial].

### <a name="required-software"></a>Requisiti software

È necessario client SSH nel tooenable computer desktop è tooremotely accesso hello della riga di comando in hello Raspberry Pi.

- Windows non include un client SSH. È consigliabile usare [PuTTY](http://www.putty.org/).
- La maggior parte delle distribuzioni di Linux e Mac OS includono hello della riga di comando SSH utilità. Per altre informazioni, vedere [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (SSH con Linux o Mac OS).

### <a name="required-hardware"></a>Requisiti hardware

Un computer desktop di tooenable tooconnect è in modalità remota toohello della riga di comando in hello Raspberry Pi.

[Starter kit di Microsoft Azure IoT per Raspberry Pi 3][lnk-starter-kits] o componenti equivalenti. Questa esercitazione vengono utilizzati i seguenti elementi del kit di hello hello:

- Raspberry Pi 3
- Scheda microSD (con NOOBS)
- Un cavo USB mini
- Un cavo Ethernet

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/