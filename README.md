## Unable to try out WebView2 WPF Browser

Please help me to try `WebView2` with a simple .NET Core WPF app.

[This rero](https://github.com/noseratio/WebView2WpfBrowser) is a clone of Microsoft's [WebView2 WPF Browser](https://github.com/MicrosoftEdge/WebView2Samples/tree/master/SampleApps/WebView2WpfBrowser), as a .NET Core 3.1 WPF app and using the [`Microsoft.Web.WebView2` 0.9.579-prerelease](https://www.nuget.org/packages/Microsoft.Web.WebView2/0.9.579-prerelease), with added error handling.

To compile it (Visual Studio is **not** required):

- Download and install [Download .NET Core 3.1 SDK](https://download.visualstudio.microsoft.com/download/pr/547f9f81-599a-4b58-9322-d1d158385df6/ebe3e02fd54c29487ac32409cb20d352/dotnet-sdk-3.1.401-win-x64.exe), v3.1.401 at the time of writing this.

- Run it from the project folder:
  ```
  dotnet run
  ```

I'm get this runtime error:
  ```
  Couldn't find a compatible Edge application to host WebViews.
  ```

My Edge version:
  ```
  Microsoft Edge is up to date.
  Version 85.0.564.41 (Official build) (64-bit)
  ```

If I change the `Microsoft.Web.WebView2` package reference to the most recent [0.9.579](https://www.nuget.org/packages/Microsoft.Web.WebView2/0.9.579) (at the time of writing), I can't even compile it. In `WebView2WpfBrowser.csproj`:

```XML
<ItemGroup>
  <PackageReference Include="Microsoft.Web.WebView2" Version="0.9.579" />
</ItemGroup>
```

I'm getting these compile time errors:

```
App.xaml(18,10): error MC3074: The tag 'CoreWebView2CreationProperties' does not exist in XML namespace 'clr-namespace:Microsoft.Web.WebView2.Wpf;assembly=Microsoft.Web.WebView2.Wpf'. 

MainWindow.xaml(57,10): error MC3074: The tag 'WebView2' does not exist in XML namespace 'clr-namespace:Microsoft.Web.WebView2.Wpf;assembly=Microsoft.Web.WebView2.Wpf'. 
```

Apparently, [the NuGet package for WebView2 v0.9.579](https://www.nuget.org/packages/Microsoft.Web.WebView2/0.9.579) is missing a bunch of DLLs and the whole `lib\netcoreapp3.0` folder:

```
Microsoft.Web.WebView2.Core.dll
Microsoft.Web.WebView2.Core.xml
Microsoft.Web.WebView2.WinForms.dll
Microsoft.Web.WebView2.WinForms.xml
Microsoft.Web.WebView2.Wpf.dll
Microsoft.Web.WebView2.Wpf.xml
```