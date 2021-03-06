TYPO3 CMS Composer installers
=============================

This package acts as composer plugin in order to download and install
TYPO3 core and extensions and put them into a directory structure
which is suitable for TYPO3 to work correctly.

The behavior of the installer can be influenced by configuration in the `extra` section of the root `composer.json`

```
  "extra": {
      "typo3/cms": {
          "web-dir": "web",
          "prepare-web-dir": true,
          "cms-package-dir": "{$vendor-dir}/typo3/cms"
      }
    }
```

#### `web-dir`
You can specify a relative path from the base directory, where the public document root should be located.
Links to the `typo3` folder and the `index.php` will be established in this folder by the installer.

*The default value* is `""`, which means next to your root `composer.json`. This default value is kept for compatiblity reasons, but is recommended to have the document root in a separate folder so that the vendor folder and the `composer.lock` file are not accessible.

#### `prepare-web-dir`
Whether or not links to the `typo3` folder and the `index.php` will be established in the web directory.
At a later point, this option might affect other actions like publishing assets.

*The default value* is `true`.

#### `cms-package-dir`
You can specify a relative path from the base directory, where the typo3/cms package should be installed into.

*The default value* is `"typo3_cms"`. This default value is kept for compatiblity reasons, but is recommended to let typo3/cms being installed in the vendor directory, which is possible with the example configuration outlined above.

#### `config-dir`
You can specify a relative path from the base directory, where the configuration folder is located.
By default extensions will be installed in a sub directory `ext` within this directory.

*The default value* is `"{$web-dir}/typo3conf"`.

#### `extension-dir`
You can specify a relative path from the base directory, where the extensions should be installed into.

*The default value* is `"{$config-dir}/ext"`. TYPO3 requires extensions to be present in `typo3conf/ext` If this value is changed, a proper publication (link or copy) of the extensions into this directory must be taken care of manually.

#### `imply-extension-key`
If this value is `true`, the name of the extension directory is implied by the first replace entry.
If a replaces section is not present in the extensions `composer.json`, the second part of the vendor name is used, but all dashes (`-`) are converted to underscores (`_`).

Example:
```
    "name": "vendor/my-fancy-extension",
```
In this case an extension directory with the name `my_fancy_extension` is implied.
However, it is highly recommended to add a replace section in the `composer.json`.

Example:
```
    "name": "vendor/my-fancy-extension",
    "replace": {
        "my_extension": "self.version"
    }
```

In this case, the install directory `my_extension` would be used, because the replace section takes precedence.

If the value is set to `false`, the package name is used as directory name.
TYPO3 assumes extensions to be present in a directory below `typo3conf/ext`.
If this value is set to `false`, the extensions need to be copied or linked to this directory manually!

*The default value* is `true`.

## Feedback/ Bugreports/ Contribution

Bug reports, feature requests and pull requests are welcome in the Github repository: https://github.com/TYPO3/CmsComposerInstallers/
