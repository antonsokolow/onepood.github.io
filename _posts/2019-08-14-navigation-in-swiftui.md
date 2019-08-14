---
title: Navigation in SwiftUI
post: layout
---

Смена окон с помощью *NavigationLink* и программым путем в *SwiftUI*.

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
