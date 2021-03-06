# .NET Standard 2.1 vs. 2.0

[Overview](netstandard2.1.md) | [Previous](netstandard2.0_diff.md)

```diff
 namespace System {
     public class AggregateException : Exception {
+        public override string Message { get; }
     }
     public sealed class AppDomain : MarshalByRefObject {
-        public new Type GetType();
-        public override object InitializeLifetimeService();
     }
-    public class ArgumentException : SystemException, ISerializable {
+    public class ArgumentException : SystemException {
     }
-    public class ArgumentOutOfRangeException : ArgumentException, ISerializable {
+    public class ArgumentOutOfRangeException : ArgumentException {
     }
     public abstract class Array : ICloneable, ICollection, IEnumerable, IList, IStructuralComparable, IStructuralEquatable {
+        public static void Fill<T>(T[] array, T value);
+        public static void Fill<T>(T[] array, T value, int startIndex, int count);
+        public static void Reverse<T>(T[] array);
+        public static void Reverse<T>(T[] array, int index, int length);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ArraySegment<T> : ICollection<T>, IEnumerable, IEnumerable<T>, IList<T>, IReadOnlyCollection<T>, IReadOnlyList<T> {
+    public readonly struct ArraySegment<T> : ICollection<T>, IEnumerable, IEnumerable<T>, IList<T>, IReadOnlyCollection<T>, IReadOnlyList<T> {
+        public struct Enumerator : IDisposable, IEnumerator, IEnumerator<T> {
+            public T Current { get; }
+            object System.Collections.IEnumerator.Current { get; }
+            public void Dispose();
+            public bool MoveNext();
+            void System.Collections.IEnumerator.Reset();
+        }
+        public static ArraySegment<T> Empty { get; }
+        public T this[int index] { get; set; }
+        public void CopyTo(ArraySegment<T> destination);
+        public void CopyTo(T[] destination);
+        public void CopyTo(T[] destination, int destinationIndex);
+        public ArraySegment<T>.Enumerator GetEnumerator();
+        public static implicit operator ArraySegment<T> (T[] array);
+        public ArraySegment<T> Slice(int index);
+        public ArraySegment<T> Slice(int index, int count);
-        void System.Collections.Generic.ICollection<T>.CopyTo(T[] array, int arrayIndex);
+        public T[] ToArray();
     }
     public static class BitConverter {
+        public static float Int32BitsToSingle(int value);
+        public static int SingleToInt32Bits(float value);
+        public static bool ToBoolean(ReadOnlySpan<byte> value);
+        public static char ToChar(ReadOnlySpan<byte> value);
+        public static double ToDouble(ReadOnlySpan<byte> value);
+        public static short ToInt16(ReadOnlySpan<byte> value);
+        public static int ToInt32(ReadOnlySpan<byte> value);
+        public static long ToInt64(ReadOnlySpan<byte> value);
+        public static float ToSingle(ReadOnlySpan<byte> value);
+        public static ushort ToUInt16(ReadOnlySpan<byte> value);
+        public static uint ToUInt32(ReadOnlySpan<byte> value);
+        public static ulong ToUInt64(ReadOnlySpan<byte> value);
+        public static bool TryWriteBytes(Span<byte> destination, char value);
+        public static bool TryWriteBytes(Span<byte> destination, short value);
+        public static bool TryWriteBytes(Span<byte> destination, int value);
+        public static bool TryWriteBytes(Span<byte> destination, long value);
+        public static bool TryWriteBytes(Span<byte> destination, double value);
+        public static bool TryWriteBytes(Span<byte> destination, float value);
+        public static bool TryWriteBytes(Span<byte> destination, ushort value);
+        public static bool TryWriteBytes(Span<byte> destination, uint value);
+        public static bool TryWriteBytes(Span<byte> destination, ulong value);
+        public static bool TryWriteBytes(Span<byte> destination, bool value);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Boolean : IComparable, IComparable<bool>, IConvertible, IEquatable<bool> {
+    public struct Boolean : IComparable, IComparable<bool>, IConvertible, IEquatable<bool> {
+        public static Boolean Parse(ReadOnlySpan<char> value);
+        public Boolean TryFormat(Span<char> destination, out int charsWritten);
+        public static Boolean TryParse(ReadOnlySpan<char> value, out Boolean result);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Byte : IComparable, IComparable<byte>, IConvertible, IEquatable<byte>, IFormattable {
+    public struct Byte : IComparable, IComparable<byte>, IConvertible, IEquatable<byte>, IFormattable {
+        public static Byte Parse(ReadOnlySpan<char> s, NumberStyles style = (NumberStyles)(7), IFormatProvider provider = null);
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider provider = null);
+        public static bool TryParse(ReadOnlySpan<char> s, out Byte result);
+        public static bool TryParse(ReadOnlySpan<char> s, NumberStyles style, IFormatProvider provider, out Byte result);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Char : IComparable, IComparable<char>, IConvertible, IEquatable<char> {
+    public struct Char : IComparable, IComparable<char>, IConvertible, IEquatable<char> {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ConsoleKeyInfo {
+    public readonly struct ConsoleKeyInfo {
     }
     public static class Convert {
+        public static string ToBase64String(ReadOnlySpan<byte> bytes, Base64FormattingOptions options = (Base64FormattingOptions)(0));
+        public static bool TryFromBase64Chars(ReadOnlySpan<char> chars, Span<byte> bytes, out int bytesWritten);
+        public static bool TryFromBase64String(string s, Span<byte> bytes, out int bytesWritten);
+        public static bool TryToBase64Chars(ReadOnlySpan<byte> bytes, Span<char> chars, out int charsWritten, Base64FormattingOptions options = (Base64FormattingOptions)(0));
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential, Size=1)]
-    public struct DateTime : IComparable, IComparable<DateTime>, IConvertible, IEquatable<DateTime>, IFormattable, ISerializable {
+    public readonly struct DateTime : IComparable, IComparable<DateTime>, IConvertible, IEquatable<DateTime>, IFormattable, ISerializable {
+        public static readonly DateTime UnixEpoch;
+        public static DateTime Parse(ReadOnlySpan<char> s, IFormatProvider provider = null, DateTimeStyles styles = (DateTimeStyles)(0));
+        public static DateTime ParseExact(ReadOnlySpan<char> s, string[] formats, IFormatProvider provider, DateTimeStyles style = (DateTimeStyles)(0));
+        public static DateTime ParseExact(ReadOnlySpan<char> s, ReadOnlySpan<char> format, IFormatProvider provider, DateTimeStyles style = (DateTimeStyles)(0));
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider provider = null);
+        public static bool TryParse(ReadOnlySpan<char> s, out DateTime result);
+        public static bool TryParse(ReadOnlySpan<char> s, IFormatProvider provider, DateTimeStyles styles, out DateTime result);
+        public static bool TryParseExact(ReadOnlySpan<char> s, string[] formats, IFormatProvider provider, DateTimeStyles style, out DateTime result);
+        public static bool TryParseExact(ReadOnlySpan<char> s, ReadOnlySpan<char> format, IFormatProvider provider, DateTimeStyles style, out DateTime result);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential, Size=1)]
-    public struct DateTimeOffset : IComparable, IComparable<DateTimeOffset>, IDeserializationCallback, IEquatable<DateTimeOffset>, IFormattable, ISerializable {
+    public struct DateTimeOffset : IComparable, IComparable<DateTimeOffset>, IDeserializationCallback, IEquatable<DateTimeOffset>, IFormattable, ISerializable {
+        public static readonly DateTimeOffset UnixEpoch;
+        public static DateTimeOffset Parse(ReadOnlySpan<char> input, IFormatProvider formatProvider = null, DateTimeStyles styles = (DateTimeStyles)(0));
+        public static DateTimeOffset ParseExact(ReadOnlySpan<char> input, string[] formats, IFormatProvider formatProvider, DateTimeStyles styles = (DateTimeStyles)(0));
+        public static DateTimeOffset ParseExact(ReadOnlySpan<char> input, ReadOnlySpan<char> format, IFormatProvider formatProvider, DateTimeStyles styles = (DateTimeStyles)(0));
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider formatProvider = null);
+        public static bool TryParse(ReadOnlySpan<char> input, out DateTimeOffset result);
+        public static bool TryParse(ReadOnlySpan<char> input, IFormatProvider formatProvider, DateTimeStyles styles, out DateTimeOffset result);
+        public static bool TryParseExact(ReadOnlySpan<char> input, string[] formats, IFormatProvider formatProvider, DateTimeStyles styles, out DateTimeOffset result);
+        public static bool TryParseExact(ReadOnlySpan<char> input, ReadOnlySpan<char> format, IFormatProvider formatProvider, DateTimeStyles styles, out DateTimeOffset result);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Decimal : IComparable, IComparable<decimal>, IConvertible, IDeserializationCallback, IEquatable<decimal>, IFormattable {
+    public struct Decimal : IComparable, IComparable<decimal>, IConvertible, IDeserializationCallback, IEquatable<decimal>, IFormattable {
+        public static Decimal Parse(ReadOnlySpan<char> s, NumberStyles style = (NumberStyles)(111), IFormatProvider provider = null);
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider provider = null);
+        public static bool TryParse(ReadOnlySpan<char> s, out Decimal result);
+        public static bool TryParse(ReadOnlySpan<char> s, NumberStyles style, IFormatProvider provider, out Decimal result);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Double : IComparable, IComparable<double>, IConvertible, IEquatable<double>, IFormattable {
+    public struct Double : IComparable, IComparable<double>, IConvertible, IEquatable<double>, IFormattable {
+        public static bool IsFinite(Double d);
+        public static bool IsNegative(Double d);
+        public static bool IsNormal(Double d);
+        public static bool IsSubnormal(Double d);
+        public static Double Parse(ReadOnlySpan<char> s, NumberStyles style = (NumberStyles)(231), IFormatProvider provider = null);
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider provider = null);
+        public static bool TryParse(ReadOnlySpan<char> s, out Double result);
+        public static bool TryParse(ReadOnlySpan<char> s, NumberStyles style, IFormatProvider provider, out Double result);
     }
     public abstract class Enum : ValueType, IComparable, IConvertible, IFormattable {
+        public static TEnum Parse<TEnum>(string value) where TEnum : struct;
+        public static TEnum Parse<TEnum>(string value, bool ignoreCase) where TEnum : struct;
+        public static bool TryParse(Type enumType, string value, bool ignoreCase, out object result);
+        public static bool TryParse(Type enumType, string value, out object result);
     }
     public static class GC {
+        public static long GetAllocatedBytesForCurrentThread();
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Guid : IComparable, IComparable<Guid>, IEquatable<Guid>, IFormattable {
+    public struct Guid : IComparable, IComparable<Guid>, IEquatable<Guid>, IFormattable {
+        public Guid(ReadOnlySpan<byte> b);
+        public static Guid Parse(ReadOnlySpan<char> input);
+        public static Guid ParseExact(ReadOnlySpan<char> input, ReadOnlySpan<char> format);
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>));
+        public static bool TryParse(ReadOnlySpan<char> input, out Guid result);
+        public static bool TryParseExact(ReadOnlySpan<char> input, ReadOnlySpan<char> format, out Guid result);
+        public bool TryWriteBytes(Span<byte> destination);
     }
+    public struct HashCode {
+        public void Add<T>(T value);
+        public void Add<T>(T value, IEqualityComparer<T> comparer);
+        public static int Combine<T1>(T1 value1);
+        public static int Combine<T1, T2>(T1 value1, T2 value2);
+        public static int Combine<T1, T2, T3>(T1 value1, T2 value2, T3 value3);
+        public static int Combine<T1, T2, T3, T4>(T1 value1, T2 value2, T3 value3, T4 value4);
+        public static int Combine<T1, T2, T3, T4, T5>(T1 value1, T2 value2, T3 value3, T4 value4, T5 value5);
+        public static int Combine<T1, T2, T3, T4, T5, T6>(T1 value1, T2 value2, T3 value3, T4 value4, T5 value5, T6 value6);
+        public static int Combine<T1, T2, T3, T4, T5, T6, T7>(T1 value1, T2 value2, T3 value3, T4 value4, T5 value5, T6 value6, T7 value7);
+        public static int Combine<T1, T2, T3, T4, T5, T6, T7, T8>(T1 value1, T2 value2, T3 value3, T4 value4, T5 value5, T6 value6, T7 value7, T8 value8);
+        public override bool Equals(object obj);
+        public override int GetHashCode();
+        public int ToHashCode();
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Int16 : IComparable, IComparable<short>, IConvertible, IEquatable<short>, IFormattable {
+    public struct Int16 : IComparable, IComparable<short>, IConvertible, IEquatable<short>, IFormattable {
+        public static Int16 Parse(ReadOnlySpan<char> s, NumberStyles style = (NumberStyles)(7), IFormatProvider provider = null);
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider provider = null);
+        public static bool TryParse(ReadOnlySpan<char> s, out Int16 result);
+        public static bool TryParse(ReadOnlySpan<char> s, NumberStyles style, IFormatProvider provider, out Int16 result);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Int32 : IComparable, IComparable<int>, IConvertible, IEquatable<int>, IFormattable {
+    public struct Int32 : IComparable, IComparable<int>, IConvertible, IEquatable<int>, IFormattable {
+        public static Int32 Parse(ReadOnlySpan<char> s, NumberStyles style = (NumberStyles)(7), IFormatProvider provider = null);
+        public bool TryFormat(Span<char> destination, out Int32 charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider provider = null);
+        public static bool TryParse(ReadOnlySpan<char> s, out Int32 result);
+        public static bool TryParse(ReadOnlySpan<char> s, NumberStyles style, IFormatProvider provider, out Int32 result);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Int64 : IComparable, IComparable<long>, IConvertible, IEquatable<long>, IFormattable {
+    public struct Int64 : IComparable, IComparable<long>, IConvertible, IEquatable<long>, IFormattable {
+        public static Int64 Parse(ReadOnlySpan<char> s, NumberStyles style = (NumberStyles)(7), IFormatProvider provider = null);
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider provider = null);
+        public static bool TryParse(ReadOnlySpan<char> s, out Int64 result);
+        public static bool TryParse(ReadOnlySpan<char> s, NumberStyles style, IFormatProvider provider, out Int64 result);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct IntPtr : ISerializable {
+    public struct IntPtr : IEquatable<IntPtr>, ISerializable {
+        bool System.IEquatable<System.IntPtr>.Equals(IntPtr other);
     }
     public class Lazy<T> {
+        public Lazy(T value);
     }
     public static class Math {
+        public static double Acosh(double d);
+        public static double Asinh(double d);
+        public static double Atanh(double d);
+        public static double Cbrt(double d);
+        public static byte Clamp(byte value, byte min, byte max);
+        public static decimal Clamp(decimal value, decimal min, decimal max);
+        public static double Clamp(double value, double min, double max);
+        public static short Clamp(short value, short min, short max);
+        public static int Clamp(int value, int min, int max);
+        public static long Clamp(long value, long min, long max);
+        public static sbyte Clamp(sbyte value, sbyte min, sbyte max);
+        public static float Clamp(float value, float min, float max);
+        public static ushort Clamp(ushort value, ushort min, ushort max);
+        public static uint Clamp(uint value, uint min, uint max);
+        public static ulong Clamp(ulong value, ulong min, ulong max);
     }
+    public static class MathF {
+        public const float E = 2.71828175f;
+        public const float PI = 3.14159274f;
+        public static float Abs(float x);
+        public static float Acos(float x);
+        public static float Acosh(float x);
+        public static float Asin(float x);
+        public static float Asinh(float x);
+        public static float Atan(float x);
+        public static float Atan2(float y, float x);
+        public static float Atanh(float x);
+        public static float Cbrt(float x);
+        public static float Ceiling(float x);
+        public static float Cos(float x);
+        public static float Cosh(float x);
+        public static float Exp(float x);
+        public static float Floor(float x);
+        public static float IEEERemainder(float x, float y);
+        public static float Log(float x);
+        public static float Log(float x, float y);
+        public static float Log10(float x);
+        public static float Max(float x, float y);
+        public static float Min(float x, float y);
+        public static float Pow(float x, float y);
+        public static float Round(float x);
+        public static float Round(float x, int digits);
+        public static float Round(float x, int digits, MidpointRounding mode);
+        public static float Round(float x, MidpointRounding mode);
+        public static int Sign(float x);
+        public static float Sin(float x);
+        public static float Sinh(float x);
+        public static float Sqrt(float x);
+        public static float Tan(float x);
+        public static float Tanh(float x);
+        public static float Truncate(float x);
+    }
+    public readonly struct Memory<T> {
+        public Memory(T[] array);
+        public Memory(T[] array, int start, int length);
+        public static Memory<T> Empty { get; }
+        public bool IsEmpty { get; }
+        public int Length { get; }
+        public Span<T> Span { get; }
+        public void CopyTo(Memory<T> destination);
+        public bool Equals(Memory<T> other);
+        public override bool Equals(object obj);
+        public override int GetHashCode();
+        public static implicit operator Memory<T> (ArraySegment<T> segment);
+        public static implicit operator ReadOnlyMemory<T> (Memory<T> memory);
+        public static implicit operator Memory<T> (T[] array);
+        public MemoryHandle Pin();
+        public Memory<T> Slice(int start);
+        public Memory<T> Slice(int start, int length);
+        public T[] ToArray();
+        public override string ToString();
+        public bool TryCopyTo(Memory<T> destination);
+    }
+    public static class MemoryExtensions {
+        public static Memory<T> AsMemory<T>(this T[] array);
+        public static Memory<T> AsMemory<T>(this T[] array, int start);
+        public static Memory<T> AsMemory<T>(this ArraySegment<T> segment);
+        public static Memory<T> AsMemory<T>(this T[] array, int start, int length);
+        public static Memory<T> AsMemory<T>(this ArraySegment<T> segment, int start);
+        public static Memory<T> AsMemory<T>(this ArraySegment<T> segment, int start, int length);
+        public static ReadOnlyMemory<char> AsMemory(this string text);
+        public static ReadOnlyMemory<char> AsMemory(this string text, int start);
+        public static ReadOnlyMemory<char> AsMemory(this string text, int start, int length);
+        public static Span<T> AsSpan<T>(this T[] array);
+        public static Span<T> AsSpan<T>(this T[] array, int start);
+        public static Span<T> AsSpan<T>(this ArraySegment<T> segment);
+        public static Span<T> AsSpan<T>(this T[] array, int start, int length);
+        public static Span<T> AsSpan<T>(this ArraySegment<T> segment, int start);
+        public static Span<T> AsSpan<T>(this ArraySegment<T> segment, int start, int length);
+        public static ReadOnlySpan<char> AsSpan(this string text);
+        public static ReadOnlySpan<char> AsSpan(this string text, int start);
+        public static ReadOnlySpan<char> AsSpan(this string text, int start, int length);
+        public static int BinarySearch<T>(this Span<T> span, IComparable<T> comparable);
+        public static int BinarySearch<T>(this ReadOnlySpan<T> span, IComparable<T> comparable);
+        public static int BinarySearch<T, TComparer>(this Span<T> span, T value, TComparer comparer) where TComparer : IComparer<T>;
+        public static int BinarySearch<T, TComparable>(this Span<T> span, TComparable comparable) where TComparable : IComparable<T>;
+        public static int BinarySearch<T, TComparer>(this ReadOnlySpan<T> span, T value, TComparer comparer) where TComparer : IComparer<T>;
+        public static int BinarySearch<T, TComparable>(this ReadOnlySpan<T> span, TComparable comparable) where TComparable : IComparable<T>;
+        public static int CompareTo(this ReadOnlySpan<char> span, ReadOnlySpan<char> other, StringComparison comparisonType);
+        public static bool Contains(this ReadOnlySpan<char> span, ReadOnlySpan<char> value, StringComparison comparisonType);
+        public static void CopyTo<T>(this T[] source, Span<T> destination);
+        public static void CopyTo<T>(this T[] source, Memory<T> destination);
+        public static bool EndsWith<T>(this Span<T> span, ReadOnlySpan<T> value) where T : IEquatable<T>;
+        public static bool EndsWith<T>(this ReadOnlySpan<T> span, ReadOnlySpan<T> value) where T : IEquatable<T>;
+        public static bool EndsWith(this ReadOnlySpan<char> span, ReadOnlySpan<char> value, StringComparison comparisonType);
+        public static bool Equals(this ReadOnlySpan<char> span, ReadOnlySpan<char> other, StringComparison comparisonType);
+        public static int IndexOf<T>(this Span<T> span, T value) where T : IEquatable<T>;
+        public static int IndexOf<T>(this ReadOnlySpan<T> span, T value) where T : IEquatable<T>;
+        public static int IndexOf<T>(this Span<T> span, ReadOnlySpan<T> value) where T : IEquatable<T>;
+        public static int IndexOf<T>(this ReadOnlySpan<T> span, ReadOnlySpan<T> value) where T : IEquatable<T>;
+        public static int IndexOf(this ReadOnlySpan<char> span, ReadOnlySpan<char> value, StringComparison comparisonType);
+        public static int IndexOfAny<T>(this Span<T> span, T value0, T value1) where T : IEquatable<T>;
+        public static int IndexOfAny<T>(this Span<T> span, T value0, T value1, T value2) where T : IEquatable<T>;
+        public static int IndexOfAny<T>(this ReadOnlySpan<T> span, T value0, T value1) where T : IEquatable<T>;
+        public static int IndexOfAny<T>(this ReadOnlySpan<T> span, T value0, T value1, T value2) where T : IEquatable<T>;
+        public static int IndexOfAny<T>(this Span<T> span, ReadOnlySpan<T> values) where T : IEquatable<T>;
+        public static int IndexOfAny<T>(this ReadOnlySpan<T> span, ReadOnlySpan<T> values) where T : IEquatable<T>;
+        public static bool IsWhiteSpace(this ReadOnlySpan<char> span);
+        public static int LastIndexOf<T>(this Span<T> span, T value) where T : IEquatable<T>;
+        public static int LastIndexOf<T>(this ReadOnlySpan<T> span, T value) where T : IEquatable<T>;
+        public static int LastIndexOf<T>(this Span<T> span, ReadOnlySpan<T> value) where T : IEquatable<T>;
+        public static int LastIndexOf<T>(this ReadOnlySpan<T> span, ReadOnlySpan<T> value) where T : IEquatable<T>;
+        public static int LastIndexOfAny<T>(this Span<T> span, T value0, T value1) where T : IEquatable<T>;
+        public static int LastIndexOfAny<T>(this Span<T> span, T value0, T value1, T value2) where T : IEquatable<T>;
+        public static int LastIndexOfAny<T>(this ReadOnlySpan<T> span, T value0, T value1) where T : IEquatable<T>;
+        public static int LastIndexOfAny<T>(this ReadOnlySpan<T> span, T value0, T value1, T value2) where T : IEquatable<T>;
+        public static int LastIndexOfAny<T>(this Span<T> span, ReadOnlySpan<T> values) where T : IEquatable<T>;
+        public static int LastIndexOfAny<T>(this ReadOnlySpan<T> span, ReadOnlySpan<T> values) where T : IEquatable<T>;
+        public static bool Overlaps<T>(this Span<T> span, ReadOnlySpan<T> other);
+        public static bool Overlaps<T>(this Span<T> span, ReadOnlySpan<T> other, out int elementOffset);
+        public static bool Overlaps<T>(this ReadOnlySpan<T> span, ReadOnlySpan<T> other);
+        public static bool Overlaps<T>(this ReadOnlySpan<T> span, ReadOnlySpan<T> other, out int elementOffset);
+        public static void Reverse<T>(this Span<T> span);
+        public static int SequenceCompareTo<T>(this Span<T> span, ReadOnlySpan<T> other) where T : IComparable<T>;
+        public static int SequenceCompareTo<T>(this ReadOnlySpan<T> span, ReadOnlySpan<T> other) where T : IComparable<T>;
+        public static bool SequenceEqual<T>(this Span<T> span, ReadOnlySpan<T> other) where T : IEquatable<T>;
+        public static bool SequenceEqual<T>(this ReadOnlySpan<T> span, ReadOnlySpan<T> other) where T : IEquatable<T>;
+        public static bool StartsWith<T>(this Span<T> span, ReadOnlySpan<T> value) where T : IEquatable<T>;
+        public static bool StartsWith<T>(this ReadOnlySpan<T> span, ReadOnlySpan<T> value) where T : IEquatable<T>;
+        public static bool StartsWith(this ReadOnlySpan<char> span, ReadOnlySpan<char> value, StringComparison comparisonType);
+        public static int ToLower(this ReadOnlySpan<char> source, Span<char> destination, CultureInfo culture);
+        public static int ToLowerInvariant(this ReadOnlySpan<char> source, Span<char> destination);
+        public static int ToUpper(this ReadOnlySpan<char> source, Span<char> destination, CultureInfo culture);
+        public static int ToUpperInvariant(this ReadOnlySpan<char> source, Span<char> destination);
+        public static ReadOnlySpan<char> Trim(this ReadOnlySpan<char> span);
+        public static ReadOnlySpan<char> Trim(this ReadOnlySpan<char> span, char trimChar);
+        public static ReadOnlySpan<char> Trim(this ReadOnlySpan<char> span, ReadOnlySpan<char> trimChars);
+        public static ReadOnlySpan<char> TrimEnd(this ReadOnlySpan<char> span);
+        public static ReadOnlySpan<char> TrimEnd(this ReadOnlySpan<char> span, char trimChar);
+        public static ReadOnlySpan<char> TrimEnd(this ReadOnlySpan<char> span, ReadOnlySpan<char> trimChars);
+        public static ReadOnlySpan<char> TrimStart(this ReadOnlySpan<char> span);
+        public static ReadOnlySpan<char> TrimStart(this ReadOnlySpan<char> span, char trimChar);
+        public static ReadOnlySpan<char> TrimStart(this ReadOnlySpan<char> span, ReadOnlySpan<char> trimChars);
+    }
-    public class MissingMethodException : MissingMemberException, ISerializable {
+    public class MissingMethodException : MissingMemberException {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ModuleHandle {
+    public struct ModuleHandle {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Nullable<T> where T : struct {
+    public struct Nullable<T> where T : struct {
     }
     public class Random {
+        public virtual void NextBytes(Span<byte> buffer);
     }
+    public readonly struct ReadOnlyMemory<T> {
+        public ReadOnlyMemory(T[] array);
+        public ReadOnlyMemory(T[] array, int start, int length);
+        public static ReadOnlyMemory<T> Empty { get; }
+        public bool IsEmpty { get; }
+        public int Length { get; }
+        public ReadOnlySpan<T> Span { get; }
+        public void CopyTo(Memory<T> destination);
+        public override bool Equals(object obj);
+        public bool Equals(ReadOnlyMemory<T> other);
+        public override int GetHashCode();
+        public static implicit operator ReadOnlyMemory<T> (ArraySegment<T> segment);
+        public static implicit operator ReadOnlyMemory<T> (T[] array);
+        public MemoryHandle Pin();
+        public ReadOnlyMemory<T> Slice(int start);
+        public ReadOnlyMemory<T> Slice(int start, int length);
+        public T[] ToArray();
+        public override string ToString();
+        public bool TryCopyTo(Memory<T> destination);
+    }
+    public readonly ref struct ReadOnlySpan<T> {
+        public ref struct Enumerator {
+            public ref readonly T Current { get; }
+            public bool MoveNext();
+        }
+        public ReadOnlySpan(T[] array);
+        public ReadOnlySpan(T[] array, int start, int length);
+        public unsafe ReadOnlySpan(void* pointer, int length);
+        public static ReadOnlySpan<T> Empty { get; }
+        public bool IsEmpty { get; }
+        public ref readonly T this[int index] { get; }
+        public int Length { get; }
+        public void CopyTo(Span<T> destination);
+        public override bool Equals(object obj);
+        public ReadOnlySpan<T>.Enumerator GetEnumerator();
+        public override int GetHashCode();
+        public ref readonly T GetPinnableReference();
+        public static bool operator ==(ReadOnlySpan<T> left, ReadOnlySpan<T> right);
+        public static implicit operator ReadOnlySpan<T> (ArraySegment<T> segment);
+        public static implicit operator ReadOnlySpan<T> (T[] array);
+        public static bool operator !=(ReadOnlySpan<T> left, ReadOnlySpan<T> right);
+        public ReadOnlySpan<T> Slice(int start);
+        public ReadOnlySpan<T> Slice(int start, int length);
+        public T[] ToArray();
+        public override string ToString();
+        public bool TryCopyTo(Span<T> destination);
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct RuntimeArgumentHandle
+    public ref struct RuntimeArgumentHandle
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct RuntimeFieldHandle : ISerializable {
+    public struct RuntimeFieldHandle : ISerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct RuntimeMethodHandle : ISerializable {
+    public struct RuntimeMethodHandle : ISerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct RuntimeTypeHandle : ISerializable {
+    public struct RuntimeTypeHandle : ISerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SByte : IComparable, IComparable<sbyte>, IConvertible, IEquatable<sbyte>, IFormattable {
+    public struct SByte : IComparable, IComparable<sbyte>, IConvertible, IEquatable<sbyte>, IFormattable {
+        public static SByte Parse(ReadOnlySpan<char> s, NumberStyles style = (NumberStyles)(7), IFormatProvider provider = null);
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider provider = null);
+        public static bool TryParse(ReadOnlySpan<char> s, out SByte result);
+        public static bool TryParse(ReadOnlySpan<char> s, NumberStyles style, IFormatProvider provider, out SByte result);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Single : IComparable, IComparable<float>, IConvertible, IEquatable<float>, IFormattable {
+    public struct Single : IComparable, IComparable<float>, IConvertible, IEquatable<float>, IFormattable {
+        public static bool IsFinite(Single f);
+        public static bool IsNegative(Single f);
+        public static bool IsNormal(Single f);
+        public static bool IsSubnormal(Single f);
+        public static Single Parse(ReadOnlySpan<char> s, NumberStyles style = (NumberStyles)(231), IFormatProvider provider = null);
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider provider = null);
+        public static bool TryParse(ReadOnlySpan<char> s, out Single result);
+        public static bool TryParse(ReadOnlySpan<char> s, NumberStyles style, IFormatProvider provider, out Single result);
     }
+    public readonly ref struct Span<T> {
+        public ref struct Enumerator {
+            public ref T Current { get; }
+            public bool MoveNext();
+        }
+        public Span(T[] array);
+        public Span(T[] array, int start, int length);
+        public unsafe Span(void* pointer, int length);
+        public static Span<T> Empty { get; }
+        public bool IsEmpty { get; }
+        public ref T this[int index] { get; }
+        public int Length { get; }
+        public void Clear();
+        public void CopyTo(Span<T> destination);
+        public override bool Equals(object obj);
+        public void Fill(T value);
+        public Span<T>.Enumerator GetEnumerator();
+        public override int GetHashCode();
+        public ref T GetPinnableReference();
+        public static bool operator ==(Span<T> left, Span<T> right);
+        public static implicit operator Span<T> (ArraySegment<T> segment);
+        public static implicit operator ReadOnlySpan<T> (Span<T> span);
+        public static implicit operator Span<T> (T[] array);
+        public static bool operator !=(Span<T> left, Span<T> right);
+        public Span<T> Slice(int start);
+        public Span<T> Slice(int start, int length);
+        public T[] ToArray();
+        public override string ToString();
+        public bool TryCopyTo(Span<T> destination);
+    }
     public sealed class String : ICloneable, IComparable, IComparable<string>, IConvertible, IEnumerable, IEnumerable<char>, IEquatable<string> {
+        public String(ReadOnlySpan<char> value);
+        public bool Contains(char value);
+        public bool Contains(char value, StringComparison comparisonType);
+        public bool Contains(String value, StringComparison comparisonType);
+        public static String Create<TState>(int length, TState state, SpanAction<char, TState> action);
+        public bool EndsWith(char value);
+        public int GetHashCode(StringComparison comparisonType);
+        public int IndexOf(char value, StringComparison comparisonType);
+        public static String Join<T>(char separator, IEnumerable<T> values);
+        public static String Join(char separator, params object[] values);
+        public static String Join(char separator, params string[] value);
+        public static String Join(char separator, string[] value, int startIndex, int count);
+        public static implicit operator ReadOnlySpan<char> (String value);
+        public String Replace(String oldValue, String newValue, bool ignoreCase, CultureInfo culture);
+        public String Replace(String oldValue, String newValue, StringComparison comparisonType);
+        public string[] Split(char separator, int count, StringSplitOptions options = (StringSplitOptions)(0));
+        public string[] Split(char separator, StringSplitOptions options = (StringSplitOptions)(0));
+        public string[] Split(String separator, int count, StringSplitOptions options = (StringSplitOptions)(0));
+        public string[] Split(String separator, StringSplitOptions options = (StringSplitOptions)(0));
+        public bool StartsWith(char value);
+        public String Trim(char trimChar);
+        public String TrimEnd();
+        public String TrimEnd(char trimChar);
+        public String TrimStart();
+        public String TrimStart(char trimChar);
     }
     public abstract class StringComparer : IComparer, IComparer<string>, IEqualityComparer, IEqualityComparer<string> {
+        public static StringComparer Create(CultureInfo culture, CompareOptions options);
+        public static StringComparer FromComparison(StringComparison comparisonType);
+        bool System.Collections.IEqualityComparer.Equals(object x, object y);
+        int System.Collections.IEqualityComparer.GetHashCode(object obj);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct TimeSpan : IComparable, IComparable<TimeSpan>, IEquatable<TimeSpan>, IFormattable {
+    public struct TimeSpan : IComparable, IComparable<TimeSpan>, IEquatable<TimeSpan>, IFormattable {
+        public TimeSpan Divide(double divisor);
+        public double Divide(TimeSpan ts);
+        public TimeSpan Multiply(double factor);
+        public static TimeSpan operator /(TimeSpan timeSpan, double divisor);
+        public static double operator /(TimeSpan t1, TimeSpan t2);
+        public static TimeSpan operator *(double factor, TimeSpan timeSpan);
+        public static TimeSpan operator *(TimeSpan timeSpan, double factor);
+        public static TimeSpan Parse(ReadOnlySpan<char> input, IFormatProvider formatProvider = null);
+        public static TimeSpan ParseExact(ReadOnlySpan<char> input, string[] formats, IFormatProvider formatProvider, TimeSpanStyles styles = (TimeSpanStyles)(0));
+        public static TimeSpan ParseExact(ReadOnlySpan<char> input, ReadOnlySpan<char> format, IFormatProvider formatProvider, TimeSpanStyles styles = (TimeSpanStyles)(0));
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider formatProvider = null);
+        public static bool TryParse(ReadOnlySpan<char> s, out TimeSpan result);
+        public static bool TryParse(ReadOnlySpan<char> input, IFormatProvider formatProvider, out TimeSpan result);
+        public static bool TryParseExact(ReadOnlySpan<char> input, string[] formats, IFormatProvider formatProvider, out TimeSpan result);
+        public static bool TryParseExact(ReadOnlySpan<char> input, ReadOnlySpan<char> format, IFormatProvider formatProvider, out TimeSpan result);
+        public static bool TryParseExact(ReadOnlySpan<char> input, string[] formats, IFormatProvider formatProvider, TimeSpanStyles styles, out TimeSpan result);
+        public static bool TryParseExact(ReadOnlySpan<char> input, ReadOnlySpan<char> format, IFormatProvider formatProvider, TimeSpanStyles styles, out TimeSpan result);
     }
     public sealed class TimeZoneInfo : IDeserializationCallback, IEquatable<TimeZoneInfo>, ISerializable {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-        public struct TransitionTime : IDeserializationCallback, IEquatable<TimeZoneInfo.TransitionTime>, ISerializable {
+        public readonly struct TransitionTime : IDeserializationCallback, IEquatable<TimeZoneInfo.TransitionTime>, ISerializable {
         }
     }
-    public class Tuple<T1> : IComparable, IStructuralComparable, IStructuralEquatable {
+    public class Tuple<T1> : IComparable, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    public class Tuple<T1, T2> : IComparable, IStructuralComparable, IStructuralEquatable {
+    public class Tuple<T1, T2> : IComparable, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    public class Tuple<T1, T2, T3> : IComparable, IStructuralComparable, IStructuralEquatable {
+    public class Tuple<T1, T2, T3> : IComparable, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    public class Tuple<T1, T2, T3, T4> : IComparable, IStructuralComparable, IStructuralEquatable {
+    public class Tuple<T1, T2, T3, T4> : IComparable, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    public class Tuple<T1, T2, T3, T4, T5> : IComparable, IStructuralComparable, IStructuralEquatable {
+    public class Tuple<T1, T2, T3, T4, T5> : IComparable, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    public class Tuple<T1, T2, T3, T4, T5, T6> : IComparable, IStructuralComparable, IStructuralEquatable {
+    public class Tuple<T1, T2, T3, T4, T5, T6> : IComparable, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    public class Tuple<T1, T2, T3, T4, T5, T6, T7> : IComparable, IStructuralComparable, IStructuralEquatable {
+    public class Tuple<T1, T2, T3, T4, T5, T6, T7> : IComparable, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    public class Tuple<T1, T2, T3, T4, T5, T6, T7, TRest> : IComparable, IStructuralComparable, IStructuralEquatable {
+    public class Tuple<T1, T2, T3, T4, T5, T6, T7, TRest> : IComparable, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
     public abstract class Type : MemberInfo, IReflect {
+        public virtual bool IsByRefLike { get; }
+        public virtual bool IsGenericMethodParameter { get; }
+        public virtual bool IsGenericTypeParameter { get; }
+        public virtual bool IsSignatureType { get; }
+        public virtual bool IsSZArray { get; }
+        public virtual bool IsTypeDefinition { get; }
+        public virtual bool IsVariableBoundArray { get; }
+        public MethodInfo GetMethod(string name, int genericParameterCount, BindingFlags bindingAttr, Binder binder, CallingConventions callConvention, Type[] types, ParameterModifier[] modifiers);
+        public MethodInfo GetMethod(string name, int genericParameterCount, BindingFlags bindingAttr, Binder binder, Type[] types, ParameterModifier[] modifiers);
+        public MethodInfo GetMethod(string name, int genericParameterCount, Type[] types);
+        public MethodInfo GetMethod(string name, int genericParameterCount, Type[] types, ParameterModifier[] modifiers);
+        protected virtual MethodInfo GetMethodImpl(string name, int genericParameterCount, BindingFlags bindingAttr, Binder binder, CallingConventions callConvention, Type[] types, ParameterModifier[] modifiers);
+        public static Type MakeGenericMethodParameter(int position);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct TypedReference {
+    public ref struct TypedReference {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct UInt16 : IComparable, IComparable<ushort>, IConvertible, IEquatable<ushort>, IFormattable {
+    public struct UInt16 : IComparable, IComparable<ushort>, IConvertible, IEquatable<ushort>, IFormattable {
+        public static UInt16 Parse(ReadOnlySpan<char> s, NumberStyles style = (NumberStyles)(7), IFormatProvider provider = null);
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider provider = null);
+        public static bool TryParse(ReadOnlySpan<char> s, out UInt16 result);
+        public static bool TryParse(ReadOnlySpan<char> s, NumberStyles style, IFormatProvider provider, out UInt16 result);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct UInt32 : IComparable, IComparable<uint>, IConvertible, IEquatable<uint>, IFormattable {
+    public struct UInt32 : IComparable, IComparable<uint>, IConvertible, IEquatable<uint>, IFormattable {
+        public static UInt32 Parse(ReadOnlySpan<char> s, NumberStyles style = (NumberStyles)(7), IFormatProvider provider = null);
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider provider = null);
+        public static bool TryParse(ReadOnlySpan<char> s, out UInt32 result);
+        public static bool TryParse(ReadOnlySpan<char> s, NumberStyles style, IFormatProvider provider, out UInt32 result);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct UInt64 : IComparable, IComparable<ulong>, IConvertible, IEquatable<ulong>, IFormattable {
+    public struct UInt64 : IComparable, IComparable<ulong>, IConvertible, IEquatable<ulong>, IFormattable {
+        public static UInt64 Parse(ReadOnlySpan<char> s, NumberStyles style = (NumberStyles)(7), IFormatProvider provider = null);
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider provider = null);
+        public static bool TryParse(ReadOnlySpan<char> s, out UInt64 result);
+        public static bool TryParse(ReadOnlySpan<char> s, NumberStyles style, IFormatProvider provider, out UInt64 result);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct UIntPtr : ISerializable {
+    public struct UIntPtr : IEquatable<UIntPtr>, ISerializable {
+        bool System.IEquatable<System.UIntPtr>.Equals(UIntPtr other);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential, Size=1)]
-    public struct ValueTuple : IComparable, IComparable<ValueTuple>, IEquatable<ValueTuple>, IStructuralComparable, IStructuralEquatable {
+    public struct ValueTuple : IComparable, IComparable<ValueTuple>, IEquatable<ValueTuple>, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ValueTuple<T1> : IComparable, IComparable<ValueTuple<T1>>, IEquatable<ValueTuple<T1>>, IStructuralComparable, IStructuralEquatable {
+    public struct ValueTuple<T1> : IComparable, IComparable<ValueTuple<T1>>, IEquatable<ValueTuple<T1>>, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ValueTuple<T1, T2> : IComparable, IComparable<ValueTuple<T1, T2>>, IEquatable<ValueTuple<T1, T2>>, IStructuralComparable, IStructuralEquatable {
+    public struct ValueTuple<T1, T2> : IComparable, IComparable<ValueTuple<T1, T2>>, IEquatable<ValueTuple<T1, T2>>, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ValueTuple<T1, T2, T3> : IComparable, IComparable<ValueTuple<T1, T2, T3>>, IEquatable<ValueTuple<T1, T2, T3>>, IStructuralComparable, IStructuralEquatable {
+    public struct ValueTuple<T1, T2, T3> : IComparable, IComparable<ValueTuple<T1, T2, T3>>, IEquatable<ValueTuple<T1, T2, T3>>, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ValueTuple<T1, T2, T3, T4> : IComparable, IComparable<ValueTuple<T1, T2, T3, T4>>, IEquatable<ValueTuple<T1, T2, T3, T4>>, IStructuralComparable, IStructuralEquatable {
+    public struct ValueTuple<T1, T2, T3, T4> : IComparable, IComparable<ValueTuple<T1, T2, T3, T4>>, IEquatable<ValueTuple<T1, T2, T3, T4>>, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ValueTuple<T1, T2, T3, T4, T5> : IComparable, IComparable<ValueTuple<T1, T2, T3, T4, T5>>, IEquatable<ValueTuple<T1, T2, T3, T4, T5>>, IStructuralComparable, IStructuralEquatable {
+    public struct ValueTuple<T1, T2, T3, T4, T5> : IComparable, IComparable<ValueTuple<T1, T2, T3, T4, T5>>, IEquatable<ValueTuple<T1, T2, T3, T4, T5>>, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ValueTuple<T1, T2, T3, T4, T5, T6> : IComparable, IComparable<ValueTuple<T1, T2, T3, T4, T5, T6>>, IEquatable<ValueTuple<T1, T2, T3, T4, T5, T6>>, IStructuralComparable, IStructuralEquatable {
+    public struct ValueTuple<T1, T2, T3, T4, T5, T6> : IComparable, IComparable<ValueTuple<T1, T2, T3, T4, T5, T6>>, IEquatable<ValueTuple<T1, T2, T3, T4, T5, T6>>, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ValueTuple<T1, T2, T3, T4, T5, T6, T7> : IComparable, IComparable<ValueTuple<T1, T2, T3, T4, T5, T6, T7>>, IEquatable<ValueTuple<T1, T2, T3, T4, T5, T6, T7>>, IStructuralComparable, IStructuralEquatable {
+    public struct ValueTuple<T1, T2, T3, T4, T5, T6, T7> : IComparable, IComparable<ValueTuple<T1, T2, T3, T4, T5, T6, T7>>, IEquatable<ValueTuple<T1, T2, T3, T4, T5, T6, T7>>, IStructuralComparable, IStructuralEquatable, ITuple {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ValueTuple<T1, T2, T3, T4, T5, T6, T7, TRest> : IComparable, IComparable<ValueTuple<T1, T2, T3, T4, T5, T6, T7, TRest>>, IEquatable<ValueTuple<T1, T2, T3, T4, T5, T6, T7, TRest>>, IStructuralComparable, IStructuralEquatable where TRest : struct {
+    public struct ValueTuple<T1, T2, T3, T4, T5, T6, T7, TRest> : IComparable, IComparable<ValueTuple<T1, T2, T3, T4, T5, T6, T7, TRest>>, IEquatable<ValueTuple<T1, T2, T3, T4, T5, T6, T7, TRest>>, IStructuralComparable, IStructuralEquatable, ITuple where TRest : struct {
+        object System.Runtime.CompilerServices.ITuple.this[int index] { get; }
+        int System.Runtime.CompilerServices.ITuple.Length { get; }
     }
     public sealed class Version : ICloneable, IComparable, IComparable<Version>, IEquatable<Version> {
+        public static Version Parse(ReadOnlySpan<char> input);
+        public bool TryFormat(Span<char> destination, out int charsWritten);
+        public bool TryFormat(Span<char> destination, int fieldCount, out int charsWritten);
+        public static bool TryParse(ReadOnlySpan<char> input, out Version result);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential, Size=1)]
-    public struct Void
+    public struct Void
 }
+namespace System.Buffers {
+    public abstract class ArrayPool<T> {
+        protected ArrayPool();
+        public static ArrayPool<T> Shared { get; }
+        public static ArrayPool<T> Create();
+        public static ArrayPool<T> Create(int maxArrayLength, int maxArraysPerBucket);
+        public abstract T[] Rent(int minimumLength);
+        public abstract void Return(T[] array, bool clearArray = false);
+    }
+    public static class BuffersExtensions {
+        public static void Write<T>(this IBufferWriter<T> writer, ReadOnlySpan<T> value);
+    }
+    public interface IBufferWriter<T> {
+        void Advance(int count);
+        Memory<T> GetMemory(int sizeHint = 0);
+        Span<T> GetSpan(int sizeHint = 0);
+    }
+    public interface IMemoryOwner<T> : IDisposable {
+        Memory<T> Memory { get; }
+    }
+    public interface IPinnable {
+        MemoryHandle Pin(int elementIndex);
+        void Unpin();
+    }
+    public struct MemoryHandle : IDisposable {
+        public unsafe MemoryHandle(void* pointer, GCHandle handle = default(GCHandle), IPinnable pinnable = null);
+        public unsafe void* Pointer { get; }
+        public void Dispose();
+    }
+    public abstract class MemoryManager<T> : IDisposable, IMemoryOwner<T>, IPinnable {
+        protected MemoryManager();
+        public virtual Memory<T> Memory { get; }
+        protected Memory<T> CreateMemory(int length);
+        protected Memory<T> CreateMemory(int start, int length);
+        protected abstract void Dispose(bool disposing);
+        public abstract Span<T> GetSpan();
+        public abstract MemoryHandle Pin(int elementIndex = 0);
+        void System.IDisposable.Dispose();
+        protected internal virtual bool TryGetArray(out ArraySegment<T> segment);
+        public abstract void Unpin();
+    }
+    public abstract class MemoryPool<T> : IDisposable {
+        protected MemoryPool();
+        public abstract int MaxBufferSize { get; }
+        public static MemoryPool<T> Shared { get; }
+        public void Dispose();
+        protected abstract void Dispose(bool disposing);
+        public abstract IMemoryOwner<T> Rent(int minBufferSize = -1);
+    }
+    public enum OperationStatus {
+        DestinationTooSmall = 1,
+        Done = 0,
+        InvalidData = 3,
+        NeedMoreData = 2,
+    }
+    public delegate void ReadOnlySpanAction<T, in TArg>(ReadOnlySpan<T> span, TArg arg); {
+        public ReadOnlySpanAction(object @object, IntPtr method);
+        public virtual IAsyncResult BeginInvoke(ReadOnlySpan<T> span, TArg arg, AsyncCallback callback, object @object);
+        public virtual void EndInvoke(IAsyncResult result);
+        public virtual void Invoke(ReadOnlySpan<T> span, TArg arg);
+    }
+    public delegate void SpanAction<T, in TArg>(Span<T> span, TArg arg); {
+        public SpanAction(object @object, IntPtr method);
+        public virtual IAsyncResult BeginInvoke(Span<T> span, TArg arg, AsyncCallback callback, object @object);
+        public virtual void EndInvoke(IAsyncResult result);
+        public virtual void Invoke(Span<T> span, TArg arg);
+    }
+    public readonly struct StandardFormat : IEquatable<StandardFormat> {
+        public const byte MaxPrecision = (byte)99;
+        public const byte NoPrecision = (byte)255;
+        public StandardFormat(char symbol, byte precision = (byte)255);
+        public bool HasPrecision { get; }
+        public bool IsDefault { get; }
+        public byte Precision { get; }
+        public char Symbol { get; }
+        public override bool Equals(object obj);
+        public bool Equals(StandardFormat other);
+        public override int GetHashCode();
+        public static bool operator ==(StandardFormat left, StandardFormat right);
+        public static implicit operator StandardFormat (char symbol);
+        public static bool operator !=(StandardFormat left, StandardFormat right);
+        public static StandardFormat Parse(ReadOnlySpan<char> format);
+        public static StandardFormat Parse(string format);
+        public override string ToString();
+    }
+}
+namespace System.Buffers.Binary {
+    public static class BinaryPrimitives {
+        public static short ReadInt16BigEndian(ReadOnlySpan<byte> source);
+        public static short ReadInt16LittleEndian(ReadOnlySpan<byte> source);
+        public static int ReadInt32BigEndian(ReadOnlySpan<byte> source);
+        public static int ReadInt32LittleEndian(ReadOnlySpan<byte> source);
+        public static long ReadInt64BigEndian(ReadOnlySpan<byte> source);
+        public static long ReadInt64LittleEndian(ReadOnlySpan<byte> source);
+        public static ushort ReadUInt16BigEndian(ReadOnlySpan<byte> source);
+        public static ushort ReadUInt16LittleEndian(ReadOnlySpan<byte> source);
+        public static uint ReadUInt32BigEndian(ReadOnlySpan<byte> source);
+        public static uint ReadUInt32LittleEndian(ReadOnlySpan<byte> source);
+        public static ulong ReadUInt64BigEndian(ReadOnlySpan<byte> source);
+        public static ulong ReadUInt64LittleEndian(ReadOnlySpan<byte> source);
+        public static byte ReverseEndianness(byte value);
+        public static short ReverseEndianness(short value);
+        public static int ReverseEndianness(int value);
+        public static long ReverseEndianness(long value);
+        public static sbyte ReverseEndianness(sbyte value);
+        public static ushort ReverseEndianness(ushort value);
+        public static uint ReverseEndianness(uint value);
+        public static ulong ReverseEndianness(ulong value);
+        public static bool TryReadInt16BigEndian(ReadOnlySpan<byte> source, out short value);
+        public static bool TryReadInt16LittleEndian(ReadOnlySpan<byte> source, out short value);
+        public static bool TryReadInt32BigEndian(ReadOnlySpan<byte> source, out int value);
+        public static bool TryReadInt32LittleEndian(ReadOnlySpan<byte> source, out int value);
+        public static bool TryReadInt64BigEndian(ReadOnlySpan<byte> source, out long value);
+        public static bool TryReadInt64LittleEndian(ReadOnlySpan<byte> source, out long value);
+        public static bool TryReadUInt16BigEndian(ReadOnlySpan<byte> source, out ushort value);
+        public static bool TryReadUInt16LittleEndian(ReadOnlySpan<byte> source, out ushort value);
+        public static bool TryReadUInt32BigEndian(ReadOnlySpan<byte> source, out uint value);
+        public static bool TryReadUInt32LittleEndian(ReadOnlySpan<byte> source, out uint value);
+        public static bool TryReadUInt64BigEndian(ReadOnlySpan<byte> source, out ulong value);
+        public static bool TryReadUInt64LittleEndian(ReadOnlySpan<byte> source, out ulong value);
+        public static bool TryWriteInt16BigEndian(Span<byte> destination, short value);
+        public static bool TryWriteInt16LittleEndian(Span<byte> destination, short value);
+        public static bool TryWriteInt32BigEndian(Span<byte> destination, int value);
+        public static bool TryWriteInt32LittleEndian(Span<byte> destination, int value);
+        public static bool TryWriteInt64BigEndian(Span<byte> destination, long value);
+        public static bool TryWriteInt64LittleEndian(Span<byte> destination, long value);
+        public static bool TryWriteUInt16BigEndian(Span<byte> destination, ushort value);
+        public static bool TryWriteUInt16LittleEndian(Span<byte> destination, ushort value);
+        public static bool TryWriteUInt32BigEndian(Span<byte> destination, uint value);
+        public static bool TryWriteUInt32LittleEndian(Span<byte> destination, uint value);
+        public static bool TryWriteUInt64BigEndian(Span<byte> destination, ulong value);
+        public static bool TryWriteUInt64LittleEndian(Span<byte> destination, ulong value);
+        public static void WriteInt16BigEndian(Span<byte> destination, short value);
+        public static void WriteInt16LittleEndian(Span<byte> destination, short value);
+        public static void WriteInt32BigEndian(Span<byte> destination, int value);
+        public static void WriteInt32LittleEndian(Span<byte> destination, int value);
+        public static void WriteInt64BigEndian(Span<byte> destination, long value);
+        public static void WriteInt64LittleEndian(Span<byte> destination, long value);
+        public static void WriteUInt16BigEndian(Span<byte> destination, ushort value);
+        public static void WriteUInt16LittleEndian(Span<byte> destination, ushort value);
+        public static void WriteUInt32BigEndian(Span<byte> destination, uint value);
+        public static void WriteUInt32LittleEndian(Span<byte> destination, uint value);
+        public static void WriteUInt64BigEndian(Span<byte> destination, ulong value);
+        public static void WriteUInt64LittleEndian(Span<byte> destination, ulong value);
+    }
+}
+namespace System.Buffers.Text {
+    public static class Base64 {
+        public static OperationStatus DecodeFromUtf8(ReadOnlySpan<byte> utf8, Span<byte> bytes, out int bytesConsumed, out int bytesWritten, bool isFinalBlock = true);
+        public static OperationStatus DecodeFromUtf8InPlace(Span<byte> buffer, out int bytesWritten);
+        public static OperationStatus EncodeToUtf8(ReadOnlySpan<byte> bytes, Span<byte> utf8, out int bytesConsumed, out int bytesWritten, bool isFinalBlock = true);
+        public static OperationStatus EncodeToUtf8InPlace(Span<byte> buffer, int dataLength, out int bytesWritten);
+        public static int GetMaxDecodedFromUtf8Length(int length);
+        public static int GetMaxEncodedToUtf8Length(int length);
+    }
+    public static class Utf8Formatter {
+        public static bool TryFormat(bool value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(byte value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(DateTime value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(DateTimeOffset value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(decimal value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(double value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(Guid value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(short value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(int value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(long value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(sbyte value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(float value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(TimeSpan value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(ushort value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(uint value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+        public static bool TryFormat(ulong value, Span<byte> destination, out int bytesWritten, StandardFormat format = default(StandardFormat));
+    }
+    public static class Utf8Parser {
+        public static bool TryParse(ReadOnlySpan<byte> source, out byte value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out Guid value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out short value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out int value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out long value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out sbyte value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out double value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out float value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out ushort value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out uint value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out ulong value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out bool value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out decimal value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out DateTime value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out TimeSpan value, out int bytesConsumed, char standardFormat = '\0');
+        public static bool TryParse(ReadOnlySpan<byte> source, out DateTimeOffset value, out int bytesConsumed, char standardFormat = '\0');
+    }
+}
 namespace System.Collections {
     public sealed class BitArray : ICloneable, ICollection, IEnumerable {
+        public BitArray LeftShift(int count);
+        public BitArray RightShift(int count);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct DictionaryEntry {
+    public struct DictionaryEntry {
+        public void Deconstruct(out object key, out object value);
     }
 }
 namespace System.Collections.Concurrent {
     public class ConcurrentBag<T> : ICollection, IEnumerable, IEnumerable<T>, IProducerConsumerCollection<T>, IReadOnlyCollection<T> {
+        public void Clear();
     }
     public class ConcurrentDictionary<TKey, TValue> : ICollection, ICollection<KeyValuePair<TKey, TValue>>, IDictionary, IDictionary<TKey, TValue>, IEnumerable, IEnumerable<KeyValuePair<TKey, TValue>>, IReadOnlyCollection<KeyValuePair<TKey, TValue>>, IReadOnlyDictionary<TKey, TValue> {
+        public TValue AddOrUpdate<TArg>(TKey key, Func<TKey, TArg, TValue> addValueFactory, Func<TKey, TValue, TArg, TValue> updateValueFactory, TArg factoryArgument);
+        public TValue GetOrAdd<TArg>(TKey key, Func<TKey, TArg, TValue> valueFactory, TArg factoryArgument);
     }
     public class ConcurrentQueue<T> : ICollection, IEnumerable, IEnumerable<T>, IProducerConsumerCollection<T>, IReadOnlyCollection<T> {
+        public void Clear();
     }
 }
 namespace System.Collections.Generic {
+    public static class CollectionExtensions {
+        public static TValue GetValueOrDefault<TKey, TValue>(this IReadOnlyDictionary<TKey, TValue> dictionary, TKey key);
+        public static TValue GetValueOrDefault<TKey, TValue>(this IReadOnlyDictionary<TKey, TValue> dictionary, TKey key, TValue defaultValue);
+        public static bool Remove<TKey, TValue>(this IDictionary<TKey, TValue> dictionary, TKey key, out TValue value);
+        public static bool TryAdd<TKey, TValue>(this IDictionary<TKey, TValue> dictionary, TKey key, TValue value);
+    }
     public class Dictionary<TKey, TValue> : ICollection, ICollection<KeyValuePair<TKey, TValue>>, IDeserializationCallback, IDictionary, IDictionary<TKey, TValue>, IEnumerable, IEnumerable<KeyValuePair<TKey, TValue>>, IReadOnlyCollection<KeyValuePair<TKey, TValue>>, IReadOnlyDictionary<TKey, TValue>, ISerializable {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-        public struct Enumerator : IDictionaryEnumerator, IDisposable, IEnumerator, IEnumerator<KeyValuePair<TKey, TValue>> {
+        public struct Enumerator : IDictionaryEnumerator, IDisposable, IEnumerator, IEnumerator<KeyValuePair<TKey, TValue>> {
         }
         public sealed class KeyCollection : ICollection, ICollection<TKey>, IEnumerable, IEnumerable<TKey>, IReadOnlyCollection<TKey> {
-            [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-            public struct Enumerator : IDisposable, IEnumerator, IEnumerator<TKey> {
+            public struct Enumerator : IDisposable, IEnumerator, IEnumerator<TKey> {
             }
         }
         public sealed class ValueCollection : ICollection, ICollection<TValue>, IEnumerable, IEnumerable<TValue>, IReadOnlyCollection<TValue> {
-            [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-            public struct Enumerator : IDisposable, IEnumerator, IEnumerator<TValue> {
+            public struct Enumerator : IDisposable, IEnumerator, IEnumerator<TValue> {
             }
         }
+        public Dictionary(IEnumerable<KeyValuePair<TKey, TValue>> collection);
+        public Dictionary(IEnumerable<KeyValuePair<TKey, TValue>> collection, IEqualityComparer<TKey> comparer);
+        public int EnsureCapacity(int capacity);
+        public bool Remove(TKey key, out TValue value);
+        public void TrimExcess();
+        public void TrimExcess(int capacity);
+        public bool TryAdd(TKey key, TValue value);
     }
     public class HashSet<T> : ICollection<T>, IDeserializationCallback, IEnumerable, IEnumerable<T>, IReadOnlyCollection<T>, ISerializable, ISet<T> {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-        public struct Enumerator : IDisposable, IEnumerator, IEnumerator<T> {
+        public struct Enumerator : IDisposable, IEnumerator, IEnumerator<T> {
         }
+        public HashSet(int capacity);
+        public HashSet(int capacity, IEqualityComparer<T> comparer);
+        public int EnsureCapacity(int capacity);
+        public bool TryGetValue(T equalValue, out T actualValue);
     }
-    public class KeyNotFoundException : SystemException, ISerializable {
+    public class KeyNotFoundException : SystemException {
     }
+    public static class KeyValuePair {
+        public static KeyValuePair<TKey, TValue> Create<TKey, TValue>(TKey key, TValue value);
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct KeyValuePair<TKey, TValue> {
+    public readonly struct KeyValuePair<TKey, TValue> {
+        public void Deconstruct(out TKey key, out TValue value);
     }
     public class LinkedList<T> : ICollection, ICollection<T>, IDeserializationCallback, IEnumerable, IEnumerable<T>, IReadOnlyCollection<T>, ISerializable {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-        public struct Enumerator : IDeserializationCallback, IDisposable, IEnumerator, IEnumerator<T>, ISerializable {
+        public struct Enumerator : IDeserializationCallback, IDisposable, IEnumerator, IEnumerator<T>, ISerializable {
         }
     }
     public class List<T> : ICollection, ICollection<T>, IEnumerable, IEnumerable<T>, IList, IList<T>, IReadOnlyCollection<T>, IReadOnlyList<T> {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-        public struct Enumerator : IDisposable, IEnumerator, IEnumerator<T> {
+        public struct Enumerator : IDisposable, IEnumerator, IEnumerator<T> {
         }
     }
     public class Queue<T> : ICollection, IEnumerable, IEnumerable<T>, IReadOnlyCollection<T> {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-        public struct Enumerator : IDisposable, IEnumerator, IEnumerator<T> {
+        public struct Enumerator : IDisposable, IEnumerator, IEnumerator<T> {
         }
+        public bool TryDequeue(out T result);
+        public bool TryPeek(out T result);
     }
     public class SortedDictionary<TKey, TValue> : ICollection, ICollection<KeyValuePair<TKey, TValue>>, IDictionary, IDictionary<TKey, TValue>, IEnumerable, IEnumerable<KeyValuePair<TKey, TValue>>, IReadOnlyCollection<KeyValuePair<TKey, TValue>>, IReadOnlyDictionary<TKey, TValue> {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-        public struct Enumerator : IDictionaryEnumerator, IDisposable, IEnumerator, IEnumerator<KeyValuePair<TKey, TValue>> {
+        public struct Enumerator : IDictionaryEnumerator, IDisposable, IEnumerator, IEnumerator<KeyValuePair<TKey, TValue>> {
         }
         public sealed class KeyCollection : ICollection, ICollection<TKey>, IEnumerable, IEnumerable<TKey>, IReadOnlyCollection<TKey> {
-            [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-            public struct Enumerator : IDisposable, IEnumerator, IEnumerator<TKey> {
+            public struct Enumerator : IDisposable, IEnumerator, IEnumerator<TKey> {
             }
         }
         public sealed class ValueCollection : ICollection, ICollection<TValue>, IEnumerable, IEnumerable<TValue>, IReadOnlyCollection<TValue> {
-            [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-            public struct Enumerator : IDisposable, IEnumerator, IEnumerator<TValue> {
+            public struct Enumerator : IDisposable, IEnumerator, IEnumerator<TValue> {
             }
         }
     }
     public class SortedSet<T> : ICollection, ICollection<T>, IDeserializationCallback, IEnumerable, IEnumerable<T>, IReadOnlyCollection<T>, ISerializable, ISet<T> {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-        public struct Enumerator : IDeserializationCallback, IDisposable, IEnumerator, IEnumerator<T>, ISerializable {
+        public struct Enumerator : IDeserializationCallback, IDisposable, IEnumerator, IEnumerator<T>, ISerializable {
         }
+        public bool TryGetValue(T equalValue, out T actualValue);
     }
     public class Stack<T> : ICollection, IEnumerable, IEnumerable<T>, IReadOnlyCollection<T> {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-        public struct Enumerator : IDisposable, IEnumerator, IEnumerator<T> {
+        public struct Enumerator : IDisposable, IEnumerator, IEnumerator<T> {
         }
+        public bool TryPeek(out T result);
+        public bool TryPop(out T result);
     }
 }
 namespace System.Collections.ObjectModel {
     public abstract class KeyedCollection<TKey, TItem> : Collection<TItem> {
+        public bool TryGetValue(TKey key, out TItem item);
     }
 }
 namespace System.Collections.Specialized {
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct BitVector32 {
+    public struct BitVector32 {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-        public struct Section {
+        public readonly struct Section {
         }
     }
 }
 namespace System.ComponentModel {
     public abstract class BaseNumberConverter : TypeConverter {
-        public override bool CanConvertTo(ITypeDescriptorContext context, Type t);
+        public override bool CanConvertTo(ITypeDescriptorContext context, Type destinationType);
     }
     public class DefaultValueAttribute : Attribute {
+        public DefaultValueAttribute(sbyte value);
+        public DefaultValueAttribute(ushort value);
+        public DefaultValueAttribute(uint value);
+        public DefaultValueAttribute(ulong value);
     }
 }
 namespace System.ComponentModel.Design.Serialization {
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct MemberRelationship {
+    public readonly struct MemberRelationship {
     }
 }
 namespace System.Data {
     public sealed class DBConcurrencyException : SystemException {
-        public override void GetObjectData(SerializationInfo si, StreamingContext context);
+        public override void GetObjectData(SerializationInfo info, StreamingContext context);
     }
 }
 namespace System.Data.Common {
+    public static class DbProviderFactories {
+        public static DbProviderFactory GetFactory(DataRow providerRow);
+        public static DbProviderFactory GetFactory(DbConnection connection);
+        public static DbProviderFactory GetFactory(string providerInvariantName);
+        public static DataTable GetFactoryClasses();
+        public static IEnumerable<string> GetProviderInvariantNames();
+        public static void RegisterFactory(string providerInvariantName, DbProviderFactory factory);
+        public static void RegisterFactory(string providerInvariantName, string factoryTypeAssemblyQualifiedName);
+        public static void RegisterFactory(string providerInvariantName, Type providerFactoryClass);
+        public static bool TryGetFactory(string providerInvariantName, out DbProviderFactory factory);
+        public static bool UnregisterFactory(string providerInvariantName);
+    }
 }
 namespace System.Data.SqlTypes {
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SqlBinary : IComparable, INullable, IXmlSerializable {
+    public struct SqlBinary : IComparable, INullable, IXmlSerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SqlBoolean : IComparable, INullable, IXmlSerializable {
+    public struct SqlBoolean : IComparable, INullable, IXmlSerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SqlByte : IComparable, INullable, IXmlSerializable {
+    public struct SqlByte : IComparable, INullable, IXmlSerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SqlDateTime : IComparable, INullable, IXmlSerializable {
+    public struct SqlDateTime : IComparable, INullable, IXmlSerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SqlDecimal : IComparable, INullable, IXmlSerializable {
+    public struct SqlDecimal : IComparable, INullable, IXmlSerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SqlDouble : IComparable, INullable, IXmlSerializable {
+    public struct SqlDouble : IComparable, INullable, IXmlSerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SqlGuid : IComparable, INullable, IXmlSerializable {
+    public struct SqlGuid : IComparable, INullable, IXmlSerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SqlInt16 : IComparable, INullable, IXmlSerializable {
+    public struct SqlInt16 : IComparable, INullable, IXmlSerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SqlInt32 : IComparable, INullable, IXmlSerializable {
+    public struct SqlInt32 : IComparable, INullable, IXmlSerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SqlInt64 : IComparable, INullable, IXmlSerializable {
+    public struct SqlInt64 : IComparable, INullable, IXmlSerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SqlMoney : IComparable, INullable, IXmlSerializable {
+    public struct SqlMoney : IComparable, INullable, IXmlSerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SqlSingle : IComparable, INullable, IXmlSerializable {
+    public struct SqlSingle : IComparable, INullable, IXmlSerializable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SqlString : IComparable, INullable, IXmlSerializable {
+    public struct SqlString : IComparable, INullable, IXmlSerializable {
     }
 }
 namespace System.Diagnostics {
     public sealed class ProcessStartInfo {
+        public Collection<string> ArgumentList { get; }
+        public Encoding StandardInputEncoding { get; set; }
     }
 }
 namespace System.Diagnostics.SymbolStore {
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SymbolToken {
+    public readonly struct SymbolToken {
     }
 }
 namespace System.Diagnostics.Tracing {
-    public class EventCounter {
+    public class EventCounter : IDisposable {
+        public void Dispose();
     }
     public abstract class EventListener : IDisposable {
-        protected internal abstract void OnEventWritten(EventWrittenEventArgs eventData);
+        protected internal virtual void OnEventWritten(EventWrittenEventArgs eventData);
+        public event EventHandler<EventSourceCreatedEventArgs> EventSourceCreated;
+        public event EventHandler<EventWrittenEventArgs> EventWritten;
     }
     public class EventSource : IDisposable {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-        protected internal struct EventData {
+        protected internal struct EventData {
         }
     }
+    public class EventSourceCreatedEventArgs : EventArgs {
+        public EventSourceCreatedEventArgs();
+        public EventSource EventSource { get; }
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct EventSourceOptions {
+    public struct EventSourceOptions {
     }
 }
 namespace System.Drawing {
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Color {
+    public readonly struct Color : IEquatable<Color> {
+        public bool IsKnownColor { get; }
+        public bool IsSystemColor { get; }
+        public bool Equals(Color other);
+        public static Color FromKnownColor(KnownColor color);
+        public KnownColor ToKnownColor();
     }
+    public class ColorConverter : TypeConverter {
+        public ColorConverter();
+        public override bool CanConvertFrom(ITypeDescriptorContext context, Type sourceType);
+        public override bool CanConvertTo(ITypeDescriptorContext context, Type destinationType);
+        public override object ConvertFrom(ITypeDescriptorContext context, CultureInfo culture, object value);
+        public override object ConvertTo(ITypeDescriptorContext context, CultureInfo culture, object value, Type destinationType);
+        public override TypeConverter.StandardValuesCollection GetStandardValues(ITypeDescriptorContext context);
+        public override bool GetStandardValuesSupported(ITypeDescriptorContext context);
+    }
+    public enum KnownColor {
+        ActiveBorder = 1,
+        ActiveCaption = 2,
+        ActiveCaptionText = 3,
+        AliceBlue = 28,
+        AntiqueWhite = 29,
+        AppWorkspace = 4,
+        Aqua = 30,
+        Aquamarine = 31,
+        Azure = 32,
+        Beige = 33,
+        Bisque = 34,
+        Black = 35,
+        BlanchedAlmond = 36,
+        Blue = 37,
+        BlueViolet = 38,
+        Brown = 39,
+        BurlyWood = 40,
+        ButtonFace = 168,
+        ButtonHighlight = 169,
+        ButtonShadow = 170,
+        CadetBlue = 41,
+        Chartreuse = 42,
+        Chocolate = 43,
+        Control = 5,
+        ControlDark = 6,
+        ControlDarkDark = 7,
+        ControlLight = 8,
+        ControlLightLight = 9,
+        ControlText = 10,
+        Coral = 44,
+        CornflowerBlue = 45,
+        Cornsilk = 46,
+        Crimson = 47,
+        Cyan = 48,
+        DarkBlue = 49,
+        DarkCyan = 50,
+        DarkGoldenrod = 51,
+        DarkGray = 52,
+        DarkGreen = 53,
+        DarkKhaki = 54,
+        DarkMagenta = 55,
+        DarkOliveGreen = 56,
+        DarkOrange = 57,
+        DarkOrchid = 58,
+        DarkRed = 59,
+        DarkSalmon = 60,
+        DarkSeaGreen = 61,
+        DarkSlateBlue = 62,
+        DarkSlateGray = 63,
+        DarkTurquoise = 64,
+        DarkViolet = 65,
+        DeepPink = 66,
+        DeepSkyBlue = 67,
+        Desktop = 11,
+        DimGray = 68,
+        DodgerBlue = 69,
+        Firebrick = 70,
+        FloralWhite = 71,
+        ForestGreen = 72,
+        Fuchsia = 73,
+        Gainsboro = 74,
+        GhostWhite = 75,
+        Gold = 76,
+        Goldenrod = 77,
+        GradientActiveCaption = 171,
+        GradientInactiveCaption = 172,
+        Gray = 78,
+        GrayText = 12,
+        Green = 79,
+        GreenYellow = 80,
+        Highlight = 13,
+        HighlightText = 14,
+        Honeydew = 81,
+        HotPink = 82,
+        HotTrack = 15,
+        InactiveBorder = 16,
+        InactiveCaption = 17,
+        InactiveCaptionText = 18,
+        IndianRed = 83,
+        Indigo = 84,
+        Info = 19,
+        InfoText = 20,
+        Ivory = 85,
+        Khaki = 86,
+        Lavender = 87,
+        LavenderBlush = 88,
+        LawnGreen = 89,
+        LemonChiffon = 90,
+        LightBlue = 91,
+        LightCoral = 92,
+        LightCyan = 93,
+        LightGoldenrodYellow = 94,
+        LightGray = 95,
+        LightGreen = 96,
+        LightPink = 97,
+        LightSalmon = 98,
+        LightSeaGreen = 99,
+        LightSkyBlue = 100,
+        LightSlateGray = 101,
+        LightSteelBlue = 102,
+        LightYellow = 103,
+        Lime = 104,
+        LimeGreen = 105,
+        Linen = 106,
+        Magenta = 107,
+        Maroon = 108,
+        MediumAquamarine = 109,
+        MediumBlue = 110,
+        MediumOrchid = 111,
+        MediumPurple = 112,
+        MediumSeaGreen = 113,
+        MediumSlateBlue = 114,
+        MediumSpringGreen = 115,
+        MediumTurquoise = 116,
+        MediumVioletRed = 117,
+        Menu = 21,
+        MenuBar = 173,
+        MenuHighlight = 174,
+        MenuText = 22,
+        MidnightBlue = 118,
+        MintCream = 119,
+        MistyRose = 120,
+        Moccasin = 121,
+        NavajoWhite = 122,
+        Navy = 123,
+        OldLace = 124,
+        Olive = 125,
+        OliveDrab = 126,
+        Orange = 127,
+        OrangeRed = 128,
+        Orchid = 129,
+        PaleGoldenrod = 130,
+        PaleGreen = 131,
+        PaleTurquoise = 132,
+        PaleVioletRed = 133,
+        PapayaWhip = 134,
+        PeachPuff = 135,
+        Peru = 136,
+        Pink = 137,
+        Plum = 138,
+        PowderBlue = 139,
+        Purple = 140,
+        Red = 141,
+        RosyBrown = 142,
+        RoyalBlue = 143,
+        SaddleBrown = 144,
+        Salmon = 145,
+        SandyBrown = 146,
+        ScrollBar = 23,
+        SeaGreen = 147,
+        SeaShell = 148,
+        Sienna = 149,
+        Silver = 150,
+        SkyBlue = 151,
+        SlateBlue = 152,
+        SlateGray = 153,
+        Snow = 154,
+        SpringGreen = 155,
+        SteelBlue = 156,
+        Tan = 157,
+        Teal = 158,
+        Thistle = 159,
+        Tomato = 160,
+        Transparent = 27,
+        Turquoise = 161,
+        Violet = 162,
+        Wheat = 163,
+        White = 164,
+        WhiteSmoke = 165,
+        Window = 24,
+        WindowFrame = 25,
+        WindowText = 26,
+        Yellow = 166,
+        YellowGreen = 167,
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Point {
+    public struct Point : IEquatable<Point> {
+        public bool Equals(Point other);
     }
+    public class PointConverter : TypeConverter {
+        public PointConverter();
+        public override bool CanConvertFrom(ITypeDescriptorContext context, Type sourceType);
+        public override bool CanConvertTo(ITypeDescriptorContext context, Type destinationType);
+        public override object ConvertFrom(ITypeDescriptorContext context, CultureInfo culture, object value);
+        public override object ConvertTo(ITypeDescriptorContext context, CultureInfo culture, object value, Type destinationType);
+        public override object CreateInstance(ITypeDescriptorContext context, IDictionary propertyValues);
+        public override bool GetCreateInstanceSupported(ITypeDescriptorContext context);
+        public override PropertyDescriptorCollection GetProperties(ITypeDescriptorContext context, object value, Attribute[] attributes);
+        public override bool GetPropertiesSupported(ITypeDescriptorContext context);
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct PointF {
+    public struct PointF : IEquatable<PointF> {
+        public bool Equals(PointF other);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Rectangle {
+    public struct Rectangle : IEquatable<Rectangle> {
+        public bool Equals(Rectangle other);
     }
+    public class RectangleConverter : TypeConverter {
+        public RectangleConverter();
+        public override bool CanConvertFrom(ITypeDescriptorContext context, Type sourceType);
+        public override bool CanConvertTo(ITypeDescriptorContext context, Type destinationType);
+        public override object ConvertFrom(ITypeDescriptorContext context, CultureInfo culture, object value);
+        public override object ConvertTo(ITypeDescriptorContext context, CultureInfo culture, object value, Type destinationType);
+        public override object CreateInstance(ITypeDescriptorContext context, IDictionary propertyValues);
+        public override bool GetCreateInstanceSupported(ITypeDescriptorContext context);
+        public override PropertyDescriptorCollection GetProperties(ITypeDescriptorContext context, object value, Attribute[] attributes);
+        public override bool GetPropertiesSupported(ITypeDescriptorContext context);
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct RectangleF {
+    public struct RectangleF : IEquatable<RectangleF> {
+        public bool Equals(RectangleF other);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Size {
+    public struct Size : IEquatable<Size> {
+        public bool Equals(Size other);
+        public static Size operator /(Size left, int right);
+        public static SizeF operator /(Size left, float right);
+        public static Size operator *(int left, Size right);
+        public static SizeF operator *(float left, Size right);
+        public static Size operator *(Size left, int right);
+        public static SizeF operator *(Size left, float right);
     }
+    public class SizeConverter : TypeConverter {
+        public SizeConverter();
+        public override bool CanConvertFrom(ITypeDescriptorContext context, Type sourceType);
+        public override bool CanConvertTo(ITypeDescriptorContext context, Type destinationType);
+        public override object ConvertFrom(ITypeDescriptorContext context, CultureInfo culture, object value);
+        public override object ConvertTo(ITypeDescriptorContext context, CultureInfo culture, object value, Type destinationType);
+        public override object CreateInstance(ITypeDescriptorContext context, IDictionary propertyValues);
+        public override bool GetCreateInstanceSupported(ITypeDescriptorContext context);
+        public override PropertyDescriptorCollection GetProperties(ITypeDescriptorContext context, object value, Attribute[] attributes);
+        public override bool GetPropertiesSupported(ITypeDescriptorContext context);
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SizeF {
+    public struct SizeF : IEquatable<SizeF> {
+        public bool Equals(SizeF other);
+        public static SizeF operator /(SizeF left, float right);
+        public static SizeF operator *(float left, SizeF right);
+        public static SizeF operator *(SizeF left, float right);
     }
+    public class SizeFConverter : TypeConverter {
+        public SizeFConverter();
+        public override bool CanConvertFrom(ITypeDescriptorContext context, Type sourceType);
+        public override bool CanConvertTo(ITypeDescriptorContext context, Type destinationType);
+        public override object ConvertFrom(ITypeDescriptorContext context, CultureInfo culture, object value);
+        public override object ConvertTo(ITypeDescriptorContext context, CultureInfo culture, object value, Type destinationType);
+        public override object CreateInstance(ITypeDescriptorContext context, IDictionary propertyValues);
+        public override bool GetCreateInstanceSupported(ITypeDescriptorContext context);
+        public override PropertyDescriptorCollection GetProperties(ITypeDescriptorContext context, object value, Attribute[] attributes);
+        public override bool GetPropertiesSupported(ITypeDescriptorContext context);
+    }
 }
 namespace System.Globalization {
     public static class CharUnicodeInfo {
+        public static UnicodeCategory GetUnicodeCategory(int codePoint);
     }
-    public class CultureNotFoundException : ArgumentException, ISerializable {
+    public class CultureNotFoundException : ArgumentException {
     }
 }
 namespace System.IO {
     public class BinaryReader : IDisposable {
+        public virtual int Read(Span<byte> buffer);
+        public virtual int Read(Span<char> buffer);
     }
     public class BinaryWriter : IDisposable {
+        public virtual void Write(ReadOnlySpan<byte> buffer);
+        public virtual void Write(ReadOnlySpan<char> chars);
     }
     public sealed class BufferedStream : Stream {
+        public int BufferSize { get; }
+        public Stream UnderlyingStream { get; }
     }
     public static class Directory {
+        public static IEnumerable<string> EnumerateDirectories(string path, string searchPattern, EnumerationOptions enumerationOptions);
+        public static IEnumerable<string> EnumerateFiles(string path, string searchPattern, EnumerationOptions enumerationOptions);
+        public static IEnumerable<string> EnumerateFileSystemEntries(string path, string searchPattern, EnumerationOptions enumerationOptions);
+        public static string[] GetDirectories(string path, string searchPattern, EnumerationOptions enumerationOptions);
+        public static string[] GetFiles(string path, string searchPattern, EnumerationOptions enumerationOptions);
+        public static string[] GetFileSystemEntries(string path, string searchPattern, EnumerationOptions enumerationOptions);
     }
     public sealed class DirectoryInfo : FileSystemInfo {
+        public IEnumerable<DirectoryInfo> EnumerateDirectories(string searchPattern, EnumerationOptions enumerationOptions);
+        public IEnumerable<FileInfo> EnumerateFiles(string searchPattern, EnumerationOptions enumerationOptions);
+        public IEnumerable<FileSystemInfo> EnumerateFileSystemInfos(string searchPattern, EnumerationOptions enumerationOptions);
+        public DirectoryInfo[] GetDirectories(string searchPattern, EnumerationOptions enumerationOptions);
+        public FileInfo[] GetFiles(string searchPattern, EnumerationOptions enumerationOptions);
+        public FileSystemInfo[] GetFileSystemInfos(string searchPattern, EnumerationOptions enumerationOptions);
     }
+    public class EnumerationOptions {
+        public EnumerationOptions();
+        public FileAttributes AttributesToSkip { get; set; }
+        public int BufferSize { get; set; }
+        public bool IgnoreInaccessible { get; set; }
+        public MatchCasing MatchCasing { get; set; }
+        public MatchType MatchType { get; set; }
+        public bool RecurseSubdirectories { get; set; }
+        public bool ReturnSpecialDirectories { get; set; }
+    }
     public static class File {
+        public static Task AppendAllLinesAsync(string path, IEnumerable<string> contents, CancellationToken cancellationToken = default(CancellationToken));
+        public static Task AppendAllLinesAsync(string path, IEnumerable<string> contents, Encoding encoding, CancellationToken cancellationToken = default(CancellationToken));
+        public static Task AppendAllTextAsync(string path, string contents, CancellationToken cancellationToken = default(CancellationToken));
+        public static Task AppendAllTextAsync(string path, string contents, Encoding encoding, CancellationToken cancellationToken = default(CancellationToken));
+        public static Task<byte[]> ReadAllBytesAsync(string path, CancellationToken cancellationToken = default(CancellationToken));
+        public static Task<string[]> ReadAllLinesAsync(string path, CancellationToken cancellationToken = default(CancellationToken));
+        public static Task<string[]> ReadAllLinesAsync(string path, Encoding encoding, CancellationToken cancellationToken = default(CancellationToken));
+        public static Task<string> ReadAllTextAsync(string path, CancellationToken cancellationToken = default(CancellationToken));
+        public static Task<string> ReadAllTextAsync(string path, Encoding encoding, CancellationToken cancellationToken = default(CancellationToken));
+        public static Task WriteAllBytesAsync(string path, byte[] bytes, CancellationToken cancellationToken = default(CancellationToken));
+        public static Task WriteAllLinesAsync(string path, IEnumerable<string> contents, CancellationToken cancellationToken = default(CancellationToken));
+        public static Task WriteAllLinesAsync(string path, IEnumerable<string> contents, Encoding encoding, CancellationToken cancellationToken = default(CancellationToken));
+        public static Task WriteAllTextAsync(string path, string contents, CancellationToken cancellationToken = default(CancellationToken));
+        public static Task WriteAllTextAsync(string path, string contents, Encoding encoding, CancellationToken cancellationToken = default(CancellationToken));
     }
     public class FileStream : Stream {
-        public string Name { get; }
+        public virtual string Name { get; }
-        public override IAsyncResult BeginRead(byte[] array, int offset, int numBytes, AsyncCallback userCallback, object stateObject);
+        public override IAsyncResult BeginRead(byte[] array, int offset, int numBytes, AsyncCallback callback, object state);
-        public override IAsyncResult BeginWrite(byte[] array, int offset, int numBytes, AsyncCallback userCallback, object stateObject);
+        public override IAsyncResult BeginWrite(byte[] array, int offset, int numBytes, AsyncCallback callback, object state);
     }
+    public enum MatchCasing {
+        CaseInsensitive = 2,
+        CaseSensitive = 1,
+        PlatformDefault = 0,
+    }
+    public enum MatchType {
+        Simple = 0,
+        Win32 = 1,
+    }
     public class MemoryStream : Stream {
+        public override IAsyncResult BeginRead(byte[] buffer, int offset, int count, AsyncCallback callback, object state);
+        public override IAsyncResult BeginWrite(byte[] buffer, int offset, int count, AsyncCallback callback, object state);
+        public override void CopyTo(Stream destination, int bufferSize);
+        public override int EndRead(IAsyncResult asyncResult);
+        public override void EndWrite(IAsyncResult asyncResult);
+        public override int Read(Span<byte> destination);
+        public override ValueTask<int> ReadAsync(Memory<byte> destination, CancellationToken cancellationToken = default(CancellationToken));
+        public override void Write(ReadOnlySpan<byte> source);
+        public override ValueTask WriteAsync(ReadOnlyMemory<byte> source, CancellationToken cancellationToken = default(CancellationToken));
     }
     public static class Path {
+        public static ReadOnlySpan<char> GetDirectoryName(ReadOnlySpan<char> path);
+        public static ReadOnlySpan<char> GetExtension(ReadOnlySpan<char> path);
+        public static ReadOnlySpan<char> GetFileName(ReadOnlySpan<char> path);
+        public static ReadOnlySpan<char> GetFileNameWithoutExtension(ReadOnlySpan<char> path);
+        public static string GetFullPath(string path, string basePath);
+        public static ReadOnlySpan<char> GetPathRoot(ReadOnlySpan<char> path);
+        public static string GetRelativePath(string relativeTo, string path);
+        public static bool HasExtension(ReadOnlySpan<char> path);
+        public static bool IsPathFullyQualified(ReadOnlySpan<char> path);
+        public static bool IsPathFullyQualified(string path);
+        public static bool IsPathRooted(ReadOnlySpan<char> path);
+        public static string Join(ReadOnlySpan<char> path1, ReadOnlySpan<char> path2);
+        public static string Join(ReadOnlySpan<char> path1, ReadOnlySpan<char> path2, ReadOnlySpan<char> path3);
+        public static bool TryJoin(ReadOnlySpan<char> path1, ReadOnlySpan<char> path2, Span<char> destination, out int charsWritten);
+        public static bool TryJoin(ReadOnlySpan<char> path1, ReadOnlySpan<char> path2, ReadOnlySpan<char> path3, Span<char> destination, out int charsWritten);
     }
     public abstract class Stream : MarshalByRefObject, IDisposable {
-        public void CopyTo(Stream destination, int bufferSize);
+        public virtual void CopyTo(Stream destination, int bufferSize);
+        public Task CopyToAsync(Stream destination, CancellationToken cancellationToken);
+        public virtual int Read(Span<byte> buffer);
+        public virtual ValueTask<int> ReadAsync(Memory<byte> buffer, CancellationToken cancellationToken = default(CancellationToken));
+        public virtual void Write(ReadOnlySpan<byte> buffer);
+        public virtual ValueTask WriteAsync(ReadOnlyMemory<byte> buffer, CancellationToken cancellationToken = default(CancellationToken));
     }
     public class StreamReader : TextReader {
+        public override int Read(Span<char> buffer);
+        public override ValueTask<int> ReadAsync(Memory<char> buffer, CancellationToken cancellationToken = default(CancellationToken));
+        public override int ReadBlock(Span<char> buffer);
+        public override ValueTask<int> ReadBlockAsync(Memory<char> buffer, CancellationToken cancellationToken = default(CancellationToken));
     }
     public class StreamWriter : TextWriter {
+        public override void Write(ReadOnlySpan<char> buffer);
+        public override Task WriteAsync(ReadOnlyMemory<char> buffer, CancellationToken cancellationToken = default(CancellationToken));
+        public override void WriteLine(ReadOnlySpan<char> buffer);
+        public override Task WriteLineAsync(ReadOnlyMemory<char> buffer, CancellationToken cancellationToken = default(CancellationToken));
     }
     public class StringReader : TextReader {
+        public override int Read(Span<char> buffer);
+        public override ValueTask<int> ReadAsync(Memory<char> buffer, CancellationToken cancellationToken = default(CancellationToken));
+        public override int ReadBlock(Span<char> buffer);
+        public override ValueTask<int> ReadBlockAsync(Memory<char> buffer, CancellationToken cancellationToken = default(CancellationToken));
     }
     public class StringWriter : TextWriter {
+        public override void Write(ReadOnlySpan<char> buffer);
+        public override Task WriteAsync(ReadOnlyMemory<char> buffer, CancellationToken cancellationToken = default(CancellationToken));
+        public override void WriteLine(ReadOnlySpan<char> buffer);
+        public override Task WriteLineAsync(ReadOnlyMemory<char> buffer, CancellationToken cancellationToken = default(CancellationToken));
     }
     public abstract class TextReader : MarshalByRefObject, IDisposable {
+        public virtual int Read(Span<char> buffer);
+        public virtual ValueTask<int> ReadAsync(Memory<char> buffer, CancellationToken cancellationToken = default(CancellationToken));
+        public virtual int ReadBlock(Span<char> buffer);
+        public virtual ValueTask<int> ReadBlockAsync(Memory<char> buffer, CancellationToken cancellationToken = default(CancellationToken));
     }
     public abstract class TextWriter : MarshalByRefObject, IDisposable {
+        public virtual void Write(ReadOnlySpan<char> buffer);
+        public virtual Task WriteAsync(ReadOnlyMemory<char> buffer, CancellationToken cancellationToken = default(CancellationToken));
+        public virtual void WriteLine(ReadOnlySpan<char> buffer);
+        public virtual Task WriteLineAsync(ReadOnlyMemory<char> buffer, CancellationToken cancellationToken = default(CancellationToken));
     }
     public class UnmanagedMemoryStream : Stream {
+        public override int Read(Span<byte> destination);
+        public override void Write(ReadOnlySpan<byte> source);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct WaitForChangedResult {
+    public struct WaitForChangedResult {
     }
 }
 namespace System.IO.Compression {
+    public struct BrotliDecoder : IDisposable {
+        public OperationStatus Decompress(ReadOnlySpan<byte> source, Span<byte> destination, out int bytesConsumed, out int bytesWritten);
+        public void Dispose();
+        public static bool TryDecompress(ReadOnlySpan<byte> source, Span<byte> destination, out int bytesWritten);
+    }
+    public struct BrotliEncoder : IDisposable {
+        public BrotliEncoder(int quality, int window);
+        public OperationStatus Compress(ReadOnlySpan<byte> source, Span<byte> destination, out int bytesConsumed, out int bytesWritten, bool isFinalBlock);
+        public void Dispose();
+        public OperationStatus Flush(Span<byte> destination, out int bytesWritten);
+        public static int GetMaxCompressedLength(int inputSize);
+        public static bool TryCompress(ReadOnlySpan<byte> source, Span<byte> destination, out int bytesWritten);
+        public static bool TryCompress(ReadOnlySpan<byte> source, Span<byte> destination, out int bytesWritten, int quality, int window);
+    }
+    public sealed class BrotliStream : Stream {
+        public BrotliStream(Stream stream, CompressionLevel compressionLevel);
+        public BrotliStream(Stream stream, CompressionLevel compressionLevel, bool leaveOpen);
+        public BrotliStream(Stream stream, CompressionMode mode);
+        public BrotliStream(Stream stream, CompressionMode mode, bool leaveOpen);
+        public Stream BaseStream { get; }
+        public override bool CanRead { get; }
+        public override bool CanSeek { get; }
+        public override bool CanWrite { get; }
+        public override long Length { get; }
+        public override long Position { get; set; }
+        public override IAsyncResult BeginRead(byte[] buffer, int offset, int count, AsyncCallback asyncCallback, object asyncState);
+        public override IAsyncResult BeginWrite(byte[] buffer, int offset, int count, AsyncCallback asyncCallback, object asyncState);
+        public override int EndRead(IAsyncResult asyncResult);
+        public override void EndWrite(IAsyncResult asyncResult);
+        public override void Flush();
+        public override int Read(byte[] buffer, int offset, int count);
+        public override Task<int> ReadAsync(byte[] buffer, int offset, int count, CancellationToken cancellationToken);
+        public override long Seek(long offset, SeekOrigin origin);
+        public override void SetLength(long value);
+        public override void Write(byte[] buffer, int offset, int count);
+        public override Task WriteAsync(byte[] buffer, int offset, int count, CancellationToken cancellationToken);
+    }
     public class DeflateStream : Stream {
-        public override IAsyncResult BeginRead(byte[] array, int offset, int count, AsyncCallback asyncCallback, object asyncState);
+        public override IAsyncResult BeginRead(byte[] buffer, int offset, int count, AsyncCallback asyncCallback, object asyncState);
+        public override Task<int> ReadAsync(byte[] array, int offset, int count, CancellationToken cancellationToken);
+        public override Task WriteAsync(byte[] array, int offset, int count, CancellationToken cancellationToken);
     }
     public class GZipStream : Stream {
+        public override Task<int> ReadAsync(byte[] array, int offset, int count, CancellationToken cancellationToken);
+        public override Task WriteAsync(byte[] array, int offset, int count, CancellationToken cancellationToken);
     }
     public class ZipArchiveEntry {
+        public uint Crc32 { get; }
+        public int ExternalAttributes { get; set; }
     }
     public static class ZipFile {
+        public static void ExtractToDirectory(string sourceArchiveFileName, string destinationDirectoryName, bool overwriteFiles);
+        public static void ExtractToDirectory(string sourceArchiveFileName, string destinationDirectoryName, Encoding entryNameEncoding, bool overwriteFiles);
     }
     public static class ZipFileExtensions {
+        public static void ExtractToDirectory(this ZipArchive source, string destinationDirectoryName, bool overwriteFiles);
     }
 }
+namespace System.IO.Enumeration {
+    public ref struct FileSystemEntry {
+        public FileAttributes Attributes { get; }
+        public DateTimeOffset CreationTimeUtc { get; }
+        public ReadOnlySpan<char> Directory { get; }
+        public ReadOnlySpan<char> FileName { get; }
+        public bool IsDirectory { get; }
+        public bool IsHidden { get; }
+        public DateTimeOffset LastAccessTimeUtc { get; }
+        public DateTimeOffset LastWriteTimeUtc { get; }
+        public long Length { get; }
+        public ReadOnlySpan<char> OriginalRootDirectory { get; }
+        public ReadOnlySpan<char> RootDirectory { get; }
+        public FileSystemInfo ToFileSystemInfo();
+        public string ToFullPath();
+        public string ToSpecifiedFullPath();
+    }
+    public class FileSystemEnumerable<TResult> : IEnumerable, IEnumerable<TResult> {
+        public delegate bool FindPredicate(ref FileSystemEntry entry); {
+            public FindPredicate(object @object, IntPtr method);
+            public virtual IAsyncResult BeginInvoke(ref FileSystemEntry entry, AsyncCallback callback, object @object);
+            public virtual bool EndInvoke(ref FileSystemEntry entry, IAsyncResult result);
+            public virtual bool Invoke(ref FileSystemEntry entry);
+        }
+        public delegate TResult FindTransform(ref FileSystemEntry entry); {
+            public FindTransform(object @object, IntPtr method);
+            public virtual IAsyncResult BeginInvoke(ref FileSystemEntry entry, AsyncCallback callback, object @object);
+            public virtual TResult EndInvoke(ref FileSystemEntry entry, IAsyncResult result);
+            public virtual TResult Invoke(ref FileSystemEntry entry);
+        }
+        public FileSystemEnumerable(string directory, FileSystemEnumerable<TResult>.FindTransform transform, EnumerationOptions options = null);
+        public FileSystemEnumerable<TResult>.FindPredicate ShouldIncludePredicate { get; set; }
+        public FileSystemEnumerable<TResult>.FindPredicate ShouldRecursePredicate { get; set; }
+        public IEnumerator<TResult> GetEnumerator();
+        IEnumerator System.Collections.IEnumerable.GetEnumerator();
+    }
+    public abstract class FileSystemEnumerator<TResult> : CriticalFinalizerObject, IDisposable, IEnumerator, IEnumerator<TResult> {
+        public FileSystemEnumerator(string directory, EnumerationOptions options = null);
+        public TResult Current { get; }
+        object System.Collections.IEnumerator.Current { get; }
+        protected virtual bool ContinueOnError(int error);
+        public void Dispose();
+        protected virtual void Dispose(bool disposing);
+        public bool MoveNext();
+        protected virtual void OnDirectoryFinished(ReadOnlySpan<char> directory);
+        public void Reset();
+        protected virtual bool ShouldIncludeEntry(ref FileSystemEntry entry);
+        protected virtual bool ShouldRecurseIntoEntry(ref FileSystemEntry entry);
+        protected abstract TResult TransformEntry(ref FileSystemEntry entry);
+    }
+    public static class FileSystemName {
+        public static bool MatchesSimpleExpression(ReadOnlySpan<char> expression, ReadOnlySpan<char> name, bool ignoreCase = true);
+        public static bool MatchesWin32Expression(ReadOnlySpan<char> expression, ReadOnlySpan<char> name, bool ignoreCase = true);
+        public static string TranslateWin32Expression(string expression);
+    }
+}
 namespace System.IO.IsolatedStorage {
     public abstract class IsolatedStorage : MarshalByRefObject {
+        protected IsolatedStorage();
     }
 }
 namespace System.IO.Pipes {
     public enum PipeOptions {
+        CurrentUserOnly = 536870912,
     }
     public abstract class PipeStream : Stream {
+        public override Task<int> ReadAsync(byte[] buffer, int offset, int count, CancellationToken cancellationToken);
+        public override Task WriteAsync(byte[] buffer, int offset, int count, CancellationToken cancellationToken);
     }
 }
 namespace System.Linq {
     public static class Enumerable {
+        public static IEnumerable<TSource> SkipLast<TSource>(this IEnumerable<TSource> source, int count);
+        public static IEnumerable<TSource> TakeLast<TSource>(this IEnumerable<TSource> source, int count);
+        public static HashSet<TSource> ToHashSet<TSource>(this IEnumerable<TSource> source);
+        public static HashSet<TSource> ToHashSet<TSource>(this IEnumerable<TSource> source, IEqualityComparer<TSource> comparer);
     }
-    public interface IOrderedEnumerable<TElement> : IEnumerable, IEnumerable<TElement> {
+    public interface IOrderedEnumerable<out TElement> : IEnumerable, IEnumerable<TElement> {
     }
     public static class Queryable {
+        public static IQueryable<TSource> Append<TSource>(this IQueryable<TSource> source, TSource element);
+        public static IQueryable<TSource> Prepend<TSource>(this IQueryable<TSource> source, TSource element);
+        public static IQueryable<TSource> SkipLast<TSource>(this IQueryable<TSource> source, int count);
+        public static IQueryable<TSource> TakeLast<TSource>(this IQueryable<TSource> source, int count);
     }
 }
 namespace System.Net {
     public class IPAddress {
+        public IPAddress(ReadOnlySpan<byte> address);
+        public IPAddress(ReadOnlySpan<byte> address, long scopeid);
+        public static IPAddress Parse(ReadOnlySpan<char> ipString);
+        public bool TryFormat(Span<char> destination, out int charsWritten);
+        public static bool TryParse(ReadOnlySpan<char> ipString, out IPAddress address);
+        public bool TryWriteBytes(Span<byte> destination, out int bytesWritten);
     }
 }
 namespace System.Net.Http {
+    public sealed class ReadOnlyMemoryContent : HttpContent {
+        public ReadOnlyMemoryContent(ReadOnlyMemory<byte> content);
+    }
 }
 namespace System.Net.Sockets {
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct IPPacketInformation {
+    public struct IPPacketInformation {
     }
     public class Socket : IDisposable {
+        public int Receive(Span<byte> buffer);
+        public int Receive(Span<byte> buffer, SocketFlags socketFlags);
+        public int Receive(Span<byte> buffer, SocketFlags socketFlags, out SocketError errorCode);
+        public int Send(ReadOnlySpan<byte> buffer);
+        public int Send(ReadOnlySpan<byte> buffer, SocketFlags socketFlags);
+        public int Send(ReadOnlySpan<byte> buffer, SocketFlags socketFlags, out SocketError errorCode);
     }
     public class SocketAsyncEventArgs : EventArgs, IDisposable {
+        public Memory<byte> MemoryBuffer { get; }
+        public void SetBuffer(Memory<byte> buffer);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SocketInformation {
+    public struct SocketInformation {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SocketReceiveFromResult {
+    public struct SocketReceiveFromResult {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SocketReceiveMessageFromResult {
+    public struct SocketReceiveMessageFromResult {
     }
     public static class SocketTaskExtensions {
+        public static ValueTask<int> ReceiveAsync(this Socket socket, Memory<byte> buffer, SocketFlags socketFlags, CancellationToken cancellationToken = default(CancellationToken));
+        public static ValueTask<int> SendAsync(this Socket socket, ReadOnlyMemory<byte> buffer, SocketFlags socketFlags, CancellationToken cancellationToken = default(CancellationToken));
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct UdpReceiveResult : IEquatable<UdpReceiveResult> {
+    public struct UdpReceiveResult : IEquatable<UdpReceiveResult> {
     }
 }
 namespace System.Net.WebSockets {
+    public readonly struct ValueWebSocketReceiveResult {
+        public ValueWebSocketReceiveResult(int count, WebSocketMessageType messageType, bool endOfMessage);
+        public int Count { get; }
+        public bool EndOfMessage { get; }
+        public WebSocketMessageType MessageType { get; }
+    }
     public abstract class WebSocket : IDisposable {
+        public virtual ValueTask<ValueWebSocketReceiveResult> ReceiveAsync(Memory<byte> buffer, CancellationToken cancellationToken);
+        public virtual ValueTask SendAsync(ReadOnlyMemory<byte> buffer, WebSocketMessageType messageType, bool endOfMessage, CancellationToken cancellationToken);
     }
 }
 namespace System.Numerics {
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct BigInteger : IComparable, IComparable<BigInteger>, IEquatable<BigInteger>, IFormattable {
+    public readonly struct BigInteger : IComparable, IComparable<BigInteger>, IEquatable<BigInteger>, IFormattable {
+        public BigInteger(ReadOnlySpan<byte> value, bool isUnsigned = false, bool isBigEndian = false);
+        public int GetByteCount(bool isUnsigned = false);
+        public static BigInteger Parse(ReadOnlySpan<char> value, NumberStyles style = (NumberStyles)(7), IFormatProvider provider = null);
+        public byte[] ToByteArray(bool isUnsigned = false, bool isBigEndian = false);
+        public bool TryFormat(Span<char> destination, out int charsWritten, ReadOnlySpan<char> format = default(ReadOnlySpan<char>), IFormatProvider provider = null);
+        public static bool TryParse(ReadOnlySpan<char> value, out BigInteger result);
+        public static bool TryParse(ReadOnlySpan<char> value, NumberStyles style, IFormatProvider provider, out BigInteger result);
+        public bool TryWriteBytes(Span<byte> destination, out int bytesWritten, bool isUnsigned = false, bool isBigEndian = false);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct Complex : IEquatable<Complex>, IFormattable {
+    public struct Complex : IEquatable<Complex>, IFormattable {
     }
+    public struct Matrix3x2 : IEquatable<Matrix3x2> {
+        public float M11;
+        public float M12;
+        public float M21;
+        public float M22;
+        public float M31;
+        public float M32;
+        public Matrix3x2(float m11, float m12, float m21, float m22, float m31, float m32);
+        public static Matrix3x2 Identity { get; }
+        public bool IsIdentity { get; }
+        public Vector2 Translation { get; set; }
+        public static Matrix3x2 Add(Matrix3x2 value1, Matrix3x2 value2);
+        public static Matrix3x2 CreateRotation(float radians);
+        public static Matrix3x2 CreateRotation(float radians, Vector2 centerPoint);
+        public static Matrix3x2 CreateScale(float scale);
+        public static Matrix3x2 CreateScale(float xScale, float yScale);
+        public static Matrix3x2 CreateScale(float xScale, float yScale, Vector2 centerPoint);
+        public static Matrix3x2 CreateScale(float scale, Vector2 centerPoint);
+        public static Matrix3x2 CreateScale(Vector2 scales);
+        public static Matrix3x2 CreateScale(Vector2 scales, Vector2 centerPoint);
+        public static Matrix3x2 CreateSkew(float radiansX, float radiansY);
+        public static Matrix3x2 CreateSkew(float radiansX, float radiansY, Vector2 centerPoint);
+        public static Matrix3x2 CreateTranslation(float xPosition, float yPosition);
+        public static Matrix3x2 CreateTranslation(Vector2 position);
+        public bool Equals(Matrix3x2 other);
+        public override bool Equals(object obj);
+        public float GetDeterminant();
+        public override int GetHashCode();
+        public static bool Invert(Matrix3x2 matrix, out Matrix3x2 result);
+        public static Matrix3x2 Lerp(Matrix3x2 matrix1, Matrix3x2 matrix2, float amount);
+        public static Matrix3x2 Multiply(Matrix3x2 value1, Matrix3x2 value2);
+        public static Matrix3x2 Multiply(Matrix3x2 value1, float value2);
+        public static Matrix3x2 Negate(Matrix3x2 value);
+        public static Matrix3x2 operator +(Matrix3x2 value1, Matrix3x2 value2);
+        public static bool operator ==(Matrix3x2 value1, Matrix3x2 value2);
+        public static bool operator !=(Matrix3x2 value1, Matrix3x2 value2);
+        public static Matrix3x2 operator *(Matrix3x2 value1, Matrix3x2 value2);
+        public static Matrix3x2 operator *(Matrix3x2 value1, float value2);
+        public static Matrix3x2 operator -(Matrix3x2 value1, Matrix3x2 value2);
+        public static Matrix3x2 operator -(Matrix3x2 value);
+        public static Matrix3x2 Subtract(Matrix3x2 value1, Matrix3x2 value2);
+        public override string ToString();
+    }
+    public struct Matrix4x4 : IEquatable<Matrix4x4> {
+        public float M11;
+        public float M12;
+        public float M13;
+        public float M14;
+        public float M21;
+        public float M22;
+        public float M23;
+        public float M24;
+        public float M31;
+        public float M32;
+        public float M33;
+        public float M34;
+        public float M41;
+        public float M42;
+        public float M43;
+        public float M44;
+        public Matrix4x4(Matrix3x2 value);
+        public Matrix4x4(float m11, float m12, float m13, float m14, float m21, float m22, float m23, float m24, float m31, float m32, float m33, float m34, float m41, float m42, float m43, float m44);
+        public static Matrix4x4 Identity { get; }
+        public bool IsIdentity { get; }
+        public Vector3 Translation { get; set; }
+        public static Matrix4x4 Add(Matrix4x4 value1, Matrix4x4 value2);
+        public static Matrix4x4 CreateBillboard(Vector3 objectPosition, Vector3 cameraPosition, Vector3 cameraUpVector, Vector3 cameraForwardVector);
+        public static Matrix4x4 CreateConstrainedBillboard(Vector3 objectPosition, Vector3 cameraPosition, Vector3 rotateAxis, Vector3 cameraForwardVector, Vector3 objectForwardVector);
+        public static Matrix4x4 CreateFromAxisAngle(Vector3 axis, float angle);
+        public static Matrix4x4 CreateFromQuaternion(Quaternion quaternion);
+        public static Matrix4x4 CreateFromYawPitchRoll(float yaw, float pitch, float roll);
+        public static Matrix4x4 CreateLookAt(Vector3 cameraPosition, Vector3 cameraTarget, Vector3 cameraUpVector);
+        public static Matrix4x4 CreateOrthographic(float width, float height, float zNearPlane, float zFarPlane);
+        public static Matrix4x4 CreateOrthographicOffCenter(float left, float right, float bottom, float top, float zNearPlane, float zFarPlane);
+        public static Matrix4x4 CreatePerspective(float width, float height, float nearPlaneDistance, float farPlaneDistance);
+        public static Matrix4x4 CreatePerspectiveFieldOfView(float fieldOfView, float aspectRatio, float nearPlaneDistance, float farPlaneDistance);
+        public static Matrix4x4 CreatePerspectiveOffCenter(float left, float right, float bottom, float top, float nearPlaneDistance, float farPlaneDistance);
+        public static Matrix4x4 CreateReflection(Plane value);
+        public static Matrix4x4 CreateRotationX(float radians);
+        public static Matrix4x4 CreateRotationX(float radians, Vector3 centerPoint);
+        public static Matrix4x4 CreateRotationY(float radians);
+        public static Matrix4x4 CreateRotationY(float radians, Vector3 centerPoint);
+        public static Matrix4x4 CreateRotationZ(float radians);
+        public static Matrix4x4 CreateRotationZ(float radians, Vector3 centerPoint);
+        public static Matrix4x4 CreateScale(float scale);
+        public static Matrix4x4 CreateScale(float xScale, float yScale, float zScale);
+        public static Matrix4x4 CreateScale(float xScale, float yScale, float zScale, Vector3 centerPoint);
+        public static Matrix4x4 CreateScale(float scale, Vector3 centerPoint);
+        public static Matrix4x4 CreateScale(Vector3 scales);
+        public static Matrix4x4 CreateScale(Vector3 scales, Vector3 centerPoint);
+        public static Matrix4x4 CreateShadow(Vector3 lightDirection, Plane plane);
+        public static Matrix4x4 CreateTranslation(float xPosition, float yPosition, float zPosition);
+        public static Matrix4x4 CreateTranslation(Vector3 position);
+        public static Matrix4x4 CreateWorld(Vector3 position, Vector3 forward, Vector3 up);
+        public static bool Decompose(Matrix4x4 matrix, out Vector3 scale, out Quaternion rotation, out Vector3 translation);
+        public bool Equals(Matrix4x4 other);
+        public override bool Equals(object obj);
+        public float GetDeterminant();
+        public override int GetHashCode();
+        public static bool Invert(Matrix4x4 matrix, out Matrix4x4 result);
+        public static Matrix4x4 Lerp(Matrix4x4 matrix1, Matrix4x4 matrix2, float amount);
+        public static Matrix4x4 Multiply(Matrix4x4 value1, Matrix4x4 value2);
+        public static Matrix4x4 Multiply(Matrix4x4 value1, float value2);
+        public static Matrix4x4 Negate(Matrix4x4 value);
+        public static Matrix4x4 operator +(Matrix4x4 value1, Matrix4x4 value2);
+        public static bool operator ==(Matrix4x4 value1, Matrix4x4 value2);
+        public static bool operator !=(Matrix4x4 value1, Matrix4x4 value2);
+        public static Matrix4x4 operator *(Matrix4x4 value1, Matrix4x4 value2);
+        public static Matrix4x4 operator *(Matrix4x4 value1, float value2);
+        public static Matrix4x4 operator -(Matrix4x4 value1, Matrix4x4 value2);
+        public static Matrix4x4 operator -(Matrix4x4 value);
+        public static Matrix4x4 Subtract(Matrix4x4 value1, Matrix4x4 value2);
+        public override string ToString();
+        public static Matrix4x4 Transform(Matrix4x4 value, Quaternion rotation);
+        public static Matrix4x4 Transpose(Matrix4x4 matrix);
+    }
+    public struct Plane : IEquatable<Plane> {
+        public float D;
+        public Vector3 Normal;
+        public Plane(float x, float y, float z, float d);
+        public Plane(Vector3 normal, float d);
+        public Plane(Vector4 value);
+        public static Plane CreateFromVertices(Vector3 point1, Vector3 point2, Vector3 point3);
+        public static float Dot(Plane plane, Vector4 value);
+        public static float DotCoordinate(Plane plane, Vector3 value);
+        public static float DotNormal(Plane plane, Vector3 value);
+        public override bool Equals(object obj);
+        public bool Equals(Plane other);
+        public override int GetHashCode();
+        public static Plane Normalize(Plane value);
+        public static bool operator ==(Plane value1, Plane value2);
+        public static bool operator !=(Plane value1, Plane value2);
+        public override string ToString();
+        public static Plane Transform(Plane plane, Matrix4x4 matrix);
+        public static Plane Transform(Plane plane, Quaternion rotation);
+    }
+    public struct Quaternion : IEquatable<Quaternion> {
+        public float W;
+        public float X;
+        public float Y;
+        public float Z;
+        public Quaternion(float x, float y, float z, float w);
+        public Quaternion(Vector3 vectorPart, float scalarPart);
+        public static Quaternion Identity { get; }
+        public bool IsIdentity { get; }
+        public static Quaternion Add(Quaternion value1, Quaternion value2);
+        public static Quaternion Concatenate(Quaternion value1, Quaternion value2);
+        public static Quaternion Conjugate(Quaternion value);
+        public static Quaternion CreateFromAxisAngle(Vector3 axis, float angle);
+        public static Quaternion CreateFromRotationMatrix(Matrix4x4 matrix);
+        public static Quaternion CreateFromYawPitchRoll(float yaw, float pitch, float roll);
+        public static Quaternion Divide(Quaternion value1, Quaternion value2);
+        public static float Dot(Quaternion quaternion1, Quaternion quaternion2);
+        public override bool Equals(object obj);
+        public bool Equals(Quaternion other);
+        public override int GetHashCode();
+        public static Quaternion Inverse(Quaternion value);
+        public float Length();
+        public float LengthSquared();
+        public static Quaternion Lerp(Quaternion quaternion1, Quaternion quaternion2, float amount);
+        public static Quaternion Multiply(Quaternion value1, Quaternion value2);
+        public static Quaternion Multiply(Quaternion value1, float value2);
+        public static Quaternion Negate(Quaternion value);
+        public static Quaternion Normalize(Quaternion value);
+        public static Quaternion operator +(Quaternion value1, Quaternion value2);
+        public static Quaternion operator /(Quaternion value1, Quaternion value2);
+        public static bool operator ==(Quaternion value1, Quaternion value2);
+        public static bool operator !=(Quaternion value1, Quaternion value2);
+        public static Quaternion operator *(Quaternion value1, Quaternion value2);
+        public static Quaternion operator *(Quaternion value1, float value2);
+        public static Quaternion operator -(Quaternion value1, Quaternion value2);
+        public static Quaternion operator -(Quaternion value);
+        public static Quaternion Slerp(Quaternion quaternion1, Quaternion quaternion2, float amount);
+        public static Quaternion Subtract(Quaternion value1, Quaternion value2);
+        public override string ToString();
+    }
+    public static class Vector {
+        public static bool IsHardwareAccelerated { get; }
+        public static Vector<T> Abs<T>(Vector<T> value) where T : struct;
+        public static Vector<T> Add<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<T> AndNot<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<Byte> AsVectorByte<T>(Vector<T> value) where T : struct;
+        public static Vector<Double> AsVectorDouble<T>(Vector<T> value) where T : struct;
+        public static Vector<Int16> AsVectorInt16<T>(Vector<T> value) where T : struct;
+        public static Vector<Int32> AsVectorInt32<T>(Vector<T> value) where T : struct;
+        public static Vector<Int64> AsVectorInt64<T>(Vector<T> value) where T : struct;
+        public static Vector<SByte> AsVectorSByte<T>(Vector<T> value) where T : struct;
+        public static Vector<Single> AsVectorSingle<T>(Vector<T> value) where T : struct;
+        public static Vector<UInt16> AsVectorUInt16<T>(Vector<T> value) where T : struct;
+        public static Vector<UInt32> AsVectorUInt32<T>(Vector<T> value) where T : struct;
+        public static Vector<UInt64> AsVectorUInt64<T>(Vector<T> value) where T : struct;
+        public static Vector<T> BitwiseAnd<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<T> BitwiseOr<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<T> ConditionalSelect<T>(Vector<T> condition, Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<Single> ConditionalSelect(Vector<Int32> condition, Vector<Single> left, Vector<Single> right);
+        public static Vector<Double> ConditionalSelect(Vector<Int64> condition, Vector<Double> left, Vector<Double> right);
+        public static Vector<Double> ConvertToDouble(Vector<Int64> value);
+        public static Vector<Double> ConvertToDouble(Vector<UInt64> value);
+        public static Vector<Int32> ConvertToInt32(Vector<Single> value);
+        public static Vector<Int64> ConvertToInt64(Vector<Double> value);
+        public static Vector<Single> ConvertToSingle(Vector<Int32> value);
+        public static Vector<Single> ConvertToSingle(Vector<UInt32> value);
+        public static Vector<UInt32> ConvertToUInt32(Vector<Single> value);
+        public static Vector<UInt64> ConvertToUInt64(Vector<Double> value);
+        public static Vector<T> Divide<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static T Dot<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<T> Equals<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<Int32> Equals(Vector<Int32> left, Vector<Int32> right);
+        public static Vector<Int64> Equals(Vector<Int64> left, Vector<Int64> right);
+        public static Vector<Int64> Equals(Vector<Double> left, Vector<Double> right);
+        public static Vector<Int32> Equals(Vector<Single> left, Vector<Single> right);
+        public static bool EqualsAll<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static bool EqualsAny<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<T> GreaterThan<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<Int32> GreaterThan(Vector<Int32> left, Vector<Int32> right);
+        public static Vector<Int64> GreaterThan(Vector<Int64> left, Vector<Int64> right);
+        public static Vector<Int64> GreaterThan(Vector<Double> left, Vector<Double> right);
+        public static Vector<Int32> GreaterThan(Vector<Single> left, Vector<Single> right);
+        public static bool GreaterThanAll<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static bool GreaterThanAny<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<T> GreaterThanOrEqual<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<Int32> GreaterThanOrEqual(Vector<Int32> left, Vector<Int32> right);
+        public static Vector<Int64> GreaterThanOrEqual(Vector<Int64> left, Vector<Int64> right);
+        public static Vector<Int64> GreaterThanOrEqual(Vector<Double> left, Vector<Double> right);
+        public static Vector<Int32> GreaterThanOrEqual(Vector<Single> left, Vector<Single> right);
+        public static bool GreaterThanOrEqualAll<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static bool GreaterThanOrEqualAny<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<T> LessThan<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<Int32> LessThan(Vector<Int32> left, Vector<Int32> right);
+        public static Vector<Int64> LessThan(Vector<Int64> left, Vector<Int64> right);
+        public static Vector<Int64> LessThan(Vector<Double> left, Vector<Double> right);
+        public static Vector<Int32> LessThan(Vector<Single> left, Vector<Single> right);
+        public static bool LessThanAll<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static bool LessThanAny<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<T> LessThanOrEqual<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<Int32> LessThanOrEqual(Vector<Int32> left, Vector<Int32> right);
+        public static Vector<Int64> LessThanOrEqual(Vector<Int64> left, Vector<Int64> right);
+        public static Vector<Int64> LessThanOrEqual(Vector<Double> left, Vector<Double> right);
+        public static Vector<Int32> LessThanOrEqual(Vector<Single> left, Vector<Single> right);
+        public static bool LessThanOrEqualAll<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static bool LessThanOrEqualAny<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<T> Max<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<T> Min<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<T> Multiply<T>(T left, Vector<T> right) where T : struct;
+        public static Vector<T> Multiply<T>(Vector<T> left, T right) where T : struct;
+        public static Vector<T> Multiply<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static Vector<SByte> Narrow(Vector<Int16> source1, Vector<Int16> source2);
+        public static Vector<Int16> Narrow(Vector<Int32> source1, Vector<Int32> source2);
+        public static Vector<Int32> Narrow(Vector<Int64> source1, Vector<Int64> source2);
+        public static Vector<Byte> Narrow(Vector<UInt16> source1, Vector<UInt16> source2);
+        public static Vector<UInt16> Narrow(Vector<UInt32> source1, Vector<UInt32> source2);
+        public static Vector<UInt32> Narrow(Vector<UInt64> source1, Vector<UInt64> source2);
+        public static Vector<Single> Narrow(Vector<Double> source1, Vector<Double> source2);
+        public static Vector<T> Negate<T>(Vector<T> value) where T : struct;
+        public static Vector<T> OnesComplement<T>(Vector<T> value) where T : struct;
+        public static Vector<T> SquareRoot<T>(Vector<T> value) where T : struct;
+        public static Vector<T> Subtract<T>(Vector<T> left, Vector<T> right) where T : struct;
+        public static void Widen(Vector<SByte> source, out Vector<Int16> dest1, out Vector<Int16> dest2);
+        public static void Widen(Vector<Int16> source, out Vector<Int32> dest1, out Vector<Int32> dest2);
+        public static void Widen(Vector<Int32> source, out Vector<Int64> dest1, out Vector<Int64> dest2);
+        public static void Widen(Vector<Byte> source, out Vector<UInt16> dest1, out Vector<UInt16> dest2);
+        public static void Widen(Vector<UInt16> source, out Vector<UInt32> dest1, out Vector<UInt32> dest2);
+        public static void Widen(Vector<UInt32> source, out Vector<UInt64> dest1, out Vector<UInt64> dest2);
+        public static void Widen(Vector<Single> source, out Vector<Double> dest1, out Vector<Double> dest2);
+        public static Vector<T> Xor<T>(Vector<T> left, Vector<T> right) where T : struct;
+    }
+    public struct Vector<T> : IEquatable<Vector<T>>, IFormattable where T : struct {
+        public Vector(Span<T> values);
+        public Vector(T value);
+        public Vector(T[] values);
+        public Vector(T[] values, int index);
+        public static int Count { get; }
+        public T this[int index] { get; }
+        public static Vector<T> One { get; }
+        public static Vector<T> Zero { get; }
+        public void CopyTo(T[] destination);
+        public void CopyTo(T[] destination, int startIndex);
+        public override bool Equals(object obj);
+        public bool Equals(Vector<T> other);
+        public override int GetHashCode();
+        public static Vector<T> operator +(Vector<T> left, Vector<T> right);
+        public static Vector<T> operator &(Vector<T> left, Vector<T> right);
+        public static Vector<T> operator |(Vector<T> left, Vector<T> right);
+        public static Vector<T> operator /(Vector<T> left, Vector<T> right);
+        public static bool operator ==(Vector<T> left, Vector<T> right);
+        public static Vector<T> operator ^(Vector<T> left, Vector<T> right);
+        public static explicit operator Vector<Byte> (Vector<T> value);
+        public static explicit operator Vector<Double> (Vector<T> value);
+        public static explicit operator Vector<Int16> (Vector<T> value);
+        public static explicit operator Vector<Int32> (Vector<T> value);
+        public static explicit operator Vector<Int64> (Vector<T> value);
+        public static explicit operator Vector<SByte> (Vector<T> value);
+        public static explicit operator Vector<Single> (Vector<T> value);
+        public static explicit operator Vector<UInt16> (Vector<T> value);
+        public static explicit operator Vector<UInt32> (Vector<T> value);
+        public static explicit operator Vector<UInt64> (Vector<T> value);
+        public static bool operator !=(Vector<T> left, Vector<T> right);
+        public static Vector<T> operator *(T factor, Vector<T> value);
+        public static Vector<T> operator *(Vector<T> value, T factor);
+        public static Vector<T> operator *(Vector<T> left, Vector<T> right);
+        public static Vector<T> operator ~(Vector<T> value);
+        public static Vector<T> operator -(Vector<T> left, Vector<T> right);
+        public static Vector<T> operator -(Vector<T> value);
+        public override string ToString();
+        public string ToString(string format);
+        public string ToString(string format, IFormatProvider formatProvider);
+    }
+    public struct Vector2 : IEquatable<Vector2>, IFormattable {
+        public float X;
+        public float Y;
+        public Vector2(float value);
+        public Vector2(float x, float y);
+        public static Vector2 One { get; }
+        public static Vector2 UnitX { get; }
+        public static Vector2 UnitY { get; }
+        public static Vector2 Zero { get; }
+        public static Vector2 Abs(Vector2 value);
+        public static Vector2 Add(Vector2 left, Vector2 right);
+        public static Vector2 Clamp(Vector2 value1, Vector2 min, Vector2 max);
+        public void CopyTo(float[] array);
+        public void CopyTo(float[] array, int index);
+        public static float Distance(Vector2 value1, Vector2 value2);
+        public static float DistanceSquared(Vector2 value1, Vector2 value2);
+        public static Vector2 Divide(Vector2 left, float divisor);
+        public static Vector2 Divide(Vector2 left, Vector2 right);
+        public static float Dot(Vector2 value1, Vector2 value2);
+        public override bool Equals(object obj);
+        public bool Equals(Vector2 other);
+        public override int GetHashCode();
+        public float Length();
+        public float LengthSquared();
+        public static Vector2 Lerp(Vector2 value1, Vector2 value2, float amount);
+        public static Vector2 Max(Vector2 value1, Vector2 value2);
+        public static Vector2 Min(Vector2 value1, Vector2 value2);
+        public static Vector2 Multiply(float left, Vector2 right);
+        public static Vector2 Multiply(Vector2 left, float right);
+        public static Vector2 Multiply(Vector2 left, Vector2 right);
+        public static Vector2 Negate(Vector2 value);
+        public static Vector2 Normalize(Vector2 value);
+        public static Vector2 operator +(Vector2 left, Vector2 right);
+        public static Vector2 operator /(Vector2 value1, float value2);
+        public static Vector2 operator /(Vector2 left, Vector2 right);
+        public static bool operator ==(Vector2 left, Vector2 right);
+        public static bool operator !=(Vector2 left, Vector2 right);
+        public static Vector2 operator *(float left, Vector2 right);
+        public static Vector2 operator *(Vector2 left, float right);
+        public static Vector2 operator *(Vector2 left, Vector2 right);
+        public static Vector2 operator -(Vector2 left, Vector2 right);
+        public static Vector2 operator -(Vector2 value);
+        public static Vector2 Reflect(Vector2 vector, Vector2 normal);
+        public static Vector2 SquareRoot(Vector2 value);
+        public static Vector2 Subtract(Vector2 left, Vector2 right);
+        public override string ToString();
+        public string ToString(string format);
+        public string ToString(string format, IFormatProvider formatProvider);
+        public static Vector2 Transform(Vector2 position, Matrix3x2 matrix);
+        public static Vector2 Transform(Vector2 position, Matrix4x4 matrix);
+        public static Vector2 Transform(Vector2 value, Quaternion rotation);
+        public static Vector2 TransformNormal(Vector2 normal, Matrix3x2 matrix);
+        public static Vector2 TransformNormal(Vector2 normal, Matrix4x4 matrix);
+    }
+    public struct Vector3 : IEquatable<Vector3>, IFormattable {
+        public float X;
+        public float Y;
+        public float Z;
+        public Vector3(float value);
+        public Vector3(float x, float y, float z);
+        public Vector3(Vector2 value, float z);
+        public static Vector3 One { get; }
+        public static Vector3 UnitX { get; }
+        public static Vector3 UnitY { get; }
+        public static Vector3 UnitZ { get; }
+        public static Vector3 Zero { get; }
+        public static Vector3 Abs(Vector3 value);
+        public static Vector3 Add(Vector3 left, Vector3 right);
+        public static Vector3 Clamp(Vector3 value1, Vector3 min, Vector3 max);
+        public void CopyTo(float[] array);
+        public void CopyTo(float[] array, int index);
+        public static Vector3 Cross(Vector3 vector1, Vector3 vector2);
+        public static float Distance(Vector3 value1, Vector3 value2);
+        public static float DistanceSquared(Vector3 value1, Vector3 value2);
+        public static Vector3 Divide(Vector3 left, float divisor);
+        public static Vector3 Divide(Vector3 left, Vector3 right);
+        public static float Dot(Vector3 vector1, Vector3 vector2);
+        public override bool Equals(object obj);
+        public bool Equals(Vector3 other);
+        public override int GetHashCode();
+        public float Length();
+        public float LengthSquared();
+        public static Vector3 Lerp(Vector3 value1, Vector3 value2, float amount);
+        public static Vector3 Max(Vector3 value1, Vector3 value2);
+        public static Vector3 Min(Vector3 value1, Vector3 value2);
+        public static Vector3 Multiply(float left, Vector3 right);
+        public static Vector3 Multiply(Vector3 left, float right);
+        public static Vector3 Multiply(Vector3 left, Vector3 right);
+        public static Vector3 Negate(Vector3 value);
+        public static Vector3 Normalize(Vector3 value);
+        public static Vector3 operator +(Vector3 left, Vector3 right);
+        public static Vector3 operator /(Vector3 value1, float value2);
+        public static Vector3 operator /(Vector3 left, Vector3 right);
+        public static bool operator ==(Vector3 left, Vector3 right);
+        public static bool operator !=(Vector3 left, Vector3 right);
+        public static Vector3 operator *(float left, Vector3 right);
+        public static Vector3 operator *(Vector3 left, float right);
+        public static Vector3 operator *(Vector3 left, Vector3 right);
+        public static Vector3 operator -(Vector3 left, Vector3 right);
+        public static Vector3 operator -(Vector3 value);
+        public static Vector3 Reflect(Vector3 vector, Vector3 normal);
+        public static Vector3 SquareRoot(Vector3 value);
+        public static Vector3 Subtract(Vector3 left, Vector3 right);
+        public override string ToString();
+        public string ToString(string format);
+        public string ToString(string format, IFormatProvider formatProvider);
+        public static Vector3 Transform(Vector3 position, Matrix4x4 matrix);
+        public static Vector3 Transform(Vector3 value, Quaternion rotation);
+        public static Vector3 TransformNormal(Vector3 normal, Matrix4x4 matrix);
+    }
+    public struct Vector4 : IEquatable<Vector4>, IFormattable {
+        public float W;
+        public float X;
+        public float Y;
+        public float Z;
+        public Vector4(float value);
+        public Vector4(float x, float y, float z, float w);
+        public Vector4(Vector2 value, float z, float w);
+        public Vector4(Vector3 value, float w);
+        public static Vector4 One { get; }
+        public static Vector4 UnitW { get; }
+        public static Vector4 UnitX { get; }
+        public static Vector4 UnitY { get; }
+        public static Vector4 UnitZ { get; }
+        public static Vector4 Zero { get; }
+        public static Vector4 Abs(Vector4 value);
+        public static Vector4 Add(Vector4 left, Vector4 right);
+        public static Vector4 Clamp(Vector4 value1, Vector4 min, Vector4 max);
+        public void CopyTo(float[] array);
+        public void CopyTo(float[] array, int index);
+        public static float Distance(Vector4 value1, Vector4 value2);
+        public static float DistanceSquared(Vector4 value1, Vector4 value2);
+        public static Vector4 Divide(Vector4 left, float divisor);
+        public static Vector4 Divide(Vector4 left, Vector4 right);
+        public static float Dot(Vector4 vector1, Vector4 vector2);
+        public override bool Equals(object obj);
+        public bool Equals(Vector4 other);
+        public override int GetHashCode();
+        public float Length();
+        public float LengthSquared();
+        public static Vector4 Lerp(Vector4 value1, Vector4 value2, float amount);
+        public static Vector4 Max(Vector4 value1, Vector4 value2);
+        public static Vector4 Min(Vector4 value1, Vector4 value2);
+        public static Vector4 Multiply(float left, Vector4 right);
+        public static Vector4 Multiply(Vector4 left, float right);
+        public static Vector4 Multiply(Vector4 left, Vector4 right);
+        public static Vector4 Negate(Vector4 value);
+        public static Vector4 Normalize(Vector4 vector);
+        public static Vector4 operator +(Vector4 left, Vector4 right);
+        public static Vector4 operator /(Vector4 value1, float value2);
+        public static Vector4 operator /(Vector4 left, Vector4 right);
+        public static bool operator ==(Vector4 left, Vector4 right);
+        public static bool operator !=(Vector4 left, Vector4 right);
+        public static Vector4 operator *(float left, Vector4 right);
+        public static Vector4 operator *(Vector4 left, float right);
+        public static Vector4 operator *(Vector4 left, Vector4 right);
+        public static Vector4 operator -(Vector4 left, Vector4 right);
+        public static Vector4 operator -(Vector4 value);
+        public static Vector4 SquareRoot(Vector4 value);
+        public static Vector4 Subtract(Vector4 left, Vector4 right);
+        public override string ToString();
+        public string ToString(string format);
+        public string ToString(string format, IFormatProvider formatProvider);
+        public static Vector4 Transform(Vector2 position, Matrix4x4 matrix);
+        public static Vector4 Transform(Vector2 value, Quaternion rotation);
+        public static Vector4 Transform(Vector3 position, Matrix4x4 matrix);
+        public static Vector4 Transform(Vector3 value, Quaternion rotation);
+        public static Vector4 Transform(Vector4 vector, Matrix4x4 matrix);
+        public static Vector4 Transform(Vector4 value, Quaternion rotation);
+    }
 }
 namespace System.Reflection {
     public abstract class Assembly : ICustomAttributeProvider, ISerializable {
+        public virtual Type[] GetForwardedTypes();
     }
     public enum BindingFlags {
+        DoNotWrapExceptions = 33554432,
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct CustomAttributeNamedArgument {
+    public struct CustomAttributeNamedArgument {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct CustomAttributeTypedArgument {
+    public struct CustomAttributeTypedArgument {
     }
+    public abstract class DispatchProxy {
+        protected DispatchProxy();
+        public static T Create<T, TProxy>() where TProxy : DispatchProxy;
+        protected abstract object Invoke(MethodInfo targetMethod, object[] args);
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct InterfaceMapping {
+    public struct InterfaceMapping {
     }
     public abstract class MemberInfo : ICustomAttributeProvider {
+        public virtual bool HasSameMetadataDefinitionAs(MemberInfo other);
     }
     public abstract class MethodBase : MemberInfo {
+        public virtual bool IsConstructedGenericMethod { get; }
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ParameterModifier {
+    public readonly struct ParameterModifier {
     }
     public class TypeDelegator : TypeInfo {
+        public override bool IsByRefLike { get; }
+        public override bool IsGenericMethodParameter { get; }
+        public override bool IsGenericTypeParameter { get; }
+        public override bool IsSZArray { get; }
+        public override bool IsTypeDefinition { get; }
+        public override bool IsVariableBoundArray { get; }
     }
     public abstract class TypeInfo : Type, IReflectableType {
+        protected TypeInfo();
     }
 }
 namespace System.Reflection.Emit {
+    public sealed class AssemblyBuilder : Assembly {
+        public override string FullName { get; }
+        public override bool IsDynamic { get; }
+        public override Module ManifestModule { get; }
+        public static AssemblyBuilder DefineDynamicAssembly(AssemblyName name, AssemblyBuilderAccess access);
+        public static AssemblyBuilder DefineDynamicAssembly(AssemblyName name, AssemblyBuilderAccess access, IEnumerable<CustomAttributeBuilder> assemblyAttributes);
+        public ModuleBuilder DefineDynamicModule(string name);
+        public override bool Equals(object obj);
+        public ModuleBuilder GetDynamicModule(string name);
+        public override int GetHashCode();
+        public override ManifestResourceInfo GetManifestResourceInfo(string resourceName);
+        public override string[] GetManifestResourceNames();
+        public override Stream GetManifestResourceStream(string name);
+        public void SetCustomAttribute(ConstructorInfo con, byte[] binaryAttribute);
+        public void SetCustomAttribute(CustomAttributeBuilder customBuilder);
+    }
+    public enum AssemblyBuilderAccess {
+        Run = 1,
+        RunAndCollect = 9,
+    }
+    public sealed class ConstructorBuilder : ConstructorInfo {
+        public override MethodAttributes Attributes { get; }
+        public override CallingConventions CallingConvention { get; }
+        public override Type DeclaringType { get; }
+        public bool InitLocals { get; set; }
+        public override RuntimeMethodHandle MethodHandle { get; }
+        public override Module Module { get; }
+        public override string Name { get; }
+        public override Type ReflectedType { get; }
+        public ParameterBuilder DefineParameter(int iSequence, ParameterAttributes attributes, string strParamName);
+        public override object[] GetCustomAttributes(bool inherit);
+        public override object[] GetCustomAttributes(Type attributeType, bool inherit);
+        public ILGenerator GetILGenerator();
+        public ILGenerator GetILGenerator(int streamSize);
+        public override MethodImplAttributes GetMethodImplementationFlags();
+        public override ParameterInfo[] GetParameters();
+        public override object Invoke(BindingFlags invokeAttr, Binder binder, object[] parameters, CultureInfo culture);
+        public override object Invoke(object obj, BindingFlags invokeAttr, Binder binder, object[] parameters, CultureInfo culture);
+        public override bool IsDefined(Type attributeType, bool inherit);
+        public void SetCustomAttribute(ConstructorInfo con, byte[] binaryAttribute);
+        public void SetCustomAttribute(CustomAttributeBuilder customBuilder);
+        public void SetImplementationFlags(MethodImplAttributes attributes);
+        public override string ToString();
+    }
+    public class CustomAttributeBuilder {
+        public CustomAttributeBuilder(ConstructorInfo con, object[] constructorArgs);
+        public CustomAttributeBuilder(ConstructorInfo con, object[] constructorArgs, FieldInfo[] namedFields, object[] fieldValues);
+        public CustomAttributeBuilder(ConstructorInfo con, object[] constructorArgs, PropertyInfo[] namedProperties, object[] propertyValues);
+        public CustomAttributeBuilder(ConstructorInfo con, object[] constructorArgs, PropertyInfo[] namedProperties, object[] propertyValues, FieldInfo[] namedFields, object[] fieldValues);
+    }
+    public sealed class DynamicMethod : MethodInfo {
+        public DynamicMethod(string name, MethodAttributes attributes, CallingConventions callingConvention, Type returnType, Type[] parameterTypes, Module m, bool skipVisibility);
+        public DynamicMethod(string name, MethodAttributes attributes, CallingConventions callingConvention, Type returnType, Type[] parameterTypes, Type owner, bool skipVisibility);
+        public DynamicMethod(string name, Type returnType, Type[] parameterTypes);
+        public DynamicMethod(string name, Type returnType, Type[] parameterTypes, bool restrictedSkipVisibility);
+        public DynamicMethod(string name, Type returnType, Type[] parameterTypes, Module m);
+        public DynamicMethod(string name, Type returnType, Type[] parameterTypes, Module m, bool skipVisibility);
+        public DynamicMethod(string name, Type returnType, Type[] parameterTypes, Type owner);
+        public DynamicMethod(string name, Type returnType, Type[] parameterTypes, Type owner, bool skipVisibility);
+        public override MethodAttributes Attributes { get; }
+        public override CallingConventions CallingConvention { get; }
+        public override Type DeclaringType { get; }
+        public bool InitLocals { get; set; }
+        public override RuntimeMethodHandle MethodHandle { get; }
+        public override string Name { get; }
+        public override Type ReflectedType { get; }
+        public override ParameterInfo ReturnParameter { get; }
+        public override Type ReturnType { get; }
+        public override ICustomAttributeProvider ReturnTypeCustomAttributes { get; }
+        public sealed override Delegate CreateDelegate(Type delegateType);
+        public sealed override Delegate CreateDelegate(Type delegateType, object target);
+        public override MethodInfo GetBaseDefinition();
+        public override object[] GetCustomAttributes(bool inherit);
+        public override object[] GetCustomAttributes(Type attributeType, bool inherit);
+        public ILGenerator GetILGenerator();
+        public ILGenerator GetILGenerator(int streamSize);
+        public override MethodImplAttributes GetMethodImplementationFlags();
+        public override ParameterInfo[] GetParameters();
+        public override object Invoke(object obj, BindingFlags invokeAttr, Binder binder, object[] parameters, CultureInfo culture);
+        public override bool IsDefined(Type attributeType, bool inherit);
+        public override string ToString();
+    }
+    public sealed class EnumBuilder : Type {
+        public override Assembly Assembly { get; }
+        public override string AssemblyQualifiedName { get; }
+        public override Type BaseType { get; }
+        public override Type DeclaringType { get; }
+        public override string FullName { get; }
+        public override Guid GUID { get; }
+        public override bool IsByRefLike { get; }
+        public override bool IsConstructedGenericType { get; }
+        public override bool IsSZArray { get; }
+        public override bool IsTypeDefinition { get; }
+        public override bool IsVariableBoundArray { get; }
+        public override Module Module { get; }
+        public override string Name { get; }
+        public override string Namespace { get; }
+        public override Type ReflectedType { get; }
+        public override RuntimeTypeHandle TypeHandle { get; }
+        public FieldBuilder UnderlyingField { get; }
+        public override Type UnderlyingSystemType { get; }
+        public TypeInfo CreateTypeInfo();
+        public FieldBuilder DefineLiteral(string literalName, object literalValue);
+        public override ConstructorInfo[] GetConstructors(BindingFlags bindingAttr);
+        public override object[] GetCustomAttributes(bool inherit);
+        public override object[] GetCustomAttributes(Type attributeType, bool inherit);
+        public override Type GetElementType();
+        public override Type GetEnumUnderlyingType();
+        public override EventInfo GetEvent(string name, BindingFlags bindingAttr);
+        public override EventInfo[] GetEvents();
+        public override EventInfo[] GetEvents(BindingFlags bindingAttr);
+        public override FieldInfo GetField(string name, BindingFlags bindingAttr);
+        public override FieldInfo[] GetFields(BindingFlags bindingAttr);
+        public override Type GetInterface(string name, bool ignoreCase);
+        public override InterfaceMapping GetInterfaceMap(Type interfaceType);
+        public override Type[] GetInterfaces();
+        public override MemberInfo[] GetMember(string name, MemberTypes type, BindingFlags bindingAttr);
+        public override MemberInfo[] GetMembers(BindingFlags bindingAttr);
+        public override MethodInfo[] GetMethods(BindingFlags bindingAttr);
+        public override Type GetNestedType(string name, BindingFlags bindingAttr);
+        public override Type[] GetNestedTypes(BindingFlags bindingAttr);
+        public override PropertyInfo[] GetProperties(BindingFlags bindingAttr);
+        public override object InvokeMember(string name, BindingFlags invokeAttr, Binder binder, object target, object[] args, ParameterModifier[] modifiers, CultureInfo culture, string[] namedParameters);
+        public override bool IsDefined(Type attributeType, bool inherit);
+        public override Type MakeArrayType();
+        public override Type MakeArrayType(int rank);
+        public override Type MakeByRefType();
+        public override Type MakePointerType();
+        public void SetCustomAttribute(ConstructorInfo con, byte[] binaryAttribute);
+        public void SetCustomAttribute(CustomAttributeBuilder customBuilder);
+    }
+    public sealed class EventBuilder {
+        public void AddOtherMethod(MethodBuilder mdBuilder);
+        public void SetAddOnMethod(MethodBuilder mdBuilder);
+        public void SetCustomAttribute(ConstructorInfo con, byte[] binaryAttribute);
+        public void SetCustomAttribute(CustomAttributeBuilder customBuilder);
+        public void SetRaiseMethod(MethodBuilder mdBuilder);
+        public void SetRemoveOnMethod(MethodBuilder mdBuilder);
+    }
+    public sealed class FieldBuilder : FieldInfo {
+        public override FieldAttributes Attributes { get; }
+        public override Type DeclaringType { get; }
+        public override RuntimeFieldHandle FieldHandle { get; }
+        public override Type FieldType { get; }
+        public override string Name { get; }
+        public override Type ReflectedType { get; }
+        public override object[] GetCustomAttributes(bool inherit);
+        public override object[] GetCustomAttributes(Type attributeType, bool inherit);
+        public override object GetValue(object obj);
+        public override bool IsDefined(Type attributeType, bool inherit);
+        public void SetConstant(object defaultValue);
+        public void SetCustomAttribute(ConstructorInfo con, byte[] binaryAttribute);
+        public void SetCustomAttribute(CustomAttributeBuilder customBuilder);
+        public void SetOffset(int iOffset);
+        public override void SetValue(object obj, object val, BindingFlags invokeAttr, Binder binder, CultureInfo culture);
+    }
+    public sealed class GenericTypeParameterBuilder : Type {
+        public override Assembly Assembly { get; }
+        public override string AssemblyQualifiedName { get; }
+        public override Type BaseType { get; }
+        public override bool ContainsGenericParameters { get; }
+        public override MethodBase DeclaringMethod { get; }
+        public override Type DeclaringType { get; }
+        public override string FullName { get; }
+        public override GenericParameterAttributes GenericParameterAttributes { get; }
+        public override int GenericParameterPosition { get; }
+        public override Guid GUID { get; }
+        public override bool IsByRefLike { get; }
+        public override bool IsConstructedGenericType { get; }
+        public override bool IsGenericParameter { get; }
+        public override bool IsGenericType { get; }
+        public override bool IsGenericTypeDefinition { get; }
+        public override bool IsSZArray { get; }
+        public override bool IsTypeDefinition { get; }
+        public override bool IsVariableBoundArray { get; }
+        public override Module Module { get; }
+        public override string Name { get; }
+        public override string Namespace { get; }
+        public override Type ReflectedType { get; }
+        public override RuntimeTypeHandle TypeHandle { get; }
+        public override Type UnderlyingSystemType { get; }
+        public override bool Equals(object o);
+        public override ConstructorInfo[] GetConstructors(BindingFlags bindingAttr);
+        public override object[] GetCustomAttributes(bool inherit);
+        public override object[] GetCustomAttributes(Type attributeType, bool inherit);
+        public override Type GetElementType();
+        public override EventInfo GetEvent(string name, BindingFlags bindingAttr);
+        public override EventInfo[] GetEvents();
+        public override EventInfo[] GetEvents(BindingFlags bindingAttr);
+        public override FieldInfo GetField(string name, BindingFlags bindingAttr);
+        public override FieldInfo[] GetFields(BindingFlags bindingAttr);
+        public override Type[] GetGenericArguments();
+        public override Type GetGenericTypeDefinition();
+        public override int GetHashCode();
+        public override Type GetInterface(string name, bool ignoreCase);
+        public override InterfaceMapping GetInterfaceMap(Type interfaceType);
+        public override Type[] GetInterfaces();
+        public override MemberInfo[] GetMember(string name, MemberTypes type, BindingFlags bindingAttr);
+        public override MemberInfo[] GetMembers(BindingFlags bindingAttr);
+        public override MethodInfo[] GetMethods(BindingFlags bindingAttr);
+        public override Type GetNestedType(string name, BindingFlags bindingAttr);
+        public override Type[] GetNestedTypes(BindingFlags bindingAttr);
+        public override PropertyInfo[] GetProperties(BindingFlags bindingAttr);
+        public override object InvokeMember(string name, BindingFlags invokeAttr, Binder binder, object target, object[] args, ParameterModifier[] modifiers, CultureInfo culture, string[] namedParameters);
+        public override bool IsAssignableFrom(Type c);
+        public override bool IsDefined(Type attributeType, bool inherit);
+        public override bool IsSubclassOf(Type c);
+        public override Type MakeArrayType();
+        public override Type MakeArrayType(int rank);
+        public override Type MakeByRefType();
+        public override Type MakeGenericType(params Type[] typeArguments);
+        public override Type MakePointerType();
+        public void SetBaseTypeConstraint(Type baseTypeConstraint);
+        public void SetCustomAttribute(ConstructorInfo con, byte[] binaryAttribute);
+        public void SetCustomAttribute(CustomAttributeBuilder customBuilder);
+        public void SetGenericParameterAttributes(GenericParameterAttributes genericParameterAttributes);
+        public void SetInterfaceConstraints(params Type[] interfaceConstraints);
+        public override string ToString();
+    }
+    public class ILGenerator {
+        public virtual int ILOffset { get; }
+        public virtual void BeginCatchBlock(Type exceptionType);
+        public virtual void BeginExceptFilterBlock();
+        public virtual Label BeginExceptionBlock();
+        public virtual void BeginFaultBlock();
+        public virtual void BeginFinallyBlock();
+        public virtual void BeginScope();
+        public virtual LocalBuilder DeclareLocal(Type localType);
+        public virtual LocalBuilder DeclareLocal(Type localType, bool pinned);
+        public virtual Label DefineLabel();
+        public virtual void Emit(OpCode opcode);
+        public virtual void Emit(OpCode opcode, byte arg);
+        public virtual void Emit(OpCode opcode, ConstructorInfo con);
+        public virtual void Emit(OpCode opcode, double arg);
+        public virtual void Emit(OpCode opcode, FieldInfo field);
+        public virtual void Emit(OpCode opcode, short arg);
+        public virtual void Emit(OpCode opcode, int arg);
+        public virtual void Emit(OpCode opcode, long arg);
+        public virtual void Emit(OpCode opcode, Label label);
+        public virtual void Emit(OpCode opcode, Label[] labels);
+        public virtual void Emit(OpCode opcode, LocalBuilder local);
+        public virtual void Emit(OpCode opcode, MethodInfo meth);
+        public void Emit(OpCode opcode, sbyte arg);
+        public virtual void Emit(OpCode opcode, SignatureHelper signature);
+        public virtual void Emit(OpCode opcode, float arg);
+        public virtual void Emit(OpCode opcode, string str);
+        public virtual void Emit(OpCode opcode, Type cls);
+        public virtual void EmitCall(OpCode opcode, MethodInfo methodInfo, Type[] optionalParameterTypes);
+        public virtual void EmitCalli(OpCode opcode, CallingConvention unmanagedCallConv, Type returnType, Type[] parameterTypes);
+        public virtual void EmitCalli(OpCode opcode, CallingConventions callingConvention, Type returnType, Type[] parameterTypes, Type[] optionalParameterTypes);
+        public virtual void EmitWriteLine(FieldInfo fld);
+        public virtual void EmitWriteLine(LocalBuilder localBuilder);
+        public virtual void EmitWriteLine(string value);
+        public virtual void EndExceptionBlock();
+        public virtual void EndScope();
+        public virtual void MarkLabel(Label loc);
+        public virtual void ThrowException(Type excType);
+        public virtual void UsingNamespace(string usingNamespace);
+    }
+    public struct Label {
+        public bool Equals(Label obj);
+        public override bool Equals(object obj);
+        public override int GetHashCode();
+        public static bool operator ==(Label a, Label b);
+        public static bool operator !=(Label a, Label b);
+    }
+    public sealed class LocalBuilder : LocalVariableInfo {
+        public override bool IsPinned { get; }
+        public override int LocalIndex { get; }
+        public override Type LocalType { get; }
+    }
+    public sealed class MethodBuilder : MethodInfo {
+        public override MethodAttributes Attributes { get; }
+        public override CallingConventions CallingConvention { get; }
+        public override bool ContainsGenericParameters { get; }
+        public override Type DeclaringType { get; }
+        public bool InitLocals { get; set; }
+        public override bool IsConstructedGenericMethod { get; }
+        public override bool IsGenericMethod { get; }
+        public override bool IsGenericMethodDefinition { get; }
+        public override RuntimeMethodHandle MethodHandle { get; }
+        public override Module Module { get; }
+        public override string Name { get; }
+        public override Type ReflectedType { get; }
+        public override ParameterInfo ReturnParameter { get; }
+        public override Type ReturnType { get; }
+        public override ICustomAttributeProvider ReturnTypeCustomAttributes { get; }
+        public GenericTypeParameterBuilder[] DefineGenericParameters(params string[] names);
+        public ParameterBuilder DefineParameter(int position, ParameterAttributes attributes, string strParamName);
+        public override bool Equals(object obj);
+        public override MethodInfo GetBaseDefinition();
+        public override object[] GetCustomAttributes(bool inherit);
+        public override object[] GetCustomAttributes(Type attributeType, bool inherit);
+        public override Type[] GetGenericArguments();
+        public override MethodInfo GetGenericMethodDefinition();
+        public override int GetHashCode();
+        public ILGenerator GetILGenerator();
+        public ILGenerator GetILGenerator(int size);
+        public override MethodImplAttributes GetMethodImplementationFlags();
+        public override ParameterInfo[] GetParameters();
+        public override object Invoke(object obj, BindingFlags invokeAttr, Binder binder, object[] parameters, CultureInfo culture);
+        public override bool IsDefined(Type attributeType, bool inherit);
+        public override MethodInfo MakeGenericMethod(params Type[] typeArguments);
+        public void SetCustomAttribute(ConstructorInfo con, byte[] binaryAttribute);
+        public void SetCustomAttribute(CustomAttributeBuilder customBuilder);
+        public void SetImplementationFlags(MethodImplAttributes attributes);
+        public void SetParameters(params Type[] parameterTypes);
+        public void SetReturnType(Type returnType);
+        public void SetSignature(Type returnType, Type[] returnTypeRequiredCustomModifiers, Type[] returnTypeOptionalCustomModifiers, Type[] parameterTypes, Type[][] parameterTypeRequiredCustomModifiers, Type[][] parameterTypeOptionalCustomModifiers);
+        public override string ToString();
+    }
+    public class ModuleBuilder : Module {
+        public override Assembly Assembly { get; }
+        public override string FullyQualifiedName { get; }
+        public override string Name { get; }
+        public void CreateGlobalFunctions();
+        public EnumBuilder DefineEnum(string name, TypeAttributes visibility, Type underlyingType);
+        public MethodBuilder DefineGlobalMethod(string name, MethodAttributes attributes, CallingConventions callingConvention, Type returnType, Type[] parameterTypes);
+        public MethodBuilder DefineGlobalMethod(string name, MethodAttributes attributes, CallingConventions callingConvention, Type returnType, Type[] requiredReturnTypeCustomModifiers, Type[] optionalReturnTypeCustomModifiers, Type[] parameterTypes, Type[][] requiredParameterTypeCustomModifiers, Type[][] optionalParameterTypeCustomModifiers);
+        public MethodBuilder DefineGlobalMethod(string name, MethodAttributes attributes, Type returnType, Type[] parameterTypes);
+        public FieldBuilder DefineInitializedData(string name, byte[] data, FieldAttributes attributes);
+        public TypeBuilder DefineType(string name);
+        public TypeBuilder DefineType(string name, TypeAttributes attr);
+        public TypeBuilder DefineType(string name, TypeAttributes attr, Type parent);
+        public TypeBuilder DefineType(string name, TypeAttributes attr, Type parent, int typesize);
+        public TypeBuilder DefineType(string name, TypeAttributes attr, Type parent, PackingSize packsize);
+        public TypeBuilder DefineType(string name, TypeAttributes attr, Type parent, PackingSize packingSize, int typesize);
+        public TypeBuilder DefineType(string name, TypeAttributes attr, Type parent, Type[] interfaces);
+        public FieldBuilder DefineUninitializedData(string name, int size, FieldAttributes attributes);
+        public override bool Equals(object obj);
+        public MethodInfo GetArrayMethod(Type arrayClass, string methodName, CallingConventions callingConvention, Type returnType, Type[] parameterTypes);
+        public override int GetHashCode();
+        public void SetCustomAttribute(ConstructorInfo con, byte[] binaryAttribute);
+        public void SetCustomAttribute(CustomAttributeBuilder customBuilder);
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct OpCode {
+    public struct OpCode {
     }
+    public class ParameterBuilder {
+        public virtual int Attributes { get; }
+        public bool IsIn { get; }
+        public bool IsOptional { get; }
+        public bool IsOut { get; }
+        public virtual string Name { get; }
+        public virtual int Position { get; }
+        public virtual void SetConstant(object defaultValue);
+        public void SetCustomAttribute(ConstructorInfo con, byte[] binaryAttribute);
+        public void SetCustomAttribute(CustomAttributeBuilder customBuilder);
+    }
+    public sealed class PropertyBuilder : PropertyInfo {
+        public override PropertyAttributes Attributes { get; }
+        public override bool CanRead { get; }
+        public override bool CanWrite { get; }
+        public override Type DeclaringType { get; }
+        public override Module Module { get; }
+        public override string Name { get; }
+        public override Type PropertyType { get; }
+        public override Type ReflectedType { get; }
+        public void AddOtherMethod(MethodBuilder mdBuilder);
+        public override MethodInfo[] GetAccessors(bool nonPublic);
+        public override object[] GetCustomAttributes(bool inherit);
+        public override object[] GetCustomAttributes(Type attributeType, bool inherit);
+        public override MethodInfo GetGetMethod(bool nonPublic);
+        public override ParameterInfo[] GetIndexParameters();
+        public override MethodInfo GetSetMethod(bool nonPublic);
+        public override object GetValue(object obj, BindingFlags invokeAttr, Binder binder, object[] index, CultureInfo culture);
+        public override object GetValue(object obj, object[] index);
+        public override bool IsDefined(Type attributeType, bool inherit);
+        public void SetConstant(object defaultValue);
+        public void SetCustomAttribute(ConstructorInfo con, byte[] binaryAttribute);
+        public void SetCustomAttribute(CustomAttributeBuilder customBuilder);
+        public void SetGetMethod(MethodBuilder mdBuilder);
+        public void SetSetMethod(MethodBuilder mdBuilder);
+        public override void SetValue(object obj, object value, BindingFlags invokeAttr, Binder binder, object[] index, CultureInfo culture);
+        public override void SetValue(object obj, object value, object[] index);
+    }
+    public sealed class SignatureHelper {
+        public void AddArgument(Type clsArgument);
+        public void AddArgument(Type argument, bool pinned);
+        public void AddArgument(Type argument, Type[] requiredCustomModifiers, Type[] optionalCustomModifiers);
+        public void AddArguments(Type[] arguments, Type[][] requiredCustomModifiers, Type[][] optionalCustomModifiers);
+        public void AddSentinel();
+        public override bool Equals(object obj);
+        public static SignatureHelper GetFieldSigHelper(Module mod);
+        public override int GetHashCode();
+        public static SignatureHelper GetLocalVarSigHelper();
+        public static SignatureHelper GetLocalVarSigHelper(Module mod);
+        public static SignatureHelper GetMethodSigHelper(CallingConventions callingConvention, Type returnType);
+        public static SignatureHelper GetMethodSigHelper(Module mod, CallingConventions callingConvention, Type returnType);
+        public static SignatureHelper GetMethodSigHelper(Module mod, Type returnType, Type[] parameterTypes);
+        public static SignatureHelper GetPropertySigHelper(Module mod, CallingConventions callingConvention, Type returnType, Type[] requiredReturnTypeCustomModifiers, Type[] optionalReturnTypeCustomModifiers, Type[] parameterTypes, Type[][] requiredParameterTypeCustomModifiers, Type[][] optionalParameterTypeCustomModifiers);
+        public static SignatureHelper GetPropertySigHelper(Module mod, Type returnType, Type[] parameterTypes);
+        public static SignatureHelper GetPropertySigHelper(Module mod, Type returnType, Type[] requiredReturnTypeCustomModifiers, Type[] optionalReturnTypeCustomModifiers, Type[] parameterTypes, Type[][] requiredParameterTypeCustomModifiers, Type[][] optionalParameterTypeCustomModifiers);
+        public byte[] GetSignature();
+        public override string ToString();
+    }
+    public sealed class TypeBuilder : Type {
+        public const int UnspecifiedTypeSize = 0;
+        public override Assembly Assembly { get; }
+        public override string AssemblyQualifiedName { get; }
+        public override Type BaseType { get; }
+        public override MethodBase DeclaringMethod { get; }
+        public override Type DeclaringType { get; }
+        public override string FullName { get; }
+        public override GenericParameterAttributes GenericParameterAttributes { get; }
+        public override int GenericParameterPosition { get; }
+        public override Guid GUID { get; }
+        public override bool IsByRefLike { get; }
+        public override bool IsConstructedGenericType { get; }
+        public override bool IsGenericParameter { get; }
+        public override bool IsGenericType { get; }
+        public override bool IsGenericTypeDefinition { get; }
+        public override bool IsSecurityCritical { get; }
+        public override bool IsSecuritySafeCritical { get; }
+        public override bool IsSecurityTransparent { get; }
+        public override bool IsSZArray { get; }
+        public override bool IsTypeDefinition { get; }
+        public override bool IsVariableBoundArray { get; }
+        public override Module Module { get; }
+        public override string Name { get; }
+        public override string Namespace { get; }
+        public PackingSize PackingSize { get; }
+        public override Type ReflectedType { get; }
+        public int Size { get; }
+        public override RuntimeTypeHandle TypeHandle { get; }
+        public override Type UnderlyingSystemType { get; }
+        public void AddInterfaceImplementation(Type interfaceType);
+        public Type CreateType();
+        public TypeInfo CreateTypeInfo();
+        public ConstructorBuilder DefineConstructor(MethodAttributes attributes, CallingConventions callingConvention, Type[] parameterTypes);
+        public ConstructorBuilder DefineConstructor(MethodAttributes attributes, CallingConventions callingConvention, Type[] parameterTypes, Type[][] requiredCustomModifiers, Type[][] optionalCustomModifiers);
+        public ConstructorBuilder DefineDefaultConstructor(MethodAttributes attributes);
+        public EventBuilder DefineEvent(string name, EventAttributes attributes, Type eventtype);
+        public FieldBuilder DefineField(string fieldName, Type type, FieldAttributes attributes);
+        public FieldBuilder DefineField(string fieldName, Type type, Type[] requiredCustomModifiers, Type[] optionalCustomModifiers, FieldAttributes attributes);
+        public GenericTypeParameterBuilder[] DefineGenericParameters(params string[] names);
+        public FieldBuilder DefineInitializedData(string name, byte[] data, FieldAttributes attributes);
+        public MethodBuilder DefineMethod(string name, MethodAttributes attributes);
+        public MethodBuilder DefineMethod(string name, MethodAttributes attributes, CallingConventions callingConvention);
+        public MethodBuilder DefineMethod(string name, MethodAttributes attributes, CallingConventions callingConvention, Type returnType, Type[] parameterTypes);
+        public MethodBuilder DefineMethod(string name, MethodAttributes attributes, CallingConventions callingConvention, Type returnType, Type[] returnTypeRequiredCustomModifiers, Type[] returnTypeOptionalCustomModifiers, Type[] parameterTypes, Type[][] parameterTypeRequiredCustomModifiers, Type[][] parameterTypeOptionalCustomModifiers);
+        public MethodBuilder DefineMethod(string name, MethodAttributes attributes, Type returnType, Type[] parameterTypes);
+        public void DefineMethodOverride(MethodInfo methodInfoBody, MethodInfo methodInfoDeclaration);
+        public TypeBuilder DefineNestedType(string name);
+        public TypeBuilder DefineNestedType(string name, TypeAttributes attr);
+        public TypeBuilder DefineNestedType(string name, TypeAttributes attr, Type parent);
+        public TypeBuilder DefineNestedType(string name, TypeAttributes attr, Type parent, int typeSize);
+        public TypeBuilder DefineNestedType(string name, TypeAttributes attr, Type parent, PackingSize packSize);
+        public TypeBuilder DefineNestedType(string name, TypeAttributes attr, Type parent, PackingSize packSize, int typeSize);
+        public TypeBuilder DefineNestedType(string name, TypeAttributes attr, Type parent, Type[] interfaces);
+        public PropertyBuilder DefineProperty(string name, PropertyAttributes attributes, CallingConventions callingConvention, Type returnType, Type[] parameterTypes);
+        public PropertyBuilder DefineProperty(string name, PropertyAttributes attributes, CallingConventions callingConvention, Type returnType, Type[] returnTypeRequiredCustomModifiers, Type[] returnTypeOptionalCustomModifiers, Type[] parameterTypes, Type[][] parameterTypeRequiredCustomModifiers, Type[][] parameterTypeOptionalCustomModifiers);
+        public PropertyBuilder DefineProperty(string name, PropertyAttributes attributes, Type returnType, Type[] parameterTypes);
+        public PropertyBuilder DefineProperty(string name, PropertyAttributes attributes, Type returnType, Type[] returnTypeRequiredCustomModifiers, Type[] returnTypeOptionalCustomModifiers, Type[] parameterTypes, Type[][] parameterTypeRequiredCustomModifiers, Type[][] parameterTypeOptionalCustomModifiers);
+        public ConstructorBuilder DefineTypeInitializer();
+        public FieldBuilder DefineUninitializedData(string name, int size, FieldAttributes attributes);
+        public static ConstructorInfo GetConstructor(Type type, ConstructorInfo constructor);
+        public override ConstructorInfo[] GetConstructors(BindingFlags bindingAttr);
+        public override object[] GetCustomAttributes(bool inherit);
+        public override object[] GetCustomAttributes(Type attributeType, bool inherit);
+        public override Type GetElementType();
+        public override EventInfo GetEvent(string name, BindingFlags bindingAttr);
+        public override EventInfo[] GetEvents();
+        public override EventInfo[] GetEvents(BindingFlags bindingAttr);
+        public override FieldInfo GetField(string name, BindingFlags bindingAttr);
+        public static FieldInfo GetField(Type type, FieldInfo field);
+        public override FieldInfo[] GetFields(BindingFlags bindingAttr);
+        public override Type[] GetGenericArguments();
+        public override Type GetGenericTypeDefinition();
+        public override Type GetInterface(string name, bool ignoreCase);
+        public override InterfaceMapping GetInterfaceMap(Type interfaceType);
+        public override Type[] GetInterfaces();
+        public override MemberInfo[] GetMember(string name, MemberTypes type, BindingFlags bindingAttr);
+        public override MemberInfo[] GetMembers(BindingFlags bindingAttr);
+        public static MethodInfo GetMethod(Type type, MethodInfo method);
+        public override MethodInfo[] GetMethods(BindingFlags bindingAttr);
+        public override Type GetNestedType(string name, BindingFlags bindingAttr);
+        public override Type[] GetNestedTypes(BindingFlags bindingAttr);
+        public override PropertyInfo[] GetProperties(BindingFlags bindingAttr);
+        public override object InvokeMember(string name, BindingFlags invokeAttr, Binder binder, object target, object[] args, ParameterModifier[] modifiers, CultureInfo culture, string[] namedParameters);
+        public override bool IsAssignableFrom(Type c);
+        public bool IsCreated();
+        public override bool IsDefined(Type attributeType, bool inherit);
+        public override bool IsSubclassOf(Type c);
+        public override Type MakeArrayType();
+        public override Type MakeArrayType(int rank);
+        public override Type MakeByRefType();
+        public override Type MakeGenericType(params Type[] typeArguments);
+        public override Type MakePointerType();
+        public void SetCustomAttribute(ConstructorInfo con, byte[] binaryAttribute);
+        public void SetCustomAttribute(CustomAttributeBuilder customBuilder);
+        public void SetParent(Type parent);
+        public override string ToString();
+    }
 }
 namespace System.Runtime.CompilerServices {
+    public sealed class AsyncMethodBuilderAttribute : Attribute {
+        public AsyncMethodBuilderAttribute(Type builderType);
+        public Type BuilderType { get; }
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct AsyncTaskMethodBuilder {
+    public struct AsyncTaskMethodBuilder {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct AsyncTaskMethodBuilder<TResult> {
+    public struct AsyncTaskMethodBuilder<TResult> {
     }
+    public struct AsyncValueTaskMethodBuilder {
+        public ValueTask Task { get; }
+        public void AwaitOnCompleted<TAwaiter, TStateMachine>(ref TAwaiter awaiter, ref TStateMachine stateMachine) where TAwaiter : INotifyCompletion where TStateMachine : IAsyncStateMachine;
+        public void AwaitUnsafeOnCompleted<TAwaiter, TStateMachine>(ref TAwaiter awaiter, ref TStateMachine stateMachine) where TAwaiter : ICriticalNotifyCompletion where TStateMachine : IAsyncStateMachine;
+        public static AsyncValueTaskMethodBuilder Create();
+        public void SetException(Exception exception);
+        public void SetResult();
+        public void SetStateMachine(IAsyncStateMachine stateMachine);
+        public void Start<TStateMachine>(ref TStateMachine stateMachine) where TStateMachine : IAsyncStateMachine;
+    }
+    public struct AsyncValueTaskMethodBuilder<TResult> {
+        public ValueTask<TResult> Task { get; }
+        public void AwaitOnCompleted<TAwaiter, TStateMachine>(ref TAwaiter awaiter, ref TStateMachine stateMachine) where TAwaiter : INotifyCompletion where TStateMachine : IAsyncStateMachine;
+        public void AwaitUnsafeOnCompleted<TAwaiter, TStateMachine>(ref TAwaiter awaiter, ref TStateMachine stateMachine) where TAwaiter : ICriticalNotifyCompletion where TStateMachine : IAsyncStateMachine;
+        public static AsyncValueTaskMethodBuilder<TResult> Create();
+        public void SetException(Exception exception);
+        public void SetResult(TResult result);
+        public void SetStateMachine(IAsyncStateMachine stateMachine);
+        public void Start<TStateMachine>(ref TStateMachine stateMachine) where TStateMachine : IAsyncStateMachine;
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct AsyncVoidMethodBuilder {
+    public struct AsyncVoidMethodBuilder {
     }
-    public sealed class ConditionalWeakTable<TKey, TValue> where TKey : class where TValue : class {
+    public sealed class ConditionalWeakTable<TKey, TValue> : IEnumerable, IEnumerable<KeyValuePair<TKey, TValue>> where TKey : class where TValue : class {
+        public void AddOrUpdate(TKey key, TValue value);
+        public void Clear();
+        IEnumerator<KeyValuePair<TKey, TValue>> System.Collections.Generic.IEnumerable<System.Collections.Generic.KeyValuePair<TKey,TValue>>.GetEnumerator();
+        IEnumerator System.Collections.IEnumerable.GetEnumerator();
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ConfiguredTaskAwaitable {
+    public readonly struct ConfiguredTaskAwaitable {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-        public struct ConfiguredTaskAwaiter : ICriticalNotifyCompletion, INotifyCompletion {
+        public readonly struct ConfiguredTaskAwaiter : ICriticalNotifyCompletion, INotifyCompletion {
         }
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ConfiguredTaskAwaitable<TResult> {
+    public readonly struct ConfiguredTaskAwaitable<TResult> {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-        public struct ConfiguredTaskAwaiter : ICriticalNotifyCompletion, INotifyCompletion {
+        public readonly struct ConfiguredTaskAwaiter : ICriticalNotifyCompletion, INotifyCompletion {
         }
     }
+    public readonly struct ConfiguredValueTaskAwaitable {
+        public readonly struct ConfiguredValueTaskAwaiter : ICriticalNotifyCompletion, INotifyCompletion {
+            public bool IsCompleted { get; }
+            public void GetResult();
+            public void OnCompleted(Action continuation);
+            public void UnsafeOnCompleted(Action continuation);
+        }
+        public ConfiguredValueTaskAwaitable.ConfiguredValueTaskAwaiter GetAwaiter();
+    }
+    public readonly struct ConfiguredValueTaskAwaitable<TResult> {
+        public readonly struct ConfiguredValueTaskAwaiter : ICriticalNotifyCompletion, INotifyCompletion {
+            public bool IsCompleted { get; }
+            public TResult GetResult();
+            public void OnCompleted(Action continuation);
+            public void UnsafeOnCompleted(Action continuation);
+        }
+        public ConfiguredValueTaskAwaitable<TResult>.ConfiguredValueTaskAwaiter GetAwaiter();
+    }
+    public sealed class IsByRefLikeAttribute : Attribute {
+        public IsByRefLikeAttribute();
+    }
+    public sealed class IsReadOnlyAttribute : Attribute {
+        public IsReadOnlyAttribute();
+    }
+    public interface ITuple {
+        object this[int index] { get; }
+        int Length { get; }
+    }
+    public static class RuntimeFeature {
+        public const string PortablePdb = "PortablePdb";
+        public static bool IsSupported(string feature);
+    }
     public static class RuntimeHelpers {
+        public static object GetUninitializedObject(Type type);
+        public static bool IsReferenceOrContainsReferences<T>();
+        public static bool TryEnsureSufficientExecutionStack();
     }
     public sealed class RuntimeWrappedException : Exception {
+        public RuntimeWrappedException(object thrownObject);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct TaskAwaiter : ICriticalNotifyCompletion, INotifyCompletion {
+    public readonly struct TaskAwaiter : ICriticalNotifyCompletion, INotifyCompletion {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct TaskAwaiter<TResult> : ICriticalNotifyCompletion, INotifyCompletion {
+    public readonly struct TaskAwaiter<TResult> : ICriticalNotifyCompletion, INotifyCompletion {
     }
+    public readonly struct ValueTaskAwaiter : ICriticalNotifyCompletion, INotifyCompletion {
+        public bool IsCompleted { get; }
+        public void GetResult();
+        public void OnCompleted(Action continuation);
+        public void UnsafeOnCompleted(Action continuation);
+    }
+    public readonly struct ValueTaskAwaiter<TResult> : ICriticalNotifyCompletion, INotifyCompletion {
+        public bool IsCompleted { get; }
+        public TResult GetResult();
+        public void OnCompleted(Action continuation);
+        public void UnsafeOnCompleted(Action continuation);
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential, Size=1)]
-    public struct YieldAwaitable {
+    public readonly struct YieldAwaitable {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential, Size=1)]
-        public struct YieldAwaiter : ICriticalNotifyCompletion, INotifyCompletion {
+        public readonly struct YieldAwaiter : ICriticalNotifyCompletion, INotifyCompletion {
         }
     }
 }
 namespace System.Runtime.ExceptionServices {
     public sealed class ExceptionDispatchInfo {
+        public static void Throw(Exception source);
     }
 }
 namespace System.Runtime.InteropServices {
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ArrayWithOffset {
+    public struct ArrayWithOffset {
     }
+    public sealed class AutomationProxyAttribute : Attribute {
+        public AutomationProxyAttribute(bool val);
+        public bool Value { get; }
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct GCHandle {
+    public struct GCHandle {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct HandleRef {
+    public struct HandleRef {
     }
+    public sealed class ImportedFromTypeLibAttribute : Attribute {
+        public ImportedFromTypeLibAttribute(string tlbFile);
+        public string Value { get; }
+    }
+    public sealed class ManagedToNativeComInteropStubAttribute : Attribute {
+        public ManagedToNativeComInteropStubAttribute(Type classType, string methodName);
+        public Type ClassType { get; }
+        public string MethodName { get; }
+    }
     public static class Marshal {
+        public static Guid GenerateGuidForType(Type type);
+        public static string GenerateProgIdForType(Type type);
+        public static object GetComObjectData(object obj, object key);
+        public static IntPtr GetHINSTANCE(Module m);
+        public static IntPtr GetIDispatchForObject(object o);
+        public static object GetTypedObjectForIUnknown(IntPtr pUnk, Type t);
+        public static string PtrToStringUTF8(IntPtr ptr);
+        public static string PtrToStringUTF8(IntPtr ptr, int byteLen);
+        public static bool SetComObjectData(object obj, object key, object data);
+        public static IntPtr StringToCoTaskMemUTF8(string s);
+        public static void ZeroFreeCoTaskMemUTF8(IntPtr s);
     }
+    public static class MemoryMarshal {
+        public static Span<byte> AsBytes<T>(Span<T> span) where T : struct;
+        public static ReadOnlySpan<byte> AsBytes<T>(ReadOnlySpan<T> span) where T : struct;
+        public static Memory<T> AsMemory<T>(ReadOnlyMemory<T> memory);
+        public static Span<TTo> Cast<TFrom, TTo>(Span<TFrom> span) where TFrom : struct where TTo : struct;
+        public static ReadOnlySpan<TTo> Cast<TFrom, TTo>(ReadOnlySpan<TFrom> span) where TFrom : struct where TTo : struct;
+        public static Memory<T> CreateFromPinnedArray<T>(T[] array, int start, int length);
+        public static ReadOnlySpan<T> CreateReadOnlySpan<T>(ref T reference, int length);
+        public static Span<T> CreateSpan<T>(ref T reference, int length);
+        public static ref T GetReference<T>(Span<T> span);
+        public static ref T GetReference<T>(ReadOnlySpan<T> span);
+        public static T Read<T>(ReadOnlySpan<byte> source) where T : struct;
+        public static IEnumerable<T> ToEnumerable<T>(ReadOnlyMemory<T> memory);
+        public static bool TryGetArray<T>(ReadOnlyMemory<T> memory, out ArraySegment<T> segment);
+        public static bool TryGetString(ReadOnlyMemory<char> memory, out string text, out int start, out int length);
+        public static bool TryRead<T>(ReadOnlySpan<byte> source, out T value) where T : struct;
+        public static bool TryWrite<T>(Span<byte> destination, ref T value) where T : struct;
+        public static void Write<T>(Span<byte> destination, ref T value) where T : struct;
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct OSPlatform : IEquatable<OSPlatform> {
+    public readonly struct OSPlatform : IEquatable<OSPlatform> {
     }
+    public sealed class TypeLibFuncAttribute : Attribute {
+        public TypeLibFuncAttribute(short flags);
+        public TypeLibFuncAttribute(TypeLibFuncFlags flags);
+        public TypeLibFuncFlags Value { get; }
+    }
+    public enum TypeLibFuncFlags {
+        FBindable = 4,
+        FDefaultBind = 32,
+        FDefaultCollelem = 256,
+        FDisplayBind = 16,
+        FHidden = 64,
+        FImmediateBind = 4096,
+        FNonBrowsable = 1024,
+        FReplaceable = 2048,
+        FRequestEdit = 8,
+        FRestricted = 1,
+        FSource = 2,
+        FUiDefault = 512,
+        FUsesGetLastError = 128,
+    }
+    public sealed class TypeLibImportClassAttribute : Attribute {
+        public TypeLibImportClassAttribute(Type importClass);
+        public string Value { get; }
+    }
+    public sealed class TypeLibTypeAttribute : Attribute {
+        public TypeLibTypeAttribute(short flags);
+        public TypeLibTypeAttribute(TypeLibTypeFlags flags);
+        public TypeLibTypeFlags Value { get; }
+    }
+    public enum TypeLibTypeFlags {
+        FAggregatable = 1024,
+        FAppObject = 1,
+        FCanCreate = 2,
+        FControl = 32,
+        FDispatchable = 4096,
+        FDual = 64,
+        FHidden = 16,
+        FLicensed = 4,
+        FNonExtensible = 128,
+        FOleAutomation = 256,
+        FPreDeclId = 8,
+        FReplaceable = 2048,
+        FRestricted = 512,
+        FReverseBind = 8192,
+    }
+    public sealed class TypeLibVarAttribute : Attribute {
+        public TypeLibVarAttribute(short flags);
+        public TypeLibVarAttribute(TypeLibVarFlags flags);
+        public TypeLibVarFlags Value { get; }
+    }
+    public enum TypeLibVarFlags {
+        FBindable = 4,
+        FDefaultBind = 32,
+        FDefaultCollelem = 256,
+        FDisplayBind = 16,
+        FHidden = 64,
+        FImmediateBind = 4096,
+        FNonBrowsable = 1024,
+        FReadOnly = 1,
+        FReplaceable = 2048,
+        FRequestEdit = 8,
+        FRestricted = 128,
+        FSource = 2,
+        FUiDefault = 512,
+    }
+    public sealed class TypeLibVersionAttribute : Attribute {
+        public TypeLibVersionAttribute(int major, int minor);
+        public int MajorVersion { get; }
+        public int MinorVersion { get; }
+    }
     public enum UnmanagedType {
+        LPUTF8Str = 48,
     }
 }
 namespace System.Runtime.InteropServices.ComTypes {
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Explicit)]
-    public struct BINDPTR {
+    public struct BINDPTR {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct BIND_OPTS {
+    public struct BIND_OPTS {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct CONNECTDATA {
+    public struct CONNECTDATA {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct DISPPARAMS {
+    public struct DISPPARAMS {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ELEMDESC {
+    public struct ELEMDESC {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Explicit)]
-        public struct DESCUNION {
+        public struct DESCUNION {
         }
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct EXCEPINFO {
+    public struct EXCEPINFO {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct FILETIME {
+    public struct FILETIME {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct FORMATETC {
+    public struct FORMATETC {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct FUNCDESC {
+    public struct FUNCDESC {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct IDLDESC {
+    public struct IDLDESC {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct PARAMDESC {
+    public struct PARAMDESC {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct STATDATA {
+    public struct STATDATA {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct STATSTG {
+    public struct STATSTG {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct STGMEDIUM {
+    public struct STGMEDIUM {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct TYPEATTR {
+    public struct TYPEATTR {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct TYPEDESC {
+    public struct TYPEDESC {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct TYPELIBATTR {
+    public struct TYPELIBATTR {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct VARDESC {
+    public struct VARDESC {
-        [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Explicit)]
-        public struct DESCUNION {
+        public struct DESCUNION {
         }
     }
 }
 namespace System.Runtime.Serialization {
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SerializationEntry {
+    public struct SerializationEntry {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct StreamingContext {
+    public readonly struct StreamingContext {
     }
 }
 namespace System.Runtime.Serialization.Formatters {
+    public interface IFieldInfo {
+        string[] FieldNames { get; set; }
+        Type[] FieldTypes { get; set; }
+    }
 }
 namespace System.Security.Authentication {
     public enum HashAlgorithmType {
+        Sha256 = 32780,
+        Sha384 = 32781,
+        Sha512 = 32782,
     }
 }
 namespace System.Security.Cryptography {
     public sealed class AesCryptoServiceProvider : Aes {
+        public override int BlockSize { get; set; }
+        public override int FeedbackSize { get; set; }
+        public override byte[] IV { get; set; }
+        public override KeySizes[] LegalBlockSizes { get; }
+        public override KeySizes[] LegalKeySizes { get; }
+        public override CipherMode Mode { get; set; }
+        public override PaddingMode Padding { get; set; }
-        public override ICryptoTransform CreateDecryptor(byte[] key, byte[] iv);
+        public override ICryptoTransform CreateDecryptor(byte[] rgbKey, byte[] rgbIV);
-        public override ICryptoTransform CreateEncryptor(byte[] key, byte[] iv);
+        public override ICryptoTransform CreateEncryptor(byte[] rgbKey, byte[] rgbIV);
     }
     public sealed class AesManaged : Aes {
+        public override int BlockSize { get; set; }
+        public override KeySizes[] LegalBlockSizes { get; }
+        public override KeySizes[] LegalKeySizes { get; }
     }
+    public static class CryptographicOperations {
+        public static bool FixedTimeEquals(ReadOnlySpan<byte> left, ReadOnlySpan<byte> right);
+        public static void ZeroMemory(Span<byte> buffer);
+    }
     public class CryptoStream : Stream, IDisposable {
+        public CryptoStream(Stream stream, ICryptoTransform transform, CryptoStreamMode mode, bool leaveOpen);
+        public override IAsyncResult BeginRead(byte[] buffer, int offset, int count, AsyncCallback callback, object state);
+        public override IAsyncResult BeginWrite(byte[] buffer, int offset, int count, AsyncCallback callback, object state);
+        public override int EndRead(IAsyncResult asyncResult);
+        public override void EndWrite(IAsyncResult asyncResult);
+        public override int ReadByte();
+        public override void WriteByte(byte value);
     }
     public sealed class DESCryptoServiceProvider : DES {
+        public override ICryptoTransform CreateDecryptor();
+        public override ICryptoTransform CreateEncryptor();
     }
     public abstract class DSA : AsymmetricAlgorithm {
+        public static DSA Create(DSAParameters parameters);
+        public static DSA Create(int keySizeInBits);
+        protected virtual byte[] HashData(byte[] data, int offset, int count, HashAlgorithmName hashAlgorithm);
+        protected virtual byte[] HashData(Stream data, HashAlgorithmName hashAlgorithm);
+        public byte[] SignData(byte[] data, HashAlgorithmName hashAlgorithm);
+        public virtual byte[] SignData(byte[] data, int offset, int count, HashAlgorithmName hashAlgorithm);
+        public virtual byte[] SignData(Stream data, HashAlgorithmName hashAlgorithm);
+        public virtual bool TryCreateSignature(ReadOnlySpan<byte> hash, Span<byte> destination, out int bytesWritten);
+        protected virtual bool TryHashData(ReadOnlySpan<byte> data, Span<byte> destination, HashAlgorithmName hashAlgorithm, out int bytesWritten);
+        public virtual bool TrySignData(ReadOnlySpan<byte> data, Span<byte> destination, HashAlgorithmName hashAlgorithm, out int bytesWritten);
+        public bool VerifyData(byte[] data, byte[] signature, HashAlgorithmName hashAlgorithm);
+        public virtual bool VerifyData(byte[] data, int offset, int count, byte[] signature, HashAlgorithmName hashAlgorithm);
+        public virtual bool VerifyData(ReadOnlySpan<byte> data, ReadOnlySpan<byte> signature, HashAlgorithmName hashAlgorithm);
+        public virtual bool VerifyData(Stream data, byte[] signature, HashAlgorithmName hashAlgorithm);
+        public virtual bool VerifySignature(ReadOnlySpan<byte> hash, ReadOnlySpan<byte> signature);
     }
     public sealed class DSACryptoServiceProvider : DSA, ICspAsymmetricAlgorithm {
+        public override KeySizes[] LegalKeySizes { get; }
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct DSAParameters {
+    public struct DSAParameters {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ECCurve {
+    public struct ECCurve {
     }
+    public abstract class ECDiffieHellman : AsymmetricAlgorithm {
+        protected ECDiffieHellman();
+        public override string KeyExchangeAlgorithm { get; }
+        public abstract ECDiffieHellmanPublicKey PublicKey { get; }
+        public override string SignatureAlgorithm { get; }
+        public static new ECDiffieHellman Create();
+        public static ECDiffieHellman Create(ECCurve curve);
+        public static ECDiffieHellman Create(ECParameters parameters);
+        public static new ECDiffieHellman Create(string algorithm);
+        public byte[] DeriveKeyFromHash(ECDiffieHellmanPublicKey otherPartyPublicKey, HashAlgorithmName hashAlgorithm);
+        public virtual byte[] DeriveKeyFromHash(ECDiffieHellmanPublicKey otherPartyPublicKey, HashAlgorithmName hashAlgorithm, byte[] secretPrepend, byte[] secretAppend);
+        public byte[] DeriveKeyFromHmac(ECDiffieHellmanPublicKey otherPartyPublicKey, HashAlgorithmName hashAlgorithm, byte[] hmacKey);
+        public virtual byte[] DeriveKeyFromHmac(ECDiffieHellmanPublicKey otherPartyPublicKey, HashAlgorithmName hashAlgorithm, byte[] hmacKey, byte[] secretPrepend, byte[] secretAppend);
+        public virtual byte[] DeriveKeyMaterial(ECDiffieHellmanPublicKey otherPartyPublicKey);
+        public virtual byte[] DeriveKeyTls(ECDiffieHellmanPublicKey otherPartyPublicKey, byte[] prfLabel, byte[] prfSeed);
+        public virtual ECParameters ExportExplicitParameters(bool includePrivateParameters);
+        public virtual ECParameters ExportParameters(bool includePrivateParameters);
+        public override void FromXmlString(string xmlString);
+        public virtual void GenerateKey(ECCurve curve);
+        public virtual void ImportParameters(ECParameters parameters);
+        public override string ToXmlString(bool includePrivateParameters);
+    }
     public abstract class ECDiffieHellmanPublicKey : IDisposable {
+        protected ECDiffieHellmanPublicKey();
+        public virtual ECParameters ExportExplicitParameters();
+        public virtual ECParameters ExportParameters();
-        public abstract string ToXmlString();
+        public virtual string ToXmlString();
     }
     public abstract class ECDsa : AsymmetricAlgorithm {
+        public override void FromXmlString(string xmlString);
+        public override string ToXmlString(bool includePrivateParameters);
+        protected virtual bool TryHashData(ReadOnlySpan<byte> data, Span<byte> destination, HashAlgorithmName hashAlgorithm, out int bytesWritten);
+        public virtual bool TrySignData(ReadOnlySpan<byte> data, Span<byte> destination, HashAlgorithmName hashAlgorithm, out int bytesWritten);
+        public virtual bool TrySignHash(ReadOnlySpan<byte> hash, Span<byte> destination, out int bytesWritten);
+        public virtual bool VerifyData(ReadOnlySpan<byte> data, ReadOnlySpan<byte> signature, HashAlgorithmName hashAlgorithm);
+        public virtual bool VerifyHash(ReadOnlySpan<byte> hash, ReadOnlySpan<byte> signature);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ECParameters {
+    public struct ECParameters {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ECPoint {
+    public struct ECPoint {
     }
     public abstract class HashAlgorithm : ICryptoTransform, IDisposable {
+        protected virtual void HashCore(ReadOnlySpan<byte> source);
+        public bool TryComputeHash(ReadOnlySpan<byte> source, Span<byte> destination, out int bytesWritten);
+        protected virtual bool TryHashFinal(Span<byte> destination, out int bytesWritten);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct HashAlgorithmName : IEquatable<HashAlgorithmName> {
+    public readonly struct HashAlgorithmName : IEquatable<HashAlgorithmName> {
     }
     public abstract class HMAC : KeyedHashAlgorithm {
+        protected override void HashCore(ReadOnlySpan<byte> source);
+        protected override bool TryHashFinal(Span<byte> destination, out int bytesWritten);
     }
     public class HMACMD5 : HMAC {
+        public override byte[] Key { get; set; }
+        protected override void Dispose(bool disposing);
+        protected override void HashCore(byte[] rgb, int ib, int cb);
+        protected override void HashCore(ReadOnlySpan<byte> source);
+        protected override byte[] HashFinal();
+        public override void Initialize();
+        protected override bool TryHashFinal(Span<byte> destination, out int bytesWritten);
     }
     public class HMACSHA1 : HMAC {
+        public override byte[] Key { get; set; }
+        protected override void Dispose(bool disposing);
+        protected override void HashCore(byte[] rgb, int ib, int cb);
+        protected override void HashCore(ReadOnlySpan<byte> source);
+        protected override byte[] HashFinal();
+        public override void Initialize();
+        protected override bool TryHashFinal(Span<byte> destination, out int bytesWritten);
     }
     public class HMACSHA256 : HMAC {
+        public override byte[] Key { get; set; }
+        protected override void Dispose(bool disposing);
+        protected override void HashCore(byte[] rgb, int ib, int cb);
+        protected override void HashCore(ReadOnlySpan<byte> source);
+        protected override byte[] HashFinal();
+        public override void Initialize();
+        protected override bool TryHashFinal(Span<byte> destination, out int bytesWritten);
     }
     public class HMACSHA384 : HMAC {
+        public override byte[] Key { get; set; }
+        protected override void Dispose(bool disposing);
+        protected override void HashCore(byte[] rgb, int ib, int cb);
+        protected override void HashCore(ReadOnlySpan<byte> source);
+        protected override byte[] HashFinal();
+        public override void Initialize();
+        protected override bool TryHashFinal(Span<byte> destination, out int bytesWritten);
     }
     public class HMACSHA512 : HMAC {
+        public override byte[] Key { get; set; }
+        protected override void Dispose(bool disposing);
+        protected override void HashCore(byte[] rgb, int ib, int cb);
+        protected override void HashCore(ReadOnlySpan<byte> source);
+        protected override byte[] HashFinal();
+        public override void Initialize();
+        protected override bool TryHashFinal(Span<byte> destination, out int bytesWritten);
     }
     public sealed class IncrementalHash : IDisposable {
+        public void AppendData(ReadOnlySpan<byte> data);
+        public bool TryGetHashAndReset(Span<byte> destination, out int bytesWritten);
     }
     public abstract class RandomNumberGenerator : IDisposable {
+        public static void Fill(Span<byte> data);
+        public virtual void GetBytes(Span<byte> data);
+        public virtual void GetNonZeroBytes(Span<byte> data);
     }
     public class Rfc2898DeriveBytes : DeriveBytes {
+        public Rfc2898DeriveBytes(byte[] password, byte[] salt, int iterations, HashAlgorithmName hashAlgorithm);
+        public Rfc2898DeriveBytes(string password, byte[] salt, int iterations, HashAlgorithmName hashAlgorithm);
+        public Rfc2898DeriveBytes(string password, int saltSize, int iterations, HashAlgorithmName hashAlgorithm);
+        public HashAlgorithmName HashAlgorithm { get; }
     }
     public sealed class RijndaelManaged : Rijndael {
+        public override int BlockSize { get; set; }
+        public override byte[] IV { get; set; }
+        public override byte[] Key { get; set; }
+        public override int KeySize { get; set; }
+        public override KeySizes[] LegalKeySizes { get; }
+        public override CipherMode Mode { get; set; }
+        public override PaddingMode Padding { get; set; }
+        public override ICryptoTransform CreateDecryptor();
+        public override ICryptoTransform CreateEncryptor();
     }
     public abstract class RSA : AsymmetricAlgorithm {
+        public static RSA Create(int keySizeInBits);
+        public static RSA Create(RSAParameters parameters);
+        public virtual bool TryDecrypt(ReadOnlySpan<byte> data, Span<byte> destination, RSAEncryptionPadding padding, out int bytesWritten);
+        public virtual bool TryEncrypt(ReadOnlySpan<byte> data, Span<byte> destination, RSAEncryptionPadding padding, out int bytesWritten);
+        protected virtual bool TryHashData(ReadOnlySpan<byte> data, Span<byte> destination, HashAlgorithmName hashAlgorithm, out int bytesWritten);
+        public virtual bool TrySignData(ReadOnlySpan<byte> data, Span<byte> destination, HashAlgorithmName hashAlgorithm, RSASignaturePadding padding, out int bytesWritten);
+        public virtual bool TrySignHash(ReadOnlySpan<byte> hash, Span<byte> destination, HashAlgorithmName hashAlgorithm, RSASignaturePadding padding, out int bytesWritten);
+        public virtual bool VerifyData(ReadOnlySpan<byte> data, ReadOnlySpan<byte> signature, HashAlgorithmName hashAlgorithm, RSASignaturePadding padding);
+        public virtual bool VerifyHash(ReadOnlySpan<byte> hash, ReadOnlySpan<byte> signature, HashAlgorithmName hashAlgorithm, RSASignaturePadding padding);
     }
     public sealed class RSACryptoServiceProvider : RSA, ICspAsymmetricAlgorithm {
+        public override KeySizes[] LegalKeySizes { get; }
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct RSAParameters {
+    public struct RSAParameters {
     }
     public sealed class TripleDESCryptoServiceProvider : TripleDES {
+        public override int BlockSize { get; set; }
+        public override int FeedbackSize { get; set; }
+        public override byte[] IV { get; set; }
+        public override byte[] Key { get; set; }
+        public override int KeySize { get; set; }
+        public override KeySizes[] LegalBlockSizes { get; }
+        public override KeySizes[] LegalKeySizes { get; }
+        public override CipherMode Mode { get; set; }
+        public override PaddingMode Padding { get; set; }
+        public override ICryptoTransform CreateDecryptor();
+        public override ICryptoTransform CreateEncryptor();
     }
 }
 namespace System.Security.Cryptography.X509Certificates {
+    public sealed class CertificateRequest {
+        public CertificateRequest(string subjectName, ECDsa key, HashAlgorithmName hashAlgorithm);
+        public CertificateRequest(string subjectName, RSA key, HashAlgorithmName hashAlgorithm, RSASignaturePadding padding);
+        public CertificateRequest(X500DistinguishedName subjectName, ECDsa key, HashAlgorithmName hashAlgorithm);
+        public CertificateRequest(X500DistinguishedName subjectName, PublicKey publicKey, HashAlgorithmName hashAlgorithm);
+        public CertificateRequest(X500DistinguishedName subjectName, RSA key, HashAlgorithmName hashAlgorithm, RSASignaturePadding padding);
+        public Collection<X509Extension> CertificateExtensions { get; }
+        public HashAlgorithmName HashAlgorithm { get; }
+        public PublicKey PublicKey { get; }
+        public X500DistinguishedName SubjectName { get; }
+        public X509Certificate2 Create(X500DistinguishedName issuerName, X509SignatureGenerator generator, DateTimeOffset notBefore, DateTimeOffset notAfter, byte[] serialNumber);
+        public X509Certificate2 Create(X509Certificate2 issuerCertificate, DateTimeOffset notBefore, DateTimeOffset notAfter, byte[] serialNumber);
+        public X509Certificate2 CreateSelfSigned(DateTimeOffset notBefore, DateTimeOffset notAfter);
+        public byte[] CreateSigningRequest();
+        public byte[] CreateSigningRequest(X509SignatureGenerator signatureGenerator);
+    }
+    public static class DSACertificateExtensions {
+        public static X509Certificate2 CopyWithPrivateKey(this X509Certificate2 certificate, DSA privateKey);
+        public static DSA GetDSAPrivateKey(this X509Certificate2 certificate);
+        public static DSA GetDSAPublicKey(this X509Certificate2 certificate);
+    }
     public static class ECDsaCertificateExtensions {
+        public static X509Certificate2 CopyWithPrivateKey(this X509Certificate2 certificate, ECDsa privateKey);
     }
     public static class RSACertificateExtensions {
+        public static X509Certificate2 CopyWithPrivateKey(this X509Certificate2 certificate, RSA privateKey);
     }
+    public sealed class SubjectAlternativeNameBuilder {
+        public SubjectAlternativeNameBuilder();
+        public void AddDnsName(string dnsName);
+        public void AddEmailAddress(string emailAddress);
+        public void AddIpAddress(IPAddress ipAddress);
+        public void AddUri(Uri uri);
+        public void AddUserPrincipalName(string upn);
+        public X509Extension Build(bool critical = false);
+    }
     public class X509Certificate : IDeserializationCallback, IDisposable, ISerializable {
+        public virtual byte[] GetCertHash(HashAlgorithmName hashAlgorithm);
+        public virtual string GetCertHashString(HashAlgorithmName hashAlgorithm);
+        public virtual bool TryGetCertHash(HashAlgorithmName hashAlgorithm, Span<byte> destination, out int bytesWritten);
     }
     public class X509CertificateCollection : CollectionBase {
+        protected override void OnValidate(object value);
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct X509ChainStatus {
+    public struct X509ChainStatus {
     }
     public enum X509KeyStorageFlags {
+        EphemeralKeySet = 32,
     }
+    public abstract class X509SignatureGenerator {
+        protected X509SignatureGenerator();
+        public PublicKey PublicKey { get; }
+        protected abstract PublicKey BuildPublicKey();
+        public static X509SignatureGenerator CreateForECDsa(ECDsa key);
+        public static X509SignatureGenerator CreateForRSA(RSA key, RSASignaturePadding signaturePadding);
+        public abstract byte[] GetSignatureAlgorithmIdentifier(HashAlgorithmName hashAlgorithm);
+        public abstract byte[] SignData(byte[] data, HashAlgorithmName hashAlgorithm);
+    }
     public sealed class X509Store : IDisposable {
+        public X509Store(StoreName storeName, StoreLocation storeLocation, OpenFlags flags);
+        public X509Store(string storeName, StoreLocation storeLocation, OpenFlags flags);
+        public bool IsOpen { get; }
     }
 }
 namespace System.Text {
     public abstract class Decoder {
+        public virtual void Convert(ReadOnlySpan<byte> bytes, Span<char> chars, bool flush, out int bytesUsed, out int charsUsed, out bool completed);
+        public virtual int GetCharCount(ReadOnlySpan<byte> bytes, bool flush);
+        public virtual int GetChars(ReadOnlySpan<byte> bytes, Span<char> chars, bool flush);
     }
     public abstract class Encoder {
+        public virtual void Convert(ReadOnlySpan<char> chars, Span<byte> bytes, bool flush, out int charsUsed, out int bytesUsed, out bool completed);
+        public virtual int GetByteCount(ReadOnlySpan<char> chars, bool flush);
+        public virtual int GetBytes(ReadOnlySpan<char> chars, Span<byte> bytes, bool flush);
     }
     public abstract class Encoding : ICloneable {
+        public virtual ReadOnlySpan<byte> Preamble { get; }
+        public virtual int GetByteCount(ReadOnlySpan<char> chars);
+        public int GetByteCount(string s, int index, int count);
+        public virtual int GetBytes(ReadOnlySpan<char> chars, Span<byte> bytes);
+        public byte[] GetBytes(string s, int index, int count);
+        public virtual int GetCharCount(ReadOnlySpan<byte> bytes);
+        public virtual int GetChars(ReadOnlySpan<byte> bytes, Span<char> chars);
+        public string GetString(ReadOnlySpan<byte> bytes);
     }
     public sealed class StringBuilder : ISerializable {
+        public StringBuilder Append(ReadOnlySpan<char> value);
+        public StringBuilder Append(StringBuilder value);
+        public StringBuilder Append(StringBuilder value, int startIndex, int count);
+        public StringBuilder AppendJoin<T>(char separator, IEnumerable<T> values);
+        public StringBuilder AppendJoin<T>(string separator, IEnumerable<T> values);
+        public StringBuilder AppendJoin(char separator, params object[] values);
+        public StringBuilder AppendJoin(char separator, params string[] values);
+        public StringBuilder AppendJoin(string separator, params object[] values);
+        public StringBuilder AppendJoin(string separator, params string[] values);
+        public void CopyTo(int sourceIndex, Span<char> destination, int count);
+        public bool Equals(ReadOnlySpan<char> span);
+        public StringBuilder Insert(int index, ReadOnlySpan<char> value);
     }
 }
 namespace System.Text.RegularExpressions {
-    public class CaptureCollection : ICollection, IEnumerable {
+    public class CaptureCollection : ICollection, ICollection<Capture>, IEnumerable, IEnumerable<Capture>, IList, IList<Capture>, IReadOnlyCollection<Capture>, IReadOnlyList<Capture> {
+        Capture System.Collections.Generic.IList<System.Text.RegularExpressions.Capture>.this[int index] { get; set; }
+        bool System.Collections.IList.IsFixedSize { get; }
+        object System.Collections.IList.this[int index] { get; set; }
+        public void CopyTo(Capture[] array, int arrayIndex);
+        void System.Collections.Generic.ICollection<System.Text.RegularExpressions.Capture>.Clear();
+        void System.Collections.Generic.ICollection<System.Text.RegularExpressions.Capture>.Add(Capture item);
+        bool System.Collections.Generic.ICollection<System.Text.RegularExpressions.Capture>.Remove(Capture item);
+        bool System.Collections.Generic.ICollection<System.Text.RegularExpressions.Capture>.Contains(Capture item);
+        IEnumerator<Capture> System.Collections.Generic.IEnumerable<System.Text.RegularExpressions.Capture>.GetEnumerator();
+        void System.Collections.Generic.IList<System.Text.RegularExpressions.Capture>.RemoveAt(int index);
+        int System.Collections.Generic.IList<System.Text.RegularExpressions.Capture>.IndexOf(Capture item);
+        void System.Collections.Generic.IList<System.Text.RegularExpressions.Capture>.Insert(int index, Capture item);
+        int System.Collections.IList.Add(object value);
+        void System.Collections.IList.Clear();
+        bool System.Collections.IList.Contains(object value);
+        int System.Collections.IList.IndexOf(object value);
+        void System.Collections.IList.Insert(int index, object value);
+        void System.Collections.IList.Remove(object value);
+        void System.Collections.IList.RemoveAt(int index);
     }
     public class Group : Capture {
+        public string Name { get; }
     }
-    public class GroupCollection : ICollection, IEnumerable {
+    public class GroupCollection : ICollection, ICollection<Group>, IEnumerable, IEnumerable<Group>, IList, IList<Group>, IReadOnlyCollection<Group>, IReadOnlyList<Group> {
+        Group System.Collections.Generic.IList<System.Text.RegularExpressions.Group>.this[int index] { get; set; }
+        bool System.Collections.IList.IsFixedSize { get; }
+        object System.Collections.IList.this[int index] { get; set; }
+        public void CopyTo(Group[] array, int arrayIndex);
+        void System.Collections.Generic.ICollection<System.Text.RegularExpressions.Group>.Clear();
+        void System.Collections.Generic.ICollection<System.Text.RegularExpressions.Group>.Add(Group item);
+        bool System.Collections.Generic.ICollection<System.Text.RegularExpressions.Group>.Remove(Group item);
+        bool System.Collections.Generic.ICollection<System.Text.RegularExpressions.Group>.Contains(Group item);
+        IEnumerator<Group> System.Collections.Generic.IEnumerable<System.Text.RegularExpressions.Group>.GetEnumerator();
+        int System.Collections.Generic.IList<System.Text.RegularExpressions.Group>.IndexOf(Group item);
+        void System.Collections.Generic.IList<System.Text.RegularExpressions.Group>.RemoveAt(int index);
+        void System.Collections.Generic.IList<System.Text.RegularExpressions.Group>.Insert(int index, Group item);
+        int System.Collections.IList.Add(object value);
+        void System.Collections.IList.Clear();
+        bool System.Collections.IList.Contains(object value);
+        int System.Collections.IList.IndexOf(object value);
+        void System.Collections.IList.Insert(int index, object value);
+        void System.Collections.IList.Remove(object value);
+        void System.Collections.IList.RemoveAt(int index);
     }
-    public class MatchCollection : ICollection, IEnumerable {
+    public class MatchCollection : ICollection, ICollection<Match>, IEnumerable, IEnumerable<Match>, IList, IList<Match>, IReadOnlyCollection<Match>, IReadOnlyList<Match> {
+        Match System.Collections.Generic.IList<System.Text.RegularExpressions.Match>.this[int index] { get; set; }
+        bool System.Collections.IList.IsFixedSize { get; }
+        object System.Collections.IList.this[int index] { get; set; }
+        public void CopyTo(Match[] array, int arrayIndex);
+        void System.Collections.Generic.ICollection<System.Text.RegularExpressions.Match>.Clear();
+        void System.Collections.Generic.ICollection<System.Text.RegularExpressions.Match>.Add(Match item);
+        bool System.Collections.Generic.ICollection<System.Text.RegularExpressions.Match>.Remove(Match item);
+        bool System.Collections.Generic.ICollection<System.Text.RegularExpressions.Match>.Contains(Match item);
+        IEnumerator<Match> System.Collections.Generic.IEnumerable<System.Text.RegularExpressions.Match>.GetEnumerator();
+        int System.Collections.Generic.IList<System.Text.RegularExpressions.Match>.IndexOf(Match item);
+        void System.Collections.Generic.IList<System.Text.RegularExpressions.Match>.RemoveAt(int index);
+        void System.Collections.Generic.IList<System.Text.RegularExpressions.Match>.Insert(int index, Match item);
+        int System.Collections.IList.Add(object value);
+        void System.Collections.IList.Clear();
+        bool System.Collections.IList.Contains(object value);
+        int System.Collections.IList.IndexOf(object value);
+        void System.Collections.IList.Insert(int index, object value);
+        void System.Collections.IList.Remove(object value);
+        void System.Collections.IList.RemoveAt(int index);
     }
 }
 namespace System.Threading {
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct AsyncFlowControl : IDisposable {
+    public struct AsyncFlowControl : IDisposable {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct AsyncLocalValueChangedArgs<T> {
+    public struct AsyncLocalValueChangedArgs<T> {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct CancellationToken {
+    public readonly struct CancellationToken {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct CancellationTokenRegistration : IDisposable, IEquatable<CancellationTokenRegistration> {
+    public readonly struct CancellationTokenRegistration : IDisposable, IEquatable<CancellationTokenRegistration> {
+        public CancellationToken Token { get; }
     }
     public static class Interlocked {
+        public static void MemoryBarrierProcessWide();
     }
     public static class LazyInitializer {
+        public static T EnsureInitialized<T>(ref T target, ref object syncLock, Func<T> valueFactory) where T : class;
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct LockCookie {
+    public struct LockCookie {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct NativeOverlapped {
+    public struct NativeOverlapped {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SpinLock {
+    public struct SpinLock {
     }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct SpinWait {
+    public struct SpinWait {
     }
     public sealed class Thread : CriticalFinalizerObject {
+        public static int GetCurrentProcessorId();
     }
     public static class ThreadPool {
+        public static bool QueueUserWorkItem<TState>(Action<TState> callBack, TState state, bool preferLocal);
     }
 }
 namespace System.Threading.Tasks {
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct ParallelLoopResult {
+    public struct ParallelLoopResult {
     }
     public class Task : IAsyncResult, IDisposable {
+        public bool IsCompletedSuccessfully { get; }
     }
     public class TaskCanceledException : OperationCanceledException {
+        public TaskCanceledException(string message, Exception innerException, CancellationToken token);
     }
+    public readonly struct ValueTask : IEquatable<ValueTask> {
+        public ValueTask(IValueTaskSource source, short token);
+        public ValueTask(Task task);
+        public bool IsCanceled { get; }
+        public bool IsCompleted { get; }
+        public bool IsCompletedSuccessfully { get; }
+        public bool IsFaulted { get; }
+        public Task AsTask();
+        public ConfiguredValueTaskAwaitable ConfigureAwait(bool continueOnCapturedContext);
+        public override bool Equals(object obj);
+        public bool Equals(ValueTask other);
+        public ValueTaskAwaiter GetAwaiter();
+        public override int GetHashCode();
+        public static bool operator ==(ValueTask left, ValueTask right);
+        public static bool operator !=(ValueTask left, ValueTask right);
+        public ValueTask Preserve();
+    }
+    public readonly struct ValueTask<TResult> : IEquatable<ValueTask<TResult>> {
+        public ValueTask(IValueTaskSource<TResult> source, short token);
+        public ValueTask(Task<TResult> task);
+        public ValueTask(TResult result);
+        public bool IsCanceled { get; }
+        public bool IsCompleted { get; }
+        public bool IsCompletedSuccessfully { get; }
+        public bool IsFaulted { get; }
+        public TResult Result { get; }
+        public Task<TResult> AsTask();
+        public ConfiguredValueTaskAwaitable<TResult> ConfigureAwait(bool continueOnCapturedContext);
+        public override bool Equals(object obj);
+        public bool Equals(ValueTask<TResult> other);
+        public ValueTaskAwaiter<TResult> GetAwaiter();
+        public override int GetHashCode();
+        public static bool operator ==(ValueTask<TResult> left, ValueTask<TResult> right);
+        public static bool operator !=(ValueTask<TResult> left, ValueTask<TResult> right);
+        public ValueTask<TResult> Preserve();
+        public override string ToString();
+    }
 }
+namespace System.Threading.Tasks.Sources {
+    public interface IValueTaskSource {
+        void GetResult(short token);
+        ValueTaskSourceStatus GetStatus(short token);
+        void OnCompleted(Action<object> continuation, object state, short token, ValueTaskSourceOnCompletedFlags flags);
+    }
+    public interface IValueTaskSource<out TResult> {
+        TResult GetResult(short token);
+        ValueTaskSourceStatus GetStatus(short token);
+        void OnCompleted(Action<object> continuation, object state, short token, ValueTaskSourceOnCompletedFlags flags);
+    }
+    public enum ValueTaskSourceOnCompletedFlags {
+        FlowExecutionContext = 2,
+        None = 0,
+        UseSchedulingContext = 1,
+    }
+    public enum ValueTaskSourceStatus {
+        Canceled = 3,
+        Faulted = 2,
+        Pending = 0,
+        Succeeded = 1,
+    }
+}
 namespace System.Transactions {
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct TransactionOptions {
+    public struct TransactionOptions {
     }
 }
 namespace System.Xml.Linq {
     public class XCData : XText {
+        public override Task WriteToAsync(XmlWriter writer, CancellationToken cancellationToken);
     }
     public class XComment : XNode {
+        public override Task WriteToAsync(XmlWriter writer, CancellationToken cancellationToken);
     }
     public class XDocument : XContainer {
+        public static Task<XDocument> LoadAsync(Stream stream, LoadOptions options, CancellationToken cancellationToken);
+        public static Task<XDocument> LoadAsync(TextReader textReader, LoadOptions options, CancellationToken cancellationToken);
+        public static Task<XDocument> LoadAsync(XmlReader reader, LoadOptions options, CancellationToken cancellationToken);
+        public Task SaveAsync(Stream stream, SaveOptions options, CancellationToken cancellationToken);
+        public Task SaveAsync(TextWriter textWriter, SaveOptions options, CancellationToken cancellationToken);
+        public Task SaveAsync(XmlWriter writer, CancellationToken cancellationToken);
+        public override Task WriteToAsync(XmlWriter writer, CancellationToken cancellationToken);
     }
     public class XDocumentType : XNode {
+        public override Task WriteToAsync(XmlWriter writer, CancellationToken cancellationToken);
     }
     public class XElement : XContainer, IXmlSerializable {
+        public static Task<XElement> LoadAsync(Stream stream, LoadOptions options, CancellationToken cancellationToken);
+        public static Task<XElement> LoadAsync(TextReader textReader, LoadOptions options, CancellationToken cancellationToken);
+        public static Task<XElement> LoadAsync(XmlReader reader, LoadOptions options, CancellationToken cancellationToken);
+        public Task SaveAsync(Stream stream, SaveOptions options, CancellationToken cancellationToken);
+        public Task SaveAsync(TextWriter textWriter, SaveOptions options, CancellationToken cancellationToken);
+        public Task SaveAsync(XmlWriter writer, CancellationToken cancellationToken);
+        public override Task WriteToAsync(XmlWriter writer, CancellationToken cancellationToken);
     }
     public abstract class XNode : XObject {
+        public static Task<XNode> ReadFromAsync(XmlReader reader, CancellationToken cancellationToken);
+        public abstract Task WriteToAsync(XmlWriter writer, CancellationToken cancellationToken);
     }
     public class XProcessingInstruction : XNode {
+        public override Task WriteToAsync(XmlWriter writer, CancellationToken cancellationToken);
     }
     public class XText : XNode {
+        public override Task WriteToAsync(XmlWriter writer, CancellationToken cancellationToken);
     }
 }
 namespace System.Xml.Serialization {
+    public abstract class SchemaImporter {
+    }
-    [System.Runtime.InteropServices.StructLayoutAttribute(System.Runtime.InteropServices.LayoutKind.Sequential)]
-    public struct XmlDeserializationEvents {
+    public struct XmlDeserializationEvents {
     }
-    public class XmlSchemaImporter {
+    public class XmlSchemaImporter : SchemaImporter {
     }
 }
 namespace Microsoft.Win32.SafeHandles {
     public sealed class SafeFileHandle : SafeHandleZeroOrMinusOneIsInvalid {
+        public override bool IsInvalid { get; }
     }
     public sealed class SafeMemoryMappedFileHandle : SafeHandleZeroOrMinusOneIsInvalid {
+        public override bool IsInvalid { get; }
     }
     public sealed class SafePipeHandle : SafeHandleZeroOrMinusOneIsInvalid {
+        public override bool IsInvalid { get; }
     }
     public sealed class SafeProcessHandle : SafeHandleZeroOrMinusOneIsInvalid {
+        public override bool IsInvalid { get; }
     }
 }
```
