# REST2 Author API

## Get Authors By Search String


### Description

This transaction allows a user to search for authors by a search 
	 string. The results can be filtered by Author Id(s), Outlet Id(s), 
	 and Outlet Name.

### URL (GET)

http://webserver/api/Public/version/Author/format?SessionId=SessionId&Callback=Callback&Offset=Offset&Records=Records&SortBy=SortBy&SearchString=SearchString

### Request Parameters

|    | Parameter                 | Type    | Description                                                                                                                                                                 | Comment                                                                                                           |
|---:|:--------------------------|:--------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------|
|  1 | Format*                   | String  | The format in which the request and response data must be processed.                                                                                                        | Valid formats are XML  and JSON.                                                                                  |
|  2 | SessionId/EncryptedToken* | String  | Credential to identify the logged-in user. This can be either the SessionId received when the current session was created or the Encrypted Tokenfor the user's credentials. | This value can be provided in the Request Header or the Request URL.                                              |
|  3 | Callback                  | String  | JSONP callback function name for cross-domain content requests.                                                                                                             | This parameter is applicable when the data is in JSON format only.                                                |
|  4 | Offset                    | Integer | The starting index of the set of records to return.<li>What is Offset?                                                                                                      | The default value is 0.                                                                                           |
|  5 | Records                   | Integer | The number of records to return.                                                                                                                                            | The default value is 100.                                                                                         |
|  6 | SortBy                    | String  | The parameter by which the results must be sorted.                                                                                                                          | Valid values:<li>Name<li>OutletName<li>OutletType<li>OutletFrequency<li>Circulation<li>Email<li>Phone<li>JobTitle |
|  7 | SortOrder                 | String  | The order in which the results must be sorted.                                                                                                                              | Valid  values:<li>Ascending<li>Descending                                                                         |
|  8 | SearchString*             | String  | The text on which the search must be performed.                                                                                                                             |                                                                                                                   |
|  9 | AuthorIds                 | Integer | The  Author Id(s) to filter the search results.                                                                                                                             | Note: Multiple values can be provided.Separate values using pipe (|) delimiter.                                   |
| 10 | OutletIds                 | Integer | The  Outlet Id(s) to filter the search results.                                                                                                                             | Note: Multiple values can be provided.Separate values using pipe (|) delimiter.                                   |
| 11 | OutletName                | String  | The  Outlet Name to filter the search results.                                                                                                                              |                                                                                                                   |
* 
 indicates Required parameter.


### Response Tags

