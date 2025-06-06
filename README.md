# Supadata JS SDK

[![NPM package](https://img.shields.io/npm/v/@supadata/js.svg?branch=main)](https://www.npmjs.com/package/@supadata/js)
[![MIT license](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat)](http://opensource.org/licenses/MIT)

The official TypeScript/JavaScript SDK for Supadata.

Get your free API key at [supadata.ai](https://supadata.ai) and start scraping data in minutes.

## Installation

```bash
npm install @supadata/js
```

## Usage

```typescript
import {
  Crawl,
  CrawlJob,
  Map,
  Scrape,
  Supadata,
  Transcript,
  YoutubeChannel,
  YoutubePlaylist,
  YoutubeVideo,
} from '@supadata/js';

// Initialize the client
const supadata = new Supadata({
  apiKey: 'YOUR_API_KEY',
});

// Get YouTube transcript
const transcript: Transcript = await supadata.youtube.transcript({
  url: 'https://youtu.be/dQw4w9WgXcQ',
});

// Translate YouTube transcript
const translated: Transcript = await supadata.youtube.translate({
  videoId: 'dQw4w9WgXcQ',
  lang: 'es',
});

// Get a YouTube Video metadata
const video: YoutubeVideo = await supadata.youtube.video({
  id: 'dQw4w9WgXcQ', // can be url or video id
});

// Get a YouTube channel metadata
const channel: YoutubeChannel = await supadata.youtube.channel({
  id: 'https://youtube.com/@RickAstleyVEVO', // can be url, channel id, handle
});

// Get a list of video IDs from a YouTube channel
const channelVideos: VideoIds = await supadata.youtube.channel.videos({
  id: 'https://youtube.com/@RickAstleyVEVO', // can be url, channel id, handle
  type: 'all', // 'video', 'short', 'all'
  limit: 10,
});

// Get the metadata of a YouTube playlist
const playlist: YoutubePlaylist = await supadata.youtube.playlist({
  id: 'PLFgquLnL59alCl_2TQvOiD5Vgm1hCaGSI', // can be url or playlist id
});

// Get a list of video IDs from a YouTube playlist
const playlistVideos: VideoIds = await supadata.youtube.playlist.videos({
  id: 'https://www.youtube.com/playlist?list=PLlaN88a7y2_plecYoJxvRFTLHVbIVAOoc', // can be url or playlist id
  limit: 10,
});

// Scrape web content
const webContent: Scrape = await supadata.web.scrape('https://supadata.ai');

// Map website URLs
const siteMap: Map = await supadata.web.map('https://supadata.ai');

// Crawl website
const crawl: Crawl = await supadata.web.crawl({
  url: 'https://supadata.ai',
  limit: 10,
});

// Get crawl job results
const crawlResults: CrawlJob = await supadata.web.getCrawlResults(crawl.jobId);
```

## Error Handling

The SDK throws `SupadataError` for API-related errors. You can catch and handle these errors as follows:

```typescript
import { SupadataError } from '@supadata/js';

try {
  const transcript = await supadata.youtube.transcript({
    videoId: 'INVALID_ID',
  });
} catch (e) {
  if (e instanceof SupadataError) {
    console.error(e.error); // e.g., 'video-not-found'
    console.error(e.message); // Human readable error message
    console.error(e.details); // Detailed error description
    console.error(e.documentationUrl); // Link to error documentation (optional)
  }
}
```

## Example

See the [example](./example) directory for a simple example of how to use the SDK.

## API Reference

See the [Documentation](https://supadata.ai/documentation) for more details on all possible parameters and options.

## License

MIT
