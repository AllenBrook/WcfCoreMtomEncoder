# WcfCoreMtomEncoder

Currently, .NET Core WCF has no build-in support MTOM.

The `MtomMessageEncoderBindingElement` allows .NET Core applications to communicate with WCF endpoints which support MTOM encoding. 

**Note:** This is _not_ a complete implementation of MTOM. It is meant as a workaround for calling existing MTOM encoded SOAP services. It consumes MTOM encoded messages, but does not perform MTOMEncoding on outbound messages. However this should be sufficent for interoperating with existing services.

[![Build status](https://ci.appveyor.com/api/projects/status/v4836gx8j9f0a8gd?svg=true)](https://ci.appveyor.com/project/lennykean/wcfcoremtomencoder)
[![NuGet](https://img.shields.io/nuget/v/WcfCoreMtomEncoder.svg)](https://www.nuget.org/packages/WcfCoreMtomEncoder/)

### Installation

#### .NET CLI
```shell
> dotnet add package WcfCoreMtomEncoder
```
#### Package Manager
```shell
PM> Install-Package WcfCoreMtomEncoder
```

## Usage

The `MtomMessageEncoderBindingElement` is meant to wrap another message encoder, usually `TextMessageEncodingBindingElement`.

### Creating a custom binding

```csharp
var encoding = new MtomMessageEncoderBindingElement(new TextMessageEncodingBindingElement());
var transport = new HttpTransportBindingElement();
var customBinding = new CustomBinding(encoding, transport);

var client = new MtomEnabledServiceClient(customBinding);
```
