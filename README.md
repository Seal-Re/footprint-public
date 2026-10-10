# footprint-public

A public, append-only data mirror. Each machine running the collector reports a heartbeat
every few minutes; every report is committed here, so the repository's commit history is the
activity timeline.

## Layout

```
data/devices/<device-id>.jsonl   # one JSON object per line, one file per device
stats.json                       # aggregate counts derived from the data
```

Each line in a device file is one sample:

```json
{"ts": "2026-09-29T16:28:49+08:00", "tz": "中国标准时间", "device": "bih-l-57616",
 "monotonic_id": 1, "accuracy_m": 85.0, "source": "WiFi", "city": "杭州市",
 "geo_method": "api", "trigger": "startup", "grid_m": 250, "lat_m": -478750, "lon_m": 3724000}
```

`trigger` is `startup` or `heartbeat`; location fields are snapped to a 250 m grid and are
omitted when a sample carries no new position. `stats.json` (`records`, `days`, `devices`,
`active_hours`, `latest_ts`, `latest_ago`, `last_updated`) is a roll-up written alongside the
data.

- Commit history: <https://github.com/Seal-Re/footprint-public/commits/main> — one commit per
  report, message `采集 <timestamp>`.
- Commit activity graph: <https://github.com/Seal-Re/footprint-public/graphs/commit-activity>

This repository contains only data; the collector itself lives elsewhere.
