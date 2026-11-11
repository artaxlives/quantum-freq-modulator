# Changed from the plan

No functional changes. Implemented the single-file, zero-build page in `index.html`, with inline styles, JavaScript, and a 6,852-word authored corpus. The corpus consists of 60 modular field notes across twelve settings and five experimental subjects, yielding 135 vocabulary tokens. This deliberately patterned corpus makes n-gram transitions easy to inspect; it is not intended to represent general English.

The initial state synchronously generates 25 tokens from “a useful prediction begins with”. Eight ranked candidates, the last eight context tokens, individual oscillator traces, their sum, and historical score breakdowns are populated immediately. Step, Play/Pause, resonance weight, interference toggle, and a convenience Reset control work locally. Reset restores the seeded sequence under the current controls.

Scoring uses the highest available context table (trigram, bigram, then unigram), normalized to probabilities. Hash-derived frequencies and phases drive 64-sample damped context oscillators. Projection of the summed signal at each candidate frequency, relative to its phase, gives signed resonance. The combined score is `p + p × alpha × resonance`. Disabled interference or zero alpha gives exactly zero contribution, with no rounding-dependent residual. Zero-count candidates remain visible with zero scores. The waveform remains visible when scoring interference is disabled so the underlying context can still be inspected.

The computation only uses a fixed vocabulary, 64 samples, and eight recent tokens; historical text and log rows are appended rather than rescored. Historical row values retain the controls used when each token was generated. No external assets, dependencies, storage, or requests are used.

Validation: opened and executed the HTML in a Node DOM/canvas harness. Confirmed 25 initial `.gen-row` elements, eight `.candidate-bar` elements, nonzero canvas dimensions and drawing operations, meaningful initial generated text, exactly one additional row per Step, changed score readout on slider input, zero resonance after disabling interference and stepping, zero contributions at alpha zero, deterministic Reset, and continuing Play growth over 3.3 seconds (25 to 32 rows). No captured console errors. All local src/href references resolve; none are needed.

# Could not do

Nothing. All planned functionality is implemented.

# Omitted for lack of a service

Nothing. The experiment runs entirely in the page and requires no service.
