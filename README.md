# TaskCluster Tools

This repository contains a collection of useful tools for use with TaskCluster.
Generally, we strive to not add UI to TaskCluster components, but instead offer
well documented APIs that can be easily consumed using a client library for
TaskCluster. See [TaskCluster documentation site](https://docs.taskcluster.net)
for details.

## Developing TaskCluster Tools

### Prerequisites for building TaskCluster Tools

- Node version v6+
- [Yarn](https://www.npmjs.com/package/yarn)

### Building

First, fork this repository to another GitHub account. Then you can clone and install:

```
git clone https://github.com/<YOUR_ACCOUNT>/taskcluster-tools.git
cd taskcluster-tools
yarn
```

### Code Organization

- `src/` (Tools source code)
- `src/<app>/`  (application specific-code, can be reused)

### Tasks and Configuration

Building this project uses [neutrino](https://github.com/mozilla-neutrino/neutrino),
[neutrino-preset-taskcluster-web](https://github.com/taskcluster/neutrino-preset-taskcluster-web),
and the `src/tools-preset` to:

- Compile ES2015+ syntax to ES5-compatible JS
- Compile React JSX to de-sugared JS
- Show ESLint errors based on TaskCluster rules
- Build application directories into page-specific bundles
- LESS files to CSS

### Testing changes

Install npm dependencies and start it up:
- `yarn`
- `yarn start`

This will start a local development server on port 9000 (http://localhost:9000).

Any ESLint errors across the project will be displayed in the terminal during development.

## Available targets

- `yarn start`: the default development build, watches `src/`, and serves on `http://localhost:9000/`
- `yarn build`: builds `src/` files into a `build/` directory

### Memory problems during development

It's possible that when building a larger project like taskcluster-tools that Node.js will run out
of memory for the amount of files being built during development. As a workaround, instead of
running `yarn start`, run the following to run the same command with more memory:

```sh
PORT=9000 node --max-old-space-size=4096 node_modules/.bin/neutrino start -p tools-preset
```

You may need to adjust the memory size to your machine specs accordingly.

## Testing

Until someone comes up with something better, all testing is manual. Open the tools and check that they work. :)

## Ngrok Setup (optional)

Ngrok allows you to expose a web server running on your local machine to the internet.
Ngrok is used to create an https connection, so that you can login to the taskcluster-tools.
For using ngrok:

- Create a free account on [ngrok](https://ngrok.com/).
- Install ngrok - `npm install -g ngrok` or `yarn global add ngrok`
- Run ngrok - `ngrok http 9000`

<sup>Note: You have to run ngrok in a separate terminal/console.</sup>
