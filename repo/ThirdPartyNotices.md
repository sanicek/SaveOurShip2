# Third-party notices

Last reviewed: 2026-10-23.

Third-party components retain their own licenses. The root CC BY-NC-SA 4.0
license does not replace the licenses below or impose its noncommercial
restriction on these independently licensed components.

## Scope and verification

The inherited file [1.1/Assemblies/0Harmony.dll](../1.1/Assemblies/0Harmony.dll)
is Harmony assembly version `2.0.2.0`. Its SHA-256 is:

```text
66af1b523b83d814a1253f7c1f2bc6b81d6a8f64dae52c0850c2aff288696680
```

This exactly matches `lib/net472/0Harmony.dll` in the published
[Lib.Harmony 2.0.2 NuGet package](https://api.nuget.org/v3-flatcontainer/lib.harmony/2.0.2/lib.harmony.2.0.2.nupkg).
The package's `LICENSE` supplies the Harmony notice reproduced below. Its
package metadata also gives `Copyright © 2016` and names Andreas Pardeike.

The [Harmony 2.0.2.0 build configuration](https://github.com/pardeike/Harmony/blob/v2.0.2.0/Harmony/Harmony.csproj)
merges `MonoMod.Common.dll`, `Mono.Cecil.dll`, `Mono.Cecil.Mdb.dll`, and
`Mono.Cecil.Pdb.dll` into .NET Framework release binaries. The bundled DLL's
metadata identifies MonoMod.Common `20.5.31.1` and Cecil `0.11.2.0`.
Their corresponding notices, including notices in Cecil's component source
headers, are retained below.

No dependency binaries were added or changed during this review. This notice
inventory covers the identified historical Harmony bundle, not an independent
rights audit of every asset, mod assembly, or dependency used by the project.
See [Provenance.md](Provenance.md) for review limitations.

## Harmony 2.0.2.0 — MIT

Source: [Harmony v2.0.2.0 LICENSE](https://github.com/pardeike/Harmony/blob/v2.0.2.0/LICENSE),
also included in the exact matching NuGet package.

```text
MIT License

Copyright (c) 2017 Andreas Pardeike

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## MonoMod.Common 20.5.31.1 — MIT

The [20.5.31.1 NuGet package](https://api.nuget.org/v3-flatcontainer/monomod.common/20.5.31.1/monomod.common.20.5.31.1.nupkg)
declares MIT, author `0x0ade`, `Copyright 2020 Maik Macho`, and source commit
`8fb58cffa6b7996b7d7da763161bcdcd4d72575e`. The
[LICENSE at that exact commit](https://github.com/MonoMod/MonoMod.Common/blob/8fb58cffa6b7996b7d7da763161bcdcd4d72575e/LICENSE)
reads:

```text
The MIT License (MIT)

Copyright (c) 2019 Maik Macho

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## Mono.Cecil 0.11.2, including Mdb and Pdb assemblies — MIT/X11

Source: [Cecil 0.11.2 LICENSE.txt](https://github.com/jbevain/cecil/blob/0.11.2/LICENSE.txt).
The assembly metadata in
[ProjectInfo.cs](https://github.com/jbevain/cecil/blob/0.11.2/ProjectInfo.cs)
also gives `Copyright © 2008 - 2018 Jb Evain`.

```text
Copyright (c) 2008 - 2015 Jb Evain
Copyright (c) 2008 - 2011 Novell, Inc.

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

### Additional Cecil component source notices — MIT/X11

The following copyright notices are retained from the corresponding source
headers in Cecil 0.11.2. The permission and disclaimer text following them
applies to these MIT/X11-licensed portions:

- [CryptoConvert.cs](https://github.com/jbevain/cecil/blob/0.11.2/Mono.Security.Cryptography/CryptoConvert.cs),
  author Sebastien Pouliot.
- [MonoSymbolFile.cs](https://github.com/jbevain/cecil/blob/0.11.2/symbols/mdb/Mono.CompilerServices.SymbolWriter/MonoSymbolFile.cs),
  authors Martin Baulig and Marek Safar; and the other symbol-writer source files,
  including [MonoSymbolTable.cs](https://github.com/jbevain/cecil/blob/0.11.2/symbols/mdb/Mono.CompilerServices.SymbolWriter/MonoSymbolTable.cs)
  and [SymbolWriterImpl.cs](https://github.com/jbevain/cecil/blob/0.11.2/symbols/mdb/Mono.CompilerServices.SymbolWriter/SymbolWriterImpl.cs).
- [ISymUnmanagedDocumentWriter.cs](https://github.com/jbevain/cecil/blob/0.11.2/symbols/pdb/Mono.Cecil.Pdb/ISymUnmanagedDocumentWriter.cs)
  and related unmanaged symbol-writer interfaces.

```text
(C) 2003 Motus Technologies Inc. (http://www.motus.com)
Copyright (C) 2004-2006 Novell Inc. (http://www.novell.com)
(C) 2003 Ximian, Inc.  http://www.ximian.com
Copyright (C) 2012 Xamarin Inc (http://www.xamarin.com)
(C) 2002 Ximian, Inc.  http://www.ximian.com
(C) 2005 Novell, Inc.  http://www.novell.com
(C) 2008 Juerg Billeter

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

### Microsoft.Cci.Pdb (included in Mono.Cecil.Pdb) — MIT

Source: [Microsoft.Cci.Pdb LICENSE in Cecil 0.11.2](https://github.com/jbevain/cecil/blob/0.11.2/symbols/pdb/Microsoft.Cci.Pdb/LICENSE).
The component's source headers also state
`Copyright (c) Microsoft. All rights reserved.`

```text
The MIT License (MIT)

Copyright (c) Microsoft

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## Other dependencies and future changes

The current `Source/1.7/RimworldMod.csproj` references `Lib.Harmony` 2.4.3,
`Krafs.Publicizer` 2.3.2, game/engine assemblies, and Vehicle Framework assemblies.
These references are separate from the historical bundled Harmony DLL above.
This document does not grant redistribution permission for those dependencies
or claim that their version-specific notice requirements have been audited.

Before adding or updating dependencies, copying source/assets, or distributing
new build artifacts, check the exact version, its license and included components,
whether material is copied or embedded, and which notices must accompany it.
Retain those notices here or in a clearly linked accompanying license file.
Do not substitute the root CC license for third-party terms or import material
with unresolved licensing. See [ForkWorkflow.md](ForkWorkflow.md).
