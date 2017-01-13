pvData Overview
---
# 1. An aggregate data type 一个聚合数据类型

Suppose want to encode a statistical summary of N floating point values. Let’s say we want

1. A mean (or some other sort average)
1. The number of samples
1. The standard deviation (or some other measure of spread) 标准偏差
1. The maximum value
1. The minimum value


We could encode this as structure consisting of an ordered set of fields.
Each field has a name and a type.
Let’s say:

1. A 64-bit floating point field for the average. Let’s call this type “double”. For the name of the field, we could choose “average”, 1. but let’s call it value.
1. A 64-bit integer field for the number of samples. Let’s call the type “long” and name the field “N”.
1. A double field for the spread. Let’s call it “dispersion”
1. A double field “max”
1. A double field “min”


We can write a description of our type as follows:
```
structure
    double value
    long N
    double dispersion
    double max
    double min
```

Let’s say we have 1000 samples with a mean of 2.0, a standard deviation of 1.0 and a minimum of 0.1 and a maximum of 4.4. We could our encoding of the statistical summary as:
```
structure
    double value       2.0
    long N            1000
    double dispersion  1.0
    double max         4.4
    double min         0.1
```
This system of encoding data in EPICS V4 is called **pvData** and this way of writing pvData structures is called the **pvData meta language**.


Some jargon(术语): There are two types of objects in pvData: *Introspection(内省的) objects* and *data objects*.

The first type of structure above, which describes the type of a piece of structured data, is an example of an *introspection object*.

The second structure, which carries values, is called a *data object*. Structure data objects have an introspection object and some of the fields can carry data (as in the case above).

The values of the fields are referred to as the value data of the fields. The value data of a structure’s fields are called the *value data* of the structure.

The introspection object corresponding to a data object is referred to as its introspection data or its introspection type.


We can additionally give the type of the structure a name, called the type ID which helps identify the structure. The default type ID for a structure is *structure*.

The above structure is an example of a standard structure (a Normative Type) called NTAggregate. So let’s give it the type ID *NTAggregate*.


When we write a structure we typically write it with the type ID:
```
NTAggregate
    double value
    long N
    double dispersion
    double max
    double min
```
and the data object above as
```
NTAggregate
    double value       2.0
    long N            1000
    double dispersion  1.0
    double max         4.4
    double min         0.1
```


# 2. Structure subfields

Now suppose we want to add timestamps for the first and last sample in the data. We could encode the timestamp using the structure:
```
time_t
    long secondsPastEpoch
    int nanoseconds
    int userTag
```
where int denotes a 32-bit signed integer


We could then add structure subfields to our NTAggregate:
```
NTAggregate
    double value
    long N
    double dispersion
    double max
    double min
    time_t firstTimeStamp
        long secondsPastEpoch
        int nanoseconds
        int userTag
    time_t lastTimeStamp
        long secondsPastEpoch
        int nanoseconds
        int userTag
```

The two timestamp fields are fields of the top-level structure as well as the previous scalar fields.

Their introspection type is the time_t structure described above. These fields are themselves structures with fields secondsPastEpoch, nanoseconds and userTag.

The indentation(缩进) rules are similar to the indentation rules in Python.


An example of a corresponding data object would be:
```
NTAggregate
    double value       2.0
    long N            1000
    double dispersion  1.0
    double max         4.4
    double min         0.1
    time_t firstTimeStamp
        long secondsPastEpoch 1460589140
        int nanoseconds         11436967
        int userTag                    0
    time_t lastTimeStamp
        long secondsPastEpoch 1460589149
        int nanoseconds        889605397
        int userTag                    0
```
# 3. pvData structures
In general a pvData structure consists of
  - 0 or more fields
  - A type ID

Each field has
  - A name
  - An introspection type

For data objects a field may also have values.

We write a structure as the type ID followed by 0 or more fields on subsequent lines, 1 per line, indented(缩进). The precise(精确的) amount of indentation is not significant, only the level relative to other fields.

An example is the NTAggregate we’ve seen already:
```
NTAggregate
    double value
    long N
    double dispersion
    double max
    double min
```

# 4. Field Types

Field Types

There are 6 basic field types namely

- Scalars
- Scalar arrays
- Structures
- Structure arrays
- Union
- Union arrays

This field type is part of the introspection type of the field.

We’ve already seen examples of two of these: scalars and structures.

## Scalar Fields

Scalar Fields

In general scalar fields can be one of the following scalar types

- boolean
- 8, 16, 32 or 64-bit signed integers: byte, short, int, long
- 8, 16, 32 or 64-bit unsigned integers: ubyte, ushort, uint, ulong
- 32 or 64-bit floating point numbers: float, double
- string

