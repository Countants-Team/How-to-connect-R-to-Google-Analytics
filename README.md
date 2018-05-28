## How-to-connect-R-to-Google-Analytics

#### Step 1) install.packages("googleAuthR")

#### Step 2) install.packages("googleAnalyticsR")

#### Step 3)  ## setup
         library(googleAnalyticsR)
         
#### Step 4) ## authenticate
            ga_auth() 
#### Step 5)  ## get your accounts
        account_list <- google_analytics_account_list()
        
#### Step 6)    ## pick a profile with data to query
      ga_id <- account_list[23,'viewId']
      
  Example:-

     ## create filters on metrics
     mf <- met_filter("bounces", "GREATER_THAN", 0)
     mf2 <- met_filter("sessions", "GREATER", 2)

       ## create filters on dimensions
     df <- dim_filter("source","BEGINS_WITH","1",not = TRUE)
     df2 <- dim_filter("source","BEGINS_WITH","a",not = TRUE)

        ## construct filter objects
     fc2 <- filter_clause_ga4(list(df, df2), operator = "AND")
     fc <- filter_clause_ga4(list(mf, mf2), operator = "AND")

         ## make v4 request
         ## demo showing how the new filters work
      ga_data1 <- google_analytics_4(ga_id, 
                              date_range = c("2015-07-30","2015-10-01"),
                              dimensions=c('source','medium')
                       metrics = c('sessions','bounces'), 
                              met_filters = fc, 
                              dim_filters = fc2, 
                              filtersExpression = "ga:source!=(direct)")

#### Print 
ga_data1


     
