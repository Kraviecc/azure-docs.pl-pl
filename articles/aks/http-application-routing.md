---
title: Dodatek routingu aplikacji protokołu HTTP w usłudze Azure Kubernetes Service (AKS)
description: Dodatek routingu aplikacji protokołu HTTP umożliwia dostęp do aplikacji wdrożonych w usłudze Azure Kubernetes Service (AKS).
services: container-service
author: lachie83
ms.topic: article
ms.date: 07/20/2020
ms.author: laevenso
ms.openlocfilehash: 25fc021a48e8936f242df35f7485fc59a93bba13
ms.sourcegitcommit: 24a12d4692c4a4c97f6e31a5fbda971695c4cd68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/05/2021
ms.locfileid: "102172804"
---
# <a name="http-application-routing"></a>Routing aplikacji protokołu HTTP

Rozwiązanie do routingu aplikacji HTTP ułatwia uzyskiwanie dostępu do aplikacji wdrożonych w klastrze usługi Azure Kubernetes Service (AKS). Po włączeniu rozwiązania konfiguruje on [kontroler](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/) transferu danych przychodzących w klastrze AKS. Po wdrożeniu aplikacji rozwiązanie tworzy również publicznie dostępne nazwy DNS dla punktów końcowych aplikacji.

Gdy dodatek jest włączony, tworzy strefę DNS w Twojej subskrypcji. Aby uzyskać więcej informacji na temat kosztu usługi DNS, zobacz [Cennik usługi DNS][dns-pricing].

> [!CAUTION]
> Dodatek routingu aplikacji protokołu HTTP jest przeznaczony do szybkiego tworzenia kontrolera transferu danych przychodzących i uzyskiwania dostępu do aplikacji. Ten dodatek nie jest obecnie przeznaczony do użycia w środowisku produkcyjnym i nie jest zalecany do użytku produkcyjnego. W przypadku gotowych do produkcji wdrożeń przychodzących obejmujących wiele replik i obsługę protokołu TLS zobacz [Tworzenie kontrolera protokołu HTTPS](./ingress-tls.md).

## <a name="http-routing-solution-overview"></a>Omówienie rozwiązania routingu HTTP

Dodatek wdraża dwa składniki: kontroler transferu danych przychodzących [Kubernetes][ingress] i [zewnętrzny kontroler DNS][external-dns] .

- **Kontroler** ruchu przychodzącego: kontroler transferu danych przychodzących jest dostępny dla Internetu za pomocą usługi Kubernetes typu modułu równoważenia obciążenia. Kontroler transferu danych przychodzących służy do obserwowania i implementowania [zasobów Kubernetes][ingress-resource], które tworzą trasy do punktów końcowych aplikacji.
- **Kontroler zewnętrzny DNS**: czujki dla zasobów przychodzących Kubernetes i tworzy rekordy A systemu DNS w strefie DNS specyficznej dla klastra.

## <a name="deploy-http-routing-cli"></a>Wdrażanie routingu HTTP: interfejs wiersza polecenia

Dodatek routingu aplikacji protokołu HTTP można włączyć przy użyciu interfejsu wiersza polecenia platformy Azure podczas wdrażania klastra AKS. Aby to zrobić, użyj polecenia [AZ AKS Create][az-aks-create] z `--enable-addons` argumentem.

```azurecli
az aks create --resource-group myResourceGroup --name myAKSCluster --enable-addons http_application_routing
```

> [!TIP]
> Jeśli chcesz włączyć wiele dodatków, podaj je jako listę rozdzieloną przecinkami. Aby na przykład włączyć Routing i monitorowanie aplikacji HTTP, użyj formatu `--enable-addons http_application_routing,monitoring` .

Routing protokołu HTTP można także włączyć w istniejącym klastrze AKS przy użyciu polecenia [AZ AKS Enable-dodatkis][az-aks-enable-addons] . Aby włączyć routing HTTP w istniejącym klastrze, Dodaj `--addons` parametr i określ *http_application_routing* , jak pokazano w następującym przykładzie:

```azurecli
az aks enable-addons --resource-group myResourceGroup --name myAKSCluster --addons http_application_routing
```

Po wdrożeniu lub zaktualizowaniu klastra użyj polecenia [AZ AKS show][az-aks-show] , aby pobrać nazwę strefy DNS.

```azurecli
az aks show --resource-group myResourceGroup --name myAKSCluster --query addonProfiles.httpApplicationRouting.config.HTTPApplicationRoutingZoneName -o table
```

Ta nazwa jest wymagana do wdrażania aplikacji w klastrze AKS i jest pokazana w następujących przykładowych danych wyjściowych:

```console
9f9c1fe7-21a1-416d-99cd-3543bb92e4c3.eastus.aksapp.io
```

