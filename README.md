![Weact](banner.png)

# Weact
[![Language: Swift 3](https://img.shields.io/badge/language-swift3-f48041.svg?style=flat)](https://developer.apple.com/swift)
![Platform: iOS 9+](https://img.shields.io/badge/platform-iOS%209%2B-blue.svg?style=flat) [![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage) <!-- [![Cocoapods compatible](https://img.shields.io/badge/Cocoapods-compatible-4BC51D.svg?style=flat)](https://cocoapods.org) -->
<!-- [![Build Status](https://www.bitrise.io/app/2c01c6f861c526d9.svg?token=H26l2Nish0WWF6yfDTL1kA&branch=master)](https://www.bitrise.io/app/2c01c6f861c526d9) put bakc once on bitrise -->
<!-- [![codebeat badge](https://codebeat.co/badges/768d3017-1e65-47e0-b287-afcb8954a1da)](https://codebeat.co/projects/github-com-s4cha-weact) put back once open source-->[![License: MIT](http://img.shields.io/badge/license-MIT-lightgrey.svg?style=flat)](https://github.com/freshOS/then/blob/master/LICENSE)
[![Release version](https://img.shields.io/badge/release-0.1-blue.svg)]()

Weact = Swift + React

```swift
func render() -> Node {
    return Label("Hello, Component !")
}
```
Weact is a Swift framework for building component-oriented interfaces.

[Facebook's React guide](https://facebook.github.io/react/) is an incredible documentation to get familiar with the concept.


|      | Weact                                   |
| ---- | ---------------------------------------- |
|  🔶  | Pure **Swift** (no JS, no XML)           |
|  🏗    | Can be used **Incrementally** |
|   📐  |Can use **Autolayout or any autolayout** lib for the layout (we like [Stevia](https://github.com/freshOS/Stevia)) |
| 💉 | Supports **Hot Reload** with [💉 injectionForXcode](http://johnholdsworth.com/injection.html)|

Because you don't need javascript to enjoy Components!

## A Bare Component

A component is pretty simple :
- It has a `render` function that returns a `Node`.
- It has a `state` property.

That's All!

```swift
import Weact

class MyFirstComponent: Component {

    var state = MyState()

    func render() -> Node {
        return Label("Hello!")
    }
}
```

## View Controller Component
To use a component as a `UIViewController` and play nicely with UIKit apis, just subclass
`UIViewController` and call  `loadComponent` in `loadView` :)

```swift
class LoadingScreen: UIViewController, Component {

    // Just call `loadComponent` in loadView :)
    override func loadView() { loadComponent() }

    func render() -> Node {
        return ...
    }
}

```

## View Component
To use a component as a `UIView` and play nicely with UIKit apis, just subclass
`UIView` and call  `loadComponent` in an `init` function :)
```swift
class MyCoolButton: UIView, Component {

    // Here we load the component
    convenience init() {
        self.init(frame:CGRect.zero)
        loadComponent()
    }

    func render() -> Node {
        return ...
    }
}

```

## View-Wrapped Component
Display your component in a UIView and use it wherever You want!
```swift
let view = ComponentView(component: MyComponent())
```
## ViewController-Wrapped Component
Embbed your component in view Controller and present it anyway you want :)
```swift
let vc = ComponentVC(component: MyComponent())
```
## Looping !

```swift
func render() -> Node {
    let items = ["Hello", "How", "Are", "You?"]
    return
        View(style: { $0.backgroundColor = .white }, [
            VerticalStack(style: { $0.spacing = 40 }, layout: { $0.centerInContainer() },
                items.map { Label($0) }
            )
        ])
}
```

## Example:  A Loading Screen

```swift
import UIKit
import Stevia
import Weact

class LoadingScreen: UIViewController, Component {

    var state = true // no state

    // Just call `loadComponent` in loadView :)
    override func loadView() { loadComponent() }

    func render() -> Node {
        return
            View(
                style: { $0.backgroundColor = .gray }, [
                HorizontalStack(
                    style: { $0.spacing = 8 },
                    layout: { $0.centerInContainer() }, [
                    Label("Loading...",
                        style: { $0.textColor = .white }
                    ),
                    ActivityIndicatorView(.white,
                        style: { $0.startAnimating() }
                    )
                ])
            ])
    }
}
```

## Inspiration
[Facebook's React](https://facebook.github.io/react/), [ComponentKit](https://github.com/facebook/componentkit),
[Preact](https://github.com/developit/preact), [Vue.js](https://vuejs.org) AlexDrone's render, Angular...
Pure Swift React/ ComponentKit implementation

## Other great Swift libraries
[Alexdrone's render](https://github.com/alexdrone/Render)

[BendingSpoons' katana](https://github.com/BendingSpoons/katana-swift)
