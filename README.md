# Self-Hosted File Sync Selector

> **Decision:** Choose the authority topology—peer-to-peer replicas, a server library, a collaboration suite, a protocol gateway, or a web portal—before comparing features.

**For:** Individuals and small teams deciding how files should synchronize and be shared across devices.  

This is a non-commercial, source-traceable decision guide. It normalizes upstream declarations; it does not claim that repository reachability proves functionality, security, maintenance, or fitness.

**Start here:** [Download the replica and gateway ledger](assets/sync-authority-conflict-sheet.csv) — twelve projects, located upstream evidence, and explicit unknowns.

## Choose by workload


- Device-to-device folder replicas with no central cloud: Syncthing or Unison.
- Central synchronized library: Seafile; full collaboration suite: Nextcloud or ownCloud Infinite Scale.
- Controlled protocol gateway: SFTPGo; broad command-line transfer: rclone.
- Low-latency development mirroring: Mutagen, not a general document collaboration suite.
- Browser portal without sync: compare Filestash and Dufs; do not call either a desktop sync engine.

## Select a file authority topology

A gateway provides access, a synchronizer reconciles copies, and a backup retains recoverable history. Identify the owner of deletion before connecting real clients.

## Authority topology


- **Replica synchronization** — Syncthing and Unison reconcile peers; Mutagen optimizes development sessions. Conflict policy and deletion propagation are the core tests.
- **Central file platforms** — Seafile, Nextcloud, ownCloud Infinite Scale, Pydio Cells, and Cozy Stack make a server authoritative and add varying collaboration layers.
- **Gateways and transfer** — SFTPGo exposes storage through protocols; rclone copies/synchronizes across backends. Neither automatically supplies collaborative editing.
- **Web access surfaces** — Filestash and Dufs expose files in a browser or over simple protocols; pair them with independently managed storage and backup.


## Replica and gateway ledger

