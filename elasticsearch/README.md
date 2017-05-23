# Elasticsearch Helm Chart

This chart installs a working version of Elasticsearch cluster on Kubernetes. 

### Installation

Values.yaml contains configuration for Elasticsearch cluster. 

#### Note: Minimum of 2 Master Nodes are required for elasticsearch cluster 

```
helm install elasticsearch

```
### To verify the helm deployment was successful:

```
helm list
```

### To confirm all pods are up and running:

```
kubectl get pods

```

### To view list of services

```
kubectl get svc
```

```
elasticsearch-discovery   10.99.148.252    <none>        9300/TCP                             47m
elasticsearch-logging     10.105.222.126   <pending>     9200:31070/TCP                       47m
```

### Test elasticsearch functionality:

#### From any host within cluster..

1) Check if Elasticsearch cluster is up
```
curl http://10.105.222.126:9200
```
```
curl http://10.105.222.126:9200/_cluster/health?pretty
```

2) Store data manually using APIs
```
curl -XPUT 'http://10.105.222.126:9200/blog/user/renmak' -d \
'{ "name" : "Dilbert Brown" }'
```
```
curl -XPUT 'http://10.105.222.126:9200/blog/post/1' -d \
'{ "user":"renmak", "title":"how to test ES"}'
```
3) Retrive data manually using APIs
```
curl -XGET 'http://10.105.222.126:9200/blog/user/renmak?pretty=true'

curl -XGET 'http://10.105.222.126:9200/blog/post/1?pretty=true'

curl -XGET 'http://10.105.222.126:9200/blog/post/_search?q=user:renmak&pretty=true'

curl -XGET 'http://10.105.222.126:9200/_search?q=*renmak&pretty=true'

```

