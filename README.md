[media-docs]:		http://docs.brightcove.com/en/media/
[media-docs-tokens]:		http://support.brightcove.com/en/video-cloud/docs/managing-media-api-tokens

[analytics-api-docs]:	http://docs.brightcove.com/en/video-cloud-analytics-api/


node-brightcove
=============================

This humble library aims to be a simple facade over Brigthcove's server APIs.  As Brightcove adds APIs or the mob demands additional functionality, it will be added here.

- [Installation](#installation)
- [Media API](#media-api)
    - [Calls](#media-api-calls)
    - [Options](#media-api-options)
    - [Events](#media-api-events)
- [Analytics API](#analytics-api) \(not yet implemented\)

<br />

<a id="installation"></a>
Installation
-----------------------------
Installation is handled via [npm](http://npmjs.org):

	$ npm install brightcove

Brightcove offers several response formats, but this library demands JSON responses and, wherever possible, passes them through to you.

<br />
<br />

<a id="media-api"></a>
Media API
----------------------------
The `MediaApi` object acts as the facade for all of the [Media API's calls and options][media-docs]. 

It is instance-based, allowing you to juggle more than one [Brightcove Token][media-docs-tokens], if needed.

	var brightcove = require('brightcove');
	var	mediaApi = new brightcove.MediaApi('myTokenOfAwesomeness');

<br />

<a id="media-api-calls"></a>
#### Calls ####
Brightcove breaks up its Media API calls between Videos (read/write) and Playlists (read/write).  For organizational purposes, that's how they're listed here:

- Video Read API
	- **findAllVideos** (options, _callback_)
	- **findAllVideos** ()
	- **findVideoById** ()
	- **findVideosByIds** ()
	- **findRelatedVideos** ()
	- **findVideoByReferenceId** ()
	- **findVideosByReferenceIds** ()
	- **searchVideos** ()

- Playlist Read API
	- **findAllPlaylists** ()
	- **findPlaylistById** ()
	- **findPlaylistsByIds** ()
	- **findPlaylistByReferenceId** ()
	- **findPlaylistsByReferenceIds** ()

- Video Write API

- Playlist Write API
	- **createPlaylist** ()
	- **updatePlaylist** ()
	- **deletePlaylist** ()

<br />

<a id="media-api-options"></a>
#### Options ####

<br />

<a id="media-api-events"></a>
#### Events ####
The `MediaApi` object inherits from node's Event Emitter, allowing you to more easily manage callbacks.  

	// Abstracted handler
	var findAllVideosHandler = function(err, jsonResponse) {
		console.log(jsonResponse);
	}

	// Register the handler
	mediaApi.on('findAllVideos', findAllVideosHandler);

	// Make the call.
	mediaApi.findAllVideos(mediaApi.withDefaultOptions());

All events are emitted with two arguments: `err, jsonResponse`.  Following node convention, the `err` argument will be null if no error occurred as will `jsonResponse` if an error _did_ occur.

**Emitted events** will have a name in congruence with Brightcove's own command names:

- Video Read API
	- `find_all_videos`
	- `find_video_by_id`
	- `find_videos_by_ids`
	- `find_related_videos`
	- `find_video_by_reference_id`
	- `find_videos_by_reference_ids`
	- `search_videos`

- Playlist Read API
	- `find_all_playlists`
	- `find_playlist_by_id`
	- `find_playlists_by_ids`
	- `find_playlist_by_reference_id`
	- `find_playlists_by_reference_ids`

- Video Write API _(not yet implemented)_

- Playlist Write API
	- `create_playlist`
	- `update_playlist`
	- `delete_playlist`

IF you'd like a _programmatic_ or _intellisense-friendly_ access to these, they can be accessed with the `commands` property:  

	// Register the handler using the 'commands' enum
	mediaApi.on(mediaApi.commands.find_all_videos, findAllVideosHandler);

	// Make the call.
	mediaApi.findAllVideos(mediaApi.withDefaultOptions());

<br />
<br />

<a id="analytics-api"></a>
Analytics API
----------------------------
Brightcove's analytics API is currently in beta.  Expect it here, soon!

<br />
<br />

Useful Links
--------------
 - [Brightcove Media API Reference][media-docs]
 - [Brightcove Video Cloud Analytics API Reference][analytics-api-docs]



<!---
Currently supported calls: 
// Video Read APIs
	find_all_videos: 'find_all_videos',
	find_video_by_id: 'find_video_by_id',
	find_videos_by_ids: 'find_videos_by_ids',
	find_related_videos: 'find_related_videos',
	find_video_by_reference_id: 'find_video_by_reference_id',
	find_videos_by_reference_ids: 'find_videos_by_reference_ids',
	search_videos: 'search_videos',

	// Playlist Read APIs
	find_all_playlists: 'find_all_playlists',
	find_playlist_by_id: 'find_playlist_by_id',
	find_playlists_by_ids: 'find_playlists_by_ids',
	find_playlist_by_reference_id: 'find_playlist_by_reference_id',
	find_playlists_by_reference_ids: 'find_playlists_by_reference_ids',

	// Video Write APIs

	// Playlist Write APIs
	create_playlist: 'create_playlist',
	update_playlist: 'update_playlist',
	delete_playlist: 'delete_playlist'

// Example usage of Options
/*
api.findAllVideos(api.withOptions()
	.includingCountOfItems()
	.havingPageSizeOf(10)
	.atPage(2)
	.inAscendingOrder()
	.inDescendingOrder()
	.sortingBy()
		.publishDate() or
		.creationDate() or
		.modifiedDate() or
		.totalPlays() or
		.totalPlaysOfLastWeek()
	.withCustomFields(Array)
	.includingField().videoId()
	.includingField().title()
	.includingField().shortDescription()
	.includingField().longDescription()
	.includingField().creationDate()
	.includingField().publishedDate()
	.includingField().lastModifiedDate()
	.includingField().linkUrl()
	.includingField().linkText()
	.includingField().tags()
	.includingField().videoStillUrl()
	.includingField().thumbnailUrl()
	.includingField().referenceId()
	.includingField().duration()
	.includingField().economics()
	.includingField().playsTotal()
	.includingField().playsTrailingWeek()
	.includingField().videoUrl()
	.includingField().renditions()
	.includingField().iOSRenditions()
	.includingField().FLVFullLength()
	.includingField().videoFullLength()

	or
	.includingField().all()

	or
	.includingField().defaults()

	.usingLiveStream()
);
*/ -->