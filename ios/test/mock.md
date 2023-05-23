# Mock

## Intro

Mocking is required when you want to just create some test objects and their dependency on the test object itself.

It goes hand in hand with Stubs and Mocking.

I do feel like I still haven't grasp its actual understanding yet but I'm trying to learn as much as possible around Dependency injection via mocking or stubing.




You can specify Mocking certain objects or classes / structs because testing can't be done on them individually as a unit.
One case was related to `User Notifications` being not able to test in unit tests.


So if the Production class is defined like this.

// Implementation Production Classes
```swift

protocol CustomControllerType {

	var viewModel: CustomViewModelProtocol
	var rx: RxSwift.Reactive<Project.Custom.Controller> { .init(Custom.Controller() )}
	
	func configure(for session: Sessionable, viewModelType: CustomViewModelProtocol.Type)		
		
}

protocol CustomViewModelProtocol { 
	var Input init(context: Sessionable, customStorage: customMetadataStorageType, userDefaults: UserDefaults)
    var input: CustomViewModel.Input { get }
    var output: CustomViewModel.Output { get }
    var customCoordinator: RxCustomCoordinatorProtocol { get }
    var disposeBag: DisposeBag { get }
    
}

class ProductionProject.CustomViewModel : CustomViewModelProtocol {
    public let input: Input
    public let output: Output
	public let customCoordinator: RxCustomCoordinatorProtocol
	    
	public required init(context: Sessionable,
                         customStorage: customMetadataStorageType,
                         userDefaults: UserDefaults = .standard) {
                         
        self.customCoordinator = customCoordinator().rx
        let listSectionsDriver = Observable
		.create{ }.asDriver(onErrorJustReturn: [])

		self.input = Input(customTypeGlobalAction: PublishSubject<CustomActionType>().asObserver(),
       refreshAction: PublishSubject<Void>().asObserver(),
       shouldDisplaySomething: PublishSubject<Bool>.asObserver())


           
		self.output = Output(
		listSections: listSectionsDriver,
		customState: PublishSubject<CustomSection>().asDriver(),
		summaryMessage: .empty(),
		confirmCancel: .empty() )
    
    }
}

// MARK: • Input + Output

extension CustomViewModel {
    public struct Input {
        public let customTypeGlobalAction: AnyObserver<CustomActionType>
        public let refreshAction: AnyObserver<Void>
        public let shouldDisplaySomething: AnyObserver<Bool>
    }
    public struct Output {
        public let listSections: Driver<[CustomSection]>
        public let customState: Driver<CustomState>
        public let summaryMessage: Driver<String>
        public let confirmCancel: Signal<Void>
    }
}

// Defining Namespace
public enum Custom { }

public extension Custom {

    final class Controller: CustomControllerType {
	    var rx: Reactive<Custom.Controller> { .init(self) }	
		private(set) var viewModel: CustomViewModelProtocol

		init() {
			self.viewModel = CustomViewModel(context: Sessionable())
		}
		func configure(for session: Sessionable, viewModelType: CustomViewModelProtocol.Type) { 
		}
    }

}

```


Mock extension for mocking classes.
```swift

import RxSwift
import CustomViewModel



extension Mock { 

	class CustomController: CustomControllerType { 
	
		var viewModel: ProjectViewModel.CustomViewModelProtocol = Mock
		.CustomViewModel(
		context: SessionContext(),
		customStorage: Custom.Metadata.Storage(),
		userDefaults: .standard)

		var rx: RxSwift.Reactive<ProductionProject.Custom.Controller> { .init(Custom.Controller()) }
		
		func configure(session: ProductionProject.Sessionable,
		viewModelType: ProductionProject.CustomViewModelProtocol.Type) { }

	
	}
	
	
	class CustomViewModel: CustomViewModelProtocol {
		var input: ProductionProject.CustomViewModel.Input
		var output: ProductionProject.CustomViewModel.Output

		init(context: ProductionProject.Sessionable,
		customStorage: customMetadataStorageType, 
		userDefaults: UserDefaults) {
			
			input = ProductionProject
			.CustomViewModel
			.Input(customTypeGlobalAction: .empty(),
			       refreshAction: .empty(),
			       shouldDisplaySomething: .empty())
			
			
			output = ProductionProject
			.CustomViewModel
			.Output(listSections: .empty(),
					customState: .empty(),
					summaryMessage: .empty(),
					confirmCancel: .empty())
 
		}
	}


}

```


## Less JSON files

In order to effectively test better without adding more fluff, dependencies and assets you would need to carefully choose your objects or make them mutable or utilize `@testable` into the class/struct code.


MR feedback around unit tests from Jersh - Mentor
```text
i don't think we need to have multiple and nearly identical JSON structures. for the most part, dependencies can usually be built in the code without needing JSON. plus, relying on it and using this strategy won't scale very well because we'll potentially end up with hundreds or thousands of JSON files each with just a small variation in them. and at that point, we'll be spending as much time maintaining JSON files as we will writing actual code
```

## Manual Mocking

http://iosunittesting.com/manual-mocking-swift/


## Core Location Mocking

1.  Open Xcode.
    
2.  Choose Product > Test Plan > Edit Test Plan.
    
3.  In the test plan editor pane, choose Configuration.
    
4.  Under Localization, click Simulated Location and choose a location from the menu.

https://developer.apple.com/documentation/xcode/simulating-location-in-tests

https://rwhtechnology.com/blog/unit-test-cllocationmanager-with-mock/

## Resources

http://iosunittesting.com/
