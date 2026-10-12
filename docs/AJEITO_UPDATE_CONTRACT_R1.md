# AJEITO Update Contract R1

Version: 1.1
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

## Android package identities
- Mobile stable: pt.omeuajeito.mobile
- Mobile staging: pt.omeuajeito.mobile.staging
- Tablet stable: pt.omeuajeito.tablet
- Tablet staging: pt.omeuajeito.tablet.staging

These package IDs are permanent identities for their respective client/channel. Changing a package ID creates a different Android application.

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
- signing_cert_sha256
- published_at
- release_notes

## Rules
- version is semantic version visible to users.
- build is a monotonically increasing technical integer per client.
- Update ordering uses semantic version plus build; a higher build of the same semantic version is newer.
- update_mode is optional or required and is controlled by the remote contract.
- sha256 must match the distributed artifact.
- On Android, package_id and signing identity must remain compatible between upgrades.
- signing_cert_sha256 identifies the Android signing certificate and must be pinned once the permanent keystore for that package ID is defined.
- Mobile and Tablet share this contract, but have independent manifests, artifacts, package IDs, builds and release cycles.
- APK is allowed for staging/beta. Google Play distribution may use AAB later.
- Staging and stable are separate Android applications and may coexist on the same device.
- available=false allows artifact_url and sha256 to be null while a client/channel is not published. package_id remains defined for Android even when unavailable.
- stable must never point to a staging-only artifact.
- Desktop keeps its existing Windows installation identity; client identity for this contract is desktop-windows.
