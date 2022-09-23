

## Compile error Segmentation

When using a `.map(\.property_name)` in the Rx chain I was having 
```error

4. While evaluating request IRGenRequest(IR Generation for file "/Users/ksave/Projects/project_name-iOS/project_name-iOS/MissionControl.swift")

5. While emitting IR SIL function "@$s8project_name14MissionControlC27setupSessionInvalidBindings33_4F5CA743207C33309D9D1A59DF29AAF2LL5usingy0aB11Coordinator0fR4Type_p_tF".

 for 'setupSessionInvalidBindings(using:)' (at /Users/ksave/Projects/project_name-iOS/project_name-iOS/MissionControl.swift:336:5)

Stack dump without symbol names (ensure you have llvm-symbolizer in your PATH or set the environment var `LLVM_SYMBOLIZER_PATH` to point to it):

error: Segmentation fault: 11 (in target 'project_name' from project 'project_name-iOS')
```