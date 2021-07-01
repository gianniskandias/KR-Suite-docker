# KR-SUITE

This KR-suite docker packs all the linked data tools developed by the [KRR&A team](http://ai.di.uoa.gr/) of the [National and Kapodistrian Univeristy of Athens](http://www.di.uoa.gr/). The KR-suite contains the following open source tools:

* __[Strabon](http://strabon.di.uoa.gr/).__ Strabon is a spatiotemporal RDF store. You can use it to store linked geospatial data that changes over time and pose queries using two popular extensions of SPARQL (GeoSPARQL and stSPARQL). Strabon has been shown experimentally to be the most efficient spatiotemporal RDF store available today.
* __[GeoTriples](http://geotriples.di.uoa.gr/).__ GeoTriples is a tool for transforming geospatial data from their original formats (e.g., shapefiles or spatially-enabled relational databases) into RDF.
* __[Sextant](http://sextant.di.uoa.gr/).__ Sextant is a web based and mobile ready platform for visualizing, exploring and interacting with linked geospatial data. The core feature of Sextant is the ability to create thematic maps by combining geospatial and temporal information that exists in a number of heterogeneous data sources.

You need to install docker engine for following any of the instructions below (<https://www.docker.com/get-docker>).

## Build docker-image from source (Dockerfile)

* Clone this repository
* Go to `/<file_path_to>/kr-suite` and build (terminal of your machine): 
	
		docker build -t docker-image-name .

## Create docker-container from docker-image

* A docker-image named _docker-image-name_ is available either locally (previously built), or in DockerHub.
* Use the docker-image (terminal of your machine): 

		docker run --name docker-container-name -p 9999:8080 -e LANG=C.UTF-8 -v /<some_local_dir>:/inout docker-image-name

* Now the docker-container _docker-container-name_  should be running.

## Using the docker-container

* In a different terminal run: 

		[sudo] docker exec -it docker-container-name /bin/bash

This will open a terminal inside the container.

* Starting tomcat (terminal of container): `rocket.sh`

**Attention**  When the container is up and running, it provides only a postgres(+postgis) DBMS. In order to make Strabon and Sextant available,
you should start container's tomcat as described in the previous instruction.

Now all the WEB Services tools (Sextant, Strabon, OnTop Spatial) are available in your machine's port 9999. For example:

		http://localhost:9999/Sextant_v2.0

		http://localhost:9999/Strabon

* Going through the logs (terminal of your machine): `[sudo] docker logs docker-container-name`
* You can make local files available in container's dir __/inout__ by copying them in you machine's dir: `/<some_local_dir>`

## General docker tips

* Listing all docker containers (terminal of your machine): `[sudo] docker ps -a`
* Listing docker images (terminal of your machine): `[sudo] docker images`
* For remote access, the credentials are 
	
		username=endpoint
		password=3ndpo1nt
		
To change them, edit the file `tomcat/webapps/*/WEB-INF/credentials.properties`

For more detailed information on docker, visit the [official Docker Documentation](https://docs.docker.com/).

## Sextant Configuration

Sextant is one of the tools that come with the KR-suite. To change the default configurations you can alter the server-configuration.properties file that is located under /Sextant/WEB-INF/classes/server/
There you can change the default SPARQL endpoint that is used to store and load maps, set PROXY server configuration and use your Bing Maps key to get access to the Bing Maps base tiles. For more detailed information you can view the embedded Manual Pages by pressing the "?" button in the top-right corner of the interface.

## GeoTriples Usage

* Go to the /bin directory of GeoTriples: `cd /<path_to_geotriples-1.1.6-bin>/bin`
* Run geotriples-all in order to see all available options and examples: `./geotriples-all`
