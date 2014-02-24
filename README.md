# elasticsearch-rss

RSS feed and management script for ElasticSearch

### TODO

* Add a -t parameter for target index (?)
* Add a ELASTICSEARCH_RSS_INDEX_NAME or similar for default index name (?)
* Add index name as parameter to create-index script (?)
* Clean up output
* Better exception handling
* Bulk indexing of new items

## Installation

Pre-requisites:

Python 2.6 with modules feedparser and elasticsearch:

  pip install feedparser elasticsearch

### Setup

First run the create-index script to create your RSS index in ElasticSearch and with some basic mappings.
Edit the script first if you want to change index name and/or particular mappings.

If you changed the index name, this must also be changed within the script, in the constant STORE=indexname.

### Usage

Suggest doing `rss -h` for the most current version.

    rss info [-v] [-s <since>] [<feeds>]                    Show feed/channel info
    rss add <name> <url>                                    Add feed
    rss remove [-c] [<feeds>]                               Remove feed
    rss list [-v] [-d] [-l <limit>] [-s <since>] [<feeds>]  List items in index
    rss clean [-b <before>] [<feeds>]                       Clean items in index
    rss fetch [-v] [-d] [-f] [<feeds>]                      Fetch items
    
    -v = verbose
    -d = debug (even more verbose)
    -c = cascading, i.e. items will also be removed if you remove a feed with this option
    -f = force, i.e. fetch all available items regardless of timestamps and last fetch
    -l limit = number of items to show
    -s since = for listing items since 'since', with format #unit, where # is a number and unit is
       one of 's', 'm', 'h', 'd', 'w', 'M', 'y' (second, minute, etc)
    -s ago = for deleting items older than 'ago', same format as for 'since'

`rss add` can also take a batch fed from standard input. I.e. with a file containing name and URL pairs (space between the two and one feed specification on each line), do `rss add <myfile`.
