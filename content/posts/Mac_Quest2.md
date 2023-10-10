---
title: "Mac connect to Quest"
date: 2023-10-9
# weight: 1
# aliases: ["/first"]
tags: ["Tech"]
author: "Orange"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: true
# canonicalURL: "https://canonical.url/to/page"
# disableHLJS: true # to disable highlightjs
# disableShare: false
# disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
# ShowPostNavLinks: true
# editPost
#     URL: "https://github.com/<path_to_repo>/content"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
math: true
type: post
---
It's hard to find a complete guide to connect Mac and Meta Quest2, build and run unity application, so I write this down. Before start, I would say that I tried several methods online but none works. Finally I found this [blog](https://www.reddit.com/r/OculusQuest/comments/bskcp2/mac_guys_sideloading_and_file_transfer_to_quest/). A lot of thanks. For MAC, I didn't find a way to cable so it only works if you want to package your application and run in Quest.

### Recipe
Mac M2 pro

Meta Quest2

Unity 2022.3.8f1

### Step 1 Open developer mode on your Quest
1. register a developer account on [meta](https://developer.oculus.com/) (register, two-factor authorization, boom!)
2. download quest app on your mobile and connect to your quest
    attention: I was stuck at this step because of the stupid facebook login loop. The account on quest and phone app should be consistent.
3. open developer mode

### Step 2 Download SideQuest on your Mac
[Install](https://sidequestvr.com/setup-howto) the advanced one so that you can install your own apk file. 

### Step 3 Connect your Quest to Mac
use the **right connection**. I use **quest link** and a **TypeC adaptor**. Try to play around and see if the Quest is charged. Once it shows charged or pop up a window for you to authorize debugging mode, then it's connected. Also refer to the instructions in the SideQuest until it shows connected.

### Step 4 Set up unity

Follow [this](https://www.youtube.com/watch?v=7mAAkB1WGpk) 05:45 - 13:40

Build and run your application in Quest!

### Step 5 Open your Application in Quest

You can find "My Project" in your Quest Application (in "unknown source" category).