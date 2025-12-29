# Thinking in Rust

An interactive, project-based web course that teaches Rust through building real tools. No videos—just code, immediate feedback, and progressively complex projects.

## Philosophy

Rust's compiler is the best teacher. This course leverages that by embedding live coding environments where learners write, fail, read error messages, and iterate. Theory emerges from necessity: you learn ownership because your code won't compile without understanding it, not because someone explained it in advance.

Each project produces something genuinely useful. Learners finish the course with a toolkit of CLI utilities they built themselves.

## Course Structure

### Module 0: Setup & First Contact
- Installing Rust and understanding the toolchain
- Cargo basics: new, build, run, test
- **Micro-project**: A "Hello, Rust" that actually does something—prints system info, checks available disk space, or greets with current time
- First encounter with `rustfmt` and `clippy`

### Module 1: The Reliable Tool — A CLI File Utility
**Project**: `rfind` — a simplified `find` command for searching files

**Concepts introduced through building**:
- Argument parsing with `clap`
- Error handling with `Result` and the `?` operator
- Pattern matching with `match`
- Working with `std::fs` and `std::path`
- Structuring a binary crate

**Exercises**:
- Add glob pattern support
- Implement file size filters
- Handle permission errors gracefully
- Add colored output with `termcolor` or `colored`

**Checkpoint**: Tool correctly finds files matching criteria across nested directories, with helpful error messages for edge cases.

---

### Module 2: The Data Pipeline — A Log Analyzer
**Project**: `logscope` — parse, filter, and aggregate log files

**Concepts introduced through building**:
- Iterators: `map`, `filter`, `fold`, `collect`
- Ownership and borrowing in practice (why cloning sometimes, borrowing other times)
- Custom types: structs and enums for representing log entries
- Parsing with simple techniques (splitting, regex introduction)
- Traits: implementing `Display` and `FromStr`

**Exercises**:
- Support multiple log formats via trait abstraction
- Add time-range filtering
- Generate summary statistics
- Output as JSON using `serde`

**Checkpoint**: Tool processes a 100MB log file efficiently, demonstrating lazy iterator evaluation.

---

### Module 3: The Connected Tool — An API Client
**Project**: `fetchr` — a configurable HTTP client for APIs

**Concepts introduced through building**:
- Async/await fundamentals
- The `tokio` runtime
- HTTP with `reqwest`
- JSON serialization/deserialization with `serde`
- Configuration files with `toml` or `config`
- Environment variables and secrets handling

**Exercises**:
- Implement retry logic with exponential backoff
- Add request caching
- Support multiple endpoints from config
- Chain API calls where one result feeds another

**Checkpoint**: Tool fetches data from a real API, handles rate limits and errors, outputs formatted results.

---

### Module 4: The Parallel Engine — A File Processor
**Project**: `hashbatch` — parallel file hashing and deduplication

