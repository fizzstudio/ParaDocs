# ParaCharts: The Mobile Experience

Document version 1.0; 16 November 2026

----

**Primary Purpose:** The primary purpose of expanding ParaCharts to a mobile system as well as a desktop system is to provide an interactive experience for users specifically using a tablet or other mobile device. This includes providing touch gestures for interacting with the chart, an easy way to enter and exit the chart without a connected bluetooth keyboard and some slight interface modifications to make the screen less crowded.

**Access:** To correctly diagnose whether a user needs the mobile or desktop site, the developers would have to add a tool that screens for one or the other (mobile/desktop) and redirects the user accordingly. This means users on a phone or tablet would go to the mobile site and users on a computer would go to the desktop site. The only use-case when automatic redirection would not occur is if a user requested the desktop version specifically from their mobile device, which can be done by going to "Page Settings" and clicking "Use Desktop Version" on Apple devices. (Apple settings are given here as an example of specific use-case; similar Android settings apply.)

**Disclaimer:** I am not entirely sure how much of a phone or tablet's native control can be commandeered from the system defaults through a browser tool. As such, I have endeavored to brainstorm a few alternative methods for adapting ParaCharts for mobile. That being said, this document operates more in ideals than in absolutes, meaning that solutions discussed herein are the "ideal" solution and do not necessarily take into account technical possibility or the logistics of how such features and adaptations could or should be implemented.

## How Do Mobile Screen Readers Work?

