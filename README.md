# StreamEngine-srs-hls-transcode
## Config for 720p, 1080p, and 480p
There are currently 3 separate servers running each transcode target resolution AND serving the VODS.
The plan is to take advantage of the SRS builtin docker cluster mode and to separate out the transcode from the vod delivery all together.

bitrate guide: https://stream.twitch.tv/encoding/
### 720p

```
docker run -p 1935:1935 -p 1985:1985 -p 8080:8080 \
    -v /root/srs/conf/custom.conf:/usr/local/srs/conf/srs.conf \
    -v /root/srs/log/srs.log:/usr/local/srs/objs/srs.log \
    -v /root/srs/vod/:/usr/local/srs/objs/nginx/html/vod/ \
    -v /root/srs/hls/:/usr/local/srs/objs/nginx/html/hls/ \
    ossrs/srs:3
```

### 1080p

```
docker run -p 1935:1935 -p 1985:1985 -p 8080:8080 \
    -v /root/srs/conf/custom_1080.conf:/usr/local/srs/conf/srs.conf \
    -v /root/srs/log/srs.log:/usr/local/srs/objs/srs.log \
    -v /root/srs/vod/:/usr/local/srs/objs/nginx/html/vod/ \
    -v /root/srs/hls/:/usr/local/srs/objs/nginx/html/hls/ \
    ossrs/srs:3
```

### 480p

```
docker run -p 1935:1935 -p 1985:1985 -p 8080:8080 \
    -v /root/srs/conf/custom_480.conf:/usr/local/srs/conf/srs.conf \
    -v /root/srs/log/srs.log:/usr/local/srs/objs/srs.log \
    -v /root/srs/vod/:/usr/local/srs/objs/nginx/html/vod/ \
    -v /root/srs/hls/:/usr/local/srs/objs/nginx/html/hls/ \
    ossrs/srs:3
```
### ABR (WIP)
```
docker run -p 1935:1935 -p 1985:1985 -p 8080:8080 \
    -v /root/srs/conf/abr.conf:/usr/local/srs/conf/srs.conf \
    -v /root/srs/log/srs.log:/usr/local/srs/objs/srs.log \
    -v /root/srs/vod/:/usr/local/srs/objs/nginx/html/vod/ \
    -v /root/srs/hls/:/usr/local/srs/objs/nginx/html/hls/ \
    -v /root/srs/m3u8/master.m3u8:/usr/local/srs/objs/nginx/html/live/master.m3u8 \
     --env "VIRTUAL_HOST=transcode.streamengine.live" \
    --env "VIRTUAL_PORT=8080" \
    --env "LETSENCRYPT_HOST=transcode.streamengine.live" \
    ossrs/srs:3
```
### Proxy
```
cd srs/reverse-proxy
docker-compose up -d
```
