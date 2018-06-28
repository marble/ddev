## `ddev` Release Checklist 

- [ ] [Create a release](https://github.com/drud/ddev/releases/new) using the github web UI, initiating a CircleCI tag build
- [ ] Check out the ddev source with `git fetch upstream && git checkout <release_tag>`
- [ ] `make push` each directory in `containers/`
- [ ] Add the commit list to the release page
- [ ] Download artifacts from CircleCI and upload them (except for the Windows installer and its sha256.txt) to the release page
- [ ] Update the `ddev` [Homebrew formula](https://github.com/drud/homebrew-ddev) with the MacOS `.tar.gz` and SHA checksum
- [ ] Test `brew upgrade ddev` and make sure ddev is the right version and behaves well
- [ ] Sign the Windows installer and create a new sha256.txt according to steps below
- [ ] Upload the signed Windows installer and SHA checksum to the release page
- [ ] Test the Windows installer and confirm it's signed correctly
- [ ] Finish updating the release page, some copy-and-paste from previous release

### Signing with Windows installer

See the [Digicert instructions](https://www.digicert.com/code-signing/signcode-signtool-command-line.htm)

Basic instructions:
1. On a Windows machine, install the certificate as suggested. You need the cert file and password, and you install it into Chrome or IE (This is a one-time operation)
2. Install the suggested [Windows SDK 10](https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk)
3. Install [Visual Studio Community 2015](https://msdn.microsoft.com/en-us/library/mt613162.aspx)
4. Run the [Developer Command Prompt](https://docs.microsoft.com/en-us/dotnet/framework/tools/developer-command-prompt-for-vs)
5. Sign the binary with something like `signtool sign /tr http://timestamp.digicert.com /td sha256 /fd sha256 /a z:\Downloads\ddev_windows_installer.v0.18.0.exe` (I did this with the downloaded ddev_windows_installer physically on my mac (Z: drive))
6. Generate a new sha256 file (I did this on mac): `shasum -a 256 ddev_windows_installer.v0.18.0.exe >ddev_windows_installer.v0.18.0.exe.sha256.txt`
7. Upload the ddev_windows_installer and sha256.txt to the release

### Additional Information

This checklist outlines the release process specific to building, packaging, and testing `ddev` releases.  For additional information on the product release process, please see the [Product Release](https://github.com/drud/community/blob/master/development/product_release.md) instructions.