|    | Parameter            | Type    | Description                                                                          | Comment                                                                                                                        |
|---:|:---------------------|:--------|:-------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------|
|  1 | AuthorSearchResponse | -       | The top-level response container.                                                    |                                                                                                                                |
|  2 | Offset               | Integer | The starting index number for the next group of results.<li>What isOffset?           |                                                                                                                                |
|  3 | Records              | Integer | The number of records returned in this response.                                     |                                                                                                                                |
|  4 | TotalRecords         | Integer | The total number of records that matched the request.                                |                                                                                                                                |
|  5 | Authors              | -       | Container for information about one or  more authors.                                |                                                                                                                                |
|  6 | Author               | -       | Container for information about one author.                                          |                                                                                                                                |
|  7 | FirstName            | String  | The first  name of the author.                                                       |                                                                                                                                |
|  8 | Id                   | Integer | The unique identifier for the author.                                                |                                                                                                                                |
|  9 | LastName             | String  | The last  name of the author.                                                        |                                                                                                                                |
| 10 | OutletId             | Integer | The  unique identifier for the primary publication the author is  associated with.   |                                                                                                                                |
| 11 | OutletName           | String  | The name of the publication.                                                         |                                                                                                                                |
| 12 | Circulation          | Integer | Circulation  figure for the publication.                                             |                                                                                                                                |
| 13 | Email                | String  | The  email address of the author.                                                    |                                                                                                                                |
| 14 | JobTitle             | String  | The  job title of the author.                                                        |                                                                                                                                |
| 15 | FullName             | String  | The full name of the author.                                                         |                                                                                                                                |
| 16 | LastName             | String  | The  last name of the author.                                                        |                                                                                                                                |
| 17 | Phone                | String  | The  phone number of the author.                                                     |                                                                                                                                |
| 18 | Gender               | String  | The  gender of the author.                                                           | Valid  values:<li>Male<li>Female<li>NotKnown                                                                                   |
| 19 | Industries           | -       | Container  for one or more industries the author writes about.                       |                                                                                                                                |
| 20 | Industry             | -       | Container  for industry information. Contains description, Id, name,  and parent Id. | <Industry>\<Id>Integer\</Id>\<Name>String\</Name>\<ParentId>Integer\</ParentId>\<Description>String\</Description>\</Industry> |
| 21 | Regions              | -       | Container  for one or more regions the author writes about.                          |                                                                                                                                |
| 22 | Region               | -       | Container  for region information. Contains description, Id, name, and  parent Id.   | <Region>\<Id>Integer\</Id>\<Name>String\</Name>\<ParentId>Integer\</ParentId>\<Description>String\</Description>\</Region>     |
| 23 | Subjects             | -       | Container  for one or more news subjects theauthor writes about.                     |                                                                                                                                |
| 24 | Subject              | -       | Container  for subject details. Contains description, Id, name, and parent  Id.      | <Subject>\<Id>Integer\</Id>\<Name>String\</Name>\<ParentId>Integer\</ParentId>\<Description>String\</Description>\</Subject>   |

### XML Payload


```xml
<AuthorSearchResponse>
	  <Offset></Offset>
	  <Records></Records>
	  <TotalRecords></TotalRecords>
	  <Authors>
	    <Author>
	      <Id></Id>
	      <OutletName></OutletName>
	      <FullName></FullName>
	    </Author>
	    ...
	  </Authors>
	</AuthorSearchResponse>

```


###  

http://api.beta.dowjones.com/api/Public/2.0/Author/xml?searchstring=moss&records=2&sessionId=YourSessionId

```xml
<AuthorSearchResponse>
	  <Offset>2</Offset>
	  <Records>2</Records>
	  <TotalRecords>166</TotalRecords>
	  <Authors>
	    <Author>
	      <Id>709596</Id>
	      <OutletName>The Times</OutletName>
	      <FullName>Andrew Moss</FullName>
	    </Author>
	    <Author>
	      <Id>889596</Id>
	      <OutletName>The Chicago Times</OutletName>
	      <FullName>Andrew Moss</FullName>
	    </Author>
	  </Authors>
	</AuthorSearchResponse>

```

http://api.beta.dowjones.com/api/Public/2.0/Author/json?records=1&searchstring=moss&sessionId=YourSessionId

```json
{
	    "Offset": 0,
	    "Records": 1,
	    "TotalRecords": 1,
	    "Authors": [
	        {
	            "Id": 
	 1465833,
	            "OutletName": 
	 "The Wall Street Journal Europe",
	            "FullName": 
	 "Walter S. Mossberg",
	        }
	    ]
	}

```

 

### URL (GET)

http://api.beta.dowjones.com/api/Public/2.0/Author/xml?searchstring=moss&records=2&sessionId=YourSessionId

### Response


```xml
<AuthorSearchResponse>
	  <Offset>2</Offset>
	  <Records>2</Records>
	  <TotalRecords>166</TotalRecords>
	  <Authors>
	    <Author>
	      <Id>709596</Id>
	      <OutletName>The Times</OutletName>
	      <FullName>Andrew Moss</FullName>
	    </Author>
	    <Author>
	      <Id>889596</Id>
	      <OutletName>The Chicago Times</OutletName>
	      <FullName>Andrew Moss</FullName>
	    </Author>
	  </Authors>
	</AuthorSearchResponse>

```


