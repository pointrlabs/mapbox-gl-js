[<img width="400" alt="Pointr" src="https://www.pointr.tech/hubfs/pointr-logo.svg">](https://www.pointr.tech/)

# Pointr README

## What is this fork?

As Mapbox decided to go open source, we decided it would be excellent to incorporate Mapbox's beautiful map engine into our SDK. Rather than relying on the main repository, though, it made sense to create our own fork so:
- Even if the main source code goes away, we have a stable copy
- We can make our own customizations as / when needed (see next question)

## Why is this fork needed?

First of all, it allows us to keep a stable copy of the source code in a safe place. Just in case Mapbox changes their mind one day.

Secondly, this allows us to make minor customizations as / when needed. At the moment, we have 1 customization: to disable **Telemetry**. Mapbox, by default, includes a **Telemetry** component that measures and reports how their maps are used (ie. user analytics). Although it should be possible to disable this via configuration, the documentation is not very clear and it is risky to rely on this functionality working (in fact, there are many developers complaining that they failed to use the Api or find any documentation on this). *We cannot let our SDK upload analytics to a 3rd party server*. Therefore, we have disabled Telemetry by disabling it directly from the source code.

## How to use this fork?

1. Go to `github.com` and generate a personal key token with only 'write:packages' and 'read:packages' scopes.
(https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)

2. Create `~/.npmrc` with the following content:
on Mac/Linux
```
//npm.pkg.github.com:/_authToken=TOKEN
```

on Windows
```
//npm.pkg.github.com/:_authToken=TOKEN
```

(https://docs.github.com/en/packages/using-github-packages-with-your-projects-ecosystem/configuring-npm-for-use-with-github-packages#authenticating-to-github-packages)

3. Create a `.npmrc` file in the project root folder (where `package.json` resides) (already done in `core-web-sdk` repo)
```
registry=https://npm.pkg.github.com/pointrlabs
```

(https://docs.github.com/en/packages/using-github-packages-with-your-projects-ecosystem/configuring-npm-for-use-with-github-packages#authenticating-with-a-personal-access-token)

4. Add `@pointrlabs/mapbox-gl-js` with the correct `pointr`version to `package.json`

eg.
```
{
  ...
  "dependencies": {
    "@pointrlabs/mapbox-gl": "1.11.1-pointr"
  }
}
```

5. Run `npm install` to install `@pointrlabs/mapbox-gl-js`.
** Note: *npm* will smartly install all other dependencies via public npm registry. **

6. Import the module to use it
```
var mapbox = import(@pointrlabs/mapbox-gl-js)
```

**Note: As long as you don't use Mapbox data, you do not need an access token. Just use a dummy string instead.**

## How to keep the code up-to-date with Mapbox? / How to release a new version?

From time to time, we should
- Pull the latest code from Mapbox and update our fork
- If there's a new stable Mapbox version, we should create a `release/A.B.C` branch
- `cherry-pick` all Pointr changes (2-3 commits, not more)
- Suffix version name with `pointr` (eg. `1.11.1` -> `1.11.1-pointr`)
- Call `npm publish` to publish this latest version to Github
- Point your `package.json` (in `core-web-sdk` or else) to this latest version instead and call `npm install`

** Note: It might be easier to have a `pointr` branch instead and use tags for each version. We can keep rebasing from the main source. **

## Won't 3rd parties have any access issues, since this repository is private?

No. When the web SDK is compiled, it creates 1x `pointrwebsdk.js` file that already contains `Mapbox`. So once compiled, there are no more dependencies to access and 3rd parties only need that 1 file.

# Original Mapbox README below

[<img width="400" alt="Mapbox" src="https://raw.githubusercontent.com/mapbox/mapbox-gl-js-docs/publisher-production/docs/pages/assets/logo.png">](https://www.mapbox.com/)

**Mapbox GL JS** is a JavaScript library for interactive, customizable vector maps on the web. It takes map styles that conform to the
[Mapbox Style Specification](https://docs.mapbox.com/mapbox-gl-js/style-spec/), applies them to vector tiles that
conform to the [Mapbox Vector Tile Specification](https://github.com/mapbox/vector-tile-spec), and renders them using
WebGL.

Mapbox GL JS is part of the [cross-platform Mapbox GL ecosystem](https://www.mapbox.com/maps/), which also includes
compatible native SDKs for applications on [Android](https://docs.mapbox.com/android/maps/overview/),
[iOS](https://docs.mapbox.com/ios/maps/overview/), [macOS](http://mapbox.github.io/mapbox-gl-native/macos),
[Qt](https://github.com/mapbox/mapbox-gl-native/tree/master/platform/qt), and [React Native](https://github.com/mapbox/react-native-mapbox-gl/). Mapbox provides building blocks to add location features like maps, search, and navigation into any experience you
create. To get started with GL JS or any of our other building blocks,
[sign up for a Mapbox account](https://www.mapbox.com/signup/).

In addition to GL JS, this repository contains code, issues, and test fixtures that are common to both GL JS and the
native SDKs. For code and issues specific to the native SDKs, see the
[mapbox/mapbox-gl-native](https://github.com/mapbox/mapbox-gl-native/) repository.

- [Getting started with Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/overview/)
- [Tutorials](https://docs.mapbox.com/help/tutorials/#web-apps)
- [API documentation](https://docs.mapbox.com/mapbox-gl-js/api/)
- [Examples](https://docs.mapbox.com/mapbox-gl-js/examples/)
- [Style documentation](https://docs.mapbox.com/mapbox-gl-js/style-spec/)
- [Open source styles](https://github.com/mapbox/mapbox-gl-styles)
- [Contributor documentation](./CONTRIBUTING.md)

[<img width="981" alt="Mapbox GL gallery" src="https://raw.githubusercontent.com/mapbox/mapbox-gl-js-docs/publisher-production/docs/pages/assets/gallery.png">](https://www.mapbox.com/gallery/)

## License

Mapbox GL JS is licensed under the [3-Clause BSD license](./LICENSE.txt).
The licenses of its dependencies are tracked via [FOSSA](https://app.fossa.io/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Fmapbox%2Fmapbox-gl-js):

[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Fmapbox%2Fmapbox-gl-js.svg?type=large)](https://app.fossa.io/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Fmapbox%2Fmapbox-gl-js?ref=badge_large)
