# Artifact from the PLDI '21 paper "Retrofitting Effect Handlers onto OCaml"

The repository contains the source files. The easiest way to run the benchmarks is to use the artifact submitted to the PLDI '21 artifact evaluation (AE). This is done by:

```bash
docker run -v "$(pwd)"/temp:/host --cap-add SYS_ADMIN -it kayceesrk/pldi82artifact:latest
```

Then, look at `README.md` in the home directory of the docker container for further instructions. 

## Timing using perf and Intel PT

```bash
sudo sh -c 'echo 104857600 > /proc/sys/kernel/perf_event_mlock_kb'
perf record -m 512,100000 -e intel_pt/cyc=1,cyc_thresh=2/u ./<snippet>
perf script --itrace=i0ns --ns -F time,pid,comm,sym,symoff,insn,ip | xed -F insn: -S /proc/kallsyms -64
```
