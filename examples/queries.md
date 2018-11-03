## Ejemplos de consultas sobre censo de locales y licencias de apertura

A continuación se presentan algunos ejemplos de consultas, utilizando como referencia los conjuntos de datos proporcionados por el Ayuntamiento de Madrid, que se corresponden con los ficheros de censo de locales y sus actividades, terrazas, y licencias otorgadas.

Por ejemplo, en esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fciudadesabiertas.linkeddata.es%2Fcenso-locales&query=PREFIX+escom%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fcomercio%2Ftejido-comercial%23%3E%0D%0APREFIX+esadm%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Fterritorio%23%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Fbarrio+%3Frotulo+WHERE%7B%0D%0A++++++++%3FuriLocal+a+escom%3ALocalComercial+.%0D%0A++++++++%3FuriLocal+esadm%3Abarrio+%3FuriBarrio+.%0D%0A++++++++%3FuriBarrio+dc%3Atitle+%22DELICIAS%22+.%0D%0A++++++++%3FuriBarrio+dc%3Atitle+%3Fbarrio+.%0D%0A++++++++%3FuriLocal+escom%3Arotulo+%3Frotulo+.%0D%0A++++++++%3FuriLocal+escom%3AtipoSituacion+%3FuriSituacion+.%0D%0A++++++++%0D%0A%7D%0D%0A+LIMIT+10&format=text%2Fhtml&timeout=0&debug=on) se piden 10 locales en situación activa que se encuentren ubicados en el barrio DELICIAS.  
```
PREFIX escom:<http://vocab.linkeddata.es/datosabiertos/def/comercio/tejido-comercial#>
PREFIX esadm:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>

SELECT DISTINCT ?barrio ?rotulo WHERE{
        ?uriLocal a escom:LocalComercial .
        ?uriLocal esadm:barrio ?uriBarrio .
        ?uriBarrio dc:title "DELICIAS" .
        ?uriBarrio dc:title ?barrio .
        ?uriLocal escom:rotulo ?rotulo .
        ?uriLocal escom:tipoSituacion ?uriSituacion .
        ?uriSituacion skos:prefLabel "activo" .         
}
 LIMIT 10
```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fciudadesabiertas.linkeddata.es%2Fcenso-locales&query=PREFIX+escom%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fcomercio%2Ftejido-comercial%23%3E%0D%0APREFIX+esadm%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Fterritorio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Frotulo+%3Fdireccion+%3Fdistrito+%3Fbarrio+WHERE%7B%0D%0A%09%3FuriLocal+a+escom%3ALocalComercial+.%0D%0A++++++++%3FuriLocal+escom%3Arotulo+%22DECORACIONES+EMBAJADORES+157%22+.%0D%0A++++++++%3FuriLocal+escom%3Arotulo+%3Frotulo+.%0D%0A++++++++%3FuriLocal+schema%3Aaddress+%3Fdireccion+.%0D%0A++++++++%3FuriLocal+esadm%3Adistrito+%3FuriDistrito+.%0D%0A++++++++%3FuriDistrito+dc%3Atitle+%3Fdistrito+.%0D%0A++++++++%3FuriLocal+esadm%3Abarrio+%3FuriBarrio+.%0D%0A++++++++%3FuriBarrio+dc%3Atitle+%3Fbarrio+.%0D%0A%0D%0A%7D+limit+10%0D%0A&format=text%2Fhtml&timeout=0&debug=on) se obtienen los datos relacionados con un local específico. En este caso el local con rótulo "DECORACIONES EMBAJADORES 157".

