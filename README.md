# Banking apps compatibility with GrapheneOS

Report and track international banking app compatibility with GrapheneOS, including which workarounds may be required.

## Tablet of Contents

- [Introduction](#introduction)
- [Usage](#usage)
- [Workarounds](#workarounds)
- [Notes](#notes)

# Introduction

A crowd-sourced project dataset for [GrapheneOS](https://grapheneos.org/) users on [supported devices](https://grapheneos.org/faq#supported-devices), featuring a maintained compatibility [list of tested international banking apps](https://privsec.dev/posts/android/banking-applications-compatibility-with-grapheneos/#international-banking-apps), which is [reviewed](https://github.com/PrivSec-dev/banking-apps-compat-report/issues?q=is%3Aissue+is%3Aclosed) and [published](https://privsec.dev/banking). 

[PrivSec.dev](https://privsec.dev) hosts this 3rd-party community-sourced effort, offering detailed information and which[ workarounds](https://akc3n.page/posts/banking-app-issues/) may be required for banking apps compatibility with GrapheneOS.

## It is essential to note that GrapheneOS:
- **[does not](https://grapheneos.org/usage#banking-apps:~:text=grapheneos%20does%20not%20make%20any%20guarantees%20regarding%20the%20list's%20validity.) make any guarantees regarding the list's validity**
- users should read the [banking apps usage guide](https://grapheneos.org/usage#banking-apps)
- provides a detailed [attestation compatibility guide](https://grapheneos.org/articles/attestation-compatibility-guide) for banking app developers
  
# Usage

- View [current list ](https://privsec.dev/posts/android/banking-applications-compatibility-with-grapheneos/#international-banking-apps)of working international banking apps compatibility with GrapheneOS.  
- See [issue tracker](https://github.com/PrivSec-dev/banking-apps-compat-report/issues) for detailed banking app reports. As well as search, track, and/or update report status.  
- Submit a banking app report by [opening a new issue and filling out the form](https://github.com/PrivSec-dev/banking-apps-compat-report/issues/new?assignees=&labels=app+report&projects=&template=app_report.yml&title=%5BReplace+this+with+the+name+of+your+banking+app%5D).

---

## Workarounds

0. Potential use of an unofficial/alternative Google Play Store frontend client may be [problematic](https://akc3n.page/posts/banking-app-issues/#auroraoss-is-problematic) for misguided apps:

- That can check if they were installed from the Play Store and can choose to refuse to work if they were not installed from the Play Store.
- Try to hinder reverse engineering using debugging features like ptrace
- Some forbid usage on non-stock OS (most OSes are insecure)
- May cause your Google Account to be disabled/blocked/blacklisted by Google.
- [Anonymous account](https://twitter.com/GrapheneOS/status/1661989816584511489) usage may have negative consequences and have a less secure connection to the Play Store servers.

General recommendation: [Install Sandboxed Google Play](https://grapheneos.org/usage#sandboxed-google-play).  Optionally use a [throwaway](https://twitter.com/search?q=throwaway%20(from%3Agrapheneos)&src=typed_query) account.

1. By default, [native code debugging](https://grapheneos.org/usage#banking-apps) is enabled. If you disabled it, try enabling it again. Launch app. *If unsuccessful, proceed to step 2.* 

`Settings` ➔ `Security` ➔ `Enable native code debugging`

2. Enable the per-app [exploit protection compatibility mode](https://grapheneos.org/usage#bugs-uncovered-by-security-features). Launch app. *If unsuccessful, proceed to step 3 for **testing only**.*

`Settings` ➔ `Apps` ➔ `AppName` ➔ `Advanced` ➔ `Exploit protection compatibility mode`

3. Temporarily disable [secure app spawning](https://grapheneos.org/usage#exec-spawning).

`Setting` ➔ `Security` ➔ `Enable secure app spawning`

4. Restart device. Launch app to see if this GrapheneOS feature caused the compatibility issue. The app may be refusing to run if it detects a different spawning mechanism.
 
**[Significant security loss and directly affecting some privacy using Zygote](https://old.reddit.com/r/GrapheneOS/comments/tq0k7q/comment/i2ex547/)** 
- Disabling exec-based spawning reverts to using the traditional Zygote spawning model AOSP's app processes
- Spawned as a clone of the Zygote
- Each app process has the same random secrets for ASLR, SSP, memory tagging, pointer authentication, setjmp canaries,  and heap randomization
- Half of the userspace is made of app processes
- Applies across all profiles
- App in profile A and profile B have same random values, which they can see

5. **Revert to secure spawning by enabling it again and restart device.** _See step 3 above_.

6. Search the [forum](https://discuss.grapheneos.org/), [os-issue-tracker](https://github.com/GrapheneOS/os-issue-tracker/issues), and/or within the [community](https://grapheneos.org/contact#community) for keyword(s) specific to the app name. *If unsuccessful with finding a solution, only than proceed to step 7.* 

7. Attempt to reproduce the issue by capturing a 'Bug report' using the feature in Developer options if you still run into the [app aborting](https://grapheneos.org/usage#banking-apps:~:text=if%20you%20run%20into%20an%20application%20aborting) at launch. 

- Enable Developer option by tapping the 'Build number' `7` times

`Settings` ➔ `About` ➔ `Device identifiers` ➔ `Build number` 

- [Capture](https://developer.android.com/studio/debug/bug-report) a bug report

`Settings` ➔ `System` ➔ `Developer options` ➔`Bug Report` ➔ `Interactive report` ➔ `REPORT`

8. Open a [new issue](https://github.com/GrapheneOS/os-issue-tracker/issues/new), provide a description and make contact via the appropriate channels with a similar message like "[Bug report capture for issue #104](https://grapheneos.org/usage#banking-apps:~:text=bug%20report%20capture%20for%20issue%20%23104)".  in order to submit the bug report capture zip privately. *(Replace the issue `#` number)*. 

- [Contacting the project](https://grapheneos.org/contact#contacting-the-project)
- [Reporting issues](https://grapheneos.org/contact#reporting-issues)
- *Friendly reminder: [instructions for getting support](https://github.com/GrapheneOS/.github/blob/main/SUPPORT.md) via [chat](https://grapheneos.org/contact#community) and* ***when to avoid using the os-issue-tracker***:  *ask questions* + *request support*

9. Disable the developer options.

`Settings` ➔ `System` ➔ `Developer options` ➔ `Use developer options`

We recommend disabling developer options as a whole for a device that's not being used for app or OS development.

---

10. It's plausible that this is app-related, rather than a compatibility issue with GrapheneOS - acknowledging this factor must be considered.

11. Please see the [Attestation compatibility guide](https://grapheneos.org/articles/attestation-compatibility-guide) on using remote attestation in a way that's compatible with GrapheneOS and **how** ***you*** **can help**. 

> *GrapheneOS users are strongly encouraged to share this documentation with app developers enforcing only being able to use the stock OS. Send an email to the developers and leave a review of the app with a link to this information. Share it with other users and create pressure to support GrapheneOS rather than locking users into the stock OS without a valid security reason. GrapheneOS not only upholds the app security model but substantially reinforces it, so it cannot be justified with reasoning based on security, anti-fraud, etc.*

---

# Notes

This repository is for reporting, tracking, and updating the status of banking app compatibility with GrapheneOS only. If you want to suggest [edits](https://github.com/PrivSec-dev/privsec.dev/blob/main/content/posts/android/Banking%20Applications%20compatibility%20with%20GrapheneOS.md) on the [banking apps web page](https://privsec.dev/posts/android/banking-applications-compatibility-with-grapheneos/), which are unrelated to the reports, please use [`PrivSec-dev/privsec.dev`](https://github.com/PrivSec-dev/privsec.dev/)'s repository [issue-tracker](https://github.com/PrivSec-dev/privsec.dev/issues).
