# thrustcurve-download

Getting data from ThrustCurve.org XML API.  Right now this is for OpenRocket.

[Trust Curve API](http://www.thrustcurve.org/searchapi.shtml)

Basic demonstration of search query.

    POST http://www.thrustcurve.org/servlets/search
    <search-request>
      <manufacturer>Estes</manufacturer>
      <diameter>18</diameter>
      <has-data-files>true</has-data-files>
      <availability>available</availability>
    </search-request>

## 1. Get a list of Manfuacturers 

Get a the list of Manufacturers and other potential search criteria.

    POST http://www.thrustcurve.org/servlets/metadata 
    <metadata-request/>

    ...
    <manufacturers>
        <manufacturer abbrev="AeroTech">AeroTech</manufacturer>
        ...
    </manufacturers>
   <cert-orgs>
        <cert-org abbrev="TRA">Tripoli Rocketry Association, Inc.</cert-org>
        ...
    </cert-orgs>
    <types>
        <type>hybrid</type>
        ...
    </types>
    <diameters>
        <diameter>6</diameter>
        ...
    </diameters>
    <impulse-classes>
        <impulse-class>A</impulse-class>
        ...
    </impulse-classes>

## 2. Get a list of the motors for each manufacturer

Get list of motors for each manfufacturer.  You can use either the full name or
abbreiviated name for the manufacturer.  We set `max-results` to something
silly because the default is to only return the first 20 results. 


    POST http://www.thrustcurve.org/servlets/search
    <search-request>
      <manufacturer>Contrail</manufacturer>
      <max-results>999999</max-results>
    </search-request>

Typical Result

    ...
    <result>
      <motor-id>6</motor-id>
      <manufacturer>Estes Industries</manufacturer>
      <manufacturer-abbrev>Estes</manufacturer-abbrev>
      <designation>1/2A3</designation>
      <brand-name>1/2A3</brand-name>
      <common-name>1/2A3</common-name>
      <impulse-class>A</impulse-class>
      <diameter>13.0</diameter>
      <length>45.0</length>
      <type>SU</type>
      <cert-org>National Association of Rocketry</cert-org>
      <avg-thrust-n>3.03</avg-thrust-n>
      <max-thrust-n>7.62</max-thrust-n>
      <tot-impulse-ns>1.09</tot-impulse-ns>
      <burn-time-s>0.36</burn-time-s>
      <data-files>2</data-files>
      <info-url>http://www.thrustcurve.org/motorsearch.jsp?id=6</info-url>
      <prop-weight-g>2.0</prop-weight-g>
      <delays>2,4</delays>
      <prop-info>black powder</prop-info>
      <updated-on>2014-07-05</updated-on>
    </result>
    ...
    
## Download Data Files

    POST http://www.thrustcurve.org/servlets/download
    <download-request>
      <motor-ids>
        <id>6</id>
        <id>7</id>
      </motor-ids>
    </download-request>
