You have 2200 lines of of text file like the below. It keeps mailing list for 1000+ servers.
-------------------------------------------------------------------------------------------
amk:asiatjb1.sang.gategate.com: mlist-crit=sga.it.infra\@gategate.com,bdc.-.database.and.web.delivery\@gategate.com,sga.it.dc.opn\@gategate.com mlist-maj=sga.it.infra\@gategate.com,bdc.-.database.and.web.delivery\@gategate.com mlist-min=sga.it.infra\@gategate.com
amk:asiatjb1: mlist-crit=sga.it.infra\@gategate.com,bdc.-.database.and.web.delivery\@gategate.com,sga.it.dc.opn\@gategate.com mlist-maj=sga.it.infra\@gategate.com,bdc.-.database.and.web.delivery\@gategate.com mlist-min=sga.it.infra\@gategate.com


amk:asiatjb2.sang.gategate.com: mlist-crit=sga.it.infra\@gategate.com,bdc.-.database.and.web.delivery\@gategate.com,sga.it.dc.opn\@gategate.com mlist-maj=sga.it.infra\@gategate.com,bdc.-.database.and.web.delivery\@gategate.com mlist-min=sga.it.infra\@gategate.com
amk:asiatjb2: mlist-crit=sga.it.infra\@gategate.com,bdc.-.database.and.web.delivery\@gategate.com,sga.it.dc.opn\@gategate.com mlist-maj=sga.it.infra\@gategate.com,bdc.-.database.and.web.delivery\@gategate.com mlist-min=sga.it.infra\@gategate.com


amk:asiatjb3.sang.gategate.com: mlist-crit=sga.it.infra\@gategate.com,bdc.-.database.and.web.delivery\@gategate.com,sga.it.dc.opn\@gategate.com mlist-maj=sga.it.infra\@gategate.com,bdc.-.database.and.web.delivery\@gategate.com mlist-min=sga.it.infra\@gategate.com
amk:asiatjb3: mlist-crit=sga.it.infra\@gategate.com,bdc.-.database.and.web.delivery\@gategate.com,sga.it.dc.opn\@gategate.com mlist-maj=sga.it.infra\@gategate.com,bdc.-.database.and.web.delivery\@gategate.com mlist-min=sga.it.infra\@gategate.com


You are given a list of nodes (/tmp/nodes), about 150 units, where u need to update the mail address for these nodes only
OLDADD="bdc.-.erp.delivery"
NEWADD="bdc.database.delivery"


# bash-script-notes
#!/bin/bash

NODES="/tmp/nodes"
HPOVNODES="/tmp/hpov-nodes.txt.bak"

OLDADD="bdc.-.erp.delivery"
NEWADD="bdc.database.delivery"

for node in `cat $NODES`
do
        echo $node
        linenum=`sed -n "/$node/I =" $HPOVNODES`
        arr=$(echo $linenum | tr " " "\n")

        for x in $arr
        do
                echo $x
                sed -i "${x}s/$OLDADD/$NEWADD/g" $HPOVNODES
        done
done
