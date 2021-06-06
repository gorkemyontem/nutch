# SWE-599-Nutch-Crawler
# NOTES

https://twg.io/blog/things-i-wish-i-knew-about-docker-before-i-started-using-it/

docker-compose build 
docker-compose build — no-cache
docker-compose up


docker exec -it frontend /bin/bash
docker exec -it <container_id> sh
docker-compose exec <container_id> sh

<!-- https://medium.com/geeks-prep/your-first-steps-to-building-a-web-crawler-integrating-nutch-with-solr-b5d916af3d32 -->
<!-- https://stackoverflow.com/questions/14788345/how-to-install-the-jdk-on-ubuntu-linux/14788889 -->
sudo apt update
<!-- sudo apt install default-jre -->
sudo apt install openjdk-8-jdk
sudo apt-get install ant
/mnt/c/Projects/SWE-599-Nutch-Crawler/nutch/nutch-release-1.18 >>> ant
SOLR_HOME="/mnt/c/Projects/SWE-599-Nutch-Crawler/solr/solr-8.5.1"
NUTCH_HOME="/mnt/c/Projects/SWE-599-Nutch-Crawler/nutch/nutch-release-1.18/src"
cd $SOLR_HOME/server/solr/configsets >>> mkdir -p nutch
cp -r ./_default/* nutch/cd
$SOLR_HOME/bin/solr create -c nutch -d $SOLR_HOME/server/solr/configsets/nutch/conf/
DOGRU SCHEMA.XML https://github.com/apache/nutch/blob/master/src/plugin/indexer-solr/schema.xml

bin/solr stop
bin/solr start

<!-- JAVA_HOME="/usr" -->
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64


$NUTCH_HOME/bin/nutch inject crawl/crawldb urls


# Nutch data is composed of:

- The crawl database, or crawldb. This contains information about every URL known to Nutch, including whether it was fetched, and, if so, when.
- The link database, or linkdb. This contains the list of known links to each URL, including both the source URL and anchor text of the link.
- A set of segments. Each segment is a set of URLs that are fetched as a unit. Segments are directories with the following subdirectories:
    - a crawl_generate names a set of URLs to be fetched
    - a crawl_fetch contains the status of fetching each URL
    - a content contains the raw content retrieved from each URL
    - a parse_text contains the parsed text of each URL
    - a parse_data contains outlinks and metadata parsed from each URL
    - a crawl_parse contains the outlink URLs, used to update the crawldb


//////////////
nutch    | Usage: nutch COMMAND [-Dproperty=value]... [command-specific args]...
nutch    | where COMMAND is one of:
nutch    |   readdb            read / dump crawl db
nutch    |   mergedb           merge crawldb-s, with optional filtering
nutch    |   readlinkdb        read / dump link db
nutch    |   inject            inject new urls into the database
nutch    |   generate          generate new segments to fetch from crawl db
nutch    |   freegen           generate new segments to fetch from text files
nutch    |   fetch             fetch a segment's pages
nutch    |   parse             parse a segment's pages
nutch    |   readseg           read / dump segment data
nutch    |   mergesegs         merge several segments, with optional filtering and slicing
nutch    |   updatedb          update crawl db from segments after fetching
nutch    |   invertlinks       create a linkdb from parsed segments
nutch    |   mergelinkdb       merge linkdb-s, with optional filtering
nutch    |   index             run the plugin-based indexer on parsed segments and linkdb
nutch    |   dedup             deduplicate entries in the crawldb and give them a special status
nutch    |   dump              exports crawled data from segments into files
nutch    |   commoncrawldump   exports crawled data from segments into common crawl data format encoded as CBOR
nutch    |   solrindex         run the solr indexer on parsed segments and linkdb - DEPRECATED use the index command instead
nutch    |   solrdedup         remove duplicates from solr - DEPRECATED use the dedup command instead
nutch    |   solrclean         remove HTTP 301 and 404 documents from solr - DEPRECATED use the clean command instead
nutch    |   clean             remove HTTP 301 and 404 documents and duplicates from indexing backends configured via plugins
nutch    |   parsechecker      check the parser for a given url
nutch    |   indexchecker      check the indexing filters for a given url
nutch    |   filterchecker     check url filters for a given url
nutch    |   normalizerchecker check url normalizers for a given url
nutch    |   domainstats       calculate domain statistics from crawldb
nutch    |   protocolstats     calculate protocol status code stats from crawldb
nutch    |   crawlcomplete     calculate crawl completion stats from crawldb
nutch    |   webgraph          generate a web graph from existing segments
nutch    |   linkrank          run a link analysis program on the generated web graph
nutch    |   scoreupdater      updates the crawldb with linkrank scores
nutch    |   nodedumper        dumps the web graph's node scores
nutch    |   plugin            load a plugin and run one of its classes main()
nutch    |   junit             runs the given JUnit test
nutch    |   startserver       runs the Nutch Server on localhost:8081
nutch    |   webapp            run a local Nutch Web Application on locahost:8080
nutch    |   warc              exports crawled data from segments at the WARC format
nutch    |   updatehostdb      update the host db with records from the crawl db
nutch    |   readhostdb        read / dump host db
nutch    |   sitemap           perform Sitemap processing
nutch    |   showproperties    print Nutch/Hadoop configuration properties to stdout
nutch    |  or
nutch    |   CLASSNAME         run the class named CLASSNAME

https://www.slideshare.net/abial/nutch-as-a-web-data-mining-platform

TODO:
https://stackoverflow.com/a/54251381
