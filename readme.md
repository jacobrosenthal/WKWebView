Steps to recreate a new xcode project managed by fastlane for testflight release

* Create an xcode project
* [install fastlane](https://docs.fastlane.tools/getting-started/ios/setup/)
* init fastlane with ```bundle exec fastlane init```
* do signing through [match](https://docs.fastlane.tools/codesigning/getting-started/#using-match) (I couldnt get xcode signing to work.. )
** note I used keybase local encrypted git to store keys, but you could use github private repo
* Create Bundle Identifier app on [Itunes Connect](https://itunesconnect.apple.com/login)
** Note I also had to dig around and clear up a bunch of bank account and legal garbage and wait a day
* install a [plugin](https://github.com/KrauseFx/fastlane-plugin-appicon) to generate our icons 
** needed to change owner of Gemfile.lock to my user ```sudo chown YOURUSER:staff Gemfile.lock```
** add ```gem "fastlane-plugin-appicon"``` to Gemfile
** note I had to ```brew install graphicsmagick``` and ```sudo gem install json -v '2.0.3'``` and ```bundle install``` to get this damn thing installed
** finally install the plugin with ```bundle exec fastlane add_plugin appicon```
** create the icons ```bundle exec fastlane icon```
* generate launch images. I couldnt find a tool for this, so used an online service called [appbuild](https://www.appicon.build)
* check and select icons and imagelaunch in target -> app icons and launch images
* add to Info.plist ```<key>ITSAppUsesNonExemptEncryption</key>  <false/>```
* build locally and clear any errors
* use fastlane to release into beta with ```bundle exec fastlane beta --verbose```
* assuming success, log into [Itunes Connect](https://itunesconnect.apple.com/login), wait to get out of "processing" status
* Add any users on [Itunes Connect](https://itunesconnect.apple.com/login) and release to users
* users should get an invite email


