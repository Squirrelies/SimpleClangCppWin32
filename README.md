# Simple Clang C++ project for Win32

## Description

A simple project template for a Win32 executable and library built using Clang-CL with CMake and VCPkg.

## Goal

The goal of this project is to have a somewhat minimal project containing various parts I commonly have in my projects such that I can clone this repo, make a few monifications and have a new application or library started quickly.

## Prerequisites

1. Visual Studio 2026 Build Tools (for SDK and STL)

    `winget install -e --id Microsoft.VisualStudio.BuildTools -a x64 --override "--passive --wait --add Microsoft.VisualStudio.Component.VC.Tools.x86.x64 --add Microsoft.VisualStudio.Component.Windows10SDK"`

2. LLVM Clang

    `winget install -e --id LLVM.LLVM -a x64`

3. CMake

    `winget install -e --id Kitware.CMake -a x64`

4. Ninja

    `winget install -e --id Ninja-build.Ninja -a x64`

5. Git

    `winget install -e --id Git.Git -a x64`

6. VCPkg

    ```powershell
    git clone https://github.com/microsoft/vcpkg.git .
    .\bootstrap-vcpkg.bat
    ```

    * Set `VCPKG_ROOT` environment variable to the folder you cloned the VCPkg repo into.
    * Add the folder you cloned the VCPkg repo in into the `PATH` environment variable.
