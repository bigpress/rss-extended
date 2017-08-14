# RSS Extended

The WXR format is based on the Really Simple Syndication or RSS. Originally created to import and export Wordpress websites but without any kind of documentation we have adopted it and formalized it.


## Version 1.3 Draft



**<title>** Contains the title of the site.


**<link>** Is the URL of the site as determined by WordPress.


**<description>** Is a tagline that can be modified in the Dashboard under Settings, General Settings, Tagline General Settings.


**<pubDate>** Was the time and date that the WXR document was created. It is in the RFC-822 format http://asg.web.cmu.edu/rfc/rfc822.html as required by the Rss standard. The format should be self explanatory except for the last numeric value which represents the local differential from GMT using a +/-hhmm format. Plus 2 hours from GMT would be represented as +0200. The WordPress time zone can be changed in the Dashboard under Settings, General Settings, Timezone General Settings, Timezone.


**<language>** Is the primary language the site is written in as determined by Settings, General Settings, Language in the WordPress Dashboard. A list of valid codes used to represent the language can be found at http://www.rssboard.org/rss-language-codes.


**<wp:wxr_version>** This is our first example of an extended Rss element. We can recognise that it does not belong to the Rss specification as the element contains a colon. Left of the colon contains the elements extension while right is the element name. wp:wxr_version is the version number for the WordPress extension Rss. At the last update to this article in December 2013 the version number was at 1.2.


**<wp:base_site_url>** Is the root URL  of the WordPress hosting provider.


**<wp:base_blog_url>** Is the root URL of the WordPress site.


**<wp:next_page>** URL of the next page


**<wp:category>** Each container holds information on a category used by the site for the classification of posts. Contains a complete collection of categories associated with the blog. You can view and edit the list within the WordPress Dashboard under Posts, Categories. Each category is given its own <category> element and contains the following 3 4 child elements.
<wp:term_idname> Is a unique numeric identifier assigned by WordPress to this category. It is found in URL strings that reference this category.


**<wp:category_nicename>** Is the category name in a URL friendly format.


**<wp:category_parent>** If the category belongs to a hierarchy then the parent category is listed.


**<wp:cat_name>**<![CDATA[]]> The original name of the category contained within an unparsed character data enclosure.


**<wp:tag>** Contains a complete collection of the tags assigned to posts. You can view and edit the tags within the Dashboard under Posts, Posts Tags. It contains the following 2 3 child elements.


**<wp:term_idname>**Is a unique numeric identifier assigned by WordPress to this tag. It is found in URL strings that reference this tag.


**<wp:tag_slug>** Is the URL friendly name of the tag.


**<wp:tag_name>** Is the original name of the tag contained within an unparsed character data enclosure.


**<generator>** Is the name or a URL pointing to the homepage of the application that was used to create the Rss document.

**<cloud>** Is a pointer to the RssCloud API which is a blog monitoring service supported by WordPress.com. It enables a supporting client to receive instant notification when the blog is updated. http://www.rssboard.org/rsscloud-interface


**<image>** Is a logo belonging to the site that can be displayed by Rss clients. You can modify the logo under the General Settings, Blog Picture / Icon dialog in the Dashboard under Settings, General, Big Picture / Icon. There are strict size and image formats requirements imposed by the Rss standard. http://www.rssboard.org/rss-specification#ltimagegtSubelementOfLtchannelgt


**<atom:link rel="search">** Is a URL pointing to the Open Search description document supplied by WordPress. It enables supported Rss clients and web browsers an easy means to provide search terms to the blog and receive results in a standardised XML format. http://www.opensearch.org/Specifications/OpenSearch/1.1#OpenSearch_description_document


**<atom:link rel="pub">** Is a URL pointing to the Google designed pubsubhubbub notification service that is supported by WordPress. In my opinion this is easier to implement and use then the alternative <cloud> service that offers similar functionality. http://code.google.com/p/pubsubhubbub/

That is the end of the Rss metadata related elements. Below are the list of child elements contained within the <item></item> elements. Items are repeated multiple times as each item holds a single blog post, article or page. Items contain the details of the unique resources used by the WordPress site. These include Posts, Pages and Media.





