### Alert API

#### Create Alert


##### Description

This transaction creates a news alert.

##### URL (POST)

http://webserver/api/Public/version/Alert/Id/format?SessionId=SessionId&Callback=Callback

##### XML Payload


```xml
<CreateAlertRequest>
	  <Alert>
	    <AlertName></AlertName>
	    <DeduplicationLevel></DeduplicationLevel>
	    <ProductType></ProductType>
	    <DeliveryOptions>
	      <Email></Email>
	      <TimeZone></TimeZone>
	      <MaximumNumberofHeadlinesPerDelivery></MaximumNumberofHeadlinesPerDelivery>
	      <LanguageCode></LanguageCode>
	      <EmailDeliveryContentTypes>
	        <EmailDeliveryContentType></EmailDeliveryContentType>
	        <EmailDeliveryContentType></EmailDeliveryContentType>
	      </EmailDeliveryContentTypes>
	      <DeliveryMethod></DeliveryMethod>
	      <DeliveryTimes></DeliveryTimes>
	      <DocumentType></DocumentType>
	      <SortBy></SortBy>
	      <ResultDisplayFormat></ResultDisplayFormat>
	    </DeliveryOptions>
	    <Contact></Contact>
	    <AlertQuery>
	      <Queries>
	        <Query>
	          <QueryString></QueryString>
	          <SearchMode></SearchMode>
	          <Scope></Scope>
	        </Query>
	        <Query>
	          <QueryString></QueryString>
	          <SearchMode></SearchMode>
	          <Scope></Scope>
	        </Query>
	      </Queries>
	      <SourceGenres>
	        <SourceGenre></SourceGenre>
	        <SourceGenre></SourceGenre>
	      </SourceGenres>
	    </AlertQuery>
	  </Alert>
	</CreateAlertRequest>

```


##### Request Parameters

|    | Parameter                           | Type    | Description                                                                                                                                                                 | Comment                                                                                                                                                                                                                                                                                                        |
|---:|:------------------------------------|:--------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | Format*                             | String  | The format in which the request and response data must be processed.                                                                                                        | Valid formats are XML  and JSON.                                                                                                                                                                                                                                                                               |
|  2 | SessionId/EncryptedToken*           | String  | Credential to identify the logged-in user. This can be either the SessionId received when the current session was created or the Encrypted Tokenfor the user's credentials. | This value can be provided in the Request Header or the Request URL.                                                                                                                                                                                                                                           |
|  3 | Callback                            | String  | JSONP callback function name for cross-domain content requests.                                                                                                             | This parameter is applicable when the data is in JSON format only.                                                                                                                                                                                                                                             |
|  4 | CreateAlertRequest*                 | -       | Container for create alert request payload.                                                                                                                                 | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
|  5 | Alert*                              | -       | Container for alert details.                                                                                                                                                | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
|  6 | AlertName*                          | String  | The name for the alert to create.                                                                                                                                           | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
|  7 | DeduplicationLevel                  | String  | The description of the source list.                                                                                                                                         | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
|  8 | ProductType                         |         | The type of product the alert is about.                                                                                                                                     | Valid values:<li>WealthManagementAlerts<li>InvestmentBankingAlerts<li>WealthManagementTriggers<li>InvestmentBankingTriggers<li>Global<li>WsjProfessional<li>DirectToClient<li>IFF<li>IWE<li>Note: Multiple values can be provided.Separate values using pipe (|) delimiter.<li>**Thisis a payload parameter.** |
|  9 | DeliveryOptions                     | -       | Container for alert's delivery options.                                                                                                                                     | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 10 | Email                               | String  | The email address to which the alert must  be delivered.                                                                                                                    | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 11 | TimeZone                            | String  | The time zone in which the alert is delivered.                                                                                                                              | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 12 | MaximumNumberofHeadlinesPerDelivery | Integer | The maximum number of headlines per alert.                                                                                                                                  | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 13 | LanguageCode                        | String  | The code representing the language of  the alert contents.                                                                                                                  | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 14 | EmailDeliveryContentTypes           | -       | Container for one or more content types  delivered in Email.                                                                                                                | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 15 | EmailDeliveryContentType            | String  | The type of content delivered in the Email.                                                                                                                                 | Valid values:<li>Publications<li>NewsSites<li>**Thisis a payload parameter.**                                                                                                                                                                                                                                  |
| 16 | DeliveryMethod                      | String  | The method in which the alert is delivered.                                                                                                                                 | Valid values:<li>Batch 	 Notifies the user of news pertaining to their interests 	 and holdings through Email at a specific time of day. 	 The time period is defined in the DeliveryTimes 	 parameter.<li>Continuous. 	 Notifies the user of news pertaining to their interests 	 and holdings 24 hours/day, 7 days/week. The user receives 	 the news as soon as it becomes available.<li>Online<li>**Thisis a payload parameter.**                                                                                                                                                                                                                                                                                                                |
| 17 | DeliveryTimes                       | String  | Indicates the time at which the alert  is delivered.                                                                                                                        | Note:  This parameter is applicable only when DeliveryMethod=Batch.<li>Valid values:<li>EarlyMorning<li>Morning<li>Afternoon<li>Both (Morning 	 and Afternoon)<li>Continuous<li>None<li>**Thisis a payload parameter.**                                                                                                                                                                                                                                                                                                                |
| 18 | DocumentType                        | String  | The type of document delivered in the  alert.                                                                                                                               | Valid values:<li>SNIP 	 - Article snippet<li>FULL 	 - Full article<li>FULR 	 - Full article and 	 indexing<li>HDLN 	 - Headline<li>**Thisis a payload parameter.**                                                                                                                                                                                                                                                                                                                |
| 19 | SortBy                              | String  | The parameter by which the results must be sorted.                                                                                                                          | Valid values:<li>Date<li>Relevance<li>ClipTime<li>EventType<li>**Thisis a payload parameter.**                                                                                                                                                                                                                 |
| 20 | ResultDisplayFormat                 | String  | The format in which the alert is delivered.                                                                                                                                 | Valid values:<li>PlainText<li>PlainTextAttachment<li>HTML<li>HTMLAttachment<li>Mobile<li>**Thisis a payload parameter.**                                                                                                                                                                                       |
| 21 | Contact                             | String  | The contact person for the alert.                                                                                                                                           | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 22 | AlertQuery                          | -       | Container for one or more query components  that determine the alert contents.                                                                                              | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 23 | Queries                             | -       | Container for one or more queries.                                                                                                                                          | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 24 | Query                               | -       | Container for a query.                                                                                                                                                      | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 25 | QueryString                         | String  | The query string that is used to search  the news for alert contents.                                                                                                       | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 26 | SearchMode                          | String  | Indicates how the search query will be  interpreted.                                                                                                                        | Valid values:<li>Simple 	 Search<li>Traditional 	 Search<li>Note:  Click a search mode for details on how to construct the querystring.<li>**Thisis a payload parameter.**                                                                                                                                                                                                                                                                                                                |
| 27 | Scope                               | String  | The scope of the query.                                                                                                                                                     | Valid values:<li>About<li>Occur<li>None<li>**Thisis a payload parameter.**                                                                                                                                                                                                                                     |
| 28 | SourceGenres                        | -       | Container for source genres to search.                                                                                                                                      | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 29 | SourceGenre                         | String  | Represents the content group to search.                                                                                                                                     | Possible values:<li>Publications<li>NewsSites<li>Blogs<li>**Thisis a payload parameter.**                                                                                                                                                                                                                      |

##### Response Tags

|    | Parameter           | Type    | Description                               | Comment   |
|---:|:--------------------|:--------|:------------------------------------------|:----------|
|  1 | CreateAlertResponse | -       | The top-level response container.         |           |
|  2 | AlertId             | Integer | The Alert Id for the newly created alert. |           |

##### XML Payload


```xml
<CreateAlertResponse>
	  <Message></Message>
	</CreateAlertResponse>

```

 

##### URL (POST)

http://api.beta.dowjones.com/api/Public/2.0/Alert/xml?sessionId=YourSessionId

##### Request


```xml
<CreateAlertRequest>
	  <Alert>
	    <AlertName>createAlert_test12</AlertName>
	    <DeduplicationLevel>Off</DeduplicationLevel>
	    <ProductType>Global</ProductType>
	    <DeliveryOptions>
	      <Email>dowjonesinc@gmail.com</Email>
	      <TimeZone>+4:30</TimeZone>
	      <MaximumNumberofHeadlinesPerDelivery>10</MaximumNumberofHeadlinesPerDelivery>
	      <LanguageCode>en</LanguageCode>
	      <EmailDeliveryContentTypes>
	        <EmailDeliveryContentType>
	        publication</EmailDeliveryContentType>
	      </EmailDeliveryContentTypes>
	      <DeliveryMethod>Batch</DeliveryMethod>
	      <DeliveryTimes>Afternoon</DeliveryTimes>
	      <DocumentType>FULL</DocumentType>
	      <SortBy>Date</SortBy>
	      <ResultDisplayFormat>Plaintext</ResultDisplayFormat>
	    </DeliveryOptions>
	    <AlertQuery>
	      <Queries>
	        <Query>
	          <QueryString>a</QueryString>
	          <SearchMode>simple</SearchMode>
	        </Query>
	      </Queries>
	      <SourceGenres>
	        <SourceGenre>publications</SourceGenre>
	      </SourceGenres>
	    </AlertQuery>
	  </Alert>
	</CreateAlertRequest>

```


##### Response


```xml
<CreateAlertResponse>
		  <AlertId>27845254</AlertId>
		</CreateAlertResponse>

```


##### URL (POST)

http://api.beta.dowjones.com/api/Public/2.0/Alert/json?sessionId=YourSessionId

##### Request


