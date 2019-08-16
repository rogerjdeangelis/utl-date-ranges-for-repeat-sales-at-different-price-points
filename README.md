# utl-date-ranges-for-repeat-sales-at-different-price-points
Date ranges for repeat sales at different price points

    Date ranges for repeat sales at different price points                                                 
                                                                                                           
    github                                                                                                 
    https://tinyurl.com/y3or54yp                                                                           
    https://github.com/rogerjdeangelis/utl-date-ranges-for-repeat-sales-at-different-price-points          
                                                                                                           
    SAS Forum                                                                                              
    https://tinyurl.com/yx8w4nca                                                                           
    https://communities.sas.com/t5/SAS-Programming/slow-proc-sort-and-code/m-p/581671                      
                                                                                                           
    Astounding                                                                                             
    https://communities.sas.com/t5/user/viewprofilepage/user-id/4954                                       
                                                                                                           
    *_                   _                                                                                 
    (_)_ __  _ __  _   _| |_                                                                               
    | | '_ \| '_ \| | | | __|                                                                              
    | | | | | |_) | |_| | |_                                                                               
    |_|_| |_| .__/ \__,_|\__|                                                                              
            |_|                                                                                            
    ;                                                                                                      
                                                                                                           
    data have;                                                                                             
      input product $ date date9.  price;                                                                  
       format date date9.;                                                                                 
    cards4;                                                                                                
    APPLES 01-Jan-18 10                                                                                    
    APPLES 02-Jan-18 10                                                                                    
    APPLES 03-Jan-18 10                                                                                    
    APPLES 04-Jan-18 10                                                                                    
    APPLES 05-Jan-18 10                                                                                    
    APPLES 06-Jan-18 10                                                                                    
    APPLES 07-Jan-18 50                                                                                    
    APPLES 08-Jan-18 11                                                                                    
    APPLES 10-Jan-18 11                                                                                    
    GRAPES 15-Jan-18 15                                                                                    
    GRAPES 16-Jan-17 15                                                                                    
    GRAPES 17-Jan-17 15                                                                                    
    GRAPES 20-Jan-17 15                                                                                    
    GRAPES 21-Jan-17 15                                                                                    
    GRAPES 22-Jan-17 19                                                                                    
    GRAPES 23-Jan-17 19                                                                                    
    GRAPES 24-Jan-17 18                                                                                    
    ;;;;                                                                                                   
    run;quit;                                                                                              
                                                                                                           
                                                                                                           
    WORK.HAVE total obs=17                                                                                 
                                                                                                           
      PRODUCT     DATE   PRICE |  RULES                                                                    
                               |                                                                           
      APPLES   01JAN2018  10   |                                                                           
      APPLES   02JAN2018  10   |                                                                           
      APPLES   03JAN2018  10   |                  START_                NUMBER_  TOTAL_                    
      APPLES   04JAN2018  10   |  PRODUCT PRICE    DATE      END_DATE  OF_SALES  SALES                     
      APPLES   05JAN2018  10   |                                                                           
      APPLES   06JAN2018  10   |  APPLES    10   01-Jan-18   06-Jan-18     6       60                      
                                                                                                           
      APPLES   07JAN2018  50   |  APPLES    50   07JAN2018   07JAN2018     1       50                      
                                                                                                           
      APPLES   08JAN2018  11   |                                                                           
      APPLES   10JAN2018  11   |                                                                           
                                                                                                           
      GRAPES   15JAN2018  15   |                                                                           
      GRAPES   16JAN2017  15   |                                                                           
      GRAPES   17JAN2017  15   |                                                                           
      GRAPES   20JAN2017  15   |                                                                           
      GRAPES   21JAN2017  15   |                                                                           
                                                                                                           
      GRAPES   22JAN2017  19   |                                                                           
      GRAPES   23JAN2017  19   |                                                                           
                                                                                                           
      GRAPES   24JAN2017  18   |                                                                           
                                                                                                           
    *          _               _                                                                           
      ___  _   _| |_ _ __  _   _| |_                                                                       
     / _ \| | | | __| '_ \| | | | __|                                                                      
    | (_) | |_| | |_| |_) | |_| | |_                                                                       
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                      
                    |_|                                                                                    
    ;                                                                                                      
                                                                                                           
    WORK.WANT total obs=6                                                                                  
                                                                                                           
                           NUMBER_     START_                   TOTAL_                                     
      PRODUCT    PRICE    OF_SALES      DATE       END_DATE      SALES                                     
                                                                                                           
      APPLES       10         6       01JAN2018    06JAN2018      60                                       
      APPLES       50         1       07JAN2018    07JAN2018      50                                       
      APPLES       11         2       08JAN2018    10JAN2018      22                                       
      GRAPES       15         5       16JAN2017    15JAN2018      75                                       
      GRAPES       19         2       22JAN2017    23JAN2017      38                                       
      GRAPES       18         1       24JAN2017    24JAN2017      18                                       
                                                                                                           
    *          _       _   _                                                                               
     ___  ___ | |_   _| |_(_) ___  _ __                                                                    
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                   
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                  
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                  
                                                                                                           
    ;                                                                                                      
    proc summary data=have;                                                                                
      by product price notsorted;                                                                          
      var date price;                                                                                      
      output out=want (drop=_t: rename=_freq_=number_of_sales)                                             
        min=start_date max=end_date                                                                        
        sum=_t total_sales;                                                                                
    run;quit;                                                                                              
                                                                                                           
                                                                                                           
