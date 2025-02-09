---
layout: default

title: Math expressions
description: "Math expression syntax and processes in ossia score"

parent: Processes
grand_parent: Reference

permalink: /processes/exprtk.html
---

# ExprTK support

Several processes allow to write simple math expressions. Such processes include:

- Micromap: for very simple math expressions, e.g. `x * 100`.
- Audio Generator: generates multi-channel audio.
- Audio Mapping: filters multi-channel audio.
- Value Generator: generates values suitable for the device explorer.
- Custom Mapping (Value): filters values suitable for the device explorer.

![ExprTK]({{ site.img }}/reference/processes/exprtk.png)

These expressions are solved within *score* using the [ExprTK library](https://www.partow.net/programming/exprtk/index.html "ExprTK website").

The expression can be written in the process built-in editor on multiple lines.

Numerous math functions are available: `sin`, `cos`, `abs`, `log`, as well as the usual `pi`, etc. constants.

## Value generator

### Logistic function
```matlab
if(m1 == 0) {
  m2 := 0.8;
  m1 := 1;
}

var r := 4 * a;
m2 := r * m2 * (1 - m2);
m2;
```

## Value mapper

### Add jitter
```matlab
var rnd_m := pow(2, 31);
var rnd_a := 1103515245;
var rnd_c := 12345;

if(m2 == 0) {
  m2 := 1;
  m1 := 12345678;
}

var r := (rnd_a * m1 + rnd_c) % rnd_m;
m1 := r;
x + a * r / (2^33);
```

## Audio generator

### Sine wave
```matlab
var phi := 2 * pi * (20 + a * 500) / fs;

m1[0] += phi;

out[0] := b * cos(m1[0]);
out[1] := b * cos(m1[0]);
```

### Square wave
```matlab
var phi := 2 * pi * (20 + a * 500) / fs;

m1[0] += phi;

var f := cos(m1[0]) > 0 ? b : -b;
out[0] := f;
out[1] := f;
```
### Wobbly synth

```matlab
var freq_l := 225 +  cos(t/(100*(a+0.1)));
freq_l := 2 * pi * m1[0] *  freq_l * b / fs;

var freq_r := 215 +  sin(t/(100*(a+0.1)));
freq_r := 2 * pi * m1[0] *  freq_l * b / fs;

m1[0] += 1;

out[0] := b * cos( freq_l );
out[1] := b * cos( freq_r );
```

## Audio filter

### Crude distortion

2-channel version:
```matlab
out[0] := clamp(0,  tan(x[0]*log(1 + 200 * a)), 1);
out[1] := clamp(0,  tan(x[1]*log(1 + 200 * a)), 1);
```

Any number of channel version:
```matlab
var n := x[];

for (var i := 0; i < n; i += 1) {
  var dist := tan(x[i]*log(1 + 200 * a));
  out[i] := clamp(0, dist, 1);
}
```


## Available variables

### Everywhere
* t: the current time
* pos: the position in the interval
* a, b, c: three provided controls
* m1, m2, m3: three provided variables (which will keep their value across a tick)
  * In the audio cases they are arrays.

### Value mapping

* x: the value of the current input
* dt: the time delta

### Audio mapping

* x: the value of the current sample
* out: where to write the output
* px: the value of the previous sample
* fs: the sampling rate

### Value generator

* dt: the time delta

### Audio generator

* out: where to write the output
* fs: the sampling rate
