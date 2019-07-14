# lerna-ts-library-with-examples-starter
A starter project for developing a Typescript library in a monorepo managed by lerna so that embedded example projects can be included

It is intended to be pretty minimal. I often find myself wanting to kick off a project like this and need this scaffolding to get
running.

I think it's nice when building a library to show *standalone* examples. Too many libraries include their source code in the
same package and it can be very confusing to see clearly how you would use it from another package. This could also be 
solved using separate repositories, but I prefer a monorepo because these examples should be intimately linked to the library
project. Using lerna + monorepo will help me ensure that example packages will stay in sync with the library they describe.

## Overview

This project is setup using lerna. Lerna adds monorepo commands to make managing multiple packages easy. Of particular note are
- building
- dependency management

Lerna is aware of all the monorepo packages and the relationship between packages. With this it can do smart things like build
your packages in the right order.

## Getting started

### If you just have NPM

`npm install` <-- (optional) installs root package dependencies. Useful to install `lerna` CLI tool at root
`npm run bootstrap` <-- will run `lerna bootstrap` to install deps

### If you have "lerna" installed

`lerna bootstrap` <-- install dependencies for all the monorepo packages

## Building

The root directory of this project contains a `package.json` which includes npm scripts to make it easy to run the monorepo.
You can use these or you can use the relevant `lerna` commands directly. Up to you.

Here is how you can build all the packages:
`npm run build`
*or*
`lerna run build`

This recursively runs a `npm run build` command in any subpackage that defines `build` as an npm script. It will skip packages
that don't have it. It will run the command in order of the dependency graphs, so core packages will get built before any
packages that depend on them. Very convenient!

## Running

To run the examples, just execute `npm run start` or `lerna run start`. It will just run a start command (in parallel) in any
package that defines it. If run using the npm script, it will ensure everything is built first.

Here is how you can run the examples:
`npm run start` <-- ensures everything is built because of a `prestart`
*or*
`lerna run --parallel start` (note: you will get errors if you haven't built yet)
