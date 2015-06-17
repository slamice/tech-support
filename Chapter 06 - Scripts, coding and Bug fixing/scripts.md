Scripts
=========================================

_script [skript]: "A list of commands that are executed by a certain program or scripting engine."_

From my experience working at Gengo, scripts are usually written to solve the following problems:

- Lacking the resources (time, money) to fit in a fix/feature in the product with UI
- Data corruption / bug fix
- Number crunching, quick analytics

They can be quick and flexible to write. However, since they are hacked together quickly and you need domain knowledge to run them, scripts inevitably get neglected. The codebase and database schema may change while the scripts slowly go out of date.

The obvious longterm solution is to have whatever problem they are trying to solve go through the development process properly, avoiding writing scripts altogether. In the short term though, scripts are still useful:

1. They record how the original problem was solved.
2. Some of the code could be re-used in the main codebase.
3. A slight variation of a script could be used to solve a different problem.

We've had a lot of scripts in our system where it's not entirely clear what they do or how to run them. There are a few practical things we can keep in mind while writing them that'll help when running, refactoring or revising in the future: 

### Arg parameters

It isn't neccesarily obvious what's the script for, what parameters you'll need and in which order. That's why it's incredibly helpful to include libraries to properly parse arguments and explain what your script does. Each command in a shell come with a manual by default for good reason.

e.g. in python, we can use [optparse](https://docs.python.org/2/library/optparse.html), [argparse](https://code.google.com/p/argparse/) or [getopt](http://pymotw.com/2/getopt/).

```
    usage = 'Usage: %prog -D <database> -F file.csv'
    cmdline = optparse.OptionParser(usage, version="example 0.1", description="""Read csv data, commit to the db, etc.""")
    
    cmdline.add_option('-D', '--database',
                       help = 'databases to pick from: {dbs}'.format(dbs=database_kwargs.keys()), 
                       action='store', type='string', dest='database', default='dev')
    cmdline.add_option('-F', '--csv_file',
                        help = """Path to and name of csv file. The data should be comma delimited like this:
                        First_param, Second_param, Third_param
                        Please don't include headers.""", action='store', type='string', dest='csv_file', default=None)
    (options, args) = cmdline.parse_args()
```

### Logging

Many of us are comfortable with print statements when writing a script. While that's ok, it's not so great when you're trying to discern what's a log and what isn't. Also, all print messages go into _stdout_. This isn't ideal if you have other data going there too.

Some advantages to adding a specific logging module:

- You can control messages and filter out unimportant ones
- You can decide where and how to output later

e.g. python has a default module for [logging](https://docs.python.org/2/library/logging.html). There's a good article explaining logging in python [here](http://victorlin.me/posts/2012/08/26/good-logging-practice-in-python). Basically you only need to call the module and initialize it with the default log output level you want.

```

import logging

...

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

...

logger.info('** Example info... **')
logging.error('Detailed exception, who knew... ', exc_info=True)
```

### Comments:

Of course this step is really important, especially since no one will read this code that often. It's also a good idea to put an intro at the top of the script with a description and assumptions on the environment to run it in. Since usually there is no strict structure to a script, a little intro will help loads.

e.g. in python script:

```

# #!/usr/bin/env python
# -*- coding: utf-8 -*-
#
# Script Name:  Example
# Description:  This is a template for a script for it to do "stuff"
#               (Describe "stuff" here).
#               that you want it to do. Please run 'python example.py -h'
#               For more info.
# Assumptions:  Running on dev env, etc. 
# Created By:   Some Guy
# Date Created: 2014/XX/XX
#
######

```

I attached a [template python script](code/example.py) as a starting point to make writing a new script easier. It includes reading a csv and connecting to a db.