| Project | Role | Authority and replica topology | Conflict or deletion behavior | State and access path |
|---|---|---|---|---|
| Syncthing | peer-to-peer sync | Syncthing is a continuous file synchronization program. It synchronizes files between two or more computers. We strive to fulfill the goals below. The goals are… | is fine to optimize for these values, as long as they are not in conflict with the stated goals above. | https://syncthing.net/security/. There is also a built-in automatic upgrade mechanism (disabled in some distribution channels) which uses a compiled in ECDSA si… |
| Seafile | server-centric library | Unknown in the frozen upstream README | Seafile is an open source cloud storage system with privacy protection and teamwork features. Collections of files are called libraries. Each library can be syn… | - Seafile Android client: GPLv3 - Desktop syncing client (this repository): GPLv2 - Seafile Server core: AGPLv3 - Seahub (Seafile server Web UI): Apache License… |
| Nextcloud | collaboration suite | 📁 Access your Data You can store your files, contacts, calendars, and more on a server of your choosing. 🔄 Sync your Data You keep your files, contacts, calenda… | licensed under the AGPLv3 or any later version. | 🔒 Security with our encryption mechanisms, HackerOne bounty program and two-factor authentication. |
| ownCloud Infinite Scale | service-oriented collaboration platform | ownCloud Infinite Scale (oCIS) is the new file sync & share platform that will be the foundation of your data management platform. | Make sure to download the latest released version today! | Make sure to download the latest released version today! |
| Pydio Cells | governed file platform | - Create a database in your chosen DB server, | Note: We have developed and tested Pydio Cells on macOS, Ubuntu, Debian and CentOS. Windows version might still have unknown glitches and is not yet supported. | - Go language v1.21 or higher and a correctly configured Go toolchain, - MySQL database 5.6 or higher (or MariaDB equivalent). |
| Cozy Stack | personal-data platform | The Cozy-Stack also allows to access the database replication API, allowing to sync documents between the server and local databases, for example in mobile clie… | - create, update, delete documents inside the database; | Cozy is a platform that brings all your web services in the same private space. With it, your web apps and your devices can share data easily, providing you wit… |
| SFTPGo | protocol gateway | Full-featured and highly configurable event-driven file transfer solution. Server protocols: SFTP, HTTP/S, FTP/S, WebDAV. Storage backends: local filesystem, en… | Thank you to KeenThemes for granting us a custom license to use their amazing themes for the SFTPGo WebAdmin and WebClient user interfaces, across both the Open… | Full-featured and highly configurable event-driven file transfer solution. Server protocols: SFTP, HTTP/S, FTP/S, WebDAV. Storage backends: local filesystem, en… |
| Filestash | web file gateway | Taken literally, the "truths of the universe" are a set of core interfaces, one for every key component of Filestash, and they're yours to implement (storage, a… | Unknown in the frozen upstream README | Taken literally, the "truths of the universe" are a set of core interfaces, one for every key component of Filestash, and they're yours to implement (storage, a… |
| Unison | peer-to-peer reconciler | Unison is a file-synchronization tool for POSIX-compliant systems (e.g. BSD, GNU/Linux, macOS) and Windows. It allows two replicas of a collection of files and … | structure. Updates that do not conflict can be propagated automatically. Conflicting updates are detected and displayed. | Please also read https://github.com/bcpierce00/unison/wiki before interacting with the issue tracker or asking for help. |
| rclone | transfer and sync engine | Rclone ("rsync for cloud storage") is a command-line program to sync files and directories to and from different cloud storage providers. | Rclone ("rsync for cloud storage") is a command-line program to sync files and directories to and from different cloud storage providers. | - Can serve local or remote files over HTTP/WebDAV/FTP/SFTP/DLNA |
| Mutagen | development synchronizer | local tools to work with code in remote environments like cloud servers and containers. It does this by providing high-performance real-time file synchronizatio… | Mutagen uses semantic versioning for tracking releases. Before Mutagen reaches version 1.0, each minor release series will be supported for one month after the … | file synchronization and flexible network forwarding. It supports synchronization and forwarding between local systems, |
| Dufs | file server and portal | Dufs is a distinctive utility file server that supports static serving, uploading, searching, accessing control, webdav... | Allow all operations like upload/delete/search/create/edit... | Dufs is a distinctive utility file server that supports static serving, uploading, searching, accessing control, webdav... |

Values are short excerpts from the frozen upstream README, not feature-test scores. The CSV retains the located evidence for each cell. “Unknown” means the retrieved document did not establish that axis; it is not a claim that the feature is absent.

## Keep the authority path explicit


Start with a disposable two-client conflict test: concurrent edits, rename, delete, offline reconnect, and rollback. For a central platform, back up database, blobs, configuration, and keys together. For gateways, document whether the gateway or backend enforces users and versions. Sync is never a substitute for an offline backup.


## Adoption notes by project

### Syncthing

- **Choose it for:** Private device synchronization with explicit conflicts.
- **License at the frozen source:** [MPL-2.0](https://raw.githubusercontent.com/syncthing/syncthing/f2ed52347ec461a2b7a70787192f3615bcb6bafd/LICENSE).
- **Adoption test:** Test concurrent edits, deletes, ignores, permissions, versioning, and a full-device loss; replicated deletion is not backup.
- **Source:** [syncthing/syncthing](https://github.com/syncthing/syncthing).

### Seafile

- **Choose it for:** Efficient synchronized libraries.
- **License at the frozen source:** [GPL-2.0 server core; verify edition-specific components](https://raw.githubusercontent.com/haiwen/seafile/af6539cebf8484fcd07a4cab7ddfdfc425034a76/LICENSE.txt).
- **Adoption test:** Verify edition boundaries, client virtual-drive behavior, object-store layout, and coordinated database/storage restore.
- **Source:** [haiwen/seafile](https://github.com/haiwen/seafile).

### Nextcloud

- **Choose it for:** Broad team collaboration.
- **License at the frozen source:** [AGPL-3.0](https://raw.githubusercontent.com/nextcloud/server/45aaca0caf6ca8dcf1525e36a721d03cd23c930e/COPYING).
- **Adoption test:** Use supported release artifacts rather than a development checkout; back up data, database, config, and app compatibility together.
- **Source:** [nextcloud/server](https://github.com/nextcloud/server).

### ownCloud Infinite Scale

- **Choose it for:** Teams evaluating modern ownCloud architecture.
- **License at the frozen source:** [Apache-2.0](https://raw.githubusercontent.com/owncloud/ocis/3c585e0b2fd7b95d72e14197ab70342ee8b03704/LICENSE).
- **Adoption test:** Do not apply legacy ownCloud Server assumptions; test identity, storage drivers, client compatibility, and upgrade path.
- **Source:** [owncloud/ocis](https://github.com/owncloud/ocis).

### Pydio Cells

- **Choose it for:** Policy-heavy team file sharing.
- **License at the frozen source:** [AGPL-3.0 with commercial offerings around the product](https://raw.githubusercontent.com/pydio/cells/e53f0eec4e719903e67aff3b61a9be83d6c242ea/LICENSE).
- **Adoption test:** Confirm community/enterprise boundary, storage migration, identity integration, and AGPL obligations for the intended deployment.
- **Source:** [pydio/cells](https://github.com/pydio/cells).

### Cozy Stack

- **Choose it for:** Personal cloud extending beyond file sync.
- **License at the frozen source:** [AGPL-3.0](https://raw.githubusercontent.com/linagora/cozy-stack/f8b67f6ff818158d1390e3db6e77d39eacb898b0/LICENSE).
- **Adoption test:** Canonical repository redirects from cozy/cozy-stack to linagora/cozy-stack; test connectors, client sync, and export separately.
- **Source:** [linagora/cozy-stack](https://github.com/linagora/cozy-stack).

### SFTPGo

- **Choose it for:** Controlled access through standard protocols.
- **License at the frozen source:** [AGPL-3.0-only with additional terms; separate enterprise edition](https://raw.githubusercontent.com/drakkan/sftpgo/360ca0118892afac6f162920b0f08e5b5660b436/LICENSE).
- **Adoption test:** Community code is AGPL with additional terms; enterprise has commercial features. Confirm needed lifecycle and HA features by edition.
- **Source:** [drakkan/sftpgo](https://github.com/drakkan/sftpgo).

### Filestash

- **Choose it for:** Giving existing storage a web interface.
- **License at the frozen source:** [AGPL-3.0](https://raw.githubusercontent.com/mickael-kerjean/filestash/b6fe63f4f01eecbada100d567a84c2503de8fbee/LICENSE).
- **Adoption test:** It does not make every backend a synchronized library; verify authentication plugins, write semantics, audit, and restore of configuration.
- **Source:** [mickael-kerjean/filestash](https://github.com/mickael-kerjean/filestash).

### Unison

- **Choose it for:** Technical users needing explicit two-way reconciliation.
- **License at the frozen source:** [GPL-3.0](https://raw.githubusercontent.com/bcpierce00/unison/8772d26a2eb77cfd0cb6da81807e81f24f51044c/LICENSE).
- **Adoption test:** Match versions across peers and test metadata, rename, delete, and conflict behavior; it is not a sharing portal.
- **Source:** [bcpierce00/unison](https://github.com/bcpierce00/unison).

### rclone

- **Choose it for:** Automating movement among heterogeneous stores.
- **License at the frozen source:** [MIT](https://raw.githubusercontent.com/rclone/rclone/ec1eb597b1921a17e871a1deb8c0e9939f2dd456/COPYING).
- **Adoption test:** The sync command can propagate deletion; test dry runs, checksum semantics, backend consistency, crypt keys, and restore.
- **Source:** [rclone/rclone](https://github.com/rclone/rclone).

### Mutagen

- **Choose it for:** Remote development where local tools edit remote code.
- **License at the frozen source:** [MIT](https://raw.githubusercontent.com/mutagen-io/mutagen/6ccfeaaf4dfd261e59ef9aac56e3c157b62e605b/LICENSE).
- **Adoption test:** It is optimized for development sessions, not multi-user document governance; test ignored files, conflict policy, and version compatibility.
- **Source:** [mutagen-io/mutagen](https://github.com/mutagen-io/mutagen).

### Dufs

- **Choose it for:** Simple LAN/web access to managed directories.
- **License at the frozen source:** [MIT OR Apache-2.0](https://raw.githubusercontent.com/sigoden/dufs/77291a230565ca090a1d7751d07db82ac418906d/LICENSE-MIT).
- **Adoption test:** No desktop replica engine or rich version history is implied; configure authentication, TLS proxying, permissions, and backup separately.
- **Source:** [sigoden/dufs](https://github.com/sigoden/dufs).

## Exercise concurrent changes

1. Edit one file concurrently on two clients, then reconnect an offline client.
2. Test rename, delete, ignored files, permissions and version retention.
3. Record which replica or server is authoritative and preserve an independent backup.
4. Recover files without the gateway and reconcile central database/blob state.

## What this guide covers

File authority, replica reconciliation and access gateways, not versioned backup-format selection.

## Located sources and update policy

[`sources.json`](sources.json) binds each cited declaration to a commit, document, exact line range and local snapshot hash. [`assets/projects.json`](assets/projects.json) holds the normalized roles and decision axes. Current HEAD reachability is recorded separately; it is not a maintenance or security assessment. Licensing is version- and directory-specific. Re-read the selected release before adoption.

Run the local evidence and package checks, then opt into public-source reachability:

```bash
python3 scripts/verify_sources.py
python3 scripts/verify_sources.py --online
```

These checks validate source binding, excerpts, hashes, language, the decision asset and nonempty public content. They do not certify feature behavior, migration success or restore success. No popularity score, paid placement or affiliate ranking is used. Restricted-license and historical examples are explicit contrasts, not silently recommended open-source defaults.
