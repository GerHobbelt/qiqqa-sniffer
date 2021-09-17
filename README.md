# Qiqqa Sniffer (*The Gonzo Lab™ Version*)

The Qiqqa Sniffer provides the workflow/UI/UX where you can **search many websites (Google Scholar, MedArchiv & _many_ others)** for document *metadata*, *abstracts* and/or related documents, while you view both the PDF you started with and the related documents that pop up in the search.

You can copy&paste *any text* from the source PDF document directly into the search engine query form to help yyou find the stuff you are looking for!

When your search ("sniff seession") uncovers any bibTeX or other metadata anywhere that matches your document, this data is automatically imported (with the option to *review* and *edit/adjust* before accepting).

You are also enabled to edit/augment/correct any *existing* metadata for your source document in the provided editor pane, empowering you to use easy copy&paste actions from both the searched web pages and the source document itself to significantly speed up the process of metadata extraction/metadata construction/metadata quality verification.

Qiqqa Sniffer also provides an easy means to step/browse/jump through your (Qiqqa) document library, editing and reviewing in **bulk** all the documents in need. (You can **filter** the library set by several criteria to produce specific document batches for (automated or manual) processing by the Sniffer.

## Qiqqa Sniffer = A 360 panoramic process

Ease of use and **Speed** in working is achieved by having all the relevant parts on screen and accessible at the same time, without the need to cycle through *any* tabs or windows: **Drag, Copy/Mark, Point, PASTE! (Next: Repeat!)**

## The *Gonzo Lab™* version?!

Yup. This is the laboratory version, developed at our Gonzo Lab™, which aims to replace the existing Qiqqa Sniffer functionality in Qiqqa Open Source. Base criteria:

> <sup>I don't call them *requirements* for in the lab we are quite flegmatic/fluid, possible even *liquid* 😄</sup>

- *ready for cross-platform* 

  while we may not build on Linux, such should be a *minimal* hassle. [Qiqqa/215](https://github.com/jimmejardine/qiqqa-open-source/issues/215), mind you!
- WPF is 🙀🦛🐷☠️🥩💣💥! Horribly non-portable and a total kill-joy to use.

  Again: [Qiqqa/215](https://github.com/jimmejardine/qiqqa-open-source/issues/215). Also: [CEF?](https://github.com/jimmejardine/qiqqa-open-source/blob/master/docs-src/Progress%20in%20Development/Moving%20away%20for%20Windows-bound%20UI%20(WPF)%20to%20HTML%20-%20feasibility%20tests%20with%20CEF%2BCEFSharp%2BCEFGlue%2BChromely.md), [Bloody Nuisances \#1](https://github.com/jimmejardine/qiqqa-open-source/blob/master/docs-src/Progress%20in%20Development/Considering%20the%20Way%20Forward/Essential%20yet%20hard(er)%20to%20port%20UI%20features.md) & [\#2](https://github.com/jimmejardine/qiqqa-open-source/blob/master/docs-src/Progress%20in%20Development/Considering%20the%20Way%20Forward/Full-Text%20Search%20Engines.md), [😭Sniffer Woes🧅](https://github.com/jimmejardine/qiqqa-open-source/blob/master/docs-src/Progress%20in%20Development/Considering%20the%20Way%20Forward/Qiqqa%20Sniffer%20-%20or%20how%20to%20access%20Google%20Scholar%20et%20al.md) 

## The Goal

The goal is to arrive at an independent, workable, solution here, which is usable across platforms and which may be joined/merged back into Qiqqa when this is deemed *wise*. Or *sane*. Or... well.


## Screenshots

TBD

## Screenshots (from Qiqqa Open Source, the original)

TBD


## Technology Choices

The pondering has been done over at [Qiqqa Docs](https://github.com/jimmejardine/qiqqa-open-source/tree/master/docs-src/Progress%20in%20Development). Here we take it to the next level. 🤸

After a long bout of 🤔 ho, 🤔 ha, 🤔 hum & several 💔🧨⚗️ trials 🧪💥💔, we *knew* we'ld have to be using CEF and *possibly* WebView2 or others native to their platforms. We also saw that generally, C# interfaces (a.k.a. "*wrappers*") are lagging behind, introduce extra bugs or limit interface surface dramtically. Meanwhile, `electron` is the only truly *big* & *active* player when it comes to total 💯% web tech for any (Desktop) UI that gets beyond *tawdry web app* form filler equivs, while even there there's troubles with multiple `webview`s as **we need for application & system security**: we will be browsing the 👿*evil*👿 *Web* in *one* of the Sniffer UI sections, while we must be able to do all sorts of *local* *fancy* *things* in the other parts of the UI. So the realization started to grow that we would have to do something similar to what Chromely was doing (quite nicely, I must say!) and then taking it up several notches: embedding **multiple** WebViews (with different security settings) in a single, *possibly neanest*, native UI wrapper.

Which has led us to picking a very old acquaintance of ours for the *native UI* bit: [**wxWidgets** (🧓 back in my time we called it **wxWindows** 👴)](https://github.com/wxWidgets/wxWidgets). In my opinion, that one is much nicer than Qt or what-have-you (probably because it always was looking *way* better on Windows boxes than any of the others) *plus* it's cross-platform portable *itself* right out of the box! 🥳🎉 

Of course, for us lab rats, nothing's ever easy: there's still [that bit of ho-hum 1700](https://github.com/wxWidgets/wxWidgets/pull/1700)[/706 😥](https://github.com/wxWidgets/wxWidgets/pull/706) but at least *native* WebView works straight out of the box and we have good hopes for Edge/CEF there. At least, *this* option looks like we might be able to pull this off in 2021 A.D. without indomitable roadblocks on the way towards production- & user-readiness.

Meanwhile, **wxWidgets** (*née wxWindows*) has been very stable and alive all those years while I was elsewhere; I still see the [*OGs*](https://www.dictionary.com/e/slang/og/) are around, so that's also giving off a good vibe towards *future soundness of technology choice* there!

*Plus* a little boon for folks like me: now I don't have to re-write every darn *pixel* of the UI in bleeding edge HTML/CSS/JS web tech if I don't want to / see another *faster or more efficient* way to get there! I'll have to 👨‍🌾 refresh a bunch of things in the brains 🧓🧠 but this means that menus and such can be done in native tech, which spares me the troubles you get when doing that stuff in a webview that's only painting **part** of the UI area -- as we would have happen in the Sniffer due to the need for separate WebView panes for user/machine safety reasons as we will be browsing *live web sites anywhere*!

But enough yakking! Let's get cookin'!

