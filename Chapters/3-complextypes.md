## Complex Types
  instanceVariableNames: ''
  classVariableNames: 'Age'
	package: 'FFITutorial'
  
FFITutorial class >> initialize
  Age := #uint
	^ self ffiCall: #( Age abs ( Age n ) )
]
  instanceVariableNames: ''
  classVariableNames: 'Age'
	package: 'FFITutorial'
  
FFITutorialTypes class >> initialize
  Age := #uint
  ...
  poolDictionaries: 'FFITutorialTypes'
  ...
anArray at: 1 put: 3.1415.
anArray at: 5 put: 42.
anArray at: 7 put: 'Hello World'.

anArray.
 => #(3.1415 nil nil nil 42 nil 'Hello World')

anArray at: 2
 => Out of Bounds Exception!
array := FFIArray newType: #char size: 10.

"In the C heap"
array := FFIArray externalNewType: #char size: 10.
array at: n "for the nth element".

"In Pharo heap"
newArrayOf128Chars := char128Type new.

"In C heap"
newArrayOf128Chars := char128Type externalNew.
{
	int numerator;
	int denominator;
} fraction;

double fraction_to_double(fraction* a_fraction){
  return a_fraction -> numerator / (double)(a_fraction -> denominator);
}
	instanceVariableNames: ''
	classVariableNames: ''
	package: 'FFITutorial'

FractionStructure class >> fieldsDesc [
	^ #(
		int numerator;
		int denominator;
		)
]

FractionStructure rebuildFieldAccessors.
	instanceVariableNames: ''
	classVariableNames: 'OFFSET_DENOMINATOR OFFSET_NUMERATOR'
	package: 'FFITutorial'

FractionStructure >> denominator [
	"This method was automatically generated"
	^handle signedLongAt: OFFSET_DENOMINATOR
]

FractionStructure >> denominator: anObject [
	"This method was automatically generated"
	handle signedLongAt: OFFSET_DENOMINATOR put: anObject
]

FractionStructure >> numerator [
	"This method was automatically generated"
	^handle signedLongAt: OFFSET_NUMERATOR
]

FractionStructure >> numerator: anObject [
	"This method was automatically generated"
	handle signedLongAt: OFFSET_NUMERATOR put: anObject
]
aFraction := FractionStructure new.

"In C heap"
aFraction := FractionStructure externalNew.
aFraction denominator: 7.
  ^ self ffiCall: #(double fraction_to_double(FractionStructure* a_fraction))
]

FFITutorial new fractionToDouble: aFraction.
>>> 5.714285714285714
int print_by_copy(fraction a_fraction_copy);

...

fraction f;

//The function below requires a copy, so just send f, the compiler takes care
print_by_copy(f);

//The function below requires a pointer, so dereference f
print_by_pointer(&f);
  ^ self ffiCall: #(int print_by_pointer(FractionStructure* a_fraction))
]

FFITutorial >> printByCopy: aFraction [
  ^ self ffiCall: #(int print_by_copy(FractionStructure a_fraction))
]
aFraction := FractionStructure externalNew.

aFraction numerator: 40.
aFraction denominator: 7.

"Both of these work"
FFITutorial new printByPointer: aFraction.
FFITutorial new printByCopy: aFraction.
	int some_array[4];
}
  int4array := FFIArray newArrayType: #int size: 4.
]
  
FFIStructure subclass: #EmbeddingArrayStructure
  instanceVariableNames: ''
  classVariableNames: ''
  poolDictionaries: 'FFITutorialTypes'
  package: 'FFITutorial'
  
EmbeddingArrayStructure class >> fieldsDesc [
  ^ #(
  int4array some_array;
  )
]

EmbeddingArrayStructure rebuildFieldAccessors.
struct {
  char a;
  int b;
}

// The compiler defines
struct {
  char a;
  char padding1[3];
  int b;
}
instanceVariableNames: ''
  classVariableNames: ''
  package: 'FFITutorial'

AlignmentExampleStructure class >> fieldsDesc [
  ^ #(
  	char a;
  	int b;
  	)
]

AlignmentExampleStructure rebuildFieldAccessors.
>>> 1
AlignmentExampleStructure classPool at: #OFFSET_B.
>>> 5
#pragma pack(1)     /* set alignment to 1 byte boundary */

struct {
  char a;
  int b;
}

#pragma pack(pop)   /* restore original alignment from stack */
  char a;
  int b __attribute__((packed));
}
instanceVariableNames: ''
  classVariableNames: ''
  package: 'FFITutorial'

PackedAlignmentExampleStructure class >> fieldsDesc [
  ^ #(
  	char a;
  	int b;
  	)
]

PackedAlignmentExampleStructure rebuildFieldAccessors.
>>> 1
PackedAlignmentExampleStructure classPool at: #OFFSET_B.
>>> 2
  goalkeeper,
  defender,
  midfielder,
  forward
} position;
  goalkeeper = 42,
  defender,
  midfielder,
  forward
} position;
#include <limits.h>

enum example {
    example0,            /* will have value 0 */
    example1,            /* will have value 1 */
    example2 = 3,        /* will have value 3 */
    example3 = 3,        /* will have value 3 */
    example4,            /* will have value 4 */
    example5 = INT_MAX,  /* will have value INT_MAX */
    /* Defining a new value after this one will cause an overflow error */
};
  instanceVariableNames: ''
  classVariableNames: ''
  package: 'FFITutorial'

ExampleEnumeration class >> enumDecl [
	^ #(
    example0 0
    example1 1
    example2 3
    example3 3
    example4 4
    example5 2147483647
		)
]

ExampleEnumeration initialize.
  instanceVariableNames: ''
  classVariableNames: 'example0 example1 example2 example3 example4 example5'
  package: 'FFITutorial'
  ...
  poolDictionaries: 'ExampleEnumeration'
  ...
  float as_float;
  int as_int;
} float_or_int;

float_or_int number;
number.as_float = 3.14f;

printf("Integer representation of PI: %d\n", number.as_int);
	instanceVariableNames: ''
	classVariableNames: ''
	package: 'FFITutorial'

FloatOrIntUnion class >> fieldsDesc [
	^ #(
		float as_float;
		int as_int;
		)
]

FloatOrIntUnion rebuildFieldAccessors.
	instanceVariableNames: ''
	classVariableNames: 'OFFSET_DENOMINATOR OFFSET_NUMERATOR'
	package: 'FFITutorial'

FloatOrIntUnion >> as_float [
	"This method was automatically generated"
	^handle floatAt: 1
]

FloatOrIntUnion >> as_float: anObject [
	"This method was automatically generated"
	handle floatAt: 1 put: anObject
]

FloatOrIntUnion >> as_int [
	"This method was automatically generated"
	^handle signedLongAt: 1
]

FloatOrIntUnion >> as_int: anObject [
	"This method was automatically generated"
	handle signedLongAt: 1 put: anObject
]
aFloatOrInt := FloatOrIntUnion new.

"In C heap"
aFloatOrInt := FloatOrIntUnion externalNew.
foi as_int.
>>> 1078523331
  ^ self ffiCall: #(char float_or_int_first_byte(FloatOrIntUnion* float_or_union))
]