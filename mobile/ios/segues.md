# Segues

## iOS Segues

### Creation

Segues can be created programmatically and Storyboard You can name your segue with an identifier so that it would be easier to differentiate which segue has been instantiated in “prepareForSegue” segue life cycle method.

### Modally

iOS 13 brings in the new method of adding the default card presentation. So it doesn’t fully overtakes the screen. Hence we may need to switch our Segue Kind to “Present Modally” Presentation: “Full Screen”

[SO Link](https://stackoverflow.com/questions/56435510/presenting-modal-in-ios-13-fullscreen)

### Storyboard

#### With Identifier

```swift
let onboardStoryboard = UIStoryboard(name: "CustomViewController", bundle: nil)
let viewC = onboardStoryboard.instantiateViewController(identifier: "CustomViewController")
viewC.modalPresentationStyle = .fullScreen
self.present(viewC, animated: true)
```

#### Without Identifier

Set View with Initial View controller of Storyboard to avoid having duplicate assigning the Storyboard Identifier.

```swift
let barChartStoryboard = UIStoryboard(name: "BarChart", bundle: nil)
let barChartVC = barChartStoryboard.instantiateInitialViewController()
barChartVC?.modalPresentationStyle = .fullScreen
if let barchart = barChartVC {
    self.present(barchart, animated: true)
}
```

### Data Passing

#### Parent - Child VC Observation

Funny enough when I put a debugger here both the following commands gets executed with perfect valid "Kautilya 2/3" strings I believe with debugger it creates/invokes the child VC just before executing this line. So in normal instance if the destination VC isn't properly invoked these values won't be changed. Better approach is to pass a whole object and then in ViewDidLoad method of childVC class initialization code should be ran.

```swift
// Parent VC
if segue.identifier == "SummaryChildSegue" {
    print("Showing Summary Child Segue")
    // Object data passing to child view controller

    if let destVC = (segue.destination as? SummaryChildVC) {
        print("In segue destination")
        destVC.titleObj  = "Kautilya"
        } }
```

> destVC.titleLabel.text = "Kautilya 3" This outright crashes as titleLabel still hasn't been invoked in Child VC destVC.titleLabel?.text = "Kautilya 2" This doesn't crash as it looks for an optional value and it doesn't find it so text assignment is not done

Child View Controller

```swift
// Child Destination VC
class SummaryChildVC: UIViewController {
    @IBOutlet weak var titleLabel: UILabel!

    var titleObj: String?
    override func viewDidLoad() {
        super.viewDidLoad()
        titleLabel.text = titleObj ?? "Summary"
  } }
```

