# UIView를 캡쳐하는 방법

카메라 화면에 이미지 캡쳐를 시도 시, 아래의 3가지 방법을 사용했었음

하지만, 3번만이 정상적으로 캡쳐가 가능했었음

### 1.
```Swift
extension UIView {
  func capture() -> UIImage? {
    UIGraphicsBeginImageContextWithOptions(self.bounds.size, false, 0.0)
    self.layer.render(in: UIGraphicsGetCurrentContext()!)
    let image = UIGraphicsGetImageFromCurrentImageContext()
    UIGraphicsEndImageContext()

    return image
  }
}
```


### 2.
```Swift
extension UIView {
  func capture() -> UIImage {
    let renderer = UIGraphicsImageRenderer(bounds: bounds)
    return renderer.image { rendererContext in
      layer.render(in: rendererContext.cgContext)
    }
  }
}
```


### 3.
```Swift
extension UIView {
  func capture() -> UIImage {
    let renderer = UIGraphicsImageRenderer(size: self.bounds.size)
    let image = renderer.image { context in
        self.drawHierarchy(in: self.bounds, afterScreenUpdates: true)
    }

    return image
  }
}
```

## 참고
https://www.robkerr.com/capture-uiview-as-jpeg

https://www.hackingwithswift.com/example-code/media/how-to-render-a-uiview-to-a-uiimage

https://stackoverflow.com/questions/30696307/how-to-convert-a-uiview-to-an-image

https://stackoverflow.com/questions/4334233/how-to-capture-uiview-to-uiimage-without-loss-of-quality-on-retina-display

