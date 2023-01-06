# Better instructions for what's going on and how to publish:
https://dev.to/alexeagleson/how-to-create-and-publish-a-react-component-library-2oe

## Notes

Can duplicate module in both devDependencies and peerDependencies

to both install locally and not include in bundle.

REMEMBER: always check if dependencies are up to date.


### for css:

look for rollup-plugin-postcss rollup plugin


### for react:
```
npm install react @types/react

npm install @testing-library/react --save-dev
```
also look into jest-environment-jsdom for testing

### for storybook:

- storybook with react and react-dom peer dependencies
we're already mentioned but I wanted to mention my
fix for it, so first is to download both react and
react-dom as a dev dependency, then duplicate react
to be a peer-dependency (this is surprisingly what
other libraries do).

- don't place react-dom as a peer dependency because
we solely need that just for storybook and our library
doesn't use it anywhere. and just in case we accidentally
include it in our bundle we need to mark the library
as external on our rollup config file, react is already
excluded because of the peerDepsExternal plugin. 

REMEMBER TO MOVE REACT TO peerDependencies


## Publishing

### 1nd way

https://docs.github.com/en/packages/quickstart

https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository#creating-a-release

If publish fails (403) ensure https://github.com/users/USERNAME/packages/npm/REPONAME/settings that repo is connected and has write access

REMEMBER:

add .npmrc file to consuming project at the same directory as package.json:
```
@watersilver:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=ACCESS_TOKEN
```

### 2st way

create .npmrc in user profile C:/Users/USERNAME

append:

```
registry=https://registry.npmjs.org/

@YOUR_GITHUB_USERNAME:registry=https://npm.pkg.github.com/

//npm.pkg.github.com/:_authToken=YOUR_AUTH_TOKEN
```

(fill in username and get your token from github)

```
npm publish
```