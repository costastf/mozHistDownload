#!/usr/bin/env python
#-*- coding: UTF-8 -*-
# File: mozilla_download_history_export.py
# Copyright (c) 2014 by None
#
# GNU General Public Licence (GPL)
# 
# This program is free software; you can redistribute it and/or modify it under
# the terms of the GNU General Public License as published by the Free Software
# Foundation; either version 2 of the License, or (at your option) any later
# version.
# This program is distributed in the hope that it will be useful, but WITHOUT
# ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS
# FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more
# details.
# You should have received a copy of the GNU General Public License along with
# this program; if not, write to the Free Software Foundation, Inc., 59 Temple
# Place, Suite 330, Boston, MA  02111-1307  USA
#
__author__    = 'Costas Tyfoxylos <costas.tyf@gmail.com>'
__docformat__ = 'plaintext'
__date__      = '12/01/2014'

import sqlite3 as sq
import json
import sys

if __name__=='__main__':
    try:
        sqfile = sys.argv[1]
    except IndexError:
        print('Please supply a firefox places.sqlite file as argument. Quiting...')
        raise SystemExit
    try:    
        con = sq.connect(sqfile)
        cur=con.cursor()
        links={}
        for row in cur.execute('select place_id from moz_historyvisits where visit_type="7"').fetchall():
            cur.execute('select content from moz_annos where place_id=%d and anno_attribute_id="15"'% row[0])
            name = cur.fetchone()[0]
            cur.execute('select url from moz_places where id=%d'% row[0])
            url = cur.fetchone()[0]
            links[name]=url
    except Exception, e:
	    print('Something happened.\nTraceback :{0}'.format(e))
	    raise SystemExit
    with open('firefox_download_history.json','w') as f:
	    f.write(json.dumps(links))

