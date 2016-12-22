## $v

- Adding support for new `.build.props` property: `project_issues_slug`. Allowing a separate repo to be used for issues.
- Developers can now create `src/includes/translations/.generate` to enable an i18n translation file for projects that would otherwise not require them.
- Lite build with pro Composer dependencies. Fixed in this release. See [Issue #146](https://github.com/websharks/phings/issues/146).
- Exclude `composer.json` and `composer.lock` from final distros. See [Issue #141](https://github.com/websharks/phings/issues/141).
- Strip unnecessary files from final distros. See [Issue #150](https://github.com/websharks/phings/issues/150).
- New Ad-Hoc command: `<adHocGitHubGetJson />` for retrieving data from the GitHub API; e.g., issue data, user data, etc.
- Updating [this wiki article](https://github.com/websharks/phings/wiki/GitHub-Features). Documented [new `force=true` alternative](https://github.com/websharks/phings/wiki/GitHub-Features#finishing-a-github-issue-forced-merge-alternative) for finishing a feature branch locally instead of remotely. See [Issue #110](https://github.com/websharks/phings/issues/110).
- PR title (when starting a new feature branch) should contain the associated issue title. See [Issue #149](https://github.com/websharks/phings/issues/149).
- Adding support for prioritized `.build.*.php` files. See [Issue #127](https://github.com/websharks/phings/issues/127).

## v160908.63229

- Adding `project_slack_channel` as a valid build property. See: #132
- Automate bleeding edge on official release. See: #142
- Update to latest i18n tools. See: #144

## v160824.8847

- Adding new `export-ignore` rules for `TODO.md` files, PsySH stubs, and for IDE helpers. See: https://github.com/websharks/phings/issues/134 and https://github.com/websharks/phings/issues/128
- Enhancing `@since` replacements and adding support for `@deprecated`. See: #130 and #133
- Adding support for `//php-required-functions//`. See: #131
- Slack notification channel. See: #132
- RV notice replacements. See: #129

## v160707.2080

- Bug fix. #109 regression.

## v160628.26132

- Enhancing MacOS Notification Center integration.
- Adding support for token replacement in `.bash` scripts.
- Enhancing version token replacement patterns.

## v160627.38807

### Most Important Changes

- **IMPORTANT:** New required `.build.props` property: `project_text_domain`
- **IMPORTANT:** New required `.build.props` property for lite variation: `project_lite_text_domain`
- If you are missing either of these new properties Phing will fail validation and you will be warned that a property is missing.
- **IMPORTANT:** As noted below, many of the pattern sets were updated in this release. Please review your next build carefully in case there are any new bugs. In particular, please be sure to review the files that make it into the final ZIP distro, as well as the final Lite repo at GitHub. I don't believe there are any problems and it should be _more_ accurate now), but given the number of changes to the pattern sets in this release, it's worth your time to do a quick review just to be sure.

### Additional Changes in This Release

- **New Wiki Article:** https://github.com/websharks/phings/wiki/Build-Props

- **New Feature:** If you're on a Mac and you have [`terminal-notifier`](https://github.com/julienXX/terminal-notifier) installed, a completion notification will now be displayed on success. Chances are, you already have this installed. You can type `$ which terminal-notifier` to check. If not, install it via Homebrew by typing: `$ brew install terminal-notifier`. Note also that Terminal Notifier can be configured from your system settings on a Mac; i.e., you can disable this if you'd like, or silence them, etc. See: **System Preferences → Notifications → `terminal-notifier`** for details.

- Reorganized all pattern sets. Now using a layered approach that is based on our `.gitignore` and `.gitattributes` file for better consistency and easier maintenance.

- Adding `defaultExcludes="false"` to all `<fileSet>` tags now that there is a more comprehensive approach being taken with exclusions (i.e., pattern sets were drastically improved in this release).

- Refactor: `_is_wp_core_framework_project` now `_is_core_project`.
- Refactor: `_is_lite_build` now `_doing_lite_build`.
- Refactor: `_has_lite_build_props` now `_has_lite_variation`.

- Adding GitHub credential validator. Now required to finish a release.

- Adding Slack credential validator. Now required to finish a release or update bleeding edge.

- Correcting indentation in all files; i.e., no need to indent inside `<?xml>` tag.

- Adding `phingVersion="2.14.0"` to main project; i.e., this version of Phing is now a strict requirement.

- Bug fix. The `_target` property during a lite-only build should be set to `build-lite`.

### Full List of All Changed Files

- See: https://github.com/websharks/phings/pull/125

## v160624.36916

- Nasty bug related to `@since` getting mangled during a release build. Fixed in this release. Referencing: #109

## v160623.42648

- Fix typo in release notification.

## v160623.42457

- Bug fix in lite clone. See: #114
- Exclude `.github` folder. See: #113
- Set `user.email` in lite repo clone. See: #117
- Adding `${_project_build_version}` in build directory phase. See: #111
- Auto-replace `@since $v` or `@since [0-9]{2}[xX]{4}` during a release build. See: #109
- `adHocSlackNotify()` See: #108 and review README for this repo.
- Adding support for `## $v` in `CHANGELOG.md` instead of the longer replacement code that is more difficult to type out all the time.

## 160531

- Now possible to build and release `websharks/phings` using `websharks/phings` :-)
- Adding `version.txt` for bleeding edge distros also, so systems can query the bleeding edge build version.
- Moving bleeding edge distro URLs from `/software/latest/bleeding-edge` to `/software/bleeding-edge` in order to avoid namespace conflicts in the `/latest/` directory and to make room for additional distro types in the future. I'm making this change while I can still improve this; i.e., before these bleeding edge URLs are circulated.

## 160530

- `$ phing release` now requires that you install the AWS CLI Tools. See: <https://github.com/websharks/phings/wiki/AWS-Uploads>

- New command `$ phing update-bleeding-edge`. See: <https://github.com/websharks/phings/wiki/AWS-Uploads#using--phing-update-bleeding-edge>

- Refactored ZIP/TGZ generation. Now calling `zip`, `unzip`, and `tar` directly, but still using `<copy toDir="">` in Phing, along with the same include/exclude patterns as before.

  The goal here was to remove our dependency on the built-in ZIP/TAR tasks in Phing, because they do not support some advanced features, such as the ability to preserve permissions in ZIP files. Fixed in this release. Props @raamdev for his research assistance and for reposting a report in https://github.com/websharks/phings/issues/97

  _Note also that a new directory is added to `.~build/.~/pkg-dirs/for-zip-tgz` for review. The `.zip` and `.tar.gz` distros are based on this directory, and this directory is created using our existing ZIP/TGZ pattern sets for inclusion/exclusion._

## 160528

- Enhancing `$ phing feature-start` and  `$ phing release`

- Enhanced `$ phing release` validation when finishing. Always check to be sure the dev branch is up-to-date before finishing, in the same way we check the master branch. This slid by because originally I was not back-merging master into dev, so it didn't matter quite so much. This has been fixed in v160528, making `$ phing release` more bulletproof.

- Removing unnecessary/overlapping git changes that impacted the master branch in target `-variations-lite-repo-update`. That target is a `-variations-lite-release` dependency and it's only job is to update the dev branch to the latest build. Not to make any changes to the master branch. Changes to the master branch should only occur during a formal release, and only in the `-variations-lite-release` target. Fixed in this release of the Phing release system. Not really a bug. More of an organizational issue.

- Drastically reducing the odds of there being any merge conflict during the lite release process by enhancing validation sub-routines and then using a more logical merge strategy option given the way that we handle lite releases; i.e., the dev branch is always king during a release, because it contains the latest build, updated via Phing target `-variations-lite-repo-update`.

  So when merging dev into master, set `--strategy-option=theirs` (favoring dev at all times, should there be a conflict). This allows Git to resolve any conflicts automatically, always in favor of the dev branch, which is always going to be the case, even if we did it manually.

- I am now back-merging master into dev when doing a lite release also, since it is conceivable that the master branch could (at times, depending on the project lead), contain commits not yet seen in the dev branch. Given the aforementioned merge strategy option, this is of little consequence, but the commit history should still be updated properly by back-merging master into dev after the release is done. For this reason, after a lite release, master is back-merged into the dev branch with `--strategy-option=ours` (favoring dev at all times, should there be a conflict). This ensures both branches have a matching history when the release is done.

- Cleaned up the output produced by `$ phing release`; i.e., removing unnecessary backticks not parsed by a terminal anyway and generally improving the feedback given to the project lead during a release.

- New ad-hoc task added to our Phing library called `<adHocUserSpecificGitChange>`. This impacts the `$ phing feature-start` (alias: `$ phing feature`) targets. Whenever a new feature branch is started, by default, a PR is opened also. In order for that to work I use a `.gitchange` file that is automatically incremented to the latest timestamp. Thereby forcing a change to occur and allowing a PR to be opened whenever the feature branch is first created; i.e., in anticipation of future commits. This prevents the developer working on the feature branch from needing to open a PR in their browser later.

  While this technique has worked well for me, a problem arises whenever multiple developers are using `$ phing feature-start`. In the past, I was the only one making changes to the `.gitchange` file. However, if multiple developers change this file by opening feature branches of their own, then there is the potential for each PR to create a merge conflict with the others with respect to the `.gitchange` file.

  To avoid this issue, the `<adHocUserSpecificGitChange>` task will intelligenty identify the current developer and build a unique string based on several environment variables concatenated together and hashed via `sha1()`. In this way, whenever the `.gitchange` file is altered, it is altering a specific line that identfies the current developer, followed by a `uniqid()` instead of a timestamp. So the effect is still the same, but now the change occurs always on a line that is unique to the user running `$ phing feature`, which avoids the multi-user issue and eliminates the potential for merge conflicts as a result of using this tool.

- Enhanced this article. See: <https://github.com/websharks/phings/wiki/GitHub-Releases>

- Enhanced this article. See: <https://github.com/websharks/phings/wiki/GitHub-Features>

- Enhancing `$ phing feature-start` by having it pull the latest dev branch automatically whenever a new feature branch is created. I was doing this myself, but now that I'm exposing this tool to others it should be more bulletproof. Whenever a new feature branch is started it should always start from the latest remote dev branch. Fixed in this release.

## 160527

- Renamed `$ phing rc-release` to `$ phing release-rc`.

- Enhanced `$ phing release` (and related) functionality. See updated Wiki article: https://github.com/websharks/phings/wiki/GitHub-Releases and these checked-off implementations suggested by @raamdev. https://github.com/websharks/phings/issues/101

- Added support for feature branch start/finish actions following the WS Hubflow model; i.e., I ported by custom bash scripts into Phing and documented them there. See: https://github.com/websharks/phings/wiki/GitHub-Features

## 160526

- [x] Adding support for `project_required_os` in https://github.com/websharks/phings/issues/98
- [x] Adding support for `project_php_required_bits` in https://github.com/websharks/phings/issues/98
- [x] Adding support for `project_php_required_extensions` in https://github.com/websharks/phings/issues/98
- [x] Support for `%now` in version strings.
  - Suggested use: `project_version = %y%m%d.%now`
  - `%now` = `time() % 86400` ... See also: http://semver.org/
  - e.g., `160525.49351`, where `.49351` is a minor version represented by the current number of seconds into the current day. Using versions like this in our build process can make it easier to maintain projects that are commonly updated more than once each day; e.g., the WPSC.
- [x] ~~Noting that `$ phing release` depends on a PEAR extension.~~
  - ~~`$ pear install VersionControl_Git-0.4.4;` on a Mac.~~
  - I removed calls that relied on this extension, in favor of `<exec command="git ...`.
- [x] Resolved issue in https://github.com/websharks/phings/issues/90 & resolved issue in https://github.com/websharks/phings/issues/88 (however, see note below).
- [x] Fix bug that prevents namespace updates (sometimes) in core rebranding via `composer install`.
- [x] Adding support for a new CLI switch: `$ phing release -D interactive=true`. The `interactive` flag is off by default now, so that it's not necessary to answer prompts. If you want to take extra care during a release you can enter interactive mode where you are given a choice before things occur; e.g., prompted to commit and push changes in lite repo variation. However, I consider this interactive mode to be deprecated now; i.e., that's why it's off by default now. The next checklist items covers some of the new `$ phing release` functionality. Given the new functionality, it's not expected that an operator would need to answer prompts during an automated release process.
- [x] Optimize autoloader built by Composer.
- [x] Teach the Phing system how to do GitHub releases following our Git workflow standards. See also: https://github.com/websharks/phings/wiki/GitHub-Releases

## 160517

- Bourbon exclusions. See: #92
- Bug fix in lite patterns. See: https://github.com/websharks/phings/issues/95

## 160418

- Improving preamble.
- Bug fix. `<elseif>` nested conditionals.
- Adding support for Linux x86_64 when satisfying dependencies.
- Better detection of framework and better separation of handlers and POT generation.

## 160416

- All dependencies are now satisfied by the Phing build script itself the first time you run it, and/or in the future should specific version requirements need to change. At this time, dependencies include: APIGen, CasperJS, Composer, PhantomJS, PHP Code Sniffer, PHPUnit, and the WP i18n Tools.

- Reorganized targets into sub-directory classifications; e.g., all build targets are now in `targets/builds` and each set of builds are now nested into sub-directories indicating which phase they run in. For instance, `/in-base-dir`, `/in-base-dir-after`, `/in-build-dir`, `/in-build-dir-after`, etc.

- Several subtle enhancements and minor bug fixes throughout; e.g., improved exclusion patterns to reduce the time it takes to complete a build, additional Phing attributes throughout in order to improve consistency from one target to another, along with a better naming convention for targets and temporary target-specific variables which are now nested into sub-directories, and into separate Phing projects referenced via `<phingCall>` which puts each target into its own local scope as a way to avoid collisions.

- New build targets. Related (somewhat) to #80, though additional work may be needed to accomplish everything we want to at some point in the future.

- Updated (and new) build targets are as follows. **See:** [new wiki article](https://github.com/websharks/phings/wiki/Build-Targets) that lists all possible targets.

- Bug fix. Large files were sometimes being emptied out (YIKES, reported by @jaswsinc) and sometimes they were just stalling (YIKES, reported by @raamdev) and this seems to have been caused by i18n regex patterns that were in need of optimization. I was able to reproduce this against `classes/MenuPageOptions.php` in the Comet Cache software (a very large file) and the i18n text-domain regex patterns. Careful optimizations were made to these routines in order to resolve this issue. In addition, our Phing build script now runs `ini_set('pcre.backtrack_limit', (string) PHP_INT_MAX);` to help prevent random failures against very large files in the future.

- Bug fix. New ad hoc task deals w/ changelog extraction for lite pushing properly. See: #8. See also: `setups/adhocs/extract-changelog-for-version.xml`. Note that changelog extraction for a specific version requires that each of your version headers in the `CHANGELOG.md` file be in one of these formats: `= [version] =`, `= v[version] =`, `## [version]`, or `## v[version]`. Actually, `##` is not required if you use ATX-style headers. If you use ATX-style headers you may use any number of `#` markers; i.e., one `#` (or more) will do fine.

- Dotbuilds (i.e., `.build.php` files) are now processed in both the project base directory and also in the `.~build/${project_slug}` directory; i.e., if you name the file `.build.php` it runs in both directories (backward compatibility was preserved). **New:** To limit the scope of these files, you can change the name to either: `.build.in-base-dir.php` or `.build.in-build-dir.php` to get more specific about which phase you want your custom sub-routines to run in.

- The `-js-css` target (now named `-builds-in-build-dir-js-css-cleanup`) now runs in the `.~build/${project_slug}` directory phase, because it's only job is to tidy-up JS/CSS files before packaging compressed archives for distribution.

- Bug fix. ZIP and TGZ archives were incorrectly excluding `.ht*` files such as `.htaccess` in the packaging phase. While these files are not important when building a PHAR archive, they _are_ important to ship with a plugin (i.e., in `.tgz` and `.zip` files) for security purposes; e.g., to prevent direct access to files not intended for a web server.

- Improved the lite push target by accepting either `y` or `yes` as an answer to prompts, and it is no longer caSe-sensitive either.

- Improved the lite push target by adding `checkReturn="true"` to all `<exec>` tags; i.e., to be sure each command succeeds before continuing.

- Optimized the lite push target by excluding `/src/vendor` from the repo content that is pushed to the remote for the lite variation. The `/src/vendor` directory should not be included because that is handled by Composer via the `/composer.json` file in this repo; i.e., those are external dependencies that are not a part of the lite repo itself.

- Optimized the lite push target by adding the `depth="1"` attribute to the `<gitClone>` tag; i.e., only clone the last history phase, which reduces download time and bandwidth.

- Adding new exclusions to the archive generators: `ISSUE_TEMPLATE.md` and `PULL_REQUEST_TEMPLATE.md` are now excluded also. See also: `setups/patterns/*.xml`.

- Removed exclusions from archive generators: `AUTHORS.txt` and `CONTRIBUTORS.txt` are now unnecessary to exclude, as we already cover the `.md` version of these files; i.e., we don't have the `.txt` variations anyway, and that just adds additional fluff to an already long list of exclusions. Removing to clean things up just a bit. See also: `setups/patterns/*.xml`.

- New pattern sets in `setups/patterns/*.xml`: `_token_pattern_set`, `_wp_token_pattern_set`, `_dotbuilds_pattern_set`, `_text_based_pattern_set`, `_php_pattern_set`, `_js_css_pattern_set`, and `_lite_repo_pattern_set`. These are designed to keep things DRYer.

- In `targets/setups/patterns.xml`, all `<fileSet>` tags were changed to `<patternSet>` tags in order to make them slightly more versatile.

- Improving support for `.x-php` files throughout. These should be considered PHP files also, and therefore all PHP-related routines should search/replace/include those files when performing various operations. The `.x-php` extension is something that WebSharks uses for any type of PHP file that should not actually be processed by a web server; e.g., files that serve only as a template for the generation of something else; or files that serve only as example API calls, etc. Since these files may also contain namespace references or tokens that need to be replaced, they must be processed in the same way regular PHP files are—during the build phase.

  **Note:** We should try to update things like `advanced-cache.txt` to `advanced-cache.x-php` in the Comet Cache plugin, at which time the `.build.props` could be updated to remove `project_lite_alter_namespace_in_other_files_pattern`.

- Now skipping POT generation for the lite build variation. See: <https://github.com/websharks/phings/issues/51#issuecomment-191911351>.

- Now enforcing a text-domain that will always exclude any `-lite|pro` suffix; i.e., always use the base plugin slug as the i18n text-domain. See: <https://github.com/websharks/phings/issues/51#issuecomment-191911351>.

- All target-specific validators have been improved with respect to the `.~build/${project_slug}` directory being necessary; e.g., the linters, the codex, tests, and distro-related targets all require the project to have already been built first before they can be run. This is now enforced, and now instead of deleting the entire `.~build/` directory at the beginning of every `$ phing` call, the `.~build/` directory can be preserved, and only sub-directories it contains are overwritten as needed; i.e., to perform an action being requested. These improvements are also being implemented in an effort to help separate the lite|pro build routines (more on this below), so that it's possible to build one or the other instead of always both at the same time.

- Reducing the amount of output during a build (slightly) by removing overly verbose output like: "Deleting previous: ..." which was already followed by output from Phing itself.

- Moving all hidden `-setup-*` targets into `<project>` scope (via imports only) to reduce the number of times each individual setup target needs to be listed in various (visible) build targets. See: `targets.xml` and `imports.xml` for more information.

- Removing support for `$ phing ... -D composer-lock-preserve=true` in favor of that being the default, and now we have a new flag called `$ phing ... -D composer-lock-delete=true` to disable it. The default value can always be overridden by passing `$ phing ... -D composer-lock-delete=true|false`. Or, before running Phing you can simply delete the `composer.lock` file yourself if you want to delete it; i.e., not preserve dependency versions. See also: [It's All About the `.lock` File](https://blog.engineyard.com/2014/composer-its-all-about-the-lock-file) for more information. Also, as a part of the reorganized codebase structure, the `-composer-lock-preserve` target was consolidated into a single target that reads the new flag.

- Bug fix. Adding `return` to regex `(namespace|use|return)` when replacing namespace references in various files. See #83.

- Bug fix. Exclude `.build.php` and `.build.*.php` files from TGZ and ZIP distro files. See also: `setups/patterns/lite-repo.xml`.

- Bug fix. Excluding `/assets` from lite push to remote repo. These assets should only be seen the pro repo. This also avoids PEAR compatibility issues with the Git LFS protocol. See also: `setups/patterns/lite-repo.xml`.

- Bug fix. Excluding `.gitmodules` from lite push to remote repo. There are no submodules in the final lite repo. This also avoids PEAR compatibility issues w/ recursive cloning. See also: `setups/patterns/lite-repo.xml`.

- Bug fix. Always look for a leading `\` slash when performing any type of namespace replacement.

- Completed a new round of tests against all build targets after the changes above.

## 160411

- Support for `/*[pro strip-file-from="lite"]*/`. See: #73

## 160410

- Bug fix related to Composer. See: #71

## 160409

- Bug fix related to lite builds. See: #69

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