## <a name="deploy-http-routing-portal"></a>Wdrażanie routingu HTTP: Portal

Dodatek routingu aplikacji protokołu HTTP można włączyć za pomocą Azure Portal podczas wdrażania klastra AKS.

![Włączanie funkcji routingu HTTP](media/http-routing/create.png)

Po wdrożeniu klastra przejdź do utworzonej grupy zasobów AKS i wybierz strefę DNS. Zanotuj nazwę strefy DNS. Ta nazwa jest wymagana do wdrażania aplikacji w klastrze AKS.

![Pobieranie nazwy strefy DNS](media/http-routing/dns.png)

## <a name="connect-to-your-aks-cluster"></a>Nawiązywanie połączenia z klastrem AKS

Aby nawiązać połączenie z klastrem Kubernetes z komputera lokalnego, należy użyć narzędzia [kubectl][kubectl], czyli klienta wiersza polecenia usługi Kubernetes.

Jeśli korzystasz z usługi Azure Cloud Shell, narzędzie `kubectl` jest już zainstalowane. Możesz także zainstalować je lokalnie za pomocą polecenia [az aks install-cli][]:

```azurecli
az aks install-cli
```

Aby skonfigurować narzędzie `kubectl` w celu nawiązania połączenia z klastrem Kubernetes, użyj polecenia [az aks get-credentials][]. Poniższy przykład pobiera poświadczenia dla klastra AKS o nazwie *MyAKSCluster* w liście *zasobów*:

```azurecli
az aks get-credentials --resource-group MyResourceGroup --name MyAKSCluster
```

## <a name="use-http-routing"></a>Korzystanie z routingu HTTP

Rozwiązanie do routingu aplikacji HTTP może być wyzwalane tylko w przypadku zasobów przychodzących, które są opatrzone adnotacją w następujący sposób:

```yaml
annotations:
  kubernetes.io/ingress.class: addon-http-application-routing
```

Utwórz plik o nazwie **Samples-http-Application-Routing. YAML** i skopiuj go do poniższego YAML. W wierszu 43 zaktualizuj `<CLUSTER_SPECIFIC_DNS_ZONE>` nazwę strefy DNS zebraną w poprzednim kroku tego artykułu.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: aks-helloworld  
spec:
  replicas: 1
  selector:
    matchLabels:
      app: aks-helloworld
  template:
    metadata:
      labels:
        app: aks-helloworld
    spec:
      containers:
      - name: aks-helloworld
        image: mcr.microsoft.com/azuredocs/aks-helloworld:v1
        ports:
        - containerPort: 80
        env:
        - name: TITLE
          value: "Welcome to Azure Kubernetes Service (AKS)"
---
apiVersion: v1
kind: Service
metadata:
  name: aks-helloworld  
spec:
  type: ClusterIP
  ports:
  - port: 80
  selector:
    app: aks-helloworld
---
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: aks-helloworld
  annotations:
    kubernetes.io/ingress.class: addon-http-application-routing
spec:
  rules:
  - host: aks-helloworld.<CLUSTER_SPECIFIC_DNS_ZONE>
    http:
      paths:
      - backend:
          serviceName: aks-helloworld
          servicePort: 80
        path: /
```

Użyj polecenia [polecenia kubectl Apply][kubectl-apply] , aby utworzyć zasoby.

```bash
kubectl apply -f samples-http-application-routing.yaml
```

W poniższym przykładzie przedstawiono utworzone zasoby:

```bash
$ kubectl apply -f samples-http-application-routing.yaml

deployment.apps/aks-helloworld created
service/aks-helloworld created
ingress.networking.k8s.io/aks-helloworld created
```

Otwórz przeglądarkę internetową, aby *AKS-HelloWorld \<CLUSTER_SPECIFIC_DNS_ZONE\> .* na przykład *AKS-HelloWorld.9f9c1fe7-21a1-416d-99cd-3543bb92e4c3.eastus.aksapp.IO* i sprawdź, czy zobaczysz aplikację demonstracyjną. Aby można było wyświetlić aplikację, może to potrwać kilka minut.

## <a name="remove-http-routing"></a>Usuń Routing HTTP

Rozwiązanie do routingu HTTP można usunąć za pomocą interfejsu wiersza polecenia platformy Azure. Aby to zrobić, uruchom następujące polecenie, zastępując klaster AKS i nazwę grupy zasobów.

```azurecli
az aks disable-addons --addons http_application_routing --name myAKSCluster --resource-group myResourceGroup --no-wait
```

Gdy dodatek routingu aplikacji protokołu HTTP jest wyłączony, niektóre zasoby Kubernetes mogą pozostać w klastrze. Te zasoby obejmują *configMaps* i wpisy *tajne* i są tworzone w przestrzeni nazw *polecenia-system* . Aby zachować czysty klaster, możesz chcieć usunąć te zasoby.

Poszukaj *dodatków-http-Application-Routing* zasobów przy użyciu następujących poleceń [polecenia kubectl Get][kubectl-get] :

```console
kubectl get deployments --namespace kube-system
kubectl get services --namespace kube-system
kubectl get configmaps --namespace kube-system
kubectl get secrets --namespace kube-system
```

Następujące przykładowe dane wyjściowe przedstawiają configMaps, które powinny zostać usunięte:

```
$ kubectl get configmaps --namespace kube-system