**Concepts introduced through building**:
- Threads and `std::thread`
- Channels for communication (`mpsc`)
- Shared state with `Arc` and `Mutex`
- The `rayon` crate for data parallelism
- Understanding when parallelism helps (and when it doesn't)

**Exercises**:
- Compare single-threaded vs parallel performance
- Implement a progress bar with `indicatif`
- Add support for different hash algorithms
- Find and report duplicate files

**Checkpoint**: Tool hashes 1000 files using all CPU cores, with measurable speedup over sequential version.

---

### Module 5: The Living System — A Terminal Roguelike
**Project**: `descent` — a simple dungeon crawler in the terminal

**Concepts introduced through building**:
- Game loop architecture
- ECS-lite: organizing entities, components, systems
- Lifetimes in practice (references between game objects)
- Terminal UI with `ratatui`
- Random generation with `rand`
- State machines for game logic

**Exercises**:
- Procedural dungeon generation
- Simple enemy AI
- Inventory system
- Save/load game state with `serde`

**Checkpoint**: A playable game with movement, items, enemies, and win/lose conditions.

---

### Module 6: The Robust System — Testing & Refinement
**Project**: Return to previous projects and harden them

**Concepts introduced through building**:
- Unit tests and integration tests
- Property-based testing with `proptest`
- Benchmarking with `criterion`
- Documentation and doc tests
- Publishing to crates.io (optional)
- CI/CD basics with GitHub Actions

**Exercises**:
- Achieve >80% test coverage on one project
- Find and fix a performance bottleneck
- Write comprehensive documentation
- Refactor using lessons learned

**Checkpoint**: One project fully tested, documented, and publishable.

---

## Interactive Features

### Embedded Playground
Each lesson embeds a Rust playground where code compiles and runs in the browser. Learners see compiler output immediately—errors become teaching moments.

### Progressive Hints
Stuck? A three-tier hint system:
1. **Conceptual**: "Think about who owns this data"
2. **Directional**: "The `?` operator can help here"
3. **Concrete**: A code snippet showing one approach

### Ownership Visualizer
An animated diagram updates as learners write code, showing:
- Which variables own which data
- When borrows begin and end
- When values move or are dropped

### Adversarial Challenges
Special exercises where the goal is to:
- Explain *why* broken code fails
- Write code that triggers a specific error
- Refactor working-but-bad code into idiomatic Rust

### Spaced Repetition
Concepts a learner struggled with resurface in later modules, interleaved with new material.

---

## Technical Architecture

```
thinking-in-rust/
├── web/                    # Frontend application
│   ├── src/
│   │   ├── components/     # UI components
│   │   ├── lessons/        # Lesson content (MDX or similar)
│   │   ├── playground/     # Embedded Rust playground integration
│   │   └── visualizers/    # Ownership/borrow visualizers
│   └── ...
├── api/                    # Backend services
│   ├── src/
│   │   ├── compiler/       # Rust compilation service
│   │   ├── exercises/      # Exercise validation
│   │   └── progress/       # User progress tracking
│   └── ...
├── content/                # Course content
│   ├── module-0/
│   ├── module-1/
│   └── ...
├── exercises/              # Exercise definitions and tests
│   ├── module-1/
│   │   ├── exercise-01.toml
│   │   ├── exercise-01-tests.rs
│   │   └── ...
│   └── ...
└── tools/                  # Development utilities
    ├── content-validator/
    └── exercise-runner/
```

### Technology Choices (Proposed)

**Frontend**: Astro (familiar to you) with interactive islands for playground and visualizers. React or Solid for complex interactive components.

**Playground**: Integration with Rust Playground API, or self-hosted solution using `rustc` in WASM or containerized compilation.

**Backend**: Rust with Axum—dogfooding the language we're teaching.

**Content**: MDX or a custom format allowing embedded interactive elements within prose.

**Database**: SQLite or PostgreSQL for user progress, exercise results, spaced repetition data.

---

## Development Roadmap

### Phase 1: Foundation
- [ ] Set up monorepo structure
- [ ] Create content format specification
- [ ] Build basic lesson renderer
- [ ] Integrate Rust Playground API
- [ ] Design and implement hint system

### Phase 2: Module 0 & 1
- [ ] Write Module 0 content
- [ ] Write Module 1 content and exercises
- [ ] Build exercise validation system
- [ ] Implement progress tracking
- [ ] User testing and iteration

### Phase 3: Core Modules
- [ ] Complete Modules 2-4
- [ ] Build ownership visualizer (MVP)
- [ ] Add adversarial challenges
- [ ] Implement spaced repetition logic

### Phase 4: Advanced & Polish
- [ ] Complete Modules 5-6
- [ ] Refine visualizers
- [ ] Performance optimization
- [ ] Accessibility audit
- [ ] Prepare for public launch

---

## Claude Code Project Context

This project uses Claude Code for development assistance. Key context:

**Primary language**: Rust for backend and exercise validation; TypeScript for frontend.

**Coding style**: 
- Rust: Follow standard `rustfmt` conventions, prefer explicit error handling over unwrap
- TypeScript: Strict mode, functional patterns where sensible

**Key decisions**:
- Content and code are separate concerns—lessons are data, not hardcoded
- Exercises are defined declaratively with TOML and validated by Rust test harnesses
- Progressive disclosure in UI—complexity revealed as needed

**When helping with this project**:
- Prioritize learner experience over technical elegance
- Compiler errors are features—design exercises that make them instructive
- Each project should produce something the learner would actually use

---

## Contributing

This project is in early development. Contributions welcome in:
- Course content and exercise design
- Frontend interactive components
- Rust exercise validation tooling
- Accessibility improvements

---

## License

Content: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)  
Code: MIT

---

## Acknowledgments

Inspired by the belief that programming is best learned by building, and that Rust's compiler—often seen as an obstacle—is actually the most patient and precise teacher available.
