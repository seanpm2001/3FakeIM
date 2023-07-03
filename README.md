
***

<img src="/3FakeIM_1024pxLogo_V1_HighCompression.png" alt="3FakieIM logo" width="256" height="256">

# [3FakeIM](#3FakeIM)

`📱️🚫️🌝️💾️ 3FakeIM is a joke program meant to imitate various fictional characters, and the "[CHARACTER] CALLED ME AT 3:00 AM" clickbait trend, while poking fun.`

***

## Language

This program is written in Rust, as I am new to the language, and wanted to use it as a universal language across all the major platforms this project is planned to support (Android, iOS, PostMarketOS, Ubuntu, etc.)

***

## App layout

### Simulation menu (application startup)

3FakeIM is designed to imitate the clickbait trend of random characters calling/texting the user at 3:00 am. The program opens to a simulation menu with 3 buttons:

- Left: Call
- Middle: Exit
- Right: Text

These buttons are all near the bottom of the screen in a nearly fullscreen view. Additionally, a gears icon is present in the upper right corner (which can be changed to the upper left corner via accessibility settings) the gears icon opens the configuration and settings menu of the app.

***

### Settings

Under settings, there are 4 sections that display as buttons on top of each other:

- Text and call settings
- Volume and visual settings
- Character settings
- Accessibility settings

Additionally, a back arrow is in the top left corner (which can be changed to the top right corner via accessibility settings) and there is an about button in the top right corner (which can also be changed, to the top left corner)

***

> **Note** _There is a lot of intricacy here, something I wasn't expecting for a joke program. This section goes into detail, but is not complete, and may need to be rewritten in some areas._

#### Text and call settings

In the text and call settings, you can choose a messaging app to mimick. A style file has to be defined under `/Text/Skins/` in the app data directory, and must be an XML file. You can browse through messaging apps and choose one. The configuration is set to only show a fake set of contacts, and a fake conversations page.

##### SMS Flags

- `<replyText>` - Defines the text in the box before you start typing a message
- `<sendbtn>` - Defines the send button graphics
- `<contacts>` - All contacts must be placed here
- `<contact1="characterName">` - Defines the name of the character, and a link to their message history
- `<settings>` - Defines a settings page under a menu button. You can define your own settings here, as long as the app supports them. It is recommended to have a clear message history section 

As usual, the back button is in the top left corner, but can be reversed through accessibility settings.

##### Call flags

Call flags build upon SMS flags. They define the cover photo of the character, the call duration, and the interface.

#### Volume and visual settings

In this page, there is a volume slider, a brightness slider, a contrast slider, and a set of filters in a dropdown, such as black on white, normal, creepy, and horror.

As usual, the back button is in the top left corner, but can be reversed through accessibility settings.

##### Text flags

You can set responses to various phrases, like so:

```xml
... char1
... ... text
... ... ... <responses>
... ... ... ... <msg1>Hello</msg1><istext="true"><wait-for-response="true">
... ... ... ... <reply1>Hello</reply1><audio_footsteps="1" path="/Characters/Audio/GHOST_Footsteps_01010101.ogg" start="0000" end="4000"><audio_voicebox="1"><switch="1" path="/Characters/Audio/GHOST_CommonReplies_12340022.ogg" start="0100" end="1200">
... ... ... </responses>
... Snippet end
```

> **Note** _Each `...` indicates a tab. Do not actually write `...` repeatedly._

You have to define where the audio file starts from. The time is set in milliseconds. The maximum duration is 10000000 (16.667 minutes)

#### Character settings

In the character settings, you can change the appearance of the character, their voice, their lines, their responses, and their actions. You can only select multiple characters at once (up to 64) although no more than 5 can visually appear on the screen at once. As usual, the back button is in the top left corner, but can be reversed through accessibility settings.

Characters are defined in *.xml files, which can be configured by users who want to use the software. The files have to be placed in the app folder under `/Character/` for them to be browsing, and they have to be placed under `/Character/Active/` to be used.