The scalar types are based on the Java primitive types with the addition of unsigned integers and string.

The scalar type entirely specifies the introspection type of a scalar field.


For data objects, scalar fields additionally have value data.

The possible values for the data for each type are what you would expect. For example:

- boolean: true or false
- byte: integer in the range -128 to 127
- ushort: integer in the range 0 to 65535
- double: 64-bit (IEEE 754) floating point value (e.g 0.1, -3.5e-7, NaN)
- string: string of ascii characters


The introspection type is written in the pvData meta language as
```
<scalar-type>
```
and scalar field as
```
<scalar-type> <field-name>
```
Examples:
```
double value
long N
string message
```

For data objects fields are written as
```
<scalar-type> <field-name> <value>
```
Examples:
```
double value 3.14159
long N 1000
string message HIHI_ALARM
```


## Structure fields

For an introspection object, a structure field, as for fields of all types, consists of introspection object and a field name.

For a structure field that introspection object is itself a structure.

In other words the top-level structure has a field whose introspection object is a structure.

As usual we write a structure with structure fields by added the fields one per line, indented, after the type ID.

For the structure fields we indent their fields one level further.
```
NTScalar
    double value
    alarm_t alarm
        int severity
        int status
        string message
    time_t timeStamp
        long secondsPastEpoch
        int nanoseconds
        int userTag
```
Data objects are similar except the fields of a structure field may have values.
```
NTScalar
    double value              8
    alarm_t alarm
        int severity          2
        int status            3
        string message        HIHI_ALARM
    time_t timeStamp
        long secondsPastEpoch 1460589140
        int nanoseconds       389605397
        int userTag           0
```
So in this case the top-level structure has a structure field
```
alarm_t alarm
    int severity
    int status
    string message
```
whose name is alarm and whose introspection type is the structure
```
alarm_t
    int severity
    int status
    string message
```
and a second structure field
```
time_t timeStamp
    long secondsPastEpoch
    int nanoseconds
    int userTag
```

whose name is timestamp and whose introspection type is the structure
```
time_t
    long secondsPastEpoch
    int nanoseconds
    int userTag
```

## Scalar Arrays

Suppose we want to encode a table of archiver data for a PV whose value is double.

We want columns for the value, the seconds past UNIX epoch, nanoseconds and the alarm severities and statuses. We’ll also have a label for each column.

We could encode this as a structure with one field for each column. These fields will be array fields with elements of the appropriate type. We’ll also have an array of strings for the labels. To separate the columns from the labels we’ll put it in a sub-structure. Call it value as it’s the primary value of the structure:
```
NTTable
    string[] labels
    structure value
        double[] value
        long[] secondsPastEpoch
        int[] nanoseconds
        int[] severity
        int[] status
```
string[] denotes string array field and so on.
```
NTTable
    string[] labels [value,  seconds, nanoseconds,  status, severity]
    structure value
        double[] value          [       1.1,       1.2,         2.0]
        long[] secondsPastEpoch [1460589140, 1460589141, 1460589142]
        int[] nanoseconds       [ 164235768,  164235245,  164235256]
        int[] severity          [         0,          0,          1]
        int[] status            [         0,          0,          3]
```

In general scalar arrays fields are used to encode arrays of data of the same scalar type.

The possible scalar types are the same as for scalar fields:

- boolean
- 8, 16, 32 or 64-bit signed integers: byte, short, int, long
- 8, 16, 32 or 64-bit unsigned integers: ubyte, ushort, uint, ulong
- 32 or 64-bit floating point numbers
- string

Like scalars, the introspection type of a scalar array field is completely specified by the scalar type.  


We write the introspection type in the meta language as
```
<scalar-type>[]
```
So the possible introspection types are

- boolean[]
- byte[], short[], int[], long[]
- ubyte[], ushort[], uint[], ulong[]
- float[], double[]
- string[]

Fields are written
```
<scalar-type>[] <field-name>
```
For example
```
string[] labels
double[] value
int[] status
```

The value data consists of zero or more scalar values. The set of possible values for each element is the same as for the values scalar field. 
We write these values as a comma separated list with square brackets. 
So examples of the data objects corresponding to the above fields are
```
string[] labels [value,  seconds, nanoseconds,  status, severity] 
double[] value  [1.1, 1.2, 2.0] 
int[] status    [  0,   0,   3]
```

## Special Structures

pvData can be used to define a wide variety of structures. However pvData itself has no knowledge of any specific structure.

Some standard structures have been defined though. These are referred to as special structures.

We’ve seen two examples so far: time_t for time stamps and alarm_t for alarms.

### time_t

