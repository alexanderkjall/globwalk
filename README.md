# GlobWalk #
A cross platform crate for recursively walking over paths matching a Glob pattern.

Based on both `walkdir` &️ `globset` (❤), this crate inherits many goodies from both, such as 

Licensed under MIT.

### Documentation ###

[docs.rs/globwalk](https://docs.rs/globwalk/)

### Usage ###

To use this crate, add `globwalk` as a dependency to your project's `Cargo.toml`:

```toml
[dependencies]
globwalk = "0.1"
```

### Example ###

The following piece of code recursively find all mp3 and FLAC files:

```rust
extern crate globwalk;
use globwalk::GlobWalker;

fn search_and_destroy() {
    for track in GlobWalker::from_patterns(&["**/*.{mp3,flac}"], ".") {
        // Destroy satanic rhythms
        std::fs::remove_file(track.path()); 
    }
}
```


### Example: Tweak walk options

```rust
extern crate globwalk;
use globwalk::GlobWalker;

fn search_and_destroy() {
    let walker = GlobWalker::from_patterns(&["**/*.{mp3,flac}"], ".")
                    .max_depth(4)
                    .follow_links(true);
                    
    for track in walker {
        // Destroy symbolic satanic rhythms, but do not stray far.
        std::fs::remove_file(track.path()); 
    }
}
```