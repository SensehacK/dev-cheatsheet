# Navigation Coordinator
## Intro

Having your view presentation and dismissal logic to different coordinators is pretty nice way of abstracting UI logic from the core functionalities of the app.

## WindowManager

Window Manager's sole job is to manage current View Hierarchy of the application.
To show more Views on top of current view or just present alerts. Or make dismissal of views via its functions.

It will take `ViewController` as one of its parameters in order to present those view controllers on the current stack.

Its responsibilities could also fallback on always providing some view which is interact-able for the end user and able to quickly recover from any state to a certain state which will not make the user be in locked zone. By locked zone I mean no UI interactions are possible and the only way out of this zone / screen / state is killing the app and relaunching it again. We don't want to serve our end users with this kind of user experience UX. 

```swift
class WindowManager: NSObject {
	let window: UIWindow

	var rootVC: UIViewController? {
        return window.rootViewController
    }

	var topVC: UIViewController? {
        return recursiveTopVC(window.rootViewController)
    }

	override init() {
	window = UIWindow(frame: UIScreen.main.bounds)
	super.init()
	}

	func setRoot(ViewController viewController: UIViewController) {
        window.rootViewController?.dismiss(animated: false)
        window.rootViewController = viewController
        window.makeKeyAndVisible()
    }

	func present(viewController: UIViewController) {
		viewController.modalPresentationStyle = .fullScreen
		if let presentedVC = rootVC?.presentedViewController {
			presentedVC.present(viewController, animated: true)
		} else {
			topVC?.present(viewController, animated: true)
		}
	}
}
```



## Navigation Context

This will host all of your views in the app and defining it as a enum case gives us performance boost and less mistakes if we just referencing in an array or numbers format. Having a name associated is very much readable and we still get the same performance boost as internally it is still referred as integer cases.

```swift
enum NavigationContext {
	case loginView(LoginContext)
	case homeView(HomeContext)
	case settingsView(SettingsContext)
	case customFeatureView(CustomFeatureContext)
	case signupView(SignUpContext)
}
```

## Example Context

```swift
struct LoginContext {
    let sessionCoordinator: SessionCoordinatorType
    let tokenDidExpire: Bool
    let successfulSignIn: AnyObserver<Void>

	init() {}
}
```
## View Controller Factory

```swift
enum ViewControllerFactory {

static func create(from navContext: NavigationContext) -> UIViewController {
	switch navContext {
	case .login(let loginContext):
		return LoginViewController(context: loginContext)
	case .MoreCases(let __):
		return ViewControllers()
	}
}

static func createMainViewController(context: GlobalContext) {
	let navigationController = UINavigationController(rootViewController: MainViewController(context: context))
	// Set delegates if needed
	navigationController.delegate
    return navigationController														  
	}
}
```

## Usage

So in one Rx - Reactive stream, you can trigger things by observing to `Publisher` | `Observable` and subscribing to those changeset.
So `AppLaunchObserver` is subscribing to those constant stream of changes.

Apple Combine or RxSwift | ReactiveX is a great option to utilize for solving these kind of builder pattern.
In this following code snippet we listen to notifier `AppLaunchObserver` , we create `LoginContext` object and map to `NavigationContext.login` which returns us `NavigationContext` enum which we further downstream to `ViewControllerFactory` create function which returns `ViewController`. In order to make the presentation logic back to `WindowManager` to do presenting of things.

```swift
AppLaunchObserver
	.map { _ in
		LoginContext(sessionCoordinator = init(),
					tokenDidExpire: false,
					successfulSignIn: .empty())
	}
	.map(NavigationContext.login)
	.observe(on: MainScheduler.instance)
	.do(onNext: { _ in
		doSomething() // Proper Side Effect
	})
	.map(ViewControllerFactory.create)
	.subscribeNext(weak: windowManager, WindowManager.present)
	.disposed(by: disposeBag)
```
