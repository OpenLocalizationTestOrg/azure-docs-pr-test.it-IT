Dopo avere propagato record hello del nome di dominio, è necessario associare l'App Web. Utilizzare hello seguendo i passaggi tooenable hello i nomi di dominio tramite il browser.

> [!NOTE]
> Può richiedere del tempo per il record TXT creato in hello precedenti passaggi toopropagate tramite hello sistema DNS. È possibile aggiungere il nome di dominio hello dell'app web tooyour fino a quando non sono state propagate hello record TXT. Se si utilizza un record A, è possibile aggiungere un'app web di record di dominio nome tooyour hello fino a quando non sono state propagate record TXT hello creato nel passaggio precedente hello.
> 
> È possibile utilizzare un servizio, ad esempio <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> tooverify che hello record TXT è disponibile.
> 
> 

1. Nel browser aprire hello [portale Azure](https://portal.azure.com).
2. In hello **App Web** scheda, fare clic sul nome dell'app web hello e quindi selezionare **i domini personalizzati**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. In hello **i domini personalizzati** pannello, fare clic su **aggiungere hostname**.
4. Hello utilizzare **Hostname** testo caselle tooenter hello dominio nomi tooassociate con questa app web.
   
    ![](./media/custom-dns-web-site/add-custom-domain.png)
5. Fare clic su **Convalida**.
6. Dopo la selezione di **Convalida**, Azure avvierà il flusso di lavoro di verifica del dominio, Verranno controllati per proprietario del dominio, nonché di esito positivo di disponibilità e i report di nome host o di errore dettagliato con protegere ricchi di indicazioni su come toofix hello errore.    

A questo punto, si deve essere di nome di dominio personalizzato in grado di tooenter hello nel browser e visualizzare correttamente necessario tooyour web app.