## The item element


**<title>** Is the Title for a page and a post or the Name for media. Title of the blog post or page.


**<link>** Is the site URL that points to the site page that displays the item. URL to the blog post or page.


**<pubDate>** Time and date the item posted to the site formatted to the RFC 822 specification. that the post was posted online.


**<dc:creator>** Lists the author of the item using the user name found in <wp:author_login> post. The element is a Dublin Core Rss extension as the Rss specification doesn’t contain any suitable elements for this role.


**<guid>** Is the globally unique identifier used for the identification of the blog post item by Rss and WordPress clients. The isPermaLink=false attribute just means according to the Rss standard should mean that this identifier is not a legitimate website URL and is not usable in a web browser. Though in WXR the URLs are valid and point to the asset.


**<description>** In Rss documents this element contains the synopsis of the item but in WXR it is left blank.


**<content:encoded>** Is the replacement for the restrictive Rss <description> element. Enclosed within a character data enclosure is the complete WordPress formatted blog post or page complete with HTML tags and all. For media this contains the Description which is also formatted in HTML.


**<excerpt:encoded>** This contains a Caption used by media. This is an unknown element. This is a summary or description of the post often used by RSS/Atom feeds.


**<wp:post_id>** This is an auto-incremental, numeric, unique identification number given to each post, article media or page.


**<wp:post_date>** Time and date that the post item was published to the site.


**<wp:post_date_gmt>** Time and date in GMT that the post item was published to the site.


**<wp:comment_status>** A value stating whether public access for posting comments is opened or closed.


**<wp:post_name>** Is a unique, URL friendly nicename based on the post title at the time of the first save.


**<wp:status>** Publish status of the post item with the options;  publish, draft, pending, private, trash, inherit.


**<wp:post_parent>** The numeric identification number if the post’s parent item. I think this is applicable to WordPress pages which can be nested within each other.


**<wp:menu_order>** I assume is related to menu navigation of nested pages.


**<wp:post_type>** Item Post type either post, page, attachment media.


**<wp:post_password>** A non-encrypted password used by WordPress to restrict reading access to the post.


**<wp:is_sticky>** A numeric Boolean value (0 is false, 1 is true) to determine if the post as a sticky. A sticky post means the post will be displayed before all other non-sticky posts.


**<wp:attachment_url>** The URL that points to the media item source. The URL could be used to display in a browser or used in an application to download the media.


**<category>** Each category or tag associated with the item is given 2 category attributes. The domain attribute lists either post_tag or category while the nickname is the URL friendly name. Media items are not given category tags. elements. The first element contains just the category as a name, while the second element contains both the category name and the URL friendly nicename attribute.


**<wp:postmeta>** Are containers for newer additions the WXR document format that have not been given their own WXR tags. have been introduced after the original WXR specification. Each <wp:postmeta> element contains 2 child elements.

**<wp:meta_key>** Is URL friendly reference key for the meta data element.
**<wp:meta_value>** Is the value for the meta data element contained within a character data enclosure.

Below are some of the <wp:meta_key> references currently used by WXR.

delicious; is data related to the Delicious social bookmarking web service. http://www.delicious.com/
geo_latitude; is the positioning location of the author when submitted the post. The value is the latitude in degrees using the World Geodetic System 1984 (WGS84) datum. It seems to be based on the Google Gears Geolocation API. http://code.google.com/apis/gears/api_geolocation.html
geo_longitude; is the positioning location of the author when they submitted the post. The value is the longitude coordinates.
geo_accuracy; is the horizontal accuracy of the above positioning values in metres.
geo_address; is the address determined by the above geolocation data.
geo_public; is a Boolean numeric value that determines if the geolocation data should be displayed in the post.
_wpas_; related tags may have something to do with the WordPress Sharing services.
reddit; is data related to the reddit social news web service. http://www.reddit.com/


**<wp:comment>** Is a child element for the post item that contains 12 13 sub-elements listed below. These sub-elements belong to the a single post comment contained within a <wp:comment> element set.


