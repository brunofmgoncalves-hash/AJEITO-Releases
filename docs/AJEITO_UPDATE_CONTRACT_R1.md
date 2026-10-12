# AJEITO Update Contract R1

Version: 1.0
Decision date: 2026-10-12

This contract is shared by Desktop, Mobile and Tablet.

## Client identities
- desktop-windows
- mobile-android
- tablet-android

## Channels
- staging
- stable

Each client/channel has its own manifest under:
- updates/<client>/staging.json
- updates/<client>/stable.json

## Required fields
- contract_version
- available
- client
- platform
- channel
- version
- build
- artifact_type
- artifact_url
- sha256
- update_mode
- package_id
- published_at
- release_notes

## Rules
- version is semantic version visible to users.
- build is a monotonically increasing technical integer per client.
- update_mode is optional or required.
- sha256 must match the distributed artifact.
- Android package_id and signing identity must remain compatible between upgrades.
- Mobile and Tablet share this contract, but have independent manifests and artifacts.
- APK is allowed for staging/beta. Google Play distribution may use AAB later.
- available=false allows artifact_url, sha256 and package_id to be null while a client/channel is not published.
- stable must never point to a staging-only artifact.