```json
{
	    "Alert":
	    {
	        "AlertName":"testing1219",
	        "DeduplicationLevel":"Off",
	        "DeliveryOptions": 
	 
	        {
	            "Email": 
	 "user@domain.com",
	            "TimeZone": 
	 "+4:30",
	            "MaximumNumberofHeadlinesPerDelivery": 
	 "10",
	            "LanguageCode": 
	 "en",
	            "EmailDeliveryContentTypes": 
	 
	            {
	                "EmailDeliveryContentType": 
	 "publication"
	            },
	            "DeliveryMethod": 
	 "Batch",
	            "DeliveryTimes": 
	 "Afternoon",
	            "DocumentType": 
	 "FULL",
	            "SortBy": 
	 "Date",
	            "ResultDisplayFormat": 
	 "Plaintext"
	         },
	        "AlertQuery":
	        {
	            "Queries":
	            [{
	            "QueryString":"fds=APPLC 
	 and Watch",
	            "SearchMode":"simple"
	            }],
	            "SourceGenres": 
	 { "SourceGenre": "publications" }
	        },
	        "ProductType" 
	 : "Global"
	    }
	}

```


##### Response


```json
{
		    "AlertId":301672344
		}

```

 
#### Update Alert


##### Description

This transaction updates a news alert.

##### URL (PUT)

http://webserver/api/Public/version/Alert/format?SessionId=SessionId&Callback=Callback

##### XML Payload


```xml
<UpdateAlertRequest>
	  <Alert>
	    <AlertId></AlertId>
	    <AlertName></AlertName>
	    <DeduplicationLevel></DeduplicationLevel>
	    <ProductType></ProductType>
	    <DeliveryOptions>
	      <Email></Email>
	      <TimeZone></TimeZone>
	      <MaximumNumberofHeadlinesPerDelivery></MaximumNumberofHeadlinesPerDelivery>
	      <LanguageCode></LanguageCode>
	      <EmailDeliveryContentTypes>
	        <EmailDeliveryContentType></EmailDeliveryContentType>
	        <EmailDeliveryContentType></EmailDeliveryContentType>
	      </EmailDeliveryContentTypes>
	      <DeliveryMethod></DeliveryMethod>
	      <DeliveryTimes></DeliveryTimes>
	      <DocumentType></DocumentType>
	      <SortBy></SortBy>
	      <ResultDisplayFormat></ResultDisplayFormat>
	    </DeliveryOptions>
	    <Contact></Contact>
	    <AlertQuery>
	      <Queries>
	        <Query>
	          <QueryString></QueryString>
	          <SearchMode></SearchMode>
	          <Scope></Scope>
	        </Query>
	        <Query>
	          <QueryString></QueryString>
	          <SearchMode></SearchMode>
	          <Scope></Scope>
	        </Query>
	      </Queries>
	      <SourceGenres>
	        <SourceGenre></SourceGenre>
	        <SourceGenre></SourceGenre>
	      </SourceGenres>
	    </AlertQuery>
	  </Alert>
	</UpdateAlertRequest>

```


##### Request Parameters

|    | Parameter                           | Type    | Description                                                                                                                                                                 | Comment                                                                                                                                                                                                                                                                                                        |
|---:|:------------------------------------|:--------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | Format*                             | String  | The format in which the request and response data must be processed.                                                                                                        | Valid formats are XML  and JSON.                                                                                                                                                                                                                                                                               |
|  2 | SessionId/EncryptedToken*           | String  | Credential to identify the logged-in user. This can be either the SessionId received when the current session was created or the Encrypted Tokenfor the user's credentials. | This value can be provided in the Request Header or the Request URL.                                                                                                                                                                                                                                           |
|  3 | Callback                            | String  | JSONP callback function name for cross-domain content requests.                                                                                                             | This parameter is applicable when the data is in JSON format only.                                                                                                                                                                                                                                             |
|  4 | UpdateAlertRequest*                 | -       | Container for create alert request payload.                                                                                                                                 | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
|  5 | Alert*                              | -       | Container for alert details.                                                                                                                                                | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
|  6 | AlertId                             | Integer |                                                                                                                                                                             |                                                                                                                                                                                                                                                                                                                |
|  7 | AlertName*                          | String  | The name for the alert to create.                                                                                                                                           | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
|  8 | DeduplicationLevel                  | String  | The description of the source list.                                                                                                                                         | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
|  9 | ProductType                         |         | The type of product the alert is about.                                                                                                                                     | Valid values:<li>WealthManagementAlerts<li>InvestmentBankingAlerts<li>WealthManagementTriggers<li>InvestmentBankingTriggers<li>Global<li>WsjProfessional<li>DirectToClient<li>IFF<li>IWE<li>Note: Multiple values can be provided.Separate values using pipe (|) delimiter.<li>**Thisis a payload parameter.** |
| 10 | DeliveryOptions                     | -       | Container for alert's delivery options.                                                                                                                                     | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 11 | Email                               | String  | The email address to which the alert must  be delivered.                                                                                                                    | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 12 | TimeZone                            | String  | The time zone in which the alert is delivered.                                                                                                                              | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 13 | MaximumNumberofHeadlinesPerDelivery | Integer | The maximum number of headlines per alert.                                                                                                                                  | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 14 | LanguageCode                        | String  | The code representing the language of  the alert contents.                                                                                                                  | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 15 | EmailDeliveryContentTypes           | -       | Container for one or more content types  delivered in Email.                                                                                                                | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 16 | EmailDeliveryContentType            | String  | The type of content delivered in the Email.                                                                                                                                 | Valid values:<li>Publications<li>NewsSites<li>Blogs<li>**Thisis a payload parameter.**                                                                                                                                                                                                                         |
| 17 | DeliveryMethod                      | String  | The method in which the alert is delivered.                                                                                                                                 | Valid values:<li>Batch 	 Notifies the user of news pertaining to their interests 	 and holdings through Email at a specific time of day. 	 The time period is defined in the DeliveryTimes 	 parameter.<li>Continuous. 	 Notifies the user of news pertaining to their interests 	 and holdings 24 hours/day, 7 days/week. The user receives 	 the news as soon as it becomes available.<li>Online<li>**Thisis a payload parameter.**                                                                                                                                                                                                                                                                                                                |
| 18 | DeliveryTimes                       | String  | Indicates the time at which the alert  is delivered.                                                                                                                        | Note:  This parameter is applicable only when DeliveryMethod=Batch.<li>Valid values:<li>EarlyMorning<li>Morning<li>Afternoon<li>Both (Morning 	 and Afternoon)<li>Continuous<li>None<li>**Thisis a payload parameter.**                                                                                                                                                                                                                                                                                                                |
| 19 | DocumentType                        | String  | The type of document delivered in the  alert.                                                                                                                               | Valid values:<li>SNIP 	 - Article snippet<li>FULL 	 - Full article<li>FULR 	 - Full article and 	 indexing<li>HDLN 	 - Headline<li>**Thisis a payload parameter.**                                                                                                                                                                                                                                                                                                                |
| 20 | SortBy                              | String  | The parameter by which the results must be sorted.                                                                                                                          | Valid values:<li>Date<li>Relevance<li>ClipTime<li>EventType<li>**Thisis a payload parameter.**                                                                                                                                                                                                                 |
| 21 | ResultDisplayFormat                 | String  | The format in which the alert is delivered.                                                                                                                                 | Valid values:<li>PlainText<li>PlainTextAttachment<li>HTML<li>HTMLAttachment<li>Mobile<li>**Thisis a payload parameter.**                                                                                                                                                                                       |
| 22 | Contact                             | String  | The contact person for the alert.                                                                                                                                           | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 23 | AlertQuery                          | -       | Container for one or more query components  that determine the alert contents.                                                                                              | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 24 | Queries                             | -       | Container for one or more queries.                                                                                                                                          | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 25 | Query                               | -       | Container for a query.                                                                                                                                                      | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 26 | QueryString                         | String  | The query string that is used to search  the news for alert contents.                                                                                                       | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 27 | SearchMode                          | String  | Indicates how the search query will be  interpreted.                                                                                                                        | Valid values:<li>Simple 	 Search<li>Traditional 	 Search<li>Note:  Click a search mode for details on how to construct the querystring.<li>**Thisis a payload parameter.**                                                                                                                                                                                                                                                                                                                |
| 28 | Scope                               | String  | The scope of the query.                                                                                                                                                     | Valid values:<li>About<li>Occur<li>None<li>**Thisis a payload parameter.**                                                                                                                                                                                                                                     |
| 29 | SourceGenres                        | -       | Container for source genres to search.                                                                                                                                      | **Thisis a payload parameter.**                                                                                                                                                                                                                                                                                |
| 30 | SourceGenre                         | String  | Represents the content group to search.                                                                                                                                     | Possible values:<li>Publications<li>NewsSites<li>Blogs<li>**Thisis a payload parameter.**                                                                                                                                                                                                                      |

##### Response Tags

|    | Parameter           | Type   | Description                                               | Comment                                                     |
|---:|:--------------------|:-------|:----------------------------------------------------------|:------------------------------------------------------------|
|  1 | UpdateAlertResponse | -      | The top-level response container.                         |                                                             |
|  2 | Message             | String | Message indicating the result of the requested operation. | Valid values are True (successful)and False (unsuccessful). |

##### XML Payload


```xml
<UpdateAlertResponse>
	  <Message></Message>
	</UpdateAlertResponse>

```

 

##### URL (PUT)

http://api.beta.dowjones.com/api/Public/2.0/Alert/xml?sessionId=YourSessionId

##### Request


