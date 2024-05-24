# utl-using-column-position-instead-of-excel-column-names-due-to-misspellings-sas-r-python
Using column position instead of excel column names due to misspellings sas r python
    %let pgm=utl-using-column-position-instead-of-excel-column-names-due-to-misspellings-sas-r-python;

    Using column position instead of excel column names due to misspellings sas r python

    My boss imported fifty state excel sheets where some of the column names have misspellings.
    The column position was accurate but some of the column names were mispelled.
    I need to fix the misspellings to match my bosses template template.
    I also need to append the 50 sheets to the template.

       SOlUTIONS

           1 SAS SQL
           2 R SQL      (uses stattrasfer to create output sas dataset)
           3 Python SQL (uses stattrasfer to create output sas dataset)


    github
    https://tinyurl.com/yshsxv79
    https://github.com/rogerjdeangelis/utl-using-column-position-instead-of-excel-column-names-due-to-misspellings-sas-r-python

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                                                  |                                  |                                  */
    /*           INPUT                                  |       PROCESS                    | OUTPUT(all have template names)  */
    /*                                                  |                                  |                                  */
    /* ALL SHEETS NEED TO HAVE THESE NAMES              | proc sql;                        | SHEET    GENDER    AGE    YEAR   */
    /*                                                  |    create                        |                                  */
    /* SD1.TEMPLATE total obs=1                         |      table want as               |   1        F        18    2001   */
    /*                                                  |    select                        |   1        M        15    2002   */
    /* SHEET    GENDER    AGE    YEAR                   |      sheet                       |   1        M        14    2009   */
    /*                                                  |     ,gender                      |   1        F        16    2008   */
    /*   .        .        .       .                    |     ,age                         |                                  */
    /*                                                  |     ,year                        |   2        M        17    2001   */
    /* BOSSES IMPORTS (MANY WRONG NAMES)                |    from                          |   2        M        16    2002   */
    /*                                                  |      sd1.template                |   2        M        14    2009   */
    /*  SD1.SHEET1 t                                    |    where                         |   2        F        16    2008   */
    /*                                                  |      not missing(sheet)          |                                  */
    /*  SHEET    SEX    AGEYR    YEAR                   |    union all                     |   3        F        13    2001   */
    /*                                                  |      (select * from sd1.sheet1)  |   3        F        13    2002   */
    /*    1       F       18     2001                   |    union all                     |   3        F        14    2009   */
    /*    1       M       15     2002                   |      (select * from sd1.sheet2)  |   3        M        15    2008   */
    /*    1       M       14     2009                   |    union all                     |                                  */
    /*    1       F       16     2008                   |      (select * from sd1.sheet3)  |                                  */
    /*                                                  | ;quit;                           |                                  */
    /*  SD1.SHEET2                                      |                                  |                                  */
    /*                                                  |                                  |                                  */
    /*  SHEET   GENDER TEENAGE   DOBYR                  |                                  |                                  */
    /*                                                  |                                  |                                  */
    /*    2       M       17      2001                  |                                  |                                  */
    /*    2       M       16      2002                  |                                  |                                  */
    /*    2       M       14      2009                  |                                  |                                  */
    /*    2       F       16      2008                  |                                  |                                  */
    /*                                                  |                                  |                                  */
    /*  SD1.SHEET3                                      |                                  |                                  */
    /*                                                  |                                  |                                  */
    /*  SHEET   GENDER  AGEYR     YR                    |                                  |                                  */
    /*                                                  |                                  |                                  */
    /*    3       F       13      2001                  |                                  |                                  */
    /*    3       F       13      2002                  |                                  |                                  */
    /*    3       F       14      2009                  |                                  |                                  */
    /*    3       M       15      2008                  |                                  |                                  */
    /*                                                  |                                  |                                  */
    /* data                                             |                                  |                                  */
    /*    sd1.sheet1(rename=(gender=sex  age=ageyr ))   |                                  |                                  */
    /*    sd1.sheet2(rename=(age=teenage year=dobyr))   |                                  |                                  */
    /*    sd1.sheet3(rename=(age=ageyr   year=yr   ))   |                                  |                                  */
    /*  ;                                               |                                  |                                  */
    /*  input sheet gender$ age year;                   |                                  |                                  */
    /*  select (sheet);                                 |                                  |                                  */
    /*    when (1) output sd1.sheet1;                   |                                  |                                  */
    /*    when (2) output sd1.sheet2;                   |                                  |                                  */
    /*    when (3) output sd1.sheet3;                   |                                  |                                  */
    /*  end; /* leave off to force error */             |                                  |                                  */
    /* cards4;                                          |                                  |                                  */
    /* 1 F 18 2001                                      |                                  |                                  */
    /* 1 M 15 2002                                      |                                  |                                  */
    /* 1 M 14 2009                                      |                                  |                                  */
    /* 1 F 16 2008                                      |                                  |                                  */
    /* 2 M 17 2001                                      |                                  |                                  */
    /* 2 M 16 2002                                      |                                  |                                  */
    /* 2 M 14 2009                                      |                                  |                                  */
    /* 2 F 16 2008                                      |                                  |                                  */
    /* 3 F 13 2001                                      |                                  |                                  */
    /* 3 F 13 2002                                      |                                  |                                  */
    /* 3 F 14 2009                                      |                                  |                                  */
    /* 3 M 15 2008                                      |                                  |                                  */
    /* ;;;;                                             |                                  |                                  */
    /* run;quit;                                        |                                  |                                  */
    /*                                                  |                                  |                                  */
    /* data sd1.template;                               |                                  |                                  */
    /*  retain sheet . gender '.' age . year .;         |                                  |                                  */
    /*  output;                                         |                                  |                                  */
    /* run;quit;                                        |                                  |                                  */
    /*                                                  |                                  |                                  */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */


    data sd1.template;
     retain sheet . gender '.' age . year .;
     output;
    run;quit;

    data
       sd1.sheet1(rename=(gender=sex  age=ageyr ))
       sd1.sheet2(rename=(age=teenage year=dobyr))
       sd1.sheet3(rename=(age=ageyr   year=yr   ))
     ;
     input sheet gender$ age year;
     select (sheet);
       when (1) output sd1.sheet1;
       when (2) output sd1.sheet2;
       when (3) output sd1.sheet3;
     end; /* leave off to force error */
    cards4;
    1 F 18 2001
    1 M 15 2002
    1 M 14 2009
    1 F 16 2008
    2 M 17 2001
    2 M 16 2002
    2 M 14 2009
    2 F 16 2008
    3 F 13 2001
    3 F 13 2002
    3 F 14 2009
    3 M 15 2008
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* ALL SHEETS NEED TO HAVE THESE NAMES                                                                                    */
    /*                                                                                                                        */
    /* SD1.TEMPLATE total obs=1                                                                                               */
    /*                                                                                                                        */
    /* SHEET    GENDER    AGE    YEAR                                                                                         */
    /*                                                                                                                        */
    /*   .        .        .       .                                                                                          */
    /*                                                                                                                        */
    /* BOSSES IMPORTS (MANY WRONG NAMES)                                                                                      */
    /*                                                                                                                        */
    /*  SD1.SHEET1 t                                                                                                          */
    /*                                                                                                                        */
    /*  SHEET    SEX    AGEYR    YEAR                                                                                         */
    /*                                                                                                                        */
    /*    1       F       18     2001                                                                                         */
    /*    1       M       15     2002                                                                                         */
    /*    1       M       14     2009                                                                                         */
    /*    1       F       16     2008                                                                                         */
    /*                                                                                                                        */
    /*  SD1.SHEET2                                                                                                            */
    /*                                                                                                                        */
    /*  SHEET   GENDER TEENAGE   DOBYR                                                                                        */
    /*                                                                                                                        */
    /*    2       M       17      2001                                                                                        */
    /*    2       M       16      2002                                                                                        */
    /*    2       M       14      2009                                                                                        */
    /*    2       F       16      2008                                                                                        */
    /*                                                                                                                        */
    /*  SD1.SHEET3                                                                                                            */
    /*                                                                                                                        */
    /*  SHEET   GENDER  AGEYR     YR                                                                                          */
    /*                                                                                                                        */
    /*    3       F       13      2001                                                                                        */
    /*    3       F       13      2002                                                                                        */
    /*    3       F       14      2009                                                                                        */
    /*    3       M       15      2008                                                                                        */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                             _
    / |  ___  __ _ ___   ___  __ _| |
    | | / __|/ _` / __| / __|/ _` | |
    | | \__ \ (_| \__ \ \__ \ (_| | |
    |_| |___/\__,_|___/ |___/\__, |_|
                                |_|
    */

    proc datasets lib=work nodetails nolist;
     delete want;
    run;quit;

    proc sql;
       create
         table want as
       select
         sheet
        ,gender
        ,age
        ,year
       from
         sd1.template
       where
         not missing(sheet)
       union all
         (select * from sd1.sheet1)
       union all
         (select * from sd1.sheet2)
       union all
         (select * from sd1.sheet3)
    ;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* OUTPUT(all have template names)                                                                                        */
    /*                                                                                                                        */
    /* SHEET    GENDER    AGE    YEAR                                                                                         */
    /*                                                                                                                        */
    /*   1        F        18    2001                                                                                         */
    /*   1        M        15    2002                                                                                         */
    /*   1        M        14    2009                                                                                         */
    /*   1        F        16    2008                                                                                         */
    /*                                                                                                                        */
    /*   2        M        17    2001                                                                                         */
    /*   2        M        16    2002                                                                                         */
    /*   2        M        14    2009                                                                                         */
    /*   2        F        16    2008                                                                                         */
    /*                                                                                                                        */
    /*   3        F        13    2001                                                                                         */
    /*   3        F        13    2002                                                                                         */
    /*   3        F        14    2009                                                                                         */
    /*   3        M        15    2008                                                                                         */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                     _
    |___ \   _ __   ___  __ _| |
      __) | | `__| / __|/ _` | |
     / __/  | |    \__ \ (_| | |
    |_____| |_|    |___/\__, |_|
                           |_|
    */


    %utl_rbegin;
    parmcards4;
    library(haven)
    library(sqldf)
    source("c:/temp/fn_tosas9.R")
    template<-read_sas("d:/sd1/template.sas7bdat")
    sheet1<-read_sas("d:/sd1/sheet1.sas7bdat")
    sheet2<-read_sas("d:/sd1/sheet2.sas7bdat")
    sheet3<-read_sas("d:/sd1/sheet3.sas7bdat")
    want<-sqldf('
       select
         sheet
        ,gender
        ,age
        ,year
       from
         template
       where
         sheet <> null
       union all
         select * from sheet1
       union all
          select * from sheet2
       union all
          select * from sheet3
        ');
    want;
    fn_tosas9(dataf=want);
    ;;;;
    %utl_rend;

    libname tmp "c:/temp";
    proc print data=tmp.want;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*   R                                                                                                                    */
    /*                                                                                                                        */
    /*      SHEET GENDER AGE YEAR                                                                                             */
    /*   1      1      F  18 2001                                                                                             */
    /*   2      1      M  15 2002                                                                                             */
    /*   3      1      M  14 2009                                                                                             */
    /*   4      1      F  16 2008                                                                                             */
    /*   5      2      M  17 2001                                                                                             */
    /*   6      2      M  16 2002                                                                                             */
    /*   7      2      M  14 2009                                                                                             */
    /*   8      2      F  16 2008                                                                                             */
    /*   9      3      F  13 2001                                                                                             */
    /*   10     3      F  13 2002                                                                                             */
    /*   11     3      F  14 2009                                                                                             */
    /*   12     3      M  15 2008                                                                                             */
    /*                                                                                                                        */
    /*   Back to SAS                                                                                                          */
    /*                                                                                                                        */
    /*   Obs    ROWNAMES    SHEET    GENDER    AGE    YEAR                                                                    */
    /*                                                                                                                        */
    /*     1        1         1        F        18    2001                                                                    */
    /*     2        2         1        M        15    2002                                                                    */
    /*     3        3         1        M        14    2009                                                                    */
    /*     4        4         1        F        16    2008                                                                    */
    /*     5        5         2        M        17    2001                                                                    */
    /*     6        6         2        M        16    2002                                                                    */
    /*     7        7         2        M        14    2009                                                                    */
    /*     8        8         2        F        16    2008                                                                    */
    /*     9        9         3        F        13    2001                                                                    */
    /*    10       10         3        F        13    2002                                                                    */
    /*    11       11         3        F        14    2009                                                                    */
    /*    12       12         3        M        15    2008                                                                    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____               _   _                             _
    |___ /   _ __  _   _| |_| |__   ___  _ __    ___  __ _| |
      |_ \  | `_ \| | | | __| `_ \ / _ \| `_ \  / __|/ _` | |
     ___) | | |_) | |_| | |_| | | | (_) | | | | \__ \ (_| | |
    |____/  | .__/ \__, |\__|_| |_|\___/|_| |_| |___/\__, |_|
            |_|    |___/                                |_|
    */

    %utl_pybegin;
    parmcards4;
    import os
    import sys
    import subprocess
    import time
    from os import path
    import pandas as pd
    import numpy as np
    import pyreadstat as ps
    from pandasql import sqldf
    mysql = lambda q: sqldf(q, globals())
    from pandasql import PandaSQL
    pdsql = PandaSQL(persist=True)
    sqlite3conn = next(pdsql.conn.gen).connection.connection
    sqlite3conn.enable_load_extension(True)
    sqlite3conn.load_extension('c:/temp/libsqlitefunctions.dll')
    mysql = lambda q: sqldf(q, globals())
    template,meta=ps.read_sas7bdat("d:/sd1/template.sas7bdat")
    sheet1,meta=ps.read_sas7bdat("d:/sd1/sheet1.sas7bdat")
    sheet2,meta=ps.read_sas7bdat("d:/sd1/sheet2.sas7bdat")
    sheet3,meta=ps.read_sas7bdat("d:/sd1/sheet3.sas7bdat")
    want = pdsql('''
       select
         sheet
        ,gender
        ,age
        ,year
       from
         template
       where
         sheet <> null
       union all
         select * from sheet1
       union all
          select * from sheet2
       union all
          select * from sheet3
    ''')
    print(want)
    exec(open('c:/temp/fn_tosas9.py').read())
    fn_tosas9(
       want
       ,dfstr="want"
       ,timeest=3
       )
    ;;;;
    %utl_pyend;

    libname tmp "c:/temp";
    proc print data=tmp.want;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* PYTHON                                                                                                                 */
    /*                                                                                                                        */
    /*     SHEET GENDER   AGE    YEAR                                                                                         */
    /* 0     1.0      F  18.0  2001.0                                                                                         */
    /* 1     1.0      M  15.0  2002.0                                                                                         */
    /* 2     1.0      M  14.0  2009.0                                                                                         */
    /* 3     1.0      F  16.0  2008.0                                                                                         */
    /* 4     2.0      M  17.0  2001.0                                                                                         */
    /* 5     2.0      M  16.0  2002.0                                                                                         */
    /* 6     2.0      M  14.0  2009.0                                                                                         */
    /* 7     2.0      F  16.0  2008.0                                                                                         */
    /* 8     3.0      F  13.0  2001.0                                                                                         */
    /* 9     3.0      F  13.0  2002.0                                                                                         */
    /* 10    3.0      F  14.0  2009.0                                                                                         */
    /* 11    3.0      M  15.0  2008.0                                                                                         */
    /*                                                                                                                        */
    /* BACK TO SAS                                                                                                            */
    /*                                                                                                                        */
    /* Obs    SHEET    GENDER    AGE    YEAR                                                                                  */
    /*                                                                                                                        */
    /*   1      1        F        18    2001                                                                                  */
    /*   2      1        M        15    2002                                                                                  */
    /*   3      1        M        14    2009                                                                                  */
    /*   4      1        F        16    2008                                                                                  */
    /*   5      2        M        17    2001                                                                                  */
    /*   6      2        M        16    2002                                                                                  */
    /*   7      2        M        14    2009                                                                                  */
    /*   8      2        F        16    2008                                                                                  */
    /*   9      3        F        13    2001                                                                                  */
    /*  10      3        F        13    2002                                                                                  */
    /*  11      3        F        14    2009                                                                                  */
    /*  12      3        M        15    2008                                                                                  */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
