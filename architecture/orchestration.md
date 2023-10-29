# Orchestration 

## Intro

This could be where you fire off all the main things of the app.
This could be a Coordinator, Mission Control, Global Manager, Mastermind, Architect of your app.


## Singletons

I know this pattern is always hated by lot of communities and its the most unrecommended for many reasons. But like everthing, there is no right or wrong with any pattern. Just knowing each limitation could make you a better engineer when using certain design pattern.
[singleton_pattern](singleton_pattern.md)

I prefer Singleton pattern for long live objects of the app. This could be your analytics, databaseManager, NetworkManager, SessionManager, AppNavigation Coordinator, Global NotificationManager.

```swift
final class Orchestrator {
	// Managers
	lazy var windowManager: WindowManager = WindowManager()
	let environment: Environment = EnvironmentConfig()
	let appConfiguration: AppConfig = AppConfig()
	let sessionCoordinator: SessionCoordinatorType
	let appTheme: ThemeControllerType = ThemeController()

	// Private instances
	private let disposeBag = DisposeBag()

	init(sessionCoordinator: SessionCoordinatorType = .init()) {
		self.sessionCoordinator = sessionCoordinator
		
		// Rx app life cycle hooks.
		UIApplication.rx.didFinishLaunching
		.mapToVoid()
		.subscribeNext(weak: self, Orchestrator.initiateConductor)
	    .disposed(by: disposeBag)
	}

	
}
```

This could be mapped as `Final` since we are not initializing it more than once and it would be always invoked once for the whole app lifecycle. So marking it final would give us better optimization as well from Swift llvm.

## Initiate Listeners


```swift
func initiateConductor {
	AnalyticsLogger.configure()
	CacheManager.shared.configure()
}
```


## Analytics

```swift
public class AnalyticsLogger: Logger {
	public static func configure() { Analytics.configure() }
}
```
[analytics](analytics.md)


## Configuration

You can read more about this in my [app_configuration](app_configuration.md) file in `iOS/Config` folder.

You can also configure your environment of the app to behave using different schemes or have explicit `xcConfig` files to read values from to properly switch network subdomains accordingly.
[app_environment](app_environment.md)

## Window Coordinator

This could be instantiated in the app lifecycle to take over the coordination of View presentation logic and keep loosely coupled with other components. We also avoid polluting our `Views`, `ViewControllers` to handle window manager presentation, dismissal, ViewBuilder responsibilities for the app.
Thus making our App internal navigation API more streamlined.

[navigation_coordinator](navigation_coordinator.md)


## Cache Manager

```swift
class CacheManager {
	static let shared = CacheManager()
}
```

[cache](ios/lifecycle/cache.md)

## Database Manager

Having default initialization for database manager is also important when trying to make all the resource connections with the backend database. Most of the time it needs to be initialize on app launch in order to perform most of the dependent things for retrieving old information.

[database](database.md)