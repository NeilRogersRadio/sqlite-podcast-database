# Neil Rogers Show - Sqlite Database

This is a copy of all the Neil shows that are published to the podcast.

There is a single table: PodcastNeil

```sql

CREATE TABLE `PodcastNeil` (
  `ShowDate` datetime DEFAULT NULL,
  `Notes` varchar(1958) DEFAULT NULL,
  `FileSize` bigint(20) DEFAULT '0',
  `Duration` int(11) DEFAULT '0',
  `Mp3Url` varchar(200) DEFAULT NULL,
  `Title` varchar(250) DEFAULT '',
  `ReleaseTime` datetime DEFAULT '1980-01-01 00:00:00'
)
```

This data is used to generate the podcast RSS.

ReleaseTime specifies when the show is to be published. Once we've gone through all 1800+ shows, the ReleaseTime will be reset to the current day and we will start again.

```sql
SELECT Title, Duration,mp3url, ShowDate, FileSize, ifnull(Notes,'') AS Notes, ReleaseTime
FROM PodcastNeil
WHERE ReleaseTime < date('now')
ORDER BY ReleaseTime DESC LIMIT 500
```

Due the size limits of RSS, we limit the feed to 500 shows.
