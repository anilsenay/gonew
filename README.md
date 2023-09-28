# gonew fork

I forked [gonew](https://go.dev/blog/gonew) to add a few features I needed. The problem in original gonew package is that it assumes the project source path is same as module name in the `go.mod` file.

This is not always the case. For example, I have a project as `github.com/username/module-name` but module name in go.mod is `username.com/module-name`.

When I use `gonew` `github.com/username/module-name` `new-module` to create a new project, it creates the project but the import paths in .go files are wrong. They remains as `username.com/module-name`. Because it tries to replace `github.com/username/module-name` with `new-module` which is not the module name and not using in import paths. This fork fixes that issue by adding new command line flags.

## Installation

```bash
go install github.com/anilsenay/gonew@latest
```

## Usage

```bash
gonew github.com/username/module-name new-module
```

## Flags

#### -srcmod

```bash
gonew -srcmod="username.com/module-name" github.com/username/module-name new-module
```

if you use `srcmod`, it will get module from `github.com/username/module-name` but module name in go.mod will be used as `username.com/module-name`. So gonew will replace `username.com/module-name` with `new-module` in .go files.

#### -dstmod

```bash
gonew -srcmod="username.com/module-name" -dstmod="username.com/some-module" github.com/username/module-name new-module
```

if you use `dstmod`, it will create folder as `new-module` but module name in go.mod will be `username.com/some-module`.
