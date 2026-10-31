# Three.js reconstruction miner

Generation pipeline in `sn17gen/` is derived from research-somthing-t/lumen-kit (commit 3594fd1a), with prompt rules adapted from golden217/sn17gen and from our earlier releases, a two-order final pick, and error-handling changes. Runner and entry point from our earlier release.

Three chains (plain, proportions-first and plain again; each generates, then refines the latest valid module twice against renders from the judge's four front cameras, repairing rejections) run stage by stage: the model calls of a stage run concurrently and all renders happen in a fixed order between stages. Request ids are fixed per chain step, so replay does not depend on thread timing. After the final pick, the picked module gets two more refinements in a row, each against the four camera views of the current module; a refined module is used only if it renders.