```xml
<UpdateAlertRequest>
	  <Alert>
	    <AlertId>300279626</AlertId>
	    <AlertName>createAlert_101test</AlertName>
	    <DeduplicationLevel>Off</DeduplicationLevel>
	    <ProductType>Global</ProductType>
	    <DeliveryOptions>
	      <Email>dowjonesinc@gmail.com</Email>
	      <TimeZone>+4:30</TimeZone>
	      <MaximumNumberofHeadlinesPerDelivery>10</MaximumNumberofHeadlinesPerDelivery>
	      <LanguageCode>en</LanguageCode>
	      <EmailDeliveryContentTypes>
	        <EmailDeliveryContentType>publication</EmailDeliveryContentType>
	      </EmailDeliveryContentTypes>
	      <DeliveryMethod>Batch</DeliveryMethod>
	      <DeliveryTimes>Afternoon</DeliveryTimes>
	      <DocumentType>FULL</DocumentType>
	      <SortBy>Date</SortBy>
	      <ResultDisplayFormat>Plaintext</ResultDisplayFormat>
	    </DeliveryOptions>
	    <AlertQuery>
	      <Queries>
	        <Query>
	          <QueryString>a</QueryString>
	          <SearchMode>simple</SearchMode>
	        </Query>
	      </Queries>
	      <SourceGenres>
	        <SourceGenre>publications</SourceGenre>
	      </SourceGenres>
	    </AlertQuery>
	  </Alert>
	</UpdateAlertRequest>

```


##### Response


```xml
<UpdateAlertResponse>
		  <Message>True</Message>
		</UpdateAlertResponse>

```


##### URL (PUT)

http://api.beta.dowjones.com/api/Public/2.0/Alert/json?sessionId=YourSessionId

##### Request


```json
{
	    "Alert": {
	        "AlertId": 
	 "301669213",
	        "AlertName": 
	 "test123",
	        "DeduplicationLevel": 
	 "Off",
	        "ProductType": 
	 "Global",
	        "DeliveryOptions": 
	 {
	            "Email": 
	 "user@domain.com",
	            "TimeZone": 
	 "+4:30",
	            "MaximumNumberofHeadlinesPerDelivery": 
	 "10",
	            "LanguageCode": 
	 "en",
	            "EmailDeliveryContentTypes": 
	 {
	                "EmailDeliveryContentType": 
	 "Publication"
	            },
	            "DeliveryMethod": 
	 "Online",
	            "DeliveryTimes": 
	 "Afternoon",
	            "DocumentType": 
	 "FULL",
	            "SortBy": 
	 "Date",
	            "ResultDisplayFormat": 
	 "Plaintext"
	        },
	        "AlertQuery": 
	 {
	            "Queries": 
	 [
	                {
	                    "QueryString": 
	 "fds=APPLC or Watch",
	                    "SearchMode": 
	 "traditional"
	                }
	            ],
	            "SourceGenres": 
	 [
	                "Publications"
	            ]
	        }
	    }
	}

```


##### Response


```json
{
		    Message: "true"
		}

```

 
#### Get Alerts by Product Type


##### Description

This transaction retrieves alert information by Product Type.

##### URL (GET)

http://webserver/api/Public/version/Alert/list/format?SessionId=SessionId&Callback=Callback&ProductType=ProductType&Parts=Parts

##### Request Parameters

|    | Parameter                 | Type   | Description                                                                                                                                                                                           | Comment                                                                                                                  |
|---:|:--------------------------|:-------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------|
|  1 | Format*                   | String | The format in which the request and response data must be processed.                                                                                                                                  | Valid formats are XML  and JSON.                                                                                         |
|  2 | SessionId/EncryptedToken* | String | Credential to identify the logged-in user. This can be either the SessionId received when the current session was created or the Encrypted Tokenfor the user's credentials.                           | This value can be provided in the Request Header or the Request URL.                                                     |
|  3 | Callback                  | String | JSONP callback function name for cross-domain content requests.                                                                                                                                       | This parameter is applicable when the data is in JSON format only.                                                       |
|  4 | ProductType*              | String | The type of product the alert is about.                                                                                                                                                               | Valid values:<li>Global<li>IFF<li>IWE<li>Note: Multiple values can be provided.Separate values using pipe (|) delimiter. |
|  5 | Parts                     | String | Parameter to request additional information  in the response.                                                                                                                                         | Valid values:<li>RssUrl - Returns 	 a link to the alert's RSS feed.<li>GroupAlerts - 	 Returns subscribed and assigned group alerts<li>Subscribed - Returns 	 subscribed group alerts<li>Assigned - Returns 	 assigned group alerts<li>PersonalSubscribed - Returns 	 subscribed personal alerts<li>DeDuplicationLevel - 	 Returns duplicate alerts as specified in the DeDuplicationLevel 	 parameter.<li>By default no additional parts are returned.                                                                                                                          |
|  6 | DeDuplicationLevel        | String | Indicates how duplicate records must be  handled.<li>Note:  When the DeDuplicationLevel is Similar  or NearExact, the  request must use  the offset from the previous response for proper pagination. |                                                                                                                          |
|    | Parameter                 | Type   | Description                                                                                                                                                                                           | Comment                                                                                                                  |
|---:|:--------------------------|:-------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------|
|  1 | Format*                   | String | The format in which the request and response data must be processed.                                                                                                                                  | Valid formats are XML  and JSON.                                                                                         |
|  2 | SessionId/EncryptedToken* | String | Credential to identify the logged-in user. This can be either the SessionId received when the current session was created or the Encrypted Tokenfor the user's credentials.                           | This value can be provided in the Request Header or the Request URL.                                                     |
|  3 | Callback                  | String | JSONP callback function name for cross-domain content requests.                                                                                                                                       | This parameter is applicable when the data is in JSON format only.                                                       |
|  4 | ProductType*              | String | The type of product the alert is about.                                                                                                                                                               | Valid values:<li>Global<li>IFF<li>IWE<li>Note: Multiple values can be provided.Separate values using pipe (|) delimiter. |
|  5 | Parts                     | String | Parameter to request additional information  in the response.                                                                                                                                         | Valid values:<li>RssUrl - Returns 	 a link to the alert's RSS feed.<li>GroupAlerts - 	 Returns subscribed and assigned group alerts<li>Subscribed - Returns 	 subscribed group alerts<li>Assigned - Returns 	 assigned group alerts<li>PersonalSubscribed - Returns 	 subscribed personal alerts<li>DeDuplicationLevel - 	 Returns duplicate alerts as specified in the DeDuplicationLevel 	 parameter.<li>By default no additional parts are returned.                                                                                                                          |
|  6 | DeDuplicationLevel        | String | Indicates how duplicate records must be  handled.<li>Note:  When the DeDuplicationLevel is Similar  or NearExact, the  request must use  the offset from the previous response for proper pagination. |                                                                                                                          |

##### Response Tags

|    | Parameter                    | Type    | Description                                                                                                                                          | Comment                                                                               |
|---:|:-----------------------------|:--------|:-----------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------|
|  1 | AlertResponse                | -       | The top-level response container.                                                                                                                    |                                                                                       |
|  2 | Records                      | Integer | The number of records returned in this response.                                                                                                     |                                                                                       |
|  3 | TotalRecords                 | Integer | The total number of records that matched the request.                                                                                                |                                                                                       |
|  4 | AlertDetails                 | -       | Container for one or more alerts.                                                                                                                    |                                                                                       |
|  5 | AlertDetail                  | -       | Container for alert details.                                                                                                                         |                                                                                       |
|  6 | AlertId                      | Integer | The unique identifier for the alert.                                                                                                                 |                                                                                       |
|  7 | AlertName                    | String  | The name of the alert.                                                                                                                               | This parameter is case sensitive.                                                     |
|  8 | DeduplicationLevel           | String  | Deduplication  applied to the alert contents.                                                                                                        | Valid  values:<li>Off<li>Similar<li>VirtuallyIdentical                                |
|  9 | DeliveryOptions              | -       | Container for alert's delivery settings.                                                                                                             |                                                                                       |
| 10 | Email                        | String  | The email address to which the alert is  delivered.                                                                                                  |                                                                                       |
| 11 | LanguageCode                 | String  | The code representing the language of  the alert contents.                                                                                           |                                                                                       |
| 12 | TimeZone                     | String  | The time zone in which the alert is delivered.                                                                                                       |                                                                                       |
| 13 | DeliveryMethod               | String  | The method in which the alert is delivered.                                                                                                          | Valid values:<li>Batch 	 Notifies the user of news pertaining to their interests 	 and holdings through Email at a specific time of day. 	 The time period is defined in the DeliveryTimes 	 parameter.<li>Continuous. 	 Notifies the user of news pertaining to their interests 	 and holdings 24 hours/day, 7 days/week. The user receives 	 the news as soon as it becomes available.<li>Online                                                                                       |
| 14 | DeliveryTimes                | String  | Indicates the time at which the email  is delivered.                                                                                                 | Note:  This parameter is applicable only when DeliveryMethod=Batch.<li>Valid values:<li>EarlyMorning<li>Morning<li>Afternoon<li>Both (Morning 	 and Afternoon)<li>Continuous<li>None                                                                                       |
| 15 | DocumentType                 | String  | The type of document delivered in the  alert.                                                                                                        | Valid values:<li>SNIP 	 - Article snippet<li>FULL 	 - Full article<li>FULR 	 - Full article and 	 indexing<li>HDLN 	 - Headline                                                                                       |
| 16 | EmailDeliveryContentTypes    | -       | Container for one or more content types  delivered in Email.                                                                                         |                                                                                       |
| 17 | EmailDeliveryContentType     | String  | The type of content delivered in the Email.                                                                                                          | Valid values:<li>Publications<li>NewsSites                                            |
| 18 | ResultDisplayFormat          | String  | The format in which the alert is delivered.                                                                                                          | Valid values:<li>PlainText<li>PlainTextAttachment<li>HTML<li>HTMLAttachment<li>Mobile |
| 19 | SortBy                       | String  | The parameter by which the results must be sorted.                                                                                                   | Valid values:<li>Date<li>Relevance<li>ClipTime<li>EventType                           |
| 20 | IsGroupAlert                 | Boolean | Indicates if this is a group alert.                                                                                                                  | Valid values are True and False.                                                      |
| 21 | OwnershipType                | String  | Indicates the ownership of the alert.                                                                                                                |                                                                                       |
| 22 | PrivateRSSLink/PublicRSSLink | String  | A URL that links to the alert's RSS feed.<li>Note:  PrivateRSSLink is returned for personal alerts and PublicRSSLink  is returned for shared alerts. | Note:  This value is returned only if Parts=RssUrl in the request.                    |
| 23 | ProductType                  | String  | The type of product the alert is about.                                                                                                              | Valid values:<li>Global<li>IFF<li>IWE                                                 |
| 24 | NewHits                      | Boolean | Indicates whether the alert contains new  headlines.                                                                                                 | Valid values are True and False.                                                      |

