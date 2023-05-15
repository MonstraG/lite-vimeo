[![npm version](https://badge.fury.io/js/%40justinribeiro%2Flite-youtube.svg)](https://badge.fury.io/js/%40justinribeiro%2Flite-youtube)

# \<lite-youtube\>

> A web component that displays Vimeo embeds faster. Based on Justin Ribeiro's excellent [\<lite-youtube\>](https://github.com/justinribeiro/lite-youtube), which, in turn, is a Shadow DOM version of Paul's [lite-youtube-embed](https://github.com/paulirish/lite-youtube-embed).

This is basically a rebadge of Justin's component, but for Vimeo.

## Features

- No dependencies; it's just a vanilla web component.
- It's fast yo.
- It's Shadow Dom encapsulated!
- It's responsive 16:9
- It's accessible via keyboard and will set ARIA via the `videotitle` attribute
- It's locale ready; you can set the `videoplay` to have a properly locale based label
- Set the `start` attribute to start at a particular place in a video
- You can set `autoload` to use Intersection Observer to load the iframe when scrolled into view.
- Loads placeholder image as WebP with a Jpeg fallback

## Install via package manager

This web component is built with ES modules in mind and is
available on NPM:

To install, use your package manager of choice:

```sh
npm i @slightlyoff/lite-vimeo
# or
yarn add @slightlyoff/lite-vimeo
```

After install, import into your project:

```js
import '@slightlyoff/lite-vimeo';
```

## Install with CDN

If you want the paste-and-go version, you can simply load it via CDN:

```html
<script type="module" src="https://cdn.jsdelivr.net/npm/@slightlyoff/lite-vimeo@0.1.2/lite-vimeo.js">
```

## Basic Usage

```html
<lite-vimeo videoid="364402896"></lite-vimeo>
```

## Basic Usage with Fallback Link

A fallback appears in any of the following circumstances:

1. Before the compontent is initialized
1. When JS is disabled (like `<noscript>`)
1. When JS fails or the lite-youtube script is not loaded/executed
1. When the browser doesn't support web components

```html
<lite-youtube videoid="guJLfqTFfIw">
  <a class="lite-youtube-fallback" href="https://www.youtube.com/watch?v=guJLfqTFfIw">Watch on YouTube: "Sample output of devtools-to-video cli tool"</a>
</lite-youtube>
```

Example CSS:

```css
.lite-youtube-fallback {
	aspect-ratio: 16 / 9; /* matches YouTube player */
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
	gap: 1em;
	padding: 1em;
	background-color: #000;
	color: #fff;
	text-decoration: none;
}

/* right-facing triangle "Play" icon */
.lite-youtube-fallback::before {
	display: block;
	content: '';
	border: solid transparent;
	border-width: 2em 0 2em 3em;
	border-left-color: red;
}

.lite-youtube-fallback:hover::before {
	border-left-color: #fff;
}

.lite-youtube-fallback:focus {
	outline: 2px solid red;
}
```

## Playlist Usage

Setting the YouTube playlistid allows the playlist interface to load on interaction. Note, this still requires a videoid for to load a placeholder thumbnail as YouTube does not return a thumbnail for playlists in the API.

```html
<lite-youtube
  videoid="VLrYOji75Vc"
  playlistid="PL-G5r6j4GptH5JTveoLTVqpp7w2oc27Q9"
></lite-youtube>
```

## Add Video Title

```html
<lite-vimeo
  videoid="364402896"
  videotitle="This is a video title"
></lite-vimeo>
```

## Update interface for Locale

```html
<lite-vimeo
  videoid="364402896"
  videoplay="Mirar"
  videotitle="Mis hijos se burlan de mi español"
></lite-vimeo>
```

## Style It

Height and Width are responsive in the component.

```html
<style>
  .styleIt {
    width: 400px;
    margin: auto;
  }
</style>
<div class="styleIt">
  <lite-vimeo videoid="364402896"></lite-vimeo>
</div>
```

## Set a video start time

```html
<!-- Start at 5 min, 30 seconds -->
<lite-vimeo videoid="364402896" start="5m30s"></lite-vimeo>
```

## AutoLoad with IntersectionObserver

Uses Intersection Observer if available to automatically load the Vimeo iframe when scrolled into view.

```html
<lite-vimeo videoid="364402896" autoload></lite-vimeo>
```

## Auto Play (requires AutoLoad)

```html
<lite-vimeo videoid="364402896" autoload autoplay></lite-vimeo>
```

## Set a video start time

```html
<!-- Start at 5 seconds -->
<lite-youtube videoid="guJLfqTFfIw" videoStartAt="5"></lite-youtube>
```

## Fine tune the poster quality for a video

```html
<lite-youtube
  videoid="guJLfqTFfIw"
  posterquality="maxresdefault"
></lite-youtube>
```

## YouTube QueryParams

Use any [YouTube Embedded Players and Player Parameters](https://developers.google.com/youtube/player_parameters) you like.

> Note: the exception to this rule is the autoplay param; because of the nature of the performance loading and the inconsistency of usage, that parameter generally does not work. See [this comment](https://github.com/justinribeiro/lite-youtube/issues/66#issuecomment-1182110925) for details.

```html
<lite-youtube videoid="guJLfqTFfIw" params="controls=0&enablejsapi=1">
</lite-youtube>
```


## Attributes

The web component allows certain attributes to be give a little additional
flexibility.

| Name           | Description                                                      | Default |
| -------------- | ---------------------------------------------------------------- | ------- |
| `videoid`      | The YouTube videoid                                              | ``      |
| `playlistid`   | The YouTube playlistid; requires a videoid for thumbnail         | ``      |
| `videotitle`   | The title of the video                                           | `Video` |
| `videoplay`    | The title of the play button (for translation)                   | `Play`  |
| `videoStartAt` | Set the point at which the video should start, in seconds        | `0`     |
| `posterquality`| Set thumbnail poster quality (maxresdefault, sddefault, mqdefault, hqdefault) | `hqdefault`  |
| `posterloading`| Set img lazy load attr `loading` for poster image | `lazy`  |
| `nocookie`     | Use youtube-nocookie.com as iframe embed uri | `false` |
| `autoload`     | Use Intersection Observer to load iframe when scrolled into view | `false` |
| `short`     | Show 9:16 YouTube Shorts-style interaction on mobile devices | `false` |
| `params`       | Set YouTube query parameters                                     | ``      |

## Events

The web component fires events to give the ability understand important lifecycle.

| Event Name     | Description                                                      | Returns |
| -------------- | ---------------------------------------------------------------- | ------- |
| `liteYoutubeIframeLoaded` | When the iframe is loaded, allowing us of JS API  | `detail: { videoId: this.videoId }` |

| Name         | Description                                                      | Default |
| ------------ | ---------------------------------------------------------------- | ------- |
| `videoid`    | The Vimeo videoid                                              | ``      |
| `videotitle` | The title of the video                                           | `Video` |
| `videoplay`  | The title of the play button (for translation)                   | `Play`  |
| `autoload`   | Use Intersection Observer to load iframe when scrolled into view | `false` |
| `autoplay`   | Video attempts to play automatically if auto-load set and browser allows it | `false` |
| `start`      | Set the point at which the video should start, in seconds        | `0`     |
