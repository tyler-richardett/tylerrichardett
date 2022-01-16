---
authors:
- tylerrichardett
tags:
- Soccer Analytics
- American Soccer Analysis
- R
date: "2021-08-26T00:00:00Z"
lastmod: "2021-08-26T00:00:00Z"
draft: false
featured: false
image:
  caption: 'Photo by [**Nathy dog**](https://unsplash.com/@nathdah) on [**Unsplash**](https://unsplash.com/photos/z1uDmJx3ZEQ).'
  focal_point: ""
  placement: 3
  preview_only: false
projects: []
summary: "Just by plotting each frame of these special goal-scoring sequences, it's enlightening to see how these attacking teams move and exploit space to ultimately unlock the opposing defense."
title: Using Optical Tracking Data from Second Spectrum to Visualize Long Goal-scoring Build-ups
---

Two weeks ago, Nashville SC scored a lovely team goal. All 10 field players contributed to a 15-pass sequence, putting Nashville up 2-1 over D.C. United.

Thanks to [Major League Soccer](https://www.mlssoccer.com/) and [Second Spectrum](https://www.secondspectrum.com/index.html), some of us lucky folks at [American Soccer Analysis](https://www.americansocceranalysis.com/) have access to 2D tracking data for every regular season and playoff MLS game. Just by plotting each frame of these special goal-scoring sequences, it's enlightening to see how these attacking teams move and exploit space to ultimately unlock the opposing defense.

Because I used `{gridExtra}` to arrange each component of the visualizations, I'm constructing and exporting each individual frame as a still image. To speed things up, I took advantage of `{doParallel}` and `{foreach}` to distribute the workload. And in order for each process's `{ggsave}` call to be able to write to the same location, I had to set `type = "cairo-png"`.

Finally, to stitch all the frames together into an MP4 file, I'm leveraging the `{mapmate}` [wrapper](https://leonawicz.github.io/mapmate/articles/ffmpeg.html) around the [FFmpeg command line tool](https://www.ffmpeg.org/):

```r
mapmate::ffmpeg(
    dir = tile_save_path, 
    pattern = glue::glue("{save_file_prefix}_%06d.png"),
    output_dir = gif_mp4_save_path, 
    output = glue::glue("{save_file_prefix}.mp4"),
    rate = export_fps, 
    start = start_frame, 
    overwrite = TRUE
)
```

This content was originally developed as part of a Twitter thread, and each original tweet is embedded below. The videos are best viewed on desktop.

#### August 15, 2021  &nbsp;|&nbsp; Nashville SC (2) - 1 D.C. United

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Two weeks ago, <a href="https://twitter.com/hashtag/EveryoneN?src=hash&amp;ref_src=twsrc%5Etfw">#EveryoneN</a> scored a lovely team goal. All 10 field players contributed to a 15-pass sequence, putting Nashville up 2-1.<br><br>Thanks to <a href="https://twitter.com/MLS?ref_src=twsrc%5Etfw">@MLS</a> and <a href="https://twitter.com/SecondSpectrum?ref_src=twsrc%5Etfw">@SecondSpectrum</a>, we <a href="https://twitter.com/AnalysisEvolved?ref_src=twsrc%5Etfw">@AnalysisEvolved</a> get an aerial view of these special build-ups. They’re more common than you might think! <a href="https://t.co/gqEUDqrLt1">pic.twitter.com/gqEUDqrLt1</a></p>&mdash; Tyler Richardett (@TylerRichardett) <a href="https://twitter.com/TylerRichardett/status/1430980050220994561?ref_src=twsrc%5Etfw">August 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

#### August 21, 2021  &nbsp;|&nbsp; Columbus Crew 1 - (2) Seattle Sounders FC

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr">More recently, a late-game winner from <a href="https://twitter.com/hashtag/Sounders?src=hash&amp;ref_src=twsrc%5Etfw">#Sounders</a> was the product of 19 consecutive passes, a forced turnover immediately after the <a href="https://twitter.com/hashtag/Crew96?src=hash&amp;ref_src=twsrc%5Etfw">#Crew96</a> restart, and an effective long ball from <a href="https://twitter.com/hashtag/MLSAllStar?src=hash&amp;ref_src=twsrc%5Etfw">#MLSAllStar</a> captain Cristian Roldan. <a href="https://t.co/muW7nIhU3x">pic.twitter.com/muW7nIhU3x</a></p>&mdash; Tyler Richardett (@TylerRichardett) <a href="https://twitter.com/TylerRichardett/status/1430980520452710400?ref_src=twsrc%5Etfw">August 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

#### July 25, 2021  &nbsp;|&nbsp; Inter Miami CF 1 - (1) Philadelphia Union

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr">This 27-pass sequence from <a href="https://twitter.com/hashtag/DOOP?src=hash&amp;ref_src=twsrc%5Etfw">#DOOP</a> had a few quick switches in the <a href="https://twitter.com/hashtag/InterMiamiCF?src=hash&amp;ref_src=twsrc%5Etfw">#InterMiamiCF</a> half and an impressive exchange between Sullivan and Gazdag at the top of the 18-yard box.<br><br>But it was a poor pressing attempt from Gonzalo Higuaín that allowed Philadelphia to strike quickly. <a href="https://t.co/e0POv6RV0S">pic.twitter.com/e0POv6RV0S</a></p>&mdash; Tyler Richardett (@TylerRichardett) <a href="https://twitter.com/TylerRichardett/status/1430980932845154313?ref_src=twsrc%5Etfw">August 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

#### July 17, 2021  &nbsp;|&nbsp; Toronto FC (1) - 0 Orlando City SC

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr"><a href="https://twitter.com/hashtag/TFCLive?src=hash&amp;ref_src=twsrc%5Etfw">#TFCLive</a> scored their opener in July’s game against <a href="https://twitter.com/hashtag/VamosOrlando?src=hash&amp;ref_src=twsrc%5Etfw">#VamosOrlando</a> after stringing together 19 consecutive passes in under 50 seconds.<br><br>Altidore’s link-up play also pulled Jansson well out of position and ultimately forced an aerial matchup against Moutinho. <a href="https://t.co/wsqKem6QeM">pic.twitter.com/wsqKem6QeM</a></p>&mdash; Tyler Richardett (@TylerRichardett) <a href="https://twitter.com/TylerRichardett/status/1430981203553886217?ref_src=twsrc%5Etfw">August 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

#### July 3, 2021  &nbsp;|&nbsp; CF Montréal (1) - 0 Inter Miami CF

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr">Side-to-side movement from <a href="https://twitter.com/hashtag/CFMTL?src=hash&amp;ref_src=twsrc%5Etfw">#CFMTL</a> seemed to lull <a href="https://twitter.com/hashtag/InterMiamiCF?src=hash&amp;ref_src=twsrc%5Etfw">#InterMiamiCF</a> to sleep in this 22-pass sequence.<br><br>And Toye’s run at 40:29 enables Quioto, Mihailović, and Choinière to turn and run hard at what’s left of Miami’s defense. <a href="https://t.co/LQ5AcP1vOb">pic.twitter.com/LQ5AcP1vOb</a></p>&mdash; Tyler Richardett (@TylerRichardett) <a href="https://twitter.com/TylerRichardett/status/1430981269597343746?ref_src=twsrc%5Etfw">August 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

#### June 19, 2021  &nbsp;|&nbsp; FC Cincinnati 0 - (2) Colorado Rapids

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr"><a href="https://twitter.com/hashtag/Rapids96?src=hash&amp;ref_src=twsrc%5Etfw">#Rapids96</a> scored their goal on the road against <a href="https://twitter.com/hashtag/FCCincy?src=hash&amp;ref_src=twsrc%5Etfw">#FCCincy</a> after 16 consecutive passes.<br><br>Cruz and Kubo simultaneously apply pressure to the ball, leaving Price with plenty of space to drive at the Cincinnati defense and play an incisive pass toward Lewis. <a href="https://t.co/MkFrhm5D9A">pic.twitter.com/MkFrhm5D9A</a></p>&mdash; Tyler Richardett (@TylerRichardett) <a href="https://twitter.com/TylerRichardett/status/1430981323443822601?ref_src=twsrc%5Etfw">August 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

#### May 2, 2021  &nbsp;|&nbsp; Seattle Sounders FC (2) - 0 LA Galaxy

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr">During week 3, <a href="https://twitter.com/hashtag/Sounders?src=hash&amp;ref_src=twsrc%5Etfw">#Sounders</a> strung together 27 consecutive passes en route to Brad Smith’s second goal in two games.<br><br>Seattle took advantage of the space out wide in their build-up, pulling the <a href="https://twitter.com/hashtag/LAGalaxy?src=hash&amp;ref_src=twsrc%5Etfw">#LAGalaxy</a> defense to one side while Smith floated in at the back post. <a href="https://t.co/yqX6mbXVTk">pic.twitter.com/yqX6mbXVTk</a></p>&mdash; Tyler Richardett (@TylerRichardett) <a href="https://twitter.com/TylerRichardett/status/1430981390254977024?ref_src=twsrc%5Etfw">August 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

#### November 22, 2020  &nbsp;|&nbsp; Minnesota United FC (3) - 0 Colorado Rapids

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr">Leading up to their third goal in the opening round of last year’s playoffs, <a href="https://twitter.com/hashtag/MNUFC?src=hash&amp;ref_src=twsrc%5Etfw">#MNUFC</a> completed 24 consecutive passes.<br><br>A smart run from Molino ultimately draws out a <a href="https://twitter.com/hashtag/Rapids96?src=hash&amp;ref_src=twsrc%5Etfw">#Rapids96</a> center back, leaving Reynoso with plenty of space to drive forward as other Minnesota attackers join. <a href="https://t.co/Z4PJLJzN3B">pic.twitter.com/Z4PJLJzN3B</a></p>&mdash; Tyler Richardett (@TylerRichardett) <a href="https://twitter.com/TylerRichardett/status/1430981455371456518?ref_src=twsrc%5Etfw">August 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

#### November 1, 2020  &nbsp;|&nbsp; Colorado Rapids (1) - 0 Seattle Sounders FC

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr">This 17-pass sequence from <a href="https://twitter.com/hashtag/Rapids96?src=hash&amp;ref_src=twsrc%5Etfw">#Rapids96</a> against <a href="https://twitter.com/hashtag/Sounders?src=hash&amp;ref_src=twsrc%5Etfw">#Sounders</a> is a great illustration of absorbing the opponent’s press and striking quickly when space opens up.<br><br>Price is fortunate not to turn the ball over to Ruidíaz in a very dangerous area, but Colorado makes no mistake afterward. <a href="https://t.co/iU1mfssJ2e">pic.twitter.com/iU1mfssJ2e</a></p>&mdash; Tyler Richardett (@TylerRichardett) <a href="https://twitter.com/TylerRichardett/status/1430981533452615684?ref_src=twsrc%5Etfw">August 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

#### October 14, 2020  &nbsp;|&nbsp; Vancouver Whitecaps FC (1) - 0 Los Angeles FC

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr">Another example comes courtesy of <a href="https://twitter.com/hashtag/VWFC?src=hash&amp;ref_src=twsrc%5Etfw">#VWFC</a> and their 19-pass sequence against <a href="https://twitter.com/hashtag/LAFC?src=hash&amp;ref_src=twsrc%5Etfw">#LAFC</a>.<br><br>With Vancouver inviting pressure from LAFC&#39;s forwards, Rossi and BWP commit, Bush breaks the first line with a pass to Bikel, Bikel finds Dájome with a long ball, and Vancouver is off to the races. <a href="https://t.co/GLlMagCIeo">pic.twitter.com/GLlMagCIeo</a></p>&mdash; Tyler Richardett (@TylerRichardett) <a href="https://twitter.com/TylerRichardett/status/1430981598380498956?ref_src=twsrc%5Etfw">August 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

#### September 23, 2020  &nbsp;|&nbsp; Real Salt Lake (2) - 0 LA Galaxy

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr">Against <a href="https://twitter.com/hashtag/LAGalaxy?src=hash&amp;ref_src=twsrc%5Etfw">#LAGalaxy</a> last September, <a href="https://twitter.com/hashtag/RSL?src=hash&amp;ref_src=twsrc%5Etfw">#RSL</a> put 17 consecutive passes together before doubling their lead.<br><br>After a switch from Glad, smart running from Baird and Rusnák draws out LA’s right back — leaving Rusnák with ample space and time to find Kreilach alone at the penalty spot. <a href="https://t.co/yS35khkgCZ">pic.twitter.com/yS35khkgCZ</a></p>&mdash; Tyler Richardett (@TylerRichardett) <a href="https://twitter.com/TylerRichardett/status/1430981663123779589?ref_src=twsrc%5Etfw">August 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

#### August 26, 2020  &nbsp;|&nbsp; Orlando City SC (1) - 1 Nashville SC

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr">And here, effective counter-pressing from <a href="https://twitter.com/hashtag/VamosOrlando?src=hash&amp;ref_src=twsrc%5Etfw">#VamosOrlando</a> deep in the <a href="https://twitter.com/hashtag/EveryoneN?src=hash&amp;ref_src=twsrc%5Etfw">#EveryoneN</a> half yields 17 consecutive passes and an equalizer from Mueller.<br><br>Controlled passing in tight quarters — particularly from Méndez — and a killer first-time ball from Pereyra make the difference. <a href="https://t.co/CN1LqblkuY">pic.twitter.com/CN1LqblkuY</a></p>&mdash; Tyler Richardett (@TylerRichardett) <a href="https://twitter.com/TylerRichardett/status/1430981724054360066?ref_src=twsrc%5Etfw">August 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

*Data: Second Spectrum*
