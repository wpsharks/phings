## 160212

- Excluding `.sass-cache` from distros and PHAR files.

## v150424

- Initial release.
- Updated the ZipTask and TarTask to use `${project_slug}/` as the filename prefix when building the distributable ZIP/TAR. See https://github.com/websharks/phings/issues/5
- Updated the ZipTask and TarTask to use exclude empty directories when building the distributable ZIP/TAR. See https://github.com/websharks/phings/issues/5

## v150925

- Making status output more verbose.
- Improving config and validation routines.
- Breaking targets into separate file imports.
- Making the entire repo more portable; i.e., it can be used as a submodule.
- Changing the name of the properties file. Now `.build.props` instead of `.build.properties`.
- Now suggesting the use of `build.xml` instead of `.build.xml`. This avoids the need to provide the path as a CLI arg; i.e., you can type `phing` instead of `phing -f .build.xml`.
- Changing hidden lite build target from `-lite-variation` to just `-lite`.
- Changing hidden lite push target from `-push-lite-variation` to just `-push-lite`.
- Refactoring temporary variables used in `-push-lite`. These now include a `_push_lite_` prefix to keep them unique.
- Breaking `-apigen` and the `codex` build target out of the normal build routine and into its own target.
- Now works in non-WordPress projects.
- Now works for projects with or without a `phar-stub.php`.
- Now works for projects with or without `wp-i18n-tools`.
- Now works for projects with or without `composer.json`.
