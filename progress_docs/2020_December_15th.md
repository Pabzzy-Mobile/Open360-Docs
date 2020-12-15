# Stamp TV - Open360

**15th December 2020** _Progress Report_ by _Pedro Pires_

The project currently named under Open360 on GitHub.
(https://github.com/Pabzzy-Mobile/Open360-Docs)

- [Stamp TV - Open360](#stamp-tv---open360)
- [Abstract](#abstract)
- [Introduction](#introduction)
- [From concept to prototype](#from-concept-to-prototype)
- [Working Prototype](#working-prototype)
- [How is it different](#how-is-it-different)
- [Looking back and forth](#looking-back-and-forth)
- [Successes and Failures](#successes-and-failures)
- [Conclusion](#conclusion)

# Abstract

This document will talk about the currently working features of the latest Stamp TV prototype (Open360) in a brief concise report.

It will also break down the successes and failures of the prototype, and look ahead for the future of development if the project gets handed to anyone.

Comparisons to features mentioned or planned on the concept document with the current prototype will also be made and broken down.

# Introduction

Stamp TV is a streaming platform centred around Tourism for tour guides to create communities and show the world their favourite locations. The audience is mainly users that cannot travel often or can’t travel at all. The creators can then create their own audiences within this general audience to create their own community and viewership.

The viewers can interact with the tour guide/creator using a stream chat for Q/As or general interaction with the creator or other users watching the stream. The platform also features its own currency, “Stamps” that can be used to donate along with a highlighted message and support creators and their streamed guides. Viewers can also subscribe to creators, supporting with a monthly donation to a streamer.

Since Stamp TV is focused on Tourism, it includes categories based around the location of the guide like “Poland”, “Japan” or “Mexico” as well as tags like “Q/A”, ”Funny”, “Casual Tour” or “Official Tour”.

Viewers can also follow a tag or creator to be notified of new live streams or being able to quickly find their favourite creators. The Explore section is also ever evolving, searching both users, current live streams and VODs as well as filtering for tags and directories.

Users coming from Twitch.TV will notice a similar layout to Twitch and won’t have to learn a new layout unlike other streaming platforms like Periscope or Facebook Gaming.

Open360 is the open-source prototype of Stamp TV.

# From concept to prototype

The main idea Stamp TV was centred around was a Tourism-based streaming website. Of course this idea was majorly influenced by the COVID-19 lockdown and the under exposure to external environments by all the steps of the human society.

The concept video revolved around users watching streamed content from tour guides around the globe streaming 360 degree video and being able to control from their couch the direction of the perspective of the video.

The concept is totally acceptable, it’s a very simple concept that uses software and ideas already found in other industries.

# Working Prototype

This lists the current features Stamp.TV has and also some features that it is missing.

- User Dashboard is fully functional for adjusting user and stream settings. The dashboard doesn’t show any statistics about the stream and doesn’t let the user change password.
- A Stream Key is required to stream to Stamp.TV. These can be regenerated on the User Dashboard and are random strings of characters. This should be the safest way to authenticate who can stream to a channel but one problem with the front-end is that the Stream Key is visible in the source code of the video element. This is both a backend and front-end issue and should be addressed soon™.
- View count depends on how many users are connected to the chat. This amount however is not verified by the chat service and if 2 connections from the same user are received the view count counts both.
- The external web API can handle requests for stream stats and status as well as micro service status.
- Only live streams are available, they are recorded and saved onto the video database but cannot be accessed by the user. Finishing a stream also overwrites the last stream’s video.
- Videos cannot be uploaded to the site for replaying later by users.
- Stream descriptions are simple text with no Twitch-like modules.
- User registration checks for username and email collisions but is only by local strategy. This should be replaced by a Auth0 authentication instead to keep with the times and allow third party authorisation.
- Chat doesn’t check for username collisions so the same user can be instanced twice on the same stream chat by accessing the same chat on 2 different pages. The chat also doesn’t pop out yet.
- Nor users nor creators can clip parts of their stream.
- Stream thumbnails don’t work properly.
- Users can’t yet control the stream’s 360º video camera direction from their phone or another device.
- Clips are not implemented yet although it might be easy to implement since the streams are already partitioned into .m3u8 playlists and a VOD is already created.

# How is it different

The current concept is not different than other streaming services right now. The completed version however would have its own identity as a Tourism oriented streaming service where any guide or person could stream tours, Q/As, history of their favourite location. The 360º video would also give the platform a different feature set than Twitch and other services.

# Looking back and forth

Looking back at the concept document, everything is there looking to be fully implemented. The following list shows where features failed/succeeded to be implemented.

1. **360º Video**

   Although not expressively implemented and deeply tested, streamed 360º video works fine on the browser. Through the power of video.js automatically recognising the video source as 360º video and displaying a 360º view of the video.

   In the future this should be more tested and deeply implemented, with stream thumbnails indicating if the stream is 360º video.

2. **Home Console**

   In the original plan, a home console made from a raspberry Pi computer was planned but could not be implemented in time. The Pi’s original browser was not able to initially process both a video stream and a socket connection to the chat. After some adjustments it was able to decode 1080p video and a chat connection while in the browser with almost stable fps and in later tests, using VLC to receive the stream directly, was able to decode 1080p video with no hiccups. This however meant that the browser could not be used for the home console and an application needed to be developed for the Pi just for our needs.

   Due to the time crunch and the reduced knowledge of the raspberry Pi, the idea was stashed to work on the backend of the server.

   The idea should be revisited with a more skilled programmer and more knowledge on the raspberry Pi and video decoding.

3. **360º Camera Controller**

   Shown in the original concept video for a project named TPeye, a user could control a 360º video stream’s camera’s direction using a virtual joystick on their phone. Although this idea was explored using already implemented systems in Open360 (mainly a socket.io chat server fork), it was never fully implemented.

   The idea should be implemented in the future, a concept document can be found in the Open360-Docs repository.

4. **Stamp TV Currency**

   0% Implemented. The concept showed users being able to donate using “Stamps”, a currency inside Stamp TV. This has not been implemented yet on Open360.

5. **Direct Messages**

   Briefly mentioned in the UI Style Concept, direct messages are a way for users to text each other. This could still be easily implemented on the chat server but would take longer on the Web frontend.

6. **Video-on-Demand and Chat Replay**

   The ingest server already generates a VOD of a finished stream, the only problem is accessing and creating an indexed database of all the VODs. The chat server does not create a persistent replay of the chat messages on its database. Both these features would take time to implement together so that a stream’s VOD and its chat could be played synchronously with scrubbing and clipping.

   This should be implemented if the project is to keep going.

7. **Explore and Home**

   The concept shows featured streams and an explore page. These are currently not implemented as I did not have time to research into indexing algorithms as well as not having an algorithm engineer.

   This is an important feature and is empirical for the success of the platform.

# Successes and Failures

The chat system is a major success, it works flawlessly sending messages between the user and the streamer even with emotes alike the Twitch chat is really well.

The ingest service is lacklustre. It lacks transmuxing video to other resolutions for user selection, safer stream key system and a complete video database.
The Web service is clean and simple, but lacks features that others don’t have and took too long to get a shape going for it. The Home page is also a mess, only showing currently available streams without any sorting.

The internal API is a major success, asynchronous and independent from other services and simple enough to understand.

# Conclusion

The 2 month time window was very optimistic to create a fully functional prototype. No stress tests were made on the system, no feedback was taken from anyone and the project didn’t gain any traction with other members of the team. Leaving this version undercooked.

Overall, the project needed more time in the oven, more cooks and more ingredients.
