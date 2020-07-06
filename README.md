# StreamEngine-srs-hls-transcode

`
docker run -p 1935:1935 -p 1985:1985 -p 8080:8080 \
    -v /root/srs/conf/custom.conf:/usr/local/srs/conf/srs.conf \
    -v /root/srs/log/srs.log:/usr/local/srs/objs/srs.log \
    -v /root/srs/vod/:/usr/local/srs/objs/nginx/html/vod/ \
    ossrs/srs:3
`
