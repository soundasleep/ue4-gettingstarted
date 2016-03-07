ue4-getting-started
===================

Testing out open source development of games.

## Development

You'll need to use `composer` to download missing assets into `Content/Shared/`:

```
composer
```

It might take some time to download things, though.
Just [ue4-starter-content](https://github.com/soundasleep/ue4-starter-content) alone includes ~620 MB of content.

(I've found that Composer runs out of memory downloading Git repositories larger than ~400 MB, so I've had to manually split [ue4-starter-content](https://github.com/soundasleep/ue4-starter-content) into smaller sub-dependencies.)

## License

As with everything made and distributed with UE4, only a few licenses are supported, and must not be copyleft: this project and its dependencies are licensed under MIT.

## Composer integration

Why rely on having to download and export heaps of random ZIP files when you can use package managers to organise them for you? Just add them as `require`s to your `composer.json`:

```json
{
  "name": "soundasleep/ue4-getting-started",
  "require": {
    "soundasleep/ue4-starter-content": "*"
  }
}
```

*NOTE* For now, you'll need to also include the incredibly experimental and very-likely-to-break requirements that I've hacked together:

```json
{
  "name": "soundasleep/ue4-getting-started",
  "repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/soundasleep/installers"
    },
    {
      "type": "vcs",
      "url": "https://github.com/soundasleep/ue4-starter-content"
    }
  ],
  "require": {
    "composer/installers": "dev-master",
    "soundasleep/ue4-starter-content": "dev-master"
  }
}
```

*NOTE* You may also need to add `Content/Shared/` to your `.gitignore`, so you don't end up committing
the same Git repository twice.

## TODO

Currently this only supports Content (i.e. assets such as Blueprints, Materials, Meshes).
I'm hoping that I'll be able to extend this same approach for
[all the other Unreal Engine 4 directories](https://docs.unrealengine.com/latest/INT/Engine/Basics/DirectoryStructure/index.html):
`Content/`, `Config/` (maybe), `Source/Engine/`, `Source/Game/`, `Plugins/`,
`Extras/`, `Shaders/`, `Documentation/`, `Programs/` etc. We'll see.
