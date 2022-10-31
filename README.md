# msbuild-issue
Demonstrating issues with msbuild with @ in path names

This is a cut down version of the MSBuild files used by Grpc.Tools based projects
to demonstate the issue https://github.com/grpc/grpc/issues/30746

All gRPC and protobuf compiler tasks and logic have been removed and the outputs mocked
below to simplify and demonstate a possible bug in MSBuild.
Original MSBuild files are in:
https://github.com/grpc/grpc/blob/master/src/csharp/Grpc.Tools/build/_protobuf/Google.Protobuf.Tools.targets

Issue:
If a directory path contains the '@' character then the <FilesToCompile> item list
is wrong - it misses out the files with '@' in their paths.

Two 'workarounds' are included <Workaround1> and <Workaround2> - using qualified metadata.
But this adds a different behaviour to the MSBuild batching. The unqualified metadata
should work.

If the directory '@myfiles' is renamed to 'myfiles' and the mocked data in
<Protobuf_ExpectedOutputs> also edited to remove the '@' then it behaves as expected
