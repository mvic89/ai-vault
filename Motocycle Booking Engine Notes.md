Målet: Få ut all data över MC-verkstäder inom EU
Det du egentligen vill ha är en **samlad datamängd** över platser i OSM som:
- säljer, reparerar eller servar motorcyklar,
- finns inom EU:s geografiska område,
- kan exporteras och bearbetas (t.ex. i CSV, GeoJSON eller en databas).

------------
#### **Strategi i 3 nivåer**

##### 1. Grunden – OSM-data i bulk (inte Overpass)
Overpass är bra för små queries, men **inte för hela EU**.  
I stället använder du **OSM:s planet-data** eller en **regional extrakt** (EU-delar).

 **Alternativ A: Geofabrik
https://download.geofabrik.de/

→ Här finns uppdelade `.osm.pbf`-filer per land (t.ex. `sweden-latest.osm.pbf`, `germany-latest.osm.pbf`, etc.).

**Så här gör du:**
1. Ladda ner alla EU-länder (du kan automatisera med `wget` eller `curl`).
2. Använd ett verktyg som:
    - **osmium-tool**
    - **osmfilter**
    - **pyosmium** (Python-bibliotek)
3. Filtrera fram objekt med taggar som:
	shop=motorcycle
	service:vehicle:repair=motorcycle
	craft=repair + motorcycle=yes
	
	Exempel med `osmfilter`:
	osmfilter sweden-latest.osm.pbf \
	 --keep="shop=motorcycle = service:vehicle:repair=motorcycle = craft=repair and motorcycle=yes" \
	--ignore-dependencies \
	--out=csv > mc_shops_sweden.csv
4. Kombinera land-filerna → EU-dataset.

Fördelar:
- Full kontroll över datan.
- Du slipper Overpass-timeouts.
- Du kan uppdatera allt regelbundet.

----------
##### 2️ Kvalitet – Kombinera med annan metadata

OSM är bra men inte fullständigt.  
För att öka täckning och noggrannhet kan du **kombinera OSM med:**

- **Google Places API / Bing Maps API**  
    → Hämta ”motorcycle repair” eller ”motorcycle shop” per land.  
    Obs: licenser kräver oftast API-nycklar och kostnad per anrop.
    
- **EU företagsregister (EU Open Data Portal)**  
    → Datamängder över registrerade företag med branschklassificering (NACE-kod `45.40` = "Sale, maintenance and repair of motorcycles and related parts and accessories").  
    Du hittar dessa via:  
    https://data.europa.eu/

Sedan kan du:
- Matcha företagsnamn + plats mot OSM-punkter med t.ex. `geopy` eller `fuzzywuzzy` (Python).
- På så sätt få **mer komplett och verifierad** lista.

-------
##### 3. Bearbetning och visualisering

När du har datan:
- Lagra i **PostGIS** (PostgreSQL med geografiskt stöd).
- Gör spatiala frågor som:

	sql:
	SELECT name, country, ST_AsGeoJSON(geom)
	FROM mc_shops
	WHERE country IN ('SE','DE','FR',...);
	
- Visualisera i **QGIS** eller **Kepler.gl** för karta.
- Du kan även exportera till GeoJSON för webbkartor (t.ex. Leaflet eller MapLibre).

--------------
##### Kort sagt: bästa vägen framåt

|Steg|Vad du gör|Verktyg|
|---|---|---|
|1|Ladda ner EU-länder via Geofabrik|`wget`, `osmium-tool`|
|2|Filtrera MC-relaterade taggar|`osmfilter` / `pyosmium`|
|3|Kombinera med EU företagsdata (NACE 45.40)|EU Open Data Portal|
|4|Lagra i PostGIS / CSV|PostgreSQL / Python|
|5|Visualisera / analysera|QGIS, Kepler.gl, Leaflet|