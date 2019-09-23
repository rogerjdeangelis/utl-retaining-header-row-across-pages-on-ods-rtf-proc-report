# utl-retaining-header-row-across-pages-on-ods-rtf-proc-report
Retaining header row across pages on ods rtf proc report
    Retaining header row across pages on ods rtf proc report                                                                         
                                                                                                                                     
    Note proc report rtf cannot retain the header row across pages                                                                   
                                                                                                                                     
    github rtf output                                                                                                                
    https://tinyurl.com/y6pkzhey                                                                                                     
    https://github.com/rogerjdeangelis/utl-retaining-header-row-across-pages-on-ods-rtf-proc-report/blob/master/repeat.rtf           
                                                                                                                                     
    github                                                                                                                           
    https://tinyurl.com/y5qee85t                                                                                                     
    https://github.com/rogerjdeangelis/utl-retaining-header-row-across-pages-on-ods-rtf-proc-report                                  
                                                                                                                                     
    related to                                                                                                                       
    SAS Forum                                                                                                                        
    https://tinyurl.com/y62sgvb7                                                                                                     
    https://communities.sas.com/t5/ODS-and-Base-Reporting/ODS-RTF-spanrows-does-not-repeat-value-after-page-break/m-p/590998         
                                                                                                                                     
    Problem: (for documentation - no the same as example)                                                                            
                                                                                                                                     
      PAGE 1                                                                                                                         
                                                                                                                                     
       +--------------------------------------+                                                                                      
       |State  |Code   | County| Zip   | PopHT|                                                                                      
       +-------+-------+-------+-------+------+                                                                                      
       |Maine  | 1234  | Trout | 51234 |88,000|                                                                                      
       ----------------------------------------                                                                                      
       |       |       | Pike  | 51333 | 8,000|                                                                                      
       ----------------------------------------                                                                                      
       |       |       | Carp  | 51890 |28,000|                                                                                      
       ----------------------------------------                                                                                      
       ..                                                                                                                            
                                                                                                                                     
      PAGE 2                                                                                                                         
                                                                                                                                     
       +--------------------------------------+                                                                                      
       |State  |Code   | County| Zip   | PopHT|                                                                                      
       +-------+-------+-------+-------+------+                                                                                      
       |       |       | Bass  | 57234 |11,000|  * Need header                                                                       
       ----------------------------------------    'Maine 14'                                                                        
       |       |       | Rock  | 58333 | 7,000|                                                                                      
       ----------------------------------------                                                                                      
       |       |       | White | 59890 |99,000|                                                                                      
       ----------------------------------------                                                                                      
       ..                                                                                                                            
                                                                                                                                     
      PAGE 3                                                                                                                         
                                                                                                                                     
       +--------------------------------------+                                                                                      
       |State  |Code   | County| Zip   | PopHT|                                                                                      
       +-------+-------+-------+-------+------+                                                                                      
       |Mass   |  24   | Bass  | 57234 |11,000|  * new state and code                                                                
       ----------------------------------------                                                                                      
       |       |       | Rock  | 58333 | 7,000|                                                                                      
       ----------------------------------------                                                                                      
       |       |       | White | 59890 |99,000|                                                                                      
       ----------------------------------------                                                                                      
       ..                                                                                                                            
                                                                                                                                     
    *_                   _                                                                                                           
    (_)_ __  _ __  _   _| |_                                                                                                         
    | | '_ \| '_ \| | | | __|                                                                                                        
    | | | | | |_) | |_| | |_                                                                                                         
    |_|_| |_| .__/ \__,_|\__|                                                                                                        
            |_|                                                                                                                      
    ;                                                                                                                                
                                                                                                                                     
    data have;                                                                                                                       
    retain statename state countynm timezone city zip;                                                                               
    informat ZIP CITY STATE STATENAME COUNTYNM TIMEZONE $16.;                                                                        
    input ZIP CITY STATE STATENAME COUNTYNM TIMEZONE;                                                                                
    cards4;                                                                                                                          
    36003 Autaugaville 1234 Maine Autauga Central                                                                                    
    36006 Billingsley 1234 Maine Autauga Central                                                                                     
    36008 Booth 1234 Maine Autauga Central                                                                                           
    36051 Marbury 1234 Maine Autauga Central                                                                                         
    36066 Prattville 1234 Maine Autauga Central                                                                                      
    36749 Jones 1234 Maine Autauga Central                                                                                           
    36507 Minette 1234 Maine Baldwin Central                                                                                         
    36511 Secour 1234 Maine Baldwin Central                                                                                          
    36526 Daphne 1234 Maine Baldwin Central                                                                                          
    36527 Daphne 1234 Maine Baldwin Central                                                                                          
    36530 Elberta 1234 Maine Baldwin Central                                                                                         
    2534 Cataumet 25 Mass Barnstable Eastern                                                                                         
    2536 Falmouth 25 Mass Barnstable Eastern                                                                                         
    2537 Sandwich 25 Mass Barnstable Eastern                                                                                         
    2540 Andwich 25 Mass Barnstable Eastern                                                                                          
    ;;;;                                                                                                                             
    run;quit;                                                                                                                        
                                                                                                                                     
    * groups have been made very short for documentation purposes;                                                                   
                                                                                                                                     
    WORK.HAVE total obs=15                                                      |  RULES                                             
                                                                                |                                                    
     STATENAME        STATE     COUNTYNM     TIMEZONE    CITY             ZIP   |                                                    
                                                                                                                                     
     Maine            1234     Autauga       Central     Autaugaville    36003  | Page 1                                             
     Maine            1234     Autauga       Central     Billingsley     36006  |                                                    
     Maine            1234     Autauga       Central     Booth           36008  |                                                    
     Maine            1234     Autauga       Central     Marbury         36051  |                                                    
     Maine            1234     Autauga       Central     Prattville      36066  |                                                    
     Maine            1234     Autauga       Central     Jones           36749  |                                                    
                                                                                                                                     
     Maine            1234     Baldwin       Central     Minette         36507  | Page 2                                             
     Maine            1234     Baldwin       Central     Secour          36511  |                                                    
     Maine            1234     Baldwin       Central     Daphne          36526  |                                                    
     Maine            1234     Baldwin       Central     Daphne          36527  |                                                    
     Maine            1234     Baldwin       Central     Elberta         36530  |                                                    
                                                                                                                                     
     Mass               25     Barnstable    Eastern     Cataumet        2534   | Page 4                                             
     Mass               25     Barnstable    Eastern     Falmouth        2536   |                                                    
     Mass               25     Barnstable    Eastern     Sandwich        2537   |                                                    
     Mass               25     Barnstable    Eastern     Andwich         2540   |                                                    
                                                                                                                                     
    *            _               _                                                                                                   
      ___  _   _| |_ _ __  _   _| |_                                                                                                 
     / _ \| | | | __| '_ \| | | | __|                                                                                                
    | (_) | |_| | |_| |_) | |_| | |_                                                                                                 
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                                
                    |_|                                                                                                              
    ;                                                                                                                                
                                                                                                                                     
    Problem: (for documentation - no the same as example)                                                                            
                                                                                                                                     
      PAGE 1                                                                                                                         
                                                                                                                                     
       +--------------------------------------+                                                                                      
       |State  |Code   | County| Zip   | PopHT|                                                                                      
       +-------+-------+-------+-------+------+                                                                                      
       |Maine  | 14    | Trout | 51234 |88,000|                                                                                      
       ----------------------------------------                                                                                      
       |       |       | Pike  | 51333 | 8,000|                                                                                      
       ----------------------------------------                                                                                      
       |       |       | Carp  | 51890 |28,000|                                                                                      
       ----------------------------------------                                                                                      
       ..                                                                                                                            
                                                                                                                                     
      PAGE 2                                                                                                                         
                                                                                                                                     
       +--------------------------------------+                                                                                      
       |State  |Code   | County| Zip   | PopHT|                                                                                      
       +-------+-------+-------+-------+------+                                                                                      
       |Maine  | 14    | Bass  | 57234 |11,000|  * header added                                                                      
       ----------------------------------------                                                                                      
       |       |       | Rock  | 58333 | 7,000|                                                                                      
       ----------------------------------------                                                                                      
       |       |       | White | 59890 |99,000|                                                                                      
       ----------------------------------------                                                                                      
       ..                                                                                                                            
                                                                                                                                     
      PAGE 3                                                                                                                         
                                                                                                                                     
       +--------------------------------------+                                                                                      
       |State  |Code   | County| Zip   | PopHT|                                                                                      
       +-------+-------+-------+-------+------+                                                                                      
       |Mass   | 24    | Bass  | 57234 |11,000|                                                                                      
       ----------------------------------------                                                                                      
       |       |       | Rock  | 58333 | 7,000|                                                                                      
       ----------------------------------------                                                                                      
       |       |       | White | 59890 |99,000|                                                                                      
       ----------------------------------------                                                                                      
       ..                                                                                                                            
                                                                                                                                     
    *                                                                                                                                
     _ __  _ __ ___   ___ ___  ___ ___                                                                                               
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                                              
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                              
    | .__/|_|  \___/ \___\___||___/___/                                                                                              
    |_|                                                                                                                              
    ;                                                                                                                                
                                                                                                                                     
    data havPge;                                                                                                                     
       retain pge 1;                                                                                                                 
       set have;                                                                                                                     
       by statename state;                                                                                                           
       select;                                                                                                                       
         when (first.state    ) do; pge=pge+1; output; end;                                                                          
         when (mod(_n_,6)=0   ) do; pge=pge+1; output; end;                                                                          
         otherwise do; call missing(statename, state); output; end;                                                                  
       end;                                                                                                                          
    run;quit;                                                                                                                        
                                                                                                                                     
    ods exclude _all_;;                                                                                                              
    ods rtf style=styles.statistical                                                                                                 
        image_dpi=192                                                                                                                
        file='d:/rtf/repeat.rtf' ;                                                                                                   
                                                                                                                                     
    options ls=100 ps=30 orientation=landscape papersize=letter missing=" ";                                                         
    proc report data = havpge(obs=200) missing noWindows split = '|'                                                                 
         style(report) = [width=8in];                                                                                                
      cols (pge StateName (State CountyNm Timezone))                                                                                 
           City Zip;                                                                                                                 
      define pge       / order noprint;                                                                                              
      define statename / display;                                                                                                    
      define state     / display;                                                                                                    
      define countynm  / display;                                                                                                    
      define timezone  / display;                                                                                                    
      define city      / display;                                                                                                    
      define zip       / display;                                                                                                    
      break after pge  / page;                                                                                                       
    run;quit;                                                                                                                        
                                                                                                                                     
    ods rtf close;                                                                                                                   
    ods select _all_;                                                                                                                
                                                                                                                                     