**<wp:comment_id>** This is an auto-incremental, numeric, unique identification number given to each comment.


**<wp:comment_author>** The name of author who submitted the comment. The name value is contained within an unparsed character data enclosure.


**<wp:comment_author_email>** An e-mail address provided by the author of the comment.


**<wp:comment_author_url>** The URL of the author’s website provided by the author of the comment.


**<wp:comment_author_IP>** The IP address belonging to the author of the comment. The IP address is automatically recorded by WordPress.


**<wp:comment_date>** The date and time local to the blog that the comment was posted.


**<wp:comment_date_gmt>** The date and time at GMT that the comment was posted.


**<wp:comment_content>** The comment text enclosed within a character data enclosure.


**<wp:comment_approved>** A numeric Boolean value to determine if the comment is displayed.


**<wp:comment_type>** The type of comment. If left blank it is classed as a normal comment. A value of pingback or trackback means it is a post request notification link http://en.wikipedia.org/wiki/Trackback.


**<wp:comment_parent>** The numeric identification of the parent comment used when the comment is a response to a pre-existing comment.


**<wp:comment_user_id>** A numeric identification belonging to the author if they were logged in when they submitted the comment.


**<wp:comment_metadata>** Seems to offer additional data much like the earlier <wp:postmeta> tag.


**<wp:wp_author>** Contains details on the authors of the site. Each author gets their own wp_author container.


**<wp:relateds>** Container for related items







```xml
<rss version="2.0" xmlns:media="http://search.yahoo.com/mrss/" xmlns:dcterms="http://purl.org/dc/terms/" xmlns:fh="http://purl.org/syndication/history/1.0">
    <channel>
        <title>LBC</title>
        <link>http://www.lbc.co.uk</link>
        <description>LBC Videos</description>
        <item>
            <guid isPermaLink="false">g4cDQxYjE6qFqPb0VDWqYFbLxcp8-4R2</guid>
            <title>May's Dinner With Juncker: The Inside Story</title>
            <description>This is the alarming inside story of Theresa May's first dinner with EU President Jean-Claude Juncker.</description>
            <link>http://cf.c.ooyala.com/g4cDQxYjE6qFqPb0VDWqYFbLxcp8-4R2/DOcJ-FxaFrRg4gtDEwOjFsaTowODE7WX</link>
            <enclosure url="http://cf.c.ooyala.com/g4cDQxYjE6qFqPb0VDWqYFbLxcp8-4R2/DOcJ-FxaFrRg4gtDEwOjFsaTowODE7WX" length="3342" type="application/x-shockwave-flash" ></enclosure>
            <media:content url="http://cf.c.ooyala.com/g4cDQxYjE6qFqPb0VDWqYFbLxcp8-4R2/DOcJ-FxaFrRg4gtDEwOjFsaTowODE7WX" type="video/x--flv" 
expression="sample" duration="3342" bitrate="3192" lang="eng" ></media:content>
            <media:title type="plain">May's Dinner With Juncker: The Inside Story</media:title>
            <media:description type="html">This is the alarming inside story of Theresa May's first dinner with EU President Jean-Claude Juncker.</media:description>
            <media:thumbnail url="http://cf.c.ooyala.com/g4cDQxYjE6qFqPb0VDWqYFbLxcp8-4R2/promo317917984" width="1280" height="720" time="3342" ></media:thumbnail>
            <media:category label="Entertainment/Celebrity News">Entertainment/Celebrity News</media:category>
            <media:text>This is the alarming inside story of Theresa May's first dinner with EU President Jean-Claude Juncker.</media:text>
            <media:keywords>LBC,Video Feature,Interview,Over 3 mins,AOL One - LBC,Dailymotion - LBC,</media:keywords>
            <media:activation></media:activation>
            <media:expiration></media:expiration>
            <pubDate>Mon, 01 May 2017 14:32:50 GMT</pubDate>
        </item>
        <next_page>
            <![CDATA[http://api.ooyala.com/v2/syndications/23/feed?pcode=44&page_token=1]]>
        </next_page>
    </channel>
</rss>
```




