# Guide

## Quick Start

1. Install Npcap.\
(An installer is provided in the "prerequisites" directory with each release)
2. Go to "Settings > Network" and select the network adapter that communicates with the Dekaron server.\
(If you're unsure which one is correct, check your IP via the cmd command "ipconfig". In most cases, you should only see one valid IPv4)
3. Select the data set corresponding to your server.\
(If you can't find your server's name, just try them out until one matches the actions correctly)
4. Click "[START] Capturing".
5. Log into the game server with your character.
6. At this point, you can stop and start capturing whenever you like, or reset the gathered data.

## Advanced Usage Tips

1. If you're multi-clienting, select which client you want to capture in "Settings > Network" to avoid duplicate data.
2. You can use "Stay on Top" and "Transparency" from "Settings > General" and drag DekaDux inside your game window for best visibility.
3. If you want to start DekaDux on the fly, you can also start capturing while already being logged into the game server - it will still be auto-detected.\
(Be aware of missing data when doing this!)
4. You can statically configure DekaDux to directly listen to your desired server. Go to "Settings > Network" and disable "Auto-detect Server Connection". Then select your target in "Dekaron Server" - this will also assign the appropriate "Dekaron Data Set" and "Protocol Version" for you.\
(This is not usable if you use a VPN that masks the game server's IP!)
5. If you have access to the unencrypted game client, you can extract the data set using the button in "Settings > Network" and activate "Use Custom Data Set" for perfectly matching IDs.
6. You can autostart DekaDux whenever you launch your Dekaron client. Configure this feature in "Settings > General".
7. Using the Traffic Analyzer with the filter narrowed down to a single decrypted packet (unrecognized disabled) will enable diff checks between the payloads.


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
4. **Nothing works ??**\
-> Some servers may use files or protocols that are so vastly different that DekaDux cannot work with them. In that case, contact us and we'll take a look at it.
5. **When using some skills with lingering damage instances, it shows the wrong skill in Combat Tracker**\
-> Sadly, it's a technical limitation. Refer to: [Technical Implementation - How Actions Reference Skills](TECHNICAL.md)
6. **Some skill/effect icons are missing**\
-> This is dependent on your client's files. If this happens to you, infrom the server owner to contact us and refer to: [DekaDux - Data Sets / Client Files (CSVs)](README.md)
7. **HP/Mana/Shield in the Combat Tracker is sometimes missing**\
-> It's a technical limitation. Refer to: [Technical Implementation - How Actions Are Managed](TECHNICAL.md)
8. **I can't find my own character**\
-> You need to relog into your character. The name only gets detected when you log in.
9. **No data is being captured when I change channel/server**\
-> When you have a dedicated game server IP or client port configured, DekaDux cannot auto-detect forwarded connections. Use auto-detection and target "<All>" Ports.
10. **Sometimes new player entries appear while the other one gets '<PRIOR>' in front of their name**\
-> This happens when an actor is assigned a new ID by the Dekaron server. This typically happens on a new server/channel connection.