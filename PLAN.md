# PLAN

## Understand

Issue #148 reports that the skill extractor does not reliably detect JavaScript and TypeScript from source-code content.

The original implementation mainly depended on file extensions, `package.json`, and limited import patterns. This caused common JavaScript and TypeScript syntax to be missed when no filename was provided.

The issue was reproduced on `origin/main` using the focused skill extractor tests:

```bash
pytest -q tests/unit/test_skill_extractor.py \
  -k "javascript_detection or typescript_files"
```

Both tests failed on `origin/main` and passed on the feature branch.

## Map

The main implementation file is:

`ingestion/parsers/skill_extractor.py`

The relevant method is:

`SkillExtractor._detect_languages()`

The unit tests are located in:

`tests/unit/test_skill_extractor.py`

The affected tests are:

- `test_text_with_typescript_files`
- `test_javascript_detection`

## Plan

1. Separate JavaScript and TypeScript evidence collection.
2. Detect TypeScript using `.ts` and `.tsx` filenames.
3. Detect TypeScript declarations such as `interface`, `type`, `enum`, and `namespace`.
4. Detect TypeScript primitive type annotations such as `string`, `number`, and `boolean`.
5. Detect JavaScript using `.js` and `.jsx` filenames.
6. Detect CommonJS and ES module imports, including `require(...)`.
7. Detect JavaScript variable declarations using `const`, `let`, and `var`.
8. Preserve the existing confidence scoring and evidence structure.
9. Run the focused JavaScript and TypeScript tests.
10. Run the broader skill extractor test suite and document unrelated failures separately.

## Inputs and Outputs

### Inputs

- Source-code or documentation text
- Optional filename

### Outputs

A list of `SkillDetection` objects containing:

- Skill name
- Category
- Confidence score
- Detection evidence

## Risks and Unknowns

- JavaScript, TypeScript, and Python share some syntax.
- Generic imports may create false positives.
- TypeScript code may also contain standard JavaScript syntax.
- Mixed-language files may detect multiple languages.
- Existing Python detection must continue working.
- The repository contains an unrelated broken PostgreSQL unit test.

## Edge Cases

- JavaScript code without a filename
- TypeScript code without a filename
- `.jsx` and `.tsx` files
- `require('module')` syntax
- ES module imports
- TypeScript interfaces and type aliases
- TypeScript primitive type annotations
- Mixed-language source text
- Empty input
- Unrecognized text