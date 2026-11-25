Title: Lost Game Revival
Type: Game dev / Research and problem solving
For: Personal
Tools: Google, Claude, Gemini, Python, JavaScript, Cloudflare
Year: 2026
Role: Everything: the search, emailing the developer, the web port, hosting and the high score server
Time: One late night of searching + an hour to rebuild it
OK to show: yes
Section: work
Play: yes
Play URL: play/andrix.html

Description:
I was showing my girlfriend my 1v1 party game and asking what she thought. She said a mini-game I should add was one she used to play on her Kindle Fire as a kid. The problem was she didn't remember the name, and only kinda remembered how it looked and worked. So I found it for her.

## The hunt
We stayed up hours past our bedtime trying to find it. All we had were her memories:

- You're a small cube moving around the edge of a big box
- A meteor bounces around inside, trying to kill you
- When you move, a thin line follows you, and if the meteor hits the line, you die
- Later levels add smaller balls that chase you along your own line
- Everything was ice themed, with a picture of like an iceberg in the background
- The name started with a T... or maybe it didn't

Search engines and AI kept showing us games that were close, but never the exact one. So we switched to scrolling through Google Images, throwing random extra words into every search. Finally we hit the right keywords, scrolled far enough down, and she saw it. "That's it, that's the one!"

The funny part: when we actually saw the game, there was nothing with ice. The background was bubbles, not an iceberg, and the "meteor" was a cloud. No wonder searching for an ice game with a meteor kept failing. But the gameplay she remembered was spot on, and that's what finally got us there.

Having a name didn't get us the game, though. It wasn't on Google Play, and the Amazon Appstore had shut down on Android phones and Windows. All I could find were two old listing pages. One of them named the developer, so I checked if his website was still up, and it was, with newer games. The game we wanted wasn't there, but his email was.

## The email
I wrote him a short email. I told him my girlfriend loved Andrix as a kid, that it was disappearing from the internet, and asked if he'd share the APK so we could keep a personal copy. I was clear that I didn't want to sell or redistribute it. I didn't expect anything back.

The next morning I was checking my email, not even thinking about it, and there was his reply. He'd uploaded the original Amazon version for us and said it was nice that someone still remembered his old games. I was so happy. At this point it really meant a lot to me, and I knew it would make her happy to get it working.

## The problem
The APK was built for a very old version of Android. It wouldn't run on BlueStacks or on my phone. I researched it, tested different things, and poked around in the code. Then I remembered people recently using AI to reverse engineer old games, like porting console games to PC or rebuilding them in JavaScript to run on the web. So I tried that.

## The rebuild
The original game is written in Java, using Android's built-in graphics tools instead of a game engine. I gave Claude clear instructions and had it decompile the game and port it to the web. The port worked almost right away, so most of my time went into turning it into something she could actually use:

- **JavaScript** (game.js): a line-by-line translation of the Java with the same function names, so you can compare the two side by side
- **Website:** I set up hosting so it opens with one tap on a phone, sounds included
- **High score backend (Cloudflare):** I connected the game to my own JavaScript and a small data server, so our scores are shared and we can compete
- **Python** (build.py): packs everything into a single file

## The reveal
I didn't tell her right away. I waited until we were just lying down and relaxing, and then told her I had a surprise. I opened the link on my phone. When the loading screen came up, her eyes went wide: "You got it? How did you... what?"

She played for a minute, looking at the screen, then looking at me. I told her the sounds were in too, and she loved them for some reason. Then she put the phone down and kept thanking me over and over, almost crying. "I don't know what to say other than thank you. I love you." I was almost crying too.

I asked her if she thought we'd actually find it and get it. She said, "Of course. I thought you would."

Now we trade high scores, and she gets mad every time I beat hers. "Check Andrix" is a regular thing we say now.

## What I learned
- **Search by what you're sure of.** Her memory of the look was wrong (bubbles, not ice; a cloud, not a meteor), so I relied on the colors and on her memory of how it played. Focusing on the gameplay is how I found it.
- **Just ask.** The fastest path was emailing a real person, politely and with a clear request.
- **Good instructions make AI fast.** Because I knew what I wanted (a faithful line-by-line port, not a remake), the AI got it right quickly, and I could spend my time on the parts that made it usable.
- **Build for the person.** The point was making her happy, so I made it easy for her to play: a link she can open on her phone or any device, anywhere, with a high score board to keep it fun and give us something to bond over.

Images:
## The hunt
Google Searchs/Screenshot_11.png {fill 44.7,72 tall note-tl} - (Search history) 
Google Searchs/Screenshot_12.png {fill 50,52 tall note-tl} - (Search history) 
Google Searchs/Screenshot_13.png {crop 1.7,4.5,70.9,93.8 big} - (Searching.) 
Google Searchs/Screenshot_14.png {97.3,46.5 tall} - (Searching...) 
Google Searchs/Screenshot_16.png {fill 0,61.8 half} - (Still Searching..) Getting a bit closer
Google Searchs/Screenshot_15.png {half} - (SEARCHING..) More in the right direction with the gameplay
Google Searchs/Screenshot_17.png - (OH STILL SEARCHING.) 
Google Searchs/Screenshot_22.png {tall} - (We feel like this direction on art is close) 
Google Searchs/Screenshot_20.png {big} - (Looking at Ice stuff) 
Google Searchs/Screenshot_21.png {full tall note-tl} - (We Found it!) 
## The email
Google Searchs/Screenshot_23.png {fill 10.7,50 tall} - (Looking for a download link) 
Google Searchs/Screenshot_24.png {crop 9,4.6,79.3,94.3 big} - (Another Website) 
Google Searchs/Screenshot_26.png {fill 0,10 big} - (Found out it was on Amazon) 
Google Searchs/Screenshot_27.png {fill 0,56.5 tall} - (Amazon Details) 2011, only 14 reviews.
Google Searchs/Screenshot_28.png {fill 57.2,42.6 wide} - (Company Website) 
Emails/Screenshot_7.png {full wide note-br} - (First Email) 
Emails/Screenshot_8.png {full wide note-br} - (Email Response) Cant Believe it
Emails/Screenshot_9.png {full wide note-br} - (Final Email) 
## The problem
Code Screenshots/Screenshot_10.png {full note-bl} - (The problem) Super old version of android, also an apk is hard to work with compared to a web port.
## The rebuild
Web/code-01-scoring.png {full wide note-tr} - (Code Comparison ) 
Web/code-02-cloud-wobble.png {full wide note-tr} - (Code Comparison ) 
Web/code-03-swipe-controls.png {full wide note-tr} - (Code Comparison) Fun one.
## The reveal
Gameplay/Video/QuickAndrixVideoClip.mkv {crop 33.3,7.6,33.4,88.1 tall} - (THE GAME IS WORKING) 
Gameplay/Video/2026-11-23 12-32-40.mkv {crop 33.6,7.6,32.8,87.2 tall} - (WIN STATE) 
Gameplay/Video/2026-11-23 12-32-58.mkv {crop 33.6,7.6,32.1,85.3 tall} - (DEATH) 
Gameplay/Video/2026-11-23 12-33-12.mkv {crop 33.8,7.9,31.4,88.1 tall} - (LOSE STATE) 
