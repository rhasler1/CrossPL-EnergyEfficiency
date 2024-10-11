# ChatGPT as a Metacompiler for Energy Efficiency

Building on prior work (https://curricula.cs.luc.edu/97-energy-efficiency/content.html) where ChatGPT was used to optimize a vector dot product algorithm in C for energy efficiency, we now exaime ChatGPT's ability to compile and opitimize code across different programming languages.

## Rust Example
### ChatGPT translating simple vector dot in C to Rust.

```rust
use std::env;

fn dot_product(a: &[f64], b: &[f64]) -> f64 {
    let mut result = 0.0;
    for i in 0..a.len() {
        result += a[i] * b[i];
    }
    result
}

fn main() {
    let args: Vec<String> = env::args().collect();
    
    if args.len() != 2 {
        println!("Usage: {} <size>", args[0]);
        std::process::exit(1);
    }

    let size: usize = args[1].parse().expect("Please provide a valid number");

    let mut a: Vec<f64> = vec![0.0; size];
    let mut b: Vec<f64> = vec![0.0; size];

    // Initialize vectors
    for i in 0..size {
        a[i] = i as f64;
        b[i] = (size - i) as f64;
    }

    let result = dot_product(&a, &b);

    println!("Dot Product: {:.2}", result);
}
```
The above code was produced by ChatGPT.


### Using Rust crate Rayon for thread level parallelism (TLP).
```rust
use std::env;
use rayon::prelude::*;

fn dot_product(a: &[f64], b: &[f64]) -> f64 {
    a.par_iter()
        .zip(b.par_iter())
        .map(|(x, y)| x * y)
        .sum()
}

fn main() {
    let args: Vec<String> = env::args().collect();
    
    if args.len() != 2 {
        println!("Usage: {} <size>", args[0]);
        std::process::exit(1);
    }

    let size: usize = args[1].parse().expect("Please provide a valid number");

    let mut a: Vec<f64> = vec![0.0; size];
    let mut b: Vec<f64> = vec![0.0; size];

    // Initialize vectors
    for i in 0..size {
        a[i] = i as f64;
        b[i] = (size - i) as f64;
    }

    let result = dot_product(&a, &b);

    println!("Dot Product: {:.2}", result);
}
```
The above code was produced by ChatGPT.

## Standard library support for instruction level parallelism (std::arch).
TODO.
