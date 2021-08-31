
### sqlink

```bash
***************** sqlink **********************
:

# This script needs "runas" program to create directories owned by informix.
RASU="userid root"; export RASU 
RASI="userid informix"; export RASI

# Prompt for location of FROM sqldist.
echo "enter Location of Nightly build sqldist."
read FROM
if [ ! -d $FROM ] ; then
    echo "Error : $FROM does not exist"
    exit 1
fi

echo
echo
TO=`pwd`
echo "Using Current directory ($TO) as TO sqldist to setup links"
echo "Do you want to proceed ? "
read ans
if [ "x$ans" != "xy" ] ; then
    echo "Exiting without setting up links"
    exit 0
fi
    
cd $TO
# Create few essential directories you where you need to write into.
dirlist="bin lib incl etc msg lib/esql"
$RASU mkdir $dirlist
$RASU chown informix $dirlist .
$RASU chgrp informix $dirlist .
$RASI chmod 777 $dirlist .

# Ok, now link everything to nightly build sqldist. You will get errors for
# bin, lib, incl, etc, msg and lib/esql alreay exists. That is ok.

echo "Linking to nightly build sqldist .."
echo "You will get errors for bin, lib, incl, etc, msg and lib/esql"
echo "alreay exists. That's ok"
echo
ln -s $FROM/* .
for d in $dirlist ; do
    cd $TO/$d
    ln -s $FROM/$d/* .
done

cd $TO/bin


# Now one little step.
# All tb* (tbinit, tbmode) utilities are now links to on* (oninit, onmode).
# Above step created links for these tb* utilities to nightly build sqldist 
# area. They should be links to your local on* utilities, otherwise if you
# replace on* utility by your private copy for testing, tb* utility will still
# be pointing to nightly build on* utility.

list="tbcheck    tbload     tbmode     tbparams   tbstat     tbunload tbinit     tblog      tbmonitor  tbspaces   tbtape"

for i in $list
do
    if [ -f $i ] ; then
	rm -f $i
        ln -s `echo $i | sed -e 's/tb/on/'` $i
    fi
done 
```