## Author item
Contained inside a wp:wp_author element


**<wp:author_login>** (optional) Is the author’s WordPress login user name.


**<wp:author_email>** Is the author’s e-mail address associated with their WordPress account.


**<wp:author_display_name>** Is the author’s public display name used in instead of the login user name for comments and posts.


**<wp:author_first_name>** Is the author’s first name.


**<wp:author_last_name>** Is the author’s last name.






## Related item
Contained inside a wp:relateds element


**<wp:related>** Container for one related element. It's quivalent of one <item> element


**<wp:type>** Type of the related content. Can be video, article, poll, photo, album, etc.


**<wp:title>** Title of the realted content


**<wp:link>** URL for the related content





## The article type

**<wp:type>** (optional) Value must be "article"


**<wp:subtitle>** Subtitle for news websites


**<wp:antetitle>** Antetitle for news websites





## The poll type

**<wp:type>** (optional) Value must be "poll" for this type


**<wp:poll>** Subtitle for news websites


**<wp:poll_question>** Container for a poll question


**<wp:poll_option_text>** Text answer for the poll option


**<wp:poll_option_color>** Color answer for the poll option


**<wp:poll_option_votes>** Poll option container




## The album type

**<wp:type>** (optional) Value must be "album"




## The photo type


**<wp:type>** Value must be "photo" for this type


**<wp:url>** (required) The source URL of the image. Consumers should be able to insert this URL into an <img> element. Only HTTP and HTTPS URLs are valid.


**<wp:width>** (required) The width in pixels of the image specified in the url parameter.


**<wp:height>** (required) The height in pixels of the image specified in the url parameter.



```xml
<rss version="2.0" xmlns:media="http://search.yahoo.com/mrss/" xmlns:dcterms="http://purl.org/dc/terms/" xmlns:fh="http://purl.org/syndication/history/1.0">
    <channel>
        <title>LBC</title>
        <link>http://www.lbc.co.uk</link>
        <description>LBC Videos</description>
        <item>
           <wp:type>photo</wp:type>
           <wp:width>240</wp:width>
           <wp:height>160</wp:height>
           <wp:title>ZB8T0193</wp:title>
           <wp:contenturl>http://farm4.static.flickr.com/3123/2341623661_7c99f48bbf_m.jpg</wp:contenturl>
           <wp:author_name>Bees</wp:author_name>
           <wp:author_url>http://www.flickr.com/photos/bees/</wp:author_url>
           <wp:provider_name>Flickr</wp:provider_name>
           <wp:provider_url>http://www.flickr.com/</wp:provider_url>
        </item>
    </channel>
</rss>
```





## The link type

**<wp:type>** Value must be "link"

**<wp:externalurl>** URL of the content




## The video type

**<wp:type>** Value must be "video"


**<wp:width>** (required) The width in pixels required to display the video


**<wp:height>** (required) The height in pixels required to display the video


**<wp:contenturl>** URL of the content. In this case a video file


**<wp:provider_name>** Name of the provider


**<wp:provider_url>** URL of the provider


```xml
<rss version="2.0" xmlns:media="http://search.yahoo.com/mrss/" xmlns:dcterms="http://purl.org/dc/terms/" xmlns:fh="http://purl.org/syndication/history/1.0">
    <channel>
        <title>LBC</title>
        <link>http://www.lbc.co.uk</link>
        <description>LBC Videos</description>
        <item>
           <wp:type>video</wp:type>
           <wp:width>240</wp:width>
           <wp:height>160</wp:height>
           <wp:title>ZB8T0193</wp:title>
           <wp:contenturl>http://farm4.static.flickr.com/3123/2341623661_7c99f48bbf_m.mp4</wp:contenturl>
           <wp:author_name>Bees</wp:author_name>
           <wp:author_url>http://www.flickr.com/photos/bees/</wp:author_url>
           <wp:provider_name>Flickr</wp:provider_name>
           <wp:provider_url>http://www.flickr.com/</wp:provider_url>
        </item>
    </channel>
</rss>
```



