Hey folks, I'm orta therox - a developer / designer currently working on the TypeScript team at Microsoft. 
My work ranges from package managers, languages to figuring out how to describe and compose complex developer tools.

In this video we're gonna talk about why Signal was made.

## Why Signal?

Signal has always been a bit of an outlier in communication tools. It first appeared on my radar when I was interacting with Frederic Jacobs ( @FredericJacobs ) around CocoaPods, then when Edward Snowdon's NSA leaks came out it switched in my mind from an interesting idea to critical privacy infrastructure.

## So what is Signal?

Signal is a privacy focused messenger, which nowadays has a lot of the modern bells and whistles but it took a considerable amount of time for Signal to get those features, why? Well, let's dig into the windy history of Signal and the Signal protocol.

https://signal.org

### How did Signal get made?

There's a pattern we're going to see coming up here: There's periods of working on Signal, then periods of the Signal team working to improve security on other messengers. 

The idea of Signal started a few companies ago in 2010, when Moxie Merlinspike and Stuart Anderson got together to create Whisper Systems. A company focused on building enterprise mobile security software, including two products for Android phones:

- TextSecure: An end-to-end encrypted SMS tool
- RedPhone: An end-to-end encrypted VoIP tool 

After about 2 years of working on these apps and more, Whisper Systems was acquired by Twitter with the goal of beefing up their mobile security. It's hard to see what they worked on from the outside, however by 2013 Moxie had left Twitter and started up Open Whisper Systems - an open community funded continuation of the apps from Whisper Systems.

If you want a sense of how useful this work was, the NSA internally described Redphone (with some other tools as)

> near-total loss/lack of insight to target communications, presence

Open Whisper Systems work was funded by the Shuttleworth foundation, bitcoin donations and for a year they quietly worked on improving the protocol used by the Android apps. Once that was shipped they unified the two apps, made them cross platform and re-branded as Signal.

This was the first time Signal was available on iOS, and got a few commits in the codebase - one cool system that had running was "BitHub" which basically Open Whisper Systems they paid contributors. If you got commits in, you received bitcoins if you hooked up your Coinbase account. From two PRs, I managed to get thousands of dollars of Bitcoin when it was at peak, so I'd like to hope that a lot of the earlier contributors ended up botcoin millionaires from their work on Signal.

Once the releases were solid, Moxie took time off the Signal app to work with WhatsApp on implementing the Signal protocol in their client/servers. This work ended up improving some of the most used messenger clients in use: Whatsapp and Facebook Messenger. Google also used the Signal protocol in a chat messenger called Allo which came and went and no-one cared about.

Once that work was wrapped up in 2016, we got Electron builds of Signal for Mac/Windows/Linux - this is my main interface to signal, it's not pretty and it's tied to the mobile apps in an annoying way, but it works and that's enough for me.

In 2017, Signal shipped end-to-end video calls and profiles, basically names and avatars - but the app was still quite barebones when compared to something like iMessage, Whatsapp, Telegram of Facebook Messenger.

In 2018, Open Whisper Systems was replaced with the Signal Foundation after the founder of Whatsapp took 50 million dollars of his facebook money and used it to fund Signal. I interviewed with Signal around this timeframe, and their goal was to build end-to-end encrpyted, privacy focused equivalents to a lot of the features you see in other apps. 

Honestly, its a really refreshing take on how to aim for mass market adoption. In my mind the two top messenger clients for security are Signal and iMessage. Signal is both Open Source, and available on the two main mobile platforms. Both have underwhelming Mac apps, but that's OK, I don't really need the fancy features.

## Why make Signal though?

I'll let Moxie explain in his own words, this clip comes from the start of Open Whisper Systems as he was starting to work on the new Signal protocol.

[moxie]

People have always had a need for trading security vs privacy, and the rise of technological tools to allow massive surveillance makes it considerably cheaper for government actors to run mass surveillance schemes. If you watch a movie like [The Lives of Others](https://en.wikipedia.org/wiki/The_Lives_of_Others) you get a sense of just how much work it was to surveil people individuals by the Stati in Germany. 

Today, any NSA operative has (or had) access to text messages (DISHFIRE) emails (PINWALE), and phone calls (MAINWAY) for the last year (MARINA) available in a search enginer (XKEYSCORE)

If you've dared do something as scary as browse a linux website (or y'know submit code to Signal) - even then they broke into the data-centers of most popular email clients (MUSCULAR)

To me, the English-speaking democractic governments stopped conforming to the social contracts of 'we let you govern us, so you can help all of us prosper' - and we've been seeing a similar problem with the police.

Using tools which make mass surveillance more expensive, and to normalize the use of privacy tools is a moral imperative to me as a technologist given the dismal state of the modern centralized internet.

If you're savvy enough to code, you're savvy enough to consider the privacy ramifications of your work - do you use Signal? if not, leave a comment on why? otherwise hit that like and subscribe button and I'll see you next time
