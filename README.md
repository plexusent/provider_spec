# GoWatchIt Affiliate Provider Data Feed Spec

## Purpose
The spec is intended for content owners and distributors to supply information about where consumers can purchase and view film and television content. The spec has both optional and required elements. 

The data is split into two rough categories: _Metadata_ and _Availabilities_

### Metadata
This includes unique industry-wide identifiers such as a ROVI or EIDR ID. It must also include a provider's own unique ID. GWI Can use industry IDs map titles to our canonical database. In the absense of known industry IDs, GoWathIt will use title metadata (Combining elements of Title, Release Date, Language, Director and/or Cast) to match titles to our canonical database. A minimum of title and release year are required, but items such as cast or director are very helpful to help disambiguate titles when there are different properties with the same title. 

### Availabilities. 
This is an optional array of items which specify consumer-relevant information about purchasing and/or viewing the content. GoWatchIt requires a URL in order to send the consumer to purchase, rent, or view the content. For television, attributes such as networks or TV channels may be useful to include. See the spec for detailed information. 

### Feed period
It is advised that the provider gives a FULL snapshot feed every day. This enables us to give the most accurate price to consumers on a daily basis. It is possible to supply a smaller "incremental" feed. If this feed is supplied we will only update/append to our existing snapshot of the provider data. If supplying incremental feeds, it is important to also supply a full feed, at least once a week--again, so that the prices and availabilities remain current. 

## Feed Fields:

 Field Name | Type | Description | Required? 
 -----------|------|-------------|---------
 catalog_provider | String | Name of the content owner. | *
catalog_name | String |  Unique name for feed (to differentiate against multiple feeds). Can be same as catalog_provider | * 
catalog_types    | String[] |Kinds of content in the feed. Acceptable values are: movies, shows, seasons, or episodes | *
catalog_period  | String |  Interval of the feed. Acceptable values are full or incremental. See General section for details. | *
_schema_version  | String | Schema version. Must be: "gwi_json_1.0" | *
items | Object[] | The main object. Each piece of content has its own item in the array. (Array can be empty) | *
items.id | String | Providers unique ID for the content item. | *
items.show_id  | String | Optional reference to a parent show. | | 
items.season_id | String | Optional reference to a parent season. | |
items.title | String | Canonical Title. | *
items.alt_titles | String |  An array of alternate titles. | |
items.type | String |        Type of item. Can be either movie, show, episode, or season. | *
items.release_year | String | Year title was released in original or US market. | * 
items.premier  | String |   Date item premiered. Usually used for TV titles. | |
items.network  | String |   Orignal Network content aired on. Only relveant for TV | |
items.description | String | Synopsis or description of title. | |
items.short_description | String | Shorter version of description. | |
items.url   | String |      Destination URL to send consumers on Provider's site. This should be a deep link, at point of purchase. | |
items.pg_rating | String |  TV or MPAA PG Rating. | |
items.categories | String | Array of Genre's or general categories. (May be used to suggest content to user). | |
items.runtime | Integer | Runtime length of the property. In seconds. | | 
items.contributions Object[] | An array of contributors. You may supply anythign but director and cast are most useful for matching titles | | 
items.contributions.role | String | Type of contribution. We look for either _creator_, _cast_, or _dirctor_. Other roles may be supplied as well. | | 
items.contributions.name | String | Name of the contributor. 
artwork | Object[] | An array of Key art. URLs to the images are expected. | | 
artwork.type | String| Type of art. Values expected are _thumbnail_, _poster_, or _scene | |
artwork.url | String| URL to the image. | | 
language_formats | Object[] | Array of languages and their formats.  | | 
language_formats.type | String | Kind of format either _audio_ or _subtitles_  | | 
language_formats.label | String | Descrition presented to the consumer.  | | 
language_formats.format | String | Relevant encoding format. | | 
language_formats.code | String | International code for language. Ie. _en_ for English. | | 
available_formats | Object[] | Array of availabilities | |
available_formats.delivery_method | String | Specifies method of consumer delivery. We expect either _stream_, _download_, _theatrical, _mail_, or _physical_ | |
available_formats.format | String | Quality of content. Usually _sd_ or _hd_ but provider may specify their own properietary formats. 
available_formats.product_id | String | Partners propietary SKU or ID number | | 
available_formats.product_url | String | URL to direct point of purchase. 
available_formats.availabilities | Object[] | Array of specific availabilies. Mainly rent, buy, or purchase. | |
available_formats.availabilities.offer | String | Kind of offer. We expect either _rent_, _buy_, or _subscription_ | |
available_formats.availabilities.start | String | Date of when content is available for purchase to consumer. | | 
available_formats.availabilities.end | String | Date of when content expires. 
available_formats.availabilities.subscription_required | Boolean| Specifies is subscription is required to view content. | |
available_formats.availabilities.price | Object[] | List of prices in respective currencies.
available_formats.availabilities.price.currency | String | Name of currency. ie. "USD" |  |
available_formats.availabilities.price.price | String | Numerical value of price in respective currency. | | 
----


 
 


### Future updates

* As of now the feed is intended only for US markets. Shortly, the feed will be updated to accomodate availabilities in multiple markets, with multiple prices in their respective currencies. 

