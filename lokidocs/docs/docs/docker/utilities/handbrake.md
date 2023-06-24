# [Docker Handbrake Compress Videos](https://github.com/lokeshreddy007/My-Utilities/tree/master/docker-video-compressor)

This script use handbrake-cli to compress the video and it is awesome..🤩

It compresses GB's of files to MB without losing quality.😱

So how to use it?🤔

```bash
# docker run -it --rm -v  "path to video source":/input -e FORMAT=mp4 image name
```

### Example

```bash
docker run -it --rm -v /home/loki/Documents/demo:/input -e FORMAT=mp4 lokeshreddy007/handbrake-video-compressor

```

The above command will compress all the files from the source demo folder and recursively
