The ProtoValidate NuGet package allows you to define custom validation rules for your Protocol Buffers messages in .NET. However, it seems like you're missing the part where you add your Protobuf File Descriptors to the `FileDescriptors` list in the `ValidatorOptions`.

Here's how you can do it:

1. **Generate the File Descriptor from your `.proto` files:** You can use the `protoc` command-line tool with the `--descriptor_set_out` option to generate a File Descriptor Set from your `.proto` files. For example:

```bash
protoc --proto_path=. --include_imports --include_source_info --descriptor_set_out=student.protoset student.proto
```

This command generates a `student.protoset` file from `student.proto`.

2. **Load the File Descriptor Set in your code:** You can use the `FileDescriptorSet.Parser.ParseFrom` method to load the File Descriptor Set in your code. For example:

```csharp
var bytes = File.ReadAllBytes("student.protoset");
var fileDescriptorSet = FileDescriptorSet.Parser.ParseFrom(bytes);
```

3. **Add the File Descriptors to the `ValidatorOptions`:** You can add the File Descriptors from the File Descriptor Set to the `ValidatorOptions`. For example:

```csharp
validatorOptions.FileDescriptors = fileDescriptorSet.File.Select(FileDescriptor.BuildFrom).ToList();
```

Here's how your code might look after these changes:

```csharp
var bytes = File.ReadAllBytes("student.protoset");
var fileDescriptorSet = FileDescriptorSet.Parser.ParseFrom(bytes);

var validatorOptions = new ProtoValidate.ValidatorOptions() {
    DisableLazy = true,
    FileDescriptors = fileDescriptorSet.File.Select(FileDescriptor.BuildFrom).ToList()
};

var validator = new ProtoValidate.Validator(validatorOptions);
```

In this code, replace `"student.protoset"` with the path to your File Descriptor Set.

Please note that this is a general guide and might need to be adjusted based on your specific project setup and requirements.