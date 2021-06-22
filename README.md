# Self Hosted Restream

Restream self hosted alternative

## Instructions:

1.  Duplicate .env.example and save as .env
2.  Replace contents of .env (change VALUE for your real twitch stream key).
3.  Start docker if not already running and run `docker-compose up`.
4.  Go to OBS Stream settings and choose Custom. On Server write `rtmp://localhost:1935/stream` (you can replace localhost for the computer ip address if your streaming from another device in the same network). On Stream Key write `hello`.
5.  Start the stream on OBS.
6.  Go to your twitch profile, you should see a stream with the same content that you're streaming to the computer running the docker container. It's being forwarded.
7.  (Optional) You can watch the stream locally from VLC opening a stream with this url `rtmp://localhost/stream/hello`.
8.  (Optional) You can also stream to other services like youtube, just add tem below twitch in [nginx.conf](./nginx.conf):
```
push rtmp://live.twitch.tv/app/${STREAM_KEY_TWITCH};
push rtmp://a.rtmp.youtube.com/live2/${STREAM_KEY_YOUTUBE};
```
9.  (Optional) If you add more environment variables like the variable STREAM_KEY_YOUTUBE in step 8, add them to your [.env](./.env.example) file below the twitch stream key environment variable.
