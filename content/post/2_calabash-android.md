+++
date = "2015-12-22"
title = "Calabash: Calabash-Android tutorial"
description = "How to use Calabash-Android to Automated Test for Android Application"
keywords = ["calabash", "android", "automation test", "testing", "quality control", "quality assurance"]
categories = ["Automation"]
+++
---

# Automation Testing for Android App
---
### Requirement 
- JAVA JDK
- ANDROID SDK
- RUBY  

## Install Java JDK
Download and install from here: [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)  

## Install and setup Android SDK.
Download and install Android SDK for Mac from here[Android SDK Stand alone download](http://developer.android.com/sdk/index.html#Other)
    ![android_sdk_for_macos](http://i.imgur.com/sm5eCyE.png)  

Download and unzip, then we need to export environment variable <code>ANDROID_HOME</code> and <code>PATH</code> to two folder <code>platform-tools</code> and <code>tools</code>from Android SDK folder   
Set <code>ANDROID_HOME</code> by enter commend below to Terminal
```bash
export ANDROID_HOME=/path/to/your/android/sdk/folder
```
<code>/path/to/your/android/sdk/folder</code> is path to your android sdk folder on your computer. In my case, this is <code>/User/hoaiviet/Documents/android-sdk</code>  

set `PATH`:
```bash
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/platform-tools
```
Reset Terminal or add this commmand to `~/.bash_profile` or `~/.zshrc` if you are using `zsh`
Reload configuration 
```bash
source ~/.bash_profile
```

## Install Ruby
We need `Homebrew` to install ruby. If not, follow command below to install:
```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Now, install ruby by command
```bash
brew install rbenv ruby-build

# Install ruby
rbenv install 2.2.3
rbenv global 2.2.3

# Check ruby version
ruby -v
```

If `ruby -v` response not equal version 2.2.3 then we need add command below to file `~/.bash_profile`
```bash
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"
```
and reload 
```bash
source ~/.bash_profile
```

## Install Calabash Android
```bash
gem install calabash-android
```

## Create folder test
In this tutorial, we use skype app for testing.

Now we create new folder
```bash
mkdir calabash-test-skype
```

Open this folder
```bash
cd calabash-test-skype
```

Generate test folder structure
```bash
calabash-android gen
```
press Enter to continue

![folder_structer](http://i.imgur.com/Ltl5gtd.png)

Copy your apk file to this folder then resign this by command
```bash
calabash-android resign skype.apk
```

## Create first scenario
Open `my_fist.feature` by whatever text editor what you like.

![first_step](http://i.imgur.com/verAlLs.png)

Note: You can view predefined command here: [canned_steps](https://github.com/calabash/calabash-android/blob/master/ruby-gem/lib/calabash-android/canned_steps.md)

First, we create scenario to test login function of skype

```
Step 1: Press Skyname button
Step 2: Enter account name to input field number 1
Step 3: Enter password to input field number 2
Step 4: Press Sign up button
Step 5: Assertion is we need to view Add friend button
```

Then we define this in `my_first.feature` :

```cucumber
Feature: Login feature

  Scenario: As a valid user I can log into my app
    Given I press the "Skype Name" button
    Given I enter "viet.ch2612" into input field number 1
    Given I enter my secret password into input fiend number 2
    When I press view with id "sign_in_btn"
    Then I should see "Add friend"
```

Connect your device or Simulator then check
```bash
adb devices
```

Now, run this test
```bash
calabash-android run skype.apk
```

This is result
![first_run](http://i.imgur.com/LuvPgK4.png)

We show "Not defined step"? Yes, now we define this step:
```ruby
Given(/^I enter my secret password into input fiend number (\d+)$/) do |index|
  enter_text("android.widget.EditText index:#{index.to_i-1}", "password")
end
```

Run again
![result](http://i.imgur.com/VAiEZP2.png)

OK all passed
## Test report?
```bash
calabash-android run skype.apk --format html --out <filename>.html
```
or
```bash
calabash-android run skype.apk -f html -o <filename>.html
```
this is test report format
![report](http://i.imgur.com/6FLE3m5.png)

## Run one feature?
```bash
calabash-android run skype.apk feature/<filename>.feature
```

## Run scenario by @tag
```bash
calabash-android run skype.apk --tag @test
```
or
```bash
calabash-android run skype.apk -t @test
```

## Clear app data
### 1: Use tag `@reset`
Add this to `feature/support/app_installation_hooks.rb` inside `Before`
```ruby
scenario_tags = scenario.source_tag_names
  if scenario_tags.include?("@reset")
    clear_app_data
  end
```

And add @reset before scenario
```cucumber
@reset
  Scenario: As a valid user I can log into my app
    Given I press the "Skype Name" button
```
### 2: Define 1 step for clear app data
First, require `require app_installation` 
```ruby
require 'calabash-android/management/app_installation'
```
and define step
```ruby
Given /^I clear app data$/ do
  clear_app_data
end
```
Note: Recommend add delay time for this step

