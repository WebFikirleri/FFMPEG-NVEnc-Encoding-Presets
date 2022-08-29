# NVEnc x265 4K HDR

Linux

    ffmpeg -loglevel debug -hide_banner -threads 4 \
    -hwaccel cuda -hwaccel_output_format cuda -i "input.mp4" \
    -max_muxing_queue_size 1024 \
    -map 0:v \
    -c:v hevc_nvenc -b:v 40M -maxrate:v 50M -minrate:v 10M -bufsize:v 50M \
    -profile:v high10 -level:v auto \
    -rc:v vbr_hq -rc-lookahead:v 32 -spatial_aq:v 1 -aq-strength:v 15 \
    -pix_fmt yuv420p10le -colorspace bt2020nc -color_primaries bt2020 -color_trc smpte2084 \
    -x265-params hdr-opt=1:repeat-headers=1:colormatrix=bt2020nc:colorprim=bt2020:transfer=smpte2084 \
    -g 30 -bf 2 \
    -coder:v cabac \
    -map 0:a \
    -c:a aac -profile:a aac_low -b:a 384k \
    -f mp4 "output.mp4"

Windows

    Same command but replace \ with ^
    
## Explanations

This lines for HDR

    -pix_fmt yuv420p10le -colorspace bt2020nc -color_primaries bt2020 -color_trc smpte2084 \
    -x265-params hdr-opt=1:repeat-headers=1:colormatrix=bt2020nc:colorprim=bt2020:transfer=smpte2084 \
    
This lines for YouTube

    -g 30 -bf 2 \
    -coder:v cabac \
    
This lines for better quality

    -rc:v vbr_hq -rc-lookahead:v 32 -spatial_aq:v 1 -aq-strength:v 15 \
