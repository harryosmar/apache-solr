## How to start

```
docker-compose up
```

Then open [http://localhost:8983](http://localhost:8983) in your browser.

## How to enter the container

```
docker exec -it --user=solr my_solr bash
```

## How to manually create solr-core on running docker container

```
docker exec -it --user=solr my_solr bin/solr create_core -c gettingstarted
```

### see list of example docs

```
docker exec -it --user=solr my_solr bash -c "ls -lah example/exampledocs"
```

Then try to index `manufacturers.xml` data

```
docker exec -it --user=solr my_solr bin/post -c gettingstarted example/exampledocs/manufacturers.xml
```

## Links 
- https://hub.docker.com/_/solr
- [Troubleshoot](https://github.com/docker-solr/docker-solr/issues/10)
- Exampe :
	- [conf/](https://github.com/apache/lucene-solr/tree/master/solr/example/files/conf)
	- [docs](https://github.com/apache/lucene-solr/tree/master/solr/example/exampledocs)