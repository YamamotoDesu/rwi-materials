# Real-World iOS by Tutorials: Materials


This repo contains all the downloadable materials and projects associated with the **[Real-World iOS by Tutorials](https://www.raywenderlich.com/books/real-world-ios-by-tutorials)** from [raywenderlich.com](https://www.raywenderlich.com).

Each edition has its own branch, named `editions/[EDITION]`. The default branch for this repo is for the most recent edition.

## Forum

We’ve set up an official forum for the book at [https://forums.raywenderlich.com/c/books/real-world-ios-by-tutorials](https://forums.raywenderlich.com/c/books/real-world-ios-by-tutorials). This is a great place to ask questions about the book or to submit any errors you may find.

## Release History

| Branch                                                                            | Edition | Release Date |
| --------------------------------------------------------------------------------- |:-------:|:------------:|
| [editions/1.0](https://github.com/raywenderlich/rwi-materials/tree/editions/1.0) | 1.0     | 2022-04-20   |


## Preparing mock data for the animal model
```swift
// 1
private struct AnimalsMock: Codable {
  let animals: [Animal]
}

// 2
private func loadAnimals() -> [Animal] {
  guard let url = Bundle.main.url(
    forResource: "AnimalsMock",
    withExtension: "json"
  ), let data = try? Data(contentsOf: url) else { return [] }
  let decoder = JSONDecoder()
  // 3
  decoder.keyDecodingStrategy = .convertFromSnakeCase
  let jsonMock = try? decoder.decode(AnimalsMock.self, from: data)
  return jsonMock?.animals ?? []
}

// 4
extension Animal {
  static let mock = loadAnimals()
}
```

## async/await
Apple introduced async/await with iOS 15 in Swift, but with the release of Xcode 13.2, it’s also backward compatible starting with iOS 13. Swift now lets you write asynchronous code without using a completion handler. 

```swift
guard let url = URL(string: "<--some-url-->") else {
  return
}

// 1
let urlRequest = URLRequest(url: url)
// 2
Task {
  do {
    // 3
    let data = try await perform(urlRequest)
    // do operations on data
  } catch { // 4
      print(error.localizedDescription)
  }
}
```

If you were to write something similar with a completion handler, you would get something like this:
```swift
guard let url = URL(string: "<--some-url-->") else {
  return
}
let urlRequest = URLRequest(url: url)
perform(_ request: urlRequest) { response in
  switch response {
    case .success(let data):
      // do some operations on data
    case .failure(let error):
      print(error.localizedDescription)
  }
}

```


