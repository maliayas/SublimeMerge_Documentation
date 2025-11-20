# Sublime Merge Documentation Mirror

This repo tracks the changes in
[Sublime Merge documentation](https://www.sublimemerge.com/docs/).

The source is automatically fetched daily and if something new is found, it gets
committed automatically. Then I review it and push to this repo manually.

I create git tags for notesworthy commits, so you can subscribe to the
[tags](https://github.com/maliayas/SublimeMerge_Documentation/tags)

## Update Script

The script that fetches fresh content and updates the git repo is below. The
operation stands on `wget`.

```sh
# Delete existing files.
rm -rf www.sublimemerge.com

# Download complete web page.
wget \
    --mirror \
    --no-parent \
    --page-requisites \
    --convert-links \
    --continue \
    --adjust-extension \
    --user-agent="" \
    --execute="robots=off" \
    --wait=1 \
    --append-output="mirror.log" \
    --no-verbose \
    https://www.sublimemerge.com/docs/

# Prettify static files for better diffs.
stylelint --fix --config "~/.stylelintrc.js" "www.sublimemerge.com/**/*.css"

# Commit if there is something new.
git add .
git commit -m "Update ($(date +%Y-%m-%d))"
```

My `.stylelintrc.js` config is as below:

```js
module.exports = {
    "rules": {
        "at-rule-no-unknown": true,
        "block-closing-brace-empty-line-before": "never",
        "block-closing-brace-newline-after": "always",
        "block-closing-brace-newline-before": "always",
        "block-opening-brace-newline-after": "always",
        "block-opening-brace-space-before": "always",
        "color-hex-case": "upper",
        "color-hex-length": "long",
        "color-named": "never",
        "color-no-invalid-hex": true,
        "comment-no-empty": true,
        "comment-whitespace-inside": "always",
        "declaration-bang-space-after": "never",
        "declaration-bang-space-before": "always",
        "declaration-block-no-duplicate-properties": [
            true, {
                "ignore": ["consecutive-duplicates-with-different-values"]
            }
        ],
        "declaration-block-no-shorthand-property-overrides": true,
        "declaration-block-semicolon-newline-after": "always",
        "declaration-block-semicolon-space-before": "never",
        "declaration-block-trailing-semicolon": "always",
        "declaration-colon-space-after": "always",
        "declaration-colon-space-before": "never",
        "font-family-name-quotes": "always-unless-keyword",
        "font-family-no-duplicate-names": true,
        "function-comma-space-after": "always",
        "function-parentheses-space-inside": "never",
        "function-url-quotes": "always",
        "function-whitespace-after": "always",
        "indentation": 4,
        "linebreaks": "unix",
        "max-empty-lines": 3,
        "media-feature-colon-space-after": "always",
        "media-feature-colon-space-before": "never",
        "media-feature-name-no-unknown": true,
        "media-feature-parentheses-space-inside": "never",
        "media-feature-range-operator-space-after": "always",
        "media-feature-range-operator-space-before": "always",
        "media-query-list-comma-space-after": "always",
        "media-query-list-comma-space-before": "never",
        "no-duplicate-at-import-rules": true,
        "no-duplicate-selectors": true,
        "no-empty-first-line": true,
        "no-empty-source": true,
        "no-eol-whitespace": true,
        "no-extra-semicolons": true,
        "no-invalid-double-slash-comments": true,
        "no-missing-end-of-source-newline": true,
        "no-unknown-animations": true,
        "property-case": "lower",
        "property-no-unknown": true,
        "selector-attribute-brackets-space-inside": "never",
        "selector-attribute-operator-space-after": "never",
        "selector-attribute-operator-space-before": "never",
        "selector-attribute-quotes": "always",
        "selector-class-pattern": "^[a-z0-9\-]+$",
        "selector-combinator-space-after": "always",
        "selector-combinator-space-before": "always",
        "selector-descendant-combinator-no-non-space": true,
        "selector-id-pattern": "^[a-z0-9\-]+$",
        "selector-list-comma-newline-after": "always",
        "selector-list-comma-space-before": "never",
        "selector-max-empty-lines": 0,
        "selector-pseudo-class-case": "lower",
        "selector-pseudo-class-no-unknown": true,
        "selector-pseudo-class-parentheses-space-inside": "never",
        "selector-pseudo-element-case": "lower",
        "selector-pseudo-element-colon-notation": "double",
        "selector-pseudo-element-no-unknown": true,
        "selector-type-case": "lower",
        "selector-type-no-unknown": true,
        "string-no-newline": true,
        "string-quotes": "double",
        "unit-case": "lower",
        "unit-no-unknown": true,
        "value-keyword-case": "lower",
        "value-list-comma-newline-after": "never-multi-line",
        "value-list-comma-newline-before": "never-multi-line",
        "value-list-comma-space-after": "always",
        "value-list-comma-space-before": "never",
    }
};
```
