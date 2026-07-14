# Naval Duel

A polished, real-time, two-player naval strategy game that runs in a web browser.

## Features

- Six-character private room codes and shareable invite links
- Remote peer-to-peer play using WebRTC data channels
- Private ship placement: layouts are not sent to the opponent during play
- Five-ship, 10 × 10 classic fleet rules
- Hit, miss, sunk, victory, rematch, sound, and in-game chat
- Placement commitments and post-game verification to detect inconsistent shot reporting
- Responsive design for phones, tablets, and computers
- No app account or database required

## Fastest way to play

The game needs to be served from a web address so both players can open the same page.

### Option 1: Netlify Drop

1. Unzip this folder.
2. Go to Netlify Drop in a desktop browser.
3. Drag the `naval-duel` folder onto the page.
4. Open the generated site address.
5. Share that address with the other player.

### Option 2: GitHub Pages

1. Create a new public GitHub repository.
2. Upload `index.html` to the repository root.
3. In **Settings → Pages**, deploy from the main branch and root folder.
4. Open the generated Pages address and share it.

### Option 3: Both players open the same file

You may send `index.html` to the other player and both open it in a browser. This works in many desktop browsers, but browser security restrictions can make local files less reliable than a hosted HTTPS page, especially on phones.

## How a match works

1. Player one chooses **Create private room**.
2. Player one sends the room code or invite link to player two.
3. Player two enters the code and joins.
4. Both players place and lock their fleets.
5. The game selects the first player deterministically from the room code and match number.
6. Players alternate one shot per turn; a hit does not grant an extra shot.
7. The first commander to sink all five enemy ships wins.

## Connection model

The app uses PeerJS 1.5.5. The public PeerJS Cloud service handles signaling so two browsers can discover each other; gameplay data then uses a WebRTC data channel between the browsers. Some restrictive corporate, hotel, school, or cellular networks may block peer-to-peer connections. In that case, try a different network or deploy a private PeerServer/TURN configuration. If either player disconnects after battle begins, the current match must be restarted in a new room.

## Files

- `index.html` — complete game, including styling and logic
- `README.md` — setup and play instructions

## Customization

Everything is contained in `index.html`. Search for these values near the start of the script:

- `BOARD_SIZE` to change grid dimensions
- `SHIP_DEFS` to change the fleet
- `PEER_PREFIX` to change the PeerJS room namespace

For production or high-volume use, replace the default PeerJS Cloud configuration with your own PeerServer and TURN infrastructure.
