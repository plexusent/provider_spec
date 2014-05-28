# GoWatchIt Affiliate Provider Data Feed Spec

## Purpose
The spec is intended for content owners and distributors to supply information about where consumers can purchase and view film and telivision content. The spec has both optional and required elements. 

The data is split into two rough categories: _Metadata_ and _Availabilities_

### Metadata
This includes unique industry-wide identifiers such as a ROVI or EIDR ID. It must also include a provider's own unique ID. GWI Can use industry IDs map titles to our canonical database. In the absense of known industry IDs, GWI will use title metadata (Combining elements of Title, Release Date, Language, Director and/or Cast) to match titles to our canonical database. A minimum of title and release year are required, but items such as cast or director are very helpful to help disambiguate titles when there are different properties with the same title. 

### Availabilities. 
This is an optional array of items which specify consumer relevant information about the purchasing and/or viewing the content. We require some URL in order to send the consumer on relevant platforms. On other platforms, things like network or TV channel may used. See the spec for detailed information. 

## Feed Fields:

 Field Name | Type | Description | Required? 
 -----------|------|-------------|---------
 catalog_provider | String | Name of the content owner. | *
catalog_name | String     Unique name for feed (to differentiate against multiple feeds). Can be same as catalog_provider | * 
catalog_types    | String[] |Kinds of content in the feed. Acceptable values are: movies, shows, seasons, or episodes | *

----



 * @apiSuccess {String[]}   
 * @apiSuccess {String}     catalog_period    Interval of the feed. Acceptable values are full or incremental. See General section for details.  REQUIRED
 * @apiSuccess {String}     _schema_version   Schema version. Must be: "gwi_json_1.0" REQUIRED
 * @apiSuccess {Object[]}   items             The main object. Each piece of content has its own item in the array. REQUIRED
 * @apiSuccess {String}     items.id          Providers unique ID for the content item. REQUIRED
 * @apiSuccess {String}     items.title       Canonical Title. REQUIRED
 * @apiSuccess {String[]}   items.alt_titles  An array of alternate titles. OPTIONAL
 * @apiSuccess {String}     items.type        Type of item. Can be either movie, show, episode, or season. REQUIRED
 * @apiSuccess {String}     items.release_year  Year title was released in original or US market. REQUIRED
 * @apiSuccess {String}     items.premier     Date item premiered. Usually used for TV titles. OPTIONAL
 * @apiSuccess {String}     items.network     Orignal Network content aired on. Only relveant for TV OPTIONAL
 * @apiSuccess {String}     items.description Synopsis or description of title. OPTIONAL
 * @apiSuccess {String}     items.short_description Shorter version of description. OPTIONAL
 * @apiSuccess {String}     items.url         Destination URL to send consumers on Provider's site. This should be a deep link, at point of purchase. REQUIRED
 * @apiSuccess {String}     items.pg_rating   TV or MPAA PG Rating. OPTIONAL
 * @apiSuccess {String[]}   items.categories  Array of Genre's or general categories. (May be used to suggest content to user) OPTIONAL
 * @apiSuccess {Object[]}   items.restrictions Array of valid and invalid markets. 
 * 


