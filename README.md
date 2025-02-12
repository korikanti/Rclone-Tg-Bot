# An Rclone Telegram bot to transfer to and from many clouds

## Features:

- Mirror from Telegram to cloud.
- Mirror direct download links and Mega.nz links to cloud
- Mirror torrent and magnets links to cloud using qBittorrent.
- Mirror batch up to 100 files at once from Telegram to cloud (private or public channel)
- Leech files and folders from cloud to Telegram.
- Extract and Zip files for leech and mirror.
- Copy from cloud to cloud.
- File manager for cloud (delete and calculate size)
- Telegram button menus to interact with cloud.
- Renaming of Telegram files.
- Progress bar when downloading and uploading.
- Direct links Supported:
  > letsupload.io, hxfile.co, anonfiles.com, bayfiles.com, antfiles, fembed.com, fembed.net, femax20.com, layarkacaxxi.icu, fcdn.stream, sbplay.org, naniplay.com, naniplay.nanime.in, naniplay.nanime.biz, sbembed.com, streamtape.com, streamsb.net, feurl.com, pixeldrain.com, racaty.net, 1fichier.com, 1drv.ms (Only works for file not folder or business account), uptobox.com (Uptobox account must be premium) and solidfiles.com

## Commands for bot(set through @BotFather)

```
mirror - mirror to selected cloud 
qbmirror - mirror torrent to cloud
unzipmirror - mirror and extract to cloud 
zipmirror - mirror and zip to cloud 
mirrorbatch - mirror files in batch to cloud 
mirrorset - select cloud/folder where to mirror
leech - leech from cloud to Telegram
unzipleech - leech and extract to telegram 
zipleech - leech and zip to telegram 
copy - copy from cloud to cloud
myfiles - file manager
logs - get logs from server
server - get server info
speedtest - test speed of server
restart - restart bot
```

## Deploy on VPS: 

1. **Installing requirements**

 - Clone repo:

        git clone https://github.com/Sam-Max/Rclone-Tg-Bot rclonetgbot/ && cd rclonetgbot

 - Install Docker(skip this if deploying without docker).

        sudo apt install snapd
        sudo snap install docker

2. **Set up config file**

- cp config_sample.env config.env 

- Fill up variables:

   - Mandatory variables:
        - `API_ID`: get this from https://my.telegram.org. Don't put this in quotes.
        - `API_HASH`: get this from https://my.telegram.org
        - `OWNER_ID`: your Telegram User ID (not username) of the owner of the bot.
        - `ALLOWED_USERS`: list of IDs of allowed users who can use this bot separated by spaces
        - `ALLOWED_CHATS`: list of IDs of allowed chats who can use this bot separated by spaces
        - `BOT_TOKEN`: The Telegram Bot Token (get from @BotFather) 
        - `DOWNLOAD_DIR`: The path to the local folder where the downloads will go.
        - `RCLONE_CONFIG`: content of the rclone.conf file generated with rclone command-line program. Set this surrounded by single quotes.
   - Non mandatory variables:
        - `UPSTREAM_REPO`: if your repo is private add your github repo link with format: `https://username:{githubtoken}@github.com/{username}/{reponame}`, so you can update your app from private repository on each restart. Get token from [Github settings](https://github.com/settings/tokens)
        - `UPSTREAM_BRANCH`: Upstream branch for update.
        - `USER_SESSION_STRING`: Pyrogram session string for using mirrorbatch command and to download/upload using your telegram account (needed for telegram premium upload). To generate string session use this command `python3 session_generator.py` on command line on your pc from repository folder. **NOTE**: when using string session you can't use bot, use it with group or channel.
        - `TG_SPLIT_SIZE`: Telegram upload limit in bytes, to automatically slice the file bigger that this size into small parts to upload to Telegram. Default is `2GB` for non premium account or `4GB` if your account is premium.
        - `EDIT_SLEEP_SECS`: Seconds for update regulary rclone progress message. Default to 10.
        - `DEFAULT_RCLONE_DRIVE`: select a default drive from your rclone.conf file.
        - `TORRENT_TIMEOUT`: Timeout of dead torrents downloading with qBittorrent.

   - MEGA
        - `MEGA_API_KEY`: Mega.nz API key to mirror mega.nz links. Get it from Mega SDK Page
        - `MEGA_EMAIL_ID`: E-Mail ID used to sign up on mega.nz for using premium account.
        - `MEGA_PASSWORD`: Password for mega.nz account.
 
3. **Deploying on VPS Using Docker**

- Start Docker daemon (skip if already running), if installed by snap then use 2nd command:
    
        sudo dockerd
        sudo snap start docker

     Note: If not started or not starting, run the command below then try to start.

        sudo apt install docker.io

- Build Docker image:

        sudo docker build . -t rclonetg-bot 

- Run the image:

        sudo docker run rclonetg-bot 

- To stop the image:

        sudo docker ps
        sudo docker stop id

- To clear the container:

        sudo docker container prune

- To delete the images:

        sudo docker image prune -a

4. **Deploying on VPS Using docker-compose**

```
sudo apt install docker-compose
```
- Build and run Docker image:
```
sudo docker-compose up
```
- After editing files with nano for example (nano start.sh):
```
sudo docker-compose up --build
```
- To stop the image:
```
sudo docker-compose stop
```
- To run the image:
```
sudo docker-compose start

```

## Deploying on Heroku
<p><a href="https://github.com/Sam-Max/Rclone-Tg-Bot/tree/heroku"> <img src="https://img.shields.io/badge/Deploy%20Guide-blueviolet?style=for-the-badge&logo=heroku" width="170""/></a></p>

## Bot Screenshot: 

<img src="./screenshot.png" alt="button menu example">

## Repositories used to develop this bot:

1- [TorToolkit-Telegram](https://github.com/yash-dk/TorToolkit-Telegram)

2- [Rclone](https://github.com/rclone/rclone)

3- [Telethon]() and [Pyrogram]()

4- [Conversation-Pyrogram](https://github.com/Ripeey/Conversation-Pyrogram/)

5- and others referenced in the code.
