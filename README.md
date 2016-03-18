# Patch to disable user profile avatar button in open source Chromium builds

# About
In Chrome 38 google introduced profile switching directly from the Title bar. Many users found it annoying and it was easy to disable through chrome://flags. In Chrome 44 you now had to use a command line switch to remove it. As of Chrome 47 it became default with no way to remove this eye sore. Those of us who only have one user profile found this quite bothersome. It bothered me so much I decided to write a patch and build my own version of Chromium.

The issue is well documented:
* <http://superuser.com/questions/805279/how-do-i-disable-the-profiles-button-in-chrome>
* <https://www.reddit.com/r/chrome/comments/3v2uu8/disablenewavatarmenu_no_longer_working_for_chrome/>
* <https://productforums.google.com/forum/#!topic/chrome/ixjLlM-Bmgc>
* <https://bugs.chromium.org/p/chromium/issues/detail?id=513899>
* <https://bugs.chromium.org/p/chromium/issues/detail?id=491038>

The issue was marked as WillNotFix by the Chrome team I decided to take matters into my own hands.

## How
The method ```bool BrowserView::ShouldShowAvatar()``` presented an easy opportunity to supress the button. The method is used to tell the UI when it should not draw the button. I simply made it say never.

### Version
Tested on version 50.0.2660.0
Commit ae70d4a tested on version 51.0.2681.0

### Usage
* Setup your build environment by following the instructions at https://www.chromium.org/developers/how-tos
* Clone this repo
* Copy `0001-Remove-profile-management-button-from-title-bar.patch` to your-build-folder/src/
* Apply patch with `git am < 0001-Remove-profile-management-button-from-title-bar.patch`
* Compile your build
* Enjoy the clean UI
