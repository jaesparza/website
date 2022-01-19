---
title: Nano VNA
weight: 1
bookToc: false
bookHidden: false
katex: true
---

# Working with data exported from NanoVNA saver in scikit-rf

## Working with Return Loss, SWR
Formulae
```
* Real and imaginary components, how to convert them to a return loss in dBs.
* How to convert the return loss in dbs to SWR.
```

## Exporting data

The NanoVNA will export data in the touchstone format, explain it.
```
* https://ibis.org/touchstone_ver2.0/touchstone_ver2_0.pdf
* https://github.com/NanoVNA-Saver/nanovna-saver/issues/245
```


https://en.wikipedia.org/wiki/Touchstone_file

An export for port 1 might look as follows:
```
# HZ S RI R 50
7000000 0.46634328677969067 -1.1851214135434094
7001500 0.4585382651110881 -1.1836587704235881
7003000 0.4505099729835122 -1.1856906840733143
7004500 0.4436196585461943 -1.186501241720678
...
```

## Processing with **scikit-rf**

```
* http://scikit-rf.org/
* https://github.com/scikit-rf/scikit-rf
```

## NanoVNA tips and tricks


## Misc resources

https://www.arrl.org/files/file/Technology/tis/info/pdf/q1106037.pdf
https://en.wikipedia.org/wiki/Touchstone_file