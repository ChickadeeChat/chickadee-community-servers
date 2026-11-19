# Chickadee community servers

The list of public signaling servers Chickadee Chat offers under **Community** when you create or move a Space. The app reads [`servers.json`](servers.json) from this repository's `main` branch.

A signaling server only relays connection handshakes and presence; calls, chat and files go peer to peer.

## How a pick works

Picking a server pins the Space to it: the server and its backups become the Space's own list, and invite codes carry them. Editing or removing an entry here never moves an existing Space; it only changes what new Spaces are offered.

## Entry format

```json
{
  "servers": [
    {
      "name": "My server",
      "url": "wss://signaling.example.com",
      "backups": ["wss://signaling-backup.example.com"]
    }
  ]
}
```

- `name`: shown in the picker.
- `url`: a public `wss://` address.
- `backups` (optional): other public `wss://` addresses members fall back to when `url` is unreachable.

The app skips an entry that has no name, a non-`wss://` address, a loopback or LAN address, or a duplicate `url`, and reads at most 20 entries.

## Adding a server

Open a pull request that adds your entry to `servers.json`. Only list a server you intend to keep running: Spaces pinned to it depend on it.
