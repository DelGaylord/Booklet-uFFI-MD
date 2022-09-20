## Foreign Function Interface and Call-Outs
	instanceVariableNames: ''
	classVariableNames: ''
	package: 'FFITutorial'

FFITutorial class >> ticksSinceStart [
  ^ self ffiCall: #( uint clock() ) library: 'libc.so.6'
]
  ^ self ffiCall: #( uint clock() ) library: 'libc.dylib'
]
  ^ self ffiCall: #( uint clock() ) library: 'msvcrt.dll'
]
	^ self ffiCall: #( uint clock() ) library: 'libc.so.6'
]
  self platform isUnix
    ifTrue: [ ^ self ticksSinceStartUnix ].
  self platform isOSX
    ifTrue: [ ^ self ticksSinceStartOSX ].
  self platform isWindows
    ifTrue: [ ^ self ticksSinceStartWindows ].
  self error: 'Non-supported platform'
]

FFITutorial class >> ticksSinceStartUnix [
  ^ self ffiCall: #( uint clock() ) library: 'libc.so.6'
]

FFITutorial class >> ticksSinceStartOSX [
  ^ self ffiCall: #( uint clock() ) library: 'libc.dylib'
]

FFITutorial class >> ticksSinceStartWindows [
  ^ self ffiCall: #( uint clock() ) library: 'msvcrt.dll'
]
	instanceVariableNames: ''
	classVariableNames: ''
	package: 'UnifiedFFI-Libraries'

MyLibC >> unixModuleName [
	^ 'libc.so.6'
]

MyLibC >> macModuleName [
	^ 'libc.dylib'
]

MyLibC >> win32ModuleName [
	"While this is not a proper 'libc', MSVCRT has the functions we need here."
	^ 'msvcrt.dll'
]
	^ self ffiCall: #( uint clock() ) library: MyLibC
]
	^ '/usr/bin/libc.so.6'
]
		"On different flavors of Linux, the path to the library may differ, depending on the distro and whether the system is 32- or 64-bit."

		#(
			'/usr/lib/i386-linux-gnu/libcairo.so.2'
			'/usr/lib32/libcairo.so.2'
			'/usr/lib/libcairo.so.2' )
		do: [ :path |
			path asFileReference exists ifTrue: [ ^ path ] ].

		self error: 'Cannot locate Cairo library. Please check that it is installed on your system.'
]
	^ self ffiCall: #( uint time( NULL ) ) library: MyLibC
]
  ^ MyLibC
]

FFITutorial class >> ticksSinceStart [
	^ self ffiCall: #( uint clock() ) library: self myLibrary
]

FFITutorial class >> time [
	^ self ffiCall: #( uint time( NULL ) ) library: self myLibrary
]
  ^ MyLibC
]

FFITutorial class >> ticksSinceStart [
	^ self ffiCall: #( uint clock() )
]

FFITutorial class >> time [
	^ self ffiCall: #( uint time( NULL ) )
]
	^ self ffiCall: #( uint time( NULL ) )
]