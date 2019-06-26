## How to start

```
docker-compose up
```

Then open [http://localhost:8983](http://localhost:8983) in your browser.

## How to enter the container

```
docker exec -it --user=solr my_solr bash
```


## Links 
- https://hub.docker.com/_/solr
- [Troubleshoot](https://github.com/docker-solr/docker-solr/issues/10)
- Exampe :
	- [conf/](https://github.com/apache/lucene-solr/tree/master/solr/example/files/conf)
	- [docs](https://github.com/apache/lucene-solr/tree/master/solr/example/exampledocs)