## 160329

- New PHP CS build target that will automatically run PHP Code Sniffer.
- New PHPUnit build target that will automatically run unit tests on a CI server.
- Adding support for CasperJS test suites.

## 160303

- Several enhancements, support for WP Sharks Core, and some bug fixes. See summary in https://github.com/websharks/phings/pull/50#issue-137523507
- Token replacement enhancements. See: https://github.com/websharks/phings/pull/52

## 160219

- Excluding `.sass-cache` (directories, not files) from distros and PHAR files.
- Remove `websharks/wp-core` from rebranded libraries.
- Rebrand subroutines now include websharks/core i18n alternations for WP themes/plugins.
- Bug fix. Minor issue. Adding conditionals around text-domain to string literal subroutine in lite handler.

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
