# 📘 Module 1: Introduction to Windows API (WinAPI)

---

## ✅ What is the Windows API?

**Windows API**, or **WinAPI**, is a set of functions provided by Microsoft that allows developers to interact directly with the **Windows operating system**.

These functions are written in **native C/C++**, and provide access to:

* System memory
* Window management
* Hardware devices
* Files and I/O
* Processes and threads
* Security, user accounts, registry
* and much more

---

## 🛠 Why Use Windows API in C#?

C# is a **managed language** running on the **.NET runtime**. Most of the time, you work with safe, high-level code. However, if you want to do **low-level or native Windows tasks**, you’ll need to use **Windows API via interop**.

---

## 🔌 What is P/Invoke (Platform Invocation Services)?

**P/Invoke** lets you call **unmanaged (native)** functions from **DLLs** like `user32.dll`, `kernel32.dll`, etc., inside your C# program.

To do this, you use:

```csharp
[DllImport("user32.dll")]
static extern int MessageBox(IntPtr hWnd, string text, string caption, uint type);
```

You're telling C#:

> "Hey! There’s a function in user32.dll called MessageBox. Let me use it."

---

## 🧠 Key Concepts

| Concept              | Description                                                                |
| -------------------- | -------------------------------------------------------------------------- |
| **DLL**              | Dynamic Link Library — where Windows API functions live                    |
| **Function Pointer** | Like a reference to a function in a DLL                                    |
| **InteropServices**  | C# namespace for dealing with interop (e.g., `DllImport`, `Marshal`, etc.) |
| **Marshaling**       | Converting data between .NET and native formats (e.g., string to `LPCSTR`) |
| **IntPtr**           | A generic type for a native pointer/handle                                 |

---

## 🏁 Getting Started Example: Hello Windows API

### 🧪 Step 1: Create a Console App

Create a new C# Console App in Visual Studio or with CLI:

```bash
dotnet new console -n WinApiDemo
cd WinApiDemo
```

### 🧪 Step 2: Add Your First Windows API Call

Edit `Program.cs`:

```csharp
using System;
using System.Runtime.InteropServices;

class Program
{
    // Import MessageBox from user32.dll
    [DllImport("user32.dll", CharSet = CharSet.Unicode)]
    static extern int MessageBox(IntPtr hWnd, string text, string caption, uint type);

    static void Main()
    {
        MessageBox(IntPtr.Zero, "Hello from Windows API!", "WinAPI C# Demo", 0);
    }
}
```

### ▶️ Run Output:

A native Windows message box will appear! 🪟

---

## 🧱 Structure of a P/Invoke Call

```csharp
[DllImport("library.dll", EntryPoint = "FunctionName", CharSet = ..., SetLastError = ...)]
return_type FunctionName(params);
```

### Example Breakdown:

```csharp
[DllImport("user32.dll", CharSet = CharSet.Unicode)]
static extern int MessageBox(IntPtr hWnd, string lpText, string lpCaption, uint uType);
```

* `user32.dll`: The DLL file where the function lives
* `MessageBox`: The native function name
* `IntPtr hWnd`: Window handle (or zero for desktop)
* `string lpText`: Message content
* `string lpCaption`: Message title
* `uint uType`: Style/type of message box

---

## ⚠️ Common Issues with P/Invoke

| Issue                        | Cause               | Fix                                           |
| ---------------------------- | ------------------- | --------------------------------------------- |
| **AccessViolationException** | Improper marshaling | Match C types correctly                       |
| **DllNotFoundException**     | Wrong DLL or path   | Ensure system DLL is correct                  |
| **BadImageFormatException**  | x86/x64 mismatch    | Match your build platform with native library |

---

## 🧪 Practice: Call Beep from kernel32.dll

```csharp
[DllImport("kernel32.dll")]
static extern bool Beep(uint frequency, uint duration);

static void Main()
{
    Beep(750, 300); // Frequency in Hz, duration in ms
}
```

---

## 🔚 Summary of Module 1

| Concept             | You Learned                          |
| ------------------- | ------------------------------------ |
| What is WinAPI      | It’s the native interface to Windows |
| Why C# Uses It      | To access low-level OS functionality |
| P/Invoke            | The bridge from C# to native DLLs    |
| DllImport           | Declares external functions in C#    |
| Your First API Call | `MessageBox` and `Beep`              |

---