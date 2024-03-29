- [How to start](#how-to-start)
	- [1st time set up](#1st-time-set-up)
		- [build container](#build-container)
		- [indexing solr documents](#indexing-solr-documents)
		- [source xml raw data vs solr document](#source-xml-raw-data-vs-solr-document)
		- [check solr documents then do solr query in core films](#check-solr-documents-then-do-solr-query-in-core-films)
	- [How to enter the container](#how-to-enter-the-container)
- [Solr schema](#solr-schema)
	- [1. Solr Uses Managed Schema by Default](#1-solr-uses-managed-schema-by-default)
	- [2. Define your own schema.xml](#2-define-your-own-schemaxml)
	- [3. indexing the documents](#3-indexing-the-documents)
- [Links](#links)

## How to start

### 1st time set up

#### build container

```
docker-compose up
```

This will create solr core `films` using `conf` [myconfig/conf/](https://github.com/harryosmar/apache-solr/tree/master/myconfig/conf).

#### indexing solr documents

```
docker exec -it --user=solr my_solr bin/post -c films data/films.xml
```

This will indexing `1098 documents` to solr using data from [data/films.xml](https://github.com/harryosmar/apache-solr/tree/master/data/films.xml)

![solr indexing](https://raw.githubusercontent.com/harryosmar/apache-solr/master/doc/solr-indexing.png)

![solr num docs](https://raw.githubusercontent.com/harryosmar/apache-solr/master/doc/solr-num-docs.png)

#### source xml raw data vs solr document

```xml
<doc>
    <field name="id">/en/45_2006</field>
    <field name="directed_by">Gary Lennon</field>
    <field name="initial_release_date">2006-11-30</field>
    <field name="genre">Black comedy</field>
    <field name="genre">Thriller</field>
    <field name="genre">Psychological thriller</field>
    <field name="genre">Indie film</field>
    <field name="genre">Action Film</field>
    <field name="genre">Crime Thriller</field>
    <field name="genre">Crime Fiction</field>
    <field name="genre">Drama</field>
    <field name="name">.45</field>
  </doc>
```

```json
{
  "id": "/en/45_2006",
  "directed_by": [
    "Gary Lennon"
  ],
  "initial_release_date": "2006-11-30T00:00:00Z",
  "genre": [
    "Black comedy",
    "Thriller",
    "Psychological thriller",
    "Indie film",
    "Action Film",
    "Crime Thriller",
    "Crime Fiction",
    "Drama"
  ],
  "name": ".45",
  "language": "",
  "_version_": 1638423141759844352
}
```

#### check solr documents then do solr query in core `films`

Then open [http://localhost:8983](http://localhost:8983) in your browser.

![solr query](https://raw.githubusercontent.com/harryosmar/apache-solr/master/doc/solr-query.png)

### How to enter the container

```
docker exec -it --user=solr my_solr bash
```

## Solr schema

There are 2 options to handle your `core` `schema` :

### 1. Solr Uses Managed Schema by Default

[Solr Uses Managed Schema by Default](https://lucene.apache.org/solr/guide/6_6/schema-factory-definition-in-solrconfig.html#SchemaFactoryDefinitioninSolrConfig-SolrUsesManagedSchemabyDefault) which means it will automatic update the `schema` according to match the indexed `documents`.

Solr core `films` is using `schema.xml` [myconfig/conf/](https://github.com/harryosmar/apache-solr/blob/master/myconfig/conf/schema.xml).

### 2. Define your own schema.xml

[Guide how to define your own schema.xml](https://lucene.apache.org/solr/guide/6_6/schema-factory-definition-in-solrconfig.html#SchemaFactoryDefinitioninSolrConfig-Classicschema.xml)

- Create solr core `gettingstarted` on running docker container
```
docker exec -it --user=solr my_solr bin/solr create_core -c gettingstarted
```

### 3. indexing the documents

- See list of example docs
```
docker exec -it --user=solr my_solr bash -c "ls -lah example/exampledocs"
```
- Then try to index `example/exampledocs/manufacturers.xml` data to solr core `gettingstarted`
```
docker exec -it --user=solr my_solr bin/post -c gettingstarted example/exampledocs/manufacturers.xml
```

## Links 
- https://hub.docker.com/_/solr
- Troubleshoot
	- https://github.com/docker-solr/docker-solr/issues/10
	- [Solr Error This Indexschema is not mutable](https://stackoverflow.com/questions/31719955/solr-error-this-indexschema-is-not-mutable)
- Example :
	- [conf/](https://github.com/apache/lucene-solr/tree/master/solr/example/files/conf)
	- [docs](https://github.com/apache/lucene-solr/tree/master/solr/example/exampledocs)
