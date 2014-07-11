docker-logstash-shipper
=======================

Logstash 1.4.2 docker build, inspired by user pblittle. Shipper version. The indexer can be found at [rohit-dantas/docker-logstash][3].

The shipper's default configuration outputs to a linked redis container adn takes stdin as the input. Ideally the configuration should be overidden as shown in the second step below, such that an actual redis host and an actual input type are chosen.

To fetch and start a container running a logstash (1.4.2) agent as a shipper:

	docker run -d \
	  --name logstash \
	  --link redis:redis \
	  rohitdantas/docker-logstash-shipper

If you want to pass your own logstash.conf file, just mount its source directory. For example, if your custom logstash.conf file is located at `/tmp/conf/logstash.conf`:

	docker run -d \
	  --name logstash \
	  --redis:redis \
	  -v /tmp/conf:/opt/conf \
	  rohitdantas/docker-logstash-shipper

Special shoutout to ehazlett's excellent post, [Logstash and Kibana3 via Docker][1], explaining the big picture and pblittle's [original container][2].

  [1]: http://ehazlett.github.io/applications/2013/08/28/logstash-kibana/
  [2]: https://github.com/pblittle/docker-logstash
  [3]: https://github.com/rohit-dantas/docker-logstash
