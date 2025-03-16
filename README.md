# ConvertToHEVC
Mac Automator QuickAction to covert videos to x265/HEVC using ffmpeg with hadware acceleration.


# Dependency
Ffmpeg needs to be installed, the script is configured to use jak ffmpeg installed via Homebrew using command:

  ```shell
   brew install ffmpeg
   ``` 
The ffmpeg should be in */opt/homebrew/bin/ffmpeg* (this can be amended inside the .workflow script).
If you don't have Homebrew installed, go here: https://brew.sh


# Workflow Installation
Download the .workflow file and open it - Automator will ask to install it and then is available. The script will automatically be copied to '/Users/YourUserName/Library/Services/Convert to HEVC.workflow'.


# Usage
Right click videos to convert, pick Quick Actions -> Convert to HEVC


# Ffmpeg parameters used
The command uses mac-specific libraries (takes advantage of M1, M2, Mx processors)

  ```shell
ffmpeg -hwaccel videotoolbox -i "input.mp4" -c:v hevc_videotoolbox -b:v 5000k -vtag hvc1 -pix_fmt yuv420p -c:a copy "output_converted.mp4"
  ```

Explanation
  ```shell
  ffmpeg                   Calls FFmpeg (video/audio processing tool).
  -hwaccel videotoolbox    Enables Apple VideoToolbox hardware acceleration for decoding.
  -i "input.mp4"           Specifies the input file (path in JavaScript).
  -c:v hevc_videotoolbox   Uses H.265 (HEVC) encoding with Appleâ€™s hardware acceleration.
  -b:v 5000k               Sets the video bitrate to 5000 kbps (adjust for quality vs. size).
  -vtag hvc1               Ensures Apple-compatible HEVC format for macOS/iOS playback.
  -pix_fmt yuv420p         Converts pixel format to YUV 4:2:0 for maximum device compatibility.
  -c:a copy                Copies the original audio without re-encoding (saves time & quality).
  "output_converted.mp4"   Defines the output file (newFilePath in JavaScript).
   ``` 

