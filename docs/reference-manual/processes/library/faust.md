---
layout: default

title: Faust
description: "Using Faust in ossia score"

parent: Processes
grand_parent: Reference

permalink: /processes/faust.html
---

# Faust

![Faust]({{ site.img }}/reference/processes/faust.png "Faust")

[Faust](https://faust.grame.fr) is a domain-specific programming language, tailored for writing digital signal processing code, for instance audio effects and synthesizers, super easily.

It is mainly developed at [Grame](https://grame.fr), with an international community of contributors.

Faust DSP files can be drag'n'dropped directly inside a score. This will compile the DSP and embed it as a signal processor in the score.
Additionally, any `.dsp` file found recursively in the library folder will be detected and added under the `Faust` section in the [[Library|process library]].

Faust code can be edited directly from within the user interface, by clicking on the small "window" icon on the node header. One must press "Compile" when the code is ready to update it to the audio engine.

# Important links

* [Faust website & docs](https://faust.grame.fr)
* [User library](https://github.com/ossia/score-user-library/tree/master/Presets/Faust)

# Video tutorial

<div class="videoWrapper">
    <iframe src="https://www.youtube.com/embed/yvTjJMrFxR0" frameborder="0" allow="autoplay; encrypted-media; picture-in-picture" allowfullscreen></iframe>
</div>
