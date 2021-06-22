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
8.  (Optional) You can also stream to other services (I think even other accounts of the same platform but I haven't tested this yet) like youtube, just add tem below twitch in [nginx.conf](./nginx.conf):
```
push rtmp://live.twitch.tv/app/${STREAM_KEY_TWITCH};
push rtmp://a.rtmp.youtube.com/live2/${STREAM_KEY_YOUTUBE};
```
9.  (Optional) If you add more environment variables like the variable STREAM_KEY_YOUTUBE in step 8, add them to your [.env](./.env.example) file below the twitch stream key environment variable.

## Example Usage

- I have a computer with a dedicated connection just for streaming and another computer with its own connection just for online gaming, but I don't have a capture card to plug the gaming computer to the streaming computer. So I also connect the gaming computer to the same network that the streaming computer uses but the gaming computer just uses this connection as a secondary connection to connect to the streaming computer not for internet connectivity. So I run this project in the streaming computer and OBS in the gaming computer, but instead of streaming to twitch directly I stream via LAN to the streaming computer running this project which forwards the stream to twitch via its own dedicated internet conneection so the gaming traffic and the streaming traffic go out via different connection, there're plenty of better ways to do this but this is one use case. In my case I just have one connection with good speed for streaming, the other one is only good for gaming. If I try to do both things from either of those connections the upload bandwith is not enough.
