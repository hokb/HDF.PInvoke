![AppVeyor Project status badge](https://ci.appveyor.com/api/projects/status/github/HDFGroup/HDF.PInvoke?branch=master&svg=true)


# What it is (not)

HDF.PInvoke is a collection of [PInvoke](https://en.wikipedia.org/wiki/Platform_Invocation_Services)
signatures for the [HDF5 C-API](https://www.hdfgroup.org/HDF5/doc/RM/RM_H5Front.html).
It's practically *code-free*, which means we can blame all the bugs on Microsoft or [The HDF Group](https://www.hdfgroup.org/) :smile:

It is **not** a high-level .NET interface for HDF5. "It's the [GCD](https://en.wikipedia.org/wiki/Greatest_common_divisor)
of .NET bindings for HDF5, not the [LCM](https://en.wikipedia.org/wiki/Least_common_multiple)." :bowtie:

## Current Release Version(s)

| HDF5 Release Version                                                   | Assembly Version | Assembly File Version | Git Tag |
| ---------------------------------------------------------------------- | ---------------- | --------------------------------------------------------------- | ------- | ------- |
| [1.8.17](https://www.hdfgroup.org/HDF5/release/obtain5.html)           | 1.8.17.0         | [1.8.17.7](https://www.nuget.org/packages/HDF.PInvoke/1.8.17.7) | v1.8.17.7  |
| [1.10.0-patch1](https://www.hdfgroup.org/HDF5/release/obtain5110.html) | 1.10.0.0         | [1.10.0.3](https://www.nuget.org/packages/HDF.PInvoke/1.10.0.3) | v1.10.0.3 |

[How "stuff" is versioned.](../../wiki/Versioning-and-Releases)

## Quick Install:

To install the latest HDF.PInvoke 1.8, run the following command in the
[Package Manager Console](https://docs.nuget.org/docs/start-here/using-the-package-manager-console)
```
    Install-Package HDF.PInvoke -Version 1.8.17.7
```
To install the latest HDF.PInvoke 1.10, run the following command in the
[Package Manager Console](https://docs.nuget.org/docs/start-here/using-the-package-manager-console)
```
    Install-Package HDF.PInvoke -Version 1.10.0.3
```

# Prerequisites

The ``HDF.PInvoke.dll`` managed assembly depends on the following native DLLs (32-bit and 64-bit):
- HDF5 core API, ``hdf5.dll``
- HDF5 high-level APIs, ``hdf5_hl.dll``
- Gzip compression, ``zlib.dll``
- Szip compression, ``szip.dll``
- The C-runtime of the Visual Studio version used to build the former, e.g., ``msvcr120.dll`` for Visual Studio 2013

All native dependencies, built with [thread-safety enabled](https://www.hdfgroup.org/hdf5-quest.html#tsafe),
are included in the NuGet packages,
**except** the Visual Studio C-runtime, which is available from Microsoft as [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/en-us/download/details.aspx?id=40784). In the unlikely event that
they aren't already installed on your system, go get 'em!
(See [this link](https://msdn.microsoft.com/en-us/library/ms235299.aspx) for the rationale behind not
distributing the Visual Studio C-runtime in the NuGet package.)

## The DLL Resolution Process

On the first call to an ``H5*`` function, the application's configuration file
(e.g., ``YourApplication.exe.config``) is searched for the key ``NativeDependenciesAbsolutePath``,
whose value, if found, is added to the DLL-search path. If this key is not
specified in the application's config-file, then the ``HDF.PInvoke.dll`` assembly
detects the processor architecture (32- or 64-bit) of the hosting process and expects
to find the native DLLs in the ``bin32`` or ``bin64`` subdirectories, relative to its
location. For example, if ``HDF.PInvoke.dll`` lives in ``C:\bin``, it looks for
the native DLLs in ``C:\bin\bin32`` and ``C:\bin\bin64``.
Finally, the ``PATH`` environment variable of the running process is searched for other locations,
such as installed by the [HDF5 installers](https://www.hdfgroup.org/HDF5/).

# Two Major HDF5 Versions for the Price of One (Free)

The HDF Group currently maintains two major HDF5 release families, HDF5 1.8 and HDF5 1.10. The Visual Studio Solution is configured to build an `HDF.PInvoke.dll` .NET assembly for the HDF5 1.8.x API. To build a .NET assembly for the HDF5 1.10.x API the *Build* properties of the *HDF.PInvoke* and *UnitTest* projects must be modified to include the `HDF5_VER1_10` conditional compilation symbol. 
# License

HDF.PInvoke is part of [HDF5](https://www.hdfgroup.org/HDF5/). It is subject to
the *same* terms and conditions as HDF5. Please review [COPYING](COPYING) or
[http://www.hdfgroup.org/HDF5/doc/Copyright.html](http://www.hdfgroup.org/HDF5/doc/Copyright.html)
for the details. If you have any questions, please [contact us](http://www.hdfgroup.org/about/contact.html).

# Supporting HDF.PInvoke

The best way to support HDF.Pinvoke is to contribute to it either by reporting
bugs, writing documentation (e.g., the [cookbook](https://github.com/HDFGroup/HDF.PInvoke/wiki/Cookbook)),
or sending pull requests.

***

![The HDF Group logo](https://github.com/HDFGroup/HDF.PInvoke/blob/master/images/The%20HDF%20Group.jpg)