### URL (GET)

http://api.beta.dowjones.com/api/Public/2.0/Author/json?records=1&searchstring=moss&sessionId=YourSessionId

### Response


```json
{
	    "Offset": 0,
	    "Records": 1,
	    "TotalRecords": 1,
	    "Authors": [
	        {
	            "Id": 
	 1465833,
	            "OutletName": 
	 "The Wall Street Journal Europe",
	            "FullName": 
	 "Walter S. Mossberg",
	        }
	    ]
	}

```

 
## Get Author By Id


### Description

This transaction retrieves information about an author by Author Id.

### URL (GET)

http://webserver/api/Public/version/Author/id/format?SessionId=SessionId&Callback=Callback&Id=AuthorId

### Request Parameters

|    | Parameter                 | Type    | Description                                                                                                                                                                   | Comment                                                              |
|---:|:--------------------------|:--------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------|
|  1 | Format*                   | String  | The format in which the request and response data must be processed.                                                                                                          | Valid formats are XML and JSON.                                      |
|  2 | SessionId/EncryptedToken* | String  | Credential to identify the logged-in user. This can be either the Session Id received when the current session was created or the Encrypted Token for the user's credentials. | This value can be provided in the Request Header or the Request URL. |
|  3 | Callback                  | String  | JSONP callback function name for cross-domain content requests.                                                                                                               | This parameter is applicable when the data is in JSON format only.   |
|  4 | Id*                       | Integer | The unique identifier for the author.                                                                                                                                         |                                                                      |
|    | Parameter                 | Type    | Description                                                                                                                                                                   | Comment                                                              |
|---:|:--------------------------|:--------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------|
|  1 | Format*                   | String  | The format in which the request and response data must be processed.                                                                                                          | Valid formats are XML and JSON.                                      |
|  2 | SessionId/EncryptedToken* | String  | Credential to identify the logged-in user. This can be either the Session Id received when the current session was created or the Encrypted Token for the user's credentials. | This value can be provided in the Request Header or the Request URL. |
|  3 | Callback                  | String  | JSONP callback function name for cross-domain content requests.                                                                                                               | This parameter is applicable when the data is in JSON format only.   |
|  4 | Id*                       | Integer | The unique identifier for the author.                                                                                                                                         |                                                                      |

### Response Tags

|    | Parameter          | Type   | Description                       | Comment   |
|---:|:-------------------|:-------|:----------------------------------|:----------|
|  1 | AuthorByIdResponse | -      | The top-level response container. |           |
|  2 | Authors            | -      |                                   |           |
|    | Parameter          | Type   | Description                       | Comment   |
|---:|:-------------------|:-------|:----------------------------------|:----------|
|  1 | AuthorByIdResponse | -      | The top-level response container. |           |
|  2 | Authors            | -      |                                   |           |

### XML Payload


