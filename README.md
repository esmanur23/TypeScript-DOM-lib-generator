# CreateDomJSTS
This tool is used to generate the DOM related part of `lib.d.ts` for TypeScript, and `domWeb.js` and `domWindows.js` for Visual Studio JavaScript language service. The input file is the XML spec file generated by the Microsoft Edge browser.

## Build Instruction
**Required Software**: Visual Studio 2015 Community Version (with Visual F# installed)

To build the tool, simply open the `Generator.sln` in Visual Studio and build the solution. A nuget restore should be done automatically before the build.

Press `F5` in Visual Studio to run the tool. If it runs successfully, the output files will be generated under the `generated` folder.

## Code Structure
- `Shared.fs`: handles the parsing from XML spec file, and stores the common data structures for later use;
- `TS.fs`: handles the emitting of the `lib.d.ts` file;
- `JS.fs`: handles the emitting of the `domWeb.js` and `domWindows.js`
files used for Visual Studio JavaScript language service;
- `Program.fs`: entry point of the tool;
- Inside the `inputfiles` folder:
    - `browser.webidl.xml`: the XML spec file generated by Microsoft Edge (due to the different updating schedules between Edge and TypeScript, this is **not** the most up-to-date version of the spec);
    - `jsTemplate.js`: the initial templates for `domWeb.js` and `domWindows.js`, which contains the necessary helper functions;
    - `additionalSharedTypes.ts`: types should exist in both browser and webworker that are missing from the Edge spec.
    - `additionalDomTypes.ts`: types should exist in only browser that are missing from the Edge spec.
    - `additionalWorkerTypes.ts`: types should exist in only webworker that are missing from the Edge spec.
