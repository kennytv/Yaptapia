# Why you shouldn't take Yatopia's claims at face value

This list aims at collecting concrete evidence of larger missteps of the Yatopia project and its members. While every developer will at some point make an unforgiving mistake or give an unflattering comment, the points below should depict a clear regularity and severity to their mistakes.

## Disclaimer
Please do not harass Yatopia project members or users, that is far from the intent of this document. Its purpose is not to personally attack the team — I am sure they are nice people and they do not deserve to get unnecessarily spammed — but to warn users. Kindly make them aware of the shortcomings of Yatopia and potentially suggest they switch to [Tuinity](https://github.com/Tuinity/Tuinity) instead; do not do that on the Yatopia Discord either unless it naturally comes up in conversation.

## Server Integrity
* **Constant influx of non-trivial issues:** They regularly have to remove (other people's as well as their own) patches they include without understanding the code's implications or potential risks, or simply because they are unable to update the code — at worst even causing irreversible world/userdata corruption.
  * [Fully reverted "lithium-gen" patch](https://github.com/YatopiaMC/Yatopia/commit/caef4c9c65a1959913ade81b34079bd005067735) because of [a block issue](https://i.imgur.com/OOiDduH.png) (unfixed; the [original commit's description](https://github.com/YatopiaMC/Yatopia/commit/fd74d8f1add9fe6345bbd4fbac1ccdd0a471a092) named this as the cause of the block issue, but was later force pushed off the main branch).
  * [Fully reverted "Lithium-CompactSineLUT" patch](https://github.com/YatopiaMC/Yatopia/commit/9695531cbca90d60c3e0bdd52769923fc4c91c4b) because of [a block issue](https://i.imgur.com/4YbP8jT.png) (unfixed and later force pushed off the main branch).
  * [Fully reverted "Port-Cadmium" patch](https://github.com/YatopiaMC/Yatopia/commit/6e5e95f4927624fa33231de8b919279a1a9a16c3) because of [a block issue](https://i.imgur.com/j913EH7.png) (unfixed and later reverted).
  * [Fully reverted "Port-LazyDFU" patch](https://github.com/YatopiaMC/Yatopia/commit/7833379e6ff7303693878d19fc30d5a81b8a8a81) (see points below).
  * [Fully reverted "lithium-AI" patch](https://github.com/YatopiaMC/Yatopia/commit/7cf4be9f2f164591db4835e82437154766fc1d5d) because of mob AI issues.
  * [Fully reverted "Port-hydrogen" patch](https://github.com/YatopiaMC/Yatopia/commit/124113a289225384f7cb22a4ba47c8fbcd60b16f) because of block-state issues.
  * [Fully reverted "Add-JsonList-save-timings" patch](https://github.com/YatopiaMC/Yatopia/commit/d11f37a9642ca5fb80a793bf73ea2fb310078449) because of a Timings issue (unfixed).
  * [Fully reverted "New-Network-System" and "Port-krypton" patches, mostly reverted "Port-hydrogen" patch](https://github.com/YatopiaMC/Yatopia/commit/49133cb64377fbf45e7fd1009d811f17b2aab495) because of major networking issues.
  * [Fully reverted "Improve-task-performance" patch](https://github.com/YatopiaMC/Yatopia/commit/620a24c1550c44808096b88692294083510b8fde) because of chunk generation issues.
  * [Fully reverted "Use-offline-uuids-if-we-need-to", "Add-a-special-case-for-floodgate-and-offline-uuids", and "ProxyForwardDataEvent" patches](https://github.com/YatopiaMC/Yatopia/commit/aebd71f72489de12054a6206b75518dd904e8ce1) because of world corruption.
  * [Mostly reverted "Port-krypton" patch](https://github.com/YatopiaMC/Yatopia/commit/188fc31d79348fa24f5f77ca4e98b6c87e015aad) because of networking issues (unfixed).
  * ... and more, like [their Fabric optimization mod](https://github.com/YatopiaMC/C2ME-fabric/issues?q=is%3Aissue+label%3Abug).
* **Not properly reviewing pull requests:** If not evident enough from the examples above, they do not *properly* review their pull requests and ported patches, despite multiple people looking at them. This includes even the simpler ones with [obvious errors made by someone exclusively using the GH web editor](https://github.com/YatopiaMC/Yatopia/pull/451) (which could have easily been checked for syntax errors with an online tool or their IDE instead of [throttling their CI with test commits](https://i.imgur.com/oHEyZMr.png)).
* **Not putting enough thought into the patches they pull:** They unnecessarily [ported the Fabric mod LazyDFU](https://github.com/YatopiaMC/Yatopia/pull/458/files#diff-47d4aca49ad0b98536c5e3be217a3a3730d8d04fd9c8fce28e7ad67d59e88283) to absolutely no effect; LazyDFU's idea originated from a [Paper patch](https://github.com/PaperMC/Paper/blob/07a18c4579e037e315db339549251f6ad856f717/Spigot-Server-Patches/0570-Cache-DataFixerUpper-Rewrite-Rules-on-demand.patch) having the same result, which they had already included before (they removed the patch only after Tux, LazyDFU's developer, told them how unnecessary the port was).
* **Inadequate testing:** Despite Yatopia very proudly talking of their testing methods, their "Tester Team" solely relies on simply [starting a server running dev builds](https://i.imgur.com/oMoSaSt.png) and [checking whether or not it obviously breaks](https://i.imgur.com/Xid8Nba.png). As evident by the regular patch reverts and reoccuring issues, this is far from being a sufficient testing method. Additionally, their "benchmarks" only consist of contextually driven [Spark reports](https://github.com/YatopiaMC/Yatopia/pull/458) or [millisecond-per-tick comparisons](https://i.imgur.com/XF7oQe7.png). These are fine if done in a perfectly replicable environment or used as anecdotal evidence, but are an insufficient performance metric if used on their own *all the time*.
  * See [Starlight Technical Details](https://github.com/Spottedleaf/Starlight/blob/fabric/TECHNICAL_DETAILS.md) for an example of actual benchmarks using proper profilers, direct method cost comparison, and more controlled in-game testing environments (*additionally* used and presented *after* the fully controlled metrics).
* **Unmaintainability:** Aside from the constant patch reverts showing a lack of understanding of the code they pull, Yatoclip is another major example of Yatopia's unmaintainability. They created Yatoclip, a version of paperclip to put [most of the actual patch work to the people using Yatopia instead of their CI](https://github.com/YatopiaMC/Yatopia/pull/360) and had to [revert it](https://github.com/YatopiaMC/Yatopia/commit/fea0b562a5fdb4f3d9031f0875638c9543cfd7af) because they did not know how to update it after an upstream build script change — it was only fixed months later.
  * Yatopia's faulty build system fully [shaded **all** used Maven plugins and dependencies](https://i.imgur.com/1EdqJLj.png), which they did not realize or fix **for months**.
  * They [copy-pasted code](https://github.com/YatopiaMC/Yatopia/pull/339) from [Toothpick](https://github.com/jpenilla/Toothpick) in its entirety, but did not care to follow its updates or how it operates, resulting in them missing the reasonably easy fix for the dependency problem.
  * Their CI was broken for multiple weeks, with a large number of [unsuccessful attempts at fixing it](https://i.imgur.com/XzawWCW.png).
  * They [*almost completely* removed all of Yatoclip and their own (and copied) build system, as well as the ability to have multiple upstreams properly separated and automated](https://github.com/YatopiaMC/Yatopia/commit/3529db07f540335d635580bddb02d2ab71af1c85) while trying to fix a [block issue](https://github.com/YatopiaMC/Yatopia/issues/496) (which first appeared about a month earlier and has been taunting the project since, with the devs unable to find its actual cause), making Purpur their only *direct* upstream.
    * The [corresponding pr](https://github.com/YatopiaMC/Yatopia/pull/497) was closed a few days later after a small number of people reported still experiencing the issue, [silently removing the PR description](https://i.imgur.com/MhwNAhc.png).
    * The issue was "fixed" later, [blaming an older, unrelated Tuinity patch](https://imgur.com/a/DJsjQRD), despite the issue exclusively occurring on Yatopia with not a single confirmed report of it on Tuinity or Purpur.
    * The [only report](https://i.imgur.com/Yocb9xZ.png) (see the [Tuinity Discord](https://discord.com/channels/538139695079489581/685631970138652704/847275849148792842)) they have [continued using as their only piece of evidence](https://i.imgur.com/8VUCTNt.png) (see [their Discord](https://discord.com/channels/743126646617407649/842793127214841906/848662345025585212) for context) is very clearly manually constructed and not at all in line with the issue Yatopia has had; [every single screenshot on their issue tracker as well as Discord](https://drive.google.com/drive/folders/1enNEFTSEHMBDAVLhOdtHznXKQyWsPvUe) suggests that their issue is due to palette corruption, meaning one block-state will always be the *same* "wrong" block-state — **not** shuffled to *multiple* different types as seen in the fabricated screenshot.
    * Yatopia is yet to provide any evidence of where the issue came from other than "We restarted 1000+ times and it was fixed, so it must be this patch" or even when exactly the issue started happening in the first place.
* **Missing fixes handed on a silver plate:** They [accepted a PR to copy-paste a log4j class, excluding a very valid warning](https://github.com/YatopiaMC/Yatopia/pull/482) instead of searching for solutions online or even reading the Stack Overflow thread provided [in the original issue](https://github.com/YatopiaMC/Yatopia/issues/477), containing the proper one line fix.

## Yatopia Developers
* Yatopia's contributors are known to post [unconvincing evidence](https://www.reddit.com/r/admincraft/comments/i33ou9/what_is_yatopia_and_why_you_should_use_it_on_your/g0as9kr?utm_source=share&utm_medium=web2x&context=3) of their advantages. "Benchmarks" they provide only consist of vague, contextually driven millisecond-per-tick and ticks-per-second comparisons.
* The performance boost they pride themselves with mostly comes from inherently unsafe patches (see above, their issue tracker, and the number of patches they have to revert after issues come up) and otherwise the actually stable fork [Tuinity](https://github.com/Tuinity/Tuinity), made by someone with proper knowledge of concurrency safe handling, testing, and benchmarking.
* They lack basic knowledge of the server's interior workings, such as the *existence* of block palettes, and fall back to [wild guessing when it comes to issue debugging](https://i.imgur.com/GCyae2m.png) (see [their Discord](https://discord.com/channels/743126646617407649/748481748035436575/837808962630844456) for context).
* In a Yatopia fork (actually marked as "experimental", but still of importance) by Titanium, Yatopia's lead developer, you can find more examples of bad decision-making:
  * It contains an Airplane patch [specifically and clearly marked as badly designed](https://gitlab.com/titaniumtown/Hyalus/-/blob/1a4123d645104529044aef93eb401ab0205d45c1/patches/server/0015-MCMT-libraries.patch#L46).
  * It contains [a supposedly concurrent implementation of a FastUtil collection](https://gitlab.com/titaniumtown/Hyalus/-/blob/1a4123d645104529044aef93eb401ab0205d45c1/patches/server/0015-MCMT-libraries.patch#L2094) (see [here](https://github.com/jediminer543/JMT-MCMT/commit/1835236aba40b2496b439a29547b019aff47eed8#diff-95423e48b8c1bc78733eda586b72ceb32048200d5846f4a4f2783ed915cea40fR11) for one of the originals), which — evident to any developer knowing how [FastUtil](https://github.com/vigna/fastutil) works — **completely** nullifies any performance gain the library usually provides. In Titanium's blog, he [states these were provided jediminer543](https://www.gardling.com/www/blog/10-05-2021.html#Origins) and that he learned a lot from him; in reality, both are unable to find these obvious flaws of their own and copied code.
  * It contains a patch from Patina [to prevent plugins from detecting Yatopia when checking for its Config class](https://gitlab.com/Titaniumtown/Hyalus/-/blob/e0cf0e7846217349ce187dfb331f87e1439bf4c6/patches/server/0015-Patina-Changes.patch#L32) (with the patch otherwise only containing insignificant changes).
* 2 Yatopia team members (more seriously than jokingly) discussed [hackily bypassing plugins' server software checks](https://i.imgur.com/EGfvy2R.png) in Yatopia (see [their Discord](https://discord.com/channels/743126646617407649/842793127214841906/847912836209705000) for context).

## Other
* Developers from Paper, Tuinity, Purpur, Airplane, as well as large plugin projects like EssentialsX are strongly and explicitly advising against using Yatopia.
* Without having a single interaction on any of the Yatopia repositories, they blocked me (KennyTV) from their organization because I put them on the "[list-of-shame](https://github.com/KennyTV/list-of-shame)".

## Expected Counterarguments
This lists arguments Yatopia members *might* respond with or *actually have* responded with in the past.
* "We are stable *now*" - The regular reverts and issues in the main branch suggest otherwise.
* "It's not 'unmaintainable'" - Dropping entire patches as well as the self-made patch system instead of fixing them suggests otherwise.
* "You are nitpicking" - This list only contains *the most obvious and severe* errors and issues. A hypercritical list would be much longer and take apart the unsafe patches (including patches during development).
* "Just let people use what they want" - Every user has the right to be informed about the stability of the software they are using as well as the fact its project members are spreading blatant misinformation.
* "This is Paper throwing unnecessary hate at Yatopia" - I do not represent Paper with this list, and both I and Paper specifically condemn harassing other projects/project members. They do, however, care about users running stable software.
* "Link X you provided is a petty example and I can counter that" - If any point is *proven* to be incorrect, I will immediately change or remove it. However, unless a majority of this page can be well disputed with more than just circumstantial evidence, its arguments still stand. 

## Closing Note
It is important to note that all of this has **nothing to do with the personality of the Yatopia members mentioned**, and I am sure Titanium and the others are good people, not driven by malice, but by naivety.

No developer working with such complex software is free of making mistakes. It does, however, become clear that these are not just mistakes (accidents), but clear-cut errors (lack of expertise) if they happen on a regular basis. Even this would not be as much of a problem if the members of Yatopia did not advertise their fork as an all-in-one solution that delivers the best performance possible. Instead, they should drop their euphemistic use of the phrases "borrowing code" and "best in class performance" and clearly state that their fork is experimentally driven and that they can at no point make promises to the stability and actual performance of their own patches.

As is, more and more people blindly start believing Yatopia is *the* solution to all their performance problems and that the (properly stable) benefits stem from Yatopia, when they actually come from the forks they are based on, fully disregarding the very real chance of instability. Nonetheless, to end on a somewhat positive note; Yatopia is better than closed-source server forks found on MCM, but still is not much more than a few inexperienced people copy-pasting code and experimenting with their own, unsafe patches.

### Yatopia Yearbook
![Yatopia Yearbook](https://i.imgur.com/quPUmso.png)
