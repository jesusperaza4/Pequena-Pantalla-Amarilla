# ESP32 configuración


Para crear archivos AVI compatibles puedes utilizar ffmpeg:

```
ffmpeg -i limon.mp4 -vf "scale=320:240:force_original_aspect_ratio=increase,crop=320:240" -r 15 -c:v mjpeg -q:v 10 -acodec pcm_u8 -af "loudnorm" -ar 16000 -ac 1 output.avi
```

* -i input.mp4: Specifies the input file named input.mp4.
* -vf "scale=320:240:force_original_aspect_ratio=increase,crop=320:240": Sets the video filter to scale the video to 320x240 resolution - this matches the CYD - change to match your display
* -r 15: Sets the frame rate to 15fps.
* -c:v mjpeg: Sets the video codec to MJPEG.
* -q:v 10: Sets the video quality (lower values mean higher quality; you can adjust this as needed) - range 2-31
* -acodec pcm_u8: Sets the audio codec to 8-bit PCM - NOTE - AVI files cannot contain pcm_s8 audio, so there's some extra processing in the audio pipeline to handle this.
* -ar 16000: Sets the audio sample rate to 16KHz.
* -ac 1: Sets the audio to mono (single channel).
* output.avi: Specifies the output file named output.avi.

If you want to get fancy you can use the loudnorm filter to normalize the audio levels. There's a script in the `tools` folder that will do this for you. You will need `jq` installed to use it.

```
./tools/convert_movie_with_normalisation.sh input.mp4 output.avi
```

