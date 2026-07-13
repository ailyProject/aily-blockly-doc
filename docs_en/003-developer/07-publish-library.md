# Publish Library

Use **Publish Library** to submit a local Blockly library from the current project to the aily Blockly public library repository so other users can install it.

aily Blockly uses your GitHub account to create or update a pull request (PR). A successful submission means the request has been accepted for processing; it does not mean the library has already passed review or been merged.

## Before You Publish

Make sure that:

- You are signed in to aily Blockly.
- You have a working GitHub account.
- The local library has been imported into the current project.
- The library has passed testing on real hardware.
- Your network can access GitHub.
- The library does not contain passwords, tokens, private addresses, or other sensitive data.

If the library has not been imported yet:

1. Open the project you use to test the library.
2. Open **Library Manager**.
3. Click **Import Local Library**.
4. Select the library root directory.
5. Wait for the import to finish and confirm that the library appears in the Blockly toolbox on the left.

## Check the Library Files

The library root directory must contain at least these files:

```
your-library/
├── package.json
├── block.json
├── toolbox.json
└── generator.js
```

The following files and directories are also recommended:

```
your-library/
├── readme.md       // User documentation
├── readme_ai.md    // AI-oriented documentation, optional
├── src/            // Arduino/C/C++ source code, optional
├── i18n/           // Localization files, optional
└── pinmaps/        // Pin mapping files, optional
```

Before submitting, aily Blockly checks that:

- `package.json`, `block.json`, and `toolbox.json` contain valid JSON.
- `package.json` contains string values for `name` and `version`, and its package name matches the imported library name.
- The top level of `block.json` is a non-empty array and every block has a unique `type`.
- Categories and blocks in `toolbox.json` are valid.
- `generator.js` exists and contains no JavaScript syntax errors.

If a non-empty `src/` directory exists, aily Blockly automatically packages it as `src.7z` during submission. If a non-empty `src.7z` already exists in the library root, that archive is used directly.

See **Library Specification** and **Library Adaptation** for the complete structure and development requirements.

## Test on Real Hardware

The publish form requires you to confirm that the library has passed testing on real hardware. Before submitting, verify at least the following:

- Blocks display, connect, and generate code correctly.
- Generated code compiles for the target board.
- Firmware uploads successfully.
- The main features work correctly on real hardware.
- The compatible boards declared in `package.json` match your test results.

## Open the Publish Form

1. Find the imported local library in the Blockly toolbox on the left.
2. Right-click the library category.
3. Select **Publish Library**.

**Publish Library** appears only in the context menu of a local library. If the option is missing, import the library again through **Library Manager > Import Local Library**.

If you are not signed in, aily Blockly asks you to open **User Center** and sign in. If you are signed in but do not have GitHub PR permission, click **Authorize**, complete authorization in the browser, and return to aily Blockly.

The current workflow requires the GitHub `repo` permission to create or update a PR. Keep aily Blockly open and complete authorization within five minutes when possible. The submission continues automatically after authorization succeeds.

## Complete the Publish Form

| Field | Required | Requirements |
| --- | --- | --- |
| Package name | Yes | Must start with `@aily-project/lib-`. The remaining name may contain only lowercase letters, digits, and hyphens, and must start and end with a letter or digit. Example: `@aily-project/lib-dht11`. |
| Version | Yes | Must use a numeric `major.minor.patch` format such as `1.0.0`. Do not add `v`, dates, or prerelease suffixes. |
| Display name | Yes | The name shown to users in Library Manager and the toolbox, such as “DHT11 Temperature and Humidity Sensor.” |
| Description | No | Briefly describe supported hardware, main features, and intended use cases. |
| PR description | No | Describe the features, reason for publishing, and completed tests. The limit is 2,000 characters. A detailed description helps reviewers. |
| Author | No | Enter the individual, team, or original library author. When using third-party open-source code, preserve its source and license information in `readme.md`. |
| Keywords | No | Separate keywords with commas, for example `sensor, temperature, humidity`. |

You can use this PR description template:

```
Main features:
- (Describe the features included in this release.)

Supported hardware and use cases:
- (List supported boards, sensors, or modules.)

Reason for publishing:
- (Explain why this library should be published.)

Testing:
- aily Blockly version:
- Board and core version:
- Features verified:
- Test result:
```

## Choose Whether to Update Local Metadata

The publish form includes **Save package name, version, display name, description, author, and keywords to the local package.json**. This option is cleared by default.

