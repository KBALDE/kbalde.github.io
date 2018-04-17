---
published: false
---
## Scripting with python to provide an app installation or configuration

I am more of shell when it comes to scripting on linux. But to manipulating many conf files, scripting with python become appear to be more efficient.

A Little cheat sheet for using configparser.

Pre-requisite
configparser module must be installed with a python version

#### Write the script

```
vim script.py
```

```python
import sys
import os
import shlex
from subprocess import Popen, PIPE
import configparser

# Here sys.argv[0] is the program ie. script name.

if (len(sys.argv) != 3):
    print ("Nb args : "+str(len(sys.argv)))
    print ("BAD INPUT ARGS, HAVE TO 2 ARGS")
    print ("ARG1 : conf File ")
    print ("ARG2 : conf File group properties and parameters ")
    sys.exit(1)

f_common=sys.argv[1]
domain=sys.argv[2]

# instanciate the file reader and parser
cfg_load=configparser.RawConfigParser()

# load the file or parse it
cfg_load.read(f_common)

source_path=cfg_load.get(domain, "source_path")

print ("Hello Louis, Ella is Bad !")

print ("The source path is " + source_path)
```


#### Now  create the conf file

```
vim conf.txt
```

And Then paste

```
[operate]
KBA=marathon
[app]
name_app=kba
version_app=1.0.0
source_path=/images/install
target_path=/var/opt/data/flat/dlab
hadoop_folder=hadoop_conf
```

Run the script

```
python script.py conf.txt app
```

You have just retrieved properties from a file and now ready to provide an app with them