These configuration files give WebGL instructions on how to operate. Graphics have to made SVG, and placed within the file. Audio is linkable separately, and should go under `/Character/Audio/` of course, all audio files have to have different names. The recommended name format is:

`Name of character` `_` `Audio` `_` `an 8 digit number` .ogg

.oga and .wav are also supported.

Do not place more than 4 gigabytes worth of audio files in the app folder in total, or the program will lag. The program does not play audio files larger than 100 megabytes (100,000,000 bytes) to keep the program running smooth. This of course can also be tweaked, but it isn't recommended. ALso, do not place more than 10000 audio files in the `/Character/Audio/` directory to prevent lag, and to prevent headaches.

There are several flags for what to do:

##### SVG flags

- `<svg_head>` - Defines the head of the character (if they have any)
- `<svg_head-mouth> - Defines the mouth of the character (if they have any)
- `<svg_head-nose> - Defines the nose of the character (if they have any)
- `<svg_head-eyes> - Defines the eyes of the character (if they have any)
- `<svg_head-ears> - Defines the ears of the character (if they have any)
- `<svg_head-horns> - Defines the horns of the character (if they have any)
- `<svg_arm>` - Defines the arms of the character (if they have any)
- `<svg_arm-l>` - Defines the left arm of the character
- `<svg_arm-r>` - Defines the right arm of the character
- `<svg_arm-3>` - Defines a 3rd arm for the character, and all subsequent arms (maximum: 64)
- `<svg_leg>` - Defines the legs of the character (if they have any)
- You can replace arms with wings if necessary
- `<svg-arm-hold>` - Defines an object for the arm(s) to hold
- `<svg_leg-l>` - Defines the left leg of the character
- `<svg_leg-r>` - Defines the right leg of the character
- `<svg_leg-3>` - Defines a 3rd leg for the character, and all subsequent legs (maximum: 64)
- `<svg_neck>` - Defines the neck of the character (if they have any)
- `<svg_torso>` - Defines the torso of the character (if they have any)
- `<svg_feet>` - Defines the feet of the character (if they have any)

##### Audio flags

- `<audio_footsteps>` - Defines the footstep noise of the character
- `<audio_wings>` - Defines the wing noise of the character
- `<audio_slap>` - Defines the slapping noise of the character
- `<audio_stomp>` - Defines the stomping noise of the character
- `<audio_voicebox>` - Defines the voicebox of the character. In this, a separate property is needed for all dialogue. You can also alternate between voices with the `<switch="1">` tag, which then has to define voicelines for this voice within this tag
- `<audio_ringtone>` - Defines the ringtone for the character. If one isn't set, it defaults to the device default. Additionally, a `<switch="1">` tag can define ringtones for multiple character sequences, which has to be defined for each situation

I was not expecting there to be so much to this, so a lot of this needs to be expanded and possibly reworded. I didn't think it would take this much for this project.

#### Accessibility settings

Under accessibility settings, you can increase/decrease the text size, enable text to speech, turn on left handed mode (which reverses the position of all buttons) and change the color scheme. All changes are recorded in a configuration file, which can be swapped or pre-loaded with the app. For example, you can make your own distribution of the app that comes with any of these settings enabled/disabled by default, so that they are all there right after installation.

#### About page

The about page shows the version number, with a back button in the top left corner (which can be reversed via accessibility settings) and also has a short list, containing:

- Languages
- Reset all settings
- Help (redirects to an offline documentation page, which has a link to the repository documentation at the top)
- Develop (redirects to an offline page that shows development links, including a link to this repository)

***

## [Documentation](#Documentation)

Additional documentation is available [:octocat: `in a separate repository`](https://github.com/seanpm2001/3FakeIM_Docs/)

***

# [File info](#File-info)

**File version:** `1 (2023, Saturday July 2nd at 11:43 pm PST)`

***

# [Footer](#Footer)

You have reached the end of this page.

###### [EOF](#EOF)

***