##### XML Payload


```xml
<AlertResponse>
	  <AlertDetails>
	    <AlertDetail>
	      <AlertId></AlertId>
	      <AlertName></AlertName>
	      <DeliveryOptions>
	        <Email></Email>
	        <LanguageCode></LanguageCode>
	        <MaximumNumberofHeadlinesPerDelivery></MaximumNumberofHeadlinesPerDelivery>
	        <TimeZone></TimeZone>
	       <DeDuplicationLevel></DeduplicationLevel>
	        <DeliveryMethod></DeliveryMethod>
	        <DeliveryTimes></DeliveryTimes>
	        <DocumentType></DocumentType>
	        <EmailDeliveryContentTypes>
	          <EmailDeliveryContentType></EmailDeliveryContentType>
	          <EmailDeliveryContentType></EmailDeliveryContentType>
	        </EmailDeliveryContentTypes>
	        <ResultDisplayFormat></ResultDisplayFormat>
	        <SortBy></SortBy>
	      </DeliveryOptions>
	      <IsGroupAlert></IsGroupAlert>
	      <OwnershipType></OwnershipType>
	      <PrivateRSSLink></PrivateRSSLink>
	      <ProductType></ProductType>
	      <PublicRSSLink></PublicRSSLink>
	      <NewHits></NewHits>
	    </AlertDetail>
	    ...
	  </AlertDetails>
	</AlertResponse>

```


#####  

http://api.beta.dowjones.com/api/Public/2.0/Alert/list/xml?productType=investmentbankingalerts&parts=rssurl&sessionId=YourSessionId

```xml
<AlertResponse>
	  <Records>2</Records>
	  <TotalRecords>2</TotalRecords>
	  <AlertDetails>
	    <AlertDetail>
	      <AlertId>300271887</AlertId>
	      <AlertName>1719_test</AlertName>
	      <DeliveryOptions>
	        <Email>naresh@naresh1.com</Email>
	        <DeliveryMethod>Online</DeliveryMethod>
	        <DeliveryTimes>Morning</DeliveryTimes>
	      </DeliveryOptions>
	      <IsGroupAlert>false</IsGroupAlert>
	      <OwnershipType>Personal</OwnershipType>
	      <PrivateRSSLink>      http://rss.int.factiva.com/headlines.aspx?folderid=300271887&amp;EID3=XqTZ%2fV5fX6pvwJzlx2RJKvbKODY7fGMZIowAsacNfzvjdnMpu44J03MFzZu4RU652mu7ghkMnY9BhUYcoP%2fWYyKoFzVm6Z3FvYc86KrKShQvtlkO57o8J8vKcrwg86DEVG1OmvAPNru1fn0MiaLZ6e4iECja37Tx2DBitb%2fR6DpQ8MObdP7syk6gYMMRFPsvjACWRo2ueYlS90Y3D86ypkS8Dgu6azTE2csb3StPQNTip6mFbVYDlWnV0GjHsJ1r7Fr57J4mi%2ffc430vb1PrdhZ47SNeTNbvobGCkM9Kxjp1h6CM9wNJUIYUCixG0UeA5ycME1r5kgM%3d%7c2</PrivateRSSLink>
	      <ProductType>IFF</ProductType>
	      <NewHits>true</NewHits>
	    </AlertDetail>
	    <AlertDetail>
	      <AlertId>300271343</AlertId>
	      <AlertName>a_twst</AlertName>
	      <DeliveryOptions>
	        <Email>new1@new.com</Email>
	        <TimeZone>-05:00|1</TimeZone>
	        <DeliveryMethod>Batch</DeliveryMethod>
	        <DeliveryTimes>Both</DeliveryTimes>
	      </DeliveryOptions>
	      <IsGroupAlert>false</IsGroupAlert>
	      <OwnershipType>Personal</OwnershipType>
	      <PrivateRSSLink>      http://rss.int.factiva.com/headlines.aspx?folderid=300271343&amp;EID3=XqTZ%2fV5fX6pvwJzlx2RJKvbKODY7fGMZIowAsacNfzvjdnMpu44J03MFzZu4RU652mu7ghkMnY9BhUYcoP%2fWYyKoFzVm6Z3FvYc86KrKShRY7vfCUZ73JTYMBcpGF%2bm646zrokgh0V8j3fm2TlDpXGKypeaIDqIpvPKIAP7xRYVz9xaN3e376eZ%2b7w23yPzEVU2CzuMjoS7diKj7ei4ci8kcHU%2fJ%2b4FMz9CatOzhiv58HF9YJzZLL4X75l91eupTJ7Kv4GWmMkiBtD38mkAl3RQFAp2Xr9IApwK91CTE0XziX4vj3JW9ZojHPtphKZbO%7c2</PrivateRSSLink>
	      <ProductType>IFF</ProductType>
	      <NewHits>true</NewHits>
	    </AlertDetail>
	  </AlertDetails>
	</AlertResponse>

```

http://api.beta.dowjones.com/api/Public/2.0/Alert/list/json?productType=investmentbankingalerts&parts=rssurl&sessionId=YourSessionId

```json
{
	    "Records": 2,
	    "TotalRecords": 2,
	    "AlertDetails": [
	        {
	            "AlertId": 
	 300271887,
	            "AlertName": 
	 "1719_test",
	            "DeliveryOptions": 
	 {
	                "Email": 
	 "naresh@naresh1.com",
	                "DeliveryMethod": 
	 "Online",
	                "DeliveryTimes": 
	 "Morning"
	            },
	            "IsGroupAlert": 
	 false,
	            "OwnershipType": 
	 "Personal",
	            "PrivateRSSLink": 
	 "http://rss.int.factiva.com/headlines.aspx?folderid=300271887&EID3=XqTZ%2fV5fX6pvwJzlx2RJKvbKODY7fGMZIowAsacNfzvjdnMpu44J03MFzZu4RU652mu7ghkMnY9BhUYcoP%2fWYyKoFzVm6Z3FvYc86KrKShQvtlkO57o8J8vKcrwg86DEVG1OmvAPNru1fn0MiaLZ6e4iECja37Tx2DBitb%2fR6DpQ8MObdP7syk6gYMMRFPsvjACWRo2ueYlS90Y3D86ypkS8Dgu6azTE2csb3StPQNTip6mFbVYDlWnV0GjHsJ1r7Fr57J4mi%2ffc430vb1PrdhZ47SNeTNbvobGCkM9Kxjp1h6CM9wNJUIYUCixG0UeA5ycME1r5kgM%3d%7c2",
	            "ProductType": 
	 "IFF",
	            "NewHits": 
	 true
	        },
	        {
	            "AlertId": 
	 300271343,
	            "AlertName": 
	 "a_twst",
	            "DeliveryOptions": 
	 {
	                "Email": 
	 "new1@new.com",
	                "TimeZone": 
	 "-05:00|1",
	                "DeliveryMethod": 
	 "Batch",
	                "DeliveryTimes": 
	 "Both"
	            },
	            "IsGroupAlert": 
	 false,
	            "OwnershipType": 
	 "Personal",
	            "PrivateRSSLink": 
	 "http://rss.int.factiva.com/headlines.aspx?folderid=300271343&EID3=XqTZ%2fV5fX6pvwJzlx2RJKvbKODY7fGMZIowAsacNfzvjdnMpu44J03MFzZu4RU652mu7ghkMnY9BhUYcoP%2fWYyKoFzVm6Z3FvYc86KrKShRY7vfCUZ73JTYMBcpGF%2bm646zrokgh0V8j3fm2TlDpXGKypeaIDqIpvPKIAP7xRYVz9xaN3e376eZ%2b7w23yPzEVU2CzuMjoS7diKj7ei4ci8kcHU%2fJ%2b4FMz9CatOzhiv58HF9YJzZLL4X75l91eupTJ7Kv4GWmMkiBtD38mkAl3RQFAp2Xr9IApwK91CTE0XziX4vj3JW9ZojHPtphKZbO%7c2",
	            "ProductType": 
	 "IFF",
	            "NewHits": 
	 true
	        }
	    ]
	}

```

 

##### URL (GET)

http://api.beta.dowjones.com/api/Public/2.0/Alert/list/xml?productType=investmentbankingalerts&parts=rssurl&sessionId=YourSessionId

##### Response


