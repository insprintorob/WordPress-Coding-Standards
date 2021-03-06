# Change Log
All notable changes to this project will be documented in this file.

This projects adheres to [Semantic Versioning](http://semver.org/) and [Keep a CHANGELOG](http://keepachangelog.com/).

## [Unreleased]

### Added
- Sniff to flag dynamic translatable strings and textdomains.
- `get_children()`, `wp_get_object_terms()`, `wp_get_post_(categories|tags|terms)()`, 
`get_category_by_slug()`, `get_cat_ID()`, `count_user_posts()`, and `wp_old_slug_redirect()` 
to the list of restricted functions in the `WordPress.VIP.RestrictedFunctions` sniff.

## [0.6.0] - 2015-06-30

### Added
- Support for `wp_cache_add()` and `wp_cache_delete()`, as well as custom cache 
functions,in the `WordPress.VIP.DirectDatabaseQuery` sniff.

### Removed
- `WordPress.Functions.FunctionRestrictions` and `WordPress.Variables.VariableRestrictions` 
from the `WordPress-VIP` standard, since they are just parents for other sniffs.

## [0.5.0] - 2015-06-01

### Added
- `WordPress.CSRF.NonceVerification` sniff to flag form processing without nonce verification.
- `in_array()` and `is_array()` to the list of sanitizing functions.
- Support for automatic error fixing to the `WordPress.Arrays.ArrayDeclaration` sniff.
- `WordPress.PHP.StrictComparisions` to the `WordPress-VIP` and `WordPress-Extra` rulesets.
- `WordPress-Docs` ruleset to sniff for proper commenting.
- `Generic.PHP.LowerCaseKeyword`, `Generic.Files.EndFileNewline`, `Generic.Files.LowercasedFilename`, 
`Generic.Formatting.SpaceAfterCast`, and `Generic.Functions.OpeningFunctionBraceKernighanRitchie` to the `WordPress-Core` ruleset.
- `Generic.PHP.DeprecatedFunctions`, `Generic.PHP.ForbiddenFunctions`, `Generic.Functions.CallTimePassByReference`, 
`Generic.Formatting.DisallowMultipleStatements`, `Generic.CodeAnalysis.EmptyStatement`, 
`Generic.CodeAnalysis.ForLoopShouldBeWhileLoop`, `Generic.CodeAnalysis.ForLoopWithTestFunctionCall`, 
`Generic.CodeAnalysis.JumbledIncrementer`, `Generic.CodeAnalysis.UnconditionalIfStatement`, 
`Generic.CodeAnalysis.UnnecessaryFinalModifier`, `Generic.CodeAnalysis.UselessOverridingMethod`, 
`Generic.Classes.DuplicateClassName`, and `Generic.Strings.UnnecessaryStringConcat` to the `WordPress-Extra` ruleset.
- Error for missing use of `wp_unslash()` on superglobal data to the `WordPress.VIP.ValidatedSanitizedInput` sniff. 

### Changed
- The `WordPress.VIP.ValidatedSanitizedInput` sniff to require sanitization of input even when it is being directly escaped and output.
- The minimum required PHP_CodeSniffer version to 2.2.0.
- The `WordPress.VIP.ValidatedSanitizedInput` and `WordPress.XSS.EscapeOutput` sniffs: 
the list of escaping functions was split from the list of sanitizing functions. The `customSanitizingFunctions` 
property has been moved to the `ValidatedSanitizedInput` sniff, and the `customEscapingFunctions`
property should now be used instead for the `EscapeOutput` sniff.
- The `WordPress.Arrays.ArrayDeclaration` sniff to give errors for `NoSpaceAfterOpenParenthesis`, `SpaceAfterArrayOpener`, and `SpaceAfterArrayCloser`, instead of warnings.
- The `WordPress.NamingConventions.ValidFunctionName` sniff to allow camelCase method names in classes that implement interfaces.

### Fixed
- The `WordPress.VIP.ValidatedSanitizedInput` sniff not reporting missing validation when reporting missing sanitization.
- The `WordPress.VIP.ValidatedSanitizedInput` sniff flagging superglobals as needing sanitization when they were only being used in a comparison using `if` or `switch`, etc.

## [0.4.0] - 2015-05-01

### Added
- Change log file.
- Handling for string-interpolated input variables in the `WordPress.VIP.ValidatedSanitizedInput` sniff.
- Errors for using uncached functions when cached equivalents exist.
- `space_before_colon` setting for the `WordPress.WhiteSpace.ControlStructureSpacing` sniff, for control structures using alternative syntax. Possible values: `'required'`, `'optional'`, `'forbidden'`.
- Support for `sanitization` whitelisting comments for the `WordPress.VIP.ValidatedSanitizedInput` sniff.
- Granular error/warning names for all errors and warnings.
- Handling for ternary conditions in the `WordPress.XSS.EscapeOutput` sniff.
- `die`, `exit`, `printf`, `vprintf`, `wp_die`, `_deprecated_argument`, `_deprecated_function`, `_deprecated_file`, `_doing_it_wrong`, `trigger_error`, and `user_error` to the list of printing functions in the `WordPress.XSS.EscapeOutput` sniff.
- `customPrintingFunctions` setting for the `WordPress.XSS.EscapeOutput` sniff.
- `rawurlencode()` and `wp_parse_id_list()` to the list of "sanitizing" functions in the `WordPress.XSS.EscapeOutput` sniff.
- `json_encode()` to the list of discouraged functions in the `WordPress.PHP.DiscouragedFunctions` sniff, in favor of `wp_json_encode()`.
- `vip_powered_wpcom()` to the list of auto-escaped functions in the `WordPress.XSS.EscapeOutput` sniff.
- `debug_print_backtrace()` and `var_export()` to the list of discouraged functions in the `WordPress.PHP.DiscouragedFunctions` sniff.
- Smart handling for formatting functions (`sprintf()` and `wp_sprintf()`) in the `WordPress.XSS.EscapeOutput` sniff.
- `WordPress.PHP.StrictComparisons` sniff.
- Correct handling of `array_map()` in the `WordPress.VIP.ValidatedSanitizedInput` sniff.
- `$_COOKIE` and `$_FILE` to the list of superglobals flagged by the `WordPress.VIP.ValidatedSanitizedInput` and `WordPress.VIP.SuperGlobalInputUsage` sniffs.
- `$_SERVER` to the list of superglobals flagged by the `WordPress.VIP.SuperGlobalInputUsage` sniff.
- `Squiz.ControlStructures.ControlSignature` sniff to the rulesets.

### Changed
- `WordPress.Arrays.ArrayKeySpacingRestrictions` sniff to give errors for `NoSpacesAroundArrayKeys` and `SpacesAroundArrayKeys` instead of just warnings.
- `WordPress.NamingConventions.ValidFunctionName` sniff to allow for camel caps method names in child classes.
- `WordPress.XSS.EscapeOutput` sniff to allow for integers (e.g. `echo 5` and `print( -1 )`).

### Removed
- Errors for mixed key/keyless array elements in the `WordPress.Arrays.ArrayDeclaration` sniff.
- BOM from `WordPress.WhiteSpace.OperatorSpacing` sniff file.
- `$content_width` from the list of non-overwritable globals in the `WordPress.Variables.GlobalVariables` sniff.
- `WordPress.Arrays.ArrayAssignmentRestrictions` sniff from the `WordPress-VIP` ruleset.

### Fixed
- Incorrect errors for `else` statements using alternative syntax.
- `WordPress.VIP.ValidatedSanitizedInput` sniff not always treating casting as sanitization.
- `WordPress.XSS.EscapeOutput` sniff flagging comments as needing to be escaped.
- `WordPress.XSS.EscapeOutput` sniff not sniffing comma-delimited `echo` arguments after encountering the first escaping function in the statement.
- `WordPress.PHP.YodaConditions` sniff not flagging comparisons to constants or function calls.
- `WordPress.Arrays.ArrayDeclaration` sniff not ignoring doc comments.
- Link to phpStorm instructions in `README.md`.
- Poor performance of the `WordPress.Arrays.ArrayAssignmentRestrictions` sniff.
- Poor performance of the `WordPress.Files.FileName` sniff.

## [0.3.0] - 2014-12-11

### Changed
- Use semantic version tags for releases.
