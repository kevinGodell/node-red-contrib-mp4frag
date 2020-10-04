# node-red-contrib-mp4frag
######
[![GitHub license](https://img.shields.io/badge/license-MIT-brightgreen.svg)](https://raw.githubusercontent.com/kevinGodell/node-red-contrib-mp4frag/master/LICENSE?token=ABOPHYQ73XPHMEGBSABCDJK7IKRQO)
[![npm](https://img.shields.io/npm/dt/node-red-contrib-mp4frag.svg?style=flat-square)](https://www.npmjs.com/package/node-red-contrib-mp4frag)
[![GitHub issues](https://img.shields.io/github/issues/kevinGodell/node-red-contrib-mp4frag.svg)](https://github.com/kevinGodell/node-red-contrib-mp4frag/issues)
#### What?
- A node-red fragmented mp4 server.
#### Why?
- Needed for extracting a fragmented mp4 from a buffer stream.
#### How?
- Parses the fragments (initialization and segments) of the mp4.
#### When?
- Using ffmpeg to connect to a video source and piping out a fragmented mp4.
#### Where?
- Fragmented mp4 files will be available on http server.
#### Requirements
- Input must be a buffer stream containing a properly fragmented mp4.
- ffmpeg flags: `-f mp4 -movflags +frag_keyframe+empty_moov+default_base_moof`.
#### Links
- [node-red](https://nodered.org/)
- [ffmpeg](https://ffmpeg.org/)
- [buffer](https://nodejs.org/api/buffer.html)
- [mp4frag](https://www.npmjs.com/package/mp4frag)
#### Installation
```
npm install kevinGodell/node-red-contrib-mp4frag
```
#### Flow Examples
- Using Built-in HTTP Routes:
```json
[{"id":"198dbe2b.3d8d9a","type":"tab","label":"Video Test 1","disabled":false,"info":""},{"id":"5c1f54b6.454f7c","type":"inject","z":"198dbe2b.3d8d9a","name":"Start stream","props":[{"p":"payload"}],"repeat":"","crontab":"","once":true,"onceDelay":"1","topic":"","payload":"true","payloadType":"bool","x":190,"y":100,"wires":[["372f3933.65a7a6"]]},{"id":"d52ddf1.b4a51a","type":"inject","z":"198dbe2b.3d8d9a","name":"Stop stream","props":[{"p":"payload"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"false","payloadType":"bool","x":190,"y":146,"wires":[["372f3933.65a7a6"]]},{"id":"372f3933.65a7a6","type":"switch","z":"198dbe2b.3d8d9a","name":"","property":"payload","propertyType":"msg","rules":[{"t":"true"},{"t":"false"}],"checkall":"true","repair":false,"outputs":2,"x":341,"y":100,"wires":[["6f7b48af.2862f"],["3f385b73.54d284"]]},{"id":"3f385b73.54d284","type":"function","z":"198dbe2b.3d8d9a","name":"stop","func":"msg = {\n    kill:'SIGHUP',\n    payload : 'SIGHUP'  \n}\n\nreturn msg;","outputs":1,"noerr":0,"initialize":"","finalize":"","x":361,"y":149,"wires":[["6f7b48af.2862f"]]},{"id":"6f7b48af.2862f","type":"exec","z":"198dbe2b.3d8d9a","command":"ffmpeg -loglevel quiet -f mp4 -re -i https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ElephantsDream.mp4 -c:a copy -c:v copy -f mp4 -movflags +frag_keyframe+empty_moov+default_base_moof pipe:1","addpay":false,"append":"","useSpawn":"true","timer":"","oldrc":false,"name":"elephants dream ffmpeg","x":572,"y":120,"wires":[["609e41bb.4ac748"],[],["609e41bb.4ac748"]]},{"id":"5aedd6d7.d727d","type":"ui_mp4frag","z":"198dbe2b.3d8d9a","name":"elephants dream ui_mp4frag","group":"28171ec9.c62efa","order":0,"width":"5","height":"4","readyPoster":"https://raw.githubusercontent.com/kevinGodell/node-red-contrib-ui-mp4frag/master/video_playback_ready.png","errorPoster":"https://raw.githubusercontent.com/kevinGodell/node-red-contrib-ui-mp4frag/master/video_playback_error.png","hlsJsConfig":"{\"liveDurationInfinity\":true,\"liveBackBufferLength\":0,\"maxBufferLength\":5,\"manifestLoadingTimeOut\":1000,\"manifestLoadingMaxRetry\":10,\"manifestLoadingRetryDelay\":500}","restart":"true","autoplay":"true","x":1103,"y":117,"wires":[[]]},{"id":"609e41bb.4ac748","type":"mp4frag","z":"198dbe2b.3d8d9a","name":"elephants dream mp4frag","hlsPlaylistSize":"10","hlsPlaylistExtra":"5","hlsPlaylistUrl":"609e41bb.4ac748","x":832,"y":117,"wires":[["5aedd6d7.d727d"]]},{"id":"5c018bd6.6c9e54","type":"inject","z":"198dbe2b.3d8d9a","name":"Start stream","props":[{"p":"payload"}],"repeat":"","crontab":"","once":true,"onceDelay":"1","topic":"","payload":"true","payloadType":"bool","x":190,"y":220,"wires":[["72de9e54.1c0068"]]},{"id":"2a3b4b00.fa1354","type":"inject","z":"198dbe2b.3d8d9a","name":"Stop stream","props":[{"p":"payload"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"false","payloadType":"bool","x":190,"y":266,"wires":[["72de9e54.1c0068"]]},{"id":"72de9e54.1c0068","type":"switch","z":"198dbe2b.3d8d9a","name":"","property":"payload","propertyType":"msg","rules":[{"t":"true"},{"t":"false"}],"checkall":"true","repair":false,"outputs":2,"x":341,"y":220,"wires":[["9f93c481.f530c8"],["c9f285e2.5f9bb"]]},{"id":"c9f285e2.5f9bb","type":"function","z":"198dbe2b.3d8d9a","name":"stop","func":"msg = {\n    kill:'SIGHUP',\n    payload : 'SIGHUP'  \n}\n\nreturn msg;","outputs":1,"noerr":0,"initialize":"","finalize":"","x":361,"y":269,"wires":[["9f93c481.f530c8"]]},{"id":"9f93c481.f530c8","type":"exec","z":"198dbe2b.3d8d9a","command":"ffmpeg -loglevel quiet -f mp4 -re -i https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/Sintel.mp4 -c:a copy -c:v copy -f mp4 -movflags +frag_keyframe+empty_moov+default_base_moof pipe:1","addpay":false,"append":"","useSpawn":"true","timer":"","oldrc":false,"name":"sintel ffmpeg","x":569,"y":240,"wires":[["47dbee0c.608cc8"],[],["47dbee0c.608cc8"]]},{"id":"a5e6df5b.fe7c28","type":"ui_mp4frag","z":"198dbe2b.3d8d9a","name":"sintel ui_mp4frag","group":"28171ec9.c62efa","order":0,"width":"5","height":"4","readyPoster":"https://raw.githubusercontent.com/kevinGodell/node-red-contrib-ui-mp4frag/master/video_playback_ready.png","errorPoster":"https://raw.githubusercontent.com/kevinGodell/node-red-contrib-ui-mp4frag/master/video_playback_error.png","hlsJsConfig":"{\"liveDurationInfinity\":true,\"liveBackBufferLength\":0,\"maxBufferLength\":5,\"manifestLoadingTimeOut\":1000,\"manifestLoadingMaxRetry\":10,\"manifestLoadingRetryDelay\":500}","restart":"true","autoplay":"true","x":1130,"y":237,"wires":[[]]},{"id":"47dbee0c.608cc8","type":"mp4frag","z":"198dbe2b.3d8d9a","name":"sintel mp4frag","hlsPlaylistSize":"10","hlsPlaylistExtra":"5","hlsPlaylistUrl":"47dbee0c.608cc8","x":828,"y":237,"wires":[["a5e6df5b.fe7c28"]]},{"id":"d22a455c.0e5c48","type":"inject","z":"198dbe2b.3d8d9a","name":"Start stream","props":[{"p":"payload"}],"repeat":"","crontab":"","once":true,"onceDelay":"1","topic":"","payload":"true","payloadType":"bool","x":190,"y":340,"wires":[["ff047477.259928"]]},{"id":"7f59ae27.f6ab3","type":"inject","z":"198dbe2b.3d8d9a","name":"Stop stream","props":[{"p":"payload"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"false","payloadType":"bool","x":190,"y":386,"wires":[["ff047477.259928"]]},{"id":"ff047477.259928","type":"switch","z":"198dbe2b.3d8d9a","name":"","property":"payload","propertyType":"msg","rules":[{"t":"true"},{"t":"false"}],"checkall":"true","repair":false,"outputs":2,"x":341,"y":340,"wires":[["27f81ab5.717a9e"],["6af91471.f4237c"]]},{"id":"6af91471.f4237c","type":"function","z":"198dbe2b.3d8d9a","name":"stop","func":"msg = {\n    kill:'SIGHUP',\n    payload : 'SIGHUP'  \n}\n\nreturn msg;","outputs":1,"noerr":0,"initialize":"","finalize":"","x":361,"y":389,"wires":[["27f81ab5.717a9e"]]},{"id":"27f81ab5.717a9e","type":"exec","z":"198dbe2b.3d8d9a","command":"ffmpeg -loglevel quiet -f mp4 -re -i https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4 -c:a copy -c:v copy -f mp4 -movflags +frag_keyframe+empty_moov+default_base_moof pipe:1","addpay":false,"append":"","useSpawn":"true","timer":"","oldrc":false,"name":"big buck bunny ffmpeg","x":576,"y":360,"wires":[["7c65c57a.0c4c2c"],[],["7c65c57a.0c4c2c"]]},{"id":"22fedad.e9cdaa6","type":"ui_mp4frag","z":"198dbe2b.3d8d9a","name":"big buck bunny ui_mp4frag","group":"28171ec9.c62efa","order":0,"width":"5","height":"4","readyPoster":"https://raw.githubusercontent.com/kevinGodell/node-red-contrib-ui-mp4frag/master/video_playback_ready.png","errorPoster":"https://raw.githubusercontent.com/kevinGodell/node-red-contrib-ui-mp4frag/master/video_playback_error.png","hlsJsConfig":"{\"liveDurationInfinity\":true,\"liveBackBufferLength\":0,\"maxBufferLength\":5,\"manifestLoadingTimeOut\":1000,\"manifestLoadingMaxRetry\":10,\"manifestLoadingRetryDelay\":500}","restart":"true","autoplay":"true","x":1101,"y":357,"wires":[[]]},{"id":"7c65c57a.0c4c2c","type":"mp4frag","z":"198dbe2b.3d8d9a","name":"big buck bunny mp4frag","hlsPlaylistSize":"10","hlsPlaylistExtra":"5","hlsPlaylistUrl":"7c65c57a.0c4c2c","x":832,"y":357,"wires":[["22fedad.e9cdaa6"]]},{"id":"28171ec9.c62efa","type":"ui_group","z":"","name":"Video Test 1","tab":"4e54a2ca.371c7c","order":15,"disp":true,"width":"15","collapse":true},{"id":"4e54a2ca.371c7c","type":"ui_tab","z":"","name":"Video Test 1","icon":"dashboard","disabled":false,"hidden":false}]
```
#### Screenshots
![mp4frag flow](https://raw.githubusercontent.com/kevinGodell/node-red-contrib-mp4frag/master/screenshots/mp4frag_flow.png)
![mp4frag settings](https://raw.githubusercontent.com/kevinGodell/node-red-contrib-mp4frag/master/screenshots/mp4frag_settings.png)