```xml
<AlertResponse>
	  <Records>2</Records>
	  <TotalRecords>2</TotalRecords>
	  <AlertDetails>
	    <AlertDetail>
	      <AlertId>300271887</AlertId>
	      <AlertName>1719_test</AlertName>
	      <DeliveryOptions>
	        <Email>naresh@naresh1.com</Email>
	        <DeliveryMethod>Online</DeliveryMethod>
	        <DeliveryTimes>Morning</DeliveryTimes>
	      </DeliveryOptions>
	      <IsGroupAlert>false</IsGroupAlert>
	      <OwnershipType>Personal</OwnershipType>
	      <PrivateRSSLink>      http://rss.int.factiva.com/headlines.aspx?folderid=300271887&amp;EID3=XqTZ%2fV5fX6pvwJzlx2RJKvbKODY7fGMZIowAsacNfzvjdnMpu44J03MFzZu4RU652mu7ghkMnY9BhUYcoP%2fWYyKoFzVm6Z3FvYc86KrKShQvtlkO57o8J8vKcrwg86DEVG1OmvAPNru1fn0MiaLZ6e4iECja37Tx2DBitb%2fR6DpQ8MObdP7syk6gYMMRFPsvjACWRo2ueYlS90Y3D86ypkS8Dgu6azTE2csb3StPQNTip6mFbVYDlWnV0GjHsJ1r7Fr57J4mi%2ffc430vb1PrdhZ47SNeTNbvobGCkM9Kxjp1h6CM9wNJUIYUCixG0UeA5ycME1r5kgM%3d%7c2</PrivateRSSLink>
	      <ProductType>IFF</ProductType>
	      <NewHits>true</NewHits>
	    </AlertDetail>
	    <AlertDetail>
	      <AlertId>300271343</AlertId>
	      <AlertName>a_twst</AlertName>
	      <DeliveryOptions>
	        <Email>new1@new.com</Email>
	        <TimeZone>-05:00|1</TimeZone>
	        <DeliveryMethod>Batch</DeliveryMethod>
	        <DeliveryTimes>Both</DeliveryTimes>
	      </DeliveryOptions>
	      <IsGroupAlert>false</IsGroupAlert>
	      <OwnershipType>Personal</OwnershipType>
	      <PrivateRSSLink>      http://rss.int.factiva.com/headlines.aspx?folderid=300271343&amp;EID3=XqTZ%2fV5fX6pvwJzlx2RJKvbKODY7fGMZIowAsacNfzvjdnMpu44J03MFzZu4RU652mu7ghkMnY9BhUYcoP%2fWYyKoFzVm6Z3FvYc86KrKShRY7vfCUZ73JTYMBcpGF%2bm646zrokgh0V8j3fm2TlDpXGKypeaIDqIpvPKIAP7xRYVz9xaN3e376eZ%2b7w23yPzEVU2CzuMjoS7diKj7ei4ci8kcHU%2fJ%2b4FMz9CatOzhiv58HF9YJzZLL4X75l91eupTJ7Kv4GWmMkiBtD38mkAl3RQFAp2Xr9IApwK91CTE0XziX4vj3JW9ZojHPtphKZbO%7c2</PrivateRSSLink>
	      <ProductType>IFF</ProductType>
	      <NewHits>true</NewHits>
	    </AlertDetail>
	  </AlertDetails>
	</AlertResponse>

```


##### URL (GET)

http://api.beta.dowjones.com/api/Public/2.0/Alert/list/json?productType=investmentbankingalerts&parts=rssurl&sessionId=YourSessionId

##### Response


```json
{
	    "Records": 2,
	    "TotalRecords": 2,
	    "AlertDetails": [
	        {
	            "AlertId": 
	 300271887,
	            "AlertName": 
	 "1719_test",
	            "DeliveryOptions": 
	 {
	                "Email": 
	 "naresh@naresh1.com",
	                "DeliveryMethod": 
	 "Online",
	                "DeliveryTimes": 
	 "Morning"
	            },
	            "IsGroupAlert": 
	 false,
	            "OwnershipType": 
	 "Personal",
	            "PrivateRSSLink": 
	 "http://rss.int.factiva.com/headlines.aspx?folderid=300271887&EID3=XqTZ%2fV5fX6pvwJzlx2RJKvbKODY7fGMZIowAsacNfzvjdnMpu44J03MFzZu4RU652mu7ghkMnY9BhUYcoP%2fWYyKoFzVm6Z3FvYc86KrKShQvtlkO57o8J8vKcrwg86DEVG1OmvAPNru1fn0MiaLZ6e4iECja37Tx2DBitb%2fR6DpQ8MObdP7syk6gYMMRFPsvjACWRo2ueYlS90Y3D86ypkS8Dgu6azTE2csb3StPQNTip6mFbVYDlWnV0GjHsJ1r7Fr57J4mi%2ffc430vb1PrdhZ47SNeTNbvobGCkM9Kxjp1h6CM9wNJUIYUCixG0UeA5ycME1r5kgM%3d%7c2",
	            "ProductType": 
	 "IFF",
	            "NewHits": 
	 true
	        },
	        {
	            "AlertId": 
	 300271343,
	            "AlertName": 
	 "a_twst",
	            "DeliveryOptions": 
	 {
	                "Email": 
	 "new1@new.com",
	                "TimeZone": 
	 "-05:00|1",
	                "DeliveryMethod": 
	 "Batch",
	                "DeliveryTimes": 
	 "Both"
	            },
	            "IsGroupAlert": 
	 false,
	            "OwnershipType": 
	 "Personal",
	            "PrivateRSSLink": 
	 "http://rss.int.factiva.com/headlines.aspx?folderid=300271343&EID3=XqTZ%2fV5fX6pvwJzlx2RJKvbKODY7fGMZIowAsacNfzvjdnMpu44J03MFzZu4RU652mu7ghkMnY9BhUYcoP%2fWYyKoFzVm6Z3FvYc86KrKShRY7vfCUZ73JTYMBcpGF%2bm646zrokgh0V8j3fm2TlDpXGKypeaIDqIpvPKIAP7xRYVz9xaN3e376eZ%2b7w23yPzEVU2CzuMjoS7diKj7ei4ci8kcHU%2fJ%2b4FMz9CatOzhiv58HF9YJzZLL4X75l91eupTJ7Kv4GWmMkiBtD38mkAl3RQFAp2Xr9IApwK91CTE0XziX4vj3JW9ZojHPtphKZbO%7c2",
	            "ProductType": 
	 "IFF",
	            "NewHits": 
	 true
	        }
	    ]
	}

```

 
#### Get Alert by Id


##### Description

This transaction retrieves alert details by Alert Id.

##### URL (GET)

http://webserver/api/Public/version/Alert/Id/format?SessionId=SessionId&Callback=Callback&Id=AlertId&Parts=Parts

##### Request Parameters

|    | Parameter                 | Type    | Description                                                                                                                                                                                      | Comment                                                                                                                                                                                                               |
|---:|:--------------------------|:--------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | Format*                   | String  | The format in which the request and response data must be processed.                                                                                                                             | Valid formats are XML and JSON.                                                                                                                                                                                       |
|  2 | SessionId/EncryptedToken* | String  | Credential to identify the logged-in user. This can be either the Session Id received when the current session was created or the Encrypted Token for the user's credentials.                    | This value can be provided in the Request Header or the Request URL.                                                                                                                                                  |
|  3 | Callback                  | String  | JSONP callback function name for cross-domain content requests.                                                                                                                                  | This parameter is applicable when the data is in JSON format only.                                                                                                                                                    |
|  4 | Id                        | Integer | The identifier for the alert to retrieve.                                                                                                                                                        |                                                                                                                                                                                                                       |
|  5 | Parts                     | String  | Parameter to request additional information in the response.                                                                                                                                     | Valid values:<li>rssurl - Provides a link to the alert's RSS feed.<li>DeDuplicationLevel - Returns duplicate alerts as specified in the DeDuplicationLevel parameter.<li>By default no additional parts are returned. |
|  6 | DeDuplicationLevel        | String  | Indicates how duplicate records must be handled.<li>Note: When the DeDuplicationLevel is Similar or NearExact, the request must use the offset from the previous response for proper pagination. |                                                                                                                                                                                                                       |
|    | Parameter                 | Type    | Description                                                                                                                                                                                      | Comment                                                                                                                                                                                                               |
|---:|:--------------------------|:--------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | Format*                   | String  | The format in which the request and response data must be processed.                                                                                                                             | Valid formats are XML and JSON.                                                                                                                                                                                       |
|  2 | SessionId/EncryptedToken* | String  | Credential to identify the logged-in user. This can be either the Session Id received when the current session was created or the Encrypted Token for the user's credentials.                    | This value can be provided in the Request Header or the Request URL.                                                                                                                                                  |
|  3 | Callback                  | String  | JSONP callback function name for cross-domain content requests.                                                                                                                                  | This parameter is applicable when the data is in JSON format only.                                                                                                                                                    |
|  4 | Id                        | Integer | The identifier for the alert to retrieve.                                                                                                                                                        |                                                                                                                                                                                                                       |
|  5 | Parts                     | String  | Parameter to request additional information in the response.                                                                                                                                     | Valid values:<li>rssurl - Provides a link to the alert's RSS feed.<li>DeDuplicationLevel - Returns duplicate alerts as specified in the DeDuplicationLevel parameter.<li>By default no additional parts are returned. |
|  6 | DeDuplicationLevel        | String  | Indicates how duplicate records must be handled.<li>Note: When the DeDuplicationLevel is Similar or NearExact, the request must use the offset from the previous response for proper pagination. |                                                                                                                                                                                                                       |

##### Response Tags

