﻿### OCaml Compatibility Library for F# ###
(FSharpx.Compatibility.OCaml)

## Design / Implementation Notes ##

-	Some modules are already implemented in the F# PowerPack (under the
	FSharp.PowerPack.Compatibility namespace). However, not all of these modules
	are completed so they should be compared to the OCaml documentation to
	determined what functions, if any, still need to be implemented.

-	The GC and Weak modules can be implemented using the System.GC type and
	the System.Diagnostics.Process / System.Diagnostics.ProcessInfo types.
-	The Lazy module can be easily re-implemented using F#'s 'lazy' keyword.
-	The Thread module should be able to be re-implemented using the
	System.Threading.Thread type (or the System.Diagnostics.ProcessThread type).
-	The Str module can be implemented using System.Text.RegularExpression.
-	The Unix, UnixLabels, and ThreadUnix modules can be implemented in a
	separate library, and built on top of the Mono.Unix / Mono.Posix libraries.
-	The Nativeint module should be trivial to re-implement using the built-in F#
	'nativeint' type. Note that most of the functions defined by the OCaml
	module translate into constants or single IL OpCodes when written in F#.
-	The Sys module can be implemented using System.Environment, System.Diagnostics.Process,
	System.IO.File, System.IO.Directory.
	-	The signal-handling functions and constants are only relevant on
		Unix-based systems, so the re-implemented module should probably go in
		the separate library that'll also contain the Unix module; this way the
		signal-handling functions can be implemented using the Mono.Unix library.
-	The Random module can be implemented using System.Random.
-	The Digest library can be implemented using System.Security.Cryptography.MD5
	(preferably MD5Cng, but that requires .NET 3.5 or later, so if we support
	.NET 2.0 use MD5CryptoServiceProvider).
-	The Complex module can be implemented using the System.Numerics.Complex type.
-	The Array, Char, List, and String modules should be easy to implement -- most
	of their functions have direct equivalents in IL or the F# core library.
-	The Arg module can be implemented using the Arg module from the F# PowerPack
	(and the code from the F# PowerPack may already serve as a drop-in replacement).
-	The Big_int module can be implemented using the F# bigint type (an alias for
	System.Numerics.BigInteger).
-	The Buffer module can be implemented using System.Text.StringBuilder.
-	The Hashtbl module can be implemented based on System.Collections.Generic.Dictionary.
-	It should be possible to implement the Graphics module in a fairly
	straightforward way using System.Windows.Forms and System.Drawing.
	With some extra effort, it may also be possible to implement it on top of WPF.
	-	It may also be possible (and useful) to implement the Tk module in the
		same way, as it's normally used to provide a higher-level API for designing
		GUI applications. Also look at implementing the interface exposed by
		liblablgtk-ocaml.
-	The Stack module is quite simple and could easily be implemented on top of
	the System.Collections.Generic.Stack type.
-	The Format module needs to be re-implemented from scratch using the documentation
	available on the OCaml website.
