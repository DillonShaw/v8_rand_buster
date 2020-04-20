# v8_rand_buster

Breaks the following pattern in modern V8 javascript engine.

```
Math.floor(CONST * Math.random())
```

Credits to [Douglas Goddard](https://github.com/TACIXAT) for the initial work and blog post that helped explain how to solve this problem initially.

# Usage

Assuming you've [watched the talk](https://www.youtube.com/watch?v=_Iv6fBrcbAM) and understand the nuances of how this works, the following should serve as a simple explanation that can get you going with this tool.

## Getting the seed
```
cat codes.txt | tac | python3 xs128p.py --multiple <MULTIPLE>
```

example codes.txt
```
12345
23451
34512
45123
51234
.
.
.
```

* **codes.txt**: an in-order list of codes you leaked from the `Math.floor(Math.random() * CONST)` invocations.
* **tac**: reverses the list (watch the talk for more details and how this might go wrong)
* **<MULTIPLE>**: equivalent to `CONST` in the `Math.floor(Math.random() * CONST)` expression.

## Getting the next secrets
Note: _this gets the next outputs of the internal math.random calls after flooring. this will not get the next JS call to math.random. See the talk for more details_

```
python3 xs128p.py --mutliple <MULTIPLE> --gen <SEEDS>,<NUMBER_OF_OUTPUTS>
```

* **<MULTIPLE>**: Same as above ^
* **<SEEDS>**: The seeds generated by the above step
* **<NUMBER_OF_OUTPUTS>**: the number of floor randoms you'd like generated. This should be greater than the number of codes you originally used to generate the seed if you want unknown values.