```
PREFIX escom:<http://vocab.linkeddata.es/datosabiertos/def/comercio/tejido-comercial#>
PREFIX esadm:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>
PREFIX schema:<http://schema.org/>
PREFIX geosparql:<http://www.opengis.net/ont/geosparql#>
PREFIX geo_core:<https://datos.ign.es/def/geo_core#>

SELECT DISTINCT ?rotulo ?direccion ?distrito ?barrio ?coordenadaX ?coordenadaY WHERE{
	?uriLocal a escom:LocalComercial .
        ?uriLocal escom:rotulo "DECORACIONES EMBAJADORES 157" .
        ?uriLocal escom:rotulo ?rotulo .
        ?uriLocal schema:address ?direccion .
        ?uriLocal esadm:distrito ?uriDistrito .
        ?uriDistrito dc:title ?distrito .
        ?uriLocal esadm:barrio ?uriBarrio .
        ?uriBarrio dc:title ?barrio .
        ?uriLocal geosparql:hasGeometry ?uriPoint .
        ?uriPoint geo_core:xETRS89 ?coordenadaX .
        ?uriPoint geo_core:yETRS89 ?coordenadaY
}

```

En la siguiente [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fciudadesabiertas.linkeddata.es%2Fcenso-locales&query=PREFIX+escom%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fcomercio%2Ftejido-comercial%23%3E%0D%0APREFIX+esadm%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Fterritorio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+geosparql%3A%3Chttp%3A%2F%2Fwww.opengis.net%2Font%2Fgeosparql%23%3E%0D%0APREFIX+geo_core%3A%3Chttps%3A%2F%2Fdatos.ign.es%2Fdef%2Fgeo_core%23%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Frotulo+%3Fdireccion+%3Fdistrito+%3Fbarrio+%3FcoordenadaX+%3FcoordenadaY+WHERE%7B%0D%0A%09%3FuriLocal+a+escom%3ALocalComercial+.%0D%0A++++++++%3FuriLocal+escom%3AtipoActividadEconomica+%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fcomercio%2Fcnae%2FCod4%2F9602%3E+.%0D%0A++++++++%3FuriLocal+escom%3Arotulo+%3Frotulo+.%0D%0A++++++++%3FuriLocal+schema%3Aaddress+%3Fdireccion+.%0D%0A++++++++%3FuriLocal+esadm%3Adistrito+%3FuriDistrito+.%0D%0A++++++++%3FuriDistrito+dc%3Atitle+%3Fdistrito+.%0D%0A++++++++%3FuriLocal+esadm%3Abarrio+%3FuriBarrio+.%0D%0A++++++++%3FuriBarrio+dc%3Atitle+%3Fbarrio+.%0D%0A++++++++%3FuriLocal+geosparql%3AhasGeometry+%3FuriPoint+.%0D%0A++++++++%3FuriPoint+geo_core%3AxETRS89+%3FcoordenadaX+.%0D%0A++++++++%3FuriPoint+geo_core%3AyETRS89+%3FcoordenadaY+++++++%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on) se obtienen todos los locales en los que se realiza la actividad “Peluquería y otros tratamientos de belleza”.

```
PREFIX escom:<http://vocab.linkeddata.es/datosabiertos/def/comercio/tejido-comercial#>
PREFIX esadm:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>
PREFIX schema:<http://schema.org/>
PREFIX geosparql:<http://www.opengis.net/ont/geosparql#>
PREFIX geo_core:<https://datos.ign.es/def/geo_core#>

SELECT DISTINCT ?rotulo ?direccion ?distrito ?barrio ?coordenadaX ?coordenadaY WHERE{
        ?uriLocal a escom:LocalComercial .
        ?uriLocal escom:tipoActividadEconomica ?uriActividad .     
        ?uriActividad rdfs:label “Peluquería y otros tratamientos de belleza” .
        ?uriLocal escom:rotulo ?rotulo .
        ?uriLocal schema:address ?direccion .
        ?uriLocal esadm:distrito ?uriDistrito .
        ?uriDistrito dc:title ?distrito .
        ?uriLocal esadm:barrio ?uriBarrio .
        ?uriBarrio dc:title ?barrio .
        ?uriLocal geosparql:hasGeometry ?uriPoint .
        ?uriPoint geo_core:xETRS89 ?coordenadaX .
        ?uriPoint geo_core:yETRS89 ?coordenadaY .      
}
```