```xml
<AuthorByIdResponse>
  <Authors>
    <Author>
      <FirstName></FirstName>
      <Id></Id>
      <Industries>
        <Industry>
          <Description></Description>
          <Id></Id>
          <Name></Name>
          <ParentId></ParentId>
        </Industry>
        ...
      </Industries>
      <LastName></LastName>
      <Regions>
        <Region>
          <Description></Description>
          <Id></Id>
          <Name></Name>
          <Code></Code>
          <ParentId></ParentId>
        </Region>
        ...
      </Regions>
      <Subjects>
        <Subject>
          <Description></Description>
          <Id></Id>
          <Name></Name>
          <ParentId></ParentId>
        </Subject>
        ...
      </Subjects>
      <Address>
        <Building></Building>
        <!--Valid elements of type: Region-->
        <City>
          <Id></Id>
          <Name></Name>
          <Code></Code>
        </City>
        <!--Valid elements of type: Region-->
        <Country>
          <Id></Id>
          <Name></Name>
          <Code></Code>
        </Country>
        <Floor></Floor>
        <Id></Id>
        <IsHeadquarters></IsHeadquarters>
        <Line1></Line1>
        <Line2></Line2>
        <PoBox></PoBox>
        <PostOrZip></PostOrZip>
        <Room></Room>
        <!--Valid elements of type: Region-->
        <State>
          <Id></Id>
          <Name></Name>
          <Code></Code>
        </State>
      </Address>
      <Biography></Biography>
      <Contacts>
        <Contact>
          <IsIM></IsIM>
          <IsPreferred></IsPreferred>
          <TemplateUrl></TemplateUrl>
          <Type></Type>
          <TypeName></TypeName>
          <Value></Value>
        </Contact>
        ...
      </Contacts>
      <EmploymentDetails>
        <Employment>
          <Bureau></Bureau>
          <Contacts>
            <Contact>
              <IsIM></IsIM>
              <IsPreferred></IsPreferred>
              <TemplateUrl></TemplateUrl>
              <Type></Type>
              <TypeName></TypeName>
              <Value></Value>
            </Contact>
            ...
          </Contacts>
          <DateCreated></DateCreated>
          <DateUpdated></DateUpdated>
          <Email></Email>
          <Id></Id>
          <IsPrimaryContact></IsPrimaryContact>
          <IsPrimaryEmployer></IsPrimaryEmployer>
          <JobTitle></JobTitle>
          <OutletId></OutletId>
          <Role>
            <Id></Id>
            <Name></Name>
          </Role>
          <TypeName></TypeName>
          <YearEnd></YearEnd>
          <YearStart></YearStart>
        </Employment>
        ...
      </EmploymentDetails>
      <OutletId></OutletId>
      <OutletName></OutletName>
      <PitchNotes></PitchNotes>
      <WebSite></WebSite>
      <WorkingLanguages>
        <Language>
          <Id></Id>
          <Name></Name>
          <Code></Code>
        </Language>
        ...
      </WorkingLanguages>
      <Books>
        <Book>
          <Id></Id>
          <Name></Name>
        </Book>
        ...
      </Books>
      <Circulation></Circulation>
      <Columns>
        <Column>
          <Id></Id>
          <Industries>
            <Industry>
              <Description></Description>
              <Id></Id>
              <Name></Name>
              <ParentId></ParentId>
            </Industry>
            <Industry>
              <Description></Description>
              <Id></Id>
              <Name></Name>
              <ParentId></ParentId>
            </Industry>
          </Industries>
          <LastName></LastName>
          <Regions>
            <Region>
              <Description></Description>
              <Id></Id>
              <Name></Name>
              <Code></Code>
              <ParentId></ParentId>
            </Region>
            <Region>
              <Description></Description>
              <Id></Id>
              <Name></Name>
              <Code></Code>
              <ParentId></ParentId>
            </Region>
          </Regions>
          <Subjects>
            <Subject>
              <Description></Description>
              <Id></Id>
              <Name></Name>
              <ParentId></ParentId>
            </Subject>...
          </Subjects>
          <AuthorIds>
            <int></int>
            <int></int>
          </AuthorIds>
          <Name></Name>
          <WebAddress></WebAddress>
        </Column>
        ...
      </Columns>
      <DayBirth></DayBirth>
      <Deceased></Deceased>
      <EducationDetails>
        <Education>
          <Degree>
            <Subject></Subject>
            <Type></Type>
          </Degree>
          <Id></Id>
          <Outcome></Outcome>
          <University>
            <Id></Id>
            <Name></Name>
            <!--Valid elements of type: Region-->
            <Country>
              <Id></Id>
              <Name></Name>
              <Code></Code>
            </Country>
          </University>
          <Year></Year>
        </Education>
        ...
      </EducationDetails>
      <Email></Email>
      <FullName></FullName>
      <Gender></Gender>
      <!--Valid elements of type: Region-->
      <HomeCity>
        <Id></Id>
        <Name></Name>
        <Code></Code>
      </HomeCity>
      <!--Valid elements of type: Region-->
      <HomeCountry>
        <Id></Id>
        <Name></Name>
        <Code></Code>
      </HomeCountry>
      <!--Valid elements of type: Region-->
      <HomeState>
        <Id></Id>
        <Name></Name>
        <Code></Code>
      </HomeState>
      <JobTitle></JobTitle>
      <LastArticleWrittenDate></LastArticleWrittenDate>
      <MiddleName></MiddleName>
      <MonthBirth></MonthBirth>
      <NNID></NNID>
      <NamePrefix></NamePrefix>
      <NameSuffix></NameSuffix>
      <NameVariations>
        <NameVariation>
          <Id></Id>
          <Name></Name>
          <Type></Type>
        </NameVariation>
        ...
      </NameVariations>
      <Phone></Phone>
      <ProprietaryInfoID></ProprietaryInfoID>
      <SocialNetworks>
        <SocialNetwork>
          <Id></Id>
          <Name></Name>
          <TemplateUrl></TemplateUrl>
          <Url></Url>
        </SocialNetwork>
        ...
      </SocialNetworks>
      <YearBirth></YearBirth>
    </Author>
  </Authors>
</AuthorByIdResponse>

```


