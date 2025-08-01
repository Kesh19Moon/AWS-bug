🪣 I Found a Hole in AWS. They Gave Me... a Mop.
Or, how I found a data leak in the cloud and Amazon said:
“Cool story. Here’s $1,600 and a wet floor sign.”

It all started, as these things usually do, at 2:47 AM.
Me. Hoodie on. Tabs open. Keyboard glowing like it knew something.
And a nagging question in my head:

“What if AWS caches something it really, really shouldn’t?”

Spoiler: it did.

💧 The Leak
Okay, imagine you’re in a private office. You whisper your Wi-Fi password to your friend.
Now imagine someone in the hallway yells “Hey! I’m your friend too!”
And suddenly the ceiling speakers repeat the password for the whole building.

That’s what I found in AWS.

🧠 What Actually Happened:
There was an API endpoint in AWS that behaved differently depending on HTTP headers.

If I added some spicy headers like X-Forwarded-Host or X-Forwarded-For, the server said:

“Oh hey, you’re internal! Here’s a response just for you.”

The server response was then cached.

So even when someone else came along without the spicy headers, they got my version — the one meant for internal systems. Oops?

I know what you're thinking:

“So… it leaked internal data?”

Yes.
AWS was accidentally sharing private internal metadata, including (but not limited to) temporary AWS credentials, because the cache didn’t know better.

🛠️ It Wasn’t a Full Exploit. But It Was... Juicy.
This wasn’t some 0-day, nation-state level exploit.

It was more like:

“Hey, your internal stuff is being publicly cached, and if someone times it right, they can drink your DevOps juice.”

And I was the one holding the straw.

💸 AWS Responds
When I reported it, I imagined fanfare. Maybe a dramatic Zoom call.
But I got this:

“Thanks for the report. This is a known pattern, but your approach was new. We’ll patch it.”

Then a few days later, a sweet little $1,600 landed in my bank account.

Not enough for a yacht.
But definitely enough for a premium mop, maybe even one of those with the squeezy handles.

🔍 Why It Mattered (And Still Does)
Even though they called it a “known pattern,” my exact method was unique.
It combined:

Header smuggling

Web cache deception

A healthy dose of “wait, is this really working?”

It showed that security is fragile not just in code, but in architecture.
Sometimes it’s not one big hole — it’s a series of small misassumptions that add up.

🧃 Takeaways
Caching is hard. Like, really hard.

HTTP headers are often way too trusted.

If it’s internal, don’t let the cache touch it.

Bug bounty isn’t always about glory. Sometimes it’s about quiet wins and quiet fixes.

🚿 Final Thoughts
This wasn’t a sexy hack. I didn’t breach the Pentagon or launch a satellite.
But I found a hole.

And AWS gave me… a mop. 🪣🧽

$1,600, a smile, and the quiet joy of knowing I made the cloud a little safer (and a little drier).

🧑‍💻 Written by Keshor Murugesan
☁️ Bug bounty hunter in the clouds (literally)
