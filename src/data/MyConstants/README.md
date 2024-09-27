In .NET, you can create a class library project that contains constant values, and then pack it into a NuGet package. Here's how you can do it:

1. Create a new Class Library project:

`dotnet new classlib -n MyConstants`

2. Navigate to the new project directory:

`cd MyConstants`

3. Create a new class that contains your constant values:

```
// Constants.cs
namespace MyConstants
{
    public static class Constants
    {
        public const string MyConstant = "Constant Value";
    }
}
```

4. Create a NuGet package from your project:


`dotnet pack --configuration Release`
This will create a `.nupkg` file in the bin/Release directory. You can then publish this package to a NuGet feed, or reference it directly in other projects.

To use the constant in another project, you would first add a reference to the NuGet package, and then you can access the constant like this:

`string value = MyConstants.Constants.MyConstant;`

