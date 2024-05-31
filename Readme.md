HypixelSkyblock
This is the back-end for https://sky.coflnet.com You can get the same data and play around with it by using this project.

For any questions visit our discord! https://discord.gg/cofl

Kafka topics
This project uses a kafka server to distribute workloads.
Topics produced are:

sky-newauction
sky-newbid
sky-soldauction
sky-canceledauction
sky-endedauction
sky-bazaarprice
sky-update-player (players whose names should be updated)
sky-updated-player (players who got updated)
sky-flips found flips, producer: flipper, consumer: light-clients
You can modify them by changing appsettings.json or setting the enviroment variables. To get a full list check appsettings.json.
Note that to set them as enviroment variables you have to prefix them with TOPICS__ because you can't add : in an env variable.
Example:
To set "MISSING_AUCTION":"sky-canceledauction" you have to set TOPICS__MISSING_AUCTION=mycooltopic

Get started/usage
Hello there fellow developer. Development of this project is done with docker-compose. The whole system is split into so called microservices ie multiple smaller projects each doing one thing eg. flip finding.

Install docker and docker-compose if you are a windows user these come with docker desktop.
create a new folder skyblock, enter it and clone this repository with git clone --depth=1 https://github.com/Coflnet/HypixelSkyblock.git dev
copy docker-compose.yml to the skyblock folder (one folder above)
Open a terminal in the skyblock folder and Start up the databases with docker-compose up -d mariadb phpmyadmin kafka redis
Clone the indexer git clone https://github.com/Coflnet/SkyIndexer.git The indexer is the service that manages and indexes skyblock data in the database. Make sure to modify the migration for first setup in SkyIndexer/Program.cs.
Also clone the updater git clone https://github.com/Coflnet/SkyUpdater.git, commands git clone https://github.com/Coflnet/SkyCommands.git and the website git clone https://github.com/Coflnet/hypixel-react.git
Start these services with docker-compose up -d indexer updater commands api modcommands frontend after that is done you have a complete setup to archive and browse auctions locally.
If you want flips you will also want to clone the flipper and/or sniper flip finders
git clone https://github.com/Coflnet/SkyFlipper.git
git clone https://github.com/Coflnet/SkySniper.git docker-compose up -d flipper sniper Note that you only need to clone services that have a build section. The ones with image are just downloaded.
For basic website functunality you need

this repo
SkyCommands
hypixel-react (frontend)
SkyUpdater (downloading process)