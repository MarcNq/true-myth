# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/) and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [3.0.0] (2019-05-17)

### Added :star:

True Myth now includes the `Maybe.wrapReturn` function, conveniently aliased as `maybeify` and `Maybe.ify`, which lets you take any function which includes `null` or `undefined` in its return type (like [`Document#querySelector`][qs] and friends) and convert it to a function which returns a `Maybe` instead:

[qs]: https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector

```ts
const querySelector = Maybe.wrapReturn(document.querySelector.bind(document));
querySelector('#neat'); // Maybe<Element>
```

See [the docs](https://true-myth.js.org/modules/_maybe_.html#wrapreturn) for more!

### Changed :boom:

All `Maybe` helper functions must now return `NonNullable<T>`. This example, which previously compiled and resulted in the type `Maybe<string | null>`, will now cause a type error:

```ts
Maybe.of(document.querySelector('#neat'))
  .map(el => el.style.color); // `color` may be `null`
```

**SemVer note:** The new behavior was the ordinary expectation for those types before—doing otherwise would cause a runtime error—and so could reasonably be described as a bugfix. Any place this type-checked before was causing a runtime error. However, it seems clearer simply to mark it as a breaking change, since it *may* cause your build to fail, and encourage you all to upgrade directly and fix those bugs if so!

### Upgrading :gear:

With yarn:

```sh
yarn upgrade true-myth@latest
```

With npm:

```sh
npm install true-myth@latest
```

### Contributors 🙇 

- @bmakuh
- @chriskrycho
- @snatvb

[unreleased]: https://github.com/true-myth/true-myth/compare/v3.0.0...HEAD
[3.0.0]: https://github.com/true-myth/true-myth/compare/v2.2.8...v3.0.0
