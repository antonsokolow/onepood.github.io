---
title: Как привильно хранить Storyboard в git
post: layout
---

Не знаю как вам, а мне жутко не нравится формат файлов storyboards. Главная проблема в том, что git не отслеживает изменения и при командной работе это превращается в ад. Также мне не нравится создавать сиги и прописывать метод prepare для передачи данных между контроллерами.

Чтобы решить проблему, рекомендуется хранить какдый ViewController в отдельном Storyboard.

Создадим отдельный файл для нашего контроллера. Для удобства, добавим в него метод storyboardInstance:

```swift
import UIKit

class MyViewController: UIViewController {
    
    static func storyboardInstance() -> MyViewController? {
        let storyboard = UIStoryboard(name: String(describing: self), bundle: nil)
        return storyboard.instantiateInitialViewController() as? MyViewController
    }
    
    
}
```

Теперь созданим Storyboard, добавим ViewController и в качестве класса укажем наш MyViewController. Чтобы было совсем хорошо, назовите Storyboard также, как контроллер, в нашем случае MyViewController.

Для отображения контроллера на экране:

```swift
if let viewController = MyViewController.storyboardInstance() {
    viewController.someValue = someValue
    viewController.anotheCoolValue = anotheCoolValue
    viewController.property = property
    navigationController?.pushViewController(viewController, animated: true)
}
```

Чтобы вернуться в предыдущий контроллер:

```swift
if let nvc = navigationController {
    nvc.popViewController(animated: true)
} else {
    dismiss(animated: true, completion: nil)
}
```

Красота, не так ли? 