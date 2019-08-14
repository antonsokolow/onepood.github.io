---
title: Navigation in SwiftUI
post: layout
---

Навигация в *SwiftUI*.

#### A Master/Detail Navigation

```swift
struct ContentView: View {
    private let items = [
        "Wardrobe", "Dresser", "Sofa"
    ]

    var body: some View {
        NavigationView {
            List(items, id: \.self) { item in
                NavigationLink(destination: DetailView(item: item)) {
                    Text(item)
                }
            }.navigationBarTitle("My Stuff")
        }
    }
}

struct DetailView: View {
    let title: String

    var body: some View {
            Text(title)
                .font(.largeTitle)
    }
}
```

#### Programmatic navigation

```swift
import SwiftUI

struct ContentView : View {
    @State var selection: Int? = nil
    
    var body: some View {
        NavigationView {
            VStack {
                NavigationLink(destination: DetailView(param: selection ?? 0), tag: 1, selection: $selection) {
                    Button("Go") {
                        self.selection = 1
                    }
                }
            }
        }
    }
}

struct DetailView: View {
    let param: Int

    var body: some View {
        HStack {
            Text("DetailView: \(param)")
            .font(.largeTitle)
        }
    }
}
```