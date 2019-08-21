---
title: API Reference

# language_tabs: # must be one of https://git.io/vQNgJ
#  - shell
#  - ruby
#  - python
#  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

# includes:
#  - errors

search: true
---

#Versions

##Technologies
##Authentication Types
##Response Types
##Policies
##Sources

#DNA

##Search
###QueryObject
###BQL
###FQL

##Analytics
###Article Volume
###Article Volume Time Series Grouped by X

##Archive Extract
###Create
###StatusTest
###Download
###List

##Delta Extract
###CreatebyType
###StatusTest
###Download
###List

##Streamed Extract
###CreateFromArchiveExtract
###CreateFromQuery
###StatusTest
###Subscribe
####Python Listener
####Javascript Listener
###Delete

##Taxonomy



#REST 2.0

##Session
###Login
#### Description

The Login request creates a dedicated user session and returns a key (Session Id) that is required for all further requests. A user may log in to the Dow Jones Web Services by using any of the combinations listed below:

*   UserId+Namespace+Password
    
*   LongUserId+Namespace+Password
    
*   UserId+Namespace+AccountPassword
    
*   LongUserId+Namespace+AccountPassword
    
*   UserId+AccountId+Password
    
*   LongUserId+AccountId+Password
    
*   UserId+AccountId+AccountPassword
    
*   LongUserId+AccountId+AccountPassword
    
*   Email+Password
    
*   Email+AccountPassword
    
*   EncryptedToken
    

#### URL (POST)

**http://**webserver**/api/Public/**version/Session/format

#### XML Payload
```
<SessionRequest>    
  <UserId></UserId>  
  <Password></Password>  
  <Namespace></Namespace>  
  <AccountId></AccountId>  
  <AccountPassword></AccountPassword>  
  <EncryptedToken></EncryptedToken>  
  <LongUserId></LongUserId>  
  <Email></Email>  
  <Parts></Parts>  
  <Timeout></Timeout>  
</SessionRequest>
```

#### Request Parameters
Parameter | Type | Description | Comments
----------|------|-------------|---------
Format | String | Indicates the Format in which the response should be provided.|Valid values are JSON and XML.
UserId|String|A unique identifier for a user.| 
Password|String|Password associated with the UserId.| 
Namespace|String|An abstract container or environment that holds a logical grouping of unique identifiers or user names. A user name defined in a namespace is always identified with the namespace.|For example, user "PeteC" in namespace "24" is logically distinct from "PeteC" in namespace "81". The namespace element enables users to seamlessly reuse their internal user names and databases for logging onto the Dow Jones Web Services.|
AccountId|String|Identifies the account to which the user belongs.| 
AccountPassword|String|Password associated with the user account.| 
EncryptedToken|String|The token that allows a user to automatically log in.| 
LongUserId|String|A LongUserId is an alternate identifier that can be used in place of the UserId.|It can be specified by a user or a client when registering with Dow Jones.| 
Email|String|This element represents a unique address (such as you@yourdomain.com) used to receive and send email to a particular destination (as specified by the user).| 
Parts|string|Parameter used to request for additional information in the response.
| Valid values: 
*   IdleTimeout: The maximum time a session can be idle before the user is automatically logged off.
*   EncryptedToken: An encrypted form of the user authentication that can used for accessing the web service.
*   GetnewEncryptedToken: Re-generates the EncryptedToken and returns the new token.|
Timeout|Integer|The number of minutes that should elapse before the current session automatically expires.|The value should be between 5 and 480.




###Logout
###Perform_Login
###Perform_LogOut

##Encryption
###Get_Encrypted_String

##Entitlements
###Get_Entitlement

##Content
###Factiva Headlines
####Get_Headlines_By_Alert_Id
####Get_Headlines_By_Collection_Code
####Get_Headlines_By_Newsstand_Section_Id
####Get_Headlines_By_Newsstand_Section_Id_and_Search_String
####Get_Headlines_By_Search_String
####Get_Headlines_By_Signal_Id
###Factiva Articles
####Get_Article_By_ArticleRef
####Get_Article_in_PDF
####Get_Article_in_RTF
####Get_Binary_Article
###Newswires Headlines
####Get_Realtime_Headlines_By_Search_String
####Get_Related_Headlines_By_ArticleRef
###Newswires Articles
####Get_Realtime_Article_By_ArticleRef
####Get_Realtime_Linked_Articles_By_ArticleRef



##Taxonomy
###Company
####Get_Company_By_Code
####Get_Company_By_Name_Search
####Get_Company_By_Ticker
###Industry
####Get_Industry_By_Code
####Get_Industry_By_Name_Search
###Subject
####Get_Subject_By_Code
####Get_Subject_By_Name_Search
###Region
####Get_Region_By_Code
####Get_Region_By_Name_Search
###Source
####Get_Source_By_Category
####Get_Source_By_Code
####Get_Source_By_Name_Search
####Get_Extended_Source_By_Name_Search
####Get_PST_Source_By_Code
####Get_PST_Source_By_Search
###Executive
####Get_Executive_By_Code
####Get_Executive_By_Name_Search
###List
####Get_Custom_Source_List
###Codes
####Get_FII_Codes
####Get_Group_Code
###Author
####Get_Author_By_Code
####Get_Author_By_Name
####Get_Author_By_Name_Search

##Chart
####Get_Chart

##Alert
####Create_Alert
####Update_Alert
####Delete_Alert_by_Id
####Subscribe_Alert_by_Id
####Unsubscribe_Alert_by_Id
####Share_Alert
####Unshare_Alert
####Get_Alert_by_Id
####Get_Alerts_by_Product_Type

##Collection

##Managed_List

##Queries

##Newsstand

##Outlet

##Author

##Signal

##
##
##
##
##


#REST 1.0
#SOAP