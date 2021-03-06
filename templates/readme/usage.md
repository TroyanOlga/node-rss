## Usage

### Create a new feed

```js
var RSS = require('rss');

var feed = new RSS(feedOptions);
```

#### `feedOptions`

 * `title` **string** Title of your site or feed
 * `description` _optional_ **string** A short description of the feed.
 * `generator` _optional_  **string** Feed generator.
 * `feed_url` **url string** Url to the rss feed.
 * `site_url` **url string** Url to the site that the feed is for.
 * `image_url` _optional_  **url string** Small image for feed readers to use.
 * `docs` _optional_ **url string** Url to documentation on this feed.
 * `managingEditor` _optional_ **string** Who manages content in this feed.
 * `webMaster` _optional_ **string** Who manages feed availability and technical support.
 * `copyright` _optional_ **string** Copyright information for this feed.
 * `language` _optional_ **string**  The language of the content of this feed.
 * `categories` _optional_ **array of strings**  One or more categories this feed belongs to.
 * `lastBuildDate` _optional_ **Date string** The publication date for content in the feed. Only taken into consideration if feed.xml is called with 'isCustomDate: true'
 * `pubDate` _optional_ **Date object or date string** The publication date for content in the feed
 * `ttl` _optional_ **integer** Number of minutes feed can be cached before refreshing from source.
 * `hub` _optional_ **PubSubHubbub hub url** Where is the PubSubHub hub located.
 * `custom_namespaces` _optional_ **object** Put additional namespaces in <rss> element (without 'xmlns:' prefix)
 * `custom_elements` _optional_ **array** Put additional elements in the feed (node-xml syntax)

### Add items to a feed

An item can be used for a blog entry, project update, log entry, etc.  Your RSS feed
can have any number of items. Most feeds use 20 or fewer items.

```js
feed.item(itemOptions);
```

#### itemOptions

 * `title` **string** Title of this particular item.
 * `description` **string** Content for the item.  Can contain html but link and image urls must be absolute path including hostname.
 * `url` **url string** Url to the item. This could be a blog entry.
 * `guid` _optional_ **unique string** A unique string feed readers use to know if an item is new or has already been seen.
 If you use a guid never change it.  If you don't provide a guid then your item urls must
 be unique. If guid is not specified, however `item.link` is a truthy value, guid will be created utilizing `item.url` value. If neither guid nor link is provided, guid will be omitted during xml creation
 * `link` _optional_ **boolean or string** Can be provided for guid creation based on url
 * `categories` _optional_ **array of strings** If provided, each array item will be added as a category element
 * `author` _optional_  **string**  If included it is the name of the item's creator.
 If not provided the item author will be the same as the feed author.  This is typical
 except on multi-author blogs.
 * `date` **Date object or date string** The date and time of when the item was created.  Feed
 readers use this to determine the sort order. Some readers will also use it to determine
 if the content should be presented as unread.
 * `lat` _optional_ **number** The latitude coordinate of the item.
 * `long` _optional_ **number** The longitude coordinate of the item.
 * `custom_elements` _optional_ **array** Put additional elements in the item (node-xml syntax)
 * `enclosure` _optional_ **object** An enclosure object
    ```js
    /* enclosure takes url or file key for the enclosure object

      url:  _required_ url to file object (or file)
      file: _required_ path to binary file (or url)
      size: _optional_ size of the file
      type: _optional_ if not provided the mimetype will be guessed
                       based on the extension of the file or url,
                       passing type to the enclosure will override the guessed type
    */

    {
      'url'  : 'http://www.example.com/path/to/image',
      'size' : 1668, //
      'type' : 'image/jpeg'
    }

    ```
#### Feed XML

```js
var xml = feed.xml({indent: true, isCustomDate: true});
```

This returns the XML as a string.

`indent` _optional_ **boolean or string** What to use as a tab. Defaults to no tabs (compressed).
For example you can use `'\t'` for tab character, or `'  '` for two-space tabs. If you set it to
`true` it will use four spaces.
`isCustomDate` _optional_ **boolean** If dates should be displayed in custom format, for example following can be provided: `'item.date: moment().format('ddd, DD MMM YYYY HH:mm:ss ZZ')'`
