Generate artifacts from proto file

`protoc -I=. -I ./protovalidate/proto/protovalidate --csharp_out=./csharp_out ./user.proto`