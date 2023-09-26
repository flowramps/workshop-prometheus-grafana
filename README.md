# Workshop - Monitoramento Prometheus e Grafana

Em sua VM, criei um path com o seguinte comando para podermos atrelar ao k3d nos próximos passos.
```
mkdir -p /data/k3dvol
```

Antes de começar é muito importamte ter criado o seu cluster, no meu exemplo estou utilizando o k3d, basta executar o seguinte comando!


```
k3d cluster create bifrost-prd --agents 2 -p "80:30000@loadbalancer" --volume /data/k3dvol:/data/k3dvol
```

Para aplicar os manifestos em seu cluster, acesse a raiz do seu repo que acabou de efetuar o git clone e Execute:


Caso não possua ainda a NS monitoring criada, execute o comando abaixo para criar!
```
kubectl create namespace monitoring
```

Os comandos abaixo, irão aplicar os manifestos.
```
kubectl create -f prometheus/

kubectl create -f grafana/

kubectl create -f app-catalogo/ 
```


Após realizar o apply dos arquivos YAML, você poderá rexecutar os seguintes comandos para visulaizar se os pods estão UPs.
```
kubectl get pods -n default
kubectl get pods -n monitoring

```

Depois acesse http://grafana.192.168.15.43.nip.io/ (Grafana)
```
Usuario: admin
Senha: admin
```


Importar dash no grafana atravez dos cod baixo  
```
K8S
Importe o dashboard do GrafanaLabs (https://grafana.com/grafana/dashboards/12740)
ID: 12740

MongoDB
Importe o dashboard do GrafanaLabs (https://grafana.com/grafana/dashboards/2583-mongodb/)
ID: 2583

ASP.NET Core
Importar o dashboard do GrafanaLabs (https://grafana.com/grafana/dashboards/10915)
ID: 10915
```


Comando para realizar request e estressar a Api
```
while true; do curl http://web.192.168.15.43.nip.io/produto; sleep 1; done;
```


EndPoints
```
Aplicação Catalogo
http://web.192.168.15.43.nip.io/produto
http://web.192.168.15.43.nip.io/swagger/index.html
http://web.192.168.15.43.nip.io/metrics

Grafana
http://grafana.192.168.15.43.nip.io/

Prometheus
http://prometheus.192.168.15.43.nip.io/

```


Para aprimorar ainda mais seus estudos, consulte as documentações oficiais abaixo!
```
https://prometheus.io/
https://grafana.com/

```
