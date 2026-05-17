# Guide

## Quick Start

1. Start 'DekaDux.exe'. If this is your first time, you will be prompted to install the prerequisites - follow the instructions.
2. Go to "Settings > Network" and select the network adapter that communicates with the Dekaron server.\
2.1. If your traffic runs through a tunnel - e.g. "ping reducer" software like ExitLag - you need to use your loopback adapter.
3. Select the data set and protocol version corresponding to your server.\
3.1. If you use DekaDux through a supported launcher or connect to a server IP that is recognized by DekaDux, data set and protocol version will be assigned automatically.\
3.2. If you can't find your server's data set, just try them out until one matches the actions close enough.
4. Click "[START] Capturing".
5. Log into the game server with your character.
6. At this point, you can stop and start capturing whenever you like, or reset the gathered data.

## Advanced Usage Tips

1. If you're multi-clienting, select which client you want to capture in "Settings > Network" to avoid duplicate data. By default the first detected client connection will be targeted.
2. You can use "Stay on Top" and "Transparency" from "Settings > General" and drag DekaDux inside your game window for best visibility.
3. If you need to start DekaDux on the fly, you can also start capturing while already being logged into the game server - it will still be auto-detected.\
(Be aware of initial missing data when doing this)
4. You can statically configure DekaDux to directly listen to your desired server. Go to "Settings > Network" and disable "Auto-detect Server Connection". Then select your target in "Dekaron Server" - this will also assign the appropriate "Dekaron Data Set" and "Protocol Version" for you.\
(This feature is mostly experimental and for debugging, most servers will have dynamic gateways which route the traffic to the actual game server and none will work on loopback (e.g. ExitLag))
5. If you have access to the unencrypted game client, you can extract the data set using the button in "Settings > Network" and activate "Use Custom Data Set" for perfectly matching IDs.
6. You can autostart DekaDux whenever you launch your Dekaron client. Configure this feature in "Settings > General".
7. Using the Traffic Analyzer with the filter narrowed down to a single decrypted packet and unrecognized disabled will enable diff checks between the payloads.


# FAQ / Troubleshooting

Please note that some issues you might encounter are simply due to the technical limitations imposed by Dekaron's protocol and client.
For example, the limited render distance often results in being able to see damage numbers from other actors, but not the actors themselves. This leads to missing actor animations, which are necessary to assign action names.\
We try to minimize the impact of this as much as possible by buffering unknown data and merging it when actors are loaded, but some gaps cannot be filled (e.g., mobs that are hit and die outside the client’s render distance or skills as mentioned before).

1. **Some skills/effects don't have the right names**\
-> Your selected data set does not match the server's CSV files. Try a different data set or refer to: [Advanced Usage Tips - 5](#advanced-usage-tips)\
If nothing matches, you should inform the server owner to reach out to us so we can import their data set into our next release.
2. **Some players or NPCs don't have the right name/don't even get shown**\
-> If actors are named "Unknown Actor" or aren't visible, then DekaDux wasn't capturing traffic when those actors were loaded in by your client. Make sure you start capturing before meeting any actor in the game.\
If you simply run out of render distance from the actor and load them back in, the name should get detected and refreshed.
3. **Every skill is being shown duplicate**\
-> You are most likely multi-clienting. Select one client to capture traffic for in "Settings > Network".
4. **When I connect to the server, DekaDux doesn't detect the connection**\
-> Make sure to use auto-detection. If no connections get detected, your dekaron traffic is not running through the selected network adapter. In some cases there might be issues with "ping reducer" software which tunnels traffic - contact us to look at this issue.
5. **When using some skills with lingering damage instances, it shows the wrong skill in Combat Tracker**\
-> Sadly, it's a technical limitation. Refer to: [Technical Implementation - How Actions Reference Skills](TECHNICAL.md)
6. **Some skill/effect icons are missing**\
-> This is dependent on your client's files. If this happens to you, infrom the server owner to contact us and refer to: [DekaDux - Data Sets / Client Files (CSVs)](README.md)
7. **HP/Mana/Shield in the Combat Tracker is sometimes missing**\
-> It's a technical limitation. Refer to: [Technical Implementation - How Actions Are Managed](TECHNICAL.md)
8. **I can't find my own character**\
-> You need to relog into your character. The name only gets detected when you log in.
9. **No data is being captured when I change channel/server**\
-> When you have a dedicated game server IP or client port configured, DekaDux cannot auto-detect forwarded connections. Use auto-detection and target "<All>" Ports.\
If you already auto-detected "server X" and now want to play on "server Y" you need to restart DekaDux - this issue can sometimes also happen when switching channels very fast back and forth on the same server.
10. **Sometimes new player entries appear while the other one gets '<X>' in front of their name**\
-> This happens when an actor is assigned a new ID by the Dekaron server, actors with this notation are not active anymore. This typically happens on a new server/channel connection (like DKSQ).
11. **When I log in, players around me have corrupted names inside the DamageMeter**\
-> If you connect to a server based on the A40 protocol which isn't identified through it's specific IP (using ExitLag for example), you can run into timing issues with the protocol auto-detection. The actors got loaded with the default protocol before it was changed to A40.\
Make sure to set the protocol version to 'A40' instead of '<Auto>' under "Settings > Network".
12. **Nothing works ??**\
-> Some servers may use files or protocols that are so vastly different that DekaDux cannot work with them. In that case, contact us and we'll take a look at it.