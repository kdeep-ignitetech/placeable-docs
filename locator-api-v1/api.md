Placeable Locator API v1
==============



## Resource 

**GET /v1/search?q=colorado+springs**

## Details

This method returns a list of locations found by searching around the location specified in the q paramter.

## Query Parameters


sortOrder

Required: false

Options: “Distance, NameAZ, NameZA”


Description:
• Distance is the distance from the point where “q” is geocoded.
• NameAZ is the results ordered by name in descending order
• NameZA is the results ordered by name in ascending order


Example:
/v1/search?q=Denver%20CO&sortOrder=NameAZ


filters

Required: false

Options: These are specific to your data.


page

Required: false

Options: Return a different page of the result sets.

Example:

Return the second page 
/v1/search?q=Denver%20CO&sortOrder=NameAZ&page=2




Description:
These are specific to your data and will filter in specific results. If your data has
“atmLanguages” with the options of “english, french and spanish” and you want to filter
in only “english” locations the URL would look like:
/search?q=Denver%20CO&filters=atmLanguages-­‐_-­‐english
and if you’d like to filter in english and spanish the url would look like:
/search?q=Denver%20CO&filters=atmLanguages-­‐_-­‐english-­‐_-­‐spanish
As you can see the _-­‐_ is the delimiter between filter/value pairs.


Example:
/v1/search?q=Denver%20CO&filters=atmLanguages-­‐_-­‐spanish_-­‐_atmLanguages-­‐_-­‐french


## HTTP Codes

| Status Code               | Description       |
|:------------------|:------------|
|400      | No key supplied, or bad request     | 
|404      | Couldn't find  search origin given the q parameter      |




    
### Response Details

The response consists of location data, and results. The location section contains information about where the search was carried out, and the results section contains the list of results that were found plus some metadata about the result set.

__Location__

        "searched": {
            "adminDistrict": "CO", 
            "country": "United States", 
            "entityType": "Address", 
            "formattedAddress": "2601 Blake St, Denver, CO 80205", 
           	"locality": "Denver", 
            "latitude": 39.7603645324707, 
            "longitude": -104.987144470215, 
            "street": "2601 Blake St"
        }
        
| Key               | Value       |
|:------------------|:------------|
|adminDistrict      | State     | 
|country            | Country     | 
|entityType         | Type of location returned e.g address, city, state, country  |
|formattedAddress | Representaton of the address found | 
|locality | City|
|latitude | Latitude | 
|longtitude| Longtitude |
|street| Street|
  
  It is possible that some of the above value may be blank given the search supplied. For example you enter Colorado as the search, the search and locality will be blank 


### Paging

Under the results section of the API response there information about paging. The resultCount is the total number of records returned by the search, and the pageCount is the total number of pages. The user can request a different page from the result set by querying with the page parameter (explained above)


### No Results found


Below is an example of a search which returned zero results

		{
		    "location": {
		        "candidates": [], 
		        "searched": {
		            "adminDistrict": "AK", 
		            "country": "United States", 
		            "entityType": "PopulatedPlace", 
		            "formattedAddress": "Nome, AK", 
		            "latitude": 64.49947357177734, 
		            "locality": "Nome", 
		            "longitude": -165.40579223632812, 
		            "street": ""
		        }
		    }, 
		    "results": {
		        "resultCount": 0, 
		        "results": []
		    }
		}
		




## Full Response

  Below is a full response, for each result any flexible fields which have been loaded during the dataload will be passed directly through.

		    {
			    "location": {
			        "candidates": [], 
			        "searched": {
			            "adminDistrict": "CO", 
			            "country": "United States", 
			            "entityType": "Address", 
			            "formattedAddress": "2601 Blake St, Denver, CO 80205", 
			            "latitude": 39.7603645324707, 
			            "locality": "Denver", 
			            "longitude": -104.987144470215, 
			            "street": "2601 Blake St"
			        }
			    }, 
			    "results": {
			        "distanceUnit": "miles", 
			        "pageCount": 1, 
			        "resultCount": 1, 
			        "sortOrder": "Distance",
			        "results": [
			            {
			                "id": "81341",
			                "city": "DENVER", 
			                "detail.languages": [
			                    "English", 
			                    " Spanish"
			                ], 
			                "detail.services": [
			                    "Bulk Mail Acceptance", 
			                    "Bulk Mail Account Balance", 
			                    "Bulk Mail New Permit", 
			                    "Burial Flags", 
			                    "Business Reply Mail Account Balance", 
			                    "Business Reply Mail New Permit", 
			                    "Duck Stamps"
			                ], 
			                "detailsUrl": "co/denver/81341", 
			                "distance": 1.5261252679006334, 
			                "email": "", 
			                "fax": "303-951-3484", 	           
			                "custom.languages": {
			                    "ENG": "English", 
			                    "SPA": "Spanish"
			                }, 
			                
			                "languages": "English, Spanish", 
			                "lastModified": "Wed, 28 Aug 2013 05:36:43 245 -0600", 
			                "latitude": "39.759108", 
			                "location": "39.759108,-105.015829", 
			                "longitude": "-105.015829", 
			                "name": "Mile High", 
			                "phone": " 303-571-0722", 
			                "result.languages": [
			                    "English", 
			                    " Spanish"
			                ], 
			                "result.services": [
			                    "Bulk Mail Acceptance", 
			                    "Bulk Mail Account Balance", 
			                    "Bulk Mail New Permit", 
			                    "Burial Flags", 
			                    "Business Reply Mail Account Balance", 
			                    "Business Reply Mail New Permit", 
			                    "Duck Stamps"
			                ], 
			                "services":  "Bulk Mail Acceptance,Bulk Mail Account Balance,Bulk Mail New Permit,Burial Flags,Business Reply Mail Account Balance,Business Reply Mail New Permit,Duck Stamps",
			                "state": "CO", 
			                "streetAddress": "450 W 14TH AVE", 
			                "streetAddress2": "", 
			                "type": "Branch", 
			                "webUrl": "http://geocities.com/mileHighLocation", 
			                "zip": "80204-9998"
			            }
			        ]
			        
			    }
			}