NAMESPACE     NAME                                                       DATA   AGE
kube-system   addon-http-application-routing-nginx-configuration         0      9m7s
kube-system   addon-http-application-routing-tcp-services                0      9m7s
kube-system   addon-http-application-routing-udp-services                0      9m7s
```

Aby usunąć zasoby, użyj polecenia [polecenia kubectl Delete][kubectl-delete] . Określ typ zasobu, nazwę zasobu i przestrzeń nazw. Poniższy przykład usuwa jeden z poprzednich configmaps:

```console
kubectl delete configmaps addon-http-application-routing-nginx-configuration --namespace kube-system
```

Powtórz poprzedni `kubectl delete` krok dla wszystkich zasobów *routingu protokołu HTTP i aplikacji* , które pozostały w klastrze.

## <a name="troubleshoot"></a>Rozwiązywanie problemów

Użyj [polecenia kubectl dzienników][kubectl-logs] , aby wyświetlić dzienniki aplikacji dla zewnętrznej aplikacji DNS. Dzienniki powinny potwierdzić pomyślne utworzenie rekordu DNS a i TXT.

```
$ kubectl logs -f deploy/addon-http-application-routing-external-dns -n kube-system

time="2018-04-26T20:36:19Z" level=info msg="Updating A record named 'aks-helloworld' to '52.242.28.189' for Azure DNS zone '471756a6-e744-4aa0-aa01-89c4d162a7a7.canadaeast.aksapp.io'."
time="2018-04-26T20:36:21Z" level=info msg="Updating TXT record named 'aks-helloworld' to '"heritage=external-dns,external-dns/owner=default"' for Azure DNS zone '471756a6-e744-4aa0-aa01-89c4d162a7a7.canadaeast.aksapp.io'."
```

Te rekordy mogą być również widoczne w zasobie strefy DNS w Azure Portal.

![Pobieranie rekordów DNS](media/http-routing/clippy.png)

Użyj [polecenia kubectl dzienników][kubectl-logs] , aby wyświetlić dzienniki aplikacji dla kontrolera Nginx transferu danych przychodzących. Dzienniki powinny potwierdzić zasób transferu `CREATE` danych przychodzących i załadować ponownie kontroler. Wszystkie aktywności HTTP są rejestrowane.

```bash
$ kubectl logs -f deploy/addon-http-application-routing-nginx-ingress-controller -n kube-system

-------------------------------------------------------------------------------
NGINX Ingress controller
  Release:    0.13.0
  Build:      git-4bc943a
  Repository: https://github.com/kubernetes/ingress-nginx
-------------------------------------------------------------------------------

