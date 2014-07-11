docker-logstash
===============

Logstash 1.4.2 docker build, inspired by user pblittle. By default it depends on a linked redis input container. The primary inspiration to fork away from pblittle's container was to allow for providing a custom logstash.conf file from a local directory.

To fetch and start a container running logstash (1.4.2), elasticsearch (1.1.1) and Kibana 3 (3.0.1), with a redis container exposed on port 6379:

	docker run -d \
	  --name logstash \
	  --link redis:redis \
	  -p 514:514 \
	  -p 9200:9200 \
	  -p 9292:9292 \
	  rohitdantas/docker-logstash

If you want to pass your own logstash.conf file, just mount its source directory. For example, if your custom logstash.conf file is located at `/tmp/conf/logstash.conf`:

	docker run -d \
	  --name logstash \
	  -link redis:redis \
	  -v /tmp/conf:/opt/conf \
	  -p 514:514 \
	  -p 9200:9200 \
	  -p 9292:9292 \
	  rohitdantas/docker-logstash

Special shoutout to ehazlett's excellent post, [Logstash and Kibana3 via Docker][1], explaining the big picture and pblittle's [original container][2].

  [1]: http://ehazlett.github.io/applications/2013/08/28/logstash-kibana/
  [2]: https://github.com/pblittle/docker-logstash
