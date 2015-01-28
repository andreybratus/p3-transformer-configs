Fusepool P3 XSLT Transformer Configuration
==========================================

The XSLT transformer takes as input xml data and the url of a xslt template and transforms the data in RDF according to the rulse specified in the XSLT file events-vt.xsl. The input data is available online from the link

    http://www.visittrentino.it/media/eventi/eventi.xml

The data are about the events in the Province of Trento. The vocabulary used in the mapping are  

rdf <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
rdfs <http://www.w3.org/2000/01/rdf-schema#>  
geo <http://www.w3.org/2003/01/geo/wgs84_pos#>
xsd <http://www.w3.org/2001/XMLSchema#>  
schema <http://schema.org/>

For each event the following information are extracted and mapped to RDF  
- Title of the events (English and Italian)  
- Description of the event (English and Italian)  
- Address  
- Geographic coordinate (lat, long)  
- Start and end dates  
- Organizer

The xml data must be sent to the transformer via HTTP POST with the url of the XSLT file as parameter. If the xslt file is in a local folder (e.g. /home/user/ ) run the command  

    curl -i -X POST -H "Content-Type: application/xml" -T foo.xml http://localhost:7100?xslt=file:///home/user/foo.xsl

The xslt transformation is assumed to be synchronous by default and the result is sent to the client as soon as the transformation is done.

An example of the transformation result is given below  

@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix schema: <http://schema.org/> .

<urn:event:uuid:a46064c9-a87e-43b3-9cb1-3a4921a3e66a> rdf:type schema:Event ;
             rdfs:label "Campionati Italiani Giovanili Under 20,18,16"@it ;
             rdfs:label "Italian Young Climbing Championship Under 20"@en ;
             schema:description "Specialità boulder, difficoltà e velocità"@it ;
             schema:category "Sport"@it ;
             schema:description "Boulder, Lead and Speed"@en ;
             schema:category "Sports"@en ;
             schema:startDate "2015-06-06"^^xsd:date ;
             schema:endDate "2015-06-07"^^xsd:date ;
             schema:location <urn:location:uuid:a46064c9-a87e-43b3-9cb1-3a4921a3e66a> ;
             schema:organizer <urn:organization:uuid:a46064c9-a87e-43b3-9cb1-3a4921a3e66a> .
<urn:location:uuid:a46064c9-a87e-43b3-9cb1-3a4921a3e66a> rdf:type schema:PostalAddress ;
             rdfs:label "Climbing Stadium" ;
             schema:addressLocality "Arco" ;
             schema:addressCountry "Italy" ;
             schema:streetAddress "Climbing Stadium" ;
             geo:lat "45.92413988812913"^^xsd:double ;
             geo:long  "10.890669822692871"^^xsd:double .
<urn:organization:uuid:a46064c9-a87e-43b3-9cb1-3a4921a3e66a>  rdf:type schema:Organization ;
             rdfs:label "Federazione Arrampicata Sportiva Italiana" ;
             schema:name "Federazione Arrampicata Sportiva Italiana" ;
             schema:telephone "+39 0544 502661" ;
             schema:email "segreteria@federclimb.it" .