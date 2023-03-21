

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