The structure
```
time_t
    long secondsPastEpoch
    int  nanoseconds
    int  userTag
```
describes a defined point in time relative to the midnight on January 1st, 1970 UTC.

secondsPastEpoch and nanoseconds are the seconds and nanoseconds relative to the above time. Note we use UNIX epoch(纪元，时间戳), not EPICS epoch.

The meaning of the userTag isn’t specified – it can be used any way the user wishes. One use to store a pulse ID in free electron lasers.


### alarm_t

The structure
```
alarm_t
    int severity
    int status
    string message
```
describes a diagnostic of the value of a control system process variable. It corresponds to the EPICS V3 alarm severity and status, but adds a message string (the meaning of the status is also different).

severity is an integer whose meaning is
```
      0: no alarm  
      1: minor alarm  
      2: major alarm  
      3: invalid alarm  
      4: undefined alarm
```
status is an integer whose meaning is
```
      0: no status  
      1: device status  
      2: driver status  
      3: record status  
      4: database status  
      5: config status  
      6: undefined status  
      7: client status
```

### enum_t

EPICS V4 has no built in support for enums. They are encoded instead using the structure
```
enum_t 
    int index
    string[] choices
```
choices contains the labels for valid values of the enumeration and index is the current value in choices.

## Union fields

Unions add dynamic typing to V4.

Union field data objects store field data objects. The introspection object describes what fields can be stored. They come in two flavours:

- Regular unions – essentially tagged unions. A union field data object stores one of a fixed list of fields. The introspection types
- Variant(变体) unions – can store a field of any type.


### Variant Union fields

If a field is a variant union this fully defines its introspection type.

In the meta language we write the introspection type as
```
<code>
any
</code>
```
So a variant union field is written
```
any <field-name>
```
A variant union data object stores a field data object. Unlike the fields of a structure this field is top-level, so has no field name (or it’s empty, which is how it’s implemented in practice).

In the meta language the stored value is indented, e.g.
```
any value
    int                   42

any x
    double                3.1415

any y
    enum_t
        int index         1
        string[] choices  [Off, On]
```


For example a key value pair with key ColorMode and value storing an integer 0:
```
NTAttribute
    string name ColorMode
    any value
        int  0
```

### Regular Union fields

A regular variant union's introspection type consists of consists of
    - 1 or more fields
    - A type ID
Each field has
    - A name
    - An introspection type
Default type ID is "union" (usually default is used).
          
In the meta language we write the introspection type as
```
union
    <field1>
    ...
    <fieldN>
```    
So a regular union field is written
```
union <field-name>
    <field1>
    ...
    <fieldN>
```    
For example
```
union value
    int i
    double x
    time_t timeStamp
        long secondsPastEpoch
        int nanoseconds
        int userTag
```

A data field stores a field of the selected type.

In the meta language we write this as
```
<code>
union <field-name>
    <selected-field>
</code>
```
Data fields corresponding to above union field:
```
union value
    int i 42
union value
    double x 3.1415
union value
    time_t timeStamp
        long secondsPastEpoch 1460589140
        int nanoseconds       389605397
        int userTag           0 
```

## Structure Arrays

Structure Arrays

Structure array fields are used for arrays of the same structure.

The introspection type of a structure array is determined by the introspection type of the structure.

In the meta language we write the introspection type as
```
structure[]
     structure
         <field-list>
```
for the default type ID, or more generally
```
<type-id>[]
     <type-id>
         <field-list>
```


The data objects consist of 0 or more top-level structures

We write them like this
```
NTAttribute[] attribute
     NTAttribute
         string name ColorMode
         any value
             int 0
     NTAttribute
         string name SR-DI-DCCT-01
         any value
             double 300.1    
```


## Union Arrays

Union array fields are used for arrays of the same union - either an array of variant unions or an array of regular unions of the same type.

The introspection type of a union array is determined by the introspection type of the union.

In the meta language we write the introspection type as
```
union[]
     union
         <field-list>
```         
for the regular union arrays and
```
any[]
     any
```


Fields are written
```
union[] <field-name>
     union
         <field-list>
```         
for the regular union arrays and
```
any[] <field-name>
     any
```     
for variant unions.

For example
```
union[] value
    union
        int i
        double x
        time_t timeStamp
            long secondsPastEpoch
            int nanoseconds
            int userTag
```            
and
```
any[] value
     any      
```

The data objects consist of 0 or more top-level unions
```
union[] value
    union
        int i 42
    union value
        double x 3.1415
    union value
        time_t timeStamp
        long secondsPastEpoch 1460589140
        int nanoseconds       389605397
        int userTag           0
any[] value
    any
        int 42
    any
       double 3.1415
```                         