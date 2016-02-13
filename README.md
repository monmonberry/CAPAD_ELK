# CAPAD_ELK
Linux Conf AU 2016 - ELK entry


Downloaded CAPAD 2014 terrestrial data from: www.environment.gov.au/fed/
Converted .dbf file inside zip to csv with Excel (todo check how to do with Linux)
The CAPAD_2014_terrestrial.csv file has been included for convenience.

Excluded first line from csv as well as any row with OVERLAP=2 or NRS_PA=N or NRS_PA=ND
Cofigured a translate for IUCN field

TODO: importing of the dates

# install required filter
./logstash-2.1.1/bin/plugin install logstash-filter-translate

# start elastic
./elasticsearch-2.1.1/bin/elasticsearch

#start kibana
./kibana-4.3.1-linux-x64/bin/kibana

# Import data
cat CAPAD_2014_terrestrial.csv |  ./logstash-2.1.1/bin/logstash -f capad-logstash.conf

#delete data after mistake!
curl -XDELETE localhost:9200/capad