|    | Parameter                           | Type    | Description                                                                                                                                        | Comment                                                                                                                                                                                                                                                                                                                                                                         |
|---:|:------------------------------------|:--------|:---------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | AlertByIdResponse                   | -       | The top-level response container.                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                 |
|  2 | Alerts                              | -       | Container for alerts.                                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                 |
|  3 | Alert                               | -       | Container for alert details.                                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                 |
|  4 | AlertId                             | Integer | The unique identifier for the alert.                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                 |
|  5 | AlertName                           | String  | The name of the alert.                                                                                                                             | This parameter is case sensitive.                                                                                                                                                                                                                                                                                                                                               |
|  6 | DeduplicationLevel                  | String  | Deduplication applied to the alert contents.                                                                                                       | Valid values:<li>Off<li>Similar<li>VirtuallyIdentical                                                                                                                                                                                                                                                                                                                           |
|  7 | DeliveryOptions                     | -       | Container for alert delivery settings.                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                 |
|  8 | Email                               | String  | The email address to which the alert is delivered.                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                 |
|  9 | LanguageCode                        | String  | The code representing the language of the alert contents.                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                 |
| 10 | MaximumNumberofHeadlinesPerDelivery | Integer | The maximum number of headlines in each alert delivered.                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                 |
| 11 | TimeZone                            | String  | The time zone in which the alert is delivered.                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                 |
| 12 | DeliveryMethod                      | String  | The method in which the alert is delivered.                                                                                                        | Valid values:<li>Batch<li>Continuous. Notifies the user of news pertaining to their interests and holdings 24 hours/day, 7 days/week. The user receives the news as soon as it becomes available.<li>Feed. Notifies the user of news pertaining to their interests and holdings at a specific time of day. The time period is defined by the DeliveryTimes parameter.<li>Online |
| 13 | DeliveryTimes                       | String  | Indicates the time at which the email is delivered.                                                                                                | Note: This parameter is applicable only when DeliveryMethod=Feed.<li>Valid values:<li>None<li>Morning<li>Afternoon<li>Both<li>Continuous                                                                                                                                                                                                                                        |
| 14 | DocumentType                        | String  | The type of content delivered in the alert.                                                                                                        | Valid values:<li>SNIP - Article snippet<li>FULL - Full article<li>FULR - Full article and indexing<li>HDLN - Headline                                                                                                                                                                                                                                                           |
| 15 | ResultDisplayFormat                 | String  | The format in which the alert is delivered.                                                                                                        | Valid values:<li>PlainText<li>PlainTextAttachment<li>HTML<li>HTMLAttachment<li>Mobile                                                                                                                                                                                                                                                                                           |
| 16 | SortBy                              | String  | The parameter by which the results must be sorted.                                                                                                 | Valid values:<li>Date<li>Relevance<li>ClipTime<li>EventType                                                                                                                                                                                                                                                                                                                     |
| 17 | IsGroupAlert                        | Boolean | Indicates if this is a group alert.                                                                                                                | Valid values are True and False.                                                                                                                                                                                                                                                                                                                                                |
| 18 | PrivateRSSLink/PublicRSSLink        | String  | A URL that links to the alert's RSS feed.<li>Note: PrivateRSSLink is returned for personal alerts and PublicRSSLink is returned for shared alerts. | Note: This value is returned only if Parts=RssUrl in the request.                                                                                                                                                                                                                                                                                                               |
| 19 | ProductType                         | String  | The type of product the alert is about.                                                                                                            | Valid values:<li>WealthManagementAlerts<li>InvestmentBankingAlerts<li>WealthManagementTriggers<li>InvestmentBankingTriggers<li>Global<li>WsjProfessional<li>DirectToClient<li>IFF<li>IWE                                                                                                                                                                                        |
| 20 | AlertQuery                          | -       | Container for components of query used to create the alert.                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                 |
| 21 | Queries                             | -       | Container for one or more queries.                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                 |
| 22 | Query                               | -       | Container for a query.                                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                 |
| 23 | QueryString                         | String  | The query string used to set up the alert.                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                 |
| 24 | Scope                               | String  | The scope of the query.                                                                                                                            | Valid values:<li>About<li>Occur<li>None                                                                                                                                                                                                                                                                                                                                         |
| 25 | SearchMode                          | String  | Indicates how the search query was interpreted.                                                                                                    | Valid values:<li>Traditional<li>Simple                                                                                                                                                                                                                                                                                                                                          |
| 26 | SourceGenres                        | -       | Container for source genres to search.                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                 |
| 27 | SourceGenre                         | String  | Represents the content group to search.                                                                                                            | Possible values:<li>Publications<li>NewsSites                                                                                                                                                                                                                                                                                                                                   |
| 28 | Contact                             | String  | The contact person for the alert.                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                 |

##### XML Payload


```xml
<AlertByIdResponse>
  <Alerts>
    <Alert>
      <AlertId></AlertId>
      <AlertName></AlertName>
      <DeliveryOptions>
        <Email></Email>
        <LanguageCode></LanguageCode>
        <MaximumNumberofHeadlinesPerDelivery></MaximumNumberofHeadlinesPerDelivery>
        <TimeZone></TimeZone>
       <DeDuplicationLevel></DeDuplicationlevel>
        <DeliveryMethod></DeliveryMethod>
        <DeliveryTimes></DeliveryTimes>
        <DocumentType></DocumentType>
        <EmailDeliveryContentTypes>
          <EmailDeliveryContentType>String
          content</EmailDeliveryContentType>
          <EmailDeliveryContentType>String
          content</EmailDeliveryContentType>
        </EmailDeliveryContentTypes>
        <ResultDisplayFormat></ResultDisplayFormat>
        <SortBy></SortBy>
      </DeliveryOptions>
      <IsGroupAlert></IsGroupAlert>
      <OwnershipType></OwnershipType>
      <PrivateRSSLink></PrivateRSSLink>
      <ProductType></ProductType>
      <PublicRSSLink></PublicRSSLink>
      <AlertQuery>
        <Queries>
          <Query>
            <QueryString></QueryString>
            <Scope></Scope>
            <SearchMode></SearchMode>
          </Query>
          ......
        </Queries>
        <SourceGenres>
          <SourceGenre></SourceGenre>
          ......
        </SourceGenres>
      </AlertQuery>
      <Contact></Contact>
    </Alert>
  </Alerts>
</AlertByIdResponse>

```


#####  

http://api.beta.dowjones.com/api/Public/2.0/Alert/id/xml?id=300272176&parts=rssurl&sessionId=YourSessionId

```xml
<AlertByIdResponse>
  <Alerts>
    <Alert>
      <AlertId>300272176</AlertId>
      <AlertName>TestAlert_10</AlertName>
      <DeliveryOptions>
        <MaximumNumberofHeadlinesPerDelivery>10</MaximumNumberofHeadlinesPerDelivery>
        <DeliveryMethod>Online</DeliveryMethod>
        <DeliveryTimes>None</DeliveryTimes>
        <DocumentType>SNIP</DocumentType>
        <EmailDeliveryContentTypes>
          <EmailDeliveryContentType>
          publication</EmailDeliveryContentType>
        </EmailDeliveryContentTypes>
        <ResultDisplayFormat>HTML</ResultDisplayFormat>
        <SortBy>Date</SortBy>
      </DeliveryOptions>
      <IsGroupAlert>false</IsGroupAlert>
      <OwnershipType>Personal</OwnershipType>
      <PrivateRSSLink>http://rss.int.factiva.com/headlines.aspx?folderid=300272176&amp;EID3=XqTZ%2fV5fX6pvwJzlx2RJKvbKODY7fGMZIowAsacNfzvjdnMpu44J03MFzZu4RU652mu7ghkMnY9BhUYcoP%2fWYyKoFzVm6Z3FdBObL1FYBTMwyfFdusyqpGQTuZvic5pr8C2%2bZ9jF%2faaEnlGhmAQpLrJRXGJ3ldjKpVGmNNgXZKqaQrzFINL2sEGe7SbQTj1mE67hOPnyWYhJcI1S%2fgT2puts%2fC85qm1uz5fljam8t3HoWwov6S5z1SbNOrNcPFyI0Tyjvs%2fXY7L%2bqvoGjoWJUpmsUXyoR5ldkhK8lRD24hFan32BwflSrDfUFW3d0tqbE1nIkLPfEKbMA%2finah5jc3AqZTlrwUl0%7c2</PrivateRSSLink>
      <ProductType>InvestmentBankingAlerts</ProductType>
      <AlertQuery>
        <Queries>
          <Query>
            <QueryString>obama</QueryString>
            <SearchMode>Simple</SearchMode>
          </Query>
        </Queries>
        <SourceGenres>
          <SourceGenre>Publications</SourceGenre>
          <SourceGenre>NewsSites</SourceGenre>
        </SourceGenres>
      </AlertQuery>
      <Contact>contactperson</Contact>
    </Alert>
  </Alerts>
</AlertByIdResponse>

```

http://api.beta.dowjones.com/api/Public/2.0/Alert/id/json?id=300272176&parts=rssurl&sessionId=YourSessionId

```json
{
    "Alerts": [
        {
            "AlertId": 300272176,
            "AlertName": "InfyTestAlert_10",
            "DeliveryOptions": {
                "MaximumNumberofHeadlinesPerDelivery": 10,
                "DeliveryMethod": "Online",
                "DeliveryTimes": "None",
                "DocumentType": "SNIP",
                "EmailDeliveryContentTypes": [
                    "publication"
                ],
                "ResultDisplayFormat": "HTML",
                "SortBy": "Date"
            },
            "IsGroupAlert": false,
            "OwnershipType": "Personal",
            "PrivateRSSLink": "http://rss.int.factiva.com/headlines.aspx?folderid=300272176&EID3=XqTZ%2fV5fX6pvwJzlx2RJKvbKODY7fGMZIowAsacNfzvjdnMpu44J03MFzZu4RU652mu7ghkMnY9BhUYcoP%2fWYyKoFzVm6Z3FdBObL1FYBTMwyfFdusyqpGQTuZvic5pr8C2%2bZ9jF%2faaEnlGhmAQpLrJRXGJ3ldjKpVGmNNgXZKqaQrzFINL2sEGe7SbQTj1mE67hOPnyWYhJcI1S%2fgT2puts%2fC85qm1uz5fljam8t3HoWwov6S5z1SbNOrNcPFyI0Tyjvs%2fXY7L%2bqvoGjoWJUpmsUXyoR5ldkhK8lRD24hFan32BwflSrDfUFW3d0tqbE1nIkLPfEKbMA%2finah5jc3AqZTlrwUl0%7c2",
            "ProductType": "InvestmentBankingAlerts",
            "AlertQuery": {
                "Queries": [
                    {
                        "QueryString": "obama",
                        "SearchMode": "Simple"
                    }
                ],
                "SourceGenres": [
                    "Publications",
                    "NewsSites"
                ]
            },
            "Contact": "contactperson"
        }
    ]
}

```

 

