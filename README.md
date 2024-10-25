# spatialsql
Llama text to spatial SQL for PostGIS
- https://huggingface.co/markrodrigo

### Architecture Diagram
</br>
TODO

### TESTING
</br>
Testing the PostGIS SQL from the LLM responses can be done in many ways. One approach is to use a Docker container and psql at the command line.
</br>

### Run a Docker container with spatial tables.
- Go to Docker hub:
  </br> https://hub.docker.com/r/kartoza/postgis/
- Pull a container:
    </br> sudo docker pull kartoza/postgis:17-3.5
- Run it:
</br> sudo docker run --name=postgis-17-3.5 -d -e POSTGRES_USER=postgres -e POSTGRES_PASS=password -e POSTGRES_DBNAME=gis -e ALLOW_IP_RANGE=0.0.0.0/0 -p 25432:5432 -v pg_data:/var/lib/postgresql --restart=always kartoza/postgis:17-3.5
- Use psql to connect to container:
  </br> psql -h localhost -U postgres -p 25432
- list the tables:
  </br> \l
- connect to gis database with test tables:
  </br> \c gis
- Run LLM responses to test:
  </br>
  Examples
  </br>
  - SELECT ST_Area(geog) As area FROM (select 'Polygon ((-3.7515154 40.3855551, -3.7514972 40.3856581, -3.7507005 40.3855767, -3.7507167 40.3854722, -3.7515154 40.3855551))' :: geography geog) subquery;
  - SELECT ST_AsText(ST_Centroid(geog)) As centroid FROM (select 'Polygon ((-3.6934636 40.4808785, -3.6933352 40.4811486, -3.6930125 40.4810598, -3.693141 40.4807897, -3.6934636 40.4808785))' :: geography geog) subquery;
  - SELECT ST_AsText(ST_Buffer(geog, 1000)) as buffer FROM (select 'Point(-8.7522658 41.3862664)' :: geography geog) subquery;
  - SELECT ST_Length(geog) As length FROM (select 'LINESTRING (-3.6976693 40.4263178, -3.6986082 40.4258729)' :: geography geog) subquery;
