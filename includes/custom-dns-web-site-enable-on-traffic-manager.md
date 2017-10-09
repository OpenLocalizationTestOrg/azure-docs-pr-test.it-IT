Dopo avere propagato record hello del nome di dominio, è necessario essere in grado di toouse il tooverify browser che può essere il nome di dominio personalizzato da tooaccess usato l'app web in Azure App Service.

> [!NOTE]
> Può richiedere del tempo per il toopropagate CNAME tramite hello sistema DNS. È possibile utilizzare un servizio, ad esempio <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> tooverify che hello CNAME è disponibile.
> 
> 

Se l'app web non è ancora stata aggiunta come un endpoint di gestione traffico, è necessario farlo prima di eseguire la risoluzione dei nomi, come nome di dominio personalizzato hello, tooTraffic route Manager. Gestione traffico indirizza tooyour web app. Utilizzare le informazioni di hello in [aggiungere o eliminare endpoint](../articles/traffic-manager/traffic-manager-endpoints.md) tooadd l'app web con un endpoint nel profilo di Traffic Manager.

> [!NOTE]
> Se l'app Web non è elencata quando si aggiunge un endpoint, verificare che sia configurata per la modalità di piano di servizio app **Standard** . È necessario utilizzare **Standard** modalità per l'app web in ordine toowork con gestione traffico.
> 
> 

1. Nel browser aprire hello [portale Azure](https://portal.azure.com).
2. In hello **App Web** scheda, fare clic sul nome dell'app web, selezionare hello **impostazioni**, quindi selezionare **i domini personalizzati**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. In hello **i domini personalizzati** pannello, fare clic su **aggiungere hostname**.
4. Hello utilizzare **Hostname** testo caselle tooenter hello Traffic Manager dominio nome tooassociate con questa app web.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-8.png)
5. Fare clic su **convalida** configurazione del nome dominio toosave hello.
6. Dopo la selezione di **Convalida**, Azure avvierà il flusso di lavoro di verifica del dominio, Verranno controllati per proprietario del dominio, nonché di esito positivo di disponibilità e i report di nome host o di errore dettagliato con protegere ricchi di indicazioni su come toofix hello errore.    
7. Dopo la convalida **aggiungere hostname** pulsante diventa attivo e sarà in grado di toohello assegnare hostname. Passare ora tooyour nome di dominio personalizzato in un browser. Sarà visibile l'app in esecuzione con il nome di dominio personalizzato. 
   
   Dopo aver completato la configurazione, il nome di dominio personalizzato hello sarà elencato nel hello **i nomi di dominio** sezione dell'app web.

A questo punto, si deve essere in grado di tooenter hello nome nome di dominio nel browser e vedere correttamente necessario tooyour web app.

