# DekaDux

This is a multifunctional tool for the MMORPG Dekaron (formerly 2Moons) which can be used either on the client side or on the server side.\
Its core concept is to provide a completely non-invasive interface for Dekaron's network protocol to capture, decrypt, process and parse all data coming from or going to the game client through your network adapter.\
Pursuing the difficult path of read-only emulation provides independence and functionality on all clients and servers - no memory access, no file access, no hooks or assembly edits are needed.\
This also comes with several comprehensive auto-detection mechanisms like valid Dekaron connections, channel forwarding, protocol version and separation of clients. Every build contains various data sets to choose from to accommodate most actively used clients.

To see this project in action with its entire feature set, check out our showcase video: [DekaDux - Feature Showcase](https://youtu.be/1euZ0Jn-CD4)

For more information about how to use it and a troubleshooting FAQ, check this: [Guide & FAQ](GUIDE_AND_FAQ.md)

## Contact

If you have any inquiries, suggestions, issues, or just wanna talk - join our Discord: [Vaerium's Discord](https://discord.gg/99zMtMGW2k)\
You can also reach out directly to me (@Rhyothos).

I am grateful for any feedback, especially considering that it's impossible for me to test all clients and constellations on my own. Most likely, there will be undiscovered issues.

Server owners who wish to be featured in DekaDux or to acquire special features are also welcome.

## Key Features

- **DPS Meter** - Track the damage dealt and PKs of all nearby actors, ranking them by a calculated DPS value.
- **Combat Tracker** - Track every action from all nearby actors coupled with in-depth statistics and filter possibilities.
- **Traffic Analyzer** - A neat byproduct created for protocol research purposes. Explore Dekaron's protocol with tons of useful research tools.
- **Loot Tracker** - [WIP]
- **Character Profiles** - [WIP]
- **Server-side Usage** - [WIP] See section: [Server-side Usage [WIP]](#server-side-usage-wip)

## Technologies & Implementation

DekaDux is written in C# targeting .NET 9.0. It requires Npcap as an interface to capture network packets.

It is split into 2 main projects:

- **DekaDux.Core** -
  The main library providing control over the Dekaron network protocol and processing its data using Dekaron CSV files. Also runs an in-memory SQLite database for parsed entities.

- **DekaDux.UI** -
  A modern UI using the WPF framework to visualize the processed data in a structured manner and provide in-depth configuration.

Until we deem this project ready and publish the full source code, the releases are fully protected and packed.
Builds are published self-contained, meaning you don't have to install any .NET prerequisites.\
(Going open source is not planned at this time, as it could lead to abuse and compromise the fair-play nature!)

If you have security concerns, rest assured that this tool does not require administrative privileges nor antivirus exclusions to function. You can even block this application from sending/receiving network traffic in your firewall (it only relies on capturing packets, which works regardless).

Some details about technical concepts regarding the protocol can be found here: [Technical Implementation](TECHNICAL.md)

## Supported Servers & Clients

Generally, it can be stated that DekaDux should work on every Dekaron server out there.\
Thanks to the auto-detection implementation, servers don't need to be explicitly added to DekaDux to be functional. There have been multiple protocols implemented, mainly divided between A9-based and A40-based, which will be auto-detected during runtime as well. You can also multi-client and then select only one certain character to track.

However, if you don't find your server, or more importantly its corresponding data set in our pre-defined collection within DekaDux, you may experience some inaccuracies. Refer to the [FAQ](GUIDE_AND_FAQ.md) regarding this.\
Full support is therefore only guaranteed for servers listed in DekaDux's network configuration.

## Data Sets / Client Files (CSVs)

DekaDux relies on static game files to process data correctly. For any Dekaron server, the following files are necessary:
- script\\skilldesc\\*.csv
- share\\skill\\status.csv
- share\\item\\itemaccessory.csv, itemarmor.csv, itemweapon.csv, itemstatus.csv
- share\\creature\\monster.csv
- share\\pc\\pcclass.csv

Icons are mapped statically since they should never change between different clients. Yet some clients changed their iconIndex in imagetables and this case requires a custom mapping:
- data\\texture\\ui\\game\\theme01
- data\\script\\ui\\com\\imagetable.txt

Releases come with a wide assortment of different data sets to choose from, some explicitly matching supported servers, some data-mined from generic clients.\
If you play on a server which is not represented in DekaDux, you can just try out different data sets until you find one that matches your client well enough. On servers that use pretty unique files, you'll encounter wrong/missing data in the Combat Tracker.

You can always add your custom client's CSV files in "custom_deka_data", and that way you have full support. But this requires them to be unencrypted and unpacked - which they almost never are.\
Network Settings provides a button to extract the necessary files from your client in one click and additionally attach iconIndex from all skill files to the skilldesc files; it's best to always use this.

If you are a server owner and want DekaDux to fully support and represent your server, please reach out to me with the necessary unencrypted CSV files so they can be added to your server within DekaDux. They will never be shared and cannot be extracted from the application.

## Server-side Usage [WIP]

You can run DekaDux on the server side with the appropriate configuration and permissions.\
This processes the data for every single actor connected to your server and opens the door for custom server implementations where you can use this tool as an interface and build features upon the data (or let me implement them for you).\
If you wish to receive custom server features, contact us.

Some examples to get the imagination going:
- Calculate the DPS for an entire party inside a dungeon run/DF and display it after clearing the boss
- Calculate an "MVP" player based on damage dealt in DKSQ/COLO, maybe even give a reward for this or announce it somewhere
- Stream the in-game chat from any place into a Discord channel for easy LFG/trade using Vaerium's Discord bot (or own webhooks)

## Disclaimer

This is a hobby project created out of love for the game and as a technical challenge. We uphold a 100% fair-play approach and do not want this to be categorized as "cheats or hacks". No systems are being exploited, its purpose is purely analytical/statistical.
We do not endorse the operation of private servers or any actions that harm Dekaron Global in any way. However, we support functionality across all servers because Dekaron players deserve it, regardless of where they play.

Please refer to the [License](LICENSE) and contact me if any issues arise.