###  

http://api.beta.dowjones.com/api/Public/2.0/Author/id/xml?id=1089207&sessionId=YourSessionId

```xml
<AuthorByIdResponse>
  <Author>
    <FirstName>Adam</FirstName>
    <Id>709596</Id>
    <LastName>Moss</LastName>
    <Address>
      <City>
        <Id>24655</Id>
        <Name>New York</Name>
      </City>
      <Country>
        <Id>256</Id>
        <Name>United States</Name>
      </Country>
      <Id>307683</Id>
      <Line1>75 Varick Street</Line1>
      <PostOrZip>10013</PostOrZip>
      <State>
        <Id>346</Id>
        <Name>New York</Name>
      </State>
    </Address>
    <Biography>http://en.wikipedia.org/wiki/Adam_Moss</Biography>
    <Contacts />
    <EmploymentDetails>
      <Employment>
        <Contacts>
          <Contact>
            <Type>PhoneOutlet</Type>
            <TypeName>Telephone, Office, Department</TypeName>
            <Value>+1 (212) 508-0700</Value>
          </Contact>
          <Contact>
            <Type>EmailWork</Type>
            <TypeName>Email, Work</TypeName>
            <Value>adam_moss@newyorkmag.com</Value>
          </Contact>
        </Contacts>
        <DateCreated>0001-01-01T00:00:00</DateCreated>
        <DateUpdated>0001-01-01T00:00:00</DateUpdated>
        <Email>adam_moss@newyorkmag.com</Email>
        <Id>3546658</Id>
        <IsPrimaryEmployer>true</IsPrimaryEmployer>
        <JobTitle>Editor in Chief</JobTitle>
        <OutletId>5210</OutletId>
        <Role>
          <Id>8</Id>
          <Name>Editor</Name>
        </Role>
        <TypeName>Staff</TypeName>
        <YearEnd>0</YearEnd>
        <YearStart>2004</YearStart>
      </Employment>
    </EmploymentDetails>
    <OutletId>0</OutletId>
    <WorkingLanguages>
      <Language>
        <Id>175</Id>
        <Name>English</Name>
      </Language>
    </WorkingLanguages>
    <Books />
    <DayBirth>0</DayBirth>
    <Deceased>false</Deceased>
    <EducationDetails />
    <Gender>Male</Gender>
    <HomeCity>
      <Id>0</Id>
    </HomeCity>
    <HomeCountry>
      <Id>0</Id>
    </HomeCountry>
    <HomeState>
      <Id>0</Id>
    </HomeState>
    <LastArticleWrittenDate>
    0001-01-01T00:00:00</LastArticleWrittenDate>
    <MonthBirth>0</MonthBirth>
    <NNID>256885</NNID>
    <NameVariations />
    <ProprietaryInfoID>0</ProprietaryInfoID>
    <SocialNetworks />
    <YearBirth>0</YearBirth>
  </Author>
</AuthorByIdResponse>

```