In order to design gestures that users of a mobile screen reader (such as Apple's VoiceOver or Android's TalkBack or Commentary) will find intuitive, it is essential that developers first understand the fundamentals of how touch gestures based on visual stimuli (such as activating an icon after it becomes visible onscreen) are translated for nonvisual users. Therefore, please find a table with some of the most common screen reader gestures described alongside their standard (non-screen reader) equivalents. (NOTE: This table is directly based on gestures for Apple's VoiceOver.)

| Without a Screen Reader | This happens | With a Screen Reader | This Happens |
| --- | --- | --- | --- |
| You tap the screen. | You select an item. | You tap the screen. | The screen Reader speaks the item you touched. |
| You tap the screen. | You select an item. | You double-tap (tap twice fast) on the screen. | You select an item. |
| You swipe up with one finger. | You scroll up. | You swipe up with three fingers. | You scroll up. |
| You hold your finger on an item. | A context menu, or additional actions, appear. | You double-tap-and hold (tap twice fast and hold down.) | A context menu, or additional actions, appear. |
| You swipe left/right with one finger. | You go to the previous or next page or view. | You swipe left/right with three fingers. | You go to the previous or next page or view. |
| You swipe down with one finger. | You scroll down. | You swipe down with one finger. | You get additional information about an item, which is specific to VoiceOver and added for users' ease-of-access. |

### A Brief Note on Use-Cases

In the education system, it is most common for students to receive a borrowed Windows laptop or Chromebook computer to help complete schoolwork, but the runner-up (second-most commonly distributed device for schoolwork) is an Apple iPad. As such, the following mobile alterations were considered with Apple products chiefly in mind. 

# Direct Touch Area: The Most Significant Change

As ParaCharts Mobile stands now, Apple's VoiceOver splits the data elements of the chart application figure into separate image elements. In other words, VoiceOver does not recognize the chart figure application as an interactive element; instead it views it as a collection of separate images with which the user is unable to interact but through which the user can swipe.

The biggest step to improving the mobile experience is to change these image elements into a single element that Apple's VoiceOver calls a "Direct Touch Area." A Direct Touch Area is a section of the screen where the default Apple gestures have been overwritten so that custom accessibility gestures can be implemented.  To interact with direct touch areas, users can do one of two things. 

- They can go into their rotor settings (which dictate what additional information the "swipe up/down with one finger" gesture does). From the Rotor, they select "Direct Touch", and are then able to interact with the Direct Touch Area by touching it.
- A user double-taps (selects in the usual way) the direct touch area, which takes focus of the screen and control of the device. 

For best use with ParaCharts mobile, the second method, the double-tap, is recommended. This way, users can still tap around the screen and explore the chart description and control panel, before or after interacting with the chart figure application directly by selecting the Direct Touch Area. This is partly because Direct Touch Areas are somewhat uncommon, since using a Direct Touch Area means the development team would have to program their own gestures, and most choose not to do this when there are already a comprehensive list of Apple-assigned gestures to choose from. However, being able to manipulate items in the chart to query data points, learn about ranges of data points and investigate a single or multiple data series by touch is a feature that other accessible chart providers have not embraced, to their detriment; this is surprising given the prevalence of VoiceOver users in the blind community and VoiceOver's overall popularity for accessible mobile devices solutions. By attempting to bring charts into the touchscreen world, ParaCharts would be occupying a niche in the market as yet unexplored.

By implementing a double-tap entrance and exit to the chart figure application, the gesture is both rooted in what the user knows from prior VoiceOver use and is consistent, meaning users do the same thing to both enter and exit the chart figure application. However, it needs to be noted here that to achieve a double-tap gesture for both the entrance and exit, the Direct Touch Area might have to be attached somehow to a web dialog or popup, so that the chart fills the screen, giving users maximum space for gestures. 

## Within the Direct Touch Area

Within the Direct Touch Area, the default Apple VoiceOver gestures would be overwritten by the custom ParaCharts ones. Below are a few ideas. **NOTE: The below list is nonexhaustive and tentative; it was planned singularly without the aid of a focus group and is provided to serve as examples to illustrate what I mean by implementing gesture into an accessible chart experience.**

| Gesture Description | How ParaCharts Responds |
| --- | --- |
| Touch the screen, single tap | The screen reader announces the data point most associated with where the user's finger is—i.e. if they touch the bottom left corner of the chart figure application, the screen reader announces the first data point. |
| Swipe left | The screen reader announces the previous data point to the one they touched last time. |
| Swipe Right | The screen reader announces the next data point to the one they are touching. |
| Two finger double-tap, meaning the user taps twice fast with two fingers | Read out the chart description. | 
| Double-tap while on a data point | Selects the data point. |
| Double-tap and hold a data point/long press | Starts multiple selection. It selects the first data point where you double-tapped and held, but then tells the system you will select another one to compare. To select the second data point, you would flick forward or back to it (depending on its location) and double-tap it normally. Since you double-tapped and held the first point, the system will know you are looking at two points together. | 
| Swipe down with three fingers | Play the sonification of the graph or series. |
| Swipe up with three fingers. | The equivalent of hitting q on the keyboard to query your selected data point. Note with this one that if you haven't selected a data point it would not be able to query, since the screen reader cursor does not necessarily equate to the system focus on mobile. |
| Swipe right with three fingers | Triggers trend mode. This means that, instead of announcing the data point by point, a user can flick left and right through a sequence of data points. |
| Swipe left with three fingers | Exit trend mode. The data would go back to being navigatible by single points. |

## A Note on Tour Guide

Since the primary use-case of "tour guide" (previously narrative highlights mode) is sighted users learning to read a specific chart-type or dyslexic users obtaining assistance in reading a specific chart type, the Direct Touch Area is uniquely suited to this task and should be repurposed accordingly. 

One common feature in reading apps for the blind or dyslexic is the "finger tracking" functionality. This means that, as a user places their finger on a word, the word is highlighted and spoken aloud by the system's native text-to-speech voice.  This helps people with reading difficulties to maintain focus by isolating and emphasizing a single element. This element isolation is available through tour guide already in the original browser app; as you navigate with the arrow keys or hover your cursor over an element, the native text-to-speech engine of the system narrates the current element, such as a specific trend or feature of a data series, to illustrate it. With a mobile adaptation, it would be helpful for users if they could touch a given element of the chart and have it described or contextualized for them. If, for example a user touched the X-axis, the text-to-speech would read, "The time (in minutes) is displayed on the x-axis." In this way the development team can utilize tour guide in a similar way to pre-existing reading apps, which should feel natural and familiar to tour guide's demographic of users. 

Another thing users might wish to do with tour guide is to take a "grand tour" of the chart as a whole. This could be accomplished by another gesture—for example, a swipe with two fingers. Users could swipe right with two fingers to start their tour from the title of the chart. This means that, after the initial swipe to the right with two fingers, the text-to-speech would announce something like, "This column chart shows the unemployment rate in Greece from 1999-2019", and the title bar of the chart would be highlighted. Subsequent two-finger swipes to the right would continue cycling through the elements of the chart such as the axes, notable trends and chart minimums and maximums.

**NOTE:** Seriously, this one is important: If we implement the gestures for tour guide, we **MUST** make a note that a screen reader must be disabled to do it. Since tour guide contextualizes precise elements, and screen reader users are, in general, unable to navigate with the precision necessary to isolate a singular element, there could be conflicting gestures and also quite possibly a serious conflict between the screen reader and native text-to-speech on mobile devices.

### Gestures: The Untapped Resource

Looking at other accessible charts mobile experiences, it seems touch gesture exploration with the chart figure application is something that has not been extensively implemented across the board. Whether this is due to technological limitation or the general preference of users, I don't know. If this is all technologically possible, touch gesture implementation is something ParaCharts can seriously capitalize on. This would not replace the current keyboard commands of the app; instead it would give users another avenue to explore and understand data in ways which otherwise (without accessibility tools) might have been closed to them.

# Collapsed Control Panel

Another helpful change from the desktop to mobile experiences would be a collapsed control panel. This is a change of practicality; due to the smaller screen of a phone or tablet, and the fact that all elements of the application are accessed through the screen space, it is important to keep that space from being cluttered. 

This is useful for two important reasons. Firstly, collapsing the control panel allows us to scale the Direct Touch Area/chart figure application as the centerpiece of the application. The more room we leave on the screen for the elements of the control panel, the smaller the chart figure application would have to be to accommodate that; this would make it more difficult to find for nonvisual users and less obvious for other users. Secondly, it reduces cognitive load; a user is less likely to be overwhelmed by tabs, buttons and links that really only come into play if they want to change their view or settings from the default. 

In summation, this means that on the screen of a demo example chart on mobile, there would be the chart figure application, chart description, a button to expand the control panel and a link to go back to the example charts list. The usual tabs and annotations box that are visible in the browser application would be absent here.

## General Navigation Consideration

You would want to do some work tying "strips" of the graph to the screen reader, rather than keeping the screen reader labels on the exact data points. The nonvisual nature of the way visually-impaired users conceptualize the screen means that they will, because they can't see exactly where to touch, be less precise about what they are touching. If a user can see a point visually, they will tap it to hear what it is, but if they don't see a point visually, the user may instead touch an area of the screen to see what's there—for example, instead of touching the bottom left icon, located a half-inch from the very bottom corner of the screen, a nonvisual user will touch near the bottom left and could potentially miss the icon without realizing. As such, it is important to ensure that, instead of "points", the label for the screen reader specifically picks up on larger sections. This, in essence, gives nonvisual users a larger "target" and will minimize the cognitive load and frustration associated with repeatedly touching blank space in search of information. 

Once a user finds a point, they can flick from one to the other, but flick-navigation only works when you start from a button or point to begin with.

# An Alternative to Mobile Layout: The App

In the event that we are unable to design a useful mobile interface for charts that works within the device's web browser, we might decide to implement an app which could be downloaded on the app store and whose purpose would be to read ParaCharts in a more mobile-friendly way. 

To access ParaCharts Mobile from the Browser application, we could incorporate a URL shortener. This means that, instead of copy/pasting a link in its entirety from the browser on desktop into an app's address bar, a user would enter a shortened version of the link, which would tell the browser the link in its entirety. Tools like this, such as Tinyurl, already exist, but hosting one natively in ParaCharts would make it more convenient for a user to access and could minimize data concerns. Perhaps in the control panel, there could be a button that says, "Get Mobile Chart", which would trigger the URL shortener, which could then be entered into the app's address bar. 

One serious con to this solution is that it's more complicated than having two interfaces for a single tool—especially when the ideal for the tool as a whole is that it is incorporated into the reading interface of an article or webpage, rather than something that you could open in an external link and which would take the chart into fullscreen. Another con to the app is that there is still a transfer of data from one source to another; therefore, it is impossible to say that data concerns surrounding an app could be eliminated. 

In talks with the development team as of October 2026, the consensus is that an app is not a preferred solution to providing a useful mobile experience for ParaCharts users. However, I am choosing to leave my ideas for the app in this document in case they can be recycled for a future Fizz product.  

# The Web Dialog: In the Event the Touch Area is Too Complex

Another alternative if the Direct Touch Area is not viable is to turn the chart figure application into a web dialog, where each data point is its own element. To activate the web dialog, a user would double-tap on it, but it would be essential that the development team added a "Close" button which would allow the user to successfully close the dialog. Within the dialog would be the chart figure application only. 

There are a few cons to using a web dialog approach, but not as many as using the application approach. The biggest con is that, without a connected Bluetooth keyboard, users will not be able to take advantage of features like "toggle data table," "chart explainer" and "sonification." The only way they would be able to use these features would be to go to the associated tab on the control panel and enable the settings. To do this, users would first lose their place in the web dialog and have to find the settings manually. The best workaround to this would be to add shortcut buttons inside the web dialog with the chart figure application, but with the elements already present, I am concerned the web dialog would become too cluttered and overwhelm new users. Additionally, the idea of implementing exploratory touch gestures is moot since the chart figure application is bound to the standard gestures of the screen reader. 

## Conclusion

To rank the possible solutions based on their usefulness and marketability, my list would be as follows:

- A browser tool with a Direct Touch Area that implements custom accessibility gestures that allow users to explore a chart and the data it contains.
- A browser tool with a web dialog that gives users partial ability to explore a chart and its data.
- A separate application to read charts that a user finds online and can use to explore data.
I regards to a short-term solution, the web dialog would be a good "stepping-stone" (temporary fix) so that users have some mobile functionality while the development team potentially builds something more complicated.