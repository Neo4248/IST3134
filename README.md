# IST3134
Individual Assignment
#mapper
#!/usr/bin/env python 3

  

import sys 

  

def mapper(value): 

    output = value.strip().split(',') 
    steam_id = output[0] 
    playtime = output[6] 

  

    try: 
        playtime = float(playtime) 
    except ValueError: 
        return 

    print("%s\t%s" % (steam_id, playtime)) 

if_name_ == "_main_":
    for line in sys.stdin: 
    mapper(line)


#reducer
#!/usr/bin/env python3 

from operator import itemgetter
import sys

def reducer(app_id, playtime):
    total_playtime = sum(playtime)
    num_playtime = len(playtime)
    average_playtime = total_playtime / num_playtime
    print("%s\t%s" % (app_id, average_playtime))

if _name_ == "_main_":
    current_app_id = None
    playtime = []

    for line in sys.stdin:
        app_id, playtime = line.strip().split('\t')
        playtime = float(playtime)

        if current_app_id is None:
            current_app_id = app_id

        if app_id != current_app_id:
            reducer(current_app_id, playtime)
            playtime = []
            current_app_id = app_id

        playtime.append(playtime)

    if current_app_id is not None:
        reducer(current_app_id, playtime)
    
