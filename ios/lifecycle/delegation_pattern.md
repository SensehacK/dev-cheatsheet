

## Implementation

Protocol Declaration
```swift
protocol DeveloperEntryDelegate: AnyObject {
    func textDeveloperPlatform(_ text: String)
    func textDeveloperLanguage(_ text: String)
}
```

Applying in the Class

```swift
weak var delegate: DeveloperEntryDelegate?
```


```swift
class SecondViewController: UIViewController {
	weak var delegate: DeveloperEntryDelegate?
	
}
```


First class delegate callbacks

```swift
class FirstViewController: UIViewController {
      @IBOutlet weak var labelPlatformDetails: UILabel!
      @IBOutlet weak var labelDeveloperLanguage: UILabel!
      
      override func viewDidLoad() { super.viewDidLoad() }

	//MARK: - Navigation
	@IBAction func actionAddDetail(_ sender: UIButton) {
	   guard  let secondView = self.storyboard?.instantiateViewController(withIdentifier: "SecondViewController") as? SecondViewController else {   
	       fatalError("View Controller not found")}
	secondView.delegate = self //Protocol conformation here
	navigationController?.pushViewController(secondView, animated: true)
	}
}
	
//MARK: - Protocol Delegate Methods
extension FirstViewController: DeveloperEntryDelegate {
   func textDeveloperPlatform(_ text: String){
	  labelPlatformDetails.text = "Platform: \(text)" 
	}
	  
	func textDeveloperLanguage(_ text: String) {
		labelDeveloperLanguage.text = "Language: \(text)" 
	} 
}
```

## OS delegation implementation

[uitableview delegate](uitableview.md##Delegates)


