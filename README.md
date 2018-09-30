Repro for Xamarin.iOS issue:

Works on the Emulator but crashes on any device.
App depends on Lib.A which depends on Lib.B. Both are strong named.
Lib.A as InternalsVisibleTo Lib.B.

Upon accessing Lib.B from the Xamarin.iOS app deployed to device, the app crashes with:

```
Unhandled Exception:
System.MethodAccessException: Method `Bla.DoNothing()' is inaccessible from method `Ble.DontThrow()'
  at (wrapper managed-to-native) System.Object.__icall_wrapper_mono_throw_method_access(intptr,intptr)
  at InternalsVisibleStrongNamed.Application.Main (System.String[] args) <0x100abb070 + 0x00023> in <e9f72ebbc6ca4ed589535b6cc146eceb#72fb15896f6c5cfbdf855a3eee9de4dc>:0 
2018-09-30 14:23:45.302 InternalsVisibleStrongNamed[387:147683] Unhandled managed exception:
Method `Bla.DoNothing()' is inaccessible from method `Ble.DontThrow()' (System.MethodAccessException)
  at (wrapper managed-to-native) System.Object.__icall_wrapper_mono_throw_method_access(intptr,intptr)
  at InternalsVisibleStrongNamed.Application.Main (System.String[] args) <0x100abb070 + 0x00023> in <e9f72ebbc6ca4ed589535b6cc146eceb#72fb15896f6c5cfbdf855a3eee9de4dc>:0 
2018-09-30 14:23:45.302 InternalsVisibleStrongNamed[387:147683] critical: Stacktrace:

2018-09-30 14:23:45.302 InternalsVisibleStrongNamed[387:147683] critical: 
Native stacktrace:

2018-09-30 14:23:45.303 InternalsVisibleStrongNamed[387:147683] critical: 	0   InternalsVisibleStrongNamed         0x0000000100c7c74c InternalsVisibleStrongNamed + 1869644
2018-09-30 14:23:45.303 InternalsVisibleStrongNamed[387:147683] critical: 	1   libsystem_platform.dylib            0x0000000181eb8b58 _sigtramp + 52
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	2   libsystem_pthread.dylib             0x0000000181ebe288 <redacted> + 376
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	3   libsystem_c.dylib                   0x0000000181c8bd0c abort + 140
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	4   InternalsVisibleStrongNamed         0x0000000100d82bf0 xamarin_get_block_descriptor + 4448
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	5   InternalsVisibleStrongNamed         0x0000000100cb90c0 InternalsVisibleStrongNamed + 2117824
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	6   InternalsVisibleStrongNamed         0x0000000100c7c398 InternalsVisibleStrongNamed + 1868696
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	7   InternalsVisibleStrongNamed         0x0000000100c7b0e8 InternalsVisibleStrongNamed + 1863912
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	8   InternalsVisibleStrongNamed         0x0000000100c73314 InternalsVisibleStrongNamed + 1831700
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	9   InternalsVisibleStrongNamed         0x0000000100b0c308 InternalsVisibleStrongNamed + 361224
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	10  InternalsVisibleStrongNamed         0x0000000100af9198 InternalsVisibleStrongNamed + 283032
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	11  InternalsVisibleStrongNamed         0x0000000100abb094 InternalsVisibleStrongNamed + 28820
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	12  InternalsVisibleStrongNamed         0x0000000100af85a8 InternalsVisibleStrongNamed + 279976
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	13  InternalsVisibleStrongNamed         0x0000000100c8ba10 InternalsVisibleStrongNamed + 1931792
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	14  InternalsVisibleStrongNamed         0x0000000100cf2094 InternalsVisibleStrongNamed + 2351252
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	15  InternalsVisibleStrongNamed         0x0000000100cf7338 InternalsVisibleStrongNamed + 2372408
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	16  InternalsVisibleStrongNamed         0x0000000100c72b28 InternalsVisibleStrongNamed + 1829672
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	17  InternalsVisibleStrongNamed         0x0000000100d88cfc xamarin_find_protocol_wrapper_type + 24688
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	18  InternalsVisibleStrongNamed         0x0000000100abaf38 InternalsVisibleStrongNamed + 28472
2018-09-30 14:23:45.304 InternalsVisibleStrongNamed[387:147683] critical: 	19  libdyld.dylib                       0x0000000181bedfc0 <redacted> + 4
2018-09-30 14:23:45.305 InternalsVisibleStrongNamed[387:147683] critical: 
=================================================================
Got a SIGABRT while executing native code. This usually indicates
a fatal error in the mono runtime or one of the native libraries 
used by your application.
=================================================================

Application 'Test.InternalsVisibleStrongNamed' terminated.
```