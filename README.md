mysql-Con
=========




#!/usr/bin/python
# -*- coding: utf-8 -*-

import MySQLdb



def supermain():
    db = MySQLdb.connect("localhost","root","6Tresxcvbhy")
    cursor = db.cursor()

    sql = """ create database IF NOT EXISTS  zivame """
    cursor.execute(sql)

    sql =""" use zivame """
    cursor.execute(sql)
    
    #dte TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

    sql = """create table IF NOT EXISTS  zivame_data (
               task_id int(11) NOT NULL AUTO_INCREMENT,
               product_id varchar(100),
	       product_title text ,
	       target_link text,
	       selliing_price text,
	       category text, 
	       sub_category text,
               sub_sub_category text, 
	       brand text, 
	       image_link text, 
	       mrp text, 
	       color text, 
	       target text, 
	       product_url varchar(500), 
	       seller text, 
	       meta_title text, 
	       meta_desc text, 
	       size text, 
	       product_desc  text,
	       product_spec text,
	       dte text,
	       status varchar(10), 
	       PRIMARY KEY (task_id, product_id)
	    )"""

    cursor.execute(sql)


    try:
        sql2 = "create unique index zivame_index on zivame_data (task_id, product_id , status)"
        cursor.execute(sql2)

    except:
        pass  



    sql = """alter ignore  table  zivame_data add upload_status enum('NO','YES', 'F') DEFAULT 'NO';"""

    try:
        cursor.execute(sql)
    except:
        pass

    sql = """UPDATE  zivame_data  set upload_status = 'NO' """
    cursor.execute(sql)
    db.commit()

    sql = """alter ignore  table  zivame_data add upload_image_status enum('NO','YES', 'F') DEFAULT 'NO';"""

    try:
        cursor.execute(sql)
        db.commit()
    except:
        pass

    sql = """alter ignore  table  zivame_data add upload_to_imgtable enum('NO','YES', 'F') DEFAULT 'NO';"""

    try:
        cursor.execute(sql)
        db.commit()
    except:
        pass




  
    db.close()
    print " db_close()......................................................"



if __name__=="__main__":
    supermain()