http://api.beta.dowjones.com/api/Public/2.0/Author/id/json?id=1089207&sessionId=YourSessionId

```json
{
    "Author": {
        "FirstName": "Adam",
        "Id": 709596,
        "LastName": "Moss",
        "Address": {
            "City": {
                "Id": 24655,
                "Name": "New York"
            },
            "Country": {
                "Id": 256,
                "Name": "United States"
            },
            "Id": 307683,
            "Line1": "75 Varick Street",
            "PostOrZip": "10013",
            "State": {
                "Id": 346,
                "Name": "New York"
            }
        },
        "Biography": "http://en.wikipedia.org/wiki/Adam_Moss",
        "Contacts": [],
        "EmploymentDetails": [
            {
                "Contacts": [
                    {
                        "Type": 5,
                        "TypeName": "Telephone, Office, Department",
                        "Value": "+1 (212) 508-0700"
                    },
                    {
                        "Type": 1,
                        "TypeName": "Email, Work",
                        "Value": "adam_moss@newyorkmag.com"
                    }
                ],
                "DateCreated": "/Date(-62135578800000-0500)/",
                "DateUpdated": "/Date(-62135578800000-0500)/",
                "Email": "adam_moss@newyorkmag.com",
                "Id": 3546658,
                "IsPrimaryEmployer": true,
                "JobTitle": "Editor in Chief",
                "OutletId": 5210,
                "Role": {
                    "Id": 8,
                    "Name": "Editor"
                },
                "TypeName": "Staff",
                "YearEnd": 0,
                "YearStart": 2004
            }
        ],
        "OutletId": 0,
        "WorkingLanguages": [
            {
                "Id": 175,
                "Name": "English"
            }
        ],
        "Books": [],
        "DayBirth": 0,
        "Deceased": false,
        "EducationDetails": [],
        "Gender": 1,
        "HomeCity": {
            "Id": 0
        },
        "HomeCountry": {
            "Id": 0
        },
        "HomeState": {
            "Id": 0
        },
        "LastArticleWrittenDate": "/Date(-62135578800000-0500)/",
        "MonthBirth": 0,
        "NNID": 256885,
        "NameVariations": [],
        "ProprietaryInfoID": 0,
        "SocialNetworks": [],
        "YearBirth": 0
    }
}

```

 

### URL (GET)

http://api.beta.dowjones.com/api/Public/2.0/Author/id/xml?id=1089207&sessionId=YourSessionId

### Response


