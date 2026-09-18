<!-- ## Example Entry 0

- Date: 2026-09-11
- Prompt:

  ```text
  give me overview on this lab
  ```

- Assistant/model: Codex (GPT-5-based; exact model variant not exposed)
- Reason for asking (inferred): To understand the lab's goals, required implementation tasks, experiments, report questions, and submission requirements before beginning the work.
- Assistance provided: Reviewed the complete 12-page Lab 06 handout and summarized the setup, five coding tasks, six experimental parts, expected checks, write-ups, and required submission artifacts.
- Assistant verification: Confirmed the PDF has 12 A4 pages and extracted/read all 12 pages, including Sections 1-12, the five TASK definitions, six write-up sections, and the submission checklist. No code, build, GPU measurement, or student result was claimed or verified.
- Student verification: Pending. The student should compare this overview with the lab handout and later verify implementation and measurements on their own machine. -->

## Entry 1

- Date: 2026-09-18
- Prompt:

  ```text
  help me fix this problem, i ran it in developer powershell for vs:

  (base) PS C:\Users\thana\Documents\Year3\Semester\_i\CG\CG\_lab7> make info
  cmake -S . -B build -DCMAKE\_BUILD\_TYPE=Release
  \-- Selecting Windows SDK version 10.0.26100.0 to target Windows 10.0.26200.
  CMake Error at CMakeLists.txt:15 (find\_package):
  By not providing "Findglfw3.cmake" in CMAKE\_MODULE\_PATH this project has
  asked CMake to find a package configuration file provided by "glfw3", but
  CMake did not find one.

  Could not find a package configuration file provided by "glfw3" with any of
  the following names:
  glfw3.cps
  glfw3Config.cmake
  glfw3-config.cmake

  Add the installation prefix of "glfw3" to CMAKE\_PREFIX\_PATH or set
  "glfw3\_DIR" to a directory containing one of the above files. If "glfw3"
  provides a separate development package or SDK, be sure it has been
  installed.

  \-- Configuring incomplete, errors occurred!
  make: \*\*\* [Makefile:11: info] Error 1
  ```

- Assistant/model: Codex (GPT-5-based; exact model variant not exposed)
- Reason for asking (inferred): To diagnose and fix the Windows CMake configuration failure caused by GLFW not being on CMake's package search path.
- Assistance provided: Inspected the project CMake files, Makefile, existing CMake cache, Vulkan SDK environment, vcpkg installation, and lab handout setup instructions. Confirmed GLFW is installed at `C:\vcpkg\installed\x64-windows\share\glfw3\glfw3Config.cmake`; added a Windows CMake prefix-path hint using `VCPKG_ROOT` with a `C:\vcpkg` fallback.
- Assistant verification: Confirmed the referenced GLFW CMake package exists at `C:\vcpkg\installed\x64-windows\share\glfw3\glfw3Config.cmake` and confirmed the CMake edit is present. Full configure/build verification was not completed because this Codex shell does not have the Visual Studio Developer PowerShell's `cmake` command on PATH.
- Student verification: Pending. The student should run the build and confirm the `info` program launches successfully.

## Entry 2

- Date: 2026-09-18
- Prompt:

  ```text
  Here what i got:

  [User reported that setting VCPKG_ROOT allowed CMake configuration to complete, but the build failed with MSVC error D8021 because `/Wextra` was passed, and `info.exe` was not produced.]
  ```

- Assistant/model: Codex (GPT-5-based; exact model variant not exposed)
- Reason for asking (inferred): To continue fixing the Windows build after GLFW discovery succeeded.
- Assistance provided: Diagnosed the new failure as GCC/Clang warning flags being passed to MSVC; changed `target_compile_options` to use `/W4` for MSVC and retain `-Wall -Wextra` for other compilers.
- Assistant verification: Confirmed the user’s output shows successful CMake configure/generation and the precise MSVC `/Wextra` failure. Build after the compiler-specific fix remains to be verified.
- Student verification: Pending. The student should rebuild and confirm that `info.exe` is generated and runs.

## Entry 3

- Date: 2026-09-18
- Prompt:

  ```text
  here is what i get:
  ```

- Assistant/model: Codex (GPT-5-based; exact model variant not exposed)
- Reason for asking (inferred): To diagnose why the successfully built `info.exe` exits without output.
- Assistance provided: Read the supplied terminal output. Interpreted exit code `-1073741515` as Windows status `0xC0000135` (missing DLL), while confirming from `vulkaninfo --summary` that Vulkan and both GPUs are available. Added a Windows post-build CMake command to copy vcpkg's GLFW runtime DLL beside each executable.
- Assistant verification: Confirmed the pasted output contains the missing-DLL exit code and successful Vulkan device enumeration. The post-build copy and runtime launch remain to be verified by rebuilding on the student's machine.
- Student verification: Pending. The student should rebuild and confirm that `info.exe` prints device/API/shader information.

## Entry 4

- Date: 2026-09-18
- Prompt:

  ```text
  Ok, I can build them now, and ready to go. Give me overview of this lab. what I have to do for some of the very first tasks?
  ```

- Assistant/model: Codex (GPT-5-based; exact model variant not exposed)
- Reason for asking (inferred): To understand the Lab 07 workflow and begin the first shader tasks correctly.
- Assistance provided: Reviewed the complete Lab 07 handout and prepared an overview of the five parts, six editable shader files, required measurements/write-ups, and the recommended order for starting with setup and Task 1.
- Assistant verification: Read all 16 pages of the supplied PDF and cross-checked the setup commands, task descriptions, check values, controls, and submission checklist. No shader implementation or student measurement was claimed.
- Student verification: Pending. The student should run the baseline commands and personally verify shader results and measurements on their machine.
