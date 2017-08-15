---
title: C++/CX Notes
date: 2017-08-15 16:32:55
categories: Programming
---
[C++/CX](https://docs.microsoft.com/en-us/cpp/cppcx/visual-c-language-reference-c-cx) is a language extension for C++ compilers from Microsoft that enables C++ programmers to write programs for the new Windows Runtime platform.

# Extension Syntax
## Object
WinRT objects are created using `ref new` and assigned to variables declared with `^` (hat) notation inherited from C++/CLI.
```c++
Dog^ dog = ref new Dog();
```
## Class
### Runtime class
There are special kinds of *runtime class* that  may contain component extension constructs. These are simply referred to as ref classes because they are declared using `ref class`.
```c++
// dog.public.h
#pragma once
#include "dog.private.h"

public ref class Dog
{
    ...
};
```
### Partial class
The feature allows a single class to be split across multiple files. The parts are later merged at compilation. Note the keyword `partial`.
```c++
// dog.private.h
#pragma once

partial ref class Dog
{
    ...
} ;
```
## Generic
Windows Runtime and thus C++/CX supports runtime-based generics. Generic type information is contained in the metadata and instantiated at runtime, unlike C++ templates which are compile-time constructs. Both are supported by the compiler and can be combined.
```c++
generic<typename T>
public ref class Bag
{
private:
    property T item;
}
```
# Asynchronous Programming
This part describes the recommended way to consume [asynchronous methods](https://docs.microsoft.com/en-us/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps) in C++/CX by using the `task` class that's defined in the `concurrency` namespace in ppltasks.h.
The following example shows how to use the task class to consume an async method that returns an `IAsyncOperation` interface and whose operation produces a value. It also shows how to get the buffer data from an opened file.
```c++
using namespace Windows::Storage;
using namespace Windows::Storage::Pickers;

void OpenFile()
{
    FileOpenPicker^ picker = ref new FileOpenPicker();

    Concurrency::create_task(picker->PickSingleFileAsync()).then([](StorageFile^ file)
    {
        return file->OpenAsync(FileAccessMode::Read);
    }).then([](IRandomAccessStream^ stream)
    {
        Buffer^ buffer = ref new Buffer(stream->Size);
        return stream->ReadAsync(buffer, stream->Size, InputStreamOptions::None);
    }).then([](IBuffer^ buffer)
    {
        Array<unsigned char>^ array = ref new Array<unsigned char>(buffer->Length);
        CryptographicBuffer::CopyToByteArray(buffer, &array);
    });
}
```