##### URL (GET)

http://api.beta.dowjones.com/api/Public/2.0/Alert/id/xml?id=300272176&parts=rssurl&sessionId=YourSessionId

##### Response


```xml
<AlertByIdResponse>
  <Alerts>
    <Alert>
      <AlertId>300272176</AlertId>
      <AlertName>TestAlert_10</AlertName>
      <DeliveryOptions>
        <MaximumNumberofHeadlinesPerDelivery>10</MaximumNumberofHeadlinesPerDelivery>
        <DeliveryMethod>Online</DeliveryMethod>
        <DeliveryTimes>None</DeliveryTimes>
        <DocumentType>SNIP</DocumentType>
        <EmailDeliveryContentTypes>
          <EmailDeliveryContentType>
          publication</EmailDeliveryContentType>
        </EmailDeliveryContentTypes>
        <ResultDisplayFormat>HTML</ResultDisplayFormat>
        <SortBy>Date</SortBy>
      </DeliveryOptions>
      <IsGroupAlert>false</IsGroupAlert>
      <OwnershipType>Personal</OwnershipType>
      <PrivateRSSLink>http://rss.int.factiva.com/headlines.aspx?folderid=300272176&amp;EID3=XqTZ%2fV5fX6pvwJzlx2RJKvbKODY7fGMZIowAsacNfzvjdnMpu44J03MFzZu4RU652mu7ghkMnY9BhUYcoP%2fWYyKoFzVm6Z3FdBObL1FYBTMwyfFdusyqpGQTuZvic5pr8C2%2bZ9jF%2faaEnlGhmAQpLrJRXGJ3ldjKpVGmNNgXZKqaQrzFINL2sEGe7SbQTj1mE67hOPnyWYhJcI1S%2fgT2puts%2fC85qm1uz5fljam8t3HoWwov6S5z1SbNOrNcPFyI0Tyjvs%2fXY7L%2bqvoGjoWJUpmsUXyoR5ldkhK8lRD24hFan32BwflSrDfUFW3d0tqbE1nIkLPfEKbMA%2finah5jc3AqZTlrwUl0%7c2</PrivateRSSLink>
      <ProductType>InvestmentBankingAlerts</ProductType>
      <AlertQuery>
        <Queries>
          <Query>
            <QueryString>obama</QueryString>
            <SearchMode>Simple</SearchMode>
          </Query>
        </Queries>
        <SourceGenres>
          <SourceGenre>Publications</SourceGenre>
          <SourceGenre>NewsSites</SourceGenre>
        </SourceGenres>
      </AlertQuery>
      <Contact>contactperson</Contact>
    </Alert>
  </Alerts>
</AlertByIdResponse>

```


##### URL (GET)

http://api.beta.dowjones.com/api/Public/2.0/Alert/id/json?id=300272176&parts=rssurl&sessionId=YourSessionId

##### Response


```json
{
    "Alerts": [
        {
            "AlertId": 300272176,
            "AlertName": "InfyTestAlert_10",
            "DeliveryOptions": {
                "MaximumNumberofHeadlinesPerDelivery": 10,
                "DeliveryMethod": "Online",
                "DeliveryTimes": "None",
                "DocumentType": "SNIP",
                "EmailDeliveryContentTypes": [
                    "publication"
                ],
                "ResultDisplayFormat": "HTML",
                "SortBy": "Date"
            },
            "IsGroupAlert": false,
            "OwnershipType": "Personal",
            "PrivateRSSLink": "http://rss.int.factiva.com/headlines.aspx?folderid=300272176&EID3=XqTZ%2fV5fX6pvwJzlx2RJKvbKODY7fGMZIowAsacNfzvjdnMpu44J03MFzZu4RU652mu7ghkMnY9BhUYcoP%2fWYyKoFzVm6Z3FdBObL1FYBTMwyfFdusyqpGQTuZvic5pr8C2%2bZ9jF%2faaEnlGhmAQpLrJRXGJ3ldjKpVGmNNgXZKqaQrzFINL2sEGe7SbQTj1mE67hOPnyWYhJcI1S%2fgT2puts%2fC85qm1uz5fljam8t3HoWwov6S5z1SbNOrNcPFyI0Tyjvs%2fXY7L%2bqvoGjoWJUpmsUXyoR5ldkhK8lRD24hFan32BwflSrDfUFW3d0tqbE1nIkLPfEKbMA%2finah5jc3AqZTlrwUl0%7c2",
            "ProductType": "InvestmentBankingAlerts",
            "AlertQuery": {
                "Queries": [
                    {
                        "QueryString": "obama",
                        "SearchMode": "Simple"
                    }
                ],
                "SourceGenres": [
                    "Publications",
                    "NewsSites"
                ]
            },
            "Contact": "contactperson"
        }
    ]
}

```

 
#### Share Alert


##### Description

This transaction shares an alert by Alert Id. Shared alerts can be subscribed by other users.

##### URL (PUT)

http://webserver/api/Public/version/Alert/Share/format?SessionId=SessionId&Callback=Callback&Id=AlertId

##### Request Parameters

|    | Parameter                 | Type    | Description                                                                                                                                                                   | Comment                                                              |
|---:|:--------------------------|:--------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------|
|  1 | Format*                   | String  | The format in which the request and response data must be processed.                                                                                                          | Valid formats are XML and JSON.                                      |
|  2 | SessionId/EncryptedToken* | String  | Credential to identify the logged-in user. This can be either the Session Id received when the current session was created or the Encrypted Token for the user's credentials. | This value can be provided in the Request Header or the Request URL. |
|  3 | Callback                  | String  | JSONP callback function name for cross-domain content requests.                                                                                                               | This parameter is applicable when the data is in JSON format only.   |
|  4 | Id*                       | Integer | The identifier of the alert that must be made public.                                                                                                                         | This value can be obtained from Get Alerts by Product Type response. |

##### Response Tags

|    | Parameter          | Type   | Description                                               | Comment                                                      |
|---:|:-------------------|:-------|:----------------------------------------------------------|:-------------------------------------------------------------|
|  1 | ShareAlertResponse | -      | The top-level response container.                         |                                                              |
|  2 | Message            | String | Message indicating the result of the requested operation. | Valid values are True (successful) and False (unsuccessful). |
Boldface indicates container element.

##### XML Payload


```xml
<ShareAlertResponse>
  <Message></Message>
</ShareAlertResponse>

```


#####  

http://api.beta.dowjones.com/api/Public/2.0/Alert/share/xml?id=8976&sessionId=YourSessionId

```xml
<ShareAlertResponse>
  <Message>True</Message>
</ShareAlertResponse>

```

http://api.beta.dowjones.com/api/Public/2.0/Alert/share/json?id=8976&sessionId=YourSessionId

```json
{
    "Message": "True"
}

```

 

##### URL (PUT)

http://api.beta.dowjones.com/api/Public/2.0/Alert/share/xml?id=8976&sessionId=YourSessionId

##### Response


```xml
<ShareAlertResponse>
  <Message>True</Message>
</ShareAlertResponse>

```


##### URL (PUT)

http://api.beta.dowjones.com/api/Public/2.0/Alert/share/json?id=8976&sessionId=YourSessionId

##### Response


```json
{
    "Message": "True"
}

```

 
#### Unshare Alert


##### Description

This transaction uhshares an alert by Alert Id. An unshared alert cannot be subscribed by other users.

##### URL (DELETE)

http://webserver/api/Public/version/Alert/Share/format?SessionId=SessionId&Callback=Callback&Id=AlertId

##### Request Parameters

|    | Parameter                 | Type    | Description                                                                                                                                                                   | Comment                                                              |
|---:|:--------------------------|:--------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------|
|  1 | Format*                   | String  | The format in which the request and response data must be processed.                                                                                                          | Valid formats are XML and JSON.                                      |
|  2 | SessionId/EncryptedToken* | String  | Credential to identify the logged-in user. This can be either the Session Id received when the current session was created or the Encrypted Token for the user's credentials. | This value can be provided in the Request Header or the Request URL. |
|  3 | Callback                  | String  | JSONP callback function name for cross-domain content requests.                                                                                                               | This parameter is applicable when the data is in JSON format only.   |
|  4 | Id*                       | Integer | The identifier of the alert that must be made public.                                                                                                                         | This value can be obtained from Get Alerts by Product Type response. |

##### Response Tags

|    | Parameter            | Type   | Description                                               | Comment                                                      |
|---:|:---------------------|:-------|:----------------------------------------------------------|:-------------------------------------------------------------|
|  1 | UnShareAlertResponse | -      | The top-level response container.                         |                                                              |
|  2 | Message              | String | Message indicating the result of the requested operation. | Valid values are True (successful) and False (unsuccessful). |
 

##### XML Payload


```xml
<UnShareAlertResponse>
  <Message></Message>
</UnShareAlertResponse>

```


#####  

http://api.beta.dowjones.com/api/Public/2.0/Alert/share/xml?id=8976&sessionId=YourSessionId

