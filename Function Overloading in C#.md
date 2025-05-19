# មេរៀន៖ Function Overloading in C#

## ១. សេចក្តីផ្តើមអំពី Function Overloading

Function Overloading ឬ Method Overloading គឺជាលក្ខណៈពិសេសមួយនៅក្នុង C# ដែលអនុញ្ញាតឱ្យ Class មួយមាន Method ច្រើនដែលមានឈ្មោះដូចគ្នា ប៉ុន្តែមាន Parameter List ខុសគ្នា។ នេះអនុញ្ញាតឱ្យអ្នកអនុវត្តប្រតិបត្តិការស្រដៀងគ្នាជាមួយ Parameter ប្រភេទ ឬចំនួនខុសគ្នា ដែលធ្វើឱ្យកូដមានភាពងាយស្រួលអាន និងប្រើឡើងវិញ។

ចំណុចសំខាន់ៗ៖
- Method Name ដូចគ្នា ប៉ុន្តែ Signature ខុសគ្នា
- ជួយបង្កើនការរៀបចំកូដ
- ជាផ្នែកនៃ Polymorphism របស់ C#
- ត្រូវបានដោះស្រាយនៅពេល Compile-Time (Static Polymorphism)

## ២. វាក្យសម្ព័ន្ធ និងច្បាប់

### វាក្យសម្ព័ន្ធមូលដ្ឋាន
```csharp
public class Calculator
{
    public int Add(int a, int b) { return a + b; }
    public double Add(double a, double b) { return a + b; }
}
```

### ច្បាប់សម្រាប់ Function Overloading
1. **Method Name**៖ ត្រូវតែដូចគ្នា
2. **Parameter List**៖ ត្រូវខុសគ្នានៅក្នុង៖
   - ចំនួន Parameter
   - ប្រភេទ Parameter
   - លំដាប់នៃប្រភេទ Parameter
3. **Return Type**៖ មិនត្រូវបានគិតពិចារណាសម្រាប់ Overloading (មិនអាច Overload ដោយ Return Type តែមួយឡើយ)
4. **Access Modifiers**៖ មិនប៉ះពាល់ដល់ Overloading
5. **Parameter Modifiers**៖ `out`, `ref`, `params` អាចប្រើបាន និងជួយបង្កើត Signature

## ៣. ឧទាហរណ៍នៃ Function Overloading

### ឧទាហរណ៍ ១៖ ចំនួន Parameter ខុសគ្នា
```csharp
public class Printer
{
    public void Print(string message)
    {
        Console.WriteLine($"Message: {message}");
    }

    public void Print(string message, int times)
    {
        for (int i = 0; i < times; i++)
        {
            Console.WriteLine($"Message {i + 1}: {message}");
        }
    }
}
```

### ឧទាហរណ៍ ២៖ ប្រភេទ Parameter ខុសគ្នា
```csharp
public class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }

    public double Add(double a, double b)
    {
        return a + b;
    }

    public string Add(string a, string b)
    {
        return a + b;
    }
}
```

### ឧទាហរណ៍ ៣៖ លំដាប់ Parameter ខុសគ្នា
```csharp
public class Person
{
    public string GetInfo(string name, int age)
    {
        return $"Name: {name}, Age: {age}";
    }

    public string GetInfo(int age, string name)
    {
        return $"Age: {age}, Name: {name}";
    }
}
```

## ៤. ការអនុវត្តជាក់ស្តែង

នេះជាកម្មវិធីពេញលេញដែលបង្ហាញពី Function Overloading៖

```csharp
using System;

public class MathOperations
{
    // Overload 1: Two integers
    public int Multiply(int a, int b)
    {
        return a * b;
    }

    // Overload 2: Three integers
    public int Multiply(int a, int b, int c)
    {
        return a * b * c;
    }

    // Overload 3: Two doubles
    public double Multiply(double a, double b)
    {
        return a * b;
    }

    // Overload 4: Array of integers
    public int Multiply(int[] numbers)
    {
        int result = 1;
        foreach (int num in numbers)
        {
            result *= num;
        }
        return result;
    }
}

class Program
{
    static void Main()
    {
        MathOperations math = new MathOperations();
        
        // Using different overloads
        Console.WriteLine($"Two integers: {math.Multiply(2, 3)}");           // Output: 6
        Console.WriteLine($"Three integers: {math.Multiply(2, 3, 4)}");     // Output: 24
        Console.WriteLine($"Two doubles: {math.Multiply(2.5, 3.5)}");       // Output: 8.75
        Console.WriteLine($"Array: {math.Multiply(new int[] {2, 3, 4})}");  // Output: 24
    }
}
```

