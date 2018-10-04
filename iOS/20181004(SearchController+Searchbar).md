# 2018/10/04
## Searchbar in Navigationbar(네비게이션바에 서치바 넣기)
### 순서
- SearchVC-SearchResultVC 설정
- Searchbar의 Placeholder 설정
- Searchbar의 Color 설정
- Searchbar의 Icon 편집

#### #1. SearchVC-SearchResultVC 설정
1. SearchVC 생성 및 스토리보드상 원하는 SearchResultVC 구현
2. SearchVC 내 SearchVC 변수 선언 Ex) ``private var searchVC: UISearchController!``
3. ``viewDidLoad()``함수 내 코드 \**나는 ``setSearchViewController()``함수로 뺐다.*
  ```
  guard let searchResultVC = storyboard?.instantiateViewController(withIdentifier: "SearchResultVC") as? SearchResultViewController else { return }
  searchVC = UISearchController(searchResultsController: searchResultVC)
  searchVC.delegate = self
  searchVC.searchResultsUpdater = searchResultVC
  searchVC.dimsBackgroundDuringPresentation = true
  definesPresentationContext = true
  searchVC.loadViewIfNeeded()
  searchVC.searchBar.delegate = searchResultVC
  searchVC.hidesNavigationBarDuringPresentation = false
  // 서치바 관련 폰트와 색상 관련 설정을 마친 후
  navigationItem.titleView = searchVC.searchBar
  ```
  - **TMI** : 기존 DrinKit이라는 개인앱에서 SearchBar를 구현해봤으나, UIView를 생성해 추가했었다. Navigationbar에 SearchBar를 넣는 작업은 StoryBoard상에서 찾아봤지만, 바로 구현하기에는 어려움이 있었다.
  - 고로, 위 코드에서 내가 가장 알고자 했던 코드 : **navigationItem.titleView = searchVC.searchBar**

### #2. Searchbar의 Placeholder 설정
  - PlaceHolder의 기본 폰트와 색상 설정
  ```
  let defaultTextAttribs = [
      NSAttributedString.Key.font: customFont(UIFont),
      NSAttributedString.Key.foregroundColor: customColor(UIColor)
  ]
  ```
  - 적용방법 1
  ```
  searchVC.searchBar.placeholder = "Texts yon want!"
  UITextField.appearance(whenContainedInInstancesOf: [UISearchBar.self]).defaultTextAttributes = defaultTextAttribs
  ```
  - 적용방법 2
  ```
  let attributedPlaceholder: NSAttributedString = NSAttributedString(string: "Search", attributes: defaultTextAttribs)
  let textFieldPlaceHolder = searchBarCustom.valueForKey("searchField") as? UITextField
  textFieldPlaceHolder?.attributedPlaceholder = attributedPlaceholder
  ```
  - **TMI** : 두 방법이 별 차이는 없을 거라 생각했지만, 적용방법 2에서 ``let textFieldPlaceHolder = searchBarCustom.valueForKey("searchField") as? UITextField``이 코드는 나중에 찾기 어려웠던 SearchBar의 내부 배경색상을 설정하는데 쓰였다.

### #3. Searchbar의 Color 설정
  - SearchBar의 TextField backgroundColor 설정
    ```
    let textfield = searchVC.searchBar.value(forKey: "searchField") as? UITextField
    textfield?.backgroundColor = UIColor.white
    ```
  - tintColor 설정
    ```
    searchVC.searchBar.tintColor = UIColor.white
    ```
  - TMI : SearchBar의 TextFiel BackgroundColor 설정하는 법을 찾는게 이상하게 오래 걸렸음. 주르륵.

### #4. SearchBar의 Icon 편집
  - SearchBar의 Cancel버튼 Text 바꾸기
    ```
    UIBarButtonItem.appearance(whenContainedInInstancesOf: [UISearchBar.self]).title = "Text"
    ```
  - SearchBar Icon 위치 바꾸기 (기존 왼쪽에서 오른쪽으로 바꾸고, 아이콘 이미지 바꾸기)
    ```
    if let searchTextField:UITextField = searchVC.searchBar.subviews.first?.subviews.last as? UITextField {
        searchTextField.leftView = nil
        searchTextField.rightView = UIImageView(image: UIImage(named: "custom"))
        searchTextField.rightViewMode = .always
    }
    ```
  - **TMI** : ``SearchTextField:UITextField = searchVC.searchBar.subviews.first?.subviews.last``가 TextField이고, leftView,rightView가 있었을 줄은 정말 몰랐다. rightViewMode까지.. 구현하고 나서 신기해서 놀랐던 코드

### 참조
- https://iosdevcenters.blogspot.com/2016/07/hacking-uisearchbar-in-swift.html