```xml
<UnShareAlertResponse>
  <Message>True</Message>
</UnShareAlertResponse>

```

http://api.beta.dowjones.com/api/Public/2.0/Alert/share/json?id=8976&sessionId=YourSessionId

```json
{
    "Message": "True"
}

```

 

##### URL (DELETE)

http://api.beta.dowjones.com/api/Public/2.0/Alert/share/xml?id=8976&sessionId=YourSessionId

##### Response


```xml
<UnShareAlertResponse>
  <Message>True</Message>
</UnShareAlertResponse>

```


##### URL (DELETE)

http://api.beta.dowjones.com/api/Public/2.0/Alert/share/json?id=8976&sessionId=YourSessionId

##### Response


```json
{
    "Message": "True"
}

```

 
#### Subscribe Alert by Id


##### Description

This transaction allows the logged-in user to subscribe to an alert by Alert Id.

##### URL (PUT)

http://webserver/api/Public/version/Alert/Subscribe/format?SessionId=SessionId&Callback=Callback&Id=AlertId

##### Request Parameters

|    | Parameter                 | Type    | Description                                                                                                                                                                   | Comment                                                              |
|---:|:--------------------------|:--------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------|
|  1 | Format*                   | String  | The format in which the request and response data must be processed.                                                                                                          | Valid formats are XML and JSON.                                      |
|  2 | SessionId/EncryptedToken* | String  | Credential to identify the logged-in user. This can be either the Session Id received when the current session was created or the Encrypted Token for the user's credentials. | This value can be provided in the Request Header or the Request URL. |
|  3 | Callback                  | String  | JSONP callback function name for cross-domain content requests.                                                                                                               | This parameter is applicable when the data is in JSON format only.   |
|  4 | Id*                       | Integer | The unique identifier of the alert to subscribe.                                                                                                                              |                                                                      |
|    | Parameter                 | Type    | Description                                                                                                                                                                   | Comment                                                              |
|---:|:--------------------------|:--------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------|
|  1 | Format*                   | String  | The format in which the request and response data must be processed.                                                                                                          | Valid formats are XML and JSON.                                      |
|  2 | SessionId/EncryptedToken* | String  | Credential to identify the logged-in user. This can be either the Session Id received when the current session was created or the Encrypted Token for the user's credentials. | This value can be provided in the Request Header or the Request URL. |
|  3 | Callback                  | String  | JSONP callback function name for cross-domain content requests.                                                                                                               | This parameter is applicable when the data is in JSON format only.   |
|  4 | Id*                       | Integer | The unique identifier of the alert to subscribe.                                                                                                                              |                                                                      |

##### Response Tags

|    | Parameter              | Type    | Description                             | Comment   |
|---:|:-----------------------|:--------|:----------------------------------------|:----------|
|  1 | SubscribeAlertResponse | -       | The top-level response container.       |           |
|  2 | AlertId                | Integer | The identifier of the alert subscribed. |           |

##### XML Payload


```xml
<SubscribeAlertResponse>
  <AlertId></AlertId>
</SubscribeAlertResponse>

```

 

##### URL (PUT)

http://api.beta.dowjones.com/api/Public/2.0/Alert/subscribe/xml?id=300270713&sessionId=YourSessionId

##### Response


```xml
<SubscribeAlertResponse>
  <Message>True</Message>
</SubscribeAlertResponse>

```


##### URL (PUT)

http://api.beta.dowjones.com/api/Public/2.0/Alert/subscribe/json?id=300270713&sessionId=YourSessionId

##### Response


```json
{
    "Message": "True"
}

```

 
#### Unsubscribe Alert by Id


##### Description

This transaction allows the logged-in user to unsubscribe from an alert by Alert Id.

##### URL (DELETE)

http://webserver/api/Public/version/Alert/Subscribe/format?SessionId=SessionId&Callback=Callback&Id=AlertId

##### Request Parameters

|    | Parameter                  | Type    | Description                                                                                                                                                                   | Comment                                                              |
|---:|:---------------------------|:--------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------|
|  1 | Format*                    | String  | The format in which the request and response data must be processed.                                                                                                          | Valid formats are XML and JSON.                                      |
|  2 | SessionId/EncryptedTokend* | String  | Credential to identify the logged-in user. This can be either the Session Id received when the current session was created or the Encrypted Token for the user's credentials. | This value can be provided in the Request Header or the Request URL. |
|  3 | Callback                   | String  | JSONP callback function name for cross-domain content requests.                                                                                                               | This parameter is applicable when the data is in JSON format only.   |
|  4 | Id*                        | Integer | The unique identifier of the alert to unsubscribe.                                                                                                                            |                                                                      |
|    | Parameter                  | Type    | Description                                                                                                                                                                   | Comment                                                              |
|---:|:---------------------------|:--------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------|
|  1 | Format*                    | String  | The format in which the request and response data must be processed.                                                                                                          | Valid formats are XML and JSON.                                      |
|  2 | SessionId/EncryptedTokend* | String  | Credential to identify the logged-in user. This can be either the Session Id received when the current session was created or the Encrypted Token for the user's credentials. | This value can be provided in the Request Header or the Request URL. |
|  3 | Callback                   | String  | JSONP callback function name for cross-domain content requests.                                                                                                               | This parameter is applicable when the data is in JSON format only.   |
|  4 | Id*                        | Integer | The unique identifier of the alert to unsubscribe.                                                                                                                            |                                                                      |

##### Response Tags

|    | Parameter                | Type   | Description                                               | Comment                                                      |
|---:|:-------------------------|:-------|:----------------------------------------------------------|:-------------------------------------------------------------|
|  1 | UnSubscribeAlertResponse | -      | The top-level response container.                         |                                                              |
|  2 | Message                  | String | Message indicating the result of the requested operation. | Valid values are True (successful) and False (unsuccessful). |

##### XML Payload


```xml
<UnSubscribeAlertResponse>
  <Message></Message>
</UnSubscribeAlertResponse>

```


##### URL (DELETE)

http://api.beta.dowjones.com/api/Public/2.0/Alert/subscribe/xml?id=300270713&sessionId=YourSessionId

##### Response


```xml
<UnSubscribeAlertResponse>
  <Message>True</Message>
</UnSubscribeAlertResponse>

```


##### URL (DELETE)

http://api.beta.dowjones.com/api/Public/2.0/Alert/subscribe/json?id=300270713&sessionId=YourSessionId

##### Response


```json
{
    "Message": "True"
}

```

 
#### Delete Alert By Id


##### Description

This transaction deletes an alert by Alert Id.

##### URL (DELETE)

http://webserver/api/Public/version/Alert/Id/format?SessionId=SessionId&Callback=Callback&Id=AlertId

##### Parameters

|    | Parameter                 | Type   | Description                                                                                                                                                                 | Comment                                                               |
|---:|:--------------------------|:-------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------|
|  1 | Format*                   | String | The format in which the request and response data must be processed.                                                                                                        | Valid formats are XML  and JSON.                                      |
|  2 | SessionId/EncryptedToken* | String | Credential to identify the logged-in user. This can be either the SessionId received when the current session was created or the Encrypted Tokenfor the user's credentials. | This value can be provided in the Request Header or the Request URL.  |
|  3 | Callback                  | String | JSONP callback function name for cross-domain content requests.                                                                                                             | This parameter is applicable when the data is in JSON format only.    |
|  4 | Id*                       | Long   | The identifier of the alert to delete.                                                                                                                                      | This value can be obtained from Get  Alerts by Product Type response. |
|    | Parameter                 | Type   | Description                                                                                                                                                                 | Comment                                                               |
|---:|:--------------------------|:-------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------|
|  1 | Format*                   | String | The format in which the request and response data must be processed.                                                                                                        | Valid formats are XML  and JSON.                                      |
|  2 | SessionId/EncryptedToken* | String | Credential to identify the logged-in user. This can be either the SessionId received when the current session was created or the Encrypted Tokenfor the user's credentials. | This value can be provided in the Request Header or the Request URL.  |
|  3 | Callback                  | String | JSONP callback function name for cross-domain content requests.                                                                                                             | This parameter is applicable when the data is in JSON format only.    |
|  4 | Id*                       | Long   | The identifier of the alert to delete.                                                                                                                                      | This value can be obtained from Get  Alerts by Product Type response. |

##### Response Tags

|    | Parameter           | Type   | Description                                               | Comment                                                     |
|---:|:--------------------|:-------|:----------------------------------------------------------|:------------------------------------------------------------|
|  1 | DeleteAlertResponse | -      | The top-level response container.                         |                                                             |
|  2 | Message             | String | Message indicating the result of the requested operation. | Valid values are True (successful)and False (unsuccessful). |

##### XML Payload


```xml
<DeleteAlertResponse>
	 <Message>String content</Message>
	</DeleteAlertResponse>

```


#####  

http://api.beta.dowjones.com/api/Public/2.0/Alert/Id/xml?Id=34834&sessionId=YourSessionId

```xml
<DeleteAlertResponse>
		 <Message>True</Message>
		</DeleteAlertResponse>

```

http://api.beta.dowjones.com/api/Public/2.0/Alert/Id/json?Id=34834&sessionId=YourSessionId

```json
{
	    "Message": "True"
	}

```


##### URL(DELETE)

http://api.beta.dowjones.com/api/Public/2.0/Alert/Id/xml?Id=34834&sessionId=YourSessionId

##### Response


```xml
<DeleteAlertResponse>
		 <Message>True</Message>
		</DeleteAlertResponse>

```


##### URL (DELETE)

http://api.beta.dowjones.com/api/Public/2.0/Alert/Id/json?Id=34834&sessionId=YourSessionId

##### Response


```json
{
	    "Message": "True"
	}

```

