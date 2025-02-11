# ESP32 configuración


Para crear archivos AVI compatibles puedes utilizar ffmpeg en el siguiente enlance https://ffmpeg-online.vercel.app/?inputOptions=-i&output=output.mp4&outputOptions=:

```
ffmpeg -i ejemplo.mp4 -vf "scale=320:240:force_original_aspect_ratio=increase,crop=320:240" -r 15 -c:v mjpeg -q:v 10 -acodec pcm_u8 -af "loudnorm" -ar 16000 -ac 1 nombredeEjemplo.avi
```

* -i ejemplo.mp4: Es el nombre de tu entrada, en este caso un video .mp4.
* -vf "scale=320:240:force_original_aspect_ratio=increase,crop=320:240": Establece la escala del video, es esta caso 320x240 es la resolución que encontré mas interesante, pero puedes probar diferentes 
* -r 15: Sets the frame rate to 15fps.
* -c:v mjpeg: Establece el codec MJPEG del video.
* -q:v 10: Establece la calidad del video (valores más bajos significan mayor calidad; puedes ajustarlo según sea necesario) - rango de 2 a 31.
* -acodec pcm_u8: Establece el códec de audio en PCM de 8 bits - NOTA: los archivos AVI no pueden contener audio pcm_s8, por lo que hay un procesamiento adicional en la canalización de audio para manejar esto.
* -ar 16000: Establece la frecuencia de muestreo de audio a 16 kHz..
* -ac 1: Configura el audio en mono (canal único).
* nombredeEjemplo.avi: Establece el nombre u el formato que tendrá la salida del video, en este caso .avi.


