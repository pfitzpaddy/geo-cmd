## geo-cmd
Commands for geo data and processing

### Prerequisits
 - Postgres 9.x 
 - PostGIS 2.x
 - GDAL/OGR 1.11.x
 
#### CSV Import

1) Create table
	
	# SQL
	CREATE TABLE public.dews_incidents_2015 (
  		id integer serial NOT NULL DEFAULT,
  		prov_code integer,
  		prov_name character varying(255),
  		dist_code integer,
  		dist_name character varying(255),
  		incidents integer
  	)
 
2) Import CSV with HEADER in Terminal

	# SQL
	# Insert into existing table dews_incidents_2015
	COPY dews_incidents_2015(prov_code, prov_name, dist_code, dist_name) FROM '/home/data/sample.csv' WITH DELIMITER ',' CSV HEADER

#### CSV Export

	# SQL
	COPY public.dews_incidents_2015 TO '/tmp/dews_incidents_2015.csv' DELIMITER ',' CSV HEADER;

#### SHP Import

	: shp2pgsql 'path/to/import/shape.shp' SCHEMA.TABLE|psql -h HOST -d DATABASE -U USER
	
#### SHP Export

	: pgsql2shp -f 'path/to/output/shape.shp' DATABASE SCHEMA.TABLE -h HOST -d DATABASE -u USER
	
#### Raster to 8 bit

	: gdal_translate -ot Byte -scale -b 1 -b 2 -b 3 input.tif output.tif
