# podcast-feed-hugo

This is a Hugo module that generates a podcast feed.

To publish new episodes of your podcast you need to run the following command:

```bash
$ hugo new podcast/new-espisode-of-my-podcast.md
```

it will create a new ".md" file with these headers:

- **title**
  - title of the episode
  - string field
- **subtitle**
  - subtitle of the episode 
  - string field
- **date**
  - publication date of the episode
  - format YYYY-mm-ddTHH:MM:SS+Z
  - datetime field
- **audio**
  - relative path to the audio file of the episode
  - string field
- **audio_duration**
  - duration of the episode
  - format "HH:MM:SS"
  - string field
- **audio_size**
  - size of the audio file in bytes
  - integer field
- **authors**
  - you can insert multiple authors
  - array of strings
- **images** 
  - relative path to the episode artwork
  - array of strings 
- **series**
  - series name for the episode
  - array of strings
- **podcast_tags**
  - tags for SEO optimizations
  - array of strings
- **episode_type**
  - the episode type
  - accepted values are: "trailer", "bonus", "full"
  - string field
- **explicit**
  - the episode parental advisory information
  - accepted values are: "yes", "no", "clean"
  - string field
- **season**
  - the episode season number
  - string field
- **draft**
  - true for a draft episode, false for publishing it
  - boolean field


## Demo

 * https://valeriogalano.github.io/podcast-feed-hugo/podcast/index.xml (Podcast feed)
 * https://valeriogalano.github.io/podcast-feed-hugo/sitemap.xml (Sitemap)


## Execute

Run following command to start the server:

```bash
$ hugo server -D
```

See the result at 
 * http://localhost:1313/podcast/index.xml (Podcast feed)
 * http://localhost:1313/sitemap.xml (Sitemap)
