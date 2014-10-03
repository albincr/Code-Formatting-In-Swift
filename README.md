Code-Formatting-In-Swift
========================

Swift code formatting cheatshet.

**Jury is still out - please add an issue for discussion.**

# General rules

- Indentation by FOUR spaces (```␣␣␣␣```) instead of TAB (```⇥```)!  
*TAB can be problematic, spaces have always the same width.*

- Every block contents always indented.  
*WHY: Helps with reading/scanning by providing visual hint.

- First argument embedded in method name: ```openDoors(doors:```.  
*Adopted from Cocoa/ObjectiveC - can save a bit of space.*

- No additional lines if not explicitly stated otherwise.  
*The shorter file, the faster reading/scanning.*

- One empty line before ```return``` if there is more than one line in method.  
*Return is very important, should not be ommited by mistake.*

# Variables and constants

- One space after ```let``` / ```var```: ```let␣computerName```.  
*One space is enough.*

- Space before and after equal sign: ```computerName␣=␣"HAL9000"```.  
*To improve legibility.*

- One space between colon and type: ```versionNumber:␣Double```.  
*To improve legibility and differentiate from conformance colon.*

**Example:** 

```swift
let computerName = "HAL9000"   
let versionNumber: Double = 1
```

# Control operator: IF

- One empty line before every (including first in block) if: ```↵if```.  
*This operator is very important, should be extra visible.*

- One empty line after every (excluding last in block) if(else) block: ```if␣true␣{return}↵↵```.  
*This operator is very important, should be extra visible.*

- Use parenthesis only to improve legibility.  
*Only logical monstrosities need that special treatment.*

**Example:**

```swift
let someString = "toShowEmptyLine"

if computer.authenticateWithPassword("pass") {
    computer.openDoors("Some doors")
}

println("toShowEmptyLine")
```

# Control operator: SWITCH

- One empty line before every switch: ```↵switch```.  
*This operator is very important, should be extra visible.*

- One empty line after every switch block: ```switch variableName {↵ ... }↵↵```.  
*This operator is very important, should be extra visible.*

- Use parenthesis in ```case``` only to improve legibility.  
*Only logical monstrosities need that special treatment.*

- Indent (```␣␣␣␣```) every case section as it were block.  
*To improve legibility.*

**Example:**

```swift
println("flight: ")
var flightNumber = 110

switch flightNumber {
case 0..<110:
    println("is less than 110")
case 110:
    println("is 110")
default:
    println("some other")
}

println("end")
```

# Protocol declaration

- One space between method parameter name+colon and type: ```doors:␣String```.  
*To improve legibility and differentiate from conformance colon.*

- One space before and after return type arrow ```)␣->␣String```.  
*To improve legibility.*

- One space before opening bracket ```␣{```.  
*To improve legibility.*

**Example:**

```swift
protocol DoorOperator {
	func openDoors(doors: String) -> String
}
```

# Class declaration

- One space before and one after conformance colon: ```HAL9000␣:␣DoorOperator```.  
*To improve legibility and differentiate from other colon applications.*

- One space before opening bracket ```␣{```.  
*To improve legibility.*

- One blank line separation from properties declaration and methods.  
*To provide visual separation.*

- One blank line between methods declarations.  
*To provide visual separation.*

- Computed properties declarations shall be treated as methods.  
*They act like methods. Should be treated as just a special case.*

**Example:** 

```swift
class HAL9000 : DoorOperator {
    let debugDescription = "HAL9000"
    let softwareVersion = 2.1

    func openDoors(doors: String) -> String {
        return ("\(debugDescription) v\(softwareVersion): Affirmative. Opened \(doors).")
    }
}

class CurrentComputer : DoorOperator {
    private var computer: HAL9000!

    var debugDescription: String {
        get {
            let computerDescription = self.computer?.debugDescription
                                                   ?? "(no computer)"

            return "computer: \(computerDescription)"
        }
    }

    func authenticateWithPassword(pass: String) -> Bool {

        if pass != "pass" {
            return false
        }
        
        computer = HAL9000()

        return true
    }

    func openDoors(doors: String) -> String {

        if computer == nil {
            return "Access Denied. I'm afraid I can't do that."
        }
        
        return computer.openDoors(doors)
    }
}
```