- Cleared: The form values apply only to this submission and do not modify the local `package.json`.
- Selected: The form values are saved to the local library after the submission succeeds.
- If the package name changes, aily Blockly also renames the local library directory and updates dependency records in the current project.

Select this option after confirming that the form contains the final release metadata. This prevents the local metadata from becoming different from the submitted metadata.

If aily Blockly asks you to reload the project, choose **Reload**. Otherwise, the toolbox and dependency information may continue to show old values.

## Submit the Library

1. Check the package name, version, and PR description.
2. Select **I confirm this library has been tested on real hardware**.
3. Choose whether to sync the values to the local `package.json`.
4. Click **Publish Library**.
5. Wait for the submission accepted message. Do not click the publish button repeatedly.

The submission includes the package configuration, block definitions, code generator, documentation, localization and pin mapping files, and the source archive when present.

## Check Submission Status

After the submission is accepted, the system creates or updates a PR automatically. Click **User Center** in the success message, or open the library submission records in User Center later.

The next steps normally include automated checks and administrator review. Watch your GitHub notifications and account email:

- Approved: The library is merged into the public [aily-blockly-libraries](https://github.com/ailyProject/aily-blockly-libraries) repository.
- Changes requested: Update the local library according to the PR review comments and publish it again with the same package name.
- Rejected: Read the reason, fix the problems, and submit again.

aily Blockly indicates that administrators normally review submissions within 48 hours. Actual review time may vary with submission volume, holidays, and the number of revision rounds.

## Update a Previously Submitted Library

When you publish the same package name again, aily Blockly reports that the library has already been submitted:

- No content changes: Continuing does not create a duplicate PR.
- Content changed: Continuing updates the existing submission record and the backend recreates or updates the PR.
- The name is owned by another user: You cannot overwrite that library. Choose an available package name.

Before publishing a new release, update the version and describe new features, fixes, compatibility changes, and the test environment in the PR description.

## Troubleshooting

### Publish Library is missing from the context menu

The option is shown only for local libraries. Import the library again through **Library Manager > Import Local Library** and confirm that it loads in the toolbox.

### Library information cannot be read or a file is invalid

Common causes include:

- `package.json`, `block.json`, `toolbox.json`, or `generator.js` is missing.
- A JSON file contains comments, a trailing comma, or unmatched brackets.
- `name` in `package.json` does not match the imported library name.
- `block.json` is empty, a block has no `type`, or multiple blocks use the same `type`.
- A category in `toolbox.json` has no `name` or `contents`.
- `generator.js` is empty or contains a syntax error.

Fix the reported problem, reload the project, and publish again.

### The package name already exists or is unavailable

If this is a library you submitted previously, confirm that you want to update it. If it belongs to another user, change the package name. Do not rename only the folder; update `name` in `package.json` as well. You can also change the name in the publish form and enable local metadata sync so aily Blockly updates the local library and project dependencies after submission succeeds.

### Submission does not continue after GitHub authorization

Confirm that authorization completed in the browser and returned to aily Blockly. If more than five minutes elapsed, authorization was canceled, the GitHub credential is invalid, or the `repo` permission is missing, open **Publish Library** and authorize again.

### Packaging `src.7z` fails

Confirm that `src/` is a readable, non-empty directory and that no files are locked by another program. For a manually created `src.7z`, confirm that the archive is not empty and uses `src/` as its top-level directory.

### The toolbox still shows the old name after syncing metadata

Choose **Reload** in the prompt. If you selected **Later**, save and reopen the project for the changes to take effect.

## Pre-submission Checklist

- [ ] The library has been added through **Import Local Library**.
- [ ] All four required files exist and load correctly.
- [ ] The package name follows the `@aily-project/lib-xxx` convention and is not owned by another user.
- [ ] The version uses `x.y.z` and has been updated for this release.
- [ ] `readme.md` documents usage, wiring, dependencies, and third-party licenses.
- [ ] Compilation, upload, and real-hardware operation pass on the target board.
- [ ] The library contains no credentials, secrets, or other sensitive data.
- [ ] The PR description includes the main features, use cases, and test environment.
- [ ] You have decided whether to sync the form values to the local `package.json`.

For additional development and submission requirements, see the [aily-blockly-libraries specification](https://github.com/ailyProject/aily-blockly-libraries/blob/main/%E5%BA%93%E8%A7%84%E8%8C%83.md) and [contribution guide](https://github.com/ailyProject/aily-blockly-libraries/blob/main/CONTRIBUTING.md).
