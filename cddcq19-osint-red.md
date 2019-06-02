# OSINT - Red

So this weekend my team and I tried to qualify for [CDDC](https://www.dsta.gov.sg/CDDC) finals 

So this is the walkthrough for the `OSINT-Red`

Credits: My teammate @Creastery, [@tcode2k16](tcode2k16.github.io), [@lord_idiot](https://blog.idiot.sg/)

## Summary

We are required to solve `[R-0] Everyone <3 Fan Mail` before we are able to unlock all other challenges for this category.

## [R-0] Everyone <3 Fan Mail

>All good hackers do recon. Let's scout out more information about what and who lightspeedcorp.global is. I heard their administrator loves replying to fan mail.

>Remember kids, don't just rely on one database to give you the information you need! Psst, I unofficially heard that the official source is always the truest :D 


So there are few important information that is important here.

1. lightspeedcorp.global
2. Admin related information
3. Official sources

Given the challenge title, we know that this challenge will require email.

Which means we will need to either find a MX record or a email address from whois for the domain `lightspeedcorp.global`

However, simple dig [result](https://whois.icann.org/en/lookup?name=lightspeedcorp.global%20) reveal Registrar WHOIS Server: whois.namecheap.com

Since previously we know that oficial sources is the best. Let's look at the [namecheap](https://www.namecheap.com/domains/whois/) database.

Which reveal the admin email address: Luther.Torvalds@outlook.com

Flag `$CDDC19${IS_IT_I_AM_FAM0US_NAO}` was found after emailing to that email.

PS: This is totally not OSINT since we needed to email the `admin`. I guess a lot of us was stuck at this step.

This allow us to unlock [R-1], [R-2], [R-3-1] and [R-4-1].

## [R-1] Travel to the Past

> The web-site lightspeedcorp.global is currently under construction. Aw shucks, what a pity that we have no way to see it.

Since the challenge title hinted at `past`. A simple way to get those information would be `wayback` 

https://web.archive.org/web/20190520070628/http://www.lightspeedcorp.global/

Flag: `$CDDC19${Past_pAst_paSt_pasT}`

## [R-2] I'm Sho Done With This

>L-l-l-l-l-look at LightSpeedCorp, hacker...

>Let's expand our scope by making use of all search engines to do more recon!

Challenge title hinted at `shodan`

Hence we look at https://www.shodan.io/search?query=LightSpeedCorp

Flag: `$CDDC19${B1g-T3ch-Br0thers-4re-Wa7ching-U}`

## [R-3-1] Have They Been Pwned?
>Breaking News: Mega conglomerate LightSpeedCorp's massive data breach. Is YOUR data safe?

>[LATEST UPDATE] LSC's CEO apologises publicly and acknowledges lapses in security. Pledges to treat sensitive customer data with utmost care and implement stricter measures.

We treated this as an news, so we googled the keyword "lightspeedcorp" with the `"`

This lead us to a [pastebin](https://pastebin.com/0v86Wua7) which contain the flag.

Flag: `$CDDC19${7H0u_H4sT_L3ArN3D_2_G000GLE}`

## [R-3-2] cHash Me Outside How 'Bout Dat

After doing `[R-3-1]` we visited the author of the pastebin, which gave us another set of (information)[https://pastebin.com/dWFhPc09]

We found some hash from there and uses hashcat example hashes `bcrypt $2*$, Blowfish (Unix)` to identify what kind of hash it is.

We then crack the hash and the flag was one of the password.
```
$2y$12$t8gqp.grVkUNPX9tEGRTBubOoxyYSFoJbQLQ.7FVYmUA4dL2oFWoa:september
$2y$12$5ITbt5DwyFp13yzfwOdm0.LWd3BqzVGhzObOmlb0gg2t/MI8LoM2G:starlight
$2y$12$0vki08h.GxvQliWCIcRVR.1cwuz6Yq0J5cqbDVSHHoo6R6JHLciNK:martha
$2y$12$4Z/4caJqv9Lfn/XvLwRnMumrqO5gxjHDYJG1xgToOwzDT/Lbf0ddm:christopher
$2y$12$DebHJ4WhdnDHX6OxSUp8au0h/iXXtDe4DtQv6OB0KhIdZDIOM5Tna:britney
$2y$12$vZZlVQxannN7EvVMzcfG/ObBvjn8PY.XXjbPajWxBg6jQcE/IHgz2
$2y$12$RjHkGRN2CoZuzHcP//jG0OQ9DcFjupmrwifly8cAKk1S//2uFoZHC:patricia
$2y$12$650fuI4woIS8BzBij.JvtusZxfv8Ltj1JR7QYaUhNduB11IlxGtkS:princesa
$2y$12$i9X0wzoW6BNJa/XOLtDrBu3PK1I8mBmyqvVQdawQIx5cwAa/8xId2:123123
$2y$12$rW6BMlkldp8gh7UgPxdAf.AWBY9uT2R1dhkfsmdAv923kG6rCFB/q:simpsons
$2y$12$9DfRXL9p2sIv9UK3Gzh9N.C7Qdq5mKFNPHSCzKL.7JE3cJPIeyVd.:pickles
$2y$12$U/mnGyz66cf8gt/4m7vXVuIvcXOInLvTWsZ1ts621gd9H32lXmE4m:moocow
$2y$12$Ntymbb5z9HuarQY3a2Od5OjprXR52EjDMTrqqaGZCJI0gYKqSc1cG:dragon1
$2y$12$C5XKdv5dV2i0ywNJByU78eHaEzwPk8NEABe.4AQOOO6KV2T0/en7O:savannah
$2y$12$eMed7u0NOskbuY.xIuEM1.uIyxrNMDoZVTvSvvB0QaNIRX8Vp.ZKu:rocky
```
Flag: `$CDDC19${starlight}`

## [R-4-1] Where I Get All My Memes From

> Red Team Tip #101: Always look for social media of our target company's personnel. Some have a tendency to overshare information about their company, which is always a good thing for us. :)

> Based on our bountiful elite hacking experiences, they usually create accounts on any of the Big Three social media platforms.

Remember that previously from `[R-0]` we gotten a name `Luther Torvalds`. 

After searching the social media, we found one at [Twitter](https://twitter.com/LutherTorvalds?lang=en)

This gave us the flag for `[R-4-1-1]`

Flag: `$CDDC19${WHR_R_MY_D4NK_MEMES}`

## [R-4-1-1] Who Uses Teams Anyway?

After finding the twitter of `Luther Torvalds`, we scan through his tweet and found the conversation between `Sjang Heinhuis` and him.

Visiting his twitter [profile](https://twitter.com/5jangh31nh1u5?lang=en) gave us more information. 

There was a photo which had a `http://bit.ly/lightspeedcorp` link as shown below

https://pbs.twimg.com/media/D5TqT23UIAE3cu4.jpg:large

Visiting the link gave us a `slack` invite. 

After looking through the slack, we found that there was a curator bot. Which was mention previously again on the twitter conversation.

Remember that they was some mention of `Star command`. https://en.wikipedia.org/wiki/Buzz_Lightyear_of_Star_Command

Hence we googled and gotten `Buzz-Lightyear` as the secret passphrase.

Flag: `$CDDC19${SL4CK_4_C00L_KIIIDS}`


## [R-4-1-2] Don't Be A Git

> Most developers generally love to share code that they've written. Not sure if that's such a good idea...

Challenge title hinted us that there will be a git repo. After looking through the both twitter of `Luther` and `Sjang`. 

We managed to find `Bobby Hashlinger` from the `Likes` tab. Note that this information can only be found if you are logged in. 

From `Bobby Hashlinger` we managed to find the git repo https://github.com/sjang3141592653

From the branches we found https://github.com/sjang3141592653/d4rkspeedcorp-framework/tree/super-new-feature

Inside one of the commits, contain the flag. However it was upside down. Hence after some googling. We managed to retrieve the flag.

Flag: `$CDDC19${D0n7_b3_5cAr3D_0f_c0MM1tM3nT5}`
