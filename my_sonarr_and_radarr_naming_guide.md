# My Sonarr and Radarr Naming Guide


---

<!-- TOC depthFrom:1 depthTo:2 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Introduction](#introduction)
- [Sonarr](#sonarr)
- [Radarr](#radarr)

<!-- /TOC -->

---


# Introduction

I like having my media files _loosely_ named with the [scene naming style](https://scenerules.org/). This format _**works**_ with Plex (even though they recommend [this](https://support.plex.tv/hc/en-us/articles/200220687-Naming-Series-Season-Based-TV-Shows)). I just like the ability to quickly see the info on the release (i.e. the episode quality, proper, edition, release group) by just looking at the filename. Another benefit is that Subzero (subtitle) lookups yield more accurate results.

_Update: I have decided to remove `{Episode.CleanTitle}` from the naming format because 1) The episode titles can sometimes get so large that you have trouble storing/uploading it, and 2) The titles can often change on TVDB, making it a nuisance to fix later. However, if you decide to keep it, you may leave it in (it comes after the episode number and before the quality proper tags)._

_Update 2: Added Year to TV Show Titles._

```
Examples:

TV Shows
└── Gotham (2014)
    └── Season 01
        └── Gotham.2014.S01E01.1080p.BluRay.x264-DEMAND.mkv

Movies
└── Guardians of the Galaxy Vol. 2 (2017)
    └── Guardians.of.the.Galaxy.Vol.2.2017.1080p.BluRay.x264-SPARKS.mkv

```
---

# Sonarr

### Quality Definitions

These are important, or else the naming format will not work.

| Quality              | Title              |
| -------------------- | ------------------ |
| Unknown*             | Unknown            |
| SDTV*                | SDTV               |
| WEBRip-480p**        | 480p.WEBRip        |
| WEBDL-480p**         | 480p.WEBDL         |
| DVD                  | DVDRip             |
| Bluray-480p**        | 480p.BluRay        |
| HDTV-720p            | 720p.HDTV          |
| HDTV-1080p           | 1080p.HDTV         |
| Raw-HD*              | Raw-HD             |
| WEBRip-720p**        | 720p.WEBRip        |
| WEBDL-720p**         | 720p.WEBDL         |
| Bluray-720p          | 720p.BluRay        |
| WEBRip-1080p**       | 1080p.WEBRip       |
| WEBDL-1080p**        | 1080p.WEBDL        |
| Bluray-1080p         | 1080p.BluRay       |
| Bluray-1080p Remux** | 1080p.BluRay.Remux |
| HDTV-2160p           | 2160p.HDTV         |
| WEBRip-2160p**       | 2160p.WEBRip       |
| WEBDL-2160p**        | 2160p.WEBDL        |
| Bluray-2160p         | 2160p.BluRay       |
| Bluray-2160p Remux** | 2160p.BluRay.Remux |

\*Haven't figured out what to do with these yet, so I left them as-is.

\*\*Denotes deviations from Desi's naming structure for missing quality profiles since added to Sonarr

### Episode Naming

#### Replace Illegal Characters

```
Yes
```

#### Standard Episode Format

```
{Series.Title}.{season:00}x{episode:00}.{Episode.Title}.{Quality.Title}.{PREFERRED WORDS}.{MediaInfo VideoDynamicRange}.{MediaInfo VideoBitDepth}bit.{MediaInfo VideoCodec}.{MediaInfo.AudioCodec}.{MediaInfo.AudioChannels}{MediaInfo AudioLanguages}-{Release Group}
```

> Single Episode: The.Series.Title!.01x01.Episode.Title.(1).720p.HDTV.INTERNAL.HDR.10bit.x264.DTS.5.1-RlsGrp


#### Daily Episode Format

~~{Series.Title}.{Air-Date}.{Episode.Title}.{Quality.Title}.{PREFERRED WORDS}.{MediaInfo VideoDynamicRange}.{MediaInfo VideoBitDepth}bit.{MediaInfo VideoCodec}..{MediaInfo.AudioCodec}.{MediaInfo.AudioChannels}{MediaInfo AudioLanguages}-{Release Group}~~

> ~~ The.Series.Title!.2013-10-30.Episode.Title.(1).720p.HDTV.INTERNAL.HDR.10bit.x264.DTS.5.1-RlsGrp~~

```
{Series.CleanTitleYear}.S{season:00}E{episode:00}.{QUALITY.REAL}.{QUALITY.PROPER}.{Quality.Title}.{MediaInfo.VideoCodec}-{RELEASE.GROUP}
```
> Daily-Episode Example: The.Series.Title.2010.S01E01.PROPER.720p.HDTV.x264-RLSGRP

_Using Standard Episode Format now because there were issues matching daily shows such as Conan (2010) properly. Also saw posts from Plex team members who also suggested using the 0x00 format for dailies._


#### Anime Episode Format

```
{[Release Group]} {Series.Title}.{absolute:000}.{season:00}x{episode:00}.{Episode.CleanTitle}.{Quality.Title}.{PREFERRED WORDS}.{MediaInfo VideoDynamicRange}.{MediaInfo VideoBitDepth}bit.{MediaInfo VideoCodec}.{MediaInfo.AudioCodec}.{MediaInfo.AudioChannels} {MediaInfo AudioLanguages}
```

> Single Episode: [RlsGrp] The.Series.Title!.001.01x01.Episode.Title.1.720p.HDTV.INTERNAL.HDR.10bit.x264.DTS.5.1 [JA]


#### Series Folder Format

```
{Series TitleYear}
```

> Series Folder Example: The Series Title (2010)

_Doing `{Series CleanTitleYear}` would add the year without the parenthesis (i.e. `The Series Title 2010`), which is why I had to do `{Series TitleYear}`._

#### Season Folder Format

```
Season {season:00}
```

> Season Folder Example: Season 01

Padding the season numbers (e.g. `01`, `02`, etc) is preferred by the scene. This also helps sort your seasons in order when you have 10+ seasons.

_This style is also preferred by [Plex](https://support.plex.tv/hc/en-us/articles/200220687-Naming-Series-Season-Based-TV-Shows)._

#### Multi-Episode Style

```
Extend
```

> Multi Episode: The.Series.Title!.01x01-02-03.Episode.Title.720p.HDTV.INTERNAL.HDR.10bit.x264.DTS.5.1-RlsGrp
>
> Anime Multi Episode: [RlsGrp] The.Series.Title!.001-002-003.01x01-02-03.Episode.Title.720p.HDTV.INTERNAL.HDR.10bit.x264.DTS.5.1 [JA]

Even though releases sometimes use the `repeat` style for multi episode TV shows (e.g. S01E01E02), the scene actually prefers the `Prefixed Range` style (e.g. S01E01-E02), which is also the naming style [Plex](https://support.plex.tv/hc/en-us/articles/200220687-Naming-Series-Season-Based-TV-Shows) recommends.







***

# Radarr

### Quality Definitions

These are important, or else the naming format will not work.


| Quality        | Title              |
| -------------- | ------------------ |
| Unknown*       | Unknown            |
| WORKPRINT*     | WORKPRINT          |
| CAM*           | CAM                |
| TELESYNC*      | TELESYNC           |
| TELECINE*      | TELECINE           |
| REGIONAL*      | REGIONAL           |
| DVDSCR*        | DVDSCR             |
| SDTV*          | SDTV               |
| DVD            | DVDRip             |
| DVD-R          | DVDR               |
| WEBRip-480p**  | 480p.WEBRip        |
| WEBDL-480p**   | 480p.WEBDL         |
| Bluray-480p    | 480p.BluRay        |
| Bluray-576p    | 576p.BluRay        |
| HDTV-720p      | 720p.HDTV          |
| WEBRip-720p**  | 720p.WEBRip        |
| WEBDL-720p**   | 720p.WEBDL         |
| Bluray-720p    | 720p.BluRay        |
| HDTV-1080p     | 1080p.HDTV         |
| WEBRip1080p**  | 1080p.WEBRip       |
| WEBDL-1080p    | 1080p.WEBDL        |
| Bluray-1080p   | 1080p.BluRay       |
| Remux-1080p    | 1080p.BluRay.REMUX |
| HDTV-2160p     | 2160p.HDTV         |
| WEBRip-2160p** | 2160p.WEBRip       |
| WEBDL-2160p**  | 2160p.WEBDL        |
| Bluray-2160p   | 2160p.BluRay       |
| Remux-2160p    | 2160p.BluRay.REMUX |
| BR-DISK*       | BR-DISK            |
| Raw-HD*        | Raw-HD             |


\*Haven't figured out what to do with these yet, so I left them as-is.

\*\*Denotes deviations from Desi's naming structure for missing quality profiles since added to Sonarr

### Movie Naming

#### Rename Movies
```
Yes
```

#### Replace Illegal Characters
```
Yes
```

#### Colon Replacement Format:
```
Replace with Space Dash
```

#### Standard Movie Format
```
{Edition Tags}/{Movie.CleanTitle}.{Release.Year}.{EDITION.TAGS}.{QUALITY.REAL}.{QUALITY.PROPER}.{Quality.Title}.{MediaInfo.VideoCodec}-{RELEASE.GROUP}
```

>Movie Example: The.Movie.Title.2010.ULTIMATE.EXTENDED.EDITION.PROPER.1080p.BluRay.x264-EVOLVE


#### Movie Folder Format
```
{Movie Collection}/{Movie TitleThe} ({Release Year}) [tmdb-{TmdbId}]
```

>Movie Folder Example: The Movie Collection/Movie - Title, The (2010) [tmdb-345691]
