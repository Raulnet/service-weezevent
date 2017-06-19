# service-weezevent
- web component service for Weez (v1.2.0*)
- Api documentation can be found [here](https://api.weezevent.com/)

***

##How to use
Access to the API is limited to registered partners of Weezevent. All requests to the API are signed with an identifier string (API key) which is unique for each partner. Please contact Weezevent if you want to obtain an API key for your application.

The API is built on HTTP and is RESTful. By default, all data is returned in JSON format. When it’s possible, data can be returned in XML format.

###Installation
bower
        
    bower install service-weezevent --save

###Required:
    - Weezevent Account registered
    - Api key (provided by weezevent)
    - Access token (generated by service function getAuthAccessToken() )
    

Declare component and his attribute:

        <link rel="import" href="service-weezevent.html">
        <service-weezevent
            id="api"
            api-key="yourAPiKey"
            access-token="yourAccessToken"
            on-response="myHandleResponse"
            params="{{paramsToRequest}}">
        </service-weezevent>
***     
   
###Exemple:      
- 1: to find your accesToken

        <service-weezevent
                id="api"
                api-key="4ger8gt4ergfed18fger45fg">
        </service-weezevent>
        <script>
            var api = document.querySelector('#api');
            api.params = {'username': 'login@email.com', 'password': 'M3g4-P4$$w0rD'};
            api.getAuthAccessToken();
            api.addEventListener('response', function (e) {
                api.accessToken = e.detail.accessToken;
            });
        </script>
     
**Important:** Just use only one time to generate your access token. record it and use it every time. Or just if need to generate a new access token
    
- 2: to find all events of your account

        <service-weezevent
                id="api"
                api-key="4ger8gt4ergfed18fger45fg"
                access-token="fsd854f56s4fsdf54sdf685dsf4s5f">
        </service-weezevent>
        <script>
            var api = document.querySelector('#api');
            api.getEvents();
            api.addEventListener('response', function (e) {
                console.log(e.detail)
            });
        </script>
**Important:** The required params, Access Token and Api Key, are always defined by defaults. You don't need to redefined them
 
3: to find all events of your account

        <service-weezevent
                id="api"
                api-key="4ger8gt4ergfed18fger45fg"
                access-token="fsd854f56s4fsdf54sdf685dsf4s5f">
        </service-weezevent>
        <script>
            var api = document.querySelector('#api');
             api.params = {'id': 12345};
            api.getEventDetails();
            api.addEventListener('response', function (e) {
                console.log(e.detail)
            });
        </script>
...        
***        
###Function/Params
Documentation [here](https://api.weezevent.com/)

**Important:** The required params, Access Token and Api Key, are always defined by defaults. You don't need to redefined them
                                                 
#####getAuthAccessToken() -  Authenticate the user and return his accessTokenKey:   
*   username: string - required: Weezevent organizer or partner login,
*   password: string - required: Weezevent organizer or partner password,
*   api_key: string - required: Your API key

#####getEvents() - List of events to which the user has access:
*   access_token: String - required: API access token
*   api_key: String - required: Your API key
*   id_event: String or Array - required: Id of event
*   display_passed: Boolean - optional : Default false.

#####getDates() - List of dates for one or multiple events
*   access_token: String - required: API access token
*   api_key: String - required: Your API key
*   id_event: String or Array - required: Id of event
*   display_passed: Boolean - optional : Default false.

#####getTickets() - List of price categories for one or multiple events
*   access_token: String - required: API access token
*   api_key: String - required: Your API key
*   id_event: String or Array - required: Id of event

#####getTicketStats() - Return the scan statistic for one price category
*   access_token: String - required: API access token
*   api_key: String - required: Your API key
*   id: String - required: Id of Ticket
*   id_date: String - optional: id of date

#####getParticipants() - Return a list of participants
*   access_token: String - required: API access token
*   api_key: String - required: Your API key
*   id_event: Array - optional
*   id_ticket: Array - optional
*   date_ticket:	Array - optional: associative array of id_date/id_ticket tuples
*   last_update:	String - Date (YYYY-MM-DD HH:MM:SS) - Optional
*   last_update_before:	Date (YYYY-MM-DD HH:MM:SS) - Optional
*   include_deleted:	Boolean - optional - Default is false.
*   moderation: Boolean - optional(beta) - Default is false.
*   include_unpaid: Boolean - optional - Default is false.
*   full: Boolean - optional - Default is false.
*   minimized: Boolean - optional - Default is false.
*   return_count: Boolean - optional
*   return_count_total: Boolean - optional
*   return_removed: Boolean - optional
*   max: Integer - optional
*   page: Integer - optional

#####getParticipantAnswers() - Return the inscription form answers of one participant
*   access_token: String - required: API access token
*   api_key: String - required: Your API key
*   id: String - required: Id of Participant

#####getScanSettings() - Update the settings of the mobile control application
*   access_token: String - required: API access token
*   api_key: String - required: Your API key
                   
#####getScanUser() - Provide a specific name for a control point
*   access_token: String - required: API access token
*   api_key: String - required: Your API key
*   user: String - required: Name of the user

#####getEventDetails() - Return details for specified event
*   access_token: String - required: API access token
*   api_key: String - required: Your API key
*   id: Integer - required: Event ID

#####getEventSearch() - Search for specific events
*   access_token: String - required: API access token
*   api_key: String - required: Your API key
*   date: String - Date (YYYY-MM-DD HH:MM:SS) - optional
*   date_start: String - Date (YYYY-MM-DD HH:MM:SS) - optional
*   date_end: String - Date (YYYY-MM-DD HH:MM:SS) optional
*   category: Integer - optional
*   city: String - optional
*   zip_code: String - optional
*   country: String - optional
*   province: String - optional
*   organizer:	String - optional
*   render: String - optional - json|xml default json
*   max_result: Integer - optional

#####getEventCategories() - List of event categories
*   render: String - optional - json|xml default json

***

License
-------
MIT: http://mit-license.org/

Copyright 2016 Laurent Negre aka Raulnet
    