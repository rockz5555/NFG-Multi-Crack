# Simplified Chinese translation resources (v2.0)

This directory contributes Simplified Chinese translations for the interface shipped in release **200 / v2.0**, based on the arm64-v8a APK. The public repository does not contain the Android application source tree, so these are reviewable integration resources for the maintainer, not an automatically activated application change.

## Contents

- `android/strings.xml`: 121 application-specific Android resources, keyed by the existing resource names. Framework/AndroidX/Material strings are excluded because upstream already bundles those translations.
- `ui-zh.tsv`: translations of literals embedded in native layouts.
- `web-zh.tsv`: help/workspace translations.
- `legacy-zh.tsv`: legacy editor and common dynamic UI translations.
- `web-dictionary.json`: merged 547-entry dictionary, including shared labels from the layout table. Keys normalize whitespace; technical identifiers remain unchanged.

## Integration

1. Merge `android/strings.xml` into the application's `res/values-zh-rCN/strings.xml`, keeping English as the default fallback. Preserve format arguments such as `%1$s`, `%2$d`, and `{0}`.
2. Extract matching literals from layouts into Android string resources and add their Chinese values. Do not change resource IDs, package identifiers, or event handlers.
3. Integrate the web dictionary into the existing locale selection mechanism. Translate text nodes and presentation attributes such as `placeholder` and `title`; exclude scripts, code/pre blocks, textareas, editable content, configuration values, and JSON keys.
4. Review dynamic text in encrypted/runtime code using the original source. This contribution cannot enumerate all such strings from the release APK.

Technical names (Hook, Xposed, BeanShell, API names, class names and configuration enums) are retained where needed. The AI prompt instructions still explicitly request English input, matching the existing application behavior rather than claiming new language support from the model service.

## Validation and scope

The translations were exercised in a local resource-only APK rebuild. Resource compilation, format-placeholder checks, ZIP checks, v1/v2/v3 signing validation of the local artifact, and help-workspace JSON generation passed. DEX/native libraries and existing web logic were preserved. Mobile-width help/editor pages were inspected, and no page errors occurred in the exercised flow.

Android installation and runtime behavior have **not** been tested. Encrypted runtime messages, remote content, image text and unmatched dynamic UI may remain English. This PR includes no APK, signing key, runtime library, decrypted code, or changes to the hook/configuration databases.