```xml
<AuthorByIdResponse>
  <Author>
    <FirstName>Adam</FirstName>
    <Id>709596</Id>
    <LastName>Moss</LastName>
    <Address>
      <City>
        <Id>24655</Id>
        <Name>New York</Name>
      </City>
      <Country>
        <Id>256</Id>
        <Name>United States</Name>
      </Country>
      <Id>307683</Id>
      <Line1>75 Varick Street</Line1>
      <PostOrZip>10013</PostOrZip>
      <State>
        <Id>346</Id>
        <Name>New York</Name>
      </State>
    </Address>
    <Biography>http://en.wikipedia.org/wiki/Adam_Moss</Biography>
    <Contacts />
    <EmploymentDetails>
      <Employment>
        <Contacts>
          <Contact>
            <Type>PhoneOutlet</Type>
            <TypeName>Telephone, Office, Department</TypeName>
            <Value>+1 (212) 508-0700</Value>
          </Contact>
          <Contact>
            <Type>EmailWork</Type>
            <TypeName>Email, Work</TypeName>
            <Value>adam_moss@newyorkmag.com</Value>
          </Contact>
        </Contacts>
        <DateCreated>0001-01-01T00:00:00</DateCreated>
        <DateUpdated>0001-01-01T00:00:00</DateUpdated>
        <Email>adam_moss@newyorkmag.com</Email>
        <Id>3546658</Id>
        <IsPrimaryEmployer>true</IsPrimaryEmployer>
        <JobTitle>Editor in Chief</JobTitle>
        <OutletId>5210</OutletId>
        <Role>
          <Id>8</Id>
          <Name>Editor</Name>
        </Role>
        <TypeName>Staff</TypeName>
        <YearEnd>0</YearEnd>
        <YearStart>2004</YearStart>
      </Employment>
    </EmploymentDetails>
    <OutletId>0</OutletId>
    <WorkingLanguages>
      <Language>
        <Id>175</Id>
        <Name>English</Name>
      </Language>
    </WorkingLanguages>
    <Books />
    <DayBirth>0</DayBirth>
    <Deceased>false</Deceased>
    <EducationDetails />
    <Gender>Male</Gender>
    <HomeCity>
      <Id>0</Id>
    </HomeCity>
    <HomeCountry>
      <Id>0</Id>
    </HomeCountry>
    <HomeState>
      <Id>0</Id>
    </HomeState>
    <LastArticleWrittenDate>
    0001-01-01T00:00:00</LastArticleWrittenDate>
    <MonthBirth>0</MonthBirth>
    <NNID>256885</NNID>
    <NameVariations />
    <ProprietaryInfoID>0</ProprietaryInfoID>
    <SocialNetworks />
    <YearBirth>0</YearBirth>
  </Author>
</AuthorByIdResponse>

```


### URL (GET)

http://api.beta.dowjones.com/api/Public/2.0/Author/id/json?id=1089207&sessionId=YourSessionId

### Response


```json
{
    "Author": {
        "FirstName": "Adam",
        "Id": 709596,
        "LastName": "Moss",
        "Address": {
            "City": {
                "Id": 24655,
                "Name": "New York"
            },
            "Country": {
                "Id": 256,
                "Name": "United States"
            },
            "Id": 307683,
            "Line1": "75 Varick Street",
            "PostOrZip": "10013",
            "State": {
                "Id": 346,
                "Name": "New York"
            }
        },
        "Biography": "http://en.wikipedia.org/wiki/Adam_Moss",
        "Contacts": [],
        "EmploymentDetails": [
            {
                "Contacts": [
                    {
                        "Type": 5,
                        "TypeName": "Telephone, Office, Department",
                        "Value": "+1 (212) 508-0700"
                    },
                    {
                        "Type": 1,
                        "TypeName": "Email, Work",
                        "Value": "adam_moss@newyorkmag.com"
                    }
                ],
                "DateCreated": "/Date(-62135578800000-0500)/",
                "DateUpdated": "/Date(-62135578800000-0500)/",
                "Email": "adam_moss@newyorkmag.com",
                "Id": 3546658,
                "IsPrimaryEmployer": true,
                "JobTitle": "Editor in Chief",
                "OutletId": 5210,
                "Role": {
                    "Id": 8,
                    "Name": "Editor"
                },
                "TypeName": "Staff",
                "YearEnd": 0,
                "YearStart": 2004
            }
        ],
        "OutletId": 0,
        "WorkingLanguages": [
            {
                "Id": 175,
                "Name": "English"
            }
        ],
        "Books": [],
        "DayBirth": 0,
        "Deceased": false,
        "EducationDetails": [],
        "Gender": 1,
        "HomeCity": {
            "Id": 0
        },
        "HomeCountry": {
            "Id": 0
        },
        "HomeState": {
            "Id": 0
        },
        "LastArticleWrittenDate": "/Date(-62135578800000-0500)/",
        "MonthBirth": 0,
        "NNID": 256885,
        "NameVariations": [],
        "ProprietaryInfoID": 0,
        "SocialNetworks": [],
        "YearBirth": 0
    }
}

```

 