I0426 20:30:12.212936       9 flags.go:162] Watching for ingress class: addon-http-application-routing
W0426 20:30:12.213041       9 flags.go:165] only Ingress with class "addon-http-application-routing" will be processed by this ingress controller
W0426 20:30:12.213505       9 client_config.go:533] Neither --kubeconfig nor --master was specified.  Using the inClusterConfig.  This might not work.
I0426 20:30:12.213752       9 main.go:181] Creating API client for https://10.0.0.1:443
I0426 20:30:12.287928       9 main.go:225] Running in Kubernetes Cluster version v1.8 (v1.8.11) - git (clean) commit 1df6a8381669a6c753f79cb31ca2e3d57ee7c8a3 - platform linux/amd64
I0426 20:30:12.290988       9 main.go:84] validated kube-system/addon-http-application-routing-default-http-backend as the default backend
I0426 20:30:12.294314       9 main.go:105] service kube-system/addon-http-application-routing-nginx-ingress validated as source of Ingress status
I0426 20:30:12.426443       9 stat_collector.go:77] starting new nginx stats collector for Ingress controller running in namespace  (class addon-http-application-routing)
I0426 20:30:12.426509       9 stat_collector.go:78] collector extracting information from port 18080
I0426 20:30:12.448779       9 nginx.go:281] starting Ingress controller
I0426 20:30:12.463585       9 event.go:218] Event(v1.ObjectReference{Kind:"ConfigMap", Namespace:"kube-system", Name:"addon-http-application-routing-nginx-configuration", UID:"2588536c-4990-11e8-a5e1-0a58ac1f0ef2", APIVersion:"v1", ResourceVersion:"559", FieldPath:""}): type: 'Normal' reason: 'CREATE' ConfigMap kube-system/addon-http-application-routing-nginx-configuration
I0426 20:30:12.466945       9 event.go:218] Event(v1.ObjectReference{Kind:"ConfigMap", Namespace:"kube-system", Name:"addon-http-application-routing-tcp-services", UID:"258ca065-4990-11e8-a5e1-0a58ac1f0ef2", APIVersion:"v1", ResourceVersion:"561", FieldPath:""}): type: 'Normal' reason: 'CREATE' ConfigMap kube-system/addon-http-application-routing-tcp-services
I0426 20:30:12.467053       9 event.go:218] Event(v1.ObjectReference{Kind:"ConfigMap", Namespace:"kube-system", Name:"addon-http-application-routing-udp-services", UID:"259023bc-4990-11e8-a5e1-0a58ac1f0ef2", APIVersion:"v1", ResourceVersion:"562", FieldPath:""}): type: 'Normal' reason: 'CREATE' ConfigMap kube-system/addon-http-application-routing-udp-services
I0426 20:30:13.649195       9 nginx.go:302] starting NGINX process...
I0426 20:30:13.649347       9 leaderelection.go:175] attempting to acquire leader lease  kube-system/ingress-controller-leader-addon-http-application-routing...
I0426 20:30:13.649776       9 controller.go:170] backend reload required
I0426 20:30:13.649800       9 stat_collector.go:34] changing prometheus collector from  to default
I0426 20:30:13.662191       9 leaderelection.go:184] successfully acquired lease kube-system/ingress-controller-leader-addon-http-application-routing
I0426 20:30:13.662292       9 status.go:196] new leader elected: addon-http-application-routing-nginx-ingress-controller-5cxntd6
I0426 20:30:13.763362       9 controller.go:179] ingress backend successfully reloaded...
I0426 21:51:55.249327       9 event.go:218] Event(v1.ObjectReference{Kind:"Ingress", Namespace:"default", Name:"aks-helloworld", UID:"092c9599-499c-11e8-a5e1-0a58ac1f0ef2", APIVersion:"extensions", ResourceVersion:"7346", FieldPath:""}): type: 'Normal' reason: 'CREATE' Ingress default/aks-helloworld
W0426 21:51:57.908771       9 controller.go:775] service default/aks-helloworld does not have any active endpoints
I0426 21:51:57.908951       9 controller.go:170] backend reload required
I0426 21:51:58.042932       9 controller.go:179] ingress backend successfully reloaded...
167.220.24.46 - [167.220.24.46] - - [26/Apr/2018:21:53:20 +0000] "GET / HTTP/1.1" 200 234 "" "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Trident/5.0)" 197 0.001 [default-aks-helloworld-80] 10.244.0.13:8080 234 0.004 200
```

## <a name="clean-up"></a>Czyszczenie

Usuń skojarzone obiekty Kubernetes utworzone w tym artykule przy użyciu programu `kubectl delete` .

```bash
kubectl delete -f samples-http-application-routing.yaml
```

Przykładowe dane wyjściowe pokazują, że obiekty Kubernetes zostały usunięte.

```bash
$ kubectl delete -f samples-http-application-routing.yaml

deployment "aks-helloworld" deleted
service "aks-helloworld" deleted
ingress "aks-helloworld" deleted
```

## <a name="next-steps"></a>Następne kroki

Aby uzyskać informacje na temat sposobu instalowania kontrolera transferu danych zabezpieczonych przy użyciu protokołu HTTPS w programie AKS, zobacz https transferal in [Azure Kubernetes Service (AKS)][ingress-https].

<!-- LINKS - internal -->
[az-aks-create]: /cli/azure/aks#az-aks-create
[az-aks-show]: /cli/azure/aks#az-aks-show
[ingress-https]: ./ingress-tls.md
[az-aks-enable-addons]: /cli/azure/aks#az-aks-enable-addons
[az aks install-cli]: /cli/azure/aks#az-aks-install-cli
[az aks get-credentials]: /cli/azure/aks#az-aks-get-credentials

<!-- LINKS - external -->
[dns-pricing]: https://azure.microsoft.com/pricing/details/dns/
[external-dns]: https://github.com/kubernetes-incubator/external-dns
[kubectl]: https://kubernetes.io/docs/user-guide/kubectl/
[kubectl-apply]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubectl-delete]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete
[kubectl-logs]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#logs
[ingress]: https://kubernetes.io/docs/concepts/services-networking/ingress/
[ingress-resource]: https://kubernetes.io/docs/concepts/services-networking/ingress/#the-ingress-resource