## ៥. ការអនុវត្តល្អបំផុត

1. **Meaningful Overloads**:
   - Overload តែ Method ដែលអនុវត្តប្រតិបត្តិការស្រដៀងគ្នា
   - រក្សាឥរិយាបថស្របគ្នាក្នុង Overload នីមួយៗ

2. **Clear Parameter Names**:
   - ប្រើឈ្មោះ Parameter ដែលពិពណ៌នាច្បាស់
   - រក្សាឈ្មោះឱ្យស្របគ្នាក្នុង Overload នីមួយៗ

3. **Avoid Ambiguity**:
   - ត្រូវប្រាកដថាប្រភេទ Parameter មានភាពខុសគ្នាគ្រប់គ្រាន់
   - ជៀសវាង Overloading ជាមួយប្រភេទ Parameter ស្រដៀងគ្នាខ្លាំង

4. **Default Parameters vs. Overloading**:
   - ពិចារណាប្រើ Default Parameters សម្រាប់ Parameter ស្រេចចិត្តសាមញ្ញ
   - ប្រើ Overloading នៅពេលដែលឥរិយាបថត្រូវខុសគ្នាយ៉ាងសំខាន់

5. **Documentation**:
   - បន្ថែម XML Comments ដើម្បីពន្យល់ Overload នីមួយៗ
   - ឯកសារពន្យល់គោលបំណង Parameter ឱ្យច្បាស់

## ៦. បញ្ហាទូទៅ

1. **Ambiguous Calls**:
```csharp
// Problematic overloads
public void Process(double value) { }
public void Process(float value) { }

// Ambiguous call
Process(5); // Compiler error: ambiguous call
```

2. **Return Type Confusion**:
```csharp
// Invalid: Cannot overload by return type alone
public int GetValue() { return 1; }
public string GetValue() { return "1"; } // Error
```

3. **Complex Overloads**:
   - Overload ច្រើនពេកអាចធ្វើឱ្យកូដពិបាកថែទាំ
   - ពិចារណាប្រើ Pattern ផ្សេង (ឧ. Builder Pattern) សម្រាប់ករណីស្មុគស្មាញ

## ៧. ប្រធានបទកម្រិតខ្ពស់

### Parameter Modifiers ក្នុង Overloading
```csharp
public class DataProcessor
{
    public void Process(int value)
    {
        Console.WriteLine($"Value: {value}");
    }

    public void Process(ref int value)
    {
        value *= 2;
        Console.WriteLine($"Doubled value: {value}");
    }

    public void Process(out int value)
    {
        value = 100;
        Console.WriteLine($"Initialized value: {value}");
    }
}
```

### Overloading ជាមួយ Generics
```csharp
public class GenericProcessor
{
    public void Process<T>(T value)
    {
        Console.WriteLine($"Generic value: {value}");
    }

    public void Process<T>(T value, int count)
    {
        Console.WriteLine($"Generic value {value} repeated {count} times");
    }
}
```

## ៨. លំហាត់

1. បង្កើត Class `Shape` ដែលមាន Method `CalculateArea` ដែល Overload សម្រាប់រូបរាងផ្សេងៗ (រង្វង់, ចតុកោណ, ត្រីកោណ)។
2. អនុវត្ត Class `StringFormatter` ដែលមាន Method `Format` ដែល Overload ដើម្បីគ្រប់គ្រងប្រភេទ Input ផ្សេងៗ។
3. បង្កើត Class `Logger` ដែលមាន Method `Log` ដែល Overload ដើម្បីគាំទ្រកម្រិត Logging និងប្រភេទសារ។

## ៩. សេចក្តីសន្និដ្ឋាន

Function Overloading គឺជាលក្ខណៈពិសេសដ៏មានឥទ្ធិពលនៅក្នុង C# ដែល៖
- ធ្វើឱ្យកូដងាយស្រួលអាន
- បង្កើនភាពបត់បែននៃ Method
- គាំទ្រ Polymorphic Behavior
- ទាមទារការរចនាដោយប្រុងប្រយ័ត្នដើម្បីជៀសវាង Ambiguity

តាមរយៈការអនុវត្តតាមច្បាប់ និងការអនុវត្តល្អបំផុត អ្នកអាចបង្កើតកូដដែលស្អាត និងថែទាំបានយ៉ាងមានប្រសិទ្ធភាពដោយប្រើ Function Overloading។