# Starboard Wrap for Data2Evidence

## Introduction
Starboard notebook wrap is modified to suit the requirements for the Data2Evidence platform

## Build guide
1. Node 16 is required for this build
2. Run `yarn` and `yarn build` in the root of this project

## Deployment
1. Commit the built files into the repository
2. Update the commit hash for `ui/yarn.lock` in `https://github.com/OHDSI/d2e`

## Modifcations
The following functions in `embed.ts` is modified

`loadDefaultSettings`
4 additional settings will be passed to the `StarboardEmbed` component from portal
- serverUrl: base url to backend/trex.The default would be `https://localhost:41100`
- token: authentication token
- userId: idp userId from user metadata
- datasetId: selected datasetId from portal

`NOTEBOOK_SET_INIT_DATA`
- this function is triggered by the `StarboardEmbed` upon its load, and the settings mentioned above are passed to the starboard notebook