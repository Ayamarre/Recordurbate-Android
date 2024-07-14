# Recordurbate For Android
The act of recording a Chaturbate live stream. Fix Youtube-dl & Recording top 500 models only, credits to @oliverjrose99 & @divenxx

## Requirements
* Termux from F-Droid not Play Store
* Python 3+ (requests)
* Yt-dlp
* FFmpeg

```commandline
# termux-setup-storage
# pkg update && pkg upgrade
# pkg install python
# pkg install git
# apt install python ffmpeg
$ pip install yt-dlp requests
```
## Installation
```commandline
$ cd /storage/emulated/0/Android/data/com.termux/files/
$ git clone https://github.com/Ayamarre/Recordurbate-Android.git
$ cd Recordurbate/recordurbate
```
The default config files will work out of the box with youtube-dl and FFmpeg installed. Streams will be saved to the folder videos/\<name>/\<name> \<date> \<hour>_\<min>.mp4. This can be changed by editing the youtube-dl.config file, see the configuration section for more. 
## Usage

View the usage/help text
```
python Recordurbate.py help
```

Add or remove a streamer to record
```
python Recordurbate.py [add | del] username
```

Start, stop or restart the daemon
```
python Recordurbate.py [start | stop | restart]
```

List the streamers in the config
```
python Recordurbate.py list
```

Import streamers from a file
```
python Recordurbate.py import [file]
```

Export streamers to a file. The file parameter is optional and the default location will be used if not passed
```
python Recordurbate.py export [file]
```

## Config Files
There are two main config files that are used, `config.json` and `youtube-dl.config`, both being stored in the configs directory. In that directory is also the log file (rb.log) and the pid file (rb.pid).

### Config.json
This file is used directly by Recordurbate and contains all the configuration options as well as the array of streamers to record.

`youtube-dl_cmd` - Sets the command used to run Youtube-dl. 

`youtube-dl_config` - Sets where the config file for Youtube-dl is located and is passed with the `--config-location` parameter. Note that system and user wide configs still apply, see [this link](https://github.com/ytdl-org/youtube-dl#configuration) for more info.

`auto_reload_config` - Sets if the bot should reload the config after every loop to allow adding or removing streamers while running.

`rate_limit` - Sets whether or not the API calls should be rate limited.

`rate_limit_time` - The time in seconds to wait between API calls, only waits if `rate_limit` is true.

`default_export_location` - Sets the default location for the export command.

`streamers` - An array of strings, each of which is a streamer to record.

### Youtube-dl.config
This file is used to set all of the Youtube-dl config options and is passed using the `--config-location` parameter. As mentioned, the system and user wide configs still apply. Options such as quality, export options and more can be [found on the Youtube-dl Github.](https://github.com/ytdl-org/youtube-dl)

## Notes

### Recordings lag and freeze
A couple users have reported that recordings may lag and freeze which was due to out of date youtube-dl and ffmpeg versions. If you experience this, please ensure you are using the latest stable versions and that your internet, storage and CPU are not bottlenecks causing issues.

### Pid file found, is * already running? pid: xxxxx
Manual delete rb.log & rb.pid 
